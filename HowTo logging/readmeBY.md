# Як весці лог #
> [!TIP]
> English version is [here](./readme.md).

## 1.  Файл логаў дыягностыкі **PLCnext** ##

Паведамленні PLCnext знаходзяцца тут: *"/var/log/messages"* і *"/var/log/error"*.
Каб прагледзець змест файла выкарыстайце адну з гэтых каманд:

```sh
cat /var/log/messages
cat /var/log/error
```

Для таго, каб пастаянна кантраляваць змесціва файла, выкарыстоўвайце гэту каманду:

```sh
tail -F /var/log/messages
```

![tail -F /opt/plcnext/logs/Output.log](images/tail_F.gif)

Параметр **-F** важны - ён робіць магчымым бачыць адрозненні
пасля змены файла (таму что ў файле лога адбываюцца змены, пры гэтым ёсць
тое, что не змяняецца зусім, а старыя данные выдаляюцца).

Наступная каманда аблегчыць выяўленне памылак з дапамогай розных колераў.
```sh
tail -F /var/log/messages /var/log/error | awk '
  /\/var\/log\/messages/ {print "\033[32m" $0 "\033[39m"; current_color="\033[32m"; next}
  /\/var\/log\/error/ {print "\033[31m" $0 "\033[39m"; current_color="\033[31m"; next}
  /WARN/ {print "\033[33m" $0 "\033[39m"; next}
  /DEBUG/ {print "\033[37m" $0 "\033[39m"; next}
  1 {print current_color $0 "\033[39m"}
  '
```

![colored tail -F](images/colored_tail_F.gif)

## 2. Файл логаў дыягностыкі сістэмы ##

Файл логаў сістэмы знаходзіцца тут: *"/var/log/messages"* і
*"/var/log/error"*. 
Вы можаце выкарыстоўваць змест гэтых файлаў для прагляду 
падзей усёй сістэмы.
Калі патрабуецца знайсці пэўныя падзеі(напрыклад,
**Arp.System**) - можна выкарыстоўваць *awk*:

```sh
tail -F /var/log/messages /var/log/error | awk '
  /\/var\/log\/messages/ {print "\033[32m" $0 "\033[39m"; current_color="\033[32m"; next}
  /\/var\/log\/error/ {print "\033[31m" $0 "\033[39m"; current_color="\033[31m"; next}
  /WARN/ && /Arp.System/ {print "\033[33m" $0 "\033[39m"; next}
  /DEBUG/ && /Arp.System/ {print "\033[37m" $0 "\033[39m"; next}
  /Arp.System/ {print current_color $0 "\033[39m"}
  '
```

## 3. Выкарыстанне **syslog** ##

Вы можаце выкарыстоўваць **syslog**
і захаваць паведамленні ў файл логаў дыягностыкі сістэмы:

```cpp
#include <syslog.h>
//...
openlog ("my_prog", LOG_CONS | LOG_PID | LOG_NDELAY, LOG_USER);

syslog (LOG_NOTICE, "Program started by User %d", getuid ());
syslog (LOG_INFO, "Test info message.");

closelog ();
//...
```
