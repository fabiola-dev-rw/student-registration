<script setup lang="ts">
import { ref, computed, onMounted } from 'vue'
import { useRouter } from 'vue-router'

const router = useRouter()
const submissions = ref<any[]>([])
const selectedSubmission = ref<any>(null)
const filterStatus = ref('all')
const adminEmail = ref('')

onMounted(() => {
  // Load admin email
  adminEmail.value = localStorage.getItem('adminEmail') || ''
  // Load submissions from localStorage
  const data = localStorage.getItem('studentSubmissions')
  if (data) {
    submissions.value = JSON.parse(data)
  }
})

const filteredSubmissions = computed(() => {
  if (filterStatus.value === 'all') {
    return submissions.value
  }
  return submissions.value.filter(s => s.status === filterStatus.value)
})

const handleViewDetails = (submission: any) => {
  selectedSubmission.value = submission
}

const handleCloseDetails = () => {
  selectedSubmission.value = null
}

const handleApprove = (id: number) => {
  const submission = submissions.value.find(s => s.id === id)
  if (submission) {
    submission.status = 'approved'
    submission.reviewedAt = new Date().toLocaleString()
    localStorage.setItem('studentSubmissions', JSON.stringify(submissions.value))
    selectedSubmission.value = submission
  }
}

const handleReject = (id: number) => {
  const submission = submissions.value.find(s => s.id === id)
  if (submission) {
    submission.status = 'rejected'
    submission.reviewedAt = new Date().toLocaleString()
    localStorage.setItem('studentSubmissions', JSON.stringify(submissions.value))
    selectedSubmission.value = submission
  }
}

const handleLogout = () => {
  localStorage.removeItem('adminLoggedIn')
  localStorage.removeItem('adminEmail')
  router.push('/')
}

const getStatusBadgeClass = (status: string) => {
  switch (status) {
    case 'approved':
      return 'badge-success'
    case 'rejected':
      return 'badge-danger'
    case 'pending':
      return 'badge-warning'
    default:
      return 'badge-default'
  }
}
</script>

