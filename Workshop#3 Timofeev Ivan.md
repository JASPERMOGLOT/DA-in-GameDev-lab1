# АНАЛИЗ ДАННЫХ И ИСКУССТВЕННЫЙ ИНТЕЛЛЕКТ [in GameDev]
Отчет по лабораторной работе #3 выполнил(а):
- Тимофеев Иван Дмитриевич
- РИ220933
Отметка о выполнении заданий (заполняется студентом):

| Задание | Выполнение | Баллы |
| ------ | ------ | ------ |
| Задание 1 | *| 60 |
| Задание 2 | * | 20 |

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
- Анализ переменных в игре. Таблицы и графики.
- Задание 2.
- Визуализация результатов выполнения задания. 10 сцен на Unity.
- Выводы.
- ✨Magic ✨

## Цель работы
Разработать оптимальный баланс для десяти уровней игры Dragon Picker

## Задание 1
### Предложите вариант изменения найденных переменных для 10 уровней в игре. Визуализируйте изменение уровня сложности в таблице. 
Ход работы:

- Для начала необходим анализ переменных, изменяя которые, мы будет повышать сложность. Берем четыре переменные:

1) Speed - отвечает за скорость перемещения дракона. Для повышения сложности, мы, соответственно, будем её повышать.
2) TimeBetweenEggDrop - время между падениями двух яиц. Чтобы повысить сложность, мы тоже будем уменьшать эту переменную.
3) LeftRightDistance - отвечает за расстояние, в пределах которого может перемещаться дракон. Дабы усложнить геймплей, с каждым уровнем будет повышаться.
4) ChanceDirection - Шанс, с которым дракон может изменить направление полета. Чтобы запутать игрока, с каждым уровнем будем увеличивать эту переменную.

- Визуализируем данные в таблице. Построим графики изменения переменных и процента сложности в зависимости от уровня:

![2023-12-15_00-52-35](https://github.com/JASPERMOGLOT/DA-in-GameDev-lab1/assets/148428630/d127d089-a6a3-491d-88ad-14677201cf43)


## Задание 2
### Создайте 10 сцен на Unity с изменяющимся уровнем сложности.

- Прикрепляю скриншоты сцен с разным уровнем сложности:

![1](https://github.com/JASPERMOGLOT/DA-in-GameDev-lab1/assets/148428630/865790e8-cf40-487e-ab57-527b3d911e4a)

![2](https://github.com/JASPERMOGLOT/DA-in-GameDev-lab1/assets/148428630/c3f235d2-5ffe-4760-9383-e9f6fbf7d4f4)

![3](https://github.com/JASPERMOGLOT/DA-in-GameDev-lab1/assets/148428630/fb92cb6d-8916-4299-91d7-b5ab9c8bd79b)

![4](https://github.com/JASPERMOGLOT/DA-in-GameDev-lab1/assets/148428630/916245ef-f98a-4be0-b308-68d9c777086c)

![5](https://github.com/JASPERMOGLOT/DA-in-GameDev-lab1/assets/148428630/7947e22a-0817-4c9e-be39-8f1db65a87bf)

![6](https://github.com/JASPERMOGLOT/DA-in-GameDev-lab1/assets/148428630/261c3214-b4d0-42a4-81b5-5c1729929083)

![7](https://github.com/JASPERMOGLOT/DA-in-GameDev-lab1/assets/148428630/d4195b0a-2171-4b39-9005-77096d089b7c)

![8](https://github.com/JASPERMOGLOT/DA-in-GameDev-lab1/assets/148428630/e225228a-042e-4a46-8665-53604ddcd2d0)

![9](https://github.com/JASPERMOGLOT/DA-in-GameDev-lab1/assets/148428630/2c550fd2-f0bb-4917-bde7-4e9e5b183685)

![10](https://github.com/JASPERMOGLOT/DA-in-GameDev-lab1/assets/148428630/3932a1e6-8c2a-413b-a3b4-1be96ac638c0)


## Выводы

Узнал о балансе в играх. Настроил баланс в игре Dragon Picker. Сделал таблицы с изменением переменных, построил график сложности.

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
