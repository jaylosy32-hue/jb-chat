<!DOCTYPE html>
<html lang="fr">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>JB CHAT</title>
<style>
*{ margin:0; padding:0; box-sizing:border-box; }
body{ font-family:Arial,sans-serif; background:#f3f4f6; color:#111; padding-bottom:70px; }
header{ height:60px; background:white; border-bottom:1px solid #ddd; display:flex; align-items:center; justify-content:space-between; padding:0 20px; position:sticky; top:0; z-index:100; }
.logo{ font-size:24px; font-weight:900; color:#d90000; }
.search{ width:300px; }
.search input{ width:100%; border:0; outline:0; background:#f0f2f5; padding:11px 16px; border-radius:25px; }
.header-icons{ display:flex; gap:10px; }
.icon{ width:38px; height:38px; border:0; border-radius:50%; background:#f0f2f5; font-size:18px; cursor:pointer; position:relative; }
.container{ max-width:1100px; margin:auto; display:grid; grid-template-columns:220px 1fr 220px; gap:20px; padding:20px; }
.sidebar{ position:sticky; top:80px; height:max-content; }
.menu{ background:white; border-radius:12px; padding:10px; }
.menu button{ width:100%; border:0; background:white; padding:13px; text-align:left; border-radius:10px; cursor:pointer; font-size:15px; }
.menu button:hover{ background:#f0f2f5; }
.feed{ min-width:0; }
.stories{ background:white; border-radius:12px; padding:15px; display:flex; gap:15px; overflow-x:auto; }
.story{ min-width:70px; text-align:center; font-size:12px; cursor:pointer; }
.story-photo{ width:60px; height:60px; border-radius:50%; background:#d90000; color:white; display:flex; align-items:center; justify-content:center; margin:auto auto 6px; font-size:22px; font-weight:bold; overflow:hidden; border:3px solid #d90000; }
.story-photo img{ width:100%; height:100%; object-fit:cover; }
.create{ margin-top:15px; background:white; padding:15px; border-radius:12px; }
.create-top{ display:flex; gap:10px; align-items:center; }
.avatar{ width:42px; height:42px; min-width:42px; border-radius:50%; background:#d90000; color:white; display:flex; align-items:center; justify-content:center; font-weight:bold; overflow:hidden; }
.avatar img{ width:100%; height:100%; object-fit:cover; }
.create input{ flex:1; border:0; outline:0; background:#f0f2f5; padding:12px 16px; border-radius:25px; }
.create-actions{ border-top:1px solid #eee; margin-top:12px; padding-top:10px; display:flex; justify-content:space-around; }
.create-actions button{ border:0; background:white; padding:8px 15px; cursor:pointer; border-radius:8px; }
.post{ background:white; margin-top:15px; border-radius:12px; overflow:hidden; }
.post-head{ display:flex; align-items:center; gap:10px; padding:15px; }
.post-menu-btn{ margin-left:auto; border:0; background:transparent; font-size:20px; line-height:1; padding:5px 8px; border-radius:8px; cursor:pointer; color:#666; }
.post-menu-btn:hover{ background:#f0f2f5; color:#111; }

.post-head small{ display:block; color:#777; margin-top:3px; }
.post-text{ padding:0 15px 15px; line-height:1.5; white-space:pre-wrap; }
.post-picture{ width:100%; max-height:500px; background:#111; display:flex; justify-content:center; align-items:center; }
.post-picture img, .post-picture video{ width:100%; max-height:500px; object-fit:contain; background:#000; }
.default-picture{ width:100%; height:280px; display:flex; justify-content:center; align-items:center; background:linear-gradient(135deg,#250000,#111); color:#e00000; font-size:35px; font-weight:900; }
.post-actions{ display:flex; border-top:1px solid #eee; border-bottom:1px solid #eee; }
.post-actions button{ flex:1; border:0; background:white; padding:13px; cursor:pointer; font-weight:bold; }
.liked{ color:#d90000; }
.comments{ padding:10px 15px; display:none; }
.comment-input{ width:80%; padding:10px; border:1px solid #ddd; border-radius:20px; }
.comment-send{ border:0; background:#d90000; color:white; padding:10px 13px; border-radius:20px; }
.comment{ margin-top:8px; padding:8px; background:#f0f2f5; border-radius:10px; }
.rightbar{ position:sticky; top:80px; height:max-content; }
.card{ background:white; border-radius:12px; padding:15px; margin-bottom:15px; }
.friend{ display:flex; align-items:center; gap:10px; margin-bottom:12px; cursor:pointer; }
.profile{ display:none; background:white; border-radius:15px; overflow:hidden; margin-bottom:20px; }
.cover{ height:140px; background:linear-gradient(135deg,#d90000,#111); }
.profile-content{ text-align:center; padding:0 20px 20px; }
.profile-photo{ width:100px; height:100px; border-radius:50%; background:#d90000; color:white; border:5px solid white; margin:-50px auto 10px; display:flex; align-items:center; justify-content:center; font-size:40px; font-weight:bold; overflow:hidden; }
.profile-photo img{ width:100%; height:100%; object-fit:cover; }
.profile-name{ font-size:24px; font-weight:bold; }
.profile-bio{ color:#666; margin:8px 0; }
.profile-stats{ display:flex; justify-content:center; gap:35px; margin:15px 0; }
.stat strong{ display:block; font-size:18px; }
.stat span{ font-size:12px; color:#777; }
.profile-button{ border:0; background:#d90000; color:white; padding:10px 20px; border-radius:8px; font-weight:bold; cursor:pointer; margin:4px; }
.bottom{ position:fixed; bottom:0; left:0; width:100%; height:65px; background:white; border-top:1px solid #ddd; display:none; justify-content:space-around; align-items:center; z-index:200; }
.bottom button{ border:0; background:white; font-size:20px; }
.modal{ display:none; position:fixed; inset:0; background:rgba(0,0,0,.65); align-items:center; justify-content:center; z-index:500; }
.modal-box{ width:90%; max-width:430px; background:white; padding:25px; border-radius:15px; max-height:85vh; overflow-y:auto; }
.modal-box h2{ margin-bottom:18px; }
.modal-box input, .modal-box textarea{ width:100%; padding:12px; margin:6px 0; border:1px solid #ddd; border-radius:8px; outline:none; }
.modal-box textarea{ height:100px; resize:none; }
.close{ float:right; border:0; background:white; font-size:25px; cursor:pointer; }
.main-btn{ width:100%; padding:12px; margin-top:10px; border:0; border-radius:8px; background:#d90000; color:white; font-weight:bold; cursor:pointer; }
.secondary-btn{ width:100%; padding:11px; margin-top:8px; border:1px solid #ddd; border-radius:8px; background:white; cursor:pointer; }
.account-info{ text-align:center; padding:10px; margin-bottom:10px; }
.account-info strong{ display:block; font-size:18px; }
.account-info small{ color:#777; }
.file-preview{ margin-top:8px; max-width:100%; max-height:200px; border-radius:8px; }
.userRow{ display:flex; align-items:center; gap:10px; padding:10px; border-radius:10px; cursor:pointer; }
.userRow:hover{ background:#f0f2f5; }
.chatItem{ display:flex; align-items:center; gap:10px; padding:10px; border-radius:10px; cursor:pointer; }
.chatItem:hover{ background:#f0f2f5; }
.chatItem small{ display:block; color:#777; }
#chatWindow{ display:none; }
#chatMessages{ height:280px; overflow-y:auto; background:#f7f7f7; border-radius:10px; padding:10px; margin:10px 0; }
.msg{ max-width:75%; padding:8px 12px; border-radius:14px; margin-bottom:8px; font-size:14px; }
.msg.mine{ background:#d90000; color:white; margin-left:auto; }
.msg.theirs{ background:white; border:1px solid #ddd; }
#storyViewer{ background:rgba(0,0,0,.9); }
#storyViewer .modal-box{ background:transparent; box-shadow:none; text-align:center; max-width:420px; }
#storyViewer img, #storyViewer video{ max-width:100%; max-height:70vh; border-radius:10px; }
#storyViewer .close{ background:transparent; color:white; }
.loading-text{ text-align:center; color:#999; padding:20px; }
@media(max-width:800px){
  .container{ display:block; padding:10px; }
  .sidebar, .rightbar{ display:none; }
  .search{ display:none; }
  .bottom{ display:flex; }
}
</style>
</head>
<body>

<header>
  <div class="logo" onclick="home()" title="Accueil">JB CHAT</div>
  <div class="search"><input id="searchInput" placeholder="Rechercher..." oninput="searchSite(this.value)" onkeydown="if(event.key==='Enter') searchSite(this.value)"></div>
  <div class="header-icons">
    <button class="icon" onclick="openMessages()">💬</button>
    <button class="icon" onclick="openAccount()">👤</button>
  </div>
</header>

<div class="container">
  <aside class="sidebar">
    <div class="menu">
      <div id="accountMenu" class="account-info">
        <strong>JB CHAT</strong>
        <small>Chargement...</small>
      </div>
      <button onclick="home()">🏠 Accueil</button>
      <button onclick="openProfile()">👤 Profil</button>
      <button onclick="openMessages()">💬 Messages</button>
      <button onclick="openNotifications()">🔔 Notifications</button>
      <button onclick="openAccount()">🔐 Compte</button>
      <button onclick="openSettings()">⚙️ Réglages</button>
    </div>
  </aside>

  <section class="feed">
    <div id="profilePage" class="profile">
      <div class="cover"></div>
      <div class="profile-content">
        <div id="profilePhoto" class="profile-photo">J</div>
        <div id="profileName" class="profile-name">JB CHAT</div>
        <div id="profileBio" class="profile-bio">Bienvenue sur mon profil ❤️</div>
         <div id="verificationBadge" style="font-size:13px;margin:6px 0;color:#777;"></div>

<div id="followStats" style="display:flex;gap:22px;justify-content:center;margin:12px 0;font-size:14px;">
  <span><b id="followersCount">0</b><br>Abonnés</span>
  <span><b id="followingCount">0</b><br>Suivis</span>
</div>
<button id="followBtn" class="main-btn" onclick="toggleFollow()" style="display:none;">➕ Suivre</button>
<button id="followersBtn" class="secondary-btn" onclick="openFollowersList()">👥 Voir les abonnés</button>
<button class="secondary-btn" onclick="openFollowingList()">➡️ Voir les suivis</button>

        <div class="profile-stats">
          <div class="stat"><strong id="postCount">0</strong><span>Publications</span></div>
        </div>
        <button class="profile-button" onclick="openEditProfile()">✏️ Modifier le profil</button>
      </div>
    </div>

    <div class="stories" id="storiesBar">
      <div class="story" onclick="triggerStoryUpload()">
        <div class="story-photo" style="background:#ccc;color:#555;">+</div>
        <span>Votre story</span>
      </div>
    </div>
    <input type="file" id="storyFileInput" accept="image/*,video/*" style="display:none" onchange="publishStory(event)">

    <div class="create">
      <div class="create-top">
        <div id="createAvatar" class="avatar">J</div>
        <input id="postInput" placeholder="Quoi de neuf ?" onkeydown="quickPost(event)">
      </div>
      <div class="create-actions">
        <button onclick="openCreate()">📝 Publication</button>
        <button onclick="openCreate()">📷 Photo / Vidéo</button>
        <button onclick="openMessages()">💬 Message</button>
      </div>
    </div>

    <div id="feed">
      <div class="loading-text">Chargement des publications...</div>
    </div>
  </section>

  <aside class="rightbar">
    <div class="card">
      <h3>Suggestions</h3>
      <div id="suggestionsList"><div class="loading-text">...</div></div>
    </div>
    <div class="card">
      <h3>JB CHAT</h3>
      <p>Connectez-vous avec votre communauté.</p>
    </div>
  </aside>
</div>

<nav class="bottom">
  <button onclick="home()">🏠</button>
  <button onclick="focusSearch()">🔍</button>
  <button onclick="openCreate()">➕</button>
  <button onclick="openMessages()">💬</button>
  <button onclick="openProfile()">👤</button>
</nav>

<!-- ACCOUNT MODAL -->
<div id="accountModal" class="modal">
  <div class="modal-box">
    <button class="close" onclick="closeAccount()">×</button>
    <h2 id="accountTitle">🔐 Compte JB CHAT</h2>
    <div id="accountContent">
      <button class="main-btn" onclick="showRegister()">📝 Créer un compte</button>
      <button class="secondary-btn" onclick="showLogin()">🔑 Se connecter</button>
      <button class="secondary-btn" onclick="loginWithGoogle()">🔵 Continuer avec Google</button>
      <button class="secondary-btn" onclick="openPhoneAuth()">📱 Continuer avec un numéro</button>
    </div>
  </div>
</div>

<!-- REGISTER -->
<div id="registerModal" class="modal">
  <div class="modal-box">
    <button class="close" onclick="closeRegister()">×</button>
    <h2>📝 Créer un compte</h2>
    <input id="registerName" placeholder="Votre nom">
    <input id="registerUsername" placeholder="Nom d'utilisateur">
    <input id="registerEmail" type="email" placeholder="Votre email">
    <input id="registerPassword" type="password" placeholder="Mot de passe">
    <input id="registerPassword2" type="password" placeholder="Confirmer le mot de passe">
    <button class="main-btn" id="registerBtn" onclick="register()">Créer mon compte</button>
    <button class="secondary-btn" onclick="loginWithGoogle()">🔵 Continuer avec Google</button>
    <button class="secondary-btn" onclick="showLogin()">J'ai déjà un compte</button>
  </div>
</div>

<!-- LOGIN -->
<div id="loginModal" class="modal">
  <div class="modal-box">
    <button class="close" onclick="closeLogin()">×</button>
    <h2>🔑 Connexion</h2>
    <input id="loginEmail" type="email" placeholder="Email">
    <input id="loginPassword" type="password" placeholder="Mot de passe">
    <button class="main-btn" id="loginBtn" onclick="login()">Se connecter</button>
    <button class="secondary-btn" onclick="loginWithGoogle()">🔵 Continuer avec Google</button>
    <button class="secondary-btn" onclick="openPhoneAuth()">📱 Utiliser un numéro</button>
    <button class="secondary-btn" onclick="showRegister()">Créer un nouveau compte</button>
  </div>
</div>


<!-- PHONE AUTH -->
<div id="phoneModal" class="modal">
  <div class="modal-box">
    <button class="close" onclick="closePhoneAuth()">×</button>
    <h2>📱 Connexion par numéro</h2>
    <p style="color:#666;font-size:14px;margin-bottom:10px;">
      Entrez votre numéro au format international, par exemple : <b>+257XXXXXXXX</b>
    </p>

    <input id="phoneNumber" type="tel" placeholder="+257XXXXXXXX">
    <div id="recaptcha-container" style="margin:10px 0;"></div>

    <button class="main-btn" id="sendCodeBtn" onclick="sendPhoneCode()">
      📩 Envoyer le code SMS
    </button>

    <div id="phoneCodeArea" style="display:none;margin-top:12px;">
      <input id="phoneCode" inputmode="numeric" maxlength="6" placeholder="Code reçu par SMS">
      <button class="main-btn" onclick="verifyPhoneCode()">✅ Vérifier le code</button>
    </div>

    <button class="secondary-btn" onclick="closePhoneAuth()">Annuler</button>
  </div>
</div>

<!-- PROFILE EDIT -->
<div id="editProfileModal" class="modal">
  <div class="modal-box">
    <button class="close" onclick="closeEditProfile()">×</button>
    <h2>✏️ Modifier le profil</h2>
    <input id="editName" placeholder="Votre nom">
    <input id="editBio" placeholder="Votre bio">
    <label style="font-size:13px;color:#777;">Photo de profil</label>
    <input type="file" id="editPhotoFile" accept="image/*">
    <button class="main-btn" id="saveProfileBtn" onclick="saveProfile()">Enregistrer</button>
    <button class="secondary-btn" onclick="logout()">Déconnexion</button>
  </div>
</div>

<!-- CREATE POST -->
<div id="createModal" class="modal">
  <div class="modal-box">
    <button class="close" onclick="closeCreate()">×</button>
    <h2>📝 Créer une publication</h2>
    <textarea id="modalText" placeholder="Quoi de neuf ?"></textarea>
    <label style="font-size:13px;color:#777;">Photo ou vidéo (optionnel)</label>
    <input type="file" id="postFile" accept="image/*,video/*" onchange="previewPostFile(event)">
    <img id="postFilePreview" class="file-preview" style="display:none;">
    <button class="main-btn" id="publishBtn" onclick="publishPost()">Publier</button>
  </div>
</div>

<!-- MESSAGES -->
<div id="messagesModal" class="modal">
  <div class="modal-box">
    <button class="close" onclick="closeMessages()">×</button>
    <h2>💬 Messages</h2>

    <div id="chatListView">
      <button class="secondary-btn" onclick="openNewChatPicker()">✉️ Nouveau message</button>
      <div id="chatList" style="margin-top:10px;"><div class="loading-text">Connectez-vous pour voir vos messages.</div></div>
    </div>

    <div id="newChatPicker" style="display:none;">
      <button class="secondary-btn" onclick="closeNewChatPicker()">← Retour</button>
      <div id="usersToChat" style="margin-top:10px;"><div class="loading-text">Chargement...</div></div>
    </div>

    <div id="chatWindow">
      <button class="secondary-btn" onclick="closeChatWindow()">← Retour</button>
      <h3 id="chatWithName" style="margin:10px 0;"></h3>
      <div id="chatMessages"></div>
      <div style="display:flex;gap:8px;">
        <input id="chatMessageInput" placeholder="Écrire un message..." style="flex:1;padding:11px;border:1px solid #ddd;border-radius:20px;" onkeydown="if(event.key==='Enter')sendChatMessage()">
        <button onclick="sendChatMessage()" style="padding:11px 15px;border:0;background:#d90000;color:white;border-radius:20px;">➤</button>
      </div>
    </div>
  </div>
</div>



<!-- FOLLOWERS / FOLLOWING -->
<div id="followersModal" class="modal">
  <div class="modal-box">
    <button class="close" onclick="closeFollowersList()">×</button>
    <h2 id="followersModalTitle">👥 Abonnés</h2>
    <div id="followersList"><div class="loading-text">Chargement...</div></div>
  </div>
</div>

<!-- NOTIFICATIONS -->
<div id="notificationsModal" class="modal">
  <div class="modal-box">
    <button class="close" onclick="closeNotifications()">×</button>
    <h2>🔔 Notifications</h2>
    <div id="notificationsContent">
      <div class="loading-text">Aucune notification pour le moment.</div>
    </div>
  </div>
</div>

<!-- SETTINGS -->
<div id="settingsModal" class="modal">
  <div class="modal-box">
    <button class="close" onclick="closeSettings()">×</button>
    <h2>⚙️ Réglages</h2>

    <div id="settingsAccountStatus" style="padding:10px 0;color:#666;"></div>

    <button class="main-btn" onclick="openEditProfile();closeSettings()">✏️ Modifier mon profil</button>
    <button class="secondary-btn" onclick="sendVerificationEmail()">📧 Envoyer la vérification e-mail</button>
    <button class="secondary-btn" onclick="refreshEmailVerification()">✅ Vérifier mon e-mail</button>
    <button class="secondary-btn" onclick="requestGallery()">📷 Ouvrir la galerie</button>
    <button class="secondary-btn" onclick="requestContacts()">👥 Autoriser les contacts</button>
    <button class="secondary-btn" onclick="requestLocation()">📍 Autoriser la localisation</button>
    <button class="secondary-btn" onclick="makeCall(prompt('Numéro à appeler :'))">📞 Appeler un numéro</button>
    <button class="secondary-btn" onclick="logout()">🚪 Déconnexion</button>
  </div>
</div>

<!-- STORY VIEWER -->
<div id="storyViewer" class="modal">
  <div class="modal-box">
    <button class="close" onclick="closeStoryViewer()">×</button>
    <div id="storyViewerName" style="color:white;margin-bottom:10px;font-weight:bold;"></div>
    <div id="storyViewerContent"></div>
  </div>
</div>

<script src="https://www.gstatic.com/firebasejs/10.12.2/firebase-app-compat.js"></script>
<script src="https://www.gstatic.com/firebasejs/10.12.2/firebase-auth-compat.js"></script>
<script src="https://www.gstatic.com/firebasejs/10.12.2/firebase-firestore-compat.js"></script>
<script src="https://www.gstatic.com/firebasejs/10.12.2/firebase-storage-compat.js"></script>

<script>
/* ============================== FIREBASE INIT ============================== */
const firebaseConfig = {
  apiKey: "AIzaSyCerm6rbNlXs86OxDrN6h0oJEfIbd95i90",
  authDomain: "jb-chat-4b3cd.firebaseapp.com",
  projectId: "jb-chat-4b3cd",
  storageBucket: "jb-chat-4b3cd.firebasestorage.app",
  messagingSenderId: "624682606365",
  appId: "1:624682606365:web:74600b2ad4aef9e0728bf4",
  measurementId: "G-R19Z7WYHHB"
};
firebase.initializeApp(firebaseConfig);
const auth = firebase.auth();
const db = firebase.firestore();
const storage = firebase.storage();
const FieldValue = firebase.firestore.FieldValue;

let currentUser = null;
let profile = null;
let postFileToUpload = null;
let commentUnsubs = {};
let chatUnsub = null;
let activeChatId = null;

/* ============================== HELPERS ============================== */
function escapeHTML(text){
  const div = document.createElement("div");
  div.textContent = text || "";
  return div.innerHTML;
}
function timeAgo(ts){
  if(!ts) return "À l'instant";
  const date = ts.toDate ? ts.toDate() : new Date(ts);
  const diff = Math.floor((Date.now() - date.getTime())/1000);
  if(diff < 60) return "À l'instant";
  if(diff < 3600) return Math.floor(diff/60) + " min";
  if(diff < 86400) return Math.floor(diff/3600) + " h";
  return date.toLocaleDateString();
}
async function uploadFile(file, path){
  const ref = storage.ref().child(path);
  const snap = await ref.put(file);
  return await snap.ref.getDownloadURL();
}

/* ============================== ACCOUNT MODALS ============================== */
function openAccount(){ document.getElementById("accountModal").style.display="flex"; }
function closeAccount(){ document.getElementById("accountModal").style.display="none"; }
function showRegister(){ closeAccount(); closeLogin(); document.getElementById("registerModal").style.display="flex"; }
function showLogin(){ closeAccount(); closeRegister(); document.getElementById("loginModal").style.display="flex"; }
function closeRegister(){ document.getElementById("registerModal").style.display="none"; }
function closeLogin(){ document.getElementById("loginModal").style.display="none"; }

/* ============================== REGISTER / LOGIN / LOGOUT ============================== */
function normalizeEmail(value){
  return (value || "").trim().toLowerCase();
}

function isValidEmail(email){
  return /^[^\s@]+@[^\s@]+\.[^\s@]{2,}$/.test(email);
}

function showEmailError(message, inputId){
  const input = document.getElementById(inputId);
  if(input){
    input.focus();
    input.style.border = "2px solid #d90000";
    setTimeout(() => input.style.border = "1px solid #ddd", 2500);
  }
  alert(message);
}

async function register(){
  const name = document.getElementById("registerName").value.trim();
  const username = document.getElementById("registerUsername").value.trim();
  const email = normalizeEmail(document.getElementById("registerEmail").value);
  const password = document.getElementById("registerPassword").value;
  const password2 = document.getElementById("registerPassword2").value;

  if(!name || !username || !email || !password || !password2){ alert("Remplissez tous les champs."); return; }
  if(!isValidEmail(email)){ showEmailError("Email invalide. Exemple : jaylosy@gmail.com", "registerEmail"); return; }
  if(password !== password2){ alert("Les mots de passe ne correspondent pas."); return; }
  if(password.length < 6){ alert("Le mot de passe doit avoir au moins 6 caractères."); return; }

  const btn = document.getElementById("registerBtn");
  btn.disabled = true; btn.textContent = "Création...";
  try{
    const cred = await auth.createUserWithEmailAndPassword(email, password);
    await db.collection("users").doc(cred.user.uid).set({
      name, username, email, bio:"Bienvenue sur mon profil ❤️",
      photoURL:"", createdAt: FieldValue.serverTimestamp()
    });
    try{ await cred.user.sendEmailVerification(); }catch(e){}
    closeRegister();
    alert("Compte créé avec succès ! 🎉\nUn e-mail de vérification a été envoyé à " + email + ".");
    openProfile();
  }catch(err){
    let message = "Impossible de créer le compte.";
    if(err.code === "auth/invalid-email") message = "Email invalide. Exemple : jaylosy@gmail.com";
    else if(err.code === "auth/email-already-in-use") message = "Cet email est déjà utilisé. Essayez de vous connecter.";
    else if(err.code === "auth/weak-password") message = "Le mot de passe est trop faible. Utilisez au moins 6 caractères.";
    else message += "\n" + err.message;
    alert(message);
  }
  btn.disabled = false; btn.textContent = "Créer mon compte";
}

async function login(){
  const email = normalizeEmail(document.getElementById("loginEmail").value);
  const password = document.getElementById("loginPassword").value;
  if(!email || !password){ alert("Remplissez tous les champs."); return; }
  if(!isValidEmail(email)){ showEmailError("Email invalide. Exemple : jaylosy@gmail.com", "loginEmail"); return; }

  const btn = document.getElementById("loginBtn");
  btn.disabled = true; btn.textContent = "Connexion...";
  try{
    await auth.signInWithEmailAndPassword(email, password);
    closeLogin();
    alert("Connexion réussie ! 👋");
  }catch(err){
    let message = "Impossible de se connecter.";
    if(err.code === "auth/invalid-email") message = "Email invalide. Exemple : jaylosy@gmail.com";
    else if(err.code === "auth/user-not-found") message = "Aucun compte ne correspond à cet email.";
    else if(err.code === "auth/wrong-password" || err.code === "auth/invalid-credential") message = "Email ou mot de passe incorrect.";
    else message += "\n" + err.message;
    alert(message);
  }
  btn.disabled = false; btn.textContent = "Se connecter";
}

async function loginWithGoogle(){
  try{
    const provider = new firebase.auth.GoogleAuthProvider();
    provider.setCustomParameters({prompt:"select_account"});
    const result = await auth.signInWithPopup(provider);
    const user = result.user;

    const ref = db.collection("users").doc(user.uid);
    const doc = await ref.get();

    if(!doc.exists){
      const name = user.displayName || "Utilisateur";
      await ref.set({
        name,
        username: (name.toLowerCase().replace(/[^a-z0-9]/g,"").slice(0,20) || "user") + Math.floor(Math.random()*10000),
        email: user.email || "",
        bio:"Bienvenue sur mon profil ❤️",
        photoURL:user.photoURL || "",
        createdAt: FieldValue.serverTimestamp()
      });
    }

    closeAccount();
    closeLogin();
    closeRegister();
    alert("Connexion Google réussie ! 👋");
  }catch(err){
    if(err.code === "auth/popup-blocked" || err.code === "auth/popup-closed-by-user"){
      alert("La fenêtre Google a été bloquée ou fermée. Autorisez les fenêtres pop-up puis réessayez.");
    }else if(err.code === "auth/operation-not-allowed"){
      alert("La connexion Google n'est pas encore activée dans Firebase Authentication.");
    }else{
      alert("Connexion Google : " + err.message);
    }
  }
}

async function sendVerificationEmail(){
  if(!currentUser) return;
  if(currentUser.emailVerified){
    alert("Votre adresse e-mail est déjà vérifiée ✅");
    return;
  }
  try{
    await currentUser.sendEmailVerification();
    alert("E-mail de vérification envoyé à " + currentUser.email + " 📧");
  }catch(err){
    alert("Erreur : " + err.message);
  }
}

async function refreshEmailVerification(){
  if(!currentUser) return;
  await currentUser.reload();
  currentUser = auth.currentUser;
  if(currentUser.emailVerified){
    alert("Votre e-mail est maintenant vérifié ✅");
  }else{
    alert("Votre e-mail n'est pas encore vérifié.");
  }
  updateInterface();
}

function requestGallery(){
  if(!currentUser){ openAccount(); return; }
  const input = document.createElement("input");
  input.type = "file";
  input.accept = "image/*,video/*";
  input.multiple = true;
  input.onchange = () => {
    if(input.files.length) alert(input.files.length + " fichier(s) sélectionné(s) depuis la galerie 📷");
  };
  input.click();
}

async function requestContacts(){
  if(!currentUser){ openAccount(); return; }

  if(!("contacts" in navigator) || !navigator.contacts.select){
    alert("La sélection des contacts n'est pas prise en charge par ce navigateur. Essayez Chrome sur Android.");
    return;
  }

  try{
    const contacts = await navigator.contacts.select(
      ["name","tel","email"],
      {multiple:true}
    );
    alert(contacts.length + " contact(s) sélectionné(s) 👥");
  }catch(err){
    if(err.name !== "AbortError") alert("Accès aux contacts refusé ou indisponible.");
  }
}

function requestLocation(){
  if(!currentUser){ openAccount(); return; }
  if(!navigator.geolocation){
    alert("La géolocalisation n'est pas disponible sur ce navigateur.");
    return;
  }

  navigator.geolocation.getCurrentPosition(
    pos => {
      const lat = pos.coords.latitude;
      const lng = pos.coords.longitude;
      alert("Position obtenue 📍\nLatitude : " + lat + "\nLongitude : " + lng);
    },
    err => alert("Autorisation de localisation refusée ou indisponible.")
  );
}

function makeCall(phone){
  if(!phone){
    alert("Aucun numéro de téléphone disponible.");
    return;
  }
  window.location.href = "tel:" + phone;
}

let phoneConfirmationResult = null;
let phoneRecaptcha = null;

function openPhoneAuth(){
  closeAccount();
  closeLogin();
  closeRegister();
  document.getElementById("phoneModal").style.display = "flex";
  document.getElementById("phoneCodeArea").style.display = "none";
  document.getElementById("phoneCode").value = "";

  setTimeout(() => {
    try{
      if(phoneRecaptcha) phoneRecaptcha.clear();
    }catch(e){}
    phoneRecaptcha = new firebase.auth.RecaptchaVerifier("recaptcha-container", {
      size: "normal",
      callback: function(){}
    });
    phoneRecaptcha.render().catch(() => {});
  }, 150);
}

function closePhoneAuth(){
  document.getElementById("phoneModal").style.display = "none";
  try{
    if(phoneRecaptcha) phoneRecaptcha.clear();
  }catch(e){}
  phoneRecaptcha = null;
  phoneConfirmationResult = null;
}

async function sendPhoneCode(){
  const phone = document.getElementById("phoneNumber").value.trim();

  if(!/^\+[1-9]\d{7,14}$/.test(phone)){
    alert("Numéro invalide. Utilisez le format international, par exemple : +257XXXXXXXX");
    return;
  }

  const btn = document.getElementById("sendCodeBtn");
  btn.disabled = true;
  btn.textContent = "Envoi du SMS...";

  try{
    if(!phoneRecaptcha){
      phoneRecaptcha = new firebase.auth.RecaptchaVerifier("recaptcha-container", {
        size: "normal",
        callback: function(){}
      });
    }

    phoneConfirmationResult = await auth.signInWithPhoneNumber(phone, phoneRecaptcha);
    document.getElementById("phoneCodeArea").style.display = "block";
    alert("Le code de vérification a été envoyé par SMS 📩");
  }catch(err){
    let msg = "Impossible d'envoyer le code.";
    if(err.code === "auth/invalid-phone-number") msg = "Numéro invalide. Exemple : +257XXXXXXXX";
    else if(err.code === "auth/operation-not-allowed") msg = "L'authentification par téléphone n'est pas activée dans Firebase.";
    else if(err.code === "auth/quota-exceeded") msg = "La limite SMS Firebase a été dépassée. Réessayez plus tard.";
    else if(err.code === "auth/captcha-check-failed") msg = "La vérification reCAPTCHA a échoué. Réessayez.";
    else msg += "\n" + err.message;
    alert(msg);

    try{
      if(phoneRecaptcha) phoneRecaptcha.clear();
    }catch(e){}
    phoneRecaptcha = null;
    setTimeout(() => openPhoneAuth(), 100);
  }

  btn.disabled = false;
  btn.textContent = "📩 Envoyer le code SMS";
}

async function verifyPhoneCode(){
  const code = document.getElementById("phoneCode").value.trim();

  if(!phoneConfirmationResult){
    alert("Demandez d'abord le code SMS.");
    return;
  }

  if(!/^\d{6}$/.test(code)){
    alert("Le code doit contenir 6 chiffres.");
    return;
  }

  try{
    const result = await phoneConfirmationResult.confirm(code);
    const user = result.user;
    const ref = db.collection("users").doc(user.uid);
    const doc = await ref.get();

    if(!doc.exists){
      const phone = user.phoneNumber || "";
      const lastDigits = phone.replace(/\D/g,"").slice(-6);
      await ref.set({
        name: "Utilisateur " + (lastDigits || "JAYLOSY"),
        username: "user" + (lastDigits || Math.floor(Math.random()*100000)),
        email: user.email || "",
        phone: phone,
        bio: "Bienvenue sur mon profil ❤️",
        photoURL: "",
        createdAt: FieldValue.serverTimestamp()
      });
    }else{
      await ref.set({phone: user.phoneNumber || ""}, {merge:true});
    }

    closePhoneAuth();
    alert("Numéro vérifié avec succès ! 🎉");
  }catch(err){
    if(err.code === "auth/invalid-verification-code"){
      alert("Code incorrect. Vérifiez le SMS et réessayez.");
    }else if(err.code === "auth/code-expired"){
      alert("Le code a expiré. Demandez un nouveau code.");
    }else{
      alert("Vérification : " + err.message);
    }
  }
}

function logout(){
  auth.signOut();
  closeAccount();
  closeEditProfile();
}

/* ============================== AUTH STATE ============================== */
auth.onAuthStateChanged(async (user) => {
  currentUser = user;
  if(user){
    const doc = await db.collection("users").doc(user.uid).get();
    profile = doc.exists ? doc.data() : null;
  } else {
    profile = null;
  }
  viewedProfileUid = user ? user.uid : null;
  viewedProfileData = user && profile ? {uid:user.uid,...profile} : null;
  updateInterface();
});

function updateInterface(){
  const menu = document.getElementById("accountMenu");
  if(currentUser && profile){
    const verificationText = currentUser.emailVerified ? "E-mail vérifié ✅" : "E-mail non vérifié ⚠️";
    menu.innerHTML = `
      <strong>${escapeHTML(profile.name)}</strong>
      <small>@${escapeHTML(profile.username)}</small><small>${verificationText}</small>
      <button onclick="logout()" style="margin-top:8px;color:#d90000;background:white;border:0;cursor:pointer;">Déconnexion</button>
    `;
    document.getElementById("profileName").textContent = profile.name;
    document.getElementById("profileBio").textContent = profile.bio || "";
    if(viewedProfileUid){ updateFollowStats(viewedProfileUid); updateFollowButton(viewedProfileUid); }
    document.getElementById("verificationBadge").textContent = currentUser.emailVerified ? "📧 E-mail vérifié ✅" : (currentUser.phoneNumber ? "📱 Numéro vérifié ✅" : "📧 E-mail non vérifié ⚠️");
    document.getElementById("createAvatar").innerHTML = profile.photoURL
      ? `<img src="${profile.photoURL}">` : escapeHTML(profile.name.charAt(0).toUpperCase());
    document.getElementById("profilePhoto").innerHTML = profile.photoURL
      ? `<img src="${profile.photoURL}">` : escapeHTML(profile.name.charAt(0).toUpperCase());
    loadChatList();
  } else {
    menu.innerHTML = `<strong>JB CHAT</strong><small>Visiteur — <a href="#" onclick="openAccount();return false;" style="color:#d90000;">connectez-vous</a></small>`;
    document.getElementById("profileName").textContent = "Visiteur";
    document.getElementById("profileBio").textContent = "Connectez-vous pour créer votre profil";
    document.getElementById("verificationBadge").textContent = "";
    document.getElementById("createAvatar").textContent = "?";
    document.getElementById("profilePhoto").textContent = "?";
    document.getElementById("chatList").innerHTML = `<div class="loading-text">Connectez-vous pour voir vos messages.</div>`;
  }
}

/* ============================== PROFILE ============================== */
async function openProfile(profileUid){
  const uid = profileUid || (currentUser ? currentUser.uid : null);
  if(!uid){ openAccount(); return; }
  viewedProfileUid = uid;
  const ref = db.collection("users").doc(uid);
  const doc = await ref.get();
  if(!doc.exists){ alert("Profil introuvable."); return; }
  viewedProfileData = { uid, ...doc.data() };
  const data = viewedProfileData;
  document.getElementById("profilePage").style.display="block";
  document.getElementById("profileName").textContent = data.name || "Utilisateur";
  document.getElementById("profileBio").textContent = data.bio || "";
  document.getElementById("verificationBadge").textContent = data.phone ? "📱 Numéro vérifié ✅" : (uid === (currentUser && currentUser.uid) && currentUser.emailVerified ? "📧 E-mail vérifié ✅" : "");
  document.getElementById("profilePhoto").innerHTML = data.photoURL ? `<img src="${escapeHTML(data.photoURL)}">` : escapeHTML((data.name || "U").charAt(0).toUpperCase());
  const editBtn = document.querySelector("#profilePage .profile-button");
  if(editBtn) editBtn.style.display = currentUser && uid === currentUser.uid ? "inline-block" : "none";
  await updateFollowStats(uid);
  await updateFollowButton(uid);
  try{
    const postsSnap = await db.collection("posts").where("uid","==",uid).get();
    document.getElementById("postCount").textContent = postsSnap.size;
  }catch(e){ document.getElementById("postCount").textContent = "0"; }
  window.scrollTo({ top:0, behavior:"smooth" });
}
function openEditProfile(){
  if(!currentUser){ alert("Connectez-vous ou créez un compte d'abord."); openAccount(); return; }
  document.getElementById("editName").value = profile.name;
  document.getElementById("editBio").value = profile.bio || "";
  document.getElementById("editProfileModal").style.display="flex";
}
function closeEditProfile(){ document.getElementById("editProfileModal").style.display="none"; }

async function saveProfile(){
  if(!currentUser) return;
  const name = document.getElementById("editName").value.trim();
  const bio = document.getElementById("editBio").value.trim();
  const file = document.getElementById("editPhotoFile").files[0];
  const btn = document.getElementById("saveProfileBtn");
  btn.disabled = true; btn.textContent = "Enregistrement...";

  try{
    const updates = {};
    if(name) updates.name = name;
    if(bio) updates.bio = bio;
    if(file){
      const url = await uploadFile(file, `profile_photos/${currentUser.uid}_${Date.now()}`);
      updates.photoURL = url;
    }
    await db.collection("users").doc(currentUser.uid).update(updates);
    profile = { ...profile, ...updates };
    updateInterface();
    closeEditProfile();
    alert("Profil modifié avec succès ✅");
  }catch(err){
    alert("Erreur : " + err.message);
  }
  btn.disabled = false; btn.textContent = "Enregistrer";
}

/* ============================== FEED (temps réel) ============================== */
db.collection("posts").orderBy("createdAt","desc").limit(100)
  .onSnapshot(snap => {
    const feed = document.getElementById("feed");
    if(snap.empty){
      feed.innerHTML = `<div class="loading-text">Aucune publication pour le moment. Soyez le premier à publier !</div>`;
      document.getElementById("postCount").textContent = "0";
      return;
    }
    let html = "";
    let myPosts = 0;
    snap.forEach(doc => {
      const p = doc.data();
      const id = doc.id;
      if(currentUser && p.uid === currentUser.uid) myPosts++;
      const liked = currentUser && Array.isArray(p.likes) && p.likes.includes(currentUser.uid);
      const likeCount = Array.isArray(p.likes) ? p.likes.length : 0;
      let mediaHTML = "";
      if(p.mediaURL){
        mediaHTML = p.mediaType === "video"
          ? `<div class="post-picture"><video src="${p.mediaURL}" controls></video></div>`
          : `<div class="post-picture"><img src="${p.mediaURL}"></div>`;
      }
      html += `
        <article class="post" data-id="${id}">
          <div class="post-head">
            <div class="avatar" onclick="openProfile('${id && p.uid ? p.uid : ""}')" style="cursor:pointer;">${p.photoURL ? `<img src="${p.photoURL}">` : escapeHTML((p.name||"?").charAt(0).toUpperCase())}</div>
            <div style="flex:1;cursor:pointer;" onclick="openProfile('${p.uid || ""}')"><strong>${escapeHTML(p.name)}</strong><small>${timeAgo(p.createdAt)}</small></div>
            <button class="post-menu-btn" onclick="openPostMenu('${id}','${p.uid || ""}')" title="Options">•••</button>
          </div>
          ${p.text ? `<p class="post-text">${escapeHTML(p.text)}</p>` : ""}
          ${mediaHTML}
          <div class="post-actions">
            <button class="${liked ? 'liked' : ''}" onclick="toggleLike('${id}')">❤️ <span>${likeCount}</span></button>
            <button onclick="showComments('${id}')">💬 Commenter</button>
            <button onclick="sharePost('${id}')">↗️ Partager</button>
          </div>
          <div class="comments" id="comments-${id}">
            <div id="commentsList-${id}"></div>
            ${currentUser ? `
              <input class="comment-input" id="commentInput-${id}" placeholder="Écrire un commentaire..." onkeydown="if(event.key==='Enter')sendComment('${id}')">
              <button class="comment-send" onclick="sendComment('${id}')">Envoyer</button>
            ` : `<small style="color:#777;">Connectez-vous pour commenter.</small>`}
          </div>
        </article>
      `;
    });
    feed.innerHTML = html;
    document.getElementById("postCount").textContent = myPosts;
  }, err => {
    document.getElementById("feed").innerHTML = `<div class="loading-text">Erreur de chargement : ${escapeHTML(err.message)}</div>`;
  });

function previewPostFile(event){
  const file = event.target.files[0];
  postFileToUpload = file || null;
  const preview = document.getElementById("postFilePreview");
  if(file && file.type.startsWith("image/")){
    preview.src = URL.createObjectURL(file);
    preview.style.display = "block";
  } else {
    preview.style.display = "none";
  }
}

function openCreate(){
  if(!currentUser){ alert("Connectez-vous ou créez un compte d'abord."); openAccount(); return; }
  document.getElementById("createModal").style.display="flex";
}
function closeCreate(){
  document.getElementById("createModal").style.display="none";
  document.getElementById("modalText").value = "";
  document.getElementById("postFile").value = "";
  document.getElementById("postFilePreview").style.display = "none";
  postFileToUpload = null;
}

async function publishPost(){
  if(!currentUser){ openAccount(); return; }
  const text = document.getElementById("modalText").value.trim();
  if(!text && !postFileToUpload){ alert("Écrivez quelque chose ou ajoutez une photo/vidéo."); return; }

  const btn = document.getElementById("publishBtn");
  btn.disabled = true; btn.textContent = "Publication...";
  try{
    let mediaURL = "", mediaType = "";
    if(postFileToUpload){
      mediaType = postFileToUpload.type.startsWith("video/") ? "video" : "image";
      mediaURL = await uploadFile(postFileToUpload, `posts/${currentUser.uid}/${Date.now()}_${postFileToUpload.name}`);
    }
    await db.collection("posts").add({
      uid: currentUser.uid, name: profile.name, photoURL: profile.photoURL || "",
      text, mediaURL, mediaType, likes: [], createdAt: FieldValue.serverTimestamp()
    });
    closeCreate();
  }catch(err){
    alert("Erreur : " + err.message);
  }
  btn.disabled = false; btn.textContent = "Publier";
}

async function quickPost(event){
  if(event.key !== "Enter") return;
  if(!currentUser){ openAccount(); return; }
  const input = document.getElementById("postInput");
  const text = input.value.trim();
  if(!text) return;
  input.value = "";
  try{
    await db.collection("posts").add({
      uid: currentUser.uid, name: profile.name, photoURL: profile.photoURL || "",
      text, mediaURL:"", mediaType:"", likes: [], createdAt: FieldValue.serverTimestamp()
    });
  }catch(err){ alert("Erreur : " + err.message); }
}

async function toggleLike(postId){
  if(!currentUser){ openAccount(); return; }
  try{
    const ref = db.collection("posts").doc(postId);
    const doc = await ref.get();
    if(!doc.exists) return;
    const post = doc.data();
    const likes = post.likes || [];
    if(likes.includes(currentUser.uid)){
      await ref.update({ likes: FieldValue.arrayRemove(currentUser.uid) });
    } else {
      await ref.update({ likes: FieldValue.arrayUnion(currentUser.uid) });
      if(post.uid && post.uid !== currentUser.uid){
        await db.collection("notifications").add({type:"like",fromUid:currentUser.uid,toUid:post.uid,text:(profile?.name||"Quelqu'un")+" a aimé votre publication.",createdAt:FieldValue.serverTimestamp(),read:false,postId});
      }
    }
  }catch(err){ alert("Impossible de modifier le like : " + err.message); }
}

function sharePost(postId){
  const url = window.location.href.split("#")[0] + "#post-" + postId;
  navigator.clipboard?.writeText(url).catch(()=>{});
  alert("Lien de la publication copié 🔗");
}

/* ============================== COMMENTS (temps réel) ============================== */
function showComments(postId){
  const box = document.getElementById("comments-" + postId);
  const isOpening = box.style.display !== "block";
  box.style.display = isOpening ? "block" : "none";
  if(isOpening && !commentUnsubs[postId]){
    commentUnsubs[postId] = db.collection("posts").doc(postId).collection("comments")
      .orderBy("createdAt","asc")
      .onSnapshot(snap => {
        let html = "";
        snap.forEach(d => {
          const c = d.data();
          html += `<div class="comment"><b>${escapeHTML(c.name)} :</b> ${escapeHTML(c.text)}</div>`;
        });
        document.getElementById("commentsList-" + postId).innerHTML = html;
      });
  }
}

async function sendComment(postId){
  if(!currentUser){ openAccount(); return; }
  const input = document.getElementById("commentInput-" + postId);
  const text = input.value.trim();
  if(!text) return;
  input.value = "";
  try{
    const postDoc = await db.collection("posts").doc(postId).get();
    const post = postDoc.exists ? postDoc.data() : null;
    await db.collection("posts").doc(postId).collection("comments").add({
      uid: currentUser.uid, name: profile.name, text, createdAt: FieldValue.serverTimestamp()
    });
    if(post && post.uid && post.uid !== currentUser.uid){
      await db.collection("notifications").add({type:"comment",fromUid:currentUser.uid,toUid:post.uid,text:(profile?.name||"Quelqu'un")+" a commenté votre publication.",createdAt:FieldValue.serverTimestamp(),read:false,postId});
    }
  }catch(err){ alert("Impossible d'envoyer le commentaire : " + err.message); }
}

/* ============================== STORIES (temps réel, 24h) ============================== */
db.collection("stories").orderBy("createdAt","desc").limit(50)
  .onSnapshot(snap => {
    const bar = document.getElementById("storiesBar");
    const cutoff = Date.now() - 24*60*60*1000;
    let html = `
      <div class="story" onclick="triggerStoryUpload()">
        <div class="story-photo" style="background:#ccc;color:#555;">+</div>
        <span>Votre story</span>
      </div>`;
    snap.forEach(doc => {
      const s = doc.data();
      const ts = s.createdAt && s.createdAt.toDate ? s.createdAt.toDate().getTime() : Date.now();
      if(ts < cutoff) return;
      html += `
        <div class="story" onclick="viewStory('${doc.id}')">
          <div class="story-photo">${s.mediaType==='video' ? '▶️' : (s.userPhotoURL ? `<img src="${s.userPhotoURL}">` : escapeHTML((s.name||"?").charAt(0).toUpperCase()))}</div>
          <span>${escapeHTML(s.name)}</span>
        </div>`;
    });
    bar.innerHTML = html;
  });

function triggerStoryUpload(){
  if(!currentUser){ alert("Connectez-vous ou créez un compte d'abord."); openAccount(); return; }
  document.getElementById("storyFileInput").click();
}

async function publishStory(event){
  const file = event.target.files[0];
  event.target.value = "";
  if(!file || !currentUser) return;
  try{
    const mediaType = file.type.startsWith("video/") ? "video" : "image";
    const mediaURL = await uploadFile(file, `stories/${currentUser.uid}/${Date.now()}_${file.name}`);
    await db.collection("stories").add({
      uid: currentUser.uid, name: profile.name, userPhotoURL: profile.photoURL || "",
      mediaURL, mediaType, createdAt: FieldValue.serverTimestamp()
    });
    alert("Story publiée ✅ (visible pendant 24h)");
  }catch(err){ alert("Erreur : " + err.message); }
}

async function viewStory(storyId){
  const doc = await db.collection("stories").doc(storyId).get();
  if(!doc.exists) return;
  const s = doc.data();
  document.getElementById("storyViewerName").textContent = s.name;
  document.getElementById("storyViewerContent").innerHTML = s.mediaType === "video"
    ? `<video src="${s.mediaURL}" controls autoplay></video>`
    : `<img src="${s.mediaURL}">`;
  document.getElementById("storyViewer").style.display = "flex";
}
function closeStoryViewer(){ document.getElementById("storyViewer").style.display="none"; }

/* ============================== MESSAGES ============================== */
function openMessages(){
  document.getElementById("messagesModal").style.display="flex";
  document.getElementById("chatListView").style.display="block";
  document.getElementById("newChatPicker").style.display="none";
  document.getElementById("chatWindow").style.display="none";
}
function closeMessages(){
  if(chatUnsub){ chatUnsub(); chatUnsub = null; }
  activeChatId = null;
  document.getElementById("messagesModal").style.display="none";
}

function loadChatList(){
  if(!currentUser) return;
  db.collection("chats").where("participants","array-contains", currentUser.uid)
    .onSnapshot(snap => {
      if(snap.empty){
        document.getElementById("chatList").innerHTML = `<div class="loading-text">Aucune conversation. Cliquez sur "Nouveau message".</div>`;
        return;
      }
      let chats = [];
      snap.forEach(doc => chats.push({ id: doc.id, ...doc.data() }));
      chats.sort((a,b) => (b.updatedAt?.toMillis?.()||0) - (a.updatedAt?.toMillis?.()||0));
      let html = "";
      chats.forEach(c => {
        const otherUid = c.participants.find(u => u !== currentUser.uid);
        const otherName = (c.participantNames && c.participantNames[otherUid]) || "Utilisateur";
        html += `
          <div class="chatItem" onclick="openChatWindow('${c.id}', '${escapeHTML(otherName)}')">
            <div class="avatar">${escapeHTML(otherName.charAt(0).toUpperCase())}</div>
            <div><strong>${escapeHTML(otherName)}</strong><small>${escapeHTML(c.lastMessage || "")}</small></div>
          </div>`;
      });
      document.getElementById("chatList").innerHTML = html;
    });
}

async function openNewChatPicker(){
  document.getElementById("chatListView").style.display="none";
  document.getElementById("newChatPicker").style.display="block";
  if(!currentUser){ document.getElementById("usersToChat").innerHTML = `<div class="loading-text">Connectez-vous d'abord.</div>`; return; }
  const snap = await db.collection("users").limit(30).get();
  let html = "";
  snap.forEach(doc => {
    if(doc.id === currentUser.uid) return;
    const u = doc.data();
    html += `
      <div class="userRow" onclick="startChat('${doc.id}','${escapeHTML(u.name)}')">
        <div class="avatar">${u.photoURL ? `<img src="${u.photoURL}">` : escapeHTML(u.name.charAt(0).toUpperCase())}</div>
        <div><strong>${escapeHTML(u.name)}</strong><small>@${escapeHTML(u.username)}</small></div>
      </div>`;
  });
  document.getElementById("usersToChat").innerHTML = html || `<div class="loading-text">Aucun autre utilisateur pour le moment.</div>`;
}
function closeNewChatPicker(){
  document.getElementById("newChatPicker").style.display="none";
  document.getElementById("chatListView").style.display="block";
}

async function startChat(otherUid, otherName){
  const chatId = [currentUser.uid, otherUid].sort().join("_");
  const ref = db.collection("chats").doc(chatId);
  const doc = await ref.get();
  if(!doc.exists){
    await ref.set({
      participants: [currentUser.uid, otherUid],
      participantNames: { [currentUser.uid]: profile.name, [otherUid]: otherName },
      lastMessage: "", updatedAt: FieldValue.serverTimestamp()
    });
  }
  openChatWindow(chatId, otherName);
}

function openChatWindow(chatId, otherName){
  document.getElementById("chatListView").style.display="none";
  document.getElementById("newChatPicker").style.display="none";
  document.getElementById("chatWindow").style.display="block";
  document.getElementById("chatWithName").textContent = otherName;
  activeChatId = chatId;

  if(chatUnsub) chatUnsub();
  chatUnsub = db.collection("chats").doc(chatId).collection("messages").orderBy("createdAt","asc")
    .onSnapshot(snap => {
      let html = "";
      snap.forEach(doc => {
        const m = doc.data();
        const mine = m.from === currentUser.uid;
        html += `<div class="msg ${mine ? 'mine' : 'theirs'}">${escapeHTML(m.text)}</div>`;
      });
      const box = document.getElementById("chatMessages");
      box.innerHTML = html;
      box.scrollTop = box.scrollHeight;
    });
}
function closeChatWindow(){
  if(chatUnsub){ chatUnsub(); chatUnsub = null; }
  activeChatId = null;
  document.getElementById("chatWindow").style.display="none";
  document.getElementById("chatListView").style.display="block";
}

async function sendChatMessage(){
  if(!activeChatId || !currentUser) return;
  const input = document.getElementById("chatMessageInput");
  const text = input.value.trim();
  if(!text) return;
  input.value = "";
  await db.collection("chats").doc(activeChatId).collection("messages").add({
    from: currentUser.uid, text, createdAt: FieldValue.serverTimestamp()
  });
  await db.collection("chats").doc(activeChatId).update({
    lastMessage: text, updatedAt: FieldValue.serverTimestamp()
  });
}

/* ============================== SUGGESTIONS (autres utilisateurs) ============================== */
db.collection("users").limit(10).onSnapshot(snap => {
  let html = "";
  snap.forEach(doc => {
    if(currentUser && doc.id === currentUser.uid) return;
    const u = doc.data();
    html += `
      <div class="friend" onclick="startChatFromSuggestion('${doc.id}','${escapeHTML(u.name)}')">
        <div class="avatar">${u.photoURL ? `<img src="${u.photoURL}">` : escapeHTML((u.name||"?").charAt(0).toUpperCase())}</div>
        <strong>${escapeHTML(u.name)}</strong>
      </div>`;
  });
  document.getElementById("suggestionsList").innerHTML = html || `<div class="loading-text">Aucun utilisateur pour le moment.</div>`;
});
function startChatFromSuggestion(uid, name){
  if(!currentUser){ openAccount(); return; }
  openMessages();
  startChat(uid, name);
}

function openSettings(){
  if(!currentUser){
    alert("Connectez-vous ou créez un compte d'abord.");
    openAccount();
    return;
  }
  const status = currentUser.emailVerified
    ? "📧 E-mail vérifié ✅"
    : "📧 E-mail non vérifié ⚠️";
  document.getElementById("settingsAccountStatus").innerHTML =
    "<strong>" + escapeHTML(currentUser.email || currentUser.phoneNumber || "") + "</strong><br>" + status +
    (currentUser.phoneNumber ? "<br>📱 " + escapeHTML(currentUser.phoneNumber) : "");
  document.getElementById("settingsModal").style.display = "flex";
}

function closeSettings(){
  document.getElementById("settingsModal").style.display = "none";
}

function focusSearch(){
  const input = document.getElementById("searchInput");
  if(input){
    input.focus();
    input.scrollIntoView({behavior:"smooth", block:"center"});
  }
}

function searchSite(query){
  query = (query || "").trim().toLowerCase();

  document.querySelectorAll(".post").forEach(post => {
    post.style.display = !query || post.textContent.toLowerCase().includes(query) ? "" : "none";
  });

  document.querySelectorAll(".friend").forEach(friend => {
    friend.style.display = !query || friend.textContent.toLowerCase().includes(query) ? "" : "none";
  });

  document.querySelectorAll(".story").forEach(story => {
    story.style.display = !query || story.textContent.toLowerCase().includes(query) ? "" : "none";
  });
}

function openNotifications(){
  if(!currentUser){ openAccount(); return; }
  document.getElementById("notificationsModal").style.display = "flex";
  loadNotifications();
}

async function loadNotifications(){
  const box = document.getElementById("notificationsContent");
  box.innerHTML = '<div class="loading-text">Chargement...</div>';
  try{
    const snap = await db.collection("notifications").where("toUid","==",currentUser.uid).limit(50).get();
    const items = snap.docs.map(d => ({id:d.id,...d.data()})).sort((a,b) => (b.createdAt?.toMillis?.()||0)-(a.createdAt?.toMillis?.()||0));
    if(!items.length){ box.innerHTML = '<div class="loading-text">Aucune notification pour le moment.</div>'; return; }
    box.innerHTML = items.map(n => `
      <div style="padding:12px;border-bottom:1px solid #eee;cursor:pointer;" onclick="markNotificationRead('${n.id}')">
        <strong>${n.type === "follow" ? "👥" : n.type === "like" ? "❤️" : n.type === "comment" ? "💬" : "🔔"}</strong>
        ${escapeHTML(n.text || "Nouvelle notification")}
        <small style="display:block;color:#888;margin-top:4px;">${timeAgo(n.createdAt)}</small>
      </div>`).join("");
    await Promise.all(items.filter(n=>!n.read).map(n=>db.collection("notifications").doc(n.id).update({read:true}).catch(()=>{})));
  }catch(err){
    box.innerHTML = `<div class="loading-text">Erreur : ${escapeHTML(err.message)}</div>`;
  }
}

async function markNotificationRead(id){
  try{ await db.collection("notifications").doc(id).update({read:true}); }catch(e){}
}

function closeNotifications(){
  document.getElementById("notificationsModal").style.display = "none";
}

function openPostMenu(postId, ownerUid){
  if(!currentUser){
    openAccount();
    return;
  }

  if(currentUser.uid === ownerUid){
    const action = prompt("Publication :\n1 = Supprimer\n2 = Annuler\n\nEntrez 1 ou 2");
    if(action === "1") deletePost(postId);
  }else{
    alert("Publication signalée. Merci pour votre signalement.");
  }
}

async function deletePost(postId){
  if(!currentUser) return;

  if(!confirm("Supprimer cette publication ?")) return;

  try{
    await db.collection("posts").doc(postId).delete();
    alert("Publication supprimée ✅");
  }catch(err){
    alert("Impossible de supprimer : " + err.message);
  }
}

let viewedProfileUid = null;
let viewedProfileData = null;
let notificationsUnsub = null;
let chatListUnsub = null;

async function getFollowDoc(targetUid){
  if(!currentUser || !targetUid) return null;
  return db.collection("follows").doc(currentUser.uid + "_" + targetUid).get();
}

async function getFollowCounts(uid){
  try{
    const followersSnap = await db.collection("follows").where("following", "==", uid).get();
    const followingSnap = await db.collection("follows").where("follower", "==", uid).get();
    return {followers: followersSnap.size, following: followingSnap.size};
  }catch(err){
    return {followers:0, following:0};
  }
}

async function updateFollowStats(uid){
  const counts = await getFollowCounts(uid);
  const fc = document.getElementById("followersCount");
  const fg = document.getElementById("followingCount");
  if(fc) fc.textContent = counts.followers;
  if(fg) fg.textContent = counts.following;
}

async function updateFollowButton(uid){
  const btn = document.getElementById("followBtn");
  if(!btn || !currentUser || !uid || currentUser.uid === uid){
    if(btn) btn.style.display = "none";
    return;
  }

  btn.style.display = "block";
  const doc = await getFollowDoc(uid);
  const isFollowing = doc && doc.exists;
  btn.textContent = isFollowing ? "✅ Suivi — Ne plus suivre" : "➕ Suivre";
  btn.dataset.following = isFollowing ? "true" : "false";
}

async function toggleFollow(){
  if(!currentUser){
    openAccount();
    return;
  }

  const uid = viewedProfileUid;
  if(!uid || uid === currentUser.uid) return;

  const followId = currentUser.uid + "_" + uid;
  const ref = db.collection("follows").doc(followId);

  try{
    const doc = await ref.get();

    if(doc.exists){
      await ref.delete();
      alert("Vous ne suivez plus cet utilisateur.");
    }else{
      await ref.set({
        follower: currentUser.uid,
        following: uid,
        createdAt: FieldValue.serverTimestamp()
      });

      await db.collection("notifications").add({
        type:"follow",
        fromUid: currentUser.uid,
        toUid: uid,
        text:"vous suit maintenant.",
        createdAt: FieldValue.serverTimestamp(),
        read:false
      });

      alert("Vous suivez maintenant cet utilisateur ! ✅");
    }

    await updateFollowStats(uid);
    await updateFollowButton(uid);
  }catch(err){
    alert("Impossible de modifier le suivi : " + err.message);
  }
}

async function openFollowersList(){
  const uid = viewedProfileUid || (currentUser && currentUser.uid);
  if(!uid) return;

  document.getElementById("followersModal").style.display = "flex";
  document.getElementById("followersModalTitle").textContent = "👥 Abonnés";
  const list = document.getElementById("followersList");
  list.innerHTML = '<div class="loading-text">Chargement...</div>';

  try{
    const snap = await db.collection("follows").where("following", "==", uid).get();

    if(snap.empty){
      list.innerHTML = '<div class="loading-text">Aucun abonné pour le moment.</div>';
      return;
    }

    let html = "";
    for(const doc of snap.docs){
      const followerUid = doc.data().follower;
      const userDoc = await db.collection("users").doc(followerUid).get();
      const u = userDoc.exists ? userDoc.data() : {};
      html += `
        <div style="display:flex;align-items:center;gap:10px;padding:10px;border-bottom:1px solid #eee;">
          <div class="avatar">${escapeHTML((u.name || "U").charAt(0).toUpperCase())}</div>
          <div style="flex:1;">
            <strong>${escapeHTML(u.name || "Utilisateur")}</strong><br>
            <small>@${escapeHTML(u.username || "")}</small>
          </div>
        </div>`;
    }
    list.innerHTML = html;
  }catch(err){
    list.innerHTML = "<div class='loading-text'>Impossible de charger les abonnés.</div>";
  }
}

function closeFollowersList(){
  document.getElementById("followersModal").style.display = "none";
}

async function openFollowingList(){
  const uid = viewedProfileUid || (currentUser && currentUser.uid);
  if(!uid) return;

  document.getElementById("followersModal").style.display = "flex";
  document.getElementById("followersModalTitle").textContent = "➡️ Abonnements";
  const list = document.getElementById("followersList");
  list.innerHTML = '<div class="loading-text">Chargement...</div>';

  try{
    const snap = await db.collection("follows").where("follower", "==", uid).get();

    if(snap.empty){
      list.innerHTML = '<div class="loading-text">Vous ne suivez encore personne.</div>';
      return;
    }

    let html = "";
    for(const doc of snap.docs){
      const targetUid = doc.data().following;
      const userDoc = await db.collection("users").doc(targetUid).get();
      const u = userDoc.exists ? userDoc.data() : {};
      html += `
        <div style="display:flex;align-items:center;gap:10px;padding:10px;border-bottom:1px solid #eee;">
          <div class="avatar">${escapeHTML((u.name || "U").charAt(0).toUpperCase())}</div>
          <div style="flex:1;">
            <strong>${escapeHTML(u.name || "Utilisateur")}</strong><br>
            <small>@${escapeHTML(u.username || "")}</small>
          </div>
        </div>`;
    }
    list.innerHTML = html;
  }catch(err){
    list.innerHTML = "<div class='loading-text'>Impossible de charger les suivis.</div>";
  }
}

/* ============================== HOME / MODALS ============================== */
function home(){
  document.getElementById("profilePage").style.display="none";
  viewedProfileUid = currentUser ? currentUser.uid : null;
  viewedProfileData = currentUser && profile ? {uid:currentUser.uid,...profile} : null;
  window.scrollTo({ top:0, behavior:"smooth" });
}
window.onclick = function(event){
  if(event.target.classList.contains("modal")){
    event.target.style.display = "none";
  }
};
document.addEventListener("keydown", function(event){
  if(event.key === "Escape"){
    document.querySelectorAll(".modal").forEach(m => m.style.display = "none");
  }
});

</script>
</body>
</html>
