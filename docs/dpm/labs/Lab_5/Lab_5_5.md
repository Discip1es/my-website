# Изменение содержимого строк с использованием встроенных методов строковых типов данных в C#.

## Введение
Предположим, вы являетесь разработчиком приложения, позволяющего предприятию обновлять свой веб-сайт «Предложения последнего шанса» путем отправки электронного письма. Обновление электронной почты использует специальный обязательный текст в заголовке и теле письма, чтобы указать автоматике, как обновлять сайт. В письме указывается название следующей сделки, % скидки, срок действия и время публикации предложения в прямом эфире.

Часто данные приложения, с которыми вам нужно работать, поступают из других программных систем и содержат данные, которые вам не нужны. Иногда данные имеют непригодный формат, содержат лишнюю информацию, из которой сложно извлечь важную информацию. Чтобы скорректировать данные для вашего приложения, вам нужны инструменты и методы для разбора строковых данных, выделения нужной вам информации и удаления ненужной.

В этом модуле вы используете методы-помощники строк для определения и выделения интересующей вас информации. Вы узнаете, как скопировать меньшую часть большой строки. Вы замените символы или удалите их из строки.

К концу этого модуля вы сможете изменять содержимое строки, выделяя в ней определенные фрагменты для извлечения, замены или удаления.

### Цели обучения
В этом модуле вы узнаете как:

- Определять положение символа или строки внутри другой строки
- Извлекать фрагменты строк
- Удалять фрагменты строк
- Заменять значения в строках другими значениями

## Используйте вспомогательные методы строки IndexOf() и Substring()

В этом упражнении вы используете метод IndexOf() для определения положения одного или нескольких символов строки внутри большей строки. С помощью метода Substring() вы вернете часть большей строки, которая следует за указанными вами позициями символов.

Вы также используете перегруженную версию метода Substring() для установки длины символов, возвращаемых после указанной позиции в строке.

### Напишите код для поиска пар скобок, встроенных в строку.

1. Убедитесь, что у вас открыт Visual Studio и Program.cs отображается на панели редактора. Program.cs должен быть пустым. Если это не так, выберите и удалите все строки кода.
2. Введите следующий код в редактор кода Visual Studio.
```cs
string message = "Find what is (inside the parentheses)";

int openingPosition = message.IndexOf('(');
int closingPosition = message.IndexOf(')');

Console.WriteLine(openingPosition);
Console.WriteLine(closingPosition);
```
3. Вы должны увидеть следующий вывод:
```
13
36
```
В этом случае индекс символа ( равен 13. Помните, что эти значения начинаются с нуля, поэтому это 14-й символ в строке. Индекс символа ) равен 36.

Теперь, когда у вас есть два индекса, вы можете использовать их в качестве границ для извлечения значения между ними.

### Добавьте код для извлечения значения в скобках
1. Обновите свой код в редакторе кода Visual Studio следующим образом:
```cs
string message = "Find what is (inside the parentheses)";

int openingPosition = message.IndexOf('(');
int closingPosition = message.IndexOf(')');

// Console.WriteLine(openingPosition);
// Console.WriteLine(closingPosition);

int length = closingPosition - openingPosition;
Console.WriteLine(message.Substring(openingPosition, length));
```
2. Сохраните файл кода, а затем используйте Visual Studio для запуска кода. Вы должны увидеть следующий вывод:
```
(inside the parentheses
```
Методу Substring() требуется начальная позиция и количество символов, или длина, для извлечения. Поэтому вы вычисляете длину во временной переменной length и передаете ее вместе со значением openingPosition, чтобы получить строку внутри круглой скобки.

Результат близок, однако вывод включает открывающую скобку. В этом упражнении включение круглой скобки нежелательно. Чтобы убрать скобку из вывода, нужно обновить код, чтобы пропустить индекс самой скобки.

### Изменить начальную позицию подстроки
1. Обновите свой код в редакторе кода Visual Studio следующим образом:
```cs
string message = "Find what is (inside the parentheses)";

int openingPosition = message.IndexOf('(');
int closingPosition = message.IndexOf(')');

openingPosition += 1;

int length = closingPosition - openingPosition;
Console.WriteLine(message.Substring(openingPosition, length));
```
2. Сохраните файл кода, а затем используйте Visual Studio для запуска кода. Вы должны увидеть следующий вывод:
```
inside the parentheses
```
3. Уделите немного времени просмотру предыдущего кода и строки openingPosition += 1;. 

Увеличивая openingPosition на 1, вы пропускаете открывающую скобку. 

