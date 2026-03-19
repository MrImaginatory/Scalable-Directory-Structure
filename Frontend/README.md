# Frontend - Scalable React Application

A scalable frontend application built with React 19, TypeScript, and Vite. This project follows a modular, feature-based folder structure designed for maintainability and scalability.

## Tech Stack

- **React 19** - UI Library
- **TypeScript** - Type safety
- **Vite** - Build tool and dev server
- **ESLint** - Code linting with React hooks support
- **React Compiler** - Experimental React compiler for automatic optimization

## Available Scripts

| Command | Description |
|---------|-------------|
| `npm run dev` | Start development server with HMR |
| `npm run build` | Build for production |
| `npm run lint` | Run ESLint |
| `npm run preview` | Preview production build |

## Folder Structure

```
Frontend/
├── public/                 # Static assets served directly
├── src/
│   ├── @types/            # Global TypeScript type definitions
│   │   └── *.d.ts        # Declaration files for types
│   │
│   ├── api/               # API layer - HTTP clients and service calls
│   │   ├── endpoints/    # API endpoint definitions
│   │   ├── interceptors/ # Request/response interceptors
│   │   └── index.ts      # API configuration and exports
│   │
│   ├── assets/            # Static assets (images, fonts, icons)
│   │   ├── images/       # Image files
│   │   ├── fonts/       # Font files
│   │   └── icons/       # Icon assets
│   │
│   ├── components/       # Reusable UI components
│   │   ├── common/      # Shared components (Button, Input, Modal, etc.)
│   │   ├── layout/      # Layout components (Header, Footer, Sidebar)
│   │   └── features/    # Feature-specific components
│   │
│   ├── hooks/            # Custom React hooks
│   │   ├── useAuth.ts   # Authentication hook
│   │   ├── useFetch.ts  # Data fetching hook
│   │   └── *.ts         # Other custom hooks
│   │
│   ├── pages/            # Page components (routes)
│   │   ├── Home/        # Home page and its components
│   │   ├── Dashboard/   # Dashboard page
│   │   └── *.tsx       # Other page components
│   │
│   ├── routes/           # Application routing
│   │   ├── index.ts     # Route definitions
│   │   ├── private/     # Protected routes
│   │   └── public/     # Public routes
│   │
│   ├── templates/        # Page templates and layouts
│   │   ├── AuthTemplate.tsx    # Authentication layout
│   │   └── DashboardTemplate.tsx # Dashboard layout
│   │
│   ├── themes/           # Theme configuration
│   │   ├── colors.ts    # Color palette
│   │   ├── typography.ts # Typography settings
│   │   └── index.ts     # Theme provider setup
│   │
│   ├── utils/            # Utility functions
│   │   ├── helpers.ts   # Helper functions
│   │   ├── constants.ts # App constants
│   │   └── formatters.ts # Data formatting utilities
│   │
│   ├── validators/       # Form and input validation
│   │   ├── auth.ts      # Auth-related validations
│   │   └── *.ts         # Other validation schemas
│   │
│   ├── App.tsx           # Root application component
│   ├── main.tsx          # Application entry point
│   └── index.css        # Global styles
│
├── index.html            # HTML entry point
├── vite.config.ts        # Vite configuration
├── tsconfig.json         # TypeScript configuration
├── eslint.config.js      # ESLint configuration
└── package.json         # Dependencies and scripts
```

## Directory Purpose Details

### `@types/`
Contains global TypeScript type definitions and declaration files. This includes:
- Extended types for libraries without types
- Global type augmentations
- Shared interface definitions

### `api/`
Handles all HTTP communications:
- Axios/Fetch configuration
- API service methods
- Request/response interceptors
- Error handling

### `assets/`
Static resources that are processed by Vite:
- Images (PNG, JPG, SVG, WebP)
- Fonts (WOFF2, TTF)
- Icon files

### `components/`
Reusable UI components organized by scope:
- **common/**: Generic components (Button, Card, Input, Modal, etc.)
- **layout/**: Structural components (Header, Footer, Sidebar, etc.)
- **features/**: Business-specific components

### `hooks/`
Custom React hooks for reusable logic:
- State management hooks
- Data fetching hooks
- Authentication hooks
- Form handling hooks

### `pages/`
Top-level page components that correspond to routes:
- Each page in its own directory
- Co-located with page-specific components
- Contains page-specific styles and types

### `routes/`
Application routing configuration:
- Public routes definition
- Protected/private routes
- Route guards
- Lazy loading configuration

### `templates/`
Page layout templates:
- Consistent layouts for different page types
- Wrapper components with common UI patterns
- Auth layout, dashboard layout, etc.

### `themes/`
Theme management:
- Color schemes
- Typography scales
- Spacing systems
- CSS custom properties

### `utils/`
Pure utility functions:
- Data transformation helpers
- Date/number formatters
- Validation helpers
- Constants

### `validators/`
Input validation logic:
- Form validation schemas
- Input sanitization
- Business rule validations

## Best Practices

1. **Colocation**: Keep related files together (components with their styles, hooks with their types)

2. **Barrel Exports**: Use `index.ts` files for clean imports

3. **Feature-Based Organization**: Group by feature when components are tightly coupled

4. **Type Safety**: Leverage TypeScript for type safety across the application

5. **Lazy Loading**: Use React.lazy for route-based code splitting

## ESLint Configuration

The project uses:
- `@eslint/js` - JavaScript recommended rules
- `typescript-eslint` - TypeScript-specific rules
- `eslint-plugin-react-hooks` - React hooks rules
- `eslint-plugin-react-refresh` - React refresh compatibility

## TypeScript Configuration

- `tsconfig.json` - Base configuration referencing other configs
- `tsconfig.app.json` - Application code configuration
- `tsconfig.node.json` - Node-specific configuration (Vite config)

## Adding New Features

1. Create a new directory in `pages/` for the feature
2. Add components in `components/features/`
3. Create hooks in `hooks/` if needed
4. Add API methods in `api/`
5. Set up routes in `routes/`
6. Add validators if needed in `validators/`
