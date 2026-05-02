# sibu-index.html
A website designed to ensure that the hunt for employment is more refined and less stressful
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Careerflow AI Clone</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0/css/all.min.css" rel="stylesheet">
    <style>
        .kanban-column { min-height: 200px; }
        .dragging { opacity: 0.5; }
        .drag-over { background-color: #e5e7eb; border: 2px dashed #4f46e5; }
        .loader { border: 4px solid #f3f3f3; border-top: 4px solid #3730a3; border-radius: 50%; width: 24px; height: 24px; animation: spin 1s linear infinite; display: inline-block; }
        @keyframes spin { 0% { transform: rotate(0deg); } 100% { transform: rotate(360deg); } }
        .hidden { display: none !important; }
        .markdown-body h3 { font-size: 1.125rem; font-weight: bold; margin-top: 1rem; color: #312e81; }
        .markdown-body ul { list-style-type: disc; padding-left: 1.5rem; margin-bottom: 1rem; }
        .markdown-body p { margin-bottom: 0.75rem; }
    </style>
</head>
<body class="bg-gray-50 text-gray-800 font-sans flex h-screen overflow-hidden">

    <!-- Sidebar -->
    <aside class="w-64 bg-indigo-900 text-white flex flex-col h-full shadow-lg z-10">
        <div class="p-6 text-2xl font-bold border-b border-indigo-800 flex items-center gap-3">
            <i class="fa-solid fa-briefcase"></i> Career AI
        </div>
        <nav class="flex-1 p-4 space-y-1 overflow-y-auto text-sm">
            <button onclick="switchTab('dashboard')" class="w-full flex items-center gap-3 px-4 py-3 bg-indigo-800 rounded-lg text-left transition hover:bg-indigo-700"><i class="fa-solid fa-chart-line w-5"></i> Dashboard</button>
            <button onclick="switchTab('tracker')" class="w-full flex items-center gap-3 px-4 py-3 rounded-lg text-left transition hover:bg-indigo-800"><i class="fa-solid fa-kanban w-5"></i> Job Tracker</button>
            <button onclick="switchTab('linkedin')" class="w-full flex items-center gap-3 px-4 py-3 rounded-lg text-left transition hover:bg-indigo-800"><i class="fa-brands fa-linkedin w-5"></i> LinkedIn Optimizer</button>
            <button onclick="switchTab('resume')" class="w-full flex items-center gap-3 px-4 py-3 rounded-lg text-left transition hover:bg-indigo-800"><i class="fa-solid fa-file-lines w-5"></i> Resume Analyzer</button>
            <button onclick="switchTab('cover-letter')" class="w-full flex items-center gap-3 px-4 py-3 rounded-lg text-left transition hover:bg-indigo-800"><i class="fa-solid fa-file-signature w-5"></i> Cover Letters</button>
            <button onclick="switchTab('jobs')" class="w-full flex items-center gap-3 px-4 py-3 rounded-lg text-left transition hover:bg-indigo-800"><i class="fa-solid fa-magnifying-glass w-5"></i> Job Search</button>
            <button onclick="switchTab('interview')" class="w-full flex items-center gap-3 px-4 py-3 rounded-lg text-left transition hover:bg-indigo-800"><i class="fa-solid fa-comments w-5"></i> Interview Prep</button>
            <button onclick="switchTab('networking')" class="w-full flex items-center gap-3 px-4 py-3 rounded-lg text-left transition hover:bg-indigo-800"><i class="fa-solid fa-users w-5"></i> Networking</button>
            <button onclick="switchTab('settings')" class="w-full flex items-center gap-3 px-4 py-3 rounded-lg text-left transition hover:bg-indigo-800 mt-4 border-t border-indigo-800 pt-4"><i class="fa-solid fa-gear w-5"></i> Settings</button>
        </nav>
    </aside>

    <!-- Main Content -->
    <main class="flex-1 overflow-y-auto p-8 relative">
        
        <!-- Dashboard Section -->
        <section id="dashboard" class="tab-content">
            <h1 class="text-3xl font-bold mb-6 text-indigo-900">Dashboard</h1>
            <div class="grid grid-cols-1 md:grid-cols-4 gap-6 mb-8">
                <div class="bg-white p-6 rounded-xl shadow border border-gray-100">
                    <h3 class="text-gray-500 text-xs font-bold uppercase tracking-wider">Total Apps</h3>
                    <p id="stat-total" class="text-4xl font-bold text-indigo-600 mt-2">0</p>
                </div>
                <div class="bg-white p-6 rounded-xl shadow border border-gray-100">
                    <h3 class="text-gray-500 text-xs font-bold uppercase tracking-wider">Interviews</h3>
                    <p id="stat-interviews" class="text-4xl font-bold text-green-600 mt-2">0</p>
                </div>
                <div class="bg-white p-6 rounded-xl shadow border border-gray-100">
                    <h3 class="text-gray-500 text-xs font-bold uppercase tracking-wider">Offers</h3>
                    <p id="stat-offers" class="text-4xl font-bold text-yellow-600 mt-2">0</p>
                </div>
                <div class="bg-white p-6 rounded-xl shadow border border-gray-100">
                    <h3 class="text-gray-500 text-xs font-bold uppercase tracking-wider">Network Contacts</h3>
                    <p id="stat-network" class="text-4xl font-bold text-purple-600 mt-2">0</p>
                </div>
            </div>
            <div class="bg-indigo-50 border border-indigo-100 p-6 rounded-xl">
                <h2 class="text-lg font-bold text-indigo-900 mb-2">Welcome to your Career Hub</h2>
                <p class="text-indigo-700 text-sm">Make sure you have added your Gemini API key in the Settings tab before using any AI features. This dashboard will automatically track your metrics as you add jobs and networking contacts.</p>
            </div>
        </section>

        <!-- Job Tracker Section -->
        <section id="tracker" class="tab-content hidden">
            <div class="flex justify-between items-center mb-6">
                <h1 class="text-3xl font-bold text-indigo-900">Job Application Tracker</h1>
                <button onclick="document.getElementById('jobModal').classList.remove('hidden')" class="bg-indigo-600 hover:bg-indigo-700 text-white px-5 py-2 rounded-lg shadow font-medium transition">+ Add Job</button>
            </div>
            <div class="grid grid-cols-1 md:grid-cols-5 gap-4 h-[calc(100vh-200px)]">
                <div class="bg-gray-100 rounded-lg p-3 flex flex-col" data-status="Wishlist"><h3 class="font-bold mb-3 px-2 border-b-2 border-gray-300 pb-2">Wishlist</h3><div class="kanban-column flex-1" ondrop="drop(event)" ondragover="allowDrop(event)"></div></div>
                <div class="bg-blue-50 rounded-lg p-3 flex flex-col" data-status="Applied"><h3 class="font-bold text-blue-800 mb-3 px-2 border-b-2 border-blue-200 pb-2">Applied</h3><div class="kanban-column flex-1" ondrop="drop(event)" ondragover="allowDrop(event)"></div></div>
                <div class="bg-purple-50 rounded-lg p-3 flex flex-col" data-status="Interview"><h3 class="font-bold text-purple-800 mb-3 px-2 border-b-2 border-purple-200 pb-2">Interview</h3><div class="kanban-column flex-1" ondrop="drop(event)" ondragover="allowDrop(event)"></div></div>
                <div class="bg-green-50 rounded-lg p-3 flex flex-col" data-status="Offer"><h3 class="font-bold text-green-800 mb-3 px-2 border-b-2 border-green-200 pb-2">Offer</h3><div class="kanban-column flex-1" ondrop="drop(event)" ondragover="allowDrop(event)"></div></div>
                <div class="bg-red-50 rounded-lg p-3 flex flex-col" data-status="Rejected"><h3 class="font-bold text-red-800 mb-3 px-2 border-b-2 border-red-200 pb-2">Rejected</h3><div class="kanban-column flex-1" ondrop="drop(event)" ondragover="allowDrop(event)"></div></div>
            </div>
        </section>

        <!-- LinkedIn Optimizer -->
        <section id="linkedin" class="tab-content hidden">
            <h1 class="text-3xl font-bold mb-6 text-indigo-900">LinkedIn Profile Optimizer</h1>
            <div class="grid grid-cols-1 lg:grid-cols-2 gap-8">
                <div class="bg-white p-6 rounded-xl shadow border border-gray-100 space-y-4">
                    <div><label class="block text-sm font-medium text-gray-700">Paste your LinkedIn Profile Text (Headline, About, Experience)</label><textarea id="li-text" rows="8" class="mt-1 w-full p-2 border rounded-md"></textarea></div>
                    <div><label class="block text-sm font-medium text-gray-700">Target Job Title for Keyword Gap Check</label><input type="text" id="li-target" class="mt-1 w-full p-2 border rounded-md" placeholder="e.g., Supply Chain Manager"></div>
                    <button onclick="analyzeLinkedIn()" class="w-full bg-blue-600 hover:bg-blue-700 text-white py-3 rounded-lg font-bold transition flex justify-center items-center gap-2">
                        <i class="fa-brands fa-linkedin"></i> Analyze Profile
                        <div id="li-loader" class="loader hidden ml-2"></div>
                    </button>
                </div>
                <div class="bg-white p-6 rounded-xl shadow border border-gray-100 overflow-y-auto h-[600px] markdown-body" id="li-result">
                    <p class="text-gray-500 italic">Your profile analysis and score out of 100 will appear here...</p>
                </div>
            </div>
        </section>

        <!-- Resume Analyzer -->
        <section id="resume" class="tab-content hidden">
            <h1 class="text-3xl font-bold mb-6 text-indigo-900">AI Resume Builder & Analyzer</h1>
            <div class="grid grid-cols-1 lg:grid-cols-2 gap-8">
                <div class="bg-white p-6 rounded-xl shadow border border-gray-100 space-y-4">
                    <div><label class="block text-sm font-medium text-gray-700">Your Current Resume Text</label><textarea id="res-text" rows="6" class="mt-1 w-full p-2 border rounded-md"></textarea></div>
                    <div><label class="block text-sm font-medium text-gray-700">Target Job Description (Optional but recommended)</label><textarea id="res-jd" rows="4" class="mt-1 w-full p-2 border rounded-md"></textarea></div>
                    <div class="flex gap-4">
                        <button onclick="analyzeResume('score')" class="flex-1 bg-indigo-600 hover:bg-indigo-700 text-white py-3 rounded-lg font-bold transition flex justify-center items-center gap-2">
                            ATS Score <div id="res-loader-1" class="loader hidden ml-2"></div>
                        </button>
                        <button onclick="analyzeResume('tailor')" class="flex-1 bg-green-600 hover:bg-green-700 text-white py-3 rounded-lg font-bold transition flex justify-center items-center gap-2">
                            Tailor Bullets <div id="res-loader-2" class="loader hidden ml-2"></div>
                        </button>
                    </div>
                </div>
                <div class="bg-white p-6 rounded-xl shadow border border-gray-100 overflow-y-auto h-[600px] markdown-body" id="res-result">
                    <p class="text-gray-500 italic">ATS evaluation or tailored bullet points will appear here...</p>
                </div>
            </div>
        </section>

        <!-- Cover Letter -->
        <section id="cover-letter" class="tab-content hidden">
            <h1 class="text-3xl font-bold mb-6 text-indigo-900">AI Cover Letter Generator</h1>
            <div class="grid grid-cols-1 lg:grid-cols-2 gap-8">
                <div class="bg-white p-6 rounded-xl shadow border border-gray-100 space-y-4">
                    <div><label class="block text-sm font-medium text-gray-700">Job Title</label><input type="text" id="cl-job" class="mt-1 w-full p-2 border rounded-md"></div>
                    <div><label class="block text-sm font-medium text-gray-700">Company Name</label><input type="text" id="cl-company" class="mt-1 w-full p-2 border rounded-md"></div>
                    <div><label class="block text-sm font-medium text-gray-700">Job Description</label><textarea id="cl-desc" rows="4" class="mt-1 w-full p-2 border rounded-md"></textarea></div>
                    <div><label class="block text-sm font-medium text-gray-700">Tone</label><select id="cl-tone" class="mt-1 w-full p-2 border rounded-md"><option>Professional</option><option>Enthusiastic</option><option>Concise</option></select></div>
                    <button onclick="generateCoverLetter()" class="w-full bg-indigo-600 hover:bg-indigo-700 text-white py-3 rounded-lg font-bold transition flex justify-center items-center gap-2">
                        <i class="fa-solid fa-wand-magic-sparkles"></i> Generate
                        <div id="cl-loader" class="loader hidden ml-2"></div>
                    </button>
                </div>
                <div class="bg-white p-6 rounded-xl shadow border border-gray-100 flex flex-col h-[600px]">
                    <div class="flex justify-between items-center mb-4">
                        <h3 class="font-bold text-gray-800">Generated Result</h3>
                        <button onclick="copyToClipboard('cl-result')" class="text-indigo-600 hover:text-indigo-800 text-sm"><i class="fa-regular fa-copy"></i> Copy</button>
                    </div>
                    <textarea id="cl-result" class="flex-1 w-full p-4 border rounded-md bg-gray-50 focus:bg-white transition" placeholder="Your cover letter will appear here..."></textarea>
                </div>
            </div>
        </section>

        <!-- Job Search Assistant -->
        <section id="jobs" class="tab-content hidden">
            <h1 class="text-3xl font-bold mb-6 text-indigo-900">Job Search Matcher</h1>
            <p class="mb-4 text-gray-600">Mock logistics and commerce roles tailored to your background. Click to generate an AI Match Score based on your profile in Settings.</p>
            <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6" id="job-board">
                <!-- Mock Cards -->
                <div class="bg-white p-5 rounded-xl shadow border border-gray-100 flex flex-col">
                    <h3 class="font-bold text-lg">Supply Chain Analyst</h3>
                    <p class="text-gray-500 text-sm mb-3">Transnet • Gqeberha • Full-time</p>
                    <p class="text-sm text-gray-700 flex-1 mb-4">Looking for a logistics professional to optimize supply chain operations and data analysis. BCom required.</p>
                    <button onclick="matchJob(this, 'Supply Chain Analyst', 'Transnet')" class="w-full bg-indigo-100 text-indigo-700 py-2 rounded font-medium hover:bg-indigo-200 transition match-btn">Get AI Match Score</button>
                    <div class="match-result text-sm mt-3 font-bold hidden"></div>
                </div>
                <div class="bg-white p-5 rounded-xl shadow border border-gray-100 flex flex-col">
                    <h3 class="font-bold text-lg">Logistics Coordinator</h3>
                    <p class="text-gray-500 text-sm mb-3">Mediterranean Shipping Co. • Gqeberha • Full-time</p>
                    <p class="text-sm text-gray-700 flex-1 mb-4">Oversee daily freight movement, liaise with clients, and manage documentation. Experience in shipping preferred.</p>
                    <button onclick="matchJob(this, 'Logistics Coordinator', 'MSC')" class="w-full bg-indigo-100 text-indigo-700 py-2 rounded font-medium hover:bg-indigo-200 transition match-btn">Get AI Match Score</button>
                    <div class="match-result text-sm mt-3 font-bold hidden"></div>
                </div>
                <div class="bg-white p-5 rounded-xl shadow border border-gray-100 flex flex-col">
                    <h3 class="font-bold text-lg">Business Operations Trainee</h3>
                    <p class="text-gray-500 text-sm mb-3">Amazon • Remote • Contract</p>
                    <p class="text-sm text-gray-700 flex-1 mb-4">Assist in automating operational workflows and cross-department collaboration. Interest in tech/automation is a plus.</p>
                    <button onclick="matchJob(this, 'Business Operations Trainee', 'Amazon')" class="w-full bg-indigo-100 text-indigo-700 py-2 rounded font-medium hover:bg-indigo-200 transition match-btn">Get AI Match Score</button>
                    <div class="match-result text-sm mt-3 font-bold hidden"></div>
                </div>
            </div>
        </section>

        <!-- Interview Prep -->
        <section id="interview" class="tab-content hidden">
            <h1 class="text-3xl font-bold mb-6 text-indigo-900">AI Interview Prep</h1>
            <div class="grid grid-cols-1 lg:grid-cols-3 gap-8">
                <div class="lg:col-span-1 bg-white p-6 rounded-xl shadow border border-gray-100 space-y-4">
                    <div><label class="block text-sm font-medium text-gray-700">Job Title</label><input type="text" id="int-job" class="mt-1 w-full p-2 border rounded-md"></div>
                    <div><label class="block text-sm font-medium text-gray-700">Company Name</label><input type="text" id="int-company" class="mt-1 w-full p-2 border rounded-md"></div>
                    <button onclick="generateInterview()" class="w-full bg-indigo-600 hover:bg-indigo-700 text-white py-3 rounded-lg font-bold transition flex justify-center items-center gap-2">
                        Generate Questions <div id="int-loader" class="loader hidden ml-2"></div>
                    </button>
                </div>
                <div class="lg:col-span-2 bg-white p-6 rounded-xl shadow border border-gray-100 overflow-y-auto h-[600px] markdown-body" id="int-result">
                    <p class="text-gray-500 italic">10 tailored STAR method interview questions will appear here...</p>
                </div>
            </div>
        </section>

        <!-- Networking Tracker -->
        <section id="networking" class="tab-content hidden">
            <div class="flex justify-between items-center mb-6">
                <h1 class="text-3xl font-bold text-indigo-900">Networking Tracker</h1>
                <button onclick="document.getElementById('networkModal').classList.remove('hidden')" class="bg-indigo-600 hover:bg-indigo-700 text-white px-5 py-2 rounded-lg shadow font-medium transition">+ Add Contact</button>
            </div>
            
            <div class="bg-white rounded-xl shadow border border-gray-100 overflow-hidden mb-6">
                <table class="w-full text-left border-collapse">
                    <thead>
                        <tr class="bg-gray-100 text-gray-700 uppercase text-xs">
                            <th class="p-4 border-b">Name</th>
                            <th class="p-4 border-b">Company / Role</th>
                            <th class="p-4 border-b">Platform</th>
                            <th class="p-4 border-b">Last Contact</th>
                            <th class="p-4 border-b">Status</th>
                            <th class="p-4 border-b">Actions</th>
                        </tr>
                    </thead>
                    <tbody id="network-table-body" class="text-sm">
                        <!-- Rows generated by JS -->
                    </tbody>
                </table>
            </div>

            <div class="bg-indigo-50 border border-indigo-100 p-6 rounded-xl space-y-4">
                <h3 class="font-bold text-indigo-900">Generate Outreach Message</h3>
                <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
                    <input type="text" id="outreach-context" placeholder="Context (e.g., Met at AFCON event, or Cold LinkedIn connect)" class="p-2 border rounded-md w-full">
                    <button onclick="generateOutreach()" class="bg-indigo-600 hover:bg-indigo-700 text-white py-2 rounded-lg font-bold transition flex justify-center items-center gap-2">
                        Draft Message <div id="outreach-loader" class="loader hidden ml-2"></div>
                    </button>
                </div>
                <textarea id="outreach-result" rows="4" class="w-full p-3 border rounded-md bg-white" placeholder="AI generated message..."></textarea>
            </div>
        </section>

        <!-- Settings Section -->
        <section id="settings" class="tab-content hidden">
            <h1 class="text-3xl font-bold mb-6 text-indigo-900">Settings & Profile</h1>
            <div class="max-w-2xl bg-white p-6 rounded-xl shadow border border-gray-100 space-y-5">
                <div class="bg-yellow-50 border-l-4 border-yellow-400 p-4 mb-4">
                    <p class="text-sm text-yellow-800 font-bold">API Key Required</p>
                    <p class="text-xs text-yellow-700 mt-1">Please paste your Google Gemini API key below to enable the AI tools. It is stored safely in your local browser storage.</p>
                </div>
                <div>
                    <label class="block text-sm font-bold text-gray-700 mb-1">Gemini API Key</label>
                    <input type="password" id="api-key" class="w-full p-2 border border-gray-300 rounded-md focus:ring focus:ring-indigo-200">
                </div>
                <hr>
                <div class="grid grid-cols-2 gap-4">
                    <div><label class="block text-sm font-medium text-gray-700">Full Name</label><input type="text" id="user-name" class="w-full p-2 border rounded-md"></div>
                    <div><label class="block text-sm font-medium text-gray-700">Target Role</label><input type="text" id="user-role" class="w-full p-2 border rounded-md" placeholder="e.g. Commerce Professional"></div>
                </div>
                <div><label class="block text-sm font-medium text-gray-700">Key Skills & Background (Used by AI to personalize everything)</label><textarea id="user-background" rows="4" class="w-full p-2 border rounded-md" placeholder="e.g. BCom graduate, experience in logistics, looking for full-time roles..."></textarea></div>
                <button onclick="saveSettings()" class="bg-green-600 hover:bg-green-700 text-white px-6 py-2 rounded-lg font-medium transition">Save Settings</button>
            </div>
        </section>

    </main>

    <!-- Modals -->
    <!-- Add Job Modal -->
    <div id="jobModal" class="hidden fixed inset-0 bg-black bg-opacity-50 flex items-center justify-center z-50">
        <div class="bg-white p-6 rounded-xl w-full max-w-md">
            <h2 class="text-xl font-bold mb-4">Add Application</h2>
            <div class="space-y-3">
                <input type="text" id="job-company" placeholder="Company Name" class="w-full p-2 border rounded">
                <input type="text" id="job-title" placeholder="Job Title" class="w-full p-2 border rounded">
                <input type="text" id="job-location" placeholder="Location" class="w-full p-2 border rounded">
                <select id="job-status" class="w-full p-2 border rounded">
                    <option value="Wishlist">Wishlist</option>
                    <option value="Applied">Applied</option>
                    <option value="Interview">Interview</option>
                    <option value="Offer">Offer</option>
                    <option value="Rejected">Rejected</option>
                </select>
                <div class="flex justify-end gap-2 mt-4">
                    <button onclick="document.getElementById('jobModal').classList.add('hidden')" class="px-4 py-2 text-gray-600">Cancel</button>
                    <button onclick="addJob()" class="px-4 py-2 bg-indigo-600 text-white rounded">Save Job</button>
                </div>
            </div>
        </div>
    </div>

    <!-- Add Contact Modal -->
    <div id="networkModal" class="hidden fixed inset-0 bg-black bg-opacity-50 flex items-center justify-center z-50">
        <div class="bg-white p-6 rounded-xl w-full max-w-md">
            <h2 class="text-xl font-bold mb-4">Add Networking Contact</h2>
            <div class="space-y-3">
                <input type="text" id="net-name" placeholder="Contact Name" class="w-full p-2 border rounded">
                <div class="flex gap-2">
                    <input type="text" id="net-company" placeholder="Company" class="w-1/2 p-2 border rounded">
                    <input type="text" id="net-role" placeholder="Role" class="w-1/2 p-2 border rounded">
                </div>
                <select id="net-platform" class="w-full p-2 border rounded">
                    <option value="LinkedIn">LinkedIn</option>
                    <option value="Email">Email</option>
                    <option value="Event">Event</option>
                </select>
                <input type="date" id="net-date" class="w-full p-2 border rounded">
                <select id="net-status" class="w-full p-2 border rounded">
                    <option value="To Contact">To Contact</option>
                    <option value="Awaiting Reply">Awaiting Reply</option>
                    <option value="Connected">Connected</option>
                </select>
                <div class="flex justify-end gap-2 mt-4">
                    <button onclick="document.getElementById('networkModal').classList.add('hidden')" class="px-4 py-2 text-gray-600">Cancel</button>
                    <button onclick="addContact()" class="px-4 py-2 bg-indigo-600 text-white rounded">Save Contact</button>
                </div>
            </div>
        </div>
    </div>

    <script>
        // State Management
        let appData = JSON.parse(localStorage.getItem('careerApp')) || {
            jobs: [],
            contacts: [],
            settings: { apiKey: '', name: '', role: '', background: '' } // API Key intentionally empty
        };

        window.onload = () => {
            loadSettings();
            renderKanban();
            renderNetwork();
            updateStats();
        };

        function saveState() {
            localStorage.setItem('careerApp', JSON.stringify(appData));
            updateStats();
        }

        // Navigation
        function switchTab(tabId) {
            document.querySelectorAll('.tab-content').forEach(el => el.classList.add('hidden'));
            document.getElementById(tabId).classList.remove('hidden');
            const buttons = document.querySelectorAll('aside nav button');
            buttons.forEach(btn => {
                btn.classList.remove('bg-indigo-800');
                if (btn.getAttribute('onclick').includes(tabId)) btn.classList.add('bg-indigo-800');
            });
        }

        // Settings
        function loadSettings() {
            document.getElementById('api-key').value = appData.settings.apiKey || '';
            document.getElementById('user-name').value = appData.settings.name || '';
            document.getElementById('user-role').value = appData.settings.role || '';
            document.getElementById('user-background').value = appData.settings.background || '';
        }

        function saveSettings() {
            appData.settings = {
                apiKey: document.getElementById('api-key').value,
                name: document.getElementById('user-name').value,
                role: document.getElementById('user-role').value,
                background: document.getElementById('user-background').value
            };
            saveState();
            alert('Settings saved successfully!');
        }

        // Dashboard Stats
        function updateStats() {
            document.getElementById('stat-total').innerText = appData.jobs.length;
            document.getElementById('stat-interviews').innerText = appData.jobs.filter(j => j.status === 'Interview').length;
            document.getElementById('stat-offers').innerText = appData.jobs.filter(j => j.status === 'Offer').length;
            document.getElementById('stat-network').innerText = appData.contacts ? appData.contacts.length : 0;
        }

        // Kanban Logic
        function addJob() {
            const job = {
                id: Date.now().toString(), company: document.getElementById('job-company').value,
                title: document.getElementById('job-title').value, location: document.getElementById('job-location').value,
                status: document.getElementById('job-status').value
            };
            if(!job.company || !job.title) return alert('Company and Title required');
            appData.jobs.push(job); saveState(); renderKanban();
            document.getElementById('jobModal').classList.add('hidden');
        }

        function renderKanban() {
            document.querySelectorAll('.kanban-column').forEach(col => col.innerHTML = '');
            appData.jobs.forEach(job => {
                const card = document.createElement('div');
                card.className = 'bg-white p-3 rounded shadow mb-3 border border-gray-200 cursor-move';
                card.draggable = true; card.id = job.id; card.ondragstart = drag;
                card.innerHTML = `<div class="font-bold text-gray-800">${job.title}</div><div class="text-sm text-gray-600">${job.company}</div><div class="text-xs text-gray-400 mt-2 flex justify-between"><span><i class="fa-solid fa-location-dot"></i> ${job.location || 'N/A'}</span><button onclick="deleteJob('${job.id}')" class="text-red-500 hover:text-red-700"><i class="fa-solid fa-trash"></i></button></div>`;
                const column = document.querySelector(`div[data-status="${job.status}"] .kanban-column`);
                if(column) column.appendChild(card);
            });
        }

        function deleteJob(id) { appData.jobs = appData.jobs.filter(j => j.id !== id); saveState(); renderKanban(); }
        function allowDrop(ev) { ev.preventDefault(); ev.currentTarget.classList.add('drag-over'); }
        function drag(ev) { ev.dataTransfer.setData("text", ev.target.id); setTimeout(() => ev.target.classList.add('dragging'), 0); }
        function drop(ev) {
            ev.preventDefault(); document.querySelectorAll('.kanban-column').forEach(col => col.classList.remove('drag-over'));
            const data = ev.dataTransfer.getData("text"); const card = document.getElementById(data);
            card.classList.remove('dragging'); const targetCol = ev.currentTarget.closest('[data-status]');
            if (targetCol) {
                const newStatus = targetCol.getAttribute('data-status');
                const job = appData.jobs.find(j => j.id === data);
                if(job) { job.status = newStatus; saveState(); renderKanban(); }
            }
        }

        // Networking Logic
        function addContact() {
            if(!appData.contacts) appData.contacts = [];
            const contact = {
                id: Date.now().toString(), name: document.getElementById('net-name').value,
                company: document.getElementById('net-company').value, role: document.getElementById('net-role').value,
                platform: document.getElementById('net-platform').value, date: document.getElementById('net-date').value,
                status: document.getElementById('net-status').value
            };
            if(!contact.name) return alert('Name required');
            appData.contacts.push(contact); saveState(); renderNetwork();
            document.getElementById('networkModal').classList.add('hidden');
        }

        function renderNetwork() {
            const tbody = document.getElementById('network-table-body');
            tbody.innerHTML = '';
            if(!appData.contacts) return;
            appData.contacts.forEach(c => {
                const tr = document.createElement('tr');
                tr.className = "border-b hover:bg-gray-50";
                // Simple 7 day reminder check
                const isOld = c.status === 'Awaiting Reply' && (new Date() - new Date(c.date)) > (7 * 24 * 60 * 60 * 1000);
                const statusColor = isOld ? 'text-red-600 font-bold' : 'text-gray-600';
                
                tr.innerHTML = `
                    <td class="p-4 font-medium text-gray-800">${c.name}</td>
                    <td class="p-4">${c.company}<br><span class="text-xs text-gray-500">${c.role}</span></td>
                    <td class="p-4"><span class="bg-gray-200 px-2 py-1 rounded text-xs">${c.platform}</span></td>
                    <td class="p-4">${c.date}</td>
                    <td class="p-4 ${statusColor}">${c.status} ${isOld ? '⚠️' : ''}</td>
                    <td class="p-4"><button onclick="deleteContact('${c.id}')" class="text-red-500 hover:text-red-700"><i class="fa-solid fa-trash"></i></button></td>
                `;
                tbody.appendChild(tr);
            });
        }
        function deleteContact(id) { appData.contacts = appData.contacts.filter(c => c.id !== id); saveState(); renderNetwork(); }

        // --- AI API HELPER ---
        async function callGemini(promptText) {
            const apiKey = appData.settings.apiKey;
            if(!apiKey) throw new Error("API Key is missing. Please add it in Settings.");
            const url = [https://generativelanguage.googleapis.com/v1beta/models/gemini-1.5-pro:generateContent?key=$](https://generativelanguage.googleapis.com/v1beta/models/gemini-1.5-pro:generateContent?key=$){apiKey}`;
            const response = await fetch(url, {
                method: 'POST', headers: { 'Content-Type': 'application/json' },
                body: JSON.stringify({ contents: [{ parts: [{ text: promptText }] }] })
            });
            if (!response.ok) {
                const err = await response.json(); throw new Error(err.error?.message || "Failed to connect to API");
            }
            const data = await response.json();
            return data.candidates[0].content.parts[0].text;
        }

        // Format Helper
        function formatMarkdown(text) {
            return text.replace(/\*\*(.*?)\*\*/g, '<strong>$1</strong>')
                       .replace(/\*(.*?)\*/g, '<em>$1</em>')
                       .replace(/\n\*/g, '<br>• ')
                       .replace(/\n/g, '<br>');
        }

        // Module: LinkedIn Optimizer
        async function analyzeLinkedIn() {
            const text = document.getElementById('li-text').value;
            const target = document.getElementById('li-target').value;
            if(!text) return alert("Please paste LinkedIn text.");
            
            document.getElementById('li-loader').classList.remove('hidden');
            document.getElementById('li-result').innerHTML = "Analyzing profile...";
            const prompt = `Act as an expert career coach. Analyze this LinkedIn profile text. 
            Target Job Title: ${target || 'General'}.
            Provide: 1. A score out of 100. 2. Missing keywords for the target role. 3. Specific section-by-section improvements. Use markdown.
            Profile Text: ${text}`;

            try {
                const response = await callGemini(prompt);
                document.getElementById('li-result').innerHTML = formatMarkdown(response);
            } catch (err) { document.getElementById('li-result').innerHTML = `<span class="text-red-500">${err.message}</span>`; }
            document.getElementById('li-loader').classList.add('hidden');
        }

        // Module: Resume Analyzer
        async function analyzeResume(type) {
            const resText = document.getElementById('res-text').value;
            const jd = document.getElementById('res-jd').value;
            if(!resText) return alert("Please paste Resume text.");

            const loaderId = type === 'score' ? 'res-loader-1' : 'res-loader-2';
            document.getElementById(loaderId).classList.remove('hidden');
            document.getElementById('res-result').innerHTML = "Processing...";

            let prompt = "";
            if (type === 'score') {
                prompt = `Act as an ATS (Applicant Tracking System). Evaluate this resume against this Job Description: ${jd || 'General Professional Role'}. Give a Match Score out of 100, identify missing skills, and suggest formatting fixes. Use markdown. Resume: ${resText}`;
            } else {
                prompt = `Act as an expert resume writer. Rewrite the bullet points in this resume to better align with this Job Description: ${jd}. Make the bullets more impactful using action verbs and metrics. Use markdown. Resume: ${resText}`;
            }

            try {
                const response = await callGemini(prompt);
                document.getElementById('res-result').innerHTML = formatMarkdown(response);
            } catch (err) { document.getElementById('res-result').innerHTML = `<span class="text-red-500">${err.message}</span>`; }
            document.getElementById(loaderId).classList.add('hidden');
        }

        // Module: Cover Letter Generator
        async function generateCoverLetter() {
            const job = document.getElementById('cl-job').value;
            const company = document.getElementById('cl-company').value;
            const desc = document.getElementById('cl-desc').value;
            const tone = document.getElementById('cl-tone').value;
            const { name, role, background } = appData.settings;
            if(!job || !company) return alert("Job Title and Company required.");
            document.getElementById('cl-loader').classList.remove('hidden');
            document.getElementById('cl-result').value = "AI is writing...";
            const prompt = `Write a cover letter. Tone: ${tone}. Job: ${job}. Company: ${company}. Description: ${desc}. Name: ${name}. Background: ${background}. Keep it natural, no placeholder brackets.`;
            try { document.getElementById('cl-result').value = await callGemini(prompt); } 
            catch (err) { document.getElementById('cl-result').value = "Error: " + err.message; }
            document.getElementById('cl-loader').classList.add('hidden');
        }

        // Module: Job Search Matcher
        async function matchJob(btn, title, company) {
            const resultDiv = btn.nextElementSibling;
            const { role, background } = appData.settings;
            if(!background) return alert("Please fill out your Key Skills & Background in Settings first.");
            
            btn.innerText = "Analyzing...";
            const prompt = `I am a professional with this background: ${background}. Rate my fit for the role of ${title} at ${company} out of 100%. Give a 2 sentence explanation.`;
            try {
                const response = await callGemini(prompt);
                resultDiv.innerText = response;
                resultDiv.classList.remove('hidden');
                resultDiv.classList.add('text-indigo-800', 'bg-indigo-50', 'p-2', 'rounded');
                btn.classList.add('hidden');
            } catch (err) {
                btn.innerText = "Error - Try Again";
            }
        }

        // Module: Interview Prep
        async function generateInterview() {
            const job = document.getElementById('int-job').value;
            const company = document.getElementById('int-company').value;
            if(!job) return alert("Job Title required.");
            document.getElementById('int-loader').classList.remove('hidden');
            document.getElementById('int-result').innerHTML = "Generating 10 STAR questions...";
            const prompt = `Generate 10 highly probable interview questions (behavioral and technical) for a ${job} at ${company || 'a company'}. For each question, provide a brief bulleted 'Model Answer' structure using the STAR method. Format nicely with Markdown headings.`;
            try {
                const response = await callGemini(prompt);
                document.getElementById('int-result').innerHTML = formatMarkdown(response);
            } catch (err) { document.getElementById('int-result').innerHTML = `<span class="text-red-500">${err.message}</span>`; }
            document.getElementById('int-loader').classList.add('hidden');
        }

        // Module: Networking Outreach
        async function generateOutreach() {
            const context = document.getElementById('outreach-context').value;
            const { name, role, background } = appData.settings;
            if(!context) return alert("Please provide some context.");
            document.getElementById('outreach-loader').classList.remove('hidden');
            document.getElementById('outreach-result').value = "Drafting...";
            const prompt = `Write a short, professional networking outreach message based on this context: "${context}". My name is ${name}, my target role is ${role}, and my background is: ${background}. Keep it under 100 words, friendly but highly professional.`;
            try { document.getElementById('outreach-result').value = await callGemini(prompt); } 
            catch (err) { document.getElementById('outreach-result').value = "Error: " + err.message; }
            document.getElementById('outreach-loader').classList.add('hidden');
        }

        // Utility
        function copyToClipboard(id) {
            const text = document.getElementById(id); text.select(); document.execCommand('copy'); alert('Copied!');
        }
    </script>
</body>
</html>
