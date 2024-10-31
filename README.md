# Практическая работа №3 WAZUH
## Выполнил студент группы ББМО-02-23 Васильев Г.М.

### 1. Разворачиваю виртуальную машину на базе ОС Ubuntu
![image](https://github.com/Archangel15520/sssl3/blob/main/screenshot/1.JPG)

### 2. Настраиваю на всех виртуальных машинах сетевой мост, чтобы они друг друга видели. 
![image](https://github.com/Archangel15520/sssl3/blob/main/screenshot/2.JPG)

### 3. Захожу на обе виртуальные машины и пингую друг друга для проверки соединения.  
![image](https://github.com/Archangel15520/sssl3/blob/main/screenshot/3.JPG)

### 4. Начинаю установку сервера Wazuh на первую хост виртуальную машину.
Команда: "curl -sO https://packages.wazuh.com/4.7/wazuh-install.sh && sudo bash ./wazuh-install.sh -a"
![image](https://github.com/Archangel15520/sssl3/blob/main/screenshot/4.JPG)

### 5. После установки также получаю логин и пароль ко входу в личный кабинет сервера.
![image](https://github.com/Archangel15520/sssl3/blob/main/screenshot/5.JPG)

### 6. Перехоим в браузер и вписываем наш ip адрес с портом который фигурировал в логах установки (по умолчанию 443). После захода на страницу вписываем наши логин и пароль. 
Пример: "https://10.0.2.15:443"
![image](https://github.com/Archangel15520/sssl3/blob/main/screenshot/6.JPG)

### 7. Попадаем на главный экран wazuh server.
![image](https://github.com/Archangel15520/sssl3/blob/main/screenshot/7.JPG)

### 8. Теперь надо дать доступ второй виртуальной машине, чтобы сделать её агентом на сервере. 
Для этого перехоим во вкладку agent.
![image](https://github.com/Archangel15520/sssl3/blob/main/screenshot/8.JPG)

### 9. Выбрав все необходимые настройки получаем сформированную команду для добавления её во вторую виртуальную машину. 
![image](https://github.com/Archangel15520/sssl3/blob/main/screenshot/9.JPG)
![image](https://github.com/Archangel15520/sssl3/blob/main/screenshot/10.JPG)

### 10. Далее я тестировал возможности атакна на сервер, агента и взял для примера из анонимных источников хакерские программы для DDoS атаки на ip адреса или конкретные ссылки. 
Впримере использую программу HOIC и LOIC. 
![image](https://github.com/Archangel15520/sssl3/blob/main/screenshot/11.JPG)
![image](https://github.com/Archangel15520/sssl3/blob/main/screenshot/12.JPG)

### 11. Настроив свои программы на атаку и активировав их я положил сервер полностью.
Я немного переборщил и в настройках утилит слишком сильную атакаху назначил, в плане колличества пакетов отправляемых на мой адрес и скорости их отправки. В итоге, вместо небольших аномалий я обвалил сервер с критическими ошибками, которые было трудно исправить.
![image](https://github.com/Archangel15520/sssl3/blob/main/screenshot/13.JPG)
![image](https://github.com/Archangel15520/sssl3/blob/main/screenshot/14.JPG)
![image](https://github.com/Archangel15520/sssl3/blob/main/screenshot/15.JPG)

### 12. Далее я начал выявлять критические ошибки и пытаться их устранить для повторного запуска. 
Не успел запечатлеть в полной мере, потому что машинально по ходу исправления перезапустил виртуальную машину. 
А так использовал команды для выявления логов, захода в конфигурационные файлы и команды на запуск сервиса во преки некоторым оставшимся не критическим ошибкам, из за которых он не хотел запускаться пока они действительны.  
Вот несколько команд в пример: 
"sudo /var/ossec/bin/wazuh-control check" - команда для проверки на ошибки, "sudo systemctl status wazuh-manager.service"- команда для просмотра статуса сервера и краткой истории важных действий, "nano /var/ossec/etc/ossec.conf" - команда для изменения кофигурационных файлов запуска сервера, а также для агента, "sudo /var/ossec/bin/wazuh-control start" - команда для принудительного запуска скрипта конфигурационных фалов сервера.
![image](https://github.com/Archangel15520/sssl3/blob/main/screenshot/16.JPG)

### 13. После перезапуска мне удалось зайти на свой сервер и увидеть очень большую историю действий с попытками повторного входа, которая сменяется на непонятную ошибку в понимании самим сервером. 
![image](https://github.com/Archangel15520/sssl3/blob/main/screenshot/18.JPG)

### 13. Не смог найти внятную ошибку в dashboard истории действий, во время которой происходила моя ddos атака. На картинке ниже нашел одну из нескольких ошибкок с большим уровням атаки для пирмера. 
Видимо он не смог внятно понять что происходит и сразу отрубился.
![image](https://github.com/Archangel15520/sssl3/blob/main/screenshot/19.JPG)
