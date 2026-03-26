# HomeSight

HomeSight is a lightweight web HMI template for Beckhoff TwinCAT systems, built with Blazor Server and MudBlazor. It is designed as a practical alternative to proprietary HMI stacks by using familiar .NET tooling, a clean web UI model, and a backend that keeps PLC communication centralized and predictable.

## Why HomeSight

- Open stack built on C#, ASP.NET Core, Blazor Server, MudBlazor, and TwinCAT ADS.
- Centralized PLC access so multiple clients can observe and interact without each session creating its own direct PLC traffic.
- Flexible frontend pages that keep machine-specific behavior in the UI where it is easier to evolve.
- Extensible deployment model with support for companion services such as Grafana, Node-RED, and other tools behind a shared reverse proxy.

## Core Approach

HomeSight keeps the backend generic and reusable while allowing each machine or station to define its own screens and behavior. The template focuses on a few core ideas:

- PLC symbols are discovered from TwinCAT metadata and mapped into .NET-friendly types.
- A polling cache continuously refreshes the latest values so the UI reads from application state instead of talking to the PLC directly.
- Write requests are funneled through the backend to keep PLC access consistent and controlled.
- Authentication and role checks are built in so both pages and proxied services can share the same access rules.

## Architecture

### TwinCAT integration

The PLC remains the source of truth for exposed HMI variables. HomeSight discovers configured symbols, maps them into application models, and reads them through a centralized service layer.

### Cache-first communication

Rather than letting each browser session query the PLC directly, the backend maintains an in-memory cache of current values. This reduces repeated traffic, simplifies client behavior, and creates a single point for validation and write orchestration.

### Blazor UI

Machine-specific screens live in Blazor components. This keeps layout, interaction flow, and presentation logic easy to customize without rewriting lower-level communication plumbing.

### Integrated access control

The included authentication system supports role-based access to application pages, machine features, and YARP-proxied services, making it easier to present a single secured entry point.

## Included capabilities

- Blazor Server UI shell
- MudBlazor-based component styling
- TwinCAT PLC read and write services
- In-memory PLC cache layer
- Built-in authentication and user management
- Optional historical data support through DumbTs
- Docker Compose setup for local service orchestration
- Reverse proxy support for adjacent tools and dashboards

## Repository layout

- `src/HomeSight.Template` contains the main web application template and Docker Compose setup.
- `src/HomeSight.TestPlc` contains a sample TwinCAT PLC project for local development and testing.

## Getting started

1. Open `src/HomeSight.Template/HomeSight.Template.sln`.
2. Review the appsettings files to choose the feature set you want to run, such as TwinCAT, YARP, DumbAuth, or DumbTs.
3. Configure PLC connectivity and any machine-specific symbols or cache settings.
4. Run the Blazor application locally and verify PLC reads, writes, and authentication behavior.
5. Customize the pages in `Components/Pages` to build the machine-facing UI.

## Next improvements

- Add a concrete setup guide for TwinCAT connectivity.
- Document the symbol attribute conventions used for discovery.
- Add screenshots or a short demo walkthrough.
- Include deployment notes for Docker and reverse-proxied companion services.

## License

This project is released under the MIT License. See [LICENSE](LICENSE) for details.
