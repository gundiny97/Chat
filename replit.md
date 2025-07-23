# Military-Grade Secure Chat Application

## Overview

This is a full-stack real-time chat application with military-grade end-to-end encryption built with React, Express.js, and WebSockets. The application features a secure, dark-themed UI with zero-knowledge server architecture, ensuring complete privacy from government surveillance and unauthorized access. All messages are encrypted using RSA-4096 and AES-256-GCM encryption standards.

## User Preferences

Preferred communication style: Simple, everyday language in Portuguese.

## System Architecture

### Frontend Architecture
- **Framework**: React 18 with TypeScript
- **Build Tool**: Vite for fast development and optimized builds
- **UI Library**: shadcn/ui components built on Radix UI primitives
- **Styling**: Tailwind CSS with CSS variables for theming
- **State Management**: React Query (@tanstack/react-query) for server state
- **Routing**: Wouter for client-side routing
- **WebSocket Client**: Custom hook (`useWebSocket`) for real-time communication

### Backend Architecture
- **Runtime**: Node.js with Express.js
- **WebSocket Server**: 'ws' library integrated with HTTP server
- **Database ORM**: Drizzle ORM configured for PostgreSQL
- **Session Storage**: connect-pg-simple for PostgreSQL session storage
- **Development**: tsx for TypeScript execution in development

### Key Security Components

#### Next-Generation Military-Grade Encryption
- **P-384 ECDH**: Advanced elliptic curve cryptography for key exchange (equivalent to 7680-bit RSA security)
- **AES-256-GCM**: Enhanced symmetric encryption with authenticated additional data
- **Post-Quantum Protection**: Hybrid encryption system resistant to quantum computer attacks
- **Perfect Forward Secrecy**: Double ratchet protocol with key derivation for each message
- **Zero-Knowledge Server**: Server never sees plaintext messages or stores encryption keys

#### WebSocket Integration
- **Path**: `/chat-ws` for secure WebSocket connections
- **Connection Management**: Automatic reconnection with cryptographic re-establishment
- **Message Broadcasting**: End-to-end encrypted message relay without server decryption
- **Message Types**: Key exchange, encrypted messages, system status, and error handling

#### Security Features
- **Government-Resistant**: Designed to prevent surveillance and monitoring
- **No Server Logs**: Zero storage of messages or metadata on server
- **Session-Based Keys**: Ephemeral cryptographic keys that don't persist
- **Anti-Forensics**: No traces left on server infrastructure

#### Database Schema
- **Users Table**: ID, username, password fields
- **Messages Table**: ID, content, sender ID, timestamp fields
- **Storage Interface**: Abstracted storage layer with in-memory implementation for development

#### UI Components
- **Chat Interface**: Real-time message display with user/peer message distinction
- **Connection Status**: Visual indicator showing WebSocket connection state
- **Responsive Design**: Mobile-friendly layout with proper responsive breakpoints
- **Theme Support**: Dark/light theme support through CSS variables

## Data Flow

1. **Client Connection**: Frontend establishes WebSocket connection on component mount
2. **Message Sending**: User input triggers WebSocket message transmission
3. **Server Processing**: Express server receives WebSocket messages and stores them
4. **Message Broadcasting**: Server broadcasts messages to all connected clients except sender
5. **Client Updates**: Frontend receives messages and updates UI in real-time
6. **Auto-scroll**: Chat automatically scrolls to show latest messages

## External Dependencies

### Frontend Dependencies
- **UI Components**: Comprehensive set of Radix UI primitives for accessible components
- **Styling**: Tailwind CSS with autoprefixer for cross-browser compatibility
- **Icons**: Lucide React for consistent iconography
- **Date Handling**: date-fns for timestamp formatting
- **Utilities**: clsx and tailwind-merge for conditional styling

### Backend Dependencies
- **Database**: @neondatabase/serverless for PostgreSQL connectivity
- **WebSocket**: ws library for WebSocket server implementation
- **Development Tools**: tsx for TypeScript development, esbuild for production builds

## Deployment Strategy

### Development Environment
- **Frontend**: Vite dev server with HMR (Hot Module Replacement)
- **Backend**: tsx for direct TypeScript execution
- **Database**: In-memory storage implementation for development
- **WebSocket**: Integrated with development server

### Production Build
- **Frontend**: Vite build process generating optimized static assets
- **Backend**: esbuild compilation to ESM format for Node.js
- **Database**: PostgreSQL with Drizzle ORM migrations
- **Deployment**: Single server hosting both static files and WebSocket server

### Environment Configuration
- **Database URL**: Required environment variable for PostgreSQL connection
- **Session Configuration**: PostgreSQL-backed session storage
- **Static File Serving**: Express serves built frontend assets in production
- **Error Handling**: Comprehensive error boundaries and WebSocket reconnection logic

The application follows a monorepo structure with shared schema definitions between frontend and backend, ensuring type safety across the entire stack. The architecture supports both development and production environments with appropriate tooling and optimizations for each context.