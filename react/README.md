# Правила оформления кода на React

React является JavaScript-библиотекой, поэтому помимо нижеизложенных, следует также придерживаться [правил оформления JavaScript кода](js/js.md).

1. [Создание компонента без внутреннего состояния и ссылок](#1-Создание-компонента-без-внутреннего-состояния-и-ссылок)
2. [Именование](#2-Именование)  
   2.1. [Расширения](#21-Расширения)  
   2.2. [Имя файла](#22-Имя-файла)  
   2.3. [Именование переменной](#23-Именование-переменной)  
   2.4. [Именование компонента](#24-Именование-компонента)  
   2.5. [Именование компонента высшего порядка](#25-Именование-компонента-высшего-порядка)  
   2.6. [Названия свойств](#26-Названия-свойств)  
3. [Выравнивание](#3-Выравнивание)
4. [Кавычки](#4-Кавычки)
5. [Пробелы](#5-Пробелы)
6. [Свойства (`Props`)](#6-Свойства-props)  
   6.1. [Названия свойств](#61-Названия-свойств)  
   6.2. [Значения свойств](#62-Значения-свойств)  
   6.3. [Свойство `key`](#63-Свойство-key)  
   6.4. [`defaultProps`](#64-defaultprops)  
7. [Круглые скобки](#7-Круглые-скобки)  
8. [Теги](#8-Теги)
9. [Методы](#9-Методы)  
   9.1. [Замыкание локальных переменных](#91-Замыкание-локальных-переменных)  
   9.2. [Привязка обработчиков событий](#92-Привязка-обработчиков-событий)  
   9.3. [Возврат значений в `render`](#93-Возврат-значений-в-render)  
10. [Последовательность](#10-Последовательность)  
    10.1. [Последовательность вызова методов внутри компонента](#101-Последовательность-вызова-методов-внутри-компонента)  
    10.2. [Как определять `propTypes`, `defaultProps`, `contextTypes`, и т.д.](#102-Как-определять-proptypes-defaultprops-contexttypes-и-тд)  
    10.3. [`isMounted`](#103-ismounted)  

## 1. Создание компонента без внутреннего состояния и ссылок
Если у компонента нет состояния (`state`) или ссылок (`refs`), используйте функции, а не классы.

**Хорошо**
```javascript
function Listing({ hello }) {
  return <div>{hello}</div>;
}
```

**Хорошо**
```javascript
const Listing = ({ hello }) => (
  <div>{hello}</div>
);
```

**Плохо**
```javascript
class Listing extends React.Component {
  render() {
    return <div>{this.props.hello}</div>;
  }
}
```

## 2. Именование

### 2.1 Расширения
Используйте расширение .js для компонентов React.

### 2.2 Имя файла
Используйте PascalCase для названий файлов, например, ReservationCard.js.

### 2.3 Именование переменной
Используйте PascalCase для компонентов React.

**Хорошо**
```javascript
import ReservationCard from './ReservationCard';
```

**Плохо**
```javascript
import reservationCard from './ReservationCard';
```

Используйте camelCase для экземпляров компонентов React.

**Хорошо**
```javascript
const reservationItem = <ReservationCard />;
```

**Плохо**
```javascript
const ReservationItem = <ReservationCard />;
```

### 2.4 Именование компонента
Называйте файлы так же как и компоненты. Например, ReservationCard.js должен содержать внутри компонент ReservationCard. Однако корневые компоненты в директории должны лежать в файле index.js, и в этом случае название папки должно быть таким же, как название компонента.

**Хорошо**
```javascript
import Footer from './Footer';
```

**Плохо**
```javascript
import Footer from './Footer/Footer';
```

**Плохо**
```javascript
import Footer from './Footer/index';
```

### 2.5 Именование компонента высшего порядка
Используйте сочетание имени компонента высшего порядка и имени переданного в него компонента как свойство `displayName` сгенерированного компонента. Например, из компонента высшего порядка `withFoo()`, которому передан компонент Bar, должен получаться компонент с `displayName` равным `withFoo(Bar)`.

Почему? Свойство `displayName` может использоваться в инструментах разработчика или сообщениях об ошибках, и если оно ясно выражает связь между компонентами, это помогает понять, что происходит.

**Хорошо**
```javascript
export default function withFoo(WrappedComponent) {
  function WithFoo(props) {
    return <WrappedComponent {...props} foo />;
  }

  const wrappedComponentName = WrappedComponent.displayName
    || WrappedComponent.name
    || 'Component';

  WithFoo.displayName = `withFoo(${wrappedComponentName})`;
  return WithFoo;
}
```

**Плохо**
```javascript
export default function withFoo(WrappedComponent) {
  return function WithFoo(props) {
    return <WrappedComponent {...props} foo />;
  }
}
```

### 2.6 Названия свойств
Избегайте использования названий свойств DOM-компонента для других целей.

Почему? Люди ожидают, что такие свойства как `style` и `className` имеют одно определенное значение. Изменение этого API в вашем приложении ухудшает читабельность и поддержку кода, что может приводить к ошибкам.

**Хорошо**
```javascript
<MyComponent variant="fancy" />
```

**Плохо**
```javascript
<MyComponent style="fancy" />
```

## 3. Выравнивание
Следуйте приведенным ниже стилям для JSX-синтаксиса.

**Хорошо**
```javascript
<Foo
  superLongParam="bar"
  anotherSuperLongParam="baz"
/>
```

**Плохо**
```javascript
<Foo superLongParam="bar"
     anotherSuperLongParam="baz" />
```

Если свойства помещаются на одну строку, оставляйте их на одной строке.

```javascript
<Foo bar="bar" />
```
Отступ у дочерних элементов задается как обычно.

```javascript
<Foo
  superLongParam="bar"
  anotherSuperLongParam="baz"
>
  <Quux />
</Foo>
```

## 4. Кавычки
Всегда используйте двойные кавычки: (`"`) для JSX-атрибутов.

**Хорошо**
```javascript
<Foo bar="bar" userName="hello" />
```

**Плохо**
```javascript
<Foo bar='bar' userName='hello' />
```

**Плохо**
```javascript
<Foo bar='bar' userName="hello" />
```

## 5. Пробелы
Не отделяйте фигурные скобки пробелами в JSX.

**Хорошо**
```javascript
<Foo bar={baz} />
```

**Плохо**
```javascript
<Foo bar={ baz } />
```

## 6. Свойства (`Props`)

### 6.1 Названия свойств
Всегда используйте camelCase для названий свойств.

**Хорошо**
```javascript
<Foo
  userName="hello"
  phoneNumber={12345678}
/>
```

**Плохо**
```javascript
<Foo
  UserName="hello"
  phone_number={12345678}
/>
```

### 6.2 Значения свойств
Не указывайте значение свойства, когда оно явно `true`.

**Хорошо**
```javascript
<Foo
  hidden
/>
```

**Плохо**
```javascript
<Foo
  hidden={true}
/>
```

### 6.3 Свойство `key`
Не используйте индексы элементов массива в качестве свойства `key`. Отдавайте предпочтение уникальному `ID`.

**Хорошо**
```javascript
{todos.map(todo => (
  <Todo
    {...todo}
    key={todo.id}
  />
))}
```

**Плохо**
```javascript
{todos.map((todo, index) =>
  <Todo
    {...todo}
    key={index}
  />
)}
```

### 6.4 `defaultProps`
Всегда указывайте явные `defaultProps` для всех свойств, которые не указаны как необходимые.

Почему? `propTypes` является способом документации, а предоставление `defaultProps` позволяет читателю вашего кода избежать множества неясностей. Кроме того, это может означать, что ваш код может пропустить определенные проверки типов.

**Хорошо**
```javascript
function SFC({ foo, bar, children }) {
  return <div>{foo}{bar}{children}</div>;
}
SFC.propTypes = {
  foo: PropTypes.number.isRequired,
  bar: PropTypes.string,
  children: PropTypes.node,
};
SFC.defaultProps = {
  bar: '',
  children: null,
};
```

**Плохо**
```javascript
function SFC({ foo, bar, children }) {
  return <div>{foo}{bar}{children}</div>;
}
SFC.propTypes = {
  foo: PropTypes.number.isRequired,
  bar: PropTypes.string,
  children: PropTypes.node,
};
```

## 7. Круглые скобки
Оборачивайте в скобки JSX теги, когда они занимают больше одной строки.

**Хорошо**
```javascript
render() {
  return (
    <MyComponent className="long body" foo="bar">
      <MyChild />
    </MyComponent>
  );
}
```

**Хорошо**, когда одна строка
```javascript
render() {
  const body = <div>hello</div>;
  return <MyComponent>{body}</MyComponent>;
}
```

**Плохо**
```javascript
render() {
  return <MyComponent className="long body" foo="bar">
           <MyChild />
         </MyComponent>;
}
```

## 8. Теги
Всегда используйте самозакрывающиеся теги, если у элемента нет дочерних элементов.

**Хорошо**
```javascript
<Foo className="stuff" />
```

**Плохо**
```javascript
<Foo className="stuff"></Foo>
```

Если ваш компонент имеет множество свойств, которые располагаются на нескольких строчках, то закрывайте тег на новой строке.

**Хорошо**
```javascript
<Foo
  bar="bar"
  baz="baz"
/>
```

**Плохо**
```javascript
<Foo
  bar="bar"
  baz="baz" />
```

## 9. Методы

### 9.1 Замыкание локальных переменных
Используйте стрелочные функции для замыкания локальных переменных.

**Хорошо**
```javascript
function ItemList(props) {
  return (
    <ul>
      {props.items.map((item, index) => (
        <Item
          key={item.key}
          onClick={() => doSomethingWith(item.name, index)}
        />
      ))}
    </ul>
  );
}
```

### 9.2 Привязка обработчиков событий
Привязывайте обработчики событий для метода `render` в конструкторе.

Почему? Вызов `bind` в методе `render` создает новую функцию при каждой перерисовке.

**Хорошо**
```javascript
class extends React.Component {
  constructor(props) {
    super(props);

    this.onClickDiv = this.onClickDiv.bind(this);
  }

  onClickDiv() {
    // ...
  }

  render() {
    return <div onClick={this.onClickDiv} />;
  }
}
```

**Плохо**
```javascript
class extends React.Component {
  onClickDiv() {
    // ...
  }

  render() {
    return <div onClick={this.onClickDiv.bind(this)} />;
  }
}
```

### 9.3 Возврат значений в `render`
Всегда возвращайте значение в методах `render`.

**Хорошо**
```javascript
render() {
  return (<div />);
}
```

**Плохо**
```javascript
render() {
  (<div />);
}
```

## 10. Последовательность

### 10.1 Последовательность вызова методов внутри компонента
Последовательность для `class extends React.Component`:

1. произвольные `static` методы;
2. `constructor`;
3. `getChildContext`;
4. `componentWillMount`;
5. `componentDidMount`;
6. `componentWillReceiveProps`;
7. `shouldComponentUpdate`;
8. `componentWillUpdate`;
9. `componentDidUpdate`;
10. `componentWillUnmount`;
11. обработчики кликов или событий, такие как `onClickSubmit()` или `onChangeDescription()`;
12. `getter` методы для `render`, такие как `getSelectReason()` или `getFooterContent()`;
13. произвольные `render` методы, такие как `renderNavigation()` или `renderProfilePicture()`;
14. `render`.

### 10.2 Как определять `propTypes`, `defaultProps`, `contextTypes`, и т.д.

```javascript
import React from 'react';
import Proptypes from 'prop-types';

const propTypes = {
  id: PropTypes.number.isRequired,
  url: PropTypes.string.isRequired,
  text: PropTypes.string,
};

const defaultProps = {
  text: 'Hello World',
};

class Link extends React.Component {
  static methodsAreOk() {
    return true;
  }

  render() {
    return <a href={this.props.url} data-id={this.props.id}>{this.props.text}</a>;
  }
}

Link.propTypes = propTypes;
Link.defaultProps = defaultProps;

export default Link;
```

### 10.3 `isMounted`
Не используйте `isMounted`.

Почему? `isMounted` — это антипаттерн, который недоступен при использовании ES6 классов и который планируют официально признать устаревшим.