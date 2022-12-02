# АНАЛИЗ ДАННЫХ И ИСКУССТВЕННЫЙ ИНТЕЛЛЕКТ [in GameDev]
Отчет по лабораторной работе #5 выполнил(а):
- Трофимова Ольга Сергеевна
- РИ210930
Отметка о выполнении заданий (заполняется студентом):

| Задание | Выполнение | Баллы |
| ------ | ------ | ------ |
| Задание 1 | * | 80 |
| Задание 2 | * | 20 |

знак "*" - задание выполнено; знак "#" - задание не выполнено;

Работу проверили:
- к.т.н., доцент Денисов Д.В.
- к.э.н., доцент Панов М.А.
- ст. преп., Фадеев В.О.

## Цель работы
Интегрировать экономическую систему в проект Unity и обучить ML-Agent. Проанализировать с помощью TensorBoard, насколько хорошо прошло обучение.


## Задание 1
Измените параметры файла. yaml-агента и определить какие параметры и как влияют на обучение модели.

Открыла проект.

С помощью Anaconda Prompt была создана среда, и скачаны необходимые библиотеки(mlagents 0.28.0, torch 1.7.1.):
```
 conda create -n MLAgent%l python=3.6.13
 conda activate MLAgent5l
 pip install mlagents==0.28.0
 pip install torch~=1.7.1 -f https://dowload.pytorch.org/whl/torch_stable.html
```
После нужно перейти в папку с проектом и запустить обучение:
```
cd C:\Users\Olga\MLA_Lab5\MLA_Lab4
mlagents-learn Economic.yaml --run-id=Economic --force
```
Далее запустить сцену в Unity.

![image](https://user-images.githubusercontent.com/103726508/204905889-f61b85d4-386d-4902-88d4-71058198f032.png)

Данный вывод говорит о том, что обучение прошло успешно и результат записан в указаный файл.

![image](https://user-images.githubusercontent.com/103726508/204906161-a125a319-bec0-4c8a-a8e9-e9b993b49064.png)


![image](https://user-images.githubusercontent.com/103726508/204906905-1eaafb22-3955-4cde-93d0-742bbae55372.png)

Вот такие результаты можно будет увидеть после выполнения команды, перейдя на локальный хост:

![image](https://user-images.githubusercontent.com/103726508/204909031-d3ce3339-48d1-4cff-b42e-3bc9725ca928.png)

В первом запуске использовались следующие параметры в .yaml файле:
``` py
behaviors:
  Economic:
    trainer_type: ppo
    hyperparameters:
      batch_size: 1024
      buffer_size: 10240
      learning_rate: 1.0e-4
      learning_rate_schedule: linear
      beta: 1.0e-2
      epsilon: 0.2
      lambd: 0.95
      num_epoch: 3      
    network_settings:
      normalize: false
      hidden_units: 128
      num_layers: 2
    reward_signals:
      extrinsic:
        gamma: 0.99
        strength: 1.0
    checkpoint_interval: 500000
    max_steps: 750000
    time_horizon: 64
    summary_freq: 5000
    self_play:
      save_steps: 20000
      team_change: 100000
      swap_steps: 10000
      play_against_latest_model_ratio: 0.5
      window: 10
```
В следующих запусках мы будем менять значение одного из параметров и смотреть, как он будет влиять на обучение модели.



## Задание 2
Опишите результаты, выведенные в TensorBoard.



## Выводы

