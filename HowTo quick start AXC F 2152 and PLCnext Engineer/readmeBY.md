#  Як пачаць працу з **AXC F 2152** і **PLCnext Engineer** #
> [!TIP]
> English version is [here](./readme.md).

## Змест ##
1. [Падключэнне кантролера](#Падключэнне-кантролера)  
2. [Абнаўленне прашыўкі кантролера](#Абнаўленне-прашыўкі-кантролера)
3. [Стварэнне праекта PLCnext Engineer](#Стварэнне-праекта-PLCnext-Engineer)  
4. [Налада праекта PLCnext Engineer](#Налада-праекта-PLCnext-Engineer)  
4.1 [Агульная налада праекта](#Агульная-налада-праекта)  
4.2 [Налада сеткавых налад кантролера](#Налада-сеткавых-налад-кантролера)  
4.3 [Падключэнне да кантролера](#Падключэнне-да-кантролера)  
4.4 [Змена пароля](#Змена-пароля)  


## Падключэнне кантролера ##
Падключыце кантролер з дапамогай USB-Ethernet пераходніка:

<p align="center"> <img src="images/usb_ethernet_hub.png"> </p>
<p align="center"> Малюнак 1. USB-Ethernet пераходнік</p>

З дапамогай браўзера адкрыйце адрас кантролера па змаўчанні [https://192.168.1.10](https://192.168.1.10):

<p align="center"> <img src="images/welcome_screen.png"> </p>
<p align="center"> Малюнак 2. Прывітальны экран</p>

## Абнаўленне прашыўкі кантролера ##

Апошняя версія прашыўкі знаходзіцца [тут](https://www.phoenixcontact.com/en-pc/products/controller-axc-f-2152-2404267#firmware-link-target).

Каб абнавіць прашыўку кантролера, выканайце наступныя дзеянні:

- Спампуйце файл прашыўкі *.zip версіі **2021.0.5 LTS** на сайце Phoenix Contact [сайт](https://www.phoenixcontact.com/en-pc/products/controller-axc-f-2152-2404267#firmware-link-target:~:text=AXC_F_2152_FW2021_0_5_Bundle.zip&prodid=2404267&lang=en&debug=0&refer=https%3a%2f%2fselect%2ephoenixcontact%2ecom%2fphoenix%2fdwl%2fdwlgwisrev01%2ejsp%3flanguage%3den%26prodid%3d2404267%26lang%3den%26pxc_s%3dy%26pxc_env%3dp_e&intCount=1&hwv=04 ).

- Распакуйце файл прашыўкі *.zip (па змаўчанні прапанаваны Windows каталог прызначэння — `%USERPROFILE%\Downloads\AXC_F_2152_FW2021_0_5_Bundle`).
  Файл абнаўлення (*.raucb) і PDF-файлы з інфармацыяй пра прыладу будуць распакаваны ў выбраны каталог прызначэння.

- Адкрыйце браўзер, а затым перайдзіце на старонку вэб-кіравання (WBM) [https://192.168.1.10/wbm](https://192.168.1.10/wbm):

<p align="center"> <img src="images/login_screen.png"> </p>
<p align="center"> Малюнак 3. Экран уваходу</p>

- Увайдзіце ў сістэму як адміністратар.

Наступныя дадзеныя доступу ўстаноўлены па змаўчанні:
```
Username: admin
Password: Надрукавана на кантролеры (гл. малюнак 4).
```
Наступныя дадзеныя доступу ўстаноўлены па змаўчанні:

<p align="center"> <img src="images/password_placement.png"> </p>
<p align="center"> Малюнак 4. Месцазнаходжанне пароля </p>

- Каб пачаць абнаўленне прашыўкі, перайдзіце ў раздзел **`"Administration"`** - **`"Firmware update"`**:
<p align="center"> <img src="images/firmware_update_screen.png"> </p>
<p align="center"> Малюнак 5. Абнаўленне прашыўкі</p>

Вам трэба выбраць файл абнаўлення. Месцазнаходжанне па змаўчанні:
```
%USERPROFILE%\Downloads\AXC_F_2152_FW2021_0_5_Bundle\axcf2152-2021.0.5.35585-LTS.raucb
```
Абнаўленне гатова да ўсталёўкі:

<p align="center"> <img src="images/ready_update_screen.png"> </p>
<p align="center"> Малюнак 6. Абнаўленне прашыўкі</p>

Пачніце абнаўленне, націснуўшы кнопку **`"Start Update"`**. Прашыўка будзе абноўлена, і на вэб-старонцы будзе паказаны працэс абнаўлення. Падчас абнаўлення прашыўкі святлодыёд RUN пачынае міргаць, а потым спыняецца.
Пасля гэтага кантролер перазапускаецца. Пасля поўнай ініцыялізацыі кантролера святлодыёд RUN загараецца пастаянна.
## Стварэнне праекта PLCnext Engineer ##

Важна выкарыстоўваць адпаведную версію **`"PLCnext Engineer"`** - **`"2021.0.5"`** (ці больш новую). Запусціце **`"PLCnext Engineer"`** і абярыце **`"Empty AXC F 2152 v00 / 2021.0.0 project"`**:
<p align="center"> <img src="images/new_project_PLCnextEng.png"> </p>
<p align="center"> Малюнак 7. Стварэнне новага праекта</p>

Будзе створаны праект па змаўчанні.

## Налада праекта PLCnext Engineer ##

### Агульная налада праекта ###

Адкрыйце ўласцівасці праекта (падвойным пстрычкай мышы на элеменце дрэва **`"Project"`**) - тут мы бачым агульныя налады сеткі па змаўчанні (кантролер і шыны):
<p align="center"> <img src="images/project_settings.png"> </p>
<p align="center"> Малюнак 8. Налады сеткі праекту</p>

Тут мы змяняем налады на патрэбныя значэнні.

На старонцы **`"IP Subnet"`** паказаны сеткавыя налады кантролера:

<p align="center"> <img src="images/IP_settings.png"> </p>
<p align="center"> Малюнак 9. Налады IP кантролера</p>

### Налада сеткавых налад кантролера ###

Адкрыйце старонку **`"Online Devices"`**, абярыце патрэбную сетку з выпадальнага спісу і націсніце кнопку **`"Scan the network"`**. Пасля сканавання павінен адлюстравацца знойдзены кантролер:

<p align="center"> <img src="images/online_scan.png"> </p>
<p align="center"> Малюнак 10. Пошук кантролера</p>

Усталюйце выяўлены кантролер у якасці кантролера праекта:

<p align="center"> <img src="images/name_selecting.png"> </p>
<p align="center"> Малюнак 11. Налады кантролера</p>

Знойдзены кантролер будзе дададзены ў праект і настроены, праз некаторы час ён павінен адлюстравацца з новымі наладамі:

<p align="center"> <img src="images/settings_ok.png"> </p>
<p align="center"> Малюнак 12. Кантролеры</p>

### Падключэнне да кантролера ###

Адкрыйце старонку з наладамі кантролера і націсніце кнопку падключэння:

<p align="center"> <img src="images/PLC_connecting_button.png"> </p>
<p align="center"> Малюнак 13. Падключэнне кантролера</p>

Пасля паспяховай аўтарызацыі мы атрымліваем інфармацыю пра бягучы стан кантролера:

<p align="center"> <img src="images/controller_info.png"> </p>
<p align="center"> Малюнак 14. Інфармацыя пра кантролер</p>

### Змена пароля ###

Настойліва рэкамендуецца змяніць пароль адміністратара:

<p align="center"> <img src="images/change_pass.png"> </p>
<p align="center"> Малюнак 15. Змена пароля</p>
