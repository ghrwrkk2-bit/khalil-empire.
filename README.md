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
            display: none; 
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
        .mic-slot i.fa-microphone { font-size: 18px; color: rgba(255,215,0,0.4); }
        .mic-slot.occupied i.fa-microphone { display: none; }
        .mic-slot .mic-user-name { font-size: 10px; color: #fff; margin-top: 2px; max-width: 90%; overflow: hidden; text-overflow: ellipsis; white-space: nowrap; background: rgba(0,0,0,0.7); padding: 1px 4px; border-radius: 4px; }
        .mic-speaking-glow { position: absolute; inset: 0; border: 2px solid #2ecc71; border-radius: 8px; animation: pulseGlow 1s infinite; display: none; }
        .mic-status-badge { position: absolute; top: -2px; left: -2px; background: #e74c3c; font-size: 8px; padding: 1px 3px; border-radius: 4px; display: none; }

        @keyframes pulseGlow { 0% { opacity: 0.4; } 50% { opacity: 1; } 100% { opacity: 0.4; } }

        #chatBox { height: calc(100vh - 190px); overflow-y: auto; padding: 135px 15px 85px; display: flex; flex-direction: column; gap: 12px; background: #0f0f0f url('https://i.ibb.co/6wXbYm2/butterflies.jpg') center center/cover no-repeat; }
        
        .msg-wrap { display: flex; flex-direction: column; align-self: flex-start; width: 95%; max-width: 420px; background: rgba(18, 22, 28, 0.94); padding: 12px; border-radius: 18px; border: 1.5px solid rgba(255, 215, 0, 0.4); box-shadow: 0 4px 15px rgba(0,0,0,0.5); position: relative; }
        .msg-header { display: flex; align-items: center; gap: 10px; width: 100%; }
        
        .pfp-main-frame { width: 44px; height: 44px; border-radius: 50%; border: 2px solid var(--gold); box-shadow: 0 0 8px var(--gold); display: flex; align-items: center; justify-content: center; background: #000; flex-shrink: 0; }
        .pfp-main { width: 100%; height: 100%; border-radius: 50%; object-fit: cover; cursor: pointer; }
        
        .rank-standalone-icon { font-size: 14px; display: flex; align-items: center; justify-content: center; width: 26px; height: 26px; background: rgba(0, 0, 0, 0.5); border-radius: 50%; border: 1px solid rgba(255, 215, 0, 0.3); flex-shrink: 0; }

        .king-name-container { display: inline-flex; align-items: center; background: linear-gradient(145deg, #1e1e1e, #111111); border: 1px solid var(--gold); padding: 4px 12px; border-radius: 20px; box-shadow: 0 2px 8px rgba(255, 215, 0, 0.2); cursor: pointer; }
        .king-name-tag { font-size: 13px; font-weight: bold; text-shadow: 0 0 3px rgba(255,215,0,0.3); }
        
        .msg-text { color: #fff; font-size: 14px; line-height: 1.5; margin-top: 8px; padding-right: 5px; word-break: break-word; }
        .msg-time { font-size: 9px; color: #888; align-self: flex-end; margin-top: 4px; }

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
        .yt-preview-icon { font-size: 28px; color: #ff3333; }

        .profile-card-wrapper { text-align: center; color: #fff; position: relative; }
        .profile-card-cover { width: 100%; height: 140px; border-radius: 10px; object-fit: cover; border: 1px solid #333; }
        .profile-card-pfp { width: 90px; height: 90px; border-radius: 50%; border: 3px solid var(--gold); margin-top: -45px; object-fit: cover; background: #111; position: relative; z-index: 2; box-shadow: 0 4px 10px rgba(0,0,0,0.5); }
        .profile-edit-pencil { position: absolute; top: 10px; left: 10px; background: rgba(0,0,0,0.7); border: 1px solid var(--gold); color: var(--gold); width: 32px; height: 32px; border-radius: 50%; display: flex; align-items: center; justify-content: center; cursor: pointer; z-index: 10; }
        .profile-action-bar { display: flex; background: rgba(255,255,255,0.04); border: 1px solid #333; padding: 10px; border-radius: 8px; justify-content: space-around; margin: 15px 0; align-items: center; }
        .profile-bar-btn { text-align: center; color: #fff; cursor: pointer; font-size: 12px; flex: 1; }
        .profile-bar-btn i { display: block; font-size: 16px; color: var(--gold); margin-bottom: 3px; }
        .profile-details-grid { background: #161616; border: 1px solid #222; border-radius: 8px; padding: 10px; display: flex; flex-direction: column; gap: 8px; text-align: right; font-size: 13px; }
        .profile-grid-row { display: flex; justify-content: space-between; border-bottom: 1px solid rgba(255,255,255,0.02); padding-bottom: 6px; }
        .profile-grid-row:last-child { border: none; }
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
        <p style="text-align:center; font-size:12px; margin:0 0 10px; color:#aaa;">لوحة الدخول الموحدة سحابياً لجميع المتصفحات</p>
        
        <div class="btn-row">
            <button class="row-btn" id="btn_b1" onclick="ui.switchBranch('b1')">دخول زائر</button>
            <button class="row-btn" id="btn_b2" onclick="ui.switchBranch('b2')">دخول عضوية</button>
            <button class="row-btn" id="btn_b3" onclick="ui.switchBranch('b3')">سجل الآن</button>
        </div>

        <div id="b1" class="branch-content">
            <input type="text" id="vName" class="form-control" placeholder="الاسم المستعار للزائر...">
            <input type="number" id="vAge" class="form-control" placeholder="العمر...">
            <select id="vGender" class="form-select">
                <option value="">اختر الجنس...</option>
                <option value="ذكر">ذكر</option>
                <option value="أنثى">أنثى</option>
            </select>
            <button class="send-btn" style="width:100%; border-radius:8px;" onclick="ui.loginAsGuest()">دخول الآن كـ زائر</button>
        </div>

        <div id="b2" class="branch-content">
            <input type="text" id="logUser" class="form-control" placeholder="الاسم المستعار أو البريد...">
            <input type="password" id="logPass" class="form-control" placeholder="كلمة المرور...">
            <button class="send-btn" style="width:100%; border-radius:8px;" onclick="ui.loginAsRegistered(false)">تسجيل الدخول الفوري</button>
        </div>

        <div id="b3" class="branch-content">
            <input type="text" id="rName" class="form-control" placeholder="الاسم المستعار الجديد...">
            <input type="email" id="rEmail" class="form-control" placeholder="البريد الإلكتروني...">
            <input type="password" id="rPass" class="form-control" placeholder="كلمة المرور السرية...">
            <select id="rGender" class="form-select">
                <option value="ذكر">ذكر</option>
                <option value="أنثى">أنثى</option>
            </select>
            <button class="send-btn" style="width:100%; border-radius:8px;" onclick="ui.loginAsRegistered(true)">إتمام التسجيل ودخول</button>
        </div>
    </div>
</div>

<div class="header-bar">
    <div class="header-btn" onclick="alert('لا توجد إشعارات')"><i class="fas fa-bell"></i>إشعارات</div>
    <div class="header-btn" onclick="alert('لوحة البلاغات فارغة')"><i class="fas fa-flag"></i>بلاغات</div>
    <div class="header-btn" onclick="alert('الخاص مشفر ومحمي')"><i class="fas fa-comments"></i>الخاص</div>
    <div class="header-btn" onclick="ui.openVIPList('الأثرياء')"><i class="fas fa-gem"></i>الأثرياء</div>
    <div class="header-btn" onclick="ui.openVIPList('الكبار')"><i class="fas fa-crown"></i>الكبار</div>
</div>

<div class="mics-container" id="micsContainer">
    <div class="mic-slot" id="mic_1" onclick="ui.clickMicSlot(1)"><div class="mic-status-badge" id="mBadge_1">MUTE</div><div class="mic-speaking-glow" id="glow_1"></div><i class="fas fa-microphone"></i><span class="mic-user-name" id="micName_1">مايك 1 فارغ</span></div>
    <div class="mic-slot" id="mic_2" onclick="ui.clickMicSlot(2)"><div class="mic-status-badge" id="mBadge_2">MUTE</div><div class="mic-speaking-glow" id="glow_2"></div><i class="fas fa-microphone"></i><span class="mic-user-name" id="micName_2">مايك 2 فارغ</span></div>
    <div class="mic-slot" id="mic_3" onclick="ui.clickMicSlot(3)"><div class="mic-status-badge" id="mBadge_3">MUTE</div><div class="mic-speaking-glow" id="glow_3"></div><i class="fas fa-microphone"></i><span class="mic-user-name" id="micName_3">مايك 3 فارغ</span></div>
    <div class="mic-slot" id="mic_4" onclick="ui.clickMicSlot(4)"><div class="mic-status-badge" id="mBadge_4">MUTE</div><div class="mic-speaking-glow" id="glow_4"></div><i class="fas fa-microphone"></i><span class="mic-user-name" id="micName_4">مايك 4 فارغ</span></div>
</div>

<div id="chatBox"></div>

<div class="input-section">
    <i class="fas fa-image" style="color:var(--gold); font-size:24px; cursor:pointer;" onclick="alert('المعرض آمن وجاهز')"></i>
    <input type="text" id="msgInp" class="chat-input" placeholder="اكتب رسالتك العامة هنا بكل حرية...">
    <button class="send-btn" onclick="ui.sendMessage()">إرسال</button>
</div>

<div class="footer-nav">
    <div class="f-btn" onclick="ui.toggleOnlineUsers()"><i class="fas fa-users"></i>المتواجدين</div>
    <div class="f-btn" onclick="ui.openRoomsManager()"><i class="fas fa-door-open"></i>الغرف</div>
    <div class="f-btn" onclick="ui.refreshChatWindowOnly()"><i class="fas fa-sync-alt"></i>تحديث</div>
    <div class="f-btn" id="ytFooterBtn" onclick="ui.openYouTubeSearchEngine()"><i class="fab fa-youtube" style="color:#ff3333"></i>يوتيوب</div>
    <div class="f-btn" id="authBtn" onclick="ui.showAuthBranchDirect()"><i class="fas fa-key" style="color:var(--gold)"></i><span>المفتاح الملكي</span></div>
    <div class="f-btn" onclick="ui.openGlobalSettings()"><i class="fas fa-cogs"></i>الإعدادات</div>
</div>

<div id="onlineUsersHalfModal" class="half-screen-modal">
    <div style="display:flex; justify-content:space-between; align-items:center; border-bottom:1px solid var(--gold); padding-bottom:5px; margin-bottom:10px;">
        <span style="color:var(--gold); font-weight:bold;"><i class="fas fa-users"></i> قائمة المتواجدين (مرتبة حسب الرتب)</span>
        <button onclick="ui.toggleOnlineUsers()" style="background:#c0392b; border:none; color:#fff; border-radius:50%; width:28px; height:28px; font-weight:bold; cursor:pointer;">X</button>
    </div>
    <div id="onlineUsersListBody"></div>
</div>

<div id="featureModal" class="feature-modal">
    <div class="feature-card">
        <h3 id="featureModalTitle" style="color:var(--gold); text-align:center; margin-top:0;"></h3>
        <div id="featureModalBody"></div>
        <button onclick="document.getElementById('featureModal').style.display='none'" class="send-btn" style="background:#c0392b; color:white; width:100%; margin-top:15px; border-radius:8px;">إغلاق النافذة</button>
    </div>
</div>

<script>
    // تكوين الفايربيس السحابي المشترك لـ شات حسوني
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
        "owner": { icon: "fas fa-trophy", color: "#ffd700", text: "البرنس الأصلي 🏆" },
        "prince": { icon: "fas fa-crown", color: "#aa0000", text: "برنس إمبراطوري 🏆🖤" },
        "king": { icon: "fas fa-crown", color: "#FF0000", text: "كنج الملك الملكي 👑❤️" },
        "honor": { icon: "fas fa-crown", color: "#0000FF", text: "انروا تاج الشرف 👑💙" },
        "admin": { icon: "fas fa-star", color: "#FFD700", text: "ادمان الإدارة العليا 👑💛" },
        "developer": { icon: "fas fa-code", color: "#00FF00", text: "مطور السيرفر 💻💚" },
        "diamond": { icon: "fas fa-gem", color: "#8A2BE2", text: "عضو ماسي 🔮" },
        "new": { icon: "fas fa-seedling", color: "#32CD32", text: "جديد" },
        "guest": { icon: "fas fa-user", color: "#ffffff", text: "زائر" }
    };

    window.rolesOrder = { 
        "owner": 1, "prince": 2, "king": 3, "honor": 4, "admin": 5, 
        "developer": 6, "diamond": 7, "new": 8, "guest": 9 
    };

    window.defaultOwnerData = { 
        uid: "owner_hassouni", name: "كاسر غرورك", role: "owner", level: 100, 
        img: "https://images.unsplash.com/photo-1535713875002-d1d0cf377fde?q=80&w=150", 
        nameBg: "rgba(255,215,0,0.15)", 
        cover: "https://images.unsplash.com/photo-1618005182384-a83a8bd57fbe?q=80&w=400",
        likes: 1000, age: 19, gender: "ذكر", country: "اليمن", status: "متصل بأناقة الملك الملكية 🏆", isMuted: false, isBanned: false
    };

    window.currentUser = null;
    window.tempUploadedCover = "";
    window.tempUploadedPfp = "";
    window.tempUploadedRoomBg = "";

    window.ui = {
        switchBranch: (id) => {
            document.querySelectorAll('.branch-content').forEach(c => c.style.display = 'none');
            document.querySelectorAll('.row-btn').forEach(b => b.classList.remove('active'));
            document.getElementById(id).style.display = 'block';
            document.getElementById('btn_' + id).classList.add('active');
        },
        showAuthBranchDirect: () => {
            document.getElementById('featureModalTitle').innerText = "🔑 تفعيل الحساب الفوري";
            document.getElementById('featureModalBody').innerHTML = `
                <div style="text-align:right;">
                    <input type="text" id="kName" class="form-control" placeholder="الاسم المستعار...">
                    <input type="email" id="kEmail" class="form-control" placeholder="البريد الإلكتروني المعتمد...">
                    <input type="password" id="kPass" class="form-control" placeholder="كلمة المرور...">
                    <button class="send-btn" style="width:100%; border-radius:8px;" onclick="ui.executeKeyActivation()">التسجيل الفوري برتبة ماسي 💎</button>
                </div>
            `;
            document.getElementById('featureModal').style.display = 'flex';
        },
        executeKeyActivation: () => {
            let n = document.getElementById('kName').value.trim();
            let em = document.getElementById('kEmail').value.trim();
            let ps = document.getElementById('kPass').value;
            if(!n || !em || !ps) { alert("يرجى إدخال البيانات كاملة."); return; }
            
            let token = "token_" + Date.now();
            if(em === "ghrwrkk2@gmail.com") {
                window.currentUser = { ...window.defaultOwnerData, name: n, sessionToken: token };
            } else {
                window.currentUser = { 
                    uid: "u_"+Date.now(), name: n, role: "diamond", level: 50, 
                    img: "https://cdn-icons-png.flaticon.com/512/1042/1042291.png", cover: "https://images.unsplash.com/photo-1618005182384-a83a8bd57fbe?q=400",
                    likes: 0, age: 20, gender: "ذكر", country: "عربي", status: "عضو ماسي جديد 💎", isMuted: false, isBanned: false, sessionToken: token
                };
            }
            ui.saveUserToFirestoreAndSession(window.currentUser);
            document.getElementById('featureModal').style.display = 'none';
            ui.enterChat();
        },
        loginAsGuest: () => {
            let n = document.getElementById('vName').value.trim();
            let a = document.getElementById('vAge').value;
            let g = document.getElementById('vGender').value;
            if(!n || !a || !g) { alert("يرجى ملء كافة حقول الزائر!"); return; }
            
            let token = "token_" + Date.now();
            window.currentUser = { 
                uid: "g_"+Date.now(), name: n, role: "guest", level: 1, 
                img: "https://cdn-icons-png.flaticon.com/512/1042/1042291.png", cover: "https://images.unsplash.com/photo-1618005182384-a83a8bd57fbe?q=400",
                likes: 0, age: a, gender: g, country: "اليمن", status: "زائر في شات حسوني", isMuted: false, isBanned: false, sessionToken: token
            };
            ui.saveUserToFirestoreAndSession(window.currentUser);
            ui.enterChat();
        },
        loginAsRegistered: (isNew) => {
            let userInp = isNew ? document.getElementById('rName').value.trim() : document.getElementById('logUser').value.trim();
            let passInp = isNew ? document.getElementById('rPass').value : document.getElementById('logPass').value;
            let genGender = isNew ? document.getElementById('rGender').value : "ذكر";

            if(!userInp || !passInp) { alert("البيانات ناقصة."); return; }

            let token = "token_" + Date.now();
            if(userInp === "ghrwrkk2@gmail.com" || passInp === "owner123") {
                window.currentUser = { ...window.defaultOwnerData, sessionToken: token };
            } else {
                window.currentUser = { 
                    uid: "u_"+Date.now(), name: userInp, role: "new", level: 5, 
                    img: "https://cdn-icons-png.flaticon.com/512/1042/1042291.png", cover: "https://images.unsplash.com/photo-1618005182384-a83a8bd57fbe?q=400",
                    likes: 0, age: 20, gender: genGender, country: "العالم العربي", status: "متواجد سحابياً", isMuted: false, isBanned: false, sessionToken: token
                };
            }
            ui.saveUserToFirestoreAndSession(window.currentUser);
            ui.enterChat();
        },
        saveUserToFirestoreAndSession: (userObj) => {
            localStorage.setItem("hassouni_user_session", JSON.stringify(userObj));
            db.collection("users").doc(userObj.uid).set(userObj, { merge: true });
        },
        checkSavedSessionOnLoad: () => {
            let savedUser = localStorage.getItem("hassouni_user_session");
            if(savedUser) {
                let parsedUser = JSON.parse(savedUser);
                db.collection("users").doc(parsedUser.uid).get().then((doc)=>{
                    if(doc.exists && doc.data().isBanned) {
                        alert("أنت محظور من دخول الشات.");
                        ui.logoutBackToWelcome();
                        return;
                    }
                    window.currentUser = doc.exists ? doc.data() : parsedUser;
                    document.getElementById('welcomeOverlay').style.display = 'none'; 
                    ui.enterChat();
                }).catch(() => {
                    window.currentUser = parsedUser;
                    ui.enterChat();
                });
            } else {
                document.getElementById('welcomeOverlay').style.display = 'flex';
                ui.switchBranch('b1');
            }
        },
        enterChat: () => {
            document.getElementById('welcomeOverlay').style.display = 'none';
            
            // إخفاء أو إظهار زر مفتاح التسجيل حسب الرتبة
            let aBtn = document.getElementById('authBtn');
            if(window.currentUser.role !== 'guest') {
                aBtn.style.display = 'none'; // يختفي تماماً لو مش زائر
            } else {
                aBtn.style.display = 'block';
                aBtn.querySelector('span').innerText = "تسجيل حساب";
            }

            db.collection("users").doc(window.currentUser.uid).update({ isOnline: true });
            
            // تفعيل المستمعات اللحظية بدون تكرار
            ui.listenToGlobalMessages();
            ui.listenToActiveMics();
            ui.listenToRoomSettings();
            ui.listenToSessionSecurity();
            ui.listenOnlineUsersRealtime();
        },
        listenToSessionSecurity: () => {
            db.collection("users").doc(window.currentUser.uid).onSnapshot((doc) => {
                if(doc.exists) {
                    let data = doc.data();
                    if(data.sessionToken && data.sessionToken !== window.currentUser.sessionToken) {
                        alert("تنبيه: تم فتح هذا الحساب من جهاز أو متصفح آخر!");
                        ui.logoutBackToWelcome();
                    }
                }
            });
        },
        listenToRoomSettings: () => {
            db.collection("room_settings").doc(window.currentRoom).onSnapshot((doc) => {
                if(doc.exists) {
                    let data = doc.data();
                    if(data.roomBg) document.getElementById('chatBox').style.backgroundImage = `url('${data.roomBg}')`;
                    
                    let ytContainer = document.getElementById('youtubeVideoFrameContainer');
                    if(data.activeAudioId) {
                        ytContainer.innerHTML = `<iframe width="100" height="100" src="https://www.youtube.com/embed/${data.activeAudioId}?autoplay=1&loop=1&playlist=${data.activeAudioId}" allow="autoplay"></iframe>`;
                    } else {
                        ytContainer.innerHTML = "";
                    }
                }
            });
        },
        listenToGlobalMessages: () => {
            db.collection("rooms").doc(window.currentRoom).collection("messages")
              .orderBy("timestamp", "asc")
              .onSnapshot((snapshot) => {
                  let chatBox = document.getElementById('chatBox');
                  chatBox.innerHTML = "";
                  snapshot.forEach((doc) => {
                      let mData = doc.data();
                      if (mData.user) ui.renderMsg(mData.user, mData.text, mData.timeStr);
                  });
              });
        },
        listenToActiveMics: () => {
            db.collection("rooms").doc(window.currentRoom).collection("mics").onSnapshot((snapshot) => {
                for(let i=1; i<=4; i++) {
                    let slot = document.getElementById(`mic_${i}`);
                    slot.classList.remove('occupied'); slot.style.backgroundImage = 'none';
                    document.getElementById(`micName_${i}`).innerText = `مايك ${i} فارغ`;
                    document.getElementById(`glow_${i}`).style.display = 'none';
                    document.getElementById(`mBadge_${i}`).style.display = 'none';
                }
                snapshot.forEach((doc) => {
                    let micData = doc.data();
                    let num = micData.micNum;
                    let slot = document.getElementById(`mic_${num}`);
                    slot.classList.add('occupied');
                    slot.style.backgroundImage = `url('${micData.userImg}')`;
                    document.getElementById(`micName_${num}`).innerText = micData.userName;
                    document.getElementById(`glow_${num}`).style.display = 'block';
                    if(micData.isMuted) {
                        document.getElementById(`mBadge_${num}`).style.display = 'block';
                    }
                });
            });
        },
        listenOnlineUsersRealtime: () => {
            db.collection("users").onSnapshot((snap) => {
                let list = []; 
                snap.forEach(doc => { if(doc.data().isOnline) list.push(doc.data()); });
                
                // ترتيب المتواجدين حسب وزن الرتبة (المالك أولاً والزوار في الأخير)
                list.sort((a, b) => (window.rolesOrder[a.role] || 99) - (window.rolesOrder[b.role] || 99));

                document.getElementById('onlineUsersListBody').innerHTML = list.map(u => {
                    let rObj = window.chatRanksData[u.role] || { icon: "fas fa-user", color: "#fff", text: "عضو" };
                    return `
                        <div class="menu-item" onclick="ui.viewProfileCard('${u.uid}')">
                            <span style="color:${rObj.color}; font-weight: bold;"><i class="${rObj.icon}"></i> ${u.name}</span>
                            <span style="font-size:11px; color:${rObj.color}; border: 1px solid ${rObj.color}; padding:2px 5px; border-radius:10px;">${rObj.text}</span>
                        </div>
                    `;
                }).join('');
            });
        },
        sendMessage: () => {
            if(window.currentUser.isMuted) { alert("أنت مكتوم!"); return; }
            let inp = document.getElementById('msgInp');
            let t = inp.value.trim(); if(!t) return;
            inp.value = '';
            
            let d = new Date();
            let timeStr = d.getHours() + ":" + (d.getMinutes()<10?'0':'') + d.getMinutes();

            db.collection("users").doc(window.currentUser.uid).get().then(doc => {
                let u = doc.exists ? doc.data() : window.currentUser;
                db.collection("rooms").doc(window.currentRoom).collection("messages").add({
                    user: { uid: u.uid, name: u.name, role: u.role, img: u.img },
                    text: t,
                    timeStr: timeStr,
                    timestamp: firebase.firestore.FieldValue.serverTimestamp()
                });
            });
        },
        renderMsg: (user, text, time) => {
            let div = document.createElement('div');
            div.className = 'msg-wrap';
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
                <div class="msg-time">${time || ''}</div>
            `;
            let box = document.getElementById('chatBox');
            box.appendChild(div); box.scrollTop = box.scrollHeight;
        },
        clickMicSlot: (num) => {
            window.selectedMicNum = num;
            db.collection("rooms").doc(window.currentRoom).collection("mics").doc(`mic_${num}`).get().then(doc => {
                if(!doc.exists) {
                    // المايك فارغ؛ يمكن الصعود
                    document.getElementById('featureModalTitle').innerText = "🎙️ حجز المصطبة الصوتية";
                    document.getElementById('featureModalBody').innerHTML = `
                        <p style="text-align:center;">هل ترغب بالصعود الفوري على مايك رقم [ ${num} ]؟</p>
                        <button class="send-btn" style="width:100%; margin-top:10px;" onclick="ui.confirmMicGoingUp(true)">تأكيد الصعود</button>
                    `;
                    document.getElementById('featureModal').style.display = 'flex';
                } else {
                    // المايك مشغول
                    let data = doc.data();
                    if(data.userId !== window.currentUser.uid && window.currentUser.role !== 'owner') {
                        alert("لا يمكنك الصعود، المايك الحالي مشغول!");
                        return;
                    }
                    
                    // إعدادات المايك المشغول (لصاحب المايك أو المالك المطلق)
                    document.getElementById('featureModalTitle').innerText = "🎛️ إدارة بث المايك واليوتيوب";
                    let isMusicPlaying = data.youtubeActive || false;
                    
                    document.getElementById('featureModalBody').innerHTML = `
                        <div class="menu-item" onclick="ui.toggleMicMuteState(${num}, ${!data.isMuted})"><i class="fas fa-microphone-slash"></i> كتم/إلغاء كتم الصوت</div>
                        <div class="menu-item" onclick="ui.vacateMicSlot(${num})" style="color:#e74c3c;"><i class="fas fa-sign-out-alt"></i> النزول فوراً من المايك</div>
                    `;
                    document.getElementById('featureModal').style.display = 'flex';
                }
            });
        },
        confirmMicGoingUp: (status) => {
            document.getElementById('featureModal').style.display = 'none';
            if(!status) return;
            let num = window.selectedMicNum;
            db.collection("rooms").doc(window.currentRoom).collection("mics").doc(`mic_${num}`).set({
                micNum: num, userId: window.currentUser.uid, userName: window.currentUser.name,
                userImg: window.currentUser.img, isMuted: false, youtubeActive: false, audioOwner: window.currentUser.uid
            });
        },
        toggleMicMuteState: (num, state) => {
            db.collection("rooms").doc(window.currentRoom).collection("mics").doc(`mic_${num}`).update({ isMuted: state });
            document.getElementById('featureModal').style.display = 'none';
        },
        vacateMicSlot: (num) => {
            db.collection("rooms").doc(window.currentRoom).collection("mics").doc(`mic_${num}`).delete();
            document.getElementById('featureModal').style.display = 'none';
        },
        openYouTubeSearchEngine: () => {
            // التحقق من صلاحية تشغيل اليوتيوب
            db.collection("room_settings").doc(window.currentRoom).get().then(doc => {
                let currentAudioOwner = doc.exists ? doc.data().audioOwner : "";
                let isOwner = (window.currentUser.role === 'owner' || window.currentUser.role === 'admin');
                
                if(currentAudioOwner && currentAudioOwner !== window.currentUser.uid && !isOwner) {
                    alert("عذراً، الأغنية الحالية مشغلة بواسطة عضو آخر ولا يمكنك التحكم بها إلا الأونر والادارة فقط!");
                    return;
                }
                
                document.getElementById('featureModalTitle').innerText = "📺 مشغل شيلات يوتيوب الموحد";
                document.getElementById('featureModalBody').innerHTML = `
                    <input type="text" id="ytLinkInput" class="form-control" placeholder="ضع رابط اليوتيوب هنا لتشغيله للجميع..." oninput="ui.previewYoutubeTrack()">
                    <div id="ytSearchPreviewContainer"></div>
                `;
                document.getElementById('featureModal').style.display = 'flex';
            });
        },
        previewYoutubeTrack: () => {
            let url = document.getElementById('ytLinkInput').value.trim();
            let regExp = /^.*(youtu.be\/|v\/|u\/\w\/|embed\/|watch\?v=|\&v=)([^#\&\?]*).*/;
            let match = url.match(regExp);
            let videoId = (match && match[2].length === 11) ? match[2] : null;
            
            if(videoId) {
                document.getElementById('ytSearchPreviewContainer').innerHTML = `
                    <div class="yt-preview-card" onclick="ui.playYoutubeForAll('${videoId}')">
                        <i class="fab fa-youtube style="color:red; font-size:24px;"></i>
                        <span style="color:#fff; font-size:12px;">🎵 تم العثور على المقطع المزامر. اضغط هنا لبثه فوراً لجميع الأعضاء!</span>
                    </div>
                `;
            }
        },
        playYoutubeForAll: (vId) => {
            db.collection("room_settings").doc(window.currentRoom).set({
                activeAudioId: vId,
                audioOwner: window.currentUser.uid
            }, { merge: true }).then(() => {
                alert("تم إطلاق البث والتحكم الصوتي لكافة المتصفحات بنجاح!");
                document.getElementById('featureModal').style.display = 'none';
            });
        },
        viewProfileCard: (uid) => {
            db.collection("users").doc(uid).get().then((doc) => {
                if(!doc.exists) return;
                let u = doc.data();
                let isMeOrOwner = (window.currentUser.uid === uid || window.currentUser.role === 'owner');
                let rObj = window.chatRanksData[u.role] || { icon: "fas fa-user", color: "#fff", text: "عضو" };

                document.getElementById('featureModalTitle').innerText = "بطاقة البروفايل الإمبراطورية";
                document.getElementById('featureModalBody').innerHTML = `
                    <div class="profile-card-wrapper">
                        ${isMeOrOwner ? `<div class="profile-edit-pencil" onclick="ui.openEditProfileModal('${uid}')"><i class="fas fa-pencil-alt"></i></div>` : ''}
                        <img src="${u.cover || 'https://images.unsplash.com/photo-1618005182384-a83a8bd57fbe?q=80&w=400'}" class="profile-card-cover">
                        <img src="${u.img}" class="profile-card-pfp">
                        <h2 style="color:${rObj.color}; margin:5px 0;">${u.name}</h2>
                        <p style="color:${rObj.color}; font-size:12px;"><i class="${rObj.icon}"></i> ${rObj.text}</p>
                        <p style="color:#aaa; font-size:11px;">${u.status || 'لا يوجد حالة بعد'}</p>
                        
                        <div class="profile-details-grid">
                            <div class="profile-grid-row"><span>العمر:</span><span>${u.age || 'غير محدد'}</span></div>
                            <div class="profile-grid-row"><span>الجنس:</span><span>${u.gender || 'غير مححدد'}</span></div>
                            <div class="profile-grid-row"><span>البلد:</span><span>${u.country || 'اليمن'}</span></div>
                        </div>
                    </div>
                `;
                document.getElementById('featureModal').style.display = 'flex';
            });
        },
        openEditProfileModal: (uid) => {
            db.collection("users").doc(uid).get().then((doc) => {
                let u = doc.data();
                window.tempUploadedCover = u.cover || "";
                window.tempUploadedPfp = u.img || "";
                
                document.getElementById('featureModalTitle').innerText = "تعديل الملف الشخصي والجنس";
                document.getElementById('featureModalBody').innerHTML = `
                    <div style="text-align:right;">
                        <label class="file-input-label"><input type="file" class="file-input-hidden" accept="image/*" onchange="ui.processLocalFile(this, 'cover')">📁 رفع صورة الغلاف من الجهاز</label>
                        <label class="file-input-label"><input type="file" class="file-input-hidden" accept="image/*" onchange="ui.processLocalFile(this, 'pfp')">📷 رفع الصورة الشخصية من الجهاز</label>
                        
                        <label style="font-size:12px; color:var(--gold);">الاسم (مزخرف):</label>
                        <input type="text" id="editName" class="form-control" value="${u.name || ''}">
                        
                        <label style="font-size:12px; color:var(--gold);">الحالة الشخصية:</label>
                        <input type="text" id="editStatus" class="form-control" value="${u.status || ''}">
                        
                        <label style="font-size:12px; color:var(--gold);">الجنس:</label>
                        <select id="editGender" class="form-select">
                            <option value="ذكر" ${u.gender==='ذكر'?'selected':''}>ذكر</option>
                            <option value="أنثى" ${u.gender==='أنثى'?'selected':''}>أنثى</option>
                        </select>
                        
                        <button class="send-btn" style="width:100%;" onclick="ui.saveProfileEdits('${uid}')">حفظ المزامنة الفورية</button>
                    </div>
                `;
            });
        },
        processLocalFile: (input, type) => {
            let file = input.files[0]; if(!file) return;
            let r = new FileReader();
            r.onload = (e) => {
                if(type==='cover') { window.tempUploadedCover = e.target.result; alert("تم تحميل الغلاف محلياً جاهز للحفظ!"); }
                if(type==='pfp') { window.tempUploadedPfp = e.target.result; alert("تم تحميل الرمزية محلياً جاهزة للحفظ!"); }
                if(type==='roomBg') { window.tempUploadedRoomBg = e.target.result; alert("تم تحميل خلفية الروم محلياً!"); }
            };
            r.readAsDataURL(file);
        },
        saveProfileEdits: (uid) => {
            let upd = {
                cover: window.tempUploadedCover,
                img: window.tempUploadedPfp,
                name: document.getElementById('editName').value.trim(),
                status: document.getElementById('editStatus').value.trim(),
                gender: document.getElementById('editGender').value
            };
            db.collection("users").doc(uid).update(upd).then(() => {
                alert("تم تحديث كافة التعديلات وظهرت للجميع فوراً!");
                if(window.currentUser.uid === uid) {
                    window.currentUser = { ...window.currentUser, ...upd };
                    localStorage.setItem("hassouni_user_session", JSON.stringify(window.currentUser));
                }
                document.getElementById('featureModal').style.display = 'none';
            });
        },
        openGlobalSettings: () => {
            document.getElementById('featureModalTitle').innerText = "لوحة تحكم الغرفة العامة";
            let isOwner = (window.currentUser.role === 'owner');
            
            let controls = isOwner ? `
                <div style="text-align:right; border-top:1px solid var(--gold); padding-top:10px;">
                    <p style="color:var(--gold); font-size:12px; font-weight:bold;">🛠️ صلاحيات البرنس الأصلي الحصرية:</p>
                    <label class="file-input-label"><input type="file" class="file-input-hidden" accept="image/*" onchange="ui.processLocalFile(this, 'roomBg')">📁 رفع خلفية الروم العامة من الملفات</label>
                    <button class="send-btn" style="width:100%; margin-bottom:10px;" onclick="ui.saveCloudRoomBg()">تطبيق الخلفية للجميع فوراً</button>
                    <button class="send-btn" style="width:100%; background:#e74c3c; color:#fff;" onclick="ui.cleanRoomMessages()">🧼 تنظيف الروم ومسح المحادثات</button>
                </div>
            ` : '';

            document.getElementById('featureModalBody').innerHTML = `
                ${controls}
                <div class="menu-item" style="color:#e74c3c;" onclick="ui.logoutBackToWelcome()"><i class="fas fa-sign-out-alt"></i> تسجيل خروج من النظام</div>
            `;
            document.getElementById('featureModal').style.display = 'flex';
        },
        saveCloudRoomBg: () => {
            if(!window.tempUploadedRoomBg) { alert("الرجاء اختيار صورة أولاً!"); return; }
            db.collection("room_settings").doc(window.currentRoom).set({ roomBg: window.tempUploadedRoomBg }, { merge: true }).then(() => {
                alert("تم تعميم خلفية الروم الجديدة وتحديثها لجميع الأعضاء فوراً!");
                document.getElementById('featureModal').style.display = 'none';
            });
        },
        cleanRoomMessages: () => {
            if(confirm("هل أنت متأكد من مسح وتنظيف كافة رسائل الروم الموحد؟")) {
                db.collection("rooms").doc(window.currentRoom).collection("messages").get().then(snap => {
                    snap.forEach(d => d.ref.delete());
                    alert("تم تنظيف الروم بنجاح كامل.");
                    document.getElementById('featureModal').style.display = 'none';
                });
            }
        },
        openRoomsManager: () => {
            document.getElementById('featureModalTitle').innerText = "الغرف السحابية";
            let isOwner = (window.currentUser.role === 'owner');
            
            // مفتاح وحقل إنشاء غرف مخفي تماماً لا يظهر إلا للأونر
            let createBox = isOwner ? `
                <div style="padding:10px; border-bottom:1px solid #333;">
                    <input type="text" id="newRoomNameInp" class="form-control" placeholder="اسم الغرفة الجديدة...">
                    <button class="send-btn" style="width:100%;" onclick="ui.createNewRoomCloud()">➕ إنشاء الغرفة سحابياً</button>
                </div>
            ` : '';

            document.getElementById('featureModalBody').innerHTML = `
                ${createBox}
                <div id="roomsContainerList" style="margin-top:10px;">
                    ${window.roomsList.map(r => `<div class="menu-item" onclick="ui.changeActiveRoom('${r}')">${r} ${window.currentRoom === r ? '🏆' : ''}</div>`).join('')}
                </div>
            `;
            document.getElementById('featureModal').style.display = 'flex';
        },
        createNewRoomCloud: () => {
            let rName = document.getElementById('newRoomNameInp').value.trim();
            if(!rName) return;
            if(!window.roomsList.includes(rName)) {
                window.roomsList.push(rName);
                alert(`تم إنشاء غرفة [ ${rName} ] بنجاح وتثبيتها للأونر.`);
                ui.openRoomsManager();
            }
        },
        changeActiveRoom: (r) => { 
            window.currentRoom = r; 
            document.getElementById('chatBox').innerHTML = ""; 
            document.getElementById('featureModal').style.display = 'none'; 
            ui.enterChat();
        },
        toggleOnlineUsers: () => {
            let m = document.getElementById('onlineUsersHalfModal');
            m.style.display = (m.style.display === 'block') ? 'none' : 'block';
        },
        refreshChatWindowOnly: () => { window.location.reload(); },
        logoutBackToWelcome: () => {
            if(window.currentUser) db.collection("users").doc(window.currentUser.uid).update({ isOnline: false });
            localStorage.removeItem("hassouni_user_session");
            setTimeout(() => { window.location.reload(); }, 300);
        },
        openVIPList: (t) => alert(`قائمة ${t} مؤمنة ونشطة`)
    };

    window.onload = () => { ui.checkSavedSessionOnLoad(); };
</script>
</body>
</html>
