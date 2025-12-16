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