---
title: "Отчёт по лабораторной работе №6"
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

1. Изучить теоретические основы алгоритмов разложения чисел на множители
2. Реализовать программно два метода
   - $\rho$ - метод Полларда
   - метод квадратов Ферма
3. Провести тестирование алгоритмов на примерах и проанализировать их эффективность

# Ход лабораторной работы

## Теоретические основы

### 1. $\rho$ - метод Полларда

Метод основан на поиске цикла в последовательности, гегерируемой функцией $f(x)$ ,например $f(x)=x^2+c \mod n$.Если разность двух элементов последовательности имеет нетривиальный общий делитель с $n$,то он и является искомым делителем

**Алгоритм:**

1. Выбрать начальное значение $c$ и функцию $f$
1. Использовать два указателя $a$ и $b$, двигая их с разной скоростью
1. На каждой итерации вычислить $d=\text{НОД}(|a-b|,n)$
1. Если $1<d<n$, то$d$ - нетривиальный делитель

### 2. Метод квадратов Ферма

Метод основан на представлении числа $n$ в виде разности квадратов:
$$
n =s^2-t^2=(s+t)(s-t)
$$

**Алгоритм:**

1. Найти наименьшее $s\geq\lceil\sqrt{n}\rceil$
1. Проверить, является ли $s^2-n$ полным квадратои
1. Если да, то $p=s-t$,$q=s+t$




## Практическая реализация



###  Реализация $\rho$ -метода Полларда

![](https://github.com/wangyao200036/cryptography-labs/raw/main/lab6/pic/1.png)

### Реализация метода квадратов Ферма



![](https://github.com/wangyao200036/cryptography-labs/raw/main/lab6/pic/2.png)


## Функциональное тестирование

### $\rho$ -метод Полларда

![](https://github.com/wangyao200036/cryptography-labs/raw/main/lab6/pic/3.png)

### Метод квадратов Ферма

![](https://github.com/wangyao200036/cryptography-labs/raw/main/lab6/pic/4.png)

## Сравнительный анализ

| Метод                   | Преимущества               | Недостатки                                    |
| ----------------------- | -------------------------- | --------------------------------------------- |
| *$\rho$*-метод Полларда | Быстрый на малых делителях | Может не сойтись для некоторых чисел          |
| Метод квадратов Ферма   | Простота реализации        | Медленный, если делители далеки от $\sqrt{n}$ |




# Выводы

1. **Теоретические знания:**  

   ​	Изучены два классических алгоритма факторизации: ρ*ρ*-метод Полларда и метод квадратов Ферма, их математические основы и области применения.

2. **Практические навыки:**  

   ​	Успешно реализованы оба алгоритма на Python. Проведено тестирование на составных числах, показавшее корректность работы методов.

3. **Аналитические способности:**  

   ​	Сравнительный анализ показал, что ρ*ρ*-метод Полларда эффективен для чисел с малыми делителями, а метод Ферма удобен для чисел, близких к квадрату целого числа.


# Литература

1. Pollard J.M. A Monte Carlo method for factorization. BIT Numerical Mathematics, 1975.
2. Python Software Foundation. Официальная документация Python. https://docs.python.org/3/

# Приложения

Полный исходный код программ доступен в репозитории GitHub:  
https://github.com/wangyao200036/cryptography-labs/tree/main/lab6