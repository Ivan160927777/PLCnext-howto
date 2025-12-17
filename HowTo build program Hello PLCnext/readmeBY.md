# Як стварыць просты дадатак "Hello PLCnext" #

> [!IMPORTANT]
> Заснавана на афіцыйнай [дакументацыі](https://github.com/PLCnext/SampleRuntime/blob/master/getting-started/Part-01/README.md).

> [!TIP]
> English version is [here](./readme.md).\
> Русский вариант находится [здесь](./readmeRU.md).

## Выкарыстанне каманднага радка (чысты **CMake**) ##

Пасля таго, як кланіравалі рэпазіторый, выканайце наступныя дзеянні ў рабочым каталозе 
`"HowTo build program Hello PLCnext\Hello-PLCnext"`.

Канфігураванне:
```sh
cmake --preset=build-windows-AXCF2152-2021.0.3.35554 .
```

Зборка:
```sh
cmake --build --preset=build-windows-AXCF2152-2021.0.3.35554 --target all
```

Разгортванне:
```sh
cmake --build --preset=build-windows-AXCF2152-2021.0.3.35554 --target install
```

У прыведзеных вышэй камандах імя перадустаноўкі
`build-windows-AXCF2152-2021.0.3.35554` вызначае параметры
зборкі ў АС Windows для AXC 2152. Яны захоўваюцца ў файле
`"HowTo build program Hello PLCnext\Hello-PLCnext\CMakePresets.json"`. 
Унутры гэтага файла вы можаце знайсці параметры:

- Параметр `PLCNEXT_SDK_ROOT` паказвае поўны шлях да карнявога каталога SDK.
- Параметры`ARP_DEVICE` и `ARP_DEVICE_VERSION` павінны паказваць устройства і версію SDK.

Пры неабходнасці вы можаце змяніць іх на выкарыстоўваемыя.

Пасля разгортвання вы можаце знайсці выконваемы файл тут:

>deploy\AXCF2152_21.0.3.35554\Release\bin\hello_PLCnext

У **АС Linux** выкарыстоўвайце імя перадустаноўкі `build-linux-AXCF2152-2021.0.3.35554`.

## Выкарыстанне MS Visual Studio Code ##

Адкрыйце каталог `"HowTo build program Hello PLCnext\Hello-PLCnext"` ў MS Visual Studio Code.

І так, вы адкрылі праект на аснове CMake.
Усталюйце аўтаматычна прапанаваную канфігурацыю і
стварыце дадатак.

## Выкарыстанне MS Visual Studio 2019 Community (АС Windows) ##

Адкрыйце каталог `"HowTo build program Hello PLCnext\Hello-PLCnext"` 
у MS Visual Studio.

Вы адкрылі праект на аснове CMake.
Усталюйце аўтаматычна прапанаваную канфігурацыю і
стварыце дадатак. (націсніце **F7**, каб пачаць працэс зборкі).

## Выкарыстанне іншай IDE, которая поддерживает предустановки CMake ##

Адкрыйце каталог `"HowTo build program Hello PLCnext\Hello-PLCnext"` у IDE.

Вы адкрылі праект на аснове CMake.
Усталюйце аўтаматычна прапанаваную канфігурацыю і
стварыце дадатак.
