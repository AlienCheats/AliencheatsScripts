
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Script Search</title>
    <style>
        :root {
            --primary-color: #6366f1;
            --secondary-color: #10b981;
            --accent-color: #f43f5e;
            --text-color: #1f2937;
            --modal-bg: rgba(255, 255, 255, 0.95);
            --gradient-start: #2563eb;
            --gradient-end: #7c3aed;
        }

        body {
            background: linear-gradient(135deg, var(--gradient-start), var(--gradient-end));
            background-attachment: fixed;
            height: 100vh;
            margin: 0;
            display: flex;
            flex-direction: column;
            align-items: center;
            padding: 40px 20px;
            position: relative;
            font-family: 'Inter', 'Segoe UI', sans-serif;
            color: var(--text-color);
        }

        .username-display {
            background: rgba(255, 255, 255, 0.95);
            border-radius: 20px;
            padding: 15px 30px;
            margin-bottom: 30px;
            box-shadow: 0 8px 25px rgba(0, 0, 0, 0.15);
            backdrop-filter: blur(10px);
            border: 1px solid rgba(255, 255, 255, 0.3);
            font-weight: 600;
            color: var(--gradient-start);
            letter-spacing: 0.5px;
        }

        .rounded-rectangle {
            background: rgba(255, 255, 255, 0.95);
            border-radius: 30px;
            width: 400px;
            height: 60px;
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.2);
            display: flex;
            justify-content: center;
            align-items: center;
            margin: 20px auto;
            border: 1px solid rgba(255, 255, 255, 0.3);
            backdrop-filter: blur(10px);
            transition: all 0.4s ease;
        }

        .rounded-rectangle:hover {
            transform: translateY(-3px);
            box-shadow: 0 15px 35px rgba(0, 0, 0, 0.25);
        }

        input {
            border: none;
            background: transparent;
            outline: none;
            width: 90%;
            font-size: 16px;
            padding: 15px 25px;
            color: var(--text-color);
        }

        input::placeholder {
            color: #6b7280;
        }

        .button-container {
            display: flex;
            gap: 15px;
            margin-top: 20px;
            flex-wrap: wrap;
            justify-content: center;
        }

        .login-button, .create-account-button, .upload-scripts-button, .logout-button {
            background: rgba(255, 255, 255, 0.95);
            border: none;
            border-radius: 25px;
            padding: 12px 30px;
            font-size: 15px;
            font-weight: 600;
            cursor: pointer;
            box-shadow: 0 8px 20px rgba(0, 0, 0, 0.15);
            color: var(--gradient-start);
            transition: all 0.3s ease;
            backdrop-filter: blur(10px);
        }

        .login-button:hover, .create-account-button:hover, 
        .upload-scripts-button:hover, .logout-button:hover {
            transform: translateY(-3px);
            box-shadow: 0 12px 25px rgba(0, 0, 0, 0.2);
            background: white;
        }

        .results-container {
            background: rgba(255, 255, 255, 0.95);
            border-radius: 20px;
            padding: 20px;
            margin-top: 30px;
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.15);
            backdrop-filter: blur(10px);
            max-width: 500px;
            width: 100%;
            text-align: center;
        }

        .upload-container {
            background: rgba(255, 255, 255, 0.95);
            border-radius: 20px;
            padding: 30px;
            margin-top: 30px;
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.15);
            backdrop-filter: blur(10px);
            max-width: 500px;
            width: 100%;
            text-align: center;
            display: none;
        }

        .script-textarea {
            width: 100%;
            min-height: 200px;
            padding: 15px;
            border-radius: 15px;
            border: 1px solid rgba(255, 255, 255, 0.3);
            background: rgba(255, 255, 255, 0.95);
            margin-bottom: 20px;
            resize: vertical;
            font-family: monospace;
        }

        .script-select {
            width: 100%;
            padding: 12px;
            border-radius: 15px;
            border: 1px solid rgba(255, 255, 255, 0.3);
            background: rgba(255, 255, 255, 0.95);
            margin-bottom: 20px;
            cursor: pointer;
        }

        .script-card {
            background: rgba(255, 255, 255, 0.95);
            border-radius: 15px;
            padding: 20px;
            margin: 10px 0;
            cursor: pointer;
            transition: all 0.3s ease;
        }

        .script-card:hover {
            transform: translateY(-3px);
            box-shadow: 0 8px 20px rgba(0, 0, 0, 0.15);
        }

        .script-details {
            display: none;
            margin-top: 15px;
            padding-top: 15px;
            border-top: 1px solid rgba(0, 0, 0, 0.1);
        }

        .get-script-btn {
            background: linear-gradient(135deg, var(--gradient-start), var(--gradient-end));
            color: white;
            border: none;
            border-radius: 25px;
            padding: 8px 20px;
            font-size: 14px;
            cursor: pointer;
            margin-top: 10px;
        }

        .upload-button {
            background: linear-gradient(135deg, var(--gradient-start), var(--gradient-end));
            color: white;
            border: none;
            border-radius: 25px;
            padding: 12px 30px;
            font-size: 15px;
            font-weight: 600;
            cursor: pointer;
            transition: all 0.3s ease;
            margin-top: 20px;
        }

        .upload-button:hover {
            transform: translateY(-3px);
            box-shadow: 0 8px 20px rgba(0, 0, 0, 0.2);
        }

        .modal {
            position: fixed;
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
            background-color: rgba(0, 0, 0, 0.5);
            display: none;
            justify-content: center;
            align-items: center;
            z-index: 1000;
            backdrop-filter: blur(5px);
        }

        .modal-content {
            background: rgba(255, 255, 255, 0.98);
            border-radius: 25px;
            padding: 40px;
            box-shadow: 0 15px 40px rgba(0, 0, 0, 0.3);
            width: 90%;
            max-width: 400px;
            position: relative;
        }

        .close-button {
            position: absolute;
            top: 20px;
            right: 20px;
            font-size: 24px;
            cursor: pointer;
            color: #6b7280;
            transition: color 0.3s ease;
        }

        .close-button:hover {
            color: var(--accent-color);
        }

        .message {
            margin: 15px 0;
            font-weight: 500;
            color: var(--text-color);
        }
    </style>
