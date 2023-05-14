# 10.2 «Кластеризация»  'Бойко Владислав'
---
## Задание 1
SMP - сильносвязанные системы. Из схемы видно что каждый процессор через кеш, связан с остальными некой комуникационной шиной, что приводит нас к выводу что это упрощенное изображение современных многоядерных процессоров, поскольку внутри одного процессора имеется несколько ядер которые имеют собстенный кеш и связанны между собой шиной (например кольцевая шина в процессорах intel или аналог от AMD infinity fabric) В свою очередь схема MPP  - слабосвязанные системы, там отдельные самостоятельные процесоры связанны между собой по средствам сети т.е. через сетевой адаптер, что говорит нам о том что мы имеед дело с кластером состоящим из нескольких компьютеров.

## Задание 2
Сильно связанные системы - несколько однородных процессоров, общий массив памяти, Слабо связанные систмы - вся память разделена между процессорными элементами

## Задаине 3 
1. Неограниченная масштабируемость узлов и кластеров;
3. Наращиваемая масштабируемость;
4. Можно расширять и уменьшать узлы по необходимости;
5. Высокий коэффициент готовности;
6. Отказоустойчивость, благодаря автономности узлов;
7. Соотношение цена/производительность;
8. Можно строить кластер из любых строительных блоков: чем проще и стандартнее блоки, тем дешевле обходится вычислительная мощность

## Задание 4
1. Отказоустойчивые кластеры (High-availability clusters, HA, кластеры высокой доступности);
    1. Corosync
    2. Red Hat Cluster Suite
    3. Microsoft Windows Serwer
    4. Linux - HA
    5. Pacemaker
2. Кластеры с балансировкой нагрузки (Load balancing clusters);
    1. Сетевая балансировка
        1. DNS балансировка
        2. построение NLB кластера
        3. Балансировка по IP с использование дополнительного маршрутерезатора
        4. Балансировка по территориальному признаку
    2. Транспортная балансировка
        1. Путем простого кругового перебора,
        2. Путем выбора наименее загруженного сервера из пула и т.п.
    3. Прикладная балансировка
3. Вычислительные кластеры (High performance computing clusters, HPC);
    1. Расчетные задачи
    2. Научные исследования
4. Системы распределенных вычислений;
    1. Добровольные гриды
    2. Научные гриды
    3. Гриды на основе выделения вычеслительных ресурсов по требованию
5. Гибридные/смешанные кластеры.

## Задание 5
Kafka и RabbitMQ это брокеры сообщений. Все дело в паттернах связи, а именно Point to Point и Pub-Sub. Брокеры сообщений выступают посредниками во взаимодействии сервисов/компьютеров/PU в нашем случае взаимодействие отдельных компьютеров в кластере. 
Брокеры позволяют:
 1. Осуществлять асинхронный обмен данными (отправитель не блокируется);
 2. Отделять отправителя от получателя (отправитель ничего не знает о получателе);
 3. Выполнять отложенную обработку сообщений. Получателю не нужно быть постоянно активным, можно читать сообщения в удобное время;
 4. Делегировать ответственность за маршрутизацию и доставку сообщений третьей стороне;
 5. Легко интегрироваться с системами, использующими различные платформы, языки и протоколы связи.
### Пожалуй процетирую Хабр:
Принцип «Умный брокер, тупой потребитель» по отношению к RabbitMQ означает, что брокер берёт на себя много дополнительных действий. Например, следит за прочитанными сообщениями и удаляет их из очереди. Или сам организует процесс распределения сообщений между подписчиками.

Apache Kafka программный Pub-Sub брокер с открытым исходным кодом. Помимо гарантий доставки At most once и At least once, поддерживает Exactly once (Строго один раз). Обычно используется в больших проектах, так как обладает большой пропускной способностью и отказоустойчивостью, превосходит по данным характеристикам RabbitMQ и многие другие брокеры. При этом имеет высокий порог вхождения, требователен к ресурсам.

Kafka можно представить, как распределённый, реплицируемый лог коммитов. Распределённый, так как он разворачивается в виде кластера нод (под управлением Apache Zookeeper). Реплицируемый, потому что все данные синхронизируются между нодами. Лог, входящие сообщения последовательно добавляются в журнал и остаются там неизменными, не удаляются при чтении, как это происходит в RabbitMQ.

Для Kafka принцип «Тупой брокер, умный потребитель» означает, что, в отличие от RabbitMQ, он не занимается контролем и распределением сообщений. Потребители сами опрашивают брокер и решают, какие сообщения им читать, брокер только хранит данные.

*"Резюмируя скажу что основное отличие это - RabbitMQ сам контролирует прочтенность сообщений сам удаляет их из очереди сам организует распределение внутри очереди, Kafka же в свою очередь подобным не занимаетс, он лишь хранит данные в топиках, а еще kafka помимо гарантий доставки At most once и At least once, поддерживает Exactly once (Строго один раз)."*

### И еще чучуть:
Kafka используется для обработки больших объёмов данных, сотен тысяч сообщений в секунду, которые подолгу хранятся на диске и много раз читаются сотнями или даже тысячами подписчиков. Kafka — это легко масштабируемая система, обладающая повышенной отказоустойчивостью, что очень важно в крупных проектах.

RabbitMQ более простой в установке и настройке, успешно справляется с асинхронным обменом данными в микросервисной архитектуре. Не требует дополнительных компонентов и затрат на дисковые ресурсы, так как все сообщения после чтения из очереди удаляются. По сравнению с Kafka обладает большими возможностями по настройке шаблонов обмена сообщениями. Отличный выбор, если нет завышенных требований к отказоустойчивости и пропускной способности.

## Задание 6