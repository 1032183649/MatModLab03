---
# Front matter
lang: ru-RU
title: "Отчёт по лабораторной работе №3"
subtitle: "дисциплина: Математическое моделирование"
author: "Купатенко Владислав Георгиевич"

# Formatting
toc-title: "Содержание"
toc: true # Table of contents
toc_depth: 2
lof: true # List of figures
lot: true # List of tables
fontsize: 12pt
linestretch: 1.5
papersize: a4paper
documentclass: scrreprt
polyglossia-lang: russian
polyglossia-otherlangs: english
mainfont: PT Serif
romanfont: PT Serif
sansfont: PT Sans
monofont: PT Mono
mainfontoptions: Ligatures=TeX
romanfontoptions: Ligatures=TeX
sansfontoptions: Ligatures=TeX,Scale=MatchLowercase
monofontoptions: Scale=MatchLowercase
indent: true
pdf-engine: lualatex
header-includes:
  - \linepenalty=10 # the penalty added to the badness of each line within a paragraph (no associated penalty node) Increasing the value makes tex try to have fewer lines in the paragraph.
  - \interlinepenalty=0 # value of the penalty (node) added after each line of a paragraph.
  - \hyphenpenalty=50 # the penalty for line breaking at an automatically inserted hyphen
  - \exhyphenpenalty=50 # the penalty for line breaking at an explicit hyphen
  - \binoppenalty=700 # the penalty for breaking a line at a binary operator
  - \relpenalty=500 # the penalty for breaking a line at a relation
  - \clubpenalty=150 # extra penalty for breaking after first line of a paragraph
  - \widowpenalty=150 # extra penalty for breaking before last line of a paragraph
  - \displaywidowpenalty=50 # extra penalty for breaking before last line before a display math
  - \brokenpenalty=100 # extra penalty for page breaking after a hyphenated line
  - \predisplaypenalty=10000 # penalty for breaking before a display
  - \postdisplaypenalty=0 # penalty for breaking after a display
  - \floatingpenalty = 20000 # penalty for splitting an insertion (can only be split footnote in standard LaTeX)
  - \raggedbottom # or \flushbottom
  - \usepackage{float} # keep figures where there are in the text
  - \floatplacement{figure}{H} # keep figures where there are in the text
---

# Цель работы

Построить графики модели боевых действий.

# Задание

**Вариант 50**  
  Задача: Между страной Х и страной У идет война. Численность состава войск
исчисляется от начала войны, и являются временными функциями
x(t) и y(t). В начальный момент времени страна Х имеет армию численностью 55 000 человек, а
в распоряжении страны У армия численностью в 45 000 человек. Для упрощения
модели считаем, что коэффициенты a, b, c, h постоянны. Также считаем
P(t) и Q(t) непрерывные функции.  
  Постройте графики изменения численности войск армии Х и армии У для
следующих случаев:

1. Модель боевых действий между регулярными войсками  
  $\frac{\partial x}{\partial t} = -0,41x(t)-0,89y(t)+sin(t+7)+1$  
  $\frac{\partial y}{\partial t} = -0,52x(t)-0,61y(t)+cos(t+6)+1$

2. Модель ведение боевых действий с участием регулярных войск и
партизанских отрядов  
  $\frac{\partial x}{\partial t} = -0,37x(t)-0,675y(t)+|2sin(t)|$  
  $\frac{\partial y}{\partial t} = -0,432x(t)y(t)-0,42y(t)+cos(t)+2$

# Выполнение лабораторной работы

**1. Рассмотрим подробнее уравнения**

1.1. В первом случае потери, не связанные с боевыми действиями, описывают члены -0,41x(t) и -0,61y(t), а
-0,89y(t) и -0,52x(t) отражают потери на поле боя. Также sin(t+7)+1 и cos(t+6)+1 учитывают
возможность подхода подкрепления к войскам Х и У в течение одного дня.

1.2. Во втором случае в борьбу добавляются партизанские отряды и потери, не связанные с боевыми действиями, описывают члены -0,37x(t) и -0,42y(t), а
-0,675y(t) и -0,432x(t)y(t) отражают потери на поле боя. Также |2sin(t)| и cos(t)+2 учитывают
возможность подхода подкрепления к войскам Х и У в течение одного дня.  

1.3. Начальные условия для обоих случаев будут равно $x_{0}=61.100$, $y_{0}=45.400$

**2. Построение графиков численности войск**

2.1. Написал программу на Modelica для 1 случая:
```
model lab03
  parameter Real a=-0.41;
  parameter Real b=-0.89;  
  parameter Real c=-0.52;
  parameter Real h=-0.61;
  parameter Real x0=61100;
  parameter Real y0=45400;
  Real x(start=x0);
  Real y(start=y0);
  Real t;
equation
  der(x)=a*x+b*y+sin(t+7)+1;
  der(y)=c*x+h*y+cos(t+6)+1;
  t=0;
end lab03;

```
Получил следующий график (см. рис. -@fig:001).

![Рис. 1. График для 1 случая](image/1.png){ #fig:001 width=70% }

2.2. Написал программу на Modelica для 2 случая:
```
model lab0302
  parameter Real a=-0.37;
  parameter Real b=-0.675;  
  parameter Real c=-0.432;
  parameter Real h=-0.42;
  parameter Real x0=61100;
  parameter Real y0=45400;
  Real x(start=x0);
  Real y(start=y0);
  Real t;
equation
  der(x)=a*x+b*y+abs(2*sin(t));
  der(y)=c*x*y+h*y+cos(t)+2;
  t=0;
end lab0302;
```
Получил следующий график (см. рис. -@fig:002).

![Рис. 2. График для 2 случая](image/2.png){ #fig:002 width=70% }

# Выводы

Построил графики модели боевых действий.
