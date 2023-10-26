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
- Пояснение и скриншоты
- Задание 2.
- Код задания, скриншоты
- Задание 3.
- Код задания, скриншоты
- Выводы.
- ✨Magic ✨

## Цель работы
Научиться передавать в Unity данные из Google Sheets с помощью Python.

## Задание 1
### Выберите одну из игровых переменных в игре, опишите её роль в игре, условия изменения / появления и диапазон допустимых значений. Постройте схему экономической модели в игре и укажите место выбранного ресурса в ней.

Ход работы:

- Опишите роль выбранной переменной в игре.

Я решил выбрать переменную "Здоровье главного героя" из игры Skyrim. В Скайриме здоровье ГГ - это количество урона, которое может получить главный герой.
Количество вашего здоровья зависит от уровня вашего персонажа, и каждый раз, когда вы повышаете уровень, вы можете выбрать, добавлять ли десять очков к вашему здоровью или к одному из других ваших атрибутов.
Ваш показатель здоровья также может быть увеличен с помощью эффектов укрепления здоровья, которые могут быть достигнуты с помощью чар, заклинаний и зелий.
Скорость восстановления вашего здоровья может быть увеличена за счет эффектов восстановления здоровья, включая зелья и зачарованные предметы.
Здоровье обычно автоматически восстанавливается в процентах от вашего максимального запаса здоровья в секунду, но в бою оно восстанавливается медленнее.
В Скайриме здоровье влияет на вашу способность выживать в бою и выполнять задания. Если ваше здоровье достигнет нуля, вы умрете.
Минимальное количество здоровья - 0 единиц. Максимальное (если при получении уровня качать только здоровья) - 900 единиц.

- Постройте схему экономической модели этой переменной.

Привожу скриншот:
![ЗДОРОВЬЕ экономич модель](https://github.com/JASPERMOGLOT/DA-in-GameDev-lab1/assets/148428630/bda76609-ce7b-4a93-b511-872e8e708b6a)



## Задание 2
### С помощью скрипта на языке Python заполните google-таблицу данными и средствами google-sheets визуализируйте данные в google-таблице для наглядного представления выбранной игровой величины.

Ход работы:

- Я решил описать выбранную переменную через модель боя с противником, во время которого главный герой получает урон, восстанавливает здоровье зельем, заклинанием и получением уровня.
- Прилагаю скриншот со скриптом на Python с заполнением таблицы:
![image](https://github.com/JASPERMOGLOT/DA-in-GameDev-lab1/assets/148428630/5fdea290-afb3-42c4-964a-4ab7d6d49109)

- Прилагаю скриншот таблицы после заполнения и наглядного представления на графике:
![image](https://github.com/JASPERMOGLOT/DA-in-GameDev-lab1/assets/148428630/919eb209-d089-47bc-9c6d-12b4a9f9cddd)

## Задание 3
### Настройте на сцене Unity воспроизведение звуковых файлов, описывающих динамику изменения выбранной переменной.

Ход работы:

- Скачал звуковые файлы из игры Skyrim. Написал код, который воспроизводит звуки в зависимости от изменения здоровья.
```csharp
using System.Collections;
using System.Collections.Generic;
using UnityEngine;
using UnityEngine.Networking;
using SimpleJSON;

public class NewBehaviourScript : MonoBehaviour
{
    public AudioClip potionSound;
    public AudioClip hitSound;
    public AudioClip levelSound;
    public AudioClip spellSound;
    private AudioSource selectAudio;
    private Dictionary<string, string> dataSet = new Dictionary<string, string>();
    private bool statusStart = false;
    private int i = 1;

    void Start()
    {
        StartCoroutine(GoogleSheets());
    }

    void Update()
    {
        if (dataSet["Mon_" + i.ToString()] == "Зелье" & statusStart == false & i != dataSet.Count)
        {
            StartCoroutine(PlaySelectAudioPotion());
            Debug.Log(dataSet["Mon_" + i.ToString()] + ". Значение здоровья: " + dataSet["Res_" + i.ToString()]);
        }

        if (dataSet["Mon_" + i.ToString()] == "Удар" & statusStart == false & i != dataSet.Count)
        {
            StartCoroutine(PlaySelectAudioHit());
            Debug.Log(dataSet["Mon_" + i.ToString()] + ". Значение здоровья: " + dataSet["Res_" + i.ToString()]);
        }

        if (dataSet["Mon_" + i.ToString()] == "Заклинание" & statusStart == false & i != dataSet.Count)
        {
            StartCoroutine(PlaySelectAudioSpell());
            Debug.Log(dataSet["Mon_" + i.ToString()] + ". Значение здоровья: " + dataSet["Res_" + i.ToString()]);
        }
        if (dataSet["Mon_" + i.ToString()] == "Уровень" & statusStart == false & i != dataSet.Count)
        {
            StartCoroutine(PlaySelectAudioLevel());
            Debug.Log(dataSet["Mon_" + i.ToString()] + ". Значение здоровья: " + dataSet["Res_" + i.ToString()]);
        }
    }

    IEnumerator GoogleSheets()
    {
        UnityWebRequest curentResp = UnityWebRequest.Get("https://sheets.googleapis.com/v4/spreadsheets/158XDckTfTL043QXg0QhYiG98SDOj31q3u6uaKYhDfxM/values/Лист1?key=AIzaSyDM5ARHWhoFT9gQDjZPJTt4jFV16tD6nTM");
        yield return curentResp.SendWebRequest();
        string rawResp = curentResp.downloadHandler.text;
        var rawJson = JSON.Parse(rawResp);
        foreach (var itemRawJson in rawJson["values"])
        {
            var parseJson = JSON.Parse(itemRawJson.ToString());
            var selectRow = parseJson[0].AsStringList;
            dataSet.Add(("Mon_" + selectRow[0]), (selectRow[1]));
            dataSet.Add(("Res_" + selectRow[0]), (selectRow[3]));
        }
    }

    IEnumerator PlaySelectAudioPotion()
    {
        statusStart = true;
        selectAudio = GetComponent<AudioSource>();
        selectAudio.clip = potionSound;
        selectAudio.Play();
        yield return new WaitForSeconds(3);
        statusStart = false;
        i++;
    }
    IEnumerator PlaySelectAudioHit()
    {
        statusStart = true;
        selectAudio = GetComponent<AudioSource>();
        selectAudio.clip = hitSound;
        selectAudio.Play();
        yield return new WaitForSeconds(3);
        statusStart = false;
        i++;
    }
    IEnumerator PlaySelectAudioSpell()
    {
        statusStart = true;
        selectAudio = GetComponent<AudioSource>();
        selectAudio.clip = spellSound;
        selectAudio.Play();
        yield return new WaitForSeconds(4);
        statusStart = false;
        i++;
    }
    IEnumerator PlaySelectAudioLevel()
    {
        statusStart = true;
        selectAudio = GetComponent<AudioSource>();
        selectAudio.clip = levelSound;
        selectAudio.Play();
        yield return new WaitForSeconds(4);
        statusStart = false;
        i++;
    }
}
```

- Настроил воспроизведение звуков. Прилагаю скриншот:

![image](https://github.com/JASPERMOGLOT/DA-in-GameDev-lab1/assets/148428630/2b818481-375c-4a69-bc69-1774c1541592)


## Выводы

- Научился передавать в Unity данные из Google Sheets с помощью Python.

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
