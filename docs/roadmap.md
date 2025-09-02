# Roadmap

## Phase 1 — Boot
- [x] Create initial project structure
- [ ] Setup Docker Compose (Postgres + RabbitMQ)

## Phase 2 — Core
- [ ] API: POST /orders (persist to DB)
- [ ] API: PUT /orders/{id}/status (update order status)

## Phase 3 — Messaging
- [ ] Add MassTransit + Outbox pattern
- [ ] Define event contracts (OrderCreated, OrderStatusChanged)
- [ ] Publish events from API (Bus Outbox)
- [ ] Worker consumes events (Consumer Outbox, logs first)

## Phase 4 — Notifications
- [ ] Add SignalR hub + demo page
- [ ] Register Firebase device token
- [ ] Push notifications via Firebase

## Phase 5 — Documentation
- [ ] Initial documentation in `README.md`
- [ ] ADR-0001 Monorepo First
- [ ] ADR-0002 Outbox with MassTransit

---

## Future Enhancements
- Dead Letter Queue + reprocess endpoint
- Observability with OpenTelemetry (traces + metrics)
- AsyncAPI for event contracts
- Saga orchestration (inventory/payment/shipping)
- Kubernetes deployment (probes, scaling)
