
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Background Image</title>
    <style>
        /* Existing styles... */
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
    
    <!-- New Upload Scripts Button -->
    <button class="upload-scripts-button" id="uploadScriptsButton" style="display: none;">Upload Scripts</button>

    <!-- Existing modals... -->

    <script>
        const accounts = {};
        let loggedInUser = null;

        const userDisplay = document.getElementById('userDisplay');
        const loginModal = document.getElementById('loginModal');
        const createAccountModal = document.getElementById('createAccountModal');
        const loginButton = document.getElementById('loginButton');
        const createAccountButton = document.getElementById('createAccountButton');
        const uploadScriptsButton = document.getElementById('uploadScriptsButton'); // New button
        const submitLogin = document.getElementById('submitLogin');
        const submitCreateAccount = document.getElementById('submitCreateAccount');
        const loginErrorMessage = document.getElementById('loginErrorMessage');
        const accountErrorMessage = document.getElementById('accountErrorMessage');
        const accountSuccessMessage = document.getElementById('accountSuccessMessage');

        // Functions to save and load accounts
        // ... existing functions ...

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
        // ... existing event listeners ...

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
                uploadScriptsButton.style.display = 'inline-block'; // Show upload button
            } else {
                loginErrorMessage.textContent = 'Username or password is incorrect.';
            }
        });

        // Handle account creation
        // ... existing code ...

        // Event listener for search input
        // ... existing code ...
    </script>
</body>
</html>
