---
title: "Отчёт по лабораторной работе №7"
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

1. Изучить теоретические основы задачи дискретного логарифмирования в конечных полях.
2. Реализовать программно алгоритм Полларда (ρ-метод) для решения задачи дискретного логарифмирования.
3. Провести тестирование алгоритма на примерах.


# Ход лабораторной работы

## Теоретические основы

### 1. Задача дискретного логарифмирования (DLP)

Пусть $p$  — простое число,$a$ элемент мультипликативной группы конечного поля $F_p^*=\mathbb{Z}/p\mathbb{Z}\setminus\{0\}$,имеющий порядок $r$.Для заданного $b \in \langle a\rangle$. (циклической подгруппе, порождённой $a$) требуется найти целое число $x$ такое, что:
$$
a^x \equiv b \pmod{x},\quad 0 \leq x < r
$$
Число $x$ называется **дискретным логарифмом** $b$ по основанию *a* по модулю $p$ и обозначается $x=\log_a b$.

### 2. **$\rho$ -метод Полларда для DLP**

Алгоритм основан на парадоксе дней рождения и методе поиска циклов Флойда. Идея — построить псевдослучайную последовательность элементов группы, в которой рано или поздно произойдёт коллизия (повторение значения). При этом каждое значение последовательности представляется в виде $a^{\alpha_i}b^{\beta_i}$,что позволяет при коллизии получить уравнение относительно $x$.

**Алгоритм:**

- Разбить группу $F_p^*$ на три непересекающихся подмножества $S_1,S_2,S_3$ (например, по остатку от деления на 3).
- Определить функцию перехода:

$$
f(c)=
\begin{cases}
c \cdot a \bmod p,&c \in S_1 \\
c \cdot b \bmod p,&c \in S_2 \\
c^2 \bmod p,&c \in S_3 
\end{cases}
$$

Соответственно обновляются показатели $(\alpha,\beta)$.

- Инициализировать два указателя ("черепаху" и "зайца") с начальным состоянием $(c,\alpha,\beta)=(1,0,0)$.
- На каждой итерации:
  - Черепаха делает один шаг:$(c_t,\alpha_t,\beta_t)=f(c_t,\alpha_t,\beta_t)$
  - Заяц делает два шага:$(c_h,\alpha_h,\beta_h)=f(f(c_h,\alpha_h,\beta_h))$
- Если $c_t=c_h$,то получаем равенство:

$$
a^{\alpha_t}b^{\beta_t}\equiv a^{\alpha_h}b^{\beta_h} \pmod p \Rightarrow a^{\alpha_t-\alpha_h}b^{\beta_t-\beta_h} \pmod p
$$

​	Подставля $b=a^x$,получаем линейное сравнение:
$$
(\beta_t-\beta_h)x \equiv (\alpha_h-\alpha_t) \pmod r
$$
- Решить это сравнение с помощью расширенного алгоритма Евклида. Проверить найденное решение подстановкой.



## Практическая реализация

### Вспомогательные функции

#### Реализация расширенного алгоритма Евклида

![](https://github.com/wangyao200036/cryptography-labs/raw/main/lab7/pic/1.png)

#### Вычисление обратного элемента по модулю

![](https://github.com/wangyao200036/cryptography-labs/raw/main/lab7/pic/2.png)

#### Основная реализация реализующая $\rho$ -метод.

![](https://github.com/wangyao200036/cryptography-labs/raw/main/lab7/pic/3.png)

## Функциональное тестирование

![](https://github.com/wangyao200036/cryptography-labs/raw/main/lab7/pic/4.png)
# Выводы

1. **Теоретические знания:** Изучена задача дискретного логарифмирования и её роль в криптографии с открытым ключом (например, в протоколе Диффи–Хеллмана). Освоен принцип работы ρ-метода Полларда для решения DLP.

2. **Практические навыки:** Успешно реализован алгоритм на языке Python. Программа корректно находит дискретные логарифмы для заданных примеров и проходит верификацию.

3. **Аналитические способности:** Подтверждена эффективность ρ-метода для групп, где порядок $r$ не слишком велик. Алгоритм демонстрирует ожидаемую сложность $O(\sqrt r)$ и является практичным инструментом для анализа стойкости криптосистем, основанных на DLP.

# Литература

1. Pollard J.M. Monte Carlo methods for index computation (mod p). Mathematics of 
2. Python Software Foundation. Официальная документация Python. https://docs.python.org/3/

# Приложения

Полный исходный код программ доступен в репозитории GitHub:  
https://github.com/wangyao200036/cryptography-labs/tree/main/lab7
   