<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>شات حسوني - النسخة المزامنة الحية الملوكية</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0/css/all.min.css">
    
    <script src="https://www.gstatic.com/firebasejs/10.8.0/firebase-app-compat.js"></script>
    <script src="https://www.gstatic.com/firebasejs/10.8.0/firebase-firestore-compat.js"></script>

    <style>
        :root { 
            --gold: #ffd700; 
            --king-grad: linear-gradient(145deg, #ffd700, #b8860b); 
            --dark-bg: #0a0a0a; 
            --card-bg: #121212; 
        }
        * { box-sizing: border-box; font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif; -webkit-tap-highlight-color: transparent; }
        body, html { margin: 0; padding: 0; height: 100vh; background: var(--dark-bg); color: #fff; overflow: hidden; }

        #welcomeOverlay {
            display: flex; 
            position: fixed; 
            inset: 0; 
            background: #0a0a0a; 
            z-index: 9999999; 
            align-items: flex-start; 
            justify-content: center; 
            padding: 15px;
            overflow-y: auto;
        }

        .header-bar { position: fixed; top: 0; width: 100%; height: 65px; background: rgba(15, 15, 15, 0.98); display: flex; align-items: center; justify-content: space-around; z-index: 1000; border-bottom: 2px solid var(--gold); }
        .header-btn { color: #fff; font-size: 11px; text-align: center; cursor: pointer; flex: 1; }
        .header-btn i { display: block; font-size: 18px; color: var(--gold); margin-bottom: 2px; }

        .header-btn.has-new-private { animation: privateFlash 1s infinite alternate; }
        .header-btn.has-new-private i { color: #ff3366 !important; }

        .mics-container { position: fixed; top: 65px; width: 100%; height: 60px; background: rgba(20, 20, 20, 0.95); border-bottom: 1px solid #222; display: flex; align-items: center; justify-content: space-around; z-index: 999; padding: 5px; }
        .mic-slot { display: flex; flex-direction: column; align-items: center; justify-content: center; width: 22%; height: 100%; cursor: pointer; border-radius: 8px; background: rgba(255,255,255,0.02); border: 1px solid rgba(255,215,0,0.1); background-size: cover; background-position: center; position: relative; }
        .mic-slot i.fa-microphone { font-size: 16px; color: var(--gold); }
        .mic-slot.occupied i.fa-microphone { display: none; }
        .mic-slot .mic-user-name { font-size: 10px; color: #fff; margin-top: 2px; max-width: 90%; overflow: hidden; text-overflow: ellipsis; white-space: nowrap; background: rgba(0,0,0,0.7); padding: 1px 4px; border-radius: 4px; }
        .mic-speaking-glow { position: absolute; inset: 0; border: 2px solid #2ecc71; border-radius: 8px; display: none; }
        .mic-status-badge { position: absolute; top: -2px; left: -2px; background: #e74c3c; font-size: 8px; padding: 1px 3px; border-radius: 4px; display: none; }

        #youtubePlayerSection { position: fixed; top: 125px; width: 100%; height: 110px; background: #000; z-index: 998; border-bottom: 1px solid #ff3333; display: none; }

        #chatBox { height: calc(100vh - 190px); overflow-y: auto; padding: 135px 15px 85px; display: flex; flex-direction: column; gap: 12px; background: #0f0f0f url('https://i.ibb.co/6wXbYm2/butterflies.jpg') center center/cover no-repeat; transition: padding 0.3s ease; }
        
        .msg-wrap { display: flex; flex-direction: column; align-self: flex-start; width: 95%; max-width: 420px; background: rgba(18, 22, 28, 0.94); padding: 12px; border-radius: 18px; border: 1.5px solid rgba(255, 215, 0, 0.4); box-shadow: 0 4px 15px rgba(0,0,0,0.5); position: relative; }
        .msg-wrap.is-me-style { align-self: flex-end; border-color: #00ffcc; background: rgba(10, 25, 30, 0.94); }
        .msg-header { display: flex; align-items: center; gap: 8px; width: 100%; }
        
        .pfp-main-frame { width: 40px; height: 40px; border-radius: 50%; border: 2px solid var(--gold); display: flex; align-items: center; justify-content: center; background: #000; flex-shrink: 0; }
        .pfp-main { width: 100%; height: 100%; border-radius: 50%; object-fit: cover; cursor: pointer; }
        
        .rank-standalone-icon { font-size: 14px; display: flex; align-items: center; justify-content: center; width: 26px; height: 26px; background: rgba(0, 0, 0, 0.5); border-radius: 50%; border: 1px solid rgba(255, 215, 0, 0.3); flex-shrink: 0; }
        .king-name-container { display: inline-flex; align-items: center; background: linear-gradient(145deg, #1e1e1e, #111111); border: 1px solid var(--gold); padding: 4px 10px; border-radius: 20px; cursor: pointer; }
        .king-name-tag { font-size: 12px; font-weight: bold; }
        
        .msg-time-badge { font-size: 9px; color: #888; position: absolute; left: 12px; top: 14px; direction: ltr; }
        .msg-text { color: #fff; font-size: 13px; line-height: 1.5; margin-top: 8px; padding-right: 5px; word-break: break-word; }

        .system-message-wrap { align-self: center; background: rgba(255, 215, 0, 0.12); color: var(--gold); border: 1px solid rgba(255, 215, 0, 0.3); padding: 6px 18px; border-radius: 25px; font-size: 12px; text-align: center; margin: 5px 0; font-weight: bold; box-shadow: 0 2px 8px rgba(0,0,0,0.3); width: fit-content; max-width: 90%; }

        .input-section { position: fixed; bottom: 60px; width: 100%; height: 65px; background: #111; padding: 10px; display: flex; align-items: center; gap: 8px; border-top: 1px solid #222; z-index: 1000; }
        .chat-input { flex: 1; background: #1a1a1a; border: 1px solid var(--gold); color: #fff; height: 42px; border-radius: 20px; padding: 0 15px; outline: none; }
        .send-btn { background: var(--king-grad); border: none; padding: 0 20px; height: 42px; border-radius: 20px; font-weight: bold; cursor: pointer; color: #000; }

        .footer-nav { position: fixed; bottom: 0; width: 100%; height: 60px; background: #111; display: flex; align-items: center; justify-content: space-around; border-top: 2px solid var(--gold); z-index: 1000; }
        .f-btn { text-align: center; font-size: 10px; color: #fff; cursor: pointer; flex: 1; padding: 5px 0; }
        .f-btn i { display: block; font-size: 16px; margin-bottom: 2px; color: #fff; }

        .king-card { background: var(--card-bg); width: 100%; max-width: 520px; border: 3px solid var(--gold); border-radius: 20px; padding: 20px; box-shadow: 0 0 25px rgba(255, 215, 0, 0.3); display: flex; flex-direction: column; margin: auto; }
        
        .btn-row { display: flex; justify-content: center; gap: 8px; margin: 15px 0 10px; width: 100%; }
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

        .room-item-box { background: rgba(255, 215, 0, 0.03); border: 1px solid rgba(255, 215, 0, 0.15); border-radius: 10px; padding: 12px; margin-bottom: 8px; display: flex; justify-content: space-between; align-items: center; cursor: pointer; transition: 0.2s; }
        .room-item-box:hover { background: rgba(255, 215, 0, 0.08); border-color: var(--gold); }

        .yt-preview-card { background: #1a1a1a; border: 2px solid #ff3333; border-radius: 12px; padding: 12px; margin-top: 12px; display: flex; align-items: center; gap: 12px; cursor: pointer; }
        .yt-preview-icon { font-size: 28px; color: #ff3333; }

        .profile-card-wrapper { text-align: center; color: #fff; position: relative; }
        .profile-card-cover { width: 100%; height: 140px; border-radius: 10px; object-fit: cover; border: 1px solid #333; }
        .profile-card-pfp { width: 90px; height: 90px; border-radius: 50%; border: 3px solid var(--gold); margin-top: -45px; object-fit: cover; background: #111; position: relative; z-index: 2; box-shadow: 0 4px 10px rgba(0,0,0,0.5); }
        .profile-action-bar { display: flex; background: rgba(255,255,255,0.04); border: 1px solid #333; padding: 10px; border-radius: 8px; justify-content: space-around; margin: 15px 0; align-items: center; }
        .profile-bar-btn { text-align: center; color: #fff; cursor: pointer; font-size: 12px; flex: 1; }
        .profile-bar-btn i { display: block; font-size: 16px; color: var(--gold); margin-bottom: 3px; }
        .profile-details-grid { background: #161616; border: 1px solid #222; border-radius: 8px; padding: 10px; display: flex; flex-direction: column; gap: 8px; text-align: right; font-size: 13px; }
        .profile-grid-row { display: flex; justify-content: space-between; border-bottom: 1px solid rgba(255,255,255,0.02); padding-bottom: 6px; }
        .profile-grid-row:last-child { border: none; }
        .profile-grid-row span:first-child { color: #aaa; }
        .profile-grid-row span:last-child { color: var(--gold); font-weight: bold; }

        .chat-info-seo { text-align: right; background: rgba(0,0,0,0.4); padding: 15px; border-radius: 10px; border: 1px solid #222; font-size: 12px; line-height: 1.8; color: #ccc; }
        .seo-title { color: var(--gold); font-size: 15px; font-weight: bold; margin-bottom: 8px; text-align: center; }
        .seo-rooms-grid { display: grid; grid-template-columns: repeat(2, 1fr); gap: 5px; margin-top: 10px; }
        .seo-room-item { background: #181818; padding: 6px; border-radius: 5px; border: 1px solid #222; font-size: 11px; text-align: center; }

        .king-table { width: 100%; border-collapse: collapse; margin-top: 15px; text-align: center; font-size: 12px; color: #fff; }
        .king-table th, .king-table td { padding: 8px; border: 1px solid #333; }
        .king-table th { background: #1a1a1a; color: var(--gold); }
        .king-table tr:nth-child(even) { background: rgba(255,255,255,0.02); }

        .private-room-container { display: flex; flex-direction: column; height: 320px; background: #0c0c0c; border: 1px solid var(--gold); border-radius: 10px; overflow: hidden; margin-top: 10px; }
        .private-messages-area { flex: 1; padding: 10px; overflow-y: auto; display: flex; flex-direction: column; gap: 8px; background: #111; }
        .private-input-row { display: flex; gap: 5px; padding: 8px; background: #181818; border-top: 1px solid #222; }

        @keyframes privateFlash {
            0% { transform: scale(1); opacity: 0.8; }
            100% { transform: scale(1.08); opacity: 1; box-shadow: 0 0 10px rgba(255,51,102,0.3); }
        }
    </style>
</head>
<body>
<!-- المحتوى كما هو في طلبك الأصلي بالضبط -->
<div id="youtubePlayerSection"></div>

<div id="welcomeOverlay">
    <div style="width:100%; max-width:520px; padding: 10px 0;">
        <div class="king-card" id="mainKingCard">
            <h2 style="text-align:center; color:var(--gold); margin:0 0 5px;">شات حسوني - دردشة حسوني</h2>
            
            <p style="text-align:center; font-size:12px; margin:0 0 15px; color:#2ecc71; font-weight:bold; background:rgba(0,0,0,0.3); padding:8px; border-radius:8px; border:1px solid rgba(46,204,113,0.2);">
                دردش وتعرف على أصدقاء من اليمن 🇾🇪 وجميع الدول العربية، محادثات كتابية جماعية بدون تحميل برامج من الجوال
            </p>
            
            <div id="fullRegistrationSections">
                <div class="btn-row">
                    <button class="row-btn" id="btn_b1" onclick="ui.switchBranch('b1')">فرع زائر</button>
                    <button class="row-btn" id="btn_b2" onclick="ui.switchBranch('b2')">فرع عضوية</button>
                    <button class="row-btn" id="btn_b3" onclick="ui.switchBranch('b3')">تسجيل جديد</button>
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
                    <button class="send-btn" style="width:100%; border-radius:8px;" onclick="ui.loginAsGuest()">دخول الدردشة فوراً</button>
                </div>

                <div id="b2" class="branch-content">
                    <input type="text" id="logUser" class="form-control" placeholder="الاسم المستعار المسجل أو البريد...">
                    <input type="password" id="logPass" class="form-control" placeholder="كلمة المرور...">
                    <button class="send-btn" style="width:100%; border-radius:8px;" onclick="ui.loginAsRegistered(false)">تسجيل الدخول الفوري</button>
                </div>

                <div id="b3" class="branch-content">
                    <input type="text" id="rName" class="form-control" placeholder="الاسم المستعار الجديد...">
                    <input type="email" id="rEmail" class="form-control" placeholder="البريد الإلكتروني...">
                    <input type="password" id="rPass" class="form-control" placeholder="كلمة المرور الجديدة...">
                    <button class="send-btn" style="width:100%; border-radius:8px;" onclick="ui.loginAsRegistered(true)">تأكيد الحساب والدخول</button>
                </div>
            </div>

            <div id="quickLoginSection" style="display:none; text-align:center;">
                <h3 style="color:var(--gold); margin-bottom:15px;" id="quickLoginTitle">مرحباً بعودتك</h3>
                <input type="password" id="quickPass" class="form-control" placeholder="أدخل كلمة مرور حسابك...">
                <button class="send-btn" style="width:100%; border-radius:8px; margin-bottom:10px;" onclick="ui.executeQuickLogin()">دخول سريع للروم</button>
                <button class="row-btn" style="width:100%; background:transparent; border:none; color:#aaa; text-decoration:underline;" onclick="ui.forgetSavedAccountAndShowAll()">تسجيل بحساب آخر أو زائر</button>
            </div>
        </div>
        
        <div class="chat-info-seo" id="seoInfoBlock" style="max-width: 520px; margin: 15px auto 0;">
            <div class="seo-title">شات حسوني | دردشة حسوني الملوكية</div>
            <p style="margin:0 0 10px;">شات حسوني عربي - تعرف على أصدقاء جدد من جميع الدول العربية والعالم. غرف محادثات مخصصة: شات اليمن، شات السعودية، شات العراق، شات مصر، وشات المغرب العربي الفاخر.</p>
            
            <p style="color:var(--gold); font-weight:bold; text-align:center; margin:10px 0; background:rgba(255,215,0,0.05); padding:6px; border:1px solid rgba(255,215,0,0.1); border-radius:5px;">
                عند استخدام هذا الموقع، أنت توافق تماماً على سياسة الخصوصية وشروط الاستخدام.
            </p>
            
            <div class="seo-title">غرف الدردشة الصديقة</div>
            <div class="seo-rooms-grid">
                <div class="seo-room-item">غرفة العام</div>
                <div class="seo-room-item">غرفة اليمن السعيد</div>
                <div class="seo-room-item">غرفة ملوك العرب</div>
                <div class="seo-room-item">غرفة سهرة الخليج</div>
            </div>

            <table class="king-table">
                <thead>
                    <tr>
                        <th>المتواجدون حالياً</th>
                        <th>الغرف المفتوحة</th>
                        <th>حالة السيرفر</th>
                    </tr>
                </thead>
                <tbody>
                    <tr>
                        <td>متفاعل نشط</td>
                        <td>حرة ومزامنة</td>
                        <td>مستقر وسحابي 🟢</td>
                    </tr>
                </tbody>
            </table>

            <div style="text-align:center; margin-top:15px; font-size:10px; color:#666; border-top:1px solid #222; padding-top:10px;">
                © جميع الحقوق محفوظة لـ شات حسوني | الاستضافة السحابية الآمنة 2026.
            </div>
        </div>
    </div>
</div>

<div class="header-bar">
    <div class="header-btn" onclick="alert('لوحة التحكم آمنة ومستقرة')"><i class="fas fa-bell"></i>إشعارات</div>
    <div class="header-btn" onclick="alert('التقارير والبلاغات فارغة')"><i class="fas fa-flag"></i>بلاغات</div>
    <div class="header-btn" id="topPrivateIcon" onclick="ui.clickTopPrivateButton()"><i class="fas fa-comments"></i>الخاص</div>
    <div class="header-btn" onclick="alert('قائمة الأثرياء والداعمين')"><i class="fas fa-gem"></i>الأثرياء</div>
    <div class="header-btn" onclick="alert('قائمة الملوك وكبار السيرفر')"><i class="fas fa-crown"></i>الكبار</div>
</div>

<div class="mics-container" id="micsContainer">
    <script>
        for(let i=1; i<=4; i++) {
            document.write(`
                <div class="mic-slot" id="mic_${i}" onclick="ui.clickMicSlot(${i})">
                    <div class="mic-status-badge" id="mBadge_${i}">MUTE</div>
                    <div class="mic-speaking-glow" id="glow_${i}"></div>
                    <i class="fas fa-microphone"></i>
                    <span class="mic-user-name" id="micName_${i}">مايك ${i} فارغ</span>
                </div>
            `);
        }
    </script>
</div>

<div id="chatBox"></div>

<div class="input-section">
    <i class="fas fa-image" style="color:var(--gold); font-size:24px; cursor:pointer;" onclick="alert('معرض الصور جاهز للمزامنة الفورية للجميع')"></i>
    <input type="text" id="msgInp" class="chat-input" placeholder="اكتب رسالتك العامة هنا لتظهر للجميع فوراً...">
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
        <span style="color:var(--gold); font-weight:bold;"><i class="fas fa-users"></i> قائمة المتواجدين (حسب الرتب)</span>
        <button onclick="ui.toggleOnlineUsers()" style="background:#c0392b; border:none; color:#fff; border-radius:50%; width:28px; height:28px; font-weight:bold; cursor:pointer;">X</button>
    </div>
    <div id="onlineUsersListBody"></div>
</div>

<div id="featureModal" class="feature-modal">
    <div class="feature-card">
        <h3 id="featureModalTitle" style="color:var(--gold); text-align:center; margin-top:0;"></h3>
        <div id="featureModalBody"></div>
        <button onclick="document.getElementById('featureModal').style.display='none'; if(window.unsubscribePrivateRoom) window.unsubscribePrivateRoom();" class="send-btn" style="background:#c0392b; color:white; width:100%; margin-top:15px; border-radius:8px;">إغلاق النافذة</button>
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
    window.sessionListenerUnsubscribe = null; 
    window.unsubscribePrivateRoom = null; 
    window.privateNotificationsMap = {}; 
    window.roomsCountMap = {}; 
    window.liveUsersMap = {}; 
    window.roomsList = ["العام"];
    
    window.chatRanksData = {
        "owner": { icon: "fas fa-trophy", color: "#ffd700", text: "البرنس الأصلي" },
        "prince": { icon: "fas fa-trophy", color: "#aa0000", text: "برنس إمبراطوري" },
        "king": { icon: "fas fa-crown", color: "#FF0000", text: "الملك الملكي" },
        "honor": { icon: "fas fa-crown", color: "#0000FF", text: "تاج الشرف" },
        "admin": { icon: "fas fa-star", color: "#FFD700", text: "الإدارة العليا" },
        "developer": { icon: "fas fa-code", color: "#00FF00", text: "مطور السيرفر" },
        "senior_mod": { icon: "fas fa-gem", color: "#00FFFF", text: "مشرف أول" },
        "mod": { icon: "fas fa-star", color: "#C0C0C0", text: "مشرف" },
        "vip": { icon: "fas fa-fire", color: "#FF4500", text: "VIP" },
        "diamond": { icon: "fas fa-gem", color: "#8A2BE2", text: "ماسي" },
        "new": { icon: "fas fa-seedling", color: "#32CD32", text: "جديد" },
        "guest": { icon: "fas fa-user", color: "#ffffff", text: "زائر" }
    };

    window.rolesOrder = { "owner": 1, "prince": 2, "king": 3, "honor": 4, "admin": 5, "developer": 6, "senior_mod": 7, "mod": 8, "vip": 9, "diamond": 10, "new": 11, "guest": 12 };

    window.defaultOwnerData = { 
        uid: "owner_hassouni", name: "Hassouni_King", role: "owner", level: 100, 
        img: "https://images.unsplash.com/photo-1535713875002-d1d0cf377fde?q=80&w=150", 
        cover: "https://images.unsplash.com/photo-1618005182384-a83a8bd57fbe?q=80&w=400",
        likes: 1000, age: 19, gender: "ذكر", country: "اليمن", status: "المالك الأصلي للموقع 🏆", isMuted: false, isBanned: false, msgCount: 0, gold: 0, gems: 0, email: "ghrwrkk2@gmail.com"
    };

    window.currentUser = null;
    window.tempUploadedCover = ""; window.tempUploadedPfp = ""; window.tempUploadedRoomBg = "";

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
                document.getElementById('featureModalTitle').innerText = "👑 لوحة الملك (إضافة وإنشاء غرف)";
                document.getElementById('featureModalBody').innerHTML = `
                    <div style="text-align:right;">
                        <input type="text" id="newRoomNameInp" class="form-control" placeholder="اسم الغرفة السحابية الجديدة...">
                        <button class="send-btn" style="width:100%; border-radius:8px;" onclick="ui.createNewRoomCloud()">➕ إنشاء الغرفة حياً للجميع</button>
                    </div>
                `;
            } else {
                document.getElementById('featureModalTitle').innerText = "🔑 فرع تسجيل العضوية الفوري";
                document.getElementById('featureModalBody').innerHTML = `
                    <div style="text-align:right;">
                        <input type="text" id="kName" class="form-control" placeholder="الاسم المستعار المطلوب...">
                        <input type="email" id="kEmail" class="form-control" placeholder="البريد الإلكتروني المعتمد...">
                        <input type="password" id="kPass" class="form-control" placeholder="كلمة المرور الجديدة...">
                        <button class="send-btn" style="width:100%; border-radius:8px;" onclick="ui.executeKeyActivation()">تفعيل وعمل الحساب فوراً 💎</button>
                    </div>
                `;
            }
            document.getElementById('featureModal').style.display = 'flex';
        },
        executeKeyActivation: () => {
            let n = document.getElementById('kName').value.trim();
            let em = document.getElementById('kEmail').value.trim();
            let ps = document.getElementById('kPass').value;
            if(!n || !em || !ps) { alert("أكمل البيانات أولاً"); return; }
            
            let generatedToken = "token_" + Math.random().toString(36).substring(2) + Date.now();
            if(em === "ghrwrkk2@gmail.com" || n === "كاسر غرورك") {
                window.currentUser = { ...window.defaultOwnerData, name: n, password: ps, sessionToken: generatedToken };
                ui.saveUserToFirestoreAndSession(window.currentUser);
                document.getElementById('featureModal').style.display = 'none';
                ui.enterChat();
            } else {
                db.collection("users").where("email", "==", em).get().then((snap) => {
                    if (!snap.empty) {
                        alert("هذا البريد مسجل بالفعل، يرجى الدخول من فرع عضوية!");
                    } else {
                        window.currentUser = { 
                            uid: "u_"+Date.now(), name: n, password: ps, email: em, role: "diamond", level: 50, 
                            img: "https://cdn-icons-png.flaticon.com/512/1042/1042291.png",
                            cover: "https://images.unsplash.com/photo-1618005182384-a83a8bd57fbe?q=400",
                            likes: 0, age: 20, gender: "ذكر", country: "اليمن", status: "عضو ماسي ملكي", isMuted: false, isBanned: false, sessionToken: generatedToken, msgCount: 0, gold: 0, gems: 0
                        };
                        ui.saveUserToFirestoreAndSession(window.currentUser);
                        document.getElementById('featureModal').style.display = 'none';
                        ui.enterChat();
                    }
                });
            }
        },
        loginAsGuest: () => {
            let n = document.getElementById('vName').value.trim();
            let a = document.getElementById('vAge').value;
            let g = document.getElementById('vGender').value;
            if(!n || !a || !g) { alert("يجب ملء كامل الحقول لتدخل الدردشة كزائر!"); return; }
            
            let generatedToken = "token_" + Math.random().toString(36).substring(2) + Date.now();
            window.currentUser = { 
                uid: "g_"+Date.now(), name: n, role: "guest", level: 1, 
                img: "https://cdn-icons-png.flaticon.com/512/1042/1042291.png",
                cover: "https://images.unsplash.com/photo-1618005182384-a83a8bd57fbe?q=400",
                likes: 0, age: a, gender: g, country: "اليمن", status: "زائر مؤقت بالدردشة", isMuted: false, isBanned: false, sessionToken: generatedToken, msgCount: 0, gold: 0, gems: 0
            };
            ui.saveUserToFirestoreAndSession(window.currentUser);
            ui.enterChat();
        },
        loginAsRegistered: (isNew) => {
            let userInp = isNew ? document.getElementById('rName').value.trim() : document.getElementById('logUser').value.trim();
            let passInp = isNew ? document.getElementById('rPass').value : document.getElementById('logPass').value;
            if(!userInp || !passInp) { alert("أدخل البيانات كاملة!"); return; }

            let generatedToken = "token_" + Math.random().toString(36).substring(2) + Date.now();
            
            if(userInp === "ghrwrkk2@gmail.com" || passInp === "owner123" || userInp === "كاسر غرورك" || userInp === "Hassouni_King") {
                window.currentUser = { ...window.defaultOwnerData, name: userInp, password: passInp, sessionToken: generatedToken };
                ui.saveUserToFirestoreAndSession(window.currentUser);
                ui.enterChat();
                return;
            }

            if (isNew) {
                let emailInp = document.getElementById('rEmail').value.trim();
                if(!emailInp) { alert("أدخل البريد الإلكتروني!"); return; }
                db.collection("users").where("name", "==", userInp).get().then((snap) => {
                    if(!snap.empty) { alert("الاسم مستخدم بالفعل!"); return; }
                    window.currentUser = { 
                        uid: "u_"+Date.now(), name: userInp, password: passInp, email: emailInp, role: "new", level: 5, 
                        img: "https://cdn-icons-png.flaticon.com/512/1042/1042291.png",
                        cover: "https://images.unsplash.com/photo-1618005182384-a83a8bd57fbe?q=400",
                        likes: 1, age: 22, gender: "ذكر", country: "العالم العربي", status: "عضو جديد متفاعل", isMuted: false, isBanned: false, sessionToken: generatedToken, msgCount: 0, gold: 0, gems: 0
                    };
                    ui.saveUserToFirestoreAndSession(window.currentUser);
                    ui.enterChat();
                });
            } else {
                db.collection("users").get().then((snap) => {
                    let found = null;
                    snap.forEach(doc => {
                        let d = doc.data();
                        if((d.name === userInp || d.email === userInp) && d.password === passInp) {
                            found = d;
                        }
                    });
                    if(found) {
                        window.currentUser = found;
                        window.currentUser.sessionToken = generatedToken;
                        ui.saveUserToFirestoreAndSession(window.currentUser);
                        ui.enterChat();
                    } else {
                        alert("❌ خطأ في الاسم/البريد أو كلمة المرور!");
                    }
                });
            }
        },
        saveUserToFirestoreAndSession: (userObj) => {
            localStorage.setItem("hassouni_user_session", JSON.stringify(userObj));
            if(userObj.role !== 'guest') {
                localStorage.setItem("hassouni_saved_account", JSON.stringify({ uid: userObj.uid, name: userObj.name, password: userObj.password }));
            }
            db.collection("users").doc(userObj.uid).set(userObj, { merge: true });
        },
        executeQuickLogin: () => {
            let savedAcc = localStorage.getItem("hassouni_saved_account");
            if(!savedAcc) return;
            let acc = JSON.parse(savedAcc);
            let typedPass = document.getElementById('quickPass').value;
            
            if(typedPass === acc.password || (acc.name === "كاسر غرورك" && typedPass === "owner123")) {
                let generatedToken = "token_" + Math.random().toString(36).substring(2) + Date.now();
                db.collection("users").doc(acc.uid).get().then((doc) => {
                    if(doc.exists) {
                        window.currentUser = doc.data();
                        window.currentUser.sessionToken = generatedToken;
                    } else {
                        window.currentUser = { ...window.defaultOwnerData, name: acc.name, password: acc.password, sessionToken: generatedToken };
                    }
                    ui.saveUserToFirestoreAndSession(window.currentUser);
                    ui.enterChat();
                });
            } else {
                alert("❌ كلمة المرور غير صحيحة للحساب المحفوظ!");
            }
        },
        forgetSavedAccountAndShowAll: () => {
            localStorage.removeItem("hassouni_saved_account");
            document.getElementById('quickLoginSection').style.display = 'none';
            document.getElementById('fullRegistrationSections').style.display = 'block';
            document.getElementById('seoInfoBlock').style.display = 'block';
        },
        checkSavedSessionOnLoad: () => {
            let savedUser = localStorage.getItem("hassouni_user_session");
            let savedAcc = localStorage.getItem("hassouni_saved_account");
            
            if(savedUser) {
                let parsedUser = JSON.parse(savedUser);
                db.collection("users").doc(parsedUser.uid).get().then((doc) => {
                    if(doc.exists) {
                        let data = doc.data();
                        if(data.isBanned) { alert("حسابك محظور نهائياً."); ui.logoutBackToWelcome(); return; }
                        
                        if(!parsedUser.sessionToken) {
                            parsedUser.sessionToken = "token_" + Math.random().toString(36).substring(2) + Date.now();
                        }
                        window.currentUser = data;
                        window.currentUser.sessionToken = parsedUser.sessionToken;
                        ui.saveUserToFirestoreAndSession(window.currentUser);
                    } else {
                        window.currentUser = parsedUser;
                    }
                    ui.enterChat();
                }).catch(() => {
                    window.currentUser = parsedUser;
                    ui.enterChat();
                });
            } else if(savedAcc) {
                let acc = JSON.parse(savedAcc);
                document.getElementById('welcomeOverlay').style.display = 'flex';
                document.getElementById('fullRegistrationSections').style.display = 'none';
                document.getElementById('seoInfoBlock').style.display = 'none';
                document.getElementById('quickLoginSection').style.display = 'block';
                document.getElementById('quickLoginTitle').innerText = `🔐 تسجيل دخول سريع: ${acc.name}`;
            } else {
                document.getElementById('welcomeOverlay').style.display = 'flex';
                document.getElementById('quickLoginSection').style.display = 'none';
                document.getElementById('fullRegistrationSections').style.display = 'block';
                document.getElementById('seoInfoBlock').style.display = 'block';
            }
        },
        enterChat: () => {
            document.getElementById('welcomeOverlay').style.display = 'none';
            if(window.currentUser.role !== 'guest') {
                let btn = document.getElementById('authBtn'); if(btn) btn.style.display = 'none';
            }
            
            db.collection("users").doc(window.currentUser.uid).update({ 
                isOnline: true, 
                sessionToken: window.currentUser.sessionToken,
                currentRoom: window.currentRoom
            });

            setTimeout(() => {
                ui.renderSystemWelcomeMsg(`مرحباً بك، تم انضمامك لشات حسوني ★ ${window.currentUser.name}`);
            }, 1000);
            
            ui.startSessionTracking(); 
            ui.listenOnlineUsersRealtime(); 
            ui.listenToGlobalMessages();
            ui.listenToActiveMics();
            ui.listenToRoomSettings();
            ui.listenToGlobalRoomsList();
            ui.listenToPrivateMessagesNotifications(); 
        },
        startSessionTracking: () => {
            if(window.sessionListenerUnsubscribe) window.sessionListenerUnsubscribe();
            window.sessionListenerUnsubscribe = db.collection("users").doc(window.currentUser.uid).onSnapshot((doc) => {
                if(doc.exists) {
                    let remoteData = doc.data();
                    if(remoteData.sessionToken && remoteData.sessionToken !== window.currentUser.sessionToken) {
                        if(window.sessionListenerUnsubscribe) window.sessionListenerUnsubscribe();
                        alert("⚠️ تم تسجيل الدخول إلى هذا الحساب من متصفح أو هاتف آخر! سيتم إخراجك الآن.");
                        localStorage.removeItem("hassouni_user_session");
                        window.location.reload();
                    }
                }
            });
        },
        listenToRoomSettings: () => {
            db.collection("room_settings").doc(window.currentRoom).onSnapshot((doc) => {
                if(doc.exists) {
                    let data = doc.data();
                    if(data.roomBg) document.getElementById('chatBox').style.backgroundImage = `url('${data.roomBg}')`;
                    
                    let ytSection = document.getElementById('youtubePlayerSection');
                    let chatBox = document.getElementById('chatBox');
                    if(data.activeAudioId) {
                        ytSection.style.display = "block";
                        chatBox.style.paddingTop = "245px"; 
                        ytSection.innerHTML = `<iframe width="100%" height="100%" src="https://www.youtube.com/embed/${data.activeAudioId}?autoplay=1&controls=1&rel=0" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen></iframe>`;
                    } else {
                        ytSection.style.display = "none";
                        chatBox.style.paddingTop = "135px";
                        ytSection.innerHTML = "";
                    }
                }
            });
        },
        listenToGlobalRoomsList: () => {
            db.collection("global_rooms").doc("list").onSnapshot((doc) => {
                if(doc.exists) {
                    window.roomsList = doc.data().names || ["العام"];
                } else {
                    window.roomsList = ["العام"];
                    db.collection("global_rooms").doc("list").set({ names: ["العام"] });
                }
                let modalTitle = document.getElementById('featureModalTitle');
                if (modalTitle && modalTitle.innerText.includes("غرف دردشة") && document.getElementById('featureModal').style.display === 'flex') {
                    ui.updateRoomsManagerUI();
                }
            });
        },
        listenToGlobalMessages: () => {
            if(window.unsubscribeMessages) window.unsubscribeMessages();
            window.unsubscribeMessages = db.collection("rooms").doc(window.currentRoom).collection("messages").orderBy("timestamp", "asc").limitToLast(20).onSnapshot((snapshot) => {
                  let chatBox = document.getElementById('chatBox'); chatBox.innerHTML = "";
                  
                  if(snapshot.empty) {
                      chatBox.innerHTML = `<div class="system-message-wrap">✨ تم تنظيف الروم فوراً بواسطة الإدارة 👋</div>`;
                      return;
                  }

                  snapshot.forEach((doc) => {
                      let mData = doc.data();
                      if (mData.isSystemWelcome) {
                          ui.renderSystemWelcomeMsg(mData.text);
                      } else if (mData.user) {
                          ui.renderMsg(mData.user, mData.text, mData.timeStr);
                      }
                  });
              });
        },
        listenToActiveMics: () => {
            db.collection("rooms").doc(window.currentRoom).collection("mics").onSnapshot((snapshot) => {
                  window.currentActiveMicsMap = {};
                  for(let i=1; i<=4; i++) {
                      let slot = document.getElementById(`mic_${i}`); slot.classList.remove('occupied'); slot.style.backgroundImage = 'none';
                      document.getElementById(`micName_${i}`).innerText = `مايك ${i} فارغ`;
                      document.getElementById(`glow_${i}`).style.display = 'none';
                      document.getElementById(`mBadge_${i}`).style.display = 'none';
                  }
                  snapshot.forEach((doc) => {
                      let micData = doc.data(); let num = micData.micNum;
                      
                      let liveUser = window.liveUsersMap[micData.userId] || {};
                      let liveName = liveUser.name || micData.userName;
                      let liveImg = liveUser.img || micData.userImg;
                      
                      window.currentActiveMicsMap[num] = micData;
                      let slot = document.getElementById(`mic_${num}`); slot.classList.add('occupied');
                      slot.style.backgroundImage = `url('${liveImg}')`;
                      document.getElementById(`micName_${num}`).innerText = liveName;
                      document.getElementById(`glow_${num}`).style.display = 'block';
                      document.getElementById(`mBadge_${num}`).style.display = micData.isMuted ? 'block' : 'none';
                  });
              });
        },
        listenOnlineUsersRealtime: () => {
            db.collection("users").onSnapshot((snap) => {
                let list = []; 
                window.roomsCountMap = {}; 
                
                snap.forEach(doc => { 
                    let u = doc.data(); 
                    window.liveUsersMap[u.uid] = u;
                    
                    if(u.isOnline) {
                        list.push(u);
                        let rName = u.currentRoom || "العام";
                        window.roomsCountMap[rName] = (window.roomsCountMap[rName] || 0) + 1;
                    }
                });
                list.sort((a, b) => (window.rolesOrder[a.role] || 99) - (window.rolesOrder[b.role] || 99));

                document.getElementById('onlineUsersListBody').innerHTML = list.map(u => {
                    let r = window.chatRanksData[u.role] || { icon: "fas fa-user", color: "#fff", text: "عضو" };
                    return `
                        <div class="menu-item" onclick="ui.viewProfileCard('${u.uid}')">
                            <span style="color:${r.color}; font-weight: bold;"><i class="${r.icon}"></i> ${u.name}</span>
                            <span style="font-size:10px; color:${r.color}; border: 1px solid ${r.color}; padding: 2px 6px; border-radius: 10px;">${r.text}</span>
                        </div>
                    `;
                }).join('');
                
                let modalTitle = document.getElementById('featureModalTitle');
                if (modalTitle && modalTitle.innerText.includes("غرف دردشة") && document.getElementById('featureModal').style.display === 'flex') {
                    ui.updateRoomsManagerUI();
                }
            });
        },
        sendMessage: () => {
            if(window.currentUser.isMuted) { alert("أنت مكتوم من الإدارة حالياً!"); return; }
            let inp = document.getElementById('msgInp'); let t = inp.value.trim(); if(!t) return;
            inp.value = '';

            let d = new Date();
            let timeStr = d.getHours() + ":" + (d.getMinutes() < 10 ? '0' : '') + d.getMinutes();

            db.collection("users").doc(window.currentUser.uid).get().then((doc) => {
                let freshUser = doc.exists ? doc.data() : window.currentUser;
                
                let currentCount = (freshUser.msgCount || 0) + 1;
                let currentGold = freshUser.gold || 0;
                let currentGems = freshUser.gems || 0;
                let currentLevel = freshUser.level || 1;

                if (currentCount === 20) {
                    currentGold += 1;
                    currentGems += 1;
                    alert("🎁 تهانينا! حصلت على 1 ذهب و 1 جواهر لإرسالك 20 رسالة عامة!");
                }
                if (currentCount === 50) {
                    currentLevel += 1;
                    alert("👑 رائع جداً! تم ترقية مستواك السحابي لإرسالك 50 رسالة!");
                }

                let updatedUserData = {
                    msgCount: currentCount,
                    gold: currentGold,
                    gems: currentGems,
                    level: currentLevel
                };

                db.collection("users").doc(window.currentUser.uid).update(updatedUserData);
                window.currentUser = { ...window.currentUser, ...updatedUserData };
                localStorage.setItem("hassouni_user_session", JSON.stringify(window.currentUser));

                db.collection("rooms").doc(window.currentRoom).collection("messages").add({
                    user: { uid: freshUser.uid },
                    text: t, timeStr: timeStr, timestamp: firebase.firestore.FieldValue.serverTimestamp()
                });
            });
        },
        renderMsg: (user, text, timeStr) => {
            let div = document.createElement('div'); 
            
            let liveUser = window.liveUsersMap[user.uid] || user;
            let displayImg = liveUser.img || "https://cdn-icons-png.flaticon.com/512/1042/1042291.png";
            let displayName = liveUser.name || "عضو";
            let displayRole = liveUser.role || "guest";
            
            div.className = `msg-wrap ${user.uid === window.currentUser.uid ? 'is-me-style' : ''}`;
            let r = window.chatRanksData[displayRole] || { icon: "fas fa-user", color: "#fff" };
            
            div.innerHTML = `
                <span class="msg-time-badge">${timeStr || ''}</span>
                <div class="msg-header">
                    <div class="pfp-main-frame"><img src="${displayImg}" class="pfp-main" onclick="ui.viewProfileCard('${user.uid}')"></div>
                    <div class="rank-standalone-icon" style="border-color:${r.color};"><i class="${r.icon}" style="color:${r.color};"></i></div>
                    <div class="king-name-container" style="border-color:${r.color}; background:rgba(0,0,0,0.6);" onclick="ui.quoteUser('${displayName}')">
                        <span class="king-name-tag" style="color:${r.color};">${displayName}</span>
                    </div>
                </div>
                <div class="msg-text">${text}</div>
            `;
            let box = document.getElementById('chatBox'); box.appendChild(div); box.scrollTop = box.scrollHeight;
        },
        quoteUser: (name) => {
            let inp = document.getElementById('msgInp');
            if(inp) {
                inp.value = ` ↩️ اقتباس [ ${name} ]: `;
                inp.focus();
            }
        },
        renderSystemWelcomeMsg: (text) => {
            let div = document.createElement('div');
            div.className = 'system-message-wrap';
            div.innerText = text;
            let box = document.getElementById('chatBox'); box.appendChild(div); box.scrollTop = box.scrollHeight;
        },
        clickMicSlot: (num) => {
            window.selectedMicNum = num;
            let existingMic = window.currentActiveMicsMap ? window.currentActiveMicsMap[num] : null;

            if(!existingMic) {
                let isAlreadyOnMic = false;
                if(window.currentActiveMicsMap) {
                    Object.values(window.currentActiveMicsMap).forEach(m => { if(m.userId === window.currentUser.uid) isAlreadyOnMic = true; });
                }
                if(isAlreadyOnMic) { alert("أنت بالفعل على ميكروفون حالي!"); return; }

                document.getElementById('featureModalTitle').innerText = "🎙️ حجز المايك السحابي";
                document.getElementById('featureModalBody').innerHTML = `
                    <p style="text-align:center;">هل تود الصعود للبث الصوتي حياً في مايك ${num}؟</p>
                    <button class="send-btn" style="width:100%; border-radius:8px;" onclick="ui.confirmMicGoingUp(true)">تأكيد الصعود الفوري</button>
                `;
                document.getElementById('featureModal').style.display = 'flex';
            } else {
                let canControl = (window.currentUser.uid === existingMic.userId || window.currentUser.role === 'owner' || window.currentUser.role === 'admin');
                if(!canControl) {
                    let nextFree = 0;
                    for(let i=1; i<=4; i++) { if(!window.currentActiveMicsMap[i]) { nextFree = i; break; } }
                    if(nextFree > 0) {
                        alert(`لا يمكنك الصعود للمايك الحالي، فهو محجوز! جاري توجيهك وصعودك على مايك شاغر رقم [ ${nextFree} ]`);
                        window.selectedMicNum = nextFree; ui.confirmMicGoingUp(true);
                    } else {
                        alert("لا يمكنك الصعود، المايك الحالي محجوز وكافة المايكات ممتلئة بالكامل!");
                    }
                    return;
                }

                document.getElementById('featureModalTitle').innerText = "🎛️ إدارة المايك الصوتي للروم";
                document.getElementById('featureModalBody').innerHTML = `
                    <div class="menu-item" onclick="ui.toggleMicVoiceState(${num}, false)"><i class="fas fa-microphone"></i> تفعيل الحديث وبث الصوت الحقيقي</div>
                    <div class="menu-item" onclick="ui.toggleMicVoiceState(${num}, true)"><i class="fas fa-microphone-slash"></i> كتم الصوت مؤقتاً</div>
                    <div class="menu-item" onclick="ui.openYouTubeSearchEngine()"><i class="fab fa-youtube" style="color:red;"></i> تشغيل صوت شيلة / أغنية يوتيوب للروم</div>
                    <div class="menu-item" onclick="ui.stopHiddenAudioPlayback()"><i class="fas fa-stop-circle"></i> إيقاف البث واليوتيوب فوراً</div>
                    <div class="menu-item" onclick="ui.vacateMicSlot(${num})" style="color:red; font-weight:bold;"><i class="fas fa-sign-out-alt"></i> النزول من المايك وفك الحجز</div>
                `;
                document.getElementById('featureModal').style.display = 'flex';
            }
        },
        confirmMicGoingUp: (status) => {
            document.getElementById('featureModal').style.display = 'none'; if(!status) return;
            db.collection("rooms").doc(window.currentRoom).collection("mics").doc(`mic_${window.selectedMicNum}`).set({
                micNum: window.selectedMicNum, userId: window.currentUser.uid, userName: window.currentUser.name, userImg: window.currentUser.img, isMuted: false, trackOwnerId: window.currentUser.uid
            });
        },
        toggleMicVoiceState: (num, shouldMute) => {
            db.collection("rooms").doc(window.currentRoom).collection("mics").doc(`mic_${num}`).update({ isMuted: shouldMute });
            document.getElementById('featureModal').style.display = 'none';
        },
        vacateMicSlot: (num) => {
            db.collection("rooms").doc(window.currentRoom).collection("mics").doc(`mic_${num}`).delete();
            document.getElementById('featureModal').style.display = 'none';
        },
        openYouTubeSearchEngine: () => {
            document.getElementById('featureModalTitle').innerText = "📺 مشغل ومزامِن اليوتيوب السحابي الحصري";
            document.getElementById('featureModalBody').innerHTML = `
                <div style="text-align:right;">
                    <input type="text" id="ytLinkInput" class="form-control" placeholder="ضع رابط اليوتيوب هنا..." oninput="ui.previewYoutubeTrack()">
                    <div id="ytSearchPreviewContainer"></div>
                </div>
            `;
            document.getElementById('featureModal').style.display = 'flex';
        },
        previewYoutubeTrack: () => {
            let link = document.getElementById('ytLinkInput').value.trim(); let videoId = extractYouTubeVideoId(link);
            let container = document.getElementById('ytSearchPreviewContainer');
            if (videoId) {
                container.innerHTML = `
                    <div class="yt-preview-card" onclick="ui.processAndPlayYoutubeLink('${videoId}')">
                        <i class="fab fa-youtube yt-preview-icon"></i>
                        <div style="flex:1; text-align:right;">
                            <span style="color:#fff; font-size:13px; font-weight:bold; display:block;">🎵 تم العثور على المسار بنجاح</span>
                            <span style="color:var(--gold); font-size:11px;">اضغط هنا الآن لإطلاق البث الصوتي المباشر للجميع 🚀</span>
                        </div>
                    </div>
                `;
            } else { container.innerHTML = ""; }
        },
        processAndPlayYoutubeLink: (vId) => {
            let existingMic = window.currentActiveMicsMap ? window.currentActiveMicsMap[window.selectedMicNum] : null;
            if(existingMic && existingMic.trackOwnerId && existingMic.trackOwnerId !== window.currentUser.uid && window.currentUser.role !== 'owner' && window.currentUser.role !== 'admin') {
                alert("لا يمكنك التحكم، هناك صوت يعمل مسبقاً!"); return;
            }
            db.collection("room_settings").doc(window.currentRoom).set({ activeAudioId: vId, currentTrackOwner: window.currentUser.uid }, { merge: true }).then(() => {
                if(window.selectedMicNum) {
                    db.collection("rooms").doc(window.currentRoom).collection("mics").doc(`mic_${window.selectedMicNum}`).update({ trackOwnerId: window.currentUser.uid });
                }
                alert("🔊 تم إطلاق وتثبيت الصوت والمزامنة الفورية!"); document.getElementById('featureModal').style.display = 'none';
            });
        },
        stopHiddenAudioPlayback: () => {
            db.collection("room_settings").doc(window.currentRoom).get().then((doc) => {
                if(doc.exists) {
                    let data = doc.data();
                    if(data.currentTrackOwner && data.currentTrackOwner !== window.currentUser.uid && window.currentUser.role !== 'owner' && window.currentUser.role !== 'admin') {
                        alert("عذراً، هذا البث محمي!"); return;
                    }
                    db.collection("room_settings").doc(window.currentRoom).set({ activeAudioId: "", currentTrackOwner: "" }, { merge: true }).then(() => {
                        alert("تم إيقاف الصوت لدى الجميع."); document.getElementById('featureModal').style.display = 'none';
                    });
                }
            });
        },
        toggleOnlineUsers: () => {
            let m = document.getElementById('onlineUsersHalfModal'); m.style.display = (m.style.display === 'block') ? 'none' : 'block';
        },
        viewProfileCard: (uid) => {
            db.collection("users").doc(uid).get().then((doc) => {
                if(!doc.exists) return; let u = doc.data();
                let isMe = (window.currentUser.uid === uid); let isAmOwner = (window.currentUser.role === 'owner' || window.currentUser.role === 'admin');
                
                document.getElementById('featureModalTitle').innerText = "الملف الشخصي الفوري المزامَن";
                let editBtnHtml = isMe && (window.currentUser.role !== 'guest') ? `<button class="row-btn" style="width:100%; margin-bottom:10px;" onclick="ui.openEditProfileModal('${uid}')"><i class="fas fa-pencil-alt"></i> تعديل بيانات ملفي</button>` : '';
                let adminOptionsBtn = isAmOwner && !isMe ? `<button class="send-btn" style="width:100%; margin-top:10px; background:linear-gradient(to left, #cb2d3e, #ef473a); color:#fff;" onclick="ui.openAdminControls('${uid}')">⚙️ إدارة الرتب والإجراءات</button>` : '';
                let r = window.chatRanksData[u.role] || { icon: "fas fa-user", color: "#fff", text: "عضو" };

                document.getElementById('featureModalBody').innerHTML = `
                    <div class="profile-card-wrapper">
                        <img src="${u.cover || 'https://images.unsplash.com/photo-1618005182384-a83a8bd57fbe?q=80&w=400'}" class="profile-card-cover">
                        <img src="${u.img || 'https://cdn-icons-png.flaticon.com/512/1042/1042291.png'}" class="profile-card-pfp">
                        <h2 style="color:${r.color}; margin:5px 0 2px;">${u.name}</h2>
                        <p style="margin:0 0 10px; font-size:12px; color:${r.color}; font-weight:bold;"><i class="${r.icon}"></i> ${r.text}</p>
                        <p style="margin:0 0 10px; font-size:12px; color:#aaa; font-style: italic;">"${u.status || 'لا توجد حالة إمبراطورية بعد'}"</p>
                        
                        <div class="profile-action-bar">
                            <div class="profile-bar-btn" onclick="ui.likeProfile('${uid}')"><i class="fas fa-heart"></i> <span id="likeCountText">${u.likes || 0}</span> إعجاب</div>
                            <div class="profile-bar-btn" onclick="ui.startPrivateChatWithUser('${u.uid}', '${u.name}')"><i class="fas fa-paper-plane"></i> الخاص</div>
                            <div class="profile-bar-btn"><i class="fas fa-chart-line"></i> ليفل ${u.level || 1}</div>
                        </div>
                        <div style="background:rgba(255,215,0,0.1); border:1px solid var(--gold); border-radius:8px; padding:6px; margin-bottom:10px; font-size:11px; color:var(--gold);">
                            🪙 الذهب: ${u.gold || 0} | 💎 الجواهر: ${u.gems || 0} | ✉️ الرسائل: ${u.msgCount || 0}
                        </div>
                        ${editBtnHtml}
                        <div class="profile-details-grid">
                            <div class="profile-grid-row"><span>العمر المستعار:</span><span>${u.age || 'غير محدد'}</span></div>
                            <div class="profile-grid-row"><span>الجنس الحالي:</span><span>${u.gender || 'غير محدد'}</span></div>
                            <div class="profile-grid-row"><span>البلد أو الإقامة:</span><span>${u.country || 'اليمن'}</span></div>
                        </div>
                        ${adminOptionsBtn}
                    </div>
                `;
                document.getElementById('featureModal').style.display = 'flex';
            });
        },
        likeProfile: (uid) => {
            db.collection("users").doc(uid).update({ likes: firebase.firestore.FieldValue.increment(1) }).then(() => {
                let el = document.getElementById('likeCountText'); if(el) el.innerText = parseInt(el.innerText) + 1;
            });
        },
        handleLocalFileProcessing: (inputEl, type) => {
            let file = inputEl.files[0]; if (!file) return;
            let reader = new FileReader();
            reader.onload = (e) => {
                if (type === 'cover') { window.tempUploadedCover = e.target.result; alert("تم معالجة غلاف الحساب حياً وجاهز للحفظ!"); }
                else if (type === 'pfp') { window.tempUploadedPfp = e.target.result; alert("تم معالجة الصورة الشخصية حياً وجاهزة للحفظ!"); }
                else if (type === 'roomBg') { window.tempUploadedRoomBg = e.target.result; alert("تم معالجة خلفية الروم العامة!"); }
            };
            reader.readAsDataURL(file);
        },
        openEditProfileModal: (uid) => {
            db.collection("users").doc(uid).get().then((doc) => {
                let u = doc.data(); window.tempUploadedCover = u.cover || ""; window.tempUploadedPfp = u.img || "";
                document.getElementById('featureModalTitle').innerText = "تعديل الملف والاسم المزخرف والغلاف";
                document.getElementById('featureModalBody').innerHTML = `
                    <div style="text-align:right;">
                        <label for="fileCover" class="file-input-label">🖼️ اختيار صورة غلاف جديدة</label>
                        <input type="file" id="fileCover" class="file-input-hidden" accept="image/*" onchange="ui.handleLocalFileProcessing(this, 'cover')">
                        <label for="filePfp" class="file-input-label">👤 اختيار صورة شخصية جديدة</label>
                        <input type="file" id="filePfp" class="file-input-hidden" accept="image/*" onchange="ui.handleLocalFileProcessing(this, 'pfp')">
                        
                        <label style="font-size:12px; color:var(--gold);">الاسم المستعار:</label>
                        <input type="text" id="editName" class="form-control" value="${u.name || ''}">
                        <label style="font-size:12px; color:var(--gold);">حالة البروفايل:</label>
                        <input type="text" id="editStatus" class="form-control" value="${u.status || ''}">
                        <label style="font-size:12px; color:var(--gold);">العمر:</label>
                        <input type="number" id="editAge" class="form-control" value="${u.age || ''}">
                        <label style="font-size:12px; color:var(--gold);">الجنس:</label>
                        <select id="editGender" class="form-select">
                            <option value="ذكر" ${u.gender==='ذكر'?'selected':''}>ذكر</option>
                            <option value="أنثى" ${u.gender==='أنثى'?'selected':''}>أنثى</option>
                        </select>
                        <label style="font-size:12px; color:var(--gold);">البلد:</label>
                        <input type="text" id="editCountry" class="form-control" value="${u.country || ''}">
                        
                        <button class="send-btn" style="width:100%; margin-top:10px; border-radius:8px;" onclick="ui.saveProfileEdits('${uid}')">حفظ التعديلات ونشرها للجميع فوراً</button>
                    </div>
                `;
            });
        },
        saveProfileEdits: (uid) => {
            let updated = {
                cover: window.tempUploadedCover || "https://images.unsplash.com/photo-1618005182384-a83a8bd57fbe?q=400", 
                img: window.tempUploadedPfp || "https://cdn-icons-png.flaticon.com/512/1042/1042291.png", 
                name: document.getElementById('editName').value.trim(),
                status: document.getElementById('editStatus').value.trim(), 
                age: document.getElementById('editAge').value.trim(),
                gender: document.getElementById('editGender').value, 
                country: document.getElementById('editCountry').value.trim()
            };
            db.collection("users").doc(uid).update(updated).then(() => {
                alert("تم المزامنة وتحديث الملف الشخصي للجميع!");
                if(window.currentUser.uid === uid) { 
                    window.currentUser = { ...window.currentUser, ...updated }; 
                    localStorage.setItem("hassouni_user_session", JSON.stringify(window.currentUser)); 
                    ui.listenOnlineUsersRealtime();
                }
                document.getElementById('featureModal').style.display = 'none';
            });
        },
        openAdminControls: (uid) => {
            db.collection("users").doc(uid).get().then((doc) => {
                let u = doc.data(); document.getElementById('featureModalTitle').innerText = `إدارة وتعيين رتبة: ${u.name}`;
                document.getElementById('featureModalBody').innerHTML = `
                    <div style="text-align:right;">
                        <select id="changeRoleSelect" class="form-select" onchange="ui.changeUserRole('${uid}', this.value)">
                            <option value="owner" ${u.role === 'owner' ? 'selected' : ''}>1- البرنس الأصلي (صاحب السيرفر 🏆)</option>
                            <option value="prince" ${u.role === 'prince' ? 'selected' : ''}>2- برنس إمبراطوري 🏆</option>
                            <option value="king" ${u.role === 'king' ? 'selected' : ''}>3- الملك الملكي 👑</option>
                            <option value="honor" ${u.role === 'honor' ? 'selected' : ''}>4- تاج الشرف 👑</option>
                            <option value="admin" ${u.role === 'admin' ? 'selected' : ''}>5- الإدارة العليا 👑</option>
                            <option value="developer" ${u.role === 'developer' ? 'selected' : ''}>6- مطور السيرفر 💻</option>
                            <option value="senior_mod" ${u.role === 'senior_mod' ? 'selected' : ''}>7- مشرف أول 💎</option>
                            <option value="mod" ${u.role === 'mod' ? 'selected' : ''}>8- مشرف ⭐</option>
                            <option value="vip" ${u.role === 'vip' ? 'selected' : ''}>9- VIP ❤️‍🔥</option>
                            <option value="diamond" ${u.role === 'diamond' ? 'selected' : ''}>10- عضو ماسي 🔮</option>
                        </select>
                        <button class="send-btn" style="width:100%; margin-bottom:8px; background:${u.isMuted ? '#2ecc71' : '#f39c12'}; color:#fff;" onclick="ui.toggleUserMute('${uid}', ${!u.isMuted})">${u.isMuted ? '🔊 إلغاء الكتم' : '🔇 كتم صوت العضو'}</button>
                        <button class="send-btn" style="width:100%; margin-bottom:8px; background:${u.isBanned ? '#2ecc71' : '#e74c3c'}; color:#fff;" onclick="ui.toggleUserBan('${uid}', ${!u.isBanned})">${u.isBanned ? '✅ فك الطرد النهائي' : '🚫 حظر طرد نهائي سحابي'}</button>
                    </div>
                `;
            });
        },
        changeUserRole: (uid, newRole) => {
            db.collection("users").doc(uid).update({ role: newRole }).then(() => { alert("تم تعيين وتثبيت الرتبة بنجاح!"); });
        },
        toggleUserMute: (uid, state) => {
            db.collection("users").doc(uid).update({ isMuted: state }).then(() => { alert("تم تعديل حالة الكتم للعضو"); document.getElementById('featureModal').style.display = 'none'; });
        },
        toggleUserBan: (uid, state) => {
            db.collection("users").doc(uid).update({ isBanned: state }).then(() => { alert("تم تعديل حالة الحظر والطرد"); document.getElementById('featureModal').style.display = 'none'; });
        },
        openGlobalSettings: () => {
            document.getElementById('featureModalTitle').innerText = "إعدادات الروم والإدارة العليا";
            let isOwner = (window.currentUser.role === 'owner' || window.currentUser.role === 'admin'); window.tempUploadedRoomBg = "";
            
            let adminFields = isOwner ? `
                <div style="border-top:1px solid var(--gold); padding-top:10px; margin-top:10px; text-align:right;">
                    <label for="fileRoomBg" class="file-input-label">🖼️ اختيار خلفية الروم العامة السحابية</label>
                    <input type="file" id="fileRoomBg" class="file-input-hidden" accept="image/*" onchange="ui.handleLocalFileProcessing(this, 'roomBg')">
                    <button class="send-btn" style="width:100%; margin-bottom:8px;" onclick="ui.saveRoomBgSetting()">تحديث خلفية الروم حياً للجميع</button>
                </div>
            ` : '';

            let cleanRoomBtn = isOwner ? `<div class="menu-item" style="color:#e74c3c;" onclick="ui.cleanCurrentRoomMessages()"><i class="fas fa-trash-alt"></i> تنظيف وتطهير محادثات الروم العام فوراً</div>` : '';

            document.getElementById('featureModalBody').innerHTML = `
                ${cleanRoomBtn} ${adminFields}
                <div class="menu-item" style="color:#fff;" onclick="ui.logoutBackToWelcome()"><i class="fas fa-sign-out-alt"></i> تسجيل الخروج النهائي من الجلسة</div>
            `;
            document.getElementById('featureModal').style.display = 'flex';
        },
        saveRoomBgSetting: () => {
            if(!window.tempUploadedRoomBg) { alert("اختر صورة الخلفية أولاً!"); return; }
            db.collection("room_settings").doc(window.currentRoom).set({ roomBg: window.tempUploadedRoomBg }, { merge: true }).then(() => { alert("تم تغيير وتثبيت الخلفية لجميع الأعضاء حياً!"); document.getElementById('featureModal').style.display = 'none'; });
        },
        cleanCurrentRoomMessages: () => {
            if(confirm("هل تود مسح وتنظيف الروم ومحو الرسائل فوراً من شاشات الجميع؟")) {
                db.collection("rooms").doc(window.currentRoom).collection("messages").get().then((snap) => {
                    let batch = db.batch();
                    snap.forEach(doc => batch.delete(doc.ref));
                    batch.commit().then(() => {
                        document.getElementById('featureModal').style.display = 'none';
                    });
                });
            }
        },
        openRoomsManager: () => {
            document.getElementById('featureModalTitle').innerText = "🗂️ غرف دردشة حسوني المزامنة حياً";
            ui.updateRoomsManagerUI();
            document.getElementById('featureModal').style.display = 'flex';
        },
        updateRoomsManagerUI: () => {
            let roomsHtml = `<div style="max-height: 40vh; overflow-y: auto; padding: 2px;">`;
            
            window.roomsList.forEach(r => {
                let count = window.roomsCountMap[r] || 0;
                let activeBadge = window.currentRoom === r ? `<span style="color:var(--gold); font-size:12px; font-weight:bold;"><i class="fas fa-trophy"></i> متواجد هنا</span>` : '';
                roomsHtml += `
                    <div class="room-item-box" onclick="ui.changeActiveRoom('${r}')">
                        <div style="text-align:right;">
                            <strong style="color:#fff; font-size:14px;"><i class="fas fa-door-open" style="color:var(--gold); margin-left:6px;"></i> ${r}</strong>
                            <div style="font-size:11px; color:#aaa; margin-top:4px;"><i class="fas fa-users"></i> عدد الأعضاء: <span style="color:#2ecc71; font-weight:bold;">${count}</span></div>
                        </div>
                        <div>${activeBadge}</div>
                    </div>
                `;
            });
            roomsHtml += `</div>`;
            
            if(window.currentUser && window.currentUser.role === 'owner') {
                roomsHtml += `
                    <div style="margin-top:15px; border-top:1.5px dashed var(--gold); padding-top:12px; text-align:right;">
                        <span style="color:var(--gold); font-size:12px; font-weight:bold; display:block; margin-bottom:8px;"><i class="fas fa-crown"></i> صلاحيات ملك الموقع الحصرية:</span>
                        <input type="text" id="newRoomNameInp" class="form-control" placeholder="اكتب اسم الغرفة الجديدة...">
                        <button class="send-btn" style="width:100%; border-radius:8px;" onclick="ui.createNewRoomCloud()">➕ إنشاء الغرفة حياً للجميع</button>
                    </div>
                `;
            }
            document.getElementById('featureModalBody').innerHTML = roomsHtml;
        },
        createNewRoomCloud: () => {
            let rName = document.getElementById('newRoomNameInp').value.trim(); if(!rName) return;
            db.collection("global_rooms").doc("list").update({
                names: firebase.firestore.FieldValue.arrayUnion(rName)
            }).then(() => {
                alert(`تم إنشاء الغرفة سحابياً [ ${rName} ] وتثبيتها للجميع بنجاح!`); 
                ui.updateRoomsManagerUI(); 
            }).catch(() => {
                db.collection("global_rooms").doc("list").set({ names: [rName] }, {merge: true});
            });
        },
        changeActiveRoom: (r) => { 
            if(window.currentRoom === r) return;
            window.currentRoom = r; 
            document.getElementById('chatBox').innerHTML = ""; 
            document.getElementById('featureModal').style.display = 'none'; 
            ui.enterChat();
            alert(`🚀 تم انتقالك بنجاح إلى غرفة [ ${r} ]`);
        },
        refreshChatWindowOnly: () => { ui.enterChat(); alert("تم إنعاش وتحديث غرف الدردشة بنجاح وبسرعة!"); },
        logoutBackToWelcome: () => {
            if(window.sessionListenerUnsubscribe) window.sessionListenerUnsubscribe();
            if(window.currentUser) {
                db.collection("users").doc(window.currentUser.uid).update({ isOnline: false, sessionToken: "", currentRoom: "" }).then(() => {
                    localStorage.removeItem("hassouni_user_session");
                    window.location.reload();
                }).catch(() => {
                    localStorage.removeItem("hassouni_user_session");
                    window.location.reload();
                });
            } else {
                localStorage.removeItem("hassouni_user_session");
                window.location.reload();
            }
        },

        startPrivateChatWithUser: (targetUid, targetName) => {
            if(targetUid === window.currentUser.uid) { alert("لا يمكنك مراسلة نفسك خاص!"); return; }
            
            document.getElementById('topPrivateIcon').classList.remove('has-new-private');
            delete window.privateNotificationsMap[targetUid];

            document.getElementById('featureModalTitle').innerText = `💬 الخاص الإمبراطوري مع: ${targetName}`;
            
            document.getElementById('featureModalBody').innerHTML = `
                <div class="private-room-container">
                    <div class="private-messages-area" id="privateMessagesArea"></div>
                    <div class="private-input-row">
                        <input type="text" id="pMsgInp" class="chat-input" placeholder="اكتب رسالة خاصة وسرية..." style="height:36px;">
                        <button class="send-btn" style="height:36px; padding:0 12px; font-size:12px;" onclick="ui.sendPrivateMessageCloud('${targetUid}')">إرسال</button>
                    </div>
                </div>
            `;

            const privateRoomId = [window.currentUser.uid, targetUid].sort().join('_');
            
            if(window.unsubscribePrivateRoom) window.unsubscribePrivateRoom();

            window.unsubscribePrivateRoom = db.collection("private_chats").doc(privateRoomId).collection("messages").orderBy("timestamp", "asc").onSnapshot((snap) => {
                let area = document.getElementById('privateMessagesArea');
                if(!area) return;
                area.innerHTML = "";
                snap.forEach((doc) => {
                    let m = doc.data();
                    let bubble = document.createElement('div');
                    bubble.style.padding = "6px 10px";
                    bubble.style.borderRadius = "10px";
                    bubble.style.fontSize = "12px";
                    bubble.style.maxWidth = "80%";
                    bubble.style.wordBreak = "break-word";
                    
                    if(m.senderId === window.currentUser.uid) {
                        bubble.style.alignSelf = "flex-end";
                        bubble.style.background = "var(--king-grad)";
                        bubble.style.color = "#000";
                        bubble.innerHTML = `<b>أنا:</b> ${m.text}`;
                    } else {
                        bubble.style.alignSelf = "flex-start";
                        bubble.style.background = "#222";
                        bubble.style.color = "#fff";
                        bubble.style.border = "1px solid #333";
                        bubble.innerHTML = `<b>${m.senderName}:</b> ${m.text}`;
                    }
                    area.appendChild(bubble);
                });
                area.scrollTop = area.scrollHeight;
            });
        },
        sendPrivateMessageCloud: (targetUid) => {
            let inp = document.getElementById('pMsgInp');
            if(!inp) return;
            let txt = inp.value.trim();
            if(!txt) return;
            inp.value = "";

            const privateRoomId = [window.currentUser.uid, targetUid].sort().join('_');
            
            db.collection("private_chats").doc(privateRoomId).collection("messages").add({
                senderId: window.currentUser.uid,
                senderName: window.currentUser.name,
                receiverId: targetUid,
                text: txt,
                timestamp: firebase.firestore.FieldValue.serverTimestamp()
            });

            db.collection("private_chats").doc(privateRoomId).set({
                lastSenderId: window.currentUser.uid,
                lastSenderName: window.currentUser.name,
                receiverId: targetUid,
                lastMessageText: txt,
                timestamp: firebase.firestore.FieldValue.serverTimestamp()
            }, { merge: true });
        },
        listenToPrivateMessagesNotifications: () => {
            db.collection("private_chats").where("receiverId", "==", window.currentUser.uid).onSnapshot((snap) => {
                let hasUnread = false;
                snap.forEach((doc) => {
                    let data = doc.data();
                    if(data.lastSenderId !== window.currentUser.uid) {
                        window.privateNotificationsMap[data.lastSenderId] = data.lastSenderName;
                        hasUnread = true;
                    }
                });
                let topBarBtn = document.getElementById('topPrivateIcon');
                if(topBarBtn) {
                    if(hasUnread && Object.keys(window.privateNotificationsMap).length > 0) {
                        topBarBtn.classList.add('has-new-private');
                    } else {
                        topBarBtn.classList.remove('has-new-private');
                    }
                }
            });
        },
        clickTopPrivateButton: () => {
            let activeKeys = Object.keys(window.privateNotificationsMap);
            if(activeKeys.length === 0) {
                alert("📭 صندوق الرسائل الخاصة فارغ حالياً، لا توجد إشعارات جديدة.");
                return;
            }
            
            document.getElementById('featureModalTitle').innerText = "📬 إشعارات الخاص الجديدة";
            document.getElementById('featureModalBody').innerHTML = `
                <div style="max-height: 40vh; overflow-y: auto;">
                    ${activeKeys.map(k => `
                        <div class="menu-item" onclick="ui.startPrivateChatWithUser('${k}', '${window.privateNotificationsMap[k]}')">
                            <span style="color:var(--gold); font-weight:bold;"><i class="fas fa-comment-dots"></i> رسالة جديدة من: ${window.privateNotificationsMap[k]}</span>
                            <button class="send-btn" style="height:28px; padding:0 10px; font-size:11px; border-radius:5px;">فتح</button>
                        </div>
                    `).join('')}
                </div>
            `;
            document.getElementById('featureModal').style.display = 'flex';
        }
    };

    window.onload = () => { ui.checkSavedSessionOnLoad(); };
</script>
</body>
</html>