Причина, по которой вы используете значение 1, заключается в том, что это длина символа. Если вы попытаетесь найти значение, начинающееся после более длинной строки, например, \<div\> или ---, вы должны использовать длину этой строки.

4. Обновите свой код в редакторе кода Visual Studio следующим образом:
```cs
string message = "What is the value <span>between the tags</span>?";

int openingPosition = message.IndexOf("<span>");
int closingPosition = message.IndexOf("</span>");

openingPosition += 6;
int length = closingPosition - openingPosition;
Console.WriteLine(message.Substring(openingPosition, length));
```
5. Уделите немного времени просмотру предыдущего кода и строки openingPosition += 6;. 

Предыдущий фрагмент кода показывает, как найти значение внутри открывающего и закрывающего тега \<span\>. 

В этом случае вы добавляете 6 к openingPosition в качестве смещения для вычисления длины подстроки.

### Избегайте магических значений

Жестко закодированные строки, такие как «\<span\>» в предыдущем листинге кода, известны как «магические строки», а жестко закодированные числовые значения, такие как 6, известны как «магические числа». Эти «магические» значения нежелательны по многим причинам, и вы должны стараться избегать их, если это возможно.

1. Просмотрите предыдущий код, чтобы понять, как код может сломаться, если вы жестко закодировали строку "\<span\>" несколько раз в своем коде, но неправильно написали один ее экземпляр как "\<sapn\>". 

Компилятор не отлавливает "\<sapn\>" во время компиляции, потому что значение находится в строке. Ошибка в написании приводит к проблемам во время выполнения, и в зависимости от сложности вашего кода ее может быть трудно отследить. 

Более того, если вы измените строку "\<span\>" на более короткую "\<div\>", но забудете изменить число 6 на 5, то ваш код выдаст нежелательные результаты.

2. Обновите свой код в редакторе кода Visual Studio следующим образом:
```cs
string message = "What is the value <span>between the tags</span>?";

const string openSpan = "<span>";
const string closeSpan = "</span>";

int openingPosition = message.IndexOf(openSpan);
int closingPosition = message.IndexOf(closeSpan);

openingPosition += openSpan.Length;
int length = closingPosition - openingPosition;
Console.WriteLine(message.Substring(openingPosition, length));
```
3. Потратьте минуту на изучение обновленного кода и использование ключевого слова const, как это сделано в const string openSpan = «\<span\>»;.

В коде используется константа с ключевым словом const. Константа позволяет определить и инициализировать переменную, значение которой никогда не может быть изменено. Затем вы будете использовать эту константу в остальной части кода всякий раз, когда вам понадобится это значение. Это гарантирует, что значение будет определено только один раз, а неправильное написание const-переменной будет отлавливаться компилятором.

Предыдущий листинг кода — это более безопасный способ написать тот же код, который вы рассмотрели в предыдущем разделе. Теперь, если значение openSpan изменится на \<div\>, строка кода, которая использует свойство Length, останется действительной.

### Выводы

В этом модуле мы изучили много материала. Вот самое важное, что следует запомнить:

- IndexOf() дает вам первую позицию символа или строки внутри другой строки.
- IndexOf() возвращает -1, если не может найти совпадение.
- Substring() возвращает только указанную часть строки, используя начальную позицию и необязательную длину.
- Часто существует более одного способа решения проблемы. Вы использовали два разных метода, чтобы найти все экземпляры заданного символа или строки.
- Избегайте жестко закодированных магических значений. Вместо этого определите переменную const. Значение константной переменной не может быть изменено после инициализации.

## Используйте вспомогательные методы строки IndexOf() и LastIndexOf()

В этом упражнении мы используем методы IndexOf() и LastIndexOf() для поиска местоположения символов и строк в заданной строке.

### IndexOf() и LastIndexOf

Метод .IndexOf() возвращает индексную позицию первого вхождения символа или строки в данной строке. Метод .LastIndexOf() возвращает позицию индекса последнего вхождения символа или строки в данной строке. Оба метода Indexof() и LastIndexOf() возвращают -1, если символ или строка не найдены.

1. Выберите и удалите все строки кода в редакторе кода Visual Studio. 
2. Обновите свой код в редакторе кода Visual Studio следующим образом:
```cs
string message = "hello there!";

int first_h = message.IndexOf('h');
int last_h = message.LastIndexOf('h');

Console.WriteLine($"For the message: '{message}', the first 'h' is at position {first_h} and the last 'h' is at position {last_h}.");
```
3. Cохраните файл кода, а затем используйте Visual Studio для запуска кода. Вы должны увидеть следующий вывод:
```
For the message: 'hello there!', the first 'h' is at position 0 and the last 'h' is at position 7.
```
Выходные данные идентифицируют первую и последнюю «h» в строке «hello there!» в позиции 0 и позиции 7.

