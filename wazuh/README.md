1. Установить osquery (вынесен в отдельный плейбук для удобства отладки)
   $  ansible-playbook deb_osquery.yml -vv

Если osquery уже установлен достаточно запустить копирование конфигов osquery и перезапуск службы:
   $  osquery_only_copy_conf_and_restart.yml -vv 

2. Установить wazuh-agent (взят с оф. репозитория, изменены default конфиги под нас)
   $  ansible-playbook wazuh-agent.yml -vv

Архитектура приложения описана здесь:
https://documentation.wazuh.com/current/getting-started/architecture.html

3. Wazuh по-умолчанию собирает логи из "стандартных" мест:

/var/log/nginx/access.log
/var/log/nginx/error.log
/var/log/messages
/var/log/auth.log
/var/log/syslog
/var/log/dpkg.log
/var/log/kern.log

и т.д.

Приложения, пишущие логи в "нестандартные" места нужно будет указывать отдельно, соответственно нужно будет 
выслать мне информацию о: 

a. расположении файла; 
b. тип лога и название приложения; 
c. пример лог файла

4. В ansible-playbook добавлен конфиг для logrotate osquery, для остальных логов logrotate настраивается индивидуально.


Системные требования:

1. Osquery+Wazuh - до 300 Mb RAM \ 10-30 % CPU 
2. OpenScap - загружает одно ядро во время сканирования + 300 Mb RAM (1ин раз в n\дней)
3. Небольшое дерградирование по iops HDD (зависит от количества логов\событий)

Для ограничения служб на слабых \ нагруженных серверах рекомендуется:

systemctl set-property osqueryd.service CPUQuota=5% MemoryLimit=150M CPUShares=400
systemctl set-property wazuh-agent.service CPUQuota=5% MemoryLimit=100M CPUShares=400

и перезапустить эти службы

systemctl daemon-reload
systemctl restart osqueryd.service
systemctl restart wazuh-agent.service

Подробнее:
https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/7/html/resource_management_guide/sec-modifying_control_groups

