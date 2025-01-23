
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Background Image</title>
    <style>
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
        }

        .username-display {
            background-color: rgba(255, 255, 255, 0.8);
            border-radius: 15px;
            padding: 10px;
            margin-bottom: 20px;
        }

        .rounded-rectangle {
            background-color: rgba(255, 255, 255, 0.8);
            border-radius: 15px;
            width: 300px;
            height: 50px;
            box-shadow: 0 4px 10px rgba(0, 0, 0, 0.5);
            display: flex;
            justify-content: center;
            align-items: center;
            margin: 0 auto;
        }

        input {
            border: none;
            background: transparent;
            outline: none;
            width: 90%;
            font-size: 16px;
            padding: 10px;
        }

        .message {
            color: red;
            text-align: center;
            margin-top: 20px;
        }

        .results {
            color: green;
            text-align: center;
            margin-top: 10px;
        }

        img {
            margin-top: 20px;
            max-width: 300px;
            border-radius: 15px;
            display: none;
        }

        .label {
            background-color: rgba(255, 255, 255, 0.8);
            border-radius: 10px;
            text-align: center;
            margin-top: 10px;
            padding: 10px;
            display: none;
        }

        .login-button, .create-account-button {
            background-color: rgba(255, 255, 255, 0.8);
            border: none;
            border-radius: 15px;
            padding: 10px 20px;
            font-size: 14px;
            font-weight: bold;
            cursor: pointer;
            box-shadow: 0 4px 10px rgba(0, 0, 0, 0.3);
            margin: 5px;
            display: inline-block;
        }

        .modal {
            position: fixed;
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
            background-color: rgba(0, 0, 0, 0.8);
            display: none;
            justify-content: center;
            align-items: center;
            z-index: 1000;
        }

        .modal-content {
            background-color: white;
            border-radius: 15px;
            padding: 20px;
            text-align: center;
            position: relative;
        }

        .close-button {
            position: absolute;
            top: 10px;
            right: 10px;
            cursor: pointer;
        }
    </style>
</head>
<body>
    <div id="userDisplay" class="username-display" style="display: none;"></div>
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

        // Functions to save and load accounts
        function saveAccounts() {
            localStorage.setItem('accounts', JSON.stringify(accounts));
        }

        function loadAccounts() {
            const savedAccounts = localStorage.getItem('accounts');
            if (savedAccounts) {
                Object.assign(accounts, JSON.parse(savedAccounts));
            }
        }

        // Initialize accounts on page load
        loadAccounts();

        // Handle login button click
        loginButton.addEventListener('click', () => {
            loginModal.style.display = 'flex';
        });

        // Handle create account button click
        createAccountButton.addEventListener('click', () => {
            createAccountModal.style.display = 'flex';
        });

        // Handle closing modals
        document.getElementById('closeLoginModal').addEventListener('click', () => {
            loginModal.style.display = 'none';
        });
        document.getElementById('closeCreateAccountModal').addEventListener('click', () => {
            createAccountModal.style.display = 'none';
        });

        // Handle login submission
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
            } else {
                loginErrorMessage.textContent = 'Username or password is incorrect.';
            }
        });

        // Handle account creation
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

        // Event listener for search input
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
