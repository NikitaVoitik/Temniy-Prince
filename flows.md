### Core User Flows

**1. User Registration & Profile Creation**
- Action: User signs up via Google OAuth, sets username
- Elements: Client, Gateway, Auth Service, Accounts DB, User Service
- Flow:
  - Auth Service validates credentials, issues JWT
  - User Service creates profile in Accounts DB

**2. Universal Content Search**
- Action: User searches for content across all media types
- Elements: Frontend App, Gateway, Search Service, Elasticsearch, Content DB
- Flow:
  - Query goes to Search Service → Elasticsearch
  - Results include media type (Manga/Anime/Novel) for routing

**3. Media Consumption & History Sync**
- Action: User reads/watches content, progress is saved
- Elements: Frontend App, Gateway, Content Service, CDN, User Service, Accounts DB
- Flow:
  - Content Service returns CDN URLs
  - Frontend sends progress events to User Service
  - History saved in Accounts DB for resume

**4. Threaded Comment Posting**
- Action: User posts comment on specific content
- Elements: Frontend App, Gateway, Social Service, Comments DB, Notification Service
- Flow:
  - Comment stored in Comments DB (linked to content ID)
  - Replies trigger Notification Service

---

### Unique Flows

**5. Uploader Publishes New Chapter**
- Action: Uploader uploads ZIP with images for new chapter
- Elements: Gateway, Auth Service, Content Service, Media Service, S3, Redis Queue
- Flow:
  - Auth checks JWT has Uploader role + title permission
  - Media Service uploads to S3 Ingest Bucket
  - Job pushed to Redis Queue
  - Returns "Processing" status immediately

**6. Async Media Compression**
- Action: System processes raw upload in background
- Elements: Redis Queue, Compression Worker, S3, Media Service, Content DB, Notification Service
- Flow:
  - Worker pulls task from Redis
  - Downloads from S3, compresses, uploads to Public Bucket
  - Updates status to "Live" in Content DB
  - Notifies Uploader

**7. Cross-Franchise Navigation**
- Action: User switches from Anime to related Manga
- Elements: AnimeApp, Gateway, Content Service, MangaApp
- Flow:
  - User clicks "View Source Material"
  - Content Service finds linked MangaID
  - Returns deep link (manga-app://title/123)
  - Client switches apps, JWT preserved

**8. New Release Notification Fan-out**
- Action: New chapter goes live, subscribers notified
- Elements: Content Service, Notification Service, User Service, Notifications DB
- Flow:
  - Content Service emits NewChapterCreated event
  - Notification Service fetches subscriber list from User Service
  - Notifications batch-inserted into Notifications DB
  - Users see notifications on next page load
