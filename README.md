# АНАЛИЗ ДАННЫХ И ИСКУССТВЕННЫЙ ИНТЕЛЛЕКТ [in GameDev]
Отчет по лабораторной работе #1 выполнил(а):
- Трофимова Ольга Сергеевна
- РИ210930
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

## Цель работы
Ознакомиться с основными операторами языка Python на примере реализации линейной регрессии.

## Задание 1
### Написать программы Hello Wold на Python и Unity
- Для Python в отчёте привести скриншоты с демострацией сохранения докумета google.colab на свой диск с запуском программы, выводящей Hello World.
- Для Unity в отчёте привести скриншоты вывод сообщения Hello World в консоль.

Hello Wold на Python см. рис. 1-3, 

Hello Wold на Unity см. рис. 4-5

Рис. 1:
![image](https://user-images.githubusercontent.com/103726508/192154249-48425269-17d5-4698-926a-36006d2378fc.png)

Рис. 2:
![image](https://user-images.githubusercontent.com/103726508/192154329-49737b79-ced4-4cdc-bfae-7cf21667b2d4.png)

Рис. 3:
![image](https://user-images.githubusercontent.com/103726508/192154350-da65cac7-8e5d-4374-8324-cc23ae468e6c.png)

Рис. 4:
![image](https://user-images.githubusercontent.com/103726508/192154367-b50a9ca4-489f-4ec5-9c52-5fd0d1067075.png)

Рис. 5:
![image](https://user-images.githubusercontent.com/103726508/192154384-594ac67c-3cf2-47aa-9a68-cab8398ad7c3.png)

## Задание 2
### Пошагово выполнить каждый пункт раздела "ход работы" с описанием и примерами реализации задачи по теме лабораторной работы
Ход работы:
- Произвести подготовку данных для работы с алгоритмом линейной регрессии. 10 видов данных были установлены случайным образом, и данные находились в линейной зависимости. Данные преобразуются в формат массива, чтобы их можно было вычислить напрямую при использовании умножения и сложения.

```py

#Import the required modules, numpy for calculation, and Matplotlib for drawing
import numpy as np
import matplotlib.pyplot as plt
#This code is for jupyter Notebook only
%matplotlib inline

# define data, and change list to array
x = [3,21,22,34,54,34,55,67,89,99]
x = np.array(x)
y = [2,22,24,65,79,82,55,130,150,199]
y = np.array(y)

#Show the effect of a scatter plot
plt.scatter(x,y)

```

- Определите связанные функции. Функция модели: определяет модель линейной регрессии wx+b. Функция потерь: функция потерь среднеквадратичной ошибки. Функция оптимизации: метод градиентного спуска для нахождения частных производных w и b.

```py

#The basic linear regressiion model is wx+ b? and since this is a two-dimensional space? the model is ax+ b
def model(a, b, x):
    return a * x +b

#Tahe most commonly used loss function of linear regression model is the loss function of mean variance difference
def loss_function(a, b, x, y):
    num = len(x)
    prediction =model(a, b, x)
    return (0.5/num)*(np.square(prediction-y)).sum()

#The optimization function mainly USES partial derivatives to update two parameters a and b
def optimize(a, b, x, y):
    num = len(x)
    prediction = model(a, b, x)
    da = (1.0/num) * ((prediction - y)*x).sum()
    db = (1.0/num) * ((prediction - y).sum())
    a = a - Lr*da
    b = b - Lr*db
    return a, b

#iterated function? return a and b
def iterate(a, b, x, y, times):
    for i in range(times):
        a,b=optimize(a, b, x, y)
    return a,b
```
- Начать итерацию
```py

#Initialize parameters and display
a = np.random.rand(1)
print(a)
b = np.random.rand(1)
Lr = 0.01
#For the first iteration, the parameter values, losses, and visualization after the iteration and displayed
a,b = iterate(a,b,x,y,1)
prediction=model(a,b,x)
loss = loss_function(a,b,x,y)
print(a,b,loss)
plt.scatter(x,y)
plt.plot(x, prediction)

```
- несколько раз запустить программу меняя кол-во итераций последовательно от 1 до 5, а после поменять на 1 000. В консоли отобразятся значения параметров, значения потерь и эффекты визуализации после итерации.

Ответ: для наглядности в конец программы была добавлена строка, выводящая график в отдельное окно:
```py

plt.show()

```
Результаты выполнения программы см. на Рис. 6-12

Рис. 6:
![image](https://user-images.githubusercontent.com/103726508/192155740-d59de2bc-bc52-4fa5-bb30-a4873961c91f.png)

Рис. 7:
![image](https://user-images.githubusercontent.com/103726508/192155749-aa95c474-7416-4a50-b329-89aaa57512c3.png)

Рис. 8:
![image](https://user-images.githubusercontent.com/103726508/192155763-ea4ddde2-83b8-4e36-aea2-f981053e4679.png)

Рис. 9:
![image](https://user-images.githubusercontent.com/103726508/192155777-f20c93c0-3dd8-4e09-8ca4-075cf2fcb864.png)

Рис. 10:
![image](https://user-images.githubusercontent.com/103726508/192155790-635bdf9c-f883-49cc-96f4-355c5a10c010.png)

Рис. 11:
![image](https://user-images.githubusercontent.com/103726508/192155799-5241b24c-b8e6-4455-9498-84a60bf3869e.png)

Рис. 12:
![image](https://user-images.githubusercontent.com/103726508/192155813-09632a7a-59fa-4c35-bb89-7dcdd90f2811.png)



## Задание 3
### Изучить код на Python и ответить на вопросы:
- Должна ли величина loss стремиться к нулю при изменении исходных данных? Ответьте на вопрос, приведите пример выполнения кода, который подтверждает ваш ответ.

Ответ: нет, т. к. даже на самых подходящих данных ( я взяла 10 точек, точно лежащих на прямой y=2x+0) алгоритм не работает достаточно корректно(см. рис. 13). 

Я поменяла кол-во итераций на 1 000 000 и график стал более корректным (см. Рис. 14). Величина loss значительно уменьшилась. 

Поэтому можно сделать вывод, что величина loss скорее зависит от кол-ва итераций, чем от входных данных.

Рис. 13:
![image](https://user-images.githubusercontent.com/103726508/192155957-4828c6a3-06e7-4a73-9275-77deca238474.png)

Рис. 14:
![image](https://user-images.githubusercontent.com/103726508/192156260-ba85adaa-7b44-4144-93eb-68f6ec60dca1.png)

- Какова роль параметра Lr? Ответьте на вопрос, приведите пример выполнения кода, который подтверждает ваш ответ. В качестве эксперимента можете изменить значение параметра.

Ответ: параметр Lr определяет некоторую ширину шага, с которой алгоритм подбирает параметры. 
Если параметр увеличить в 10 раз(см. Рис. 15), в 100 раз(см. Рис. 16) и в 10 000 раз(см. Рис. 17), то при сравнении с изначальным значением(см. Рис. 13) отчётливо видна разница в точности работы алгоритма. 

Замечу, что запуски осуществлялись на самых подходящих данных (см. предыдущий вопрос) и на одинаковом кол-ве итераций (1 000), чтобы не влиять на результат.

Так же стоит заметить, что даже за небольшое кол-во итераций (5) результат становится достаточно корректным при Lr в 10 000 большем, чем изначальное занчение(см. Рис. 19).

Рис. 15: 
![image](https://user-images.githubusercontent.com/103726508/192156285-851811f9-9c2d-4e0f-97bb-3645a99a271b.png)

Рис. 16:
![image](https://user-images.githubusercontent.com/103726508/192156299-d557de9c-72bb-45d9-a6e7-005f88023e1b.png)

Рис. 17:
![image](https://user-images.githubusercontent.com/103726508/192156306-1371508b-033e-41ef-92aa-64ab8b86026b.png)

Рис. 18:
![image](https://user-images.githubusercontent.com/103726508/192156319-4a86bca8-6e98-4039-b17f-1fe255ea7bd1.png)

Рис. 19:
![image](https://user-images.githubusercontent.com/103726508/192156703-fdcd5d82-dd00-4006-8379-f0d895aed48c.png)

## Выводы

В ходе Лабораторной работы №1 я познакомилась с основными операторами языка Python на примере реализации линейной линейной рагрессии, так же выяснила, что точность работы этого алгоритма не зависит от входных данных, но напрямую зависит от кол-ва итераций и значения параметра Lr (величины шага).