<template>
  <div class="admin-dashboard">
    <nav class="navbar">
      <div class="nav-container">
        <div class="logo">e-Training Portal - Admin</div>
        <div class="nav-actions">
          <span class="admin-email">{{ adminEmail }}</span>
          <button @click="handleLogout" class="btn-logout">Logout</button>
        </div>
      </div>
    </nav>

    <div class="dashboard-container">
      <div class="sidebar">
        <div class="menu-item active">
          <span class="icon">📋</span>
          <span>Applications</span>
        </div>
        <div class="menu-item">
          <span class="icon">📊</span>
          <span>Reports</span>
        </div>
        <div class="menu-item">
          <span class="icon">⚙️</span>
          <span>Settings</span>
        </div>
      </div>

      <div class="main-content">
        <!-- Header -->
        <div class="content-header">
          <h1>Application Management</h1>
          <p>Review and manage student applications</p>
        </div>

        <!-- Stats -->
        <div class="stats-container">
          <div class="stat-card">
            <div class="stat-number">{{ submissions.length }}</div>
            <div class="stat-label">Total Applications</div>
          </div>
          <div class="stat-card">
            <div class="stat-number">
              {{ submissions.filter(s => s.status === 'pending').length }}
            </div>
            <div class="stat-label">Pending Review</div>
          </div>
          <div class="stat-card">
            <div class="stat-number">
              {{ submissions.filter(s => s.status === 'approved').length }}
            </div>
            <div class="stat-label">Approved</div>
          </div>
          <div class="stat-card">
            <div class="stat-number">
              {{ submissions.filter(s => s.status === 'rejected').length }}
            </div>
            <div class="stat-label">Rejected</div>
          </div>
        </div>

        <!-- Filter -->
        <div class="filter-section">
          <div class="filter-group">
            <label>Filter by Status:</label>
            <select v-model="filterStatus" class="filter-select">
              <option value="all">All Applications</option>
              <option value="pending">Pending</option>
              <option value="approved">Approved</option>
              <option value="rejected">Rejected</option>
            </select>
          </div>
        </div>

        <!-- Applications Table -->
        <div class="table-section">
          <table v-if="filteredSubmissions.length > 0" class="applications-table">
            <thead>
              <tr>
                <th>Name</th>
                <th>Email</th>
                <th>Submitted At</th>
                <th>Status</th>
                <th>Actions</th>
              </tr>
            </thead>
            <tbody>
              <tr v-for="submission in filteredSubmissions" :key="submission.id">
                <td>{{ submission.firstName }} {{ submission.lastName }}</td>
                <td>{{ submission.email }}</td>
                <td>{{ submission.submittedAt }}</td>
                <td>
                  <span :class="['badge', getStatusBadgeClass(submission.status)]">
                    {{ submission.status || 'Pending' }}
                  </span>
                </td>
                <td>
                  <button
                    @click="handleViewDetails(submission)"
                    class="btn btn-small btn-view"
                  >
                    View Details
                  </button>
                </td>
              </tr>
            </tbody>
          </table>

          <div v-else class="no-data">
            <p>No applications found</p>
          </div>
        </div>
      </div>
    </div>

    <!-- Details Modal -->
    <div v-if="selectedSubmission" class="modal-overlay" @click="handleCloseDetails">
      <div class="modal-content" @click.stop>
        <button @click="handleCloseDetails" class="close-btn">✕</button>

        <div class="modal-header">
          <h2>Application Details</h2>
        </div>

        <div class="modal-body">
          <!-- Personal Information -->
          <div class="detail-section">
            <h3>Personal Information</h3>
            <div class="detail-grid">
              <div class="detail-item">
                <label>First Name:</label>
                <p>{{ selectedSubmission.firstName }}</p>
              </div>
              <div class="detail-item">
                <label>Last Name:</label>
                <p>{{ selectedSubmission.lastName }}</p>
              </div>
              <div class="detail-item">
                <label>Email:</label>
                <p>{{ selectedSubmission.email }}</p>
              </div>
              <div class="detail-item">
                <label>Phone:</label>
                <p>{{ selectedSubmission.phone || 'N/A' }}</p>
              </div>
              <div class="detail-item">
                <label>Date of Birth:</label>
                <p>{{ selectedSubmission.dateOfBirth || 'N/A' }}</p>
              </div>
              <div class="detail-item">
                <label>Gender:</label>
                <p>{{ selectedSubmission.gender || 'N/A' }}</p>
              </div>
            </div>
          </div>

          <!-- Address Information -->
          <div class="detail-section">
            <h3>Address Information</h3>
            <div class="detail-grid">
              <div class="detail-item">
                <label>Province:</label>
                <p>{{ selectedSubmission.province || 'N/A' }}</p>
              </div>
              <div class="detail-item">
                <label>District:</label>
                <p>{{ selectedSubmission.district || 'N/A' }}</p>
              </div>
              <div class="detail-item">
                <label>Sector:</label>
                <p>{{ selectedSubmission.sector || 'N/A' }}</p>
              </div>
              <div class="detail-item">
                <label>Cell:</label>
                <p>{{ selectedSubmission.cell || 'N/A' }}</p>
              </div>
            </div>
          </div>

          <!-- Education -->
          <div class="detail-section">
            <h3>Education & Interests</h3>
            <div class="detail-grid">
              <div class="detail-item">
                <label>Education Level:</label>
                <p>{{ selectedSubmission.educationLevel || 'N/A' }}</p>
              </div>
              <div class="detail-item">
                <label>Trade/Field of Study:</label>
                <p>{{ selectedSubmission.trade || 'N/A' }}</p>
              </div>
              <div class="detail-item full-width">
                <label>Interested Courses:</label>
                <div class="courses-list">
                  <span
                    v-for="course in selectedSubmission.coursesInterested"
                    :key="course"
                    class="course-tag"
                  >
                    {{ course }}
                  </span>
                  <span v-if="!selectedSubmission.coursesInterested.length">N/A</span>
                </div>
              </div>
            </div>
          </div>

          <!-- Status -->
          <div class="detail-section">
            <h3>Application Status</h3>
            <div class="detail-grid">
              <div class="detail-item">
                <label>Status:</label>
                <p>
                  <span :class="['badge', getStatusBadgeClass(selectedSubmission.status)]">
                    {{ selectedSubmission.status || 'Pending' }}
                  </span>
                </p>
              </div>
              <div class="detail-item">
                <label>Submitted At:</label>
                <p>{{ selectedSubmission.submittedAt }}</p>
              </div>
              <div v-if="selectedSubmission.reviewedAt" class="detail-item">
                <label>Reviewed At:</label>
                <p>{{ selectedSubmission.reviewedAt }}</p>
              </div>
            </div>
          </div>
        </div>

        <div class="modal-footer">
          <button
            v-if="!selectedSubmission.status || selectedSubmission.status === 'pending'"
            @click="handleApprove(selectedSubmission.id)"
            class="btn btn-approve"
          >
            Approve
          </button>
          <button
            v-if="!selectedSubmission.status || selectedSubmission.status === 'pending'"
            @click="handleReject(selectedSubmission.id)"
            class="btn btn-reject"
          >
            Reject
          </button>
          <button @click="handleCloseDetails" class="btn btn-close">Close</button>
        </div>
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

