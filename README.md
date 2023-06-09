# Домашнее задание к занятию 11.1. «Базы данных, их типы» - Карпов Роман

### Задание 1. СУБД

### Кейс
Крупная строительная компания, которая также занимается проектированием и девелопментом, решила создать 
правильную архитектуру для работы с данными. Ниже представлены задачи, которые необходимо решить для
каждой предметной области. 

Какие типы СУБД, на ваш взгляд, лучше всего подойдут для решения этих задач и почему? 
 
1.1. Бюджетирование проектов с дальнейшим формированием финансовых аналитических отчётов и прогнозирования рисков.
СУБД должна гарантировать целостность и чёткую структуру данных.
1.1.* Хеширование стало занимать длительно время, какое API можно использовать для ускорения работы? 
1.2. Под каждый девелоперский проект создаётся отдельный лендинг, и все данные по лидам стекаются в CRM к 
маркетологам и менеджерам по продажам. Какой тип СУБД лучше использовать для лендингов и для CRM? 
СУБД должны быть гибкими и быстрыми.
1.2.* Можно ли эту задачу закрыть одной СУБД? И если да, то какой именно СУБД и какой реализацией?
1.3. Отдел контроля качества решил создать базу по корпоративным нормам и правилам, обучающему материалу 
и так далее, сформированную согласно структуре компании. СУБД должна иметь простую и понятную структуру.
1.3.* Можно ли под эту задачу использовать уже существующую СУБД из задач выше и если да, то как лучше это 
реализовать?
1.4. Департамент логистики нуждается в решении задач по быстрому формированию маршрутов доставки материалов 
по объектам и распределению курьеров по маршрутам с доставкой документов. СУБД должна уметь быстро работать
со связями.
1.4.* Можно ли к этой СУБД подключить отдел закупок или для них лучше сформировать свою СУБД в связке с СУБД 
логистов?
1.5.* Можно ли все перечисленные выше задачи решить, используя одну СУБД? Если да, то какую именно?

#### Ответ:  
<ins>1.1. Бюджетирование проектов с дальнейшим формированием финансовых аналитических отчётов и прогнозирования рисков. СУБД должна гарантировать целостность и чёткую структуру данных.</ins>  
    В этом случае, подойдут Реляционные БД, SQL. Т.к. одна из их основных особенностей - это надежность и неизменяемость данных, при минимальном риске потери информации. При том, данные храняться в табличной форме и четко структурированы. Как вариант СУБД: Oracle, PostgreSQL. 
   

<ins>1.2. Под каждый девелоперский проект создаётся отдельный лендинг, и все данные по лидам стекаются в CRM к маркетологам и менеджерам по продажам. Какой тип СУБД лучше использовать для лендингов и для CRM? СУБД должны быть гибкими и быстрыми.</ins>   
     На мой взгляд, тут отлично подойдет MySQL. MySQL - хорошо работает с реляционными данными и имеет свободное ПО. 


<ins>1.3. Отдел контроля качества решил создать базу по корпоративным нормам и правилам, обучающему материалу и так далее, сформированную согласно структуре компании. СУБД должна иметь простую и понятную структуру.</ins>   
    Подобный подход при организации, говорит нам о том, что нам понадобиться СУБД, со схожей системой хранения данных. В этом случае, на мой взгляд отлично подойдет 
MongoBD - бд расчитанная на работу с данными иерархической структуры. В иерархической модели данные организованы в древовидную структуру. Данные хранятся в виде набора полей, где каждое поле содержит только одно значение. Записи связаны друг с другом через связи в отношениях родитель-потомок. В иерархической модели базы данных каждая дочерняя запись имеет только одного родителя. Родитель может иметь несколько детей.
MongoDB - по своей сути, хранилище документов, без использования схематичного или таблоичного формата хранения. Данную СУБД за счет быстродействия и простой обработки данных, рекомендуют использовать так, где отсутствуют потребности в сложных выборках. 


