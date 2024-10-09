## Практика №1
## Сетевая связанность обеспечена, установил и настроил rsyslog
![image](https://github.com/kiberbull/TOIB/assets/65900037/8c90e248-b699-465c-90ee-5fc6d038816c)
![image](https://github.com/kiberbull/TOIB/assets/65900037/8a2e9721-d64f-4961-9ee5-fc21075fe257)
![image](https://github.com/kiberbull/TOIB/assets/65900037/c220cdbc-df84-4563-b872-4b60a67c135c)


![image](https://github.com/kiberbull/TOIB/assets/65900037/b3a3767b-ef05-490a-8ce4-04b1b47d85d7)

## Вторая машина 
![image](https://github.com/kiberbull/TOIB/assets/65900037/20b20d48-6121-45e6-86e9-7e95954aaa9b)
![image](https://github.com/kiberbull/TOIB/assets/65900037/03d312df-a566-43bf-8986-8f1216568ca4)
![image](https://github.com/kiberbull/TOIB/assets/65900037/22920e39-5cb3-4b9f-8f54-86ecf40c1adf)
## Скачиваем и настроиваем loki на сервере
![image](https://github.com/kiberbull/TOIB/assets/65900037/34593bd9-0782-4790-b3f9-2531cd0ba2ba)
## Скачиваем и настроиваем promtail на клиенте
![image](https://github.com/kiberbull/TOIB/assets/65900037/c503610a-1797-4aeb-9bb7-80bee92b07b4)
## Grafana Loki Загрузка compose-файла Loki
    wget https://raw.githubusercontent.com/grafana/loki/v2.9.1/production/docker-compose.yaml
## Запуск Loki
    sudo docker-compose up -d
    [+] Building 0.0s (0/0)
    [+] Running 3/3
    • Network loki_loki
    Created
    • Container loki-grafana-1
    Started
    • Container loki-loki-1
    Started
