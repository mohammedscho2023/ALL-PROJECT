<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>RB-PMS Pro | Complete Project Management System</title>
    <!-- Fonts & Icons -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0-beta3/css/all.min.css">
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700;800&display=swap" rel="stylesheet">
    <!-- Chart.js -->
    <script src="https://cdn.jsdelivr.net/npm/chart.js@4.4.0/dist/chart.umd.min.js"></script>
    <style>
        :root {
            --primary: #0a4a6b;
            --primary-light: #1a6a94;
            --secondary: #2a9d8f;
            --accent: #e9c46a;
            --bg-light: #f4f9ff;
            --border-light: #d9e6f2;
            --text-dark: #0b2a40;
            --text-muted: #4a6f89;
            --success: #2a9d8f;
            --warning: #e9c46a;
            --danger: #e76f51;
            --sidebar-width: 280px;
        }

        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Inter', sans-serif;
            background: #edf3f9;
            color: var(--text-dark);
            line-height: 1.5;
        }

        .app-layout {
            display: flex;
            min-height: 100vh;
        }

        /* ===== SIDEBAR ===== */
        .sidebar {
            width: var(--sidebar-width);
            background: linear-gradient(180deg, #0a3a54 0%, #0a4a6b 100%);
            color: white;
            padding: 24px 0;
            display: flex;
            flex-direction: column;
            position: fixed;
            height: 100vh;
            overflow-y: auto;
        }

        .sidebar-header {
            padding: 0 20px 24px;
            border-bottom: 1px solid rgba(255,255,255,0.1);
        }

        .sidebar-header h2 {
            font-size: 1.4rem;
            display: flex;
            align-items: center;
            gap: 10px;
        }

        .user-profile {
            padding: 20px;
            border-bottom: 1px solid rgba(255,255,255,0.1);
            display: flex;
            align-items: center;
            gap: 12px;
        }

        .user-avatar {
            width: 48px;
            height: 48px;
            background: var(--secondary);
            border-radius: 14px;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 1.5rem;
        }

        .user-info h4 {
            font-size: 0.95rem;
            margin-bottom: 4px;
        }

        .user-info span {
            font-size: 0.75rem;
            opacity: 0.7;
        }

        .nav-menu {
            flex: 1;
            padding: 20px 12px;
        }

        .nav-item {
            display: flex;
            align-items: center;
            gap: 14px;
            padding: 14px 16px;
            color: rgba(255,255,255,0.7);
            cursor: pointer;
            border-radius: 14px;
            margin-bottom: 6px;
            transition: all 0.2s;
            font-weight: 500;
        }

        .nav-item i {
            width: 24px;
            font-size: 1.2rem;
        }

        .nav-item:hover {
            background: rgba(255,255,255,0.1);
            color: white;
        }

        .nav-item.active {
            background: var(--secondary);
            color: white;
        }

        /* ===== MAIN CONTENT ===== */
        .main-content {
            flex: 1;
            margin-left: var(--sidebar-width);
            padding: 24px 32px;
        }

        .top-bar {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 28px;
        }

        .page-title {
            font-size: 1.8rem;
            font-weight: 700;
            color: var(--primary);
        }

        .action-buttons {
            display: flex;
            gap: 12px;
        }

        .btn {
            padding: 12px 24px;
            border-radius: 40px;
            font-weight: 600;
            cursor: pointer;
            border: none;
            display: flex;
            align-items: center;
            gap: 8px;
            transition: all 0.2s;
            font-size: 0.9rem;
        }

        .btn-primary {
            background: var(--primary);
            color: white;
            box-shadow: 0 4px 12px rgba(10,74,107,0.2);
        }

        .btn-primary:hover {
            background: var(--primary-light);
            transform: translateY(-2px);
        }

        .btn-secondary {
            background: white;
            color: var(--primary);
            border: 1.5px solid var(--border-light);
        }

        .btn-success {
            background: var(--success);
            color: white;
        }

        /* ===== CARDS ===== */
        .stats-grid {
            display: grid;
            grid-template-columns: repeat(4, 1fr);
            gap: 20px;
            margin-bottom: 28px;
        }

        .stat-card {
            background: white;
            border-radius: 20px;
            padding: 24px;
            box-shadow: 0 4px 16px rgba(0,0,0,0.04);
            border: 1px solid var(--border-light);
        }

        .stat-card .label {
            color: var(--text-muted);
            font-size: 0.85rem;
            text-transform: uppercase;
            font-weight: 600;
            margin-bottom: 12px;
        }

        .stat-card .value {
            font-size: 2.2rem;
            font-weight: 800;
            color: var(--primary);
        }

        /* ===== CONTENT PANELS ===== */
        .content-panel {
            display: none;
            background: white;
            border-radius: 28px;
            padding: 32px;
            box-shadow: 0 4px 20px rgba(0,0,0,0.04);
            border: 1px solid var(--border-light);
        }

        .content-panel.active {
            display: block;
        }

        .panel-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 28px;
        }

        .panel-header h2 {
            color: var(--primary);
            display: flex;
            align-items: center;
            gap: 12px;
        }

        /* ===== FORMS ===== */
        .form-grid {
            display: grid;
            grid-template-columns: repeat(2, 1fr);
            gap: 20px;
        }

        .form-group {
            margin-bottom: 20px;
        }

        .form-group label {
            display: block;
            font-weight: 600;
            color: var(--text-dark);
            margin-bottom: 8px;
        }

        .form-control {
            width: 100%;
            padding: 14px 18px;
            border: 1.5px solid var(--border-light);
            border-radius: 14px;
            font-family: 'Inter', sans-serif;
            font-size: 0.95rem;
            background: #fafcff;
        }

        .form-control:focus {
            outline: none;
            border-color: var(--primary);
        }

        /* ===== TABLES ===== */
        .data-table {
            width: 100%;
            border-collapse: collapse;
            margin-top: 20px;
        }

        .data-table th {
            background: var(--bg-light);
            padding: 16px;
            text-align: left;
            font-weight: 700;
            color: var(--primary);
            border-bottom: 2px solid var(--border-light);
        }

        .data-table td {
            padding: 16px;
            border-bottom: 1px solid var(--border-light);
        }

        .data-table tr:hover td {
            background: var(--bg-light);
        }

        /* ===== PROJECT CARD ===== */
        .project-card {
            background: var(--bg-light);
            border-radius: 20px;
            padding: 24px;
            margin-bottom: 16px;
            border: 1px solid var(--border-light);
            cursor: pointer;
            transition: all 0.2s;
        }

        .project-card:hover {
            box-shadow: 0 8px 20px rgba(0,0,0,0.06);
            transform: translateY(-2px);
        }

        .project-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 16px;
        }

        .project-title {
            font-size: 1.2rem;
            font-weight: 700;
            color: var(--primary);
        }

        .project-meta {
            display: flex;
            gap: 20px;
            color: var(--text-muted);
            font-size: 0.9rem;
        }

        .status-badge {
            padding: 6px 16px;
            border-radius: 40px;
            font-size: 0.8rem;
            font-weight: 600;
        }

        .status-active {
            background: rgba(42,157,143,0.15);
            color: var(--success);
        }

        .progress-bar-large {
            height: 10px;
            background: #dee6ed;
            border-radius: 20px;
            margin-top: 16px;
        }

        .progress-fill {
            height: 10px;
            border-radius: 20px;
            background: var(--primary);
        }

        /* ===== LOCATION TREE ===== */
        .location-tree {
            background: var(--bg-light);
            border-radius: 16px;
            padding: 20px;
        }

        .region-item {
            margin-bottom: 16px;
        }

        .region-header {
            font-weight: 700;
            color: var(--primary);
            margin-bottom: 8px;
            cursor: pointer;
        }

        .zone-list, .woreda-list, .school-list {
            margin-left: 24px;
            padding-left: 16px;
            border-left: 2px solid var(--border-light);
        }

        /* ===== MODAL ===== */
        .modal-overlay {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
            background: rgba(0,0,0,0.5);
            z-index: 1000;
            align-items: center;
            justify-content: center;
        }

        .modal {
            background: white;
            border-radius: 28px;
            padding: 32px;
            max-width: 700px;
            width: 90%;
            max-height: 80vh;
            overflow-y: auto;
        }

        .modal-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 24px;
        }

        .modal-header h3 {
            color: var(--primary);
        }

        .close-modal {
            cursor: pointer;
            font-size: 1.5rem;
            color: var(--text-muted);
        }

        /* ===== UPLOAD AREA ===== */
        .upload-area {
            border: 2px dashed var(--border-light);
            border-radius: 20px;
            padding: 40px;
            text-align: center;
            cursor: pointer;
            transition: all 0.2s;
            background: var(--bg-light);
        }

        .upload-area:hover {
            border-color: var(--primary);
            background: white;
        }

        .upload-area i {
            font-size: 3rem;
            color: var(--primary);
            margin-bottom: 16px;
        }

        /* ===== LOGIN PAGE ===== */
        .login-container {
            min-height: 100vh;
            display: flex;
            align-items: center;
            justify-content: center;
            background: linear-gradient(135deg, var(--primary) 0%, var(--primary-light) 100%);
        }

        .login-card {
            background: white;
            border-radius: 32px;
            padding: 48px;
            width: 100%;
            max-width: 450px;
            box-shadow: 0 20px 40px rgba(0,0,0,0.1);
        }

        .login-card h2 {
            color: var(--primary);
            margin-bottom: 32px;
            text-align: center;
        }

        /* ===== UTILITIES ===== */
        .hidden {
            display: none !important;
        }

        .text-success { color: var(--success); }
        .text-warning { color: var(--warning); }
        .text-danger { color: var(--danger); }

        .mt-4 { margin-top: 20px; }
        .mb-4 { margin-bottom: 20px; }
        .flex { display: flex; }
        .gap-2 { gap: 12px; }
        .justify-between { justify-content: space-between; }
        .items-center { align-items: center; }
    </style>
