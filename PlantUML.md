PlantUML
========

PlantUML — это язык и инструмент для создания диаграмм, который использует текстовый формат для описания бизнес-процессов, диаграмм классов, состояний, последовательностей и многих других видов диаграмм. 

### Диаграмма классов

Диаграмма классов - это набор статических, декларативных элементов модели (используется при кодогенерации). Диаграммы классов отражают статическую структуру приложения: классы, интерфейсы и отношения между ними.

##### Работа в PlantUML над диаграммой классов

Для начала создания диаграммы классов с помощью инструмента PlantUML необходимо создать файл в корневой папке проекта с расширением ".puml". Это и будет файл с диаграммой классов.

В начале работы в файле указываем границы UML-диаграммы с помощью следующих ключевых слов:

```
@startuml
#
# Код нашей диаграммы
#
@enduml
```

Для создания класса указываем ключевое слово "class", далее имя класса, после открываем фигурные скобки, подобно языку программирования Java.

```
class main {
    
}
```

Для того, чтобы добавить в класс переменную, принадлежащую этому классу, её инициализация прописывается в следующем порядке: знак указания области видимости, имя переменной, двоеточие, тип данных переменной. Все параметры указываются через пробел. Ниже приведены все знаки указания области видимости переменных:

```
+  public
-  private
#  protected
~  package
/  derived
```

Для методов инициализация прописывается в следующем порядке: знак указания области видимости; имя метода, в скобках после которого указываются поступаемые в метод переменные с типом их данных; двоеточие; тип возвращаемых данных метода. Все параметры указываются через пробел. Для методов используются те же указания области видимости, что и для переменных, кроме последнего ("/ derived").

##### Взаимосвязи между классами

Для указания взаимосвязей между классами используются следующие связи: ассоциация, наследование, реализация/имплементация, зависимость, агрегация, композиция.

**Наследование** показывает, что один из двух связанных классов (подтип) является частной формой другого (надтипа), который называется обобщением первого. Один класс (надтип) является родительским для другого (подтип).

**Ассоциация** показывает, что объекты одной сущности (класса) связаны с объектами другой сущности таким образом, что можно перемещаться от объектов одного класса к другому. Является общим случаем композиции и агрегации. 

**Реализация** — отношение между двумя элементами модели, в котором один элемент (клиент) реализует поведение, заданное другим (поставщиком). Реализация — отношение целое-часть. Поставщик, как правило, является абстрактным классом или классом-интерфейсом.

**Зависимость** — это слабая форма отношения использования, при которой изменение в спецификации одного влечёт за собой изменение другого, причём обратное не обязательно. Возникает, когда объект выступает, например, в форме параметра или локальной переменной. Зависимость может быть между экземплярами, классами или экземпляром и классом. 

**Агрегация** — это разновидность ассоциации при отношении между целым и его частями. Одно отношение агрегации не может включать более двух классов (контейнер и содержимое). Агрегация встречается, когда один класс является коллекцией или контейнером других. Причём по умолчанию, агрегацией называют агрегацию по ссылке, то есть когда время существования содержащихся классов не зависит от времени существования содержащего их класса. Если контейнер будет уничтожен, то его содержимое — нет. 

**Композиция** — более строгий вариант агрегации. Известна также как агрегация по значению. Композиция имеет жёсткую зависимость времени существования экземпляров класса контейнера и экземпляров содержащихся классов. Если контейнер будет уничтожен, то всё его содержимое будет также уничтожено. 

В PlantUML эти взаимосвязи могут быть реализованы следующим образом:

```
<|--  Наследование
<--   Ассоциация
<|..  Реализация/имплементация
<..   Зависимость
o--   Агрегация
*--   Композиция
```

В том месте, куда указывает стрелочка (в данном случае влево) указывается класс, к которому направлена связь, а с другой стороны указывается класс, от которого эта связь исходит.

### Диаграмма последовательностей

Диаграмма последовательностей - это диаграмма, отображающая последовательность, в которой объекты на единой временной оси в процессе взаимодействия обмениваются сообщениями. Является одной из двух диаграмм взаимодействия.

##### Создание в PlantUML диаграммы последовательностей

В начале работы также, как и в прошлом случае, создаём в корневой папке проекта файл с расширением ".puml" и внутри самого файла указываем границы UML-диаграммы:

```
@startuml
#
# Код диаграммы
#
@enduml
```

##### Объявление участников

При использовании ключевого слова participant возможно получить больший контроль над отображением участников. Порядок перечисления участников задаёт также пороядок отображения участников по умолчанию. Использование других ключевых слов (отличных от participant) позволяет изменить форму представления (отображения) участника: 

```
actor
boundary
control
entity
database
collection
queue
```

PlantUML предоставляет возможность переименовать участника, используя ключевое слово "as":

```
actor Actor as aktep
``` 

Также возможно изменить цвет фона участника:

```
actor Actor #red
```

Возможно изменить порядок следования участников с помощью ключевого слова order:

```
@startuml
participant Last order 30
participant Middle order 20
participant First order 10
@enduml
```

##### Взаимодействие между участниками

Последовательность "->" используется для передачи сообщения (запроса) между двумя участниками. Участники не обязательно должны быть явно объявлены. Чтобы иметь пунктирную стрелку (ответное сообщение), необходимо использовать "-->".

Также можно использовать "<-" и "<--". Это не меняет рисунок, но может улучшить читабельность. Обратите внимание, что это справедливо только для диаграмм последовательности, для других диаграмм правила другие.

```
@startuml
Alice -> Bob: <текст_запроса>     # запрос
Bob --> Alice: <текст_ответа>     # ответ

Alice -> Bob: <текст_запроса>     # ещё один запрос
Alice <-- Bob: <текст_ответа>     # ещё один ответ

Alice -> Alice: <текст_запроса>   # запрос самому себе 
@enduml
```

##### Активация и деактивация линии существования

Ключевые слова "activate" и "deactivate" используются чтобы обозначить активацию участника. Линия существования появляется в момент активации участника. "activate" и "deactivate" применяются к предыдущему сообщению. "destroy" обозначает конец линии существования участника. 

```
@startuml
participant User

User -> A: DoWork
activate A

A -> B: << createRequest >>
activate B

B -> C: DoWork
activate C
C --> B: WorkDone
destroy C

B --> A: RequestCreated
deactivate B

A -> User: Done
deactivate A

@enduml
```

##### Полезные команды

PlantUML позволяет оставлять комментарии:

```
@startuml
Alice->Bob : привет
note left: это первая заметка

Bob->Alice : ага
note right: это другая заметка

Bob->Bob : я размышляю над этим
note left of Alice
заметки
могут занимать
несколько строчек
end note
@enduml
```

Вы можете использовать "|||" чтобы показать промежутки в диаграммах. Также возможно указать промежуток в пикселях. 

```
@startuml

Alice -> Bob: message 1
Bob --> Alice: ok
|||
Alice -> Bob: message 2
Bob --> Alice: ok
||45||
Alice -> Bob: message 3
Bob --> Alice: ok

@enduml
```