</head>
<body>
    <div id="userDisplay" class="username-display" style="display: none;"></div>
    
    <div class="button-container">
        <button class="upload-scripts-button" id="uploadScriptsButton" style="display: none;">Upload Scripts</button>
        <button class="logout-button" id="logoutButton" style="display: none;">Log Out</button>
    </div>

    <div class="rounded-rectangle" id="searchContainer">
        <input type="text" id="searchInput" placeholder="Search scripts with keywords...">
    </div>

    <div class="upload-container" id="uploadContainer">
        <h2>Upload Your Script</h2>
        
        <div class="script-input-container">
            <textarea id="scriptText" placeholder="Paste your script here..." class="script-textarea"></textarea>
        </div>

        <div class="keyword-selector">
            <select id="scriptKeyword" class="script-select">
                <option value="">Select a keyword...</option>
                <option value="mm2">MM2</option>
                <option value="arsenal">Arsenal</option>
                <option value="blox">Blox Fruits</option>
                <option value="pet">Pet Simulator</option>
            </select>
        </div>

        <div class="rounded-rectangle">
            <input type="text" id="scriptName" placeholder="Script name...">
        </div>
        
        <div class="rounded-rectangle">
            <input type="text" id="scriptDescription" placeholder="Script description...">
        </div>
        
        <button class="upload-button">Upload Script</button>
    </div>

    <div class="results-container">
        <div class="message" id="resultMessage"></div>
        <div class="results" id="resultsMessage"></div>
    </div>

    <div class="button-container">
        <button class="login-button" id="loginButton">Login</button>
        <button class="create-account-button" id="createAccountButton">Create Account</button>
    </div>

    <!-- Login Modal -->
    <div id="loginModal" class="modal">
        <div class="modal-content">
            <span class="close-button" id="closeLoginModal">&times;</span>
            <h2>Login</h2>
            <input type="text" id="usernameInput" placeholder="Username">
            <input type="password" id="passwordInput" placeholder="Password">
            <button id="submitLogin" class="login-button">Login</button>
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
            <button id="submitCreateAccount" class="create-account-button">Create Account</button>
            <div class="message" id="accountErrorMessage"></div>
            <div class="message" id="accountSuccessMessage"></div>
        </div>
    </div>

    <script>
        const accounts = {};
        let loggedInUser = null;
        const scripts = JSON.parse(localStorage.getItem('scripts') || '[]');

        const userDisplay = document.getElementById('userDisplay');
        const loginModal = document.getElementById('loginModal');
        const createAccountModal = document.getElementById('createAccountModal');
        const loginButton = document.getElementById('loginButton');
        const logoutButton = document.getElementById('logoutButton');
        const createAccountButton = document.getElementById('createAccountButton');
        const uploadScriptsButton = document.getElementById('uploadScriptsButton');
        const searchContainer = document.getElementById('searchContainer');
        const uploadContainer = document.getElementById('uploadContainer');
        const resultsContainer = document.querySelector('.results-container');

        function saveAccounts() {
            localStorage.setItem('accounts', JSON.stringify(accounts));
        }

        function loadAccounts() {
            const savedAccounts = localStorage.getItem('accounts');
            if (savedAccounts) {
                Object.assign(accounts, JSON.parse(savedAccounts));
            }
        }

        function saveLoginState(username) {
            localStorage.setItem('loggedInUser', username);
        }

        function clearLoginState() {
            localStorage.removeItem('loggedInUser');
        }

        function checkLoginState() {
            const savedUser = localStorage.getItem('loggedInUser');
            if (savedUser && accounts[savedUser]) {
                loggedInUser = savedUser;
                updateUIForLoggedInUser();
            }
        }

        function updateUIForLoggedInUser() {
            userDisplay.textContent = `Welcome, ${loggedInUser}!`;
            userDisplay.style.display = 'block';
            loginButton.style.display = 'none';
            createAccountButton.style.display = 'none';
            uploadScriptsButton.style.display = 'inline-block';
            logoutButton.style.display = 'inline-block';
        }

        function logout() {
            loggedInUser = null;
            clearLoginState();
            userDisplay.style.display = 'none';
            loginButton.style.display = 'inline-block';
            createAccountButton.style.display = 'inline-block';
            uploadScriptsButton.style.display = 'none';
            logoutButton.style.display = 'none';
            uploadContainer.style.display = 'none';
            searchContainer.style.display = 'flex';
            resultsContainer.style.display = 'block';
        }

        loadAccounts();
        checkLoginState();

        loginButton.addEventListener('click', () => {
            loginModal.style.display = 'flex';
        });

        createAccountButton.addEventListener('click', () => {
            createAccountModal.style.display = 'flex';
        });

        logoutButton.addEventListener('click', logout);

        document.getElementById('closeLoginModal').addEventListener('click', () => {
            loginModal.style.display = 'none';
        });

        document.getElementById('closeCreateAccountModal').addEventListener('click', () => {
            createAccountModal.style.display = 'none';
        });

        document.getElementById('submitLogin').addEventListener('click', () => {
            const username = document.getElementById('usernameInput').value.trim();
            const password = document.getElementById('passwordInput').value.trim();

            if (accounts[username] && accounts[username] === password) {
                loggedInUser = username;
                saveLoginState(username);
                updateUIForLoggedInUser();
                loginModal.style.display = 'none';
                document.getElementById('usernameInput').value = '';
                document.getElementById('passwordInput').value = '';
                loginErrorMessage.textContent = '';
            } else {
                loginErrorMessage.textContent = 'Username or password is incorrect.';
            }
        });

        document.getElementById('submitCreateAccount').addEventListener('click', () => {
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
            uploadContainer.style.display = 'block';
            searchContainer.style.display = 'none';
            resultsContainer.style.display = 'none';
        });

        document.querySelector('.upload-button').addEventListener('click', function() {
            const scriptText = document.getElementById('scriptText').value;
            const keyword = document.getElementById('scriptKeyword').value;
            const name = document.getElementById('scriptName').value;
            const description = document.getElementById('scriptDescription').value;

            if (!scriptText || !keyword || !name || !description) {
                alert('Please fill in all fields');
                return;
            }

            scripts.push({
                text: scriptText,
                keyword: keyword,
                name: name,
                description: description
            });

            localStorage.setItem('scripts', JSON.stringify(scripts));
            
            alert('Script uploaded successfully!');
            uploadContainer.style.display = 'none';
            searchContainer.style.display = 'flex';
            resultsContainer.style.display = 'block';
            
            // Clear inputs
            document.getElementById('scriptText').value = '';
            document.getElementById('scriptKeyword').value = '';
            document.getElementById('scriptName').value = '';
            document.getElementById('scriptDescription').value = '';
        });

        document.getElementById('searchInput').addEventListener('keypress', function(event) {
            if (event.key === 'Enter') {
                const keyword = this.value.trim().toLowerCase();
                const matchingScripts = scripts.filter(script => 
                    script.keyword.toLowerCase() === keyword
                );

                const resultsContainer = document.getElementById('resultsMessage');
                resultsContainer.innerHTML = '';

                if (matchingScripts.length > 0) {
                    matchingScripts.forEach(script => {
                        const scriptCard = document.createElement('div');
                        scriptCard.className = 'script-card';
                        scriptCard.innerHTML = `
                            <h3>${script.name}</h3>
                            <div class="script-details">
                                <p>${script.description}</p>
                                <button class="get-script-btn" onclick="copyScript('${script.text}')">Get Script</button>
                            </div>
                        `;
                        
                        scriptCard.addEventListener('click', function() {
                            const details = this.querySelector('.script-details');
                            details.style.display = details.style.display === 'none' ? 'block' : 'none';
                        });

                        resultsContainer.appendChild(scriptCard);
                    });
                } else {
                    resultsContainer.innerHTML = 'No scripts found for this keyword';
                }
                
                this.value = '';
            }
        });

        function copyScript(text) {
            navigator.clipboard.writeText(text);
            alert('Script copied to clipboard!');
        }
    </script>
</body>
</html>
