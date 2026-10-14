# Role & Objective
Act as a Principal Full-Stack Software Architect and Lead Developer. Design and build a comprehensive, multi-tenant Legal Tech Platform ("DahiLex") that connects clients with advocates/law firms, enables monetized advocate-to-advocate collaboration, includes a peer-to-peer social connection network, and integrates a dedicated Judiciary Management System for courts and judges.

---

## 1. User Roles & RBAC (Role-Based Access Control)
1. **Client / Public User:** Searches advocates/firms, sends/receives friend and network connection requests, books appointments, pays consultation fees, and communicates during scheduled sessions.
2. **Advocate (Individual Practitioner):** Manages profile, availability, fee rates (messages, video, meetings), connects with peers/clients via friend requests, collaborates in firm groups, and manages court cases.
3. **Law Firm Admin:** Manages firm profile, associates list, firm calendar, fee distribution, firm group chats, and firm-wide connections.
4. **Judge / Court Official:** Manages court dockets, cause lists, case files, issues summons/notices, and connects/communicates with linked advocates and legal officials.
5. **Super Admin:** Platform governance, transaction splits, bar license verification, connection dispute moderation, and platform analytics.

---

## 2. Core Feature Modules

### Module A: Frontend Discovery & Geo-Search Engine
* **Filter Criteria:**
  * "Near Me" (Haversine geospatial radius search via live GPS lat/long).
  * City, Bar Council License Number, Name, Experience (Years), Practice Areas (Corporate, Criminal, Family, Civil), and User Ratings.
* **Law Firm & Advocate Profiles:** Displays addresses, bio, license verification badge, online/offline slots, pricing schedule, reviews, and a "Send Friend/Connection Request" CTA.

### Module B: Social Network & Connection Engine (Friends Feature)
* **Friend / Connection Request Workflow:**
  * Cross-role request system (Client-to-Advocate, Advocate-to-Advocate, Client-to-Client, Judge-to-Advocate).
  * Request states: `PENDING`, `ACCEPTED`, `DECLINED`, `BLOCKED`.
  * Actions: Send Request, Accept/Decline Request, Cancel Sent Request, Remove Friend, Block User.
* **Privacy & Monetization Overrides:**
  * Advocates can configure if **Connected Friends** receive free messaging/discounted consultation rates or adhere to standard rate cards.
  * Direct messaging permissions based on relationship state (e.g., Friends can direct chat, Non-friends must pay per-message fee).
  * Real-time push notifications for new connection requests, acceptances, and status updates.

### Module C: Dual Booking & Payment Gateway System
* **Booking Types:**
  * **Online:** WebRTC video call or encrypted voice consultation.
  * **Offline:** Physical office visit / court premise meeting.
* **Workflow:**
  1. Client/Friend selects type (Online/Offline) -> Chooses available time slot.
  2. Dynamic Fee Calculation (Advocate Fee [adjusted for connection status] + Platform Fee).
  3. Integrated Payment Gateways (Stripe / Local Bank Gateways).
  4. Escrow / Hold Payment until consultation completion or instant release rules.
  5. Automated ICS calendar invite, SMS/Email confirmation, and WebRTC room generation.

### Module D: Communication & Monetization Engine
* **Channels:**
  * **Direct Peer / Friend Chat:** Real-time messaging between connected friends or paid client sessions.
  * **Firm / Group Chat:** Multi-user channels for law firms, practice groups, and legal research teams.
* **Rate Cards & Monetization:**
  * Per-Message Rate (for non-connected or premium message requests).
  * Per-Minute / Per-Session Video Call Rate.
  * In-Person Meeting Consultation Rate.
* **Tech Stack:** WebSockets (Socket.io / Pusher) with audio/video via WebRTC / Agora SDK.

### Module E: Judiciary & Court Portal Integration
* **Court & Judge Dashboard:**
  * E-Filing & Case Bench Management (Status: Pending, Under Hearing, Disposed, Stayed).
  * Digital Cause Lists / Daily Dockets.
* **Advocate-Judiciary Connection:**
  * Direct official notice/summons dispatch to advocates' accounts.
  * Judge-Advocate professional networking & official communication channels.
  * Virtual Courtroom Integration for live online hearings.

---

## 3. Database Architecture Requirements (SQL Schema)
Generate optimized schema tables including foreign keys, indexes, and ENUM types for:

* `users` & `user_roles`
* `friendships` / `connection_requests` (`id`, `requester_id`, `addressee_id`, `status` [PENDING, ACCEPTED, DECLINED, BLOCKED], `created_at`, `updated_at`)
* `user_privacy_settings` (`user_id`, `allow_friend_requests_from`, `free_chat_for_friends`)
* `advocate_profiles` (`lat`, `lng`, `experience_years`, `bar_license`, `specialization_tags`)
* `law_firms` & `firm_advocates`
* `advocate_pricing_rates` (`per_message_fee`, `video_call_fee`, `offline_meeting_fee`, `friend_discount_percent`)
* `appointments` (`status`, `booking_type`, `start_time`, `end_time`, `payment_status`)
* `chat_rooms`, `chat_messages`, & `firm_groups`
* `court_rooms`, `judges`, `cases`, `case_hearings`, & `court_notices`
* `transactions` & `escrow_payouts`

---

## 4. RESTful API Endpoints Specification
Include endpoints for:
* **Connections:**
  * `POST /api/v1/connections/request` (Send request)
  * `PUT /api/v1/connections/request/:id/respond` (Accept/Decline)
  * `DELETE /api/v1/connections/:id` (Remove friend / Cancel request)
  * `GET /api/v1/connections/list` (Fetch friends with status filter)
  * `POST /api/v1/connections/block` (Block user)
* **Search & Booking:** `GET /api/v1/advocates/search`, `POST /api/v1/appointments/book`
* **Chat & Rates:** `POST /api/v1/chat/rate-card`, `POST /api/v1/chat/send-paid-message`
* **Judiciary:** `GET /api/v1/court/cause-list`, `POST /api/v1/court/summons`

---

## 5. Deliverables Requested
1. **Entity Relationship Diagram (ERD) & Production-Ready SQL Schema.**
2. **Complete RESTful / GraphQL API Endpoints Documentation.**
3. **Frontend Architecture & Component Layout** (React / Next.js / Flutter UI structure).
4. **Implementation Guide** for the dynamic payment booking pipeline, friend request state machine, and real-time chat/video architecture.
........................
