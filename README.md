# Product Requirements Document (PRD)
## Creator App — Subscription & Exclusive Content Platform


---

## 1. Overview

Creator App is a subscription-based content platform where creators (including AI influencers) can share exclusive and subscription-only content (images, videos) with their audience. Users can follow creators, subscribe to their content, pay for exclusive posts, and interact through dedicated chat rooms — similar in spirit to platforms like OnlyFans/Patreon, but built around a specific creator/influencer use case.

## 2. Goals & Objectives

- Allow any user to become a **creator** and monetize content through subscriptions and pay-per-content (exclusive) posts.
- Allow **followers/fans** to discover creators (via an Explore feed), follow them for free, subscribe for recurring paid access, and unlock exclusive one-off content.
- Build a direct communication channel between creators and their paying audience via chat rooms.
- Provide a simple, secure account system (login/signup/forgot password) as the foundation.

## 3. Target Users

| Persona | Description |
|---|---|
| **Creator** | A user (e.g., an AI influencer's operator) who posts content, sets subscription/exclusive pricing, and engages with subscribers via chat. |
| **Fan / Subscriber** | A user who follows creators, subscribes to unlock recurring content, and/or purchases individual exclusive posts. |
| **Simple User** | Any registered user who hasn't opted into being a creator yet — can still follow, browse, and purchase content from creators. |

> Note: Every account starts as a "user" and can enable a **Creator Profile** — there's no separate signup flow for creators vs. fans.

## 4. Core Features & Requirements

### 4.1 Authentication
- User **Signup** (email/phone + password, or social login — to be decided)
- User **Login**
- **Forgot Password** flow (OTP or reset-link based)
- Session management (JWT or token-based auth)
- Email/phone verification (recommended, for trust & safety)

### 4.2 User Roles
- A single user account can toggle **Creator Mode** on:
  - Enabling Creator Mode unlocks: post creation, pricing settings, subscription plan setup, and chat room creation.
- **Simple User** capabilities: browse, follow, subscribe, purchase, comment/like (if in scope), chat (if subscribed).

### 4.3 Profile
- Editable profile: name, username, profile picture, cover photo, bio.
- **Bio section** supports:
  - Social media links (Instagram, X/Twitter, YouTube, etc.)
  - Custom usernames/handles per platform
- Creator-specific profile additions:
  - Subscription price & plan details
  - Total posts, subscriber count (visible per creator's privacy setting)

### 4.4 Follow System
- Users can **follow** other users/creators for free (no payment required).
- Following ≠ Subscribing:
  - **Follow** → get updates/notifications, see public/free posts.
  - **Subscribe** → paid, unlocks subscription-tier content.
- Follower/following counts shown on profile.

### 4.5 Content Posting — Two Categories

#### A. Subscription Posts
- Visible only to users who hold an **active subscription** to that creator.
- Supports **image** and **video** content.
- Creators can offer **Monthly** and **Yearly** subscription plans (creator sets pricing for each).
- Subscriptions include **auto-renew payment** — billing cycle renews automatically until the user cancels.
- If subscription lapses/expires (or auto-renew fails/is cancelled), access to this content is revoked.

#### B. Exclusive Posts
- Independent of subscription status — a **one-time purchase** per post.
- Each exclusive post can be priced individually:
  - **Free**
  - **Paid** (creator sets custom amount)
- Users must complete payment to unlock and view (image/video).
- Once purchased, content remains accessible to that buyer for **1 year** from the purchase date (access expires after 1 year).
- **No active subscription required** — any user can purchase and unlock an Exclusive post independently, whether or not they're subscribed to that creator.

### 4.6 Payments & Monetization
- Payment gateway: **Razorpay** (confirmed).
- Handle:
  - Recurring subscription billing (monthly/yearly plans, auto-renew, cancellation, expiry)
  - One-time purchases for Exclusive posts (1-year access window)
  - Creator payout/withdrawal system
  - Platform commission (%) on transactions
- Transaction history for both users (purchases) and creators (earnings).

### 4.7 Chat Rooms
- Each creator has **one shared chat room/group** (not multiple or tiered rooms).
- All of that creator's active subscribers can join this single group and talk with the creator and/or each other.
- **1:1 DM** (optional/future scope): private chat between a subscriber and creator — not part of launch scope.
- Access control: only users with an active subscription can join/view the chat room; access revoked on subscription expiry.
- Real-time messaging (text at minimum; image/media sharing as a stretch goal).

### 4.8 Explore / Discovery Feed
- A public **Explore feed** to help new/upcoming creators get discovered (not purely follow/link-based growth).
- Surfaces creator profiles (and their public/free content) to users who aren't following them yet.
- Basis for ranking (e.g., new creators, trending, most subscribed) to be defined during design.

## 5. Non-Functional Requirements

- **Security:** Encrypted passwords, secure payment handling (PCI-DSS compliant gateway), signed URLs for paid media so content can't be accessed without authorization.
- **Media Storage:** Cloud storage (e.g., AWS S3 / Cloudflare R2) with CDN delivery for images/videos.
- **Scalability:** Should support growing number of creators/subscribers without performance drop (especially chat and media delivery).
- **Content Protection:** Watermarking or DRM-lite measures to reduce screenshot/screen-recording leaks — **confirmed as a future enhancement, not required at launch.**
- **Notifications:** Push/email notifications for new posts, new subscribers, chat messages, payment confirmations.
- **Moderation:** Content reporting/flagging system, admin panel for reviewing reported content and managing platform policy compliance.

## 6. Suggested Phased Roadmap

| Phase | Scope |
|---|---|
| **Phase 1 (MVP)** | Auth (login/signup/forgot password), profile with bio & social links, follow system, subscription posts (monthly/yearly, Razorpay auto-renew) |
| **Phase 2** | Exclusive posts (free/paid, 1-year access via Razorpay), creator payout dashboard, Explore/discovery feed |
| **Phase 3** | Chat rooms (one shared group per creator), notifications |
| **Phase 4** | 1:1 DMs, content protection (watermarking), analytics dashboard for creators, admin/moderation panel |

---

*This PRD reflects your confirmed decisions. Ready to move to wireframes/technical design.*
