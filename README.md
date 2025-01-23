
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
            justify-content: center;
            align-items: flex-start;
            padding-top: 50px;
            flex-direction: column;
            position: relative; /* Relative positioning for the buttons */
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
            margin: 5px; /* Add some margin between buttons */
        }

        .modal {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background-color: rgba(0, 0, 0, 0.7);
            display: none; /* Hide modal by default */
            justify-content: center;
            align-items: center;
            z-index: 1000; /* Ensure modal is on top */
        }

        .modal-content {
            background-color: black;
            border-radius: 15px;
            padding: 30px;
            width: 300px;
            box-shadow: 0 4px 10px rgba(255, 255, 255, 0.3);
        }

        .modal-content input {
            width: 100%;
            margin-bottom: 15px;
            padding: 10px;
            border: none;
            border-radius: 10px;
            background-color: #ddd;
        }

        .modal-content button {
            width: 100%;
            padding: 10px;
            background-color: #444;
            color: white;
            font-weight: bold;
            border: none;
            border-radius: 10px;
            cursor: pointer;
        }

        .error-message, .success-message {
            text-align: center;
            margin-top: 10px;
        }

        .error-message {
            color: red;
        }

        .success-message {
            color: green;
        }

        .user-display {
            background-color: rgba(255, 255, 255, 0.8);
            border-radius: 15px;
            width: 300px;
            height: 50px;
            display: flex;
            justify-content: center;
            align-items: center;
            margin: 0 auto;
            font-weight: bold;
        }
    </style>
</head>
<body>
    <div id="userDisplay" class="user-display" style="display: none;"></div>

    <div class="rounded-rectangle" id="searchContainer">
        <input type="text" id="searchInput" placeholder="Search scripts with keywords...">
    </div>
    <div class="message" id="resultMessage"></div>
    <div class="results" id="resultsMessage"></div>
    <img id="resultImage" src="https://raw.githubusercontent.com/AlienCheats/-AlienCheats-Scripts/refs/heads/main/t%C3%A9l%C3%A9chargement%20(1).jpg" alt="MM2 Result Image">
    <div class="label" id="resultLabel">Yarhm</div>

    <!-- Login Button -->
    <button class="login-button" id="loginButton">Login</button>

    <!-- Create Account Button -->
    <button class="create-account-button" id="createAccountButton">Create Account</button>

    <!-- Login Modal -->
    <div class="modal" id="loginModal">
        <div class="modal-content">
            <input type="text" id="usernameInput" placeholder="Username">
            <input type="password" id="passwordInput" placeholder="Password">
            <button id="submitLogin">Login</button>
            <div class="error-message" id="errorMessage"></div>
        </div>
    </div>

    <!-- Create Account Modal -->
    <div class="modal" id="createAccountModal">
        <div class="modal-content">
            <input type="text" id="newUsernameInput" placeholder="New Username">
            <input type="password" id="newPasswordInput" placeholder="New Password">
            <button id="submitCreateAccount">Create Account</button>
            <div class="error-message" id="accountErrorMessage"></div>
            <div class="success-message" id="accountSuccessMessage"></div>
        </div>
    </div>

    <script>
        const loginButton = document.getElementById('loginButton');
        const createAccountButton = document.getElementById('createAccountButton');
        const loginModal = document.getElementById('loginModal');
        const createAccountModal = document.getElementById('createAccountModal');
        const submitLogin = document.getElementById('submitLogin');
        const submitCreateAccount = document.getElementById('submitCreateAccount');
        const errorMessage = document.getElementById('errorMessage');
        const accountErrorMessage = document.getElementById('accountErrorMessage');
        const accountSuccessMessage = document.getElementById('accountSuccessMessage');
        const usernameInput = document.getElementById('usernameInput');
        const passwordInput = document.getElementById('passwordInput');
        const newUsernameInput = document.getElementById('newUsernameInput');
        const newPasswordInput = document.getElementById('newPasswordInput');
        const searchInput = document.getElementById('searchInput');
        const resultMessage = document.getElementById('resultMessage');
        const resultsMessage = document.getElementById('resultsMessage');
        const resultImage = document.getElementById('resultImage');
        const resultLabel = document.getElementById('resultLabel');
        const userDisplay = document.getElementById('userDisplay');
        const searchContainer = document.getElementById('searchContainer');

        // Retrieve stored accounts from localStorage
        const accounts = JSON.parse(localStorage.getItem('accounts')) || {};
        let loggedInUser = localStorage.getItem('loggedInUser');

        const saveAccounts = () => {
            localStorage.setItem('accounts', JSON.stringify(accounts));
        };

        // Update user display
        const updateUserDisplay = () => {
            if (loggedInUser) {
                userDisplay.textContent = loggedInUser;
                userDisplay.style.display = 'flex';
                searchContainer.style.display = 'none'; // Hide search bar when logged in
            } else {
                userDisplay.style.display = 'none';
                searchContainer.style.display = 'flex'; // Show search bar when logged out
            }
        };

        // Show login modal
        loginButton.addEventListener('click', () => {
            loginModal.style.display = 'flex';
        });

        // Show create account modal
        createAccountButton.addEventListener('click', () => {
            createAccountModal.style.display = 'flex';
        });

        // Handle login
        submitLogin.addEventListener('click', () => {
            const username = usernameInput.value.trim();
            const password = passwordInput.value.trim();

            if (accounts[username] && accounts[username] === password) {
                errorMessage.textContent = '';
                loggedInUser = username;
                localStorage.setItem('loggedInUser', loggedInUser); // Save logged-in user
                alert(`Login successful! Welcome, ${loggedInUser}!`);
                loginModal.style.display = 'none';
                updateUserDisplay();
            } else {
                errorMessage.textContent = 'Username or password is incorrect. Please try again.';
            }
        });

        // Handle account creation
        submitCreateAccount.addEventListener('click', () => {
            const newUsername = newUsernameInput.value.trim();
            const newPassword = newPasswordInput.value.trim();

            if (accounts[newUsername]) {
                accountErrorMessage.textContent = 'Username already taken.';
                accountSuccessMessage.textContent = '';
            } else {
                accounts[newUsername] = newPassword;
                saveAccounts();
                accountSuccessMessage.textContent = 'Account created successfully!';
                accountErrorMessage.textContent = '';
                newUsernameInput.value = '';
                newPasswordInput.value = '';
            }
        });

        // Event listener for search input
        searchInput.addEventListener('keypress', function(event) {
            if (event.key === 'Enter') {
                const keyword = searchInput.value.trim().toLowerCase();
                if (keyword === 'mm2') {
                    resultMessage.textContent = '';
                    resultsMessage.textContent = `Results for "${keyword}"`;
                    resultImage.style.display = 'block';
                    resultLabel.style.display = 'block';
                } else if (keyword === 'fisch') {
                    resultMessage.textContent = '';
                    resultsMessage.textContent = `Results for "${keyword}"`;
                    resultImage.style.display = 'none';
                    resultLabel.style.display = 'none';
                } else {
                    resultMessage.textContent = 'Nothing found here';
                    resultsMessage.textContent = '';
                    resultImage.style.display = 'none';
                    resultLabel.style.display = 'none';
                }
                searchInput.value = '';
            }
        });

        // Initialize user display on page load
        updateUserDisplay();

        // Close modals when clicking outside
        window.addEventListener('click', (event) => {
            if (event.target === loginModal) {
                loginModal.style.display = 'none';
            }
            if (event.target === createAccountModal) {
                createAccountModal.style.display = 'none';
            }
        });
    </script>
</body>
</html>

