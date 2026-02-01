<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Campus Bridge - EGS Pillay Engineering College</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700;800&display=swap" rel="stylesheet">
    <style>
        * { font-family: 'Inter', sans-serif; }
        .card-hover { transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1); }
        .card-hover:hover { transform: translateY(-4px); box-shadow: 0 20px 25px -5px rgba(0, 0, 0, 0.1), 0 10px 10px -5px rgba(0, 0, 0, 0.04); }
        .gradient-bg { background: linear-gradient(135deg, #667eea 0%, #764ba2 100%); }
        .gradient-header { background: linear-gradient(135deg, #1e3a8a 0%, #3b82f6 100%); }
        .priority-high { background: linear-gradient(135deg, #dc2626 0%, #991b1b 100%); }
        .priority-today { background: linear-gradient(135deg, #f59e0b 0%, #d97706 100%); }
        .priority-upcoming { background: linear-gradient(135deg, #10b981 0%, #059669 100%); }
        .shimmer { animation: shimmer 2s infinite; }
        @keyframes shimmer { 0%, 100% { opacity: 1; } 50% { opacity: 0.5; } }
        .sidebar-active { background: rgba(59, 130, 246, 0.1); border-left: 4px solid #3b82f6; }
        .modal { display: none; position: fixed; z-index: 1000; left: 0; top: 0; width: 100%; height: 100%; background-color: rgba(0,0,0,0.5); }
        .modal.active { display: flex; align-items: center; justify-content: center; }
        .fade-in { animation: fadeIn 0.3s ease-in; }
        @keyframes fadeIn { from { opacity: 0; transform: translateY(-20px); } to { opacity: 1; transform: translateY(0); } }
        .notification-badge { animation: pulse 2s cubic-bezier(0.4, 0, 0.6, 1) infinite; }
        @keyframes pulse { 0%, 100% { opacity: 1; } 50% { opacity: .5; } }
    </style>
</head>
<body class="bg-gray-50">
    
    <!-- Mobile Menu Button -->
    <button id="mobileMenuBtn" class="lg:hidden fixed top-4 left-4 z-50 bg-blue-600 text-white p-3 rounded-lg shadow-lg">
        <svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 6h16M4 12h16M4 18h16"></path>
        </svg>
    </button>

    <!-- Sidebar -->
    <aside id="sidebar" class="fixed left-0 top-0 h-full w-72 bg-white shadow-xl z-40 transform -translate-x-full lg:translate-x-0 transition-transform duration-300">
        <div class="gradient-header p-6 text-white">
            <div class="flex items-center gap-3 mb-2">
                <div class="bg-white/20 p-2 rounded-lg">
                    <svg class="w-8 h-8" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19 21V5a2 2 0 00-2-2H7a2 2 0 00-2 2v16m14 0h2m-2 0h-5m-9 0H3m2 0h5M9 7h1m-1 4h1m4-4h1m-1 4h1m-5 10v-5a1 1 0 011-1h2a1 1 0 011 1v5m-4 0h4"></path>
                    </svg>
                </div>
                <div>
                    <h1 class="text-lg font-bold leading-tight">Campus Bridge</h1>
                    <p class="text-xs text-blue-100">Unified Communication Platform</p>
                </div>
            </div>
            <div class="mt-4 pt-4 border-t border-white/20">
                <p class="text-sm font-semibold">EGS Pillay Engineering College</p>
                <p class="text-xs text-blue-100 mt-1">Thittacherry, Nagapattinam – 611002</p>
            </div>
        </div>

        <nav class="p-4">
            <div class="mb-6">
                <p class="text-xs font-semibold text-gray-400 uppercase tracking-wider mb-3">Main Menu</p>
                <button onclick="switchView('feed')" id="nav-feed" class="sidebar-active w-full flex items-center gap-3 px-4 py-3 rounded-lg text-left hover:bg-gray-50 transition-colors mb-2">
                    <svg class="w-5 h-5 text-blue-600" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19 20H5a2 2 0 01-2-2V6a2 2 0 012-2h10a2 2 0 012 2v1m2 13a2 2 0 01-2-2V7m2 13a2 2 0 002-2V9a2 2 0 00-2-2h-2m-4-3H9M7 16h6M7 8h6v4H7V8z"></path>
                    </svg>
                    <div class="flex-1">
                        <p class="font-semibold text-gray-800">Announcement Feed</p>
                        <p class="text-xs text-gray-500">All updates</p>
                    </div>
                    <span id="feed-badge" class="notification-badge bg-blue-600 text-white text-xs font-bold px-2 py-1 rounded-full">0</span>
                </button>

                <button onclick="switchView('archive')" id="nav-archive" class="w-full flex items-center gap-3 px-4 py-3 rounded-lg text-left hover:bg-gray-50 transition-colors mb-2">
                    <svg class="w-5 h-5 text-gray-600" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M5 8h14M5 8a2 2 0 110-4h14a2 2 0 110 4M5 8v10a2 2 0 002 2h10a2 2 0 002-2V8m-9 4h4"></path>
                    </svg>
                    <div class="flex-1">
                        <p class="font-semibold text-gray-800">Archive & History</p>
                        <p class="text-xs text-gray-500">Past records</p>
                    </div>
                </button>

                <button onclick="switchView('admin')" id="nav-admin" class="w-full flex items-center gap-3 px-4 py-3 rounded-lg text-left hover:bg-gray-50 transition-colors">
                    <svg class="w-5 h-5 text-gray-600" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 6V4m0 2a2 2 0 100 4m0-4a2 2 0 110 4m-6 8a2 2 0 100-4m0 4a2 2 0 110-4m0 4v2m0-6V4m6 6v10m6-2a2 2 0 100-4m0 4a2 2 0 110-4m0 4v2m0-6V4"></path>
                    </svg>
                    <div class="flex-1">
                        <p class="font-semibold text-gray-800">Admin Panel</p>
                        <p class="text-xs text-gray-500">Manage posts</p>
                    </div>
                </button>
            </div>

            <div class="mb-6">
                <p class="text-xs font-semibold text-gray-400 uppercase tracking-wider mb-3">Priority Filters</p>
                <button onclick="filterByPriority('High Priority')" class="w-full flex items-center gap-3 px-4 py-2.5 rounded-lg text-left hover:bg-red-50 transition-colors mb-2 group">
                    <div class="w-3 h-3 bg-red-500 rounded-full"></div>
                    <span class="text-sm font-medium text-gray-700 group-hover:text-red-700">High Priority</span>
                </button>
                <button onclick="filterByPriority('Today')" class="w-full flex items-center gap-3 px-4 py-2.5 rounded-lg text-left hover:bg-yellow-50 transition-colors mb-2 group">
                    <div class="w-3 h-3 bg-yellow-500 rounded-full"></div>
                    <span class="text-sm font-medium text-gray-700 group-hover:text-yellow-700">Today</span>
                </button>
                <button onclick="filterByPriority('Upcoming')" class="w-full flex items-center gap-3 px-4 py-2.5 rounded-lg text-left hover:bg-green-50 transition-colors group">
                    <div class="w-3 h-3 bg-green-500 rounded-full"></div>
                    <span class="text-sm font-medium text-gray-700 group-hover:text-green-700">Upcoming</span>
                </button>
            </div>

            <div>
                <p class="text-xs font-semibold text-gray-400 uppercase tracking-wider mb-3">Departments</p>
                <button onclick="filterByDepartment('CSE')" class="w-full text-left px-4 py-2 text-sm text-gray-700 hover:bg-blue-50 hover:text-blue-700 rounded-lg transition-colors mb-1">Computer Science</button>
                <button onclick="filterByDepartment('ECE')" class="w-full text-left px-4 py-2 text-sm text-gray-700 hover:bg-blue-50 hover:text-blue-700 rounded-lg transition-colors mb-1">Electronics</button>
                <button onclick="filterByDepartment('MECH')" class="w-full text-left px-4 py-2 text-sm text-gray-700 hover:bg-blue-50 hover:text-blue-700 rounded-lg transition-colors mb-1">Mechanical</button>
                <button onclick="filterByDepartment('CIVIL')" class="w-full text-left px-4 py-2 text-sm text-gray-700 hover:bg-blue-50 hover:text-blue-700 rounded-lg transition-colors mb-1">Civil</button>
                <button onclick="filterByDepartment('All')" class="w-full text-left px-4 py-2 text-sm text-gray-700 hover:bg-blue-50 hover:text-blue-700 rounded-lg transition-colors">All Departments</button>
            </div>
        </nav>

        <div class="absolute bottom-0 left-0 right-0 p-4 bg-gradient-to-t from-white">
            <div class="bg-blue-50 border border-blue-200 rounded-lg p-3">
                <p class="text-xs text-blue-800 font-medium">📚 Academic Year 2025-26</p>
                <p class="text-xs text-blue-600 mt-1">All announcements stored permanently</p>
            </div>
        </div>
    </aside>

    <!-- Main Content -->
    <main class="lg:ml-72 min-h-screen">
        <!-- Header -->
        <header class="bg-white border-b border-gray-200 sticky top-0 z-30">
            <div class="px-4 lg:px-8 py-4">
                <div class="flex items-center justify-between">
                    <div class="flex items-center gap-4">
                        <div class="lg:hidden w-12"></div>
                        <div>
                            <h2 id="pageTitle" class="text-xl font-bold text-gray-900">Announcement Feed</h2>
                            <p id="pageSubtitle" class="text-sm text-gray-500">Real-time campus updates</p>
                        </div>
                    </div>
                    <div class="flex items-center gap-3">
                        <div class="relative">
                            <input type="text" id="searchInput" placeholder="Search announcements..." class="pl-10 pr-4 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-blue-500 focus:border-transparent w-64 hidden md:block">
                            <svg class="w-5 h-5 text-gray-400 absolute left-3 top-2.5 hidden md:block" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M21 21l-6-6m2-5a7 7 0 11-14 0 7 7 0 0114 0z"></path>
                            </svg>
                        </div>
                        <button onclick="refreshData()" class="p-2 hover:bg-gray-100 rounded-lg transition-colors" title="Refresh">
                            <svg class="w-5 h-5 text-gray-600" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 4v5h.582m15.356 2A8.001 8.001 0 004.582 9m0 0H9m11 11v-5h-.581m0 0a8.003 8.003 0 01-15.357-2m15.357 2H15"></path>
                            </svg>
                        </button>
                        <div class="w-10 h-10 bg-gradient-to-br from-blue-500 to-purple-600 rounded-full flex items-center justify-center text-white font-semibold">
                            EP
                        </div>
                    </div>
                </div>
            </div>
        </header>

        <!-- Content Container -->
        <div id="mainContent" class="p-4 lg:p-8">
            <!-- Content will be dynamically loaded here -->
        </div>
    </main>

    <!-- Delete Confirmation Modal -->
    <div id="deleteModal" class="modal">
        <div class="bg-white rounded-xl shadow-2xl p-6 max-w-md w-full mx-4 fade-in">
            <div class="flex items-center gap-3 mb-4">
                <div class="w-12 h-12 bg-red-100 rounded-full flex items-center justify-center">
                    <svg class="w-6 h-6 text-red-600" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 9v2m0 4h.01m-6.938 4h13.856c1.54 0 2.502-1.667 1.732-3L13.732 4c-.77-1.333-2.694-1.333-3.464 0L3.34 16c-.77 1.333.192 3 1.732 3z"></path>
                    </svg>
                </div>
                <div>
                    <h3 class="text-lg font-bold text-gray-900">Confirm Deletion</h3>
                    <p class="text-sm text-gray-600">This action cannot be undone</p>
                </div>
            </div>
            <p class="text-gray-700 mb-6">Are you sure you want to delete this announcement? It will be permanently removed from the system.</p>
            <div class="flex gap-3">
                <button onclick="closeDeleteModal()" class="flex-1 px-4 py-2 bg-gray-100 text-gray-700 rounded-lg font-medium hover:bg-gray-200 transition-colors">Cancel</button>
                <button onclick="confirmDelete()" class="flex-1 px-4 py-2 bg-red-600 text-white rounded-lg font-medium hover:bg-red-700 transition-colors">Delete</button>
            </div>
        </div>
    </div>

    <script>
        // State Management
        let announcements = [];
        let currentView = 'feed';
        let selectedPriority = 'All';
        let selectedDepartment = 'All';
        let deleteTargetId = null;
        let editingId = null;

        // Demo Data
        const demoAnnouncements = [
            {
                id: '1',
                title: 'Campus Placement Drive - Infosys',
                description: 'Infosys will be conducting an on-campus placement drive for final year students (2025 batch). Eligibility: All branches with 60%+ aggregate. Pre-placement talk on Feb 5, 2026 at 10:00 AM in Seminar Hall. Online test scheduled for Feb 8, 2026. Registration deadline: Feb 3, 2026.',
                priority: 'High Priority',
                department: 'All',
                date: '2026-01-31',
                time: '09:00 AM',
                createdAt: '2026-01-31T09:00:00',
                author: 'Training & Placement Cell',
                contactStaff: 'Dr. Vijayalakshmi R',
                contactDesignation: 'Training & Placement Officer',
                contactLocation: 'T&P Office, Admin Block, 2nd Floor, Room No. 205',
                contactPhone: '+91 98765 43210',
                contactEmail: 'placement@egspillay.ac.in',
                availableTime: 'Monday to Friday, 9:00 AM - 5:00 PM'
            },
            {
                id: '2',
                title: 'Mid-Semester Exam Schedule Released',
                description: 'The mid-semester examinations for all departments will be conducted from February 15-22, 2026. Students can download their exam timetables from the college portal. Hall tickets will be available from Feb 12. Please check your email for detailed schedule.',
                priority: 'High Priority',
                department: 'All',
                date: '2026-01-30',
                time: '02:30 PM',
                createdAt: '2026-01-30T14:30:00',
                author: 'Examination Cell',
                contactStaff: 'Mr. Senthil Kumar K',
                contactDesignation: 'Chief Superintendent - Examinations',
                contactLocation: 'Examination Section, Admin Block, Ground Floor, Room No. 105',
                contactPhone: '+91 98765 12345',
                contactEmail: 'exams@egspillay.ac.in',
                availableTime: 'Monday to Saturday, 9:00 AM - 4:00 PM'
            },
            {
                id: '3',
                title: 'Assignment Submission - Data Structures',
                description: 'CSE 3rd year students must submit Assignment #3 on Binary Search Trees today before 5:00 PM. Late submissions will not be accepted. Submit hard copy to Department office and upload soft copy to classroom portal.',
                priority: 'Today',
                department: 'CSE',
                date: '2026-01-31',
                time: '10:00 AM',
                createdAt: '2026-01-31T10:00:00',
                author: 'Dr. Ramesh Kumar - CSE Dept',
                contactStaff: 'Dr. Ramesh Kumar S',
                contactDesignation: 'Associate Professor - Computer Science',
                contactLocation: 'CSE Department, Block C, 3rd Floor, Staff Room No. 12',
                contactPhone: '+91 98765 98765',
                contactEmail: 'ramesh.cse@egspillay.ac.in',
                availableTime: 'Monday to Friday, 10:00 AM - 4:00 PM (Lunch: 1-2 PM)'
            },
            {
                id: '4',
                title: 'Technical Workshop on Machine Learning',
                description: 'Department of CSE is organizing a 3-day workshop on "Machine Learning and AI Applications" from Feb 10-12, 2026. Topics: Python, TensorFlow, Neural Networks. Expert speakers from industry. Registration fee: ₹500. Limited seats - 50 only. Register at CSE office.',
                priority: 'Upcoming',
                department: 'CSE',
                date: '2026-02-10',
                time: '09:00 AM',
                createdAt: '2026-01-29T11:00:00',
                author: 'CSE Department',
                contactStaff: 'Dr. Priya Dharshini M',
                contactDesignation: 'Workshop Coordinator & HOD - CSE',
                contactLocation: 'HOD Chamber, CSE Department, Block C, 3rd Floor',
                contactPhone: '+91 98765 55555',
                contactEmail: 'hod.cse@egspillay.ac.in',
                availableTime: 'Monday to Friday, 9:30 AM - 5:00 PM'
            },
            {
                id: '5',
                title: 'Industrial Visit - Automotive Plant',
                description: 'Mechanical Engineering students (3rd & 4th year) - Industrial visit to Ashok Leyland Manufacturing Plant, Chennai scheduled for Feb 18, 2026. Reporting time: 6:00 AM at college gate. Fee: ₹300 per student. Last date for registration: Feb 5, 2026.',
                priority: 'Upcoming',
                department: 'MECH',
                date: '2026-02-18',
                time: '06:00 AM',
                createdAt: '2026-01-28T16:00:00',
                author: 'MECH Department',
                contactStaff: 'Prof. Murugan P',
                contactDesignation: 'Industrial Visit Coordinator - Mechanical Dept',
                contactLocation: 'Mechanical Department, Block B, 2nd Floor, Faculty Room',
                contactPhone: '+91 98765 66666',
                contactEmail: 'murugan.mech@egspillay.ac.in',
                availableTime: 'Monday to Saturday, 9:00 AM - 5:00 PM'
            },
            {
                id: '6',
                title: 'Library Book Return Reminder',
                description: 'All students who have borrowed books before December 2025 must return them by Feb 3, 2026. Late fees applicable: ₹5 per day per book. Library timing: 8:00 AM - 8:00 PM. Contact: library@egspillay.ac.in',
                priority: 'Today',
                department: 'All',
                date: '2026-01-31',
                time: '11:30 AM',
                createdAt: '2026-01-31T11:30:00',
                author: 'Central Library',
                contactStaff: 'Mrs. Lakshmi Devi S',
                contactDesignation: 'Chief Librarian',
                contactLocation: 'Central Library, Ground Floor, Circulation Desk',
                contactPhone: '+91 98765 77777',
                contactEmail: 'library@egspillay.ac.in',
                availableTime: 'Monday to Saturday, 8:00 AM - 8:00 PM'
            },
            {
                id: '7',
                title: 'Project Review - ECE Final Year',
                description: 'Final year ECE students: Phase-1 project review scheduled for Feb 6-7, 2026. Each team will get 15 minutes presentation + 5 minutes Q&A. Panels will be announced tomorrow. Ensure all documentation is complete. Attendance mandatory for all team members.',
                priority: 'Upcoming',
                department: 'ECE',
                date: '2026-02-06',
                time: '10:00 AM',
                createdAt: '2026-01-30T09:00:00',
                author: 'ECE Department',
                contactStaff: 'Dr. Anitha Kumari R',
                contactDesignation: 'Project Coordinator - ECE Department',
                contactLocation: 'ECE Department, Block D, 1st Floor, Room No. 8',
                contactPhone: '+91 98765 88888',
                contactEmail: 'anitha.ece@egspillay.ac.in',
                availableTime: 'Monday to Friday, 10:00 AM - 4:00 PM'
            },
            {
                id: '8',
                title: 'Construction Safety Seminar',
                description: 'Civil Engineering Department invites all students for a seminar on "Modern Construction Safety Practices" on Feb 4, 2026 at 2:00 PM. Guest speaker: Er. Suresh Babu (Chief Safety Officer, L&T). Venue: Civil Block Auditorium. Attendance will be counted.',
                priority: 'Upcoming',
                department: 'CIVIL',
                date: '2026-02-04',
                time: '02:00 PM',
                createdAt: '2026-01-29T13:00:00',
                author: 'CIVIL Department',
                contactStaff: 'Prof. Karthikeyan M',
                contactDesignation: 'HOD - Civil Engineering',
                contactLocation: 'Civil Department, Block A, 2nd Floor, HOD Chamber',
                contactPhone: '+91 98765 99999',
                contactEmail: 'hod.civil@egspillay.ac.in',
                availableTime: 'Monday to Saturday, 9:00 AM - 5:00 PM'
            }
        ];

        // Initialize
        function init() {
            loadAnnouncements();
            renderCurrentView();
            updateBadges();
            setupEventListeners();
        }

        function setupEventListeners() {
            // Mobile menu
            document.getElementById('mobileMenuBtn').addEventListener('click', toggleSidebar);
            
            // Search
            document.getElementById('searchInput').addEventListener('input', handleSearch);
            
            // Close sidebar on outside click (mobile)
            document.addEventListener('click', (e) => {
                const sidebar = document.getElementById('sidebar');
                const menuBtn = document.getElementById('mobileMenuBtn');
                if (window.innerWidth < 1024 && !sidebar.contains(e.target) && !menuBtn.contains(e.target)) {
                    sidebar.classList.remove('translate-x-0');
                    sidebar.classList.add('-translate-x-full');
                }
            });
        }

        function toggleSidebar() {
            const sidebar = document.getElementById('sidebar');
            sidebar.classList.toggle('-translate-x-full');
            sidebar.classList.toggle('translate-x-0');
        }

        function loadAnnouncements() {
            const stored = localStorage.getItem('campus_bridge_announcements');
            if (stored) {
                announcements = JSON.parse(stored);
            } else {
                announcements = [...demoAnnouncements];
                saveAnnouncements();
            }
        }

        function saveAnnouncements() {
            localStorage.setItem('campus_bridge_announcements', JSON.stringify(announcements));
        }

        function updateBadges() {
            document.getElementById('feed-badge').textContent = announcements.length;
        }

        function switchView(view) {
            currentView = view;
            selectedPriority = 'All';
            selectedDepartment = 'All';
            
            // Update sidebar active state
            document.querySelectorAll('nav button').forEach(btn => {
                btn.classList.remove('sidebar-active');
            });
            document.getElementById(`nav-${view}`).classList.add('sidebar-active');
            
            // Close mobile sidebar
            if (window.innerWidth < 1024) {
                document.getElementById('sidebar').classList.add('-translate-x-full');
            }
            
            renderCurrentView();
        }

        function renderCurrentView() {
            const container = document.getElementById('mainContent');
            
            switch(currentView) {
                case 'feed':
                    document.getElementById('pageTitle').textContent = 'Announcement Feed';
                    document.getElementById('pageSubtitle').textContent = 'Real-time campus updates';
                    container.innerHTML = renderFeedView();
                    break;
                case 'archive':
                    document.getElementById('pageTitle').textContent = 'Archive & History';
                    document.getElementById('pageSubtitle').textContent = 'Browse past announcements';
                    container.innerHTML = renderArchiveView();
                    break;
                case 'admin':
                    document.getElementById('pageTitle').textContent = 'Admin Panel';
                    document.getElementById('pageSubtitle').textContent = 'Manage announcements';
                    container.innerHTML = renderAdminView();
                    if (editingId) {
                        prefillEditForm();
                    }
                    break;
            }
        }

        function renderFeedView() {
            const filtered = getFilteredAnnouncements();
            const stats = calculateStats();
            
            return `
                <!-- Stats Cards -->
                <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-6 mb-8">
                    <div class="bg-white rounded-xl shadow-sm border border-gray-200 p-6 card-hover">
                        <div class="flex items-center justify-between mb-3">
                            <div class="w-12 h-12 bg-blue-100 rounded-lg flex items-center justify-center">
                                <svg class="w-6 h-6 text-blue-600" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 17h5l-1.405-1.405A2.032 2.032 0 0118 14.158V11a6.002 6.002 0 00-4-5.659V5a2 2 0 10-4 0v.341C7.67 6.165 6 8.388 6 11v3.159c0 .538-.214 1.055-.595 1.436L4 17h5m6 0v1a3 3 0 11-6 0v-1m6 0H9"></path>
                                </svg>
                            </div>
                            <span class="text-3xl font-bold text-gray-900">${stats.total}</span>
                        </div>
                        <p class="text-sm font-medium text-gray-600">Total Announcements</p>
                        <p class="text-xs text-gray-500 mt-1">All time records</p>
                    </div>

                    <div class="bg-white rounded-xl shadow-sm border border-gray-200 p-6 card-hover">
                        <div class="flex items-center justify-between mb-3">
                            <div class="w-12 h-12 bg-red-100 rounded-lg flex items-center justify-center">
                                <svg class="w-6 h-6 text-red-600" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 9v2m0 4h.01m-6.938 4h13.856c1.54 0 2.502-1.667 1.732-3L13.732 4c-.77-1.333-2.694-1.333-3.464 0L3.34 16c-.77 1.333.192 3 1.732 3z"></path>
                                </svg>
                            </div>
                            <span class="text-3xl font-bold text-red-600">${stats.highPriority}</span>
                        </div>
                        <p class="text-sm font-medium text-gray-600">High Priority</p>
                        <p class="text-xs text-gray-500 mt-1">Urgent updates</p>
                    </div>

                    <div class="bg-white rounded-xl shadow-sm border border-gray-200 p-6 card-hover">
                        <div class="flex items-center justify-between mb-3">
                            <div class="w-12 h-12 bg-yellow-100 rounded-lg flex items-center justify-center">
                                <svg class="w-6 h-6 text-yellow-600" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 8v4l3 3m6-3a9 9 0 11-18 0 9 9 0 0118 0z"></path>
                                </svg>
                            </div>
                            <span class="text-3xl font-bold text-yellow-600">${stats.today}</span>
                        </div>
                        <p class="text-sm font-medium text-gray-600">Today's Updates</p>
                        <p class="text-xs text-gray-500 mt-1">Posted today</p>
                    </div>

                    <div class="bg-white rounded-xl shadow-sm border border-gray-200 p-6 card-hover">
                        <div class="flex items-center justify-between mb-3">
                            <div class="w-12 h-12 bg-green-100 rounded-lg flex items-center justify-center">
                                <svg class="w-6 h-6 text-green-600" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M8 7V3m8 4V3m-9 8h10M5 21h14a2 2 0 002-2V7a2 2 0 00-2-2H5a2 2 0 00-2 2v12a2 2 0 002 2z"></path>
                                </svg>
                            </div>
                            <span class="text-3xl font-bold text-green-600">${stats.upcoming}</span>
                        </div>
                        <p class="text-sm font-medium text-gray-600">Upcoming Events</p>
                        <p class="text-xs text-gray-500 mt-1">Future activities</p>
                    </div>
                </div>

                <!-- Active Filters -->
                ${selectedPriority !== 'All' || selectedDepartment !== 'All' ? `
                    <div class="bg-blue-50 border border-blue-200 rounded-lg p-4 mb-6 flex items-center justify-between flex-wrap gap-3">
                        <div class="flex items-center gap-2 flex-wrap">
                            <svg class="w-5 h-5 text-blue-600" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3 4a1 1 0 011-1h16a1 1 0 011 1v2.586a1 1 0 01-.293.707l-6.414 6.414a1 1 0 00-.293.707V17l-4 4v-6.586a1 1 0 00-.293-.707L3.293 7.293A1 1 0 013 6.586V4z"></path>
                            </svg>
                            <span class="text-sm font-semibold text-blue-900">Active Filters:</span>
                            ${selectedPriority !== 'All' ? `<span class="px-3 py-1 bg-blue-600 text-white text-xs font-semibold rounded-full">${selectedPriority}</span>` : ''}
                            ${selectedDepartment !== 'All' ? `<span class="px-3 py-1 bg-blue-600 text-white text-xs font-semibold rounded-full">${selectedDepartment}</span>` : ''}
                        </div>
                        <button onclick="clearFilters()" class="text-sm text-blue-700 hover:text-blue-900 font-medium">Clear All</button>
                    </div>
                ` : ''}

                <!-- Announcements Grid -->
                <div class="space-y-6">
                    ${filtered.length === 0 ? `
                        <div class="bg-white rounded-xl shadow-sm border border-gray-200 p-12 text-center">
                            <div class="w-16 h-16 bg-gray-100 rounded-full flex items-center justify-center mx-auto mb-4">
                                <svg class="w-8 h-8 text-gray-400" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M20 13V6a2 2 0 00-2-2H6a2 2 0 00-2 2v7m16 0v5a2 2 0 01-2 2H6a2 2 0 01-2-2v-5m16 0h-2.586a1 1 0 00-.707.293l-2.414 2.414a1 1 0 01-.707.293h-3.172a1 1 0 01-.707-.293l-2.414-2.414A1 1 0 006.586 13H4"></path>
                                </svg>
                            </div>
                            <h3 class="text-lg font-semibold text-gray-900 mb-2">No announcements found</h3>
                            <p class="text-gray-600 mb-4">Try adjusting your filters or check back later</p>
                            <button onclick="clearFilters()" class="px-6 py-2 bg-blue-600 text-white rounded-lg font-medium hover:bg-blue-700 transition-colors">Clear Filters</button>
                        </div>
                    ` : filtered.map(a => renderAnnouncementCard(a)).join('')}
                </div>
            `;
        }

        function renderAnnouncementCard(announcement) {
            const priorityStyles = {
                'High Priority': { bg: 'bg-gradient-to-r from-red-500 to-red-600', text: 'text-white', icon: 'M12 9v2m0 4h.01m-6.938 4h13.856c1.54 0 2.502-1.667 1.732-3L13.732 4c-.77-1.333-2.694-1.333-3.464 0L3.34 16c-.77 1.333.192 3 1.732 3z' },
                'Today': { bg: 'bg-gradient-to-r from-yellow-500 to-yellow-600', text: 'text-white', icon: 'M12 8v4l3 3m6-3a9 9 0 11-18 0 9 9 0 0118 0z' },
                'Upcoming': { bg: 'bg-gradient-to-r from-green-500 to-green-600', text: 'text-white', icon: 'M8 7V3m8 4V3m-9 8h10M5 21h14a2 2 0 002-2V7a2 2 0 00-2-2H5a2 2 0 00-2 2v12a2 2 0 002 2z' }
            };
            
            const style = priorityStyles[announcement.priority];
            const daysAgo = getDaysAgo(announcement.createdAt);
            
            return `
                <div class="bg-white rounded-xl shadow-sm border border-gray-200 overflow-hidden card-hover">
                    <!-- Priority Banner -->
                    <div class="${style.bg} px-6 py-3 flex items-center justify-between">
                        <div class="flex items-center gap-2">
                            <svg class="w-5 h-5 ${style.text}" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="${style.icon}"></path>
                            </svg>
                            <span class="${style.text} font-bold text-sm uppercase tracking-wide">${announcement.priority}</span>
                        </div>
                        <span class="${style.text} text-sm font-medium">${announcement.department}</span>
                    </div>

                    <!-- Content -->
                    <div class="p-6">
                        <div class="flex items-start justify-between mb-4">
                            <h3 class="text-xl font-bold text-gray-900 flex-1">${announcement.title}</h3>
                            <div class="flex gap-2 ml-4">
                                <button onclick="editAnnouncement('${announcement.id}')" class="p-2 text-blue-600 hover:bg-blue-50 rounded-lg transition-colors" title="Edit">
                                    <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M11 5H6a2 2 0 00-2 2v11a2 2 0 002 2h11a2 2 0 002-2v-5m-1.414-9.414a2 2 0 112.828 2.828L11.828 15H9v-2.828l8.586-8.586z"></path>
                                    </svg>
                                </button>
                                <button onclick="openDeleteModal('${announcement.id}')" class="p-2 text-red-600 hover:bg-red-50 rounded-lg transition-colors" title="Delete">
                                    <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19 7l-.867 12.142A2 2 0 0116.138 21H7.862a2 2 0 01-1.995-1.858L5 7m5 4v6m4-6v6m1-10V4a1 1 0 00-1-1h-4a1 1 0 00-1 1v3M4 7h16"></path>
                                    </svg>
                                </button>
                            </div>
                        </div>

                        <p class="text-gray-700 leading-relaxed mb-6">${announcement.description}</p>

                        <!-- Meta Info -->
                        <div class="grid grid-cols-1 md:grid-cols-3 gap-4 pt-4 border-t border-gray-200">
                            <div class="flex items-center gap-2">
                                <svg class="w-5 h-5 text-gray-400" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M8 7V3m8 4V3m-9 8h10M5 21h14a2 2 0 002-2V7a2 2 0 00-2-2H5a2 2 0 00-2 2v12a2 2 0 002 2z"></path>
                                </svg>
                                <div>
                                    <p class="text-xs text-gray-500">Date</p>
                                    <p class="text-sm font-semibold text-gray-900">${formatDate(announcement.date)}</p>
                                </div>
                            </div>
                            <div class="flex items-center gap-2">
                                <svg class="w-5 h-5 text-gray-400" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 8v4l3 3m6-3a9 9 0 11-18 0 9 9 0 0118 0z"></path>
                                </svg>
                                <div>
                                    <p class="text-xs text-gray-500">Time</p>
                                    <p class="text-sm font-semibold text-gray-900">${announcement.time}</p>
                                </div>
                            </div>
                            <div class="flex items-center gap-2">
                                <svg class="w-5 h-5 text-gray-400" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M16 7a4 4 0 11-8 0 4 4 0 018 0zM12 14a7 7 0 00-7 7h14a7 7 0 00-7-7z"></path>
                                </svg>
                                <div>
                                    <p class="text-xs text-gray-500">Posted by</p>
                                    <p class="text-sm font-semibold text-gray-900">${announcement.author}</p>
                                </div>
                            </div>
                        </div>

                        <!-- Footer -->
                        <div class="mt-4 pt-4 border-t border-gray-200 flex items-center justify-between">
                            <span class="text-xs text-gray-500">${daysAgo === 0 ? 'Posted today' : daysAgo === 1 ? 'Posted yesterday' : `Posted ${daysAgo} days ago`}</span>
                            <span class="px-3 py-1 bg-gray-100 text-gray-700 text-xs font-medium rounded-full">ID: ${announcement.id}</span>
                        </div>

                        <!-- Contact Information Section -->
                        ${announcement.contactStaff ? `
                            <div class="mt-6 pt-6 border-t-2 border-blue-100 bg-gradient-to-r from-blue-50 to-indigo-50 rounded-lg p-5">
                                <div class="flex items-center gap-2 mb-4">
                                    <svg class="w-6 h-6 text-blue-600" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M16 7a4 4 0 11-8 0 4 4 0 018 0zM12 14a7 7 0 00-7 7h14a7 7 0 00-7-7z"></path>
                                    </svg>
                                    <h4 class="text-base font-bold text-blue-900">Contact Information - For Queries & Assistance</h4>
                                </div>
                                
                                <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
                                    <!-- Staff Name & Designation -->
                                    <div class="bg-white rounded-lg p-4 border border-blue-200">
                                        <div class="flex items-start gap-3">
                                            <div class="w-10 h-10 bg-blue-600 rounded-full flex items-center justify-center text-white font-bold text-sm flex-shrink-0">
                                                ${announcement.contactStaff.split(' ').map(n => n[0]).slice(0, 2).join('')}
                                            </div>
                                            <div class="flex-1">
                                                <p class="text-xs text-gray-500 mb-1">Contact Person</p>
                                                <p class="font-bold text-gray-900">${announcement.contactStaff}</p>
                                                <p class="text-sm text-blue-700 mt-1">${announcement.contactDesignation}</p>
                                            </div>
                                        </div>
                                    </div>

                                    <!-- Location -->
                                    <div class="bg-white rounded-lg p-4 border border-blue-200">
                                        <div class="flex items-start gap-3">
                                            <div class="w-10 h-10 bg-green-100 rounded-lg flex items-center justify-center flex-shrink-0">
                                                <svg class="w-5 h-5 text-green-600" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                                                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M17.657 16.657L13.414 20.9a1.998 1.998 0 01-2.827 0l-4.244-4.243a8 8 0 1111.314 0z"></path>
                                                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 11a3 3 0 11-6 0 3 3 0 016 0z"></path>
                                                </svg>
                                            </div>
                                            <div class="flex-1">
                                                <p class="text-xs text-gray-500 mb-1">Office Location</p>
                                                <p class="text-sm font-semibold text-gray-900 leading-relaxed">${announcement.contactLocation}</p>
                                            </div>
                                        </div>
                                    </div>

                                    <!-- Phone -->
                                    <div class="bg-white rounded-lg p-4 border border-blue-200">
                                        <div class="flex items-start gap-3">
                                            <div class="w-10 h-10 bg-purple-100 rounded-lg flex items-center justify-center flex-shrink-0">
                                                <svg class="w-5 h-5 text-purple-600" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                                                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3 5a2 2 0 012-2h3.28a1 1 0 01.948.684l1.498 4.493a1 1 0 01-.502 1.21l-2.257 1.13a11.042 11.042 0 005.516 5.516l1.13-2.257a1 1 0 011.21-.502l4.493 1.498a1 1 0 01.684.949V19a2 2 0 01-2 2h-1C9.716 21 3 14.284 3 6V5z"></path>
                                                </svg>
                                            </div>
                                            <div class="flex-1">
                                                <p class="text-xs text-gray-500 mb-1">Phone Number</p>
                                                <a href="tel:${announcement.contactPhone.replace(/\s/g, '')}" class="text-sm font-bold text-purple-700 hover:text-purple-900 hover:underline">${announcement.contactPhone}</a>
                                                <p class="text-xs text-gray-600 mt-1">Click to call</p>
                                            </div>
                                        </div>
                                    </div>

                                    <!-- Email -->
                                    <div class="bg-white rounded-lg p-4 border border-blue-200">
                                        <div class="flex items-start gap-3">
                                            <div class="w-10 h-10 bg-orange-100 rounded-lg flex items-center justify-center flex-shrink-0">
                                                <svg class="w-5 h-5 text-orange-600" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                                                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3 8l7.89 5.26a2 2 0 002.22 0L21 8M5 19h14a2 2 0 002-2V7a2 2 0 00-2-2H5a2 2 0 00-2 2v10a2 2 0 002 2z"></path>
                                                </svg>
                                            </div>
                                            <div class="flex-1">
                                                <p class="text-xs text-gray-500 mb-1">Email Address</p>
                                                <a href="mailto:${announcement.contactEmail}" class="text-sm font-bold text-orange-700 hover:text-orange-900 hover:underline break-all">${announcement.contactEmail}</a>
                                                <p class="text-xs text-gray-600 mt-1">Click to email</p>
                                            </div>
                                        </div>
                                    </div>
                                </div>

                                <!-- Available Time -->
                                <div class="mt-4 bg-white rounded-lg p-3 border border-blue-200">
                                    <div class="flex items-center gap-2">
                                        <svg class="w-5 h-5 text-blue-600" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                                            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 8v4l3 3m6-3a9 9 0 11-18 0 9 9 0 0118 0z"></path>
                                        </svg>
                                        <div>
                                            <span class="text-xs text-gray-600 font-medium">Available Time: </span>
                                            <span class="text-sm font-bold text-gray-900">${announcement.availableTime}</span>
                                        </div>
                                    </div>
                                </div>

                                <div class="mt-4 bg-blue-600 text-white rounded-lg p-3 text-center">
                                    <p class="text-sm font-semibold">💡 Visit during available hours or contact via phone/email for assistance</p>
                                </div>
                            </div>
                        ` : ''}
                    </div>
                </div>
            `;
        }

        function renderArchiveView() {
            const byMonth = groupByMonth(announcements);
            
            return `
                <div class="bg-white rounded-xl shadow-sm border border-gray-200 p-6 mb-6">
                    <div class="flex items-center gap-3 mb-4">
                        <div class="w-12 h-12 bg-blue-100 rounded-lg flex items-center justify-center">
                            <svg class="w-6 h-6 text-blue-600" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M5 8h14M5 8a2 2 0 110-4h14a2 2 0 110 4M5 8v10a2 2 0 002 2h10a2 2 0 002-2V8m-9 4h4"></path>
                            </svg>
                        </div>
                        <div>
                            <h3 class="text-lg font-bold text-gray-900">Archive & History</h3>
                            <p class="text-sm text-gray-600">All announcements are stored permanently for future reference</p>
                        </div>
                    </div>

                    <div class="grid grid-cols-1 md:grid-cols-3 gap-4 mt-6">
                        <div class="bg-gradient-to-br from-blue-50 to-blue-100 rounded-lg p-4">
                            <p class="text-sm text-blue-700 font-medium mb-1">Total Records</p>
                            <p class="text-3xl font-bold text-blue-900">${announcements.length}</p>
                        </div>
                        <div class="bg-gradient-to-br from-purple-50 to-purple-100 rounded-lg p-4">
                            <p class="text-sm text-purple-700 font-medium mb-1">Months Archived</p>
                            <p class="text-3xl font-bold text-purple-900">${Object.keys(byMonth).length}</p>
                        </div>
                        <div class="bg-gradient-to-br from-green-50 to-green-100 rounded-lg p-4">
                            <p class="text-sm text-green-700 font-medium mb-1">This Month</p>
                            <p class="text-3xl font-bold text-green-900">${getThisMonthCount()}</p>
                        </div>
                    </div>
                </div>

                <!-- Search & Filter -->
                <div class="bg-white rounded-xl shadow-sm border border-gray-200 p-6 mb-6">
                    <div class="grid grid-cols-1 md:grid-cols-3 gap-4">
                        <div>
                            <label class="block text-sm font-semibold text-gray-700 mb-2">Search</label>
                            <input type="text" id="archiveSearch" onkeyup="searchArchive()" placeholder="Search by title or content..." class="w-full px-4 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-blue-500">
                        </div>
                        <div>
                            <label class="block text-sm font-semibold text-gray-700 mb-2">Department</label>
                            <select id="archiveDept" onchange="searchArchive()" class="w-full px-4 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-blue-500">
                                <option value="All">All Departments</option>
                                <option value="CSE">CSE</option>
                                <option value="ECE">ECE</option>
                                <option value="MECH">MECH</option>
                                <option value="CIVIL">CIVIL</option>
                            </select>
                        </div>
                        <div>
                            <label class="block text-sm font-semibold text-gray-700 mb-2">Priority</label>
                            <select id="archivePriority" onchange="searchArchive()" class="w-full px-4 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-blue-500">
                                <option value="All">All Priorities</option>
                                <option value="High Priority">High Priority</option>
                                <option value="Today">Today</option>
                                <option value="Upcoming">Upcoming</option>
                            </select>
                        </div>
                    </div>
                </div>

                <!-- Timeline View -->
                <div id="archiveResults">
                    ${Object.keys(byMonth).sort((a, b) => new Date(b) - new Date(a)).map(month => `
                        <div class="mb-8">
                            <div class="flex items-center gap-3 mb-4">
                                <h3 class="text-lg font-bold text-gray-900">${formatMonth(month)}</h3>
                                <div class="flex-1 h-px bg-gray-300"></div>
                                <span class="px-3 py-1 bg-blue-100 text-blue-800 text-sm font-semibold rounded-full">${byMonth[month].length} posts</span>
                            </div>
                            <div class="space-y-4">
                                ${byMonth[month].map(a => `
                                    <div class="bg-white border border-gray-200 rounded-lg p-4 hover:shadow-md transition-shadow">
                                        <div class="flex items-start justify-between">
                                            <div class="flex-1">
                                                <div class="flex items-center gap-2 mb-2">
                                                    <span class="px-2 py-1 text-xs font-semibold rounded ${getPriorityBadgeClass(a.priority)}">${a.priority}</span>
                                                    <span class="px-2 py-1 bg-gray-100 text-gray-700 text-xs font-medium rounded">${a.department}</span>
                                                </div>
                                                <h4 class="font-bold text-gray-900 mb-1">${a.title}</h4>
                                                <p class="text-sm text-gray-600 line-clamp-2">${a.description}</p>
                                            </div>
                                            <div class="ml-4 text-right">
                                                <p class="text-sm font-semibold text-gray-900">${formatDate(a.date)}</p>
                                                <p class="text-xs text-gray-500">${a.time}</p>
                                            </div>
                                        </div>
                                    </div>
                                `).join('')}
                            </div>
                        </div>
                    `).join('')}
                </div>
            `;
        }

        function renderAdminView() {
            return `
                <div class="max-w-4xl mx-auto">
                    <div class="bg-white rounded-xl shadow-sm border border-gray-200 p-8">
                        <div class="flex items-center gap-3 mb-6">
                            <div class="w-12 h-12 bg-gradient-to-br from-blue-500 to-purple-600 rounded-lg flex items-center justify-center">
                                <svg class="w-6 h-6 text-white" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 6v6m0 0v6m0-6h6m-6 0H6"></path>
                                </svg>
                            </div>
                            <div>
                                <h3 class="text-2xl font-bold text-gray-900">${editingId ? 'Edit Announcement' : 'Create New Announcement'}</h3>
                                <p class="text-sm text-gray-600">Fill in the details below to post an announcement</p>
                            </div>
                        </div>

                        <div class="bg-blue-50 border border-blue-200 rounded-lg p-4 mb-6 flex items-start gap-3">
                            <svg class="w-5 h-5 text-blue-600 mt-0.5 flex-shrink-0" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M13 16h-1v-4h-1m1-4h.01M21 12a9 9 0 11-18 0 9 9 0 0118 0z"></path>
                            </svg>
                            <div class="flex-1">
                                <p class="text-sm font-semibold text-blue-900">Information</p>
                                <p class="text-xs text-blue-700 mt-1">All announcements are automatically stored in the database and will appear in the Archive section. Choose the appropriate priority template to ensure proper categorization.</p>
                            </div>
                        </div>

                        <form id="announcementForm" onsubmit="handleSubmit(event)" class="space-y-6">
                            <div>
                                <label class="block text-sm font-bold text-gray-900 mb-2">Title *</label>
                                <input type="text" id="title" required class="w-full px-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-blue-500 focus:border-transparent text-gray-900" placeholder="Enter announcement title">
                            </div>

                            <div>
                                <label class="block text-sm font-bold text-gray-900 mb-2">Description *</label>
                                <textarea id="description" required rows="6" class="w-full px-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-blue-500 focus:border-transparent text-gray-900" placeholder="Enter detailed description..."></textarea>
                            </div>

                            <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
                                <div>
                                    <label class="block text-sm font-bold text-gray-900 mb-2">Priority Template *</label>
                                    <select id="priority" required class="w-full px-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-blue-500 focus:border-transparent text-gray-900">
                                        <option value="">Select Priority</option>
                                        <option value="High Priority">🔴 High Priority (Urgent - Exams, Placements, Emergency)</option>
                                        <option value="Today">🟡 Today (Daily schedules, submissions due today)</option>
                                        <option value="Upcoming">🟢 Upcoming (Future events, workshops, training)</option>
                                    </select>
                                </div>

                                <div>
                                    <label class="block text-sm font-bold text-gray-900 mb-2">Department *</label>
                                    <select id="department" required class="w-full px-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-blue-500 focus:border-transparent text-gray-900">
                                        <option value="">Select Department</option>
                                        <option value="All">All Departments</option>
                                        <option value="CSE">Computer Science & Engineering</option>
                                        <option value="ECE">Electronics & Communication</option>
                                        <option value="MECH">Mechanical Engineering</option>
                                        <option value="CIVIL">Civil Engineering</option>
                                    </select>
                                </div>
                            </div>

                            <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
                                <div>
                                    <label class="block text-sm font-bold text-gray-900 mb-2">Date *</label>
                                    <input type="date" id="date" required class="w-full px-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-blue-500 focus:border-transparent text-gray-900">
                                </div>

                                <div>
                                    <label class="block text-sm font-bold text-gray-900 mb-2">Time *</label>
                                    <input type="time" id="time" required class="w-full px-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-blue-500 focus:border-transparent text-gray-900">
                                </div>
                            </div>

                            <div>
                                <label class="block text-sm font-bold text-gray-900 mb-2">Author / Posted By *</label>
                                <input type="text" id="author" required class="w-full px-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-blue-500 focus:border-transparent text-gray-900" placeholder="e.g., Training & Placement Cell">
                            </div>

                            <!-- Contact Information Section -->
                            <div class="mt-6 pt-6 border-t-2 border-blue-200">
                                <div class="flex items-center gap-2 mb-4">
                                    <svg class="w-6 h-6 text-blue-600" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M16 7a4 4 0 11-8 0 4 4 0 018 0zM12 14a7 7 0 00-7 7h14a7 7 0 00-7-7z"></path>
                                    </svg>
                                    <h4 class="text-lg font-bold text-gray-900">Staff Contact Details (Optional)</h4>
                                </div>
                                <p class="text-sm text-gray-600 mb-4">Provide staff contact information so students know whom to meet for queries and assistance.</p>

                                <div class="bg-blue-50 rounded-lg p-4 space-y-4">
                                    <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
                                        <div>
                                            <label class="block text-sm font-semibold text-gray-900 mb-2">Contact Person Name</label>
                                            <input type="text" id="contactStaff" class="w-full px-4 py-2.5 border border-gray-300 rounded-lg focus:ring-2 focus:ring-blue-500 text-gray-900" placeholder="e.g., Dr. Ramesh Kumar">
                                        </div>
                                        <div>
                                            <label class="block text-sm font-semibold text-gray-900 mb-2">Designation</label>
                                            <input type="text" id="contactDesignation" class="w-full px-4 py-2.5 border border-gray-300 rounded-lg focus:ring-2 focus:ring-blue-500 text-gray-900" placeholder="e.g., HOD - CSE Department">
                                        </div>
                                    </div>

                                    <div>
                                        <label class="block text-sm font-semibold text-gray-900 mb-2">Office Location</label>
                                        <input type="text" id="contactLocation" class="w-full px-4 py-2.5 border border-gray-300 rounded-lg focus:ring-2 focus:ring-blue-500 text-gray-900" placeholder="e.g., CSE Department, Block C, 3rd Floor, Room No. 12">
                                    </div>

                                    <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
                                        <div>
                                            <label class="block text-sm font-semibold text-gray-900 mb-2">Phone Number</label>
                                            <input type="tel" id="contactPhone" class="w-full px-4 py-2.5 border border-gray-300 rounded-lg focus:ring-2 focus:ring-blue-500 text-gray-900" placeholder="e.g., +91 98765 43210">
                                        </div>
                                        <div>
                                            <label class="block text-sm font-semibold text-gray-900 mb-2">Email Address</label>
                                            <input type="email" id="contactEmail" class="w-full px-4 py-2.5 border border-gray-300 rounded-lg focus:ring-2 focus:ring-blue-500 text-gray-900" placeholder="e.g., staff@egspillay.ac.in">
                                        </div>
                                    </div>

                                    <div>
                                        <label class="block text-sm font-semibold text-gray-900 mb-2">Available Time</label>
                                        <input type="text" id="availableTime" class="w-full px-4 py-2.5 border border-gray-300 rounded-lg focus:ring-2 focus:ring-blue-500 text-gray-900" placeholder="e.g., Monday to Friday, 9:00 AM - 5:00 PM">
                                    </div>
                                </div>
                            </div>

                            <div class="flex gap-4 pt-4">
                                <button type="submit" class="flex-1 bg-gradient-to-r from-blue-600 to-purple-600 text-white py-3 px-6 rounded-lg font-bold hover:from-blue-700 hover:to-purple-700 transition-all shadow-lg hover:shadow-xl">
                                    ${editingId ? '✓ Update Announcement' : '✓ Publish Announcement'}
                                </button>
                                ${editingId ? `
                                    <button type="button" onclick="cancelEdit()" class="px-6 py-3 border-2 border-gray-300 text-gray-700 rounded-lg font-bold hover:bg-gray-50 transition-colors">
                                        Cancel
                                    </button>
                                ` : ''}
                            </div>
                        </form>
                    </div>
                </div>
            `;
        }

        // Helper Functions
        function getFilteredAnnouncements() {
            let filtered = [...announcements];
            
            if (selectedPriority !== 'All') {
                filtered = filtered.filter(a => a.priority === selectedPriority);
            }
            
            if (selectedDepartment !== 'All') {
                filtered = filtered.filter(a => a.department === selectedDepartment || a.department === 'All');
            }
            
            // Sort by date (newest first)
            filtered.sort((a, b) => new Date(b.createdAt) - new Date(a.createdAt));
            
            return filtered;
        }

        function calculateStats() {
            const today = new Date().toISOString().split('T')[0];
            return {
                total: announcements.length,
                highPriority: announcements.filter(a => a.priority === 'High Priority').length,
                today: announcements.filter(a => a.date === today).length,
                upcoming: announcements.filter(a => a.priority === 'Upcoming').length
            };
        }

        function formatDate(dateString) {
            const date = new Date(dateString);
            const options = { day: 'numeric', month: 'short', year: 'numeric' };
            return date.toLocaleDateString('en-US', options);
        }

        function formatMonth(dateString) {
            const date = new Date(dateString);
            const options = { month: 'long', year: 'numeric' };
            return date.toLocaleDateString('en-US', options);
        }

        function getDaysAgo(dateString) {
            const created = new Date(dateString);
            const today = new Date();
            const diff = Math.floor((today - created) / (1000 * 60 * 60 * 24));
            return diff;
        }

        function getPriorityBadgeClass(priority) {
            const classes = {
                'High Priority': 'bg-red-100 text-red-800',
                'Today': 'bg-yellow-100 text-yellow-800',
                'Upcoming': 'bg-green-100 text-green-800'
            };
            return classes[priority] || 'bg-gray-100 text-gray-800';
        }

        function groupByMonth(items) {
            const grouped = {};
            items.forEach(item => {
                const date = new Date(item.createdAt);
                const key = `${date.getFullYear()}-${String(date.getMonth() + 1).padStart(2, '0')}-01`;
                if (!grouped[key]) grouped[key] = [];
                grouped[key].push(item);
            });
            return grouped;
        }

        function getThisMonthCount() {
            const thisMonth = new Date().toISOString().slice(0, 7);
            return announcements.filter(a => a.createdAt.startsWith(thisMonth)).length;
        }

        // Filter Functions
        function filterByPriority(priority) {
            selectedPriority = priority;
            selectedDepartment = 'All';
            currentView = 'feed';
            switchView('feed');
        }

        function filterByDepartment(dept) {
            selectedDepartment = dept;
            selectedPriority = 'All';
            currentView = 'feed';
            switchView('feed');
        }

        function clearFilters() {
            selectedPriority = 'All';
            selectedDepartment = 'All';
            renderCurrentView();
        }

        function handleSearch(e) {
            const term = e.target.value.toLowerCase();
            // Implement search logic here
        }

        function searchArchive() {
            const searchTerm = document.getElementById('archiveSearch').value.toLowerCase();
            const dept = document.getElementById('archiveDept').value;
            const priority = document.getElementById('archivePriority').value;
            
            let filtered = [...announcements];
            
            if (searchTerm) {
                filtered = filtered.filter(a => 
                    a.title.toLowerCase().includes(searchTerm) || 
                    a.description.toLowerCase().includes(searchTerm)
                );
            }
            
            if (dept !== 'All') {
                filtered = filtered.filter(a => a.department === dept || a.department === 'All');
            }
            
            if (priority !== 'All') {
                filtered = filtered.filter(a => a.priority === priority);
            }
            
            // Re-render results
            const byMonth = groupByMonth(filtered);
            const resultsHtml = Object.keys(byMonth).sort((a, b) => new Date(b) - new Date(a)).map(month => `
                <div class="mb-8">
                    <div class="flex items-center gap-3 mb-4">
                        <h3 class="text-lg font-bold text-gray-900">${formatMonth(month)}</h3>
                        <div class="flex-1 h-px bg-gray-300"></div>
                        <span class="px-3 py-1 bg-blue-100 text-blue-800 text-sm font-semibold rounded-full">${byMonth[month].length} posts</span>
                    </div>
                    <div class="space-y-4">
                        ${byMonth[month].map(a => `
                            <div class="bg-white border border-gray-200 rounded-lg p-4 hover:shadow-md transition-shadow">
                                <div class="flex items-start justify-between">
                                    <div class="flex-1">
                                        <div class="flex items-center gap-2 mb-2">
                                            <span class="px-2 py-1 text-xs font-semibold rounded ${getPriorityBadgeClass(a.priority)}">${a.priority}</span>
                                            <span class="px-2 py-1 bg-gray-100 text-gray-700 text-xs font-medium rounded">${a.department}</span>
                                        </div>
                                        <h4 class="font-bold text-gray-900 mb-1">${a.title}</h4>
                                        <p class="text-sm text-gray-600 line-clamp-2">${a.description}</p>
                                    </div>
                                    <div class="ml-4 text-right">
                                        <p class="text-sm font-semibold text-gray-900">${formatDate(a.date)}</p>
                                        <p class="text-xs text-gray-500">${a.time}</p>
                                    </div>
                                </div>
                            </div>
                        `).join('')}
                    </div>
                </div>
            `).join('');
            
            document.getElementById('archiveResults').innerHTML = resultsHtml || '<div class="text-center py-12 text-gray-500">No results found</div>';
        }

        // CRUD Operations
        function handleSubmit(event) {
            event.preventDefault();
            
            const formData = {
                title: document.getElementById('title').value,
                description: document.getElementById('description').value,
                priority: document.getElementById('priority').value,
                department: document.getElementById('department').value,
                date: document.getElementById('date').value,
                time: document.getElementById('time').value,
                author: document.getElementById('author').value,
                contactStaff: document.getElementById('contactStaff').value,
                contactDesignation: document.getElementById('contactDesignation').value,
                contactLocation: document.getElementById('contactLocation').value,
                contactPhone: document.getElementById('contactPhone').value,
                contactEmail: document.getElementById('contactEmail').value,
                availableTime: document.getElementById('availableTime').value
            };
            
            if (editingId) {
                // Update existing
                const index = announcements.findIndex(a => a.id === editingId);
                announcements[index] = {
                    ...announcements[index],
                    ...formData
                };
                editingId = null;
            } else {
                // Create new
                const announcement = {
                    id: Date.now().toString(),
                    ...formData,
                    createdAt: new Date().toISOString()
                };
                announcements.unshift(announcement);
            }
            
            saveAnnouncements();
            updateBadges();
            
            // Show success and redirect
            showSuccessMessage();
            setTimeout(() => {
                switchView('feed');
            }, 1500);
        }

        function editAnnouncement(id) {
            editingId = id;
            switchView('admin');
        }

        function prefillEditForm() {
            const announcement = announcements.find(a => a.id === editingId);
            if (!announcement) return;
            
            setTimeout(() => {
                document.getElementById('title').value = announcement.title;
                document.getElementById('description').value = announcement.description;
                document.getElementById('priority').value = announcement.priority;
                document.getElementById('department').value = announcement.department;
                document.getElementById('date').value = announcement.date;
                document.getElementById('time').value = announcement.time;
                document.getElementById('author').value = announcement.author;
                document.getElementById('contactStaff').value = announcement.contactStaff || '';
                document.getElementById('contactDesignation').value = announcement.contactDesignation || '';
                document.getElementById('contactLocation').value = announcement.contactLocation || '';
                document.getElementById('contactPhone').value = announcement.contactPhone || '';
                document.getElementById('contactEmail').value = announcement.contactEmail || '';
                document.getElementById('availableTime').value = announcement.availableTime || '';
            }, 100);
        }

        function cancelEdit() {
            editingId = null;
            document.getElementById('announcementForm').reset();
            switchView('feed');
        }

        function openDeleteModal(id) {
            deleteTargetId = id;
            document.getElementById('deleteModal').classList.add('active');
        }

        function closeDeleteModal() {
            deleteTargetId = null;
            document.getElementById('deleteModal').classList.remove('active');
        }

        function confirmDelete() {
            if (deleteTargetId) {
                announcements = announcements.filter(a => a.id !== deleteTargetId);
                saveAnnouncements();
                updateBadges();
                closeDeleteModal();
                renderCurrentView();
            }
        }

        function refreshData() {
            loadAnnouncements();
            renderCurrentView();
            updateBadges();
            showRefreshMessage();
        }

        function showSuccessMessage() {
            // Could add a toast notification here
            alert('Announcement saved successfully!');
        }

        function showRefreshMessage() {
            // Could add a toast notification here
        }

        // Initialize on load
        window.onload = init;
    </script>
</body>
</html>
