# **Salyte - A Performance-Oriented Social Network**

## **Problem Statement**
The evolution of social networks has seen a shift toward privacy, reduced digital profiling, and a focus on creating individualized projections in specific contexts. Platforms like Discord, X (formerly Twitter), Bluesky, and Instagram prioritize personal representation over exhaustive digital footprints. However, this trend faces challenges when combined with the rise of short-video platforms like TikTok, which leave hard digital imprints.

Modern social networks often suffer from:
- **Performance inefficiencies** due to reliance on large frameworks like React.
- **High DOM update frequencies** and excessive data loads.
- **Backend scalability and latency issues** caused by non-uniform architectural decisions.

**Salyte** addresses these issues by building a high-performance, privacy-centric social network optimized for speed, scalability, and user experience.

---

## **Project Overview**
Salyte is a lightweight, performance-oriented social network for microblogging, multimedia sharing, and community-driven interactions. Key features include:
- A clean, fast-loading, and minimalistic user interface.
- Privacy-centric user profiles with customizable visibility settings.
- Advanced analytics for creators, running in parallel to avoid user-facing delays.

---

## **Technology Stack**

### **Frontend**
- **Framework/Libs:** Svelte, Web Workers, other small libraries TBD.
- **Styling:** Tailwind CSS (utility-first CSS framework).
- **Build Tool:** Vite (for fast builds and development).

### **Backend**
- **API:** GraphQL (flexible data querying and fetching).
- **Languages:**
  - **Go:** Lightweight and fast microservices.
  - **Java or C#:** Type-safe, scalable services.
  - **Python/Node.js (TypeScript):** Analytics and data processing.
- **Database:** PostgreSQL (reliable and scalable).
- **Cache:** Redis (session management and frequently accessed data).

### **DevOps**
- **Containerization:** Docker and Kubernetes.
- **Version Control:** Git.
- **Deployment:** TBD (likely VPS or cloud-based solution).

---

## **Features to Be Implemented**
1. User authentication and registration (OAuth support for social logins).
2. Privacy-centric user profiles with visibility controls.
3. Post creation and sharing (text, images, videos).
4. Microblogging features (short posts, replies, hashtags).
5. Real-time notifications (via WebSocket or SSE).
6. Advanced search and content discovery with tagging and filtering.
7. Like, comment, and share functionality.
8. Content moderation and reporting tools.
9. Direct messaging with end-to-end encryption.
10. Follower/following system with customizable feed options.
11. Analytics dashboard for user and content performance tracking.
12. Mobile-friendly UI/UX with responsive design.
13. Integration with third-party services for content sharing.
14. Efficient media uploads with compression and CDN support.
15. Dark mode and accessibility features.

---

## **User Stories**
### **Core User Stories**
1. **User Authentication:**  
   *As a user, I want to register and log in using my email or social accounts so that I can access my profile and interact with the platform.*
2. **Privacy Settings:**  
   *As a user, I want to control the visibility of my posts and profile so that I can choose who sees my content.*
3. **Content Sharing:**  
   *As a user, I want to create and share text, images, and videos so that I can express myself on the platform.*
4. **Engagement Features:**  
   *As a user, I want to like, comment on, and share posts so that I can interact with others’ content.*
5. **Real-Time Notifications:**  
   *As a user, I want to receive instant notifications about likes, comments, and new followers so that I stay updated on my interactions.*

### **Extended User Stories**
6. **Direct Messaging:**  
   *As a user, I want to send secure messages to other users so that I can communicate privately.*
7. **Customizable Feeds:**  
   *As a user, I want to follow users and customize my feed so that I see the content that interests me most.*
8. **Search Functionality:**  
   *As a user, I want to search for posts and users using keywords and hashtags so that I can discover relevant content.*
9. **Content Moderation:**  
   *As an admin, I want tools to monitor and manage reports so that inappropriate content can be addressed promptly.*
10. **Performance Tracking:**  
    *As a creator, I want access to analytics about my posts so that I can understand my audience and improve engagement.*
11. **Responsive Design:**  
    *As a user, I want the platform to be mobile-friendly so that I can use it seamlessly on any device.*
12. **Dark Mode:**  
    *As a user, I want to enable dark mode so that I can reduce eye strain while using the app at night.*
13. **Media Upload Optimization:**  
    *As a user, I want my media uploads to be fast and of high quality so that my content looks good without long waits.*
14. **Tagging and Hashtags:**  
    *As a user, I want to tag users and add hashtags to my posts so that I can improve discoverability.*