### Извлечь последнее вхождение подстроки

Вы увеличиваете сложность переменной message, добавляя множество наборов круглых скобок, а затем пишете код для получения содержимого внутри последнего набора круглых скобок.

1. Выделите и удалите все строки кода в редакторе кода Visual Studio.

2. Обновите код в редакторе кода Visual Studio следующим образом:
```cs
string message = "(What if) I am (only interested) in the last (set of parentheses)?";
int openingPosition = message.LastIndexOf('(');

openingPosition += 1;
int closingPosition = message.LastIndexOf(')');
int length = closingPosition - openingPosition;
Console.WriteLine(message.Substring(openingPosition, length));
```
3. Сохраните файл кода, а затем используйте Visual Studio для запуска кода. Вы должны увидеть следующий вывод:
```
set of parentheses
```
Ключевым моментом в этом примере является использование LastIndexOf(), который используется для получения позиций последних открывающих и закрывающих скобок.

:::note
Предыдущий пример кода работает без ошибок только потому, что строка сообщения содержит правильно отформатированные пары круглых скобок. Но код хрупок и выдает ошибки, когда в нем нет пары скобок или когда последние скобки не образуют открывающую и закрывающую пару.
:::
### Извлечь все экземпляры подстрок внутри скобок
На этот раз измените сообщение так, чтобы в нем было три набора круглых скобок, и напишите код для извлечения любого текста внутри круглых скобок. Вы можете использовать часть предыдущей работы, но вам нужно добавить оператор while для итерации строки, пока все наборы круглых скобок не будут обнаружены, извлечены и отображены.
1. Обновите свой код в редакторе кода Visual Studio следующим образом:
```cs
string message = "(What if) there are (more than) one (set of parentheses)?";
while (true)
{
    int openingPosition = message.IndexOf('(');
    if (openingPosition == -1) break;

    openingPosition += 1;
    int closingPosition = message.IndexOf(')');
    int length = closingPosition - openingPosition;
    Console.WriteLine(message.Substring(openingPosition, length));

    // Note the overload of the Substring to return only the remaining 
    // unprocessed message:
    message = message.Substring(closingPosition + 1);
}
```
2. Сохраните файл кода, а затем используйте Visual Studio для запуска кода. Вы должны увидеть следующий вывод:
```
What if
more than
set of parentheses
```
3. Уделите минутку, чтобы обратить внимание на последнюю строку кода внутри цикла while, извлеченную из следующего кода:
```cs
message = message.Substring(closingPosition + 1);
```
Когда вы используете Substring() без указания входного параметра длины, она вернет каждый символ после указанной вами начальной позиции. В обрабатываемой строке message = «(Что, если) есть (более) одного (набора скобок)?» есть преимущество в удалении первого набора скобок (What if) из значения message. То, что останется, будет обработано в следующей итерации цикла while.

4. Потратьте минуту на то, что произойдет во время последней итерации цикла while, когда останется только последний символ ?

В следующем коде рассматривается обработка конца строки:

```cs
int openingPosition = message.IndexOf('(');
if (openingPosition == -1) break;
```
Метод IndexOf() возвращает -1, если не может найти входной параметр в строке. Вы просто проверяете значение -1 и выходите из цикла.

### Работа с различными типами наборов символов

На этот раз ищите несколько разных символов, а не просто набор круглых скобок.

Обновите строку сообщения, добавив различные типы символов, например квадратные [] скобки и фигурные скобки {}. Чтобы искать несколько символов одновременно, используйте .IndexOfAny(). Поиск с помощью .IndexOfAny() возвращает индекс первого символа из массива openSymbols, найденного в строке сообщения.

1. Обновите свой код в редакторе Visual Studio следующим образом:
```cs
string message = "Help (find) the {opening symbols}";
Console.WriteLine($"Searching THIS Message: {message}");
char[] openSymbols = { '[', '{', '(' };
int startPosition = 5;
int openingPosition = message.IndexOfAny(openSymbols);
Console.WriteLine($"Found WITHOUT using startPosition: {message.Substring(openingPosition)}");

openingPosition = message.IndexOfAny(openSymbols, startPosition);
Console.WriteLine($"Found WITH using startPosition {startPosition}:  {message.Substring(openingPosition)}");
```
2. Сохраните файл кода, а затем используйте Visual Studio для запуска кода. Вы должны увидеть следующий вывод:
```
Searching THIS message: Help (find) the {opening symbols}
Found WITHOUT using startPosition: (find) the {opening symbols}
Found WITH using startPosition 5:  (find) the {opening symbols}
```
3. Уделите минуту просмотру введенного ранее кода.

