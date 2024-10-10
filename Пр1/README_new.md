# Шаг 1: Установка и настройка rsyslog
Установил rsyslog на 1-ю ВМ

![image](https://github.com/user-attachments/assets/4f1d8076-e24b-41eb-8b1f-dffe1dc81872)

Настройка клиента Rsyslog для отправки логов на центральный сервер (1 ВМ)

![image](https://github.com/user-attachments/assets/21a6cdd0-856a-420c-84f8-ec51b89af991)

Настройка центрального сервера Rsyslog (2 ВМ)

![image](https://github.com/user-attachments/assets/6378289c-d968-4afe-87b2-3808b2000a5a)

![image](https://github.com/user-attachments/assets/5f69519e-1268-4577-8382-2905543b4eb8)

Проверка соединения - приходят ли логи на сервер

![image](https://github.com/user-attachments/assets/6fb26cab-03ae-40cc-9a0e-bb14c046e977)

#Шаг 2 установка и настройка loki
Установка Loki и создание файла конфигурации

![image](https://github.com/user-attachments/assets/92f42a18-ea8e-4b0d-a484-6d2c621e054e)

![image](https://github.com/user-attachments/assets/949c2dad-8871-4399-b00e-0b118a7dbd6f)

Делаем сервис для loki

![image](https://github.com/user-attachments/assets/25e7b057-3038-44b5-b5cd-73975387f860)

![image](https://github.com/user-attachments/assets/016983d6-e265-4bb9-a9bf-9306ba845fb4)

Загрузил модуль omhttp для Rsyslog

![image](https://github.com/user-attachments/assets/d6bc6c47-caad-4e0f-a7c1-51470df32914)

Настроил локи и подключил к Grafana

![image](https://github.com/user-attachments/assets/d7db7956-4114-408f-914f-434709cff521)

![image](https://github.com/user-attachments/assets/03eeb5a8-dd7e-4225-89db-4658ac86f6d9)
