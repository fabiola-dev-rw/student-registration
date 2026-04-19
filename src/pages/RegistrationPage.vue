<script setup lang="ts">
import { ref } from 'vue'
import { useRouter } from 'vue-router'

const router = useRouter()

interface FormData {
  firstName: string
  lastName: string
  email: string
  phone: string
  dateOfBirth: string
  gender: string
  province: string
  district: string
  sector: string
  cell: string
  educationLevel: string
  trade: string
  coursesInterested: string[]
  agreeToTerms: boolean
}

const formData = ref<FormData>({
  firstName: '',
  lastName: '',
  email: '',
  phone: '',
  dateOfBirth: '',
  gender: '',
  province: '',
  district: '',
  sector: '',
  cell: '',
  educationLevel: '',
  trade: '',
  coursesInterested: [],
  agreeToTerms: false
})

const submitted = ref(false)
const submitSuccess = ref(false)
const error = ref('')

const courses = [
  'Web Development',
  'Data Science',
  'UI/UX Design',
  'Mobile Development',
  'Cloud Computing',
  'Machine Learning'
]

const handleSubmit = () => {
  error.value = ''
  submitted.value = true

  // Validate required fields
  if (!formData.value.firstName || !formData.value.lastName || !formData.value.email) {
    error.value = 'Please fill in all required fields (marked with *)'
    return
  }

  if (!formData.value.agreeToTerms) {
    error.value = 'Please agree to the terms and conditions'
    return
  }

  // Store in localStorage (for demo purposes)
  const submissions = JSON.parse(localStorage.getItem('studentSubmissions') || '[]')
  submissions.push({
    id: Date.now(),
    ...formData.value,
    submittedAt: new Date().toLocaleString()
  })
  localStorage.setItem('studentSubmissions', JSON.stringify(submissions))

  submitSuccess.value = true

  // Redirect after 2 seconds
  setTimeout(() => {
    router.push('/')
  }, 2000)
}

const handleToggleCourse = (course: string) => {
  const index = formData.value.coursesInterested.indexOf(course)
  if (index > -1) {
    formData.value.coursesInterested.splice(index, 1)
  } else {
    formData.value.coursesInterested.push(course)
  }
}

const handleBackToHome = () => {
  router.push('/')
}
</script>

