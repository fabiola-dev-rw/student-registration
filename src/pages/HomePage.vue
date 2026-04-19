<script setup lang="ts">
import { useRouter } from 'vue-router'

const router = useRouter()
</script>

<template>
  <div class="home-page">
    <nav class="navbar">
      <div class="nav-container">
        <div class="logo">e-Training Portal</div>
        <ul class="nav-menu">
          <li><a href="#" @click="$router.push('/')" class="nav-link active">Home</a></li>
          <li><a href="#" @click="$router.push('/login')" class="nav-link">Admin Login</a></li>
          <li><a href="#" @click="$router.push('/register')" class="nav-link">Student Registration</a></li>
        </ul>
      </div>
    </nav>

    <section class="hero">
      <div class="hero-content">
        <h1>Welcome to e-Training Portal</h1>
        <p class="subtitle">Transform Your Skills, Build Your Future</p>
      </div>
    </section>

    <!-- School Introduction Section -->
    <section class="school-intro-section">
      <div class="container">
        <div class="school-intro-content">
          <div class="school-text">
            <h2>Welcome to Our Institution</h2>
            <p class="school-description">
              Founded with a vision to provide quality vocational and professional training, our institution has been serving the community for over a decade. We are committed to equipping students with practical skills and theoretical knowledge needed to succeed in their chosen trades and professions.
            </p>
            <div class="school-highlights">
              <div class="highlight-item">
                <span class="highlight-icon">🎯</span>
                <h4>Our Mission</h4>
                <p>To provide accessible, quality training that transforms lives and builds skilled professionals.</p>
              </div>
              <div class="highlight-item">
                <span class="highlight-icon">🌟</span>
                <h4>Our Vision</h4>
                <p>To be the leading training institute recognized for excellence, innovation, and student success.</p>
              </div>
              <div class="highlight-item">
                <span class="highlight-icon">✨</span>
                <h4>Our Values</h4>
                <p>Excellence, Integrity, Student-centered learning, and Continuous improvement in all we do.</p>
              </div>
            </div>
          </div>
          <div class="school-gallery">
            <div class="school-image main-image">
              <span>🏫</span>
              <p>Main Campus Building</p>
            </div>
            <div class="school-images-grid">
              <div class="school-image">
                <span>📚</span>
                <p>Library</p>
              </div>
              <div class="school-image">
                <span>💻</span>
                <p>Computer Lab</p>
              </div>
              <div class="school-image">
                <span>🔬</span>
                <p>Science Lab</p>
              </div>
              <div class="school-image">
                <span>🎓</span>
                <p>Lecture Hall</p>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>

    <section class="intro-section">
      <div class="container">
        <h2>About Our Platform</h2>
        <p class="intro-text">
          Our e-Training Portal is a comprehensive platform designed to connect educators and students in a digital learning environment. Whether you're looking to expand your knowledge or manage educational programs, our platform provides the tools you need.
        </p>

        <div class="features">
          <div class="feature-card">
            <div class="feature-icon">📚</div>
            <h3>For Students</h3>
            <p>Register easily, access course materials, and track your learning progress all in one place.</p>
            <button @click="$router.push('/register')" class="btn btn-primary">
              Get Started
            </button>
          </div>

          <div class="feature-card">
            <div class="feature-icon">👨‍💼</div>
            <h3>For Administrators</h3>
            <p>Manage student registrations, review applications, and oversee all training programs efficiently.</p>
            <button @click="$router.push('/login')" class="btn btn-secondary">
              Admin Login
            </button>
          </div>

          <div class="feature-card">
            <div class="feature-icon">✓</div>
            <h3>Key Features</h3>
            <p>Secure authentication, easy registration, application tracking, and comprehensive dashboards.</p>
          </div>
        </div>
      </div>
    </section>

    <!-- Students Examination Section -->
    <section class="exam-section">
      <div class="container">
        <h2>Students Examination</h2>
        <p class="section-subtitle">Our students excel in comprehensive examinations across various disciplines</p>
        
        <div class="exam-gallery">
          <div class="exam-card">
            <div class="exam-image">📖</div>
            <h3>Written Examination</h3>
            <p>Students complete comprehensive written assessments to evaluate theoretical knowledge and understanding.</p>
          </div>

          <div class="exam-card">
            <div class="exam-image">💻</div>
            <h3>Practical Examination</h3>
            <p>Hands-on practical exams test real-world application skills and technical competencies.</p>
          </div>

          <div class="exam-card">
            <div class="exam-image">🎓</div>
            <h3>Online Assessment</h3>
            <p>Interactive online examinations with immediate feedback to enhance learning outcomes.</p>
          </div>

          <div class="exam-card">
            <div class="exam-image">🏆</div>
            <h3>Certification</h3>
            <p>Students receive recognized certifications upon successful completion of examinations.</p>
          </div>
        </div>

        <div class="exam-stats">
          <div class="stat-item">
            <div class="stat-number">95%</div>
            <div class="stat-text">Pass Rate</div>
          </div>
          <div class="stat-item">
            <div class="stat-number">5000+</div>
            <div class="stat-text">Students Certified</div>
          </div>
          <div class="stat-item">
            <div class="stat-number">50+</div>
            <div class="stat-text">Courses Available</div>
          </div>
          <div class="stat-item">
            <div class="stat-number">10+</div>
            <div class="stat-text">Years Experience</div>
          </div>
        </div>
      </div>
    </section>

    <!-- Student Gallery Section -->
    <section class="gallery-section">
      <div class="container">
        <h2>Our Students</h2>
        <p class="section-subtitle">Meet our talented and dedicated students achieving excellence</p>
        
        <div class="student-gallery">
          <div class="student-card">
            <div class="student-image">👨‍🎓</div>
            <h3>John Doe</h3>
            <p class="student-trade">Information Technology</p>
            <p class="student-status">Certified - Web Developer</p>
          </div>

          <div class="student-card">
            <div class="student-image">👩‍🎓</div>
            <h3>Sarah Smith</h3>
            <p class="student-trade">Business & Management</p>
            <p class="student-status">Certified - Project Manager</p>
          </div>

          <div class="student-card">
            <div class="student-image">👨‍💼</div>
            <h3>Michael Brown</h3>
            <p class="student-trade">Engineering</p>
            <p class="student-status">Certified - Software Engineer</p>
          </div>

          <div class="student-card">
            <div class="student-image">👩‍⚕️</div>
            <h3>Emma Wilson</h3>
            <p class="student-trade">Healthcare</p>
            <p class="student-status">Certified - Healthcare Professional</p>
          </div>

          <div class="student-card">
            <div class="student-image">👨‍🔧</div>
            <h3>David Johnson</h3>
            <p class="student-trade">Electrical & Electronics</p>
            <p class="student-status">Certified - Technician</p>
          </div>

          <div class="student-card">
            <div class="student-image">👩‍🍳</div>
            <h3>Lisa Anderson</h3>
            <p class="student-trade">Culinary Arts</p>
            <p class="student-status">Certified - Chef</p>
          </div>

          <div class="student-card">
            <div class="student-image">👨‍🌾</div>
            <h3>James Taylor</h3>
            <p class="student-trade">Agriculture</p>
            <p class="student-status">Certified - Specialist</p>
          </div>

          <div class="student-card">
            <div class="student-image">👩‍💻</div>
            <h3>Rachel Lee</h3>
            <p class="student-trade">Information Technology</p>
            <p class="student-status">Certified - Data Analyst</p>
          </div>
        </div>
      </div>
    </section>

    <section class="cta-section">
      <div class="container">
        <h2>Ready to Get Started?</h2>
        <p>Join our platform and begin your learning journey today</p>
        <button @click="$router.push('/register')" class="btn btn-large">
          Register as Student
        </button>
      </div>
    </section>

    <footer class="footer">
      <p>&copy; 2026 e-Training Portal. All rights reserved.</p>
    </footer>
  </div>
