## Вариант 5 HPC
# Клонирование репозитория с логами

```python
!git clone https://github.com/logpai/loghub.git
```

    Cloning into 'loghub'...
    remote: Enumerating objects: 575, done.[K
    remote: Counting objects: 100% (171/171), done.[K
    remote: Compressing objects: 100% (39/39), done.[K
    remote: Total 575 (delta 145), reused 135 (delta 132), pack-reused 404 (from 1)[K
    Receiving objects: 100% (575/575), 7.27 MiB | 14.52 MiB/s, done.
    Resolving deltas: 100% (267/267), done.
    
# Переход в директорию с логами HPC


```python
%cd loghub/HPC
```

    /home/parallels/Desktop/SSSL/loghub/HPC


    /usr/lib/python3/dist-packages/IPython/core/magics/osm.py:417: UserWarning: using dhist requires you to install the `pickleshare` library.
      self.shell.db['dhist'] = compress_dhist(dhist)[-100:]

# Получение списка всех файлов логов в папке:

```python
import os

# Получить список всех файлов логов в текущей директории
log_files = [file for file in os.listdir() if file.endswith('.log')]
print("Найденные файлы логов:", log_files)
```

    Найденные файлы логов: ['HPC_2k.log']
# Парсинг логов


```python
import re
import pandas as pd

# Путь к файлу логов
log_file_path = 'HPC_2k.log'

# Список для хранения результатов парсинга
parsed_logs = []

# Регулярное выражение для текущего формата строк логов
regex_pattern = r"(\d+)\s+(\w+-\d+)\s+([\w\.]+)\s+([\w\.]+)\s+\d+\s+.*\(HWID=(\d+)\)"

# Чтение файла и парсинг строк
with open(log_file_path, 'r') as file:
    for line in file:
        match = re.search(regex_pattern, line)
        if match:
            parsed_logs.append({
                'id': match.group(1),
                'node': match.group(2),
                'component': match.group(3),
                'state': match.group(4),
                'hwid': match.group(5)
            })

# Преобразование в DataFrame
logs_df = pd.DataFrame(parsed_logs)
logs_df.head()
```

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>id</th>
      <th>node</th>
      <th>component</th>
      <th>state</th>
      <th>hwid</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>134681</td>
      <td>node-246</td>
      <td>unix.hw</td>
      <td>state_change.unavailable</td>
      <td>1973</td>
    </tr>
    <tr>
      <th>1</th>
      <td>350766</td>
      <td>node-109</td>
      <td>unix.hw</td>
      <td>state_change.unavailable</td>
      <td>3180</td>
    </tr>
    <tr>
      <th>2</th>
      <td>344518</td>
      <td>node-246</td>
      <td>unix.hw</td>
      <td>state_change.unavailable</td>
      <td>5089</td>
    </tr>
    <tr>
      <th>3</th>
      <td>344448</td>
      <td>node-153</td>
      <td>unix.hw</td>
      <td>state_change.unavailable</td>
      <td>4088</td>
    </tr>
    <tr>
      <th>4</th>
      <td>366633</td>
      <td>node-200</td>
      <td>unix.hw</td>
      <td>state_change.unavailable</td>
      <td>2538</td>
    </tr>
  </tbody>
</table>
</div>





Сохранение данных в CSV


```python
logs_df.to_csv('parsed_hpc_logs.csv', index=False)
print("Данные сохранены в 'parsed_hpc_logs.csv'")
```

    Данные сохранены в 'parsed_hpc_logs.csv'



```python
# Анализ распределения значений для столбца 'node'
node_counts = logs_df['node'].value_counts()
print("Distribution for 'node':")
print(node_counts)
print("\n" + "="*50 + "\n")

# Анализ распределения значений для столбца 'component'
component_counts = logs_df['component'].value_counts()
print("Distribution for 'component':")
print(component_counts)
print("\n" + "="*50 + "\n")

# Анализ распределения значений для столбца 'state'
state_counts = logs_df['state'].value_counts()
print("Distribution for 'state':")
print(state_counts)
```

    Distribution for 'node':
    node
    node-246    2
    node-109    1
    node-153    1
    node-200    1
    node-122    1
    node-228    1
    node-10     1
    node-130    1
    node-169    1
    node-187    1
    node-199    1
    Name: count, dtype: int64
    
    ==================================================
    
    Distribution for 'component':
    component
    unix.hw    12
    Name: count, dtype: int64
    
    ==================================================
    
    Distribution for 'state':
    state
    state_change.unavailable    12
    Name: count, dtype: int64




Построение таблицы


```python
import pandas as pd

# Создание таблицы распределения значений для столбцов 'node', 'component', и 'state'
summary_data = {
    'node': logs_df['node'].value_counts(),
    'component': logs_df['component'].value_counts(),
    'state': logs_df['state'].value_counts()
}

# Преобразование в DataFrame
summary_df = pd.DataFrame.from_dict(summary_data, orient='index').transpose()

# Отображение таблицы
print("Сводная таблица для столбцов логов HPC:")
print(summary_df)


```

    Сводная таблица для столбцов логов HPC:
                              node  component  state
    node-246                   2.0        NaN    NaN
    node-109                   1.0        NaN    NaN
    node-153                   1.0        NaN    NaN
    node-200                   1.0        NaN    NaN
    node-122                   1.0        NaN    NaN
    node-228                   1.0        NaN    NaN
    node-10                    1.0        NaN    NaN
    node-130                   1.0        NaN    NaN
    node-169                   1.0        NaN    NaN
    node-187                   1.0        NaN    NaN
    node-199                   1.0        NaN    NaN
    unix.hw                    NaN       12.0    NaN
    state_change.unavailable   NaN        NaN   12.0

# Построение графиков для столбцов node, component, и state:

```python
# Создание графиков для каждого категориального столбца

# Распределение значений для столбца 'node'
node_counts = logs_df['node'].value_counts()
plt.figure(figsize=(10, 6))
node_counts.plot(kind='bar')
plt.xlabel('Node')
plt.ylabel('Count')
plt.title('Distribution of Node')
plt.xticks(rotation=45)
plt.tight_layout()
plt.show()

# Распределение значений для столбца 'component'
component_counts = logs_df['component'].value_counts()
plt.figure(figsize=(10, 6))
component_counts.plot(kind='bar')
plt.xlabel('Component')
plt.ylabel('Count')
plt.title('Distribution of Component')
plt.xticks(rotation=45)
plt.tight_layout()
plt.show()

# Распределение значений для столбца 'state'
state_counts = logs_df['state'].value_counts()
plt.figure(figsize=(10, 6))
state_counts.plot(kind='bar')
plt.xlabel('State')
plt.ylabel('Count')
plt.title('Distribution of State')
plt.xticks(rotation=45)
plt.tight_layout()
plt.show()
```


    
![prz_2_14_0](https://github.com/user-attachments/assets/6cba79cd-da5c-4afc-8618-99c2e090320a)

![prz_2_14_1](https://github.com/user-attachments/assets/1b63b872-2f42-4465-9fd4-179f17f6d142)

![prz_2_14_2](https://github.com/user-attachments/assets/290cf286-8edf-4d75-9308-715e434464cf)




```python
plt.savefig('State_distribution.png')
print("График сохранён в 'State_distribution.png'")
```
    График сохранён в 'State_distribution.png'
    <Figure size 640x480 with 0 Axes>



<img width="879" alt="image" src="https://github.com/user-attachments/assets/54552e90-0016-4596-a7db-eda310df51bd">

<img width="929" alt="image" src="https://github.com/user-attachments/assets/0a2ddd31-b09e-48cb-98e8-064033471297">

<img width="933" alt="image" src="https://github.com/user-attachments/assets/71e64345-2638-47cc-8f7c-70736f2ee432">

<img width="926" alt="image" src="https://github.com/user-attachments/assets/7eb78ea1-7163-4c5c-bc57-1a0787fcb8aa">

<img width="895" alt="image" src="https://github.com/user-attachments/assets/3926b6ea-44a1-497d-a822-15c92f73b390">




