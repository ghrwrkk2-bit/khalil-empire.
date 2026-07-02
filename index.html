<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>شات حسوني المطور - النسخة الماسية المتكاملة</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    
    <script src="https://www.gstatic.com/firebasejs/10.7.1/firebase-app-compat.js"></script>
    <script src="https://www.gstatic.com/firebasejs/10.7.1/firebase-database-compat.js"></script>

    <style>
        * { box-sizing: border-box; margin: 0; padding: 0; font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif; }
        body { background-color: #f0f2f5; display: flex; justify-content: center; align-items: center; height: 100vh; overflow: hidden; }

        /* حاوية الشات الرئيسية */
        .chat-container { width: 100%; max-width: 480px; height: 100vh; background-color: #f7f9fa; display: flex; flex-direction: column; position: relative; background-size: cover; background-position: center; }

        /* لوحة الدخول البدئية */
        #welcomeWelcomePanel { position: absolute; top:0; left:0; width:100%; height:100%; background:#fff; z-index: 5000; overflow-y: auto; padding: 15px; }
        .gold-banner { background: linear-gradient(135deg, #ffd700, #aa7c11); color: #fff; padding: 20px; text-align: center; border-radius: 12px; box-shadow: 0 4px 15px rgba(0,0,0,0.15); margin-bottom: 15px; }
        .gold-banner h1 { font-size: 24px; margin-bottom: 5px; text-shadow: 1px 1px 3px rgba(0,0,0,0.3); font-weight: bold; }
        .enter-form { background: #fdfdfd; border: 1px solid #ffd700; padding: 15px; border-radius: 12px; margin-bottom: 15px; }
        .styled-enter-btn { width: 100%; padding: 12px; background: linear-gradient(135deg, #2a2a35, #1e1e24); color:#ffd700; border:2px solid #ffd700; font-weight:bold; font-size:16px; border-radius:30px; cursor:pointer; margin-top:10px; transition: 0.3s; }
        .styled-enter-btn:hover { background: #ffd700; color:#1e1e24; }

        /* معلومات اللوحة الإرشادية لشات حسوني */
        .promo-section { background: #f8f9fa; padding: 12px; border-radius: 10px; border-right: 4px solid #ffd700; margin-bottom: 12px; text-align: right; }
        .promo-section h3 { font-size: 14px; color: #1e1e24; margin-bottom: 4px; display: flex; align-items: center; gap: 6px; }
        .promo-section p { font-size: 12px; color: #4a5568; line-height: 1.6; }

        /* الشريط العلوي */
        .chat-header { background: linear-gradient(135deg, #1e1e24, #2a2a35); color: #fff; padding: 10px; border-bottom: 2px solid #ffd700; flex-shrink: 0; }
        .header-top-row { display: flex; justify-content: space-between; align-items: center; margin-bottom: 6px; }
        .logo-area { font-weight: bold; font-size: 15px; color: #ffd700; display: flex; align-items: center; gap: 6px; }
        .header-nav-menu { display: flex; justify-content: space-between; background: rgba(255, 255, 255, 0.08); padding: 4px; border-radius: 8px; gap: 2px; }
        .nav-item { flex: 1; text-align: center; font-size: 11px; color: #e2e8f0; cursor: pointer; padding: 4px 2px; border-radius: 4px; display: flex; flex-direction: column; align-items: center; gap: 2px; }

        /* قسم المايكات المطور */
        .mics-section { background-color: #ffffff; display: flex; justify-content: space-around; padding: 10px 5px; border-bottom: 1px solid #e1e8ed; flex-shrink: 0; gap: 10px; }
        .mic-box { display: flex; flex-direction: column; align-items: center; flex: 1; background: #ffffff; border-radius: 12px; padding: 8px 4px; cursor: pointer; box-shadow: 0 2px 5px rgba(0,0,0,0.05); border: 1px solid #edf2f7; transition: all 0.3s ease; position: relative; background-size: cover; background-position: center; }
        .mic-box.active { border: 2px solid #e53e3e; box-shadow: 0 0 8px rgba(229, 62, 62, 0.4); }
        
        .heart-icon-wrapper { position: relative; width: 24px; height: 22px; margin-bottom: 6px; margin-top: 5px; z-index: 2; }
        .heart-icon-wrapper::before, .heart-icon-wrapper::after { content: ""; position: absolute; top: 0; width: 12px; height: 20px; border-radius: 10px 10px 0 0; background: #cbd5e0; }
        .heart-icon-wrapper::before { left: 12px; transform: rotate(-45deg); transform-origin: 0 100%; }
        .heart-icon-wrapper::after { left: 0; transform: rotate(45deg); transform-origin: 100% 100%; }
        
        .mic-box.active .heart-icon-wrapper::before, .mic-box.active .heart-icon-wrapper::after { background: #e53e3e; }
        .mic-box.muted .heart-icon-wrapper::before, .mic-icon-wrapper::after { background: #718096; }
        .heart-inner-icon { position: absolute; z-index: 5; top: 2px; left: 5px; color: #fff; font-size: 9px; width: 14px; text-align: center; }
        
        .mic-name { font-size: 10px; color: #4a5568; font-weight: bold; text-align: center; width: 100%; overflow: hidden; text-overflow: ellipsis; white-space: nowrap; z-index: 2; background: rgba(255, 255, 255, 0.85); padding: 1px 2px; border-radius: 4px; }
        .mic-status-tag { font-size: 8px; color: #edf2f7; font-weight: bold; margin-top: 2px; display: none; z-index: 2; background: rgba(0,0,0,0.6); padding: 0 4px; border-radius: 4px; }
        .mic-box.muted .mic-status-tag { display: block; }

        /* ساحة الرسائل */
        .chat-messages { flex: 1; padding: 12px; overflow-y: auto; background-color: rgba(243, 244, 246, 0.85); display: flex; flex-direction: column; gap: 12px; padding-bottom: 115px; }
        .message-row { display: flex; align-items: flex-start; gap: 8px; width: 100%; }
        .avatar { width: 40px; height: 40px; border-radius: 50%; object-fit: cover; border: 2px solid #ffd700; cursor: pointer; }
        .message-content { flex: 1; display: flex; flex-direction: column; }
        
        .user-tag-bar { display: flex; align-items: center; gap: 8px; margin-bottom: 4px; }
        .username-container { border: 1px solid #cbd5e0; background-color: #ffffff; padding: 2px 8px; border-radius: 4px; font-size: 12px; font-weight: bold; color: #2d3748; }
        .message-text { background-color: #ffffff; color: #212529; padding: 8px 12px; border-radius: 8px; font-size: 13px; max-width: 85%; box-shadow: 0 1px 3px rgba(0,0,0,0.05); font-weight: 600; }

        /* التحكم السفلي الثابت */
        .bottom-controls-container { position: fixed; bottom: 0; left: 50%; transform: translateX(-50%); width: 100%; max-width: 480px; display: flex; flex-direction: column; z-index: 999; background-color: #fff; box-shadow: 0 -2px 10px rgba(0,0,0,0.05); }
        .chat-input-bar { background-color: #ffffff; padding: 8px 10px; display: flex; align-items: center; gap: 8px; border-top: 1px solid #e1e8ed; }
        .input-container { flex: 1; display: flex; align-items: center; background-color: #f1f3f5; border-radius: 20px; padding: 0 12px; }
        .chat-input { width: 100%; background: none; border: none; padding: 8px 0; outline: none; font-size: 14px; }
        .action-btn { width: 36px; height: 36px; border-radius: 50%; border: none; display: flex; justify-content: center; align-items: center; cursor: pointer; }
        
        .footer-nav-bar { background: #1e1e24; display: flex; justify-content: space-around; align-items: center; height: 50px; border-top: 2px solid #ffd700; }
        .footer-item { color: #a0aec0; font-size: 11px; text-align: center; cursor: pointer; display: flex; flex-direction: column; align-items: center; gap: 2px; flex: 1; }
        .footer-item.active, .footer-item:hover { color: #ffd700; }

        /* النوافذ المنبثقة */
        .popup-overlay { position: absolute; top: 0; left: 0; width: 100%; height: 100%; background: rgba(0,0,0,0.6); display: none; justify-content: center; align-items: center; z-index: 2000; padding: 10px; }
        .popup-box { background: white; width: 100%; max-width: 360px; border-radius: 12px; padding: 20px; position: relative; max-height: 90%; overflow-y: auto; }
        .close-x-btn { position: absolute; top: 10px; left: 10px; background: #e53e3e; color: white; border: none; width: 24px; height: 24px; border-radius: 50%; font-weight: bold; cursor: pointer; display: flex; justify-content: center; align-items: center; font-size: 12px; z-index: 10; }
        
        .form-group { text-align: right; margin-bottom: 12px; }
        .form-group label { font-size: 12px; font-weight: bold; color: #4a5568; display: block; margin-bottom: 4px; }
        .form-control { width: 100%; padding: 8px; border: 1px solid #cbd5e0; border-radius: 6px; outline: none; font-size: 13px; }
        .popup-btn { width: 100%; padding: 10px; background: #1a1a1a; color: white; border: none; border-radius: 6px; font-weight: bold; cursor: pointer; margin-top: 8px; }
        
        .confirm-btn-group { display: flex; gap: 10px; margin-top: 15px; }
        .btn-yes { flex: 1; background: #28a745; color: white; padding: 10px; border: none; border-radius: 6px; font-weight: bold; cursor: pointer; }
        .btn-no { flex: 1; background: #dc3545; color: white; padding: 10px; border: none; border-radius: 6px; font-weight: bold; cursor: pointer; }

        /* كارت البروفايل الإحترافي */
        .profile-card { background: #fff; width: 100%; max-width: 350px; border-radius: 14px; overflow: hidden; box-shadow: 0 10px 25px rgba(0,0,0,0.3); position: relative; text-align: center; padding-bottom: 15px; }
        .profile-cover { width: 100%; height: 110px; background: linear-gradient(135deg, #2c3e50, #3498db); background-size: cover; background-position: center; position: relative; }
        .profile-avatar-wrapper { position: relative; margin-top: -45px; display: inline-block; }
        .profile-card-avatar { width: 85px; height: 85px; border-radius: 50%; border: 3px solid #fff; object-fit: cover; background: #fff; }
        .profile-info-section { padding: 10px 15px; }
        .profile-name { font-size: 16px; font-weight: bold; color: #1a202c; padding: 4px 10px; border-radius: 6px; display: inline-block; }
        
        .profile-actions-bar { display: flex; justify-content: space-around; background: #f1f3f5; margin: 10px 15px 5px 15px; padding: 5px; border-radius: 20px; gap: 4px; }
        .prof-bar-btn { flex: 1; border: none; background: #fff; padding: 6px 2px; font-size: 11px; font-weight: bold; border-radius: 15px; cursor: pointer; color: #4a5568; box-shadow: 0 1px 3px rgba(0,0,0,0.05); display: flex; align-items: center; justify-content: center; gap: 2px; }
        .prof-bar-btn:hover { background: #ffd700; color: #1a1a1a; }

        .profile-advanced-grid { background: #f7f9fa; padding: 10px; border-radius: 8px; margin-top: 8px; font-size: 12px; text-align: right; display: flex; flex-direction: column; gap: 5px; }
        .profile-advanced-grid div { display: flex; justify-content: space-between; border-bottom: 1px dashed #edf2f7; padding-bottom: 3px; }
        
        .menu-list-item { display: flex; align-items: center; gap: 10px; padding: 12px; border-bottom: 1px solid #edf2f7; cursor: pointer; font-size: 14px; color: #2d3748; font-weight: 600; text-align: right; }
        .user-online-row { display: flex; align-items: center; justify-content: space-between; padding: 10px; border-bottom: 1px solid #edf2f7; cursor: pointer; }
        .user-online-avatar { width: 42px; height: 42px; border-radius: 50%; object-fit: cover; }
        .owner-gold-frame { border: 2.5px solid #ffd700 !important; box-shadow: 0 0 8px #ffd700; }
        .rank-badge-pill { padding: 3px 8px; font-size: 11px; border-radius: 12px; color: white; font-weight: bold; display: flex; align-items: center; gap: 3px; }
        
        .pencil-btn { position: absolute; top: 10px; right: 10px; background: rgba(0,0,0,0.6); color: #ffd700; width: 30px; height: 30px; border-radius: 50%; display: flex; justify-content: center; align-items: center; font-size: 13px; cursor: pointer; border: 1px solid #ffd700; z-index: 20; }
        #pinnedSpecialMsg { background: #fff3cd; border-bottom: 1px solid #ffeeba; color: #856404; padding: 8px 12px; font-size: 13px; font-weight: bold; text-align: center; display: none; }
    </style>
</head>
<body>

<div id="ytPlayerContainer" style="display:none; position:absolute; width:1px; height:1px; opacity:0;"></div>

<div class="chat-container" id="chatContainerView">

    <div id="welcomeWelcomePanel">
        <div class="gold-banner">
            <h1>✨ شات حسوني المطور ✨</h1>
            <p>مرحباً بك في موقعنا المتميز والأكبر عربياً</p>
        </div>
        
        <div class="enter-form">
            <div class="form-group">
                <label><i class="fa-solid fa-user"></i> الاسم المستعار</label>
                <input type="text" id="initNameInput" class="form-control" placeholder="اكتب اسمك هنا...">
            </div>
            <div class="form-group">
                <label><i class="fa-solid fa-venus-mars"></i> الجنس</label>
                <select id="initGenderInput" class="form-control">
                    <option value="ذكر">ذكر</option>
                    <option value="أنثى">أنثى</option>
                </select>
            </div>
            <div class="form-group">
                <label><i class="fa-solid fa-cake-candles"></i> العمر</label>
                <select id="initAgeInput" class="form-control"></select>
            </div>
            <div class="form-group">
                <label><i class="fa-solid fa-earth-americas"></i> البلاد</label>
                <input type="text" id="initCountryInput" class="form-control" value="العراق">
            </div>
            <button class="styled-enter-btn" onclick="loginAsVisitor()">دخول سريع للشات بنجاح 🚀</button>
        </div>

        <div class="promo-section">
            <h3><i class="fa-solid fa-radio" style="color:#e53e3e;"></i> غرف البث المباشر والصوت</h3>
            <p>استمتع بالاستماع إلى محطات الراديو المختلفة والصوتيات المتنوعة أثناء الدردشة ودخولك البث المباشر الخاص بالدردشة الكتابية.</p>
        </div>

        <div class="promo-section">
            <h3><i class="fa-solid fa-image" style="color:#3182ce;"></i> مشاركة الصور</h3>
            <p>يمكنك مشاركة الصور مباشرة من الإنترنت أو من جهازك الشخصي مع أصدقائك والجميع.</p>
        </div>

        <div class="promo-section">
            <h3><i class="fa-solid fa-clipboard-list" style="color:#ecc94b;"></i> حائط اليوميات</h3>
            <p>انشر يومياتك على حائطك الخاص، وشاركها مع أصدقائك ليطلعوا على كل جديد.</p>
        </div>

        <div class="promo-section">
            <h3><i class="fa-solid fa-shield-halved" style="color:#38a169;"></i> الأمان والخصوصية</h3>
            <p>شات حسوني المطور يضمن لك حماية وأمان بياناتك الشخصية، حيث يتم تشفير جميع البيانات والمعلومات. كل ما تنشره وتشاركه مع الآخرين هو مسؤوليتك الشخصية بالكامل.</p>
        </div>
    </div>
    
    <div class="chat-header">
        <div class="header-top-row">
            <div class="logo-area"><i class="fa-solid fa-heart" style="color: #e53e3e;"></i> شات حسوني</div>
            <div style="font-size: 11px; color: #ffd700;" id="topUserRank">زائر مؤقت</div>
        </div>
        <div class="header-nav-menu">
            <div class="nav-item" onclick="alert('بلاغ')"><i class="fa-solid fa-triangle-exclamation" style="color:#e53e3e;"></i>بلاغ</div>
            <div class="nav-item" onclick="alert('الخاص')"><i class="fa-solid fa-envelope" style="color:#3182ce;"></i>الخاص</div>
            <div class="nav-item" onclick="alert('الأثرياء')"><i class="fa-solid fa-gem" style="color:#ecc94b;"></i>الأثرياء</div>
            <div class="nav-item" onclick="alert('الكبار')"><i class="fa-solid fa-crown" style="color:#ed64a6;"></i>الكبار</div>
            <div class="nav-item" onclick="openRoomOptionsModal()"><i class="fa-solid fa-gear"></i>الخيارات</div>
        </div>
    </div>

    <div id="pinnedSpecialMsg"></div>

    <div class="mics-section">
        <div class="mic-box" id="micNode1" onclick="handleMicClick(1)"><div class="heart-icon-wrapper"><div class="heart-inner-icon"><i class="fa-solid fa-microphone"></i></div></div><div class="mic-name" id="mName1">فارغ</div><div class="mic-status-tag" id="mStatus1">مكتوم</div></div>
        <div class="mic-box" id="micNode2" onclick="handleMicClick(2)"><div class="heart-icon-wrapper"><div class="heart-inner-icon"><i class="fa-solid fa-microphone"></i></div></div><div class="mic-name" id="mName2">فارغ</div><div class="mic-status-tag" id="mStatus2">مكتوم</div></div>
        <div class="mic-box" id="micNode3" onclick="handleMicClick(3)"><div class="heart-icon-wrapper"><div class="heart-inner-icon"><i class="fa-solid fa-microphone"></i></div></div><div class="mic-name" id="mName3">فارغ</div><div class="mic-status-tag" id="mStatus3">مكتوم</div></div>
        <div class="mic-box" id="micNode4" onclick="handleMicClick(4)"><div class="heart-icon-wrapper"><div class="heart-inner-icon"><i class="fa-solid fa-microphone"></i></div></div><div class="mic-name" id="mName4">فارغ</div><div class="mic-status-tag" id="mStatus4">مكتوم</div></div>
    </div>

    <div class="chat-messages" id="chatMessages"></div>

    <div class="bottom-controls-container">
        <div class="chat-input-bar">
            <button class="action-btn plus-btn" onclick="alert('إرسال ميديا')"><i class="fa-solid fa-plus"></i></button>
            <div class="input-container">
                <input type="text" id="chatInput" class="chat-input" placeholder="اكتب رسالتك هنا...">
            </div>
            <button class="action-btn" id="sendBtn" style="background:#1a1a1a; color:#fff;"><i class="fa-solid fa-paper-plane"></i></button>
        </div>

        <div class="footer-nav-bar">
            <div class="footer-item" onclick="openOnlineUsersModal()"><i class="fa-solid fa-users"></i>المتواجدين</div>
            <div class="footer-item" onclick="refreshChatData();"><i class="fa-solid fa-rotate"></i>تحديث</div>
            <div class="footer-item" id="keyAuthBtn" onclick="openLoginModal()"><i class="fa-solid fa-key" style="color:#ffd700;"></i>التسجيل للابد</div>
            <div class="footer-item" onclick="alert('يوتيوب')"><i class="fa-brands fa-youtube" style="color:#ff0000;"></i>يوتيوب</div>
            <div class="footer-item" onclick="alert('الغرف')"><i class="fa-solid fa-door-open"></i>الغرف</div>
        </div>
    </div>

</div>

<div class="popup-overlay" id="profileCardModal">
    <div class="profile-card">
        <button class="close-x-btn" onclick="closeAllModals()">X</button>
        <div class="profile-cover" id="pCoverDisplay">
            <div class="pencil-btn" id="profilePenEditBtn" onclick="openProfileEditInputs()"><i class="fa-solid fa-pen"></i></div>
        </div>
        <div class="profile-avatar-wrapper">
            <img src="" class="profile-card-avatar" id="pAvatarDisplay">
        </div>
        <div class="profile-actions-bar">
            <button class="prof-bar-btn" onclick="alert('خلفية العضو')"><i class="fa-solid fa-image"></i> الخلفية</button>
            <button class="prof-bar-btn" onclick="alert('غلاف العضو')"><i class="fa-solid fa-photo-film"></i> الغلاف</button>
            <button class="prof-bar-btn" onclick="likeUserProfile()"><i class="fa-solid fa-heart" style="color:#e53e3e;"></i> لايك (<span id="pLikesDisplay">0</span>)</button>
            <button class="prof-bar-btn" onclick="alert('فتح محادثة خاصة')"><i class="fa-solid fa-envelope" style="color:#3182ce;"></i> الخاص</button>
        </div>
        <div class="profile-info-section">
            <div class="profile-name" id="pNameDisplay">اسم العضو</div>
            <div id="pStatusTextDisplay" style="font-size:13px; color:#718096; margin:4px 0;">الحالة الشخصية</div>
            <div class="profile-advanced-grid">
                <div><strong>الرتبة:</strong> <span id="pRankDisplay">--</span></div>
                <div><strong>العمر:</strong> <span id="pAgeDisplay">--</span></div>
                <div><strong>الجنس:</strong> <span id="pGenderDisplay">--</span></div>
                <div><strong>البلاد:</strong> <span id="pCountryDisplay">--</span></div>
            </div>
            <div style="font-size:11px; text-align:center; color:#2b6cb0; padding:5px; background:#edf2f7; border-radius:6px; margin-top:8px; word-break: break-all;">
                <strong>رابط الملف:</strong> <span id="pProfileUrlLink">--</span>
            </div>
            <button id="adminOperationsBtn" class="popup-btn" style="background:#e53e3e; color:#fff; display:none; margin-top:10px;" onclick="openAdminOperationsModal()">🛠️ زر أوامر الإدارة</button>
        </div>
    </div>
</div>

<div class="popup-overlay" id="adminOperationsModal">
    <div class="popup-box">
        <button class="close-x-btn" onclick="closeAllModals()">X</button>
        <h3 style="text-align:center; margin-bottom:15px; font-size:16px; color:#e53e3e;"><i class="fa-solid fa-shield-halved"></i> لوحة تحكم الإدارة</h3>
        <div class="form-group">
            <label>تغيير رتبة العضو:</label>
            <select id="adminRankSelector" class="form-control"></select>
        </div>
        <button class="popup-btn" style="background:#2b6cb0; margin-bottom:10px;" onclick="executeRankChangeByAdmin()">تثبيت وتغيير الرتبة فورا</button>
        <hr style="margin:10px 0; border:0; border-top:1px solid #e2e8f0;">
        <button class="popup-btn" style="background:#ecc94b; color:#1a1a1a;" onclick="executeAdminAction('كتم')">🚫 كتم العضو</button>
        <button class="popup-btn" style="background:#dd6b20;" onclick="executeAdminAction('طرد')">🚪 طرد العضو</button>
        <button class="popup-btn" style="background:#e53e3e;" onclick="executeAdminAction('حظر')">🔨 حظر العضو (باند)</button>
    </div>
</div>

<div class="popup-overlay" id="editProfileFieldsModal">
    <div class="popup-box">
        <button class="close-x-btn" onclick="closeAllModals()">X</button>
        <h3 style="text-align:center; margin-bottom:12px; font-size:15px;"><i class="fa-solid fa-user-pen"></i> تعديل البروفايل الشخصي</h3>
        <div class="form-group"><label>الاسم المستعار:</label><input type="text" id="editProfileName" class="form-control"></div>
        <div class="form-group"><label>الحالة الشخصية:</label><input type="text" id="editProfileStatus" class="form-control"></div>
        <div class="form-group"><label>العمر:</label><input type="number" id="editProfileAge" class="form-control"></div>
        <div class="form-group"><label>البلاد:</label><input type="text" id="editProfileCountry" class="form-control"></div>
        <div class="form-group"><label>لون خلفية الاسم:</label><input type="color" id="editProfileNameBg" class="form-control" style="height:40px; padding:2px;"></div>
        <button class="popup-btn" style="background:#ffd700; color:#1a1a1a;" onclick="saveAdvancedProfileChanges()">حفظ وتحديث التغييرات</button>
    </div>
</div>

<div class="popup-overlay" id="roomOptionsModal">
    <div class="popup-box">
        <button class="close-x-btn" onclick="closeAllModals()">X</button>
        <h3 style="text-align:center; margin-bottom:15px; font-size:16px;"><i class="fa-solid fa-gear"></i> خيارات الغرفة</h3>
        <div class="menu-list-item" onclick="alert('حائط النشر')"><i class="fa-solid fa-clipboard-list"></i> ١- حائط النشر</div>
        <div class="menu-list-item" id="roomCleanOpt" onclick="cleanRoomMessages()"><i class="fa-solid fa-broom"></i> ٢- تنظيف الروم</div>
        <div class="menu-list-item" id="roomBgOpt" style="position:relative; font-weight: bold; color: #2b6cb0;">
            <i class="fa-solid fa-image"></i> ٣- خلفية الروم من الملف 
            <input type="file" accept="image/*" onchange="changeRoomBackgroundFromFile(event)" style="position:absolute; top:0; left:0; width:100%; height:100%; opacity:0; cursor:pointer;">
        </div>
        <div class="menu-list-item" id="roomMsgOpt" onclick="setSpecialRoomMessage()"><i class="fa-solid fa-star"></i> ٤- رسالة مميزة</div>
    </div>
</div>

<div class="popup-overlay" id="confirmMicJoinModal">
    <div class="popup-box" style="text-align: center;">
        <h3 style="margin-bottom:10px; color:#1a202c;"><i class="fa-solid fa-microphone"></i> الصعود للميكروفون</h3>
        <p style="font-size:14px; color:#4a5568; font-weight:bold;">هل تريد الصعود والتحدث بنجاح؟</p>
        <div class="confirm-btn-group">
            <button class="btn-yes" onclick="confirmAscendToMic()">نعم، اصعد</button>
            <button class="btn-no" onclick="closeAllModals()">إلغاء</button>
        </div>
    </div>
</div>

<div class="popup-overlay" id="onlineUsersModal">
    <div class="popup-box">
        <button class="close-x-btn" onclick="closeAllModals()">X</button>
        <h3 style="text-align:center; margin-bottom:15px; font-size:16px;"><i class="fa-solid fa-users"></i> المتواجدين حالياً</h3>
        <div id="onlineUsersListContainer"></div>
    </div>
</div>

<div class="popup-overlay" id="myMicControlPanelModal">
    <div class="popup-box">
        <button class="close-x-btn" onclick="closeAllModals()">X</button>
        <h3 style="text-align:center; margin-bottom:15px;"><i class="fa-solid fa-sliders"></i> خيارات التحكم في المايك</h3>
        <button class="popup-btn" style="background:#4a5568;" onclick="triggerMuteToggle()">كتم الميك / فتح كتم الميك</button>
        <button class="popup-btn" style="background:#e53e3e;" onclick="stopGlobalMusic()">إيقاف الأغنية الحالية</button>
        <button class="popup-btn" style="background:#1a1a1a; margin-top:15px;" onclick="descendFromMic()">نزول من المايك ⬇️</button>
    </div>
</div>

<div class="popup-overlay" id="loginPopupModal">
    <div class="popup-box">
        <button class="close-x-btn" onclick="closeAllModals()">X</button>
        <h3 style="text-align:center; margin-bottom:12px;"><i class="fa-solid fa-key" style="color:#ffd700;"></i> التسجيل للأبد وتفعيل العضوية الماسية</h3>
        <div class="form-group"><label>اسم الحساب الدائم</label><input type="text" id="secureNameInput" class="form-control" placeholder="اكتب اسمك الدائم..."></div>
        <div class="form-group"><label>البريد الإلكتروني</label><input type="email" id="secureEmailInput" class="form-control" placeholder="email@example.com"></div>
        <div class="form-group"><label>كلمة المرور السرية</label><input type="password" id="securePassInput" class="form-control" placeholder="******"></div>
        <button class="popup-btn" style="background:#00b4db; color:#fff;" onclick="executeSecureAuth()">تأكيد التسجيل ومنح الرتبة الماسية 💎</button>
    </div>
</div>

<script src="https://www.youtube.com/iframe_api"></script>

<script>
    // --- تهيئة وربط الـ Firebase بمفاتيح مشروعك الرسمية ---
    const firebaseConfig = {
        apiKey: "AIzaSyDTUvD1gQqmnSAaqjJJ6DvBY-G6SVolsiw",
        authDomain: "hasoni-22097.firebaseapp.com",
        projectId: "hasoni-22097",
        storageBucket: "hasoni-22097.firebasestorage.app",
        messagingSenderId: "55912694950",
        appId: "1:55912694950:web:b94e4be56a3ed3c68c2067",
        measurementId: "G-WBGMD4Z52P"
    };

    // بدء تشغيل الفايربيز وقاعدة البيانات الحية
    firebase.initializeApp(firebaseConfig);
    const database = firebase.database();

    // إعداد الـ 20 رتبة المتكاملة
    const sysRanksConfig = {
        'owner': { label: 'صاحب الموقع', color: '#ffd700', icon: '<i class="fa-solid fa-trophy" style="color:#ffd700;"></i>', isStaff: true },
        'prince': { label: 'برنس', color: '#ffaa00', icon: '<i class="fa-solid fa-crown" style="color:#ffaa00;"></i>', isStaff: true },
        'king': { label: 'كنج', color: '#e53e3e', icon: '<i class="fa-solid fa-crown" style="color:#e53e3e;"></i>', isStaff: true },
        'honor': { label: 'انروا', color: '#1a1a1a', icon: '<i class="fa-solid fa-crown" style="color:#1a1a1a;"></i>', isStaff: true },
        'admin': { label: 'ادمان', color: '#718096', icon: '<i class="fa-solid fa-crown" style="color:#cbd5e0;"></i>', isStaff: true },
        'diamond': { label: 'عضو ماسي', color: '#00b4db', icon: '<i class="fa-solid fa-gem" style="color:#00b4db;"></i>', isStaff: false },
        'vip': { label: 'VIP', color: '#ed64a6', icon: '<i class="fa-solid fa-star" style="color:#ed64a6;"></i>', isStaff: false },
        'gold_member': { label: 'مشارك ذهبي', color: '#ecc94b', icon: '<i class="fa-solid fa-medal" style="color:#ecc94b;"></i>', isStaff: false },
        'r9': { label: 'تاج الملوك', color: '#805ad5', icon: '<i class="fa-solid fa-chess-king"></i>', isStaff: false },
        'r10': { label: 'العميد', color: '#3182ce', icon: '<i class="fa-solid fa-user-shield"></i>', isStaff: false },
        'r11': { label: 'العقيد', color: '#dd6b20', icon: '<i class="fa-solid fa-award"></i>', isStaff: false },
        'r12': { label: 'الزعيم', color: '#319795', icon: '<i class="fa-solid fa-user-ninja"></i>', isStaff: false },
        'r13': { label: 'المستشار', color: '#4a5568', icon: '<i class="fa-solid fa-gavel"></i>', isStaff: false },
        'r14': { label: 'الامبراطور', color: '#b7791f', icon: '<i class="fa-solid fa-bolt"></i>', isStaff: false },
        'r15': { label: 'الجنرال', color: '#718096', icon: '<i class="fa-solid fa-star-half-stroke"></i>', isStaff: false },
        'r16': { label: 'الفارس', color: '#e53e3e', icon: '<i class="fa-solid fa-shield"></i>', isStaff: false },
        'r17': { label: 'الصقر', color: '#3182ce', icon: '<i class="fa-solid fa-feather"></i>', isStaff: false },
        'r18': { label: 'مشارك نشط', color: '#4bc7ec', icon: '<i class="fa-solid fa-bolt-lightning"></i>', isStaff: false },
        'r19': { label: 'عضو دائم', color: '#a0aec0', icon: '<i class="fa-solid fa-user-check"></i>', isStaff: false },
        'visitor': { label: 'زائر', color: '#718096', icon: '<i class="fa-solid fa-user"></i>', isStaff: false }
    };

    // حساب صاحب الموقع الثابت والأساسي
    let siteOwnerObj = {
        name: "حسوني (صاحب الموقع)", age: "19", gender: "ذكر", country: "العراق", rank: "owner",
        avatar: "https://via.placeholder.com/40/ffd700/000000?text=👑",
        cover: "linear-gradient(135deg, #aa7c11, #ffd700)",
        status: "صاحب الموقع الرسمي لشات حسوني المطور", nameBg: "#ffffff", likes: 999
    };

    let dynamicRoomUsers = [];
    let accountData = {
        name: "زائر مؤقت", age: "20", gender: "ذكر", country: "العراق", rank: "visitor",
        avatar: "https://via.placeholder.com/40/cbd5e0/000000?text=U",
        cover: "linear-gradient(135deg, #1e1e24, #2a2a35)",
        status: "اضغط على المفتاح للتسجيل للأبد وتعديل ملفك", nameBg: "#ffffff", likes: 1
    };

    let activeMicSlot = null; 
    let selectedMicTarget = null; 
    let ytPlayer = null;
    let currentProfileUserTarget = null;
    let userRefKey = null; // لمتابعة تواجد العضو أونلاين

    window.onload = function() {
        const ageSelect = document.getElementById('initAgeInput');
        for (let i = 15; i <= 100; i++) {
            let opt = document.createElement('option');
            opt.value = i; opt.innerText = i;
            if(i === 20) opt.selected = true;
            ageSelect.appendChild(opt);
        }

        const selectContainer = document.getElementById('adminRankSelector');
        for (let key in sysRanksConfig) {
            let opt = document.createElement('option');
            opt.value = key; opt.innerText = sysRanksConfig[key].label;
            selectContainer.appendChild(opt);
        }

        const localSave = localStorage.getItem('hasoni_secure_session');
        if (localSave) { 
            accountData = JSON.parse(localSave); 
            document.getElementById('welcomeWelcomePanel').style.display = 'none';
            applyUserSessionUI(); 
        }

        // الاستماع الحي للرسائل من الفايربيز وعرضها فوراً للكل
        database.ref('messages').limitToLast(50).on('child_added', function(snapshot) {
            renderHistoricalMessage(snapshot.val());
        });

        // الاستماع الحي للمتواجدين أونلاين في الفايربيز
        database.ref('users_online').on('value', function(snapshot) {
            dynamicRoomUsers = [];
            snapshot.forEach(child => {
                dynamicRoomUsers.push(child.val());
            });
        });
    };

    function loginAsVisitor() {
        const inputName = document.getElementById('initNameInput').value.trim();
        if(!inputName) { alert("يرجى كتابة اسمك المستعار."); return; }
        accountData.name = inputName;
        accountData.gender = document.getElementById('initGenderInput').value;
        accountData.age = document.getElementById('initAgeInput').value;
        accountData.country = document.getElementById('initCountryInput').value || "العراق";
        accountData.rank = "visitor";
        
        localStorage.setItem('hasoni_secure_session', JSON.stringify(accountData));
        document.getElementById('welcomeWelcomePanel').style.display = 'none';
        applyUserSessionUI();
    }

    function executeSecureAuth() {
        const nameInput = document.getElementById('secureNameInput').value.trim();
        const emailInput = document.getElementById('secureEmailInput').value.trim();
        const passInput = document.getElementById('securePassInput').value.trim();

        if(!nameInput) { alert("يرجى كتابة اسم الحساب."); return; }

        if (emailInput === "ghrwrkk2@gmail.com" && passInput === "780718519") {
            accountData = siteOwnerObj;
        } else {
            accountData.name = nameInput;
            accountData.rank = "diamond";
            accountData.avatar = "https://via.placeholder.com/40/00b4db/ffffff?text=💎";
            accountData.cover = "linear-gradient(135deg, #00b4db, #2c3e50)";
            accountData.status = "عضو ماسي مسجل للأبد بنجاح 💎";
        }

        localStorage.setItem('hasoni_secure_session', JSON.stringify(accountData));
        applyUserSessionUI();
        closeAllModals();
        alert("تم دخولك وتفعيل الرتبة الماسية الدائمة بنجاح 💎");
    }

    function applyUserSessionUI() {
        const keyBtn = document.getElementById('keyAuthBtn');
        const currentRankInfo = sysRanksConfig[accountData.rank] || sysRanksConfig['visitor'];
        document.getElementById('topUserRank').innerHTML = `${currentRankInfo.icon} ${currentRankInfo.label}`;
        
        if(accountData.rank !== 'visitor') {
            if(keyBtn) keyBtn.style.display = 'none';
        } else {
            if(keyBtn) keyBtn.style.display = 'flex';
        }

        const hasStaffPower = currentRankInfo.isStaff;
        document.getElementById('roomCleanOpt').style.display = hasStaffPower ? 'flex' : 'none';
        document.getElementById('roomBgOpt').style.display = hasStaffPower ? 'flex' : 'none';
        document.getElementById('roomMsgOpt').style.display = hasStaffPower ? 'flex' : 'none';

        // تسجيل دخول العضو في الفايربيز وحذفه تلقائياً عند قفل الصفحة
        if(!userRefKey) {
            let onlineRef = database.ref('users_online').push();
            userRefKey = onlineRef.key;
            onlineRef.set(accountData);
            onlineRef.onDisconnect().remove();
        } else {
            database.ref('users_online/' + userRefKey).set(accountData);
        }
    }

    function openLoginModal() { document.getElementById('loginPopupModal').style.display = 'flex'; }
    function openRoomOptionsModal() { document.getElementById('roomOptionsModal').style.display = 'flex'; }
    function closeAllModals() { document.querySelectorAll('.popup-overlay').forEach(m => m.style.display = 'none'); }

    function changeRoomBackgroundFromFile(event) {
        let file = event.target.files[0];
        if (file) {
            let reader = new FileReader();
            reader.onload = function(e) { document.getElementById('chatContainerView').style.backgroundImage = `url('${e.target.result}')`; };
            reader.readAsDataURL(file);
        }
        closeAllModals();
        alert("تم تحديث وتثبيت خلفية الروم بنجاح 🖼️");
    }

    function openAnyUserProfileCard(userObj) {
        currentProfileUserTarget = userObj;
        document.getElementById('pNameDisplay').innerText = userObj.name;
        document.getElementById('pNameDisplay').style.backgroundColor = userObj.nameBg || '#ffffff';
        document.getElementById('pStatusTextDisplay').innerText = userObj.status || "لا توجد حالة";
        document.getElementById('pGenderDisplay').innerText = userObj.gender || "ذكر";
        document.getElementById('pAgeDisplay').innerText = userObj.age || "20";
        document.getElementById('pCountryDisplay').innerText = userObj.country || "العراق";
        
        const rankInfo = sysRanksConfig[userObj.rank] || sysRanksConfig['visitor'];
        document.getElementById('pRankDisplay').innerHTML = `${rankInfo.icon} ${rankInfo.label}`;
        document.getElementById('pLikesDisplay').innerText = userObj.likes || '0';
        document.getElementById('pAvatarDisplay').src = userObj.avatar;
        document.getElementById('pProfileUrlLink').innerText = "https://hasonichat.com/user/" + encodeURIComponent(userObj.name);

        const coverDiv = document.getElementById('pCoverDisplay');
        if(userObj.cover && (userObj.cover.startsWith('http') || userObj.cover.startsWith('data:image'))) {
            coverDiv.style.background = `url('${userObj.cover}')`; coverDiv.style.backgroundSize = 'cover'; coverDiv.style.backgroundPosition = 'center';
        } else {
            coverDiv.style.background = userObj.cover || "linear-gradient(135deg, #2c3e50, #3498db)";
        }

        if(userObj.name === accountData.name && accountData.rank !== 'visitor') {
            document.getElementById('profilePenEditBtn').style.display = 'flex';
        } else {
            document.getElementById('profilePenEditBtn').style.display = 'none';
        }

        if(accountData.rank === 'owner' && userObj.name !== accountData.name) {
            document.getElementById('adminOperationsBtn').style.display = 'block';
        } else {
            document.getElementById('adminOperationsBtn').style.display = 'none';
        }

        document.getElementById('profileCardModal').style.display = 'flex';
    }

    function openProfileEditInputs() {
        document.getElementById('editProfileName').value = currentProfileUserTarget.name;
        document.getElementById('editProfileStatus').value = currentProfileUserTarget.status || '';
        document.getElementById('editProfileAge').value = currentProfileUserTarget.age || '20';
        document.getElementById('editProfileCountry').value = currentProfileUserTarget.country || 'العراق';
        document.getElementById('editProfileNameBg').value = currentProfileUserTarget.nameBg || '#ffffff';
        document.getElementById('editProfileFieldsModal').style.display = 'flex';
    }

    function saveAdvancedProfileChanges() {
        let target = currentProfileUserTarget;
        target.name = document.getElementById('editProfileName').value.trim() || target.name;
        target.status = document.getElementById('editProfileStatus').value.trim() || target.status;
        target.age = document.getElementById('editProfileAge').value.trim() || target.age;
        target.country = document.getElementById('editProfileCountry').value.trim() || target.country;
        target.nameBg = document.getElementById('editProfileNameBg').value;

        if(target.name === accountData.name) {
            accountData = target;
            localStorage.setItem('hasoni_secure_session', JSON.stringify(accountData));
            applyUserSessionUI();
        }
        closeAllModals();
        openAnyUserProfileCard(target);
        alert("تم تحديث البروفايل بنجاح تام! ✨");
    }

    function openAdminOperationsModal() {
        document.getElementById('adminRankSelector').value = currentProfileUserTarget.rank;
        document.getElementById('adminOperationsModal').style.display = 'flex';
    }

    function executeRankChangeByAdmin() {
        const selectedRank = document.getElementById('adminRankSelector').value;
        currentProfileUserTarget.rank = selectedRank;
        alert(`تم تحديث رتبة العضو [${currentProfileUserTarget.name}] بنجاح إلى: ${sysRanksConfig[selectedRank].label}`);
        closeAllModals();
    }

    function executeAdminAction(actionType) {
        alert(`تم تطبيق أمر الإدارة [ ${actionType} ] بنجاح ضد العضو ${currentProfileUserTarget.name}.`);
        closeAllModals();
    }

    function likeUserProfile() {
        currentProfileUserTarget.likes = (currentProfileUserTarget.likes || 0) + 1;
        document.getElementById('pLikesDisplay').innerText = currentProfileUserTarget.likes;
    }

    function handleMicClick(slotNum) {
        if (activeMicSlot === slotNum) {
            document.getElementById('myMicControlPanelModal').style.display = 'flex';
        } else {
            const occupant = document.getElementById(`mName${slotNum}`).innerText.trim();
            if (occupant === "فارغ") {
                selectedMicTarget = slotNum;
                document.getElementById('confirmMicJoinModal').style.display = 'flex';
            } else {
                alert("هذا المايك مشغول حالياً.");
            }
        }
    }

    function confirmAscendToMic() {
        if(activeMicSlot !== null) { resetMicNode(activeMicSlot); }
        activeMicSlot = selectedMicTarget;
        let nodeName = document.getElementById(`mName${activeMicSlot}`);
        let nodeBox = document.getElementById(`micNode${activeMicSlot}`);
        nodeName.innerText = accountData.name; 
        nodeBox.classList.add('active');
        
        if(accountData.cover && (accountData.cover.startsWith('http') || accountData.cover.startsWith('data:image'))) {
            nodeBox.style.backgroundImage = `url('${accountData.cover}')`;
        } else {
            nodeBox.style.background = accountData.cover || "linear-gradient(135deg, #1e1e24, #2a2a35)";
        }
        nodeBox.style.backgroundSize = "cover"; nodeBox.style.backgroundPosition = "center";
        closeAllModals();
        alert("تم صعودك للمايك بنجاح 🎙️");
    }

    function descendFromMic() {
        if (activeMicSlot !== null) {
            resetMicNode(activeMicSlot); activeMicSlot = null; closeAllModals();
            alert("لقد قمت بالنزول من المايك.");
        }
    }

    function resetMicNode(slot) {
        let nodeBox = document.getElementById(`micNode${slot}`);
        let nodeName = document.getElementById(`mName${slot}`);
        nodeName.innerText = "فارغ";
        nodeBox.classList.remove('active', 'muted');
        nodeBox.style.background = "#ffffff"; nodeBox.style.backgroundImage = "none";
    }

    function triggerMuteToggle() {
        if (activeMicSlot !== null) { document.getElementById(`micNode${activeMicSlot}`).classList.toggle('muted'); closeAllModals(); }
    }

    function openOnlineUsersModal() {
        let container = document.getElementById('onlineUsersListContainer');
        container.innerHTML = "";

        // حساب صاحب الموقع يثبت أول القائمة دائماً
        let ownerRow = document.createElement('div');
        ownerRow.className = "user-online-row";
        ownerRow.onclick = function() { closeAllModals(); openAnyUserProfileCard(siteOwnerObj); };
        ownerRow.innerHTML = `
            <div style="display:flex; align-items:center; gap:10px;">
                <img src="${siteOwnerObj.avatar}" class="user-online-avatar owner-gold-frame">
                <span style="font-weight:bold; font-size:13px; background:#ffffff; padding:2px 6px; border-radius:4px;">${siteOwnerObj.name}</span>
            </div>
            <span class="rank-badge-pill" style="background:#ffd700; color:#1a1a1a;">${sysRanksConfig['owner'].icon} ${sysRanksConfig['owner'].label}</span>
        `;
        container.appendChild(ownerRow);

        // سحب بقية الحسابات أونلاين من الفايربيز
        dynamicRoomUsers.forEach(u => {
            if(u.name !== siteOwnerObj.name) {
                let row = document.createElement('div');
                row.className = "user-online-row";
                row.onclick = function() { closeAllModals(); openAnyUserProfileCard(u); };
                let currentRankInfo = sysRanksConfig[u.rank] || sysRanksConfig['visitor'];
                row.innerHTML = `
                    <div style="display:flex; align-items:center; gap:10px;">
                        <img src="${u.avatar}" class="user-online-avatar">
                        <span style="font-weight:bold; font-size:13px; background:${u.nameBg || '#ffffff'}; padding:2px 6px; border-radius:4px;">${u.name}</span>
                    </div>
                    <span class="rank-badge-pill" style="background:${currentRankInfo.color}">${currentRankInfo.icon} ${currentRankInfo.label}</span>
                `;
                container.appendChild(row);
            }
        });

        document.getElementById('onlineUsersModal').style.display = 'flex';
    }

    function refreshChatData() { alert("تم تحديث الشات بنجاح 🔄"); }
    
    function cleanRoomMessages() { 
        database.ref('messages').remove();
        document.getElementById('chatMessages').innerHTML = ""; 
        closeAllModals(); 
    }
    
    function setSpecialRoomMessage() {
        let msg = prompt("أدخل الرسالة المميزة لتثبيتها في الأعلى:");
        if(msg) { let pBox = document.getElementById('pinnedSpecialMsg'); pBox.innerText = "📢 " + msg; pBox.style.display = "block"; }
        closeAllModals();
    }

    const sendBtn = document.getElementById('sendBtn');
    const chatInput = document.getElementById('chatInput');
    const chatMessages = document.getElementById('chatMessages');

    // إرسال الرسالة الحية وحفظها في الفايربيز
    function sendMessage() {
        const text = chatInput.value.trim();
        if (text !== "") {
            const packedMsg = {
                name: accountData.name, avatar: accountData.avatar, rank: accountData.rank, nameBg: accountData.nameBg, text: text
            };
            database.ref('messages').push(packedMsg);
            chatInput.value = "";
        }
    }

    function renderHistoricalMessage(msgObj) {
        const messageRow = document.createElement('div');
        messageRow.className = 'message-row';
        const rankInfo = sysRanksConfig[msgObj.rank] || sysRanksConfig['visitor'];
        
        messageRow.innerHTML = `
            <img src="${msgObj.avatar}" class="avatar" onclick="openAnyUserProfileCard(accountData)">
            <div class="message-content">
                <div class="user-tag-bar">
                    ${rankInfo.icon}
                    <div class="username-container" style="background:${msgObj.nameBg || '#ffffff'}"><span>${msgObj.name}</span></div>
                </div>
                <div class="message-text">${msgObj.text}</div>
            </div>
        `;
        chatMessages.appendChild(messageRow);
        chatMessages.scrollTop = chatMessages.scrollHeight;
    }

    sendBtn.addEventListener('click', sendMessage);
    chatInput.addEventListener('keypress', function(e) { if (e.key === 'Enter') { sendMessage(); } });
</script>

</body>
</html>
