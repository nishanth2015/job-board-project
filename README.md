<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Job Seeker Portal</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <script src="https://unpkg.com/lucide@latest"></script>
    <style>
        body { font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Helvetica, Arial, sans-serif; }
        .animate-spin { animation: spin 1s linear infinite; }
        @keyframes spin { from { transform: rotate(0deg); } to { transform: rotate(360deg); } }
        .animate-bounce { animation: bounce 1s infinite; }
        @keyframes bounce { 0%, 100% { transform: translateY(-5%); } 50% { transform: translateY(0); } }
    </style>
</head>
<body class="bg-slate-50 text-slate-800 pb-20">

    <!-- Header -->
    <header class="bg-white shadow-sm border-b border-slate-200 sticky top-0 z-10">
        <div class="max-w-4xl mx-auto px-6 py-4 flex justify-between items-center">
            <h1 class="text-xl font-bold text-indigo-700">Job Seeker Portal</h1>
            <div class="flex items-center gap-2">
                <span class="text-sm text-slate-500 hidden md:inline">Logged in as Nishanth</span>
                <div class="w-8 h-8 bg-indigo-100 rounded-full flex items-center justify-center text-indigo-700 font-bold">N</div>
            </div>
        </div>
    </header>

    <main class="max-w-4xl mx-auto px-4 md:px-6 mt-6">
        
        <!-- Progress Bar -->
        <div class="bg-white p-4 md:p-6 rounded-xl shadow-sm mb-6 border border-slate-100">
            <div class="flex justify-between items-center mb-2">
                <h2 class="text-sm font-semibold text-slate-600">Profile Completion</h2>
                <span id="progress-text" class="text-sm font-bold text-indigo-600">0%</span>
            </div>
            <div class="w-full bg-slate-200 rounded-full h-2.5">
                <div id="progress-bar" class="bg-indigo-600 h-2.5 rounded-full transition-all duration-500 ease-out" style="width: 0%"></div>
            </div>
        </div>

        <!-- Error Banner -->
        <div id="error-banner" class="hidden bg-red-50 border-l-4 border-red-500 p-4 mb-6 rounded-r-lg flex items-start gap-3">
            <i data-lucide="alert-circle" class="text-red-500 mt-0.5" size="20"></i>
            <div>
                <p class="font-semibold text-red-700">Missing Mandatory Fields</p>
                <p id="error-message" class="text-red-600 text-sm">Please fill in the required fields.</p>
            </div>
        </div>

        <!-- AI Upload Zone -->
        <div class="bg-white p-4 md:p-6 rounded-xl shadow-sm mb-6 border border-slate-100">
            <h2 class="text-lg font-semibold mb-4 text-slate-800">AI-Powered CV Parsing</h2>
            <div id="upload-zone" class="border-2 border-dashed border-indigo-200 bg-indigo-50/50 rounded-lg p-6 text-center relative cursor-pointer hover:bg-indigo-50 transition-colors">
                <input type="file" id="file-input" accept=".pdf,.doc,.docx" class="absolute inset-0 w-full h-full opacity-0 cursor-pointer" />
                <div id="upload-idle" class="flex flex-col items-center text-slate-500">
                    <i data-lucide="upload" class="mb-2 text-indigo-500" size="32"></i>
                    <p class="font-medium text-slate-700">Upload your CV to auto-fill</p>
                    <p class="text-xs text-slate-400 mt-1">Supports PDF, DOC, DOCX</p>
                </div>
                <div id="upload-loading" class="hidden flex-col items-center text-indigo-600">
                    <i data-lucide="loader-2" class="animate-spin mb-2" size="32"></i>
                    <p class="font-medium">AI is extracting your data...</p>
                </div>
            </div>
        </div>

        <!-- Form Sections -->
        <div class="bg-white p-4 md:p-6 rounded-xl shadow-sm mb-6 border border-slate-100 space-y-8">
            
            <!-- Personal Info -->
            <section>
                <h3 class="text-lg font-semibold text-slate-800 border-b pb-2 mb-4">Personal Information</h3>
                <div class="grid grid-cols-1 md:grid-cols-3 gap-4">
                    <div>
                        <label class="block text-sm font-medium text-slate-600 mb-1">First Name *</label>
                        <input type="text" id="firstName" class="w-full p-2.5 border border-slate-300 rounded-lg focus:ring-2 focus:ring-indigo-500 outline-none" placeholder="e.g. Nishanth">
                    </div>
                    <div>
                        <label class="block text-sm font-medium text-slate-600 mb-1">Last Name *</label>
                        <input type="text" id="lastName" class="w-full p-2.5 border border-slate-300 rounded-lg focus:ring-2 focus:ring-indigo-500 outline-none" placeholder="e.g. P">
                    </div>
                    <div>
                        <label class="block text-sm font-medium text-slate-600 mb-1">Date of Birth *</label>
                        <input type="date" id="dob" class="w-full p-2.5 border border-slate-300 rounded-lg focus:ring-2 focus:ring-indigo-500 outline-none">
                    </div>
                    <div class="md:col-span-3">
                        <label class="block text-sm font-medium text-slate-600 mb-1">Specialization *</label>
                        <select id="specialization" class="w-full p-2.5 border border-slate-300 rounded-lg focus:ring-2 focus:ring-indigo-500 outline-none">
                            <option value="">Select Specialization</option>
                            <option value="Business Analysis" selected>Business Analysis</option>
                            <option value="Software Engineering">Software Engineering</option>
                            <option value="Product Management">Product Management</option>
                            <option value="Data Science">Data Science</option>
                        </select>
                    </div>
                </div>
            </section>

            <!-- Address -->
            <section>
                <h3 class="text-lg font-semibold text-slate-800 border-b pb-2 mb-4">Address Details</h3>
                <div class="space-y-4">
                    <div>
                        <label class="block text-sm font-medium text-slate-600 mb-1">Current Address *</label>
                        <textarea id="currentAddress" rows="2" class="w-full p-2.5 border border-slate-300 rounded-lg focus:ring-2 focus:ring-indigo-500 outline-none" placeholder="City, State, Country"></textarea>
                    </div>
                    <div class="flex items-center gap-2">
                        <input type="checkbox" id="sameAsCurrent" class="w-4 h-4 text-indigo-600 rounded">
                        <label class="text-sm text-slate-600">Permanent address is same as current</label>
                    </div>
                    <div id="permanent-address-container" class="hidden">
                        <label class="block text-sm font-medium text-slate-600 mb-1">Permanent Address</label>
                        <textarea id="permanentAddress" rows="2" class="w-full p-2.5 border border-slate-300 rounded-lg focus:ring-2 focus:ring-indigo-500 outline-none"></textarea>
                    </div>
                </div>
            </section>

            <!-- Experience -->
            <section>
                <div class="flex justify-between items-center border-b pb-2 mb-4">
                    <h3 class="text-lg font-semibold text-slate-800">Work Experience</h3>
                    <button onclick="addExperience()" class="text-sm text-indigo-600 font-medium flex items-center gap-1"><i data-lucide="plus" size="16"></i> Add Role</button>
                </div>
                <div id="experience-container" class="space-y-4"></div>
            </section>
        </div>

        <!-- Action Buttons -->
        <div class="flex justify-end gap-4 mb-8">
            <button onclick="validateAndSubmit()" class="w-full md:w-auto px-6 py-3 rounded-lg bg-indigo-600 text-white font-bold hover:bg-indigo-700 shadow-md transition-colors">Validate & Submit</button>
        </div>

        <!-- AI Results Section -->
        <div id="results-section" class=" detailshidden space-y-6">
            
            <!-- AI Generated CV to -->
            <div class="bg-white p-6 rounded-xl shadow-sm border border-slate-100">
                <h3 class="text-lg font-semibold text-slate-800 mb-4 flex items-center gap-2"><i data-lucide="download" class="text-indigo-600"></i> AI-Generated CV</h3>
                <div id="cv-output" class="bg-slate-50 p-4 rounded-lg border border-slate-200 text-sm overflow-x-auto whitespace-pre-wrap font-mono"></div>
            </div>

            <!-- Job Recommendations -->
            <div class="bg-white p-6 rounded-xl shadow-sm border border-slate-100">
                <h3 class="text-lg font-semibold text-slate-800 mb-2 flex items-center gap-2"><i data-lucide="briefcase" class="text-indigo-600"></i> AI Job Recommendations</h3>
                <p class="text-sm text-slate-600 mb-4">Based on your profile, you are eligible for: <span id="eligible-roles" class="font-semibold text-indigo-700"></span></p>
                <div id="jobs-list" class="space-y-4"></div>
            </div>
        </div>

    </main>

    <!-- Portal Connection Modal -->
    <div id="portal-modal" class="hidden fixed inset-0 bg-black/50 flex items-center justify-center p-4 z-50">
        <div class="bg-white rounded-xl p-6 w-full max-w-sm">
            <h3 class="text-lg font-bold mb-2">Connect to Portal</h3>
            <p class="text-sm text-slate-500 mb-4">Enter your login apply directly.</p>
            <input type="text" id="portal-user" placeholder="Username / Email" class="w-full p-2 border border-slate-300 rounded-lg mb-3">
            <input type="password" id="portal-pass" placeholder="Password" class="w-full p-2 border border-slate-300 rounded-lg mb-4">
            <div class="flex justify-end gap-2">
                <button onclick="closeModal()" class="px-4 py-2 text-slate-600 text-sm font-medium">Cancel</button>
                <button onclick="submitPortal()" class="px-4 py-2 bg-indigo-600 text-white text-sm font-bold rounded-lg">Connect & Redirect</button>
            </div>
        </div>
    </div>

    <!-- Toast Notification -->
    <div id="toast" class="hidden fixed bottom-6 right-6 bg-emerald-500 text-white px-6 py-3 rounded-lg shadow-lg flex items-center gap-2">
        <i data-lucide="check-circle" size="20"></i>
        <span class="font-medium">Profile Processed Successfully!</span>
    </div>

    <script>
        // Initialize Lucide icons
        lucide.createIcons();

        // --- STATE MANAGEMENT ---
        let experienceData = [];
        let currentJobUrl = "";

        // Pre-defined data from the PDF (Simulating AI Extraction)
        const extractedData = {
            firstName: "Nishanth",
            lastName: "P",
            dob: "1990-01-01", // Placeholder as not in PDF
            specialization: "Business Analysis",
            currentAddress: "Hyderabad, India", // Placeholder
            experience: [
                { role: "Product Owner", company: "Ernst & Young (EY)", location: "National Vaccination Management System", startDate: "May 2022", endDate: "Apr 2023", description: "Led requirement elicitation and discovery sessions for a National Vaccination Management System reaching 5M+ citizens. Mapped 10+ clearinghouse data exchange processes and defined exception-handling logic. Facilitated 25+ cross-functional workshops with government and technical stakeholders." },
                { role: "Senior Business Analyst", company: "Infor", location: "Healthcare IT Clients", startDate: "Oct 2021", endDate: "May 2022", description: "Led structured discovery and requirement elicitation sessions across 6 Healthcare IT modules. Documented 30+ Functional and Technical Specifications, process flows, and use case descriptions. Maintained requirement traceability matrices and supported UAT sign-off." },
                { role: "Project Manager", company: "Ernst & Young (EY)", location: "Karnataka Government Insurance Department", startDate: "Jan 2020", endDate: "Oct 2021", description: "Engaged stakeholders to align solution designs with strategic objectives. Developed PMO frameworks and managed RAID governance across 50+ risks and issues. Contributed to 5 RFP responses and consulting proposals, supporting $20M+ in government insurance modernisation pursuits." },
                { role: "PMO", company: "Ernst & Young (EY)", location: "Navratnalu", startDate: "Aug 2019", endDate: "Jan 2020", description: "Reported programme status directly to the PA to the Chief Minister of Andhra Pradesh across 10+ milestones for a welfare initiative reaching 1M+ citizens. Established PMO governance structures — status reporting, RAID tracking, review cadences." },
                { role: "Senior Business Analyst", company: "Ernst & Young (EY)", location: "e-Pragathi", startDate: "Aug 2018", endDate: "Aug 2019", description: "Conducted discovery sessions, interviews, and workshops for Pega BPM implementations; drafted 15+ BRDs aligned with Functional and Technical Specifications. Led Pega-based implementations end-to-end, driving a 30% improvement in team productivity." },
                { role: "Senior Business Analyst", company: "SRIT", location: "ESIC Healthcare IT, Aarogyasri", startDate: "Oct 2016", endDate: "Aug 2018", description: "Built traceability matrices linking 200+ requirements to test cases, reducing audit findings by about 25%. Facilitated 15+ stakeholder sign-off sessions across ESIC and Aarogyasri workstreams. Partnered with QA leads to prioritise defect triage ahead of release milestones." },
                { role: "Senior Business Analyst", company: "Wipro Technologies", location: "ESIC", startDate: "Nov 2013", endDate: "Oct 2016", description: "Used HL7, SNOMED CT, and FHIR standards to write 25+ detailed Requirement Specification Documents for enterprise healthcare platforms. Trained 5,000+ end users across 8 hospital sites, driving about 95% adoption within 3 months of go-live." },
                { role: "Senior Business Analyst", company: "Apollo Hospitals", location: "Medmantra", startDate: "Aug 2010", endDate: "Oct 2013", description: "Analysed healthcare data using HL7 standards; streamlined clinical processes with SNOMED CT, cutting documentation discrepancies by about 20%. Supported data migration and validation activities during Medmantra HIS rollouts across multiple hospital departments." }
            ]
        };

        // --- AI UPLOAD SIMULATION ---
        document.getElementById('file-input').addEventListener('change', function(e) {
            if (!e.target.files.length) return;
            
            // Show loading state
            document.getElementById('upload-idle').classList.add('hidden');
            document.getElementById('upload-loading').classList.remove('hidden');
            document.getElementById('upload-loading').classList.add('flex');

            // Simulate AI Processing time
            setTimeout(() => {
                // Populate form fields
                document.getElementById('firstName').value = extractedData.firstName;
                document.getElementById('lastName').value = extractedData.lastName;
                document.getElementById('dob').value = extractedData.dob;
                document.getElementById('specialization').value = extractedData.specialization;
                document.getElementById('currentAddress').value = extractedData.currentAddress;

                // Populate Experience
                experienceData = extractedData.experience;
                renderExperience();

                // Reset UI
                document.getElementById('upload-idle').classList.remove('hidden');
                document.getElementById('upload-loading').classList.add('hidden');
                document.getElementById('upload-loading').classList.remove('flex');

                updateProgress();
                showToast("CV Parsed Successfully!");
            }, 2000);
        });

        // --- EXPERIENCE FORM LOGIC ---
        function addExperience() {
            experienceData.push({ role: '', company: '', location: '', startDate: '', endDate: '', description: '' });
            renderExperience();
            updateProgress();
        }

        function removeExperience(index) {
            experienceData.splice(index, 1);
            renderExperience();
            updateProgress();
        }

        function updateExperience(index, field, value) {
            experienceData[index][field] = value;
            updateProgress();
        }

        function renderExperience() {
            const container = document.getElementById('experience-container');
            if (experienceData.length === 0) {
                container.innerHTML = '<p class="text-sm text-slate-400 text-center py-4">No experience added yet. Tap "Add Role" to begin.</p>';
                return;
            }

            container.innerHTML = experienceData.map((exp, index) => `
                <div class="bg-slate-50 p-4 rounded-lg border border-slate-200 relative">
                    <button onclick="removeExperience(${index})" class="absolute top-4 right-4 text-red-400 hover:text-red-600"><i data-lucide="trash-2" size="18"></i></button>
                    <div class="grid grid-cols-1 md:grid-cols-2 gap-3 mb-3">
                        <input type="text" value="${exp.role}" oninput="updateExperience(${index}, 'role', this.value)" placeholder="Job Title" class="p-2 border border-slate-300 rounded-lg text-sm w-full">
                        <input type="text" value="${exp.company}" oninput="updateExperience(${index}, 'company', this.value)" placeholder="Company Name" class="p-2 border border-slate-300 rounded-lg text-sm w-full">
                        <input type="text" value="${exp.location}" oninput="updateExperience(${index}, 'location', this.value)" placeholder="Client / Domain / Location" class="p-2 border border-slate-300 rounded-lg text-sm w-full">
                        <div class="flex gap-2">
                            <input type="text" value="${exp.startDate}" oninput="updateExperience(${index}, 'startDate', this.value)" placeholder="Start Date" class="p-2 border border-slate-300 rounded-lg text-sm w-full">
                            <input type="text" value="${exp.endDate}" oninput="updateExperience(${index}, 'endDate', this.value)" placeholder="End Date" class="p-2 border border-slate-300 rounded-lg text-sm w-full">
                        </div>
                    </div>
                    <textarea oninput="updateExperience(${index}, 'description', this.value)" placeholder="Description / Achievements" rows="3" class="w-full p-2 border border-slate-300 rounded-lg text-sm">${exp.description}</textarea>
                </div>
            `).join('');
            lucide.createIcons();
        }

        // --- PROGRESS & VALIDATION ---
        function updateProgress() {
            const mandatory = ['firstName', 'lastName', 'dob', 'specialization', 'currentAddress'];
            const filledMandatory = mandatory.filter(id => document.getElementById(id).value.trim() !== '').length;
            const hasExperience = experienceData.length > 0 ? 1 : 0;
            
            const total = mandatory.length + 1;
            const progress = Math.round(((filledMandatory + hasExperience) / total) * 100);
            
            document.getElementById('progress-bar').style.width = progress + '%';
            document.getElementById('progress-text').innerText = progress + '%';
        }

        // Add event listeners for live progress tracking
        ['firstName', 'lastName', 'dob', 'specialization', 'currentAddress'].forEach(id => {
            document.getElementById(id).addEventListener('input', updateProgress);
        });

        document.getElementById('sameAsCurrent').addEventListener('change', function(e) {
            const container = document.getElementById('permanent-address-container');
            if (e.target.checked) {
                container.classList.add('hidden');
                document.getElementById('permanentAddress').value = document.getElementById('currentAddress').value;
            } else {
                container.classList.remove('hidden');
            }
            updateProgress();
        });

        function validateAndSubmit() {
            const mandatory = ['firstName', 'lastName', 'dob', 'specialization', 'currentAddress'];
            let missing = [];
            
            mandatory.forEach(id => {
                const el = document.getElementById(id);
                if (!el.value.trim()) {
                    missing.push(id);
                    el.classList.add('border-red-500', 'bg-red-50');
                } else {
                    el.classList.remove('border-red-500', 'bg-red-50');
                }
            });

            if (missing.length > 0) {
                document.getElementById('error-banner').classList.remove('hidden');
                document.getElementById('error-message').innerText = "Please fill in: " + missing.map(m => m.replace(/([A-Z])/g, ' $1').trim()).join(', ');
                window.scrollTo({ top: 0, behavior: 'smooth' });
                return;
            }

            document.getElementById('error-banner').classList.add('hidden');
            
            // Trigger AI Generation
            generateAIResults();
        }

        // --- AI CV GENERATION & JOB RECOMMENDATIONS ---
        function generateAIResults() {
            const fName = document.getElementById('firstName').value;
            const lName = document.getElementById('lastName').value;
            const spec = document.getElementById('specialization').value;
            const address = document.getElementById('currentAddress').value;

            // 1. Generate CV in the format provided in the PDF
            let cvText = `=========================================\n${fName.toUpperCase()} ${lName.toUpperCase()}\n${spec}\n=========================================\n\n`;
            cvText += `PROFESSIONAL SUMMARY\n--------------------\nHighly skilled ${spec} professional with over 10 years of experience in healthcare IT, government projects, and business process management. Proven track record in requirement elicitation, stakeholder management, and driving successful project outcomes.\n\n`;
            cvText += `WORK EXPERIENCE\n---------------\n`;
            
            experienceData.forEach(exp => {
                cvText += `\n${exp.role} | ${exp.company}\n`;
                if(exp.location) cvText += `Domain/Client: ${exp.location} | ${exp.startDate} - ${exp.endDate}\n`;
                cvText += `• ${exp.description}\n`;
            });

            cvText += `\nCERTIFICATIONS\n--------------\n`;
            cvText += `• Certified Pega Business Architect (CPBA) – Pegasystems\n`;
            cvText += `• Robust Scrum Product Owner (RSPO) – Agile Scrum Certification\n\n`;
            cvText += `EDUCATION\n---------\n`;
            cvText += `• M.Tech – Parallel Computing | Aurora College of Engineering, JNTU Hyderabad | 2008 – 2012\n`;
            cvText += `• B.Tech – Industrial & Production Engineering | Jaya Prakash Narayan College of Engineering, JNTU Hyderabad | 2002 – 2007\n`;

            document.getElementById('cv-output').innerText = cvText;
            document.getElementById('results-section').classList.remove('hidden');

            // 2. Job Recommendations
            document.getElementById('eligible-roles').innerText = "Senior Business Analyst, Product Owner, Project Manager";
            
            const jobs = [
                { title: "Senior Business Analyst", company: "Deloitte", match: 95, keywords: ["Requirement Elicitation", "Stakeholder Management", "Healthcare IT"], tip: "Highlight your experience with EY and Infor.", url: "https://www2.deloitte.com/global/en/careers.html" },
                { title: "Product Owner", company: "Tech Mahindra", match: 90, keywords: ["Agile", "Scrum", "Product Backlog"], tip: "Emphasize your RSPO certification and Product Owner role at EY.", url: "https://careers.techmahindra.com/" },
                { title: "Project Manager", company: "Accenture", match: 85, keywords: ["PMO", "RAID", "Government Projects"], tip: "Focus on your $20M+ government insurance modernisation project.", url: "https://www.accenture.com/us-en/careers" }
            ];

            const jobsList = document.getElementById('jobs-list');
            jobsList.innerHTML = jobs.map((job, idx) => `
                <div class="border border-slate-200 rounded-lg p-4 flex flex-col md:flex-row justify-between items-start md:items-center gap-4">
                    <div>
                        <h4 class="font-bold text-slate-800">${job.title}</h4>
                        <p class="text-sm text-slate-500">${job.company}</p>
                        <div class="flex flex-wrap gap-2 mt-2">
                            ${job.keywords.map(k => `<span class="bg-indigo-50 text-indigo-600 text-xs px-2 py-1 rounded">${k}</span>`).join('')}
                        </div>
                        <p class="text-xs text-slate-400 mt-2">💡 AI Tip: ${job.tip}</p>
                    </div>
                    <div class="flex flex-col items-end gap-2 w-full md:w-auto">
                        <span class="text-sm font-bold text-emerald-600">${job.match}% Match</span>
                        <button onclick="openModal('${job.url}', '${job.company}')" class="w-full md:w-auto px-4 py-2 bg-indigo-600 text-white text-sm rounded-lg hover:bg-indigo-700 flex items-center justify-center gap-1">
                            <i data-lucide="key" size="14"></i> Connect & Apply <i data-lucide="external-link" size="14"></i>
                        </button>
                    </div>
                </div>
            `).join('');
            lucide.createIcons();

            showToast("AI Processing Complete!");
        }

        // --- PORTAL CONNECTION MODAL ---
        function openModal(url, company) {
            currentJobUrl = url;
            document.getElementById('portal-modal').classList.remove('hidden');
        }

        function closeModal() {
            document.getElementById('portal-modal').classList.add('hidden');
            document.getElementById('portal-user').value = '';
            document.getElementById('portal-pass').value = '';
        }

        function submitPortal() {
            const user = document.getElementById('portal-user').value;
            const pass = document.getElementById('portal-pass').value;
            if (!user || !pass) {
                alert("Please enter dummy credentials to simulate connection.");
                return;
            }
            closeModal();
            showToast("Portal Connected! Redirecting...");
            setTimeout(() => {
                window.open(currentJobUrl, '_blank');
            }, 1000);
        }

        // --- UTILITIES ---
        function showToast(message) {
            const toast = document.getElementById('toast');
            toast.querySelector('span').innerText = message;
            toast.classList.remove('hidden');
            setTimeout(() => toast.classList.add('hidden'), 3000);
        }

        // Initialize empty experience section
        renderExperience();
    </script>
</body>
</html>