Вы использовали .IndexOfAny() без перегрузки начальной позиции, а затем с ней.

Теперь, когда вы нашли открывающий символ, вам нужно найти соответствующий ему закрывающий символ.

4. Обновите свой код в редакторе кода Visual Studio следующим образом:
```cs
string message = "(What if) I have [different symbols] but every {open symbol} needs a [matching closing symbol]?";

// The IndexOfAny() helper method requires a char array of characters. 
// You want to look for:

char[] openSymbols = { '[', '{', '(' };

// You'll use a slightly different technique for iterating through 
// the characters in the string. This time, use the closing 
// position of the previous iteration as the starting index for the 
//next open symbol. So, you need to initialize the closingPosition 
// variable to zero:

int closingPosition = 0;

while (true)
{
    int openingPosition = message.IndexOfAny(openSymbols, closingPosition);

    if (openingPosition == -1) break;

    string currentSymbol = message.Substring(openingPosition, 1);

    // Now  find the matching closing symbol
    char matchingSymbol = ' ';

    switch (currentSymbol)
    {
        case "[":
            matchingSymbol = ']';
            break;
        case "{":
            matchingSymbol = '}';
            break;
        case "(":
            matchingSymbol = ')';
            break;
    }

    // To find the closingPosition, use an overload of the IndexOf method to specify 
    // that the search for the matchingSymbol should start at the openingPosition in the string. 

    openingPosition += 1;
    closingPosition = message.IndexOf(matchingSymbol, openingPosition);

    // Finally, use the techniques you've already learned to display the sub-string:

    int length = closingPosition - openingPosition;
    Console.WriteLine(message.Substring(openingPosition, length));
}
```
5. Уделите несколько минут изучению предыдущего кода и прочтите комментарии, которые помогают объяснить его.

6. Продолжайте изучать код и найдите следующую строку кода, использующую IndexOf() для определения позиции закрытия (closingPosition):
```cs
closingPosition = message.IndexOf(matchingSymbol, openingPosition);
```
Переменная closingPosition используется для определения длины, переданной в метод Substring(), и для поиска следующего значения openingPosition:
```cs
int openingPosition = message.IndexOfAny(openSymbols, closingPosition);
```
По этой причине переменная closingPosition определяется вне области цикла while и инициализируется 0 на первой итерации.

7. Сохраните файл с кодом, а затем запустите его с помощью Visual Studio. Вы должны увидеть следующий результат:
```
What if
different symbols
open symbol
matching closing symbol
```
### Выводы
Вот два важных момента, которые следует запомнить:

- LastIndexOf() возвращает последнюю позицию символа или строки внутри другой строки.
- IndexOfAny() возвращает первую позицию массива символов, которая встречается внутри другой строки.

## Используйте методы Remove() и Replace().

В этом упражнении вы удалите символы из строки с помощью метода Remove() и замените их с помощью метода Replace(). 

Иногда вам нужно изменить содержимое строки, удалив или заменив символы. Хотя вы можете заменить символы с помощью уже известных вам инструментов, это требует некоторого временного хранения и сшивания строк обратно. К счастью, у типа данных string есть другие встроенные методы, Remove() и Replace(), для таких специализированных сценариев.

### Используйте метод Remove()
Обычно функцию Remove() используют, когда существует стандартное и последовательное расположение символов, которые нужно удалить из строки.

В этом упражнении данные хранятся в старых файлах, имеющих фиксированную длину, и с позициями символов, выделенными для определенных полей информации. Первые пять цифр представляют собой идентификационный номер клиента. Следующие 20 цифр содержат имя клиента. Следующие шесть позиций представляют собой сумму последнего счета клиента, а последние три позиции - количество товаров, заказанных по этому счету.

В следующих шагах вам нужно удалить имя заказчика, чтобы отформатировать данные для отправки в отдельный процесс. Поскольку вы знаете точную позицию и длину имени пользователя, вы можете легко удалить его с помощью метода Remove().

#### Удалите из строки символы в определенных местах

1. Удалите или используйте оператор комментария строки //, чтобы закомментировать весь код из предыдущих упражнений. 
2. Обновите код в редакторе кода Visual Studio следующим образом:
```cs
string data = "12345John Smith          5000  3  ";
string updatedData = data.Remove(5, 20);
Console.WriteLine(updatedData);
```
3. Вы должны увидеть следующий результат:
```
123455000  3
```
Метод Remove() работает аналогично методу Substring(). Вы указываете начальную позицию и длину, чтобы удалить эти символы из строки.

