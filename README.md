# Защита хоста. Сергей Миронов SYS-20


# Задание 1  

Установите eCryptfs.  
Добавьте пользователя cryptouser.  
Зашифруйте домашний каталог пользователя с помощью eCryptfs.  
В качестве ответа пришлите снимки экрана домашнего каталога пользователя с исходными и зашифрованными данными.  

# Ответ.  

Нужно применить следующие команды:  

apt install ecryptfs-utils    
adduser cryptouser   
ecryptfs-migrate-home --user cryptouser   

Перезаходим под юзером cryptouser, создаем файл, перезаходим под root, убеждаемся, что каталог недоступен:

![image](https://github.com/SergeyM90/Defence1/assets/84016375/a54271df-c685-4614-8093-ca1b0c2452f5)


# Задание 2  

Установите поддержку LUKS.  
Создайте небольшой раздел, например, 100 Мб.  
Зашифруйте созданный раздел с помощью LUKS.  
В качестве ответа пришлите снимки экрана с поэтапным выполнением задания.  

# Ответ.  
 
К виртуальной машине подключен дополнительный диск объемом 100 МБ
Установка LUKS, форматирование диска:

apt install cryptsetup  
fdisk /dev/sdb  

![task2-1 (1)](https://github.com/SergeyM90/Defence1/assets/84016375/5f2f24b0-0fb7-444d-8361-d0ef123df31e)

Шифрование раздела:

cryptsetup -y -v --type=luks2 luksFormat /dev/sdb1  
cryptsetup luksOpen /dev/sdb1 disk  
mkfs.ext4 /dev/mapper/disk   

![image](https://github.com/SergeyM90/Defence1/assets/84016375/9c8df4b3-d45e-44a8-8627-d8f6711ca1ed)

Монтирование в папку:  

mkdir .secret  
mount /dev/mapper/disk .secret/  

![image](https://github.com/SergeyM90/Defence1/assets/84016375/8b045c85-5b7e-40ad-a611-a81723689380)