.admin-dashboard {
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
  background-color: #f5f5f5;
  min-height: 100vh;
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
  max-width: 1400px;
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

.nav-actions {
  display: flex;
  align-items: center;
  gap: 1.5rem;
}

.admin-email {
  color: white;
  font-weight: 500;
}

.btn-logout {
  padding: 0.5rem 1rem;
  background-color: rgba(255, 255, 255, 0.2);
  color: white;
  border: 2px solid white;
  border-radius: 5px;
  cursor: pointer;
  font-weight: 600;
  transition: all 0.3s ease;
}

.btn-logout:hover {
  background-color: white;
  color: #667eea;
}

/* Dashboard Container */
.dashboard-container {
  display: flex;
  max-width: 1400px;
  margin: 0 auto;
  gap: 2rem;
  padding: 2rem;
}

/* Sidebar */
.sidebar {
  width: 250px;
  background: white;
  border-radius: 10px;
  padding: 1.5rem;
  box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
  height: fit-content;
  position: sticky;
  top: 80px;
}

.menu-item {
  padding: 1rem;
  margin-bottom: 0.5rem;
  border-radius: 5px;
  cursor: pointer;
  display: flex;
  align-items: center;
  gap: 1rem;
  transition: all 0.3s ease;
  color: #666;
}

.menu-item:hover {
  background-color: #f0f0f0;
  color: #667eea;
}

.menu-item.active {
  background-color: #667eea;
  color: white;
}

.icon {
  font-size: 1.2rem;
}

/* Main Content */
.main-content {
  flex: 1;
}

.content-header {
  background: white;
  padding: 2rem;
  border-radius: 10px;
  margin-bottom: 2rem;
  box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
}

.content-header h1 {
  color: #667eea;
  margin-bottom: 0.5rem;
}

.content-header p {
  color: #999;
}

/* Stats */
.stats-container {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
  gap: 1.5rem;
  margin-bottom: 2rem;
}

.stat-card {
  background: white;
  padding: 1.5rem;
  border-radius: 10px;
  box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
  text-align: center;
}

.stat-number {
  font-size: 2.5rem;
  font-weight: bold;
  color: #667eea;
}

.stat-label {
  color: #999;
  margin-top: 0.5rem;
}

/* Filter */
.filter-section {
  background: white;
  padding: 1.5rem;
  border-radius: 10px;
  margin-bottom: 2rem;
  box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
}

.filter-group {
  display: flex;
  align-items: center;
  gap: 1rem;
}

.filter-group label {
  font-weight: 600;
  color: #333;
}

.filter-select {
  padding: 0.5rem 1rem;
  border: 2px solid #e0e0e0;
  border-radius: 5px;
  cursor: pointer;
  transition: border-color 0.3s ease;
}

.filter-select:focus {
  outline: none;
  border-color: #667eea;
}

/* Table */
.table-section {
  background: white;
  border-radius: 10px;
  padding: 1.5rem;
  box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
}

.applications-table {
  width: 100%;
  border-collapse: collapse;
}

.applications-table thead {
  background-color: #f5f5f5;
  border-bottom: 2px solid #e0e0e0;
}

.applications-table th {
  padding: 1rem;
  text-align: left;
  font-weight: 600;
  color: #667eea;
}

.applications-table td {
  padding: 1rem;
  border-bottom: 1px solid #e0e0e0;
}

.applications-table tbody tr:hover {
  background-color: #f9f9f9;
}

/* Badge */
.badge {
  padding: 0.4rem 0.8rem;
  border-radius: 20px;
  font-size: 0.85rem;
  font-weight: 600;
}

.badge-success {
  background-color: #e8f5e9;
  color: #2e7d32;
}

.badge-danger {
  background-color: #ffebee;
  color: #c62828;
}

.badge-warning {
  background-color: #fff3e0;
  color: #e65100;
}

.badge-default {
  background-color: #e0e0e0;
  color: #666;
}

/* Buttons */
.btn {
  padding: 0.5rem 1rem;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  font-weight: 600;
  transition: all 0.3s ease;
}

.btn-small {
  padding: 0.4rem 0.8rem;
  font-size: 0.85rem;
}

.btn-view {
  background-color: #667eea;
  color: white;
}

.btn-view:hover {
  background-color: #5568d3;
}

.btn-approve {
  background-color: #4caf50;
  color: white;
}

.btn-approve:hover {
  background-color: #45a049;
}

.btn-reject {
  background-color: #f44336;
  color: white;
}

.btn-reject:hover {
  background-color: #da190b;
}

.btn-close {
  background-color: #999;
  color: white;
}

.btn-close:hover {
  background-color: #777;
}

/* No Data */
.no-data {
  text-align: center;
  padding: 3rem;
  color: #999;
}

/* Modal */
.modal-overlay {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: rgba(0, 0, 0, 0.5);
  display: flex;
  align-items: center;
  justify-content: center;
  z-index: 1000;
  padding: 1rem;
}

.modal-content {
  background: white;
  border-radius: 15px;
  max-width: 700px;
  max-height: 90vh;
  overflow-y: auto;
  box-shadow: 0 10px 40px rgba(0, 0, 0, 0.3);
  position: relative;
}

.close-btn {
  position: absolute;
  top: 1rem;
  right: 1rem;
  background: #e0e0e0;
  border: none;
  border-radius: 50%;
  width: 30px;
  height: 30px;
  cursor: pointer;
  font-size: 1.2rem;
  display: flex;
  align-items: center;
  justify-content: center;
  transition: all 0.3s ease;
  z-index: 10;
}

.close-btn:hover {
  background: #d0d0d0;
}

.modal-header {
  padding: 2rem;
  border-bottom: 2px solid #e0e0e0;
}

.modal-header h2 {
  color: #667eea;
}

.modal-body {
  padding: 2rem;
}

.detail-section {
  margin-bottom: 2rem;
}

.detail-section h3 {
  color: #667eea;
  margin-bottom: 1rem;
  font-size: 1.1rem;
  padding-bottom: 0.5rem;
  border-bottom: 1px solid #e0e0e0;
}

.detail-grid {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  gap: 1.5rem;
}

.detail-item {
  display: flex;
  flex-direction: column;
}

.detail-item.full-width {
  grid-column: 1 / -1;
}

.detail-item label {
  font-weight: 600;
  color: #667eea;
  margin-bottom: 0.5rem;
  font-size: 0.9rem;
}

.detail-item p {
  color: #333;
  word-break: break-word;
}

.courses-list {
  display: flex;
  flex-wrap: wrap;
  gap: 0.5rem;
}

.course-tag {
  display: inline-block;
  background-color: #667eea;
  color: white;
  padding: 0.3rem 0.8rem;
  border-radius: 15px;
  font-size: 0.85rem;
}

.modal-footer {
  padding: 2rem;
  border-top: 2px solid #e0e0e0;
  display: flex;
  gap: 1rem;
  justify-content: flex-end;
}

@media (max-width: 1200px) {
  .dashboard-container {
    gap: 1.5rem;
  }

  .sidebar {
    width: 200px;
  }
}

@media (max-width: 1024px) {
  .dashboard-container {
    flex-direction: column;
    gap: 1rem;
  }

  .sidebar {
    width: 100%;
    position: static;
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    gap: 0.5rem;
    padding: 1rem;
  }

  .menu-item {
    margin-bottom: 0;
    padding: 0.75rem;
    font-size: 0.9rem;
  }

  .icon {
    font-size: 1rem;
  }

  .detail-grid {
    grid-template-columns: 1fr;
  }

  .content-header {
    padding: 1.5rem;
  }

  .stats-container {
    grid-template-columns: repeat(2, 1fr);
  }
}

@media (max-width: 768px) {
  .navbar {
    padding: 0.75rem 0;
  }

  .nav-container {
    flex-wrap: wrap;
    gap: 0.75rem;
    padding: 0 1rem;
  }

  .logo {
    font-size: 1.2rem;
  }

  .admin-email {
    font-size: 0.9rem;
  }

  .btn-logout {
    padding: 0.4rem 0.8rem;
    font-size: 0.85rem;
  }

  .dashboard-container {
    padding: 1rem;
    gap: 1rem;
  }

  .sidebar {
    grid-template-columns: repeat(2, 1fr);
    padding: 1rem;
    gap: 0.5rem;
  }

  .menu-item {
    padding: 0.6rem;
    font-size: 0.8rem;
  }

  .content-header {
    padding: 1.25rem;
    margin-bottom: 1.5rem;
  }

  .content-header h1 {
    font-size: 1.5rem;
  }

  .content-header p {
    font-size: 0.9rem;
  }

  .stats-container {
    grid-template-columns: 1fr;
    gap: 1rem;
  }

  .stat-card {
    padding: 1rem;
  }

  .stat-number {
    font-size: 2rem;
  }

  .stat-label {
    font-size: 0.9rem;
  }

  .filter-section {
    padding: 1rem;
  }

  .filter-group {
    flex-direction: column;
    gap: 0.5rem;
  }

  .filter-group label {
    font-size: 0.95rem;
  }

  .filter-select {
    font-size: 0.95rem;
    padding: 0.5rem;
  }

  .table-section {
    padding: 1rem;
    overflow-x: auto;
  }

  .applications-table {
    font-size: 0.85rem;
  }

  .applications-table th,
  .applications-table td {
    padding: 0.6rem;
  }

  .applications-table th {
    font-size: 0.8rem;
  }

  .badge {
    padding: 0.3rem 0.6rem;
    font-size: 0.75rem;
  }

  .btn-small {
    padding: 0.35rem 0.6rem;
    font-size: 0.8rem;
  }

  .modal-overlay {
    padding: 1rem;
  }

  .modal-content {
    max-width: 95vw;
    max-height: 85vh;
    border-radius: 10px;
  }

  .modal-header {
    padding: 1.5rem;
  }

  .modal-header h2 {
    font-size: 1.3rem;
  }

  .modal-body {
    padding: 1.5rem;
  }

  .detail-section h3 {
    font-size: 1rem;
  }

  .detail-item label {
    font-size: 0.85rem;
  }

  .detail-item p {
    font-size: 0.9rem;
  }

  .course-tag {
    font-size: 0.75rem;
    padding: 0.25rem 0.6rem;
  }

  .modal-footer {
    padding: 1.5rem;
    flex-direction: column;
    gap: 0.75rem;
  }

  .btn {
    padding: 0.6rem 1rem;
  }
}

@media (max-width: 480px) {
  .nav-container {
    flex-direction: column;
    gap: 0.5rem;
    padding: 0 0.75rem;
  }

  .logo {
    font-size: 1rem;
  }

  .admin-email {
    font-size: 0.75rem;
  }

  .nav-actions {
    width: 100%;
    gap: 0.5rem;
  }

  .btn-logout {
    padding: 0.35rem 0.6rem;
    font-size: 0.75rem;
  }

  .dashboard-container {
    padding: 0.75rem;
    flex-direction: column;
  }

  .sidebar {
    grid-template-columns: 1fr;
    padding: 0.75rem;
    gap: 0.25rem;
  }

  .menu-item {
    padding: 0.5rem;
    font-size: 0.75rem;
  }

  .icon {
    font-size: 0.9rem;
  }

  .content-header {
    padding: 1rem;
    margin-bottom: 1rem;
  }

  .content-header h1 {
    font-size: 1.2rem;
  }

  .content-header p {
    font-size: 0.8rem;
  }

  .stats-container {
    gap: 0.75rem;
  }

  .stat-card {
    padding: 0.75rem;
  }

  .stat-number {
    font-size: 1.5rem;
  }

  .stat-label {
    font-size: 0.75rem;
  }

  .filter-section {
    padding: 0.75rem;
    margin-bottom: 1rem;
  }

  .filter-group {
    gap: 0.35rem;
  }

  .filter-group label {
    font-size: 0.85rem;
  }

  .filter-select {
    font-size: 0.85rem;
    padding: 0.4rem;
  }

  .table-section {
    padding: 0.75rem;
    border-radius: 8px;
  }

  .applications-table {
    font-size: 0.75rem;
  }

  .applications-table th {
    font-size: 0.7rem;
    padding: 0.4rem;
  }

  .applications-table td {
    padding: 0.4rem;
  }

  .badge {
    padding: 0.25rem 0.5rem;
    font-size: 0.65rem;
  }

  .btn-small {
    padding: 0.3rem 0.5rem;
    font-size: 0.7rem;
  }

  .no-data {
    padding: 2rem 1rem;
    font-size: 0.9rem;
  }

  .modal-overlay {
    padding: 0.75rem;
  }

  .modal-content {
    max-height: 90vh;
  }

  .close-btn {
    width: 28px;
    height: 28px;
    font-size: 1rem;
  }

  .modal-header {
    padding: 1rem;
  }

  .modal-header h2 {
    font-size: 1.1rem;
  }

  .modal-body {
    padding: 1rem;
  }

  .detail-section {
    margin-bottom: 1rem;
  }

  .detail-section h3 {
    font-size: 0.95rem;
    margin-bottom: 0.75rem;
  }

  .detail-grid {
    gap: 1rem;
  }

  .detail-item label {
    font-size: 0.8rem;
    margin-bottom: 0.3rem;
  }

  .detail-item p {
    font-size: 0.85rem;
  }

  .courses-list {
    gap: 0.35rem;
  }

  .course-tag {
    font-size: 0.7rem;
    padding: 0.2rem 0.5rem;
  }

  .modal-footer {
    padding: 1rem;
    gap: 0.5rem;
  }

  .btn {
    padding: 0.5rem 0.75rem;
    font-size: 0.85rem;
  }
}
</style>
