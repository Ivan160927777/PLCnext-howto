# Як выкарыстоўваць **valgrind** #
> [!TIP]
> English version is [here](./readme.md).
## 1. Зборка **valgrind** (на Linux) ##

> Заснавана на афіцыйнай [дакументацыі](https://valgrind.org/downloads/repository.html).

Выканайце кланаванне зыходнага кода **valgrind** з рэпазіторыя:

```sh
git clone git://sourceware.org/git/valgrind.git
```

Кланаванне павінна завяршыцца паспяхова:
```sh
Cloning into 'valgrind'...
remote: Enumerating objects: 132463, done.
remote: Counting objects: 100% (132463/132463), done.
remote: Compressing objects: 100% (31192/31192), done.
remote: Total 132463 (delta 101212), reused 126261 (delta 96216), pack-reused 0
Receiving objects: 100% (132463/132463), 44.84 MiB | 6.33 MiB/s, done.
Resolving deltas: 100% (101212/101212), done.
Updating files: 100% (6435/6435), done.
```

Выканайце пераход да рабочага каталога:
```sh
cd valgrind
```

Запусціце аўтаканфігурацыю:
```sh
./autogen.sh
```

Аўтаканфігурацыя павінна завяршыцца паспяхова:
```sh
running: aclocal
running: autoheader
running: automake -a
configure.ac:53: installing './compile'
configure.ac:224: installing './config.guess'
configure.ac:224: installing './config.sub'
configure.ac:37: installing './install-sh'
configure.ac:37: installing './missing'
Makefile.vex.am: installing './depcomp'
running: autoconf
```

Наладзьце асяроддзе (для магчымасці кросскампіляцыі):
```sh
source /opt/pxc/sdk/AXCF2152/2021.0/environment-setup-cortexa9t2hf-neon-pxc-linux-gnueabi
```

дзе `/opt/pxc/sdk/AXCF2152/2021.0` - шлях да вашага SDK.

Канфігурацыя:
```sh
./configure --host=armv7-linux-gnueabi --prefix=/opt/valgrind
```

Зборка:
```sh
make
```

Стварыць каталог для разгортвання і змяніць правы доступа:
```sh
sudo mkdir /opt/valgrind
sudo chmod 777 /opt/valgrind
```

Усталяванне
```sh
sudo make install
```
## 2. Разгортванне **valgrind** на кантролеры ##

Скапіруйце каталог `/opt/valgrind` на кантроллер па адрасе 
`/opt/valgrind`:
```sh
scp -r /opt/valgrind/ admin@x.x.x.x:/opt/
```

## 3. Праверка **valgrind** (на кантролеры) ##

Праверка valgrind:
```sh
/opt/valgrind/bin/valgrind --version
```

Правільны вывад павінен быць:
```sh
valgrind-3.19.0.GIT
```

Праверка з дадатковай інфармацыяй:
```sh
/opt/valgrind/bin/valgrind -d -v
```

Правільны вывад павінен быць:
```sh
--1667:1:debuglog DebugLog system started by Stage 1, level 1 logging requested
--1667:1:launcher no tool requested, defaulting to 'memcheck'
--1667:1:launcher no client specified, defaulting platform to 'arm-linux'
--1667:1:launcher launching /usr/local/libexec/valgrind/memcheck-arm-linux
--1667:1:debuglog DebugLog system started by Stage 2 (main), level 1 logging requested
--1667:1:    main Welcome to Valgrind version 3.19.0.GIT debug logging
--1667:1:    main Checking current stack is plausible
--1667:1:    main Checking initial stack was noted
--1667:1:    main Starting the address space manager
--1667:1:    main Address space manager is running
--1667:1:    main Starting the dynamic memory manager
--1667:1:mallocfr newSuperblock at 0x615AA000 (pszB 4194288)  owner VALGRIND/core
--1667:1:mallocfr deferred_reclaimSuperblock at 0x615AA000 (pszB 4194288)  (prev 0x0) owner VALGRIND/core
--1667:1:    main Dynamic memory manager is running
--1667:1:    main Initialise m_debuginfo
--1667:1:    main VG_(libdir) = /usr/local/libexec/valgrind
--1667:1:    main Getting launcher's name ...
--1667:1:    main ... /opt/valgrind/bin/valgrind
--1667:1:    main Get hardware capabilities ...
--1667:1: machine ARMv7 VFP 1 VFP2 1 VFP3 1 NEON 1
--1667:1:   cache Could not autodetect cache info
--1667:1:    main ... arch = ARM, hwcaps = ARMv7-neon-vfp
--1667:1:    main Getting the working directory at startup
--1667:1:    main ... /opt/valgrind/bin
--1667:1:    main Split up command line
--1667:1:    main (early_) Process Valgrind's command line options
--1667:1:    main Create initial image
--1667:1: initimg Loading client
valgrind: no program specified
valgrind: Use --help for more information.
```

## 4. Разгортванне сістэмных бібліятэк з інфармацыяй аб атладцы на кантролеры ##

Скапіруйце файлы з  `/opt/pxc/sdk/AXCF2152/2021.0/sysroots/cortexa9t2hf-neon-pxc-linux-gnueabi/lib/.debug/` (ПК) на `/opt/.debug/` (кантролер):
```sh
scp -r /opt/pxc/sdk/AXCF2152/2021.0/sysroots/cortexa9t2hf-neon-pxc-linux-gnueabi/lib/.debug/ admin@x.x.x.x:/opt/
```

Скапіруйце файлы на `/lib/.debug` (на кантролеры):
```sh
cp -r /opt/.debug/ /lib/
```

## 5. Выкарыстанне **valgrind** (на кантролеры) ##

Праверым сістэмную утыліту капіравання **cp**:
```sh
/opt/valgrind/bin/valgrind cp
```

Правільны вывад павінен быць:
```sh
==1975== Memcheck, a memory error detector
==1975== Copyright (C) 2002-2017, and GNU GPL'd, by Julian Seward et al.
==1975== Using Valgrind-3.19.0.GIT and LibVEX; rerun with -h for copyright info
==1975== Command: cp
==1975==
cp: missing file operand
Try 'cp --help' for more information.
==1975==
==1975== HEAP SUMMARY:
==1975==     in use at exit: 1,088 bytes in 2 blocks
==1975==   total heap usage: 4 allocs, 2 frees, 1,120 bytes allocated
==1975==
==1975== LEAK SUMMARY:
==1975==    definitely lost: 0 bytes in 0 blocks
==1975==    indirectly lost: 0 bytes in 0 blocks
==1975==      possibly lost: 0 bytes in 0 blocks
==1975==    still reachable: 1,088 bytes in 2 blocks
==1975==         suppressed: 0 bytes in 0 blocks
==1975== Rerun with --leak-check=full to see details of leaked memory
==1975==
==1975== For lists of detected and suppressed errors, rerun with: -s
==1975== ERROR SUMMARY: 0 errors from 0 contexts (suppressed: 0 from 0)
```
