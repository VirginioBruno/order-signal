# Order Signal

<!-- Badges -->
![.NET 8](https://img.shields.io/badge/.NET-8.0-512BD4?logo=dotnet&logoColor=white)
![MassTransit](https://img.shields.io/badge/MassTransit-8.x-0FA9A7)
![RabbitMQ](https://img.shields.io/badge/RabbitMQ-3.x-FF6600?logo=rabbitmq&logoColor=white)
![PostgreSQL](https://img.shields.io/badge/Postgres-16-336791?logo=postgresql&logoColor=white)
![SignalR](https://img.shields.io/badge/SignalR-realtime-2C3E50)
![Firebase](https://img.shields.io/badge/Firebase-Cloud%20Messaging-FFCA28?logo=firebase&logoColor=black)

**Order Signal** is a showcase project demonstrating a modern event-driven backend in **.NET 8**.  
Scope of the MVP: create an order, update its status, publish an event, process it in a worker, and notify the user in real time (SignalR + Firebase).

> This is a study/portfolio project, not a production system.


## Tech Stack (MVP)
- .NET 8 (ASP.NET Core, Background services)
- MassTransit + RabbitMQ (event-driven, outbox)
- EF Core + PostgreSQL (persistence) — provider TBD in the MVP
- SignalR (real-time updates), Firebase Cloud Messaging (push)
- Testing: xUnit (unit), Testcontainers (integration) — later


## Repository Structure

```text
order-signal/
├─ src/
│  ├─ OrderSignal.Api/
│  │  ├─ OrderSignal.Api.csproj
│  │  ├─ Program.cs
│  │  └─ (Controllers/, Hubs/, etc.)
│  ├─ OrderSignal.Worker/
│  │  ├─ OrderSignal.Worker.csproj
│  │  └─ Program.cs
│  └─ OrderSignal.Contracts/
│     └─ OrderSignal.Contracts.csproj
├─ tests/
│  └─ OrderSignal.Unit/
│     └─ OrderSignal.Unit.csproj
├─ docs/
│  ├─ roadmap.md
│  └─ adr/
├─ .gitignore
├─ .env
├─ docker-compose.yml
├─ order-signal.sln
└─ README.md
```

## Current Status
- ✅ Repo scaffold created
- 🚧 Implementing MVP (see [docs/roadmap.md](./docs/roadmap.md))
- ⏭️ Next: add MassTransit + Outbox, publish events from API, basic consumer

➡️ Project board: [Order Signal showcase](https://github.com/users/VirginioBruno/projects/4)

## Quickstart (WIP)
For now, run the projects locally:

```bash
# Dependencies
docker-compose up -d

# API
dotnet run --project src/OrderSignal.Api/OrderSignal.Api.csproj

# Worker
dotnet run --project src/OrderSignal.Worker/OrderSignal.Worker.csproj

```

- RabbitMQ UI → [http://localhost:15672](http://localhost:15672) (user: `guest`, pass: `guest`)  
- Postgres → `localhost:5432` (db/user/password: `orders`)  

- Connection string used by API/Worker:

```json
{
    "ConnectionStrings": {
        "OrdersDb": "Host=postgres;Port=5432;Database=orders;Username=orders;Password=orders"
    }
}
```

## Architecture (high level)

```mermaid
flowchart LR
    A[API Create/Update Order] -->|publish event| B[(Outbox/Bus)]
    B --> C([RabbitMQ])
    C --> D[Worker - Consumer]
    D --> E[SignalR Hub]
    D --> F[Firebase Push]
    E & F --> G[User]
```
---

## Events (planned)

- `OrderCreated { OrderId, UserId, OccurredAt }`
- `OrderStatusChanged { OrderId, UserId, Status, OccurredAt }`

**Headers (planned):**
- `correlationId`
- `causationId`
- `eventType`
- `eventVersion`

---

## Roadmap

- [x] Setup Docker Compose (Postgres + RabbitMQ) — [#3](https://github.com/VirginioBruno/order-signal/issues/3)
- [ ] Implement API routes: create/update orders — [#2](https://github.com/VirginioBruno/order-signal/issues/2), [#6](https://github.com/VirginioBruno/order-signal/issues/6)
- [ ] Add MassTransit with Outbox pattern — [#4](https://github.com/VirginioBruno/order-signal/issues/4)
- [ ] Worker consumes events and logs — [#5](https://github.com/VirginioBruno/order-signal/issues/5)
- [ ] Add SignalR hub + demo page — [#8](https://github.com/VirginioBruno/order-signal/issues/8)
- [ ] Register device token endpoint — [#9](https://github.com/VirginioBruno/order-signal/issues/9)
- [ ] Firebase push notifications — [#7](https://github.com/VirginioBruno/order-signal/issues/7)
- [ ] Initial documentation — [#10](https://github.com/VirginioBruno/order-signal/issues/10)

➡️ More details in [docs/roadmap.md](./docs/roadmap.md).