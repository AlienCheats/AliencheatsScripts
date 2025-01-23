
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

        .modal {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background-color: rgba(0, 0, 0, 0.7);
            display: none;
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

    <div class="rounded-rectangle">
        <input type="text" id="searchInput" placeholder="Search scripts with keywords...">
    </div>
    <div class="message" id="resultMessage"></div>
    <div class="results" id="resultsMessage"></div>
    <img id="resultImage" src="https://raw.githubusercontent.com/AlienCheats/-AlienCheats-Scripts/refs/heads/main/t%C3%A9l%C3%A9chargement%20(1).jpg" alt="MM2 Result Image">
    <div class="label" id="resultLabel">Yarhm</div>

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
        const searchInput = document.getElementById('searchInput');
        const resultMessage = document.getElementById('resultMessage');
        const resultsMessage = document.getElementById('resultsMessage');
        const resultImage = document.getElementById('resultImage');
        const resultLabel = document.getElementById('resultLabel');

        const validCredentials = {
            username: 'admin',
            password: 'password123'
        };

        // Show login modal
        loginButton.addEventListener('click', () => {
            loginModal.style.display = 'flex';
        });

        // Handle login
        submitLogin.addEventListener('click', () => {
            const username = usernameInput.value.trim();
            const password = passwordInput.value.trim();

            if (username === validCredentials.username && password === validCredentials.password) {
                errorMessage.textContent = '';
                alert('Login successful!');
                loginModal.style.display = 'none';
                usernameInput.value = '';
                passwordInput.value = '';
            } else {
                errorMessage.textContent = 'Password or username wrong, please try again.';
            }
        });

        // Hide modal when clicking outside
        window.addEventListener('click', (event) => {
            if (event.target === loginModal) {
                loginModal.style.display = 'none';
            }
        });

        // Search scripts
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
                searchInput.value = '';
            }
        });
    </script>
</body>
</html>


