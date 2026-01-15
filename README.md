<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>StudentPortfolio Pro</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <link href="https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;500;600;700&family=Raleway:wght@400;500;600;700&display=swap" rel="stylesheet">
    <script src="https://cdnjs.cloudflare.com/ajax/libs/html2pdf.js/0.10.1/html2pdf.bundle.min.js"></script>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        :root {
            --primary: #4361ee;
            --primary-dark: #3a56d4;
            --secondary: #7209b7;
            --light: #f8f9fa;
            --dark: #212529;
            --gray: #6c757d;
            --light-gray: #e9ecef;
            --success: #4cc9f0;
            --warning: #f72585;
            --shadow: 0 10px 20px rgba(0, 0, 0, 0.1);
            --border-radius: 15px;
        }

        body {
            font-family: 'Poppins', sans-serif;
            background: linear-gradient(135deg, #f5f7fa 0%, #c3cfe2 100%);
            min-height: 100vh;
            color: var(--dark);
            overflow-x: hidden;
        }

        .container {
            max-width: 1200px;
            margin: 0 auto;
            padding: 0 20px;
        }

        /* Welcome Animation */
        .welcome-overlay {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: linear-gradient(135deg, var(--primary), var(--secondary));
            display: flex;
            justify-content: center;
            align-items: center;
            z-index: 2000;
            animation: fadeOut 1s ease-out 2s forwards;
        }

        .welcome-content {
            text-align: center;
            color: white;
            animation: zoomIn 1.5s ease-out;
        }

        .welcome-content h1 {
            font-size: 3.5rem;
            margin-bottom: 20px;
            font-family: 'Raleway', sans-serif;
        }

        .welcome-content p {
            font-size: 1.5rem;
            opacity: 0.9;
        }

        /* Login/Signup Page */
        .auth-container {
            min-height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            padding: 20px;
            animation: fadeIn 1s ease-out;
        }

        .auth-card {
            background: white;
            border-radius: var(--border-radius);
            box-shadow: var(--shadow);
            overflow: hidden;
            width: 100%;
            max-width: 450px;
            position: relative;
            animation: slideUp 0.8s ease-out;
        }

        .auth-header {
            background: linear-gradient(90deg, var(--primary), var(--secondary));
            color: white;
            padding: 40px 30px;
            text-align: center;
        }

        .auth-header h1 {
            font-family: 'Raleway', sans-serif;
            font-weight: 700;
            font-size: 2.5rem;
            margin-bottom: 10px;
            letter-spacing: 1px;
        }

        .auth-header p {
            font-size: 1.1rem;
            opacity: 0.9;
        }

        .auth-tabs {
            display: flex;
            background: var(--light-gray);
        }

        .auth-tab {
            flex: 1;
            padding: 20px;
            text-align: center;
            font-weight: 600;
            cursor: pointer;
            transition: all 0.3s;
            font-size: 1.1rem;
        }

        .auth-tab.active {
            background: white;
            color: var(--primary);
        }

        .auth-form-container {
            padding: 40px 30px;
        }

        .auth-form {
            display: none;
            animation: fadeIn 0.5s ease-out;
        }

        .auth-form.active {
            display: block;
        }

        .form-group {
            margin-bottom: 25px;
            position: relative;
        }

        .form-group label {
            display: block;
            margin-bottom: 8px;
            font-weight: 500;
            color: var(--dark);
        }

        .form-control {
            width: 100%;
            padding: 15px;
            border: 2px solid var(--light-gray);
            border-radius: 10px;
            font-size: 1rem;
            transition: all 0.3s;
            font-family: 'Poppins', sans-serif;
        }

        .form-control:focus {
            border-color: var(--primary);
            outline: none;
            box-shadow: 0 0 0 3px rgba(67, 97, 238, 0.2);
        }

        textarea.form-control {
            resize: vertical;
            min-height: 100px;
        }

        .btn {
            display: block;
            width: 100%;
            padding: 16px;
            border: none;
            border-radius: 10px;
            font-size: 1.1rem;
            font-weight: 600;
            cursor: pointer;
            transition: all 0.3s;
            font-family: 'Poppins', sans-serif;
        }

        .btn-primary {
            background: linear-gradient(90deg, var(--primary), var(--secondary));
            color: white;
        }

        .btn-primary:hover {
            transform: translateY(-3px);
            box-shadow: 0 7px 15px rgba(67, 97, 238, 0.4);
        }

        .btn-logout {
            background: var(--warning);
            color: white;
            padding: 10px 20px;
            border-radius: 8px;
            border: none;
            cursor: pointer;
            font-weight: 500;
            transition: all 0.3s;
        }

        .btn-logout:hover {
            background: #e11570;
            transform: translateY(-2px);
        }

        /* Dashboard */
        .dashboard {
            display: none;
            animation: fadeIn 1s ease-out;
        }

        .navbar {
            background: white;
            box-shadow: var(--shadow);
            position: sticky;
            top: 0;
            z-index: 1000;
            animation: slideDown 0.5s ease-out;
        }

        .nav-container {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 20px;
        }

        .logo {
            font-family: 'Raleway', sans-serif;
            font-size: 1.8rem;
            font-weight: 700;
            background: linear-gradient(90deg, var(--primary), var(--secondary));
            -webkit-background-clip: text;
            background-clip: text;
            color: transparent;
            text-decoration: none;
        }

        .nav-links {
            display: flex;
            gap: 30px;
            align-items: center;
        }

        .nav-link {
            text-decoration: none;
            color: var(--dark);
            font-weight: 500;
            transition: all 0.3s;
            position: relative;
            padding: 5px 0;
        }

        .nav-link:hover {
            color: var(--primary);
        }

        .nav-link.active:after {
            content: "";
            position: absolute;
            bottom: -5px;
            left: 0;
            width: 100%;
            height: 3px;
            background: var(--primary);
            border-radius: 2px;
        }

        .user-info {
            display: flex;
            align-items: center;
            gap: 15px;
        }

        .avatar {
            width: 40px;
            height: 40px;
            border-radius: 50%;
            background: linear-gradient(90deg, var(--primary), var(--secondary));
            color: white;
            display: flex;
            align-items: center;
            justify-content: center;
            font-weight: 600;
        }

        .main-content {
            padding: 40px 0;
        }

        .section {
            display: none;
            animation: fadeIn 0.8s ease-out;
        }

        .section.active {
            display: block;
        }

        .section-header {
            margin-bottom: 40px;
            text-align: center;
        }

        .section-header h2 {
            font-family: 'Raleway', sans-serif;
            font-size: 2.2rem;
            color: var(--dark);
            margin-bottom: 15px;
            position: relative;
            display: inline-block;
        }

        .section-header h2:after {
            content: "";
            position: absolute;
            bottom: -10px;
            left: 50%;
            transform: translateX(-50%);
            width: 70px;
            height: 4px;
            background: linear-gradient(90deg, var(--primary), var(--secondary));
            border-radius: 2px;
        }

        .card {
            background: white;
            border-radius: var(--border-radius);
            box-shadow: var(--shadow);
            padding: 30px;
            margin-bottom: 30px;
            transition: transform 0.3s;
        }

        .card:hover {
            transform: translateY(-5px);
        }

        .card-title {
            font-size: 1.5rem;
            color: var(--dark);
            margin-bottom: 20px;
            display: flex;
            align-items: center;
            gap: 10px;
        }

        .card-title i {
            color: var(--primary);
        }

        /* Skills Styles */
        .skills-container {
            display: flex;
            flex-wrap: wrap;
            gap: 15px;
            margin-top: 20px;
        }

        .skill-tag {
            background: linear-gradient(90deg, var(--primary), var(--secondary));
            color: white;
            padding: 10px 20px;
            border-radius: 50px;
            font-weight: 500;
            display: flex;
            align-items: center;
            gap: 8px;
            animation: fadeIn 0.5s ease-out;
        }

        .skill-tag .delete-skill {
            cursor: pointer;
            opacity: 0.8;
            transition: opacity 0.2s;
        }

        .skill-tag .delete-skill:hover {
            opacity: 1;
        }

        /* Input Groups */
        .input-group {
            display: flex;
            gap: 15px;
            margin-bottom: 20px;
        }

        .input-group .form-control {
            flex: 1;
        }

        .btn-small {
            padding: 10px 20px;
            background: var(--primary);
            color: white;
            border: none;
            border-radius: 8px;
            cursor: pointer;
            transition: all 0.3s;
            font-weight: 500;
            font-family: 'Poppins', sans-serif;
        }

        .btn-small:hover {
            background: var(--primary-dark);
        }

        .btn-danger {
            background: var(--warning);
        }

        .btn-danger:hover {
            background: #e11570;
        }

        /* List Items */
        .list-item {
            display: flex;
            justify-content: space-between;
            align-items: flex-start;
            padding: 20px;
            border-bottom: 1px solid var(--light-gray);
            animation: slideIn 0.5s ease-out;
        }

        .list-item:last-child {
            border-bottom: none;
        }

        .list-item-content h4 {
            font-size: 1.2rem;
            margin-bottom: 8px;
            color: var(--dark);
        }

        .list-item-content p {
            color: var(--gray);
            margin-bottom: 5px;
        }

        .list-actions {
            display: flex;
            gap: 10px;
        }

        /* Resume Preview */
        .resume-preview {
            background: white;
            padding: 40px;
            border-radius: var(--border-radius);
            box-shadow: var(--shadow);
            max-width: 800px;
            margin: 0 auto;
            font-family: 'Poppins', sans-serif;
        }

        .resume-header {
            text-align: center;
            margin-bottom: 40px;
            padding-bottom: 20px;
            border-bottom: 2px solid var(--light-gray);
        }

        .resume-name {
            font-size: 2.5rem;
            font-weight: 700;
            color: var(--dark);
            margin-bottom: 10px;
            font-family: 'Raleway', sans-serif;
        }

        .resume-contact {
            display: flex;
            justify-content: center;
            flex-wrap: wrap;
            gap: 20px;
            color: var(--gray);
            font-size: 0.95rem;
        }

        .resume-section {
            margin-bottom: 30px;
        }

        .resume-section-title {
            font-size: 1.5rem;
            color: var(--primary);
            margin-bottom: 15px;
            padding-bottom: 8px;
            border-bottom: 1px solid var(--light-gray);
            font-family: 'Raleway', sans-serif;
        }

        .resume-item {
            margin-bottom: 20px;
        }

        .resume-item-title {
            font-weight: 600;
            color: var(--dark);
            font-size: 1.1rem;
        }

        .resume-item-subtitle {
            color: var(--gray);
            font-style: italic;
            margin-bottom: 5px;
        }

        .resume-item-details {
            color: var(--gray);
            margin-bottom: 5px;
        }

        .resume-skills-list {
            display: flex;
            flex-wrap: wrap;
            gap: 10px;
            margin-top: 10px;
        }

        .resume-skill {
            background: var(--light-gray);
            padding: 5px 15px;
            border-radius: 20px;
            font-size: 0.9rem;
        }

        /* File Upload */
        .file-upload {
            border: 2px dashed var(--light-gray);
            border-radius: 10px;
            padding: 30px;
            text-align: center;
            margin-bottom: 20px;
            cursor: pointer;
            transition: all 0.3s;
        }

        .file-upload:hover {
            border-color: var(--primary);
            background: rgba(67, 97, 238, 0.05);
        }

        .file-upload i {
            font-size: 3rem;
            color: var(--gray);
            margin-bottom: 15px;
        }

        /* Empty States */
        .empty-state {
            text-align: center;
            padding: 40px 20px;
            color: var(--gray);
        }

        .empty-state i {
            font-size: 3rem;
            margin-bottom: 15px;
            color: var(--light-gray);
        }

        /* Animations */
        @keyframes fadeIn {
            from { opacity: 0; }
            to { opacity: 1; }
        }

        @keyframes slideUp {
            from { transform: translateY(50px); opacity: 0; }
            to { transform: translateY(0); opacity: 1; }
        }

        @keyframes slideDown {
            from { transform: translateY(-50px); opacity: 0; }
            to { transform: translateY(0); opacity: 1; }
        }

        @keyframes slideIn {
            from { transform: translateX(-20px); opacity: 0; }
            to { transform: translateX(0); opacity: 1; }
        }

        @keyframes zoomIn {
            from { transform: scale(0.5); opacity: 0; }
            to { transform: scale(1); opacity: 1; }
        }

        @keyframes fadeOut {
            from { opacity: 1; }
            to { opacity: 0; visibility: hidden; }
        }

        /* Responsive */
        @media (max-width: 768px) {
            .nav-container {
                flex-direction: column;
                gap: 20px;
            }
            
            .nav-links {
                flex-wrap: wrap;
                justify-content: center;
                gap: 15px;
            }
            
            .input-group {
                flex-direction: column;
            }
            
            .resume-contact {
                flex-direction: column;
                gap: 5px;
                align-items: center;
            }
            
            .list-item {
                flex-direction: column;
                gap: 15px;
            }
            
            .list-actions {
                width: 100%;
                justify-content: flex-end;
            }
        }

        /* Footer */
        .footer {
            background: var(--dark);
            color: white;
            padding: 30px 0;
            text-align: center;
            margin-top: 60px;
        }

        /* Notification */
        .notification {
            position: fixed;
            top: 20px;
            right: 20px;
            background: white;
            padding: 15px 25px;
            border-radius: 10px;
            box-shadow: var(--shadow);
            display: flex;
            align-items: center;
            gap: 10px;
            z-index: 1001;
            animation: slideIn 0.3s ease-out;
            border-left: 4px solid var(--primary);
        }

        .notification.hidden {
            display: none;
        }

        .notification.success {
            border-left-color: #4CAF50;
        }

        .notification.error {
            border-left-color: var(--warning);
        }

        /* Loading */
        .loading {
            display: inline-block;
            width: 20px;
            height: 20px;
            border: 3px solid rgba(255,255,255,.3);
            border-radius: 50%;
            border-top-color: white;
            animation: spin 1s ease-in-out infinite;
        }

        @keyframes spin {
            to { transform: rotate(360deg); }
        }
    </style>
</head>
<body>
    <!-- Welcome Animation -->
    <div class="welcome-overlay" id="welcomeOverlay">
        <div class="welcome-content">
            <h1>StudentPortfolio Pro</h1>
            <p>Your Complete Placement Solution</p>
        </div>
    </div>

    <!-- Notification -->
    <div class="notification hidden" id="notification">
        <i class="fas fa-check-circle"></i>
        <span id="notificationText"></span>
    </div>

    <!-- Login/Signup Page -->
    <div class="auth-container" id="authContainer">
        <div class="auth-card">
            <div class="auth-header">
                <h1>StudentPortfolio Pro</h1>
                <p>Build Your Professional Portfolio</p>
            </div>
            
            <div class="auth-tabs">
                <div class="auth-tab active" data-tab="login">Login</div>
                <div class="auth-tab" data-tab="signup">Sign Up</div>
            </div>
            
            <div class="auth-form-container">
                <form class="auth-form active" id="loginForm">
                    <div class="form-group">
                        <label for="loginEmail">Email Address</label>
                        <input type="email" id="loginEmail" class="form-control" required>
                    </div>
                    
                    <div class="form-group">
                        <label for="loginPassword">Password</label>
                        <input type="password" id="loginPassword" class="form-control" required>
                    </div>
                    
                    <button type="submit" class="btn btn-primary" id="loginBtn">
                        <span>Login to Dashboard</span>
                    </button>
                </form>
                
                <form class="auth-form" id="signupForm">
                    <div class="form-group">
                        <label for="signupName">Full Name</label>
                        <input type="text" id="signupName" class="form-control" required>
                    </div>
                    
                    <div class="form-group">
                        <label for="signupEmail">Email Address</label>
                        <input type="email" id="signupEmail" class="form-control" required>
                    </div>
                    
                    <div class="form-group">
                        <label for="signupPassword">Password</label>
                        <input type="password" id="signupPassword" class="form-control" required>
                    </div>
                    
                    <div class="form-group">
                        <label for="confirmPassword">Confirm Password</label>
                        <input type="password" id="confirmPassword" class="form-control" required>
                    </div>
                    
                    <button type="submit" class="btn btn-primary" id="signupBtn">
                        <span>Create Account</span>
                    </button>
                </form>
            </div>
        </div>
    </div>

    <!-- Dashboard -->
    <div class="dashboard" id="dashboard">
        <nav class="navbar">
            <div class="container nav-container">
                <a href="#" class="logo">StudentPortfolio Pro</a>
                <div class="nav-links">
                    <a href="#" class="nav-link active" data-section="personal">
                        <i class="fas fa-user"></i> Personal
                    </a>
                    <a href="#" class="nav-link" data-section="education">
                        <i class="fas fa-graduation-cap"></i> Education
                    </a>
                    <a href="#" class="nav-link" data-section="skills">
                        <i class="fas fa-code"></i> Skills
                    </a>
                    <a href="#" class="nav-link" data-section="projects">
                        <i class="fas fa-project-diagram"></i> Projects
                    </a>
                    <a href="#" class="nav-link" data-section="certificates">
                        <i class="fas fa-certificate"></i> Certificates
                    </a>
                    <a href="#" class="nav-link" data-section="achievements">
                        <i class="fas fa-trophy"></i> Achievements
                    </a>
                    <a href="#" class="nav-link" data-section="resume">
                        <i class="fas fa-file-pdf"></i> Resume
                    </a>
                    <div class="user-info">
                        <div class="avatar" id="userAvatar">U</div>
                        <span id="userName">User</span>
                        <button class="btn-logout" id="logoutBtn">
                            <i class="fas fa-sign-out-alt"></i> Logout
                        </button>
                    </div>
                </div>
            </div>
        </nav>
        
        <div class="container main-content">
            <!-- Personal Information Section -->
            <section class="section active" id="personalSection">
                <div class="section-header">
                    <h2>Personal Information</h2>
                    <p>Manage your contact details and social links</p>
                </div>
                
                <div class="card">
                    <h3 class="card-title"><i class="fas fa-user-circle"></i> Personal Details</h3>
                    <div class="form-group">
                        <label for="personalName">Full Name *</label>
                        <input type="text" id="personalName" class="form-control">
                    </div>
                    
                    <div class="input-group">
                        <div class="form-group" style="flex: 1;">
                            <label for="personalEmail">Email Address *</label>
                            <input type="email" id="personalEmail" class="form-control">
                        </div>
                        <div class="form-group" style="flex: 1;">
                            <label for="personalPhone">Phone Number *</label>
                            <input type="tel" id="personalPhone" class="form-control">
                        </div>
                    </div>
                    
                    <div class="form-group">
                        <label for="personalLocation">Location</label>
                        <input type="text" id="personalLocation" class="form-control" placeholder="City, Country">
                    </div>
                    
                    <div class="input-group">
                        <div class="form-group" style="flex: 1;">
                            <label for="personalLinkedIn">LinkedIn URL</label>
                            <input type="url" id="personalLinkedIn" class="form-control" placeholder="https://linkedin.com/in/yourname">
                        </div>
                        <div class="form-group" style="flex: 1;">
                            <label for="personalGitHub">GitHub URL</label>
                            <input type="url" id="personalGitHub" class="form-control" placeholder="https://github.com/yourusername">
                        </div>
                    </div>
                    
                    <div class="input-group">
                        <div class="form-group" style="flex: 1;">
                            <label for="personalPortfolio">Portfolio Website</label>
                            <input type="url" id="personalPortfolio" class="form-control" placeholder="https://yourportfolio.com">
                        </div>
                    </div>
                    
                    <button class="btn btn-primary" id="savePersonal">
                        <i class="fas fa-save"></i> Save Personal Information
                    </button>
                </div>
            </section>
            
            <!-- Education Section -->
            <section class="section" id="educationSection">
                <div class="section-header">
                    <h2>Education Details</h2>
                    <p>Add your academic qualifications</p>
                </div>
                
                <div class="card">
                    <h3 class="card-title"><i class="fas fa-graduation-cap"></i> Add Education</h3>
                    <div class="form-group">
                        <label for="eduDegree">Degree / Course *</label>
                        <input type="text" id="eduDegree" class="form-control" placeholder="e.g., Bachelor of Computer Science">
                    </div>
                    
                    <div class="input-group">
                        <div class="form-group" style="flex: 1;">
                            <label for="eduInstitution">College / School *</label>
                            <input type="text" id="eduInstitution" class="form-control" placeholder="University Name">
                        </div>
                        <div class="form-group" style="flex: 1;">
                            <label for="eduYear">Year of Passing *</label>
                            <input type="number" id="eduYear" class="form-control" placeholder="2024" min="2000" max="2030">
                        </div>
                    </div>
                    
                    <div class="form-group">
                        <label for="eduScore">CGPA / Percentage *</label>
                        <input type="text" id="eduScore" class="form-control" placeholder="e.g., 8.5 CGPA or 85%">
                    </div>
                    
                    <button class="btn btn-primary" id="addEducation">
                        <i class="fas fa-plus"></i> Add Education
                    </button>
                </div>
                
                <div class="card">
                    <h3 class="card-title"><i class="fas fa-university"></i> Education History</h3>
                    <div id="educationList" class="empty-state">
                        <i class="fas fa-graduation-cap"></i>
                        <p>No education added yet</p>
                    </div>
                </div>
            </section>
            
            <!-- Skills Section -->
            <section class="section" id="skillsSection">
                <div class="section-header">
                    <h2>Skills Management</h2>
                    <p>Add and manage your technical skills</p>
                </div>
                
                <div class="card">
                    <h3 class="card-title"><i class="fas fa-code"></i> Add Skill</h3>
                    <div class="input-group">
                        <input type="text" id="newSkill" class="form-control" placeholder="e.g., JavaScript, Python, React">
                        <button class="btn-small" id="addSkill">
                            <i class="fas fa-plus"></i> Add
                        </button>
                    </div>
                    <div class="skills-container" id="skillsList">
                        <!-- Skills will be added here dynamically -->
                    </div>
                </div>
            </section>
            
            <!-- Projects Section -->
            <section class="section" id="projectsSection">
                <div class="section-header">
                    <h2>Projects</h2>
                    <p>Showcase your projects with details</p>
                </div>
                
                <div class="card">
                    <h3 class="card-title"><i class="fas fa-project-diagram"></i> Add Project</h3>
                    <div class="form-group">
                        <label for="projectTitle">Project Title *</label>
                        <input type="text" id="projectTitle" class="form-control" placeholder="e.g., E-Commerce Website">
                    </div>
                    
                    <div class="form-group">
                        <label for="projectDescription">Description *</label>
                        <textarea id="projectDescription" class="form-control" rows="3" placeholder="Describe your project..."></textarea>
                    </div>
                    
                    <div class="form-group">
                        <label for="projectTech">Technologies Used *</label>
                        <input type="text" id="projectTech" class="form-control" placeholder="e.g., React, Node.js, MongoDB">
                    </div>
                    
                    <div class="form-group">
                        <label for="projectLink">Project Link (Optional)</label>
                        <input type="url" id="projectLink" class="form-control" placeholder="https://github.com/username/project">
                    </div>
                    
                    <button class="btn btn-primary" id="addProject">
                        <i class="fas fa-plus"></i> Add Project
                    </button>
                </div>
                
                <div class="card">
                    <h3 class="card-title"><i class="fas fa-list"></i> My Projects</h3>
                    <div id="projectsList" class="empty-state">
                        <i class="fas fa-project-diagram"></i>
                        <p>No projects added yet</p>
                    </div>
                </div>
            </section>
            
            <!-- Certificates Section -->
            <section class="section" id="certificatesSection">
                <div class="section-header">
                    <h2>Certificates</h2>
                    <p>Upload and manage your certificates</p>
                </div>
                
                <div class="card">
                    <h3 class="card-title"><i class="fas fa-certificate"></i> Add Certificate</h3>
                    <div class="form-group">
                        <label for="certificateTitle">Certificate Title *</label>
                        <input type="text" id="certificateTitle" class="form-control" placeholder="e.g., AWS Certified Solutions Architect">
                    </div>
                    
                    <div class="form-group">
                        <label for="certificatePlatform">Platform/Issuer *</label>
                        <input type="text" id="certificatePlatform" class="form-control" placeholder="e.g., Coursera, Udemy, AWS">
                    </div>
                    
                    <div class="form-group">
                        <label for="certificateDate">Issue Date</label>
                        <input type="month" id="certificateDate" class="form-control">
                    </div>
                    
                    <div class="form-group">
                        <label for="certificateFile">Upload Certificate (Optional)</label>
                        <div class="file-upload" onclick="document.getElementById('certificateFile').click()">
                            <i class="fas fa-cloud-upload-alt"></i>
                            <p>Click to upload certificate (PDF/Image)</p>
                            <small>Max size: 5MB</small>
                        </div>
                        <input type="file" id="certificateFile" class="form-control" accept=".jpg,.jpeg,.png,.pdf" style="display: none;">
                        <div id="fileName"></div>
                    </div>
                    
                    <button class="btn btn-primary" id="uploadCertificate">
                        <i class="fas fa-upload"></i> Add Certificate
                    </button>
                </div>
                
                <div class="card">
                    <h3 class="card-title"><i class="fas fa-trophy"></i> My Certificates</h3>
                    <div id="certificatesList" class="empty-state">
                        <i class="fas fa-certificate"></i>
                        <p>No certificates added yet</p>
                    </div>
                </div>
            </section>
            
            <!-- Achievements Section -->
            <section class="section" id="achievementsSection">
                <div class="section-header">
                    <h2>Achievements & Trainings</h2>
                    <p>Add your accomplishments and training experiences</p>
                </div>
                
                <div class="card">
                    <h3 class="card-title"><i class="fas fa-medal"></i> Add Achievement/Training</h3>
                    <div class="form-group">
                        <label for="achievementTitle">Title *</label>
                        <input type="text" id="achievementTitle" class="form-control" placeholder="e.g., Hackathon Winner, Workshop on AI">
                    </div>
                    
                    <div class="form-group">
                        <label for="achievementType">Type *</label>
                        <select id="achievementType" class="form-control">
                            <option value="">Select Type</option>
                            <option value="hackathon">Hackathon</option>
                            <option value="workshop">Workshop</option>
                            <option value="training">Online Training</option>
                            <option value="award">Award</option>
                            <option value="internship">Internship</option>
                            <option value="publication">Publication</option>
                            <option value="other">Other</option>
                        </select>
                    </div>
                    
                    <div class="form-group">
                        <label for="achievementDescription">Description *</label>
                        <textarea id="achievementDescription" class="form-control" rows="3" placeholder="Describe your achievement..."></textarea>
                    </div>
                    
                    <div class="form-group">
                        <label for="achievementDate">Date (Optional)</label>
                        <input type="month" id="achievementDate" class="form-control">
                    </div>
                    
                    <button class="btn btn-primary" id="addAchievement">
                        <i class="fas fa-plus"></i> Add Achievement
                    </button>
                </div>
                
                <div class="card">
                    <h3 class="card-title"><i class="fas fa-star"></i> My Achievements</h3>
                    <div id="achievementsList" class="empty-state">
                        <i class="fas fa-trophy"></i>
                        <p>No achievements added yet</p>
                    </div>
                </div>
            </section>
            
            <!-- Resume Section -->
            <section class="section" id="resumeSection">
                <div class="section-header">
                    <h2>Resume Builder</h2>
                    <p>Generate and download your professional resume</p>
                </div>
                
                <div class="card">
                    <div style="text-align: center; margin-bottom: 30px;">
                        <button class="btn btn-primary" id="downloadResume" style="width: auto; padding: 15px 40px;">
                            <i class="fas fa-download"></i> Download Resume as PDF
                        </button>
                        <button class="btn-small" id="refreshResume" style="margin-left: 15px;">
                            <i class="fas fa-sync-alt"></i> Refresh Preview
                        </button>
                    </div>
                    
                    <div class="resume-preview" id="resumePreview">
                        <div class="resume-header">
                            <h1 class="resume-name" id="resumeName">Your Name</h1>
                            <div class="resume-contact" id="resumeContact">
                                <span id="resumeEmail">email@example.com</span>
                                <span id="resumePhone">+1 234 567 8900</span>
                                <span id="resumeLocation">City, Country</span>
                            </div>
                            <div class="resume-contact" id="resumeLinks">
                                <span id="resumeLinkedIn">linkedin.com/in/yourname</span>
                                <span id="resumeGitHub">github.com/username</span>
                                <span id="resumePortfolio">yourportfolio.com</span>
                            </div>
                        </div>
                        
                        <div class="resume-section">
                            <h3 class="resume-section-title">Education</h3>
                            <div id="resumeEducation">
                                <p>No education added yet</p>
                            </div>
                        </div>
                        
                        <div class="resume-section">
                            <h3 class="resume-section-title">Skills</h3>
                            <div id="resumeSkills">
                                <p>No skills added yet</p>
                            </div>
                        </div>
                        
                        <div class="resume-section">
                            <h3 class="resume-section-title">Projects</h3>
                            <div id="resumeProjects">
                                <p>No projects added yet</p>
                            </div>
                        </div>
                        
                        <div class="resume-section">
                            <h3 class="resume-section-title">Certifications & Achievements</h3>
                            <div id="resumeCertifications">
                                <p>No certifications or achievements added yet</p>
                            </div>
                        </div>
                    </div>
                </div>
            </section>
        </div>
        
        <div class="footer">
            <div class="container">
                <p>StudentPortfolio Pro &copy; 2023 | Your Complete Placement Solution</p>
                <p style="margin-top: 10px; opacity: 0.8;">All data is securely stored in your browser's LocalStorage</p>
            </div>
        </div>
    </div>

    <script>
        // DOM Elements
        const welcomeOverlay = document.getElementById('welcomeOverlay');
        const authContainer = document.getElementById('authContainer');
        const dashboard = document.getElementById('dashboard');
        const notification = document.getElementById('notification');
        const notificationText = document.getElementById('notificationText');
        
        // Auth Elements
        const authTabs = document.querySelectorAll('.auth-tab');
        const authForms = document.querySelectorAll('.auth-form');
        const loginForm = document.getElementById('loginForm');
        const signupForm = document.getElementById('signupForm');
        const loginBtn = document.getElementById('loginBtn');
        const signupBtn = document.getElementById('signupBtn');
        const logoutBtn = document.getElementById('logoutBtn');
        
        // Navigation Elements
        const navLinks = document.querySelectorAll('.nav-link');
        const sections = document.querySelectorAll('.section');
        const userAvatar = document.getElementById('userAvatar');
        const userName = document.getElementById('userName');
        
        // Personal Info Elements
        const savePersonalBtn = document.getElementById('savePersonal');
        
        // Education Elements
        const addEducationBtn = document.getElementById('addEducation');
        const educationList = document.getElementById('educationList');
        
        // Skills Elements
        const addSkillBtn = document.getElementById('addSkill');
        const newSkillInput = document.getElementById('newSkill');
        const skillsList = document.getElementById('skillsList');
        
        // Projects Elements
        const addProjectBtn = document.getElementById('addProject');
        const projectsList = document.getElementById('projectsList');
        
        // Certificates Elements
        const uploadCertificateBtn = document.getElementById('uploadCertificate');
        const certificateFile = document.getElementById('certificateFile');
        const certificatesList = document.getElementById('certificatesList');
        
        // Achievements Elements
        const addAchievementBtn = document.getElementById('addAchievement');
        const achievementsList = document.getElementById('achievementsList');
        
        // Resume Elements
        const downloadResumeBtn = document.getElementById('downloadResume');
        const refreshResumeBtn = document.getElementById('refreshResume');
        const resumePreview = document.getElementById('resumePreview');
        
        // App State
        let currentUser = null;
        
        // Utility Functions
        function showNotification(message, type = 'success') {
            notification.className = `notification ${type}`;
            notificationText.textContent = message;
            notification.classList.remove('hidden');
            
            const icon = notification.querySelector('i');
            if (type === 'success') {
                icon.className = 'fas fa-check-circle';
            } else {
                icon.className = 'fas fa-exclamation-circle';
            }
            
            setTimeout(() => {
                notification.classList.add('hidden');
            }, 3000);
        }
        
        function validateEmail(email) {
            const re = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
            return re.test(email);
        }
        
        function validatePassword(password) {
            return password.length >= 6;
        }
        
        function getInitials(name) {
            return name.split(' ').map(n => n[0]).join('').toUpperCase().substring(0, 2);
        }
        
        function formatDate(dateString) {
            if (!dateString) return '';
            const date = new Date(dateString);
            return date.toLocaleDateString('en-US', { month: 'short', year: 'numeric' });
        }
        
        // Data Management Functions
        function getCurrentUserData() {
            const allUsers = JSON.parse(localStorage.getItem('studentPortfolioUsers')) || {};
            return allUsers[currentUser] || null;
        }
        
        function saveCurrentUserData(data) {
            const allUsers = JSON.parse(localStorage.getItem('studentPortfolioUsers')) || {};
            allUsers[currentUser] = data;
            localStorage.setItem('studentPortfolioUsers', JSON.stringify(allUsers));
        }
        
        function initializeUserData() {
            const defaultData = {
                personal: {},
                education: [],
                skills: [],
                projects: [],
                certificates: [],
                achievements: []
            };
            
            const userData = getCurrentUserData();
            if (!userData) {
                saveCurrentUserData(defaultData);
                return defaultData;
            }
            return userData;
        }
        
        // Welcome animation timeout
        setTimeout(() => {
            welcomeOverlay.style.display = 'none';
        }, 3000);
        
        // Auth tab switching
        authTabs.forEach(tab => {
            tab.addEventListener('click', () => {
                const targetTab = tab.getAttribute('data-tab');
                
                // Update active tab
                authTabs.forEach(t => t.classList.remove('active'));
                tab.classList.add('active');
                
                // Show corresponding form
                authForms.forEach(form => {
                    form.classList.remove('active');
                    if (form.id === `${targetTab}Form`) {
                        form.classList.add('active');
                    }
                });
            });
        });
        
        // Login form submission
        loginForm.addEventListener('submit', async (e) => {
            e.preventDefault();
            
            const email = document.getElementById('loginEmail').value.trim();
            const password = document.getElementById('loginPassword').value;
            
            if (!email || !password) {
                showNotification('Please enter both email and password', 'error');
                return;
            }
            
            if (!validateEmail(email)) {
                showNotification('Please enter a valid email address', 'error');
                return;
            }
            
            // Show loading state
            const originalText = loginBtn.innerHTML;
            loginBtn.innerHTML = '<div class="loading"></div>';
            loginBtn.disabled = true;
            
            // Simulate API call
            await new Promise(resolve => setTimeout(resolve, 1000));
            
            const allUsers = JSON.parse(localStorage.getItem('studentPortfolioUsers')) || {};
            
            if (allUsers[email]) {
                // User exists, check password
                const user = allUsers[email];
                if (user.password === password) {
                    // Login successful
                    currentUser = email;
                    localStorage.setItem('currentUser', email);
                    
                    // Update UI
                    const initials = getInitials(user.personal?.name || email);
                    userAvatar.textContent = initials;
                    userName.textContent = user.personal?.name || email.split('@')[0];
                    
                    // Show dashboard
                    authContainer.style.display = 'none';
                    dashboard.style.display = 'block';
                    
                    // Load user data
                    loadUserData();
                    
                    showNotification('Login successful!');
                } else {
                    showNotification('Invalid password', 'error');
                }
            } else {
                showNotification('User not found. Please sign up first.', 'error');
            }
            
            // Reset button state
            loginBtn.innerHTML = originalText;
            loginBtn.disabled = false;
        });
        
        // Signup form submission
        signupForm.addEventListener('submit', async (e) => {
            e.preventDefault();
            
            const name = document.getElementById('signupName').value.trim();
            const email = document.getElementById('signupEmail').value.trim();
            const password = document.getElementById('signupPassword').value;
            const confirmPassword = document.getElementById('confirmPassword').value;
            
            // Validation
            if (!name || !email || !password || !confirmPassword) {
                showNotification('Please fill in all fields', 'error');
                return;
            }
            
            if (!validateEmail(email)) {
                showNotification('Please enter a valid email address', 'error');
                return;
            }
            
            if (!validatePassword(password)) {
                showNotification('Password must be at least 6 characters long', 'error');
                return;
            }
            
            if (password !== confirmPassword) {
                showNotification('Passwords do not match', 'error');
                return;
            }
            
            // Show loading state
            const originalText = signupBtn.innerHTML;
            signupBtn.innerHTML = '<div class="loading"></div>';
            signupBtn.disabled = true;
            
            // Simulate API call
            await new Promise(resolve => setTimeout(resolve, 1000));
            
            const allUsers = JSON.parse(localStorage.getItem('studentPortfolioUsers')) || {};
            
            if (allUsers[email]) {
                showNotification('User already exists. Please login.', 'error');
            } else {
                // Create new user
                allUsers[email] = {
                    password: password,
                    personal: { name: name, email: email },
                    education: [],
                    skills: [],
                    projects: [],
                    certificates: [],
                    achievements: []
                };
                
                localStorage.setItem('studentPortfolioUsers', JSON.stringify(allUsers));
                
                // Set as current user
                currentUser = email;
                localStorage.setItem('currentUser', email);
                
                // Update UI
                const initials = getInitials(name);
                userAvatar.textContent = initials;
                userName.textContent = name;
                
                // Show dashboard
                authContainer.style.display = 'none';
                dashboard.style.display = 'block';
                
                // Initialize user data
                initializeUserData();
                loadUserData();
                
                showNotification('Account created successfully!');
            }
            
            // Reset button state
            signupBtn.innerHTML = originalText;
            signupBtn.disabled = false;
        });
        
        // Logout functionality
        logoutBtn.addEventListener('click', () => {
            currentUser = null;
            localStorage.removeItem('currentUser');
            
            // Reset forms
            loginForm.reset();
            signupForm.reset();
            
            // Reset auth tabs
            authTabs.forEach(tab => tab.classList.remove('active'));
            authTabs[0].classList.add('active');
            
            authForms.forEach(form => form.classList.remove('active'));
            authForms[0].classList.add('active');
            
            // Show auth container
            dashboard.style.display = 'none';
            authContainer.style.display = 'flex';
            
            showNotification('Logged out successfully');
        });
        
        // Navigation between sections
        navLinks.forEach(link => {
            link.addEventListener('click', (e) => {
                e.preventDefault();
                
                // Update active nav link
                navLinks.forEach(l => l.classList.remove('active'));
                link.classList.add('active');
                
                // Show corresponding section
                const sectionId = link.getAttribute('data-section');
                sections.forEach(section => {
                    section.classList.remove('active');
                    if (section.id === `${sectionId}Section`) {
                        section.classList.add('active');
                    }
                });
                
                // Update resume preview when resume tab is clicked
                if (sectionId === 'resume') {
                    updateResumePreview();
                }
            });
        });
        
        // Load user data into forms
        function loadUserData() {
            const userData = getCurrentUserData();
            if (!userData) return;
            
            // Load personal data
            if (userData.personal) {
                const personal = userData.personal;
                document.getElementById('personalName').value = personal.name || '';
                document.getElementById('personalEmail').value = personal.email || '';
                document.getElementById('personalPhone').value = personal.phone || '';
                document.getElementById('personalLocation').value = personal.location || '';
                document.getElementById('personalLinkedIn').value = personal.linkedin || '';
                document.getElementById('personalGitHub').value = personal.github || '';
                document.getElementById('personalPortfolio').value = personal.portfolio || '';
            }
            
            // Load education data
            renderEducationList();
            
            // Load skills data
            renderSkillsList();
            
            // Load projects data
            renderProjectsList();
            
            // Load certificates data
            renderCertificatesList();
            
            // Load achievements data
            renderAchievementsList();
        }
        
        // Save personal information
        savePersonalBtn.addEventListener('click', () => {
            const personalData = {
                name: document.getElementById('personalName').value.trim(),
                email: document.getElementById('personalEmail').value.trim(),
                phone: document.getElementById('personalPhone').value.trim(),
                location: document.getElementById('personalLocation').value.trim(),
                linkedin: document.getElementById('personalLinkedIn').value.trim(),
                github: document.getElementById('personalGitHub').value.trim(),
                portfolio: document.getElementById('personalPortfolio').value.trim()
            };
            
            // Validation
            if (!personalData.name || !personalData.email || !personalData.phone) {
                showNotification('Please fill in all required fields (Name, Email, Phone)', 'error');
                return;
            }
            
            if (!validateEmail(personalData.email)) {
                showNotification('Please enter a valid email address', 'error');
                return;
            }
            
            const userData = getCurrentUserData();
            userData.personal = personalData;
            saveCurrentUserData(userData);
            
            // Update UI
            const initials = getInitials(personalData.name);
            userAvatar.textContent = initials;
            userName.textContent = personalData.name;
            
            showNotification('Personal information saved successfully!');
        });
        
        // Education management
        addEducationBtn.addEventListener('click', () => {
            const degree = document.getElementById('eduDegree').value.trim();
            const institution = document.getElementById('eduInstitution').value.trim();
            const year = document.getElementById('eduYear').value;
            const score = document.getElementById('eduScore').value.trim();
            
            if (!degree || !institution || !year || !score) {
                showNotification('Please fill all education fields', 'error');
                return;
            }
            
            const userData = getCurrentUserData();
            const newEducation = {
                id: Date.now(),
                degree,
                institution,
                year,
                score
            };
            
            userData.education.push(newEducation);
            saveCurrentUserData(userData);
            
            // Clear form
            document.getElementById('eduDegree').value = '';
            document.getElementById('eduInstitution').value = '';
            document.getElementById('eduYear').value = '';
            document.getElementById('eduScore').value = '';
            
            renderEducationList();
            showNotification('Education added successfully!');
        });
        
        function renderEducationList() {
            const userData = getCurrentUserData();
            const educationContainer = document.getElementById('educationList');
            
            if (!userData.education || userData.education.length === 0) {
                educationContainer.innerHTML = `
                    <div class="empty-state">
                        <i class="fas fa-graduation-cap"></i>
                        <p>No education added yet</p>
                    </div>
                `;
                return;
            }
            
            educationContainer.innerHTML = '';
            userData.education.forEach((edu, index) => {
                const eduItem = document.createElement('div');
                eduItem.className = 'list-item';
                eduItem.innerHTML = `
                    <div class="list-item-content">
                        <h4>${edu.degree}</h4>
                        <p>${edu.institution}</p>
                        <p>Year: ${edu.year} | Score: ${edu.score}</p>
                    </div>
                    <div class="list-actions">
                        <button class="btn-small btn-danger" onclick="deleteEducation(${edu.id})">
                            <i class="fas fa-trash"></i> Delete
                        </button>
                    </div>
                `;
                educationContainer.appendChild(eduItem);
            });
        }
        
        // Skills management
        addSkillBtn.addEventListener('click', () => {
            const skill = newSkillInput.value.trim();
            
            if (!skill) {
                showNotification('Please enter a skill', 'error');
                return;
            }
            
            const userData = getCurrentUserData();
            
            // Check if skill already exists
            if (userData.skills.includes(skill)) {
                showNotification('Skill already exists', 'error');
                return;
            }
            
            userData.skills.push(skill);
            saveCurrentUserData(userData);
            
            // Clear input
            newSkillInput.value = '';
            
            renderSkillsList();
            showNotification('Skill added successfully!');
        });
        
        function renderSkillsList() {
            const userData = getCurrentUserData();
            const skillsContainer = document.getElementById('skillsList');
            
            if (!userData.skills || userData.skills.length === 0) {
                skillsContainer.innerHTML = '';
                return;
            }
            
            skillsContainer.innerHTML = '';
            userData.skills.forEach((skill, index) => {
                const skillTag = document.createElement('div');
                skillTag.className = 'skill-tag';
                skillTag.innerHTML = `
                    ${skill}
                    <i class="fas fa-times delete-skill" onclick="deleteSkill(${index})"></i>
                `;
                skillsContainer.appendChild(skillTag);
            });
        }
        
        // Projects management
        addProjectBtn.addEventListener('click', () => {
            const title = document.getElementById('projectTitle').value.trim();
            const description = document.getElementById('projectDescription').value.trim();
            const tech = document.getElementById('projectTech').value.trim();
            const link = document.getElementById('projectLink').value.trim();
            
            if (!title || !description || !tech) {
                showNotification('Please fill all required project fields', 'error');
                return;
            }
            
            const userData = getCurrentUserData();
            const newProject = {
                id: Date.now(),
                title,
                description,
                tech,
                link
            };
            
            userData.projects.push(newProject);
            saveCurrentUserData(userData);
            
            // Clear form
            document.getElementById('projectTitle').value = '';
            document.getElementById('projectDescription').value = '';
            document.getElementById('projectTech').value = '';
            document.getElementById('projectLink').value = '';
            
            renderProjectsList();
            showNotification('Project added successfully!');
        });
        
        function renderProjectsList() {
            const userData = getCurrentUserData();
            const projectsContainer = document.getElementById('projectsList');
            
            if (!userData.projects || userData.projects.length === 0) {
                projectsContainer.innerHTML = `
                    <div class="empty-state">
                        <i class="fas fa-project-diagram"></i>
                        <p>No projects added yet</p>
                    </div>
                `;
                return;
            }
            
            projectsContainer.innerHTML = '';
            userData.projects.forEach((project, index) => {
                const projectItem = document.createElement('div');
                projectItem.className = 'list-item';
                projectItem.innerHTML = `
                    <div class="list-item-content">
                        <h4>${project.title}</h4>
                        <p>${project.description}</p>
                        <p><strong>Technologies:</strong> ${project.tech}</p>
                        ${project.link ? `<p><strong>Link:</strong> <a href="${project.link}" target="_blank">${project.link}</a></p>` : ''}
                    </div>
                    <div class="list-actions">
                        <button class="btn-small btn-danger" onclick="deleteProject(${project.id})">
                            <i class="fas fa-trash"></i> Delete
                        </button>
                    </div>
                `;
                projectsContainer.appendChild(projectItem);
            });
        }
        
        // Certificates management
        certificateFile.addEventListener('change', function(e) {
            const fileName = this.files[0]?.name || 'No file selected';
            document.getElementById('fileName').textContent = `Selected: ${fileName}`;
        });
        
        uploadCertificateBtn.addEventListener('click', () => {
            const title = document.getElementById('certificateTitle').value.trim();
            const platform = document.getElementById('certificatePlatform').value.trim();
            const date = document.getElementById('certificateDate').value;
            const file = certificateFile.files[0];
            
            if (!title || !platform) {
                showNotification('Please fill all required certificate fields', 'error');
                return;
            }
            
            const userData = getCurrentUserData();
            const newCertificate = {
                id: Date.now(),
                title,
                platform,
                date,
                fileName: file ? file.name : null
            };
            
            userData.certificates.push(newCertificate);
            saveCurrentUserData(userData);
            
            // Clear form
            document.getElementById('certificateTitle').value = '';
            document.getElementById('certificatePlatform').value = '';
            document.getElementById('certificateDate').value = '';
            certificateFile.value = '';
            document.getElementById('fileName').textContent = '';
            
            renderCertificatesList();
            showNotification('Certificate added successfully!');
        });
        
        function renderCertificatesList() {
            const userData = getCurrentUserData();
            const certificatesContainer = document.getElementById('certificatesList');
            
            if (!userData.certificates || userData.certificates.length === 0) {
                certificatesContainer.innerHTML = `
                    <div class="empty-state">
                        <i class="fas fa-certificate"></i>
                        <p>No certificates added yet</p>
                    </div>
                `;
                return;
            }
            
            certificatesContainer.innerHTML = '';
            userData.certificates.forEach((cert, index) => {
                const certItem = document.createElement('div');
                certItem.className = 'list-item';
                certItem.innerHTML = `
                    <div class="list-item-content">
                        <h4>${cert.title}</h4>
                        <p>Issued by: ${cert.platform}</p>
                        ${cert.date ? `<p>Date: ${formatDate(cert.date + '-01')}</p>` : ''}
                        ${cert.fileName ? `<p>File: ${cert.fileName}</p>` : ''}
                    </div>
                    <div class="list-actions">
                        <button class="btn-small" style="margin-right: 10px;">
                            <i class="fas fa-eye"></i> View
                        </button>
                        <button class="btn-small btn-danger" onclick="deleteCertificate(${cert.id})">
                            <i class="fas fa-trash"></i> Delete
                        </button>
                    </div>
                `;
                certificatesContainer.appendChild(certItem);
            });
        }
        
        // Achievements management
        addAchievementBtn.addEventListener('click', () => {
            const title = document.getElementById('achievementTitle').value.trim();
            const type = document.getElementById('achievementType').value;
            const description = document.getElementById('achievementDescription').value.trim();
            const date = document.getElementById('achievementDate').value;
            
            if (!title || !type || !description) {
                showNotification('Please fill all required achievement fields', 'error');
                return;
            }
            
            const userData = getCurrentUserData();
            const newAchievement = {
                id: Date.now(),
                title,
                type,
                description,
                date
            };
            
            userData.achievements.push(newAchievement);
            saveCurrentUserData(userData);
            
            // Clear form
            document.getElementById('achievementTitle').value = '';
            document.getElementById('achievementType').value = '';
            document.getElementById('achievementDescription').value = '';
            document.getElementById('achievementDate').value = '';
            
            renderAchievementsList();
            showNotification('Achievement added successfully!');
        });
        
        function renderAchievementsList() {
            const userData = getCurrentUserData();
            const achievementsContainer = document.getElementById('achievementsList');
            
            if (!userData.achievements || userData.achievements.length === 0) {
                achievementsContainer.innerHTML = `
                    <div class="empty-state">
                        <i class="fas fa-trophy"></i>
                        <p>No achievements added yet</p>
                    </div>
                `;
                return;
            }
            
            achievementsContainer.innerHTML = '';
            userData.achievements.forEach((achievement, index) => {
                const achievementItem = document.createElement('div');
                achievementItem.className = 'list-item';
                
                // Map type to icon
                let icon = 'fas fa-star';
                let typeText = 'Achievement';
                switch(achievement.type) {
                    case 'hackathon': icon = 'fas fa-code'; typeText = 'Hackathon'; break;
                    case 'workshop': icon = 'fas fa-chalkboard-teacher'; typeText = 'Workshop'; break;
                    case 'training': icon = 'fas fa-laptop'; typeText = 'Training'; break;
                    case 'award': icon = 'fas fa-trophy'; typeText = 'Award'; break;
                    case 'internship': icon = 'fas fa-briefcase'; typeText = 'Internship'; break;
                    case 'publication': icon = 'fas fa-book'; typeText = 'Publication'; break;
                }
                
                achievementItem.innerHTML = `
                    <div style="display: flex; align-items: flex-start; gap: 15px;">
                        <i class="${icon}" style="font-size: 1.5rem; color: var(--primary); margin-top: 5px;"></i>
                        <div class="list-item-content">
                            <h4>${achievement.title}</h4>
                            <p><strong>Type:</strong> ${typeText}</p>
                            <p>${achievement.description}</p>
                            ${achievement.date ? `<p><strong>Date:</strong> ${formatDate(achievement.date + '-01')}</p>` : ''}
                        </div>
                    </div>
                    <div class="list-actions">
                        <button class="btn-small btn-danger" onclick="deleteAchievement(${achievement.id})">
                            <i class="fas fa-trash"></i> Delete
                        </button>
                    </div>
                `;
                achievementsContainer.appendChild(achievementItem);
            });
        }
        
        // Resume preview and download
        refreshResumeBtn.addEventListener('click', () => {
            updateResumePreview();
            showNotification('Resume preview updated!');
        });
        
        function updateResumePreview() {
            const userData = getCurrentUserData();
            if (!userData) return;
            
            // Update personal info
            if (userData.personal) {
                const p = userData.personal;
                document.getElementById('resumeName').textContent = p.name || 'Your Name';
                
                const contact = [];
                if (p.email) contact.push(p.email);
                if (p.phone) contact.push(p.phone);
                if (p.location) contact.push(p.location);
                document.getElementById('resumeContact').innerHTML = contact.map(c => `<span>${c}</span>`).join('');
                
                const links = [];
                if (p.linkedin) links.push(`<span>${p.linkedin}</span>`);
                if (p.github) links.push(`<span>${p.github}</span>`);
                if (p.portfolio) links.push(`<span>${p.portfolio}</span>`);
                document.getElementById('resumeLinks').innerHTML = links.join('');
            }
            
            // Update education
            const resumeEducation = document.getElementById('resumeEducation');
            if (userData.education && userData.education.length > 0) {
                resumeEducation.innerHTML = userData.education.map(edu => `
                    <div class="resume-item">
                        <div class="resume-item-title">${edu.degree}</div>
                        <div class="resume-item-subtitle">${edu.institution}</div>
                        <div class="resume-item-details">${edu.year} | ${edu.score}</div>
                    </div>
                `).join('');
            } else {
                resumeEducation.innerHTML = '<p>No education added yet</p>';
            }
            
            // Update skills
            const resumeSkills = document.getElementById('resumeSkills');
            if (userData.skills && userData.skills.length > 0) {
                resumeSkills.innerHTML = `
                    <div class="resume-skills-list">
                        ${userData.skills.map(skill => `<span class="resume-skill">${skill}</span>`).join('')}
                    </div>
                `;
            } else {
                resumeSkills.innerHTML = '<p>No skills added yet</p>';
            }
            
            // Update projects
            const resumeProjects = document.getElementById('resumeProjects');
            if (userData.projects && userData.projects.length > 0) {
                resumeProjects.innerHTML = userData.projects.map(project => `
                    <div class="resume-item">
                        <div class="resume-item-title">${project.title}</div>
                        <div class="resume-item-details">${project.description}</div>
                        <div class="resume-item-details"><strong>Technologies:</strong> ${project.tech}</div>
                    </div>
                `).join('');
            } else {
                resumeProjects.innerHTML = '<p>No projects added yet</p>';
            }
            
            // Update certifications and achievements
            const resumeCertifications = document.getElementById('resumeCertifications');
            const allItems = [];
            
            if (userData.certificates && userData.certificates.length > 0) {
                userData.certificates.forEach(cert => {
                    allItems.push(`
                        <div class="resume-item">
                            <div class="resume-item-title">${cert.title}</div>
                            <div class="resume-item-details">${cert.platform}${cert.date ? ` • ${formatDate(cert.date + '-01')}` : ''}</div>
                        </div>
                    `);
                });
            }
            
            if (userData.achievements && userData.achievements.length > 0) {
                userData.achievements.forEach(achievement => {
                    allItems.push(`
                        <div class="resume-item">
                            <div class="resume-item-title">${achievement.title}</div>
                            <div class="resume-item-details">${achievement.description}${achievement.date ? ` • ${formatDate(achievement.date + '-01')}` : ''}</div>
                        </div>
                    `);
                });
            }
            
            if (allItems.length > 0) {
                resumeCertifications.innerHTML = allItems.join('');
            } else {
                resumeCertifications.innerHTML = '<p>No certifications or achievements added yet</p>';
            }
        }
        
        // Download resume as PDF
        downloadResumeBtn.addEventListener('click', () => {
            updateResumePreview();
            
            const element = document.getElementById('resumePreview');
            const opt = {
                margin: [10, 10],
                filename: 'resume.pdf',
                image: { type: 'jpeg', quality: 0.98 },
                html2canvas: { 
                    scale: 2,
                    useCORS: true,
                    logging: false
                },
                jsPDF: { 
                    unit: 'mm', 
                    format: 'a4', 
                    orientation: 'portrait' 
                }
            };
            
            // Show loading
            const originalText = downloadResumeBtn.innerHTML;
            downloadResumeBtn.innerHTML = '<div class="loading"></div>';
            downloadResumeBtn.disabled = true;
            
            // Generate PDF
            html2pdf().set(opt).from(element).save().then(() => {
                showNotification('Resume downloaded successfully!');
                // Reset button
                downloadResumeBtn.innerHTML = originalText;
                downloadResumeBtn.disabled = false;
            }).catch(err => {
                showNotification('Error downloading resume. Please try again.', 'error');
                console.error('PDF generation error:', err);
                // Reset button
                downloadResumeBtn.innerHTML = originalText;
                downloadResumeBtn.disabled = false;
            });
        });
        
        // Delete functions (global for onclick handlers)
        window.deleteEducation = function(id) {
            const userData = getCurrentUserData();
            userData.education = userData.education.filter(edu => edu.id !== id);
            saveCurrentUserData(userData);
            renderEducationList();
            showNotification('Education deleted successfully!');
        };
        
        window.deleteSkill = function(index) {
            const userData = getCurrentUserData();
            userData.skills.splice(index, 1);
            saveCurrentUserData(userData);
            renderSkillsList();
            showNotification('Skill deleted successfully!');
        };
        
        window.deleteProject = function(id) {
            const userData = getCurrentUserData();
            userData.projects = userData.projects.filter(project => project.id !== id);
            saveCurrentUserData(userData);
            renderProjectsList();
            showNotification('Project deleted successfully!');
        };
        
        window.deleteCertificate = function(id) {
            const userData = getCurrentUserData();
            userData.certificates = userData.certificates.filter(cert => cert.id !== id);
            saveCurrentUserData(userData);
            renderCertificatesList();
            showNotification('Certificate deleted successfully!');
        };
        
        window.deleteAchievement = function(id) {
            const userData = getCurrentUserData();
            userData.achievements = userData.achievements.filter(achievement => achievement.id !== id);
            saveCurrentUserData(userData);
            renderAchievementsList();
            showNotification('Achievement deleted successfully!');
        };
        
        // Initialize the app
        document.addEventListener('DOMContentLoaded', () => {
            // Check if user is already logged in
            const savedUser = localStorage.getItem('currentUser');
            if (savedUser) {
                currentUser = savedUser;
                
                // Get user data
                const userData = getCurrentUserData();
                if (userData) {
                    // Update UI
                    const initials = getInitials(userData.personal?.name || savedUser);
                    userAvatar.textContent = initials;
                    userName.textContent = userData.personal?.name || savedUser.split('@')[0];
                    
                    // Show dashboard
                    authContainer.style.display = 'none';
                    dashboard.style.display = 'block';
                    
                    // Load user data
                    loadUserData();
                } else {
                    // User data not found, clear saved user
                    localStorage.removeItem('currentUser');
                }
            }
            
            // Initialize skills list
            renderSkillsList();
        });
        
        // File upload display
        certificateFile.addEventListener('change', function() {
            if (this.files.length > 0) {
                document.getElementById('fileName').textContent = `Selected file: ${this.files[0].name}`;
            }
        });
    </script>
</body>
</html>
