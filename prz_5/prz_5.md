## ББМО-02-23 Дурягин Михаил Романович
## Практическая работа номер 5
-------------------------------------
# 1 этап
Wazuh сервер и агент уже установлены в прошлой практической работе.
# Настройка проверки целостности файлов

Добавление директорий и/или файлов в раздел «syscheck» в конфигурационный
файл агента /var/ossec/etc/ossec.conf или сервера (конфиг сервера имеет более
высокий приоритет);

![image](https://github.com/user-attachments/assets/1c7920da-b19b-4905-ab77-56f01ef79bc1)
![image](https://github.com/user-attachments/assets/acc9b2d1-2b65-4ba2-8df0-e285dcda00cd)

Далее директории появятся в разделе Integrity monitoring

![image](https://github.com/user-attachments/assets/d7feba44-d1a1-409f-8d68-0fb0ea296f36)

# Настройка выявления уязвимостей

Добавление раздела, отвечающего за syscollector в конфигурационный
файл агента или сервера /var/ossec/etc/shared/default/agent.conf

![image](https://github.com/user-attachments/assets/2a3b1aa9-5704-4a1a-aeab-b4279ce1f099)

Активация модуля детектора уязвимостей и указание операционных
систем агентов в конфигурационном файле сервера /var/ossec/etc/ossec.conf

![image](https://github.com/user-attachments/assets/eaee182d-134c-434e-85c8-f96d0192ef67)

Перезапуск сервиса агента и/или сервера для применения изменений.

![image](https://github.com/user-attachments/assets/8c3c60a9-b59c-4e23-96be-a12d87b47c84)

Теперь на сервере Wazuh будут генерироваться журналы с
оповещениями, которые содержат поля с описанием найденных уязвимостей.

# Настройка выявления скрытых процессов

Настройка конфигурационного файла агента /var/ossec/etc/ossec.conf с
целью уменьшения таймаута срабатывания рутчекера

![image](https://github.com/user-attachments/assets/5064c10a-f16a-4abb-a739-e7c8f33aca0f)

Далее необходимо перезапустить агента для применения изменений

![image](https://github.com/user-attachments/assets/5901485f-7d2c-412c-b806-7c4777ecab8f)

Эмуляция атаки
Представляет из себя следующий алгоритм:
Клонирование репозитория с руткитом

![image](https://github.com/user-attachments/assets/e9dffeb6-e093-4571-8713-548c1aea678d)

Компиляция руткита

![image](https://github.com/user-attachments/assets/724e7bf0-16e5-4756-9ca6-afbfc9b73fb5)

Загрузка руткита в ядро

![image](https://github.com/user-attachments/assets/76342d66-ce4f-4207-8839-183a4ff59cab)

Отправка сигнала KILL -63 со случайным PID для обнаружения руткита

![image](https://github.com/user-attachments/assets/298c7928-d769-48e2-bb64-3e4f67199926)

Создание скрытого процесса
Скроем процесс rsyslogd с помощью руткита. Для этого нужно отправить
сигнал KILL -31 с PID rsyslogd

![image](https://github.com/user-attachments/assets/1fe9db3f-0471-4ec9-a4cc-bd0ae04764fd)

Визуализация события.

![image](https://github.com/user-attachments/assets/0ff8f2e4-76ec-47fe-bad9-30052b188810)
![image](https://github.com/user-attachments/assets/6d1b86fa-cf7d-4181-9369-ef2a8a689df1)

# Настройка выявления SQL-инъекций

Установка веб-сервера

![image](https://github.com/user-attachments/assets/74d9f46b-fe5d-4ff5-a934-375e6d4778f2)

Активация и настройка фаервола

![image](https://github.com/user-attachments/assets/c4c71e96-2a21-4a17-abe0-b66734976d1b)

Настройка конфигурационного файла агента /var/ossec/etc/ossec.conf для
подключения веб-сервера к мониторингу, далее необходимо выполнить

![image](https://github.com/user-attachments/assets/4a8ec17d-b2ce-4e8d-9e15-26e08d42fc86)

Эмуляция атаки

![image](https://github.com/user-attachments/assets/3a4811ac-49d3-44f9-a83a-1498bf9e0f41)

Фиксация события

![image](https://github.com/user-attachments/assets/ec735095-344e-4e6f-8926-7efc6ec90572)

# Настройка выявления web shell attack
Настройка выявления web shell attack может быть проведена
следующими вариантами: 
- Использование Integrity monitoring (FIM) для обнаружения создания и
модификации файлов web shell;
- Использование кастомных правил Wazuh для обнаружения действий
- Использование мониторинга команд для отслеживания сетевых
подключений и попыток атак.

Установка Snort

![image](https://github.com/user-attachments/assets/8cf993b2-8b38-426c-a9db-4d158240365c)
![image](https://github.com/user-attachments/assets/9d6a6871-2001-4fc3-ae7d-afac8a62512b)

Подключим лог-файл с алертами Snort к Wazuh и перезагрузим сервер
Wazuh.

![image](https://github.com/user-attachments/assets/3d7c03ff-68ed-4adc-9265-b7d92ad6eef6)




















