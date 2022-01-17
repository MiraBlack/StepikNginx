Данный репозиторий создан в качестве ответа на задание из пункта 1.8 Web-сервера 
курса "Web-технологии" на образовательной платформе Stepik, и может помочь в его прохождении.
Ссылка на курс: https://stepik.org/course/154/syllabus

!Прежде чем пользоваться готовым репозиторием, попробуйте реализовать все сами :)!

Здесь будут разобраны возможные ошибки.

Для использования этого репозитория в качестве ответа введите в терминале Степика:

1)git clone https://github.com/MiraBlack/StepikNginx.git
2)cd StepikNginx
3)sudo sh init.sh

Готово! Можно отправлять.


Полезные команды и возможные ошибки:

sudo nginx -t - проверяет файл конфигурации на ошибки и выводит их. 

Возможные ошибки:

Наличие http или events блоков в файле конфига. Их быть не должно.

Ошибка Failed test #1. /home/box/web/public does not exists or not directory

Варианты:

-Была создана лишняя директория box: /home/box/box
-При копировании из ГитХаба не перенесли содержимое папки с названием вашего репозитория в \home\box, отчего имеем не
\home\box\web, а \home\box\ИмяВашегоРепозитория\web 

Ошибка <urlopen error [Errno 111] Connection refused>

В моем случае ошибка была в данной части конфиг-файла. За основу брался дефолтный конфиг по пути
/etc/nginx/sites-enabled/default (с помощью sudo vim default можно посмотреть и изменить его содержимое в ручную, дописав
location сюда, но это немного противоречит заданию).

server {
  listen 80 default_server;
  listen [::]:80 default_server ipv6only=on;
  
  root /usr/share/nginx/html;
  index index.html index.html;

 server_name localhost;

Ошибка Failed test #3. 10.42.103.127/js/test.js didn't returned 200

Варианты: 

-Неверное регулярное выражение 
-Не удалили ссылку на дефолтный конфиг по пути /etc/nginx/sites-enabled/
-Не сделали ссылку на Ваш написанный конфиг из /home/box/web/etc/nginx.conf к /etc/nginx/sites-enabled/ 

Ошибка Failed test #4. http://10.42.187.67/uploads/test.js didn't returned 200

-Неверное регулярное выражение 
-Неверно указан путь: 
 
Правильный путь:
    root   /home/box/web/ 


Чтобы возвращать 404, достаточно написать return 404;
--------------------------
Команды из init.sh (он для тех, кто не любит вводить все ручками)
sudo mv /home/box/StepikNginx/web ~ - переносим папку web в home
sudo ln -fs /home/box/web/etc/nginx.conf  /etc/nginx/sites-enabled/ - создаем ссылку на наш конфиг в папке, откуда он должен читаться
sudo rm -rf /etc/nginx/sites-enabled/default - удаляем ссылку на старый конфиг
sudo /etc/init.d/nginx restart - перезапускаем nginx



Хороший видеоурок по Git'y -https://www.youtube.com/watch?v=SEvR78OhGtw&t=4267s&ab_channel=АртемМатяшов
