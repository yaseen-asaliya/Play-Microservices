# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a .NET 6 microservices solution in early development. Currently contains one service: **Play.Catalog**, a catalog microservice built with ASP.NET Core Web API.

## Build & Run Commands

All commands assume the `dotnet` CLI is available. Run from the relevant project directory or the solution root.

```bash
# Build entire solution
dotnet build

# Run the catalog service (from Play.Catalog/src/Play.Catalog.Service/)
dotnet run

# Run with explicit project path (from repo root)
dotnet run --project Play.Catalog/src/Play.Catalog.Service/Play.Catalog.Service.csproj
```

The service starts on:
- HTTPS: `https://localhost:7002`
- HTTP: `http://localhost:5042`
- Swagger UI: `https://localhost:7002/swagger`

## Solution Structure

```
dotnet-microservices.sln          # Root solution (references service solutions)
Play.Catalog/
  Play.Catalog.sln                # Service-level solution
  src/
    Play.Catalog.Service/         # ASP.NET Core Web API service
      Controllers/                # API controllers
      appsettings.json            # Base configuration
      appsettings.Development.json
      Program.cs                  # App startup/middleware configuration
```

## Architecture & Conventions

- **Framework:** .NET 6, ASP.NET Core Web API with controller-based routing
- **API style:** `[ApiController]` + `[Route]` attributes; file-scoped namespaces
- **API docs:** Swagger/OpenAPI via Swashbuckle, enabled in all environments
- **Config:** Environment-specific `appsettings.{Environment}.json` files
- **Nullable:** `<Nullable>enable</Nullable>` is set — all reference types require null handling
- **Implicit usings:** Enabled; no need to manually add common `using` directives

## Key Files

- [Play.Catalog.Service.csproj](Play.Catalog/src/Play.Catalog.Service/Play.Catalog.Service.csproj) — dependencies and target framework
- [Program.cs](Play.Catalog/src/Play.Catalog.Service/Program.cs) — middleware pipeline and service registration
- [Properties/launchSettings.json](Play.Catalog/src/Play.Catalog.Service/Properties/launchSettings.json) — dev server ports and profiles
