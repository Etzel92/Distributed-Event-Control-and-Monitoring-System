# Distributed Event Control and Monitoring System

A distributed real-time event control and monitoring system with a .NET API, WinForms client, React dashboard, SignalR messaging, and centralized event logging.

This solution connects a web-based administrative interface with multiple desktop clients, allowing remote command execution, real-time communication, and centralized event tracking across the system.

> **Repository scope**: real-time command dispatching, event logging, centralized monitoring, REST API endpoints, SignalR-based communication, desktop client actions, and web-based event visualization.

---

## Contents

- [Overview](#overview)
- [System Architecture](#system-architecture)
- [Components](#components)
- [Key Features](#key-features)
- [Tech Stack](#tech-stack)
- [Typical Workflow](#typical-workflow)
- [Requirements](#requirements)
- [Configuration](#configuration)
- [How to Run](#how-to-run)
- [Common Use Cases](#common-use-cases)
- [Notes](#notes)

---

## Overview

**Distributed Event Control and Monitoring System** is a multi-component solution designed to control and monitor client-side activity in real time.

The system is composed of three main parts:

- a **React web interface** for administration and monitoring
- an **ASP.NET Core API** with REST endpoints and a SignalR hub
- a **Windows Forms client application** that receives remote commands and logs activity

The goal of the system is to provide centralized control over multiple desktop clients while keeping a traceable event log in a SQL Server database.

---

## System Architecture

The solution follows a distributed three-part architecture:

```text
[React Admin UI] ⇄ [ASP.NET Core API + SignalR Hub] ⇄ [WinForms Client]
```

### High-level flow

- The administrator interacts with the web UI
- The API exposes REST endpoints and real-time communication through SignalR
- The WinForms client listens for commands from the backend
- Client actions are logged into SQL Server
- The web interface can query and visualize the centralized event log

This allows the system to combine:

- remote client control
- real-time messaging
- centralized persistence
- monitoring and audit visibility

---

## Components

### EventControl.UI
React-based administrative interface used to:

- send remote commands
- monitor client activity
- review centralized logs
- edit log comments where supported

### EventControl.API
ASP.NET Core backend responsible for:

- exposing REST endpoints
- hosting the SignalR hub
- coordinating communication between components
- persisting and retrieving event data from SQL Server

### EventClient.App
Windows Forms desktop application that:

- receives remote commands
- opens or closes forms depending on incoming instructions
- records activity triggered manually or remotely
- communicates back through the centralized system

### SQL Server
Database layer used for:

- event persistence
- traceability and auditing
- stored procedure-driven event registration
- centralized event history queries

---

## Key Features

- Real-time communication between web UI, API, and desktop clients
- Remote command execution through SignalR
- Centralized event logging in SQL Server
- Traceable event records with time, source, type, and machine context
- Editable comments in the event log from the web interface
- Modular architecture with independently runnable components
- Distributed interaction between web, backend, and desktop application
- Event visualization through a centralized dashboard

---

## Tech Stack

### Frontend
- React
- Vite
- JavaScript
- SignalR Client

### Backend
- ASP.NET Core
- Entity Framework Core
- SignalR

### Desktop Client
- WinForms (.NET 8)
- SignalR Client

### Database
- SQL Server
- Stored procedures

---

## Typical Workflow

A typical interaction in the system looks like this:

1. The administrator opens the React dashboard
2. A command is sent from the UI to the ASP.NET Core backend
3. The backend forwards the instruction through SignalR
4. A connected WinForms client receives the command
5. The client performs the requested action
6. The event is registered in SQL Server
7. The web dashboard displays the recorded event in the centralized log

This flow allows both operational control and event traceability in a single system.

---

## Requirements

- .NET 8 SDK
- Node.js 18+
- npm
- SQL Server
- Visual Studio or a compatible .NET development environment

---

## Configuration

Before running the system, make sure each component is configured correctly.

### Backend configuration
Update the API configuration with:

- SQL Server connection string
- SignalR-related settings if needed
- local development URLs

Typical file:
```text
appsettings.json
```

### Frontend configuration
Make sure the web UI points to the correct backend/API URL and SignalR hub URL.

### Desktop client configuration
Make sure the WinForms client points to the correct backend or hub endpoint.

> Keep local URLs aligned across all components during development.

---

## How to Run

### 1. Clone the repositories

```bash
git clone https://github.com/your-username/EventControl.UI.git
git clone https://github.com/your-username/EventControl.API.git
git clone https://github.com/your-username/EventClient.App.git
```

### 2. Run the backend

- Open `EventControl.API`
- Configure `appsettings.json`
- Restore packages
- Run the API from Visual Studio or CLI

Example:

```bash
dotnet restore
dotnet run
```

### 3. Run the desktop client

- Open the WinForms solution
- Build the project
- Run the main client application

### 4. Run the web UI

```bash
cd EventControl.UI
npm install
npm run dev
```

### 5. Verify connectivity

Make sure:

- the API is running
- the SignalR hub is reachable
- the client is connected
- the web UI uses the correct backend URL

---

## Common Use Cases

- An administrator needs to remotely open a form on a specific client machine
- The system must register when a client form was opened or closed
- A team needs to audit client-side activity from a centralized web interface
- Operators need a shared real-time view of distributed event activity
- Comments must be added to log entries for operational follow-up

---

## Notes

- SignalR is the core mechanism used for real-time interaction between components.
- SQL Server provides the persistence layer for event traceability.
