## [README принципа работы от разработчика>>](https://github.com/nikrays/Zapret-on-Keenetic/blob/master/docs/readme.txt)

# Подробная обновляемая [@nik](https://t.me/nik_pushistov) инструкция настройки репозитория [Zapret](https://github.com/bol-van/zapret) от [bol-van](https://github.com/bol-van) на Keenetic.

## Краткое описание.

Автономное, без задействования сторонних серверов, средство противодействия DPI.
Может помочь обойти замедления сайтов http(s), сигнатурный анализ tcp и udp протоколов,
например с целью замедления YouTube.

Существуют режимы обхода TPWS и NFQWS. Режим NFQWS имеет ряд преимуществ пред режимом TPWS. Больше параметров модификации TCP соединения на уровне пакетов. Реализуется через обработчик очереди NFQUEUE и raw сокеты, а также возможность модификации трафика по протоколу QUIC.

### P.S. Это не VPN и не прокси, это средство для обмана (подмены) пакетов tcp и udp протокола, не режет скорость, повышается анонимность, а также не ломает то, что и так хорошо работало.

### По необходимости улучшаются: [config](https://github.com/nikrays/Zapret-on-Keenetic?tab=readme-ov-file#14-%D0%B7%D0%B0%D0%B3%D1%80%D1%83%D0%B6%D0%B0%D0%B5%D0%BC-%D0%B3%D0%BE%D1%82%D0%BE%D0%B2%D1%8B%D0%B9-%D0%BA%D0%BE%D0%BD%D1%84%D0%B8%D0%B3-zapret-%D0%BF%D0%BE%D0%B4%D1%85%D0%BE%D0%B4%D0%B8%D1%82-%D0%B4%D0%BB%D1%8F-%D0%B1%D0%BE%D0%BB%D1%8C%D1%88%D0%B8%D0%BD%D1%81%D1%82%D0%B0-%D0%BF%D1%80%D0%BE%D0%B2%D0%B0%D0%B9%D0%B4%D0%B5%D1%80%D0%BE%D0%B2-%D1%81-pppoe-%D1%82%D0%B5%D1%81%D1%82%D0%B8%D1%80%D0%BE%D0%B2%D0%B0%D0%BB%D1%81%D1%8F-%D0%BD%D0%B0-%D1%80%D0%BE%D1%81%D1%82%D0%B5%D0%BB%D0%B5%D0%BA%D0%BE%D0%BC-%D0%B4%D0%BE%D0%BC%D1%80%D1%83), [hostlists](https://github.com/nikrays/Zapret-on-Keenetic?tab=readme-ov-file#15-%D0%B4%D0%B0%D0%BB%D0%B5%D0%B5-%D0%B2%D1%8B%D0%B1%D0%B8%D1%80%D0%B0%D0%B5%D0%BC-%D1%87%D1%82%D0%BE-%D0%B1%D1%83%D0%B4%D0%B5%D0%BC-%D1%83%D1%81%D0%BA%D0%BE%D1%80%D1%8F%D1%82%D1%8C), [zapret](https://github.com/nikrays/Zapret-on-Keenetic?tab=readme-ov-file#%D0%BE%D0%B1%D0%BD%D0%BE%D0%B2%D0%B8%D1%82%D1%8C-%D1%80%D0%B5%D0%BF%D0%BE%D0%B7%D0%B8%D1%82%D0%BE%D1%80%D0%B8%D0%B9-zapret-%D0%BC%D0%BE%D0%B6%D0%BD%D0%BE-%D0%B2%D1%8B%D0%BF%D0%BE%D0%BB%D0%BD%D0%B8%D0%B2-%D1%8D%D1%82%D1%83-%D0%BA%D0%BE%D0%BC%D0%B0%D0%BD%D0%B4%D1%83-%D1%80%D0%B0%D0%B7%D1%80%D0%B0%D0%B1%D0%BE%D1%82%D1%87%D0%B8%D0%BA-%D0%B2-%D0%BF%D0%BE%D1%81%D0%BB%D0%B5%D0%B4%D0%BD%D0%B5%D0%B5-%D0%B2%D1%80%D0%B5%D0%BC%D1%8F-%D0%B0%D0%BA%D1%82%D0%B8%D0%B2%D0%B8%D0%B7%D0%B8%D1%80%D0%BE%D0%B2%D0%B0%D0%BB%D1%81%D1%8F-%D0%B8-%D1%80%D0%B5%D0%B3%D1%83%D0%BB%D1%8F%D1%80%D0%BD%D0%BE-%D0%BF%D1%80%D0%B0%D0%B2%D0%B8%D1%82-%D0%BA%D0%BE%D0%B4). После обновления хотя бы одного из них, обязательно [перезагружаем entware(openwrt)](https://github.com/nikrays/Zapret-on-Keenetic?tab=readme-ov-file#16-%D0%BF%D0%B5%D1%80%D0%B5%D0%B7%D0%B0%D0%B3%D1%80%D1%83%D0%B6%D0%B0%D0%B5%D0%BC-entwareopenwrt-%D0%BA%D0%BE%D0%BC%D0%B0%D0%BD%D0%B4%D0%BE%D0%B9-%D0%BD%D0%B8%D0%B6%D0%B5) В конце инструкции вас ждут полезные команды.

