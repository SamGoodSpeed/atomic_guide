Date:**2024-06-03

**Abstract/Summary:**

## Лучшие практики и советы

- **Советы по эффективному использованию Atomic Design**
    - Как поддерживать и обновлять дизайн-систему
    - Работа в команде с Atomic Design
- **Ошибки, которых следует избегать**
    - Частые ошибки и как их избежать


**Keywords:** [[Atomic Patterns Study]]

Использование CSS-in-JS и модульного CSS с Sass имеют свои преимущества и недостатки. Вот обновленный раздел с учетом использования модульного CSS и Sass.

## Лучшие практики и советы

### Советы по эффективному использованию Atomic Design

#### Как поддерживать и обновлять дизайн-систему

1. **Единый источник правды (Single Source of Truth)**: Убедитесь, что все компоненты и стили хранятся в одном месте. Это облегчает обновление и поддержание согласованности между всеми частями проекта.
 

```markdown
<!-- README.md -->
# Дизайн-система

Наша дизайн-система хранится в папке `src/components`. Все изменения должны быть внесены сюда.
```

    
- **Документация компонентов**: Ведите документацию для каждого компонента, объясняя его использование, пропсы и примеры. Это особенно полезно для новых членов команды.


```markdown
<!-- components/atoms/Button/README.md -->
# Button

## Пропсы
- `label` (string): Текст кнопки.
- `onClick` (function): Функция, вызываемая при клике.
- `disabled` (boolean): Флаг для отключения кнопки.

## Пример использования
```jsx
<Button label="Click Me" onClick={() => alert('Clicked!')} />

```

- **Ревью кода и стандарты**: Введите практику регулярного ревью кода и следуйте стандартам кодирования, чтобы гарантировать качество и согласованность кода.
 
```markdown
<!-- CONTRIBUTING.md -->
# Рекомендации по внесению изменений

- Все компоненты должны быть протестированы.
- Обязательно добавляйте истории в Storybook для новых компонентов.
- Следуйте стилю кодирования, установленному в проекте.

```
    
- **Использование Storybook**: Storybook помогает визуализировать и тестировать компоненты в изоляции. Регулярно обновляйте истории компонентов, чтобы отражать изменения в дизайне.
  

```jsx
// components/atoms/Button/Button.stories.js
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
    

#### Работа в команде с Atomic Design

1. **Четкая коммуникация**: Обеспечьте, чтобы все члены команды понимали принципы Atomic Design и следовали единому подходу при создании компонентов.
    
```markdown
<!-- README.md -->
# Руководство по Atomic Design

Atomic Design помогает нам создавать модульные и переиспользуемые компоненты. В этой дизайн-системе мы используем следующие уровни:
- Атомы
- Молекулы
- Организмы
- Шаблоны
- Страницы

Убедитесь, что вы понимаете и используете эти уровни при разработке.

```
    
- **Использование Git**: Ветвление и пулл-реквесты позволяют эффективно управлять изменениями и улучшениями компонентов.
    
    sh
    

1. `git checkout -b feature/add-new-button git commit -m "Добавил новый компонент Button" git push origin feature/add-new-button`
    
2. **Регулярные встречи**: Обсуждение текущих задач и проблем на регулярных встречах помогает синхронизировать работу команды и решать возникающие вопросы.
    

### Ошибки, которых следует избегать

#### Частые ошибки и как их избежать

1. **Избыточная детализация компонентов**: Не дробите компоненты слишком мелко. Атомы должны быть действительно базовыми элементами. Если компонент можно разбить, но это приведет к усложнению, оставьте его как есть.
    
    **Как избежать**: Всегда оценивайте, насколько компонент самодостаточен и функционален.
    
2. **Неправильное использование уровней**: Иногда разработчики могут путать уровни и создавать сложные компоненты на уровне атомов или простые на уровне организмов.
    
    **Как избежать**: Всегда проверяйте, соответствует ли компонент своему уровню в Atomic Design.
    
3. **Отсутствие тестов**: Без тестирования компоненты могут содержать ошибки, которые сложно отловить.
    
    **Как избежать**: Используйте тестовые фреймворки, такие как Jest, для создания и запуска тестов для каждого компонента.
    
    jsx
    
```jsx
// components/atoms/Button/Button.test.js
import React from 'react';
import { render, fireEvent } from '@testing-library/react';
import Button from './Button';

test('Button renders correctly', () => {
  const { getByText } = render(<Button label="Click Me" />);
  expect(getByText('Click Me')).toBeInTheDocument();
});

test('Button onClick works', () => {
  const handleClick = jest.fn();
  const { getByText } = render(<Button label="Click Me" onClick={handleClick} />);
  fireEvent.click(getByText('Click Me'));
  expect(handleClick).toHaveBeenCalledTimes(1);
});

```
    
- **Плохая организация стилей**: Использование различных подходов к стилизации может привести к несогласованности стилей.
    
    **Как избежать**: Используйте модульный CSS и Sass для управления стилями компонентов. Это позволяет избежать конфликтов имен и улучшить организацию стилей.
    
```css
// components/atoms/Button/Button.module.scss
.button {
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
}

```

```jsx
// components/atoms/Button/Button.js
import React from 'react';
import styles from './Button.module.scss';

const Button = ({ label, onClick, disabled }) => (
  <button className={styles.button} onClick={onClick} disabled={disabled}>
    {label}
  </button>
);

export default Button;

```

Следование этим лучшим практикам и советам поможет вам эффективно использовать Atomic Design, избегая распространенных ошибок и создавая высококачественные, поддерживаемые и масштабируемые интерфейсы.