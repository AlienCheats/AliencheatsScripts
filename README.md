
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Background Image</title>
    <style>
        :root {
            --primary-color: #4a90e2;
            --secondary-color: #2ecc71;
            --accent-color: #e74c3c;
            --text-color: #2c3e50;
            --modal-bg: rgba(255, 255, 255, 0.95);
        }

        body {
            background-image: url('https://raw.githubusercontent.com/AlienCheats/AliencheatsScripts/refs/heads/main/wood-grain-texture-close-up-0410-5698738.webp');
            background-size: cover;
            background-position: center;
            background-repeat: no-repeat;
            height: 100vh;
            margin: 0;
            display: flex;
            flex-direction: column;
            align-items: flex-start;
            padding: 20px;
            position: relative;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            color: var(--text-color);
        }

        .username-display {
            background: linear-gradient(145deg, var(--modal-bg), rgba(255, 255, 255, 0.8));
            border-radius: 15px;
            padding: 12px 20px;
            margin-bottom: 20px;
            box-shadow: 0 4px 15px rgba(0, 0, 0, 0.1);
            backdrop-filter: blur(5px);
            border: 1px solid rgba(255, 255, 255, 0.2);
            font-weight: 600;
            color: var(--primary-color);
        }

        .rounded-rectangle {
            background: linear-gradient(145deg, var(--modal-bg), rgba(255, 255, 255, 0.8));
            border-radius: 25px;
            width: 350px;
            height: 55px;
            box-shadow: 0 8px 20px rgba(0, 0, 0, 0.15);
            display: flex;
            justify-content: center;
            align-items: center;
            margin: 0 auto;
            border: 1px solid rgba(255, 255, 255, 0.2);
            backdrop-filter: blur(5px);
            transition: transform 0.3s ease, box-shadow 0.3s ease;
        }

        .rounded-rectangle:hover {
            transform: translateY(-2px);
            box-shadow: 0 10px 25px rgba(0, 0, 0, 0.2);
        }

        input {
            border: none;
            background: transparent;
            outline: none;
            width: 90%;
            font-size: 16px;
            padding: 15px;
            color: var(--text-color);
        }

        input::placeholder {
            color: #95a5a6;
        }

        .message {
            color: var(--accent-color);
            text-align: center;
            margin-top: 20px;
            font-weight: 500;
            animation: fadeIn 0.3s ease;
        }

        .results {
            color: var(--secondary-color);
            text-align: center;
            margin-top: 15px;
            font-weight: 500;
            animation: fadeIn 0.3s ease;
        }

        img {
            margin-top: 20px;
            max-width: 300px;
            border-radius: 15px;
            display: none;
            box-shadow: 0 8px 20px rgba(0, 0, 0, 0.2);
            transition: transform 0.3s ease;
        }

        img:hover {
            transform: scale(1.02);
        }

        .label {
            background: linear-gradient(145deg, var(--modal-bg), rgba(255, 255, 255, 0.8));
            border-radius: 12px;
            text-align: center;
            margin-top: 15px;
            padding: 12px 20px;
            display: none;
            font-weight: 600;
            box-shadow: 0 4px 15px rgba(0, 0, 0, 0.1);
            animation: fadeIn 0.3s ease;
        }

        .login-button, .create-account-button, .upload-scripts-button {
            background: linear-gradient(145deg, var(--primary-color), #357abd);
            border: none;
            border-radius: 25px;
            padding: 12px 25px;
            font-size: 14px;
            font-weight: 600;
            cursor: pointer;
            box-shadow: 0 4px 15px rgba(74, 144, 226, 0.3);
            margin: 8px;
            display: inline-block;
            color: white;
            transition: all 0.3s ease;
        }

        .create-account-button {
            background: linear-gradient(145deg, var(--secondary-color), #27ae60);
            box-shadow: 0 4px 15px rgba(46, 204, 113, 0.3);
        }

        .upload-scripts-button {
            background: linear-gradient(145deg, #9b59b6, #8e44ad);
            box-shadow: 0 4px 15px rgba(155, 89, 182, 0.3);
        }

        .login-button:hover, .create-account-button:hover, .upload-scripts-button:hover {
            transform: translateY(-2px);
            box-shadow: 0 6px 20px rgba(0, 0, 0, 0.2);
            filter: brightness(1.1);
        }

        .modal {
            position: fixed;
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
            background-color: rgba(0, 0, 0, 0.7);
            display: none;
            justify-content: center;
            align-items: center;
            z-index: 1000;
            backdrop-filter: blur(5px);
        }

        .modal-content {
            background: linear-gradient(145deg, var(--modal-bg), rgba(255, 255, 255, 0.9));
            border-radius: 20px;
            padding: 30px;
            text-align: center;
            position: relative;
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.2);
            max-width: 400px;
            width: 90%;
        }

        .close-button {
            position: absolute;
            top: 15px;
            right: 15px;
            cursor: pointer;
            font-size: 24px;
            color: #95a5a6;
            transition: color 0.3s ease;
        }

        .close-button:hover {
            color: var(--accent-color);
        }

        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(-10px); }
            to { opacity: 1; transform: translateY(0); }
        }

        .modal-content input {
            width: 100%;
            margin: 10px 0;
            padding: 12px;
            border: 1px solid rgba(0, 0, 0, 0.1);
            border-radius: 12px;
            background: rgba(255, 255, 255, 0.9);
            transition: all 0.3s ease;
        }

        .modal-content input:focus {
            border-color: var(--primary-color);
            box-shadow: 0 0 0 2px rgba(74, 144, 226, 0.2);
        }

        .modal-content button {
            margin-top: 15px;
            width: 100%;
        }

        .modal-content h2 {
            color: var(--text-color);
            margin-bottom: 20px;
            font-weight: 600;
        }
    </style>
