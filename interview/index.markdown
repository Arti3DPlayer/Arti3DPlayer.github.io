---
layout: interview
---


## Python

# Как получить список всех атрибутов объекта
*   
    ```print dir(Foo)```

#Как получить список всех публичных атрибутов объекта

*   В **Python** для обозначения protected атрибутов используют ``_``, для private — ``__`` перед названием переменной.

			print [arg for arg in dir(Foo) if not arg.startswith('_')]

    **Public** — доступ открыт всем, кто видит определение данного класса.

	**Private** — доступ открыт самому классу (т.е. функциям-членам данного класса) и друзьям (friend) данного класса, как функциям, так и классам.

	**Protected** — доступ открыт классам, производным от данного.

# Вкакой «магической» переменной хранится содержимое help?
*   В атрибуте ```__doc__```.

# Почему если в цикле меняется список, то используется ```for x in lst[:]```, что означает ```[:]```?
*    ```[:]``` — обозначение среза в питоне. Про них можно почитать, например, тут. В кратце: ```[:]``` создает копию lst и изменения в первом никак не влияют на итерацию по исходным значениям.

*   Есть два списка одинаковой длины, в одном ключи, в другом значения.Составить словарь.
    Будем использовать функцию ```zip```, которая делает кортежи из пары значений и ```dict```, которая создает словарь из переданных аргументов.

        a = ('John', 'Peter')
        b = (1, 2)
        print dict(zip(a, b))

#Какие структуры данных в питоне вы знаете и применяли на практике?
*   Python есть базовые структуры данных, типа **tuple, list, dict, set**
    Список это обьект или запись которая имеет ссылку на адрес следующего и предыдущего элемента и поле для хранения значения. 
    **tuple(Кортеж)**, по сути - неизменяемый список.
    **Set** — множество, в котором отсутствуют повторяющиеся элементы

