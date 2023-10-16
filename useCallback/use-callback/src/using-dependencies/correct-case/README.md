# CorrectCase

Компонент `CorrectCase` - это пример элементарного React компонента, который использует хуки `useState` и `useCallback`. Компонент отображает кнопку, которая увеличивает внутренний счетчик количество раз, которое она была нажата.

## Важные элементы кода:

### Импорт

```javascript
import './CorrectCase.css';
import {useCallback, useState} from 'react';
```
Здесь мы импортируем `useCallback` и `useState` хуки из React и добавляем файл стилей CorrectCase.css.


### useState
```javascript
const [count, setCount] = useState(0);
```
`useState` - это React хук, который мы используем для создания состояния счетчика `count`. `setCount` - это функция, которую мы будем использовать для обновления значения `count`.

### useCallback
```javascript
const increment = useCallback(() => {
        setCount(count + 1);
    }, [count]);
```
`useCallback` является хуком React, который возвращает мемоизированную версию колбэка, который изменяется только если изменяются зависимости. В данном случае зависимостью является `count`, это значит, что новая функция `increment` будет создана только когда `count` изменится.

### JSX
```javascript
return (
    <div className="wrapper">
        <button className="increment-button" onClick={increment}>
            Увеличить: {count}
        </button>
    </div>
);
```
Компонент возвращает JSX разметку. Это кнопка, при клике на которую вызывается функция `increment`. Мы также отображаем текущее значение счетчика `count` на кнопке.

## Нюансы работы компонента:

Обратите внимание на зависимость в `useCallback`:

```javascript
}, [count]);
```
Это означает, что каждый раз когда `count` изменяется, создается новая версия функции `increment`. Это означает, что каждый раз, когда мы нажимаем кнопку и увеличиваем `count`, мы фактически создаем новую функцию.

Подобное поведение может быть избегнуто, если вместо текущего значения `count` использовать функцию обновления `setCount`. Когда `setCount` вызывается с функцией вместо значения, React передает текущее состояние в эту функцию. Это означает, что следующий код будет работать корректно и не будет создавать новую функцию при каждом рендере:

```javascript
const increment = useCallback(() => {
    setCount(c => c + 1);
}, []);
```