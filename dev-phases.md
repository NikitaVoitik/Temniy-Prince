# Development Phases

## MVP (dia-mvp.png)

MangaApp only, 5 core services, direct S3, no optimization.

## Phase I: Launch (dia.png)

Add to MVP:

- AnimeApp, NovelApp
- Search Service + Elasticsearch
- Notification Service
- CDN + Redis Cache
- Compression Jobs + Queue

**Build order:** Cache → CDN → Search → Notifications → Jobs → Apps (parallel)

---

## Team Distribution

### MVP (6-8 devs) - 2 Feature Squads

```
Team 1: Core Backend (3-4 devs)
├── Auth Service (JWT)
├── User Service (Accounts DB)
├── API Gateway
└── Content DB Schema

Team 2: Product & Experience (3-4 devs)
├── MangaApp Frontend (Web)
├── Media Service (Direct S3)
└── Social (Comments)
```

### Phase I (10-14 devs) - 3 Specialized Layers

```
Team 1: Frontend Federation (4-5 devs)
├── MangaApp, AnimeApp, NovelApp
├── BFF pattern
└── Cross-app navigation

Team 2: Platform & Infrastructure (3-4 devs)
├── Search Service (Elasticsearch)
├── Redis Cache
├── CDN integration
├── Async Compression Workers
└── DevOps/Deployments

Team 3: Core Services (3-4 devs)
├── Auth/User maintenance
├── Content Service
├── Notification Service
└── Social scaling
```

### Structure Evolution

As complexity grows:

1. Frontend separates to manage three distinct interfaces (Video/Text/Image readers)
2. Infrastructure gets dedicated focus for Elasticsearch, CDN, and Compression Queues
3. Core Services maintains shared business logic

---

## Phase II

| Feature               | Signal                 |
|-----------------------|------------------------|
| Recommendation Engine | 10K+ users             |
| Native Mobile Apps    | asap                   |
| Advanced Search       | High search refinement |
| Moderation Tools      | Differentiation        |

## Future Phases

| Feature                 | Signal                                |
|-------------------------|---------------------------------------|
| WebSocket Notifications | There is a demand for instant updates |
| Creator Analytics       | 500+ uploaders                        |
| Paid chapters/episodes  | Revenue needed                        |
| Forums                  | >100 comments/day                     |
| AI Features             | Differentiation                       |