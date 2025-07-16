# TradePro - Cryptocurrency Trading Platform

## Overview

TradePro is a modern cryptocurrency trading platform built with React, Express.js, and PostgreSQL. The application provides real-time cryptocurrency prices from Binance API, trading functionality with time-based profit mechanics, and comprehensive user account management with deposits and withdrawals.

## User Preferences

Preferred communication style: Simple, everyday language.
Data storage: User requested 3 separate JSON files for backing up database data:
- users.json: Store usernames, IDs, phone numbers, passwords (hashed), and balances (USDT, EGP)
- deposits.json: Store all deposit operations
- withdrawals.json: Store all withdrawal operations

## System Architecture

### Frontend Architecture
- **Framework**: React 18 with TypeScript
- **Routing**: Wouter for client-side routing
- **State Management**: TanStack Query (React Query) for server state
- **UI Framework**: Radix UI components with Tailwind CSS
- **Styling**: Tailwind CSS with custom design system (shadcn/ui)
- **Build Tool**: Vite for development and bundling

### Backend Architecture
- **Framework**: Express.js with TypeScript
- **Runtime**: Node.js with ES modules
- **Database ORM**: Drizzle ORM for type-safe database operations
- **Authentication**: Passport.js with local strategy and session-based auth
- **Session Storage**: PostgreSQL session store

### Database Design
- **Primary Database**: PostgreSQL (configured for Neon serverless)
- **Schema**: Four main tables - users, transactions, deposits, withdrawals
- **Migrations**: Drizzle Kit for schema management
- **Connection**: Neon serverless with WebSocket support

## Key Components

### Authentication System
- Session-based authentication using Passport.js
- Password hashing with Node.js crypto scrypt
- Protected routes with authentication middleware
- User registration and login flows

### Trading Engine
- Real-time cryptocurrency price feeds from Binance API
- Time-based trading logic (8:00-8:15 PM Cairo time for guaranteed profits)
- Simulated trading with profit/loss calculations
- Transaction history tracking

### Financial Operations
- Deposit system supporting USDT and EGP methods
- Withdrawal system with pending approval workflow
- User balance management
- Transaction categorization (trade, deposit, withdrawal)

### UI/UX Features
- Arabic language support with RTL-friendly design
- Mobile-first responsive design
- Bottom navigation for mobile devices
- Real-time price updates and trading modals
- Toast notifications for user feedback

## Data Flow

1. **User Authentication**: Users register/login → Session created → Access to protected routes
2. **Price Data**: Binance API → Backend proxy → Frontend display (5-second intervals)
3. **Trading**: User selects crypto → Trading modal → 60-second countdown → Result calculation → Balance update
4. **Financial Operations**: Deposit/withdrawal requests → Pending status → Admin approval (simulated)
5. **Transaction History**: All operations logged → Displayed in user profile

## External Dependencies

### Core Runtime Dependencies
- **Database**: @neondatabase/serverless, drizzle-orm
- **Authentication**: passport, passport-local, express-session, connect-pg-simple
- **Frontend**: react, @tanstack/react-query, wouter
- **UI Components**: @radix-ui/* components, tailwindcss
- **API Integration**: axios for Binance API calls
- **Validation**: zod, drizzle-zod for schema validation

### Development Tools
- **Build**: vite, esbuild for production builds
- **TypeScript**: Full type safety across frontend/backend/shared
- **CSS**: PostCSS, Autoprefixer, Tailwind CSS
- **Replit Integration**: Runtime error overlay, cartographer plugin

### External APIs
- **Binance API**: Real-time cryptocurrency prices and chart data
- **Cairo Time**: Server-side time calculations for trading logic

## Deployment Strategy

### Development Environment
- Vite dev server for frontend with HMR
- Express server with tsx for TypeScript execution
- Database migrations via Drizzle Kit
- Replit-specific development tooling

### Production Build
- Frontend: Vite build to static assets
- Backend: esbuild bundling to single Node.js file
- Assets served from Express static middleware
- Database schema deployed via migrations

### Environment Configuration
- DATABASE_URL for PostgreSQL connection
- SESSION_SECRET for secure session management
- NODE_ENV for environment-specific behavior
- Replit-specific environment detection

### Key Architectural Decisions

1. **Monorepo Structure**: Single repository with client, server, and shared code for easier development and deployment
2. **Type Safety**: Shared TypeScript types between frontend and backend using Drizzle schema
3. **Real-time Data**: Polling-based updates for crypto prices rather than WebSockets for simplicity
4. **Session-based Auth**: Chosen over JWT for better security in server-rendered context
5. **Time-based Trading**: Simulated trading with Cairo timezone logic for realistic Middle Eastern market feel
6. **Mobile-first Design**: Bottom navigation and responsive design optimized for mobile users
7. **Database Design**: Separate tables for different transaction types to maintain data integrity and enable complex queries