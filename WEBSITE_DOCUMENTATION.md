# e-Training Portal

A comprehensive web application built with Vue 3 + TypeScript + Vite that allows students to register and administrators to review applications.

## Features

### 🏠 Home Page
- Beautiful introduction explaining what the website is about
- Navigation menu with links to all sections
- Feature highlights showcasing key capabilities
- Call-to-action buttons for students and admins
- Responsive design with smooth animations

### 👨‍🎓 Student Registration
- Comprehensive registration form with fields for:
  - Personal Information (name, email, phone, DOB, gender)
  - Address Information (address, city, state, zip code)
  - Education & Interests (education level, course interests)
- Form validation to ensure all required fields are filled
- Multiple course selection checkboxes
- Terms & conditions agreement requirement
- Success message upon submission
- Data stored in browser's localStorage
- Responsive form layout that works on all devices

### 🔐 Admin Login
- Secure login page for administrators
- Form validation for email and password
- Demo credentials for testing:
  - Email: `admin@etraining.com`
  - Password: `admin123`
- Session management with localStorage
- Protected routes that require authentication
- Redirect to login if session expires

### 📊 Admin Dashboard
- View all submitted student applications
- Statistics showing:
  - Total applications
  - Pending reviews
  - Approved applications
  - Rejected applications
- Filter applications by status (All, Pending, Approved, Rejected)
- View detailed application information in a modal
- Approve or reject applications
- Track review timestamps
- Secure logout functionality
- Responsive admin interface

## Project Structure

```
src/
├── pages/
│   ├── HomePage.vue          # Home/landing page
│   ├── LoginPage.vue         # Admin login page
│   ├── RegistrationPage.vue  # Student registration form
│   └── AdminDashboard.vue    # Admin dashboard
├── router/
│   └── index.ts              # Vue Router configuration
├── App.vue                   # Root component
├── main.ts                   # Application entry point
└── assets/
    ├── main.css              # Global styles
    └── base.css              # Base styles
```

## Getting Started

### Prerequisites
- Node.js 20.19.0 or higher
- npm or yarn

### Installation

1. Install dependencies:
```bash
npm install
```

2. Start the development server:
```bash
npm run dev
```

3. Open your browser and navigate to `http://localhost:5174/`

### Building for Production

```bash
npm run build
```

This will create an optimized production build in the `dist/` directory.

## Usage

### For Students
1. Visit the home page
2. Click on "Student Registration" button
3. Fill in all required information (marked with *)
4. Select interested courses
5. Agree to terms and conditions
6. Submit the form
7. Success message will appear

### For Administrators
1. Visit the home page
2. Click on "Admin Login" button
3. Use credentials:
   - Email: `admin@etraining.com`
   - Password: `admin123`
4. View submitted applications in the dashboard
5. Click "View Details" to see full application
6. Approve or reject applications as needed
7. Use the filter to view applications by status

## Technologies Used

- **Vue 3**: Progressive JavaScript framework
- **TypeScript**: Static typing for JavaScript
- **Vite**: Next generation frontend build tool
- **Vue Router**: Official router for Vue.js
- **CSS3**: Modern styling with animations

## Features Overview

### State Management
- Uses Vue's reactive system with `ref()` for local state
- Browser's localStorage for persistence between sessions
- Simple authentication system with session storage

### Routing
- Hash-based routing for easy deployment
- Protected routes for admin dashboard
- Navigation guards for authentication checks
- Smooth page transitions

### Data Persistence
- Student registrations stored in localStorage
- Admin login state managed with localStorage
- Data persists across browser sessions (can be cleared manually)

## Browser Compatibility

- Chrome (latest)
- Firefox (latest)
- Safari (latest)
- Edge (latest)

## Demo Credentials

**Admin Login:**
- Email: `admin@etraining.com`
- Password: `admin123`

## Notes

- This is a frontend demonstration application
- Data is stored in browser localStorage (not persistent)
- For production, integrate with a backend API
- Implement proper authentication with JWT tokens
- Add server-side validation and security measures
- Use a proper database for data persistence

## Future Enhancements

- Backend API integration
- User authentication with JWT
- Email notifications for applications
- Application status updates
- Student profile management
- Admin analytics and reports
- Course management interface
- Payment integration
- User password reset functionality
- Two-factor authentication

## License

This project is part of the e-Training Portal initiative.
