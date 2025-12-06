# Temniy-Prince

A digital platform for manga, light novels, and anime streaming with social features.
It will be an app with 3 frontends, one for each type of content, one for manga, one for novels etc.
But they will be combine thought the single user account and characters/franchises that are repeated.
The platform is user driven, so there will be simple users, uploaders (user who have permission to upload new
chapters/new titles) and admins.
Each user will have public profiles with library of their titles and each chapter and title will have a tree-like
comment section.
For the async jobs:

1. on each upload of new images or videos we would run async image compression
2. background jobs for notification delivery


1. Elements

- 3 Frontend Apps: MangaApp, NovelApp, AnimeApp
- 7 Backend Services: Auth, Content, Media, User, Social, Search, Notification
- Data: PostgreSQL (primary), Redis (cache/queue), S3-compatible (media)
- CDN, Elasticsearch

2. Architectural Patterns

- Microservices
- Federated Frontend (3 apps, 1 auth)
- BFF Pattern for each frontend (server side rendering)
- Queue-Based Load Leveling

3. Communication

- REST + Queues for async jobs like compression

4. AuthN & AuthZ

- AuthN: JWT, OAuth
- AuthZ: Guest -> User -> Uploader -> Moderator -> Admin
- Resource-level permissions (like uploaders assigned to specific titles)

