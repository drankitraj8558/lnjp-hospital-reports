# lnjp-hospital-reports
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>LNJP Hospital • Lab Report Hub</title>
  
  <!-- Google Fonts: Inter -->
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700&display=swap" rel="stylesheet">
  
  <!-- FontAwesome Icons -->
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">

  <style>
    :root {
      --primary: #0284c7;
      --primary-hover: #0369a1;
      --primary-light: #e0f2fe;
      --bg: #f8fafc;
      --surface: #ffffff;
      --surface-border: #e2e8f0;
      --text-main: #0f172a;
      --text-muted: #64748b;
      --success: #10b981;
      --warning: #f59e0b;
      --danger: #ef4444;
      --radius: 12px;
      --shadow: 0 4px 6px -1px rgb(0 0 0 / 0.07), 0 2px 4px -2px rgb(0 0 0 / 0.05);
    }

    [data-theme="dark"] {
      --primary: #38bdf8;
      --primary-hover: #0ea5e9;
      --primary-light: #1e293b;
      --bg: #0b0f19;
      --surface: #111827;
      --surface-border: #1f2937;
      --text-main: #f8fafc;
      --text-muted: #94a3b8;
      --shadow: 0 4px 10px rgb(0 0 0 / 0.3);
    }

    * { box-sizing: border-box; margin: 0; padding: 0; font-family: 'Inter', sans-serif; transition: background-color 0.2s ease, border-color 0.2s ease; }
    body { background-color: var(--bg); color: var(--text-main); padding-bottom: 60px; }

    /* Top Navbar */
    header {
      background: var(--surface);
      border-bottom: 1px solid var(--surface-border);
      position: sticky;
      top: 0;
      z-index: 50;
      box-shadow: var(--shadow);
    }
    .nav-container {
      max-width: 1000px;
      margin: 0 auto;
      padding: 12px 16px;
      display: flex;
      justify-content: space-between;
      align-items: center;
    }
    .brand {
      display: flex;
      align-items: center;
      gap: 10px;
      font-weight: 700;
      font-size: 1.15rem;
      color: var(--primary);
    }
    .theme-toggle {
      background: none;
      border: 1px solid var(--surface-border);
      color: var(--text-main);
      padding: 8px 12px;
      border-radius: 8px;
      cursor: pointer;
      font-size: 14px;
    }

    /* Main Container & Tabs */
    .container { max-width: 1000px; margin: 20px auto; padding: 0 16px; }
    
    .tab-bar {
      display: flex;
      background: var(--surface);
      border: 1px solid var(--surface-border);
      padding: 4px;
      border-radius: 10px;
      margin-bottom: 20px;
      gap: 4px;
    }
    .tab-btn {
      flex: 1;
      padding: 10px 14px;
      border: none;
      background: none;
      font-weight: 600;
      font-size: 14px;
      color: var(--text-muted);
      border-radius: 8px;
      cursor: pointer;
      display: flex;
      align-items: center;
      justify-content: center;
      gap: 8px;
    }
    .tab-btn.active {
      background: var(--primary);
      color: #ffffff;
      box-shadow: 0 2px 4px rgba(0,0,0,0.1);
    }

    /* Card Panels */
    .panel { display: none; }
    .panel.active { display: block; }

    .card {
      background: var(--surface);
      border: 1px solid var(--surface-border);
      border-radius: var(--radius);
      padding: 20px;
      margin-bottom: 20px;
      box-shadow: var(--shadow);
    }
    .card-title {
      font-size: 1.1rem;
      font-weight: 600;
      margin-bottom: 15px;
      display: flex;
      align-items: center;
      gap: 8px;
      color: var(--primary);
    }

    /* Search Controls */
    .search-group {
      position: relative;
      margin-bottom: 12px;
    }
    .search-input {
      width: 100%;
      padding: 14px 14px 14px 44px;
      border-radius: 10px;
      border: 1px solid var(--surface-border);
      background: var(--bg);
      color: var(--text-main);
      font-size: 15px;
      outline: none;
    }
    .search-input:focus { border-color: var(--primary); }
    .search-icon {
      position: absolute;
      left: 15px;
      top: 50%;
      transform: translateY(-50%);
      color: var(--text-muted);
    }

    /* Filter Chips */
    .filter-section {
      display: flex;
      flex-direction: column;
      gap: 10px;
      margin-bottom: 15px;
    }
    .filter-chips {
      display: flex;
      gap: 6px;
      flex-wrap: wrap;
      align-items: center;
    }
    .chip {
      padding: 6px 12px;
      border-radius: 20px;
      font-size: 12px;
      font-weight: 600;
      background: var(--bg);
      border: 1px solid var(--surface-border);
      color: var(--text-muted);
      cursor: pointer;
      user-select: none;
    }
    .chip.active {
      background: var(--primary-light);
      color: var(--primary);
      border-color: var(--primary);
    }

    /* Action Buttons */
    .actions-row {
      display: flex;
      gap: 10px;
      justify-content: space-between;
      align-items: center;
      margin-bottom: 15px;
    }
    .btn-secondary {
      background: var(--bg);
      border: 1px solid var(--surface-border);
      color: var(--text-main);
      padding: 8px 14px;
      border-radius: 8px;
      cursor: pointer;
      font-size: 13px;
      font-weight: 600;
      display: inline-flex;
      align-items: center;
      gap: 6px;
    }
    .btn-secondary:hover { border-color: var(--primary); }

    /* Results Grid */
    .results-grid {
      display: grid;
      grid-template-columns: repeat(auto-fill, minmax(280px, 1fr));
      gap: 16px;
    }
    .result-card {
      background: var(--surface);
      border: 1px solid var(--surface-border);
      border-radius: var(--radius);
      padding: 14px;
      box-shadow: var(--shadow);
      display: flex;
      flex-direction: column;
      justify-content: space-between;
      gap: 10px;
    }
    .result-header {
      display: flex;
      justify-content: space-between;
      align-items: flex-start;
    }
    .badge {
      font-size: 11px;
      font-weight: 700;
      padding: 4px 8px;
      border-radius: 6px;
      text-transform: uppercase;
    }
    .badge-w1 { background: #dbeafe; color: #1e40af; }
    .badge-w2 { background: #fef3c7; color: #92400e; }
    
    .patient-name { font-size: 1.05rem; font-weight: 700; color: var(--text-main); }
    .meta-row { font-size: 13px; color: var(--text-muted); margin-top: 2px; }
    .meta-row span { color: var(--text-main); font-weight: 500; }

    .img-preview {
      width: 100%;
      height: 140px;
      object-fit: cover;
      border-radius: 8px;
      border: 1px solid var(--surface-border);
      cursor: pointer;
    }
    
    .card-actions {
      display: flex;
      gap: 8px;
      margin-top: 4px;
    }
    .btn-action {
      flex: 1;
      padding: 8px;
      border-radius: 6px;
      border: none;
      font-size: 12px;
      font-weight: 600;
      cursor: pointer;
      display: flex;
      align-items: center;
      justify-content: center;
      gap: 6px;
    }
    .btn-view { background: var(--primary-light); color: var(--primary); }
    .btn-wa { background: #dcfce7; color: #15803d; }

    /* Upload Desk Styling */
    .upload-zone {
      border: 2px dashed var(--primary);
      background: var(--bg);
      border-radius: var(--radius);
      padding: 30px 20px;
      text-align: center;
      cursor: pointer;
      margin-bottom: 15px;
    }
    .upload-zone:hover { background: var(--primary-light); }
    .upload-icon { font-size: 2.5rem; color: var(--primary); margin-bottom: 10px; }

    .preview-tray {
      display: flex;
      gap: 10px;
      overflow-x: auto;
      padding: 10px 0;
      margin-bottom: 15px;
    }
    .thumb-box {
      position: relative;
      flex-shrink: 0;
      width: 75px;
      height: 75px;
      border-radius: 8px;
      border: 1px solid var(--surface-border);
      overflow: hidden;
    }
    .thumb-box img { width: 100%; height: 100%; object-fit: cover; }
    .thumb-remove {
      position: absolute;
      top: 2px;
      right: 2px;
      background: rgba(239, 68, 68, 0.9);
      color: white;
      border: none;
      border-radius: 50%;
      width: 18px;
      height: 18px;
      font-size: 10px;
      cursor: pointer;
    }

    .btn-submit {
      width: 100%;
      background: var(--primary);
      color: white;
      padding: 14px;
      border: none;
      border-radius: 10px;
      font-size: 16px;
      font-weight: 700;
      cursor: pointer;
      display: flex;
      align-items: center;
      justify-content: center;
      gap: 10px;
    }
    .btn-submit:hover { background: var(--primary-hover); }

    /* Progress Bar */
    .progress-wrapper {
      margin-top: 15px;
      display: none;
    }
    .progress-bar-bg {
      background: var(--bg);
      border: 1px solid var(--surface-border);
      border-radius: 10px;
      height: 12px;
      overflow: hidden;
    }
    .progress-fill {
      background: var(--primary);
      height: 100%;
      width: 0%;
      transition: width 0.3s ease;
    }
    .progress-text {
      font-size: 12px;
      font-weight: 600;
      margin-top: 6px;
      color: var(--text-muted);
      text-align: center;
    }

    /* Lightbox Modal */
    .modal {
      display: none;
      position: fixed;
      inset: 0;
      background: rgba(0,0,0,0.85);
      z-index: 100;
      align-items: center;
      justify-content: center;
      padding: 15px;
    }
    .modal.active { display: flex; }
    .modal-content {
      position: relative;
      max-width: 90vw;
      max-height: 85vh;
      display: flex;
      flex-direction: column;
      align-items: center;
    }
    .modal-img-container {
      overflow: hidden;
      display: flex;
      align-items: center;
      justify-content: center;
    }
    .modal-img {
      max-width: 100%;
      max-height: 75vh;
      border-radius: 8px;
      transition: transform 0.2s ease;
    }
    .modal-toolbar {
      display: flex;
      gap: 10px;
      margin-top: 12px;
      background: rgba(255, 255, 255, 0.15);
      backdrop-filter: blur(8px);
      padding: 8px 16px;
      border-radius: 30px;
    }
    .tool-btn {
      background: none;
      border: none;
      color: white;
      font-size: 16px;
      cursor: pointer;
      padding: 6px 10px;
    }
    .modal-close {
      position: absolute;
      top: -35px;
      right: 0;
      color: white;
      font-size: 24px;
      cursor: pointer;
      background: none;
      border: none;
    }

    /* Skeleton Loading State */
    .skeleton {
      height: 180px;
      border-radius: var(--radius);
      background: linear-gradient(90deg, var(--surface-border) 25%, var(--bg) 50%, var(--surface-border) 75%);
      background-size: 200% 100%;
      animation: loading 1.5s infinite;
    }
    @keyframes loading {
      0% { background-position: 200% 0; }
      100% { background-position: -200% 0; }
    }
  </style>
</head>
<body>

  <!-- Top Navigation -->
  <header>
    <div class="nav-container">
      <div class="brand">
        <i class="fa-solid fa-hospital-user"></i>
        <span>LNJP ReportHub</span>
      </div>
      <button class="theme-toggle" onclick="toggleTheme()">
        <i class="fa-solid fa-moon" id="themeIcon"></i>
      </button>
    </div>
  </header>

  <div class="container">
    
    <!-- Tab Navigation -->
    <div class="tab-bar">
      <button class="tab-btn active" onclick="switchTab('search')">
        <i class="fa-solid fa-magnifying-glass"></i> Search Directory
      </button>
      <button class="tab-btn" onclick="switchTab('upload')">
        <i class="fa-solid fa-camera"></i> Intern Upload Desk
      </button>
    </div>

    <!-- TAB 1: Search & Directory -->
    <div id="tab-search" class="panel active">
      <div class="card">
        
        <!-- Live Search Bar -->
        <div class="search-group">
          <i class="fa-solid fa-search search-icon"></i>
          <input type="text" id="liveSearchInput" class="search-input" placeholder="Type Patient Name, CR No., or Department (e.g. Med EM)..." oninput="applyFilters()">
        </div>

        <!-- Filter Chips Section -->
        <div class="filter-section">
          
          <!-- Window Filter -->
          <div class="filter-chips" id="windowChips">
            <span style="font-size: 12px; font-weight: bold; color: var(--text-muted);">Window:</span>
            <div class="chip active" onclick="setWindowFilter('ALL', this)">All Windows</div>
            <div class="chip" onclick="setWindowFilter('Window 1', this)">Window 1 (CBC)</div>
            <div class="chip" onclick="setWindowFilter('Window 2', this)">Window 2 (Immunoassay)</div>
          </div>

          <!-- Department Filter -->
          <div class="filter-chips" id="deptChips">
            <span style="font-size: 12px; font-weight: bold; color: var(--text-muted);">Department:</span>
            <div class="chip active" onclick="setDeptFilter('ALL', this)">All Depts</div>
            <div class="chip" onclick="setDeptFilter('Med EM', this)">Med EM</div>
            <div class="chip" onclick="setDeptFilter('Sx EM', this)">Sx EM</div>
            <div class="chip" onclick="setDeptFilter('PICU', this)">PICU</div>
            <div class="chip" onclick="setDeptFilter('CLR', this)">CLR</div>
            <div class="chip" onclick="setDeptFilter('W14', this)">W14</div>
            <div class="chip" onclick="setDeptFilter('Ortho EM', this)">Ortho EM</div>
          </div>

        </div>

        <!-- Header Actions -->
        <div class="actions-row">
          <span id="resultsCount" style="font-size: 13px; font-weight: 600; color: var(--text-muted);">Loading database...</span>
          <div style="display: flex; gap: 8px;">
            <button class="btn-secondary" onclick="fetchDatabase(true)"><i class="fa-solid fa-rotate"></i> Sync Data</button>
            <button class="btn-secondary" onclick="exportToCSV()"><i class="fa-solid fa-file-csv"></i> Export CSV</button>
          </div>
        </div>

        <!-- Results Display Grid -->
        <div class="results-grid" id="resultsGrid">
          <div class="skeleton"></div>
          <div class="skeleton"></div>
          <div class="skeleton"></div>
        </div>

      </div>
    </div>

    <!-- TAB 2: Intern Upload Desk -->
    <div id="tab-upload" class="panel">
      <div class="card">
        <div class="card-title">
          <i class="fa-solid fa-cloud-arrow-up"></i>
          <span>Upload New Lab Sheet Photos</span>
        </div>

        <label style="font-size: 13px; font-weight: 600; margin-bottom: 6px; display: block;">Select Target Window:</label>
        <select id="uploadWindowType" class="search-input" style="padding: 10px; margin-bottom: 15px;">
          <option value="Window 1">Window 1 (CBC / Hematology Sheet)</option>
          <option value="Window 2">Window 2 (Immunoassay / Hormone Markers)</option>
        </select>

        <!-- Drag & Drop / Click Zone -->
        <div class="upload-zone" onclick="document.getElementById('fileChooser').click()">
          <i class="fa-solid fa-camera-retro upload-icon"></i>
          <p style="font-weight: 600; font-size: 15px;">Click to Snap Photo or Select from Gallery</p>
          <p style="font-size: 12px; color: var(--text-muted); margin-top: 4px;">Supports multi-page batch upload (Up to 30 sheets)</p>
          <input type="file" id="fileChooser" accept="image/*" multiple style="display: none;" onchange="handleFileSelection(event)">
        </div>

        <!-- Selected Thumbnails Preview -->
        <div class="preview-tray" id="previewTray"></div>

        <button class="btn-submit" id="btnUpload" onclick="startBatchUpload()">
          <i class="fa-solid fa-microchip-ai"></i> Upload & Process with AI
        </button>

        <!-- Progress Bar -->
        <div class="progress-wrapper" id="progressWrapper">
          <div class="progress-bar-bg">
            <div class="progress-fill" id="progressFill"></div>
          </div>
          <p class="progress-text" id="progressText">Processing photos...</p>
        </div>

      </div>
    </div>

  </div>

  <!-- In-App Image Lightbox Modal -->
  <div class="modal" id="imageModal">
    <div class="modal-content">
      <button class="modal-close" onclick="closeModal()"><i class="fa-solid fa-xmark"></i></button>
      <div class="modal-img-container">
        <img src="" id="modalImage" class="modal-img">
      </div>
      <div class="modal-toolbar">
        <button class="tool-btn" title="Zoom In" onclick="zoomImage(0.2)"><i class="fa-solid fa-magnifying-glass-plus"></i></button>
        <button class="tool-btn" title="Zoom Out" onclick="zoomImage(-0.2)"><i class="fa-solid fa-magnifying-glass-minus"></i></button>
        <button class="tool-btn" title="Rotate" onclick="rotateImage()"><i class="fa-solid fa-rotate-right"></i></button>
        <button class="tool-btn" title="Reset" onclick="resetImageTransform()"><i class="fa-solid fa-arrows-rotate"></i></button>
        <a id="modalDownloadLink" class="tool-btn" target="_blank" title="Open Full Drive Image"><i class="fa-solid fa-up-right-from-square"></i></a>
      </div>
    </div>
  </div>

  <script>
    // YOUR LIVE GOOGLE APPS SCRIPT WEB APP URL:
    const SCRIPT_URL = "https://script.google.com/macros/s/AKfycbw9qjLCPhAXlJwDMas5ydr7_WfryVV78EUxr3mo3pb2-DW6sxRoH95FQUlWqfFyhdS6ng/exec";

    let rawRecords = [];
    let selectedFiles = [];
    let activeWindowFilter = "ALL";
    let activeDeptFilter = "ALL";
    let currentZoom = 1;
    let currentRotation = 0;

    // --- INIT ---
    window.addEventListener('DOMContentLoaded', () => {
      fetchDatabase();
    });

    // --- TAB SWITCHER ---
    function switchTab(tab) {
      document.querySelectorAll('.tab-btn').forEach(btn => btn.classList.remove('active'));
      document.querySelectorAll('.panel').forEach(p => p.classList.remove('active'));
      
      if (tab === 'search') {
        document.querySelectorAll('.tab-btn')[0].classList.add('active');
        document.getElementById('tab-search').classList.add('active');
      } else {
        document.querySelectorAll('.tab-btn')[1].classList.add('active');
        document.getElementById('tab-upload').classList.add('active');
      }
    }

    // --- DARK MODE TOGGLE ---
    function toggleTheme() {
      const isDark = document.body.getAttribute('data-theme') === 'dark';
      document.body.setAttribute('data-theme', isDark ? 'light' : 'dark');
      document.getElementById('themeIcon').className = isDark ? 'fa-solid fa-moon' : 'fa-solid fa-sun';
    }

    // --- FETCH & CACHE DATABASE ---
    async function fetchDatabase(manual = false) {
      const countLabel = document.getElementById('resultsCount');
      if (manual) countLabel.innerText = "Syncing from Google Sheet...";

      try {
        const response = await fetch(SCRIPT_URL);
        rawRecords = await response.json();
        applyFilters();
      } catch (err) {
        countLabel.innerText = "Failed to load database. Check connection.";
      }
    }

    // --- FILTER & RENDER ENGINE ---
    function setWindowFilter(win, element) {
      activeWindowFilter = win;
      document.querySelectorAll('#windowChips .chip').forEach(c => c.classList.remove('active'));
      element.classList.add('active');
      applyFilters();
    }

    function setDeptFilter(dept, element) {
      activeDeptFilter = dept;
      document.querySelectorAll('#deptChips .chip').forEach(c => c.classList.remove('active'));
      element.classList.add('active');
      applyFilters();
    }

    function applyFilters() {
      const query = document.getElementById('liveSearchInput').value.toLowerCase().trim();
      const grid = document.getElementById('resultsGrid');
      const countLabel = document.getElementById('resultsCount');

      const filtered = rawRecords.filter(row => {
        const [timestamp, windowType, name, crNo, dept, imgUrl] = row;
        
        const matchQuery = !query || 
          name.toString().toLowerCase().includes(query) ||
          crNo.toString().toLowerCase().includes(query) ||
          dept.toString().toLowerCase().includes(query);

        const matchWindow = (activeWindowFilter === 'ALL') || (windowType === activeWindowFilter);
        const matchDept = (activeDeptFilter === 'ALL') || (dept.toString().toLowerCase().includes(activeDeptFilter.toLowerCase()));

        return matchQuery && matchWindow && matchDept;
      });

      countLabel.innerText = `Showing ${filtered.length} matching report(s)`;
      grid.innerHTML = "";

      if (filtered.length === 0) {
        grid.innerHTML = `
          <div style="grid-column: 1/-1; text-align: center; padding: 40px 10px; color: var(--text-muted);">
            <i class="fa-regular fa-folder-open" style="font-size: 2rem; margin-bottom: 10px;"></i>
            <p>No matching patient records found.</p>
          </div>
        `;
        return;
      }

      filtered.reverse().forEach(row => {
        const [timestamp, windowType, name, crNo, dept, imgUrl] = row;
        const badgeClass = windowType === 'Window 1' ? 'badge-w1' : 'badge-w2';

        const card = document.createElement('div');
        card.className = 'result-card';
        card.innerHTML = `
          <div>
            <div class="result-header">
              <span class="patient-name">${name || 'Unknown Patient'}</span>
              <span class="badge ${badgeClass}">${windowType}</span>
            </div>
            <div class="meta-row">CR No: <span>${crNo || 'N/A'}</span></div>
            <div class="meta-row">Dept: <span>${dept || 'N/A'}</span></div>
            <div class="meta-row" style="font-size: 11px;">Logged: ${new Date(timestamp).toLocaleDateString()} ${new Date(timestamp).toLocaleTimeString([], {hour: '2-digit', minute:'2-digit'})}</div>
          </div>

          <img src="${imgUrl}" class="img-preview" alt="Lab Sheet" onclick="openModal('${imgUrl}')">

          <div class="card-actions">
            <button class="btn-action btn-view" onclick="openModal('${imgUrl}')">
              <i class="fa-solid fa-expand"></i> Inspect
            </button>
            <button class="btn-action btn-wa" onclick="shareWhatsApp('${name}', '${crNo}', '${dept}', '${imgUrl}')">
              <i class="fa-brands fa-whatsapp"></i> Share
            </button>
          </div>
        `;
        grid.appendChild(card);
      });
    }

    // --- LIGHTBOX CONTROLS ---
    function openModal(url) {
      const modal = document.getElementById('imageModal');
      const img = document.getElementById('modalImage');
      const dl = document.getElementById('modalDownloadLink');
      
      img.src = url;
      dl.href = url;
      resetImageTransform();
      modal.classList.add('active');
    }

    function closeModal() {
      document.getElementById('imageModal').classList.remove('active');
    }

    function zoomImage(factor) {
      currentZoom = Math.max(0.5, Math.min(currentZoom + factor, 4));
      updateImageTransform();
    }

    function rotateImage() {
      currentRotation = (currentRotation + 90) % 360;
      updateImageTransform();
    }

    function resetImageTransform() {
      currentZoom = 1;
      currentRotation = 0;
      updateImageTransform();
    }

    function updateImageTransform() {
      document.getElementById('modalImage').style.transform = `scale(${currentZoom}) rotate(${currentRotation}deg)`;
    }

    // --- WHATSAPP SHARE GENERATOR ---
    function shareWhatsApp(name, crNo, dept, imgUrl) {
      const text = encodeURIComponent(`*LNJP Hospital Lab Report*\n👤 *Patient:* ${name}\n🔢 *CR No:* ${crNo}\n🏥 *Dept:* ${dept}\n📄 *View Sheet:* ${imgUrl}`);
      window.open(`https://api.whatsapp.com/send?text=${text}`, '_blank');
    }

    // --- CSV EXPORTER ---
    function exportToCSV() {
      if (rawRecords.length === 0) return alert("No records to export!");
      let csvContent = "data:text/csv;charset=utf-8,Timestamp,Window,Name,CR_No,Dept,Image_URL\n";
      rawRecords.forEach(row => {
        csvContent += row.map(e => `"${e}"`).join(",") + "\n";
      });
      const encodedUri = encodeURI(csvContent);
      const link = document.createElement("a");
      link.setAttribute("href", encodedUri);
      link.setAttribute("download", `LNJP_Reports_${Date.now()}.csv`);
      document.body.appendChild(link);
      link.click();
      document.body.removeChild(link);
    }

    // --- CLIENT-SIDE IMAGE COMPRESSION (10x Faster Uploads) ---
    function compressImage(file) {
      return new Promise((resolve) => {
        const reader = new FileReader();
        reader.readAsDataURL(file);
        reader.onload = (event) => {
          const img = new Image();
          img.src = event.target.result;
          img.onload = () => {
            const canvas = document.createElement('canvas');
            const MAX_WIDTH = 1800;
            let width = img.width;
            let height = img.height;

            if (width > MAX_WIDTH) {
              height = Math.round((height * MAX_WIDTH) / width);
              width = MAX_WIDTH;
            }

            canvas.width = width;
            canvas.height = height;
            const ctx = canvas.getContext('2d');
            ctx.drawImage(img, 0, 0, width, height);

            // Compress to JPEG with 0.82 quality
            resolve(canvas.toDataURL('image/jpeg', 0.82));
          };
        };
      });
    }

    // --- FILE SELECTION & PREVIEWS ---
    function handleFileSelection(e) {
      const files = Array.from(e.target.files);
      selectedFiles = selectedFiles.concat(files).slice(0, 30);
      renderThumbnailTray();
    }

    function renderThumbnailTray() {
      const tray = document.getElementById('previewTray');
      tray.innerHTML = "";

      selectedFiles.forEach((file, index) => {
        const box = document.createElement('div');
        box.className = 'thumb-box';
        
        const img = document.createElement('img');
        img.src = URL.createObjectURL(file);

        const removeBtn = document.createElement('button');
        removeBtn.className = 'thumb-remove';
        removeBtn.innerHTML = '×';
        removeBtn.onclick = (e) => {
          e.stopPropagation();
          selectedFiles.splice(index, 1);
          renderThumbnailTray();
        };

        box.appendChild(img);
        box.appendChild(removeBtn);
        tray.appendChild(box);
      });
    }

    // --- BATCH UPLOAD WITH REAL-TIME PROGRESS BAR ---
    async function startBatchUpload() {
      if (selectedFiles.length === 0) {
        alert("Please select or capture photos first!");
        return;
      }

      const windowType = document.getElementById('uploadWindowType').value;
      const btn = document.getElementById('btnUpload');
      const progressWrapper = document.getElementById('progressWrapper');
      const progressFill = document.getElementById('progressFill');
      const progressText = document.getElementById('progressText');

      btn.disabled = true;
      btn.style.opacity = "0.6";
      progressWrapper.style.display = "block";

      let successCount = 0;

      for (let i = 0; i < selectedFiles.length; i++) {
        const percent = Math.round(((i) / selectedFiles.length) * 100);
        progressFill.style.width = `${percent}%`;
        progressText.innerText = `Compressing & AI Reading Sheet ${i + 1} of ${selectedFiles.length}...`;

        try {
          const base64Data = await compressImage(selectedFiles[i]);

          const response = await fetch(SCRIPT_URL, {
            method: "POST",
            body: JSON.stringify({ image: base64Data, window: windowType })
          });

          const data = await response.json();
          if (data.status === "success") successCount++;
        } catch (err) {
          console.error(`Sheet ${i + 1} failed:`, err);
        }
      }

      progressFill.style.width = "100%";
      progressText.innerText = `✅ Done! Successfully processed ${successCount} out of ${selectedFiles.length} sheets.`;

      // Reset
      selectedFiles = [];
      renderThumbnailTray();
      btn.disabled = false;
      btn.style.opacity = "1";

      // Refresh database in background
      setTimeout(() => {
        fetchDatabase();
        switchTab('search');
        progressWrapper.style.display = "none";
      }, 1500);
    }
  </script>
</body>
</html>