<template>
  <div class="registration-page">
    <nav class="navbar">
      <div class="nav-container">
        <div class="logo">e-Training Portal</div>
        <div class="back-link" @click="handleBackToHome">← Back to Home</div>
      </div>
    </nav>

    <div class="registration-container">
      <div class="registration-card" v-if="!submitSuccess">
        <h1>Student Registration</h1>
        <p class="subtitle">Join our platform and start your learning journey</p>

        <form @submit.prevent="handleSubmit" class="registration-form">
          <div v-if="error" class="alert alert-error">
            {{ error }}
          </div>

          <!-- Personal Information Section -->
          <div class="form-section">
            <h2>Personal Information</h2>

            <div class="form-row">
              <div class="form-group">
                <label for="firstName">First Name <span class="required">*</span></label>
                <input
                  id="firstName"
                  v-model="formData.firstName"
                  type="text"
                  placeholder="Enter your first name"
                  required
                />
              </div>

              <div class="form-group">
                <label for="lastName">Last Name <span class="required">*</span></label>
                <input
                  id="lastName"
                  v-model="formData.lastName"
                  type="text"
                  placeholder="Enter your last name"
                  required
                />
              </div>
            </div>

            <div class="form-row">
              <div class="form-group">
                <label for="email">Email Address <span class="required">*</span></label>
                <input
                  id="email"
                  v-model="formData.email"
                  type="email"
                  placeholder="Enter your email"
                  required
                />
              </div>

              <div class="form-group">
                <label for="phone">Phone Number</label>
                <input
                  id="phone"
                  v-model="formData.phone"
                  type="tel"
                  placeholder="Enter your phone number"
                />
              </div>
            </div>

            <div class="form-row">
              <div class="form-group">
                <label for="dateOfBirth">Date of Birth</label>
                <input
                  id="dateOfBirth"
                  v-model="formData.dateOfBirth"
                  type="date"
                />
              </div>

              <div class="form-group">
                <label for="gender">Gender</label>
                <select id="gender" v-model="formData.gender">
                  <option value="">Select Gender</option>
                  <option value="male">Male</option>
                  <option value="female">Female</option>
                  <option value="other">Other</option>
                </select>
              </div>
            </div>
          </div>

          <!-- Address Information Section -->
          <div class="form-section">
            <h2>Address Information</h2>

            <div class="form-row">
              <div class="form-group">
                <label for="province">Province</label>
                <input
                  id="province"
                  v-model="formData.province"
                  type="text"
                  placeholder="Enter your province"
                />
              </div>

              <div class="form-group">
                <label for="district">District</label>
                <input
                  id="district"
                  v-model="formData.district"
                  type="text"
                  placeholder="Enter your district"
                />
              </div>
            </div>

            <div class="form-row">
              <div class="form-group">
                <label for="sector">Sector</label>
                <input
                  id="sector"
                  v-model="formData.sector"
                  type="text"
                  placeholder="Enter your sector"
                />
              </div>

              <div class="form-group">
                <label for="cell">Cell</label>
                <input
                  id="cell"
                  v-model="formData.cell"
                  type="text"
                  placeholder="Enter your cell"
                />
              </div>
            </div>
          </div>

          <!-- Education & Interests Section -->
          <div class="form-section">
            <h2>Education & Interests</h2>

            <div class="form-row">
              <div class="form-group">
                <label for="educationLevel">Education Level</label>
                <select id="educationLevel" v-model="formData.educationLevel">
                  <option value="">Select Education Level</option>
                  <option value="high-school">High School</option>
                  <option value="bachelor">Bachelor's Degree</option>
                  <option value="master">Master's Degree</option>
                  <option value="phd">PhD</option>
                  <option value="other">Other</option>
                </select>
              </div>

              <div class="form-group">
                <label for="trade">Trade/Field of Study</label>
                <select id="trade" v-model="formData.trade">
                  <option value="">Select Trade/Field</option>
                  <option value="information-technology">Information Technology</option>
                  <option value="business">Business & Management</option>
                  <option value="engineering">Engineering</option>
                  <option value="healthcare">Healthcare</option>
                  <option value="agriculture">Agriculture</option>
                  <option value="hospitality">Hospitality & Tourism</option>
                  <option value="construction">Construction & Building</option>
                  <option value="automotive">Automotive</option>
                  <option value="electrical">Electrical & Electronics</option>
                  <option value="plumbing">Plumbing & HVAC</option>
                  <option value="beauty">Beauty & Wellness</option>
                  <option value="culinary">Culinary Arts</option>
                  <option value="other">Other</option>
                </select>
              </div>
            </div>

            <div class="form-group">
              <label>Courses Interested In</label>
              <div class="checkbox-group">
                <div v-for="course in courses" :key="course" class="checkbox-item">
                  <input
                    :id="course"
                    type="checkbox"
                    :checked="formData.coursesInterested.includes(course)"
                    @change="handleToggleCourse(course)"
                  />
                  <label :for="course">{{ course }}</label>
                </div>
              </div>
            </div>
          </div>

          <!-- Terms & Conditions -->
          <div class="form-section">
            <div class="form-group checkbox">
              <input
                id="agreeToTerms"
                v-model="formData.agreeToTerms"
                type="checkbox"
              />
              <label for="agreeToTerms">
                I agree to the terms and conditions <span class="required">*</span>
              </label>
            </div>
          </div>

          <button type="submit" class="btn btn-submit">
            Submit Registration
          </button>
        </form>
      </div>

      <div class="success-message" v-else>
        <div class="success-icon">✓</div>
        <h1>Registration Successful!</h1>
        <p>Thank you for registering. Your application has been submitted successfully.</p>
        <p class="redirect-message">You will be redirected to the home page in 2 seconds...</p>
      </div>
    </div>
  </div>
</template>

<style scoped>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

.registration-page {
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  min-height: 100vh;
  padding-bottom: 2rem;
}

/* Navbar */
.navbar {
  background: rgba(0, 0, 0, 0.1);
  padding: 1rem 0;
  backdrop-filter: blur(10px);
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
  font-size: 1.5rem;
  font-weight: bold;
  color: white;
}

