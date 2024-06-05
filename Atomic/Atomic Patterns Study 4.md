Date:**2024-06-03

**Abstract/Summary:** 
## Файловая структура в Atomic Design

- **Пример файловой структуры**
    - atoms/
    - molecules/
    - organisms/
    - templates/
    - pages/
- **Организация компонентов**
    - Как правильно организовать файлы и папки
    - Примеры хорошей практики

**Key Words:** [[Atomic Patterns Study]]
## Файловая структура в Atomic Design

### Пример файловой структуры

Atomic Design предполагает организацию файловой структуры по типам компонентов, что делает её интуитивно понятной и удобной для поддержки. Вот пример файловой структуры для проекта, использующего Atomic Design:

```CSS
src/
├── components/
│   ├── atoms/
│   │   ├── Button/
│   │   │   ├── Button.js
│   │   │   └── Button.css
│   │   ├── Input/
│   │   │   ├── Input.js
│   │   │   └── Input.css
│   │   └── Label/
│   │       ├── Label.js
│   │       └── Label.css
│   ├── molecules/
│   │   ├── FormField/
│   │   │   ├── FormField.js
│   │   │   └── FormField.css
│   │   └── ProductCard/
│   │       ├── ProductCard.js
│   │       └── ProductCard.css
│   ├── organisms/
│   │   ├── Header/
│   │   │   ├── Header.js
│   │   │   └── Header.css
│   │   ├── LoginForm/
│   │   │   ├── LoginForm.js
│   │   │   └── LoginForm.css
│   │   └── ProductSection/
│   │       ├── ProductSection.js
│   │       └── ProductSection.css
│   ├── templates/
│   │   ├── ProductPage/
│   │   │   ├── ProductPage.js
│   │   │   └── ProductPage.css
│   │   └── ProfilePage/
│   │       ├── ProfilePage.js
│   │       └── ProfilePage.css
│   └── pages/
│       ├── HomePage.js
│       ├── ProductPage.js
│       └── ProfilePage.js
└── index.js

```

### Организация компонентов

#### Как правильно организовать файлы и папки

1. **Ясные и логичные имена**: Каждый компонент должен находиться в папке, соответствующей его типу (атом, молекула, организм, шаблон или страница). Папки и файлы должны быть названы ясно и логично, чтобы легко понимать их назначение.
    
2. **Единая структура файлов**: Каждый компонент должен содержать все необходимые файлы (например, JavaScript для логики и CSS для стилей) в одной папке. Это помогает держать все, что связано с компонентом, в одном месте, упрощая поддержку и обновления.
    
3. **Разделение стилей и логики**: Хотя все файлы компонента находятся в одной папке, рекомендуется разделять логику (JavaScript/TypeScript) и стили (CSS/SCSS) для облегчения чтения и понимания кода.
    

#### Примеры хорошей практики

1. **Использование index.js**: В папке компонента можно создать файл `index.js`, который будет экспортировать основной компонент. Это упрощает импорт компонентов в других частях приложения.

```jsx
// atoms/Button/index.js 
import Button from './Button'; 
export default Button;
```
    
- **Компоненты высшего порядка (HOCs) и хуки**: Если вы используете HOC или хуки, храните их в отдельной папке `hoc` или `hooks` в соответствующем компоненте.
     
```jsx
// molecules/FormField/hooks/useFormField.js
import { useState } from 'react';

const useFormField = (initialValue) => {
  const [value, setValue] = useState(initialValue);

  const handleChange = (e) => {
    setValue(e.target.value);
  };

  return [value, handleChange];
};

export default useFormField;

```    

- **Документация компонентов**: Используйте `README.md` файлы внутри папок компонентов для документирования их использования и особенностей. Это особенно полезно для больших проектов и работы в команде.
    
    markdown
    

```markdown
<!-- molecules/FormField/README.md -->
# FormField

## Описание
Компонент FormField объединяет метку и поле ввода.

## Пропсы
- `label` (string): Текст метки
- `type` (string): Тип ввода (например, "text", "password")
- `value` (string): Значение поля ввода
- `onChange` (function): Обработчик изменения значения

## Пример использования
```jsx
import React from 'react';
import FormField from './FormField';

const Example = () => {
  const [value, setValue] = useState('');

  return (
    <FormField
      label="Email"
      type="email"
      value={value}
      onChange={(e) => setValue(e.target.value)}
    />
  );
};

export default Example;

```

### Заключение

Организация файловой структуры в Atomic Design помогает упростить разработку, тестирование и поддержку компонентов. Следование этим принципам обеспечит ясность, модульность и повторное использование кода, что приведет к более стабильному и масштабируемому проекту.