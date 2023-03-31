# Bookstack app with docker-compose
====
## 📚 Bookstack 

BookStack - это платформа с открытым исходным кодом для создания документации и вики-контента для пользователей. <br>
Платформа построена на стеке LAMP или LEMP и отлично подходит для создания документов для любого проекта. <br>

[Автор проекта и сам проект](https://github.com/BookStackApp/BookStack)

## 🔧 Installation 

Project was created on Ubuntu 20.04v <br>

##### Requirements: <br>

- Install docker on your machine

Thats all))0) <br>

##### Change ENV or PORT

If you want to change port, for example, 8080-8081, you should change 3 files from this project: <br>

- docker-compose.yml (ports 80 -> needed port)
- apache/Dockerfile (EXPOSE 80 -> needed port)
- apache/bookstack.conf (VirteulHost *:80 -> *.[needed port])

To make yours user, password and database name change <b>envs</b> file

###### Host 

If you install on local machine you must change your local hosts file necessarily

 
