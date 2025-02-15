# АНАЛИЗ ДАННЫХ И ИСКУССТВЕННЫЙ ИНТЕЛЛЕКТ [in GameDev]
Отчет по лабораторной работе #3 выполнил(а):
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
познакомиться с программными средствами для создания
системы машинного обучения и ее интеграции в Unity.

## Постановка задачи
В данной лабораторной работе мы создадим ML-агент и будем тренировать
нейросеть, задача которой будет заключаться в управлении шаром. Задача шара
заключается в том, чтобы оставаясь на плоскости находить кубик, смещающийся в
заданном случайном диапазоне координат.

## Задание 1
### Реализовать систему машинного обучения в связке Python - Google-Sheets – Unity.
При выполнении задания можно использовать видео-
материалы и исходные данные, предоставленные преподавателями курса.
Создайте новый пустой 3D проект на Unity.
Скачайте папку с ML агентом. Вы найдете ее в облаке с исходными
файлами к лабораторной работе – ml-agents-release_19.
В созданный проект добавьте ML Agent, выбрав Window - Package
Manager - Add Package from disk. Последовательно добавьте .json –
 -  ml-agents-release_19 / com,unity.ml-agents / package.json
 -  ml-agents-release_19 / com,unity.ml-agents.extensions / package.json
Если все сделано правильно, то во вкладке с компонентами
(Components) внутри Unity вы увидите строку ML Agent.
Далее запускаем Anaconda Prompt для возможности запуска команд
через консоль.
Далее пишем серию команд для создания и активации нового ML-
агента, а также для скачивания необходимых библиотек:
 -  mlagents 0.28.0;
 -  torch 1.7.1;
 -  Создайте на сцене плоскость, куб и сферу так, как показано на рисунке
ниже. Создайте простой C# скрипт-файл и подключите его к сфере.
 - В скрипт-файл RollerAgent.cs добавьте код, опубликованный в
материалах лабораторных работ – по ссылке.
Объекту «сфера» добавить компоненты Rigidbody, Decision Requester,
Behavior Parameters и настройте их так, как показано на рисунке ниже.
 - В корень проекта добавьте файл конфигурации нейронной сети,
доступный в папке с файлами проекта по ссылке.
 - Pапустите работу ml-агента.
 - Вернитесь в проект Unity, запустите сцену, проверьте работу ML-
Agent’a.
 - Сделайте 3, 9, 27 копий модели «Плоскость-Сфера-Куб», запустите
симуляцию сцены и наблюдайте за результатом обучения модели.
 - После завершения обучения проверьте работу модели.
 - Сделайте выводы.