</head>
<body>
<!-- LOGIN PAGE -->
<div id="loginPage" class="login-container">
    <div class="login-card">
        <h2><i class="fas fa-cubes"></i> RB-PMS Pro</h2>
        <p style="text-align: center; color: var(--text-muted); margin-bottom: 32px;">Results-Based Project Management</p>
        <form id="loginForm">
            <div class="form-group">
                <label><i class="fas fa-envelope"></i> Email</label>
                <input type="email" class="form-control" id="loginEmail" placeholder="admin@rbpms.org" value="admin@rbpms.org">
            </div>
            <div class="form-group">
                <label><i class="fas fa-lock"></i> Password</label>
                <input type="password" class="form-control" id="loginPassword" placeholder="••••••••" value="password">
            </div>
            <button type="submit" class="btn btn-primary" style="width: 100%; justify-content: center;">
                <i class="fas fa-sign-in-alt"></i> Sign In
            </button>
        </form>
        <p style="text-align: center; margin-top: 24px; color: var(--text-muted);">
            Don't have an account? <a href="#" id="showRegisterLink" style="color: var(--primary);">Register</a>
        </p>
    </div>
</div>

<!-- REGISTER PAGE -->
<div id="registerPage" class="login-container hidden">
    <div class="login-card">
        <h2><i class="fas fa-user-plus"></i> Register</h2>
        <p style="text-align: center; color: var(--text-muted); margin-bottom: 32px;">Create your organization account</p>
        <form id="registerForm">
            <div class="form-group">
                <label><i class="fas fa-building"></i> Organization Name</label>
                <input type="text" class="form-control" id="regOrgName" placeholder="Your Organization" required>
            </div>
            <div class="form-group">
                <label><i class="fas fa-user"></i> Full Name</label>
                <input type="text" class="form-control" id="regFullName" placeholder="Your Name" required>
            </div>
            <div class="form-group">
                <label><i class="fas fa-envelope"></i> Email</label>
                <input type="email" class="form-control" id="regEmail" placeholder="email@example.com" required>
            </div>
            <div class="form-group">
                <label><i class="fas fa-lock"></i> Password</label>
                <input type="password" class="form-control" id="regPassword" placeholder="••••••••" required>
            </div>
            <div class="form-group">
                <label><i class="fas fa-map-marker-alt"></i> Country</label>
                <select class="form-control" id="regCountry">
                    <option value="ET">Ethiopia</option>
                    <option value="KE">Kenya</option>
                    <option value="UG">Uganda</option>
                    <option value="SO">Somalia</option>
                    <option value="SS">South Sudan</option>
                </select>
            </div>
            <button type="submit" class="btn btn-primary" style="width: 100%; justify-content: center;">
                <i class="fas fa-check-circle"></i> Register
            </button>
        </form>
        <p style="text-align: center; margin-top: 24px; color: var(--text-muted);">
            Already have an account? <a href="#" id="showLoginLink" style="color: var(--primary);">Sign In</a>
        </p>
    </div>
