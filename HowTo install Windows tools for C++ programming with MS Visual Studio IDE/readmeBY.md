# Як наладзіць MS Visual Studio Community® для праграмавання і кроскампіляцыі для the AXC F **x**152 controllers на Windows 10 #
> [!TIP]
> English version is [here](./readme.md).

> Гэта кіраўніцтва працуе толькі для прашыўкі AXC F 2152 версіі 2021.9. Для іншых прылад або версій фрэймворкаў сцягі зборкі адрозніваюцца і могуць змяняцца ў залежнасці ад версіі.

> Заснавана на афіцыйнай [дакументацыі](https://www.plcnext.help/te/Programming/Cpp/Cpp-programming.htm).

## 1. Усталяванне **MS Visual Studio Community®** IDE ##

1. Для усталявання **Visual Studio Community®** перайдзіце па спасылцы: https://visualstudio.microsoft.com/, выбярыце і скачайце Community version.

## 2. Усталяванне (абнаўленне) PLCnext CLI ##

>**PLCnext CLI** гэта интерфейс каманднага радка які можна выкарыстоўваць для генерацыі метададзеных, загалоўкавых файлаў С++, інжынерных бібліятэк PLCnext і працэса зборкі. Функцыі мажліва выклікаць з дапамогай простых каманд. Убудаваная даведка ўключае у сябе спіс каманд і апісанне іх функцый.

Загрузіце апошнюю версію з сайта Phoenix Contact: https://www.phoenixcontact.com/products (напрыклад, з вобласці **AXC F 2152** - http://www.phoenixcontact.com/qr/2404267/softw, цяперашняя версія: `2021.6`).

Перайдзіце ў каталог у якім знаходзяца файлы для загрузкі (тыповы шлях: `%userprofile%/Downloads`), распакуйце архіў (`PLCnext_Toolchain_WindowsSetup_.zip`).

Перайдзіце ў каталог, у які раней былі распакаваны файлы для спампавання, запусціце установачны файл (`PLCnext_Toolchain_WindowsSetup.exe`) і выканайце інструкцыі майстра ўстаноўкі.

![SDK ok](images/PLCNCLI_setup.png)

>Для абнаўлення проста запусціце праграму ўстаноўкі і пераканайцеся, што яна ўстаноўлена ў той жа каталог, у якім быў усталяваны папярэдні PLCnext CLI.

Праверце ўстаноўку:

```ps
plcncli.exe --version
```

Пасля гэтага праверка павінна выглядаць наступным чынам:

```ps
plcncli 21.6.0.726 (21.6.0.726)
```
## 3. Скачыванне PLCnext Technology C++ Toolchain ##

Загрузіце апошнюю версію з сайта Phoenix Contact: https://www.phoenixcontact.com/products (напрыклад, з вобласці **AXC F 2152** - http://www.phoenixcontact.com/qr/2404267/softw, цяперашняя версія: `2021.9`).

Перайдзіце ў каталог у якім знаходзяца загружаныя файлы (тыповы шлях: `%userprofile%/Downloads`), распакуйце архіў (`SDK_2021.9_Windows_AXC_F_2152.tar.xz.zip`).

## 4. Устаноўка (абнаўленне) SDK ##

Перайдзіце ў каталог, у які раней былі разархіваваны загружаныя файлы. Выклічце інтэрфейс каманднага радка ў кансолі, выкарыстоўваючы наступную каманду:

```ps
plcncli.exe install sdk –d [installation path] –p [path to archive file]
```

>Калі вы ўсталёўваеце некалькі пакетаў SDK, Phoenix Contact рэкамендуе выкарыстоўваць структуру каталогаў "target name/firmware version".

Напрыклад:

```ps
plcncli.exe install sdk -d C:\CLI\SDKs\AXCF2152\2021_9\ -p pxc-glibc-x86_64-mingw32-axcf2152-image-mingw-cortexa9t2hf-neon-axcf2152-toolchain-2021.9.tar.xz
```

> SDK спецыялізаваны пад кантролер. Поўны спіс кантролераў можаце знайсці на сайте PHOENIX CONTACT ([Home > Products > PLCs and I/O systems > PLCnext Control > Product list PLCnext Technology components](https://www.phoenixcontact.com/online/portal/pi?1dmy&urile=wcm%3apath%3a/pien/web/main/products/list_pages/PLCnext_technology_components_P-21-14-01/f77f0eb0-2a70-40c3-8679-7df2450e26db)).

## 5. Стварэнне новага C++ праекта в Visual Studio ##

Цяпер вы можаце стварыць C++ проект з шаблону **PLCnext**. Запусціце Visual Studio, выбярыце `"Create a new project"` і адшукайце **plcnext** у дыялогавым акне каб праглядзець шаблоны праектаў **PLCnext** і выбраць шаблон які вам патрэбен, затым націсніце Next.

Больш інфармаціі знаходзіца [тут](https://www.plcnext.help/te/Programming/Cpp/Cpp_programming/Working_with_Visual_Studio.htm).

## 6. Адкрыцце існуючага C++ праекта в Visual Studio ##

З-за вядомай [праблемы](https://github.com/PLCnext/PLCnext_CLI_VS/issues/4) вы можаце атрымаць памылкі падчас кампіляцыі. Каб выправіць гэта, вам патрэбна выдаліць кэш .NET:

```ps
rmdir %temp%\.net /s
```
