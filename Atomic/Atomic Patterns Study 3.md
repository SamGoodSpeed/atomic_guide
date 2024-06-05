Date:**2024-06-03

**Abstract/Summary:**
## Основные принципы Atomic Design

- **Атомы (Atoms)**
    - Определение и примеры
    - Роль в дизайне
- **Молекулы (Molecules)**
    - Определение и примеры
    - Роль в дизайне
- **Организмы (Organisms)**
    - Определение и примеры
    - Роль в дизайне
- **Шаблоны (Templates)**
    - Определение и примеры
    - Роль в дизайне
- **Страницы (Pages)**
    - Определение и примеры
    - Роль в дизайне
	
**Keywords:** [[Atomic Patterns Study]]

## Основные принципы Atomic Design

### Атомы (Atoms)

#### Определение и примеры

Атомы — это самые простые и базовые компоненты интерфейса. Они включают в себя элементы, которые не могут быть разбиты на более мелкие части, такие как кнопки, иконки, текстовые поля, и т.д.

**Примеры:**

- Кнопка (Button)
- Иконка (Icon)
- Текстовое поле (Input)
- Заголовок (Heading)

```jsx
// atoms/Button.js
import React from 'react';
import './Button.css';
const Button = ({ label, onClick, disabled }) => (
	<button className="button" onClick={onClick} disabled={disabled}>     
		{label}   
	</button> 
);  
export default Button;
```

#### Роль в дизайне

Атомы служат строительными блоками для более сложных компонентов. Они обеспечивают базовые элементы интерфейса, которые могут быть переиспользованы в различных частях приложения, обеспечивая согласованность и простоту поддержки.

### Молекулы (Molecules)

#### Определение и примеры

Молекулы — это комбинации атомов, которые вместе создают более сложные компоненты. Они объединяют несколько атомов для выполнения определённых функций.

**Примеры:**

- Поле формы с меткой (Form Field with Label)
- Карточка товара (Product Card)
- Навигационный элемент (Navigation Item)

jsx


```jsx
// molecules/FormField.js 
import React from 'react'; 
import Label from '../atoms/Label'; 
import Input from '../atoms/Input';  

const FormField = ({ label, type, value, onChange, error }) => (   
	<div className="form-field">     
		<Label text={label} />     
		<Input type={type} value={value} onChange={onChange} />
		{error && <span className="error">{error}</span>}   
	 </div> 
 );  
export default FormField;```

#### Роль в дизайне

Молекулы объединяют атомы в более функциональные компоненты. Они позволяют создать сложные элементы интерфейса из простых строительных блоков, обеспечивая модульность и повторное использование.

### Организмы (Organisms)

#### Определение и примеры

Организмы — это более сложные структуры, состоящие из атомов и молекул. Они создают части интерфейса, которые могут включать взаимодействие и состояние.

**Примеры:**

- Форма входа (Login Form)
- Шапка сайта (Website Header)
- Секция товаров (Product Section)

jsx


```jsx
// organisms/LoginForm.js
import React, { useState } from 'react';
import FormField from '../molecules/FormField';
import Button from '../atoms/Button';

const LoginForm = ({ onSubmit }) => {
  const [email, setEmail] = useState('');
  const [password, setPassword] = useState('');
  const [error, setError] = useState('');

  const handleSubmit = (e) => {
    e.preventDefault();
    if (!email || !password) {
      setError('All fields are required');
      return;
    }
    setError('');
    onSubmit({ email, password });
  };

  return (
    <form onSubmit={handleSubmit}>
      <FormField label="Email" type="email" value={email} onChange={(e) => setEmail(e.target.value)} error={error} />
      <FormField label="Password" type="password" value={password} onChange={(e) => setPassword(e.target.value)} error={error} />
      <Button label="Login" />
    </form>
  );
};

export default LoginForm;

```

#### Роль в дизайне

Организмы создают крупные и функциональные блоки интерфейса, которые могут включать логику и состояние. Они служат для создания значительных частей интерфейса и часто используются в шаблонах.

### Шаблоны (Templates)

#### Определение и примеры

Шаблоны — это комбинации организмов, молекул и атомов, которые создают макет страницы без конкретного контента. Они определяют структуру и расположение элементов на странице.

**Примеры:**

- Макет страницы продукта (Product Page Layout)
- Макет страницы профиля (Profile Page Layout)
- Макет главной страницы (Homepage Layout)

jsx


```jsx
// templates/ProductPage.js
import React from 'react';
import Header from '../organisms/Header';
import ProductSection from '../organisms/ProductSection';
import Footer from '../organisms/Footer';

const ProductPage = () => (
  <div>
    <Header />
    <ProductSection />
    <Footer />
  </div>
);

export default ProductPage;

```

#### Роль в дизайне

Шаблоны определяют общую структуру страниц, задавая расположение компонентов. Они помогают определить, как организмы и другие компоненты будут размещены на странице, но без конкретного содержимого.

### Страницы (Pages)

#### Определение и примеры

Страницы — это конкретные реализации шаблонов с наполненным контентом. Они включают все компоненты и данные, необходимые для полной страницы.

**Примеры:**

- Главная страница (Homepage)
- Страница продукта (Product Page)
- Страница профиля пользователя (User Profile Page)

jsx

```jsx
 // pages/Product.js
import React from 'react';
import ProductPageTemplate from '../templates/ProductPage';
import productData from '../data/productData';

const ProductPage = () => (
  <ProductPageTemplate product={productData} />
);

export default ProductPage;
```

#### Роль в дизайне

Страницы представляют собой конечный продукт, который видит пользователь. Они объединяют шаблоны с конкретным содержимым, создавая полные страницы, готовые к использованию в приложении.