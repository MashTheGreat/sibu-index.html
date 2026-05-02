# sibu-index.html
A website designed to ensure that the hunt for employment is more refined and less stressful
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Career Hub AI</title>
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
                <div class="bg-white p-6 rounded-xl shadow border border-gray-100 text-center">
                    <h3 class="text-gray-500 text-xs font-bold uppercase tracking-wider">Total Apps</h3>
                    <p id="stat-total" class="text-4xl font-bold text-indigo-600 mt-2">0</p>
                </div>
                <div class="bg-white p-6 rounded-xl shadow border border-gray-100 text-center">
                    <h3 class="text-gray-500 text-xs font-bold uppercase tracking-wider">Interviews</h3>
                    <p id="stat-interviews" class="text-4xl font-bold text-green-600 mt-2">0</p>
                </div>
                <div class="bg-white p-6 rounded-xl shadow border border-gray-100 text-center">
                    <h3 class="text-gray-500 text-xs font-bold uppercase tracking-wider">Offers</h3>
                    <p id="stat-offers" class="text-4xl font-bold text-yellow-600 mt-2">0</p>
                </div>
                <div class="bg-white p-6 rounded-xl shadow border border-gray-100 text-center">
                    <h3 class="text-gray-500 text-xs font-bold uppercase tracking-wider">Network Contacts</h3>
                    <p id="stat-network" class="text-4xl font-bold text-purple-600 mt-2">0</p>
                </div>
            </div>
            <div class="bg-indigo-50 border border-indigo-100 p-6 rounded-xl">
                <h2 class="text-lg font-bold text-indigo-900 mb-2">Welcome to your Career Hub</h2>
                <p class="text-indigo-700 text-sm">Paste your Gemini API key in the <strong>Settings</strong> tab to activate all AI modules. All your data stays private and is saved directly to your browser's local storage.</p>
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
                    <div><label class="block text-sm font-medium text-gray-700">Paste your LinkedIn Profile Text</label><textarea id="li-text" rows="8" class="mt-1 w-full p-2 border rounded-md"></textarea></div>
                    <div><label class="block text-sm font-medium text-gray-700">Target Job Title</label><input type="text" id="li-target" class="mt-1 w-full p-2 border rounded-md" placeholder="e.g., Logistics Manager"></div>
                    <button onclick="analyzeLinkedIn()" class="w-full bg-blue-600 hover:bg-blue-700 text-white py-3 rounded-lg font-bold transition flex justify-center items-center gap-2">
                        <i class="fa-brands fa-linkedin"></i> Analyze Profile
                        <div id="li-loader" class="loader hidden ml-2"></div>
                    </button>
                </div>
                <div class="bg-white p-6 rounded-xl shadow border border-gray-100 overflow-y-auto h-[600px] markdown-body" id="li-result">
                    <p class="text-gray-500 italic">Score and keyword gap analysis will appear here...</p>
                </div>
            </div>
        </section>

        <!-- Resume Analyzer -->
        <section id="resume" class="tab-content hidden">
            <h1 class="text-3xl font-bold mb-6 text-indigo-900">AI Resume Analyzer</h1>
            <div class="grid grid-cols-1 lg:grid-cols-2 gap-8">
                <div class="bg-white p-6 rounded-xl shadow border border-gray-100 space-y-4">
                    <div><label class="block text-sm font-medium text-gray-700">Paste Resume Text</label><textarea id="res-text" rows="6" class="mt-1 w-full p-2 border rounded-md"></textarea></div>
                    <div><label class="block text-sm font-medium text-gray-700">Target Job Description</label><textarea id="res-jd" rows="4" class="mt-1 w-full p-2 border rounded-md"></textarea></div>
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
                    <p class="text-gray-500 italic">ATS compatibility check results will appear here...</p>
                </div>
            </div>
        </section>

        <!-- Cover Letter -->
        <section id="cover-letter" class="tab-content hidden">
            <h1 class="text-3xl font-bold mb-6 text-indigo-900">AI Cover Letter Generator</h1>
            <div class="grid grid-cols-1 lg:grid-cols-2 gap-8">
                <div class="bg-white p-6 rounded-xl shadow border border-gray-100 space-y-4">
                    <input type="text" id="cl-job" placeholder="Job Title" class="w-full p-2 border rounded-md">
                    <input type="text" id="cl-company" placeholder="Company Name" class="w-full p-2 border rounded-md">
                    <textarea id="cl-desc" rows="4" placeholder="Job Description" class="w-full p-2 border rounded-md"></textarea>
                    <select id="cl-tone" class="w-full p-2 border rounded-md"><option>Professional</option><option>Enthusiastic</option><option>Concise</option></select>
                    <button onclick="generateCoverLetter()" class="w-full bg-indigo-600 hover:bg-indigo-700 text-white py-3 rounded-lg font-bold transition flex justify-center items-center gap-2">
                        Generate Cover Letter <div id="cl-loader" class="loader hidden ml-2"></div>
                    </button>
                </div>
                <div class="bg-white p-6 rounded-xl shadow border border-gray-100 flex flex-col h-[600px]">
                    <div class="flex justify-between items-center mb-4"><h3 class="font-bold text-gray-800">Generated Result</h3><button onclick="copyToClipboard('cl-result')" class="text-indigo-600 text-sm"><i class="fa-regular fa-copy"></i> Copy</button></div>
                    <textarea id="cl-result" class="flex-1 w-full p-4 border rounded-md bg-gray-50" placeholder="Result..."></textarea>
                </div>
            </div>
        </section>

        <!-- Job Matcher -->
        <section id="jobs" class="tab-content hidden">
            <h1 class="text-3xl font-bold mb-6 text-indigo-900">Job Search Matcher</h1>
            <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6">
                <div class="bg-white p-5 rounded-xl shadow border border-gray-100 flex flex-col">
                    <h3 class="font-bold text-lg">Supply Chain Specialist</h3>
                    <p class="text-gray-500 text-sm mb-3">Transnet • Gqeberha • Full-time</p>
                    <p class="text-sm text-gray-700 flex-1 mb-4">Focus on logistics network optimization and operational efficiency. BCom in Logistics preferred.</p>
                    <button onclick="matchJob(this, 'Supply Chain Specialist', 'Transnet')" class="w-full bg-indigo-100 text-indigo-700 py-2 rounded font-medium hover:bg-indigo-200">AI Match Score</button>
                    <div class="match-result text-sm mt-3 font-bold hidden"></div>
                </div>
                <div class="bg-white p-5 rounded-xl shadow border border-gray-100 flex flex-col">
                    <h3 class="font-bold text-lg">Logistics Trainee</h3>
                    <p class="text-gray-500 text-sm mb-3">Maersk • Gqeberha • Graduate</p>
                    <p class="text-sm text-gray-700 flex-1 mb-4">A entry-level role managing port documentation and client relationships in the Eastern Cape region.</p>
                    <button onclick="matchJob(this, 'Logistics Trainee', 'Maersk')" class="w-full bg-indigo-100 text-indigo-700 py-2 rounded font-medium hover:bg-indigo-200">AI Match Score</button>
                    <div class="match-result text-sm mt-3 font-bold hidden"></div>
                </div>
            </div>
        </section>

        <!-- Interview Prep -->
        <section id="interview" class="tab-content hidden">
            <h1 class="text-3xl font-bold mb-6 text-indigo-900">AI Interview Prep</h1>
            <div class="grid grid-cols-1 lg:grid-cols-3 gap-8">
                <div class="lg:col-span-1 bg-white p-6 rounded-xl shadow border border-gray-100 space-y-4">
                    <input type="text" id="int-job" placeholder="Job Title" class="w-full p-2 border rounded-md">
                    <input type="text" id="int-company" placeholder="Company Name" class="w-full p-2 border rounded-md">
                    <button onclick="generateInterview()" class="w-full bg-indigo-600 hover:bg-indigo-700 text-white py-3 rounded-lg font-bold transition flex justify-center items-center gap-2">
                        Get STAR Questions <div id="int-loader" class="loader hidden ml-2"></div>
                    </button>
                </div>
                <div class="lg:col-span-2 bg-white p-6 rounded-xl shadow border border-gray-100 overflow-y-auto h-[600px] markdown-body" id="int-result">
                    <p class="text-gray-500 italic">Interview questions and model answers will appear here...</p>
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
                    <thead class="bg-gray-100 text-gray-700 uppercase text-xs">
                        <tr><th class="p-4">Name</th><th class="p-4">Company</th><th class="p-4">Platform</th><th class="p-4">Status</th><th class="p-4">Action</th></tr>
                    </thead>
                    <tbody id="network-table-body" class="text-sm"></tbody>
                </table>
            </div>
            <div class="bg-indigo-50 border border-indigo-100 p-6 rounded-xl space-y-4">
                <h3 class="font-bold text-indigo-900">AI Outreach Draft</h3>
                <input type="text" id="outreach-context" placeholder="Where did you meet? (e.g., LinkedIn, Career Fair)" class="p-2 border rounded-md w-full">
                <button onclick="generateOutreach()" class="bg-indigo-600 hover:bg-indigo-700 text-white py-2 rounded-lg font-bold transition flex items-center justify-center gap-2 w-full max-w-xs">Draft Message <div id="outreach-loader" class="loader hidden ml-2"></div></button>
                <textarea id="outreach-result" rows="4" class="w-full p-3 border rounded-md bg-white"></textarea>
            </div>
        </section>

        <!-- Settings -->
        <section id="settings" class="tab-content hidden">
            <h1 class="text-3xl font-bold mb-6 text-indigo-900">Settings</h1>
            <div class="max-w-2xl bg-white p-6 rounded-xl shadow border border-gray-100 space-y-5">
                <div><label class="block text-sm font-bold text-gray-700 mb-1">Gemini API Key</label><input type="password" id="api-key" class="w-full p-2 border border-gray-300 rounded-md"></div>
                <div class="grid grid-cols-2 gap-4">
                    <div><label class="block text-sm font-medium text-gray-700">Full Name</label><input type="text" id="user-name" class="w-full p-2 border rounded-md"></div>
                    <div><label class="block text-sm font-medium text-gray-700">Target Industry</label><input type="text" id="user-role" class="w-full p-2 border rounded-md" placeholder="e.g. Logistics"></div>
                </div>
                <div><label class="block text-sm font-medium text-gray-700">My Background (Short Bio for AI)</label><textarea id="user-background" rows="4" class="w-full p-2 border rounded-md"></textarea></div>
                <button onclick="saveSettings()" class="bg-green-600 hover:bg-green-700 text-white px-6 py-2 rounded-lg font-medium transition">Save Settings</button>
            </div>
        </section>

    </main>

    <!-- Modals -->
    <div id="jobModal" class="hidden fixed inset-0 bg-black bg-opacity-50 flex items-center justify-center z-50">
        <div class="bg-white p-6 rounded-xl w-full max-w-md">
            <h2 class="text-xl font-bold mb-4">Add Application</h2>
            <div class="space-y-3">
                <input type="text" id="job-company" placeholder="Company Name" class="w-full p-2 border rounded">
                <input type="text" id="job-title" placeholder="Job Title" class="w-full p-2 border rounded">
                <select id="job-status" class="w-full p-2 border rounded"><option value="Wishlist">Wishlist</option><option value="Applied">Applied</option><option value="Interview">Interview</option><option value="Offer">Offer</option><option value="Rejected">Rejected</option></select>
                <div class="flex justify-end gap-2 mt-4"><button onclick="document.getElementById('jobModal').classList.add('hidden')" class="px-4 py-2 text-gray-600">Cancel</button><button onclick="addJob()" class="px-4 py-2 bg-indigo-600 text-white rounded">Save</button></div>
            </div>
        </div>
    </div>

    <div id="networkModal" class="hidden fixed inset-0 bg-black bg-opacity-50 flex items-center justify-center z-50">
        <div class="bg-white p-6 rounded-xl w-full max-w-md">
            <h2 class="text-xl font-bold mb-4">Add Contact</h2>
            <div class="space-y-3">
                <input type="text" id="net-name" placeholder="Name" class="w-full p-2 border rounded">
                <input type="text" id="net-company" placeholder="Company" class="w-full p-2 border rounded">
                <select id="net-platform" class="w-full p-2 border rounded"><option>LinkedIn</option><option>Email</option><option>Event</option></select>
                <div class="flex justify-end gap-2 mt-4"><button onclick="document.getElementById('networkModal').classList.add('hidden')" class="px-4 py-2 text-gray-600">Cancel</button><button onclick="addContact()" class="px-4 py-2 bg-indigo-600 text-white rounded">Save</button></div>
            </div>
        </div>
    </div>

    <script>
        // Data State
        let appData = JSON.parse(localStorage.getItem('careerApp')) || {
            jobs: [], contacts: [],
            settings: { apiKey: '', name: '', role: '', background: '' }
        };

        window.onload = () => { loadSettings(); renderKanban(); renderNetwork(); updateStats(); };

        function saveState() { localStorage.setItem('careerApp', JSON.stringify(appData)); updateStats(); }

        function switchTab(tabId) {
            document.querySelectorAll('.tab-content').forEach(el => el.classList.add('hidden'));
            document.getElementById(tabId).classList.remove('hidden');
            document.querySelectorAll('aside nav button').forEach(btn => btn.classList.remove('bg-indigo-800'));
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
            saveState(); alert('Settings saved!');
        }

        // Stats
        function updateStats() {
            document.getElementById('stat-total').innerText = appData.jobs.length;
            document.getElementById('stat-interviews').innerText = appData.jobs.filter(j => j.status === 'Interview').length;
            document.getElementById('stat-offers').innerText = appData.jobs.filter(j => j.status === 'Offer').length;
            document.getElementById('stat-network').innerText = appData.contacts.length;
        }

        // Kanban
        function addJob() {
            const job = { id: Date.now().toString(), company: document.getElementById('job-company').value, title: document.getElementById('job-title').value, status: document.getElementById('job-status').value };
            if(!job.company || !job.title) return alert('Fill info');
            appData.jobs.push(job); saveState(); renderKanban(); document.getElementById('jobModal').classList.add('hidden');
        }

        function renderKanban() {
            document.querySelectorAll('.kanban-column').forEach(col => col.innerHTML = '');
            appData.jobs.forEach(job => {
                const card = document.createElement('div');
                card.className = 'bg-white p-3 rounded shadow mb-3 border border-gray-200 cursor-move';
                card.draggable = true; card.id = job.id; card.ondragstart = drag;
                card.innerHTML = `<div class='font-bold text-gray-800 text-sm'>${job.title}</div><div class='text-xs text-gray-500'>${job.company}</div><button onclick="deleteJob('${job.id}')" class='text-red-400 text-xs mt-2'>Delete</button>`;
                const column = document.querySelector(`div[data-status="${job.status}"] .kanban-column`);
                if(column) column.appendChild(card);
            });
        }
        function deleteJob(id) { appData.jobs = appData.jobs.filter(j => j.id !== id); saveState(); renderKanban(); }
        function allowDrop(ev) { ev.preventDefault(); ev.currentTarget.classList.add('drag-over'); }
        function drag(ev) { ev.dataTransfer.setData("text", ev.target.id); }
        function drop(ev) {
            ev.preventDefault(); document.querySelectorAll('.kanban-column').forEach(col => col.classList.remove('drag-over'));
            const data = ev.dataTransfer.getData("text");
            const targetCol = ev.currentTarget.closest('[data-status]');
            const job = appData.jobs.find(j => j.id === data);
            if(job && targetCol) { job.status = targetCol.getAttribute('data-status'); saveState(); renderKanban(); }
        }

        // Networking
        function addContact() {
            const contact = { id: Date.now().toString(), name: document.getElementById('net-name').value, company: document.getElementById('net-company').value, platform: document.getElementById('net-platform').value };
            if(!contact.name) return; appData.contacts.push(contact); saveState(); renderNetwork(); document.getElementById('networkModal').classList.add('hidden');
        }
        function renderNetwork() {
            const body = document.getElementById('network-table-body'); body.innerHTML = '';
            appData.contacts.forEach(c => {
                const row = `<tr><td class='p-4'>${c.name}</td><td class='p-4'>${c.company}</td><td class='p-4'>${c.platform}</td><td class='p-4 text-xs text-blue-600'>Active</td><td class='p-4'><button onclick="deleteContact('${c.id}')" class='text-red-500'>X</button></td></tr>`;
                body.innerHTML += row;
            });
        }
        function deleteContact(id) { appData.contacts = appData.contacts.filter(c => c.id !== id); saveState(); renderNetwork(); }

        // --- AI LOGIC (FIXED ENDPOINT) ---
        async function callGemini(promptText) {
            const apiKey = appData.settings.apiKey;
            if(!apiKey) throw new Error("Missing API Key in Settings.");
            const url = `https://generativelanguage.googleapis.com/v1beta/models/gemini-1.5-pro:generateContent?key=${apiKey}`;
            const response = await fetch(url, {
                method: 'POST', headers: { 'Content-Type': 'application/json' },
                body: JSON.stringify({ contents: [{ parts: [{ text: promptText }] }] })
            });
            if (!response.ok) { const err = await response.json(); throw new Error(err.error?.message || "API Error"); }
            const data = await response.json();
            return data.candidates[0].content.parts[0].text;
        }

        function formatMarkdown(text) {
            return text.replace(/\*\*(.*?)\*\*/g, '<strong>$1</strong>').replace(/\n/g, '<br>');
        }

        // Modules
        async function analyzeLinkedIn() {
            const text = document.getElementById('li-text').value;
            if(!text) return; document.getElementById('li-loader').classList.remove('hidden');
            try { const res = await callGemini(`Analyze this LinkedIn profile and score out of 100 for a role in ${document.getElementById('li-target').value}. Give section feedback: ${text}`); document.getElementById('li-result').innerHTML = formatMarkdown(res); }
            catch(e) { alert(e.message); } document.getElementById('li-loader').classList.add('hidden');
        }

        async function analyzeResume(type) {
            const text = document.getElementById('res-text').value;
            const loader = type === 'score' ? 'res-loader-1' : 'res-loader-2';
            document.getElementById(loader).classList.remove('hidden');
            try { const res = await callGemini(`Act as a resume expert. ${type === 'score' ? 'Score this resume vs JD' : 'Tailor bullet points'}. Resume: ${text}. JD: ${document.getElementById('res-jd').value}`); document.getElementById('res-result').innerHTML = formatMarkdown(res); }
            catch(e) { alert(e.message); } document.getElementById(loader).classList.add('hidden');
        }

        async function generateCoverLetter() {
            document.getElementById('cl-loader').classList.remove('hidden');
            const p = `Write a ${document.getElementById('cl-tone').value} cover letter for ${document.getElementById('cl-job').value} at ${document.getElementById('cl-company').value}. My bio: ${appData.settings.background}`;
            try { document.getElementById('cl-result').value = await callGemini(p); } catch(e) { alert(e.message); }
            document.getElementById('cl-loader').classList.add('hidden');
        }

        async function generateInterview() {
            document.getElementById('int-loader').classList.remove('hidden');
            try { const res = await callGemini(`Generate 10 STAR interview questions and model answers for a ${document.getElementById('int-job').value} at ${document.getElementById('int-company').value}`); document.getElementById('int-result').innerHTML = formatMarkdown(res); }
            catch(e) { alert(e.message); } document.getElementById('int-loader').classList.add('hidden');
        }

        async function matchJob(btn, title, company) {
            const resDiv = btn.nextElementSibling;
            try { const res = await callGemini(`How well does this background match ${title} at ${company}? Background: ${appData.settings.background}`); resDiv.innerText = res; resDiv.classList.remove('hidden'); btn.classList.add('hidden'); }
            catch(e) { alert(e.message); }
        }

        async function generateOutreach() {
            document.getElementById('outreach-loader').classList.remove('hidden');
            try { const res = await callGemini(`Draft a short professional networking message. Context: ${document.getElementById('outreach-context').value}. My name: ${appData.settings.name}`); document.getElementById('outreach-result').value = res; }
            catch(e) { alert(e.message); } document.getElementById('outreach-loader').classList.add('hidden');
        }

        function copyToClipboard(id) { const el = document.getElementById(id); el.select(); document.execCommand('copy'); alert('Copied'); }
    </script>
</body>
</html>
