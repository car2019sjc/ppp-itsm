# IT Operations Dashboard - Technical Documentation

## Table of Contents
1. [Introduction](#introduction)
2. [Architecture Overview](#architecture-overview)
3. [Key Features](#key-features)
4. [Technology Stack](#technology-stack)
5. [Project Structure](#project-structure)
6. [Core Components](#core-components)
7. [Data Models](#data-models)
8. [Utility Functions](#utility-functions)
9. [Authentication](#authentication)
10. [Environment Configuration](#environment-configuration)
11. [Backup and Restore Functionality](#backup-and-restore-functionality)
12. [AI Integration](#ai-integration)
13. [Deployment Guidelines](#deployment-guidelines)
14. [Future Enhancements](#future-enhancements)

## Introduction

The IT Operations Dashboard is a comprehensive web application designed to visualize and analyze IT service management data, specifically focused on incidents and service requests. The application provides real-time insights into IT operations, helping teams monitor performance, identify trends, and make data-driven decisions.

The dashboard supports two primary data types:
- **Incidents**: Issues that disrupt normal service operations
- **Requests**: Service requests from users

## Architecture Overview

The application follows a modern React single-page application (SPA) architecture with the following key characteristics:

- **Component-Based Structure**: Modular components for reusability and maintainability
- **State Management**: React's built-in state management with hooks
- **Data Processing**: Client-side data processing and visualization
- **Responsive Design**: Mobile-first approach using Tailwind CSS
- **File-Based Data**: Excel file import for data analysis (no backend database)
- **AI Analysis**: Integration with OpenAI for advanced data insights

## Key Features

### Incident Management
- Incident tracking and visualization
- Priority-based analysis
- SLA compliance monitoring
- Category and subcategory analysis
- Assignment group performance metrics
- Historical trend analysis

### Request Management
- Request tracking and visualization
- Priority and category analysis
- SLA compliance monitoring
- Completion rate analysis
- User and location-based insights

### Advanced Analytics
- AI-powered predictive analysis
- Shift-based performance metrics
- Root cause identification
- Recommendation engine
- Impact analysis

### User Interface
- Dark mode interface
- Interactive charts and graphs
- Responsive design for all devices
- Filterable data views
- Detailed drill-down capabilities

## Technology Stack

### Frontend
- **React**: UI library (v18.3.1)
- **TypeScript**: Type-safe JavaScript
- **Vite**: Build tool and development server
- **Tailwind CSS**: Utility-first CSS framework
- **Recharts**: Chart visualization library
- **Lucide React**: Icon library
- **date-fns**: Date manipulation library
- **XLSX**: Excel file parsing

### Data Processing
- **Fuse.js**: Fuzzy search functionality
- **OpenAI API**: AI-powered analysis

### Development Tools
- **ESLint**: Code linting
- **TypeScript-ESLint**: TypeScript-specific linting
- **Autoprefixer**: CSS vendor prefixing
- **PostCSS**: CSS processing

## Project Structure

```
/
├── public/                  # Static assets
├── src/
│   ├── apps/                # Specialized application modules
│   │   ├── knowledge-base/  # Knowledge base application
│   │   └── request-dashboard/ # Request dashboard application
│   ├── components/          # Reusable UI components
│   │   ├── dev/             # Development-specific components
│   │   └── prod/            # Production-specific components
│   ├── config/              # Configuration files
│   ├── contexts/            # React contexts
│   ├── types/               # TypeScript type definitions
│   ├── utils/               # Utility functions
│   ├── App.tsx              # Main application component
│   ├── main.tsx             # Application entry point
│   └── index.css            # Global styles
├── scripts/                 # Utility scripts
├── backups/                 # Backup storage
├── .env.development         # Development environment variables
├── .env.production          # Production environment variables
├── backup.js                # Backup functionality
├── eslint.config.js         # ESLint configuration
├── index.html               # HTML entry point
├── package.json             # Project dependencies and scripts
├── postcss.config.js        # PostCSS configuration
├── tailwind.config.js       # Tailwind CSS configuration
├── tsconfig.json            # TypeScript configuration
├── tsconfig.app.json        # App-specific TypeScript configuration
├── tsconfig.node.json       # Node-specific TypeScript configuration
└── vite.config.ts           # Vite configuration
```

## Core Components

### Main Dashboard Components

#### `App.tsx`
The main application component that serves as the container for the incident dashboard. It manages the global state, handles data loading, and orchestrates the rendering of various dashboard components.

Key responsibilities:
- User authentication state management
- Incident and request data management
- Filter state management
- Component visibility control

#### `RequestDashboard.tsx`
A specialized dashboard for visualizing and analyzing service requests. Similar to the main dashboard but focused on request-specific metrics and visualizations.

#### `DashboardHeader.tsx`
The application header component that displays the title, environment information, and user controls.

#### `SearchBar.tsx`
A comprehensive search and filter component that allows users to find specific incidents or requests based on various criteria.

### Data Visualization Components

#### Analysis Components
- `CategoryAnalysis.tsx`: Analyzes incidents by category and priority
- `SoftwareAnalysis.tsx`: Specialized analysis for software-related incidents
- `HardwareAnalysis.tsx`: Specialized analysis for hardware-related incidents
- `GroupAnalysis.tsx`: Analyzes incidents by assignment group
- `SLAAnalysis.tsx`: Analyzes SLA compliance
- `UserAnalysis.tsx`: Analyzes incidents by user
- `LocationAnalysis.tsx`: Analyzes incidents by location
- `AnalystAnalysis.tsx`: Analyzes incidents by assigned analyst
- `ShiftHistoryAnalysis.tsx`: Analyzes incidents by work shift

#### Historical Analysis Components
- `GroupHistoryAnalysis.tsx`: Historical analysis by assignment group
- `CategoryHistoryAnalysis.tsx`: Historical analysis by category
- `SLAHistoryAnalysis.tsx`: Historical analysis of SLA compliance
- `HistoricalDataAnalysis.tsx`: Comprehensive historical data analysis

#### AI-Powered Components
- `AIAnalyst.tsx`: AI-powered incident analysis
- `AIPredictiveAnalysis.tsx`: AI-powered predictive analysis for requests

### UI Components

#### `StatsCard.tsx`
Displays key metrics in a card format with optional trend indicators.

#### `CategoryCard.tsx`
Interactive card component for selecting different analysis views.

#### `IncidentDetails.tsx`
Modal component for displaying detailed information about a specific incident.

#### `PriorityAlert.tsx`
Alert component for highlighting high-priority incidents.

#### `FileUpload.tsx`
Component for uploading and processing Excel files containing incident or request data.

#### `FileUploadSelector.tsx`
Component for selecting the type of data to upload (incidents or requests).

## Data Models

### Incident Model
```typescript
export interface Incident {
  Number: string;
  Opened: string;
  ShortDescription: string;
  Caller: string;
  Priority: string;
  State: string;
  Category: string;
  Subcategory: string;
  AssignmentGroup: string;
  AssignedTo: string;
  Updated: string;
  UpdatedBy: string;
  BusinessImpact: string;
  ResponseTime: string;
  Location?: string;
  CommentsAndWorkNotes?: string;
}
```

### Request Model
```typescript
export interface Request {
  Number: string;
  Opened: string;
  ShortDescription: string;
  RequestItem: string;
  RequestedForName: string;
  Priority: string;
  State: string;
  AssignmentGroup: string;
  AssignedTo: string;
  Updated: string;
  UpdatedBy: string;
  CommentsAndWorkNotes: string;
  BusinessImpact: string;
}
```

### Analyst Model
```typescript
export interface Analyst {
  name: string;
  level: string;
  startTime: string;
  endTime: string;
  schedule: string;
  location?: string;
}
```

### Historical Data Model
```typescript
export interface HistoricalData {
  month: string; // Format: YYYY-MM
  incidents: {
    total: number;
    byPriority: Record<string, number>;
    byCategory: Record<string, number>;
    byState: Record<string, number>;
    slaCompliance: {
      withinSLA: number;
      outsideSLA: number;
      percentage: number;
    };
  };
  requests: {
    total: number;
    byPriority: Record<string, number>;
    byStatus: Record<string, number>;
    byCategory: Record<string, number>;
    completionRate: number;
  };
}
```

## Utility Functions

### Incident Utilities (`incidentUtils.ts`)

Key functions:
- `getIncidentState(state: string)`: Normalizes incident state values
- `isHighPriority(priority: string)`: Determines if an incident is high priority
- `isCancelled(state: string)`: Checks if an incident is cancelled
- `isActiveIncident(state: string)`: Checks if an incident is active
- `normalizePriority(priority: string)`: Normalizes priority values

### Shift Utilities (`shiftUtils.ts`)

Key functions:
- `getShiftFromTime(dateStr: string)`: Determines the work shift based on time
- `getShiftName(shift: string)`: Gets the display name for a shift
- `getShiftTimes(shift: string)`: Gets the start and end times for a shift

## Authentication

The application uses a simple username/password authentication system:

- Development credentials: Username: `Onset-ISRA`, Password: `Socorro01@`
- Production credentials: Same as development

Authentication is managed through the `AuthContext` which provides:
- `isAuthenticated`: Boolean indicating authentication status
- `login()`: Function to authenticate the user
- `logout()`: Function to log out the user

## Environment Configuration

The application uses environment variables to configure different environments:

### Development Environment (`.env.development`)
```
VITE_APP_ENV=development
VITE_APP_TITLE="IT Operations Dashboard (Development)"
VITE_OPENAI_API_KEY=YOUR_API_KEY_HERE
```

### Production Environment (`.env.production`)
```
VITE_APP_ENV=production
VITE_APP_TITLE="IT Operations Dashboard"
VITE_OPENAI_API_KEY=YOUR_API_KEY_HERE
```

## Backup and Restore Functionality

The application includes a robust backup and restore system for preserving application data.

### Backup Functionality (`backup.js`)
- Creates versioned ZIP archives of the application
- Includes all source code, configuration files, and assets
- Automatically increments version numbers
- Timestamps backups for easy identification

### Restore Functionality (`scripts/restore.js`)
- Allows restoring from any previous backup
- Validates backup integrity before restoration
- Preserves current files when needed
- Provides detailed error handling

## AI Integration

The application integrates with OpenAI's API to provide advanced analytics and insights.

### AI Analyst Component (`AIAnalyst.tsx`)
- Analyzes incident patterns and trends
- Identifies root causes
- Provides actionable recommendations
- Calculates confidence metrics
- Performs shift-based analysis

### AI Predictive Analysis Component (`AIPredictiveAnalysis.tsx`)
- Similar functionality but focused on request data
- Predicts future trends
- Identifies potential issues before they occur
- Suggests process improvements

## Deployment Guidelines

### Development Environment
```bash
# Start development server
npm run dev

# Build for development
npm run build:dev

# Preview development build
npm run preview
```

### Production Environment
```bash
# Start production-like server locally
npm run dev:prod

# Build for production
npm run build

# Create backup before deployment
npm run backup
```

### Backup and Restore
```bash
# Create backup
npm run backup

# List available backups
npm run restore

# Restore from specific backup
npm run restore backup-v1-2025-03-29T12-43-46.zip
```

## Future Enhancements

### Potential Improvements
1. **Backend Integration**: Add a backend server for persistent data storage
2. **User Management**: Implement multi-user support with role-based access control
3. **Real-time Updates**: Add WebSocket support for real-time data updates
4. **Advanced Filtering**: Enhance search and filter capabilities
5. **Export Functionality**: Add PDF and Excel export options for reports
6. **Mobile App**: Develop a companion mobile application
7. **Notification System**: Implement alerts for critical incidents
8. **Integration with ITSM Tools**: Direct integration with ServiceNow, Jira, etc.
9. **Custom Dashboards**: Allow users to create personalized dashboard views
10. **Automated Reporting**: Scheduled report generation and distribution

## Appendix: Component Dependencies

### Main Dashboard Dependencies
- React
- Recharts
- date-fns
- Lucide React
- OpenAI API

### Data Processing Dependencies
- XLSX
- Fuse.js

### UI Dependencies
- Tailwind CSS
- React Dropzone

### Development Dependencies
- TypeScript
- Vite
- ESLint
- PostCSS
- Autoprefixer