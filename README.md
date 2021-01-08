# Домашнее задание по ТПОС №3 (Ansible)

## Описание

Представлены скрипт ансибл, вагрантфайл для виртуальной машины и доп файлы (ssh ключи, inventory, nginx конфиг, шаблон service_state и.т.д.)

## Userguide
IP виртуалки: 192.168.10.20
Для запуска виртуальной машины:
```
vagrant up
```
Для запуска скрипта:
```
ansible-playbook -i ./hosts tasks.yml
```
Проверка работы:
```
curl 192.168.10.20/service_data
```
должен отдать содержимое ```service_state```, что то вроде:
```
Seems work fine
Service uptime is * minutes
```