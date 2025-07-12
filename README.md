# Arquebuse Controller Core

A .NET 8 Minimal API service that manages client subscriptions, queries Active Directory via LDAP, persists data in SQLite, and dispatches notifications through WNS.

## Goals

- Secure client registration/unregistration
- AD‑driven targeting
- Scalable persistence
- Reliable WNS delivery

## Architecture

- **ASP.NET Core Minimal API** over HTTPS (Kestrel)
- **LDAP** for AD interactions (`System.DirectoryServices`)
- **SQLite** for subscription storage
- **WNS HTTP calls** using app credentials
- JSON audit logging

## Technologies

- .NET 8, Kestrel, System.DirectoryServices, Microsoft.Data.Sqlite, Dapper or EF Core

## Example Usage

```bash
docker-compose up -d   # start controller-core and SQLite
```

```powershell
# Register a client
Invoke-RestMethod -Uri https://localhost:5001/register -Method Post -Body $clientInfo -UseBasicParsing
```

```powershell
# Send a notification
Invoke-RestMethod -Uri https://localhost:5001/notify -Method Post -Body @{ filters=@{ group='IT' }; message='App X is down' }
```
