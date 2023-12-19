# Як наладзіць Eclipse® для праграмавання і кроскампіляцыі для AXC F 2152 на Ubuntu 18.04 LTS #
> [!TIP]
> English version is [here](./readme.md).

> Гэта кіраўніцтва працуе толькі для прашыўкі AXC F 2152 версіі 2021.9. Для іншых прылад або версій фрэймворкаў сцягі зборкі адрозніваюцца і могуць змяняцца ў залежнасці ад версіі.

## 1. Усталяванне **Eclipse®** IDE ##

1. Праверце, ці ўсталявана ўжо **JRE**. Рэкамендуецца апошняя версія **Java SE**::

```sh
java -version
```

![java version](images/java_-version.png)

Калі не ўсталявана, ўсталюйце **OpenJdk**:

```sh
sudo apt-get install openjdk-11-jre
```

Пасля гэтага, рэзультат праверкі павінен выглядаць так:

![java version ok](images/java_-version_ok.png)

2. Каб усталяваць **Eclipse IDE for C/C++ Developers** наведайце https://www.eclipse.org/downloads/packages/
, выбраць і запампаваць адпаведны пакет:

![eclipse package](images/eclipse_package.png)

Або выкарыстайце wget для запампоўкі **2021‑9 R** версіі (ёсць рызыка, што яна зменіцца):

```sh
wget -P ~/Downloads 
https://www.eclipse.org/downloads/download.php?file=/technology/epp/downloads/release/2021-09/R/eclipse-cpp-2021-09-R-linux-gtk-x86_64.tar.gz
```
Пераканайцеся, што вы спампавалі правільную версію і загрузка прайшла паспяхова.

Распакуйце „eclipse-cpp-2021-09-R-linux-gtk-x86_64.tar.gz“:

```sh
cd ~/Downloads
tar -xzf eclipse-cpp-2021-09-R-linux-gtk-x86_64.tar.gz
```

> **Падказка:** Перамясціце распакаваную тэчку ў */opt*. Тэчка **Opt**ional звычайна для праграм, якія не ўсталёўваюцца праз пакетны мэнаджар, і ў адрозненне ад галоўнай тэчкі, яна даступная любому карыстальніку сістэмы.
>
> \> sudo mv eclipse /opt/

Стварыце праграму запуску Eclipse на працоўным стале:
```sh
sudo nano /usr/share/applications/eclipse.desktop
```

Скапіюйце наступны код у файл працоўнага стала:

```sh
[Desktop Entry]
Name=Eclipse
Type=Application
Exec=/opt/eclipse/eclipse
Terminal=false
Icon=/opt/eclipse/icon.xpm
Comment=Integrated Development Environment
NoDisplay=false
Categories=Development;IDE
Name[en]=eclipse.desktop
```

Стварыце сімвалічную спасылку, каб зрабіць Eclipse даступным з кансолі:

```sh
cd /usr/local/bin
sudo ln -s /opt/eclipse/eclipse
```

**Eclipse** зараз гатовы да выкарыстання.

## 2. Усталяванне Toolchain ##

Спампуйце неабходны Toolchain з вэб-сайта Phoenix Contact.

[LINK](https://www.phoenixcontact.com/online/portal/pi?uri=pxc-oc-itemdetail:pid=2404267&library=piru&tab=5&requestType=qr&productId=2404267#softw)

Перайдзіце ў тэчку, дзе знаходзіцца ваш Toolchain.

Усталяванне Toolchain:

```sh
chmod +x ./pxc-glibc-x86_64-axcf2152-image-sdk-cortexa9t2hf-neon-toolchain-2021.9.sh
./pxc-glibc-x86_64-axcf2152-image-sdk-cortexa9t2hf-neon-toolchain-2021.9.sh
```
Укажыце шлях усталёўкі:

>/opt/pxc/sdk/AXCF2152/2021.9

**Заўвага**:
PLCnext Technology SDK розных версій могуць выкарыстоўвацца адначасова.
Каб пазбегнуць такога выкарыстання, Phoenix Contact
рэкамендуе выдаліць усе старыя SDK.

## 3. Наладзьце Eclipse® IDE для выкарыстання ўсталяванага PLCnext SDK ##

Устанавіць перакрыжаваныя налады праекта (прэфікс і шлях):

>arm-pxc-linux-gnueabi-  
>/opt/pxc/sdk/AXCF2152/2021.9/sysroots/x86_64-pokysdk-linux/usr/bin/arm-pxc-linux-gnueabi

![SDK ok](images/cdt_cross_settings.png)

Задаць налады дыялекту кампілятара G++ для кроспраекта:

>-march=armv7-a -mthumb -mfpu=neon -mfloat-abi=hard -mcpu=cortex-a9 --sysroot=/opt/pxc/sdk/AXCF2152/2021.9/sysroots/cortexa9t2hf-neon-pxc-linux-gnueabi -fno-gnu-unique

![SDK ok](images/cdt_dialect_flags.png)

Задаць прэпрацэсарныя азначэнні G++ для кроспраекта:

>ARP_DEVICE_AXCF2152

![SDK ok](images/cdt_defines.png)

Задаць шляхі ўключэння прэпрацэсара G++ для крос‑праекта:

>/opt/pxc/sdk/AXCF2152/2021.9/sysroots/cortexa9t2hf-neon-pxc-linux-gnueabi/usr/include/plcnext

![SDK ok](images/cdt_includes.png)

Задаць сцягі кампаноўніка G++ для кроспраекта:

>--sysroot=/opt/pxc/sdk/AXCF2152/2021.9/sysroots/cortexa9t2hf-neon-pxc-linux-gnueabi -march=armv7-a -mthumb -mfpu=neon -mfloat-abi=hard -mcpu=cortex-a9 -Wl,--no-undefined

![SDK ok](images/cdt_cross_linker_settings.png)

Пасля завяршэння ўсіх налад запусціце праект і, калі ёсць памылкі, трэба прайсці ўсе папярэднія крокі
і праверыць напісанне каманд.