## Технические требования.

(рекомендуемые) Keenetic Viva kn-1912 равным или более 256мб ОЗУ и наличием USB порта.

(минимальные) Keenetic Extra, Viva с менее 256мб ОЗУ и наличием USB порта.

## Подготовка.

(обязательно) Проверить, что установленны все пакеты под категорией OPKG в наборах компонентов в настройках, также протокол IPv6 и Модули ядра подсистемы Netfilter (он появится в списке пакетов только после установки пакета "Протокол IPv6").

(обязательно) Необходимо заменить в настройках роутера DNS-серверы провайдера на публичные. Прописываем IP адреса DNS - 8.8.8.8 и 77.88.8.8, и не забываем поставить галочку "игнорировать DNS предлагаемые провайдером интернета".

(обязательно) [Установка системы пакетов репозитория Entware на USB-накопитель](https://help.keenetic.com/hc/ru/articles/360021214160). 
Или не очень хороший метод [Установка OPKG Entware на встроенную память роутера](https://help.keenetic.com/hc/ru/articles/360021888880).

(опционально) Можно настроить, но не обязательно, если совсем ничего не поможет. [Прокси-серверы DNS-over-TLS и DNS-over-HTTPS для шифрования DNS-запросов](https://help.keenetic.com/hc/ru/articles/360007687159).

Все дальнейшие команды выполняются не в cli роутера, а **в среде entware**.

### Подключение по SSH к роутеру через "putty", например если адрес вашего роутера 192.168.1.1 а порт 22 или 222 если активировали сервер SSH

### Логин: 
```shell
root
```

### Пароль: 
```shell
keenetic
```

### Если увидите "(config)>" значит вошли под admin, чтобы продолжить, вводим:
```shell
exec sh
```

### Если видим BusyBox v1.36.1 (XXXX-XX-XX xx:xx:xx UTC) built-in shell (ash), переходим к установке, левой кнопкой мыши нажимая на квадратики копируем код, а правой вставляем в putty.

## Установка.

### 1. Обновляем пакеты opkg.
```shell
opkg update
```

### 2. Устанавливаем пакеты ipset:

```shell
opkg install coreutils-sort curl git-http grep gzip ipset iptables kmod_ndms nano xtables-addons_legacy
```

### 3. Загружаем репозитории Zapret:
```shell
cd /opt/tmp
git clone --depth=1 https://github.com/bol-van/zapret.git
```

### 4. Начнинаем устновку, выполняем скрипт:
```shell
cd zapret
./install_easy.sh
```

### 5. Далее (будут спрашивать, 3 раза отвечаем Y, затем enter после каждого раза):
```shell
y
```

### 6. Далее нас будут много о чем спрашивать, везде нажимаем ENTER, пока не увидим надпись press enter to continue, а затем снова жмем ENTER.

### 7. Удаляем ненужное:
```shell
rm -rf /opt/tmp/*
```

### 8. Создадим правило для автозапуска Zapret при включении роутера:
```shell
ln -fs /opt/zapret/init.d/sysv/zapret /opt/etc/init.d/S90-zapret
```

### 9. Загружаем готовый стартовый скрипт с dnsmasq внутри:
```shell
cd /opt/zapret/init.d/sysv
curl -O https://raw.githubusercontent.com/nikrays/Zapret-on-Keenetic/master/opt/zapret/init.d/sysv/zapret
```

### 10. Загружаем готовый скрипт, чтобы роутер не забывал правила:
```shell
cd /opt/etc/ndm/netfilter.d
curl -O https://raw.githubusercontent.com/nikrays/Zapret-on-Keenetic/master/opt/etc/ndm/netfilter.d/000-zapret.sh
```

### 11. Исполняем:
```shell
chmod +x /opt/etc/ndm/netfilter.d/000-zapret.sh
```

### 12. Загружаем готовый скрипт для перевода net.netfilter.nf_conntrack_checksum в 0:
```shell
cd /opt/etc/init.d
curl -O https://raw.githubusercontent.com/nikrays/Zapret-on-Keenetic/master/opt/etc/init.d/S00fix
```

### 13. Исполняем:
```shell
chmod +x /opt/etc/init.d/S00fix
```

### 14. (обновляемый пункт) Загружаем готовый конфиг Zapret, подходит для большинста провайдеров с pppoe (Тестировался на Ростелеком, Дом.ру):
```shell
cd /opt/zapret
curl -O https://raw.githubusercontent.com/nikrays/Zapret-on-Keenetic/master/opt/zapret/config
```
##### Или такой, разницу сможете ощутить после завершения цикла настройки (сменил первый сегмент фейка с disorder2 на split2, а также ttl на знаение 6).
```shell
cd /opt/zapret
curl -O https://raw.githubusercontent.com/nikrays/Zapret-on-Keenetic/master/opt/zapret_alt/config
```

#### Так как вы вставили мой конфиг, вы также перенесли несколько настроек, если у вас авторизация у провайдера pppoe, а роутер с ОЗУ более 256мб, то переходим к 15 шагу.
```bash
IFACE_WAN=ppp0
MODE_FILTER=autohostlist
```

#### Для начала узнаем имя внешнего сетевого интерфейса (WAN) на роутере. Его можно узнать воспользовавшись командой ifconfig, которая выведет все сетевые интерфейсы в системе. Просто находим тот интерфейс, у которого будет ваш внешний IP адрес. В моем случае – это ppp0, в вашем же, если у вам провайдер выдает адрес по статике или DHCP, значит у вас eth3. Запоминаем.
```shell
ifconfig
```

#### Если у вас роутер с ОЗУ менее 256мб или авторизация у провайдера не pppoe, а динамика или статика по динамике, то правим конфиг Zapret, редактором, командой ниже.
```shell
nano /opt/zapret/config
```

#### Если у вас роутер с ОЗУ менее 256мб, ищем строку MODE_FILTER=autohostlist и на:
```bash
MODE_FILTER=hostlist
```

#### Прописываем интерфейс провайдера в строке IFACE_WAN=ваш интерфейс, например:
```bash
IFACE_WAN=eth3
```

#### Также можно прописать несколько используемых WAN интерфейсов через пробел, например:
```bash
IFACE_WAN="eth3 usb0"
```

#### (опционально, надо проверить) Если необходимо направить трафик не на всю сеть, а например только гостевую сеть, vlan, опеределенный порт или l2tp, уберите решетку в #IFACE_LAN=eth0 и укажите 1 или несколько интерфейсов (узнать какой интерфейс за что отвечает, можно все той же командой ifconfig):
```bash
IFACE_LAN=br0
```
#### Или br0 - это бридж основной сети, br1 - vlan гостевой сети, ezcfg0 - частный VPN сервер IKEv2/IPsec и т.д.:
```bash
IFACE_LAN="br0 br1 ezcfg0"
```

Если закончили править, сохраняем CTRL+S, затем CTRL+X для выхода.

### 15. (обновляемый пункт) Далее выбираем, что будем ускорять:

#### Если необходимо ускорить только youtube, загружаем:
```shell
cd /opt/zapret/ipset
curl -O https://raw.githubusercontent.com/nikrays/Zapret-on-Keenetic/master/hostlists/youtube/zapret-hosts-user.txt
```

#### Если необходимо ускорить youtube и соц. сети f, i, t(x):
```shell
cd /opt/zapret/ipset
curl -O https://raw.githubusercontent.com/nikrays/Zapret-on-Keenetic/master/hostlists/yfit/zapret-hosts-user.txt
```

#### Если необходимо ускорить все что можно, то:
```shell
cd /opt/zapret/ipset
curl -O https://raw.githubusercontent.com/nikrays/Zapret-on-Keenetic/master/hostlists/blacklist-russia/zapret-hosts-user.txt
```

### 16. Перезагружаем entware(openwrt) командой ниже:
```shell
/opt/etc/init.d/rc.unslung restart
```

## Готово, проверяем.



### Если не заработало, открываем снова конфиг:
```shell
nano /opt/zapret/config
```

#### Обращаем внимание на:
```bash
NFQWS_OPT_DESYNC="--dpi-desync=fake,disorder2 --dpi-desync-split-pos=1 --dpi-desync-ttl=0 --dpi-desync-fooling=md5sig,badsum --dpi-desync-repeats=6 --dpi-desync-any-protocol --dpi-desync-cutoff=d4" 
```

#### Можно попробовать менять значение ttl от 0 до 12 или же сменить значения dpi-desync с split2 на disorber2 ниже несколько примеров:
```bash
NFQWS_OPT_DESYNC="--dpi-desync=split2"
```
```bash
NFQWS_OPT_DESYNC="--dpi-desync=fake,split2 --dpi-desync-ttl=2 --dpi-desync-fooling=badsum"
```
```bash
NFQWS_OPT_DESYNC="--dpi-desync=fake,disorder2 --dpi-desync-ttl=3 --dpi-desync-fooling=badsum"
```
```bash
NFQWS_OPT_DESYNC="--dpi-desync=fake,split2 --dpi-desync-ttl=6 --dpi-desync-fooling=badsum"
```
```bash
NFQWS_OPT_DESYNC="--dpi-desync=fake,split2 --dpi-desync-ttl=3 --dpi-desync-fooling=badsum"
```
```bash
NFQWS_OPT_DESYNC="--dpi-desync=fake,split2 --dpi-desync-ttl=6 --dpi-desync-fooling=md5sig"
```
```bash
NFQWS_OPT_DESYNC="--dpi-desync=fake,split2 --dpi-desync-ttl=6 --dpi-desync-ttl6=2 --dpi-desync-split-pos=1 --wssize 1:6 --dpi-desync-fooling=md5sig"
```

#### После этого перезагружаем entware(openwrt) и так до тех пор, пока не достигните результата.
```shell
/opt/etc/init.d/rc.unslung restart
```
Или
```shell
/opt/zapret/init.d/sysv/zapret restart
```

## P.S.:

### Также можно воспользоваться автоподбором. Автоподбор параметров, у каждого могут быть индивидуальными
Следует прогнать blockcheck по нескольким замедленным сайтам и выявить общий характер замедленний.
Разные сайты могут быть замедленны по-разному, нужно искать такую технику, которая работает на большинстве.
Чтобы записать вывод blockcheck.sh в файл, выполните : ./blockcheck.sh | tee /tmp/blockcheck.txt
```shell
/opt/zapret/blockcheck.sh | tee /opt/zapret/blockcheck.txt
```

<details>
    <summary>Проанализируйте какие методы дурения DPI работают, в соответствии с ними настройте /opt/zapret/config.<summary>


Имейте в виду, что у провайдеров может быть несколько DPI или запросы могут идти через разные каналы
по методу балансировки нагрузки. Балансировка может означать, что на разных ветках разные DPI или
они находятся на разных хопах. Такая ситуация может выражаться в нестабильности работы обхода.
Дернули несколько раз curl. То работает, то connection reset или редирект. blockcheck.sh выдает
странноватые результаты. То split работает на 2-м. хопе, то на 4-м. Достоверность результата вызывает сомнения.
В этом случае задайте несколько повторов одного и того же теста. Тест будет считаться успешным только,
если все попытки пройдут успешно.

При использовании autottl следует протестировать как можно больше разных доменов. Эта техника
может на одних провайдерах работать стабильно, на других потребуется выяснить при каких параметрах
она стабильна, на третьих полный хаос, и проще отказаться.

Blockcheck имеет 3 уровня сканирования.
Цель режима quick - максимально быстро найти хоть что-то работающее.
standard дает возможность провести исследование как и на что реагирует DPI в плане методов обхода.
force дает максимум проверок даже в случаях, когда ресурс работает без обхода или с более простыми стратегиями.
<details>

#### Автохостлист находится по адресу (Сюда идет пополнение доменов на те к которым вы пытаетесь достучаться, например рутор, чуть позже он автоматически туда попадает):
```shell
nano /opt/zapret/ipset/zapret-hosts-auto.txt
```

#### Ручной список доменов:
```shell
nano /opt/zapret/ipset/zapret-hosts-user.txt
```

#### Запустить NFQWS и проверять работоспособность с помощью команды:
```shell
/opt/zapret/init.d/sysv/zapret start
```

#### Для перезагрузки NFQWS использовать команду:
```shell
/opt/zapret/init.d/sysv/zapret restart
```

#### Для остановки NFQWS использовать команду:
```shell
/opt/zapret/init.d/sysv/zapret stop
```

### Сделать backup entware(openwrt) с Zapret:
```shell
cd /opt
tar cvzf /opt/backup-`date -I`.tar.gz *
```

### Для очистки содержимого накопителя, чтобы например, попробовать все заново:
```shell
rm -rf /opt/*
```

### Чтобы восстановить backup entware(openwrt) с Zapret, достаточно снова создать папку install и загрузить в нее ранее созданный backup, после чего переопределить накопитель в менеджере OPKG выбрав "не выбран" затем снова выбрать "накопитель", ждем когда закончится процесс развертывания. Далее вставляем скрипт ниже в параметр "Сценарий initrc" в менеджере OPKG, после перезагружаем роутер.
```shell
/opt/etc/init.d/rc.unslung
```

### Обновить репозиторий Zapret можно выполнив эту команду (разработчик в последнее время активизировался и регулярно правит код):
```shell
cd /opt/zapret
git pull --rebase
```

#zapret #bol-van #keenetic #youtube #ускорение #ростелеком #дом.ру #мтс
