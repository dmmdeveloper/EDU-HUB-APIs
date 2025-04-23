# 📚 EduHub – Online Learning Platform API

Welcome to **EduHub**, a fully-featured REST API for an online learning platform. This platform enables students to learn from instructors via video courses, interact through messaging, and even earn certificates.

---

## 🌐 Project Overview
EduHub is designed as a mega practice project for backend developers. It includes authentication, course management, enrollment, messaging, payments, and more.

---

## 🧑‍🎓 1️⃣ USERS

### Roles
- `student`
- `instructor`
- `admin`

### User Schema
```js
{
  _id,
  name,
  email,
  password, // hashed
  role, // 'student' | 'instructor' | 'admin'
  avatar, // Cloudinary URL
  bio,
  skills: [String],
  socialLinks: {
    website,
    github,
    linkedin,
    twitter
  },
  isEmailVerified,
  createdAt,
  updatedAt
}
```

### Auth & Profile APIs
| Method | Route | Description |
|--------|-------|-------------|
| POST   | `/api/auth/register`       | Register user              |
| POST   | `/api/auth/login`          | Login user                 |
| POST   | `/api/auth/forgot-password`| Send reset email           |
| POST   | `/api/auth/reset-password/:token` | Reset password       |
| GET    | `/api/auth/me`             | Get own profile            |
| PUT    | `/api/users/update-profile`| Update profile             |
| PUT    | `/api/users/update-password`| Change password           |
| PUT    | `/api/users/upload-avatar` | Upload user avatar         |

---

## 📘 2️⃣ COURSES

### Course Schema
```js
{
  _id,
  title,
  description,
  thumbnail, // Cloudinary URL
  category,
  price,
  level: 'beginner' | 'intermediate' | 'advanced',
  instructor: ObjectId,
  sections: [{
    title,
    videos: [{
      title,
      videoUrl,
      duration
    }]
  }],
  enrolledStudents: [ObjectId],
  ratings: [{
    userId,
    rating,
    review
  }],
  averageRating,
  totalRatings,
  isApproved,
  createdAt,
  updatedAt
}
```

### Course APIs
| Method | Route | Description |
|--------|-------|-------------|
| POST   | `/api/courses`           | Create a new course *(instructor only)* |
| GET    | `/api/courses`           | Get all courses (search, pagination, filter) |
| GET    | `/api/courses/:id`       | Get single course by ID                    |
| PUT    | `/api/courses/:id`       | Update course *(owner only)*              |
| DELETE | `/api/courses/:id`       | Delete course *(owner/admin)*             |
| POST   | `/api/courses/:id/rate`  | Add/Update rating & review *(students only)* |

---

## 📝 3️⃣ ENROLLMENTS

### Enrollment Logic
- Only `students` can enroll
- Cannot enroll twice
- Handle payments for paid courses

### Enrollment APIs
| Method | Route | Description |
|--------|-------|-------------|
| POST   | `/api/enroll/:courseId`   | Enroll in a course         |
| GET    | `/api/enroll/my-courses` | Get all enrolled courses   |
| GET    | `/api/enroll/course/:id` | Check enrollment status    |

---

## 🔐 4️⃣ ADMIN CONTROLS

### Admin APIs
| Method | Route | Description |
|--------|-------|-------------|
| GET    | `/api/admin/users`         | Get all users           |
| PUT    | `/api/admin/users/:id/role`| Change user role        |
| DELETE | `/api/admin/users/:id`     | Delete user             |
| GET    | `/api/admin/courses`       | Get all courses         |
| PUT    | `/api/admin/courses/:id/approve` | Approve/decline course |

---

## 💬 5️⃣ MESSAGING (Optional)

### Message Schema
```js
{
  _id,
  sender: ObjectId,
  receiver: ObjectId,
  message,
  isRead,
  createdAt
}
```

### Messaging APIs
| Method | Route | Description |
|--------|-------|-------------|
| POST   | `/api/messages/:receiverId` | Send a message         |
| GET    | `/api/messages/inbox`      | Get all received messages |
| GET    | `/api/messages/sent`       | Get all sent messages  |

---

## 🎓 6️⃣ CERTIFICATES (Optional)

### Certificate APIs
| Method | Route | Description |
|--------|-------|-------------|
| GET    | `/api/certificates/:courseId` | Generate/download certificate |

---

## 💳 7️⃣ PAYMENTS (Advanced)

### Payment APIs (Stripe)
| Method | Route | Description |
|--------|-------|-------------|
| POST   | `/api/payments/checkout/:courseId` | Create Stripe checkout session |
| GET    | `/api/payments/history`           | Get payment history             |
| POST   | `/api/webhook`                    | Stripe webhook endpoint         |

---

## 📁 Suggested Folder Structure
```
/controllers
/models
/routes
/middleware
/utils
/config
/uploads
```

---

## 🔧 Optional Technologies
- **Stripe** – Payments
- **Cloudinary** – Media Uploads
- **Nodemailer** – Emails
- **Multer** – File uploads
- **JWT** – Authentication
- **Socket.IO** – Real-time messaging
- **Swagger** – API Documentation

---

> Want to start building? Begin with `Authentication` → then `Courses` → then `Enrollments`, etc. Happy Coding! 🚀