<ins>1.4. Департамент логистики нуждается в решении задач по быстрому формированию маршрутов доставки материалов по объектам и распределению курьеров по маршрутам с доставкой документов. СУБД должна уметь быстро работать со связями.</ins>     
На мой взгляд. отлично подойдут Графовые СУБД. Данные СУБД предназначены для хранения информации, связанной с графами (узлами и связями между узлами). 

---

### Задание 2. Транзакции

2.1. Пользователь пополняет баланс счёта телефона, распишите пошагово, какие действия должны произойти для того, чтобы транзакция завершилась успешно. Ориентируйтесь на шесть действий.
2.1.* Какие действия должны произойти, если пополнение счёта телефона происходило бы через автоплатёж?

#### Ответ:  
<ins>2.1. Пользователь пополняет баланс счёта телефона, распишите пошагово, какие действия должны произойти для того, чтобы транзакция завершилась успешно. Ориентируйтесь на шесть действий.</ins>     
 Если говорить, про весь процесс, то получаем: 
 - Проверка баланса (или уведомление от провайдера о неободимсоти пополнить счет);  
 - Авторизация в ЛК МБ или провайдера телефонных услуг;  
 - Введение номера для пополнения;  
 - Подтвердить корректность введенного номера;
 - Выбрать номер счета для списания средств (если счета нет, ввести);
 - Указать сумму пополнения;
 - Подтвердить оплату;
 - Проверить баланс счета (получить уведомление об удачном пополнении);  

С точки зрения банка: 
- Получение запроса от клиента на перевод ДС;
- Выбор банковского счета (если их несколько), на который поступает запрос о списании;
- Сопоставление запланированной суммы платежа, с наличием ДС на банковском счете;
- Отправка подтверждения о переводе клиенту;
- Получени результат о подтаверждении перевода;
- Перевод ДС на указанный номер телефона;

---

### Задание 3. SQL vs NoSQL

3.1. Напишите пять преимуществ SQL-систем по отношению к NoSQL. 
3.1.* Какие, на ваш взгляд, преимущества у NewSQL систем перед SQL и NoSQL.

#### Ответ:  
<ins>3.1. Напишите пять преимуществ SQL-систем по отношению к NoSQL.</ins>     
Выделить 5 - сложно (но попробуем), опишу просто причины по которым SQLЮ на мой взгляд, имеет преимущество перед NoSQL. SQL - отличный выбор, когда доступна предварительно определенная структура и схемы заданы; все данные должны быть строго согласованы; требуется выполнять многорядные транзакции; требуется разработка пользовательских панелей мониторинга; требуется выполнение сложных запросов. 

---

### Задание 4. Кластеры

Необходимо производить большое количество вычислений при работе с огромным количеством данных, под эту задачу 
выделено 1000 машин. 

На основе какого критерия будете выбирать тип СУБД и какая модель *распределённых вычислений* 
здесь справится лучше всего и почему?


#### Ответ:  
Критерий по которому будет производиться выбор СУБД - если под огромным количеством данных мы понимаем понятие "Big Data" (т.е. огромное количество данных), то сложно говорить об 1 типе СУБД. Вероятно нам придется рассмотреть "готовое решение" на базе платформы.   
Основу в работе с большими данными заложили товарищи с Google, когда опубликовали подход "MapReduce" - это модель распределенной обработки данных, для обработки больших объёмов данных на компьютерных кластерах.   
Одним из хороших инструментов на мой взгляд, это Haboop - стек технологий так или иначе связанных с обработкой больших данных (не только при помощи MapReduce).  
Основными компонентами ядра hadoop являются:   
- Hadoop Distributed File System (HDFS) – распределённая файловая система, позволяющая хранить информацию практически неограниченного объёма.  
- Hadoop YARN – фреймворк для управления ресурсами кластера и менеджмента задач, в том числе включает фреймворк MapReduce.  
- Hadoop common  
И довольно большое количество внешнего инструментария (проектов), не относящихся к центральному "ядру" стека, которое упрощают работу с большими данными. 