Было создано рабочее простанство и подключены соответсвующие библиотеки:
![image](https://user-images.githubusercontent.com/103726508/204106783-0e4aea20-2d40-4302-9ac5-fb6cb49fcaae.png)
![image](https://user-images.githubusercontent.com/103726508/204106793-e7d129b8-a7a0-4a23-8e7f-b49a5acec8bc.png)
![image](https://user-images.githubusercontent.com/103726508/204106805-9f7b6e62-937b-41ef-9d5c-ab0c8594270b.png)

В Unity был создан проект:
![image](https://user-images.githubusercontent.com/103726508/204106773-5aaddfc4-a2ce-4d34-b91e-2428537ae4e1.png)

Написан код:
![image](https://user-images.githubusercontent.com/103726508/201184576-5d62cdb0-540b-477d-ba66-439811ce3ad7.png)
![image](https://user-images.githubusercontent.com/103726508/201184598-a7e28295-1b24-406c-86ab-6be24a48bff1.png)

Было начато обучение:
![image](https://user-images.githubusercontent.com/103726508/204106987-8e9f541c-4388-4e83-bb35-fe6ad1d27ae3.png)
![image](https://user-images.githubusercontent.com/103726508/204148572-2944a2db-8068-40ca-9af6-85bde6fd11f9.png)

Но один шар обучается очень долго, поэтому количество площадок было постепенно увеличено до 64:
![image](https://user-images.githubusercontent.com/103726508/204148845-75d186c2-400c-42ce-828b-88e245be5f43.png)
![image](https://user-images.githubusercontent.com/103726508/204149517-04c66329-1793-49ee-8352-6449c67d29a0.png)
![image](https://user-images.githubusercontent.com/103726508/204149771-91df2911-af2c-48b7-9870-2d4392c6eff5.png)
![image](https://user-images.githubusercontent.com/103726508/204150250-b4851d05-2765-4b49-b032-8faa9dce803d.png)

На скринах видно, что все они обучаются:
![image](https://user-images.githubusercontent.com/103726508/204150494-626c9b20-55d5-4854-9010-7b7e8323434a.png)
![image](https://user-images.githubusercontent.com/103726508/204150553-f2b90bd4-b6fc-4e34-8b1d-ddbae5a6941d.png)
![image](https://user-images.githubusercontent.com/103726508/204150669-b581ee36-bc88-4920-8ab2-16c1571ea7cf.png)

После завершения обучения, полученную модель поведения присвоили одному из шаров(остальные скрыли):
![очень короткий](https://user-images.githubusercontent.com/103726508/204151843-91b61775-1cb2-40e4-af9e-82072978d8e2.gif)

Видно, что обучение прошло хорошо, шарик четко катится к кубику, хоть иногда и падает с площадки.

## Задание 2

Подробно опишите каждую строку файла конфигурации
нейронной сети, доступного в папке с файлами проекта по ссылке. Самостоятельно
найдите информацию о компонентах Decision Requester, Behavior Parameters,
добавленных на сфере.

![image](https://user-images.githubusercontent.com/103726508/204106896-8a476e07-8e9a-4ab3-9eae-6fa18137e65a.png)


behaviors: описание поведения объекта

RollerBall: имя объекта

trainer_type: тип используемого для обучения тренажёра, здесь обучение с поощрением

hyperparameters: группировка параметров, отвечающих за управления процессом обучения

batch_size: количество опытов на каждой итерации градиентного спуска

buffer_size: количество опыта, которое нужно собрать для обновления итерации или её изучения

learning_rate: изменение скорости обучения модели с течением времени

beta: сила регуляризации энтропии, которая делает политику "более случайной". Это гарантирует, что агенты должным образом исследуют пространство действий во время обучения. Увеличение этого параметра обеспечит выполнение большего количества случайных действий

epsilon: параметр влияющий на быстроту развития (ускорения работы) системы с каждой итерацией

lambd: параметр оценивающий совпадение стоимости вознаграждения обучений между собой (что то вроде погрешности), чем стабильнее значения, тем быстрее идёт процесс.

num_epoch: количество проходов через буфер опыта при выполнении оптимизации градиентного спуска (чем больше, тем быстрее итерация и наоборот)

learning_rate_schedule: скорость обучения, которая в нашем случае уменьшается линейно до нуля.

normalize: отвечает за то будут ли нормироваться (усредняться) входные данные 

network_settings: группировка параметров, отвечающих за обучение сети

hidden_units: количество значений в подключенном слое нейронной сети (то есть чем больше будет поток входных данных, тем больше нужно ввести значения параметра и наоборот).

num_layers: количество скрытых слоев в нейронной сети(число слоёв, принимающих на себя работу, чем сложнее задача, тем больше нужно слоёв)

reward_signals: раздел позволяющий задавать настройки как для внешних, так и для внутренних сигналов вознаграждения

extrinsic: внешний сигнал из reward_signals

gamma: параметр, отвечающий за то, насколько далеко вперёд должен думать о вознаграждении агент. Должен быть в состоянии подготовиться – выделить объём места и т.д.

strength: коэффициент, на который умножается вознаграждение, предоставляемое средой. Благодаря этому параметру можно увеличивать или уменьшать количество поступаемой валюты

max_steps: общее количество шагов-действий, которые должны быть выполнены в среде до завершения процесса обучения

time_horizon: сколько опыта нужно собрать перед тем, как добавить в буфер. Также используется, как среднее значение для общего ожидаемого вознаграждения

summary_freq: количество опыта, которое необходимо собрать перед созданием и отображением статистики обучения

Decision Requester: компонент, автоматически запрашивающий решение с постоянным интервалом времени. То есть он отвечает за принятие решения в цикле: наблюдение-принятия решения-действие-вознаграждение.

Behavior Parameters: компонент, выполняющий функции настройки поведения агента (генерирует объекты и их свойства согласно заданным параметрам).

## Задание 3
Доработайте сцену и обучите ML-Agent таким образом, чтобы шар
перемещался между двумя кубами разного цвета. Кубы должны, как и в первом
задании, случайно изменять координаты на плоскости.

Был создан соответствующий проект в Unity:
![image](https://user-images.githubusercontent.com/103726508/204352554-d74afdf1-8ecd-4685-90ae-0935821d372d.png)

Код был изменён под 2 цели вот таким образом:
![image](https://user-images.githubusercontent.com/103726508/204379676-d6c612e5-2256-4afb-b3f3-6c4d827053f4.png)
![image](https://user-images.githubusercontent.com/103726508/204379709-1b136794-ac1e-4262-8242-371108090727.png)
![image](https://user-images.githubusercontent.com/103726508/204379735-61a93b91-d1c7-4e38-9a76-e16cf258dc1c.png)

Аналогично 1 заданию было начато обучение:
![image](https://user-images.githubusercontent.com/103726508/204376681-499e0478-aab3-4b3e-8b81-ecf408077f5c.png)
![3задание обучаются](https://user-images.githubusercontent.com/103726508/204380884-abf710bb-a826-42d1-b035-59abc0273d68.gif)

Обучение прошло успешно:
![image](https://user-images.githubusercontent.com/103726508/204379195-d2704ffb-ec40-409e-837f-1f8197c83819.png)

После обучения шар ведёт себя так:

![3задание уже обучился](https://user-images.githubusercontent.com/103726508/204380751-8ab2be08-a639-4fff-ac2f-94814a1a1911.gif)

## Выводы

В ходе Лабораторной работы №3 я познакомилась с программными средствами для создания
системы машинного обучения и ее интеграции в Unity, создала 2 проекта, обучающий MLAgentов.
