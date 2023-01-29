# АНАЛИЗ ДАННЫХ И ИСКУССТВЕННЫЙ ИНТЕЛЛЕКТ [in GameDev]
Отчет по лабораторной работе #2 выполнил(а):
- Лутков Евгений Александрович
- РИ210933
Отметка о выполнении заданий (заполняется студентом):

| Задание | Выполнение | Баллы |
| ------ | ------ | ------ |
| Задание 1 | * | 60 |
| Задание 2 | * | 20 |
| Задание 3 | * | 20 |

знак "*" - задание выполнено; знак "#" - задание не выполнено;

Работу проверили:
- к.т.н., доцент Денисов Д.В.
- к.э.н., доцент Панов М.А.
- ст. преп., Фадеев В.О.

[![N|Solid](https://cldup.com/dTxpPi9lDf.thumb.png)](https://nodesource.com/products/nsolid)

[![Build Status](https://travis-ci.org/joemccann/dillinger.svg?branch=master)](https://travis-ci.org/joemccann/dillinger)

Структура отчета

- Данные о работе: название работы, фио, группа, выполненные задания.
- Цель работы.
- Задание 1.
- Код реализации выполнения задания. Визуализация результатов выполнения (если применимо).
- Задание 2.
- Код реализации выполнения задания. Визуализация результатов выполнения (если применимо).
- Задание 3.
- Код реализации выполнения задания. Визуализация результатов выполнения (если применимо).
- Выводы.
- ✨Magic ✨

## Цель работы
Ознакомиться с основными операторами зыка Python на примере реализации линейной регрессии.

## Задание 1
### Реализовать совместную работу и передачу данных в связке Python - Google-Sheets – Unity.

При выполнении задания использовал видео-материалы и исходные данные, предоставленные преподавателями курса.

```py
import gspread
import numpy as np
gc = gspread.service_account(filename='unitydatasciense-376111-12b39e604d43.json')
sh = gc.open("UnitySheets")
price = np.random.randint(2000, 10000, 11)
mon = list(range(1,11))
i = 0
while i <= len(mon):
    i += 1
    if i == 0:
        continue
    else:
        tempInf = ((price[i-1]-price[i-2])/price[i-2])*100
        tempInf = str(tempInf)
        tempInf = tempInf.replace('.',',')
        sh.sheet1.update(('A'+ str(i)),str(i))
        sh.sheet1.update(('B' + str(i)), str(price[i-1]))
        sh.sheet1.update(('C' + str(i)), str(tempInf))
        print(tempInf)
```
Не получалось установить пакет gspread, но расправился с этой задачей запустив PyCharm через Anaconda
![image_2023-01-28_23-29-42](https://user-images.githubusercontent.com/113372135/215284891-279497b7-2635-44dd-b1cc-5602ceb1343f.png)

Вывод в Google Sheets:
![image_2023-01-28_23-58-06](https://user-images.githubusercontent.com/113372135/215286105-a945d753-1b71-4ea8-b278-a55510401dfb.png)

- Определите связанные функции. Функция модели: определяет модель линейной регрессии wx+b. Функция потерь: функция потерь среднеквадратичной ошибки. Функция оптимизации: метод градиентного спуска для нахождения частных производных w и b.
```
def model (a, b, x): # F Модели
    return a*x + b


def loss_function(a, b, x, y): # F потерь
    num = len(x)
    prediction = model (a,b,x)
    return (0.5/num) * (np.square(prediction-y)).sum()

def optimize(a,b,x,y):
    num=len(x)
    prediction = model(a,b,x)
    da = (1.0/num) * ( (prediction -y)*x).sum()
    db = (1.0/num) * ((prediction -y).sum())
    a = a - Lr*da
    b = b = Lr*db
    return a, b

def iterate(a, b, x, y, times) :
    for i in range(times):
        a,b = optimize(a,b,x,y)
    return a, b
```
![image_2023-01-27_14-33-09](https://user-images.githubusercontent.com/113372135/215065615-b4011654-a292-4052-9633-430943391eb2.png)

```
a = np.random.rand (1)
print(a)
b = np.random.rand(1)
print (b)
Lr = 0.00001

a,b = iterate(a,b,x,y,1)
prediction=model (a, b, x)
loss = loss_function(a, b, x, y)
print (a, b, loss)
plt.scatter(x, y)
plt.plot(x,prediction)
```
![image_2023-01-27_14-52-17](https://user-images.githubusercontent.com/113372135/215065787-493a0042-bbdb-4c33-ac24-0b608a83fb64.png)


## Задание 2
### Должна ли величина loss стремиться к нулю при изменении исходных данных? Ответьте на вопрос, приведите пример выполнения кода, который подтверждает ваш ответ.

При изменении исходных данных, loss не меняется.
![image_2023-01-27_14-52-17](https://user-images.githubusercontent.com/113372135/215066053-90dd6364-d89c-4560-b4af-7bf0c40d7dee.png)

## Задание 3
### Какова роль параметра Lr? Ответьте на вопрос, приведите пример выполнения кода, который подтверждает ваш ответ. В качестве эксперимента можете изменить значение параметра.

Параметр loss настраивает кривую, изменяя x и y. Так при меньшем loss, точность кривой упадёт.
![image_2023-01-27_15-09-43](https://user-images.githubusercontent.com/113372135/215066289-a473d4ed-bd03-4a17-9f62-a19738aafb01.png)
![image_2023-01-27_15-10-27](https://user-images.githubusercontent.com/113372135/215066297-1b829fa2-9e9c-4732-b7ce-c619e58cfebd.png)

## Выводы

Немного разобрался с использованием Unity, через муки и нервы настроил использование Unity и Jupiter. Ознакомился с линейной регрессией в python. 

| Plugin | README |
| ------ | ------ |
| Dropbox | [plugins/dropbox/README.md][PlDb] |
| GitHub | [plugins/github/README.md][PlGh] |
| Google Drive | [plugins/googledrive/README.md][PlGd] |
| OneDrive | [plugins/onedrive/README.md][PlOd] |
| Medium | [plugins/medium/README.md][PlMe] |
| Google Analytics | [plugins/googleanalytics/README.md][PlGa] |

## Powered by

**BigDigital Team: Denisov | Fadeev | Panov**
