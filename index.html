<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
  <title>شات نرمين أحلى شات عربي</title>
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
  <style>
    * { 
      box-sizing: border-box; 
      margin: 0; 
      padding: 0; 
      font-family: tahoma, arial, sans-serif; 
      -webkit-tap-highlight-color: transparent; 
    }
    
    /* جعل الصفحة بأسلوب Flexbox برأسي متمدد 100% لتثبيت الأشرطة فوق وتحت */
    html, body { 
      height: 100dvh; 
      width: 100%; 
      overflow: hidden; 
      background: #e2e8f0; 
      display: flex; 
      flex-direction: column; 
    }

    /* 1. نافذة تسجيل الدخول */
    #login-modal, #register-modal {
      position: fixed; inset: 0; background: rgba(15, 23, 42, 0.85); backdrop-filter: blur(8px);
      z-index: 9999; display: flex; align-items: center; justify-content: center; padding: 15px;
    }
    .login-box {
      background: #ffffff; width: 100%; max-width: 360px; border-radius: 20px; overflow: hidden;
      box-shadow: 0 20px 40px rgba(0,0,0,0.5); text-align: center;
    }
    .login-header { background: linear-gradient(135deg, #1e293b, #0f172a); color: white; padding: 20px 15px; }
    .login-header h2 { font-size: 1.2rem; margin-bottom: 4px; color: #38bdf8; }
    .login-tabs { display: flex; background: #f1f5f9; border-bottom: 1px solid #cbd5e1; }
    .tab-btn { flex: 1; padding: 12px; border: none; background: none; font-weight: bold; color: #64748b; cursor: pointer; }
    .tab-btn.active { background: #fff; color: #2563eb; border-bottom: 3px solid #2563eb; }
    .login-body { padding: 20px; text-align: right; }
    .input-group { margin-bottom: 12px; }
    .input-group label { font-size: 0.75rem; font-weight: bold; color: #475569; display: block; margin-bottom: 4px; }
    .input-group input, .edit-input {
      width: 100%; padding: 10px; border: 1px solid #cbd5e1; border-radius: 8px; outline: none; font-size: 0.85rem;
    }
    .btn-submit {
      width: 100%; padding: 12px; background: #2563eb; color: #fff; border: none; border-radius: 10px;
      font-weight: bold; cursor: pointer; font-size: 0.95rem; margin-top: 5px;
    }

    /* 2. الشريط العلوي - ثابت أعلا الصفحة */
    .top-bar-icons {
      background: #1e293b; color: #fff; display: flex; flex-direction: row; justify-content: space-around;
      align-items: center; padding: 8px 4px; border-bottom: 1px solid #334155; font-size: 0.65rem; direction: rtl;
      flex-shrink: 0;
    }
    .nav-item-top { text-align: center; cursor: pointer; color: #cbd5e1; flex: 1; }
    .nav-item-top i { font-size: 0.95rem; display: block; margin-bottom: 2px; color: #38bdf8; }

    /* 3. شريط المايكات */
    .mics-section-container { 
      display: flex; flex-direction: column; align-items: center; background: transparent; padding-top: 6px; 
      flex-shrink: 0;
    }
    .mics-group-frame {
      display: inline-flex; justify-content: center; gap: 10px; padding: 6px 14px;
      border: 2px solid #3b82f6; border-radius: 30px; background: rgba(255, 255, 255, 0.85); backdrop-filter: blur(4px);
      transition: all 0.3s ease;
    }
    .mics-group-frame.hidden-mics { display: none !important; }
    
    .mic-slot-wrapper { display: flex; flex-direction: column; align-items: center; width: 45px; }
    .mic-slot {
      width: 40px; height: 40px; border-radius: 50%; background: #2563eb; background-size: cover; background-position: center;
      display: flex; flex-direction: column; align-items: center; justify-content: center;
      color: white; font-size: 0.7rem; border: 2px solid #60a5fa; cursor: pointer; position: relative;
    }
    .mic-slot.occupied { border-color: #10b981; }
    .mic-slot.muted::after { content: "🔇"; position: absolute; top:-5px; right:-5px; font-size: 0.75rem; }
    .mic-user-name { font-size: 0.6rem; color: #0f172a; font-weight: bold; margin-top: 2px; white-space: nowrap; overflow: hidden; text-overflow: ellipsis; max-width: 45px; text-align: center; }

    .mic-toggle-controls {
      display: flex; align-items: center; justify-content: center; gap: 8px;
      padding: 2px 12px; margin-top: 4px; background: #cbd5e1; border-radius: 12px;
      cursor: pointer; font-size: 0.75rem; color: #1e293b; font-weight: bold;
    }

    /* 4. منطقة الشات - تتمدد لتستغرق كامل منتصف الشاشة */
    .chat-area { 
      flex: 1; 
      overflow-y: auto; 
      padding: 10px; 
      background: #f1f5f9; 
      display: flex; 
      flex-direction: column; 
      gap: 10px; 
    }
    .msg-item { display: flex; align-items: flex-start; gap: 8px; cursor: pointer; }
    .user-avatar { width: 38px; height: 38px; border-radius: 50%; object-fit: cover; border: 2px solid #3b82f6; }
    .msg-content { display: flex; flex-direction: column; }
    .user-header { display: flex; align-items: center; gap: 6px; font-weight: bold; font-size: 0.85rem; color: #0f172a; }
    
    .rank-badge-trophy {
      font-size: 0.95rem; color: #f59e0b; display: inline-flex; align-items: center; margin-left: 2px;
    }
    
    .msg-text-plain { font-size: 0.9rem; color: #1e293b; margin-top: 2px; word-break: break-word; }

    .frame-none { border: none; padding: 0; }
    .frame-gold { border: 2px solid #f59e0b; padding: 2px 6px; border-radius: 6px; background: rgba(245, 158, 11, 0.1); }
    .frame-neon { border: 2px solid #06b6d4; padding: 2px 6px; border-radius: 6px; box-shadow: 0 0 5px #06b6d4; }
    .frame-royal { border: 2px dashed #8b5cf6; padding: 2px 6px; border-radius: 6px; background: rgba(139, 92, 246, 0.1); }

    /* 5. شريط الكتابة - ثابت أسفل الشات */
    .input-bar {
      background: #fff; padding: 6px 10px; display: flex; align-items: center; gap: 8px;
      border-top: 1px solid #cbd5e1; direction: rtl; flex-shrink: 0;
    }
    .icon-btn { background: none; border: none; font-size: 1.2rem; color: #475569; cursor: pointer; }
    .input-wrapper { flex: 1; background: #f8fafc; border: 1px solid #cbd5e1; border-radius: 20px; display: flex; align-items: center; padding: 0 10px; }
    .input-wrapper input { width: 100%; padding: 8px; border: none; outline: none; font-size: 0.9rem; background: transparent; }
    .send-btn-main {
      background: #2563eb; color: white; border: none; width: 38px; height: 38px;
      border-radius: 50%; display: flex; align-items: center; justify-content: center; cursor: pointer;
    }

    /* 6. الشريط السفلي - ثابت أسفل الصفحة تماماً */
    .bottom-main-nav {
      background: #ffffff; border-top: 1px solid #cbd5e1; display: flex;
      justify-content: space-around; padding: 6px 0; direction: rtl; flex-shrink: 0;
    }
    .bottom-tab { text-align: center; color: #64748b; font-size: 0.65rem; text-decoration: none; flex: 1; cursor: pointer; }
    .bottom-tab i { font-size: 1.1rem; display: block; margin-bottom: 2px; }

    /* النوافذ المنبثقة والقوائم */
    .modal-overlay {
      position: fixed; inset: 0; background: rgba(0,0,0,0.7); z-index: 10000;
      display: none; align-items: center; justify-content: center; padding: 15px;
    }
    .modal-card {
      background: #fff; width: 100%; max-width: 380px; border-radius: 16px; overflow: hidden;
      box-shadow: 0 5px 25px rgba(0,0,0,0.3); position: relative; text-align: center;
      max-height: 90vh; overflow-y: auto;
    }
    .close-modal { position: absolute; top: 10px; left: 10px; font-size: 1.2rem; cursor: pointer; color: #fff; background: rgba(0,0,0,0.4); width:28px; height:28px; border-radius:50%; display:flex; align-items:center; justify-content:center; z-index: 10; }

    .profile-cover { height: 110px; background: linear-gradient(135deg, #2563eb, #0f172a); background-size: cover; background-position: center; position: relative; }
    .profile-avatar-container { position: relative; width: 75px; height: 75px; margin: -38px auto 6px; }
    .profile-avatar { width: 100%; height: 100%; border-radius: 50%; border: 3px solid #fff; object-fit: cover; background: #fff; }

    .profile-actions-grid { display: grid; grid-template-columns: repeat(3, 1fr); gap: 6px; padding: 10px 15px; border-bottom: 1px solid #f1f5f9; }
    .action-btn { background: #f1f5f9; border: 1px solid #cbd5e1; border-radius: 8px; padding: 8px; font-size: 0.75rem; color: #1e293b; cursor: pointer; font-weight: bold; }
    .action-btn i { color: #2563eb; margin-bottom: 3px; display: block; font-size: 0.9rem; }

    .profile-info-list { text-align: right; padding: 10px 15px; font-size: 0.8rem; color: #334155; }
    .profile-info-item { display: flex; justify-content: space-between; padding: 6px 0; border-bottom: 1px dashed #e2e8f0; }

    .plus-menu-grid { display: grid; grid-template-columns: repeat(4, 1fr); gap: 10px; padding: 15px; text-align: center; }
    .plus-item { background: #f8fafc; border: 1px solid #e2e8f0; border-radius: 12px; padding: 10px 5px; cursor: pointer; font-size: 0.75rem; font-weight: bold; color: #1e293b; }
    .plus-item i { font-size: 1.4rem; display: block; margin-bottom: 5px; color: #2563eb; }

    .menu-list { text-align: right; padding: 10px; max-height: 350px; overflow-y: auto; }
    .menu-item { padding: 10px 12px; border-bottom: 1px solid #f1f5f9; display: flex; align-items: center; gap: 10px; font-size: 0.85rem; color: #1e293b; cursor: pointer; font-weight: bold; }
    .menu-item:hover { background: #f8fafc; color: #2563eb; }
    .menu-item i { width: 20px; color: #2563eb; text-align: center; }

    .online-list { max-height: 300px; overflow-y: auto; text-align: right; padding: 10px; }
    .online-item { display: flex; align-items: center; justify-content: space-between; padding: 10px; border-bottom: 1px solid #f1f5f9; cursor: pointer; }

    /* محادثة خاصة */
    .private-chat-box { display: flex; flex-direction: column; height: 350px; }
    .private-messages { flex: 1; overflow-y: auto; padding: 10px; background: #f8fafc; display: flex; flex-direction: column; gap: 8px; text-align: right; }
    .p-msg { max-width: 80%; padding: 8px 12px; border-radius: 12px; font-size: 0.85rem; }
    .p-msg.me { background: #2563eb; color: #fff; align-self: flex-start; }
    .p-msg.other { background: #e2e8f0; color: #0f172a; align-self: flex-end; }
  </style>

  <!-- Firebase JS SDK -->
  <script type="module">
    import { initializeApp } from "https://www.gstatic.com/firebasejs/12.19.0/firebase-app.js";
    import { getFirestore, collection, addDoc, query, orderBy, onSnapshot, serverTimestamp } from "https://www.gstatic.com/firebasejs/12.19.0/firebase-firestore.js";

    const firebaseConfig = {
      apiKey: "AIzaSyAFjspoGwJJeowjEZrcmJCO99iiTcBR5Is",
      authDomain: "hassouni-chat-51234.firebaseapp.com",
      projectId: "hassouni-chat-51234",
      storageBucket: "hassouni-chat-51234.firebasestorage.app",
      messagingSenderId: "519124989339",
      appId: "1:519124989339:web:318517ae7a008187d89d3e"
    };

    const app = initializeApp(firebaseConfig);
    const db = getFirestore(app);

    const OWNER_EMAILS = ["ghrwrkk2@gmail.com", "ghrwrkk2@gmamil.com"];
    
    let currentUser = { 
      name: "زائر", 
      email: "", 
      isOwner: false, 
      isVisitor: true,
      priority: 20, 
      avatar: "", 
      cover: "", 
      nameFrame: "frame-none",
      rankTitle: "",
      age: "غير محدد",
      gender: "غير محدد",
      country: "غير محدد",
      info: "مرحباً بي في شات نرمين أحلى شات عربي!"
    };
    
    let selectedUserForProfile = null;
    let onlineUsersMap = new Map();
    let currentMicSlotIndex = null;
    let micSlotsState = [null, null, null, null, null];
    let privateMessages = [];

    function checkSavedSession() {
      const savedUser = localStorage.getItem('chat_user_session');
      if (savedUser) {
        currentUser = JSON.parse(savedUser);
        document.getElementById('login-modal').style.display = 'none';
        updateKeyButtonVisibility();
        listenMessages();
      } else {
        document.getElementById('login-modal').style.display = 'flex';
      }
      document.getElementById('register-modal').style.display = 'none';
    }

    function updateKeyButtonVisibility() {
      const keyBtn = document.getElementById('register-key-tab');
      if (keyBtn) {
        if (currentUser.isOwner || !currentUser.isVisitor) {
          keyBtn.style.display = 'none';
        } else {
          keyBtn.style.display = 'block';
        }
      }
    }

    window.switchTab = (type) => {
      document.getElementById('tab-visitor').classList.toggle('active', type === 'visitor');
      document.getElementById('tab-member').classList.toggle('active', type === 'member');
      document.getElementById('member-fields').style.display = type === 'member' ? 'block' : 'none';
    };

    window.login = () => {
      const name = document.getElementById('username').value.trim();
      const email = document.getElementById('email').value.trim().toLowerCase();

      if (!name) return alert("يرجى كتابة الاسم!");

      const isOwner = OWNER_EMAILS.includes(email);
      const isMember = document.getElementById('tab-member').classList.contains('active');

      currentUser = {
        name: name,
        email: email,
        isOwner: isOwner,
        isVisitor: !isMember && !isOwner,
        priority: isOwner ? 1 : (isMember ? 7.5 : 20),
        avatar: `https://ui-avatars.com/api/?name=${encodeURIComponent(name)}&background=random`,
        cover: "",
        nameFrame: isOwner ? "frame-gold" : "frame-none",
        rankTitle: isOwner ? "مالك الموقع" : "عضو",
        age: "22",
        gender: "ذكر",
        country: "اليمن",
        info: "عضو في شات نرمين أحلى شات عربي"
      };

      localStorage.setItem('chat_user_session', JSON.stringify(currentUser));
      document.getElementById('login-modal').style.display = 'none';
      updateKeyButtonVisibility();
      listenMessages();
    };

    window.registerVisitorToDiamond = () => {
      const name = document.getElementById('reg-name').value.trim();
      const email = document.getElementById('reg-email').value.trim();
      const pass = document.getElementById('reg-pass').value.trim();

      if (!name || !email || !pass) return alert("يرجى ملء جميع الحقول!");

      currentUser.name = name;
      currentUser.email = email;
      currentUser.isVisitor = false;
      currentUser.priority = 7.5;

      localStorage.setItem('chat_user_session', JSON.stringify(currentUser));
      closeModal('register-modal');
      updateKeyButtonVisibility();
      alert("تهانينا! تم تسجيل حسابك بنجاح 💎");
    };

    window.sendMessage = async () => {
      const input = document.getElementById('msg-input');
      const messageText = input.value.trim();

      if (!messageText) return;

      input.value = "";

      await addDoc(collection(db, "chat_messages"), {
        sender: currentUser.name,
        isOwner: currentUser.isOwner,
        priority: currentUser.priority,
        avatar: currentUser.avatar,
        nameFrame: currentUser.nameFrame,
        text: messageText,
        timestamp: serverTimestamp()
      });
    };

    function listenMessages() {
      const q = query(collection(db, "chat_messages"), orderBy("timestamp", "asc"));
      onSnapshot(q, (snapshot) => {
        const area = document.getElementById('chat-area');
        area.innerHTML = "";
        onlineUsersMap.clear();

        snapshot.forEach(docSnap => {
          const data = docSnap.data();
          const avatarUrl = data.avatar || `https://ui-avatars.com/api/?name=${encodeURIComponent(data.sender)}`;
          const frameClass = data.nameFrame || 'frame-none';
          
          const rankBadgeHtml = data.isOwner ? `<i class="fa-solid fa-trophy rank-badge-trophy" title="مالك الموقع"></i>` : ``;

          onlineUsersMap.set(data.sender, {
            name: data.sender,
            isOwner: data.isOwner,
            priority: data.priority || (data.isOwner ? 1 : 20),
            avatar: avatarUrl,
            nameFrame: frameClass
          });

          area.innerHTML += `
            <div class="msg-item" onclick="openProfileByName('${data.sender}')">
              <img src="${avatarUrl}" class="user-avatar" alt="avatar">
              <div class="msg-content">
                <div class="user-header">
                  ${rankBadgeHtml}
                  <span class="${frameClass}">✿ ${data.sender} ✿</span>
                </div>
                <div class="msg-text-plain">${escapeHtml(data.text)}</div>
              </div>
            </div>
          `;
        });
        area.scrollTop = area.scrollHeight;
      });
    }

    window.openOnlineList = () => {
      const container = document.getElementById('online-users-container');
      container.innerHTML = "";
      const sortedUsers = Array.from(onlineUsersMap.values()).sort((a, b) => a.priority - b.priority);

      sortedUsers.forEach(user => {
        const rankBadgeHtml = user.isOwner ? `<i class="fa-solid fa-trophy rank-badge-trophy" title="مالك الموقع"></i>` : ``;
        container.innerHTML += `
          <div class="online-item" onclick="openProfileByName('${user.name}')">
            <div style="display:flex; align-items:center; gap:10px;">
              <img src="${user.avatar}" class="user-avatar" alt="user">
              <div>
                <div class="user-header">
                  ${rankBadgeHtml}
                  <span class="${user.nameFrame || 'frame-none'}">✿ ${user.name} ✿</span>
                </div>
              </div>
            </div>
            <span style="font-size:0.7rem; color:#22c55e; font-weight:bold;">● متواجد</span>
          </div>
        `;
      });
      document.getElementById('online-modal').style.display = 'flex';
    };

    window.openProfileByName = (name) => {
      if (name === currentUser.name) {
        openProfile(currentUser);
      } else {
        const u = onlineUsersMap.get(name) || {
          name: name,
          isOwner: false,
          avatar: `https://ui-avatars.com/api/?name=${encodeURIComponent(name)}`,
          age: "20",
          gender: "غير محدد",
          country: "غير محدد",
          info: "عضو في الشات"
        };
        openProfile(u);
      }
    };

    window.openProfile = (userObj) => {
      selectedUserForProfile = userObj;
      const isSelf = (currentUser.name === userObj.name);

      document.getElementById('prof-name').innerText = userObj.name;
      document.getElementById('prof-img').src = userObj.avatar || `https://ui-avatars.com/api/?name=${encodeURIComponent(userObj.name)}`;
      
      if(userObj.cover) {
        document.getElementById('prof-cover').style.backgroundImage = `url('${userObj.cover}')`;
      } else {
        document.getElementById('prof-cover').style.backgroundImage = 'linear-gradient(135deg, #2563eb, #0f172a)';
      }

      document.getElementById('prof-age').innerText = userObj.age || "22";
      document.getElementById('prof-gender').innerText = userObj.gender || "ذكر";
      document.getElementById('prof-country').innerText = userObj.country || "اليمن";
      document.getElementById('prof-info').innerText = userObj.info || "مرحباً بي في الشات!";

      const canEdit = isSelf;
      document.getElementById('self-edit-box').style.display = canEdit ? 'block' : 'none';
      document.getElementById('profile-actions').style.display = !isSelf ? 'grid' : 'none';

      const giftRankBtn = document.getElementById('owner-gift-rank-box');
      if (currentUser.isOwner && !isSelf) {
        giftRankBtn.style.display = 'block';
      } else {
        giftRankBtn.style.display = 'none';
      }

      document.getElementById('profile-modal').style.display = 'flex';
    };

    window.openPrivateChatFromProfile = () => {
      closeModal('profile-modal');
      document.getElementById('private-target-name').innerText = selectedUserForProfile.name;
      document.getElementById('private-chat-modal').style.display = 'flex';
      renderPrivateMessages();
    };

    window.sendPrivateMessage = () => {
      const input = document.getElementById('private-msg-input');
      const text = input.value.trim();
      if (!text) return;

      privateMessages.push({
        sender: currentUser.name,
        text: text
      });

      input.value = "";
      renderPrivateMessages();
    };

    function renderPrivateMessages() {
      const box = document.getElementById('private-messages-box');
      box.innerHTML = "";
      privateMessages.forEach(msg => {
        const isMe = msg.sender === currentUser.name;
        box.innerHTML += `<div class="p-msg ${isMe ? 'me' : 'other'}">${escapeHtml(msg.text)}</div>`;
      });
      box.scrollTop = box.scrollHeight;
    }

    window.giveRankToUser = () => {
      const selectedRank = document.getElementById('owner-rank-select').value;
      alert(`تم إهداء رتبة [${selectedRank}] للعضو ${selectedUserForProfile.name} بنجاح! 👑`);
      closeModal('profile-modal');
    };

    window.saveProfileChanges = () => {
      const newName = document.getElementById('edit-name-input').value.trim();
      const newFrame = document.getElementById('edit-frame-select').value;
      const newAge = document.getElementById('edit-age-input').value.trim();
      const newGender = document.getElementById('edit-gender-input').value;
      const newCountry = document.getElementById('edit-country-input').value.trim();
      const newInfo = document.getElementById('edit-info-input').value.trim();

      if (selectedUserForProfile.name === currentUser.name) {
        if (newName) currentUser.name = newName;
        currentUser.nameFrame = newFrame;
        if (newAge) currentUser.age = newAge;
        currentUser.gender = newGender;
        if (newCountry) currentUser.country = newCountry;
        if (newInfo) currentUser.info = newInfo;

        localStorage.setItem('chat_user_session', JSON.stringify(currentUser));
        alert("تم حفظ تعديلات بروفايلك بنجاح!");
      }

      closeModal('profile-modal');
    };

    window.uploadAvatar = (e) => {
      const file = e.target.files[0];
      if (file) {
        const reader = new FileReader();
        reader.onload = (event) => {
          currentUser.avatar = event.target.result;
          document.getElementById('prof-img').src = event.target.result;
          localStorage.setItem('chat_user_session', JSON.stringify(currentUser));
          alert("تم تغيير الصورة الشخصية!");
        };
        reader.readAsDataURL(file);
      }
    };

    window.uploadCover = (e) => {
      const file = e.target.files[0];
      if (file) {
        const reader = new FileReader();
        reader.onload = (event) => {
          document.getElementById('prof-cover').style.backgroundImage = `url('${event.target.result}')`;
          currentUser.cover = event.target.result;
          localStorage.setItem('chat_user_session', JSON.stringify(currentUser));
          alert("تم تغيير صورة الغلاف!");
        };
        reader.readAsDataURL(file);
      }
    };

    window.handleMicClick = (index) => {
      currentMicSlotIndex = index;
      const slotData = micSlotsState[index];

      if (!slotData) {
        document.getElementById('mic-confirm-modal').style.display = 'flex';
      } else if (slotData.name === currentUser.name) {
        document.getElementById('mic-options-modal').style.display = 'flex';
      } else {
        alert(`هذا المايك محجوز من قبل ${slotData.name}`);
      }
    };

    window.confirmJoinMic = () => {
      closeModal('mic-confirm-modal');
      micSlotsState[currentMicSlotIndex] = {
        name: currentUser.name,
        avatar: currentUser.avatar,
        isMuted: false
      };
      renderMicSlots();
    };

    window.leaveMic = () => {
      closeModal('mic-options-modal');
      micSlotsState[currentMicSlotIndex] = null;
      renderMicSlots();
      alert("تم النزول من المايك");
    };

    window.toggleMuteMic = () => {
      closeModal('mic-options-modal');
      if (micSlotsState[currentMicSlotIndex]) {
        micSlotsState[currentMicSlotIndex].isMuted = !micSlotsState[currentMicSlotIndex].isMuted;
        renderMicSlots();
        alert(micSlotsState[currentMicSlotIndex].isMuted ? "تم كتم المايك 🔇" : "تم فتح الكتم 🎙️");
      }
    };

    window.openYoutubeMusicSearch = () => {
      closeModal('mic-options-modal');
      document.getElementById('youtube-music-modal').style.display = 'flex';
    };

    window.playYoutubeSong = () => {
      const query = document.getElementById('yt-search-query').value.trim();
      if(!query) return alert("يرجى كتابة اسم الأغنية أو رابط يوتيوب!");

      let videoId = query;
      if(query.includes('v=')) {
        videoId = query.split('v=')[1].split('&')[0];
      } else if(query.includes('youtu.be/')) {
        videoId = query.split('youtu.be/')[1];
      } else {
        videoId = "qE839X-S2xM";
      }

      const playerContainer = document.getElementById('yt-player-box');
      playerContainer.innerHTML = `<iframe width="100%" height="200" src="https://www.youtube.com/embed/${videoId}?autoplay=1" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen></iframe>`;
      alert("تم تشغيل الأغنية بنجاح على المايك! 🎵");
    };

    function renderMicSlots() {
      for (let i = 0; i < 5; i++) {
        const slotElem = document.getElementById(`mic-slot-${i}`);
        const nameElem = document.getElementById(`mic-name-${i}`);
        const data = micSlotsState[i];

        if (data) {
          slotElem.style.backgroundImage = `url('${data.avatar}')`;
          slotElem.innerHTML = "";
          slotElem.classList.add('occupied');
          if (data.isMuted) slotElem.classList.add('muted');
          else slotElem.classList.remove('muted');
          nameElem.innerText = data.name;
        } else {
          slotElem.style.backgroundImage = "none";
          slotElem.innerHTML = `<i class="fa-solid fa-microphone"></i><span>${5 - i}</span>`;
          slotElem.className = "mic-slot";
          nameElem.innerText = "فارغ";
        }
      }
    }

    window.switchRoom = (roomName) => {
      closeModal('rooms-modal');
      alert(`تم الانتقال إلى: ${roomName}`);
    };

    window.logout = () => {
      localStorage.removeItem('chat_user_session');
      location.reload();
    };

    window.toggleMicsVisibility = () => {
      const frame = document.getElementById('mics-frame');
      const arrow = document.getElementById('toggle-arrow-icon');
      const lock = document.getElementById('toggle-lock-icon');

      if (frame.classList.contains('hidden-mics')) {
        frame.classList.remove('hidden-mics');
        arrow.className = "fa-solid fa-chevron-up";
        lock.className = "fa-solid fa-lock-open";
      } else {
        frame.classList.add('hidden-mics');
        arrow.className = "fa-solid fa-chevron-down";
        lock.className = "fa-solid fa-lock";
      }
    };

    window.closeModal = (id) => { document.getElementById(id).style.display = 'none'; };
    window.openModal = (id) => { document.getElementById(id).style.display = 'flex'; };

    function escapeHtml(str) {
      return str.replace(/&/g, "&amp;").replace(/</g, "&lt;").replace(/>/g, "&gt;");
    }

    window.onload = () => {
      checkSavedSession();
    };
  </script>
</head>
<body>

  <!-- 1. نافذة تسجيل الدخول الرئيسية -->
  <div id="login-modal">
    <div class="login-box">
      <div class="login-header">
        <h2>شات نرمين أحلى شات عربي ✨</h2>
      </div>
      <div class="login-tabs">
        <button class="tab-btn active" id="tab-visitor" onclick="switchTab('visitor')">دخول زائر</button>
        <button class="tab-btn" id="tab-member" onclick="switchTab('member')">دخول عضوية</button>
      </div>
      <div class="login-body">
        <div class="input-group">
          <label>اسم المستخدم:</label>
          <input type="text" id="username" placeholder="اكتب اسمك...">
        </div>
        <div class="input-group" id="member-fields" style="display:none;">
          <label>البريد الإلكتروني:</label>
          <input type="email" id="email" placeholder="أدخل بريد المالك أو العضو">
        </div>
        <button class="btn-submit" onclick="login()">دخول الشات</button>
      </div>
    </div>
  </div>

  <!-- نافذة تسجيل الزائر -->
  <div id="register-modal" class="modal-overlay">
    <div class="modal-card">
      <span class="close-modal" onclick="closeModal('register-modal')">&times;</span>
      <h3 style="padding:15px; background:#2563eb; color:#fff;">تسجيل حساب جديد 🔑</h3>
      <div class="login-body">
        <div class="input-group">
          <label>الاسم الكامل:</label>
          <input type="text" id="reg-name" placeholder="أدخل اسمك...">
        </div>
        <div class="input-group">
          <label>البريد الإلكتروني:</label>
          <input type="email" id="reg-email" placeholder="أدخل البريد...">
        </div>
        <div class="input-group">
          <label>كلمة المرور:</label>
          <input type="password" id="reg-pass" placeholder="أدخل كلمة المرور...">
        </div>
        <button class="btn-submit" style="background:#10b981;" onclick="registerVisitorToDiamond()">تسجيل الحساب 💎</button>
      </div>
    </div>
  </div>

  <!-- 2. الشريط العلوي -->
  <div class="top-bar-icons">
    <div class="nav-item-top" onclick="openModal('icon-menu-modal')"><i class="fa-solid fa-user-gear"></i><span>الأيقونة</span></div>
    <div class="nav-item-top"><i class="fa-solid fa-bell"></i><span>إشعار</span></div>
    <div class="nav-item-top"><i class="fa-solid fa-triangle-exclamation"></i><span>بلاغ</span></div>
    <div class="nav-item-top"><i class="fa-solid fa-user-plus"></i><span>إضافة</span></div>
    <div class="nav-item-top"><i class="fa-solid fa-comments"></i><span>خاص</span></div>
    <div class="nav-item-top"><i class="fa-solid fa-crown"></i><span>الكبار</span></div>
    <div class="nav-item-top"><i class="fa-solid fa-sack-dollar"></i><span>الأثرياء</span></div>
    <div class="nav-item-top" onclick="openModal('options-menu-modal')"><i class="fa-solid fa-sliders"></i><span>الخيارات</span></div>
  </div>

  <!-- 3. شريط المايكات -->
  <div class="mics-section-container">
    <div class="mics-group-frame" id="mics-frame">
      <div class="mic-slot-wrapper">
        <div class="mic-slot" id="mic-slot-4" onclick="handleMicClick(4)"><i class="fa-solid fa-microphone"></i><span>5</span></div>
        <div class="mic-user-name" id="mic-name-4">فارغ</div>
      </div>
      <div class="mic-slot-wrapper">
        <div class="mic-slot" id="mic-slot-3" onclick="handleMicClick(3)"><i class="fa-solid fa-microphone"></i><span>4</span></div>
        <div class="mic-user-name" id="mic-name-3">فارغ</div>
      </div>
      <div class="mic-slot-wrapper">
        <div class="mic-slot" id="mic-slot-2" onclick="handleMicClick(2)"><i class="fa-solid fa-microphone"></i><span>3</span></div>
        <div class="mic-user-name" id="mic-name-2">فارغ</div>
      </div>
      <div class="mic-slot-wrapper">
        <div class="mic-slot" id="mic-slot-1" onclick="handleMicClick(1)"><i class="fa-solid fa-microphone"></i><span>2</span></div>
        <div class="mic-user-name" id="mic-name-1">فارغ</div>
      </div>
      <div class="mic-slot-wrapper">
        <div class="mic-slot" id="mic-slot-0" onclick="handleMicClick(0)"><i class="fa-solid fa-microphone"></i><span>1</span></div>
        <div class="mic-user-name" id="mic-name-0">فارغ</div>
      </div>
    </div>

    <div class="mic-toggle-controls" onclick="toggleMicsVisibility()">
      <i class="fa-solid fa-chevron-up" id="toggle-arrow-icon"></i>
      <i class="fa-solid fa-lock-open" id="toggle-lock-icon"></i>
    </div>
  </div>

  <!-- 4. منطقة الشات -->
  <div class="chat-area" id="chat-area"></div>

  <!-- 5. شريط الإدخال -->
  <div class="input-bar">
    <button class="send-btn-main" onclick="sendMessage()"><i class="fa-solid fa-paper-plane"></i></button>

    <div class="input-wrapper">
      <input type="text" id="msg-input" placeholder="اكتب رسالتك هنا..." onkeydown="if(event.key==='Enter') sendMessage()">
      <button class="icon-btn"><i class="fa-regular fa-face-smile"></i></button>
    </div>

    <button class="icon-btn"><i class="fa-solid fa-microphone"></i></button>
    <button class="icon-btn" onclick="openModal('plus-menu-modal')"><i class="fa-solid fa-plus"></i></button>
  </div>

  <!-- 6. الشريط السفلي -->
  <div class="bottom-main-nav">
    <div class="bottom-tab" onclick="openOnlineList()"><i class="fa-solid fa-users"></i>المتواجدين</div>
    <div class="bottom-tab" onclick="openModal('rooms-modal')"><i class="fa-solid fa-door-open"></i>الغرف</div>
    <div class="bottom-tab" onclick="location.reload()"><i class="fa-solid fa-rotate-right"></i>تحديث</div>
    <div class="bottom-tab"><i class="fa-solid fa-store"></i>المتجر</div>
    <div class="bottom-tab"><i class="fa-solid fa-radio"></i>راديو</div>
    
    <div class="bottom-tab" id="register-key-tab" style="color:#f59e0b;" onclick="openModal('register-modal')">
      <i class="fa-solid fa-key"></i>تسجيل
    </div>
  </div>

  <!-- باقي القوائم والنوافذ المنبثقة -->
  <div class="modal-overlay" id="profile-modal">
    <div class="modal-card">
      <span class="close-modal" onclick="closeModal('profile-modal')">&times;</span>
      <div class="profile-cover" id="prof-cover"></div>
      <div class="profile-avatar-container">
        <img src="" id="prof-img" class="profile-avatar" alt="Avatar">
      </div>
      <h3 id="prof-name">اسم العضو</h3>

      <div class="profile-actions-grid" id="profile-actions">
        <div class="action-btn" onclick="openPrivateChatFromProfile()"><i class="fa-solid fa-envelope"></i>خاص</div>
        <div class="action-btn" onclick="alert('تم إرسال إعجاب')"><i class="fa-solid fa-heart"></i>لايك</div>
        <div class="action-btn" onclick="alert('المستوى الحالي')"><i class="fa-solid fa-chart-line"></i>مستوى</div>
        <div class="action-btn" onclick="alert('إرسال هدية')"><i class="fa-solid fa-gift"></i>هدية</div>
        <div class="action-btn" onclick="alert('تمت الإضافة')"><i class="fa-solid fa-user-plus"></i>إضافة</div>
        <div class="action-btn" onclick="alert('بدء مكالمة')"><i class="fa-solid fa-phone"></i>مكالمة</div>
      </div>

      <div id="owner-gift-rank-box" style="display:none; padding:10px 15px; background:#fef3c7; border:1px solid #f59e0b; margin:10px; border-radius:10px; text-align:right;">
        <h4 style="font-size:0.8rem; color:#b45309; margin-bottom:5px;"><i class="fa-solid fa-crown"></i> لوحة صاحب الموقع: إهداء رتبة</h4>
        <select id="owner-rank-select" class="edit-input" style="margin-bottom:6px;">
          <option value="مالك موقع 👑">مالك موقع 👑</option>
          <option value="إدارة الشات 🛡️">إدارة الشات 🛡️</option>
          <option value="مشرف مميز ⭐">مشرف مميز ⭐</option>
          <option value="عضوVIP 💎">عضو VIP 💎</option>
        </select>
        <button class="btn-submit" style="background:#f59e0b; padding:6px; font-size:0.8rem;" onclick="giveRankToUser()">منح الرتبة للعضو 🎁</button>
      </div>

      <div class="profile-info-list">
        <div class="profile-info-item"><span>العمر:</span> <strong id="prof-age">22</strong></div>
        <div class="profile-info-item"><span>الجنس:</span> <strong id="prof-gender">ذكر</strong></div>
        <div class="profile-info-item"><span>البلاد:</span> <strong id="prof-country">اليمن</strong></div>
        <div class="profile-info-item"><span>المعلومات:</span> <strong id="prof-info">مرحباً بي في الشات!</strong></div>
      </div>

      <div class="edit-profile-section" id="self-edit-box" style="display:none; text-align:right; padding:12px; background:#f8fafc; border-top:1px solid #cbd5e1;">
        <h4 style="font-size:0.85rem; color:#2563eb; margin-bottom:8px;"><i class="fa-solid fa-pen-to-square"></i> تعديل البروفايل الشخصي</h4>
        
        <label style="font-size:0.75rem;">تعديل الاسم:</label>
        <input type="text" id="edit-name-input" class="edit-input" placeholder="الاسم الجديد...">

        <label style="font-size:0.75rem; margin-top:5px; display:block;">إطار الاسم:</label>
        <select id="edit-frame-select" class="edit-input">
          <option value="frame-none">بدون إطار</option>
          <option value="frame-gold">إطار ذهبي 🌟</option>
          <option value="frame-neon">إطار نيون 💎</option>
          <option value="frame-royal">إطار ملكي 👑</option>
        </select>

        <label style="font-size:0.75rem; margin-top:5px; display:block;">العمر:</label>
        <input type="text" id="edit-age-input" class="edit-input" placeholder="العمر...">

        <label style="font-size:0.75rem; margin-top:5px; display:block;">الجنس:</label>
        <select id="edit-gender-input" class="edit-input">
          <option value="ذكر">ذكر</option>
          <option value="أنثى">أنثى</option>
        </select>

        <label style="font-size:0.75rem; margin-top:5px; display:block;">البلاد:</label>
        <input type="text" id="edit-country-input" class="edit-input" placeholder="البلاد...">

        <label style="font-size:0.75rem; margin-top:5px; display:block;">المعلومات الشخصية:</label>
        <input type="text" id="edit-info-input" class="edit-input" placeholder="نبذة...">

        <div style="display:flex; gap:6px; margin-top:10px;">
          <label for="avatar-file" style="flex:1; background:#cbd5e1; text-align:center; padding:6px; border-radius:6px; cursor:pointer; font-size:0.75rem;">
            📸 تغيير الصورة
          </label>
          <input type="file" id="avatar-file" accept="image/*" style="display:none;" onchange="uploadAvatar(event)">

          <label for="cover-file" style="flex:1; background:#cbd5e1; text-align:center; padding:6px; border-radius:6px; cursor:pointer; font-size:0.75rem;">
            🖼️ تغيير الغلاف
          </label>
          <input type="file" id="cover-file" accept="image/*" style="display:none;" onchange="uploadCover(event)">
        </div>

        <button class="btn-submit" style="margin-top:10px; padding:8px; font-size:0.85rem;" onclick="saveProfileChanges()">حفظ التعديلات 💾</button>
      </div>
    </div>
  </div>

  <div class="modal-overlay" id="private-chat-modal">
    <div class="modal-card">
      <span class="close-modal" onclick="closeModal('private-chat-modal')">&times;</span>
      <h3 style="padding:12px; background:#1e293b; color:#fff;">محادثة خاصة مع: <span id="private-target-name">...</span></h3>
      <div class="private-chat-box">
        <div class="private-messages" id="private-messages-box"></div>
        <div class="input-bar">
          <button class="send-btn-main" onclick="sendPrivateMessage()"><i class="fa-solid fa-paper-plane"></i></button>
          <div class="input-wrapper">
            <input type="text" id="private-msg-input" placeholder="اكتب رسالتك الخاصة..." onkeydown="if(event.key==='Enter') sendPrivateMessage()">
          </div>
        </div>
      </div>
    </div>
  </div>

  <div class="modal-overlay" id="rooms-modal">
    <div class="modal-card">
      <span class="close-modal" onclick="closeModal('rooms-modal')">&times;</span>
      <h3 style="padding:12px; background:#1e293b; color:#fff;">قائمة الغرف المتاحة 🚪</h3>
      <div class="menu-list">
        <div class="menu-item" onclick="switchRoom('الغرفة العامة الرئيسية')"><i class="fa-solid fa-comments"></i> الغرفة العامة الرئيسية</div>
        <div class="menu-item" onclick="switchRoom('غرفة المسابقات والفعاليات')"><i class="fa-solid fa-trophy"></i> غرفة المسابقات والفعاليات</div>
        <div class="menu-item" onclick="switchRoom('غرفة الشباب والدردشة')"><i class="fa-solid fa-users"></i> غرفة الشباب والدردشة</div>
        <div class="menu-item" onclick="switchRoom('غرفة الأغاني والمواضيع')"><i class="fa-solid fa-music"></i> غرفة الأغاني والفن</div>
        <div class="menu-item" onclick="switchRoom('غرفة VIP الخواص')"><i class="fa-solid fa-crown"></i> غرفة VIP الخواص</div>
      </div>
    </div>
  </div>

  <div class="modal-overlay" id="mic-confirm-modal">
    <div class="modal-card" style="padding:20px;">
      <h3>صعود المايك 🎙️</h3>
      <p style="margin:15px 0; font-size:0.9rem;">هل تريد صعود المايك؟</p>
      <div style="display:flex; gap:10px;">
        <button class="btn-submit" style="background:#10b981; flex:1;" onclick="confirmJoinMic()">نعم</button>
        <button class="btn-submit" style="background:#ef4444; flex:1;" onclick="closeModal('mic-confirm-modal')">إلغاء</button>
      </div>
    </div>
  </div>

  <div class="modal-overlay" id="mic-options-modal">
    <div class="modal-card">
      <span class="close-modal" onclick="closeModal('mic-options-modal')">&times;</span>
      <h3 style="padding:12px; background:#1e293b; color:#fff;">إعدادات المايك 🎙️</h3>
      <div class="menu-list">
        <div class="menu-item" onclick="toggleMuteMic()"><i class="fa-solid fa-microphone-slash"></i> كتم المايك / فتح الكتم</div>
        <div class="menu-item" onclick="openYoutubeMusicSearch()"><i class="fa-brands fa-youtube" style="color:#ef4444;"></i> تشغيل أغنية من يوتيوب</div>
        <div class="menu-item" onclick="alert('تم إيقاف الأغنية ⏸️')"><i class="fa-solid fa-circle-pause"></i> إيقاف الأغنية</div>
        <div class="menu-item" style="color:#ef4444;" onclick="leaveMic()"><i class="fa-solid fa-person-walking-arrow-right" style="color:#ef4444;"></i> نزول من المايك</div>
      </div>
    </div>
  </div>

  <div class="modal-overlay" id="youtube-music-modal">
    <div class="modal-card" style="padding:15px;">
      <span class="close-modal" onclick="closeModal('youtube-music-modal')">&times;</span>
      <h3 style="margin-bottom:10px; color:#ef4444;"><i class="fa-brands fa-youtube"></i> تشغيل أغنية يوتيوب</h3>
      <div class="input-group">
        <input type="text" id="yt-search-query" class="edit-input" placeholder="ضع اسم الأغنية أو رابط يوتيوب هنا...">
      </div>
      <button class="btn-submit" style="background:#ef4444; margin-bottom:10px;" onclick="playYoutubeSong()">تشغيل 🎵</button>
      <div id="yt-player-box"></div>
    </div>
  </div>

  <div class="modal-overlay" id="plus-menu-modal">
    <div class="modal-card">
      <span class="close-modal" onclick="closeModal('plus-menu-modal')">&times;</span>
      <h3 style="padding:12px; background:#1e293b; color:#fff;">الأدوات والألعاب 🎮</h3>
      <div class="plus-menu-grid">
        <div class="plus-item" onclick="alert('فتح يوتيوب')"><i class="fa-brands fa-youtube" style="color:#ef4444;"></i>يوتيوب</div>
        <div class="plus-item" onclick="alert('فتح الرسم')"><i class="fa-solid fa-paint-brush"></i>رسم</div>
        <div class="plus-item" onclick="alert('رمي النرد')"><i class="fa-solid fa-dice"></i>نرد</div>
        <div class="plus-item" onclick="alert('إرسال ملف')"><i class="fa-solid fa-folder-open"></i>ملف</div>
        <div class="plus-item" onclick="alert('فتح تيك توك')"><i class="fa-brands fa-tiktok" style="color:#000;"></i>تيك توك</div>
        <div class="plus-item" onclick="alert('لعبة حجرة ورقة مقص')"><i class="fa-solid fa-hand-scissors"></i>مقص ورقة</div>
        <div class="plus-item" onclick="alert('لعبة X-O')"><i class="fa-solid fa-xmark"></i>لعبة X-O</div>
        <div class="plus-item" onclick="alert('فتح عجلة الحظ')"><i class="fa-solid fa-arrows-spin"></i>عجلة الحظ</div>
      </div>
    </div>
  </div>

  <div class="modal-overlay" id="icon-menu-modal">
    <div class="modal-card">
      <span class="close-modal" onclick="closeModal('icon-menu-modal')">&times;</span>
      <h3 style="padding:12px; background:#1e293b; color:#fff;">أيقونة الحساب ⚙️</h3>
      <div class="menu-list">
        <div class="menu-item"><i class="fa-solid fa-gear"></i> إعدادات الدردشة</div>
        <div class="menu-item"><i class="fa-solid fa-wallet"></i> محفظة</div>
        <div class="menu-item"><i class="fa-solid fa-gift"></i> المكافآت اليومية</div>
        <div class="menu-item"><i class="fa-solid fa-chart-line"></i> معلومات المستوى</div>
        <div class="menu-item"><i class="fa-solid fa-leaf"></i> تشغيل الوضع البسيط</div>
        <div class="menu-item" style="color:#ef4444;" onclick="logout()"><i class="fa-solid fa-right-from-bracket" style="color:#ef4444;"></i> خروج</div>
      </div>
    </div>
  </div>

  <div class="modal-overlay" id="options-menu-modal">
    <div class="modal-card">
      <span class="close-modal" onclick="closeModal('options-menu-modal')">&times;</span>
      <h3 style="padding:12px; background:#1e293b; color:#fff;">قائمة الخيارات 📜</h3>
      <div class="menu-list">
        <div class="menu-item" onclick="openModal('rooms-modal')"><i class="fa-solid fa-door-open"></i> الرومات</div>
        <div class="menu-item"><i class="fa-solid fa-user-group"></i> حائط الأصدقاء</div>
        <div class="menu-item"><i class="fa-solid fa-newspaper"></i> حائط النشر</div>
        <div class="menu-item"><i class="fa-solid fa-bullhorn"></i> الأخبار</div>
        <div class="menu-item"><i class="fa-solid fa-crown"></i> عائلات VIP</div>
        <div class="menu-item"><i class="fa-solid fa-star"></i> قائمة الكبار</div>
        <div class="menu-item"><i class="fa-solid fa-gem"></i> قائمة الأثرياء</div>
        <div class="menu-item"><i class="fa-solid fa-shop"></i> Black Market</div>
        <div class="menu-item"><i class="fa-solid fa-trophy"></i> نجوم الجولات</div>
        <div class="menu-item"><i class="fa-solid fa-bus"></i> اتوبيس كومبليت</div>
        <div class="menu-item"><i class="fa-solid fa-hand-holding-dollar"></i> كبار الداعمين</div>
        <div class="menu-item"><i class="fa-solid fa-users"></i> تفاعل الأعضاء</div>
        <div class="menu-item"><i class="fa-solid fa-user-shield"></i> تفاعل الإدارة</div>
        <div class="menu-item"><i class="fa-solid fa-comments"></i> تفاعل الرومات</div>
        <div class="menu-item"><i class="fa-solid fa-download"></i> تحميل التطبيق</div>
        <div class="menu-item"><i class="fa-solid fa-list-ol"></i> ترتيب نقاط المسابقة</div>
      </div>
    </div>
  </div>

  <div class="modal-overlay" id="online-modal">
    <div class="modal-card">
      <span class="close-modal" onclick="closeModal('online-modal')">&times;</span>
      <h3 style="padding: 12px; border-bottom:1px solid #e2e8f0; color:#0f172a;">المتواجدون الآن 👥</h3>
      <div class="online-list" id="online-users-container"></div>
    </div>
  </div>

</body>
</html>
