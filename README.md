Данный репозиторий сделан для личного использования
-----------------------------------------------
За основу взяты : https://github.com/apolloclark/ansible-role-osquery ; https://github.com/wazuh/wazuh-ansible . 
Для утановки osquery + wazuh будем использовать playbook который обьединяет в себе 2 роли: 
* Установка  osquery
* Установка wazuh-agent

В данном плейбуке для регистрации агента используется переменная '{{ address }}' поэтому запукаем плейбук в таком виде 
```ansible-playbook osquery+wazuh.yml --extra-vars "сюда вводим адрес" -u root```
