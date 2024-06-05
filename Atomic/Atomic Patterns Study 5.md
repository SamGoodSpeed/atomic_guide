## Practical Application of Atomic Design

### Implementing Atomic Design in a Project

#### Setting up the Development Environment

1. **Create a New React Project:**

```bash
npx create-react-app atomic-design-example
cd atomic-design-example
```

2. **Install Additional Dependencies:**

   - **Styled-components** for CSS-in-JS:

```bash
npm install styled-components
```

   - **Storybook** for component visualization:

```bash
npx sb init
```

### Creating Atoms

Atoms are the fundamental building blocks. Let's start by creating a few simple atoms:

```jsx
// atoms/Button/Button.js
import styled from 'styled-components';

const Button = styled.button`
  padding: 10px 20px;
  background-color: #007bff;
  color: white;
  border: none;
  border-radius: 5px;
  cursor: pointer;
`;

export default Button;
```

```jsx
// atoms/Input/Input.js
import styled from 'styled-components';

const Input = styled.input`
  padding: 10px;
  border: 1px solid #ccc;
  border-radius: 5px;
  width: 100%;
`;

export default Input;
```

```jsx
// atoms/Label/Label.js
import styled from 'styled-components';

const Label = styled.label`
  display: block;
  margin-bottom: 5px;
  font-weight: bold;
`;

export default Label;
```

These components represent basic UI elements like buttons, inputs, and labels. They are styled using Styled-components, keeping styles within the component files.

### Building Molecules and Organisms

Molecules combine atoms to create more complex components. Organisms, in turn, combine molecules to form even larger functional units.

```jsx
// molecules/FormField/FormField.js
import React from 'react';
import atoms from '../atoms';
const { Label, Input } = atoms;

const FormField = ({ label, type, value, onChange }) => (
  <div className="form-field">
    <Label text={label} />
    <Input type={type} value={value} onChange={onChange} />
  </div>
);

export default FormField;
```

```jsx
// organisms/LoginForm/LoginForm.js
import React from 'react';
import molecules from '../molecules';
import atoms from '../atoms';
const { FormField, Button } = molecules;
const { Label } = atoms;

const LoginForm = () => (
  <form>
    <FormField label="Email" type="email" />
    <FormField label="Password" type="password" />
    <Button type="submit">Login</Button>
  </form>
);

export default LoginForm;
```

These components illustrate how molecules combine atoms (FormField) and organisms combine molecules (LoginForm).

### Creating Templates and Pages

Templates define the layout of pages, while pages combine templates with content to form the final user interface.

```jsx
// templates/ProductPageTemplate.js
import React from 'react';
import organisms from '../organisms';
const { Header, ProductSection } = organisms;

const ProductPageTemplate = ({ product }) => (
  <div>
    <Header />
    <ProductSection product={product} />
  </div>
);

export default ProductPageTemplate;
```

```jsx
// pages/ProductPage.js
import React from 'react';
import templates from '../templates';
import productData from './productData';
const { ProductPageTemplate } = templates;

const ProductPage = () => (
  <ProductPageTemplate product={productData} />
);

export default ProductPage;
```

These components demonstrate how templates (ProductPageTemplate) structure the layout and pages (ProductPage) populate it with content.

### Tools and Libraries

Atomic Design benefits from various tools and libraries:

- **Storybook:** Visualize and interact with components in isolation.

- **CSS-in-JS:** Use libraries like Styled-components to style components within their code.

- **Design Systems:** Implement Atomic Design principles in a larger design system context.

### Example Integration with React

The provided code examples showcase Atomic Design implementation using React and Styled-components. This setup enables creating reusable and modular UI components that follow Atomic Design principles.

By following these steps and utilizing the mentioned tools, developers can effectively implement Atomic Design in their React projects, leading to maintainable, scalable, and consistent user interfaces.

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
    
#### Building molecules and organisms

Molecules combine atoms to create more complex components.

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
    

#### Formation of templates and pages

Templates define the structure of pages without specific content.

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
    

Pages use templates and are filled with specific content.

1. **ProductPage.js:**
    
```jsx
// src/pages/ProductPage.js
import React from 'react';
import ProductPageTemplate from '../components/templates/ProductPage/ProductPageTemplate';
import products from '../data/products'; // Пример данных

const ProductPage = () => <ProductPageTemplate products={products} />;

export default ProductPage;

```
### Tools and Libraries

#### Storybook for visualizing components

1. **Installing and setting up Storybook:**
   
    sh
    

- `npx sb init`
    
- **Creating a history for the Button component:**
    
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
    

#### Using CSS-in-JS (e.g. Styled-components)

Styled-components allows you to create styles directly in JavaScript, providing dynamic style updating and component style isolation.

**Example of using Styled-components:**


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

#### Examples of integration with React

Using Atomic Design in React projects allows you to create structured and modular components. The example above shows how you can create and organize components in a project using Atomic Design. These principles make it easy to maintain and expand a project by adding new features and changing existing components without breaking the code structure.

### Conclusion

Atomic Design helps you structure your project, making it more organized and maintainable. Using tools like Storybook and libraries like Styled-components can improve your development process and ensure high-quality code.
