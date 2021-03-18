# DNS

## Задание

Взять стенд https://github.com/erlong15/vagrant-bind, добавить еще один сервер client2.

Завести в зоне dns.lab имена:

web1 - смотрит на клиент1
web2 - смотрит на клиент2

Завести еще одну зону newdns.lab, завести в ней запись:

www - смотрит на обоих клиентов

Настроить split-dns:

клиент1 - видит обе зоны, но в зоне dns.lab только web1
клиент2 - видит только dns.lab

*) настроить все без выключения selinux

## Выполнение ДЗ

Копируем файлы в каталог и запускаем Vagrantfile:

```shell
vagrant up
```

После загрузки, запускаем client1 и client2:

```shell
vagrant ssh client1
```

```shell
vagrant ssh client2
```

## Проверяем видимость зон:

Клиент1 - видит обе зоны, но в зоне dns.lab только web1:

```shell
otus@otus-VirtualBox:~/Desktop/HW20$ vagrant ssh client1
Last login: Thu Mar 18 07:14:45 2021 from 10.10.10.1
[vagrant@client1 ~]$ sudo -i
[root@client1 ~]# dig web1.dns.lab +short @192.168.50.10
192.168.50.111
[root@client1 ~]# dig web1.dns.lab +short @192.168.50.11
192.168.50.111
[root@client1 ~]# dig web2.dns.lab +short @192.168.50.10
[root@client1 ~]# dig web2.dns.lab +short @192.168.50.11
[root@client1 ~]# dig www.newdns.lab +short @192.168.50.10
192.168.50.103
[root@client1 ~]# dig www.newdns.lab +short @192.168.50.11
192.168.50.103
[root@client1 ~]# 
```

Клиент2 - видит только dns.lab:

```shell
otus@otus-VirtualBox:~/Desktop/HW20$ vagrant ssh client2
Last login: Thu Mar 18 07:18:25 2021 from 10.10.10.1
[vagrant@client2 ~]$ sudo -i
[root@client2 ~]# dig web1.dns.lab +short @192.168.50.10
192.168.50.111
[root@client2 ~]# dig web1.dns.lab +short @192.168.50.11
192.168.50.111
[root@client2 ~]# dig web2.dns.lab +short @192.168.50.10
192.168.50.112
[root@client2 ~]# dig web2.dns.lab +short @192.168.50.11
192.168.50.112
[root@client2 ~]# dig www.newdns.lab +short @192.168.50.10
[root@client2 ~]# dig www.newdns.lab +short @192.168.50.11
[root@client2 ~]# 
```

Видим, что запросы отрабатываются в соответсвии с заданием как на мастере, так и на слэйве.



