# Aadhaar Operator Dashboard

## Overview

This is a full-stack web application for managing Aadhaar enrollment data across multiple branches and zones. The system enables operators to submit daily enrollment entries, zone managers to monitor their regions, and admins to view comprehensive reports across all locations. The application supports 200+ branches with daily and 5-day interval data collection, real-time calculations for enrollment amounts, and HTML file upload functionality for batch data processing.

## User Preferences

Preferred communication style: Simple, everyday language.

## System Architecture

### Frontend Architecture
- **Framework**: React 18 with TypeScript
- **Routing**: Wouter (lightweight React router)
- **State Management**: TanStack React Query for server state caching and synchronization
- **UI Components**: shadcn/ui component library built on Radix UI primitives
- **Styling**: Tailwind CSS with custom design system (CSS variables for theming)
- **Charts**: Recharts for data visualization on dashboards
- **Build Tool**: Vite with custom plugins for Replit integration

### Backend Architecture
- **Runtime**: Node.js with Express.js
- **Language**: TypeScript (ESM modules)
- **API Design**: RESTful endpoints defined in `shared/routes.ts` with Zod validation schemas
- **File Uploads**: Multer for HTML file processing (5MB limit, .html only)

### Database
- **ORM**: Drizzle ORM with PostgreSQL dialect
- **Schema Location**: `shared/schema.ts` - contains tables for users, branches, operators, and enrollments
- **Migrations**: Drizzle Kit for schema migrations (`drizzle.config.ts`)

### Authentication & Authorization
- **Role-Based Access Control**: Three user roles - admin, zone_manager, operator
- **Session Management**: Simple credential-based login (password stored in DB)
- **Route Protection**: Client-side auth hook (`use-auth.ts`) with protected route wrapper

### Attendance System
- **Daily Attendance**: Operators can mark themselves present via the Mark Attendance button on their dashboard
- **Leave Management**: Admins can add leave records with quick duration options (today, 2 days, 5 days, etc.)
- **Zone-wise Summary**: Leave Management page includes Attendance Summary tab showing present/absent/leave counts by zone
- **Automatic Status**: If operator doesn't mark attendance, they're shown as absent; approved leaves override absence

### Project Structure
```
├── client/           # React frontend
│   └── src/
│       ├── components/   # UI components (shadcn + custom)
│       ├── hooks/        # React Query hooks for API calls
│       ├── pages/        # Route components
│       └── lib/          # Utilities and query client
├── server/           # Express backend
│   ├── routes.ts     # API route handlers
│   ├── storage.ts    # Database operations (IStorage interface)
│   └── db.ts         # Database connection
├── shared/           # Shared types and schemas
│   ├── schema.ts     # Drizzle table definitions
│   └── routes.ts     # API route contracts with Zod
└── migrations/       # Database migrations
```

### Key Design Patterns
- **Shared Schema**: Both frontend and backend use the same Zod schemas for type safety
- **Storage Interface**: `IStorage` interface abstracts database operations for testability
- **Query Key Convention**: API paths used as React Query cache keys
- **Role-Based Views**: Dashboard component renders different UIs based on user role

## External Dependencies

### Database
- **PostgreSQL**: Primary database accessed via `DATABASE_URL` environment variable
- **Connection**: pg Pool with Drizzle ORM wrapper

### Third-Party Libraries
- **Radix UI**: Accessible component primitives (dialogs, dropdowns, forms)
- **date-fns**: Date formatting and manipulation for reports
- **Zod**: Runtime schema validation for API requests/responses
- **drizzle-zod**: Automatic Zod schema generation from Drizzle tables

### Development Tools
- **Replit Plugins**: Runtime error overlay, cartographer, dev banner for Replit environment
- **esbuild**: Production server bundling with dependency allowlist optimization