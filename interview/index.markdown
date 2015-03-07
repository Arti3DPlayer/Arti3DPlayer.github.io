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

#Что такое юникод
*   Cтандарт кодирования символов, позволяющий представить знаки почти всех письменных языков

# Что выведет данный код на *python 2*. Какой результат будет на  *Python 3* (если конечно превратить синтаксис в Python 3)?
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

## Django

# Какой основной шаблон проектирования лежит в основе фреймверка?
*   MTV (Model-Template-View)  
    Наиболее распространенные виды MVC-паттерна, это:
    * Model-View-Controller
    * Model-View-Presenter
    * Model-View-View Model
    
    [Подробнее](http://habrahabr.ru/post/215605/)

# Что такое middleware?
*   **Middleware** - промежуточный слой который может срабатывать перед view и после view
    