15. **Third-Party Integration:**  
    *As a user, I want to share my posts directly to other platforms so that I can reach a wider audience.*

---

# High-level design

![alt text](<README.images/high-level arch.drawio-1.png>)

---
# Database schema

There will be two databases, one for user and auth, and other one for general manipulations

## User Database
![alt text](<README.images/Salyte auth preview.png>)

## Social Network Database
![alt text](<README.images/Salyte sn preview.png>)

---
# Salyte API
First of all Salyte API is shared between to main endpoints
`/secure` and `/api`

## `/secure` Endpoints (Authentication and Security)

### Users
- **POST `/secure/register`**
  - **Request Body:**
    ```json
    {
      "email": "user@example.com",
      "password": "password123"
    }
    ```
  - **Response:**
    ```json
    {
      "user_id": "uuid",
      "email": "user@example.com",
      "is_verified": false
    }
    ```
  - **Description:** Register a new user.

- **POST `/secure/login`**
  - **Request Body:**
    ```json
    {
      "email": "user@example.com",
      "password": "password123"
    }
    ```
  - **Response:**
    ```json
    {
      "session_token": "token",
      "expires_at": "timestamp"
    }
    ```
  - **Description:** Log in a user.

- **POST `/secure/logout`**
  - **Request Header:**
    ```
    Authorization: Bearer <session_token>
    ```
  - **Response:**
    ```json
    {
      "message": "Logged out successfully"
    }
    ```
  - **Description:** Log out a user.

- **POST `/secure/verify-email`**
  - **Request Body:**
    ```json
    {
      "user_id": "uuid",
      "verification_code": "code"
    }
    ```
  - **Response:**
    ```json
    {
      "message": "Email verified successfully"
    }
    ```
  - **Description:** Verify a user's email.

- **POST `/secure/request-password-reset`**
  - **Request Body:**
    ```json
    {
      "email": "user@example.com"
    }
    ```
  - **Response:**
    ```json
    {
      "message": "Password reset link sent"
    }
    ```
  - **Description:** Request a password reset.

- **POST `/secure/reset-password`**
  - **Request Body:**
    ```json
    {
      "reset_token": "token",
      "new_password": "newpassword123"
    }
    ```
  - **Response:**
    ```json
    {
      "message": "Password reset successfully"
    }
    ```
  - **Description:** Reset a user's password.

### Sessions
- **GET `/secure/sessions`**
  - **Request Header:**
    ```
    Authorization: Bearer <session_token>
    ```
  - **Response:**
    ```json
    [
      {
        "session_id": "uuid",
        "created_at": "timestamp",
        "expires_at": "timestamp"
      }
    ]
    ```
  - **Description:** Get all active sessions for a user.

- **DELETE `/secure/sessions/{session_id}`**
  - **Request Header:**
    ```
    Authorization: Bearer <session_token>
    ```
  - **Response:**
    ```json
    {
      "message": "Session terminated successfully"
    }
    ```
  - **Description:** Terminate a specific session.

### Security Logs
- **GET `/secure/security-logs`**
  - **Request Header:**
    ```
    Authorization: Bearer <session_token>
    ```
  - **Response:**
    ```json
    [
      {
        "log_id": "uuid",
        "action": "login",
        "ip_address": "192.168.1.1",
        "timestamp": "timestamp"
      }
    ]
    ```
  - **Description:** Get security logs for a user.

---

## `/api` Endpoints (Social Networking Features)

### Profiles
- **GET `/api/profiles/{profile_id}`**
  - **Response:**
    ```json
    {
      "profile_id": "uuid",
      "username": "user123",
      "bio": "Hello world!",
      "profile_picture_url": "url",
      "visibility": "public"
    }
    ```
  - **Description:** Get a profile by ID.

- **PUT `/api/profiles/{profile_id}`**
  - **Request Body:**
    ```json
    {
      "bio": "Updated bio",
      "visibility": "private"
    }
    ```
  - **Response:**
    ```json
    {
      "message": "Profile updated successfully"
    }
    ```
  - **Description:** Update a profile.

### Posts
- **POST `/api/posts`**
  - **Request Body:**
    ```json
    {
      "profile_id": "uuid",
      "content": "This is a post",
      "visibility": "public"
    }
    ```
  - **Response:**
    ```json
    {
      "post_id": "uuid",
      "created_at": "timestamp"
    }
    ```
  - **Description:** Create a new post.

