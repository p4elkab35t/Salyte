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
- **Framework/Libs:** Svelte 5
- **Styling:** Tailwind CSS (utility-first CSS framework).
- **Build Tool:** Vite (for fast builds and development).

### **Backend**
- **API:** GRPc, WebSocket, Rest
- **Languages:**
  - **Go:** Lightweight and fast microservices.
  - **Bun (TypeScript):** API Gateway
- **Database:** PostgreSQL (reliable and scalable).
- **Cache:** HTTP caching

### **DevOps**
- **Containerization:** Docker and Docker-compose
- **Version Control:** Git.
- **Deployment:** any linux-based vm.

---

## **Features to Be Implemented**
1. User authentication and registration.
2. ~~Privacy-centric user profiles with visibility controls.~~
3. Post creation and sharing (text, images, videos).
4. Microblogging features (short posts, replies, ~~hashtags~~).
5. ~~Real-time notifications (via WebSocket or SSE).~~
6. Advanced search and content discovery with tagging and filtering.
7. Like, comment, ~~and share~~ functionality.
8. ~~Content moderation and reporting tools~~.
9. ~~Direct messaging with end-to-end encryption.~~
10. Follower/following system with ~~customizable feed ~~options.
11. ~~Analytics dashboard for user and content performance tracking.~~
12. Mobile-friendly UI/UX with responsive design.
13. Integration with third-party services for content sharing.
14. ~~Efficient media uploads with compression and CDN support.~~
15. ~~Dark mode and accessibility features.~~

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

  **[Salyte API is fully documented here](https://github.com/p4elkab35t/salyte_backend/blob/2cbdcd25e43335032643aea5101d3dd4a16693fd/README.md)**

# **Getting Started**
1. Clone the repository:  
   ```bash
   git clone https://github.com/p4elkab35t/Salyte.git
   ```
2. Initialize docker-compose for backend
    ```bash
    cd salyte/backend
    docker-compose up --build -d
    ```
    `-d` option is used for running token
3. Initiailize docker-compose for front-end
    ```bash
    cd salyte/frontend
    docker-compose up --build -d
    ```
4. Identify your server ip with 
    ```bash
    ip a
    ```
5. connect to your front-end

