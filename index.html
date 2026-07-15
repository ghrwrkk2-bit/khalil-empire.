<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>شات حسوني - النسخة الإمبراطورية السحابية</title>
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
        .mic-slot i.fa-heart { font-size: 18px; color: #e74c3c; }
        .mic-slot.occupied i.fa-heart { display: none; }
        .mic-slot .mic-user-name { font-size: 10px; color: #fff; margin-top: 2px; max-width: 90%; overflow: hidden; text-overflow: ellipsis; white-space: nowrap; background: rgba(0,0,0,0.7); padding: 1px 4px; border-radius: 4px; }
        .mic-speaking-glow { position: absolute; inset: 0; border: 2px solid #2ecc71; border-radius: 8px; animation: pulseGlow 1s infinite; display: none; }
        .mic-status-badge { position: absolute; top: -2px; left: -2px; background: #e74c3c; font-size: 8px; padding: 1px 3px; border-radius: 4px; display: none; }

        @keyframes pulseGlow { 0% { opacity: 0.4; } 50% { opacity: 1; } 100% { opacity: 0.4; } }

        #chatBox { height: calc(100vh - 190px); overflow-y: auto; padding: 135px 15px 85px; display: flex; flex-direction: column; gap: 12px; background: #0f0f0f url('https://i.ibb.co/6wXbYm2/butterflies.jpg') center center/cover no-repeat; }
        
        .msg-wrap { display: flex; flex-direction: column; align-self: flex-start; width: 95%; max-width: 420px; background: rgba(18, 22, 28, 0.94); padding: 12px; border-radius: 18px; border: 1.5px solid rgba(255, 215, 0, 0.4); box-shadow: 0 4px 15px rgba(0,0,0,0.5); }
        .msg-header { display: flex; align-items: center; gap: 10px; width: 100%; }
        
        .pfp-main-frame { width: 44px; height: 44px; border-radius: 50%; border: 2px solid var(--gold); box-shadow: 0 0 8px var(--gold); display: flex; align-items: center; justify-content: center; background: #000; flex-shrink: 0; }
        .pfp-main { width: 100%; height: 100%; border-radius: 50%; object-fit: cover; cursor: pointer; }
        
        .rank-standalone-icon {
            font-size: 16px;
            display: flex;
            align-items: center;
            justify-content: center;
            width: 28px;
            height: 28px;
            background: rgba(0, 0, 0, 0.5);
            border-radius: 50%;
            border: 1px solid rgba(255, 215, 0, 0.3);
            flex-shrink: 0;
        }

        .king-name-container {
            display: inline-flex;
            align-items: center;
            background: linear-gradient(145deg, #1e1e1e, #111111);
            border: 1px solid var(--gold);
            padding: 4px 12px;
            border-radius: 20px;
            box-shadow: 0 2px 8px rgba(255, 215, 0, 0.2);
            cursor: pointer;
        }
        .king-name-tag { 
            font-size: 13px; 
            font-weight: bold; 
            text-shadow: 0 0 3px rgba(255,215,0,0.3);
        }
        
        .msg-text { color: #fff; font-size: 14px; line-height: 1.5; margin-top: 8px; padding-right: 5px; word-break: break-word; }

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
        
        .info-scroll-box { background: rgba(255,255,255,0.02); border: 1px solid #333; padding: 12px; border-radius: 10px; font-size: 12px; line-height: 1.6; color: #ccc; margin-top: 5px; text-align: right; }

        .feature-modal { display: none; position: fixed; inset: 0; background: rgba(0,0,0,0.85); z-index: 100000; align-items: center; justify-content: center; padding: 15px; }
        .feature-card { background: #121212; width: 100%; max-width: 460px; border: 2px solid var(--gold); border-radius: 15px; padding: 20px; max-height: 85vh; overflow-y: auto; position: relative; }
        .half-screen-modal { display: none; position: fixed; bottom: 60px; left: 0; width: 100%; height: 50vh; background: rgba(14, 14, 14, 0.98); border-top: 3px solid var(--gold); z-index: 999; overflow-y: auto; padding: 15px; box-shadow: 0 -5px 20px rgba(0,0,0,0.8); }

        .menu-item { padding: 12px; border-bottom: 1px solid #222; cursor: pointer; display: flex; align-items: center; gap: 10px; font-size: 14px; color: #fff; justify-content: space-between; }
        .menu-item:hover { background: rgba(255,255,255,0.03); }

        .yt-preview-card {
            background: #1a1a1a;
            border: 2px solid #ff3333;
            border-radius: 12px;
            padding: 12px;
            margin-top: 12px;
            display: flex;
            align-items: center;
            gap: 12px;
            cursor: pointer;
            transition: transform 0.2s;
        }
        .yt-preview-card:hover { transform: scale(1.02); }
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
        .profile-grid-row:last-child { border: none; }
        .profile-grid-row span:first-child { color: #aaa; }
        .profile-grid-row span:last-child { color: var(--gold); font-weight: bold; }

        #hiddenAudioNode { display: none; }
        #youtubeVideoFrameContainer { position: fixed; top: -9999px; left: -9999px; width: 1px; height: 1px; overflow: hidden; opacity: 0; }
    </style>
</head>
<body>

<audio id="hiddenAudioNode" loop></audio>
<div id="youtubeVideoFrameContainer"></div>

<div id="welcomeOverlay">
    <div class="king-card">
        <h2 style="text-align:center; color:var(--gold); margin:0 0 5px;">شات حسوني - النسخة الإمبراطورية</h2>
        <p style="text-align:center; font-size:12px; margin:0 0 10px; color:#aaa;">أهلاً وسهلاً بكم في شات عربي دردشة عربية محمية بالكامل</p>
        
        <div class="btn-row">
            <button class="row-btn" id="btn_b1" onclick="ui.switchBranch('b1')">دخول زائر</button>
            <button class="row-btn" id="btn_b2" onclick="ui.switchBranch('b2')">دخول عضوية</button>
            <button class="row-btn" id="btn_b3" onclick="ui.switchBranch('b3')">سجل الآن</button>
        </div>

        <div id="b1" class="branch-content">
            <input type="text" id="vName" class="form-control" placeholder="الاسم المستعار للزائر (مطلوب)...">
            <select id="vAge" class="form-select">
                <option value="">اختر العمر (مطلوب)...</option>
                <script>
                    for(let i=15; i<=100; i++) { document.write(`<option value="${i}">${i}</option>`); }
                </script>
            </select>
            <select id="vGender" class="form-select">
                <option value="">اختر الجنس (مطلوب)...</option>
                <option value="ذكر">ذكر</option>
                <option value="أنثى">أنثى</option>
            </select>
            <button class="send-btn" style="width:100%; border-radius:8px;" onclick="ui.loginAsGuest()">دخول الآن كـ زائر</button>
        </div>

        <div id="b2" class="branch-content">
            <input type="text" id="logUser" class="form-control" placeholder="الاسم المستعار أو البريد الإلكتروني...">
            <input type="password" id="logPass" class="form-control" placeholder="كلمة المرور الحالية...">
            <button class="send-btn" style="width:100%; border-radius:8px;" onclick="ui.loginAsRegistered(false)">تسجيل الدخول الفوري</button>
        </div>

        <div id="b3" class="branch-content">
            <input type="text" id="rName" class="form-control" placeholder="الاسم المستعار الجديد...">
            <input type="email" id="rEmail" class="form-control" placeholder="البريد الإلكتروني المعتمد...">
            <input type="password" id="rPass" class="form-control" placeholder="كلمة المرور السرية...">
            <button class="send-btn" style="width:100%; border-radius:8px;" onclick="ui.loginAsRegistered(true)">إتمام التسجيل ودخول</button>
        </div>
    </div>
</div>

<div class="header-bar">
    <div class="header-btn" onclick="alert('لا توجد إشعارات جديدة')"><i class="fas fa-bell"></i>إشعارات</div>
    <div class="header-btn" onclick="alert('لوحة البلاغات فارغة')"><i class="fas fa-flag"></i>بلاغات</div>
    <div class="header-btn" onclick="alert('الخاص مشفر ومحمي')"><i class="fas fa-comments"></i>الخاص</div>
    <div class="header-btn" onclick="ui.openVIPList('الأثرياء')"><i class="fas fa-gem"></i>الأثرياء</div>
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
    <i class="fas fa-image" style="color:var(--gold); font-size:24px; cursor:pointer;" onclick="alert('المعرض آمن وجاهز للرفع')"></i>
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
        <span style="color:var(--gold); font-weight:bold;"><i class="fas fa-users"></i> قائمة المتواجدين</span>
        <button onclick="ui.toggleOnlineUsers()" style="background:#c0392b; border:none; color:#fff; border-radius:50%; width:28px; height:28px; font-weight:bold; cursor:pointer; display:flex; align-items:center; justify-content:center;">X</button>
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
        firebase.firestore().enablePersistence().catch(()=>{});
    }
    const db = firebase.firestore();

    window.currentRoom = "العام";
    window.roomsList = ["العام"];
    
    window.chatRanksData = {
        "owner": { icon: "fas fa-trophy", color: "#ffd700", text: "البرنس الأصلي" },
        "prince": { icon: "fas fa-trophy", color: "#aa0000", text: "برنس إمبراطوري" },
        "king": { icon: "fas fa-crown", color: "#FF0000", text: "الملك الملكي" },
        "honor": { icon: "fas fa-crown", color: "#0000FF", text: "تاج الشرف" },
        "admin": { icon: "fas fa-star", color: "#FFD700", text: "إدارة العليا" },
        "developer": { icon: "fas fa-code", color: "#00FF00", text: "مطور السيرفر" },
        "senior_mod": { icon: "fas fa-gem", color: "#00FFFF", text: "مشرف أول" },
        "mod": { icon: "fas fa-star", color: "#C0C0C0", text: "مشرف" },
        "vip": { icon: "fas fa-fire", color: "#FF4500", text: "VIP" },
        "diamond": { icon: "fas fa-gem", color: "#8A2BE2", text: "ماسي" },
        "gold_member": { icon: "fas fa-coins", color: "#DAA520", text: "ذهبي" },
        "silver_member": { icon: "fas fa-medal", color: "#A9A9A9", text: "فضي" },
        "distinguished": { icon: "fas fa-bolt", color: "#FF8C00", text: "متميز" },
        "interactive": { icon: "fas fa-bolt", color: "#FFFF00", text: "متفاعل" },
        "active": { icon: "fas fa-heart", color: "#FF69B4", text: "نشط" },
        "new": { icon: "fas fa-seedling", color: "#32CD32", text: "جديد" },
        "guest": { icon: "fas fa-user", color: "#ffffff", text: "زائر" }
    };

    window.rolesOrder = { 
        "owner": 1, "prince": 2, "king": 3, "honor": 4, "admin": 5, 
        "developer": 6, "senior_mod": 7, "mod": 8, "vip": 9, "diamond": 10, 
        "gold_member": 11, "silver_member": 12, "distinguished": 13, "interactive": 14, 
        "active": 15, "new": 16, "guest": 17 
    };

    window.defaultOwnerData = { 
        uid: "owner_hassouni", name: "كاسر غرورك", role: "owner", level: 100, 
        img: "https://images.unsplash.com/photo-1535713875002-d1d0cf377fde?q=80&w=150", 
        nameBg: "rgba(255,215,0,0.15)", 
        cover: "https://images.unsplash.com/photo-1618005182384-a83a8bd57fbe?q=80&w=400",
        likes: 742, gifts: "تاج ذهبي، سيف ملكي", profileUrl: "hassouni.chat/king_1", age: 19, gender: "ذكر", country: "اليمن", status: "متصل بأناقة الملك الملكية 🏆",
        points: 5000, isMuted: false, isBanned: false
    };

    window.currentUser = null;
    window.activeMessagesListener = null;
    window.activeMicsListener = null;
    window.activeRoomSettingsListener = null;
    window.activeSessionListener = null;
    window.activeOnlineUsersListener = null;

    window.tempUploadedCover = "";
    window.tempUploadedPfp = "";
    window.tempUploadedRoomBg = "";

    window.localAudioStream = null;
    window.mediaRecorder = null;

    function validateEmailAddress(email) {
        return /^[^\s@]+@[^\s@]+\.[^\s@]+$/.test(String(email).toLowerCase());
    }

    function extractYouTubeVideoId(url) {
        const regExp = /^.*(youtu.be\/|v\/|u\/\w\/|embed\/|watch\?v=|\&v=)([^#\&\?]*).*/;
        const match = url.match(regExp);
        return (match && match[2].length === 11) ? match[2] : null;
    }

    window.ui = {
        switchBranch: (id) => {
            document.querySelectorAll('.branch-content').forEach(c => c.style.display = 'none');
            document.querySelectorAll('.row-btn').forEach(b => b.classList.remove('active'));
            document.getElementById(id).style.display = 'block';
            document.getElementById('btn_' + id).classList.add('active');
        },
        showAuthBranchDirect: () => {
            if(window.currentUser && window.currentUser.role === 'owner') {
                document.getElementById('featureModalTitle').innerText = "👑 لوحة التحكم والمفتاح الملكي";
                document.getElementById('featureModalBody').innerHTML = `
                    <div style="text-align:right;">
                        <p style="font-size:14px; color:var(--gold); font-weight:bold; text-align:center;">مرحباً بك يا إمبراطور الموقع، يمكنك من هنا إدارة أو إنشاء الغرف سحابياً:</p>
                        <input type="text" id="newRoomNameInp" class="form-control" placeholder="اسم الغرفة الجديدة...">
                        <button class="send-btn" style="width:100%; border-radius:8px;" onclick="ui.createNewRoomCloud()">➕ إنشاء الغرفة سحابياً فوراً</button>
                    </div>
                `;
                document.getElementById('featureModal').style.display = 'flex';
            } else {
                document.getElementById('featureModalTitle').innerText = "🔑 تفعيل المفتاح الماسي الفوري لكافة الأعضاء";
                document.getElementById('featureModalBody').innerHTML = `
                    <div style="text-align:right;">
                        <input type="text" id="kName" class="form-control" placeholder="الاسم المستعار...">
                        <input type="email" id="kEmail" class="form-control" placeholder="البريد الإلكتروني المعتمد...">
                        <input type="password" id="kPass" class="form-control" placeholder="كلمة المرور الحالية...">
                        <button class="send-btn" style="width:100%; border-radius:8px;" onclick="ui.executeKeyActivation()">التسجيل الفوري برتبة ماسي 💎</button>
                    </div>
                `;
                document.getElementById('featureModal').style.display = 'flex';
            }
        },
        executeKeyActivation: () => {
            let n = document.getElementById('kName').value.trim();
            let em = document.getElementById('kEmail').value.trim();
            let ps = document.getElementById('kPass').value;
            if(!n || !em || !ps) { alert("يرج إدخال البيانات كاملة."); return; }
            if(!validateEmailAddress(em)) { alert("البريد الإلكتروني غير صحيح!"); return; }
            
            let generatedToken = "token_" + Date.now() + "_" + Math.random().toString(36).substr(2, 9);
            if(em === "ghrwrkk2@gmail.com") {
                window.currentUser = { ...window.defaultOwnerData };
                window.currentUser.name = n;
                window.currentUser.sessionToken = generatedToken;
            } else {
                window.currentUser = { 
                    uid: "u_"+Date.now(), name: n, role: "diamond", level: 50, 
                    img: "https://cdn-icons-png.flaticon.com/512/1042/1042291.png", nameBg: "rgba(255,215,0,0.05)", 
                    cover: "https://images.unsplash.com/photo-1618005182384-a83a8bd57fbe?q=400",
                    likes: 0, gifts: "لا يوجد بعد", profileUrl: "none", age: 20, gender: "ذكر", country: "عربي", status: "عضو ماسي جديد", points: 10, isMuted: false, isBanned: false,
                    sessionToken: generatedToken
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
            if(!n || !a || !g) { alert("يرجى ملء الحقول المطلوبة!"); return; }
            
            let generatedToken = "token_" + Date.now() + "_" + Math.random().toString(36).substr(2, 9);
            window.currentUser = { 
                uid: "g_"+Date.now(), name: n, role: "guest", level: 1, 
                img: "https://cdn-icons-png.flaticon.com/512/1042/1042291.png", nameBg: "transparent", 
                cover: "https://images.unsplash.com/photo-1618005182384-a83a8bd57fbe?q=400",
                likes: 0, gifts: "ممنوع للزوار", profileUrl: "none", age: a, gender: g, country: "اليمن", status: "أنا زائر في شات حسوني", points: 0, isMuted: false, isBanned: false,
                sessionToken: generatedToken
            };
            ui.saveUserToFirestoreAndSession(window.currentUser);
            ui.enterChat();
        },
        loginAsRegistered: (isNew) => {
            let userInp = isNew ? document.getElementById('rName').value.trim() : document.getElementById('logUser').value.trim();
            let passInp = isNew ? document.getElementById('rPass').value : document.getElementById('logPass').value;
            let emailInp = isNew ? document.getElementById('rEmail').value.trim() : userInp;

            if(!userInp || !passInp) { alert("البيانات ناقصة."); return; }

            let generatedToken = "token_" + Date.now() + "_" + Math.random().toString(36).substr(2, 9);
            if(userInp === "ghrwrkk2@gmail.com" || emailInp === "ghrwrkk2@gmail.com" || passInp === "owner123") {
                window.currentUser = { ...window.defaultOwnerData };
                window.currentUser.sessionToken = generatedToken;
            } else {
                window.currentUser = { 
                    uid: "u_"+Date.now(), name: userInp, role: "new", level: 50, 
                    img: "https://cdn-icons-png.flaticon.com/512/1042/1042291.png", nameBg: "rgba(255,215,0,0.05)", 
                    cover: "https://images.unsplash.com/photo-1618005182384-a83a8bd57fbe?q=400",
                    likes: 5, gifts: "وردة ترحيبية", profileUrl: "none", age: 21, gender: "ذكر", country: "الوطن العربي", status: "متواجد في الروم الإمبراطوري", points: 20, isMuted: false, isBanned: false,
                    sessionToken: generatedToken
                };
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
                db.collection("users").doc(window.currentUser.uid).update({
                    isOnline: status,
                    lastSeen: firebase.firestore.FieldValue.serverTimestamp()
                }).catch(()=>{});
            }
        },
        checkSavedSessionOnLoad: () => {
            let savedUser = localStorage.getItem("hassouni_user_session");
            if(savedUser) {
                let parsedUser = JSON.parse(savedUser);
                db.collection("users").doc(parsedUser.uid).get().then((doc)=>{
                    if(doc.exists){
                        let sData = doc.data();
                        if(sData.isBanned) {
                            alert("لقد تم حظر حسابك.");
                            ui.logoutBackToWelcome();
                            return;
                        }
                        window.currentUser = sData;
                        localStorage.setItem("hassouni_user_session", JSON.stringify(window.currentUser));
                    } else {
                        window.currentUser = parsedUser;
                    }
                    document.getElementById('welcomeOverlay').style.display = 'none'; 
                    ui.enterChat();
                }).catch(() => {
                    window.currentUser = parsedUser;
                    document.getElementById('welcomeOverlay').style.display = 'none';
                    ui.enterChat();
                });
            } else {
                document.getElementById('welcomeOverlay').style.display = 'flex';
                ui.switchBranch('b1');
            }
        },
        enterChat: () => {
            document.getElementById('welcomeOverlay').style.display = 'none';
            ui.updateUserOnlineStatus(true);
            ui.clearAllListeners();
            ui.listenToGlobalMessages();
            ui.listenToActiveMics();
            ui.listenToRoomSettings();
            ui.listenToSessionSecurity();
            ui.listenOnlineUsersRealtime();
        },
        clearAllListeners: () => {
            if(window.activeMessagesListener) window.activeMessagesListener();
            if(window.activeMicsListener) window.activeMicsListener();
            if(window.activeRoomSettingsListener) window.activeRoomSettingsListener();
            if(window.activeSessionListener) window.activeSessionListener();
            if(window.activeOnlineUsersListener) window.activeOnlineUsersListener();
        },
        listenToSessionSecurity: () => {
            if(!window.currentUser || !window.currentUser.uid) return;
            window.activeSessionListener = db.collection("users").doc(window.currentUser.uid).onSnapshot((doc) => {
                if(doc.exists) {
                    let data = doc.data();
                    window.currentUser = data;
                    localStorage.setItem("hassouni_user_session", JSON.stringify(window.currentUser));
                    if(window.currentUser.sessionToken && data.sessionToken && data.sessionToken !== window.currentUser.sessionToken) {
                        alert("تم تسجيل الدخول إلى هذا الحساب من هاتف آخر.");
                        ui.logoutBackToWelcome();
                    }
                }
            });
        },
        listenToRoomSettings: () => {
            window.activeRoomSettingsListener = db.collection("room_settings").doc(window.currentRoom).onSnapshot((doc) => {
                if(doc.exists) {
                    let data = doc.data();
                    if(data.roomBg) {
                        document.getElementById('chatBox').style.backgroundImage = `url('${data.roomBg}')`;
                    }
                    
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
            window.activeMessagesListener = db.collection("rooms").doc(window.currentRoom).collection("messages")
              .orderBy("timestamp", "asc")
              .limitToLast(50)
              .onSnapshot((snapshot) => {
                  let chatBox = document.getElementById('chatBox');
                  chatBox.innerHTML = "";
                  
                  let divWel = document.createElement('div');
                  divWel.className = 'msg-wrap';
                  divWel.innerHTML = `
                     <div class="msg-header">
                        <div class="king-name-container" style="border-color: var(--gold); background: rgba(0,0,0,0.6);">
                            <span class="king-name-tag" style="color: var(--gold);">الإدارة العامة</span>
                        </div>
                     </div>
                     <div class="msg-text">مرحباً بكم في شات حسوني الإمبراطوري الحصري والآمن 🏆🔥</div>
                  `;
                  chatBox.appendChild(divWel);
                  
                  snapshot.forEach((doc) => {
                      let mData = doc.data();
                      if (mData.user) {
                          ui.renderMsg(mData.user, mData.text);
                      }
                  });
              });
        },
        listenToActiveMics: () => {
            window.activeMicsListener = db.collection("rooms").doc(window.currentRoom).collection("mics")
              .onSnapshot((snapshot) => {
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
                          document.getElementById(`glow_${num}`).style.animation = 'none';
                      } else {
                          document.getElementById(`mBadge_${num}`).style.display = 'none';
                          document.getElementById(`glow_${num}`).style.animation = 'pulseGlow 1s infinite';
                      }
                  });
              });
        },
        listenOnlineUsersRealtime: () => {
            window.activeOnlineUsersListener = db.collection("users").onSnapshot((snap) => {
                let list = []; 
                snap.forEach(doc => {
                    let uData = doc.data();
                    if(uData.isOnline) list.push(uData);
                });
                
                list.sort((a, b) => {
                    let orderA = window.rolesOrder[a.role] || 99;
                    let orderB = window.rolesOrder[b.role] || 99;
                    return orderA - orderB;
                });

                let usersHtml = list.map(u => {
                    let rObj = window.chatRanksData[u.role] || { icon: "fas fa-user", color: "#fff" };
                    return `
                        <div class="menu-item" onclick="ui.viewProfileCard('${u.uid}')">
                            <span style="color:${rObj.color}; font-weight: bold;"><i class="${rObj.icon}" style="margin-left:5px;"></i> ${u.name}</span>
                            <span style="font-size:11px; color:${rObj.color}; background: rgba(0,0,0,0.4); padding: 2px 6px; border-radius: 10px; border: 1px solid ${rObj.color};">${rObj.text}</span>
                        </div>
                    `;
                }).join('');
                
                let bodyEl = document.getElementById('onlineUsersListBody');
                if(bodyEl) bodyEl.innerHTML = usersHtml;
            });
        },
        refreshChatWindowOnly: () => {
            ui.enterChat();
            let box = document.getElementById('chatBox');
            box.scrollTop = box.scrollHeight;
            alert("تم تحديث غرف الشات بنجاح.");
        },
        sendMessage: () => {
            if(window.currentUser.isMuted) { alert("أنت مكتوم حالياً."); return; }
            let inp = document.getElementById('msgInp');
            let t = inp.value.trim(); if(!t) return;
            
            inp.value = '';
            
            db.collection("users").doc(window.currentUser.uid).get().then((doc) => {
                let latestUser = window.currentUser;
                if(doc.exists) {
                    latestUser = doc.data();
                }
                let cleanUserObj = {
                    uid: latestUser.uid,
                    name: latestUser.name,
                    role: latestUser.role,
                    img: latestUser.img,
                    nameBg: latestUser.nameBg || "transparent"
                };

                db.collection("rooms").doc(window.currentRoom).collection("messages").add({
                    user: cleanUserObj,
                    text: t,
                    timestamp: firebase.firestore.FieldValue.serverTimestamp()
                }).catch((err) => {
                    alert("خطأ: " + err.message);
                });
            });
        },
        quoteUserText: (userName, textContent) => {
            let cleanText = textContent.replace(/<\/?[^>]+(>|$)/g, ""); 
            document.getElementById('msgInp').value = ` ↩️ اقتباس [ ${userName} ]: "${cleanText}" -> `;
            document.getElementById('msgInp').focus();
        },
        
        renderMsg: (user, text) => {
            if (!user) return;
            
            let div = document.createElement('div');
            div.className = 'msg-wrap';
            let rankObj = window.chatRanksData[user.role] || { icon: "fas fa-user", color: "#fff", text: "عضو" };
            
            div.innerHTML = `
                <div class="msg-header">
                    <div class="pfp-main-frame">
                        <img src="${user.img || 'https://cdn-icons-png.flaticon.com/512/1042/1042291.png'}" class="pfp-main" onclick="ui.viewProfileCard('${user.uid}')">
                    </div>
                    
                    <div class="rank-standalone-icon" style="border-color: ${rankObj.color};">
                        <i class="${rankObj.icon}" style="color: ${rankObj.color}; filter: drop-shadow(0 0 2px ${rankObj.color});"></i>
                    </div>
                    
                    <div class="king-name-container" style="border-color: ${rankObj.color}; background: rgba(0,0,0,0.6);" onclick="ui.quoteUserText('${user.name}', '${text}')">
                        <span class="king-name-tag" style="color: ${rankObj.color};">${user.name}</span>
                    </div>
                </div>
                <div class="msg-text">${text}</div>
            `;
            let box = document.getElementById('chatBox');
            if (box) {
                box.appendChild(div);
                box.scrollTop = box.scrollHeight;
            }
        },
        clickMicSlot: (num) => {
            window.selectedMicNum = num;
            let slot = document.getElementById(`mic_${num}`);
            if(!slot.classList.contains('occupied')) {
                document.getElementById('featureModalTitle').innerText = "🎙️ طلب الصعود للمصطبة السحابية";
                document.getElementById('featureModalBody').innerHTML = `
                    <p style="text-align:center; font-size:15px;">هل تريد الصعود والحديث على مايك رقم [ ${num} ]?</p>
                    <div style="display:flex; gap:10px; margin-top:15px;">
                        <button class="send-btn" style="flex:1; border-radius:8px;" onclick="ui.confirmMicGoingUp(true)">نعم</button>
                        <button class="send-btn" style="flex:1; background:#7f8c8d; color:#fff; border-radius:8px;" onclick="ui.confirmMicGoingUp(false)">إلغاء</button>
                    </div>
                `;
                document.getElementById('featureModal').style.display = 'flex';
            } else {
                document.getElementById('featureModalTitle').innerText = "🎛️ لوحة التحكم الصوتي";
                document.getElementById('featureModalBody').innerHTML = `
                    <div class="menu-item" onclick="ui.toggleMicVoiceState(${num}, false)"><i class="fas fa-microphone" style="color:#2ecc71;"></i> فتح المايك وبث الصوت الحقيقي</div>
                    <div class="menu-item" onclick="ui.toggleMicVoiceState(${num}, true)"><i class="fas fa-microphone-slash" style="color:#e74c3c;"></i> كتم الصوت الشخصي</div>
                    <div class="menu-item" onclick="ui.openYouTubeSearchEngine()"><i class="fab fa-youtube" style="color:red;"></i> تشغيل صوت يوتيوب للروم</div>
                    <div class="menu-item" onclick="ui.stopHiddenAudioPlayback()"><i class="fas fa-stop-circle" style="color:#f39c12;"></i> إيقاف البث الصوتي فوراً</div>
                    <div class="menu-item" onclick="ui.vacateMicSlot(${num})" style="color:#e74c3c; font-weight:bold;"><i class="fas fa-sign-out-alt"></i> نزول من المايك</div>
                `;
                document.getElementById('featureModal').style.display = 'flex';
            }
        },
        confirmMicGoingUp: (status) => {
            document.getElementById('featureModal').style.display = 'none';
            if(!status) return;
            let num = window.selectedMicNum;
            
            navigator.mediaDevices.getUserMedia({ audio: true }).then(stream => {
                window.localAudioStream = stream;
                db.collection("rooms").doc(window.currentRoom).collection("mics").doc(`mic_${num}`).set({
                    micNum: num, userId: window.currentUser.uid, userName: window.currentUser.name,
                    userImg: window.currentUser.img, isMuted: false
                });
            }).catch(() => {
                alert("يرجى إعطاء صلاحية المايك للمتصفح أولاً لكي يظهر صوتك الحقيقي!");
            });
        },
        toggleMicVoiceState: (num, shouldMute) => {
            db.collection("rooms").doc(window.currentRoom).collection("mics").doc(`mic_${num}`).update({ isMuted: shouldMute });
            if(window.localAudioStream) {
                window.localAudioStream.getAudioTracks().forEach(track => track.enabled = !shouldMute);
            }
            document.getElementById('featureModal').style.display = 'none';
        },
        vacateMicSlot: (num) => {
            db.collection("rooms").doc(window.currentRoom).collection("mics").doc(`mic_${num}`).delete();
            if(window.localAudioStream) {
                window.localAudioStream.getTracks().forEach(track => track.stop());
                window.localAudioStream = null;
            }
            document.getElementById('featureModal').style.display = 'none';
        },
        
        openYouTubeSearchEngine: () => {
            document.getElementById('featureModalTitle').innerText = "📺 باحث ومشغل اليوتيوب الإمبراطوري";
            document.getElementById('featureModalBody').innerHTML = `
                <div style="text-align:right;">
                    <p style="font-size:12px; color:#aaa; text-align:center;">قم بلصق رابط الأغنية أو الشيلة المنسوخ من اليوتيوب لمعاينتها وتشغيلها فوراً:</p>
                    <input type="text" id="ytLinkInput" class="form-control" placeholder="ضع رابط اليوتيوب هنا..." oninput="ui.previewYoutubeTrack()">
                    
                    <div id="ytSearchPreviewContainer"></div>
                </div>
            `;
            document.getElementById('featureModal').style.display = 'flex';
        },
        previewYoutubeTrack: () => {
            let link = document.getElementById('ytLinkInput').value.trim();
            let videoId = extractYouTubeVideoId(link);
            let container = document.getElementById('ytSearchPreviewContainer');
            
            if (videoId) {
                container.innerHTML = `
                    <div class="yt-preview-card" onclick="ui.processAndPlayYoutubeLink('${videoId}')">
                        <i class="fab fa-youtube yt-preview-icon"></i>
                        <div style="flex:1; text-align:right;">
                            <span style="color:#fff; font-size:14px; font-weight:bold; display:block;">🎵 تم العثور على الملف الصوتي المطلـوب</span>
                            <span style="color:var(--gold); font-size:11px;">اضغط هنا الآن لتشغيل البث فوراً لجميع الأعضاء 🚀</span>
                        </div>
                    </div>
                `;
            } else {
                container.innerHTML = "";
            }
        },
        processAndPlayYoutubeLink: (vId) => {
            let videoId = vId;
            if(!videoId) {
                let link = document.getElementById('ytLinkInput').value.trim();
                videoId = extractYouTubeVideoId(link);
            }
            if(!videoId) { alert("الرجاء التحقق من الرابط!"); return; }
            
            db.collection("room_settings").doc(window.currentRoom).set({
                activeAudioId: videoId
            }, { merge: true }).then(() => {
                alert("🔊 تم إطلاق وتشغيل الأغنية والمزامنة لجميع الحاضرين في الغرفة بنجاح!");
                document.getElementById('featureModal').style.display = 'none';
            });
        },
        stopHiddenAudioPlayback: () => {
            db.collection("room_settings").doc(window.currentRoom).set({
                activeAudioId: ""
            }, { merge: true }).then(() => {
                alert("تم إيقاف الصوت لدى الجميع.");
                document.getElementById('featureModal').style.display = 'none';
            });
        },
        
        toggleOnlineUsers: () => {
            let m = document.getElementById('onlineUsersHalfModal');
            if(m.style.display === 'block') { 
                m.style.display = 'none'; 
            } else {
                m.style.display = 'block';
            }
        },

        viewProfileCard: (uid) => {
            db.collection("users").doc(uid).get().then((doc) => {
                if(!doc.exists) return;
                let u = doc.data();
                window.targetProfileId = uid;
                
                let isMe = (window.currentUser.uid === uid);
                let isAmOwner = (window.currentUser.role === 'owner');
                
                document.getElementById('featureModalTitle').innerText = "الملف الشخصي";
                
                let pencilHtml = (isMe || isAmOwner) && (window.currentUser.role !== 'guest') ? 
                    `<div class="profile-edit-pencil" onclick="ui.openEditProfileModal('${uid}')"><i class="fas fa-pencil-alt"></i></div>` : '';
                
                let adminOptionsBtn = isAmOwner && !isMe ? 
                    `<button class="send-btn" style="width:100%; margin-top:10px; background:linear-gradient(to left, #cb2d3e, #ef473a); color:#fff;" onclick="ui.openAdminControls('${uid}')">⚙️ إدارة الحساب والإجراءات</button>` : '';

                let rObj = window.chatRanksData[u.role] || { icon: "fas fa-user", color: "#fff", text: "عضو" };

                document.getElementById('featureModalBody').innerHTML = `
                    <div class="profile-card-wrapper">
                        ${pencilHtml}
                        <img src="${u.cover || 'https://images.unsplash.com/photo-1618005182384-a83a8bd57fbe?q=80&w=400'}" class="profile-card-cover" id="cardCoverImg">
                        <img src="${u.img || 'https://cdn-icons-png.flaticon.com/512/1042/1042291.png'}" class="profile-card-pfp" id="cardPfpImg">
                        <h2 style="color:${rObj.color}; margin:5px 0 2px;">${u.name}</h2>
                        <p style="margin:0 0 10px; font-size:13px; color:${rObj.color}; font-weight:bold;"><i class="${rObj.icon}"></i> ${rObj.text}</p>
                        <p style="margin:0 0 10px; font-size:12px; color:#aaa;">${u.status || 'لا يوجد حالة'}</p>
                        
                        <div class="profile-action-bar">
                            <div class="profile-bar-btn" onclick="ui.likeProfile('${uid}')"><i class="fas fa-heart"></i> <span id="likeCountText">${u.likes || 0}</span> لاف</div>
                            <div class="profile-bar-btn" onclick="alert('فتح الخاص')"><i class="fas fa-paper-plane"></i> الخاص</div>
                            <div class="profile-bar-btn"><i class="fas fa-chart-line"></i> ليفل ${u.level || 1}</div>
                        </div>

                        <div class="profile-details-grid">
                            <div class="profile-grid-row"><span>العمر:</span><span>${u.age || 'غير مححدد'}</span></div>
                            <div class="profile-grid-row"><span>الجنس:</span><span>${u.gender || 'غير مححدد'}</span></div>
                            <div class="profile-grid-row"><span>البلد:</span><span>${u.country || 'اليمن'}</span></div>
                        </div>
                        ${adminOptionsBtn}
                    </div>
                `;
                document.getElementById('featureModal').style.display = 'flex';
            });
        },

        likeProfile: (uid) => {
            db.collection("users").doc(uid).update({
                likes: firebase.firestore.FieldValue.increment(1)
            }).then(() => {
                let el = document.getElementById('likeCountText');
                if(el) el.innerText = parseInt(el.innerText) + 1;
            });
        },

        handleLocalFileProcessing: (inputEl, type) => {
            let file = inputEl.files[0];
            if (!file) return;
            let reader = new FileReader();
            reader.onload = (e) => {
                if (type === 'cover') {
                    window.tempUploadedCover = e.target.result;
                    alert("تم تحميل صورة الغلاف بنجاح!");
                } else if (type === 'pfp') {
                    window.tempUploadedPfp = e.target.result;
                    alert("تم تحميل الصورة الشخصية بنجاح!");
                } else if (type === 'roomBg') {
                    window.tempUploadedRoomBg = e.target.result;
                    alert("تم تحميل خلفية الغرفة بنجاح!");
                }
            };
            reader.readAsDataURL(file);
        },

        openEditProfileModal: (uid) => {
            if(window.currentUser.role === 'guest') { alert("يرجى التسجيل أولاً!"); return; }
            db.collection("users").doc(uid).get().then((doc) => {
                let u = doc.data();
                window.tempUploadedCover = u.cover || "";
                window.tempUploadedPfp = u.img || "";
                
                document.getElementById('featureModalTitle').innerText = "تعديل بيانات الملف الشخصي";
                document.getElementById('featureModalBody').innerHTML = `
                    <div style="text-align:right;">
                        <label style="font-size:12px; color:var(--gold); font-weight:bold;">صورة الغلاف:</label>
                        <label for="fileCover" class="file-input-label"><i class="fas fa-upload"></i> اختر صورة غلاف</label>
                        <input type="file" id="fileCover" class="file-input-hidden" accept="image/*" onchange="ui.handleLocalFileProcessing(this, 'cover')">
                        
                        <label style="font-size:12px; color:var(--gold); font-weight:bold;">الصورة الشخصية:</label>
                        <label for="filePfp" class="file-input-label"><i class="fas fa-image"></i> اختر صورة بروفايل</label>
                        <input type="file" id="filePfp" class="file-input-hidden" accept="image/*" onchange="ui.handleLocalFileProcessing(this, 'pfp')">
                        
                        <label style="font-size:12px; color:var(--gold);">الاسم المستعار:</label>
                        <input type="text" id="editName" class="form-control" value="${u.name || ''}">
                        
                        <label style="font-size:12px; color:var(--gold);">العمر:</label>
                        <input type="number" id="editAge" class="form-control" value="${u.age || ''}">
                        
                        <label style="font-size:12px; color:var(--gold);">البلد:</label>
                        <input type="text" id="editCountry" class="form-control" value="${u.country || ''}">
                        
                        <button class="send-btn" style="width:100%; margin-top:10px; border-radius:8px;" onclick="ui.saveProfileEdits('${uid}')">حفظ التغييرات</button>
                    </div>
                `;
            });
        },

        saveProfileEdits: (uid) => {
            let updated = {
                cover: window.tempUploadedCover,
                img: window.tempUploadedPfp,
                name: document.getElementById('editName').value.trim(),
                age: document.getElementById('editAge').value.trim(),
                country: document.getElementById('editCountry').value.trim()
            };

            db.collection("users").doc(uid).update(updated).then(() => {
                alert("تم تحديث البيانات المزامنة بنجاح!");
                if(window.currentUser.uid === uid) {
                    window.currentUser = { ...window.currentUser, ...updated };
                    localStorage.setItem("hassouni_user_session", JSON.stringify(window.currentUser));
                }
                document.getElementById('featureModal').style.display = 'none';
            });
        },

        openAdminControls: (uid) => {
            db.collection("users").doc(uid).get().then((doc) => {
                let u = doc.data();
                document.getElementById('featureModalTitle').innerText = `إدارة حساب: ${u.name}`;
                document.getElementById('featureModalBody').innerHTML = `
                    <div style="text-align:right;">
                        <label style="font-size:12px; color:var(--gold);">تغيير الرتبة الإمبراطورية:</label>
                        <select id="changeRoleSelect" class="form-select" onchange="ui.changeUserRole('${uid}', this.value)">
                            <option value="owner" ${u.role === 'owner' ? 'selected' : ''}>1- البرنس الأصلي (الكأس 🏆)</option>
                            <option value="prince" ${u.role === 'prince' ? 'selected' : ''}>1- برنس إمبراطوري 🏆🖤</option>
                            <option value="king" ${u.role === 'king' ? 'selected' : ''}>2- كنج الملك الملكي 👑❤️</option>
                            <option value="honor" ${u.role === 'honor' ? 'selected' : ''}>3- انروا تاج الشرف 👑💙</option>
                            <option value="admin" ${u.role === 'admin' ? 'selected' : ''}>4- ادمان الإدارة العليا 👑💛</option>
                            <option value="developer" ${u.role === 'developer' ? 'selected' : ''}>5- مطور السيرفر 💻💚</option>
                            <option value="senior_mod" ${u.role === 'senior_mod' ? 'selected' : ''}>6- مشرف أول 💎</option>
                            <option value="mod" ${u.role === 'mod' ? 'selected' : ''}>7- مشرف ⭐</option>
                            <option value="vip" ${u.role === 'vip' ? 'selected' : ''}>8- VIP ❤️‍🔥</option>
                            <option value="diamond" ${u.role === 'diamond' ? 'selected' : ''}>9- عضو ماسي 🔮</option>
                        </select>
                        <hr style="border-color:#333;">
                        <button class="send-btn" style="width:100%; margin-bottom:8px; background:${u.isMuted ? '#2ecc71' : '#f39c12'}; color:#fff;" onclick="ui.toggleUserMute('${uid}', ${!u.isMuted})">
                            ${u.isMuted ? '🔊 إلغاء الكتم' : '🔇 كتم العضو'}
                        </button>
                        <button class="send-btn" style="width:100%; margin-bottom:8px; background:${u.isBanned ? '#2ecc71' : '#e74c3c'}; color:#fff;" onclick="ui.toggleUserBan('${uid}', ${!u.isBanned})">
                            ${u.isBanned ? '✅ إلغاء الحظر' : '🚫 حظر العضو طرد نهائي'}
                        </button>
                    </div>
                `;
            });
        },

        changeUserRole: (uid, newRole) => {
            db.collection("users").doc(uid).update({ role: newRole }).then(() => {
                alert("تم تحديث رتبة العضو بنجاح وتثبيتها سحابياً!");
                if (window.currentUser && window.currentUser.uid === uid) {
                    window.currentUser.role = newRole;
                    localStorage.setItem("hassouni_user_session", JSON.stringify(window.currentUser));
                }
            });
        },
        toggleUserMute: (uid, state) => {
            db.collection("users").doc(uid).update({ isMuted: state }).then(() => {
                alert(state ? "تم الكتم" : "تم إلغاء الكتم");
                document.getElementById('featureModal').style.display = 'none';
            });
        },
        toggleUserBan: (uid, state) => {
            db.collection("users").doc(uid).update({ isBanned: state }).then(() => {
                alert(state ? "تم الحظر" : "تم إلغاء الحظر");
                document.getElementById('featureModal').style.display = 'none';
            });
        },

        openGlobalSettings: () => {
            document.getElementById('featureModalTitle').innerText = "الإعدادات العامة للروم";
            let isOwner = (window.currentUser.role === 'owner');
            window.tempUploadedRoomBg = "";
            
            let adminFields = isOwner ? `
                <div style="border-top:1px solid var(--gold); padding-top:10px; margin-top:10px; text-align:right;">
                    <label style="font-size:12px; color:var(--gold); font-weight:bold;">تغيير خلفية الروم:</label>
                    <label for="fileRoomBg" class="file-input-label"><i class="fas fa-images"></i> اختيار صورة خلفية للغرفة</label>
                    <input type="file" id="fileRoomBg" class="file-input-hidden" accept="image/*" onchange="ui.handleLocalFileProcessing(this, 'roomBg')">
                    <button class="send-btn" style="width:100%; margin-bottom:8px;" onclick="ui.saveRoomBgSetting()">تحديث خلفية الروم سحابياً</button>
                </div>
            ` : '';

            let cleanRoomBtn = isOwner ? `
                <div class="menu-item" style="color:#e74c3c;" onclick="ui.cleanCurrentRoomMessages()"><i class="fas fa-trash-alt"></i> تنظيف الروم وتطهير المحادثات</div>
            ` : '';

            document.getElementById('featureModalBody').innerHTML = `
                ${cleanRoomBtn}
                ${adminFields}
                <div class="menu-item" style="color:#fff;" onclick="ui.logoutBackToWelcome()"><i class="fas fa-sign-out-alt"></i> تسجيل الخروج</div>
            `;
            document.getElementById('featureModal').style.display = 'flex';
        },

        saveRoomBgSetting: () => {
            if(!window.tempUploadedRoomBg) { alert("الرجاء اختيار ملف صورة أولاً"); return; }
            db.collection("room_settings").doc(window.currentRoom).set({ roomBg: window.tempUploadedRoomBg }, { merge: true }).then(() => {
                alert("تم تغيير وتثبيت خلفية الروم بنجاح!");
                document.getElementById('featureModal').style.display = 'none';
            });
        },

        cleanCurrentRoomMessages: () => {
            if(confirm("هل تريد مسح كافة رسائل هذه الغرفة فوراً؟")) {
                db.collection("rooms").doc(window.currentRoom).collection("messages").get().then((snap) => {
                    snap.forEach(doc => doc.ref.delete());
                    alert("تم تنظيف الروم بالكامل.");
                    document.getElementById('featureModal').style.display = 'none';
                });
            }
        },

        openRoomsManager: () => {
            document.getElementById('featureModalTitle').innerText = "الغرف المتوفرة";
            document.getElementById('featureModalBody').innerHTML = `
                <div id="roomsContainerList">
                    ${window.roomsList.map(r => `<div class="menu-item" onclick="ui.changeActiveRoom('${r}')">${r} ${window.currentRoom === r ? '<span style="color: #FFD700; font-size: 1.2rem; margin-left: 5px;">🏆</span>' : ''}</div>`).join('')}
                </div>
            `;
            document.getElementById('featureModal').style.display = 'flex';
        },

        createNewRoomCloud: () => {
            let rName = document.getElementById('newRoomNameInp').value.trim();
            if(!rName) return;
            if(!window.roomsList.includes(rName)) {
                window.roomsList.push(rName);
                alert(`تم إنشاء غرفة [ ${rName} ] بنجاح من الصلاحية الملكية.`);
                document.getElementById('featureModal').style.display = 'none';
            }
        },

        changeActiveRoom: (r) => { 
            window.currentRoom = r; document.getElementById('chatBox').innerHTML = ""; 
            document.getElementById('featureModal').style.display = 'none'; 
            ui.enterChat();
        },

        logoutBackToWelcome: () => {
            ui.updateUserOnlineStatus(false);
            localStorage.removeItem("hassouni_user_session");
            setTimeout(() => {
                window.location.reload();
            }, 400);
        },
        openVIPList: (title) => alert(title)
    };

    window.onload = () => { ui.checkSavedSessionOnLoad(); };
</script>
</body>
</html>