#Уровни модели OSI
*   1. Прикладной уровень
    2. Уровень представления
    3. Сеансовый уровень
    4. Транспортный уровень
    5. Сетевой уровень
    6. Канальный уровень
    7. Физический уровень  
     
    ![имаже](https://encrypted-tbn2.gstatic.com/images?q=tbn:ANd9GcQ9XER2SC4erktboqpjLH1hLQDsVmOQrxe_5UP8y54Rbmxp8-QqFQYXgRg)

# Протокол tcp/ip  
*   Стек протоколов TCP/IP включает в себя четыре уровня:

    1.   **Прикладной уровень**  
    
    На прикладном уровне (Application layer) работает большинство сетевых приложений.
    Эти программы имеют свои собственные протоколы обмена информацией, например, HTTP для WWW, FTP (передача файлов), SMTP (электронная почта), SSH (безопасное соединение с удалённой машиной), DNS (преобразование символьных имён в IP-адреса) и многие другие.
    2. **Транспортный уровень**  
    
    **TCP** (IP идентификатор 6) — «гарантированный» транспортный механизм с предварительным установлением соединения, предоставляющий приложению надёжный поток данных, дающий уверенность в безошибочности получаемых данных, перезапрашивающий данные в случае потери и устраняющий дублирование данных. 
    **UDP** (IP идентификатор 17) протокол передачи датаграмм без установления соединения. Также его называют протоколом «ненадёжной» передачи, в смысле невозможности удостовериться в доставке сообщения адресату, а также возможного перемешивания пакетов.
    3. **Сетевой уровень**  
    
    Сетевой уровень (Internet layer) изначально разработан для передачи данных из одной (под)сети в другую. 
    4. Канальный уровень
    
    Канальный уровень (Link layer) описывает, каким образом передаются пакеты данных через физический уровень, включая кодирование (то есть специальные последовательности бит, определяющих начало и конец пакета данных). 

#Что такое юникод
*   Cтандарт кодирования символов, позволяющий представить знаки почти всех письменных языков

# Что выведет данный код на python 2. Какой результат будет на  Python 3 (если конечно превратить синтаксис в Python 3)?
* 

        def div1(x,y):
            print "%s/%s = %s" % (x, y, x/y)

        def div2(x,y):
            print "%s//%s = %s" % (x, y, x//y)

        div1(5,2)
        div1(5.,2)
        div2(5,2)
        div2(5.,2.)

    In **Python 2**, the output of the above code will be:

        5/2 = 2
        5.0/2 = 2.5
        5//2 = 2
        5.0//2.0 = 2.0


    By default, **Python 2** automatically performs integer arithmetic if both operands are integers. As a result, ```5/2 yields 2, while 5./2 yields 2.5```.
    Note that you can override this behavior in Python 2 by adding the following import:

        from __future__ import division


    Also note that the **“double-slash”** (```//```) operator will always perform integer division, regardless of the operand types. That’s why 5.
    ```0//2.0 yields 2.0``` even in **Python 2**.

    **Python 3**, however, does not have this behavior; i.e., it does not perform integer arithmetic if both operands are integers. Therefore, in Python 3, the output will be as follows:
    
        5/2 = 2.5
        5.0/2 = 2.5
        5//2 = 2
        5.0//2.0 = 2.0

# What will be the output of the code below? Explain your answer. How would you modify the definition of extendList to produce the presumably desired behavior?
* 
        def extendList(val, list=[]):
            list.append(val)
            return list

        list1 = extendList(10)
        list2 = extendList(123,[])
        list3 = extendList('a')

        print "list1 = %s" % list1
        print "list2 = %s" % list2
        print "list3 = %s" % list3



    The output of the above code will be:

        list1 = [10, 'a']
        list2 = [123]
        list3 = [10, 'a']


    Many will mistakenly expect list1 to be equal to **[10]** and list3 to be equal to **['a']**, thinking that the list argument will be set to its default value of **[]** each time extendList is called.  
    
    However, what actually happens is that the new default list is created only once when the function is defined, and that same list is then used subsequently whenever extendList is invoked without a list argument being specified. This is because expressions in default arguments are calculated when the function is defined, not when it’s called.
    list1 and list3 are therefore operating on the same default list, whereas list2 is operating on a separate list that it created (by passing its own empty list as the value for the list parameter).
    The definition of the extendList function could be modified as follows, though, to always begin a new list when no list argument is specified, which is more likely to have been the desired behavior:

        def extendList(val, list=None):
            if list is None:
                list = []
            list.append(val)
            return list


    With this revised implementation, the output would be:

        list1 = [10]
        list2 = [123]
        list3 = ['a']

#What will be the output of the code below? Explain your answer.
*        

        class Parent(object):
            x = 1

        class Child1(Parent):
            pass

        class Child2(Parent):
            pass

        print Parent.x, Child1.x, Child2.x
        Child1.x = 2
        print Parent.x, Child1.x, Child2.x
        Parent.x = 3
        print Parent.x, Child1.x, Child2.x

    The output of the above code will be:

        1 1 1
        1 2 1
        3 2 3

    **What confuses or surprises many about this is that the last line of output is ```3 2 3 ```rather than ```3 2 1```. Why does changing the value of ```Parent.x``` also change the value of Child2.x, but at the same time not change the value of  ``` Child1.x```?**  

    The key to the answer is that, in Python, class variables are internally handled as dictionaries. If a variable name is not found in the dictionary of the current class, the class hierarchy (i.e., its parent classes) are searched until the referenced variable name is found (if the referenced variable name is not found in the class itself or anywhere in its hierarchy, an AttributeError occurs).
    Therefore, setting **x = 1** in the Parent class makes the class variable x (with a value of 1) referenceable in that class and any of its children. That’s why the first print statement outputs **1 1 1**.
    Subsequently, if any of its child classes overrides that value (for example, when we execute the statement **Child1.x = 2**), then the value is changed in that child only. That’s why the second print statement outputs **1 2 1**.
    Finally, if the value is then changed in the Parent (for example, when we execute the statement **Parent.x = 3**), that change is reflected also by any children that have not yet overridden the value (which in this case would be **Child2**). That’s why the third print statement outputs **3 2 3**.


#Чему равна a = ?

*  
        def f(a=[]): 
            a.append(1)
            return a

            a=(f(),f()) 

    Ответ:

            а = ([1,1], [1,1])

    Default values are calculated, once, when the function is defined; thus, a mutable object such as a list or dictionary used as default value will be shared by all calls that don’t specify an argument value for the corresponding slot; this should usually be avoided.. 

    
#Что такое процессы и потоки в Python? Какие возникают проблемы?

*  Запущенная на Python программа называется процессом. Процесс при запуске содержит один единственный поток, который обычно называют главным потоком процесса. Поток последовательно выполняет инструкции программного кода.

    Процесс содержит информацию об объеме занимаемой оперативной памяти, списке открытых файлов, программный счетчик ссылающийся на выполняемую инструкцию, стек вызовов используемый для хранения локальных переменных функции.

    Программа может создавать новые процессы, называемые — дочерними. Дочерние процессы являются независимыми и изолированными друг от друга. У процесса существует флаг, говорящий о том, является ли процесс демоническим. Демонический процесс автоматически завершается вместе с процессом создавшим его, кроме того демонические процессы не могут создавать дочерних.

    Если нужно, чтобы ваше приложение выполняло несколько задач в одно и то же время, то можете воспользоваться потоками (threads). Потоки позволяют приложениям выполнять в одно и то же время множество задач. Многопоточность (multi-threading) важна во множестве приложений, от примитивных серверов до современных сложных и ресурсоёмких игр.
    Когда в одной программе работают несколько потоков, возникает проблема разграничения доступа потоков к общим данным. Предположим, что есть два потока, имеющих доступ к общему списку. Первый поток может делать итерацию по этому списку:
        for x in L
    а второй в этот момент начнет удалять значения из этого списка. Тут может произойти все что угодно: программа может упасть, или мы просто получим неверные данные.
    Решением в этом случае является применение блокировки. При этом доступ к заблокированному списку будет иметь только один поток, второй будет ждать, пока блокировка не будет снята.
    Применение блокировки порождает другую проблему – дедлок (deadlock) – мертвая блокировка. Пример дедлока: имеется два потока и два списка. Первый поток блокирует первый список, второй поток блокирует второй список. Первый поток изнутри первой блокировки пытается получить доступ к уже заблокированному второму списку, второй поток пытается проделать то же самое с первым списком. Получается неопределенная ситуация с бесконечным ожиданием. Эту ситуации легко описать, на практике все гораздо сложнее.
    Вариантом решения проблемы дедлоков является политика определения очередности блокировок. Например, в предыдущем примере мы должны определить, что блокировка первого списка идет всегда первой, а уже потом идет блокировка второго списка.
    Другая проблема с блокировками – в том, что несколько потоков могут одновременно ждать доступа к уже заблокированному ресурсу и при этом ничего не делать. Каждая питоновская программа всегда имеет главный управляющий поток.
    Питоновская реализация многопоточности ограниченная. Интерпретатор питона использует внутренний глобальный блокировщик (GIL), который позволяет выполняться только одному потоку. Это сводит на нет преимущества многоядерной архитектуры процессоров. Для многопоточных приложений, которые работают в основном на дисковые операции чтения/записи, это не имеет особого значения, а для приложений, которые делят процессорное время между потоками, это является серьезным ограничением.

#Что такое GIL(более подробно)?:

*   **Global Interpreter Lock (GIL)** — это способ синхронизации потоков, который используется в некоторых интерпретируемых языках программирования, например в **Python, Ruby и Java Script.**
GIL является самым простым способом избежать конфликтов при одновременном обращении разных потоков к одним и тем же участкам памяти]. Когда один поток захватывает его, GIL. Нет параллельных потоков — нет конфликтов при обращении к разделяемым объектам. Очередность выполнения потоков определяет интерпретатор, в зависимости от реализации, переключение между потоками может происходить: когда активный поток пытается осуществить ввод-вывод, по исчерпании лимита выполненных инструкций, либо по таймеру.

#Что такое итераторы?

*  Итераторы используются для прохождения по какому-нибудь контейнеру без учета особенностей его внутреннего строения. Обычно итераторы используются в циклах типа «foreach»  
    
    В классах, реализующих итераторы, должны быть определены методы «__iter__()» и «next()». __iter__() возвращает ссылку на итерируемый объект-контейнер, а next() при каждом вызове должен возвращать следующий элемент и бросать исключение StopIteration, если все элементы уже обработаны.

    По умолчанию, итераторы однонаправленные и не возобновляемые.

#Что такое генераторы?

* Генераторы — это «ленивые» итераторы — функции, возвращающие следующий элемент тогда, когда он запрашивается. В генераторах запоминается точка выхода из функции и при следующем обращении работа функции продолжается с места выхода.

    Для создания генераторов используют функции, содержащие в своем теле ключевое слово «yield» — такие функции возвращают объект-генератор.

    Генераторы занимают в памяти меньше места, чем списки, так как каждый раз в ячейке памяти хранится только один результат, когда список требует память для храниения всех своих значений.


#Что такое list comprehensions?

* Генерация списков (не знаю как адекватно перевести на русский list comprehensions) — яркий пример «синтаксического сахара». То есть конструкции, без которой легко можно обойтись, но с ней намного лучше :) Генераторы списков, как это не странно, предназначены для удобной обработки списков, к которой можно отнести и создание новых списков, и модификацию существующих.
Допустим, нам необходимо получить список нечетных чисел, не превышающих 25.
В принципе, только познакомившись с работой команды xrange решить эту проблему несложно.

        >>> res = []
        >>> for x in xrange(1, 25, 2):
        ...     res.append(x)
        ...
        >>> print res

    В общем-то, полученный результат — целиком нас устраивает всем, кроме длинной записи. тут-то на помощь и придет наш «сахарок». В самом простом виде, он обычно

        >>> res = [x for x in xrange(1, 25, 2)]
        >>> print res
        [1, 3, 5, 7, 9, 11, 13, 15, 17, 19, 21, 23]