</template>

<style scoped>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

.home-page {
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
  color: #333;
}

/* Navbar */
.navbar {
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  padding: 1rem 0;
  box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
  position: sticky;
  top: 0;
  z-index: 100;
}

.nav-container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 2rem;
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.logo {
  font-size: 1.8rem;
  font-weight: bold;
  color: white;
}

.nav-menu {
  display: flex;
  list-style: none;
  gap: 2rem;
}

.nav-link {
  color: white;
  text-decoration: none;
  transition: opacity 0.3s ease;
  font-weight: 500;
  cursor: pointer;
}

.nav-link:hover,
.nav-link.active {
  opacity: 0.8;
  text-decoration: underline;
}

/* Hero Section */
.hero {
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  color: white;
  padding: 6rem 2rem;
  text-align: center;
}

.hero-content h1 {
  font-size: 3rem;
  margin-bottom: 1rem;
  animation: slideDown 0.8s ease;
}

.subtitle {
  font-size: 1.5rem;
  opacity: 0.9;
  animation: slideUp 0.8s ease;
}

@keyframes slideDown {
  from {
    opacity: 0;
    transform: translateY(-30px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

@keyframes slideUp {
  from {
    opacity: 0;
    transform: translateY(30px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

/* School Introduction Section */
.school-intro-section {
  background: linear-gradient(135deg, #f5f7fa 0%, #c3cfe2 100%);
  padding: 4rem 2rem;
}

.school-intro-content {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 3rem;
  align-items: center;
}

.school-text h2 {
  font-size: 2.5rem;
  color: #667eea;
  margin-bottom: 1.5rem;
}

.school-description {
  font-size: 1.1rem;
  color: #555;
  line-height: 1.8;
  margin-bottom: 2rem;
  text-align: justify;
}

.school-highlights {
  display: grid;
  grid-template-columns: 1fr;
  gap: 1.5rem;
}

.highlight-item {
  background: white;
  padding: 1.5rem;
  border-radius: 8px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
  border-left: 4px solid #667eea;
}

.highlight-icon {
  font-size: 2rem;
  display: block;
  margin-bottom: 0.5rem;
}

.highlight-item h4 {
  color: #667eea;
  margin-bottom: 0.5rem;
  font-size: 1.1rem;
}

.highlight-item p {
  color: #666;
  font-size: 0.95rem;
  line-height: 1.5;
}

/* School Gallery */
.school-gallery {
  display: flex;
  flex-direction: column;
  gap: 1.5rem;
}

.main-image {
  grid-column: 1 / -1;
  min-height: 300px;
}

.school-image {
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  padding: 2rem;
  border-radius: 10px;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  text-align: center;
  color: white;
  box-shadow: 0 4px 15px rgba(102, 126, 234, 0.3);
  transition: transform 0.3s ease, box-shadow 0.3s ease;
  min-height: 180px;
}

.school-image:hover {
  transform: translateY(-5px);
  box-shadow: 0 8px 25px rgba(102, 126, 234, 0.4);
}

.school-image span {
  font-size: 3rem;
  margin-bottom: 1rem;
  display: inline-block;
}

.school-image p {
  font-size: 1.1rem;
  font-weight: 600;
}

.school-images-grid {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  gap: 1rem;
}

.school-images-grid .school-image {
  min-height: 140px;
  padding: 1.5rem;
}

.school-images-grid .school-image span {
  font-size: 2.5rem;
}

.school-images-grid .school-image p {
  font-size: 0.95rem;
}

/* Intro Section */
.intro-section {
  padding: 4rem 2rem;
  background: #f8f9fa;
}

.container {
  max-width: 1200px;
  margin: 0 auto;
}

.intro-section h2 {
  text-align: center;
  font-size: 2.5rem;
  margin-bottom: 2rem;
  color: #667eea;
}

.intro-text {
  text-align: center;
  font-size: 1.1rem;
  line-height: 1.6;
  margin-bottom: 3rem;
  color: #555;
  max-width: 800px;
  margin-left: auto;
  margin-right: auto;
}

.features {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
  gap: 2rem;
}

.feature-card {
  background: white;
  padding: 2rem;
  border-radius: 10px;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
  text-align: center;
  transition: transform 0.3s ease, box-shadow 0.3s ease;
}

.feature-card:hover {
  transform: translateY(-5px);
  box-shadow: 0 8px 12px rgba(0, 0, 0, 0.15);
}

.feature-icon {
  font-size: 3rem;
  margin-bottom: 1rem;
}

.feature-card h3 {
  font-size: 1.5rem;
  margin-bottom: 1rem;
  color: #667eea;
}

.feature-card p {
  color: #666;
  line-height: 1.6;
  margin-bottom: 1.5rem;
}

/* Buttons */
.btn {
  padding: 0.75rem 1.5rem;
  border: none;
  border-radius: 5px;
  font-size: 1rem;
  cursor: pointer;
  transition: all 0.3s ease;
  font-weight: 600;
}

.btn-primary {
  background-color: #667eea;
  color: white;
}

.btn-primary:hover {
  background-color: #5568d3;
}

.btn-secondary {
  background-color: #764ba2;
  color: white;
}

.btn-secondary:hover {
  background-color: #63408b;
}

.btn-large {
  padding: 1rem 2rem;
  font-size: 1.1rem;
}

/* CTA Section */
.cta-section {
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  color: white;
  padding: 4rem 2rem;
  text-align: center;
}

.cta-section h2 {
  font-size: 2.5rem;
  margin-bottom: 1rem;
}

.cta-section p {
  font-size: 1.2rem;
  margin-bottom: 2rem;
  opacity: 0.9;
}

.cta-section .btn-large {
  background-color: white;
  color: #667eea;
}

.cta-section .btn-large:hover {
  background-color: #f0f0f0;
}

/* Examination Section */
.exam-section {
  background: #f8f9fa;
  padding: 4rem 2rem;
}

.exam-section h2 {
  text-align: center;
  font-size: 2.5rem;
  color: #667eea;
  margin-bottom: 1rem;
}

.section-subtitle {
  text-align: center;
  font-size: 1.1rem;
  color: #666;
  margin-bottom: 3rem;
}

.exam-gallery {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
  gap: 2rem;
  margin-bottom: 3rem;
}

.exam-card {
  background: white;
  padding: 2rem;
  border-radius: 10px;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
  text-align: center;
  transition: transform 0.3s ease, box-shadow 0.3s ease;
  border-top: 4px solid #667eea;
}

.exam-card:hover {
  transform: translateY(-5px);
  box-shadow: 0 8px 12px rgba(0, 0, 0, 0.15);
}

.exam-image {
  font-size: 3.5rem;
  margin-bottom: 1rem;
  display: inline-block;
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
}

.exam-card h3 {
  font-size: 1.3rem;
  color: #333;
  margin-bottom: 1rem;
}

.exam-card p {
  color: #666;
  line-height: 1.6;
  font-size: 0.95rem;
}

/* Exam Stats */
.exam-stats {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(150px, 1fr));
  gap: 2rem;
  background: white;
  padding: 2rem;
  border-radius: 10px;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
}

.stat-item {
  text-align: center;
}

.stat-number {
  font-size: 2.5rem;
  font-weight: bold;
  color: #667eea;
  margin-bottom: 0.5rem;
}

.stat-text {
  color: #666;
  font-size: 1rem;
}

/* Student Gallery Section */
.gallery-section {
  background: white;
  padding: 4rem 2rem;
}

.gallery-section h2 {
  text-align: center;
  font-size: 2.5rem;
  color: #667eea;
  margin-bottom: 1rem;
}

.student-gallery {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
  gap: 2rem;
  margin-top: 3rem;
}

.student-card {
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  padding: 2rem;
  border-radius: 10px;
  text-align: center;
  box-shadow: 0 4px 15px rgba(0, 0, 0, 0.1);
  transition: transform 0.3s ease, box-shadow 0.3s ease;
  color: white;
}

.student-card:hover {
  transform: translateY(-10px);
  box-shadow: 0 8px 25px rgba(102, 126, 234, 0.3);
}

.student-image {
  font-size: 4rem;
  margin-bottom: 1rem;
  display: inline-block;
  animation: float 3s ease-in-out infinite;
}

@keyframes float {
  0%, 100% {
    transform: translateY(0px);
  }
  50% {
    transform: translateY(-10px);
  }
}

.student-card h3 {
  font-size: 1.3rem;
  margin-bottom: 0.5rem;
  font-weight: 600;
}

.student-trade {
  font-size: 0.95rem;
  opacity: 0.9;
  margin-bottom: 0.5rem;
  font-weight: 500;
}

.student-status {
  font-size: 0.85rem;
  opacity: 0.8;
  font-style: italic;
}

/* Footer */
.footer {
  background-color: #333;
  color: white;
  text-align: center;
  padding: 2rem;
}

@media (max-width: 1024px) {
  .nav-container {
    flex-wrap: wrap;
  }

  .nav-menu {
    gap: 1rem;
    flex-wrap: wrap;
  }

  .school-intro-content {
    grid-template-columns: 1fr;
    gap: 2rem;
  }
}

@media (max-width: 768px) {
  .nav-menu {
    gap: 0.5rem;
    font-size: 0.85rem;
  }

  .logo {
    font-size: 1.3rem;
  }

  .hero {
    padding: 4rem 1rem;
  }

  .hero-content h1 {
    font-size: 1.8rem;
  }

  .subtitle {
    font-size: 1rem;
  }

  .intro-section {
    padding: 2rem 1rem;
  }

  .intro-section h2 {
    font-size: 1.5rem;
  }

  .intro-text {
    font-size: 1rem;
  }

  .features {
    grid-template-columns: 1fr;
    gap: 1rem;
  }

  .feature-card {
    padding: 1.5rem;
  }

  .feature-icon {
    font-size: 2rem;
  }

  .school-intro-section {
    padding: 2rem 1rem;
  }

  .school-intro-content {
    grid-template-columns: 1fr;
    gap: 1.5rem;
  }

  .school-text h2 {
    font-size: 1.8rem;
  }

  .school-description {
    font-size: 1rem;
  }

  .school-highlights {
    gap: 1rem;
  }

  .highlight-item {
    padding: 1rem;
  }

  .highlight-icon {
    font-size: 1.5rem;
  }

  .highlight-item h4 {
    font-size: 1rem;
  }

  .highlight-item p {
    font-size: 0.9rem;
  }

  .main-image {
    min-height: 200px;
  }

  .school-image {
    min-height: 140px;
    padding: 1.5rem;
  }

  .school-image span {
    font-size: 2.5rem;
  }

  .school-image p {
    font-size: 1rem;
  }

  .cta-section {
    padding: 2rem 1rem;
  }

  .cta-section h2 {
    font-size: 1.5rem;
  }

  .cta-section p {
    font-size: 1rem;
  }
}

@media (max-width: 480px) {
  .nav-container {
    flex-direction: column;
    gap: 0.5rem;
  }

  .logo {
    font-size: 1.1rem;
  }

  .nav-menu {
    flex-direction: column;
    gap: 0.3rem;
    width: 100%;
  }

  .nav-link {
    font-size: 0.8rem;
  }

  .hero {
    padding: 3rem 1rem;
  }

  .hero-content h1 {
    font-size: 1.4rem;
  }

  .subtitle {
    font-size: 0.9rem;
  }

  .intro-text {
    font-size: 0.9rem;
  }

  .feature-card {
    padding: 1rem;
  }

  .feature-card h3 {
    font-size: 1.2rem;
  }

  .feature-card p {
    font-size: 0.9rem;
  }

  .btn {
    padding: 0.6rem 1rem;
    font-size: 0.9rem;
  }

  .exam-section {
    padding: 2rem 1rem;
  }

  .exam-section h2 {
    font-size: 1.8rem;
  }

  .section-subtitle {
    font-size: 1rem;
    margin-bottom: 2rem;
  }

  .exam-gallery {
    gap: 1rem;
    margin-bottom: 2rem;
  }

  .exam-card {
    padding: 1.5rem;
    border-top: 3px solid #667eea;
  }

  .exam-image {
    font-size: 2.5rem;
  }

  .exam-card h3 {
    font-size: 1.1rem;
  }

  .exam-card p {
    font-size: 0.9rem;
  }

  .exam-stats {
    grid-template-columns: repeat(2, 1fr);
    gap: 1rem;
    padding: 1.5rem;
  }

  .stat-number {
    font-size: 2rem;
  }

  .stat-text {
    font-size: 0.9rem;
  }

  .gallery-section {
    padding: 2rem 1rem;
  }

  .gallery-section h2 {
    font-size: 1.8rem;
  }

  .student-gallery {
    grid-template-columns: repeat(2, 1fr);
    gap: 1.5rem;
    margin-top: 2rem;
  }

  .student-card {
    padding: 1.5rem;
  }

  .student-image {
    font-size: 3rem;
  }

  .student-card h3 {
    font-size: 1.1rem;
  }

  .student-trade {
    font-size: 0.9rem;
  }

  .student-status {
    font-size: 0.8rem;
  }

  .footer {
    padding: 1rem;
    font-size: 0.85rem;
  }
}

@media (max-width: 480px) {
  .nav-container {
    flex-direction: column;
    gap: 0.5rem;
  }

  .logo {
    font-size: 1.1rem;
  }

  .nav-menu {
    flex-direction: column;
    gap: 0.3rem;
    width: 100%;
  }

  .nav-link {
    font-size: 0.8rem;
  }

  .hero {
    padding: 3rem 1rem;
  }

  .hero-content h1 {
    font-size: 1.4rem;
  }

  .subtitle {
    font-size: 0.9rem;
  }

  .school-intro-section {
    padding: 1.5rem 1rem;
  }

  .school-intro-content {
    grid-template-columns: 1fr;
    gap: 1rem;
  }

  .school-text h2 {
    font-size: 1.5rem;
  }

  .school-description {
    font-size: 0.95rem;
  }

  .school-highlights {
    gap: 1rem;
  }

  .highlight-item {
    padding: 1rem;
  }

  .highlight-icon {
    font-size: 1.5rem;
  }

  .highlight-item h4 {
    font-size: 0.95rem;
  }

  .highlight-item p {
    font-size: 0.85rem;
  }

  .school-gallery {
    gap: 1rem;
  }

  .main-image {
    min-height: 150px;
  }

  .school-image {
    min-height: 120px;
    padding: 1rem;
  }

  .school-image span {
    font-size: 2rem;
  }

  .school-image p {
    font-size: 0.9rem;
  }

  .school-images-grid {
    grid-template-columns: repeat(2, 1fr);
    gap: 0.75rem;
  }

  .intro-text {
    font-size: 0.9rem;
  }

  .feature-card {
    padding: 1rem;
  }

  .feature-card h3 {
    font-size: 1.2rem;
  }

  .feature-card p {
    font-size: 0.9rem;
  }

  .btn {
    padding: 0.6rem 1rem;
    font-size: 0.9rem;
  }

  .exam-section {
    padding: 2rem 1rem;
  }

  .exam-section h2 {
    font-size: 1.8rem;
  }

  .section-subtitle {
    font-size: 1rem;
    margin-bottom: 2rem;
  }

  .exam-gallery {
    gap: 1rem;
    margin-bottom: 2rem;
  }

  .exam-card {
    padding: 1.5rem;
    border-top: 3px solid #667eea;
  }

  .exam-image {
    font-size: 2.5rem;
  }

  .exam-card h3 {
    font-size: 1.1rem;
  }

  .exam-card p {
    font-size: 0.9rem;
  }

  .exam-stats {
    grid-template-columns: repeat(2, 1fr);
    gap: 1rem;
    padding: 1.5rem;
  }

  .stat-number {
    font-size: 2rem;
  }

  .stat-text {
    font-size: 0.9rem;
  }

  .gallery-section {
    padding: 2rem 1rem;
  }

  .gallery-section h2 {
    font-size: 1.8rem;
  }

  .student-gallery {
    grid-template-columns: repeat(2, 1fr);
    gap: 1.5rem;
    margin-top: 2rem;
  }

  .student-card {
    padding: 1.5rem;
  }

  .student-image {
    font-size: 3rem;
  }

  .student-card h3 {
    font-size: 1.1rem;
  }

  .student-trade {
    font-size: 0.9rem;
  }

  .student-status {
    font-size: 0.8rem;
  }

  .footer {
    padding: 1rem;
    font-size: 0.85rem;
  }
}
</style>
