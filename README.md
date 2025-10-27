# 🐀 DevRats

> Transform your coding journey into a shared experience. Stay consistent, stay motivated, stay coding.

[![Next.js](https://img.shields.io/badge/Next.js-15.5.6-black?style=flat&logo=next.js)](https://nextjs.org/)
[![MongoDB](https://img.shields.io/badge/MongoDB-Database-green?style=flat&logo=mongodb)](https://www.mongodb.com/)
[![Tailwind CSS](https://img.shields.io/badge/Tailwind-CSS-38B2AC?style=flat&logo=tailwind-css)](https://tailwindcss.com/)
[![NextAuth.js](https://img.shields.io/badge/NextAuth.js-Authentication-purple?style=flat)](https://next-auth.js.org/)

## 📖 About

**DevRats** is a gamified social platform that transforms learning and practicing programming into a collaborative and motivating experience. Built for developers who want to maintain consistency in their studies and projects through shared accountability in groups.

### Core Concept

Users make **daily check-ins** by sharing photos of the code they're working on, building a **streak** of active days that encourages constant practice and reinforces commitment. Think Duolingo, but for coding consistency.

### Key Features

- 📸 **Daily Check-ins**: Share code screenshots with title, description, and technology stack
- 🔥 **Streak System**: Build and maintain consecutive active days
- 👥 **Thematic Groups**: Create or join groups focused on specific technologies or goals
- 🏆 **Rankings**: Weekly, monthly, yearly, and all-time leaderboards based on active days
- 💬 **Integrated Chat**: Discuss technical topics and provide mutual support
- 📅 **Activity Calendar**: Visual record of your learning journey with photos
- ⚡ **Real-time Feed**: See what your group members are working on

## 🎯 Perfect For

- Students maintaining consistent study routines
- Developers in career transitions
- Remote teams practicing asynchronous collaboration
- Study groups focused on specific technologies
- Bootcamps encouraging daily practice
- Anyone participating in challenges like #100DaysOfCode

## 🛠️ Tech Stack

| Category | Technology |
|----------|------------|
| **Framework** | Next.js 15.5.6 (App Router) |
| **Database** | MongoDB + Mongoose |
| **Authentication** | NextAuth.js |
| **Styling** | Tailwind CSS |
| **Deployment** | Vercel |

## 📂 Project Structure

```
DevRats/
├── public/
│   ├── icons/              # Application icons
│   └── images/             # Static images
│
├── src/
│   ├── app/
│   │   ├── (auth)/         # Authentication routes
│   │   │   ├── login/
│   │   │   └── register/
│   │   │
│   │   ├── (dashboard)/    # Protected dashboard routes
│   │   │   ├── home/
│   │   │   ├── profile/
│   │   │   ├── settings/
│   │   │   └── group/
│   │   │       ├── create/
│   │   │       ├── join/
│   │   │       └── [id]/
│   │   │           ├── details/
│   │   │           ├── ranking/
│   │   │           └── chat/
│   │   │
│   │   └── api/            # API routes
│   │       ├── auth/
│   │       ├── users/
│   │       ├── groups/
│   │       ├── posts/
│   │       └── chat/
│   │
│   ├── components/         # React components
│   │   ├── auth/
│   │   ├── layout/
│   │   ├── posts/
│   │   ├── groups/
│   │   ├── profile/
│   │   ├── ranking/
│   │   └── chat/
│   │
│   ├── models/             # MongoDB schemas
│   │   ├── User.js
│   │   ├── Group.js
│   │   ├── Post.js
│   │   ├── Comment.js
│   │   ├── Reaction.js
│   │   └── Message.js
│   │
│   └── lib/                # Utilities
│       ├── mongodb.js
│       ├── auth.js
│       └── utils.js
│
├── .env.local              # Environment variables
├── next.config.js
├── tailwind.config.js
└── package.json
```

## 🗄️ Database Schema

### Users Collection
```javascript
{
  _id: ObjectId,
  name: String,
  email: String,                    // Unique, indexed
  password: String,                 // Bcrypt hash
  avatar: String,                   // URL or /public path
  streak: Number,                   // Consecutive active days (default: 0)
  lastPostDate: String,             // YYYY-MM-DD format
  activeGroup: ObjectId,            // Currently selected group (ref: Groups)
  createdAt: Date,
  updatedAt: Date
}
```

### Groups Collection
```javascript
{
  _id: ObjectId,
  name: String,
  description: String,
  picture: String,                  // URL
  inviteCode: String,               // Unique invite code
  creator: ObjectId,                // ref: Users
  members: [
    {
      user: ObjectId,               // ref: Users
      role: String,                 // "admin" or "member"
      joinedAt: Date
    }
  ],
  createdAt: Date,
  updatedAt: Date
}
```

### Posts Collection
```javascript
{
  _id: ObjectId,
  title: String,
  description: String,
  imageUrl: String,                 // Code screenshot URL
  technology: String,               // e.g., "React", "Python", "Node.js"
  startTime: Date,
  user: ObjectId,                   // ref: Users
  group: ObjectId,                  // ref: Groups
  createdAt: Date,
  updatedAt: Date
}
```

### Comments Collection
```javascript
{
  _id: ObjectId,
  content: String,
  user: ObjectId,                   // ref: Users
  post: ObjectId,                   // ref: Posts
  createdAt: Date
}
```

### Reactions Collection
```javascript
{
  _id: ObjectId,
  type: String,                     // "like", "fire", "clap", "rocket"
  user: ObjectId,                   // ref: Users
  post: ObjectId,                   // ref: Posts
  createdAt: Date
}
```

### Messages Collection
```javascript
{
  _id: ObjectId,
  content: String,
  user: ObjectId,                   // ref: Users
  group: ObjectId,                  // ref: Groups
  createdAt: Date
}
```

## 🚀 Getting Started

### Prerequisites

- Node.js 18+ 
- MongoDB database
- npm or yarn

### Installation

1. **Clone the repository**
```bash
git clone https://github.com/yourusername/devrats.git
cd devrats
```

2. **Install dependencies**
```bash
npm install
# or
yarn install
```

3. **Set up environment variables**

Create a `.env.local` file in the root directory:

```env
# MongoDB
MONGODB_URI=your_mongodb_connection_string

# NextAuth
NEXTAUTH_URL=http://localhost:3000
NEXTAUTH_SECRET=your_nextauth_secret

# Optional: File Upload (if using external service)
# CLOUDINARY_URL=your_cloudinary_url
# or configure for your preferred upload service
```

4. **Run the development server**
```bash
npm run dev
# or
yarn dev
```

5. **Open your browser**

Navigate to [http://localhost:3000](http://localhost:3000)

## 📱 Application Pages

| Page | Route | Description |
|------|-------|-------------|
| Login | `/login` | User authentication |
| Register | `/register` | Account creation |
| Dashboard | `/home` | Feed with group posts |
| Profile | `/profile` | User profile with activity calendar |
| Settings | `/settings` | Edit profile and account settings |
| Create Group | `/group/create` | Create a new group |
| Join Group | `/group/join` | Enter group with invite code |
| Group Details | `/group/[id]/details` | Group information and members |
| Rankings | `/group/[id]/ranking` | Leaderboards by period |
| Chat | `/group/[id]/chat` | Group conversation |

## 🔌 API Endpoints

### Authentication
- `POST /api/auth/login` - User login
- `POST /api/auth/register` - User registration
- `POST /api/auth/logout` - User logout

### Users
- `GET /api/users/me` - Get current user data
- `PUT /api/users/me` - Update user profile
- `DELETE /api/users/me` - Delete account
- `POST /api/users/me/avatar` - Upload avatar
- `GET /api/users/me/groups` - Get user's groups
- `GET /api/users/me/activity?month=YYYY-MM` - Get activity calendar
- `GET /api/users/me/posts` - Get user's posts
- `GET /api/users/me/stats` - Get user statistics

### Groups
- `POST /api/groups` - Create new group
- `POST /api/groups/join` - Join group with invite code
- `GET /api/groups/:id` - Get group details
- `GET /api/groups/:id/members` - Get group members
- `POST /api/groups/:id/invite` - Generate invite code
- `DELETE /api/groups/:id/leave` - Leave group
- `GET /api/groups/:id/rankings?period=week|month|year|all-time` - Get rankings

### Posts
- `POST /api/posts` - Create new post (check-in)
- `GET /api/posts/:id` - Get single post
- `GET /api/posts/groups/:groupId/feed` - Get group feed
- `POST /api/posts/:id/comments` - Add comment
- `POST /api/posts/:id/reactions` - Add reaction

### Chat
- `GET /api/chat/groups/:groupId/messages?since=timestamp` - Get messages
- `POST /api/chat/groups/:groupId/messages` - Send message
- `DELETE /api/chat/messages/:id` - Delete message

## 📝 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🤝 Contributing

Contributions, issues, and feature requests are welcome! Feel free to check the [issues page](https://github.com/yourusername/devrats/issues).

## ⭐ Show your support

Give a ⭐️ if this project helped you stay consistent in your coding journey!

---

<div align="center">
  <strong>Built with ❤️ by developers, for developers</strong>
</div>