# Что значит ключевое слово global?
* ```global``` - позволяет изменять глобальные переменные внутри функции и присваивать их.

        X = 88         # Глобальная переменная X

        def func():
            global X
            X = 99 # Глобальная переменная X: внутри инструкции def

        func()
        print(X)       # Выведет 99


# Какие особенности областей видимости в Python?
* Три основные области видимости:

    * Если присваивание переменной выполняется внутри инструкции ```def```, переменная является локальной для этой функции.

    * Если присваивание производится в пределах объемлющей инструкции ```def```, переменная является нелокальной для этой функции.

    * Если  присваивание  производится  за пределами всех инструкций ```def```,  она
является глобальной для всего файла.

    Функции образуют локальную область видимости, а модули – глобальную. 

    Эти две области взаимосвязаны между собой следующим образом:

    * **Объемлющий модуль** – это глобальная область видимости.Глобальные переменные для внешнего мира становятся атрибутами объекта модуля, но внутри модуля могут использоваться как простые переменные.

    * **Глобальная область** видимости охватывает единственный файл. Не надо заблуждаться насчет слова «глобальный» – имена на верхнем уровне файла являются глобальными только для программного кода в этом файле. Имена всегда относятся  к какому-нибудь  модулю и всегда необходимо явно импортировать модуль, чтобы иметь возможность использовать имена, определяемые в нем. Когда вы слышите слово «глобальный», подразумевайте «модуль».

    * Каждый вызов функции создает новую локальную область видимости. Всякий раз, когда вызывается функция, создается новая локальная область видимости – то есть пространство имен, в котором находятся имена, определяемые внутри функции. Каждую инструкцию ```def``` (и выражение ```lambda```) можно представить себе, как определение новой локальной области видимости.

    * Операция присваивания создает локальные имена, если они не были объявлены глобальными или нелокальными.  По  умолчанию все имена, которым  присваиваются значения  внутри функции, помещаются  в локальную  область  видимости. Если  необходимо  присвоить  значение  имени  верхнего  уровня в  модуле, который  вмещает функцию, это имя необходимо  объявить внутри функции глобальным с помощью инструкции ```global```. Если необходимо присвоить значение имени, которое находится в объемлющей инструкции ```def```, в **Python 3.0** это имя необходимо объявить внутри функции с помощью инструкции ```nonlocal```.

    * Все остальные имена являются локальными в области видимости объемлющей функции, глобальными или встроенными.

    ![image](http://3.bp.blogspot.com/-tujodN6vJ4g/UI789aJIgtI/AAAAAAAAAdQ/f7vQGVbq09I/s1600/222.jpg)

# Функции map, zip, sorted и lambda. Что делают? *Быстрее ли работают ?*
* Функции ```map```, ```zip``` и лямбда (кстати говоря называются "функции высшего порядка" или "first-class-functions") позволяют достаточно просто выполнять различные манипуляции с данными, для чего в "обычном" процедурном стиле приходится писать немного больше кода. Все ниженаписанное относится к так называемому функциональному программированию, луркайте подробности.

    Простая задача есть список ```a = [1, 2]``` и список ```b = [3, 4]``` одинаковой длины и нужно слить их парами. Проще простого - используя функцию ```zip``` :

        a = [1,2]
        b = [3,4]
        print zip(a,b)
        [(1, 3), (2, 4)]

    или тройками :

        a = [1,2]
        b = [3,4]
        c = [5,6]
        print zip(a,b,c)
        [(1, 3, 5), (2, 4, 6)]

    или в более общем виде

        list = [a, b, c]
        print zip(*list)
        [(1, 3, 5), (2, 4, 6)]

    Далее, функция – ```map```. Случаются ситуации, когда внезапно нужно применить какую-либо функцию к каждому элементу списка. Нуб напишет так :

        def f(x):
            return x*x

        nums = [1, 2, 3]
        for num in nums:
            print f(num)

    Более опытный нуб изучивший ```list comprehensions```:

        def f(x):
            return x*x
        print [f(num) for num in nums]

        Программист сделает проще :

        def f(x):
            return x*x
        print map(f, nums)

    А тру-мэдскиллз хакер сделает следующим образом (при условии конечно, что функцию можно записать лямбдой, далеко не всегда функция будет достаточно простой чтобы записать ее лямбдой) :

        print map(lambda x: x*x, nums)

    Из примера понятно, что map применяет какую-либо функцию к списку и возвращает результат опять же в виде списка. Вы можете передать несколько списков, тогда функция (идущая первым параметром) должна принимать несколько аргументов (по количеству списков переданных в map).

        def f(x, y):    
            return x*y

        a = [1,3,4]
        b = [3,4,5]
        print map(f, a, b)
        [3, 12, 20]

    Классно, правда?

    Однако если списки разной длины, т.е. Один короче другого, то он будет дополнен значениями None до нужной длины. Если убрать из списка ```b``` последнее значение – пример не будет работать, т.к. В функции ```f``` произойдет попытка умножения числа на ```None```, и питоне не позволяет это делать. Поэтому если функция ```f``` достаточно объемна, неплохо бы проверять передаваемые значения. Например;

        def f(x, y):
            if (y == None):
                y = 1    
            return x*y

    Если же заместо функции стоит ```None``` – то map действует примерно так же как и zip, но если передаваемые списки разной длины в результат будет писаться None – что кстати очень уместно в некоторых моментах.

        a = [1,3,4]
        b = [3,4]
        print map(None, a, b)
        [(1, 3), (3, 4), (4, None)]

    Теперь про лямбда функции в **python**. Они используются когда вам необходимо определить функцию без исподьзования ```def func_name(): ...```, ведь часто (как в предыдущих примерах) функция настолько мала, что определять её отдельно смыла нет (лишние строчки кода, что ухудшение читабельность). Поэтому функцию можно определить “на месте” ```f = lambda x: x*x``` как бы говорит нам – принимает ```x```, возвращает ```x*x```

    Так используя стандартные инструменты питона можно записать довольно сложные действия в одну строчку. К примеру функцию :

        def f(x, y):
            if (y == None):
                y = 1    
            return x*y

    можно представить как :

        lambda x, y: x * (y if y is not None else 1)

    А теперь хорошо бы передавать списки отсортированные по длине – ```len(a) > (b)``` – проще простого - воспользуемся функцией ```sorted```:

        sorted([a, b], key=lambda x: len(x), reverse=True)

    фунция ```sorted``` принимает список значений ```([a,b] = [[1,2],[2,4,5]])``` и сортирует по ключу key – который у нас задан функцией ```len(x)``` - возвращающей длину списка, сортируем в порядке убывания ```(reverse=True)```

    В конечном итоге вся операция записывается таким образом:

        map(lambda x, y: x * (y if y is not None else 1), *sorted([a, b], key=lambda x: len(x), reverse=True))

    списки ```a``` и ```b``` могут быть разной длины и передаваться в каком угодно порядке. Лямбда-выражения удобны для определения не очень сложных функций, которые передаются затем другим функциям.


#Чем отличается list от tuple?
* **Список** - это обьект или запись которая имеет ссылку на адрес следующего и предыдущего элемента и поле для хранения значения. 

    **Кортеж**, по сути - неизменяемый список.
    Зачем нужны кортежи, если есть списки?

    * Защита от дурака. То есть кортеж защищен от изменений, как намеренных (что плохо), так и случайных (что хорошо).

    * Меньший размер.

    * Возможность использовать кортежи в качестве ключей словаря.


#Операции с кортежами
* Все операции над списками, не изменяющие список (сложение, умножение на число, методы ```index()``` и ```count()``` и некоторые другие операции). Можно также по-разному менять 
элементы местами и так далее.


#Что такое immutable объекты? Какие Вы знаете? В чем особенность?
* **Mutable** — это обекты, значения которых могут быть изменены(например, ```list```), а **immutable** — это обекты, значения которых не может меняться (например, ```string```). Но это не значит, что если у нас есть переменная **immutable** типа, то ее нельзя изменить. Например, с типом string все привыкли работать так:

        In [11]: text = 'Hello'
        In [12]: text
        Out[12]: 'Hello'
        In [13]: text = 'Hello, World'
        In [14]: text
        Out[14]: 'Hello, World'

    Как мы видим, начение переменной ```text``` поменялось. На самом деле, при присвоении переменной ```text``` нового значения, в памяти создается новый объект, и переменная text начинает на него ссылаться. В этом легко убедится при помощи функции ```id()``` - получить идентификатор до и после изменения переменной.
    **Mutable** типы ведут себя так:

        In [15]: l = [1, 2, 3]
        In [16]: l
        Out[16]: [1, 2, 3]
        In [17]: id(l)
        Out[17]: 139901299808088
        In [18]: l.append(4)
        In [19]: l
        Out[19]: [1, 2, 3, 4]
        In [20]: id(l)
        Out[20]: 139901299808088

    Основываясь на этом свойстве(и не только), ключами в словаре (dict) могут быть только **immutable** обекты:

        In [21]: d = {'one': 1}
        In [22]: type(d)
        Out[22]: dict
        In [23]: d[1]=1
        In [24]: d
        Out[24]: {1: 1, 'one': 1}
        In [25]: d[l] = 'list'
        ---------------------------------------------------------------------------
        TypeError                                 Traceback (most recent call last)
        <ipython-input-25-4f49b18d7af7> in <module>() ----> 1 d[l] = 'list'
        TypeError: unhashable type: 'list'

    **Immutable** типы в Python — это числа(```numbers```), строки (```strings```) и кортежи (```tuples```).


#Что такое dict? Что может являться ключом? Что не может являться ключом? Каким образом нужно изменить класс что бы он смог быть ключом?

* Словарь в **Python** реализован в виде хэш-таблицы. Ключами словаря могут быть значения только hashable типов, то есть типов, у которых может быть получен хэш (для этого у них должен быть метод ```__hash__()```). Поэтому значения таких типов, как список (```list```), набор (```set```) и собственно сам словарь (```dict```), не могут быть ключами словаря.

    Чтобы класс был ключем к нему нужно добавить метод ```__hash__()```

    Подробнее про словари можно почитать [здесь](http://habrahabr.ru/post/247843/)


# *Что такое новые классы? чем отличаются от старых классов?*


#Чем отличается @staticmethod от @classmethod?

* ```@classmethod``` means: when this method is called, we pass the class as the first argument instead of the instance of that class (as we normally do with methods). This means you can use the class and its properties inside that method rather than a particular instance.

    ```@staticmethod``` means: when this method is called, we don't pass an instance of the class to it (as we normally do with methods). This means you can put a function inside a class but you can't access the instance of that class (this is useful when your method does not use the instance).


# *Что происходит при обращении к property b экземпляра класса А? Как ищутся properties/methods класса?*


# *Что происходит если property не найдено?*

# **Что такое metaclass?**
*   

    A metaclass is the class of a class. Like a class defines how an instance of the class behaves, a metaclass defines how a class behaves. A class is an instance of a metaclass.

    While in Python you can use arbitrary callables for metaclasses (like Jerub shows), the more useful approach is actually to make it an actual class itself. 'type' is the usual metaclass in Python. In case you're wondering, yes, 'type' is itself a class, and it is its own type. You won't be able to recreate something like 'type' purely in Python, but Python cheats a little. To create your own metaclass in Python you really just want to subclass 'type'.

    A metaclass is most commonly used as a class-factory. Like you create an instance of the class by calling the class, Python creates a new class (when it executes the 'class' statement) by calling the metaclass. Combined with the normal __init__ and __new__ methods, metaclasses therefore allow you to do 'extra things' when creating a class, like registering the new class with some registry, or even replace the class with something else entirely.

    When the 'class' statement is executed, Python first executes the body of the 'class' statement as a normal block of code. The resulting namespace (a dict) holds the attributes of the class-to-be. The metaclass is determined by looking at the baseclasses of the class-to-be (metaclasses are inherited), at the __metaclass__ attribute of the class-to-be (if any) or the '__metaclass__' global variable. The metaclass is then called with the name, bases and attributes of the class to instantiate it.

    However, metaclasses actually define the type of a class, not just a factory for it, so you can do much more with them. You can, for instance, define normal methods on the metaclass. These metaclass-methods are like classmethods, in that they can be called on the class without an instance, but they are also not like classmethods in that they cannot be called on an instance of the class. type.__subclasses__() is an example of a method on the 'type' metaclass. You can also define the normal 'magic' methods, like __add__, __iter__ and __getattr__, to implement or change how the class behaves.

    Here's an aggregated example of the bits and pieces:

            def make_hook(f):
                """Decorator to turn 'foo' method into '__foo__'"""
                f.is_hook = 1
                return f

            class MyType(type):
                def __new__(cls, name, bases, attrs):

                    if name.startswith('None'):
                        return None

                    # Go over attributes and see if they should be renamed.
                    newattrs = {}
                    for attrname, attrvalue in attrs.iteritems():
                        if getattr(attrvalue, 'is_hook', 0):
                            newattrs['__%s__' % attrname] = attrvalue
                        else:
                            newattrs[attrname] = attrvalue

                    return super(MyType, cls).__new__(cls, name, bases, newattrs)

                def __init__(self, name, bases, attrs):
                    super(MyType, self).__init__(name, bases, attrs)

                    # classregistry.register(self, self.interfaces)
                    print "Would register class %s now." % self

                def __add__(self, other):
                    class AutoClass(self, other):
                        pass
                    return AutoClass
                    # Alternatively, to autogenerate the classname as well as the class:
                    # return type(self.__name__ + other.__name__, (self, other), {})

                def unregister(self):
                    # classregistry.unregister(self)
                    print "Would unregister class %s now." % self

            class MyObject:
                __metaclass__ = MyType


            class NoneSample(MyObject):
                pass

            # Will print "NoneType None"
            print type(NoneSample), repr(NoneSample)

            class Example(MyObject):
                def __init__(self, value):
                    self.value = value
                @make_hook
                def add(self, other):
                    return self.__class__(self.value + other.value)

            # Will unregister the class
            Example.unregister()

            inst = Example(10)
            # Will fail with an AttributeError
            #inst.unregister()

            print inst + inst
            class Sibling(MyObject):
                pass

            ExampleSibling = Example + Sibling
            # ExampleSibling is now a subclass of both Example and Sibling (with no
            # content of its own) although it will believe it's called 'AutoClass'
            print ExampleSibling
            print ExampleSibling.__mro__



## Django

# Какой основной шаблон проектирования лежит в основе фреймверка?
*   MTV (Model-Template-View)  
    Наиболее распространенные виды MVC-паттерна, это:
    * Model-View-Controller
    * Model-View-Presenter
    * Model-View-View Model
    
    [Подробнее](http://habrahabr.ru/post/215605/)


#Что пошагово происходит когда пользователь нажал на ссылку? от браузера до приложения и обратно.

* После нажатия на ссылку, отправляеться ```http``` запрос, на указанный адресс. Веб сервер в этот момент ловит все запросы приходящие на указанный порт(по умолчанию 80) и обрабатывает его. Можно указать ряд инстукций что бы вебсервер сразу же отдавал ответ(как например со статикой и медиа файлами) или же мы дёргаем uwsgi файл, который передаёт запрос django по протоколу [WSGI](https://ru.wikipedia.org/wiki/WSGI), который в свою очередь превращает ```http``` запрос в обьект ```request``` и после прохождения middleware слоя попадает в view. View выполняет некую логику и возвращает ответ пользователю. 



# Что такое middleware?
*   **Middleware** - промежуточный слой который может срабатывать перед view и после view
    

#Какие встроенные сигналы бывают в Django?
* 
    * ```pre_save```
    * ```post_save```
    * ```post_delete```
    * ```pre_delete```
    * ```m2m_changed```
    * ```request_started``` - Sent when Django begins processing an HTTP request.
    * ```request_finished``` - Sent when Django finishes delivering an HTTP response to the client.

    [Подробнее](https://docs.djangoproject.com/en/dev/topics/signals/)


#Что такое mod_wsgi?
* **mod_wsgi** - модуль для веб-сервера [Apache](https://ru.wikipedia.org/wiki/Apache), который предоставляет [WSGI](https://ru.wikipedia.org/wiki/WSGI)-совместимый интерфейс для работы с web-приложениями.


#Что такое fixtures?
* Работать с “пустой” базой данных неудобно. Поэтому, при настройке и отладке приложения часто возникает необходимость в “начальных” данных для проекта. **Django** предлагает нам ряд возможностей для автоматического создания таких данных: с помощью файлов предварительной настройки (```fixtures```), либо с помощью ```SQL``` запросов.

##SQL

#Что такое внешний ключ и зачем он нужен?
* ```PK``` - первичный ключ

    ```FK``` - внешний ключ

    Первичный ключ (```primary key```) представляет собой один из примеров уникальных индексов и применяется для уникальной идентификации записей таблицы. Никакие из двух записей таблицы не могут иметь одинаковых значений первичного ключа.

    ```FK``` нужны для поддержания целостности базы, что бы нельзя было создать пост не привязанный ни какому топику, нельзя было удалить топик, если в нем есть посты, или удалить топик, а заодно автоматически удалить из базы все посты связанные с ним.

#Что такое GROUP BY? Что обозначает ключевое слово HAVING?
* ```GROUP BY``` - для аггрегации результирующих строк по заданным признакам-атрибутам.

    ```HAVING``` - для фильтрации результата GROUP BY по заданным логическим условиям. Используется как WHERE, но в другой части SQL-выражения и, соответственно, на другой стадии формирования ответа.    
    
    Пример:

    Скажем есть у нас Интернет-магазин. Чтобы узнать сколько денег нам принес каждый отдельно взятый покупатель в общей сложности за всё время существования магазина, мы делаем запрос с аггрегацией стоимости купленных товаров для конкретного покупателя:

        SELECT customer_name, SUM(order_price) FROM orders GROUP BY customer_name;

    Когда мы не хотим видеть "малоактивных покупателей" (те кто купил на малую сумму), мы можем отфильтровать аггрегированные данные из прошлого запроса по какой-то суммарной планке. Скажем, показать тех, кто купил у нас товаров в общей сложности на 100 т.р. и больше:

        SELECT customer_name, SUM(order_price) FROM orders GROUP BY customer_name HAVING SUM(order_price) >= 100000;                                 

#Что в чем отличие между LEFT JOIN, RIGHT JOIN и INNER JOIN?
* Простой ```JOIN``` - тоже самое что ```INNER JOIN``` и означает показывать только общие записи обоих таблиц. Каким образом записи считаются общими определяется полями в join-выражении. Например следующая запись

        FROM t1 JOIN t2 on t1.id = t2.id 

    означает что будут показаны записи с одинаковыми ```id```, существующие в обоих таблицах.

    ```LEFT JOIN``` (или LEFT ```OUTER JOIN```) означает показывать все записи из левой таблицы (той, которая идет первой в join-выражении) независимо от наличия соответствующих записей в правой таблице.

    ```RIGHT JOIN``` (или ```RIGHT OUTER JOIN```) действует в противоположность ```LEFT JOIN``` - показывает все записи из правой (второй) таблицы и только совпавшие из левой (первой) таблицы.

#Релизовать aggregation без orm.
* Агрегация это все функции типа ```SUM()```, ```COUNT()```

        SELECT ProductName, COUNT(product_id) FROM Products        

##Алгоритмы

#Что такое сложность алгоритмов? Как вычисляется? Какова сложность алгоритма: 

*       
        for i in x: 
            for j in y: 
                i*j

    Сложность алгоритма - зависит от скорости его роста. Вычисляется в количестве элементарных операций или шагов, которые необходимо выполнить. Сложность алгоритма данного в примере можно оценить как ```O(n^2)```;

# Какие алгоритмы сортировки знаете?

*   
    1. Сортировка вставками
    2. Сортировка выбором
    3. Сортировка слиянием
    4. Пузырьковая сортировка

# Какие есть способы обхода дерева?

* Пошаговый перебор элементов дерева по связям между узлами-предками и узлами-потомками называется обходом дерева. Зачастую, операция может быть выполнена переходом указателя по отдельным узлам. Обход, при котором каждый узел-предок просматривается прежде его потомков называется предупорядоченным обходом или обходом в прямом порядке (pre-order walk), а когда просматриваются сначала потомки, а потом предки, то обход называется поступорядоченным обходом или обходом в обратном порядке (post-order walk). Существует также симметричный обход, при котором посещается сначала левое поддерево, затем узел, затем — правое поддерево, и обход в ширину, при котором узлы посещаются уровень за уровнем (N-й уровень дерева — множество узлов с высотой N). Каждый уровень обходится слева направо.

## SCM

#Чем git rebase отличается от git merge?
* В Git'е есть два способа включить изменения из одной ветки в другую: **merge** (слияние) и **rebase** (перемещение).
    **Merge** - эта команда выполняет слияние между последними снимками состояний веток и последним общим предком этих веток, создавая новый снимок состояния (и коммит).

    При помощи команды **rebase** вы можете взять все изменения, которые попали в коммиты на одной из веток, и повторить их на другой.

    [Подробнее](https://www.atlassian.com/git/tutorials/merging-vs-rebasing/), [еще](http://git-scm.com/book/ru/v1/%D0%92%D0%B5%D1%82%D0%B2%D0%BB%D0%B5%D0%BD%D0%B8%D0%B5-%D0%B2-Git-%D0%9F%D0%B5%D1%80%D0%B5%D0%BC%D0%B5%D1%89%D0%B5%D0%BD%D0%B8%D0%B5)

#Что такое git reset?
*   Существует 3 режима команды git reset: **--soft**, **--mixed**(по умолчанию), **--hard**
    
    * **git reset --soft**

        Возьмем для примера ветку:
                - A - B - C (master)
        HEAD указывает на C и индекс совпадает с C.

        После выполнения

            git reset --soft B

        HEAD будет указывать на **B** и изменения из коммита **C** будут в индексе, как будто вы их добавили командой ```git add```. Если вы сейчас выполните ```git commit``` вы получите коммит полностью идентичный **C**.

    *   **git reset --mixed (по умолчанию)**

        Режим **--mixed** используется по умолчанию, т.е. ```git reset --mixed = git reset```

        Вернемся к тем же начальным условиям:
            - A - B - C (master)

        Выполнив

            git reset --mixed B

        или

            git reset B

        **HEAD** опять же будет указывать на **B**, но на этот раз изменения из **С** не будут в индексе и если вы запустите здесь ```git commit``` ничего не произойдет т.к. ничего нет в индексе. У нас есть все изменения из **С**, но если запустить ```git status``` то вы увидите, что все изменения ```not staged```. Чтобы их закоммитить нужно сначала добавить их в индекс командой ```git add``` и только после этого ```git commit```.

    *   **git reset --hard**
    
        Те же самые начальные условия:
            - A - B - C (master)

        Последний режим **--hard** также как и **--mixed** переместит **HEAD** на **В** и очистит индекс, но в отличие от **--mixed** жесткий **reset** изменит файлы в вашей рабочей директории. Если выполнить

            git reset --hard B

        то изменения из С, равно как и незакоммиченные изменения, будут удалены и файлы в репозитории будут совпадать с B. Учитывая то, что этот режим подразумевает потерю изменений, вы всегда должны проверять ```git status``` перед тем как выполнить жесткий **reset** чтобы убедиться что нет незакоммиченных изменений(или они не нужны).

    [Подробне](http://habrahabr.ru/post/203282/)


#  *В чем отличие веток git от веток в svn?*
  
