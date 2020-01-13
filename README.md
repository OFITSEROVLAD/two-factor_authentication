# «Система контроля доступа с двухфакторной авторизацией по лицу и какому-то специфическому жесту»
##### Офицеров Владислав 2 курс ВМК МГУ 

Graphics CS MSU project 


## Постановка задачи:
Система должна брать на вход видео, находить лицо человека, распознавать его по базе из нескольких, отслеживать движение фигуры и распознавать какой-то жест.

## Данные:
Датасет необходимо было собрать самостоятельно.

## Проблемы*:

- Отсутствие датасета (собран датасет из 100 видео)
- Жест должен быть в самом начале видео
- Жест только правой рукой (скорее ограничение)
- Только 2 жеста (добавлен класс «левых» жестов)
- Очень долгая обработка одного видео, 5.5 мин на 5 сек. видео (решение данной проблемы далее)

*После сбора первой версии

## Что есть на данный момент: 
### Заранее подготовленные данные:
- Обученная нейросеть – “OpenPose”
- База данных - ”name_motion_table”: «Name» - «Motion»
- База данных лиц - “faces”
- Обученная модель распознавания жеста - “SVC”

#### Пример работы OpenPose (Желтые точки на руке) 
<img width="393" alt="Снимок экрана 2020-01-07 в 14 40 35" src="https://user-images.githubusercontent.com/56963957/72260423-e0b5fd80-3623-11ea-9e87-fc62056545ac.png">


### Алгоритм работы:
- Берем весь видеопоток
- На 1 frame опознаем лицо человека (если нет в базе, сразу делаем вердикт)
- Далее через каждые 4 frame’a запоминаем координаты смещения локтя и кисти относительно плеча, превращаем их в признаки
- Соотносим предсказание модели с необходимым движением человека с помощью «name_motion_table»

## Решение проблемы времени работы системы
<img width="862" alt="Снимок экрана 2020-01-13 в 16 27 10" src="https://user-images.githubusercontent.com/56963957/72260355-b7956d00-3623-11ea-8611-341b4b2bcbe4.png">