</div>

<!-- MAIN APPLICATION (hidden until login) -->
<div id="mainApp" class="app-layout hidden">
    <!-- SIDEBAR -->
    <div class="sidebar">
        <div class="sidebar-header">
            <h2><i class="fas fa-cubes"></i> RB-PMS Pro</h2>
        </div>
        <div class="user-profile">
            <div class="user-avatar">
                <i class="fas fa-user"></i>
            </div>
            <div class="user-info">
                <h4 id="displayUserName">Admin User</h4>
                <span id="displayOrgName">Organization</span>
            </div>
        </div>
        <div class="nav-menu">
            <div class="nav-item active" data-page="dashboard">
                <i class="fas fa-tachometer-alt"></i> Dashboard
            </div>
            <div class="nav-item" data-page="projects">
                <i class="fas fa-folder-open"></i> Projects
            </div>
            <div class="nav-item" data-page="newProject">
                <i class="fas fa-plus-circle"></i> New Project
            </div>
            <div class="nav-item" data-page="resultsFramework">
                <i class="fas fa-sitemap"></i> Results Framework
            </div>
            <div class="nav-item" data-page="budget">
                <i class="fas fa-coins"></i> Budget Planning
            </div>
            <div class="nav-item" data-page="locations">
                <i class="fas fa-map-marked-alt"></i> Locations & Schools
            </div>
            <div class="nav-item" data-page="staff">
                <i class="fas fa-users"></i> Staff & Materials
            </div>
            <div class="nav-item" data-page="dataImport">
                <i class="fas fa-upload"></i> Import Data (Excel)
            </div>
            <div class="nav-item" data-page="reports">
                <i class="fas fa-file-alt"></i> Reports
            </div>
        </div>
        <div style="padding: 20px;">
            <button class="btn btn-secondary" id="logoutBtn" style="width: 100%; background: rgba(255,255,255,0.1); color: white; border: none;">
                <i class="fas fa-sign-out-alt"></i> Logout
            </button>
        </div>
    </div>

    <!-- MAIN CONTENT -->
    <div class="main-content">
        <div class="top-bar">
            <h1 class="page-title" id="pageTitle">Dashboard</h1>
            <div class="action-buttons">
                <button class="btn btn-primary" id="quickNewProject"><i class="fas fa-plus"></i> New Project</button>
                <button class="btn btn-secondary" id="exportDataBtn"><i class="fas fa-download"></i> Export</button>
            </div>
        </div>

        <!-- DASHBOARD PAGE -->
        <div class="content-panel active" id="dashboard">
            <div class="stats-grid">
                <div class="stat-card">
                    <div class="label">Active Projects</div>
                    <div class="value" id="activeProjectsCount">3</div>
                </div>
                <div class="stat-card">
                    <div class="label">Total Beneficiaries</div>
                    <div class="value" id="totalBeneficiaries">48,320</div>
                </div>
                <div class="stat-card">
                    <div class="label">Budget Execution</div>
                    <div class="value">72%</div>
                </div>
                <div class="stat-card">
                    <div class="label">Schools Covered</div>
                    <div class="value" id="schoolsCount">247</div>
                </div>
            </div>
            <div style="display: grid; grid-template-columns: 2fr 1fr; gap: 24px;">
                <div style="background: var(--bg-light); border-radius: 20px; padding: 24px;">
                    <h3 style="margin-bottom: 20px;"><i class="fas fa-chart-line"></i> Project Progress Overview</h3>
                    <canvas id="dashboardChart" style="max-height: 250px;"></canvas>
                </div>
                <div style="background: var(--bg-light); border-radius: 20px; padding: 24px;">
                    <h3 style="margin-bottom: 20px;"><i class="fas fa-bell"></i> Recent Activity</h3>
                    <div id="activityFeed">
                        <p><i class="fas fa-check-circle text-success"></i> Project "Ethiopia Education" updated</p>
                        <p><i class="fas fa-upload"></i> School data imported - 45 schools</p>
                        <p><i class="fas fa-users"></i> 3 new staff members added</p>
                    </div>
                </div>
            </div>
        </div>

        <!-- PROJECTS LIST PAGE -->
        <div class="content-panel" id="projects">
            <div class="panel-header">
                <h2><i class="fas fa-folder-open"></i> My Projects</h2>
                <button class="btn btn-primary" onclick="showNewProjectModal()"><i class="fas fa-plus"></i> New Project</button>
            </div>
            <div id="projectsList">
                <!-- Dynamic project cards -->
            </div>
        </div>

        <!-- NEW PROJECT PAGE -->
        <div class="content-panel" id="newProject">
            <div class="panel-header">
                <h2><i class="fas fa-plus-circle"></i> Register New Project</h2>
            </div>
            <form id="projectForm">
                <div class="form-grid">
                    <div class="form-group">
                        <label>Project Name</label>
                        <input type="text" class="form-control" id="projectName" placeholder="e.g., Ethiopia Education CAN 2026" required>
                    </div>
                    <div class="form-group">
                        <label>Project Type</label>
                        <select class="form-control" id="projectType">
                            <option value="education">Education (STEP-GPE)</option>
                            <option value="cp">Child Protection</option>
                            <option value="eie">EiE / Humanitarian</option>
                            <option value="wash">WASH</option>
                            <option value="health">Health & Nutrition</option>
                        </select>
                    </div>
                    <div class="form-group">
                        <label>Donor</label>
                        <input type="text" class="form-control" id="projectDonor" placeholder="e.g., GPE, UNICEF, ECW">
                    </div>
                    <div class="form-group">
                        <label>Total Budget (USD)</label>
                        <input type="number" class="form-control" id="projectBudget" placeholder="e.g., 4500000">
                    </div>
                    <div class="form-group">
                        <label>Start Date</label>
                        <input type="date" class="form-control" id="projectStartDate">
                    </div>
                    <div class="form-group">
                        <label>End Date</label>
                        <input type="date" class="form-control" id="projectEndDate">
                    </div>
                </div>

                <h3 style="margin: 32px 0 20px;"><i class="fas fa-sitemap"></i> Theory of Change</h3>
                <div class="form-group">
                    <label>IF Statement</label>
                    <textarea class="form-control" id="tocIf" rows="3" placeholder="If children access safe inclusive education, teachers are trained..."></textarea>
                </div>
                <div class="form-group">
                    <label>THEN Statement</label>
                    <textarea class="form-control" id="tocThen" rows="3" placeholder="Then learning outcomes improve, protection risks reduce..."></textarea>
                </div>
                <div class="form-group">
                    <label>Assumptions</label>
                    <textarea class="form-control" id="tocAssumptions" rows="2" placeholder="Schools remain accessible, community buy-in exists..."></textarea>
                </div>

                <h3 style="margin: 32px 0 20px;"><i class="fas fa-chart-bar"></i> Results Framework</h3>
                <div id="resultsFrameworkBuilder">
                    <div class="form-group">
                        <label>Impact Indicator</label>
                        <input type="text" class="form-control" id="impactIndicator" placeholder="% children achieving minimum learning">
                    </div>
                    <div class="form-grid">
                        <div class="form-group">
                            <label>Baseline</label>
                            <input type="text" class="form-control" id="impactBaseline" placeholder="42%">
                        </div>
                        <div class="form-group">
                            <label>Target</label>
                            <input type="text" class="form-control" id="impactTarget" placeholder="65%">
                        </div>
                    </div>
                    <div class="form-group">
                        <label>Outcome Indicator</label>
                        <input type="text" class="form-control" id="outcomeIndicator" placeholder="# children accessing safe education">
                    </div>
                    <div class="form-grid">
                        <div class="form-group">
                            <label>Baseline</label>
                            <input type="text" class="form-control" id="outcomeBaseline" placeholder="18,200">
                        </div>
                        <div class="form-group">
                            <label>Target</label>
                            <input type="text" class="form-control" id="outcomeTarget" placeholder="35,000">
                        </div>
                    </div>
                </div>

                <button type="submit" class="btn btn-success" style="margin-top: 32px; padding: 16px 40px;">
                    <i class="fas fa-save"></i> Save Project
                </button>
            </form>
        </div>

        <!-- RESULTS FRAMEWORK PAGE -->
        <div class="content-panel" id="resultsFramework">
            <div class="panel-header">
                <h2><i class="fas fa-sitemap"></i> Results Framework Management</h2>
                <button class="btn btn-primary" onclick="updateProgress()"><i class="fas fa-edit"></i> Update Progress</button>
            </div>
            <div id="resultsDisplay">
                <p>Select a project to view its results framework.</p>
            </div>
        </div>

        <!-- BUDGET PLANNING PAGE -->
        <div class="content-panel" id="budget">
            <div class="panel-header">
                <h2><i class="fas fa-coins"></i> Budget Planning & Costing</h2>
                <button class="btn btn-primary" onclick="addBudgetLine()"><i class="fas fa-plus"></i> Add Budget Line</button>
            </div>
            <table class="data-table">
                <thead>
                    <tr><th>Category</th><th>Description</th><th>Unit Cost</th><th>Quantity</th><th>Total</th></tr>
                </thead>
                <tbody id="budgetTableBody">
                    <tr><td>Personnel</td><td>Project Staff</td><td>$50,000</td><td>24</td><td>$1,200,000</td></tr>
                    <tr><td>Training</td><td>Teacher Training</td><td>$190</td><td>1,600</td><td>$304,000</td></tr>
                    <tr><td>Supplies</td><td>Learning Materials</td><td>$67</td><td>48,320</td><td>$3,237,440</td></tr>
                </tbody>
            </table>
            <div style="margin-top: 24px; text-align: right;">
                <strong>Total Budget: </strong><span id="totalBudgetDisplay">$4,741,440</span>
            </div>
        </div>

        <!-- LOCATIONS & SCHOOLS PAGE -->
        <div class="content-panel" id="locations">
            <div class="panel-header">
                <h2><i class="fas fa-map-marked-alt"></i> Locations & Schools</h2>
                <div>
                    <button class="btn btn-secondary" onclick="addRegion()"><i class="fas fa-plus"></i> Add Region</button>
                    <button class="btn btn-primary" onclick="addSchool()"><i class="fas fa-school"></i> Add School</button>
                </div>
            </div>
            <div class="location-tree" id="locationTree">
                <div class="region-item">
                    <div class="region-header"><i class="fas fa-chevron-down"></i> Afar Region</div>
                    <div class="zone-list">
                        <div class="region-header"><i class="fas fa-chevron-down"></i> Zone 1</div>
                        <div class="woreda-list">
                            <div class="region-header">Asayita Woreda</div>
                            <div class="school-list">
                                <div><i class="fas fa-school"></i> Asayita Primary School (Grades 1-8, Enrolled: 1,245)</div>
                                <div><i class="fas fa-school"></i> Dubti Secondary School (Grades 9-12, Enrolled: 876)</div>
                            </div>
                        </div>
                    </div>
                </div>
                <div class="region-item">
                    <div class="region-header"><i class="fas fa-chevron-down"></i> Somali Region</div>
                    <div class="zone-list">
                        <div class="region-header">Jijiga Zone</div>
                        <div class="woreda-list">
                            <div class="region-header">Jijiga Woreda</div>
                            <div class="school-list">
                                <div><i class="fas fa-school"></i> Jijiga Primary (Grades 1-8, Enrolled: 2,100)</div>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
            <div style="margin-top: 24px;">
                <h3>School Enrollment Summary</h3>
                <table class="data-table">
                    <thead><tr><th>Grade Level</th><th>Male</th><th>Female</th><th>Total</th></tr></thead>
                    <tbody>
                        <tr><td>Pre-School</td><td>1,245</td><td>1,189</td><td>2,434</td></tr>
                        <tr><td>Primary (1-4)</td><td>8,456</td><td>8,234</td><td>16,690</td></tr>
                        <tr><td>Middle (5-8)</td><td>6,234</td><td>6,012</td><td>12,246</td></tr>
                        <tr><td>Secondary (9-12)</td><td>4,123</td><td>3,987</td><td>8,110</td></tr>
                    </tbody>
                </table>
            </div>
        </div>

        <!-- STAFF & MATERIALS PAGE -->
        <div class="content-panel" id="staff">
            <div class="panel-header">
                <h2><i class="fas fa-users"></i> Staff & Materials Management</h2>
                <button class="btn btn-primary" onclick="addStaff()"><i class="fas fa-user-plus"></i> Add Staff</button>
            </div>
            <h3>Project Staff</h3>
            <table class="data-table">
                <thead><tr><th>Name</th><th>Position</th><th>Location</th><th>Status</th></tr></thead>
                <tbody id="staffTableBody">
                    <tr><td>Dr. Amina Hassan</td><td>Project Manager</td><td>Addis Ababa</td><td>Active</td></tr>
                    <tr><td>Mr. Tesfaye Bekele</td><td>MEAL Officer</td><td>Semera, Afar</td><td>Active</td></tr>
                    <tr><td>Ms. Fatuma Ali</td><td>Education Specialist</td><td>Jijiga, Somali</td><td>Active</td></tr>
                </tbody>
            </table>
            <h3 style="margin-top: 32px;">Materials & Supplies</h3>
            <table class="data-table">
                <thead><tr><th>Item</th><th>Quantity</th><th>Unit</th><th>Status</th></tr></thead>
                <tbody>
                    <tr><td>Textbooks</td><td>25,000</td><td>pieces</td><td>Procured</td></tr>
                    <tr><td>School-in-a-Box Kits</td><td>450</td><td>kits</td><td>Distributed</td></tr>
                    <tr><td>Teacher Guides</td><td>1,600</td><td>copies</td><td>In Transit</td></tr>
                </tbody>
            </table>
        </div>

        <!-- DATA IMPORT PAGE -->
        <div class="content-panel" id="dataImport">
            <div class="panel-header">
                <h2><i class="fas fa-upload"></i> Import Data (Excel/CSV)</h2>
            </div>
            <div class="upload-area" onclick="document.getElementById('fileInput').click()">
                <i class="fas fa-cloud-upload-alt"></i>
                <h3>Click to upload Excel or CSV file</h3>
                <p>Supports .xlsx, .xls, .csv formats</p>
                <input type="file" id="fileInput" accept=".xlsx,.xls,.csv" style="display: none;" onchange="handleFileUpload(event)">
            </div>
            <div id="importPreview" style="margin-top: 24px;"></div>
            <div style="margin-top: 24px;">
                <h3>Data Processing Options</h3>
                <select class="form-control" id="dataType">
                    <option value="schools">School Enrollment Data</option>
                    <option value="indicators">Indicator Progress Data</option>
                    <option value="beneficiaries">Beneficiary Lists</option>
                    <option value="budget">Budget & Expenditure</option>
                </select>
                <button class="btn btn-primary mt-4" onclick="processImportedData()">
                    <i class="fas fa-cogs"></i> Process Data
                </button>
            </div>
        </div>

        <!-- REPORTS PAGE -->
        <div class="content-panel" id="reports">
            <div class="panel-header">
                <h2><i class="fas fa-file-alt"></i> Generate Reports</h2>
            </div>
            <div style="display: grid; grid-template-columns: repeat(3, 1fr); gap: 20px;">
                <div class="stat-card" style="cursor: pointer;" onclick="generateReport('progress')">
                    <i class="fas fa-chart-line" style="font-size: 2rem; color: var(--primary);"></i>
                    <h3 style="margin: 16px 0;">Progress Report</h3>
                    <p>Results framework progress, achievements vs targets</p>
                </div>
                <div class="stat-card" style="cursor: pointer;" onclick="generateReport('financial')">
                    <i class="fas fa-dollar-sign" style="font-size: 2rem; color: var(--primary);"></i>
                    <h3 style="margin: 16px 0;">Financial Report</h3>
                    <p>Budget execution, burn rate, variance analysis</p>
                </div>
                <div class="stat-card" style="cursor: pointer;" onclick="generateReport('beneficiary')">
                    <i class="fas fa-users" style="font-size: 2rem; color: var(--primary);"></i>
                    <h3 style="margin: 16px 0;">Beneficiary Report</h3>
                    <p>Disaggregated by sex, age, disability, location</p>
                </div>
                <div class="stat-card" style="cursor: pointer;" onclick="generateReport('donor')">
                    <i class="fas fa-hand-holding-heart" style="font-size: 2rem; color: var(--primary);"></i>
                    <h3 style="margin: 16px 0;">Donor Report</h3>
                    <p>GPE/UNICEF/ECW compliant format</p>
                </div>
                <div class="stat-card" style="cursor: pointer;" onclick="generateReport('cluster')">
                    <i class="fas fa-network-wired" style="font-size: 2rem; color: var(--primary);"></i>
                    <h3 style="margin: 16px 0;">Cluster 4Ws/5Ws</h3>
                    <p>Education/CP cluster reporting</p>
                </div>
                <div class="stat-card" style="cursor: pointer;" onclick="generateReport('school')">
                    <i class="fas fa-school" style="font-size: 2rem; color: var(--primary);"></i>
                    <h3 style="margin: 16px 0;">School Report</h3>
                    <p>Enrollment by grade, gender, location</p>
                </div>
            </div>
        </div>
    </div>
