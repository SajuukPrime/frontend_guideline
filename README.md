# 前端开发规范 - React + TypeScript + Vite 项目

## 目录 / Table of Contents
1. [项目结构 / Project Structure](#项目结构)
2. [代码风格 / Code Style](#代码风格)
3. [TypeScript 规范 / TypeScript Guidelines](#typescript-规范)
4. [React 组件 / React Components](#react-组件)
5. [状态管理 / State Management](#状态管理)
6. [API 请求 / API Requests](#api-请求)
7. [错误处理 / Error Handling](#错误处理)
8. [Git 规范 / Git Guidelines](#git-规范)
9. [代码审查和合并请求 / Code Review and Pull Requests](#代码审查和合并请求)
10. [测试规范 / Testing Guidelines](#测试规范)
11. [文档编写 / Documentation](#文档编写)
12. [环境管理 / Environment Management](#环境管理)
13. [性能优化 / Performance Optimization](#性能优化)
14. [国际化支持 / Internationalization Support](#国际化支持)
15. [持续集成和持续部署 (CI/CD) / Continuous Integration and Continuous Deployment (CI/CD)](#持续集成和持续部署-cicd)

---

## 项目结构 / Project Structure

确保项目结构一致，促进代码可维护性和可读性。  
```
Ensure a consistent project structure to promote code maintainability and readability.
├── public # 静态资源 / Static Assets 
│ ├── index.html # 入口 HTML 文件 / Entry HTML File 
│ └── favicon.ico # 网站图标 / Website Icon 
├── src 
│ ├── assets # 资源文件（图片、字体等）/ Asset Files (Images, Fonts, etc.) 
│ ├── components # 可复用的组件 / Reusable Components 
│ ├── hooks # 自定义 Hooks / Custom Hooks 
│ ├── pages # 页面组件 / Page Components 
│ ├── services # API 服务 / API Services 
│ ├── styles # 样式文件（CSS/SCSS）/ Style Files (CSS/SCSS) 
│ ├── typings # TypeScript 类型声明 / TypeScript Type Declarations 
│ ├── utils # 工具函数 / Utility Functions 
│ ├── contexts # React Contexts 
│ ├── App.tsx # 主应用组件 / Main Application Component 
│ ├── Router.tsx # 路由配置文件 / Routing Configuration File 
│ └── index.tsx # 入口文件 / Entry File 
├── .env # 环境变量配置 / Environment Variables Configuration 
├── .eslintrc.js # ESLint 配置 / ESLint Configuration 
├── .prettierrc # Prettier 配置 / Prettier Configuration 
├── tsconfig.json # TypeScript 配置 / TypeScript Configuration 
└── vite.config.ts # Vite 配置 / Vite Configuration
```
## 代码风格 / Code Style

- **代码格式化**：使用 ESLint 和 Prettier 自动化代码样式检查和格式化，确保代码一致性。  
  **Code Formatting**: Use ESLint and Prettier to automate style checking and formatting to ensure consistency.

- **缩进**：使用 2 个空格进行缩进。  
  **Indentation**: Use 2 spaces for indentation.

- **字符串引号**：使用单引号（`'`）包裹字符串，双引号（`"`）仅在字符串中包含单引号时使用。  
  **String Quotes**: Use single quotes (`'`) for strings; use double quotes (`"`) only when single quotes are included in the string.

- **行长**：每行代码限制为 80-120 个字符，超出部分应换行。  
  **Line Length**: Limit each line of code to 80-120 characters and wrap lines that exceed this limit.

- **空行**：组件、函数和类之间应添加一个空行，逻辑块之间添加一个或多个空行以增强可读性。  
  **Blank Lines**: Add one blank line between components, functions, and classes, and one or more blank lines between logical blocks for better readability.

### 示例 / Example

```javascript
// 正确示例 / Correct Example
const message = 'Hello, World!';

// 错误示例 / Incorrect Example
const message = "Hello, World!";
```

### TypeScript 规范 / TypeScript Guidelines
- **严格模式**：启用 TypeScript 的严格模式 (strict), 强制使用类型。
**Strict Mode**: Enable TypeScript's strict mode (strict) to enforce type usage.

- **基本类型**：避免使用 any 类型，避免隐式 any，应使用具体类型。
**Basic Types**: Avoid using the any type and implicit any; use specific types instead.

- **接口与类型**：优先使用 interface 进行对象的类型定义，接口可扩展。
**Interfaces and Types**: Prefer using interface for object type definitions as interfaces are extensible.

### 示例 / Example
```
interface User {
  id: number;
  name: string;
  email: string;
}

// 正确示例 / Correct Example
const user: User = {
  id: 1,
  name: 'Jane Doe',
  email: 'jane.doe@example.com',
};

// 可选属性 / Optional Properties
interface User {
  id: number;
  name: string;
  email?: string; // 可选属性 / Optional Property
}
```

### React 组件 / React Components
- **函数式组件**：使用函数式组件和 Hooks 进行开发，避免类组件。
**Functional Components**: Use functional components and Hooks for development; avoid class components.

- **组件命名**：组件命名遵循 PascalCase，例如 MyComponent。
**Component Namin**g: Component names should follow PascalCase, e.g., MyComponent.

- **Props 类型**：所有组件的 props 都需要定义类型，优先使用接口（interface）。
**Props Types**: All component props must have their types defined, preferably using an interface.

- **默认 Props**：使用 defaultProps 设置组件的默认属性。
**Default Props**: Use defaultProps to set default properties for components.

- **事件处理**：使用箭头函数或 bind 语法确保 this 的正确指向。
**Event Handling**: Use arrow functions or bind syntax to ensure correct handling of this.

### 示例 / Example
``` tsx
复制代码
import React from 'react';

interface ButtonProps {
  label: string;
  onClick: () => void;
}

const Button: React.FC<ButtonProps> = ({ label, onClick }) => (
  <button onClick={onClick}>{label}</button>
);

Button.defaultProps = {
  label: 'Default Label',
};

export default Button;
```

### 状态管理 / State Management
- **React Context**：对于全局状态管理，动画、主题等场景使用 React Context，配合 Hooks 使用。
**React Context**: Use React Context for global state management in scenarios like animations and themes, alongside Hooks.

- **状态管理库**：对于大型应用，推荐使用 Redux、Zustand 或 Recoil 等状态管理库。
**State Management Libraries**: For large applications, consider using state management libraries such as Redux, Zustand, or Recoil.

- **状态设计**：合理划分状态管理的责任，尽量让状态层和 UI 层分离。
**State Design**: Carefully divide responsibilities for state management to separate the state layer from the UI layer.

### API 请求 / API Requests
- **API 服务**：使用 Axios 或 Fetch 封装 API 请求，统一处理请求和响应。
**API Services**: Use Axios or Fetch to encapsulate API requests, consolidating request and response handling.

-**错误处理**：统一处理错误，给予用户友好提示。
**Error Handling**: Standardize error handling to provide user-friendly feedback.

-**请求类型**：使用 TypeScript 定义请求和响应的类型，以便进行正确的数据处理。
**Request Types**: Define request and response types using TypeScript for proper data handling.

### 示例 / Example
```typescript
import axios from 'axios';

const API_URL = import.meta.env.VITE_API_URL;

interface User {
  id: number;
  name: string;
  email: string;
}

const fetchUsers = async (): Promise<User[]> => {
  try {
    const response = await axios.get<User[]>(`${API_URL}/users`);
    return response.data;
  } catch (error) {
    console.error('Error fetching users:', error);
    throw error; // 应考虑抛出自定义错误 / Consider throwing a custom error
  }
};

export { fetchUsers };
```

### 错误处理 / Error Handling
- **错误边界**：使用 React 的错误边界捕获组件崩溃的错误。
**Error Boundaries**: Use React's error boundaries to catch errors from component crashes.

- **用户反馈**：在发生错误的情况下，针对用户进行适当的反馈，如 toast 通知或错误页面。
**User Feedback**: Provide appropriate feedback to users in case of errors, such as toast notifications or error pages.

- **日志记录**：对错误进行适当的日志记录，便于后续排查。
**Logging**: Properly log errors for future troubleshooting.

### 示例 / Example
``` tsx
import React from 'react';

class ErrorBoundary extends React.Component {
  state = { hasError: false };

  static getDerivedStateFromError(error: Error) {
    return { hasError: true };
  }

  componentDidCatch(error: Error) {
    console.error('Error caught in error boundary:', error);
  }

  render() {
    if (this.state.hasError) {
      return <h1>Something went wrong.</h1>; // 出现错误时的反馈信息 / Feedback message when an error occurs
    }
    return this.props.children;
  }
}

// 使用方式 / Usage
<ErrorBoundary>
  <MyComponent />
</ErrorBoundary>
```

### Git 规范 / Git Guidelines
- **版本控制**：使用 Git 进行版本控制，全员遵循以下分支命名约定：
Version Control: Use Git for version control; all team members should follow these branch naming conventions:
feature/描述：新功能 / New Features
bugfix/描述：修复 bug / Bug Fixes
hotfix/描述：紧急修复 / Hotfixes
提交信息格式 / Commit Message Format
提交信息应遵循如下格式：
Commit messages should follow this format:

```diff
类型: 描述
- 详细说明变更内容 / Detailed description of the changes
```

### 示例 / Example
``` diff
feat: 添加用户登录功能
- 新增 Login 组件 / Added Login component
- 更新路由配置 / Updated routing configuration
```

### 代码审查和合并请求 / Code Review and Pull Requests
- **代码审查**：所有代码更改应通过 Pull Request 提交，文本必须包含变更说明。
**Code Review**: All code changes should be submitted through Pull Requests, and the text must include change descriptions.

- **审核流程**：每个 PR 必须至少经过一名团队成员的审核。
**Review Process**: Each PR must be reviewed by at least one team member.

- **PR 描述**：PR 描述应包括变更内容的简单摘要、相关任务或问题 ID（如适用）以及任何依赖关系或配置更改的说明。
**PR Description**: The PR description should include a brief summary of the changes, related task or issue IDs (if applicable), and explanations for any dependencies or configuration changes.

### 测试规范 / Testing Guidelines
- **测试框架**：使用 Jest 和 React Testing Library 进行单元测试，确保所有功能的正常运作。
**Testing Framework**: Use Jest and React Testing Library for unit testing to ensure proper functionality.

- **测试覆盖率**：每个组件和服务应有相应的测试覆盖率，测试结果应在 CI/CD 流程中被验证。
**Test Coverage**: Each component and service should have corresponding test coverage, and test results should be validated in the CI/CD process.

- **测试文件命名**：测试文件命名为 [ComponentName].test.tsx。
**Test File Naming**: Test files should be named [ComponentName].test.tsx.

### 示例 / Example
``` tsx
import { render, screen } from '@testing-library/react';
import Button from './Button';

test('renders button with label', () => {
  render(<Button label="Click me" onClick={() => {}} />);
  const buttonElement = screen.getByText(/click me/i);
  expect(buttonElement).toBeInTheDocument();
});

test('handles clicks correctly', () => {
  const handleClick = jest.fn();
  render(<Button label="Click me" onClick={handleClick} />);
  
  const buttonElement = screen.getByText(/click me/i);
  buttonElement.click();
  
  expect(handleClick).toHaveBeenCalled();
});

```












