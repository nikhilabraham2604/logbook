# WorkLog - Time Tracking Application

## Overview

WorkLog is a full-stack time tracking application built with a modern tech stack. The application allows users to manage clients, log time entries with progress tracking, and view comprehensive statistics and history. It features a clean, professional interface with authentication, dashboard analytics, and comprehensive time management capabilities.

## User Preferences

Preferred communication style: Simple, everyday language.

## System Architecture

### Frontend Architecture
- **Framework**: React 18 with TypeScript
- **Routing**: Wouter (lightweight React router)
- **State Management**: TanStack Query (React Query) for server state
- **UI Framework**: Radix UI primitives with custom shadcn/ui components
- **Styling**: Tailwind CSS with CSS variables for theming
- **Form Management**: React Hook Form with Zod validation
- **Build Tool**: Vite with custom configuration

### Backend Architecture
- **Runtime**: Node.js with Express.js
- **Language**: TypeScript (ESM modules)
- **Authentication**: Passport.js with local strategy and session-based auth
- **Session Storage**: PostgreSQL sessions with connect-pg-simple
- **API Design**: RESTful endpoints with proper error handling
- **Security**: Password hashing with scrypt, CSRF protection, secure sessions

### Database Architecture
- **Database**: PostgreSQL (Neon serverless)
- **ORM**: Drizzle ORM with Drizzle Kit for migrations
- **Schema**: Three main entities (users, clients, time_entries) with proper relations
- **Validation**: Drizzle-Zod integration for runtime type safety

## Key Components

### Authentication System
- **Strategy**: Session-based authentication using Passport.js local strategy
- **Password Security**: Scrypt-based password hashing with salt
- **Session Management**: PostgreSQL-backed sessions with automatic table creation
- **Protection**: Authentication middleware for protected routes

### Data Models
- **Users**: Basic user account with username (email), password, and profile info
- **Clients**: Client management with industry, description, and user association
- **Time Entries**: Time logging with hours, progress percentage, description, and notes
- **Relations**: Proper foreign key relationships with cascade deletion

### UI Components
- **Design System**: Custom shadcn/ui components built on Radix UI primitives
- **Layout**: Fixed sidebar navigation with responsive design
- **Forms**: React Hook Form with Zod validation schemas
- **Feedback**: Toast notifications and loading states
- **Data Display**: Tables, cards, and progress indicators

### Business Logic
- **Time Tracking**: Flexible time entry with decimal hours and progress tracking
- **Client Management**: CRUD operations for client information
- **Analytics**: Dashboard statistics including daily/weekly hours and client metrics
- **History**: Filterable time entry history with date ranges and client filtering

## Data Flow

### Authentication Flow
1. User submits login credentials
2. Passport.js validates against database
3. Session created and stored in PostgreSQL
4. Frontend receives user data and updates query cache
5. Protected routes check authentication status

### Time Entry Flow
1. User selects client and enters time details
2. Form validation with Zod schemas
3. API request with authentication check
4. Database insertion with user association
5. Query cache invalidation and UI updates

### Data Fetching
1. TanStack Query manages all server state
2. Automatic background refetching and caching
3. Optimistic updates for better UX
4. Error boundaries and loading states

## External Dependencies

### Core Dependencies
- **@neondatabase/serverless**: PostgreSQL connection with WebSocket support
- **@tanstack/react-query**: Server state management
- **drizzle-orm & drizzle-kit**: Database ORM and migration tools
- **passport & passport-local**: Authentication strategy
- **express-session**: Session management
- **react-hook-form**: Form state management
- **zod**: Runtime type validation

### UI Dependencies
- **@radix-ui/***: Headless UI primitives (20+ components)
- **tailwindcss**: Utility-first CSS framework
- **lucide-react**: Icon library
- **class-variance-authority**: Utility for component variants
- **date-fns**: Date manipulation utilities

### Development Dependencies
- **vite**: Build tool and dev server
- **typescript**: Type safety
- **tsx**: TypeScript execution for development
- **esbuild**: Fast bundling for production

## Deployment Strategy

### Build Process
- **Frontend**: Vite builds React app to `dist/public`
- **Backend**: esbuild bundles server code to `dist/index.js`
- **Database**: Drizzle Kit handles schema migrations

### Environment Configuration
- **Development**: Uses tsx for hot reloading and Vite dev server
- **Production**: Node.js serves static files and API
- **Database**: Requires `DATABASE_URL` environment variable
- **Sessions**: Configurable `SESSION_SECRET` for security

### File Structure
- `client/`: Frontend React application
- `server/`: Backend Express application  
- `shared/`: Shared types and schemas
- `migrations/`: Database migration files
- Root configuration files for build tools

The application follows a monorepo structure with clear separation between frontend, backend, and shared code, making it maintainable and scalable for a time tracking solution.