</head>
<body>
    <div id="userDisplay" class="username-display" style="display: none;"></div>
    <button class="upload-scripts-button" id="uploadScriptsButton" style="display: none;">Upload Scripts</button>
    <div class="rounded-rectangle">
        <input type="text" id="searchInput" placeholder="Search scripts with keywords...">
    </div>
    <div class="message" id="resultMessage"></div>
    <div class="results" id="resultsMessage"></div>
    <img id="resultImage" src="https://raw.githubusercontent.com/AlienCheats/-AlienCheats-Scripts/refs/heads/main/t%C3%A9l%C3%A9chargement%20(1).jpg" alt="MM2 Result Image">
    <div class="label" id="resultLabel">Yarhm</div>

    <button class="login-button" id="loginButton">Login</button>
    <button class="create-account-button" id="createAccountButton">Create Account</button>

    <!-- Login Modal -->
    <div id="loginModal" class="modal">
        <div class="modal-content">
            <span class="close-button" id="closeLoginModal">&times;</span>
            <h2>Login</h2>
            <input type="text" id="usernameInput" placeholder="Username">
            <input type="password" id="passwordInput" placeholder="Password">
            <button id="submitLogin">Login</button>
            <div class="message" id="loginErrorMessage"></div>
        </div>
    </div>

    <!-- Create Account Modal -->
    <div id="createAccountModal" class="modal">
        <div class="modal-content">
            <span class="close-button" id="closeCreateAccountModal">&times;</span>
            <h2>Create Account</h2>
            <input type="text" id="newUsernameInput" placeholder="New Username">
            <input type="password" id="newPasswordInput" placeholder="New Password">
            <button id="submitCreateAccount">Create Account</button>
            <div class="message" id="accountErrorMessage"></div>
            <div class="message" id="accountSuccessMessage"></div>
        </div>
    </div>

    <script>
        const accounts = {};
        let loggedInUser = null;

        const userDisplay = document.getElementById('userDisplay');
        const loginModal = document.getElementById('loginModal');
        const createAccountModal = document.getElementById('createAccountModal');
        const loginButton = document.getElementById('loginButton');
        const createAccountButton = document.getElementById('createAccountButton');
        const submitLogin = document.getElementById('submitLogin');
        const submitCreateAccount = document.getElementById('submitCreateAccount');
        const loginErrorMessage = document.getElementById('loginErrorMessage');
        const accountErrorMessage = document.getElementById('accountErrorMessage');
        const accountSuccessMessage = document.getElementById('accountSuccessMessage');
        const uploadScriptsButton = document.getElementById('uploadScriptsButton');

        function saveAccounts() {
            localStorage.setItem('accounts', JSON.stringify(accounts));
        }

        function loadAccounts() {
            const savedAccounts = localStorage.getItem('accounts');
            if (savedAccounts) {
                Object.assign(accounts, JSON.parse(savedAccounts));
            }
        }

        loadAccounts();

        loginButton.addEventListener('click', () => {
            loginModal.style.display = 'flex';
        });

        createAccountButton.addEventListener('click', () => {
            createAccountModal.style.display = 'flex';
        });

        document.getElementById('closeLoginModal').addEventListener('click', () => {
            loginModal.style.display = 'none';
        });
        document.getElementById('closeCreateAccountModal').addEventListener('click', () => {
            createAccountModal.style.display = 'none';
        });

        submitLogin.addEventListener('click', () => {
            const username = document.getElementById('usernameInput').value.trim();
            const password = document.getElementById('passwordInput').value.trim();

            if (accounts[username] && accounts[username] === password) {
                loggedInUser = username;
                userDisplay.textContent = `Welcome, ${loggedInUser}!`;
                userDisplay.style.display = 'block';
                loginModal.style.display = 'none';
                createAccountButton.style.display = 'none';
                loginButton.style.display = 'none';
                uploadScriptsButton.style.display = 'inline-block';
            } else {
                loginErrorMessage.textContent = 'Username or password is incorrect.';
            }
        });

        submitCreateAccount.addEventListener('click', () => {
            const newUsername = document.getElementById('newUsernameInput').value.trim();
            const newPassword = document.getElementById('newPasswordInput').value.trim();

            if (accounts[newUsername]) {
                accountErrorMessage.textContent = 'Username already taken.';
                accountSuccessMessage.textContent = '';
            } else {
                accounts[newUsername] = newPassword;
                saveAccounts();
                accountSuccessMessage.textContent = 'Account created successfully!';
                accountErrorMessage.textContent = '';
                document.getElementById('newUsernameInput').value = '';
                document.getElementById('newPasswordInput').value = '';
            }
        });

        uploadScriptsButton.addEventListener('click', () => {
            alert('Upload Scripts feature coming soon!');
        });

        document.getElementById('searchInput').addEventListener('keypress', function(event) {
            if (event.key === 'Enter') {
                const keyword = this.value.trim().toLowerCase();
                if (keyword === 'mm2') {
                    document.getElementById('resultMessage').textContent = '';
                    document.getElementById('resultsMessage').textContent = `Results for "${keyword}"`;
                    document.getElementById('resultImage').style.display = 'block';
                    document.getElementById('resultLabel').style.display = 'block';
                } else if (keyword === 'fisch') {
                    document.getElementById('resultMessage').textContent = '';
                    document.getElementById('resultsMessage').textContent = `Results for "${keyword}"`;
                    document.getElementById('resultImage').style.display = 'none';
                    document.getElementById('resultLabel').style.display = 'none';
                } else {
                    document.getElementById('resultMessage').textContent = 'Nothing found here';
                    document.getElementById('resultsMessage').textContent = '';
                    document.getElementById('resultImage').style.display = 'none';
                    document.getElementById('resultLabel').style.display = 'none';
                }
                this.value = '';
            }
        });
    </script>
</body>
</html>
