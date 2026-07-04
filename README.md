<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=yes">
  <title>Focusullu · OTT</title>
  <!-- Font & Icons -->
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0-beta3/css/all.min.css">
  <!-- Firebase SDKs -->
  <script src="https://www.gstatic.com/firebasejs/10.7.1/firebase-app-compat.js"></script>
  <script src="https://www.gstatic.com/firebasejs/10.7.1/firebase-auth-compat.js"></script>
  <script src="https://www.gstatic.com/firebasejs/10.7.1/firebase-firestore-compat.js"></script>
  <script src="https://www.gstatic.com/firebasejs/10.7.1/firebase-storage-compat.js"></script>
  <style>
    * { margin: 0; padding: 0; box-sizing: border-box; font-family: 'Inter', system-ui, -apple-system, sans-serif; }
    body { background: #0b0e14; color: #f0f2f5; overflow-x: hidden; }
    /* scrollbar */
    ::-webkit-scrollbar { width: 6px; height: 6px; }
    ::-webkit-scrollbar-track { background: #1a1f2a; }
    ::-webkit-scrollbar-thumb { background: #4a5a72; border-radius: 12px; }

    /* dark premium theme */
    .app { max-width: 1440px; margin: 0 auto; padding: 0 20px 40px; }
    /* navbar */
    .navbar { display: flex; align-items: center; justify-content: space-between; padding: 18px 0; flex-wrap: wrap; gap: 12px; }
    .logo { font-size: 26px; font-weight: 700; letter-spacing: -0.5px; background: linear-gradient(135deg, #c0d0e0, #a0b8d0); -webkit-background-clip: text; -webkit-text-fill-color: transparent; }
    .logo i { margin-right: 6px; color: #b0c8e0; -webkit-text-fill-color: #b0c8e0; }
    .nav-links { display: flex; gap: 28px; font-weight: 500; font-size: 15px; }
    .nav-links a { color: #b0bccf; text-decoration: none; transition: 0.2s; }
    .nav-links a:hover, .nav-links a.active { color: #fff; }
    .nav-actions { display: flex; gap: 18px; align-items: center; }
    .nav-actions i { font-size: 20px; color: #b0bccf; cursor: pointer; transition: 0.2s; }
    .nav-actions i:hover { color: #fff; }
    .search-box { display: flex; background: #1e2532; border-radius: 30px; padding: 6px 16px; align-items: center; border: 1px solid #2d3645; }
    .search-box input { background: transparent; border: none; color: #fff; padding: 8px 6px; width: 160px; outline: none; font-size: 14px; }
    .search-box i { color: #6a7a92; }

    /* hero banner */
    .hero { background: linear-gradient(145deg, #141c28, #0e141e); border-radius: 32px; padding: 40px 40px 30px; margin: 20px 0 30px; box-shadow: 0 20px 40px -12px rgba(0,0,0,0.8); border: 1px solid #26303e; }
    .hero h1 { font-size: 3.2rem; font-weight: 700; max-width: 700px; line-height: 1.2; }
    .hero p { color: #b0c0d0; margin: 18px 0 22px; font-size: 1.1rem; max-width: 500px; }
    .hero-btn { background: #3a4c66; border: none; color: #fff; padding: 14px 36px; border-radius: 40px; font-weight: 600; font-size: 1rem; cursor: pointer; transition: 0.25s; box-shadow: 0 8px 18px rgba(0,20,40,0.6); }
    .hero-btn:hover { background: #4f6482; transform: scale(1.02); }

    /* section headers */
    .section-header { display: flex; justify-content: space-between; align-items: center; margin: 32px 0 14px; }
    .section-header h2 { font-weight: 600; font-size: 1.7rem; letter-spacing: -0.3px; }
    .section-header a { color: #7a8ca8; font-size: 0.95rem; text-decoration: none; }

    /* movie cards slider */
    .slider { display: flex; gap: 16px; overflow-x: auto; padding: 8px 2px 16px; scroll-snap-type: x mandatory; }
    .slider::-webkit-scrollbar { height: 4px; }
    .card { min-width: 180px; max-width: 200px; background: #151e28; border-radius: 20px; overflow: hidden; scroll-snap-align: start; transition: 0.2s; border: 1px solid #29323f; }
    .card:hover { transform: translateY(-6px); border-color: #4f6580; }
    .card img { width: 100%; height: 110px; object-fit: cover; background: #1f2836; }
    .card-body { padding: 12px 14px 16px; }
    .card-body h4 { font-size: 1rem; font-weight: 600; }
    .card-body p { font-size: 0.75rem; color: #8a9bb0; margin-top: 4px; }

    /* admin panel */
    .admin-panel { background: #131b24; border-radius: 28px; padding: 28px; margin: 40px 0 20px; border: 1px solid #26303e; }
    .admin-panel h3 { margin-bottom: 20px; font-weight: 500; }
    .admin-grid { display: flex; flex-wrap: wrap; gap: 18px; }
    .admin-grid input, .admin-grid select, .admin-grid textarea { background: #1e2734; border: 1px solid #314050; border-radius: 16px; padding: 12px 16px; color: #fff; font-size: 0.95rem; flex: 1 1 180px; outline: none; }
    .admin-grid textarea { flex: 1 1 300px; resize: vertical; }
    .admin-grid button { background: #3d5a78; border: none; color: #fff; padding: 12px 28px; border-radius: 40px; font-weight: 600; cursor: pointer; transition: 0.2s; }
    .admin-grid button:hover { background: #54739b; }

    /* profile cards */
    .profile-grid { display: flex; flex-wrap: wrap; gap: 24px; margin: 20px 0; }
    .profile-card { background: #151f2a; border-radius: 28px; padding: 24px; flex: 1 1 200px; border: 1px solid #2a3545; }
    .profile-card i { font-size: 2.2rem; color: #6e8aaa; }

    /* responsive */
    @media (max-width: 700px) {
      .navbar { flex-direction: column; align-items: stretch; }
      .nav-links { justify-content: center; flex-wrap: wrap; gap: 12px; }
      .search-box input { width: 100px; }
      .hero h1 { font-size: 2.2rem; }
      .admin-grid { flex-direction: column; }
    }
    @media (max-width: 480px) {
      .hero { padding: 24px; }
      .card { min-width: 140px; }
    }

    /* auth buttons */
    .auth-btn { background: #293544; border: none; color: #e0e8f0; padding: 8px 22px; border-radius: 40px; font-weight: 500; cursor: pointer; transition: 0.2s; }
    .auth-btn:hover { background: #3f546a; color: #fff; }

    .user-badge { display: flex; align-items: center; gap: 12px; }
    .user-badge i { font-size: 24px; color: #a0b8d0; }

    .hidden { display: none; }
    .mt-2 { margin-top: 12px; }
    .flex { display: flex; gap: 16px; flex-wrap: wrap; }
  </style>
</head>
<body>
<div class="app" id="app">
  <!-- Navigation -->
  <nav class="navbar">
    <div class="logo"><i class="fas fa-film"></i> Focusullu</div>
    <div class="nav-links">
      <a href="#" class="active" data-page="home">Home</a>
      <a href="#" data-page="movies">Movies</a>
      <a href="#" data-page="series">Series</a>
      <a href="#" data-page="categories">Categories</a>
    </div>
    <div class="nav-actions">
      <div class="search-box">
        <i class="fas fa-search"></i>
        <input type="text" id="globalSearch" placeholder="Search...">
      </div>
      <div id="authSection">
        <button class="auth-btn" id="loginBtn"><i class="fas fa-sign-in-alt"></i> Login</button>
        <button class="auth-btn" id="signupBtn"><i class="fas fa-user-plus"></i> Signup</button>
      </div>
      <div id="userSection" class="user-badge hidden">
        <i class="fas fa-user-circle"></i>
        <span id="userName">User</span>
        <button class="auth-btn" id="logoutBtn" style="background:#3a2a2a;">Logout</button>
      </div>
    </div>
  </nav>

  <!-- Page content -->
  <div id="pageContent">
    <!-- Home -->
    <div id="homePage">
      <div class="hero">
        <h1>Stream the best of <br>independent cinema</h1>
        <p>Focusullu · curated stories, premium quality. Watch trending movies, series & short films.</p>
        <button class="hero-btn" onclick="alert('Explore now →')"><i class="fas fa-play"></i> Start watching</button>
      </div>

      <div class="section-header"><h2>🔥 Trending Now</h2><a href="#">View all</a></div>
      <div class="slider" id="trendingSlider"></div>

      <div class="section-header"><h2>📺 Web Series</h2><a href="#">View all</a></div>
      <div class="slider" id="seriesSlider"></div>

      <div class="section-header"><h2>🎬 Short Films</h2><a href="#">View all</a></div>
      <div class="slider" id="shortSlider"></div>

      <!-- profile quick -->
      <div class="profile-grid">
        <div class="profile-card"><i class="fas fa-list"></i> <h4>Watchlist</h4><p>0 items</p></div>
        <div class="profile-card"><i class="fas fa-clock"></i> <h4>Continue Watching</h4><p>0</p></div>
        <div class="profile-card"><i class="fas fa-history"></i> <h4>History</h4><p>0</p></div>
      </div>
    </div>

    <!-- other pages placeholder: Movies, Series, Categories (dynamic) -->
    <div id="moviesPage" class="hidden"><h2 style="margin:30px 0;">🎥 Movies</h2><div class="slider" id="moviesSlider"></div></div>
    <div id="seriesPage" class="hidden"><h2 style="margin:30px 0;">📺 Series</h2><div class="slider" id="seriesPageSlider"></div></div>
    <div id="categoriesPage" class="hidden"><h2 style="margin:30px 0;">🏷️ Categories</h2><div id="categoriesList" style="display:flex;flex-wrap:wrap;gap:14px;"></div></div>

    <!-- Admin Dashboard -->
    <div id="adminPanel" class="admin-panel">
      <h3><i class="fas fa-crown"></i> Admin Dashboard · Upload</h3>
      <div class="admin-grid">
        <input type="text" id="videoTitle" placeholder="Title">
        <input type="text" id="videoCategory" placeholder="Category (e.g. Movie)">
        <input type="text" id="videoRelease" placeholder="Release date (YYYY)">
        <textarea id="videoDesc" placeholder="Description" rows="2"></textarea>
        <input type="file" id="videoFile" accept="video/*">
        <input type="file" id="thumbFile" accept="image/*">
        <button id="uploadBtn"><i class="fas fa-cloud-upload-alt"></i> Upload</button>
      </div>
      <div id="uploadStatus" style="margin-top:14px;color:#a0c0e0;"></div>
    </div>
  </div>
</div>

<!-- Auth modals (simple inline) -->
<div id="authModal" style="display:none;position:fixed;inset:0;background:rgba(0,0,0,0.7);backdrop-filter:blur(6px);z-index:999;justify-content:center;align-items:center;">
  <div style="background:#181f2a;padding:32px;border-radius:32px;max-width:400px;width:90%;border:1px solid #2e3b4a;">
    <h3 id="authModalTitle">Login</h3>
    <input id="authEmail" placeholder="Email" style="width:100%;padding:14px;margin:12px 0;background:#1e2836;border:1px solid #304050;border-radius:20px;color:#fff;">
    <input id="authPassword" placeholder="Password" type="password" style="width:100%;padding:14px;margin:12px 0;background:#1e2836;border:1px solid #304050;border-radius:20px;color:#fff;">
    <button id="authSubmitBtn" style="background:#3d5a78;border:none;padding:14px;border-radius:40px;color:#fff;font-weight:600;width:100%;cursor:pointer;">Sign in</button>
    <p style="margin-top:14px;text-align:center;color:#8a9bb0;"><span id="authToggleText">Don't have an account?</span> <a href="#" id="authToggleLink" style="color:#9ab8e0;">Sign up</a></p>
    <button id="closeAuthModal" style="background:transparent;border:1px solid #3a4a5a;padding:8px;border-radius:40px;color:#b0c0d0;margin-top:10px;width:100%;cursor:pointer;">Close</button>
  </div>
</div>

<script>
  // Firebase config (replace with your own)
  const firebaseConfig = {
    apiKey: "AIzaSyDummyKeyReplaceWithYourOwn",
    authDomain: "focusullu-12345.firebaseapp.com",
    projectId: "focusullu-12345",
    storageBucket: "focusullu-12345.appspot.com",
    messagingSenderId: "123456789012",
    appId: "1:123456789012:web:abcdef123456"
  };
  firebase.initializeApp(firebaseConfig);
  const auth = firebase.auth();
  const db = firebase.firestore();
  const storage = firebase.storage();

  // DOM refs
  const homePage = document.getElementById('homePage');
  const moviesPage = document.getElementById('moviesPage');
  const seriesPage = document.getElementById('seriesPage');
  const categoriesPage = document.getElementById('categoriesPage');
  const trendingSlider = document.getElementById('trendingSlider');
  const seriesSlider = document.getElementById('seriesSlider');
  const shortSlider = document.getElementById('shortSlider');
  const moviesSlider = document.getElementById('moviesSlider');
  const seriesPageSlider = document.getElementById('seriesPageSlider');
  const categoriesList = document.getElementById('categoriesList');

  const authSection = document.getElementById('authSection');
  const userSection = document.getElementById('userSection');
  const userName = document.getElementById('userName');
  const loginBtn = document.getElementById('loginBtn');
  const signupBtn = document.getElementById('signupBtn');
  const logoutBtn = document.getElementById('logoutBtn');

  const authModal = document.getElementById('authModal');
  const authModalTitle = document.getElementById('authModalTitle');
  const authEmail = document.getElementById('authEmail');
  const authPassword = document.getElementById('authPassword');
  const authSubmitBtn = document.getElementById('authSubmitBtn');
  const authToggleLink = document.getElementById('authToggleLink');
  const authToggleText = document.getElementById('authToggleText');
  const closeAuthModal = document.getElementById('closeAuthModal');

  let isLogin = true;

  // --- Helper: render cards from Firestore ---
  function renderCards(sliderEl, query, filterCategory = null) {
    if (!sliderEl) return;
    sliderEl.innerHTML = '<div style="color:#6a7a92;padding:20px;">Loading...</div>';
    db.collection('videos').where('approved', '==', true).get().then(snap => {
      let items = [];
      snap.forEach(doc => {
        const data = doc.data();
        if (filterCategory && data.category !== filterCategory) return;
        items.push(data);
      });
      if (items.length === 0) {
        sliderEl.innerHTML = `<div style="color:#6a7a92;padding:20px;">No content yet. Be the first to upload!</div>`;
        return;
      }
      sliderEl.innerHTML = items.map(item => `
        <div class="card">
          <img src="${item.thumbnail || 'https://placehold.co/300x180/1a2533/8a9bb0?text=Focusullu'}" alt="${item.title}">
          <div class="card-body">
            <h4>${item.title || 'Untitled'}</h4>
            <p>${item.category || 'General'} · ${item.release || '2025'}</p>
          </div>
        </div>
      `).join('');
    }).catch(e => { sliderEl.innerHTML = '<div>Error loading</div>'; });
  }

  // load all sections
  function loadAllContent() {
    renderCards(trendingSlider, db.collection('videos'), null);
    renderCards(seriesSlider, db.collection('videos'), 'Series');
    renderCards(shortSlider, db.collection('videos'), 'Short');
    renderCards(moviesSlider, db.collection('videos'), 'Movie');
    renderCards(seriesPageSlider, db.collection('videos'), 'Series');
    // categories
    db.collection('videos').get().then(snap => {
      const cats = new Set();
      snap.forEach(d => { if (d.data().category) cats.add(d.data().category); });
      categoriesList.innerHTML = Array.from(cats).map(c => `<span style="background:#1f2a38;padding:12px 28px;border-radius:40px;border:1px solid #314050;">#${c}</span>`).join('');
    });
  }

  // --- Navigation ---
  document.querySelectorAll('.nav-links a').forEach(link => {
    link.addEventListener('click', (e) => {
      e.preventDefault();
      document.querySelectorAll('.nav-links a').forEach(l => l.classList.remove('active'));
      link.classList.add('active');
      const page = link.dataset.page;
      homePage.classList.add('hidden');
      moviesPage.classList.add('hidden');
      seriesPage.classList.add('hidden');
      categoriesPage.classList.add('hidden');
      if (page === 'home') homePage.classList.remove('hidden');
      else if (page === 'movies') moviesPage.classList.remove('hidden');
      else if (page === 'series') seriesPage.classList.remove('hidden');
      else if (page === 'categories') categoriesPage.classList.remove('hidden');
    });
  });

  // --- Auth ---
  function updateUI(user) {
    if (user) {
      authSection.classList.add('hidden');
      userSection.classList.remove('hidden');
      userName.textContent = user.displayName || user.email || 'User';
    } else {
      authSection.classList.remove('hidden');
      userSection.classList.add('hidden');
    }
  }

  auth.onAuthStateChanged(user => {
    updateUI(user);
    if (user) loadAllContent();
  });

  loginBtn.addEventListener('click', () => { isLogin = true; showAuthModal('Login', 'Sign in', 'Don\'t have an account?', 'Sign up'); });
  signupBtn.addEventListener('click', () => { isLogin = false; showAuthModal('Signup', 'Create account', 'Already have an account?', 'Login'); });

  function showAuthModal(title, btnText, toggleText, toggleLinkText) {
    authModal.style.display = 'flex';
    authModalTitle.textContent = title;
    authSubmitBtn.textContent = btnText;
    authToggleText.textContent = toggleText;
    authToggleLink.textContent = toggleLinkText;
    authEmail.value = ''; authPassword.value = '';
  }

  closeAuthModal.addEventListener('click', () => authModal.style.display = 'none');
  authToggleLink.addEventListener('click', (e) => {
    e.preventDefault();
    isLogin = !isLogin;
    if (isLogin) showAuthModal('Login', 'Sign in', 'Don\'t have an account?', 'Sign up');
    else showAuthModal('Signup', 'Create account', 'Already have an account?', 'Login');
  });

  authSubmitBtn.addEventListener('click', () => {
    const email = authEmail.value.trim();
    const pass = authPassword.value.trim();
    if (!email || pass.length < 6) { alert('Email and password (6+ chars)'); return; }
    if (isLogin) {
      auth.signInWithEmailAndPassword(email, pass).catch(e => alert(e.message));
    } else {
      auth.createUserWithEmailAndPassword(email, pass).then(cred => {
        cred.user.updateProfile({ displayName: email.split('@')[0] });
      }).catch(e => alert(e.message));
    }
    authModal.style.display = 'none';
  });

  logoutBtn.addEventListener('click', () => { auth.signOut(); });

  // --- Admin Upload ---
  document.getElementById('uploadBtn').addEventListener('click', async () => {
    const title = document.getElementById('videoTitle').value.trim();
    const category = document.getElementById('videoCategory').value.trim();
    const release = document.getElementById('videoRelease').value.trim();
    const desc = document.getElementById('videoDesc').value.trim();
    const videoFile = document.getElementById('videoFile').files[0];
    const thumbFile = document.getElementById('thumbFile').files[0];
    if (!title || !videoFile) { alert('Title and video file required'); return; }
    const status = document.getElementById('uploadStatus');
    status.textContent = 'Uploading...';
    try {
      const videoRef = storage.ref('videos/' + videoFile.name + '_' + Date.now());
      await videoRef.put(videoFile);
      const videoURL = await videoRef.getDownloadURL();
      let thumbURL = '';
      if (thumbFile) {
        const thumbRef = storage.ref('thumbnails/' + thumbFile.name + '_' + Date.now());
        await thumbRef.put(thumbFile);
        thumbURL = await thumbRef.getDownloadURL();
      }
      await db.collection('videos').add({
        title, category: category || 'Uncategorized', release: release || '2025',
        description: desc || '', videoUrl: videoURL, thumbnail: thumbURL || '',
        approved: true, createdAt: firebase.firestore.FieldValue.serverTimestamp()
      });
      status.textContent = '✅ Upload successful!';
      loadAllContent();
      document.getElementById('videoTitle').value = '';
      document.getElementById('videoCategory').value = '';
      document.getElementById('videoRelease').value = '';
      document.getElementById('videoDesc').value = '';
      document.getElementById('videoFile').value = '';
      document.getElementById('thumbFile').value = '';
    } catch (e) { status.textContent = '❌ Error: ' + e.message; }
  });

  // Search (simple client-side)
  document.getElementById('globalSearch').addEventListener('input', function(e) {
    const q = this.value.toLowerCase().trim();
    document.querySelectorAll('.card').forEach(card => {
      const title = card.querySelector('h4')?.textContent?.toLowerCase() || '';
      card.style.display = (q === '' || title.includes(q)) ? '' : 'none';
    });
  });

  // initial load
  loadAllContent();
  // show home by default
  homePage.classList.remove('hidden');
  moviesPage.classList.add('hidden');
  seriesPage.classList.add('hidden');
  categoriesPage.classList.add('hidden');
</script>
</body>
</html>
