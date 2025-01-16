# Отчёт по 4 практической работе
ББМО-02-23 Дурягин Михаил Романович
## Задание 1
Скачиваем, разворачиваем и проверяем ВМ :

![image](https://github.com/user-attachments/assets/0ae7b6fa-c117-484d-a28c-c727e7be4e5b)

Перейдём в директорию для первого задания:

![image](https://github.com/user-attachments/assets/247bbf85-d9ca-4a0a-9f7a-7487f8635aa3)

Выполним импорт с помощью rita:

Ы![image](https://github.com/user-attachments/assets/2a41e507-0872-4f13-8f39-5a0395c2bb21)

Удостоверимся, что в списке появилось название lab1:

![image](https://github.com/user-attachments/assets/e275b8f7-229a-41de-b0bd-8b5bf1013871)

Откроем lab1:

![image](https://github.com/user-attachments/assets/db7ef876-5796-4f51-9faa-74bee821cdb0)

Перейдём во вкладку beacons web, увидим 6 записей, которые набрали более 80 баллов:

![image](https://github.com/user-attachments/assets/90692689-77f4-4374-8ed1-15ddbf47c259)

Рассмотрим поподробнее эти 6 записей. 

В первой записи мы видим, что beacon score имеет большое значение. 
Агент пользователя - Windows 7, нет строки хоста, должно идентифицироваться полное доменное имя веб-сервера 
Кроме того, видно большое количество подключений за последние 24 часа - 3011.

Проанализируем вторую запись:

![image](https://github.com/user-attachments/assets/18637076-14c4-4523-9aba-4eacfb3ec364)

Во второй записи указан узел оптимизации доставки Microsoft. Для исправления ошибок используется Windows.
Сертификат выглядит легитимным. Таким образом, эту запись можно добавить в безопасный список. 

Проанализируем третью запись:

![image](https://github.com/user-attachments/assets/d41dd1f4-aef3-491f-8934-956f61acd902)

Здесь мы видим, что указан Windows title service, так что эту запись можно занести в безопасный список.

Остальные адреса также связаны с Windows, поэтому начнём добавление в safelist
Здесь мы также видим исправление ошибок Windows, поэтому можно также добавить в безопасный список.

Добавим безопасные записи в соответствующий список, также включим использование подстановочных знаков
(сюда входит array503, array506, array509):

![image](https://github.com/user-attachments/assets/57ce9b5a-f059-4ee9-b408-29532eb5fde9)

Далее добавим ещё две записи в безопасный список и отобразим все созданные правила:

![image](https://github.com/user-attachments/assets/4f0704aa-1aae-4b74-9e70-94f5f04938a4)

Откроем вкладку Longest Connection. Увидим, что для обоих записей не опеределён FQDN (ACH хранит FQDN 24 часа, 
а здесь после 24 часов оба имени помечены, как неизвестные):

![image](https://github.com/user-attachments/assets/4e9e08bc-bfd1-45e5-adf3-c96fd3e2d190)

Проверим эти адреса с помощью VirusTotal. Увидим, что вредоносов нет:

![image](https://github.com/user-attachments/assets/2164faa2-da14-449a-8fa8-eea9c231f38b)
![image](https://github.com/user-attachments/assets/2cf9ff41-1a98-40fc-983d-c028c0267ecc)

Вернёмся к самой первой записи (beacon score имеет значение 99,70%) и проанализируем её детальнее
(возможно здесь замешана угроза С2). Видим, что не происходил запрос FQDN перед подключением:

![image](https://github.com/user-attachments/assets/942b294a-1dd9-47fc-b275-a8c43644b269)

Если обратиться к логам HTTP, то можно заметить, что  FQDN отсутствует (вместо него адрес).
Кроме того, в качестве агента указан Windows 7, при этом видим FQDN, которые используются при работе windows 10, а не 7:

![image](https://github.com/user-attachments/assets/e4a4b8e6-86f5-4f27-bb19-43428aec187e)

Также можно заметить, что общение Windows 7 происходит только в одном случае (в других случаях используется Windows 10):

![image](https://github.com/user-attachments/assets/d779e492-a625-4162-ba52-f8546664334f)

Далее можно заметить, что 3011 соединений имеют одну и ту же ссылку.
Поэтому скорее всего это вредоностное подключение:

![image](https://github.com/user-attachments/assets/0b9be39b-1dae-49a6-a02c-8d758857b0c9)

## Задание 2
Импортируем данные для второго задания и откроем его.
На основной странице пусто, но система отсылается к модулю DNS:

![image](https://github.com/user-attachments/assets/7ee1ecc5-9d63-47ed-b902-eada8f9883ce)
![image](https://github.com/user-attachments/assets/32849629-aab6-433c-ae9b-6cc163278d0b)
![image](https://github.com/user-attachments/assets/c9aa25ce-3c25-4cdc-82a0-ff8c9466d901)

Здесь мы видим слишком большое количество уникальных записей - 2074. При этом пользователи не получают доступа к ресурсам:

![image](https://github.com/user-attachments/assets/174e61da-6c37-4a2a-aca2-aac62def9d74)

Кроме того, можно заметить, что имя хоста состоит из шестнадцетиричного кода, это очень странно, учитывая,
что мы обычно не используем такое при выдаче имени:

![image](https://github.com/user-attachments/assets/0658ab48-64de-4321-814d-2f6f16a6d1b0)

Таким образом, можно с уверенностью сказать, что это C2 через DNS.

## Задание 3
Импортируем данные для третьего задания и откроем его:

![image](https://github.com/user-attachments/assets/75cb60d7-e5af-4329-8c35-ce58ae106242)
![image](https://github.com/user-attachments/assets/101eddd4-9063-4e1d-8a9b-72fc1a624c49)

Зайдём в раздел beacons web. Рассмотрим пару записей из этого раздела.

Отобразим информацию по первой записи:

![image](https://github.com/user-attachments/assets/99eaa4f2-c49d-4a46-b03e-a22b43a44f58)

Заметим, что в данной записи используется домен Skype, но нельзя сказать, что он настоящий.
Также здесь указан internet explorer в качестве агента. Время ожидания соединения колеблется. 
Проверка на VirusTotal показывает, что здесь имеется вредонос:

![image](https://github.com/user-attachments/assets/af8b595b-919a-49a9-9cbe-693717d93b9e)

Таким образом, необходимо принять меры для устранения данного инцидента.

Отобразим информацию по второй записи.

![image](https://github.com/user-attachments/assets/a769d336-75b6-4837-8ca0-fd92ba2988d9)

Связан с microsoft, можно добавить в safelist

![image](https://github.com/user-attachments/assets/bbef767e-4c7c-4361-a7e4-d97c2e42c04c)

Вкладка длительных соединений идентична lab1. Следовательно, первый адрес вредоносный