### Используйте метод Replace()

Метод Replace() используется, когда вам нужно заменить один или несколько символов на другой символ (или без символа). Метод Replace() отличается от других методов, использованных до сих пор: он заменяет каждый экземпляр заданных символов, а не только первый или последний.

#### Удаляйте символы независимо от того, где они встречаются в строке

1. Обновите код в редакторе кода Visual Studio следующим образом:
```cs
string message = "This--is--ex-amp-le--da-ta";
message = message.Replace("--", " ");
message = message.Replace("-", "");
Console.WriteLine(message);
```
2. Сохраните файл кода, а затем запустите его с помощью Visual Studio. Вы должны увидеть следующий результат:
```
This is example data
```
Здесь вы дважды использовали метод Replace(). В первый раз вы заменили строку -- на пробел. Во второй раз вы заменили строку -- пустой строкой, которая полностью удаляет символ из строки.

### Выводы
Запомните две важные вещи: 
- Метод Remove() работает так же, как метод Substring(), за исключением того, что он удаляет указанные символы в строке. 
- Метод Replace() меняет все экземпляры строки на новую строку.

## Общее задание. Выполните задание по извлечению, замене и удалению данных из входной строки.

В этой задаче вы работаете со строкой, содержащей фрагмент HTML. Вы извлекаете данные из фрагмента HTML, заменяете часть его содержимого и удаляете другие части содержимого, чтобы получить желаемый результат.

### Извлечение, замена и удаление данных из входной строки
1. Выделите и удалите все строки кода в редакторе кода Visual Studio. 
2. В Visual Studio Code добавьте следующий "стартовый" код, чтобы получить данные для задачи:
```cs
const string input = "<div><h2>Widgets &trade;</h2><span>5000</span></div>";

string quantity = "";
string output = "";

// Your work here

Console.WriteLine(quantity);
Console.WriteLine(output);
```
При выполнении кода на выходе отображаются пустые строки, начальные значения quantity и output - пустые строковые значения.

3. Уделите минуту просмотру начальной строки кода, содержащей строку HTML.
```cs
const string input = "<div><h2>Widgets &trade;</h2><span>5000</span></div>";
```
Обратите внимание на теги:\<div\>, \<h2\>, \<span\> и символьный код \&trade;, содержащийся во входной переменной.

4. Изучите желаемый выход для окончательного вывода программы:
```
Quantity: 5000
Output: <h2>Widgets &reg;</h2><span>5000</span>
```
5. Начните добавлять свой код решения к стартовому коду под комментарием // Your work here
6. Установите переменную quantity в значение, полученное при извлечении текста между тегами \<span\> и \</span\>.
7. Установите переменную output в значение input, затем удалите теги \<div\> и \</div\>.
8. Замените в выходной переменной HTML-символ ™ (\&trade;) на ® (\&reg;).
9. Запустите решение и убедитесь, что полученный результат соответствует ожидаемому.
```
Quantity: 5000
Output: <h2>Widgets &reg;</h2><span>5000</span>
```

## Заключение

Ваша цель - извлечь, удалить и заменить значения в строках. Часто в полученных данных присутствуют посторонние данные или символы, которые необходимо избежать или удалить, прежде чем использовать целевые данные.

Использование метода IndexOf() позволяет определить позицию символа или строки в другой строке. Позиция, возвращаемая методом IndexOf(), является первым строительным блоком для использования метода Substring() для извлечения части строки с учетом начальной позиции и количества символов для извлечения (длины). Он также позволил вам использовать метод Remove() для удаления символов из строки с учетом начальной позиции и длины. Вы узнали о таких вариантах, как метод LastIndexOf() для поиска последней позиции символа строки внутри другой строки и IndexOfAny() для поиска позиции любого значения заданного массива символов. Вы использовали оператор while для итерации по длинной строке, чтобы найти и извлечь все экземпляры символа или строки в большей исходной строке. Наконец, вы использовали метод Replace(), чтобы поменять местами все экземпляры символа или строки в большей строке.

Хотя можно было бы выполнить эти операции с помощью массива символов, итерируя каждый символ для поиска совпадений, отслеживая начальную и конечную точки, которые нужно найти, и так далее. Чтобы выполнить то, что могут сделать эти методы-помощники для работы со строками, потребуется гораздо больше шагов за один вызов.



