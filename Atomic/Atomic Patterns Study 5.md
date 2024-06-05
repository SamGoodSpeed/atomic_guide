Date:**2024-06-03

**Abstract/Summary:**
## Практическое применение Atomic Design

- **Создание проекта с использованием Atomic Design**
    - Установка и настройка окружения
    - Создание атомов
    - Построение молекул и организмов
    - Формирование шаблонов и страниц
- **Инструменты и библиотеки**
    - Storybook для визуализации компонентов
    - Использование CSS-in-JS (например, Styled-components)
    - Примеры интеграции с React

**Keywords:** [[Atomic Patterns Study]]

## Практическое применение Atomic Design

### Создание проекта с использованием Atomic Design

#### Установка и настройка окружения

Для начала создадим новый проект React и установим необходимые зависимости:

1. **Создание нового проекта:**
    
    sh
    

- `npx create-react-app atomic-design-example cd atomic-design-example`
    
- **Установка дополнительных зависимостей:**
    
    - **Styled-components** для CSS-in-JS:
        
        sh
        
- `npm install styled-components`
    
- **Storybook** для визуализации компонентов:
    
    sh
    

1. - `npx sb init`
        

#### Создание атомов

Атомы — это базовые строительные блоки. Начнем с создания нескольких простых атомов.

1. **Button.js:**
    
```jsx
// src/components/atoms/Button/Button.js
import React from 'react';
import styled from 'styled-components';

const StyledButton = styled.button`
  padding: 10px 20px;
  font-size: 16px;
  color: white;
  background-color: #007bff;
  border: none;
  border-radius: 4px;
  cursor: pointer;

  &:hover {
    background-color: #0056b3;
  }

  &:disabled {
    background-color: #cccccc;
    cursor: not-allowed;
  }
`;

const Button = ({ label, onClick, disabled }) => (
  <StyledButton onClick={onClick} disabled={disabled}>
    {label}
  </StyledButton>
);

export default Button;

```
    
- **Input.js:**
    
```jsx
// src/components/atoms/Input/Input.js
import React from 'react';
import styled from 'styled-components';

const StyledInput = styled.input`
  padding: 10px;
  font-size: 16px;
  border: 1px solid #cccccc;
  border-radius: 4px;
  width: 100%;
  box-sizing: border-box;
`;

const Input = ({ type, value, onChange, placeholder }) => (
  <StyledInput
    type={type}
    value={value}
    onChange={onChange}
    placeholder={placeholder}
  />
);

export default Input;

```
    

#### Построение молекул и организмов

Молекулы комбинируют атомы для создания более сложных компонентов.

1. **FormField.js:**
    
 ```jsx
 // src/components/molecules/FormField/FormField.js
import React from 'react';
import styled from 'styled-components';
import Input from '../../atoms/Input/Input';
import Label from '../../atoms/Label/Label';

const FieldWrapper = styled.div`
  margin-bottom: 20px;
`;

const FormField = ({ label, type, value, onChange, placeholder }) => (
  <FieldWrapper>
    <Label>{label}</Label>
    <Input type={type} value={value} onChange={onChange} placeholder={placeholder} />
  </FieldWrapper>
);

export default FormField;

```
    
- **LoginForm.js:**
    
```jsx
// src/components/organisms/LoginForm/LoginForm.js
import React, { useState } from 'react';
import FormField from '../../molecules/FormField/FormField';
import Button from '../../atoms/Button/Button';

const LoginForm = ({ onSubmit }) => {
  const [email, setEmail] = useState('');
  const [password, setPassword] = useState('');

  const handleSubmit = (e) => {
    e.preventDefault();
    onSubmit({ email, password });
  };

  return (
    <form onSubmit={handleSubmit}>
      <FormField label="Email" type="email" value={email} onChange={(e) => setEmail(e.target.value)} placeholder="Enter your email" />
      <FormField label="Password" type="password" value={password} onChange={(e) => setPassword(e.target.value)} placeholder="Enter your password" />
      <Button label="Login" />
    </form>
  );
};

export default LoginForm;

```
    

#### Формирование шаблонов и страниц

Шаблоны определяют структуру страниц без конкретного контента.

1. **ProductPageTemplate.js:**
    
```jsx
// src/components/templates/ProductPage/ProductPageTemplate.js
import React from 'react';
import Header from '../../organisms/Header/Header';
import ProductSection from '../../organisms/ProductSection/ProductSection';
import Footer from '../../organisms/Footer/Footer';

const ProductPageTemplate = ({ products }) => (
  <div>
    <Header />
    <ProductSection products={products} />
    <Footer />
  </div>
);

export default ProductPageTemplate;

```
    

Страницы используют шаблоны и заполняются конкретным контентом.

1. **ProductPage.js:**
    
```jsx
// src/pages/ProductPage.js
import React from 'react';
import ProductPageTemplate from '../components/templates/ProductPage/ProductPageTemplate';
import products from '../data/products'; // Пример данных

const ProductPage = () => <ProductPageTemplate products={products} />;

export default ProductPage;

```

### Инструменты и библиотеки

#### Storybook для визуализации компонентов

1. **Установка и настройка Storybook:**
    
    sh
    

- `npx sb init`
    
- **Создание истории для компонента Button:**
    
```jsx
// src/components/atoms/Button/Button.stories.js
import React from 'react';
import Button from './Button';

export default {
  title: 'Atoms/Button',
  component: Button,
};

const Template = (args) => <Button {...args} />;

export const Primary = Template.bind({});
Primary.args = {
  label: 'Primary Button',
};

export const Disabled = Template.bind({});
Disabled.args = {
  label: 'Disabled Button',
  disabled: true,
};

```
    

#### Использование CSS-in-JS (например, Styled-components)

Styled-components позволяет создавать стили непосредственно в JavaScript, обеспечивая динамическое обновление стилей и изоляцию стилей компонентов.

**Пример использования Styled-components:**

```jsx
// src/components/atoms/Button/Button.js
import styled from 'styled-components';

const StyledButton = styled.button`
  padding: 10px 20px;
  font-size: 16px;
  color: white;
  background-color: #007bff;
  border: none;
  border-radius: 4px;
  cursor: pointer;

  &:hover {
    background-color: #0056b3;
  }

  &:disabled {
    background-color: #cccccc;
    cursor: not-allowed;
  }
`;

const Button = ({ label, onClick, disabled }) => (
  <StyledButton onClick={onClick} disabled={disabled}>
    {label}
  </StyledButton>
);

export default Button;

```

#### Примеры интеграции с React

Использование Atomic Design в React-проектах позволяет создать структурированные и модульные компоненты. Пример выше показывает, как можно создавать и организовывать компоненты в проекте, используя Atomic Design. Эти принципы позволяют легко поддерживать и расширять проект, добавляя новые функции и изменяя существующие компоненты без нарушения структуры кода.

### Заключение

Atomic Design помогает структурировать проект, делая его более организованным и поддерживаемым. Использование инструментов, таких как Storybook, и библиотек, таких как Styled-components, позволяет улучшить процесс разработки и обеспечить высокое качество кода.