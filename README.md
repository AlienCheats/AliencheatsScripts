<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Background Image</title>
    <style>
        body {
            background-color: green; /* Green background */
            height: 100vh; /* Full viewport height */
            margin: 0; /* Remove default margin */
            display: flex; /* Use flexbox for positioning */
            justify-content: center; /* Center horizontally */
            align-items: flex-start; /* Align items to the top */
            padding-top: 50px; /* Add padding to move the rectangle down */
            flex-direction: column; /* Stack items vertically */
        }

        .rounded-rectangle {
            background-color: rgba(210, 180, 140, 0.8); /* Light brown color */
            border-radius: 15px; /* Rounded corners */
            width: 300px; /* Width of the rectangle */
            height: 50px; /* Height of the rectangle (thinner) */
            box-shadow: 0 4px 10px rgba(0, 0, 0, 0.5); /* Shadow effect */
            display: flex; /* Use flexbox for content alignment */
            justify-content: center; /* Center content horizontally */
            align-items: center; /* Center content vertically */
            margin: 0 auto; /* Center the rectangle */
        }

        input {
            border: none; /* Remove default border */
            background: transparent; /* Make input background transparent */
            outline: none; /* Remove outline on focus */
            width: 90%; /* Width of the input field */
            font-size: 16px; /* Font size */
            padding: 10px; /* Padding inside the input */
        }

        .message {
            color: red; /* Color for the message */
            text-align: center; /* Center the message */
            margin-top: 20px; /* Margin above the message */
        }

        .results {
            color: green; /* Color for the results message */
            text-align: center; /* Center the results message */
            margin-top: 10px; /* Margin above the results message */
        }

        img {
            margin-top: 20px; /* Margin above the image */
            max-width: 300px; /* Maximum width for the image */
            border-radius: 15px; /* Make the image rounded */
            display: none; /* Initially hide the image */
        }

        .label {
            background-color: rgba(210, 180, 140, 0.8); /* Light brown color */
            border-radius: 10px; /* Rounded corners */
            text-align: center; /* Center text */
            margin-top: 10px; /* Margin above the label */
            padding: 10px; /* Padding inside the label */
            display: none; /* Initially hide the label */
        }

        .login-button, .create-account-button {
            background-color: rgba(210, 180, 140, 0.8); /* Light brown color */
            border-radius: 15px; /* Rounded corners */
            border: none; /* No border */
            padding: 10px 15px; /* Padding */
            color: white; /* Text color */
            font-size: 16px; /* Font size */
            cursor: pointer; /* Pointer cursor on hover */
            margin: 5px; /* Margin for buttons */
        }

        .modal {
            position: fixed; /* Fixed position */
            top: 0; /* Align to top */
            left: 0; /* Align to left */
            width: 100%; /* Full width */
            height: 100%; /* Full height */
            background-color: rgba(0, 0, 0, 0.7); /* Black with transparency */
            display: none; /* Initially hidden */
            justify-content: center; /* Center modal content */
            align-items: center; /* Center modal content */
        }

        .modal-content {
            background-color: black; /* Black background for modal */
            border-radius: 15px; /* Rounded corners */
            padding: 20px; /* Padding inside modal */
            text-align: center; /* Center text */
            color: white; /* Text color */
        }

        .modal-input {
            border: none; /* Remove border */
            padding: 10px; /* Padding inside input */
            margin: 10px 0; /* Margin around inputs */
            border-radius: 5px; /* Rounded corners */
            width: 80%; /* Width of input */
        }
    </style>
</head>
<body>
    <div class="rounded-rectangle">
        <input type="text" id="searchInput" placeholder="Search scripts with keywords...">
    </div>
    <div class="message" id="resultMessage"></div>
    <div class="results" id="resultsMessage"></div>
    <img id="resultImage" src="https://raw.githubusercontent.com/AlienCheats/-AlienCheats-Scripts/refs/heads/main/t%C3%A9l%C3%A9chargement%20(1).jpg" alt="MM2 Result Image">
    <div class="label" id="resultLabel">Yarhm</div>

    <button class="login-button" id="loginButton">Login</button>
    <button class="create-account-button" id="createAccountButton">Create Account</button>

    <div class="modal" id="modal">
        <div class="modal-content">
            <div id="modalText"></div>
            <input type="text" id="usernameInput" class="modal-input" placeholder="Username">
            <input type="password" id="passwordInput" class="modal-input" placeholder="Password">
            <button id="submitModalButton">Login</button>
        </div>
    </div>

    <script>
        const searchInput = document.getElementById('searchInput');
        const resultMessage = document.getElementById('resultMessage');
        const resultsMessage = document.getElementById('resultsMessage');
        const resultImage = document.getElementById('resultImage');
        const resultLabel = document.getElementById('resultLabel');
        const loginButton = document.getElementById('loginButton');
        const createAccountButton = document.getElementById('createAccountButton');
        const modal = document.getElementById('modal');
        const modalText = document.getElementById('modalText');
        const usernameInput = document.getElementById('usernameInput');
        const passwordInput = document.getElementById('passwordInput');
        const submitModalButton = document.getElementById('submitModalButton');

        let currentUser = null;
        const accounts = JSON.parse(localStorage.getItem('accounts')) || {};

        searchInput.addEventListener('keypress', function(event) {
            if (event.key === 'Enter') {
                const keyword = searchInput.value.trim().toLowerCase();
                if (keyword === '') {
                    resultMessage.textContent = '';
                    resultsMessage.textContent = '';
                    resultImage.style.display = 'none';
                    resultLabel.style.display = 'none';
                } else if (keyword === 'mm2') {
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
                this.value = '';
            }
        });

        loginButton.addEventListener('click', function() {
            modal.style.display = 'flex';
            modalText.textContent = 'Login';
            submitModalButton.textContent = 'Login';
            usernameInput.value = '';
            passwordInput.value = '';
        });

        createAccountButton.addEventListener('click', function() {
            modal.style.display = 'flex';
            modalText.textContent = 'Create Account';
            submitModalButton.textContent = 'Create Account';
            usernameInput.value = '';
            passwordInput.value = '';
        });

        submitModalButton.addEventListener('click', function() {
            const username = usernameInput.value.trim();
            const password = passwordInput.value.trim();
            
            if (modalText.textContent === 'Login') {
                // Login logic
                if (accounts[username] && accounts[username] === password) {
                    currentUser = username;
                    alert('Login successful');
                    updateUI();
                    modal.style.display = 'none';
                } else {
                    alert('Username or password wrong. Please try again.');
                }
            } else {
                // Create account logic
                if (!accounts[username]) {
                    accounts[username] = password;
                    localStorage.setItem('accounts', JSON.stringify(accounts));
                    alert('Account created successfully!');
                    modal.style.display = 'none';
                } else {
                    alert('Username already taken.');
                }
            }
        });

        function updateUI() {
            if (currentUser) {
                loginButton.style.display = 'none'; // Hide login button
                createAccountButton.style.display = 'none'; // Hide create account button
                const usernameDisplay = document.createElement('div');
                usernameDisplay.textContent = currentUser; // Display logged-in username
                usernameDisplay.classList.add('rounded-rectangle'); // Add class for styling
                document.body.insertBefore(usernameDisplay, modal); // Insert before modal
            }
        }
    </script>
</body>
</html>