.back-link {
  color: white;
  cursor: pointer;
  text-decoration: none;
  font-weight: 500;
  transition: opacity 0.3s ease;
}

.back-link:hover {
  opacity: 0.8;
}

/* Registration Container */
.registration-container {
  max-width: 900px;
  margin: 2rem auto;
  padding: 0 2rem;
}

.registration-card {
  background: white;
  padding: 3rem;
  border-radius: 15px;
  box-shadow: 0 10px 40px rgba(0, 0, 0, 0.2);
}

.registration-card h1 {
  font-size: 2rem;
  color: #667eea;
  margin-bottom: 0.5rem;
  text-align: center;
}

.subtitle {
  color: #666;
  text-align: center;
  margin-bottom: 2rem;
}

/* Form */
.registration-form {
  margin-top: 2rem;
}

/* Alert */
.alert {
  padding: 1rem;
  border-radius: 5px;
  margin-bottom: 2rem;
  text-align: center;
}

.alert-error {
  background-color: #ffe0e0;
  color: #d32f2f;
  border: 1px solid #d32f2f;
}

/* Form Sections */
.form-section {
  margin-bottom: 2.5rem;
}

.form-section h2 {
  font-size: 1.3rem;
  color: #667eea;
  margin-bottom: 1.5rem;
  padding-bottom: 0.5rem;
  border-bottom: 2px solid #e0e0e0;
}

/* Form Group */
.form-group {
  margin-bottom: 1.5rem;
}

.form-group label {
  display: block;
  margin-bottom: 0.5rem;
  color: #333;
  font-weight: 600;
  font-size: 0.95rem;
}

.required {
  color: #d32f2f;
}

.form-group input,
.form-group select,
.form-group textarea {
  width: 100%;
  padding: 0.75rem;
  border: 2px solid #e0e0e0;
  border-radius: 5px;
  font-size: 1rem;
  transition: border-color 0.3s ease;
  font-family: inherit;
}

.form-group input:focus,
.form-group select:focus,
.form-group textarea:focus {
  outline: none;
  border-color: #667eea;
}

.form-group input::placeholder,
.form-group textarea::placeholder {
  color: #999;
}

/* Form Row */
.form-row {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
  gap: 1.5rem;
  margin-bottom: 0;
}

.form-row .form-group {
  margin-bottom: 0;
}

/* Checkbox Group */
.checkbox-group {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
  gap: 1rem;
  margin-top: 1rem;
}

.checkbox-item {
  display: flex;
  align-items: center;
}

.checkbox-item input[type='checkbox'] {
  width: auto;
  margin-right: 0.5rem;
  cursor: pointer;
}

.checkbox-item label {
  margin: 0;
  font-weight: 500;
  cursor: pointer;
}

/* Checkbox */
.form-group.checkbox {
  display: flex;
  align-items: center;
  margin-bottom: 2rem;
}

.form-group.checkbox input[type='checkbox'] {
  width: auto;
  margin-right: 1rem;
  cursor: pointer;
  width: 20px;
  height: 20px;
}

.form-group.checkbox label {
  margin: 0;
  font-weight: 500;
  cursor: pointer;
}

/* Button */
.btn {
  padding: 0.75rem 2rem;
  border: none;
  border-radius: 5px;
  font-size: 1rem;
  cursor: pointer;
  font-weight: 600;
  transition: all 0.3s ease;
}

.btn-submit {
  width: 100%;
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  color: white;
  padding: 1rem;
}

.btn-submit:hover {
  transform: translateY(-2px);
  box-shadow: 0 5px 15px rgba(102, 126, 234, 0.4);
}

/* Success Message */
.success-message {
  background: white;
  padding: 3rem 2rem;
  border-radius: 15px;
  box-shadow: 0 10px 40px rgba(0, 0, 0, 0.2);
  text-align: center;
  max-width: 500px;
  margin: 0 auto;
}

.success-icon {
  font-size: 4rem;
  color: #4caf50;
  margin-bottom: 1rem;
  animation: bounce 0.6s ease;
}

