# 10.2 «Кластеризация»  'Бойко Владислав'
---
## Задание 1
SMP - сильносвязанные системы. Из схемы видно что каждый процессор через кеш, связан с остальными некой комуникационной шиной, что приводит нас к выводу что это упрощенное изображение современных многоядерных процессоров, поскольку внутри одного процессора имеется несколько ядер которые имеют собстенный кеш и связанны между собой шиной (например кольцевая шина в процессорах intel или аналог от AMD infinity fabric) В свою очередь схема MPP  - слабосвязанные системы, там отдельные самостоятельные процесоры связанны между собой по средствам сети т.е. через сетевой адаптер, что говорит нам о том что мы имеед дело с кластером состоящим из нескольких компьютеров.
---
## Задание 2
Сильно связанные системы - несколько однородных процессоров, общий массив памяти, Слабо связанные систмы - вся память разделена между процессорными элементами
---
## Задаине 3 
1. Неограниченная масштабируемость узлов и кластеров
3. Наращиваемая масштабируемость
4. Можно расширять и уменьшать узлы по необходимости
5. Высокий коэффициент готовности
6. Отказоустойчивость, благодаря автономности узлов
7. Соотношение цена/производительность 
8. Можно строить кластер из любых строительных блоков: чем проще и стандартнее блоки, тем дешевле обходится вычислительная мощность
---
## Задание 4

---
## Задание 5

---
## Задание 6