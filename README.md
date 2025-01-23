
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
        }

        .login-button {
            position: absolute; 
            top: 10px; 
            right: 10px; 
            background-color: rgba(255, 255, 255, 0.8); 
            border: none; 
            border-radius: 15px; 
            padding: 10px 20px; 
            font-size: 14px; 
            font-weight: bold; 
            cursor: pointer; 
            box-shadow: 0 4px 10px rgba(0, 0, 0, 0.3); 
        }

        /* Login modal styles */
        .modal {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background-color: rgba(0, 0, 0, 0.7); /* Semi-transparent black background */
            display: none; /* Hidden by default */
            justify-content: center;
            align-items: center;
            z-index: 1000;
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

        .error-message {
            color: red;
            text-align: center;
            margin-top: 10px;
        }
    </style>
</head>
<body>
    <button class="login-button" id="loginButton">Login</button>

    <div class="modal" id="loginModal">
        <div class="modal-content">
            <input type="text" id="usernameInput" placeholder="Username">
            <input type="password" id="passwordInput" placeholder="Password">
            <button id="submitLogin">Login</button>
            <div class="error-message" id="errorMessage"></div>
        </div>
    </div>

    <script>
        const loginButton = document.getElementById('loginButton');
        const loginModal = document.getElementById('loginModal');
        const submitLogin = document.getElementById('submitLogin');
        const errorMessage = document.getElementById('errorMessage');
        const usernameInput = document.getElementById('usernameInput');
        const passwordInput = document.getElementById('passwordInput');

        const validCredentials = {
            username: 'admin',
            password: 'password123'
        };

        // Show login modal
        loginButton.addEventListener('click', () => {
            loginModal.style.display = 'flex'; // Show the modal
        });

        // Handle login
        submitLogin.addEventListener('click', () => {
            const username = usernameInput.value.trim();
            const password = passwordInput.value.trim();

            if (username === validCredentials.username && password === validCredentials.password) {
                errorMessage.textContent = ''; // Clear any error messages
                alert('Login successful!');
                loginModal.style.display = 'none'; // Hide the modal
                usernameInput.value = ''; // Clear input fields
                passwordInput.value = '';
            } else {
                errorMessage.textContent = 'Password or username wrong, please try again.';
            }
        });

        // Hide the modal when clicking outside of it
        window.addEventListener('click', (event) => {
            if (event.target === loginModal) {
                loginModal.style.display = 'none';
            }
        });
    </script>
</body>
</html>


