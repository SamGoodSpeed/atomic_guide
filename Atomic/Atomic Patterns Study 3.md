### Date: 2024-06-03

**Abstract/Summary:**
## Core Principles of Atomic Design

- **Atoms**
    - Definition and examples
    - Role in design
- **Molecules**
    - Definition and examples
    - Role in design
- **Organisms**
    - Definition and examples
    - Role in design
- **Templates**
    - Definition and examples
    - Role in design
- **Pages**
    - Definition and examples
    - Role in design
	
**Keywords:** [[Atomic Patterns Study]]

## Core Principles of Atomic Design

### Atoms

#### Definition and Examples

Atoms are the simplest and most basic components of an interface. They include elements that cannot be broken down into smaller parts, such as buttons, icons, input fields, etc.

**Examples:**

- Button
- Icon
- Input
- Heading

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

#### Role in Design

Atoms serve as the building blocks for more complex components. They provide basic interface elements that can be reused in various parts of the application, ensuring consistency and ease of maintenance.

### Molecules

#### Definition and Examples

Molecules are combinations of atoms that together create more complex components. They combine several atoms to perform specific functions.

**Examples:**

- Form Field with Label
- Product Card
- Navigation Item

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
export default FormField;
```

#### Role in Design

Molecules combine atoms into more functional components. They allow for the creation of complex interface elements from simple building blocks, providing modularity and reusability.

### Organisms

#### Definition and Examples

Organisms are more complex structures composed of atoms and molecules. They create parts of the interface that can include interaction and state.

**Examples:**

- Login Form
- Website Header
- Product Section

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

#### Role in Design

Organisms create large and functional blocks of the interface that can include logic and state. They are used to create significant parts of the interface and are often used in templates.

### Templates

#### Definition and Examples

Templates are combinations of organisms, molecules, and atoms that create a page layout without specific content. They define the structure and placement of elements on a page.

**Examples:**

- Product Page Layout
- Profile Page Layout
- Homepage Layout

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

#### Role in Design

Templates define the overall structure of pages, setting the layout for components. They help determine how organisms and other components will be placed on the page, but without specific content.

### Pages

#### Definition and Examples

Pages are specific implementations of templates filled with content. They include all the components and data necessary for a complete page.

**Examples:**

- Homepage
- Product Page
- User Profile Page

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

#### Role in Design

Pages represent the final product that the user sees. They combine templates with specific content, creating complete pages ready for use in the application.
