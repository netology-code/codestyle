# Правила оформления Swift кода

## Оглавление

- [Правила оформления Swift кода](#правила-оформления-swift-кода)
  - [Оглавление](#оглавление)
- [Важно](#важно)
  - [1. Форматирование кода](#1-форматирование-кода)
  - [2. Именование](#2-именование)
  - [3. Стиль кода](#3-стиль-кода)

# Важно
Изучите правила кода, они помогут вам во время написания кода. Используйте их при работе над каждым домашним заданием на обучении. Это поможет избежать типовых ошибок, а также ускорит проверку вашей работы для преподавателя.

## 1. Форматирование кода

**1.1** Не забывайте про вложенность кода. Используйте 4 пробела для табуляции. Можете воспользоваться автоформатированием: выделить весь код (Command + a), применить автоформатирование (Control + i)
```swift
// ХОРОШО
struct SomeStruct {
    var firsrNumber: Int
    var secondNumber: Int
    if firsrNumber == firsrNumber {
        print("Equal!")
    }
}

// ПЛОХО
struct SomeStruct {
var firsrNumber: Int
var secondNumber: Int
if firsrNumber == firsrNumber {
print("Equal!")
}
}
```

**1.2** Не допускайте использования строк длинной более 160 символов (Xcode->Preferences->Text Editing->Page guide at column: 160 - включение этого пункта поможет наглядно видеть, если строка будет больше)

**1.3** Убедитесь, что в конце каждого файла есть новая строка. 

**1.4** Убедитесь, что нигде нет конечных пробелов (Xcode->Preferences->Text Editing->Automatically trim trailing whitespace + Including whitespace-only lines).

**1.5** Не ставьте открывающиеся скобки на новую строку [1TBS style](https://en.m.wikipedia.org/wiki/Indentation_style#1TBS).

```swift
// ХОРОШО
class SomeClass {
    func someMethod() {
        if x == y {
            /* ... */
        } else if x == z {
            /* ... */
        } else {
            /* ... */
        }
    }

    /* ... */
}

// ПЛОХО
class SomeClass 
{
    func someMethod() 
    {
        if x == y 
        {
            /* ... */
        } else if x == z 
        {
            /* ... */
        } else 
        {
            /* ... */
        }
    }

    /* ... */
}
```

**1.6** При написании типов констант, переменных, ключей для словарей, аргументов функций, подписывания под протоколы или суперклассы не ставьте пробелы перед двоеточием, при этом после двоеточия пробел должен быть.

```swift
// ХОРОШО
let pirateViewController: PirateViewController

// dictionary syntax (note that we left-align as opposed to aligning colons)
let ninjaDictionary: [String: AnyObject] = [
    "fightLikeDairyFarmer": false,
    "disgusting": true
]

// объявление функции
func myFunction<T, U: SomeProtocol>(firstArgument: U, secondArgument: T) where T.RelatedType == U {
    /* ... */
}

// вызов функции
someFunction(someArgument: "Kitten")

// суперклассы
class PirateViewController: UIViewController {
    /* ... */
}

// протоколы
extension PirateViewController: UITableViewDataSource {
    /* ... */
}

// ПЛОХО
let pirateViewController:PirateViewController
let pirateViewController : PirateViewController
let pirateViewController :PirateViewController
```

**1.7** Как правило, после запятой должен стоять пробел. 

```swift
// ХОРОШО
let myArray = [1, 2, 3, 4, 5]

// ПЛОХО
let myArray = [1,2,3,4,5]
```

**1.8** До и после бинарного оператора должны стоять пробелы `+`, `==`, or `->`. При этом не должно быть пробелов после `(` и перед `)`.

```swift
// ХОРОШО
let myValue = 20 + (30 / 2) * 3
if 1 + 1 == 3 {
    fatalError("The universe is broken.")
}
func pancake(with syrup: Syrup) -> Pancake {
    /* ... */
}

// ПЛОХО
let myValue=20+(30/2)*3
```

**1.9** Мы должны следовать рекомендуемому стилю Xcode, то есть ваш код не должен менять при нажатии Ctrl+I. При объявлении функции, охватывающей несколько строк, предпочтительнее использовать синтаксис Xcode по умолчанию. 

```swift
// Отступ Xcode при объявлении функции, которая занимает несколько строк. 
func myFunctionWithManyParameters(
        parameterOne: String,
        parameterTwo: String,
        parameterThree: String
) {
    // Отступы для такой инструкции
    print("\(parameterOne) \(parameterTwo) \(parameterThree)")
}

// Отступы для многострочного `if`
if myFirstValue > (mySecondValue + myThirdValue)
    && myFourthValue == .someEnumValue {

    // Отступы для такой инструкции
    print("Hello, World!")
}
```

**1.10** При вызове функции с множеством аргументов помещайте каждый из них в отдельную строку с одним дополнительным отступом. 

```swift
someFunctionWithManyArguments(
    firstArgument: "Hello, I am a string",
    secondArgument: resultFromSomeFunction(),
    thirdArgument: someOtherLocalProperty
)
```

**1.11** При работе с неявным массивом или словарем, достаточно большим, чтобы можно было разбить его на несколько строк, обрабатывайте `[` и `]` как если бы они были фигурными скобками в методе, операторе `if` и т.д. Замыкания в методе должны обрабатываться схожим образом.

```swift
//ХОРОШО
someFunctionWithABunchOfArguments(
    someStringArgument: "hello I am a string",
    someArrayArgument: [
        "dadada daaaa daaaa dadada daaaa daaaa dadada daaaa daaaa",
        "string one is crazy - what is it thinking?"
    ],
    someDictionaryArgument: [
        "dictionary key 1": "some value 1, but also some more text here",
        "dictionary key 2": "some value 2"
    ],
    someClosure: { parameter1 in
        print(parameter1)
    }
)

// ПЛОХО
someArrayArgument: 
[
    "dadada daaaa daaaa dadada daaaa daaaa dadada daaaa daaaa",
    "string one is crazy - what is it thinking?"
]

someClosure: 
{ parameter1 in
    print(parameter1)
}
```

## 2. Именование

**2.1** Используйте `PascalCase` для названий типов (например `struct`, `enum`, `class`, `typedef`, `associatedtype`, и т.д.).

**2.2** Используйте `camelCase` (начальная буква строчная) для функций, методов, свойств, констант, переменных, имен аргументов, значений enum и т.д.

**2.3** Сталкиваясь с аббревиатурой или другим именем, которое обычно пишется заглавными буквами, используйте заглавные буквы также. Исключение составляют имена, в которых такое слово стоит в начале - здесь имя должно быть написано строчными буквами. 

```swift
// "HTML" присутствует в начале константы, значит мы будем писать строчные буквы "html"
let htmlBodyContent: String = "<p>Hello, World!</p>"
// В данном примере лучше использовать ID вместо Id
let profileID: Int = 1
// Лучше писать URLFinder чем UrlFinder
class URLFinder {
    /* ... */
}
```

**2.5** Все константы, не зависящие от экземпляра должны быть `static`. Все такие `static` константы должны быть помещены в определенный раздел их `class`, `struct` или` enum`. Для классов с большим количеством констант вы должны группировать константы с похожими или одинаковыми префиксами, суффиксами и/или вариантами использования.

```swift
// ПРЕДПОЧТИТЕЛЬНО    
class MyClassName {
    // MARK: - Constants
    static let buttonPadding: CGFloat = 20.0
    static let indianaPi = 3
    static let shared = MyClassName()
}

// НЕ ЖЕЛАТЕЛЬНО
class MyClassName {
    // Не используй `k`-prefix
    static let kButtonPadding: CGFloat = 20.0

    // Не используй имя констант
    enum Constant {
        static let indianaPi = 3
    }
}
```

**2.6** Имена должны быть говорящими и недвусмысленными.

```swift
// ПРЕДПОЧТИТЕЛЬНО
class RoundAnimatingButton: UIButton { /* ... */ }

// НЕ ЖЕЛАТЕЛЬНО
class CustomButton: UIButton { /* ... */ }
```

**2.8** Не используйте аббревиатуры, сокращенные и однобуквенные имена.

```swift
// ПРЕДПОЧТИТЕЛЬНО
class RoundAnimatingButton: UIButton {
    let animationDuration: NSTimeInterval

    func startAnimating() {
        let firstSubview = subviews.first
    }

}

// НЕ ЖЕЛАТЕЛЬНО
class RoundAnimating: UIButton {
    let aniDur: NSTimeInterval

    func srtAnmating() {
        let v = subviews.first
    }
}
```

**2.9** Включайте в имена информацию о типе данных, если он не очевиден.

```swift
// ПРЕДПОЧТИТЕЛЬНО
class ConnectionTableViewCell: UITableViewCell {
    let personImageView: UIImageView

    let animationDuration: TimeInterval

    // возможно использовать `Controller` вместо` ViewController` 
    let popupController: UIViewController
    let popupViewController: UIViewController

    // при работе с подклассом `UIViewController` таким как table view
    // controller, collection view controller, split view controller, и т.д.,
    // полностью укажите тип в имени.
    let popupTableViewController: UITableViewController

    // при работе с аутлетами будьте уверены, что их типы указаны в названии свойств. 
    @IBOutlet weak var submitButton: UIButton!
    @IBOutlet weak var emailTextField: UITextField!
    @IBOutlet weak var nameLabel: UILabel!

}

// НЕ ЖЕЛАТЕЛЬНО
class ConnectionTableViewCell: UITableViewCell {
    // это не `UIImage`, поэтому нужно
    // использовать personImageView вместо этого
    let personImage: UIImageView

    // это не `String`, поэтому нужно использовать`textLabel`
    let text: UILabel

    // `animation` не является временным интервалом
    // используйте `animationDuration` или `animationTimeInterval` вместо этого
    let animation: TimeInterval

    // не очевидно, что это `String`
    // используйте `transitionText` или `transitionString` вместо этого
    let transition: String

    // это view controller, а не view
    let popupView: UIViewController

    // как упоминалось ранее, мы не должны использовать сокращения
    // поэтому не нужно использовать`VC` вместо `ViewController`
    let popupVC: UIViewController

    // хотя технически это все еще `UIViewController`, это свойство
    // это свойство должно указывать, что мы работаем с *Table* View Controller
    let popupViewController: UITableViewController

    // для единообразия мы должны помещать 
    // имя типа в конец, но не в начало
    @IBOutlet weak var btnSubmit: UIButton!
    @IBOutlet weak var buttonSubmit: UIButton!

    // при работе с аутлетами у нас всегда должен быть тип в имени
    // для примера, тут мы должны использовать`firstNameLabel` вместо этого
    @IBOutlet weak var firstName: UILabel!
}
```

**2.10** При именовании аргументов функции убедитесь, что функция легко читается, что было понятно назначение каждого аргумента.

**2.11** Согласно [Apple's API Design Guidelines](https://swift.org/documentation/api-design-guidelines/), `protocol` должны именоваться существительными (например `Collection`) и используя суффиксы `able`, `ible`, или `ing` если он описывает возможность (например `Equatable`, `ProgressReporting`). Если не один из этих вариантов не подоходит, то можете использовать суффикс `Protocol` к имени протокола. Несколько примеров ниже: 

```swift
// здесь существительное, описываюшее, что делает протокол
protocol TableViewSectionProvider {
    func rowHeight(at row: Int) -> CGFloat
    var numberOfRows: Int { get }
    /* ... */
}

// здесь протокол - это возможность, описываем соответствующим образом
protocol Loggable {
    func logCurrentState()
    /* ... */
}

// предположим, что у нас есть класс `InputTextView`, но также мы хотим, 
// чтобы протокол обобщал некоторые функции - поэтому тут уместно 
// использовать суффикс `Protocol`
protocol InputTextViewProtocol {
    func sendTrackingEvent()
    func inputText() -> String
    /* ... */
}
```

## 3. Стиль кода

**3.1.1** Используйте `let` вместо `var` везде где эт возможно.

**3.1.2** При трансформации одной коллекции в другую предпочтительно использовать `map`, `filter`, `reduce`, и т.д. 

```swift
// ПРЕДПОЧТИТЕЛЬНО
let stringOfInts = [1, 2, 3].flatMap { String($0) }
// ["1", "2", "3"]

// НЕ ЖЕЛАТЕЛЬНО
var stringOfInts: [String] = []
for integer in [1, 2, 3] {
    stringOfInts.append(String(integer))
}

// ПРЕДПОЧТИТЕЛЬНО
let evenNumbers = [4, 8, 15, 16, 23, 42].filter { $0 % 2 == 0 }
// [4, 8, 16, 42]

// НЕ ЖЕЛАТЕЛЬНО
var evenNumbers: [Int] = []
for integer in [4, 8, 15, 16, 23, 42] {
    if integer % 2 == 0 {
        evenNumbers.append(integer)
    }
}
```

* **3.1.3** Можно не объявлять типы для констант и переменных если вы инициализируете их значениями. 
```swift
// ПРЕДПОЧТИТЕЛЬНО
let number = 3

// НЕ ЖЕЛАТЕЛЬНО
let number: Int = 3
```

**3.1.4** Если функция возвращает несколько значений, предпочтительнее возвращать кортеж вместо использования аргументов `inout`. Если вы используете определенный кортеж более одного раза, подумайте об использовании `typealias`. Если вы возвращаете 3 или более элементов в кортеже, рассмотрите возможность использования вместо них `struct` или `class`.

```swift
func pirateName() -> (firstName: String, lastName: String) {
    return ("Guybrush", "Threepwood")
}

let name = pirateName()
let firstName = name.firstName
let lastName = name.lastName
```

**3.1.5** Будьте осторожны с циклами сильных ссылок при создании delegates/protocols для ваших классов classes; как правило их нужно объявлять `weak`.

**3.1.6** Будьте осторожны при вызове `self` напрямую из escaping closure, так как это может вызвать цикл сильных ссылок - используйте [capture list](https://developer.apple.com/library/ios/documentation/swift/conceptual/Swift_Programming_Language/Closures.html#//apple_ref/doc/uid/TP40014097-CH11-XID_163):

```swift
myFunctionWithEscapingClosure() { [weak self] (error) -> Void in
    // вы можете сделать это

    self?.doSomething()

    // или вы можете сделать это

    guard let self = self else {
        return
    }

    self.doSomething()
}
```

**3.1.7** Не заключайте в скобки сравнения.

```swift
// ПРЕДПОЧТИТЕЛЬНО
if x == y {
    /* ... */
}

// НЕ ЖЕЛАТЕЛЬНО
if (x == y) {
    /* ... */
}
```

**3.1.8** По возможности используйте значение `enum` вместо указания полной строки.

```swift
// ПРЕДПОЧТИТЕЛЬНО
imageView.setImageWithURL(url, type: .person)

// НЕ ЖЕЛАТЕЛЬНО
imageView.setImageWithURL(url, type: AsyncImageView.Type.person)
```

**3.1.9** Используйте сокращения для методов классов.

```swift
// ПРЕДПОЧТИТЕЛЬНО

imageView.backgroundColor = .white

// НЕ ЖЕЛАТЕЛЬНО
imageView.backgroundColor = UIColor.white
```

**3.1.10** Предпочтительно не использовать `self.`, кроме случаев где это необходимо.

**3.1.11** При написании методов подумайте, предназначен ли метод для переопределения или нет. Если нет, пометьте его как final, но имейте в виду, что это предотвратит перезапись метода в целях тестирования. Методы final приводят к сокращению времени компиляции, поэтому рекомендуется использовать их, когда это применимо.

**3.1.12** Если у вас есть функция, которая не принимает аргументов, не имеет побочных эффектов и возвращает какой-либо объект или значение, лучше вместо этого использовать вычисляемое свойство.
