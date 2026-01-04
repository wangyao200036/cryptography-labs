---
title: "Отчёт по лабораторной работе №1"
author: "Ван Яо"

lang: ru-RU
toc-title: "Содержание"

bibliography: bib/cite.bib
csl: pandoc/csl/gost-r-7-0-5-2008-numeric.csl

toc: true
toc-depth: 2
lof: true
lot: true
fontsize: 12pt
linestretch: 1.5
papersize: a4
documentclass: scrreprt

polyglossia-lang:
  name: russian
  options:
    - spelling=modern
    - babelshorthands=true
polyglossia-otherlangs:
  name: english

babel-lang: russian
babel-otherlangs: english

mainfont: Times New Roman
romanfont: Times New Roman
sansfont: Arial
monofont: Courier New
mainfontoptions: Ligatures=TeX
romanfontoptions: Ligatures=TeX
sansfontoptions: Ligatures=TeX,Scale=MatchLowercase
monofontoptions: Scale=MatchLowercase,Scale=0.9

biblatex: true
biblio-style: "gost-numeric"
biblatexoptions:
  - parentracker=true
  - backend=biber
  - hyperref=auto
  - language=auto
  - autolang=other*
  - citestyle=gost-numeric

figureTitle: "Рис."
tableTitle: "Таблица"
listingTitle: "Листинг"
lofTitle: "Список иллюстраций"
lotTitle: "Список таблиц"
lolTitle: "Листинги"

indent: true
header-includes:
  - \usepackage{indentfirst}
  - \usepackage{float}
  - \floatplacement{figure}{H}
---


# Цель работы

Разобраться с основой функционирования шифров простой замены, где для получения шифртекста отдельные символы или группы символов исходного алфавита заменяются символами или группами символов шифроалфавита. Написать программный код на языке Python, который реализует "Шифр Цезаря" и "Шифр Атбаш".


# Ход лабораторной работы
## Теоретические основы

### Шифр Цезаря

Исторический шифр, использовавшийся Юлием Цезарем в I веке н.э. для секретной переписки. Основан на алфавитном сдвиге.

**Математическая модель:**
$$
T_j(a) = (a + j) \mod m
$$
где:
1. $a$ — номер символа в алфавите
2. $j$ — ключ (величина сдвига)
3. $m$ — мощность алфавита


### Шифр Атбаш

Шифр зеркального отображения алфавита, где первая буква заменяется на последнюю, вторая — на предпоследнюю и т.д.

**Математическая модель:**
$$
T(a) = (m - 1 - a)
$$


## Подготовка рабочей среды

Для выполнения лабораторной работы использовался язык программирования Python 3. Была создана виртуальная среда и установлены необходимые пакеты для разработки.

## Практическая реализация


## Реализация шифра Цезаря

![](https://github.com/wangyao200036/cryptography-labs/raw/main/lab1/pic/1.png)

**Тестирование функции:**


![](https://github.com/wangyao200036/cryptography-labs/raw/main/lab1/pic/2.png)

## Реализация шифра Атбаш

![](https://github.com/wangyao200036/cryptography-labs/raw/main/lab1/pic/3.png)

**Тестирование функции:**

![](https://github.com/wangyao200036/cryptography-labs/raw/main/lab1/pic/4.png)

### Функциональное тестирование

| Тестовый пример           | Алгоритм | Ключ | Результат | Статус  |
|---------------------------|---------------------|------------------------|---------|---------|
| "привет" | Цезарь         | 3                  | "тулезх" | √     |
| "шифрование" | Цезарь             | 5                     | "щнчажснйут" | √     |
| "криптография" | Атбаш              | -                     | "пячкэимтфхся" | √     |
| "информация" | Атбаш              | -                     | "рцэнчгхрц" | √     |

## Анализ криптостойкости

Уязвимости шифра Цезаря

1. **Малое пространство ключей** — всего \(m-1\) возможных ключей

2. **Уязвимость к частотному анализу** — сохраняет распределение частот символов

3. **Простота взлома** — возможен полный перебор всех ключей

Уязвимости шифра Атбаш

1. **Фиксированное преобразование** — отсутствие ключа делает шифр детерминированным
2. **Самодвойственность** — двойное применение дает исходный текст
3. **Уязвимость к частотному анализу** — как и все моноалфавитные шифры

# Выводы

1. **Теоретические знания:**
   Изучены принципы работы моноалфавитных шифров замены, их математические модели и историческое значение.

2. **Практические навыки:**
   Реализованы два классических шифра — Цезаря и Атбаш, проведено их функциональное тестирование.
3. **Аналитические способности:**
   Проанализированы криптографические слабости шифров, выявлена их уязвимость к частотному анализу.

   
# Литература
Python Software Foundation. Официальная документация Python. https://docs.python.org/3/

# Приложения
Полный исходный код программ доступен в репозитории GitHub:
https://github.com/wangyao200036/cryptography-labs/tree/main/lab1