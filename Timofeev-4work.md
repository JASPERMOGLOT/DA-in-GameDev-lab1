# АНАЛИЗ ДАННЫХ И ИСКУССТВЕННЫЙ ИНТЕЛЛЕКТ [in GameDev]
Отчет по лабораторной работе #1 выполнил(а):
- Тимофеев Иван Дмитриевич
- РИ220933
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
Реализовать перцептрон, визуализировать работу перцептрона.

## Задание 1
### В проекте Unity реализовать перцептрон, который умеет производить вычисления: OR, AND, NAND, XOR
Ход работы:
- Написал код перцептрона, обучающегося на 4 Training Set'ах. Добавил в сцену.

```

using System.Collections;
using System.Collections.Generic;
using UnityEngine;

[System.Serializable]
public class TrainingSet
{
    public double[] input;
    public double output;
}

public class Perceptron : MonoBehaviour
{

    public TrainingSet[] tsOR;
    public TrainingSet[] tsAnd;
    public TrainingSet[] tsNAND;
    public TrainingSet[] tsXOR;

    double[] weights = { 0, 0 };
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

    double CalcOutput(int i, TrainingSet[] ts)
    {
        double dp = DotProductBias(weights, ts[i].input);
        if (dp > 0) return (1);
        return (0);
    }

    void InitialiseWeights()
    {
        for (int i = 0; i < weights.Length; i++)
        {
            weights[i] = Random.Range(-1.0f, 1.0f);
        }
        bias = Random.Range(-1.0f, 1.0f);
    }

    void UpdateWeights(int j, TrainingSet[] ts)
    {
        double error = ts[j].output - CalcOutput(j, ts);
        totalError += Mathf.Abs((float)error);
        for (int i = 0; i < weights.Length; i++)
        {
            weights[i] = weights[i] + error * ts[j].input[i];
        }
        bias += error;
    }

    double CalcOutput(double i1, double i2)
    {
        double[] inp = new double[] { i1, i2 };
        double dp = DotProductBias(weights, inp);
        if (dp > 0) return (1);
        return (0);
    }

    void Train(int epochs, TrainingSet[] ts)
    {
        InitialiseWeights();

        for (int e = 0; e < epochs; e++)
        {
            totalError = 0;
            for (int t = 0; t < ts.Length; t++)
            {
                UpdateWeights(t, ts);
                Debug.Log("W1: " + (weights[0]) + " W2: " + (weights[1]) + " B: " + bias);
            }
            Debug.Log("TOTAL ERROR: " + totalError);
        }
    }

    void Start()
    {
        Train(16, tsOR);
        Debug.Log("Test 0 0: " + CalcOutput(0, 0));
        Debug.Log("Test 0 1: " + CalcOutput(0, 1));
        Debug.Log("Test 1 0: " + CalcOutput(1, 0));
        Debug.Log("Test 1 1: " + CalcOutput(1, 1));

        Train(8, tsAnd);
        Debug.Log("Test 0 0: " + CalcOutput(0, 0));
        Debug.Log("Test 0 1: " + CalcOutput(0, 1));
        Debug.Log("Test 1 0: " + CalcOutput(1, 0));
        Debug.Log("Test 1 1: " + CalcOutput(1, 1));

        Train(8, tsNAND);
        Debug.Log("Test 0 0: " + CalcOutput(0, 0));
        Debug.Log("Test 0 1: " + CalcOutput(0, 1));
        Debug.Log("Test 1 0: " + CalcOutput(1, 0));
        Debug.Log("Test 1 1: " + CalcOutput(1, 1));

        Train(8, tsXOR);
        Debug.Log("Test 0 0: " + CalcOutput(0, 0));
        Debug.Log("Test 0 1: " + CalcOutput(0, 1));
        Debug.Log("Test 1 0: " + CalcOutput(1, 0));
        Debug.Log("Test 1 1: " + CalcOutput(1, 1));

    }

    void Update()
    {

    }
}

```

Всё обучение проходит корректно, за исключением вычисления XOR. 

- Добавил перцептрон в сцену:

![2023-12-15_16-16-04](https://github.com/Den1sovDm1triy/DA-in-GameDev-lab1/assets/148428630/6cb837ef-22f8-49fb-ba41-1121ab6db535)


## Задание 2
### Построить графики зависимости количества эпох от ошибки  обучения. Указать от чего зависит необходимое количество эпох обучения.

- Построил графики зависимости эпох от ошибок обучения:

- ![2023-12-15_16-17-13](https://github.com/Den1sovDm1triy/DA-in-GameDev-lab1/assets/148428630/71287f81-98ed-4aad-8bc9-10a909793e1a)

- Ошибка обучения на каждой эпохе зависит от множества факторов, таких как размер обучающей выборки, структура нейронной сети, выбранный метод обучения и параметры инициализации весов.

## Задание 3
### Построить визуальную модель работы перцептрона на сцене Unity.

- Написал код для объекта Cube, который в зависимости от сигнала, принятого при столкновении с объектом Sphere, меняет цвет.
- 

```

using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class Perceptron1 : MonoBehaviour
{
    // Цвета для отображения различных сигналов
    public Color neutralColor = Color.gray;
    public Color positiveColor = Color.green;
    public Color negativeColor = Color.red;

    private Renderer rend;

    void Start()
    {
        // Получаем компонент Renderer нейрона
        rend = GetComponent<Renderer>();
        // Устанавливаем начальный цвет нейрона
        rend.material.color = neutralColor;
    }

    void OnCollisionEnter(Collision col)
    {
        if (col.gameObject.CompareTag("InputSignal"))
        {
            // Получаем входной сигнал
            InputSignal signal = col.gameObject.GetComponent<InputSignal>();

            // Обрабатываем входной сигнал
            ProcessInputSignal(signal);
        }
    }

    void ProcessInputSignal(InputSignal signal)
    {
        // Получаем значение входного сигнала
        float input = (float)signal.GetValue();

        if (input > 0)
        {
            rend.material.color = positiveColor; 
        }
        else if (input < 0)
        {
            rend.material.color = negativeColor; 
        }
        else
        {
            rend.material.color = neutralColor;
        }
    }
}

```

- Написал скрипт для установки на сферу определенного сигнала:
```
using System.Collections;
using System.Collections.Generic;
using UnityEngine;
public class InputSignal : MonoBehaviour
{
    public float value;

    // Метод для установки нового значения входного сигнала
    public void SetValue(float newValue)
    {
        value = newValue;
    }

    // Метод для получения текущего значения входного сигнала
    public float GetValue()
    {
        return value;
    }
}
```

- Разместил объекты на сцене:
![2023-12-15-16-21-43](https://github.com/Den1sovDm1triy/DA-in-GameDev-lab1/assets/148428630/6f296d38-f737-4a36-922e-1fd59812dc97)

## Выводы

Научился визуализировать работу перцептрона. Понял устройство перцептрона.

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
