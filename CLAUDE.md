# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Tunez is a Phoenix LiveView application built with the Ash Framework for the upcoming Ash Framework book. It's a music management application that demonstrates Ash's capabilities for building Phoenix applications with domain-driven design patterns.

## Key Technologies

- **Elixir/Phoenix**: Web framework with LiveView for real-time UI
- **Ash Framework**: Resource and domain management framework
- **Ash Postgres**: PostgreSQL data layer integration
- **Phoenix LiveView**: Real-time, server-rendered HTML
- **Tailwind CSS**: Utility-first CSS framework
- **esbuild**: JavaScript bundler
- **Bandit**: HTTP server adapter

## Development Commands

### Setup and Installation
```bash
# Initial setup - installs dependencies and sets up database
mix setup

# Alternative setup commands
mix deps.get
mix ash.setup
mix assets.setup
mix assets.build
```

### Running the Application
```bash
# Start the Phoenix server
mix phx.server

# Start with IEx (Interactive Elixir)
iex -S mix phx.server
```

### Database Management
```bash
# Run Ash setup (preferred for this project)
mix ash.setup

# Traditional Ecto commands (if needed)
mix ecto.create
mix ecto.migrate
mix ecto.reset
```

### Asset Management
```bash
# Setup assets (install Tailwind and esbuild if missing)
mix assets.setup

# Build assets for development
mix assets.build

# Build and minify assets for production
mix assets.deploy
```

### Testing
```bash
# Run tests (includes ash.setup --quiet)
mix test
```

### Code Formatting
```bash
# Format code according to .formatter.exs
mix format
```

### Seeding Data
```bash
# Run main seeds file
mix run priv/repo/seeds.exs

# Individual seed files are available in priv/repo/seeds/
```

## Architecture

### Domain Structure
- **lib/tunez/**: Core domain logic and contexts
- **lib/tunez_web/**: Phoenix web layer (controllers, live views, components)
- **lib/tunez_web/live/**: LiveView modules organized by domain (artists, albums)
- **priv/repo/**: Database migrations and seed files

### Ash Framework Integration
- Uses Ash Resources for domain modeling
- Ash Domains for organizing related resources
- Ash.Postgres for PostgreSQL data layer
- Custom Ash configurations in config/config.exs

### Phoenix Structure
- **Router**: Standard Phoenix router with LiveView routes (lib/tunez_web/router.ex)
- **LiveViews**: Organized by domain (artists, albums) in lib/tunez_web/live/
- **Components**: Core UI components in lib/tunez_web/components/
- **Layouts**: Application layouts in lib/tunez_web/components/layouts.ex

### Configuration
- **config/**: Environment-specific configurations
- **Ash config**: Extensive Ash framework configuration in config/config.exs
- **Assets**: esbuild and Tailwind configurations
- **Database**: PostgreSQL with Ash.Postgres integration

## Key Files and Patterns

### Application Structure
- `lib/tunez/application.ex`: OTP application supervision tree
- `lib/tunez.ex`: Main application module and domain contexts
- `lib/tunez_web.ex`: Web application structure and imports

### Database and Migrations
- Uses standard Phoenix/Ecto migrations in `priv/repo/migrations/`
- Seed files organized in `priv/repo/seeds/` by domain

### LiveView Organization
- Domain-based organization (artists, albums)
- Standard Phoenix LiveView patterns (index, show, form)
- Component-based UI with core_components.ex

### Asset Pipeline
- Tailwind CSS for styling
- esbuild for JavaScript bundling
- Assets located in `assets/` directory

## Development Workflow

1. Use `mix setup` for initial project setup
2. Start development server with `mix phx.server`
3. Access application at http://localhost:4000
4. Use `mix format` to format code before committing
5. Run `mix test` before pushing changes
6. Use Phoenix LiveDashboard at http://localhost:4000/dev/dashboard (in development)

## Important Notes

- This project uses Ash Framework patterns, not traditional Phoenix contexts
- Database operations should use Ash actions rather than direct Ecto queries
- LiveView is the primary UI pattern - avoid traditional controllers where possible
- Assets are automatically watched and rebuilt in development mode
- The application includes Phoenix LiveDashboard for monitoring in development