Данный репозиторий сделан для личного использования
-----------------------------------------------
За основу взяты : https://github.com/apolloclark/ansible-role-osquery ; https://github.com/wazuh/wazuh-ansible . 
Для утановки osquery + wazuh будем использовать playbook, который объединяет в себе 2 роли: 
* Установка  osquery
* Установка wazuh-agent
-----------------------------------------
Данный плейбук расчитан на
* Debian
* Centos
-----------------------------------------
Тесты проводились на
* Debian 8 ; 9
* Centos 7.5 ; 7.6 (В документации указано что работает с 6 версией)
---------------------------------------------
Для начала установки wazuh + osquery запускаем плейбук в таком виде
* ```ansible-playbook osquery+wazuh.yml --extra-vars "Адресс Сервера wazuh" -u root```

В данной сборке в конфиге ./agents/wazuh/wazuh-agent-role/templateslocal_internal_options.conf указанны параметры которые не позволяют серверу делать что-либо на стороне агента
```
agent.remote_conf=0
logcollector.remote_commands=0
sca.remote_commands=0
wazuh_command.remote_commands=0
```