@keyframes bounce {
  0% {
    transform: scale(0);
  }
  50% {
    transform: scale(1.1);
  }
  100% {
    transform: scale(1);
  }
}

.success-message h1 {
  color: #4caf50;
  margin-bottom: 1rem;
}

.success-message p {
  color: #666;
  line-height: 1.6;
  margin-bottom: 1rem;
}

.redirect-message {
  color: #999;
  font-size: 0.9rem;
  font-style: italic;
}

@media (max-width: 1024px) {
  .registration-card {
    padding: 2.5rem;
  }
}

@media (max-width: 768px) {
  .navbar {
    padding: 0.75rem 0;
  }

  .nav-container {
    padding: 0 1rem;
  }

  .logo {
    font-size: 1.2rem;
  }

  .registration-container {
    padding: 1rem;
  }

  .registration-card {
    padding: 1.5rem;
  }

  .registration-card h1 {
    font-size: 1.5rem;
    margin-bottom: 0.25rem;
  }

  .subtitle {
    font-size: 0.95rem;
  }

  .form-section {
    margin-bottom: 1.5rem;
  }

  .form-section h2 {
    font-size: 1.1rem;
    margin-bottom: 1rem;
  }

  .form-row {
    grid-template-columns: 1fr;
    gap: 1rem;
  }

  .form-row .form-group {
    margin-bottom: 0;
  }

  .form-group {
    margin-bottom: 1rem;
  }

  .form-group label {
    font-size: 0.9rem;
  }

  .form-group input,
  .form-group select {
    font-size: 16px; /* Prevents zoom on iOS */
    padding: 0.65rem;
  }

  .checkbox-group {
    grid-template-columns: 1fr;
    gap: 0.75rem;
  }

  .checkbox-item label {
    font-size: 0.9rem;
  }

  .btn-submit {
    padding: 0.75rem;
    font-size: 1rem;
  }

  .success-message {
    padding: 2rem 1rem;
  }
}

@media (max-width: 480px) {
  .nav-container {
    flex-direction: column;
    gap: 0.5rem;
    padding: 0 1rem;
  }

  .logo {
    font-size: 1rem;
  }

  .back-link {
    font-size: 0.8rem;
  }

  .registration-container {
    padding: 0.5rem;
    margin: 1rem 0;
  }

  .registration-card {
    padding: 1rem;
    border-radius: 10px;
  }

  .registration-card h1 {
    font-size: 1.2rem;
  }

  .subtitle {
    font-size: 0.85rem;
    margin-bottom: 1rem;
  }

  .form-section {
    margin-bottom: 1.25rem;
  }

  .form-section h2 {
    font-size: 1rem;
    margin-bottom: 0.75rem;
  }

  .form-group {
    margin-bottom: 0.75rem;
  }

  .form-group label {
    font-size: 0.85rem;
    margin-bottom: 0.35rem;
  }

  .form-group input,
  .form-group select {
    font-size: 16px;
    padding: 0.6rem;
  }

  .checkbox-group {
    grid-template-columns: 1fr;
    gap: 0.5rem;
  }

  .checkbox-item {
    font-size: 0.85rem;
  }

  .checkbox-item input[type='checkbox'] {
    width: 18px;
    height: 18px;
    margin-right: 0.4rem;
  }

  .form-group.checkbox {
    margin-bottom: 1.5rem;
  }

  .form-group.checkbox input[type='checkbox'] {
    width: 18px;
    height: 18px;
    margin-right: 0.5rem;
  }

  .form-group.checkbox label {
    font-size: 0.85rem;
  }

  .btn-submit {
    padding: 0.65rem;
    font-size: 0.95rem;
  }

  .alert {
    padding: 0.75rem;
    font-size: 0.85rem;
    margin-bottom: 1rem;
  }

  .success-message {
    padding: 1.5rem 1rem;
    border-radius: 10px;
  }

  .success-icon {
    font-size: 3rem;
    margin-bottom: 0.75rem;
  }

  .success-message h1 {
    font-size: 1.2rem;
    margin-bottom: 0.75rem;
  }

  .success-message p {
    font-size: 0.9rem;
    margin-bottom: 0.5rem;
  }

  .redirect-message {
    font-size: 0.8rem;
  }
}
</style>
