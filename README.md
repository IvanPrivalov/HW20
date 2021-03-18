# DHCP, PXE Linux

## Настройка сервера установки дистрибутива

## Выполнение ДЗ

Копируем файлы в каталог и запускаем PXE сервер:

```sgell
vagrant up pxeserver
```

После загрузки PXE сервера, запускаем клиент:

```sgell
vagrant up pxeclient
```

В окне VirtualBox открываем консоль pxeclient, увидим загрузку по PXE 

![Image 1](https://github.com/IvanPrivalov/HW19/blob/master/Screenshots/1.PNG)

Выбираем Install System и запустится установка Centos 7

![Image 2](https://github.com/IvanPrivalov/HW19/blob/master/Screenshots/2.PNG)



