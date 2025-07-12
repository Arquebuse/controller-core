# Prompts used for project creation and implementation

## Blueprint creation (ChatGPT o4-mini-high + Deep reaserch)

You are a senior Windows architect and .NET developer. 

You work on the Arquebuse project: An open‑source notification system delivering secure, targeted Windows alerts with enterprise‑focused simplicity. This project is based on 3 distinct modules:
- **Desktop‑App**: Windows service that registers with WNS, receives and displays notifications.
- **Controller‑Core**: .NET 8 Minimal API managing client registrations, AD queries, and sending WNS notifications (uses SQLite).
- **Controller‑CLI**: PowerShell Core module to manage subscriptions and send notifications via Controller‑Core.

I need an MVP blueprint for the **Arquebuse Controller-Core** module that:

- Exposes HTTPS endpoints for client registration/unregistration and notification dispatch
- Authenticates callers via Active Directory (LDAP bind)  
- Queries Active Directory groups/users to resolve filters  
- Persists subscriptions in SQLite  
- Sends notifications to WNS using app credentials & authenticated HTTPS  
- Produces JSON audit logs (one object per line)

Please produce, in concise bullet points:

1. **High-Level Architecture Diagram** describing:
   - How clients (Desktop-App) register/unregister  
   - How the CLI module triggers notifications  
   - How WNS is invoked  
2. **Folder/project structure** for a .NET 8 Minimal API solution, including Database and Logging folders.
3. **Key class/function sketches** (pseudo-code) for:
   - LDAP authentication & query service  
   - Subscription repository (SQLite)  
   - Notification controller (REST methods)  
   - WNS client helper (OAuth2 + POST)  
4. **Sample configuration snippets**:
   - appsettings.json (LDAP connection, SQLite path, WNS credentials, TLS cert settings)  
   - Dockerfile + docker-compose.yml for local Windows container with SQLite  
5. **Step-by-step setup instructions** for a beginner:
   - Generating/trusting a self-signed certificate for Kestrel  
   - Seeding a mock LDAP (AD LDS or OpenLDAP container)  
   - Running migrations and starting the service  
6. **Best practices** references:
   - .NET 8 Minimal API HTTPS hardening  
   - LDAP querying patterns (`System.DirectoryServices`)  
   - Secure handling of WNS credentials  
7. Explain exactly **how this Controller-Core will integrate** with:
   - The **Desktop-App** (registration endpoints, polling pattern)  
   - The **Controller-CLI** (API routes consumed by PowerShell cmdlets)

Use the readme.md in the arquebuse/desktop-app github repository to get more information about this module.

Finally if you need clarification on AD schema, SQLite migration tooling, or certificate formats, please ask me.