- **GET `/api/posts/{post_id}`**
  - **Response:**
    ```json
    {
      "post_id": "uuid",
      "content": "This is a post",
      "media_url": "url",
      "visibility": "public",
      "created_at": "timestamp"
    }
    ```
  - **Description:** Get a post by ID.
- **GET `/api/posts/community/{community_id}`**
  - **Request Body:**
    ```json
    {
      "page": 1,
      "posts_per_page": 15
    }
    ```
  - **Response:**
    ```json
    {
      "posts": 
         [{
            "post_id": "uuid",
            "content": "This is a post",
            "media_url": "url",
            "visibility": "public",
            "created_at": "timestamp"
         }],
      "current_page": 1,
      "number_of_pages": 1
    }
    ```
  - **Description:** Get community posts for a page.

- **GET `/api/posts/profile/{profile_id}`**
  - **Request Body:**
    ```json
    {
      "page": 1,
      "posts_per_page": 15
    }
    ```
  - **Response:**
    ```json
    {
      "posts": 
         [{
            "post_id": "uuid",
            "content": "This is a post",
            "media_url": "url",
            "visibility": "public",
            "created_at": "timestamp"
         }],
      "current_page": 1,
      "number_of_pages": 1
    }
    ```
  - **Description:** Get profile posts for a page.


- **DELETE `/api/posts/{post_id}`**
  - **Response:**
    ```json
    {
      "message": "Post deleted successfully"
    }
    ```
  - **Description:** Delete a post.

### Comments
- **POST `/api/comments`**
  - **Request Body:**
    ```json
    {
      "profile_id": "uuid",
      "post_id": "uuid",
      "content": "Great post!"
    }
    ```
  - **Response:**
    ```json
    {
      "comment_id": "uuid",
      "created_at": "timestamp"
    }
    ```
  - **Description:** Add a comment to a post.

- **DELETE `/api/comments/{comment_id}`**
  - **Response:**
    ```json
    {
      "message": "Comment deleted successfully"
    }
    ```
  - **Description:** Delete a comment.

### Likes
- **POST `/api/likes`**
  - **Request Body:**
    ```json
    {
      "profile_id": "uuid",
      "post_id": "uuid"
    }
    ```
  - **Response:**
    ```json
    {
      "like_id": "uuid",
      "created_at": "timestamp"
    }
    ```
  - **Description:** Like a post.

- **DELETE `/api/likes/{like_id}`**
  - **Response:**
    ```json
    {
      "message": "Like removed successfully"
    }
    ```
  - **Description:** Unlike a post.

### Shares
- **POST `/api/shares`**
  - **Request Body:**
    ```json
    {
      "profile_id": "uuid",
      "post_id": "uuid"
    }
    ```
  - **Response:**
    ```json
    {
      "share_id": "uuid",
      "created_at": "timestamp"
    }
    ```
  - **Description:** Share a post.

### Followers
- **POST `/api/follow`**
  - **Request Body:**
    ```json
    {
      "follower_profile_id": "uuid",
      "followed_profile_id": "uuid"
    }
    ```
  - **Response:**
    ```json
    {
      "follower_id": "uuid",
      "created_at": "timestamp"
    }
    ```
  - **Description:** Follow a profile.

- **DELETE `/api/follow/{follower_id}`**
  - **Response:**
    ```json
    {
      "message": "Unfollowed successfully"
    }
    ```
  - **Description:** Unfollow a profile.

### Messages
- **POST `/api/messages`**
  - **Request Body:**
    ```json
    {
      "sender_profile_id": "uuid",
      "receiver_profile_id": "uuid",
      "content": "Hello!"
    }
    ```
  - **Response:**
    ```json
    {
      "message_id": "uuid",
      "created_at": "timestamp"
    }
    ```
  - **Description:** Send a message.

- **GET `/api/messages`**
  - **Request Header:**
    ```
    Authorization: Bearer <session_token>
    ```
  - **Response:**
    ```json
    [
      {
        "message_id": "uuid",
        "sender_profile_id": "uuid",
        "content": "Hello!",
        "created_at": "timestamp"
      }
    ]
    ```
  - **Description:** Get all messages for a user.

### Notifications
- **GET `/api/notifications`**
  - **Request Header:**
    ```
    Authorization: Bearer <session_token>
    ```
  - **Response:**
    ```json
    [
      {
        "notification_id": "uuid",
        "type": "like",
        "source_id": "uuid",
        "is_read": false,
        "created_at": "timestamp"
      }
    ]
    ```
  - **Description:** Get all notifications for a user.

