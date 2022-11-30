# АНАЛИЗ ДАННЫХ И ИСКУССТВЕННЫЙ ИНТЕЛЛЕКТ [in GameDev]
Отчет по лабораторной работе #4 выполнил(а):
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
Познакомиться с применением перцептрона. Реализовать логические операции с его применением.


## Задание 1
В проекте Unity реализовать перцептрон, который умеет производить вычисления:
 - OR | дать коментарий о корректности работы
 - AND | дать коментарий о корректности работы
 - NAND | дать коментарий о корректности работы
 - XOR | дать коментарий о корректности работы


В Unity был создан поект. На пустой объект навешен скрипт из методических указаний.

![image](https://user-images.githubusercontent.com/103726508/204795352-5d0c62a2-5527-4470-9b9b-6f9f4f388dc7.png)


``` C#
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

[System.Serializable]
public class TrainingSet
{
	public double[] input;
	public double output;
}

public class Perceptron : MonoBehaviour {

	public TrainingSet[] ts;
	double[] weights = {0,0};
	double bias = 0;
	double totalError = 0;

	double DotProductBias(double[] v1, double[] v2) 
	{
		if (v1 == null || v2 == null)
			return -1;
	 
		if (v1.Length != v2.Length)
			return -1;
	 
		double d = 0;
		for (int x = 0; x < v1.Length; x++)
		{
			d += v1[x] * v2[x];
		}

		d += bias;
	 
		return d;
	}

	double CalcOutput(int i)
	{
		double dp = DotProductBias(weights,ts[i].input);
		if(dp > 0) return(1);
		return (0);
	}

	void InitialiseWeights()
	{
		for(int i = 0; i < weights.Length; i++)
		{
			weights[i] = Random.Range(-1.0f,1.0f);
		}
		bias = Random.Range(-1.0f,1.0f);
	}

	void UpdateWeights(int j)
	{
		double error = ts[j].output - CalcOutput(j);
		totalError += Mathf.Abs((float)error);
		for(int i = 0; i < weights.Length; i++)
		{			
			weights[i] = weights[i] + error*ts[j].input[i]; 
		}
		bias += error;
	}

	double CalcOutput(double i1, double i2)
	{
		double[] inp = new double[] {i1, i2};
		double dp = DotProductBias(weights,inp);
		if(dp > 0) return(1);
		return (0);
	}

	void Train(int epochs)
	{
		InitialiseWeights();
		
		for(int e = 0; e < epochs; e++)
		{
			totalError = 0;
			for(int t = 0; t < ts.Length; t++)
			{
				UpdateWeights(t);
				Debug.Log("W1: " + (weights[0]) + " W2: " + (weights[1]) + " B: " + bias);
			}
			Debug.Log("TOTAL ERROR: " + totalError);
		}
	}

	void Start () {
		Train(8);
		Debug.Log("Test 0 0: " + CalcOutput(0,0));
		Debug.Log("Test 0 1: " + CalcOutput(0,1));
		Debug.Log("Test 1 0: " + CalcOutput(1,0));
		Debug.Log("Test 1 1: " + CalcOutput(1,1));		
	}
	
	void Update () {
		
	}
}
```


### Логическая операция OR:
| A | B | A OR B|
|---|---|-----|
| 0 | 0 | 0 |
| 0 | 1 | 1 |
| 1 | 0 | 1 |
| 1 | 1 | 1 |

Введём эти значения в скрипт:

![image](https://user-images.githubusercontent.com/103726508/204792969-17b22085-ed59-4bc0-8212-4ed6d4dacdab.png)

Для начала зададим 1 обучающую эпоху и посмотрим на результаты наших тестов:

![image](https://user-images.githubusercontent.com/103726508/204798461-4e2f9abc-3203-41c2-bf20-ed249b3057d4.png)

Значение Total Error отвечает за обучение перцептрона: если оно отлично от нуля, то модель не обучилась, если же ноль - тогда модель успешно обучилась. При первой эпохе обучения значение Total Error = 2.
Теперь зададим 4 эпохи обучения:

![image](https://user-images.githubusercontent.com/103726508/204799665-b81830dc-a594-4957-b11d-7a184eec7f75.png)

Total Error всё ещё не 0. Увеличим кол-во эпох до 5:

![image](https://user-images.githubusercontent.com/103726508/204801018-5e8bb66d-2b68-4a72-9c47-ed5e515b6291.png)

Total Error = 0. Перцептрон обучился.
Более подробную статистику можно посмотреть в 2 задании.

### Логическая операция AND:
| A | B | A AND B|
|---|---|-----|
| 0 | 0 | 0 |
| 0 | 1 | 0 |
| 1 | 0 | 0 |
| 1 | 1 | 1 |

Введём эти значения в скрипт:

![image](https://user-images.githubusercontent.com/103726508/204801890-b4842402-0500-470f-8c52-52055b41ee7b.png)

Для начала зададим 1 обучающую эпоху и посмотрим на результаты наших тестов:

![image](https://user-images.githubusercontent.com/103726508/204806969-0eecd291-a6ed-4058-92c6-efc4dfe406db.png)

Только на 8 эпохе обучения Total Error стабильно из раза в раз равен 0:

![image](https://user-images.githubusercontent.com/103726508/204810302-b3554d00-7080-4153-bf16-6fe8e512c96e.png)

Более подробную статистику можно посмотреть в 2 задании.

### Логическая операция NAND:
| A | B | A NAND B|
|---|---|-----|
| 0 | 0 | 1 |
| 0 | 1 | 1 |
| 1 | 0 | 1 |
| 1 | 1 | 0 |

Введём эти значения в скрипт:

![image](https://user-images.githubusercontent.com/103726508/204819000-91c5e321-ed36-406d-80ab-948284ea010f.png)

Для начала зададим 1 обучающую эпоху и посмотрим на результаты наших тестов:

![image](https://user-images.githubusercontent.com/103726508/204815664-1b9e8352-92dc-4187-b649-2a5b40810468.png)

Только на 7 эпохе обучения Total Error стабильно из раза в раз равен 0:

![image](https://user-images.githubusercontent.com/103726508/204818936-b6ba8135-c464-48c7-8192-44882139450c.png)

Более подробную статистику можно посмотреть в 2 задании.

### Логическая операция XOR:
| A | B | A XOR B|
|---|---|-----|
| 0 | 0 | 0 |
| 0 | 1 | 1 |
| 1 | 0 | 1 |
| 1 | 1 | 0 |

Введём эти значения в скрипт:

![image](https://user-images.githubusercontent.com/103726508/204811536-358292d8-3136-47bf-a200-7ff76d9128d8.png)

Для начала зададим 1 обучающую эпоху и посмотрим на результаты наших тестов:

![image](https://user-images.githubusercontent.com/103726508/204811402-260aa19c-8416-475b-8c11-be5f884af3b9.png)

Даже после 20 эпох обучения, перцептрон не может обучиться 
той логической операции. Total Error всегда было равно 4. Следовательно - однослойный перцептрон не может обучиться этой операции.
Однослойный перцептрон в силах решать линейные задачи, а XOR таковой не является.

![image](https://user-images.githubusercontent.com/103726508/204813614-8346ad33-2bdc-4772-8bff-89332d02f90f.png)

Более подробную статистику можно посмотреть в 2 задании.

## Задание 2
Построить графики зависимости количества эпох от ошибки обучения. Указать от чего зависит необходимое количество эпох обучения.

## Задание 3
Построить визуальную модель работы перцептрона на сцене Unity.

## Выводы


