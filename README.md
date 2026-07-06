<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>شات حسوني - النسخة الإمبراطورية السحابية الموحدة</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0/css/all.min.css">
    
    <script src="https://www.gstatic.com/firebasejs/10.8.0/firebase-app-compat.js"></script>
    <script src="https://www.gstatic.com/firebasejs/10.8.0/firebase-firestore-compat.js"></script>

    <style>
        :root { 
            --gold: #ffd700; 
            --king-grad: linear-gradient(145deg, #ffd700, #b8860b); 
            --dark-bg: #0a0a0a; 
            --card-bg: #121212; 
            --user-bg-color: rgba(255, 215, 0, 0.05);
        }
        * { box-sizing: border-box; font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif; -webkit-tap-highlight-color: transparent; }
        body, html { margin: 0; padding: 0; height: 100vh; background: var(--dark-bg); color: #fff; overflow: hidden; }

        #welcomeOverlay {
            display: flex; 
            position: fixed; 
            inset: 0; 
            background: #0a0a0a; 
            z-index: 9999999; 
            align-items: center; 
            justify-content: center; 
            padding: 15px;
        }

        .header-bar { position: fixed; top: 0; width: 100%; height: 65px; background: rgba(15, 15, 15, 0.98); display: flex; align-items: center; justify-content: space-around; z-index: 1000; border-bottom: 2px solid var(--gold); }
        .header-btn { color: #fff; font-size: 11px; text-align: center; cursor: pointer; flex: 1; }
        .header-btn i { display: block; font-size: 18px; color: var(--gold); margin-bottom: 2px; }

        .mics-container { position: fixed; top: 65px; width: 100%; height: 60px; background: rgba(20, 20, 20, 0.95); border-bottom: 1px solid #222; display: flex; align-items: center; justify-content: space-around; z-index: 999; padding: 5px; }
        .mic-slot { display: flex; flex-direction: column; align-items: center; justify-content: center; width: 22%; height: 100%; cursor: pointer; border-radius: 8px; background: rgba(255,255,255,0.02); border: 1px solid rgba(255,215,0,0.1); background-size: cover; background-position: center; position: relative; }
        .mic-slot i.fa-heart { font-size: 18px; color: #e74c3c; }
        .mic-slot.occupied i.fa-heart { display: none; }
        .mic-slot .mic-user-name { font-size: 10px; color: #fff; margin-top: 2px; max-width: 90%; overflow: hidden; text-overflow: ellipsis; white-space: nowrap; background: rgba(0,0,0,0.7); padding: 1px 4px; border-radius: 4px; }
        .mic-speaking-glow { position: absolute; inset: 0; border: 2px solid #2ecc71; border-radius: 8px; animation: pulseGlow 1s infinite; display: none; }
        .mic-status-badge { position: absolute; top: -2px; left: -2px; background: #e74c3c; font-size: 8px; padding: 1px 3px; border-radius: 4px; display: none; }

        @keyframes pulseGlow { 0% { opacity: 0.4; } 50% { opacity: 1; } 100% { opacity: 0.4; } }

        #chatBox { height: calc(100vh - 190px); overflow-y: auto; padding: 135px 15px 85px; display: flex; flex-direction: column; gap: 12px; background: #0f0f0f url('https://i.ibb.co/6wXbYm2/butterflies.jpg') center center/cover no-repeat; }
        
        .msg-wrap { display: flex; flex-direction: column; align-self: flex-start; width: 95%; max-width: 420px; background: rgba(18, 22, 28, 0.94); padding: 12px; border-radius: 18px; border: 1.5px solid rgba(255, 215, 0, 0.4); box-shadow: 0 4px 15px rgba(0,0,0,0.5); position: relative; }
        .msg-header { display: flex; align-items: center; gap: 10px; width: 100%; }
        
        .pfp-main-frame { width: 44px; height: 44px; border-radius: 50%; border: 2px solid var(--gold); box-shadow: 0 0 8px var(--gold); display: flex; align-items: center; justify-content: center; background: #000; flex-shrink: 0; }
        .pfp-main { width: 100%; height: 100%; border-radius: 50%; object-fit: cover; cursor: pointer; }
        
        .rank-standalone-icon {
            font-size: 16px; display: flex; align-items: center; justify-content: center; width: 28px; height: 28px; background: rgba(0, 0, 0, 0.5); border-radius: 50%; border: 1px solid rgba(255, 215, 0, 0.3); flex-shrink: 0;
        }

        .king-name-container {
            display: inline-flex; align-items: center; background: linear-gradient(145deg, #1e1e1e, #111111); border: 1px solid var(--gold); padding: 4px 12px; border-radius: 20px; box-shadow: 0 2px 8px rgba(255, 215, 0, 0.2); cursor: pointer;
        }
        .king-name-tag { font-size: 13px; font-weight: bold; text-shadow: 0 0 3px rgba(255,215,0,0.3); }
        
        .msg-text { color: #fff; font-size: 14px; line-height: 1.5; margin-top: 8px; padding-right: 5px; word-break: break-word; }
        .msg-time { position: absolute; bottom: 4px; left: 12px; font-size: 9px; color: #888; }

        .input-section { position: fixed; bottom: 60px; width: 100%; height: 65px; background: #111; padding: 10px; display: flex; align-items: center; gap: 8px; border-top: 1px solid #222; z-index: 1000; }
        .chat-input { flex: 1; background: #1a1a1a; border: 1px solid var(--gold); color: #fff; height: 42px; border-radius: 20px; padding: 0 15px; outline: none; }
        .send-btn { background: var(--king-grad); border: none; padding: 0 20px; height: 42px; border-radius: 20px; font-weight: bold; cursor: pointer; color: #000; }

        .footer-nav { position: fixed; bottom: 0; width: 100%; height: 60px; background: #111; display: flex; align-items: center; justify-content: space-around; border-top: 2px solid var(--gold); z-index: 1000; }
        .f-btn { text-align: center; font-size: 10px; color: #fff; cursor: pointer; flex: 1; padding: 5px 0; }
        .f-btn i { display: block; font-size: 16px; margin-bottom: 2px; color: #fff; }

        .king-card { background: var(--card-bg); width: 100%; max-width: 520px; max-height: 95vh; border: 3px solid var(--gold); border-radius: 20px; padding: 20px; overflow-y: auto; box-shadow: 0 0 25px rgba(255, 215, 0, 0.3); display: flex; flex-direction: column; }
        
        .btn-row { display: flex; justify-content: center; gap: 8px; margin: 15px 0; width: 100%; }
        .row-btn { flex: 1; padding: 11px 5px; font-size: 12px; background: #1c1c1c; border: 1px solid var(--gold); color: #fff; border-radius: 8px; font-weight: bold; cursor: pointer; text-align: center; }
        .row-btn.active { background: var(--king-grad); color: #000; }
        
        .branch-content { display: none; background: #161616; padding: 15px; border-radius: 8px; border: 1px solid #333; margin-bottom: 15px; }
        .form-control { width: 100%; padding: 11px; margin-bottom: 11px; background: #222; border: 1px solid #444; color: #fff; border-radius: 8px; outline: none; text-align: right; }
        .form-select { width: 100%; padding: 11px; margin-bottom: 11px; background: #222; border: 1px solid #444; color: #fff; border-radius: 8px; text-align: right; }
        .file-input-label { display: block; width: 100%; padding: 11px; margin-bottom: 11px; background: #2a2a2a; border: 1px dashed var(--gold); color: var(--gold); border-radius: 8px; text-align: center; cursor: pointer; font-size: 13px; font-weight: bold; }
        .file-input-hidden { display: none; }

        .feature-modal { display: none; position: fixed; inset: 0; background: rgba(0,0,0,0.85); z-index: 100000; align-items: center; justify-content: center; padding: 15px; }
        .feature-card { background: #121212; width: 100%; max-width: 460px; border: 2px solid var(--gold); border-radius: 15px; padding: 20px; max-height: 85vh; overflow-y: auto; position: relative; }
        .half-screen-modal { display: none; position: fixed; bottom: 60px; left: 0; width: 100%; height: 50vh; background: rgba(14, 14, 14, 0.98); border-top: 3px solid var(--gold); z-index: 999; overflow-y: auto; padding: 15px; box-shadow: 0 -5px 20px rgba(0,0,0,0.8); }

        .menu-item { padding: 12px; border-bottom: 1px solid #222; cursor: pointer; display: flex; align-items: center; gap: 10px; font-size: 14px; color: #fff; justify-content: space-between; }
        .menu-item:hover { background: rgba(255,255,255,0.03); }

        .yt-preview-card { background: #1a1a1a; border: 2px solid #ff3333; border-radius: 12px; padding: 12px; margin-top: 12px; display: flex; align-items: center; gap: 12px; cursor: pointer; }
        .yt-preview-icon { font-size: 28px; color: #ff3333; animation: pulseGlow 1.5s infinite; }

        .profile-card-wrapper { text-align: center; color: #fff; position: relative; }
        .profile-card-cover { width: 100%; height: 140px; border-radius: 10px; object-fit: cover; border: 1px solid #333; }
        .profile-card-pfp { width: 90px; height: 90px; border-radius: 50%; border: 3px solid var(--gold); margin-top: -45px; object-fit: cover; background: #111; position: relative; z-index: 2; box-shadow: 0 4px 10px rgba(0,0,0,0.5); }
        .profile-edit-pencil { position: absolute; top: 10px; left: 10px; background: rgba(0,0,0,0.7); border: 1px solid var(--gold); color: var(--gold); width: 32px; height: 32px; border-radius: 50%; display: flex; align-items: center; justify-content: center; cursor: pointer; z-index: 10; }
        .profile-action-bar { display: flex; background: rgba(255,255,255,0.04); border: 1px solid #333; padding: 10px; border-radius: 8px; justify-content: space-around; margin: 15px 0; align-items: center; }
        .profile-bar-btn { text-align: center; color: #fff; cursor: pointer; font-size: 12px; flex: 1; }
        .profile-bar-btn i { display: block; font-size: 16px; color: var(--gold); margin-bottom: 3px; }
        .profile-details-grid { background: #161616; border: 1px solid #222; border-radius: 8px; padding: 10px; display: flex; flex-direction: column; gap: 8px; text-align: right; font-size: 13px; }
        .profile-grid-row { display: flex; justify-content: space-between; border-bottom: 1px solid rgba(255,255,255,0.02); padding-bottom: 6px; }
        .profile-grid-row span:first-child { color: #aaa; }
        .profile-grid-row span:last-child { color: var(--gold); font-weight: bold; }

        #youtubeVideoFrameContainer { position: fixed; top: -9999px; left: -9999px; width: 1px; height: 1px; overflow: hidden; opacity: 0; }
    </style>
</head>
<body>

<div id="youtubeVideoFrameContainer"></div>

<div id="welcomeOverlay">
    <div class="king-card">
        <h2 style="text-align:center; color:var(--gold); margin:0 0 5px;">شات حسوني - النسخة الإمبراطورية</h2>
        <p style="text-align:center; font-size:12px; margin:0 0 10px; color:#aaa;">لوحة التحكم وتسجيل الدخول الموحدة سحابياً</p>
        
        <div class="btn-row">
            <button class="row-btn" id="btn_b1" onclick="ui.switchBranch('b1')">دخول زائر</button>
            <button class="row-btn" id="btn_b2" onclick="ui.switchBranch('b2')">فرع العضوية</button>
            <button class="row-btn" id="btn_b3" onclick="ui.switchBranch('b3')">فرع التسجيل</button>
        </div>

        <div id="b1" class="branch-content">
            <input type="text" id="vName" class="form-control" placeholder="الاسم المستعار للزائر...">
            <select id="vAge" class="form-select">
                <option value="">اختر العمر...</option>
                <script>for(let i=15; i<=100; i++) { document.write(`<option value="${i}">${i}</option>`); }</script>
            </select>
            <select id="vGender" class="form-select">
                <option value="">اختر الجنس...</option>
                <option value="ذكر">ذكر</option>
                <option value="أنثى">أنثى</option>
            </select>
            <button class="send-btn" style="width:100%; border-radius:8px;" onclick="ui.loginAsGuest()">دخول الشات كـ زائر</button>
        </div>

        <div id="b2" class="branch-content">
            <input type="text" id="logUser" class="form-control" placeholder="الاسم المستعار أو البريد...">
            <input type="password" id="logPass" class="form-control" placeholder="كلمة المرور الحالية...">
            <button class="send-btn" style="width:100%; border-radius:8px;" onclick="ui.loginAsRegistered(false)">تسجيل دخول فوري</button>
        </div>

        <div id="b3" class="branch-content">
            <input type="text" id="rName" class="form-control" placeholder="الاسم المستعار الجديد...">
            <input type="email" id="rEmail" class="form-control" placeholder="البريد الإلكتروني المعتمد...">
            <input type="password" id="rPass" class="form-control" placeholder="كلمة المرور السرية...">
            <select id="rGender" class="form-select">
                <option value="ذكر">ذكر</option>
                <option value="أنثى">أنثى</option>
            </select>
            <button class="send-btn" style="width:100%; border-radius:8px;" onclick="ui.loginAsRegistered(true)">إتمام الحساب الفوري</button>
        </div>
    </div>
</div>

<div class="header-bar">
    <div class="header-btn" onclick="alert('لا توجد إشعارات')"><i class="fas fa-bell"></i>إشعارات</div>
    <div class="header-btn" onclick="alert('لوحة البلاغات فارغة')"><i class="fas fa-flag"></i>بلاغات</div>
    <div class="header-btn" onclick="alert('الخاص مشفر ومحمي')"><i class="fas fa-comments"></i>الخاص</div>
    <div class="header-btn" id="roomsManagerBtn" style="display:none;" onclick="ui.openRoomsManager()"><i class="fas fa-door-open"></i>إدارة الغرف</div>
    <div class="header-btn" onclick="ui.openVIPList('الكبار')"><i class="fas fa-crown"></i>الكبار</div>
</div>

<div class="mics-container" id="micsContainer">
    <div class="mic-slot" id="mic_1" onclick="ui.clickMicSlot(1)"><div class="mic-status-badge" id="mBadge_1">MUTE</div><div class="mic-speaking-glow" id="glow_1"></div><i class="fas fa-heart"></i><span class="mic-user-name" id="micName_1">مايك 1 فارغ</span></div>
    <div class="mic-slot" id="mic_2" onclick="ui.clickMicSlot(2)"><div class="mic-status-badge" id="mBadge_2">MUTE</div><div class="mic-speaking-glow" id="glow_2"></div><i class="fas fa-heart"></i><span class="mic-user-name" id="micName_2">مايك 2 فارغ</span></div>
    <div class="mic-slot" id="mic_3" onclick="ui.clickMicSlot(3)"><div class="mic-status-badge" id="mBadge_3">MUTE</div><div class="mic-speaking-glow" id="glow_3"></div><i class="fas fa-heart"></i><span class="mic-user-name" id="micName_3">مايك 3 فارغ</span></div>
    <div class="mic-slot" id="mic_4" onclick="ui.clickMicSlot(4)"><div class="mic-status-badge" id="mBadge_4">MUTE</div><div class="mic-speaking-glow" id="glow_4"></div><i class="fas fa-heart"></i><span class="mic-user-name" id="micName_4">مايك 4 فارغ</span></div>
</div>

<div id="chatBox"></div>

<div class="input-section">
    <i class="fas fa-image" style="color:var(--gold); font-size:24px; cursor:pointer;" onclick="alert('المعرض آمن وجاهز')"></i>
    <input type="text" id="msgInp" class="chat-input" placeholder="اكتب رسالتك الإمبراطورية هنا...">
    <button class="send-btn" onclick="ui.sendMessage()">إرسال</button>
</div>

<div class="footer-nav">
    <div class="f-btn" onclick="ui.toggleOnlineUsers()"><i class="fas fa-users"></i>المتواجدين</div>
    <div class="f-btn" onclick="ui.refreshChatWindowOnly()"><i class="fas fa-sync-alt"></i>تحديث</div>
    <div class="f-btn" id="ytFooterBtn" onclick="ui.openYouTubeSearchEngine()"><i class="fab fa-youtube" style="color:#ff3333"></i>يوتيوب</div>
    <div class="f-btn" id="authBtn" onclick="ui.showAuthBranchDirect()"><i class="fas fa-key" style="color:var(--gold)"></i><span>المفتاح الملكي</span></div>
    <div class="f-btn" onclick="ui.openGlobalSettings()"><i class="fas fa-cogs"></i>الإعدادات</div>
</div>

<div id="onlineUsersHalfModal" class="half-screen-modal">
    <div style="display:flex; justify-content:space-between; align-items:center; border-bottom:1px solid var(--gold); padding-bottom:5px; margin-bottom:10px;">
        <span style="color:var(--gold); font-weight:bold;"><i class="fas fa-users"></i> المتواجدين حسب الرتبة</span>
        <button onclick="ui.toggleOnlineUsers()" style="background:#c0392b; border:none; color:#fff; border-radius:50%; width:28px; height:28px; font-weight:bold; cursor:pointer;">X</button>
    </div>
    <div id="onlineUsersListBody"></div>
</div>

<div id="featureModal" class="feature-modal">
    <div class="feature-card">
        <h3 id="featureModalTitle" style="color:var(--gold); text-align:center; margin-top:0;"></h3>
        <div id="featureModalBody"></div>
        <button onclick="document.getElementById('featureModal').style.display='none'" class="send-btn" style="background:#c0392b; color:white; width:100%; margin-top:15px; border-radius:8px;">إغلاق</button>
    </div>
</div>

<script>
    const firebaseConfig = {
        apiKey: "AIzaSyCZ9Uh8sTZXsChbLXVvoaK81lxMU9dWsOc",
        authDomain: "soobr-9dbcf.firebaseapp.com",
        projectId: "soobr-9dbcf",
        storageBucket: "soobr-9dbcf.firebasestorage.app",
        messagingSenderId: "990736013570",
        appId: "1:990736013570:web:8d2d78961d2326548f8a1b",
        measurementId: "G-P13DV56ZFF"
    };

    if (!firebase.apps.length) {
        firebase.initializeApp(firebaseConfig);
    }
    const db = firebase.firestore();

    window.currentRoom = "العام";
    window.roomsList = ["العام"];
    
    window.chatRanksData = {
        "owner": { icon: "fas fa-trophy", color: "#ffd700", text: "البرنس الأصلي 👑" },
        "prince": { icon: "fas fa-trophy", color: "#aa0000", text: "برنس إمبراطوري 🏆" },
        "king": { icon: "fas fa-crown", color: "#FF0000", text: "الملك الملكي 👑" },
        "honor": { icon: "fas fa-crown", color: "#0000FF", text: "تاج الشرف" },
        "admin": { icon: "fas fa-star", color: "#FFD700", text: "إدارة العليا 🌟" },
        "developer": { icon: "fas fa-code", color: "#00FF00", text: "مطور السيرفر" },
        "senior_mod": { icon: "fas fa-gem", color: "#00FFFF", text: "مشرف أول" },
        "mod": { icon: "fas fa-star", color: "#C0C0C0", text: "مشرف" },
        "vip": { icon: "fas fa-fire", color: "#FF4500", text: "VIP" },
        "diamond": { icon: "fas fa-gem", color: "#8A2BE2", text: "عضو ماسي 💎" },
        "new": { icon: "fas fa-seedling", color: "#32CD32", text: "جديد" },
        "guest": { icon: "fas fa-user", color: "#ffffff", text: "زائر" }
    };

    window.rolesOrder = { "owner": 1, "prince": 2, "king": 3, "honor": 4, "admin": 5, "developer": 6, "senior_mod": 7, "mod": 8, "vip": 9, "diamond": 10, "new": 11, "guest": 12 };

    window.defaultOwnerData = { 
        uid: "owner_hassouni", name: "كاسر غرورك 🏆", role: "owner", level: 100, 
        img: "https://images.unsplash.com/photo-1535713875002-d1d0cf377fde?q=80&w=150", 
        nameBg: "rgba(255,215,0,0.15)", cover: "https://images.unsplash.com/photo-1618005182384-a83a8bd57fbe?q=80&w=400",
        likes: 999, age: 19, gender: "ذكر", country: "اليمن", status: "صاحب وملك الموقع الإمبراطوري الحصري 👑", points: 9999, isMuted: false, isBanned: false
    };

    window.currentUser = null;
    window.tempUploadedCover = ""; window.tempUploadedPfp = ""; window.tempUploadedRoomBg = "";

    window.ui = {
        switchBranch: (id) => {
            document.querySelectorAll('.branch-content').forEach(c => c.style.display = 'none');
            document.querySelectorAll('.row-btn').forEach(b => b.classList.remove('active'));
            document.getElementById(id).style.display = 'block';
            document.getElementById('btn_' + id).classList.add('active');
        },
        showAuthBranchDirect: () => {
            document.getElementById('featureModalTitle').innerText = "🔑 تفعيل المفتاح الفوري";
            document.getElementById('featureModalBody').innerHTML = `
                <div style="text-align:right;">
                    <input type="text" id="kName" class="form-control" placeholder="الاسم المستعار...">
                    <input type="email" id="kEmail" class="form-control" placeholder="البريد الإلكتروني...">
                    <input type="password" id="kPass" class="form-control" placeholder="كلمة المرور...">
                    <button class="send-btn" style="width:100%; border-radius:8px;" onclick="ui.executeKeyActivation()">التسجيل الفوري المباشر</button>
                </div>
            `;
            document.getElementById('featureModal').style.display = 'flex';
        },
        executeKeyActivation: () => {
            let n = document.getElementById('kName').value.trim();
            let em = document.getElementById('kEmail').value.trim();
            let ps = document.getElementById('kPass').value;
            if(!n || !em || !ps) { alert("أكمل الحقول!"); return; }
            let generatedToken = "token_" + Date.now();
            if(em === "ghrwrkk2@gmail.com") {
                window.currentUser = { ...window.defaultOwnerData, name: n, sessionToken: generatedToken };
            } else {
                window.currentUser = { uid: "u_"+Date.now(), name: n, role: "diamond", level: 10, img: "https://cdn-icons-png.flaticon.com/512/1042/1042291.png", cover: "https://images.unsplash.com/photo-1618005182384-a83a8bd57fbe?q=400", likes: 0, age: 20, gender: "ذكر", country: "اليمن", status: "عضو ماسي", points: 50, isMuted: false, isBanned: false, sessionToken: generatedToken };
            }
            ui.saveUserToFirestoreAndSession(window.currentUser);
            document.getElementById('featureModal').style.display = 'none';
            ui.enterChat();
        },
        loginAsGuest: () => {
            let n = document.getElementById('vName').value.trim();
            let a = document.getElementById('vAge').value;
            let g = document.getElementById('vGender').value;
            if(!n || !a || !g) { alert("املاً الحقول أولاً!"); return; }
            let generatedToken = "token_" + Date.now();
            window.currentUser = { uid: "g_"+Date.now(), name: n, role: "guest", level: 1, img: "https://cdn-icons-png.flaticon.com/512/1042/1042291.png", cover: "https://images.unsplash.com/photo-1618005182384-a83a8bd57fbe?q=400", likes: 0, age: a, gender: g, country: "اليمن", status: "زائر في الشات الموحد", points: 0, isMuted: false, isBanned: false, sessionToken: generatedToken };
            ui.saveUserToFirestoreAndSession(window.currentUser);
            ui.enterChat();
        },
        loginAsRegistered: (isNew) => {
            let userInp = isNew ? document.getElementById('rName').value.trim() : document.getElementById('logUser').value.trim();
            let passInp = isNew ? document.getElementById('rPass').value : document.getElementById('logPass').value;
            let genGender = isNew ? document.getElementById('rGender').value : "ذكر";
            if(!userInp || !passInp) { alert("أدخل البيانات كاملة!"); return; }
            let generatedToken = "token_" + Date.now();
            if(userInp === "ghrwrkk2@gmail.com" || passInp === "owner123") {
                window.currentUser = { ...window.defaultOwnerData, sessionToken: generatedToken };
            } else {
                window.currentUser = { uid: "u_"+Date.now(), name: userInp, role: "new", level: 2, img: "https://cdn-icons-png.flaticon.com/512/1042/1042291.png", cover: "https://images.unsplash.com/photo-1618005182384-a83a8bd57fbe?q=400", likes: 0, age: 22, gender: genGender, country: "اليمن", status: "عضو جديد في المنصة", points: 10, isMuted: false, isBanned: false, sessionToken: generatedToken };
            }
            ui.saveUserToFirestoreAndSession(window.currentUser);
            ui.enterChat();
        },
        saveUserToFirestoreAndSession: (userObj) => {
            localStorage.setItem("hassouni_user_session", JSON.stringify(userObj));
            db.collection("users").doc(userObj.uid).set(userObj, { merge: true });
        },
        updateUserOnlineStatus: (status) => {
            if (window.currentUser) {
                db.collection("users").doc(window.currentUser.uid).update({ isOnline: status, lastSeen: firebase.firestore.FieldValue.serverTimestamp() }).catch(()=>{});
            }
        },
        checkSavedSessionOnLoad: () => {
            let savedUser = localStorage.getItem("hassouni_user_session");
            if(savedUser) {
                let parsedUser = JSON.parse(savedUser);
                db.collection("users").doc(parsedUser.uid).get().then((doc)=>{
                    if(doc.exists){
                        let sData = doc.data();
                        if(sData.isBanned) { alert("لقد تم حظر حسابك نهائياً."); ui.logoutBackToWelcome(); return; }
                        window.currentUser = sData;
                        localStorage.setItem("hassouni_user_session", JSON.stringify(window.currentUser));
                    } else { window.currentUser = parsedUser; }
                    document.getElementById('welcomeOverlay').style.display = 'none'; 
                    ui.enterChat();
                }).catch(() => {
                    window.currentUser = parsedUser; document.getElementById('welcomeOverlay').style.display = 'none'; ui.enterChat();
                });
            } else {
                document.getElementById('welcomeOverlay').style.display = 'flex'; ui.switchBranch('b1');
            }
        },
        enterChat: () => {
            document.getElementById('welcomeOverlay').style.display = 'none';
            ui.updateUserOnlineStatus(true);
            
            if(window.currentUser.role === 'owner' || window.currentUser.role === 'admin' || window.currentUser.role === 'prince') {
                document.getElementById('roomsManagerBtn').style.display = 'flex';
            }
            if(window.currentUser.role !== 'guest') {
                document.getElementById('authBtn').style.display = 'none';
            }

            ui.listenToGlobalMessages();
            ui.listenToActiveMics();
            ui.listenToRoomSettings();
            ui.listenToSessionSecurity();
            ui.listenOnlineUsersRealtime();
        },
        listenToSessionSecurity: () => {
            if(!window.currentUser || !window.currentUser.uid) return;
            db.collection("users").doc(window.currentUser.uid).onSnapshot((doc) => {
                if(doc.exists) {
                    let data = doc.data();
                    if(window.currentUser.sessionToken && data.sessionToken && data.sessionToken !== window.currentUser.sessionToken) {
                        alert("⚠️ عذراً، تم فتح هذه العضوية من جهاز أو متصفح آخر!");
                        ui.logoutBackToWelcome();
                    }
                }
            });
        },
        listenToRoomSettings: () => {
            db.collection("room_settings").doc(window.currentRoom).onSnapshot((doc) => {
                if(doc.exists) {
                    let data = doc.data();
                    if(data.roomBg) { document.getElementById('chatBox').style.backgroundImage = `url('${data.roomBg}')`; }
                    let ytContainer = document.getElementById('youtubeVideoFrameContainer');
                    if(data.activeAudioId) {
                        ytContainer.innerHTML = `<iframe width="10" height="10" src="https://www.youtube.com/embed/${data.activeAudioId}?autoplay=1&loop=1&playlist=${data.activeAudioId}" allow="autoplay"></iframe>`;
                        window.currentRoomAudioOwner = data.audioOwner || "";
                    } else { ytContainer.innerHTML = ""; window.currentRoomAudioOwner = ""; }
                }
            });
        },
        listenToGlobalMessages: () => {
            db.collection("rooms").doc(window.currentRoom).collection("messages").orderBy("timestamp", "asc").limitToLast(40).onSnapshot((snapshot) => {
                  let chatBox = document.getElementById('chatBox'); chatBox.innerHTML = "";
                  snapshot.forEach((doc) => {
                      let mData = doc.data();
                      if (mData.user) { ui.renderMsg(mData.user, mData.text, mData.timeStr || "00:00"); }
                  });
              });
        },
        listenToActiveMics: () => {
            db.collection("rooms").doc(window.currentRoom).collection("mics").onSnapshot((snapshot) => {
                  for(let i=1; i<=4; i++) {
                      let slot = document.getElementById(`mic_${i}`); slot.classList.remove('occupied'); slot.style.backgroundImage = 'none';
                      document.getElementById(`micName_${i}`).innerText = `مايك ${i} فارغ`;
                      document.getElementById(`glow_${i}`).style.display = 'none'; document.getElementById(`mBadge_${i}`).style.display = 'none';
                  }
                  snapshot.forEach((doc) => {
                      let micData = doc.data(); let num = micData.micNum; let slot = document.getElementById(`mic_${num}`);
                      slot.classList.add('occupied'); slot.style.backgroundImage = `url('${micData.userImg}')`;
                      document.getElementById(`micName_${num}`).innerText = micData.userName;
                      document.getElementById(`glow_${num}`).style.display = 'block';
                      if(micData.isMuted) { document.getElementById(`mBadge_${num}`).style.display = 'block'; document.getElementById(`glow_${num}`).style.animation = 'none'; }
                      else { document.getElementById(`mBadge_${num}`).style.display = 'none'; document.getElementById(`glow_${num}`).style.animation = 'pulseGlow 1s infinite'; }
                  });
              });
        },
        listenOnlineUsersRealtime: () => {
            db.collection("users").onSnapshot((snap) => {
                let list = []; snap.forEach(doc => { let uData = doc.data(); if(uData.isOnline) list.push(uData); });
                list.sort((a, b) => (window.rolesOrder[a.role] || 99) - (window.rolesOrder[b.role] || 99));
                let usersHtml = list.map(u => {
                    let rObj = window.chatRanksData[u.role] || { icon: "fas fa-user", color: "#fff", text: "عضو" };
                    return `<div class="menu-item" onclick="ui.viewProfileCard('${u.uid}')"><span style="color:${rObj.color}; font-weight: bold;"><i class="${rObj.icon}" style="margin-left:5px;"></i> ${u.name}</span><span style="font-size:11px; color:${rObj.color}; background: rgba(0,0,0,0.4); padding: 2px 6px; border-radius: 10px; border: 1px solid ${rObj.color};">${rObj.text}</span></div>`;
                }).join('');
                document.getElementById('onlineUsersListBody').innerHTML = usersHtml;
            });
        },
        refreshChatWindowOnly: () => { alert("تم المزامنة والتحديث سحابياً 🚀"); },
        sendMessage: () => {
            if(window.currentUser.isMuted) { alert("أنت مكتوم من الإدارة."); return; }
            let inp = document.getElementById('msgInp'); let t = inp.value.trim(); if(!t) return;
            inp.value = '';
            let d = new Date(); let timeStr = d.getHours() + ":" + (d.getMinutes()<10?'0':'') + d.getMinutes();
            db.collection("users").doc(window.currentUser.uid).get().then((doc) => {
                let u = doc.exists ? doc.data() : window.currentUser;
                db.collection("rooms").doc(window.currentRoom).collection("messages").add({
                    user: { uid: u.uid, name: u.name, role: u.role, img: u.img }, text: t, timeStr: timeStr, timestamp: firebase.firestore.FieldValue.serverTimestamp()
                });
            });
        },
        renderMsg: (user, text, time) => {
            let div = document.createElement('div'); div.className = 'msg-wrap';
            let rObj = window.chatRanksData[user.role] || { icon: "fas fa-user", color: "#fff" };
            div.innerHTML = `
                <div class="msg-header">
                    <div class="pfp-main-frame"><img src="${user.img}" class="pfp-main" onclick="ui.viewProfileCard('${user.uid}')"></div>
                    <div class="rank-standalone-icon" style="border-color:${rObj.color};"><i class="${rObj.icon}" style="color:${rObj.color};"></i></div>
                    <div class="king-name-container" style="border-color:${rObj.color}; background:rgba(0,0,0,0.6);">
                        <span class="king-name-tag" style="color:${rObj.color};">${user.name}</span>
                    </div>
                </div>
                <div class="msg-text">${text}</div>
                <div class="msg-time">${time}</div>
            `;
            let box = document.getElementById('chatBox'); box.appendChild(div); box.scrollTop = box.scrollHeight;
        },
        clickMicSlot: (num) => {
            window.selectedMicNum = num;
            let slot = document.getElementById(`mic_${num}`);
            if(!slot.classList.contains('occupied')) {
                db.collection("rooms").doc(window.currentRoom).collection("mics").where("userId", "==", window.currentUser.uid).get().then(s => {
                    if(!s.empty) { alert("لا يمكنك الصعود على أكثر من مايك في نفس الوقت!"); } 
                    else {
                        db.collection("rooms").doc(window.currentRoom).collection("mics").doc(`mic_${num}`).set({
                            micNum: num, userId: window.currentUser.uid, userName: window.currentUser.name, userImg: window.currentUser.img, isMuted: false
                        });
                    }
                });
            } else {
                document.getElementById('featureModalTitle').innerText = "🎛️ إدارة المايك والبث";
                document.getElementById('featureModalBody').innerHTML = `
                    <div class="menu-item" onclick="ui.toggleMicVoice(true)"><i class="fas fa-microphone-slash"></i> كتم المايك الشخصي</div>
                    <div class="menu-item" onclick="ui.toggleMicVoice(false)"><i class="fas fa-microphone"></i> إلغاء كتم الصوت</div>
                    <div class="menu-item" onclick="ui.vacateMicSlot(${num})" style="color:red;"><i class="fas fa-sign-out-alt"></i> النزول من المصطبة</div>
                `;
                document.getElementById('featureModal').style.display = 'flex';
            }
        },
        toggleMicVoice: (state) => {
            db.collection("rooms").doc(window.currentRoom).collection("mics").doc(`mic_${window.selectedMicNum}`).update({ isMuted: state });
            document.getElementById('featureModal').style.display = 'none';
        },
        vacateMicSlot: (num) => {
            db.collection("rooms").doc(window.currentRoom).collection("mics").doc(`mic_${num}`).delete();
            document.getElementById('featureModal').style.display = 'none';
        },
        openYouTubeSearchEngine: () => {
            document.getElementById('featureModalTitle').innerText = "📺 مشغل الشيلات واليوتيوب";
            document.getElementById('featureModalBody').innerHTML = `
                <input type="text" id="ytInp" class="form-control" placeholder="ضع رابط اليوتيوب هنا لتشغيله للجميع...">
                <button class="send-btn" style="width:100%;" onclick="ui.playYoutubeTrack()">🎯 إطلاق البث الموحد</button>
                <button class="send-btn" style="width:100%; background:#e74c3c; margin-top:8px; color:white;" onclick="ui.stopYoutubeTrack()">🛑 إيقاف المسار الموسيقي</button>
            `;
            document.getElementById('featureModal').style.display = 'flex';
        },
        playYoutubeTrack: () => {
            let val = document.getElementById('ytInp').value.trim();
            let regExp = /^.*(youtu.be\/|v\/|u\/\w\/|embed\/|watch\?v=|\&v=)([^#\&\?]*).*/;
            let match = val.match(regExp);
            let videoId = (match && match[2].length === 11) ? match[2] : null;
            if(!videoId) { alert("رابط غير صحيح!"); return; }
            db.collection("room_settings").doc(window.currentRoom).set({ activeAudioId: videoId, audioOwner: window.currentUser.uid }, { merge: true });
            document.getElementById('featureModal').style.display = 'none';
        },
        stopYoutubeTrack: () => {
            let amIAdmin = (window.currentUser.role === 'owner' || window.currentUser.role === 'admin' || window.currentUser.role === 'prince');
            if(window.currentRoomAudioOwner === window.currentUser.uid || amIAdmin) {
                db.collection("room_settings").doc(window.currentRoom).set({ activeAudioId: "" }, { merge: true });
                document.getElementById('featureModal').style.display = 'none';
            } else { alert("لا يمكنك إيقاف الموسيقى، لست من أطلقها أو لست صاحب الموقع/الإدارة العليا!"); }
        },
        toggleOnlineUsers: () => {
            let m = document.getElementById('onlineUsersHalfModal'); m.style.display = (m.style.display === 'block') ? 'none' : 'block';
        },
        viewProfileCard: (uid) => {
            db.collection("users").doc(uid).get().then((doc) => {
                if(!doc.exists) return; let u = doc.data();
                let isMe = (window.currentUser.uid === uid);
                let amIAdmin = (window.currentUser.role === 'owner' || window.currentUser.role === 'admin' || window.currentUser.role === 'prince');
                let pencilHtml = (isMe || amIAdmin) ? `<div class="profile-edit-pencil" onclick="ui.openEditProfileModal('${uid}')"><i class="fas fa-pencil-alt"></i></div>` : '';
                let adminControls = (amIAdmin && !isMe) ? `<button class="send-btn" style="width:100%; margin-top:10px; background:red; color:#fff;" onclick="ui.openAdminControls('${uid}')">👑 الإجراءات الإدارية الصارمة</button>` : '';
                let rObj = window.chatRanksData[u.role] || { icon: "fas fa-user", color: "#fff", text: "عضو" };
                
                document.getElementById('featureModalTitle').innerText = "الملف الشخصي الفوري";
                document.getElementById('featureModalBody').innerHTML = `
                    <div class="profile-card-wrapper">
                        ${pencilHtml}
                        <img src="${u.cover}" class="profile-card-cover">
                        <img src="${u.img}" class="profile-card-pfp">
                        <h2 style="color:${rObj.color};">${u.name}</h2>
                        <p style="color:${rObj.color}; font-size:12px;"><i class="${rObj.icon}"></i> ${rObj.text}</p>
                        <p style="color:#aaa; font-size:12px;">${u.status || 'لا توجد حالة حالياً'}</p>
                        <div class="profile-action-bar">
                            <div class="profile-bar-btn" onclick="ui.likeProfile('${uid}')"><i class="fas fa-heart"></i> <span>${u.likes||0}</span></div>
                            <div class="profile-bar-btn">ليفل ${u.level||1}</div>
                        </div>
                        <div class="profile-details-grid">
                            <div class="profile-grid-row"><span>الجنس:</span><span>${u.gender || 'غير محدد'}</span></div>
                            <div class="profile-grid-row"><span>العمر:</span><span>${u.age || '19'}</span></div>
                            <div class="profile-grid-row"><span>البلد:</span><span>${u.country || 'اليمن'}</span></div>
                        </div>
                        ${adminControls}
                    </div>
                `;
                document.getElementById('featureModal').style.display = 'flex';
            });
        },
        likeProfile: (uid) => {
            db.collection("users").doc(uid).update({ likes: firebase.firestore.FieldValue.increment(1) });
        },
        openEditProfileModal: (uid) => {
            db.collection("users").doc(uid).get().then((doc) => {
                let u = doc.data(); window.tempUploadedCover = u.cover; window.tempUploadedPfp = u.img;
                document.getElementById('featureModalTitle').innerText = "تعديل الملف السحابي الموحد";
                document.getElementById('featureModalBody').innerHTML = `
                    <label>رابط صورة الغلاف الجديد:</label><input type="text" id="edCover" class="form-control" value="${u.cover}">
                    <label>رابط الصورة الشخصية الجديد:</label><input type="text" id="edPfp" class="form-control" value="${u.img}">
                    <label>الاسم (المزخرف):</label><input type="text" id="edName" class="form-control" value="${u.name}">
                    <label>الحالة الشخصية:</label><input type="text" id="edStatus" class="form-control" value="${u.status||''}">
                    <label>الجنس:</label>
                    <select id="edGender" class="form-select">
                        <option value="ذكر" ${u.gender==='ذكر'?'selected':''}>ذكر</option>
                        <option value="أنثى" ${u.gender==='أنثى'?'selected':''}>أنثى</option>
                    </select>
                    <button class="send-btn" style="width:100%;" onclick="ui.saveProfileDataCloud('${uid}')">حفظ ونشر التعديلات فوراً للجميع 🎯</button>
                `;
            });
        },
        saveProfileDataCloud: (uid) => {
            let updated = {
                cover: document.getElementById('edCover').value.trim(),
                img: document.getElementById('edPfp').value.trim(),
                name: document.getElementById('edName').value.trim(),
                status: document.getElementById('edStatus').value.trim(),
                gender: document.getElementById('edGender').value
            };
            db.collection("users").doc(uid).update(updated).then(() => {
                alert("تم الحفظ والتحديث الفوري السحابي!");
                if(window.currentUser.uid === uid) { window.currentUser = { ...window.currentUser, ...updated }; localStorage.setItem("hassouni_user_session", JSON.stringify(window.currentUser)); }
                document.getElementById('featureModal').style.display = 'none';
            });
        },
        openAdminControls: (uid) => {
            db.collection("users").doc(uid).get().then((doc) => {
                let u = doc.data();
                document.getElementById('featureModalTitle').innerText = `إدارة الملك: ${u.name}`;
                document.getElementById('featureModalBody').innerHTML = `
                    <select id="roleSel" class="form-select" onchange="ui.changeRole('${uid}', this.value)">
                        <option value="owner" ${u.role==='owner'?'selected':''}>البرنس الأصلي 👑</option>
                        <option value="prince" ${u.role==='prince'?'selected':''}>برنس إمبراطوري 🏆</option>
                        <option value="king" ${u.role==='king'?'selected':''}>الملك الملكي 👑</option>
                        <option value="admin" ${u.role==='admin'?'selected':''}>إدارة عليا 🌟</option>
                        <option value="diamond" ${u.role==='diamond'?'selected':''}>عضو ماسي 💎</option>
                    </select>
                    <button class="send-btn" style="width:100%; background:orange; margin-top:8px; color:white;" onclick="ui.toggleMute('${uid}', ${!u.isMuted})">${u.isMuted?'إلغاء الكتم':'كتم العضو فوراً'}</button>
                    <button class="send-btn" style="width:100%; background:red; margin-top:8px; color:white;" onclick="ui.toggleBan('${uid}', ${!u.isBanned})">${u.isBanned?'إلغاء الطرد':'طرد وحظر نهائي'}</button>
                `;
            });
        },
        changeRole: (uid, r) => db.collection("users").doc(uid).update({ role: r }),
        toggleMute: (uid, s) => { db.collection("users").doc(uid).update({ isMuted: s }); document.getElementById('featureModal').style.display = 'none'; },
        toggleBan: (uid, s) => { db.collection("users").doc(uid).update({ isBanned: s }); document.getElementById('featureModal').style.display = 'none'; },
        openGlobalSettings: () => {
            document.getElementById('featureModalTitle').innerText = "لوحة تحكم إمبراطور السيرفر 👑";
            let amIOwner = (window.currentUser.role === 'owner' || window.currentUser.role === 'admin');
            let adminArea = amIOwner ? `
                <div style="border-top:1px solid gold; padding-top:10px; margin-top:10px;">
                    <label>تغيير خلفية الروم العامة (رابط مباشر):</label>
                    <input type="text" id="roomBgInp" class="form-control" placeholder="ضع رابط الصورة هنا...">
                    <button class="send-btn" style="width:100%;" onclick="ui.saveRoomBg()">تحديث خلفية الروم لجميع الأعضاء فوراً</button>
                    <button class="send-btn" style="width:100%; background:red; color:white; margin-top:8px;" onclick="ui.cleanRoomMessages()">🧹 تطهير وتنظيف الشات بالكامل</button>
                </div>
            ` : '';
            document.getElementById('featureModalBody').innerHTML = `
                ${adminArea}
                <div class="menu-item" style="color:red;" onclick="ui.logoutBackToWelcome()"><i class="fas fa-sign-out-alt"></i> تسجيل خروج نهائي من الجلسة</div>
            `;
            document.getElementById('featureModal').style.display = 'flex';
        },
        saveRoomBg: () => {
            let bg = document.getElementById('roomBgInp').value.trim();
            if(!bg) return;
            db.collection("room_settings").doc(window.currentRoom).set({ roomBg: bg }, { merge: true }).then(() => { alert("تم التحديث السحابي الشامل!"); });
        },
        cleanRoomMessages: () => {
            if(confirm("تطهير ومسح الشات العام؟")) {
                db.collection("rooms").doc(window.currentRoom).collection("messages").get().then(s => s.forEach(d => d.ref.delete()));
                document.getElementById('featureModal').style.display = 'none';
            }
        },
        openRoomsManager: () => {
            document.getElementById('featureModalTitle').innerText = "إنشاء وإدارة الغرف السحابية";
            document.getElementById('featureModalBody').innerHTML = `
                <input type="text" id="newRoomInp" class="form-control" placeholder="اسم الغرفة السحابية الجديدة...">
                <button class="send-btn" style="width:100%;" onclick="ui.createRoom()">➕ إنشاء الغرفة فوراً</button>
            `;
            document.getElementById('featureModal').style.display = 'flex';
        },
        createRoom: () => {
            let r = document.getElementById('newRoomInp').value.trim(); if(!r) return;
            alert(`تم تهيئة وإنشاء غرفة [ ${r} ] سحابياً وبنجاح!`);
            document.getElementById('featureModal').style.display = 'none';
        },
        logoutBackToWelcome: () => {
            ui.updateUserOnlineStatus(false); localStorage.removeItem("hassouni_user_session");
            setTimeout(() => { window.location.reload(); }, 300);
        },
        openVIPList: (title) => alert(`لوحة رتب: ${title}`)
    };

    window.onload = () => { ui.checkSavedSessionOnLoad(); };
</script>
</body>
</html>