</div>

<!-- MODAL FOR NEW PROJECT -->
<div class="modal-overlay" id="projectModal">
    <div class="modal">
        <div class="modal-header">
            <h3>Register New Project</h3>
            <span class="close-modal" onclick="closeModal()">&times;</span>
        </div>
        <div id="modalContent">
            <!-- Quick project form -->
        </div>
    </div>
</div>

<script>
    // ===== APPLICATION STATE =====
    let currentUser = null;
    let projects = [];
    let selectedProject = null;

    // ===== INITIALIZATION =====
    document.addEventListener('DOMContentLoaded', function() {
        // Check for saved session
        const savedUser = localStorage.getItem('rbpms_user');
        if (savedUser) {
            currentUser = JSON.parse(savedUser);
            showMainApp();
        }

        // Login form
        document.getElementById('loginForm').addEventListener('submit', function(e) {
            e.preventDefault();
            const email = document.getElementById('loginEmail').value;
            const password = document.getElementById('loginPassword').value;
            
            // Simple validation
            if (email && password) {
                currentUser = {
                    name: email.split('@')[0],
                    email: email,
                    organization: 'STEP-GPE Partner'
                };
                localStorage.setItem('rbpms_user', JSON.stringify(currentUser));
                showMainApp();
            }
        });

        // Register form
        document.getElementById('registerForm').addEventListener('submit', function(e) {
            e.preventDefault();
            const orgName = document.getElementById('regOrgName').value;
            const fullName = document.getElementById('regFullName').value;
            const email = document.getElementById('regEmail').value;
            
            currentUser = {
                name: fullName,
                email: email,
                organization: orgName
            };
            localStorage.setItem('rbpms_user', JSON.stringify(currentUser));
            showMainApp();
        });

        // Show register/login toggle
        document.getElementById('showRegisterLink').addEventListener('click', function(e) {
            e.preventDefault();
            document.getElementById('loginPage').classList.add('hidden');
            document.getElementById('registerPage').classList.remove('hidden');
        });

        document.getElementById('showLoginLink').addEventListener('click', function(e) {
            e.preventDefault();
            document.getElementById('registerPage').classList.add('hidden');
            document.getElementById('loginPage').classList.remove('hidden');
        });

        // Logout
        document.getElementById('logoutBtn').addEventListener('click', function() {
            localStorage.removeItem('rbpms_user');
            location.reload();
        });

        // Navigation
        document.querySelectorAll('.nav-item').forEach(item => {
            item.addEventListener('click', function() {
                const page = this.dataset.page;
                switchPage(page);
            });
        });

        // Quick new project
        document.getElementById('quickNewProject').addEventListener('click', function() {
            switchPage('newProject');
        });

        // Project form submission
        document.getElementById('projectForm').addEventListener('submit', function(e) {
            e.preventDefault();
            saveProject();
        });

        // Initialize charts if on dashboard
        initCharts();
        loadProjects();
    });

    // ===== FUNCTIONS =====
    function showMainApp() {
        document.getElementById('loginPage').classList.add('hidden');
        document.getElementById('registerPage').classList.add('hidden');
        document.getElementById('mainApp').classList.remove('hidden');
        
        document.getElementById('displayUserName').textContent = currentUser.name;
        document.getElementById('displayOrgName').textContent = currentUser.organization;
        
        loadProjects();
    }

    function switchPage(pageId) {
        document.querySelectorAll('.nav-item').forEach(item => {
            item.classList.remove('active');
            if (item.dataset.page === pageId) {
                item.classList.add('active');
            }
        });

        document.querySelectorAll('.content-panel').forEach(panel => {
            panel.classList.remove('active');
        });
        document.getElementById(pageId).classList.add('active');

        const titles = {
            'dashboard': 'Dashboard',
            'projects': 'My Projects',
            'newProject': 'Register New Project',
            'resultsFramework': 'Results Framework',
            'budget': 'Budget Planning',
            'locations': 'Locations & Schools',
            'staff': 'Staff & Materials',
            'dataImport': 'Import Data',
            'reports': 'Reports'
        };
        document.getElementById('pageTitle').textContent = titles[pageId] || pageId;

        if (pageId === 'projects') {
            loadProjects();
        }
    }

    function saveProject() {
        const project = {
            id: Date.now(),
            name: document.getElementById('projectName').value,
            type: document.getElementById('projectType').value,
            donor: document.getElementById('projectDonor').value,
            budget: document.getElementById('projectBudget').value,
            startDate: document.getElementById('projectStartDate').value,
            endDate: document.getElementById('projectEndDate').value,
            toc: {
                if: document.getElementById('tocIf').value,
                then: document.getElementById('tocThen').value,
                assumptions: document.getElementById('tocAssumptions').value
            },
            results: {
                impact: {
                    indicator: document.getElementById('impactIndicator').value,
                    baseline: document.getElementById('impactBaseline').value,
                    target: document.getElementById('impactTarget').value,
                    current: document.getElementById('impactBaseline').value
                },
                outcome: {
                    indicator: document.getElementById('outcomeIndicator').value,
                    baseline: document.getElementById('outcomeBaseline').value,
                    target: document.getElementById('outcomeTarget').value,
                    current: document.getElementById('outcomeBaseline').value
                }
            },
            createdAt: new Date().toISOString()
        };

        projects.push(project);
        localStorage.setItem('rbpms_projects', JSON.stringify(projects));
        
        alert('✅ Project saved successfully!');
        document.getElementById('projectForm').reset();
        switchPage('projects');
    }

    function loadProjects() {
        const saved = localStorage.getItem('rbpms_projects');
        if (saved) {
            projects = JSON.parse(saved);
        }
        
        const container = document.getElementById('projectsList');
        if (container) {
            if (projects.length === 0) {
                container.innerHTML = '<p>No projects yet. Click "New Project" to get started.</p>';
                return;
            }
            
            container.innerHTML = projects.map(p => `
                <div class="project-card" onclick="viewProject(${p.id})">
                    <div class="project-header">
                        <span class="project-title">${p.name}</span>
                        <span class="status-badge status-active">Active</span>
                    </div>
                    <div class="project-meta">
                        <span><i class="fas fa-tag"></i> ${p.type}</span>
                        <span><i class="fas fa-hand-holding-heart"></i> ${p.donor || 'N/A'}</span>
                        <span><i class="fas fa-calendar"></i> ${p.startDate} - ${p.endDate}</span>
                    </div>
                    <div class="project-meta">
                        <span><i class="fas fa-dollar-sign"></i> Budget: $${Number(p.budget).toLocaleString()}</span>
                    </div>
                    <div class="progress-bar-large">
                        <div class="progress-fill" style="width: 45%"></div>
                    </div>
                </div>
            `).join('');
        }
        
        document.getElementById('activeProjectsCount').textContent = projects.length;
    }

    function viewProject(id) {
        selectedProject = projects.find(p => p.id === id);
        if (selectedProject) {
            switchPage('resultsFramework');
            displayResultsFramework();
        }
    }

    function displayResultsFramework() {
        const container = document.getElementById('resultsDisplay');
        if (!selectedProject) {
            container.innerHTML = '<p>Select a project to view its results framework.</p>';
            return;
        }
        
        container.innerHTML = `
            <h3>${selectedProject.name}</h3>
            <h4 style="margin-top: 24px;">Theory of Change</h4>
            <p><strong>IF:</strong> ${selectedProject.toc.if || 'N/A'}</p>
            <p><strong>THEN:</strong> ${selectedProject.toc.then || 'N/A'}</p>
            <p><strong>Assumptions:</strong> ${selectedProject.toc.assumptions || 'N/A'}</p>
            
            <h4 style="margin-top: 24px;">Results Framework</h4>
            <table class="data-table">
                <thead><tr><th>Level</th><th>Indicator</th><th>Baseline</th><th>Target</th><th>Current</th><th>Progress</th></tr></thead>
                <tbody>
                    <tr>
                        <td>Impact</td>
                        <td>${selectedProject.results.impact.indicator}</td>
                        <td>${selectedProject.results.impact.baseline}</td>
                        <td>${selectedProject.results.impact.target}</td>
                        <td>${selectedProject.results.impact.current}</td>
                        <td><div class="progress-bar-large"><div class="progress-fill" style="width: 45%"></div></div></td>
                    </tr>
                    <tr>
                        <td>Outcome</td>
                        <td>${selectedProject.results.outcome.indicator}</td>
                        <td>${selectedProject.results.outcome.baseline}</td>
                        <td>${selectedProject.results.outcome.target}</td>
                        <td>${selectedProject.results.outcome.current}</td>
                        <td><div class="progress-bar-large"><div class="progress-fill" style="width: 60%"></div></div></td>
                    </tr>
                </tbody>
            </table>
        `;
    }

    function updateProgress() {
        if (!selectedProject) {
            alert('Please select a project first.');
            return;
        }
        const newProgress = prompt('Enter current progress value for Outcome:');
        if (newProgress) {
            selectedProject.results.outcome.current = newProgress;
            localStorage.setItem('rbpms_projects', JSON.stringify(projects));
            displayResultsFramework();
        }
    }

    function generateReport(type) {
        alert(`📊 Generating ${type} report...\n\nThis will export a comprehensive report with all project data, indicators, and financial information in donor-ready format.`);
    }

    function handleFileUpload(event) {
        const file = event.target.files[0];
        if (file) {
            document.getElementById('importPreview').innerHTML = `
                <div class="info-block">
                    <i class="fas fa-check-circle text-success"></i> File loaded: ${file.name}<br>
                    <strong>Size:</strong> ${(file.size / 1024).toFixed(2)} KB<br>
                    <strong>Type:</strong> ${file.type}
                </div>
            `;
        }
    }

    function processImportedData() {
        const dataType = document.getElementById('dataType').value;
        alert(`✅ Processing ${dataType} data...\n\nData will be integrated into the system.`);
    }

    function addBudgetLine() {
        alert('Add new budget line - form would open here');
    }

    function addRegion() {
        const region = prompt('Enter region name:');
        if (region) {
            alert(`Region "${region}" added.`);
        }
    }

    function addSchool() {
        const school = prompt('Enter school name:');
        if (school) {
            alert(`School "${school}" added.`);
        }
    }

    function addStaff() {
        alert('Add new staff member - form would open here');
    }

    function showNewProjectModal() {
        switchPage('newProject');
    }

    function closeModal() {
        document.getElementById('projectModal').style.display = 'none';
    }

    function initCharts() {
        const ctx = document.getElementById('dashboardChart');
        if (ctx) {
            new Chart(ctx, {
                type: 'line',
                data: {
                    labels: ['Jan', 'Feb', 'Mar', 'Apr', 'May', 'Jun'],
                    datasets: [{
                        label: 'Target',
                        data: [10, 20, 30, 45, 60, 75],
                        borderColor: '#0a4a6b',
                        borderWidth: 2,
                        fill: false
                    }, {
                        label: 'Actual',
                        data: [8, 18, 28, 42, 58, 72],
                        borderColor: '#2a9d8f',
                        borderWidth: 2,
                        fill: false
                    }]
                },
                options: {
                    responsive: true,
                    maintainAspectRatio: true
                }
            });
        }
    }

    // Initialize with sample data if empty
    if (!localStorage.getItem('rbpms_projects')) {
        projects = [{
            id: 1,
            name: 'Ethiopia Education CAN 2026',
            type: 'education',
            donor: 'GPE/STEP',
            budget: 4500000,
            startDate: '2026-01-01',
            endDate: '2027-12-31',
            toc: {
                if: 'Children access safe inclusive education, teachers are trained',
                then: 'Learning outcomes improve, protection risks reduce',
                assumptions: 'Schools accessible, community buy-in'
            },
            results: {
                impact: { indicator: '% children achieving minimum learning', baseline: '42%', target: '65%', current: '58%' },
                outcome: { indicator: '# children accessing safe education', baseline: '18,200', target: '35,000', current: '31,450' }
            }
        }];
        localStorage.setItem('rbpms_projects', JSON.stringify(projects));
    }
</script>
</body>
</html>