- **PUT `/api/notifications/{notification_id}`**
  - **Response:**
    ```json
    {
      "message": "Notification marked as read"
    }
    ```
  - **Description:** Mark a notification as read.

### Analytics
- **GET `/api/analytics/{profile_id}`**
  - **Response:**
    ```json
    {
      "profile_id": "uuid",
      "views": 100,
      "likes": 50,
      "shares": 10,
      "created_at": "timestamp"
    }
    ```
  - **Description:** Get analytics for a profile.

- **GET `/api/analytics/posts/{post_id}`**
  - **Response:**
    ```json
    {
      "post_id": "uuid",
      "views": 100,
      "likes": 50,
      "shares": 10,
      "created_at": "timestamp"
    }
    ```
  - **Description:** Get analytics for a specific post.

### Settings
- **GET `/api/settings/{profile_id}`**
  - **Response:**
    ```json
    {
      "setting_id": "uuid",
      "dark_mode_enabled": false,
      "language": "en"
    }
    ```
  - **Description:** Get settings for a profile.

- **PUT `/api/settings/{setting_id}`**
  - **Request Body:**
    ```json
    {
      "dark_mode_enabled": true,
      "language": "fr"
    }
    ```
  - **Response:**
    ```json
    {
      "message": "Settings updated successfully"
    }
    ```
  - **Description:** Update settings.

### Friendships
- **POST `/api/friendships`**
  - **Request Body:**
    ```json
    {
      "profile_id": "uuid",
      "friend_profile_id": "uuid"
    }
    ```
  - **Response:**
    ```json
    {
      "friendship_id": "uuid",
      "status": "pending",
      "created_at": "timestamp"
    }
    ```
  - **Description:** Send a friend request.

- **PUT `/api/friendships/{friendship_id}`**
  - **Request Body:**
    ```json
    {
      "status": "accepted"
    }
    ```
  - **Response:**
    ```json
    {
      "message": "Friend request accepted"
    }
    ```
  - **Description:** Accept or reject a friend request.

- **DELETE `/api/friendships/{friendship_id}`**
  - **Response:**
    ```json
    {
      "message": "Friend removed successfully"
    }
    ```
  - **Description:** Remove a friend.

### Communities
- **POST `/api/communities`**
  - **Request Body:**
    ```json
    {
      "name": "Community Name",
      "description": "Description",
      "visibility": "public"
    }
    ```
  - **Response:**
    ```json
    {
      "community_id": "uuid",
      "created_at": "timestamp"
    }
    ```
  - **Description:** Create a new community.

- **GET `/api/communities/{community_id}`**
  - **Response:**
    ```json
    {
      "community_id": "uuid",
      "name": "Community Name",
      "description": "Description",
      "profile_picture_url": "url",
      "visibility": "public",
      "created_at": "timestamp"
    }
    ```
  - **Description:** Get a community by ID.

- **POST `/api/communities/{community_id}/join`**
  - **Request Body:**
    ```json
    {
      "profile_id": "uuid"
    }
    ```
  - **Response:**
    ```json
    {
      "member_id": "uuid",
      "role": "member",
      "joined_at": "timestamp"
    }
    ```
  - **Description:** Join a community.

- **DELETE `/api/communities/{community_id}/leave`**
  - **Request Body:**
    ```json
    {
      "profile_id": "uuid"
    }
    ```
  - **Response:**
    ```json
    {
      "message": "Left community successfully"
    }
    ```
  - **Description:** Leave a community.

### Community Members
- **GET `/api/communities/{community_id}/members`**
  - **Response:**
    ```json
    [
      {
        "member_id": "uuid",
        "profile_id": "uuid",
        "role": "member",
        "joined_at": "timestamp"
      }
    ]
    ```
  - **Description:** Get all members of a community.

- **PUT `/api/communities/{community_id}/members/{member_id}`**
  - **Request Body:**
    ```json
    {
      "role": "admin"
    }
    ```
  - **Response:**
    ```json
    {
      "message": "Member role updated successfully"
    }
    ```
  - **Description:** Update a member's role in a community.

- **DELETE `/api/communities/{community_id}/members/{member_id}`**
  - **Response:**
    ```json
    {
      "message": "Member removed successfully"
    }
    ```
  - **Description:** Remove a member from a community.
## **Getting Started**
1. Clone the repository:  
   ```bash
   git clone https://github.com/p4elkab35t/Salyte.git
   ```

