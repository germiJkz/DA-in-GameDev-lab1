# АНАЛИЗ ДАННЫХ И ИСКУССТВЕННЫЙ ИНТЕЛЛЕКТ [in GameDev]
Отчет по лабораторной работе #2 выполнил(а):
- Трофимова Ольга Сергеевна
- РИ210930
Отметка о выполнении заданий (заполняется студентом):

| Задание | Выполнение | Баллы |
| ------ | ------ | ------ |
| Задание 1 | * | 60 |
| Задание 2 | # | 20 |
| Задание 3 | # | 20 |

знак "*" - задание выполнено; знак "#" - задание не выполнено;

Работу проверили:
- к.т.н., доцент Денисов Д.В.
- к.э.н., доцент Панов М.А.
- ст. преп., Фадеев В.О.

## Цель работы
познакомиться с программными средствами для организции
передачи данных между инструментами google, Python и Unity

## Задание 1
### Реализовать совместную работу и передачу данных в связке Python
- Google-Sheets – Unity. При выполнении задания используйте видео-материалы и
исходные данные, предоставленные преподавателя курса.
- В облачном сервисе google console подключить API для работы с google
sheets и google drive.
- Реализовать запись данных из скрипта на python в google-таблицу. Данные
описывают изменение темпа инфляции на протяжении 11 отсчётных периодов, с
учётом стоимости игрового объекта в каждый период.
- Создать новый проект на Unity, который будет получать данные из google-
таблицы, в которую были записаны данные в предыдущем пункте.
- Написать функционал на Unity, в котором будет воспризводиться аудио-
файл в зависимости от значения данных из таблицы.

Были повторены все действия из видео(смотри скриншоты ниже).
![image](https://user-images.githubusercontent.com/103726508/195164659-8fc248e1-9d1f-4dd5-a9ab-2ea9dbc15d25.png)
![image](https://user-images.githubusercontent.com/103726508/195164734-b783953e-0025-4fb2-8850-d8958588ac47.png)
![image](https://user-images.githubusercontent.com/103726508/195164789-cce2b144-d5f9-4503-ae0b-e2a3893c51f8.png)
![image](https://user-images.githubusercontent.com/103726508/195164951-30bd6d36-21c9-4a6d-8b14-247f8756c786.png)
![image](https://user-images.githubusercontent.com/103726508/195164998-53b4780c-0fc3-4eaa-8a4e-02b10fad06c4.png)
![image](https://user-images.githubusercontent.com/103726508/195165030-7324cc96-051c-4e0f-898e-663a40468683.png)


## Задание 2
### Реализовать запись в Google-таблицу набора данных, полученных
с помощью линейной регрессии из лабораторной работы № 1

В первой л.р. требовалось менять кол-во итераций от 1 до 5, и поменять на 10000. Кол-во итераций покащывается в первом столбце. После я меняю значение Lr и отображаю его значение в первом столбце Код, выполняющий эту задачу, и скрин таблицы приведёны ниже:
```py

import gspread
import numpy as np
gc = gspread.service_account(filename='pelagic-chalice-365213-f2071a548fdf.json')
sh = gc.open("UnitySheets")


def model(a, b, x):
    return a * x + b


def loss_function(a, b, x, y):
    num = len(x)
    prediction = model(a, b, x)
    return (0.5/num)*(np.square(prediction-y)).sum()


def optimize(a, b, x, y):
    num = len(x)
    prediction = model(a, b, x)
    da = (1.0/num) * ((prediction - y)*x).sum()
    db = (1.0/num) * ((prediction - y).sum())
    a = a - Lr*da
    b = b - Lr*db
    return a, b


def iterate(a, b, x, y, times):
    for i in range(times):
        a, b = optimize(a, b, x, y)
    return a, b


x = [3,21,22,34,54,34,55,67,89,99]
x = np.array(x)
y = [2,22,24,65,79,82,55,130,150,199]
y = np.array(y)
a = np.random.rand(1)
b = np.random.rand(1)
Lr = 0.000001
testing_n = [1, 2, 3, 4, 5, 10000]
i = 1
for n in testing_n:
    a, b = iterate(a, b, x, y, n)
    prediction = model(a, b, x)
    loss = loss_function(a, b, x, y)
    print(n, a, b, loss)
    sh.sheet1.update(('A' + str(i)), n)
    sh.sheet1.update(('B' + str(i)), str(a))
    sh.sheet1.update(('C' + str(i)), str(b))
    sh.sheet1.update(('D' + str(i)), str(loss))
    i += 1

testing_Lr = [0.00001, 0.0001, 0.001]
for lr in testing_Lr:
    Lr = lr
    a, b = iterate(a, b, x, y, 500)
    prediction = model(a, b, x)
    loss = loss_function(a, b, x, y)
    print(lr, a, b, loss)
    sh.sheet1.update(('A' + str(i)), lr)
    sh.sheet1.update(('B' + str(i)), str(a))
    sh.sheet1.update(('C' + str(i)), str(b))
    sh.sheet1.update(('D' + str(i)), str(loss))
    i += 1
```
![image](https://user-images.githubusercontent.com/103726508/195174891-519605eb-2269-47eb-be90-0ac835445cd7.png)


## Задание 3
### Самостоятельно разработать сценарий воспроизведения звукового
сопровождения в Unity в зависимости от изменения считанных данных в задании 2



## Выводы

В ходе Лабораторной работы №1 я познакомилась с основными операторами языка Python на примере реализации линейной линейной рагрессии, так же выяснила, что точность работы этого алгоритма не зависит от входных данных, но напрямую зависит от кол-ва итераций и значения параметра Lr (величины шага).
