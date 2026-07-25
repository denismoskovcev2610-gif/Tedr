<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Одноклассники</title>
    <style>
        :root {
            --bg-color: #e3edf6;
            --main-bg: #ffffff;
            --header-bg: #f4731c;
            --text-color: #111111;
            --label-color: #2b577a;
            --border-color: #7ea3c3;
            --secondary-bg: #f8fafc;
        }

        [data-theme="dark"] {
            --bg-color: #12181f;
            --main-bg: #1e293b;
            --header-bg: #c2520c;
            --text-color: #f1f5f9;
            --label-color: #93c5fd;
            --border-color: #475569;
            --secondary-bg: #0f172a;
        }

        body {
            background-color: var(--bg-color);
            font-family: Arial, sans-serif;
            margin: 0;
            padding: 0;
            display: flex;
            justify-content: center;
            color: var(--text-color);
            transition: background-color 0.3s, color 0.3s;
        }
        .main-container {
            width: 100%;
            max-width: 600px;
            background-color: var(--main-bg);
            min-height: 100vh;
            box-shadow: 0 0 10px rgba(0,0,0,0.1);
            display: flex;
            flex-direction: column;
        }
        .header {
            background-color: var(--header-bg);
            color: white;
            padding: 15px;
            font-size: 18px;
            font-weight: bold;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }
        .btn-outline {
            background: none;
            border: 1px solid white;
            color: white;
            padding: 5px 8px;
            cursor: pointer;
            font-size: 11px;
            border-radius: 2px;
        }
        
        .nav-tabs {
            display: flex;
            background-color: var(--secondary-bg);
            border-bottom: 1px solid var(--border-color);
            overflow-x: auto;
        }
        .nav-tab {
            flex: 1;
            padding: 10px 3px;
            text-align: center;
            font-size: 10px;
            color: var(--label-color);
            cursor: pointer;
            font-weight: bold;
            border-bottom: 2px solid transparent;
            white-space: nowrap;
        }
        .nav-tab.active {
            border-bottom-color: var(--header-bg);
            background-color: var(--main-bg);
        }

        .login-card {
            padding: 40px 20px;
            width: 280px;
            margin: auto;
        }
        .form-group {
            margin-bottom: 15px;
        }
        label {
            display: block;
            color: var(--label-color);
            font-size: 13px;
            margin-bottom: 5px;
        }
        input[type="text"],
        input[type="password"] {
            width: 100%;
            padding: 8px;
            border: 1px solid var(--border-color);
            background-color: var(--main-bg);
            color: var(--text-color);
            box-sizing: border-box;
            font-size: 14px;
            outline: none;
        }
        .btn-submit {
            background: linear-gradient(to bottom, #ff9e3b 0%, #f4731c 100%);
            border: 1px solid #d45f12;
            color: white;
            padding: 6px 18px;
            font-size: 13px;
            font-weight: bold;
            cursor: pointer;
            border-radius: 2px;
        }

        .content-screen {
            flex: 1;
            overflow-y: auto;
        }

        .feed {
            padding: 15px;
        }
        .post {
            border-bottom: 1px solid var(--border-color);
            padding-bottom: 15px;
            margin-bottom: 15px;
        }
        .post-author {
            font-weight: bold;
            color: var(--label-color);
            margin-bottom: 5px;
        }
        .new-post {
            padding: 15px;
            background-color: var(--secondary-bg);
            border-bottom: 1px solid var(--border-color);
        }
        .new-post textarea {
            width: 100%;
            padding: 8px;
            border: 1px solid var(--border-color);
            background-color: var(--main-bg);
            color: var(--text-color);
            box-sizing: border-box;
            resize: none;
            height: 60px;
            outline: none;
        }
        .new-post button {
            background-color: var(--header-bg);
            color: white;
            border: none;
            padding: 6px 15px;
            font-weight: bold;
            cursor: pointer;
            margin-top: 5px;
            border-radius: 2px;
        }

        .profile-container {
            padding: 20px;
            text-align: center;
        }
        .avatar-box {
            width: 90px;
            height: 90px;
            border-radius: 50%;
            background-color: var(--border-color);
            margin: 0 auto 10px auto;
            overflow: hidden;
            display: flex;
            align-items: center;
            justify-content: center;
            border: 2px solid var(--header-bg);
        }
        .avatar-box img {
            width: 100%;
            height: 100%;
            object-fit: cover;
        }
        .profile-name {
            font-size: 18px;
            font-weight: bold;
            margin-bottom: 2px;
        }
        .profile-username {
            font-size: 13px;
            color: var(--header-bg);
            margin-bottom: 5px;
            font-weight: bold;
        }
        .profile-status {
            font-size: 13px;
            color: var(--label-color);
            margin-bottom: 20px;
        }
        .edit-profile-box {
            background-color: var(--secondary-bg);
            padding: 15px;
            border-radius: 6px;
            text-align: left;
            margin-top: 20px;
            border: 1px solid var(--border-color);
        }
        .edit-profile-box h4 {
            margin-top: 0;
            color: var(--label-color);
        }
        .edit-profile-box input {
            width: 100%;
            padding: 6px;
            margin-bottom: 10px;
            box-sizing: border-box;
            border: 1px solid var(--border-color);
            background: var(--main-bg);
            color: var(--text-color);
        }

        .friends-container {
            padding: 15px;
        }
        .friend-item {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 10px;
            border-bottom: 1px solid var(--border-color);
        }
        .chat-box {
            display: flex;
            flex-direction: column;
            height: calc(100vh - 110px);
        }
        .chat-messages {
            flex: 1;
            padding: 15px;
            overflow-y: auto;
            display: flex;
            flex-direction: column;
            gap: 8px;
        }
        .message {
            max-width: 75%;
            padding: 8px 12px;
            border-radius: 8px;
            font-size: 13px;
            word-break: break-word;
        }
        .message.my {
            background-color: var(--header-bg);
            color: white;
            align-self: flex-end;
        }
        .message.other {
            background-color: var(--secondary-bg);
            border: 1px solid var(--border-color);
            align-self: flex-start;
        }
        .chat-input-area {
            display: flex;
            padding: 10px;
            background-color: var(--secondary-bg);
            border-top: 1px solid var(--border-color);
        }
        .chat-input-area input {
            flex: 1;
            padding: 8px;
            border: 1px solid var(--border-color);
            background: var(--main-bg);
            color: var(--text-color);
            outline: none;
        }
        .chat-input-area button {
            background-color: var(--header-bg);
            color: white;
            border: none;
            padding: 0 15px;
            font-weight: bold;
            cursor: pointer;
            margin-left: 5px;
        }

        .settings-container {
            padding: 20px;
        }
        .settings-item {
            margin-bottom: 20px;
        }
        select {
            width: 100%;
            padding: 8px;
            border: 1px solid var(--border-color);
            background-color: var(--main-bg);
            color: var(--text-color);
            font-size: 14px;
            outline: none;
        }

        .hidden {
            display: none !important;
        }
    </style>
</head>
<body>

    <div class="main-container">
        <div class="header">
            <span id="headerTitle">Одноклассники</span>
            <button class="btn-outline hidden" id="logoutBtn">Выйти</button>
        </div>

        <div class="nav-tabs hidden" id="navTabs">
            <div class="nav-tab active" data-target="feedScreen" id="tabFeed">Лента</div>
            <div class="nav-tab" data-target="profileScreen" id="tabProfile">Профиль</div>
            <div class="nav-tab" data-target="friendsScreen" id="tabFriends">Друзья</div>
            <div class="nav-tab" data-target="publicChatScreen" id="tabPublicChat">Общий чат</div>
            <div class="nav-tab" data-target="channelScreen" id="tabChannel">Канал</div>
            <div class="nav-tab" data-target="settingsScreen" id="tabSettings">Настройки</div>
        </div>

        <!-- Авторизация -->
        <div id="loginScreen" class="login-card">
            <form id="loginForm">
                <div class="form-group">
                    <label id="labelLogin" for="loginInput">логин, адрес почты или телефон</label>
                    <input type="text" id="loginInput" autocomplete="username">
                </div>
                <div class="form-group">
                    <label id="labelPass" for="passwordInput">пароль</label>
                    <input type="password" id="passwordInput" autocomplete="current-password">
                </div>
                <button type="submit" id="btnLogin" class="btn-submit">Войти</button>
            </form>
        </div>

        <!-- Лента -->
        <div id="feedScreen" class="content-screen hidden">
            <div class="new-post">
                <textarea id="postText" placeholder="О чём вы думаете?"></textarea>
                <button id="sendPost">Опубликовать</button>
            </div>
            <div class="feed" id="feedContainer"></div>
        </div>

        <!-- Профиль -->
        <div id="profileScreen" class="content-screen hidden">
            <div class="profile-container">
                <div class="avatar-box" id="avatarBox"><span style="font-size: 12px;">Нет фото</span></div>
                <div class="profile-name" id="profileDisplayName">Имя</div>
                <div class="profile-username" id="profileDisplayUsername">@username</div>
                <div class="profile-status" id="profileDisplayStatus">Статус</div>

                <div class="edit-profile-box">
                    <h4 id="editProfileTitle">Редактировать профиль</h4>
                    <label id="labelUname">Ваш юзернейм (ЮЗ):</label>
                    <input type="text" id="inputUsername" placeholder="@username">
                    <label id="labelName">Ваше имя:</label>
                    <input type="text" id="inputName">
                    <label id="labelStatus">Ваш статус:</label>
                    <input type="text" id="inputStatus">
                    <label id="labelAvatar">Ссылка на аватар (фото):</label>
                    <input type="text" id="inputAvatar">
                    <button class="btn-submit" id="saveProfile">Сохранить</button>
                </div>
                <h4 id="myPostsHeader" style="text-align: left; margin-top: 20px; color: var(--label-color);">Мои записи:</h4>
                <div id="myPostsContainer" style="text-align: left;"></div>
            </div>
        </div>

        <!-- Друзья (ЛС заблокированы) -->
        <div id="friendsScreen" class="content-screen hidden">
            <div class="friends-container">
                <h3 id="searchFriendTitle" style="color: var(--label-color); margin-top:0;">Найти друга по ЮЗ</h3>
                <div style="display: flex; gap: 5px; margin-bottom: 15px;">
                    <input type="text" id="searchFriendInput" placeholder="@username">
                    <button class="btn-submit" id="addFriendBtn">Добавить</button>
                </div>
                <h3 id="friendsListTitle" style="color: var(--label-color);">Список друзей</h3>
                <div id="friendsContainer"></div>
            </div>
        </div>

        <!-- Общий чат для всех -->
        <div id="publicChatScreen" class="content-screen hidden">
            <div class="chat-box" style="height: calc(100vh - 65px);">
                <div style="padding: 10px; background: var(--secondary-bg); border-bottom: 1px solid var(--border-color); text-align: center; font-weight: bold;">
                    Общий чат для всех пользователей
                </div>
                <div class="chat-messages" id="publicChatMessages"></div>
                <div class="chat-input-area">
                    <input type="text" id="publicChatInput" placeholder="Введите сообщение в общий чат...">
                    <button id="sendPublicMsgBtn">Отправить</button>
                </div>
            </div>
        </div>

        <!-- Канал -->
        <div id="channelScreen" class="content-screen hidden">
            <div class="new-post hidden" id="channelAdminBox">
                <h4 style="margin-top:0; color: var(--header-bg);">Панель администратора канала</h4>
                <textarea id="channelPostText" placeholder="Написать пост в канал..."></textarea>
                <button id="sendChannelPost">Опубликовать в канал</button>
            </div>
            <div class="feed" id="channelContainer"></div>
        </div>

        <!-- Настройки -->
        <div id="settingsScreen" class="content-screen hidden">
            <div class="settings-container">
                <h3 id="settingsHeading">Настройки</h3>
                
                <div class="settings-item">
                    <label id="langLabel">Язык / Language</label>
                    <select id="langSelect">
                        <option value="ru">Русский</option>
                        <option value="en">English</option>
                    </select>
                </div>

                <div class="settings-item">
                    <label id="themeLabel">Тема оформления</label>
                    <select id="themeSelect">
                        <option value="light">Светлая</option>
                        <option value="dark">Тёмная</option>
                    </select>
                </div>
            </div>
        </div>
    </div>

    <script>
        const ADMIN_USERNAME = "@admin"; 

        const loginScreen = document.getElementById('loginScreen');
        const feedScreen = document.getElementById('feedScreen');
        const profileScreen = document.getElementById('profileScreen');
        const friendsScreen = document.getElementById('friendsScreen');
        const publicChatScreen = document.getElementById('publicChatScreen');
        const channelScreen = document.getElementById('channelScreen');
        const settingsScreen = document.getElementById('settingsScreen');
        const navTabs = document.getElementById('navTabs');
        
        const loginForm = document.getElementById('loginForm');
        const loginInput = document.getElementById('loginInput');
        const passwordInput = document.getElementById('passwordInput');
        const logoutBtn = document.getElementById('logoutBtn');
        const themeSelect = document.getElementById('themeSelect');
        const langSelect = document.getElementById('langSelect');

        const texts = {
            ru: {
                title: "Одноклассники",
                logout: "Выйти",
                tabFeed: "Лента",
                tabProfile: "Профиль",
                tabFriends: "Друзья",
                tabPublicChat: "Общий чат",
                tabChannel: "Канал",
                tabSettings: "Настройки",
                loginLabel: "логин, адрес почты или телефон",
                passLabel: "пароль",
                btnLogin: "Войти",
                editProfileTitle: "Редактировать профиль",
                labelUname: "Ваш юзернейм (ЮЗ):",
                labelName: "Ваше имя:",
                labelStatus: "Ваш статус:",
                labelAvatar: "Ссылка на аватар (фото):",
                saveProfile: "Сохранить",
                myPostsHeader: "Мои записи:",
                searchFriendTitle: "Найти друга по ЮЗ",
                addFriendBtn: "Добавить",
                friendsListTitle: "Список друзей",
                publicChatPlaceholder: "Введите сообщение в общий чат...",
                sendMsgBtn: "Отправить",
                settingsHeading: "Настройки",
                langLabel: "Язык / Language",
                themeLabel: "Тема оформления",
                light: "Светлая",
                dark: "Тёмная",
                placeholderPost: "О чём вы думаете?",
                publishBtn: "Опубликовать"
            },
            en: {
                title: "Odnoklassniki",
                logout: "Log out",
                tabFeed: "Feed",
                tabProfile: "Profile",
                tabFriends: "Friends",
                tabPublicChat: "Public Chat",
                tabChannel: "Channel",
                tabSettings: "Settings",
                loginLabel: "login, email or phone",
                passLabel: "password",
                btnLogin: "Sign In",
                editProfileTitle: "Edit Profile",
                labelUname: "Your username (ЮЗ):",
                labelName: "Your name:",
                labelStatus: "Your status:",
                labelAvatar: "Avatar image URL:",
                saveProfile: "Save",
                myPostsHeader: "My posts:",
                searchFriendTitle: "Find friend by username",
                addFriendBtn: "Add",
                friendsListTitle: "Friends list",
                publicChatPlaceholder: "Type a message in public chat...",
                sendMsgBtn: "Send",
                settingsHeading: "Settings",
                langLabel: "Language",
                themeLabel: "Theme",
                light: "Light",
                dark: "Dark",
                placeholderPost: "What's on your mind?",
                publishBtn: "Publish"
            }
        };

        function applyLanguage(lang) {
            const t = texts[lang];
            document.getElementById('headerTitle').textContent = t.title;
            logoutBtn.textContent = t.logout;
            document.getElementById('tabFeed').textContent = t.tabFeed;
            document.getElementById('tabProfile').textContent = t.tabProfile;
            document.getElementById('tabFriends').textContent = t.tabFriends;
            document.getElementById('tabPublicChat').textContent = t.tabPublicChat;
            document.getElementById('tabChannel').textContent = t.tabChannel;
            document.getElementById('tabSettings').textContent = t.tabSettings;
            
            document.getElementById('labelLogin').textContent = t.loginLabel;
            document.getElementById('labelPass').textContent = t.passLabel;
            document.getElementById('btnLogin').textContent = t.btnLogin;

            document.getElementById('editProfileTitle').textContent = t.editProfileTitle;
            document.getElementById('labelUname').textContent = t.labelUname;
            document.getElementById('labelName').textContent = t.labelName;
            document.getElementById('labelStatus').textContent = t.labelStatus;
            document.getElementById('labelAvatar').textContent = t.labelAvatar;
            document.getElementById('saveProfile').textContent = t.saveProfile;
            document.getElementById('myPostsHeader').textContent = t.myPostsHeader;

            document.getElementById('searchFriendTitle').textContent = t.searchFriendTitle;
            document.getElementById('addFriendBtn').textContent = t.addFriendBtn;
            document.getElementById('friendsListTitle').textContent = t.friendsListTitle;
            document.getElementById('publicChatInput').placeholder = t.publicChatPlaceholder;
            document.getElementById('sendPublicMsgBtn').textContent = t.sendMsgBtn;

            document.getElementById('settingsHeading').textContent = t.settingsHeading;
            document.getElementById('langLabel').textContent = t.langLabel;
            document.getElementById('themeLabel').textContent = t.themeLabel;
            
            document.getElementById('postText').placeholder = t.placeholderPost;
            document.getElementById('sendPost').textContent = t.publishBtn;

            themeSelect.options[0].text = t.light;
            themeSelect.options[1].text = t.dark;
        }

        document.querySelectorAll('.nav-tab').forEach(tab => {
            tab.addEventListener('click', () => {
                document.querySelectorAll('.nav-tab').forEach(t => t.classList.remove('active'));
                tab.classList.add('active');
                [feedScreen, profileScreen, friendsScreen, publicChatScreen, channelScreen, settingsScreen].forEach(s => s.classList.add('hidden'));
                
                const target = tab.getAttribute('data-target');
                document.getElementById(target).classList.remove('hidden');

                if(target === 'feedScreen') renderFeed();
                if(target === 'profileScreen') renderMyPosts();
                if(target === 'friendsScreen') renderFriends();
                if(target === 'publicChatScreen') renderPublicMessages();
                if(target === 'channelScreen') {
                    renderChannel();
                    checkChannelAdmin();
                }
            });
        });

        function getCurrentUserUname() {
            const login = localStorage.getItem('ok_login') || 'user';
            return localStorage.getItem('ok_username') || ('@' + login);
        }

        function loadUserData() {
            const login = localStorage.getItem('ok_login') || 'Гость';
            const name = localStorage.getItem('ok_name') || login;
            const username = getCurrentUserUname();
            const status = localStorage.getItem('ok_status') || 'Привет!';
            const avatar = localStorage.getItem('ok_avatar') || '';

            document.getElementById('profileDisplayName').textContent = name;
            document.getElementById('profileDisplayUsername').textContent = username;
            document.getElementById('profileDisplayStatus').textContent = status;
            
            document.getElementById('inputName').value = name;
            document.getElementById('inputUsername').value = username;
            document.getElementById('inputStatus').value = status;
            document.getElementById('inputAvatar').value = avatar;

            if(avatar) {
                document.getElementById('avatarBox').innerHTML = `<img src="${avatar}">`;
            } else {
                document.getElementById('avatarBox').innerHTML = `<span style="font-size: 12px;">Нет фото</span>`;
            }
        }

        document.getElementById('saveProfile').addEventListener('click', () => {
            let uname = document.getElementById('inputUsername').value.trim();
            if(uname && !uname.startsWith('@')) uname = '@' + uname;

            localStorage.setItem('ok_name', document.getElementById('inputName').value);
            localStorage.setItem('ok_username', uname);
            localStorage.setItem('ok_status', document.getElementById('inputStatus').value);
            localStorage.setItem('ok_avatar', document.getElementById('inputAvatar').value);
            loadUserData();
            alert('Профиль сохранен!');
        });

        // Лента
        function getPosts() {
            const userUname = getCurrentUserUname();
            return JSON.parse(localStorage.getItem(`ok_posts_${userUname}`) || '[]');
        }

        function renderFeed() {
            const container = document.getElementById('feedContainer');
            container.innerHTML = '';
            getPosts().forEach(p => {
                container.innerHTML += `<div class="post"><div class="post-author">${p.author}</div><div class="post-text">${p.text}</div></div>`;
            });
        }

        function renderMyPosts() {
            const container = document.getElementById('myPostsContainer');
            container.innerHTML = '';
            getPosts().forEach(p => {
                container.innerHTML += `<div class="post"><div class="post-text">${p.text}</div></div>`;
            });
        }

        document.getElementById('sendPost').addEventListener('click', () => {
            const text = document.getElementById('postText').value.trim();
            if(!text) return;
            const userUname = getCurrentUserUname();
            const posts = getPosts();
            posts.unshift({ author: localStorage.getItem('ok_name') || 'Гость', text: text });
            localStorage.setItem(`ok_posts_${userUname}`, JSON.stringify(posts));
            document.getElementById('postText').value = '';
            renderFeed();
        });

        // Канал
        function getChannelPosts() {
            return JSON.parse(localStorage.getItem('ok_channel_posts') || '[]');
        }

        function renderChannel() {
            const container = document.getElementById('channelContainer');
            container.innerHTML = '';
            const posts = getChannelPosts();
            if(posts.length === 0) {
                container.innerHTML = '<p style="color:gray; font-size:13px; padding: 15px;">В канале пока нет записей.</p>';
                return;
            }
            posts.forEach(p => {
                container.innerHTML += `<div class="post"><div class="post-author">📢 ${p.author}</div><div class="post-text">${p.text}</div></div>`;
            });
        }

        function checkChannelAdmin() {
            const adminBox = document.getElementById('channelAdminBox');
            const userUname = getCurrentUserUname();
            const isFirstUser = !localStorage.getItem('ok_admin_set');
            if(isFirstUser) {
                localStorage.setItem('ok_admin_set', userUname);
            }
            const currentAdmin = localStorage.getItem('ok_admin_set') || ADMIN_USERNAME;

            if(userUname === currentAdmin) {
                adminBox.classList.remove('hidden');
            } else {
                adminBox.classList.add('hidden');
            }
        }

        document.getElementById('sendChannelPost').addEventListener('click', () => {
            const text = document.getElementById('channelPostText').value.trim();
            if(!text) return;
            const posts = getChannelPosts();
            posts.unshift({ author: localStorage.getItem('ok_name') || 'Администратор', text: text });
            localStorage.setItem('ok_channel_posts', JSON.stringify(posts));
            document.getElementById('channelPostText').value = '';
            renderChannel();
        });

        // Друзья (ЛС заблокированы)
        function getFriends() {
            const userUname = getCurrentUserUname();
            return JSON.parse(localStorage.getItem(`ok_friends_${userUname}`) || '[]');
        }

        function renderFriends() {
            const container = document.getElementById('friendsContainer');
            container.innerHTML = '';
            const friends = getFriends();
            if(friends.length === 0) {
                container.innerHTML = '<p style="color:gray; font-size:13px;">Список друзей пуст.</p>';
                return;
            }
            friends.forEach(friend => {
                container.innerHTML += `
                    <div class="friend-item">
                        <span>👤 ${friend}</span>
                        <button class="btn-submit" onclick="blockChat()">Написать</button>
                    </div>`;
            });
        }

        window.blockChat = function() {
            alert('Эта функция недоступна в ваш регион');
        }

        document.getElementById('addFriendBtn').addEventListener('click', () => {
            let uname = document.getElementById('searchFriendInput').value.trim();
            if(!uname) return;
            if(!uname.startsWith('@')) uname = '@' + uname;

            const userUname = getCurrentUserUname();
            if(uname === userUname) {
                alert('Нельзя добавить самого себя!');
                return;
            }

            const friends = getFriends();
            if(!friends.includes(uname)) {
                friends.push(uname);
                localStorage.setItem(`ok_friends_${userUname}`, JSON.stringify(friends));
                document.getElementById('searchFriendInput').value = '';
                renderFriends();
            } else {
                alert('Этот пользователь уже в списке друзей!');
            }
        });

        // Общий чат для всех (с общим глобальным хранилищем)
        function renderPublicMessages() {
            const container = document.getElementById('publicChatMessages');
            container.innerHTML = '';
            const currentUser = getCurrentUserUname();
            const msgs = JSON.parse(localStorage.getItem('ok_public_chat') || '[]');
            
            if(msgs.length === 0) {
                container.innerHTML = '<p style="color:gray; font-size:13px; text-align:center; margin-top:20px;">В общем чате пока нет сообщений. Напишите первыми!</p>';
                return;
            }

            msgs.forEach(m => {
                const isMyMessage = (m.senderUname === currentUser);
                container.innerHTML += `
                    <div class="message ${isMyMessage ? 'my' : 'other'}">
                        <div style="font-size: 10px; opacity: 0.8; margin-bottom: 2px; font-weight: bold;">${m.senderName} (${m.senderUname})</div>
                        <div>${m.text}</div>
                    </div>`;
            });
            container.scrollTop = container.scrollHeight;
        }

        document.getElementById('sendPublicMsgBtn').addEventListener('click', () => {
            const input = document.getElementById('publicChatInput');
            const text = input.value.trim();
            if(!text) return;
            
            const currentUser = getCurrentUserUname();
            const currentName = localStorage.getItem('ok_name') || 'Гость';
            const msgs = JSON.parse(localStorage.getItem('ok_public_chat') || '[]');
            
            msgs.push({ senderName: currentName, senderUname: currentUser, text: text });
            localStorage.setItem('ok_public_chat', JSON.stringify(msgs));
            
            input.value = '';
            renderPublicMessages();
        });

        loginForm.addEventListener('submit', (e) => {
            e.preventDefault();
            const loginVal = loginInput.value.trim();
            if(!loginVal) return;
            localStorage.setItem('ok_login', loginVal);
            if(!localStorage.getItem('ok_name')) localStorage.setItem('ok_name', loginVal);
            if(!localStorage.getItem('ok_username')) localStorage.setItem('ok_username', '@' + loginVal);
            showApp();
        });

        function showApp() {
            loginScreen.classList.add('hidden');
            navTabs.classList.remove('hidden');
            feedScreen.classList.remove('hidden');
            logoutBtn.classList.remove('hidden');
            loadUserData();
            renderFeed();
        }

        window.addEventListener('DOMContentLoaded', () => {
            if(localStorage.getItem('ok_login')) {
                loginInput.value = localStorage.getItem('ok_login');
                showApp();
            }
            const theme = localStorage.getItem('ok_theme') || 'light';
            const lang = localStorage.getItem('ok_lang') || 'ru';
            
            themeSelect.value = theme;
            langSelect.value = lang;
            applyLanguage(lang);

            if(theme === 'dark') document.documentElement.setAttribute('data-theme', 'dark');
        });

        logoutBtn.addEventListener('click', () => {
            localStorage.removeItem('ok_login');
            location.reload();
        });

        themeSelect.addEventListener('change', (e) => {
            localStorage.setItem('ok_theme', e.target.value);
            if(e.target.value === 'dark') document.documentElement.setAttribute('data-theme', 'dark');
            else document.documentElement.removeAttribute('data-theme');
        });

        langSelect.addEventListener('change', (e) => {
            const lang = e.target.value;
            localStorage.setItem('ok_lang', lang);
            applyLanguage(lang);
        });
    </script>
</body>
</html>
