---
title: "ООП y29 и кодстайл ITMO is DEV — правила"
---

# Курс ООП y29


## Инструкции

- [ASAP](https://github.com/itmo-is-dev/asap-docs)
- [Подсказка по исправлению проблем с git](https://dangitgit.com/ru)
- [is-oop-y26 | Воркшоп 1 | Основы C# (Youtube)](https://www.youtube.com/watch?v=Sh6IZzDRPjQ&t=1s)

### Лекции

- Лекция 1 – Основы ООП
- Лекция 2 – SOLID и GRASP
- Лекция 3 – Структурные паттерны
- Лекция 4 - Порождающие паттерны

## Syllabus

### **Лабораторные работы**

Лабораторная работа считается выполненной, если преподаватель оценил её **на очной защите** и баллы за неё появились у вас в
таблице.

#### Причины снижения баллов

1. Дедлайны. У каждой лабораторной работы будет установлен дедлайн. Если работа сдаётся после этого периода, то за каждую неделю
   после дедлайна, возможные к получению баллы уменьшаются на 20% от максимальных баллов за лабораторную работу. (начиная с первой
   недели после дедлайна, т.е. если дедлайн в субботу, а вы сдали в следующий понедельник, то вы получите на 20% меньше баллов)

2. Неполное выполнение. Если лабораторная выполнена не полностью (например, студент отправил пул реквест, чтобы попасть в
   дедлайн), то работа не считается выполненной, отправляется на доработки. Время сдачи в таком случае будет считаться временем
   отправки новой версии.

3. Грубые или систематические ошибки. За определенные ошибки снимаются баллы:
    1. Не следование "Do and don't".
    2. Многократное повторение ошибки на которую уже было указано в ревью.
    3. Разрешение комментариев без фактического изменения кодовой базы.
    4. Большое количество замечаний. В зависимости от их грубости и на усмотрение преподавателя.

4. Нарушение регламента сдачи:
    1. Мердж реквеста без апрува
    2. Плохой нейминг веток, пул реквестов и комитов
    3. Пул реквесты в которые попадает код из других лабораторных или файлы не относящиеся к лабораторной работе в целом.

#### Приоритетная очередь:

Приоритет строится по следующим критериям: (в порядке важности)

- Люди выполняющие текущую лабораторную
- Люди выполнившие лабораторную у которой прошёл дедлайн, залившие выполненную работу до дедлайна
- Люди выполнившие лабораторную у которой прошёл дедлайн, залившие выполненную работу после дедлайна
- Остальные

## Do/Don’t

### **Нейминг**

1. [Следуйте правилам нейминга](https://github.com/itmo-is-dev/.github/blob/master/profile/codestyle/naming.md), используйте
   семантику
2. Не использовать сокращения
3. Использовать общепринятые английские термины для нейминга классов/свойств/методов
    1. Не используйте транслитерацию
    2. Не используйте машинный перевод для исконно русских терминов
    3. Не используйте системные/зарезервированные термины в ваших классах
    4. Если термин является сокращением сам по себе, то используйте CamelCase (Например: вместо HTTP используйте Http)

       Пример плохого нейминга:

        ```csharp
        // Метод добавления студента в подпоток 
        class Thread 
        { 
        	void Join(Student student) { … } 
        }
        ```

4. Познакомиться с кодстайлом, префиксами для интерфейсов

### **Do:**

1. [Следуйте кодстайлу](https://github.com/itmo-is-dev/.github/blob/master/profile/README.md)
2. Следуйте
   правилам [семантического нейминга комитов](https://gist.github.com/joshbuchea/6f47e86d2510bce28f8e7f42ae84c716)
3. Использовать конструкторы для создания полностью инициализированного объекта
4. Минимизировать область доступа к данным, закрывать возможность изменять тип из-вне. Стремиться к минимизации
   статических полей. Если поле класса используется только внутри одного метода - инлайнить, если используется для
   передачи данных между методами - перепроектировать решение.
5. Проверяйте, может ли метод выполниться с переданными аргументами, если эти аргументы - это пользовательский ввод.
6. При реализации методов создания или поиска, стоит возвращать сущности, а не какие-то их части - названия или
   идентификаторы. Если написано, что нужно найти магазин, то ожидается, что вернется не строка, а магазин.
7. Минимизировать использование статических методов, полей и классов. Если в коде была использована статика, то нужно
   обозначить комментарием почему это решение лучше в таком виде, нежели без статики.
8. Стараться минимизировать вложенность за счет инвертирования условий.
9. Делать всю возможную валидацию аргументов в конструкторе
10. Стараться делать типы иммутабельными. Особенно в кейсах, где мутабельность объекта нужно для инициализации вне
    конструктора:

    ```csharp
    // Плохо:
    var group = new Group(); 
    group.Name = "Tasks";
    
    // Хорошо:
    var group = new Group("Tasks"); 
    ```

11. Поддерживать инвариант типа. Никакое изменение не должно делать экземпляр класса не валидным.
12. Разделять бизнес логику и логику работы с UI. Разделять логику, парсинг аргументов и валидацию
13. Если есть зависимость от внешних сущностей, то их нужно прокидывать аргументами.
14. Старайтесь вместо множества вложенных операторов выделить все граничные условия и обработать их в самом начале
    метода для достижения большей читаемости кода.
    см.[https://refactoring.guru/ru/replace-nested-conditional-with-guard-clauses](https://refactoring.guru/ru/replace-nested-conditional-with-guard-clauses)
15. Используйте свойства/автосвойства вместо геттер/сеттер методов.
16. Использовать LINQ для работы с коллекциями (вместо написания своих вариантов итерации).
17. Используйте
    подход [Arrange-Act-Assert](https://docs.microsoft.com/ru-ru/visualstudio/test/unit-test-basics?view=vs-2019#write-your-tests)
    при написании ваших тест-кейсов (предпочитаемо явно разделять секции комментариями).
18. Использовать в тестах специализированные проверки вместо общих, по типу
    `Assert.Contains(…)` вместо `Assert.True(collection.Contains(…))`.
19. Стараться работать с абстракциями, а не с конкретными видами коллекций

```csharp
// Плохо:
List<int> FindOddNumbers(int[] numbers) 
{
    return numbers.Where(x => x % 2 == 0).ToList();
}

// Хорошо:
IEnumerable<T> FindOddNumbers(IReadOnlyCollection<T> numbers) where T : INumber 
{
    return numbers.Where(x => x % 2 == 0);
}
```

20. Использовать ограничения для явного указания поддерживаемых generic типов (см. пример выше)
21. Соблюдайте принципы [DRY, KISS, YAGNI](https://habr.com/ru/articles/144611/)

- **DRY - Don’t repeat yourself**. Вместо копирования одного куска кода, рекомендуется вынести его в метод для
  дальшейшего переиспользования.
- **KISS - Keep it stupid simple**. Старайтесь делать методы максимально атомарными и не переусложнять логику. Для
  большой сложной операции рекомендуется декомпозировать сценарий на несколько простых.
- **YAGNI - You ain’t gonna need this**. Не добавляйте преждевременные абстракции для того, чтобы поддержать какой-то
  сценарий из будущего, для которого ещё неизвестны бизнес требования. Проектируйте непосредственно ту предметную
  область, которая описана в текущей задаче.

### **Don't:**

1. Не вносить изменения в различные файлы конфигурации без апрува преподавателей.
2. Не используйте в коде магические числа. Имеет смысл выносить как константное поле, чтобы по его названию можно было
   понять, что это.
3. Не работать с потоками ввода-вывода в бизнес-логике
4. Ловить и игнорировать исключение, которое не может быть обработано
5. Не используйте default или специализированные (-1, int.MaxValue и т.д.) значения как определение того, что значение
   не найдено. Если метод может не найти результат, то метод нужно называть Find и он должен вернуть null в случае
   ссылочных типов. Для примитивов стоит использовать Nullable. Для коллекций стоит возвращать пустой список или массив,
   если ничего не нашлось, а не null.
6. Избегайте кастов там, где можно их не использовать. Программа должна стремиться к повышению типизации и увеличении
   количества мест, где происходят проверки во время компиляции.
7. Минимизировать количество [down casting](https://qna.habr.com/q/448799). Стараться не использовать более общие типы в
   сигнатурах, если они не поддерживаются.
8. Не использовать Tuple, ValueTuple и KeyValuePair, Dictionary (I/IReadOnly) в сигнатурах методов.
   Используйте свой `Discriminated Union` / `Value Object` / `Data Transfer Object` для передачи множества значений в
   качестве параметров/результатов.
9. Не оставлять код, который не нужен или не используется
10. Не нужно комментировать очевидные места

    ```csharp
    static class Program 
    {
        // Точка входа в программу
        static void Main(string[] args) 
        {
            // Вывод привет мир в консоль
            Console.WriteLine("Hello, world!");
        }
    }
    ```

11. Не использовать наследование для переиспользования логики. Если объект наследуется, то справедливым должно быть
    высказывание, что производный объект является базовым (
    см. [LSP](https://www.csharptutorial.net/csharp-design-patterns/csharp-liskov-substitution-principle/)).
12. Не используйте циклы для перебора коллекций ради того чтобы в теле цикла вернуть/найти объект или собрать лист
    значений. Воспользуйтесь LINQ, а именно: `.SelectMany()`, `.Where()`, `.FirstOrDefault()`
13. Не использовать Reflection.
14. Не использовать boolean флаги, для того чтобы управлять условиями выхода из цикла.
15. Не использовать SQL-like синтаксис для написания LINQ.
16. Не использовать конструкции вида `.ToList().ForEach(...)` / `.ToList().Select(...)` для итерации по колекциям. (
    Итерация после вызова терминальной операции)
17. Не использовать регулярные выражения
18. Не использовать null forgiving operator (`!`)
19. Не подавлять ошибки статического анализатора (например через `#pragma disable`)
20. Не использовать публичные поля или приватные свойства
21. Не используйте коллекции из namespace’а **System.Collections.ObjectModel**
22. Не бросайте исключения в случае ошибок бизнес логики
23. Не использовать примитивы языка для ограничения области допустимых значений каких либо доменных примитивов.
    1. Пример 1: если ваш домен подразумевает, что какой-то атрибут не может быть отрицательным – не стоит использовать
       `uint` в качестве его типа. Вместо этого определите собственный value object, инкапсулирующий эту валидацию.
    2. Пример 2: если ваш домен подразумевает, что какой-то атрибут может иметь значения только от 0 до 255 – не стоит
       использовать `byte` в качестве его типа. Если это ограничение неявно следует из доменных правил – просто
       воспользуйтесь типом `int`, если это ограничение явно задаётся доменными правилами – определите собственный value
       object, инкапсулирующий эту валидацию.
    > Зачастую код, вызывающий вашу логику не будет использовать эти "специальные" типы данных (byte, short, float,
    uint, ulong). Поэтому, если вы будете использовать их в своём коде, то взаимодействие с ним может обрасти множеством
    кастов, что является не самой лучшей практикой.

    > Также в C# у численных литералов есть типы, которые они используют по умолчанию: `int` – для целочисленных
    значений, если значение литерала подходит под область значений Int32, `long` – для целочисленных значений, если
    значение литерала выходит за пределы Int32, `double` – для дробных значений.
    Если преобразование `int` –> `long` происходит неявно, то преобразование `double` –> `float` – нет, аналогично с
    целочисленными типами, имеющие меньшую область значений чем Int32 (`short`, `byte`).
    Поэтому использование типов, с меньшей областью допустимых значений повлечёт за собой либо лишние касты, либо явных
    указаний типов в литералах, что усложняет читаемость кода.

---

# Кодстайл ITMO is DEV

## General

1. Код должен быть простым, ясным и читаемым, в той мере, в которой это возможно для реализации требуемой функциональности.
2. Код должен быть самодокументируемым. Следует избегать костылей и воркэраундов, проектируя архитектуру и решения так, чтобы в них не возникало необходимости. Комментируйте только действительно нетривиальные вещи (почему сделано именно так, внешние ограничения) — если решение требует комментария, для этого должна быть веская причина.
3. Нужно стремиться к минимизации статических методов и классов.

## Naming

1. Основой нейминга является кодстайл майкрософта: <https://learn.microsoft.com/en-us/dotnet/standard/design-guidelines/naming-guidelines>;
2. Имена должны быть читабельными и понятными, без сокращений и грамматических ошибок во всех идентификаторах (классы, методы, свойства, переменные). Исключение – общепринятые сокращения, напр. `i`, `j`, `k` в циклах;

```csharp
// ПЛОХО
public class StudRepo { ... }
public void CalcAvgGrade() { ... }

var a = new List<Student>();
var stds = new List<Student>();
var list = new List<Student>();

// ХОРОШО
public class StudentRepository { ... }
public void CalculateAverageGrade() { ... }

var students = new List<Student>();
```
3. Не используйте отрицание в названиях (например, `isNotValid`, `hasNoAccess`). Отрицание в имени создает лишнюю когнитивную нагрузку и требует мысленного разворачивания дополнительной логической инверсии при чтении условий, особенно в комбинации с проверками (например, `isNotValid is false`):

```csharp
bool isRed = color == Colors.Red; // Good
bool isNotBlue = color != Colors.Blue; // Bad

if (isRed is false // Ok
    && isNotBlue is false) // Трудно воспринимать (двойное отрицание)
    return ...
```
4. Избегайте конструкций с предлогом `Of` вида `<характеристика>Of<Сущность>` (например, `numberOfStudents`, `countOfOrders`, `listOfUsers`). Размещайте ключевую сущность в начале, а уточняющую характеристику — в качестве суффикса: `<сущность><Характеристика>` (`studentsCount`, `ordersCount`), либо используйте множественное число для коллекций (`students`, `users`). Это делает названия чище и логичнее группирует переменные.

```csharp
// ПЛОХО
int numberOfStudents = 10;
int countOfOrders = 5;
List<User> listOfUsers = GetUsers();

// ХОРОШО
int studentsCount = 10;
int ordersCount = 5;
IReadOnlyCollection<User> users = GetUsers();
```
5. Придерживайтесь нейминга в соответствии с [A/HC/LC Pattern'ом](https://github.com/kettanaito/naming-cheatsheet#ahclc-pattern).  
   Имя состоит из `prefix? + action (A) + high context (HC) + low context? (LC)`:
   1. `Action` (A) — действие, которое выполняется (`Get`, `Set`, `Create`, `Remove`, etc.)
   2. `High Context` (HC) — ключевая сущность, над которой совершается действие (`User`, `Order`, etc.)
   3. `Low Context` (LC) — зависимая сущность, детализация или модификатор (`Assignments`, `ById`, `Status`, etc.)

```csharp
// ПЛОХО
public IEnumerable<Assignment> GetAssignmentsUser(Guid userId); // Нарушен порядок: LC перед HC
public void UserPasswordUpdate(User user, string password);    // Action в конце, а не в начале
public IEnumerable<Assignment> GetAssignments(Guid userId);    // Отсутствует HC — неясен контекст сущности

// ХОРОШО
// Action (Get) + HC (User) + LC (Assignments)
public IEnumerable<Assignment> GetUserAssignments(Guid userId);

// Action (Update) + HC (User) + LC (Password)
public void UpdateUserPassword(User user, string password);
```

### Префиксы

1. Для методов получения/доступа к данным используйте префиксы **`Find`** и **`Get`** в зависимости от гарантии существования результата:
   - **`Find`** — используется, когда объект может отсутствовать. Метод возвращает nullable-тип (`T?`) или `null`, если элемент не найден, и **не** бросает исключение при отсутствии данных.
   - **`Get`** — используется, когда объект гарантированно должен существовать. Метод возвращает non-nullable значение (`T`) и **обязан** выбросить исключение, если объект не найден.

```csharp
// ПЛОХО
// Get возвращает null вместо непустого значения
public Student? GetStudent(int id)
{
    return _students.FirstOrDefault(s => s.Id == id);
}

// Find бросает исключение при отсутствии сущности
public Student FindStudent(int id)
{
    return _students.Single(s => s.Id == id);
}

// ХОРОШО
// Find возвращает null, если студент не найден
public Student? FindStudent(int id)
{
    return _students.FirstOrDefault(s => s.Id == id);
}

// Get гарантированно возвращает студента либо выбрасывает исключение
public Student GetStudent(int id)
{
    Student? student = FindStudent(id);

    if (student is null)
        throw new NotFoundException($"Student with id {id} was not found.");

    return student;
}
```

2. Методы, пытающиеся выполнить действие или получение данных, которые могут завершиться неудачей без выброса исключения, должны иметь префикс `Try` и возвращать `bool` (в том числе в рамках классического .NET Try-паттерна с `out` параметром).

```csharp
// ПЛОХО: метод с префиксом Try возвращает void, статус выполнения операции неизвестен
public void TryWithdrawMoney(CreditCard creditCard, int password, double moneyToWithdraw)
{
    if (creditCard.IsPasswordCorrect(password))
        creditCard.Withdraw(moneyToWithdraw);
}

// ХОРОШО: метод возвращает bool, отражающий успешность операции
public bool TryWithdrawMoney(CreditCard creditCard, int password, double moneyToWithdraw)
{
    if (creditCard.IsPasswordCorrect(password) is false)
        return false;

    creditCard.Withdraw(moneyToWithdraw);
    return true;
}

// ХОРОШО: классический Try-паттерн с out-параметром
// [NotNullWhen(true)] указывает компилятору, что если метод вернул true, то student гарантированно не null
public bool TryFindStudent(int id, [NotNullWhen(true)] out Student? student)
{
    student = _students.FirstOrDefault(s => s.Id == id);
    return student is not null;
}
```

## Formatting

1. Добавляйте переносы строк до и после многострочных элементов кода (кроме случаев когда элемент находится в конце блока). 
Однострочные элементы кода можно группировать без пропуска строк.

#### Хорошо
```csharp
var location = "Yerevan";
var age = 69;

var relevantStudents = _students
   .Where(x => x.Location.Equals(location))
   .Where(x => x.Age.Equals(age));
   
foreach (var student in relevantStudents)
{
   Console.WriteLine($"Найден дед - {student.Name}");
}
```

#### Плохо
```cs
var location = "Yerevan";
var age = 69;
var relevantStudents = _students
   .Where(x => x.Location.Equals(location))
   .Where(x => x.Age.Equals(age));
foreach (var student in relevantStudents)
{
   Console.WriteLine($"Найден дед - {student.Name}");
}
```

2. Добавляйте перенос строки перед оператором `return`.

#### Хорошо
```csharp
public double Calculate(double width, double height)
{
    var baseArea = width * height;
    var scale = baseArea / 2.0;
   
    return baseArea + scale;
}
```

#### Плохо
```csharp
public double Calculate(double width, double height)
{
    var baseArea = width * height;
    var scale = baseArea / 2.0;
    return baseArea + scale;
}
```

## Variable and operator declaration

1. Для неочевидных числовых значений необходимо создавать именованные константы. Не используйте в коде магические числа.

```csharp
// ПЛОХО
public Student AddStudent(string name, string surname)
{
   var student = new Student(name, surname);

   // сравниваем с магическим числом
   if (_students.Count >= 20)
   {
      throw new Exception("Students limit exceeded");
   }

   _students.Add(student);

   return student;
}

// ХОРОШО
public Student AddStudent(string name, string surname)
{
   var student = new Student(name, surname);

   // сравниваем с читаемой константой
   if (_students.Count >= MaxStudentsAmount)
   {
      throw new Exception("Students limit exceeded");
   }

   _students.Add(student);

   return student;
}
```

2. Используйте `var`, только если тип переменной понятен из контекста (например, при инициализации через конструктор). Если тип неочевиден или является встроенным, указывайте тип явно. Правила и инспекции IDE / `.editorconfig` имеют приоритет над описанием в данном документе.

```csharp
// ПЛОХО
var percents = bankAccount.CalculatePercents();
var count = 0;

// ХОРОШО
Money percents = bankAccount.CalculatePercents();
int count = 0;
var students = new List<Student>();
```

3. Задавайте `default` ветку в операторе `switch` (или `_` в switch-выражениях). Если поведение не определено — выбрасывайте исключение. Предпочитайте switch-выражения (`switch expressions`) классическим операторам `switch`.

```csharp
// ПЛОХО: отсутствие обработки неопределенного поведения
switch (deposit)
{
   case < 30:
      Console.WriteLine("Your percent is 3");
      break;
   case < 50:
      Console.WriteLine("Your percent is 5");
      break;
}

// ХОРОШО: использование switch expression и явный выброс исключения в default-ветке
decimal percent = deposit switch
{
    < 30 => 3m,
    < 50 => 5m,
    _ => throw new InvalidOperationException($"Unexpected deposit value: {deposit}"),
};
```

4. При сравнении переменной с константой сначала указывается переменная, потом константа.

```csharp
// ПЛОХО
if (MaxStudentsAmount <= _students.Count)
{
   throw new InvalidOperationException("Students limit exceeded");
}

// ХОРОШО
if (_students.Count >= MaxStudentsAmount)
{
   throw new InvalidOperationException("Students limit exceeded");
}
```

5. Локальные переменные должны объявляться и инициализироваться как можно ближе к месту их непосредственного использования.

```csharp
// ПЛОХО
public void ProcessNumbers(IEnumerable<int> numbers)
{
   var oddOnly = new List<int>();
   var oddUnique = new List<int>();
   int count;

   // ...вычисления...
   oddOnly.AddRange(numbers.Where(x => x % 2 != 0));

   // ...вычисления...
   oddUnique.AddRange(oddOnly.Distinct());
}

// ХОРОШО
public void ProcessNumbers(IEnumerable<int> numbers)
{
   var oddOnly = numbers.Where(x => x % 2 != 0).ToList();
   // ...вычисления...

   var oddUnique = oddOnly.Distinct().ToList();
   // ...вычисления...
}
```

6. Минимизируйте уровень вложенности, где это возможно без потери читаемости (Guard Clauses). Этого можно добиться ранним выходом (`return` / `throw`), инвертированием условного оператора `if` ([Replace Nested Conditional with Guard Clauses](https://refactoring.com/catalog/replaceNestedConditionalWithGuardClauses.html)), а также использованием встроенных `ThrowIf*` методов (`ArgumentNullException.ThrowIfNull`, `ArgumentOutOfRangeException.ThrowIfNegativeOrZero` и т.д.).

```csharp
// ПЛОХО: лишняя вложенность через else и ручные проверки аргументов
if (amount <= 0)
{
    throw new ArgumentOutOfRangeException(nameof(amount));
}
else
{
    if (_students.Count >= MaxStudentsAmount)
    {
        throw new InvalidOperationException("Students limit exceeded");
    }
    else 
    {
        _students.Add(student);
        return student;
    }
}

// ХОРОШО: Guard Clauses и встроенные Throw-хелперы
ArgumentOutOfRangeException.ThrowIfNegativeOrZero(amount);

if (_students.Count >= MaxStudentsAmount)
{
    throw new InvalidOperationException("Students limit exceeded");
}

_students.Add(student);

return student;
```

7. Не используйте искусственные boolean-флаги для управления условиями выхода из цикла (когда можно использовать `break`, `return` или понятное условие завершения).

```csharp
// ПЛОХО: управление выходом через внешний флаг-мутатор
var isFound = false;
foreach (var student in students)
{
    if (isFound is false && student.Id == targetId)
    {
        ProcessStudent(student);
        isFound = true;
    }
}

// ХОРОШО: немедленный выход через break или return
foreach (var student in students)
{
    if (student.Id == targetId)
    {
        ProcessStudent(student);
        break;
    }
}
```

8. Предпочитайте `condition is false` вместо `!condition` (not pattern).

```csharp
// ПЛОХО
if (!isFound)
{
   ...
}

// ХОРОШО
if (isFound is false)
{
   ...
}
```

## Type declaration

1. Инициализация полей должна происходить в конструкторе, а не при их объявлении. Исключение — инициализация пустых коллекций (например, `new List<T>()`) и базовых структур по умолчанию.

```csharp
// ПЛОХО: нетривиальная инициализация или создание зависимостей при объявлении поля
public class OrderService
{
    private readonly IUserRepository _userRepository = new UserRepository();
    private readonly DateTime _createdAt = DateTime.UtcNow;
}

// ХОРОШО: инициализация зависимостей в конструкторе; пустые коллекции допустимо инициализировать inline
public class OrderService
{
    private readonly List<Order> _orders = new List<Order>();
    private readonly IUserRepository _userRepository;
    private readonly DateTime _createdAt;

    public OrderService(IUserRepository userRepository, DateTime createdAt)
    {
        _userRepository = userRepository;
        _createdAt = createdAt;
    }
}
```
2. Конструкторы должны полностью инициализировать объект. Валидация аргументов должна происходить в конструкторах.
3. Минимизируйте область доступа к данным. Предпочтительней хранить информацию в приватных полях нежели в публичных свойствах. Методы, которые не нужны внешнему коду, нужно делать приватными.
4. Не оставляйте мутабельные поля для отложенной инициализации. Инициализируйте поля в конструкторах и делайте иммутабельные поля и свойства, где это уместно.
5. Не использовать поля для передачи данных внутри метода или между методами класса.

```csharp
// ПЛОХО: использование поля для передачи промежуточного состояния/данных между методами
public class OrderProcessor
{
    private decimal _discountAmount;

    public void Process(Order order)
    {
        CalculateDiscount(order);
        ApplyDiscount(order);
    }

    private void CalculateDiscount(Order order)
    {
        _discountAmount = order.Total * 0.1m;
    }

    private void ApplyDiscount(Order order)
    {
        order.Total -= _discountAmount;
    }
}

// ХОРОШО: передача данных через аргументы и возвращаемые значения методов
public class OrderProcessor
{
    public void Process(Order order)
    {
        var discountAmount = CalculateDiscount(order);
        ApplyDiscount(order, discountAmount);
    }

    private decimal CalculateDiscount(Order order)
    {
        return order.Total * 0.1m;
    }

    private void ApplyDiscount(Order order, decimal discountAmount)
    {
        order.Total -= discountAmount;
    }
}
```
6. Поддерживайте инвариант типа. Если у типа есть несколько полей, которые между собой связаны, то не должно быть способа изменить одно из полей и нарушить связь между ними.
7. Члены класса должны располагаться [в следующем порядке](https://github.com/DotNetAnalyzers/StyleCopAnalyzers/blob/master/documentation/SA1201.md):
   1. Константы
   2. Поля
   3. Конструкторы и Create-методы
   4. Свойства
   5. Публичные методы
   6. Приватные методы
8. Нумерация значений енама должна начинаться с 1. 0 должен быть использован для неопределённых значений.
9. Не используйте приватные свойства.
10. Не используйте публичные поля.
11. Не используйте оператор `==` для сравнения не числовых типов. Не переопределяйте оператор `==` для не числовых типов.
12. Не используйте наследование для переиспользования логики. Если объект наследуется, то справедливым должно быть высказывание, что производный объект является базовым (см. LSP).

## Method declaration

1. Метод, возвращающий коллекцию, в случае отсутствия элементов для возврата, должен возвращать пустую коллекцию, а не
   null.

```csharp
// ПЛОХО
public List<Student>? FindStudents(int course)
{
    List<Student>? students = null;

    /* ищем студентов любым возможным методом */

    // если студенты не нашлись, возвращаем null
    if (students is null || students.Count == 0)
        return null;

    // возвращаем студентов, если хоть кто-то нашёлся
    return students;
}

// ХОРОШО
public List<Student> FindStudents(int course)
{
    // создаём пустой лист
    var students = new List<Student>();

    /* ищем студентов любым возможным методом */

    // возвращаем студентов даже, если это пустой лист (не null)
    return students;
}
```

2. Метод, который работает с пользовательскими аргументами, должен валидировать их.

```csharp
// ПЛОХО
public void FindStudentByFullName(string name, string surname)
{
    /* поиск студента без проверки входных данных */
}

// ХОРОШО
public void FindStudentByFullName(string name, string surname)
{
    ArgumentException.ThrowIfNullOrWhiteSpace(name);
    ArgumentException.ThrowIfNullOrWhiteSpace(surname);

    /* поиск студента после проверки входных данных */
}
```

3. В конструкторе должен соблюдаться порядок инициализации:
    1. Валидация аргументов
    2. Инициализация, которая не зависит от аргументов
    3. Инициализация полей аргументами
    4. Инициализация, которая требует какой-то логики, вызовов методов

```csharp
// ХОРОШО
public MegaFaculty(string facultyName)
{
    // валидация
    ArgumentException.ThrowIfNullOrWhiteSpace(facultyName);

    // инициализация, не зависящая от аргументов
    _courses = new List<OgnpCourse>();

    // инициализация полей аргументами
    Name = facultyName;

    /* сложная инициализация с вызовом различных методов */
    NotifyISU(this);
}
```

## Property declaration

1. При объявлении автосвойств, помещайте аксессоры на одной строке с названием и типом
```csharp
// ПЛОХО
public int Value
{ get; set; }

// ХОРОШО
public int Value { get; set; }
```
2. При объявлении get-only свойств, используйте bodied expressions вместо явного `get` аксессора
```csharp
// ПЛОХО
public IReadOnlyCollection<string> Values
{
    get 
    {
        return _values;
    }
}

public IReadOnlyCollection<string> Values
{
    get => _values;
}

// ХОРОШО
public IReadOnlyCollection<string> Values => _values;
```

## Exceptions

1. Все производные от Exception классы должны иметь постфикс "Exception".
2. Для негативных исходов бизнес-логики стоит использовать Result-тип. Исключения выбрасывать стоит только при действительно исключительных ситуациях, которые нельзя обработать, или при валидации параметров (для стандартных ошибок валидации аргументов стоит использовать стандартные типы).
3. Нужно обрабатывать, где это оправдано, ошибки NRE, OutOfRange etc и вместо них бросать более понятные ошибки, которые описывают проблемную ситуацию.
4. Если ошибка не может быть обработана, то её необходимо прокидывать дальше, а не игнорировать.
5. Если возникает ошибка при валидации аргументов, то нужно указывать, какой именно аргумент приводит к ошибке в тексте ошибки.

## Common

1. Методы расширения должны выделяться в специальные классы. Они должны иметь соответствующий постфикс Extensions.
2. Весь исходный код должен быть написан на английском. Это касается нейминга, комментариев и ошибок. Если есть необходимость использовать другой язык, то нужно применить инструменты локализации.
3. Для обозначения отсутствия значения стоит использовать null, а не default. Для значимых типов стоит возвращать Nullable<T>.
4. Избегайте кастов там, где можно их не использовать. Программа должна стремиться к повышению типизации и увеличению количества мест, где происходят проверки во время компиляции.
5. Минимизируйте количество ап кастов. Старайтесь не использовать более общие типы в сигнатурах, если они не поддерживаются.
6. При написании цепочки вызовов методов, переносите каждый вызов на отдельную строку, начиная строку с точки.

```csharp
// ПЛОХО
var result = users.Where(u => u.IsActive).OrderBy(u => u.Name).Select(u => u.Email).ToList();

var result = users.
    Where(u => u.IsActive).
    OrderBy(u => u.Name).
    Select(u => u.Email).
    ToList();

// ХОРОШО
var result = users
    .Where(u => u.IsActive)
    .OrderBy(u => u.Name)
    .Select(u => u.Email)
    .ToList();
```
7. Для проверки на null использовать конструкции `is null` и `is not null`. Не используйте операторы `== null` и `!= null`, так как операторы `==` и `!=` могут быть перегружены.

```csharp
// ПЛОХО: операторы == и != могут быть перегружены
if (user == null)
{
}

if (user != null)
{
}

// ХОРОШО
if (user is null)
{
}

if (user is not null)
{
}
```
8. Используйте Type.Parse вместо Convert.ToType (например, int.Parse вместо Convert.ToInt32).
9. Название namespace должно содержать название проекта и все папки через точку, ведущие от корня проекта к текущему файлу.
    
    Пример структуры проекта: 
    ```
    Project
        Users
            Models
            Entities
                Student.cs
            Services
        Orders
            Models
            Entities
            Services
    ```
    При такой структуре проекта название namespace в файле Student.cs будет Project.Users.Entities

## Restrictions

1. Не используйте dynamic.
2. Не используйте goto.
3. Не пишите касты для своих типов - implicit или explicit.
4. Не используйте публичные вложенные типы.
5. Не используйте модификатор доступа internal. Исключение - если нет возможности использовать другой.
6. Не используйте reflection для доступа к полям.
7. Не используйте query-like LINQ.
8. Не используйте Tuple, ValueTuple и KeyValueTuple в сигнатурах своих методов. Вводите специальные типы, которые лучше
   описывают данную структуру.
9. Не пишите в лямбдах больше одной операции, выносите сложную логику в методы.
10. Не используйте char, short для экономии памяти. Большинство интерфейсов работают с int, а значит в коде появится
    много кастов, которые усложняют код.
11. Не используйте unsigned для гарантии, что значение будет больше нуля. Большинство интерфейсов работают с int, а
    значит в коде появится много кастов, которые усложняют код.
12. Не делайте избыточных проверок на null в коде бизнес-логики. Проверки на null (в любом виде: `is null`,
    `ArgumentNullException.ThrowIfNull` и др.) должны выполняться на границах системы при работе с данными, полученными
    извне (пользовательский ввод, БД, интеграции по сети). Внутри бизнес-логики следует полагаться на систему типов и
    nullable-аннотации. Это ограничение не затрагивает комбинированные проверки (например, `string.IsNullOrEmpty`,
    `string.IsNullOrWhiteSpace`, `ArgumentException.ThrowIfNullOrWhiteSpace`).

## Suggestions

1. При реализации методов создания или поиска, стоит возвращать сущности, а не какие-то их части - названия или идентификаторы. Если написано, что нужно найти магазин, то ожидается, что вернется не строка, а магазин.
2. Используйте специализированные проверки вида CollectionAssert.Contains(...) вместо Assert.IsTrue(collection.Contains(...)).
3. Не пишите сложную логику поверх примитивных типов, вводите информативные обёртки, в которых можно инкапсулировать валидацию и логику.
4. Стоит отделять логику ввода, вывода и бизнес-логику.
5. Для простых DTO, где это возможно, стоит использовать `record`.
