<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=yes">
    <title>AI-Powered Project Management System | Advanced RBM Platform</title>
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <script src="https://cdn.jsdelivr.net/npm/xlsx@0.18.5/dist/xlsx.full.min.js"></script>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            min-height: 100vh;
            padding: 20px;
        }

        .container {
            max-width: 1600px;
            margin: 0 auto;
        }

        /* Header */
        .header {
            background: white;
            border-radius: 15px;
            padding: 25px;
            margin-bottom: 25px;
            box-shadow: 0 10px 30px rgba(0,0,0,0.2);
            text-align: center;
        }

        .header h1 {
            background: linear-gradient(135deg, #667eea, #764ba2);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
            font-size: 2.2em;
            margin-bottom: 10px;
        }

        /* Stats Bar */
        .stats-bar {
            background: white;
            border-radius: 15px;
            padding: 15px 25px;
            margin-bottom: 25px;
            display: flex;
            justify-content: space-around;
            flex-wrap: wrap;
            gap: 15px;
            box-shadow: 0 5px 15px rgba(0,0,0,0.1);
        }

        .stat-card {
            text-align: center;
            padding: 10px 20px;
            background: linear-gradient(135deg, #f5f7fa 0%, #c3cfe2 100%);
            border-radius: 10px;
            min-width: 150px;
        }

        .stat-number {
            font-size: 2em;
            font-weight: bold;
            color: #667eea;
        }

        /* Tabs */
        .tabs {
            display: flex;
            gap: 10px;
            margin-bottom: 25px;
            flex-wrap: wrap;
        }

        .tab-btn {
            background: white;
            border: none;
            padding: 12px 25px;
            font-size: 0.9em;
            font-weight: 600;
            border-radius: 10px;
            cursor: pointer;
            transition: all 0.3s;
            color: #667eea;
            box-shadow: 0 2px 5px rgba(0,0,0,0.1);
        }

        .tab-btn:hover, .tab-btn.active {
            background: linear-gradient(135deg, #667eea, #764ba2);
            color: white;
            transform: translateY(-2px);
        }

        /* Tab Content */
        .tab-content {
            display: none;
            background: white;
            border-radius: 15px;
            padding: 25px;
            box-shadow: 0 10px 30px rgba(0,0,0,0.2);
            animation: fadeIn 0.5s;
        }

        .tab-content.active {
            display: block;
        }

        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(10px); }
            to { opacity: 1; transform: translateY(0); }
        }

        /* Forms */
        .form-group {
            margin-bottom: 20px;
        }

        label {
            display: block;
            margin-bottom: 8px;
            font-weight: 600;
            color: #333;
        }

        input, textarea, select {
            width: 100%;
            padding: 12px;
            border: 2px solid #e0e0e0;
            border-radius: 8px;
            font-size: 1em;
            transition: border 0.3s;
        }

        input:focus, textarea:focus, select:focus {
            outline: none;
            border-color: #667eea;
        }

        button {
            background: linear-gradient(135deg, #667eea, #764ba2);
            color: white;
            border: none;
            padding: 12px 30px;
            font-size: 1em;
            font-weight: 600;
            border-radius: 8px;
            cursor: pointer;
            transition: transform 0.2s;
        }

        button:hover {
            transform: scale(1.02);
        }

        /* Cards */
        .cards-grid {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(380px, 1fr));
            gap: 20px;
            margin-top: 20px;
        }

        .card {
            background: #f8f9fa;
            border-radius: 12px;
            padding: 20px;
            border-left: 5px solid #667eea;
            transition: transform 0.2s;
        }

        .card:hover {
            transform: translateY(-5px);
            box-shadow: 0 5px 20px rgba(0,0,0,0.1);
        }

        /* Budget Monitor */
        .budget-monitor {
            background: linear-gradient(135deg, #667eea15 0%, #764ba215 100%);
            padding: 20px;
            border-radius: 12px;
            margin: 20px 0;
        }

        .progress-bar {
            background: #e0e0e0;
            border-radius: 10px;
            overflow: hidden;
            height: 30px;
            margin: 10px 0;
        }

        .progress-fill {
            background: linear-gradient(90deg, #28a745, #20c997);
            height: 100%;
            color: white;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 0.9em;
            font-weight: bold;
            transition: width 0.5s;
        }

        .progress-fill.warning {
            background: linear-gradient(90deg, #ffc107, #fd7e14);
        }

        .progress-fill.danger {
            background: linear-gradient(90deg, #dc3545, #c82333);
        }

        /* AI Assistant */
        .ai-assistant {
            background: linear-gradient(135deg, #e0c3fc 0%, #8ec5fc 100%);
            border-radius: 15px;
            padding: 20px;
            margin-bottom: 20px;
        }

        .chat-message {
            margin: 10px 0;
            padding: 10px;
            border-radius: 10px;
        }

        .user-msg {
            background: #667eea;
            color: white;
            text-align: right;
        }

        .ai-msg {
            background: white;
            color: #333;
        }

        /* Alert */
        .alert {
            position: fixed;
            top: 20px;
            right: 20px;
            padding: 12px 20px;
            border-radius: 8px;
            z-index: 1000;
            animation: slideIn 0.3s;
            max-width: 400px;
        }

        .alert.success { background: #d4edda; color: #155724; border-left: 4px solid #28a745; }
        .alert.error { background: #f8d7da; color: #721c24; border-left: 4px solid #dc3545; }

        @keyframes slideIn {
            from { transform: translateX(100%); opacity: 0; }
            to { transform: translateX(0); opacity: 1; }
        }

        table {
            width: 100%;
            border-collapse: collapse;
            margin-top: 15px;
        }

        th, td {
            border: 1px solid #ddd;
            padding: 10px;
            text-align: left;
        }

        th {
            background: #667eea;
            color: white;
        }

        .delete-btn {
            background: #dc3545;
            padding: 5px 10px;
            font-size: 0.8em;
        }
    </style>
</head>
<body>
    <div class="container">
        <div class="header">
            <h1>🤖 AI-Powered Project Management System</h1>
            <p>Activities | Indicators | Baseline | Excel Upload | AI Assistant | Budget Monitor | Staff & Expenses</p>
        </div>

        <div class="stats-bar" id="statsBar">
            <div class="stat-card"><div class="stat-number" id="totalProjects">0</div><div>Projects</div></div>
            <div class="stat-card"><div class="stat-number" id="totalBudget">$0</div><div>Total Budget</div></div>
            <div class="stat-card"><div class="stat-number" id="totalExpenses">$0</div><div>Total Expenses</div></div>
            <div class="stat-card"><div class="stat-number" id="budgetUtilization">0%</div><div>Utilization</div></div>
        </div>

        <div class="tabs">
            <button class="tab-btn active" onclick="switchTab('dashboard')">📊 Dashboard</button>
            <button class="tab-btn" onclick="switchTab('project')">📁 Projects & Activities</button>
            <button class="tab-btn" onclick="switchTab('staff')">👥 Staff</button>
            <button class="tab-btn" onclick="switchTab('expenses')">💰 Expenses</button>
            <button class="tab-btn" onclick="switchTab('budget')">📈 Budget Monitor</button>
            <button class="tab-btn" onclick="switchTab('excel')">📊 Excel Upload</button>
            <button class="tab-btn" onclick="switchTab('ai')">🤖 AI Assistant</button>
        </div>

        <!-- Dashboard Tab -->
        <div id="dashboardTab" class="tab-content active">
            <h2>📊 Executive Dashboard</h2>
            <canvas id="budgetChart" style="max-height: 300px; margin: 20px 0;"></canvas>
            <div id="dashboardInsights"></div>
        </div>

        <!-- Projects & Activities Tab -->
        <div id="projectTab" class="tab-content">
            <h2>📁 Register Project with Activities, Indicators & Baseline</h2>
            <form id="projectForm">
                <div class="form-group"><label>Project Name</label><input type="text" id="projName" required></div>
                <div class="form-group"><label>Project ID</label><input type="text" id="projId" required></div>
                <div class="form-group"><label>Total Budget</label><input type="number" id="projBudget" required></div>
                <div class="form-group"><label>Activities (comma separated)</label><input type="text" id="activities" placeholder="e.g., Training, Infrastructure, Monitoring"></div>
                <div class="form-group"><label>Indicators (comma separated)</label><input type="text" id="indicators" placeholder="e.g., # trained, km built"></div>
                <div class="form-group"><label>Baseline Values (comma separated)</label><input type="text" id="baseline" placeholder="e.g., 0, 0"></div>
                <button type="submit">➕ Register Project</button>
            </form>
            <hr>
            <div id="projectsList"></div>
        </div>

        <!-- Staff Tab -->
        <div id="staffTab" class="tab-content">
            <h2>👥 Register Project Staff</h2>
            <form id="staffForm">
                <div class="form-group"><label>Select Project</label><select id="staffProject" required></select></div>
                <div class="form-group"><label>Staff Name</label><input type="text" id="staffName" required></div>
                <div class="form-group"><label>Role</label><input type="text" id="staffRole" required></div>
                <div class="form-group"><label>Monthly Salary</label><input type="number" id="staffSalary" required></div>
                <button type="submit">➕ Add Staff</button>
            </form>
            <div id="staffList"></div>
        </div>

        <!-- Expenses Tab -->
        <div id="expensesTab" class="tab-content">
            <h2>💰 Record Project Expenses (Auto-feeds to Budget Monitor)</h2>
            <form id="expenseForm">
                <div class="form-group"><label>Select Project</label><select id="expenseProject" required></select></div>
                <div class="form-group"><label>Expense Category</label><input type="text" id="expenseCat" required></div>
                <div class="form-group"><label>Amount</label><input type="number" id="expenseAmount" required></div>
                <div class="form-group"><label>Description</label><input type="text" id="expenseDesc"></div>
                <button type="submit">➕ Record Expense</button>
            </form>
            <div id="expensesList"></div>
        </div>

        <!-- Budget Monitor Tab -->
        <div id="budgetTab" class="tab-content">
            <h2>📈 Budget Monitoring (Interlinked & Auto-feeding)</h2>
            <div id="budgetMonitor"></div>
        </div>

        <!-- Excel Upload Tab -->
        <div id="excelTab" class="tab-content">
            <h2>📊 Upload Excel Sheet (Projects, Activities, Indicators, Baseline)</h2>
            <input type="file" id="excelUpload" accept=".xlsx, .xls">
            <button onclick="uploadExcel()">Upload & Import</button>
            <div id="excelPreview"></div>
        </div>

        <!-- AI Assistant Tab -->
        <div id="aiTab" class="tab-content">
            <h2>🤖 AI Assistant - Learn, Adapt & Recommend</h2>
            <div class="ai-assistant">
                <div id="chatHistory"></div>
                <div class="form-group"><input type="text" id="aiQuestion" placeholder="Ask me anything about your projects..."></div>
                <button onclick="askAI()">Ask AI</button>
                <button onclick="learnFromData()">📚 Learn from Project Data</button>
                <button onclick="generateRecommendations()">💡 Generate Recommendations</button>
            </div>
        </div>
    </div>

    <script>
        // Data Structure
        let appData = {
            projects: {},
            staff: {},
            expenses: {}
        };

        // Load/Save
        function loadData() {
            const saved = localStorage.getItem('aiProjectManager');
            if (saved) appData = JSON.parse(saved);
            else initDemoData();
            refreshAll();
        }

        function initDemoData() {
            appData = {
                projects: {
                    "PRJ001": {
                        id: "PRJ001", name: "Rural Education Initiative", budget: 100000,
                        activities: ["Teacher Training", "School Renovation", "Materials Supply"],
                        indicators: ["Trained Teachers", "Renovated Schools", "Students Reached"],
                        baseline: [0, 0, 0], current: [15, 3, 450], expenses: 45000
                    },
                    "PRJ002": {
                        id: "PRJ002", name: "Health Clinic Support", budget: 75000,
                        activities: ["Equipment Purchase", "Staff Training", "Outreach"],
                        indicators: ["Equipment Units", "Trained Nurses", "Patients Served"],
                        baseline: [0, 0, 100], current: [8, 12, 850], expenses: 32000
                    }
                },
                staff: { "PRJ001": [], "PRJ002": [] },
                expenses: { "PRJ001": [], "PRJ002": [] }
            };
            saveData();
        }

        function saveData() {
            localStorage.setItem('aiProjectManager', JSON.stringify(appData));
            updateStats();
        }

        function updateStats() {
            const projCount = Object.keys(appData.projects).length;
            let totalBudget = 0, totalExpenses = 0;
            for (let id in appData.projects) {
                totalBudget += appData.projects[id].budget;
                totalExpenses += appData.projects[id].expenses || 0;
            }
            document.getElementById('totalProjects').innerText = projCount;
            document.getElementById('totalBudget').innerText = '$' + totalBudget.toLocaleString();
            document.getElementById('totalExpenses').innerText = '$' + totalExpenses.toLocaleString();
            const utilization = totalBudget ? ((totalExpenses / totalBudget) * 100).toFixed(1) : 0;
            document.getElementById('budgetUtilization').innerText = utilization + '%';
            drawChart();
        }

        // Register Project with Activities, Indicators, Baseline
        document.getElementById('projectForm')?.addEventListener('submit', (e) => {
            e.preventDefault();
            const id = document.getElementById('projId').value.trim().toUpperCase();
            if (appData.projects[id]) { showAlert('Project exists!', 'error'); return; }
            const activities = document.getElementById('activities').value.split(',').map(s=>s.trim());
            const indicators = document.getElementById('indicators').value.split(',').map(s=>s.trim());
            const baseline = document.getElementById('baseline').value.split(',').map(s=>parseFloat(s.trim()));
            appData.projects[id] = {
                id, name: document.getElementById('projName').value,
                budget: parseFloat(document.getElementById('projBudget').value),
                activities, indicators, baseline,
                current: [...baseline], expenses: 0
            };
            appData.staff[id] = [];
            appData.expenses[id] = [];
            saveData();
            showAlert('Project registered with activities & indicators!');
            refreshAll();
        });

        // Staff Registration
        document.getElementById('staffForm')?.addEventListener('submit', (e) => {
            e.preventDefault();
            const pid = document.getElementById('staffProject').value;
            const staff = { name: document.getElementById('staffName').value, role: document.getElementById('staffRole').value, salary: parseFloat(document.getElementById('staffSalary').value) };
            if (!appData.staff[pid]) appData.staff[pid] = [];
            appData.staff[pid].push(staff);
            saveData();
            showAlert('Staff added!');
            refreshAll();
        });

        // Expenses (auto-feeds to budget monitor)
        document.getElementById('expenseForm')?.addEventListener('submit', (e) => {
            e.preventDefault();
            const pid = document.getElementById('expenseProject').value;
            const amount = parseFloat(document.getElementById('expenseAmount').value);
            const expense = {
                category: document.getElementById('expenseCat').value,
                amount: amount,
                description: document.getElementById('expenseDesc').value,
                date: new Date().toISOString()
            };
            if (!appData.expenses[pid]) appData.expenses[pid] = [];
            appData.expenses[pid].push(expense);
            appData.projects[pid].expenses = (appData.projects[pid].expenses || 0) + amount;
            saveData();
            showAlert(`Expense recorded: $${amount} (Auto-updated budget monitor)`);
            refreshAll();
        });

        // Excel Upload
        function uploadExcel() {
            const file = document.getElementById('excelUpload').files[0];
            if (!file) { showAlert('Select Excel file', 'error'); return; }
            const reader = new FileReader();
            reader.onload = function(e) {
                const data = new Uint8Array(e.target.result);
                const workbook = XLSX.read(data, { type: 'array' });
                const sheet = workbook.Sheets[workbook.SheetNames[0]];
                const rows = XLSX.utils.sheet_to_json(sheet);
                rows.forEach(row => {
                    if (row['Project ID'] && row['Project Name']) {
                        const id = row['Project ID'].toString().toUpperCase();
                        appData.projects[id] = {
                            id, name: row['Project Name'],
                            budget: parseFloat(row['Budget'] || 0),
                            activities: row['Activities'] ? row['Activities'].split(',') : [],
                            indicators: row['Indicators'] ? row['Indicators'].split(',') : [],
                            baseline: row['Baseline'] ? row['Baseline'].split(',').map(Number) : [],
                            current: row['Baseline'] ? row['Baseline'].split(',').map(Number) : [],
                            expenses: 0
                        };
                        if (!appData.staff[id]) appData.staff[id] = [];
                        if (!appData.expenses[id]) appData.expenses[id] = [];
                    }
                });
                saveData();
                showAlert('Excel data imported successfully!');
                refreshAll();
            };
            reader.readAsArrayBuffer(file);
        }

        // AI Assistant - Learning & Adaptation
        function askAI() {
            const question = document.getElementById('aiQuestion').value;
            if (!question) return;
            addChatMessage(question, 'user');
            const response = generateAIResponse(question);
            addChatMessage(response, 'ai');
            document.getElementById('aiQuestion').value = '';
        }

        function generateAIResponse(question) {
            const q = question.toLowerCase();
            const totalBudget = Object.values(appData.projects).reduce((s,p)=>s+p.budget,0);
            const totalExp = Object.values(appData.projects).reduce((s,p)=>s+(p.expenses||0),0);
            if (q.includes('budget')) return `💰 Total Budget: $${totalBudget.toLocaleString()} | Expenses: $${totalExp.toLocaleString()} | Utilization: ${((totalExp/totalBudget)*100).toFixed(1)}%`;
            if (q.includes('project')) return `📁 Active Projects: ${Object.keys(appData.projects).join(', ')}`;
            if (q.includes('indicator')) return `📊 Top indicators: ${Object.values(appData.projects).flatMap(p=>p.indicators).slice(0,5).join(', ')}`;
            if (q.includes('learn')) return learnFromDataText();
            return `I see ${Object.keys(appData.projects).length} projects. Ask about budget, indicators, activities, or recommendations.`;
        }

        function learnFromDataText() {
            let insights = "🧠 AI Learning from your data:\n";
            for (let id in appData.projects) {
                const p = appData.projects[id];
                const progress = ((p.expenses||0)/p.budget)*100;
                insights += `• ${p.name}: ${progress.toFixed(1)}% budget used. `;
                if (progress > 80) insights += "⚠️ Near overspending. ";
                else if (progress < 30) insights += "📉 Low utilization. ";
                insights += "\n";
            }
            return insights;
        }

        function learnFromData() { addChatMessage(learnFromDataText(), 'ai'); }
        
        function generateRecommendations() {
            let recs = "💡 AI Recommendations:\n";
            for (let id in appData.projects) {
                const p = appData.projects[id];
                const used = ((p.expenses||0)/p.budget)*100;
                if (used > 85) recs += `• ${p.name}: ⚠️ Reduce expenses or request budget revision.\n`;
                else if (used < 20 && p.expenses>0) recs += `• ${p.name}: 🔄 Increase activity implementation to utilize budget.\n`;
                else recs += `• ${p.name}: ✅ On track. Focus on indicator achievement: ${p.indicators[0]}.\n`;
            }
            addChatMessage(recs, 'ai');
        }

        function addChatMessage(msg, sender) {
            const chatDiv = document.getElementById('chatHistory');
            chatDiv.innerHTML += `<div class="chat-message ${sender}-msg">${sender==='user'?'👤 You':'🤖 AI'}: ${msg}</div>`;
            chatDiv.scrollTop = chatDiv.scrollHeight;
        }

        // Budget Monitor Display (Interlinked)
        function displayBudgetMonitor() {
            const container = document.getElementById('budgetMonitor');
            let html = '<div class="cards-grid">';
            for (let id in appData.projects) {
                const p = appData.projects[id];
                const spent = p.expenses || 0;
                const remaining = p.budget - spent;
                const percent = (spent / p.budget) * 100;
                let progressClass = 'progress-fill';
                if (percent > 90) progressClass += ' danger';
                else if (percent > 75) progressClass += ' warning';
                html += `<div class="card"><h3>${p.name}</h3>
                    <p>💰 Budget: $${p.budget.toLocaleString()}</p>
                    <p>💸 Expenses: $${spent.toLocaleString()}</p>
                    <p>✅ Remaining: $${remaining.toLocaleString()}</p>
                    <div class="progress-bar"><div class="${progressClass}" style="width:${percent}%">${percent.toFixed(1)}%</div></div>
                    <p>📊 Activities: ${p.activities.join(', ')}</p>
                    <p>🎯 Indicators: ${p.indicators.join(', ')}</p>
                    <p>📈 Baseline → Current: ${p.baseline.map((b,i)=>`${b}→${p.current[i]||b}`).join(', ')}</p>
                </div>`;
            }
            container.innerHTML = html + '</div>';
        }

        // Display Projects
        function displayProjects() {
            const container = document.getElementById('projectsList');
            let html = '<div class="cards-grid">';
            for (let id in appData.projects) {
                const p = appData.projects[id];
                html += `<div class="card"><h3>${p.name}</h3><p>ID: ${p.id}</p><p>Budget: $${p.budget}</p>
                    <p>🎯 Activities: ${p.activities.join(', ')}</p><p>📊 Indicators: ${p.indicators.join(', ')}</p>
                    <p>📉 Baseline: ${p.baseline.join(', ')}</p><button onclick="updateProgress('${id}')">Update Progress</button></div>`;
            }
            container.innerHTML = html + '</div>';
        }

        function updateProgress(pid) {
            const newVal = prompt('Enter new progress values (comma separated)');
            if (newVal) {
                appData.projects[pid].current = newVal.split(',').map(Number);
                saveData();
                refreshAll();
            }
        }

        function displayStaff() {
            const container = document.getElementById('staffList');
            let html = '';
            for (let pid in appData.staff) {
                if (appData.staff[pid].length) {
                    html += `<h3>${appData.projects[pid]?.name || pid}</h3><table><tr><th>Name</th><th>Role</th><th>Salary</th></tr>`;
                    appData.staff[pid].forEach(s => html += `<tr><td>${s.name}</td><td>${s.role}</td><td>$${s.salary}</td></tr>`);
                    html += `</table>`;
                }
            }
            container.innerHTML = html || '<p>No staff registered</p>';
        }

        function displayExpenses() {
            const container = document.getElementById('expensesList');
            let html = '';
            for (let pid in appData.expenses) {
                if (appData.expenses[pid].length) {
                    html += `<h3>${appData.projects[pid]?.name || pid}</h3><table><tr><th>Category</th><th>Amount</th><th>Description</th><th>Date</th></tr>`;
                    appData.expenses[pid].forEach(e => html += `<tr><td>${e.category}</td><td>$${e.amount}</td><td>${e.description}</td><td>${new Date(e.date).toLocaleDateString()}</td></tr>`);
                    html += `</table>`;
                }
            }
            container.innerHTML = html || '<p>No expenses recorded</p>';
        }

        function drawChart() {
            const ctx = document.getElementById('budgetChart')?.getContext('2d');
            if (!ctx) return;
            if (window.budgetChart) window.budgetChart.destroy();
            const labels = Object.values(appData.projects).map(p=>p.name);
            const budgetData = Object.values(appData.projects).map(p=>p.budget);
            const expenseData = Object.values(appData.projects).map(p=>p.expenses||0);
            window.budgetChart = new Chart(ctx, { type: 'bar', data: { labels, datasets: [
                { label: 'Budget', data: budgetData, backgroundColor: '#667eea' },
                { label: 'Expenses', data: expenseData, backgroundColor: '#28a745' }
            ]}, options: { responsive: true } });
        }

        function displayDashboardInsights() {
            const container = document.getElementById('dashboardInsights');
            let insights = '<div class="cards-grid">';
            for (let id in appData.projects) {
                const p = appData.projects[id];
                const percent = ((p.expenses||0)/p.budget)*100;
                insights += `<div class="card"><h3>${p.name}</h3><p>📊 Budget Used: ${percent.toFixed(1)}%</p>
                    <p>🎯 Top Indicator: ${p.indicators[0]}</p><p>📈 Progress: ${p.current[0] || 0} / ${p.baseline[0] || 100}</p></div>`;
            }
            container.innerHTML = insights + '</div>';
        }

        function populateDropdowns() {
            const selects = ['staffProject', 'expenseProject'];
            selects.forEach(selId => {
                const sel = document.getElementById(selId);
                if (sel) {
                    sel.innerHTML = '';
                    for (let id in appData.projects) {
                        sel.innerHTML += `<option value="${id}">${appData.projects[id].name}</option>`;
                    }
                }
            });
        }

        function refreshAll() {
            populateDropdowns();
            displayProjects();
            displayStaff();
            displayExpenses();
            displayBudgetMonitor();
            displayDashboardInsights();
            updateStats();
        }

        function switchTab(tabName) {
            const tabs = ['dashboard', 'project', 'staff', 'expenses', 'budget', 'excel', 'ai'];
            tabs.forEach(t => {
                const el = document.getElementById(`${t}Tab`);
                const btn = document.querySelector(`.tab-btn[onclick="switchTab('${t}')"]`);
                if (el && btn) {
                    if (t === tabName) { el.classList.add('active'); btn.classList.add('active'); }
                    else { el.classList.remove('active'); btn.classList.remove('active'); }
                }
            });
            if (tabName === 'dashboard') displayDashboardInsights();
            if (tabName === 'budget') displayBudgetMonitor();
        }

        function showAlert(msg, type='success') {
            const alert = document.createElement('div');
            alert.className = `alert ${type}`;
            alert.innerText = msg;
            document.body.appendChild(alert);
            setTimeout(() => alert.remove(), 3000);
        }

        window.switchTab = switchTab;
        window.uploadExcel = uploadExcel;
        window.askAI = askAI;
        window.learnFromData = learnFromData;
        window.generateRecommendations = generateRecommendations;
        window.updateProgress = updateProgress;

        loadData();
    </script>
</body>
</html>
