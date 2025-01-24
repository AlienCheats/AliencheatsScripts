
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Script Search</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0/css/all.min.css">
    <style>
        :root {
            --primary-color: #4f46e5;
            --secondary-color: #0ea5e9;
            --accent-color: #f43f5e;
            --text-color: #1f2937;
            --background-color: #f8fafc;
            --card-bg: #ffffff;
            --shadow-sm: 0 1px 3px rgba(0,0,0,0.1);
            --shadow-md: 0 4px 6px rgba(0,0,0,0.1);
            --shadow-lg: 0 10px 15px rgba(0,0,0,0.1);
            --radius-sm: 0.375rem;
            --radius-md: 0.5rem;
            --radius-lg: 1rem;
        }

        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Inter', system-ui, sans-serif;
            background: linear-gradient(135deg, var(--primary-color), var(--secondary-color));
            color: var(--text-color);
            line-height: 1.5;
            min-height: 100vh;
            padding-top: 60px;
        }

        .container {
            max-width: 1200px;
            margin: 0 auto;
            padding: 2rem 1rem;
        }

        /* Header & Navigation */
        .top-bar {
            position: fixed;
            top: 0;
            left: 0;
            right: 0;
            background: rgba(255, 255, 255, 0.95);
            backdrop-filter: blur(10px);
            padding: 1rem;
            box-shadow: var(--shadow-md);
            z-index: 1000;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }

        .manage-scripts-button {
            background: var(--card-bg);
            border: none;
            border-radius: var(--radius-lg);
            padding: 0.75rem 1.5rem;
            font-weight: 600;
            cursor: pointer;
            color: var(--primary-color);
            transition: all 0.3s ease;
        }

        .username-display {
            background: var(--card-bg);
            border-radius: var(--radius-lg);
            padding: 0.75rem 1.5rem;
            font-weight: 600;
            color: var(--primary-color);
        }

        /* Search Container */
        .search-container {
            background: var(--card-bg);
            border-radius: var(--radius-lg);
            padding: 1rem;
            margin: 2rem auto;
            max-width: 600px;
            box-shadow: var(--shadow-lg);
        }

        .search-input {
            width: 100%;
            padding: 1rem;
            border: 2px solid transparent;
            border-radius: var(--radius-md);
            font-size: 1rem;
            transition: all 0.3s ease;
        }

        .search-input:focus {
            outline: none;
            border-color: var(--primary-color);
        }

        /* Script Cards */
        .script-card {
            background: var(--card-bg);
            border-radius: var(--radius-lg);
            padding: 1.5rem;
            margin-bottom: 1.5rem;
            box-shadow: var(--shadow-md);
            transition: transform 0.3s ease;
        }

        .script-card:hover {
            transform: translateY(-3px);
            box-shadow: var(--shadow-lg);
        }

        /* Rating System */
        .rating-container {
            margin: 1rem 0;
        }

        .stars {
            color: #ffd700;
            font-size: 1.25rem;
            cursor: pointer;
        }

        .stars i {
            margin-right: 0.25rem;
        }

        /* Comments Section */
        .comments-section {
            margin-top: 1.5rem;
            padding-top: 1rem;
            border-top: 1px solid rgba(0, 0, 0, 0.1);
        }

        .comment-input {
            width: 100%;
            padding: 0.75rem;
            border: 1px solid #e5e7eb;
            border-radius: var(--radius-md);
            margin-bottom: 1rem;
            resize: vertical;
        }

        /* Version History */
        .version-history {
            margin-top: 1rem;
            padding: 1rem;
            background: rgba(0, 0, 0, 0.02);
            border-radius: var(--radius-md);
        }

        .version-item {
            padding: 0.75rem;
            border-bottom: 1px solid rgba(0, 0, 0, 0.1);
        }

        /* Tags */
        .tags-container {
            display: flex;
            flex-wrap: wrap;
            gap: 0.5rem;
            margin: 0.5rem 0;
        }

        .tag {
            background: rgba(79, 70, 229, 0.1);
            color: var(--primary-color);
            padding: 0.25rem 0.75rem;
            border-radius: var(--radius-sm);
            font-size: 0.875rem;
        }

        /* Modal Styles */
        .modal {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0, 0, 0, 0.5);
            z-index: 1000;
        }

        .modal-content {
            background: var(--card-bg);
            padding: 2rem;
            border-radius: var(--radius-lg);
            max-width: 500px;
            width: 90%;
            margin: 50px auto;
            position: relative;
        }

        .close-button {
            position: absolute;
            top: 1rem;
            right: 1rem;
            font-size: 1.5rem;
            cursor: pointer;
            color: var(--text-color);
        }

        /* Buttons */
        .button {
            display: inline-flex;
            align-items: center;
            padding: 0.75rem 1.5rem;
            border-radius: var(--radius-md);
            font-weight: 500;
            border: none;
            cursor: pointer;
            transition: all 0.3s ease;
        }

        .button-primary {
            background: var(--primary-color);
            color: white;
        }

        .button-secondary {
            background: var(--secondary-color);
            color: white;
        }

        /* Manage Scripts Container */
        .manage-container {
            background: var(--card-bg);
            border-radius: var(--radius-lg);
            padding: 2rem;
            margin-top: 2rem;
            box-shadow: var(--shadow-lg);
            display: none;
        }

        /* Upload Container */
        .upload-container {
            background: var(--card-bg);
            border-radius: var(--radius-lg);
            padding: 2rem;
            margin-top: 2rem;
            box-shadow: var(--shadow-lg);
            display: none;
        }

        /* Responsive Design */
        @media (max-width: 768px) {
            .container {
                padding: 1rem;
            }
            
            .modal-content {
                width: 95%;
                margin: 20px auto;
            }
            
            .button {
                width: 100%;
                margin-bottom: 0.5rem;
            }
        }
    </style>
</head>
<body>
    <div class="top-bar">
        <button id="manageScriptsButton" class="manage-scripts-button" style="display: none;">
            <i class="fas fa-cog"></i> Manage Scripts
        </button>
        <div id="userDisplay" class="username-display" style="display: none;"></div>
    </div>

    <div class="container">
        <!-- Button Container -->
        <div class="button-container">
            <button class="button button-primary" id="uploadScriptsButton" style="display: none;">Upload Scripts</button>
            <button class="button button-secondary" id="logoutButton" style="display: none;">Log Out</button>
            <button class="button button-primary" id="loginButton">Login</button>
            <button class="button button-secondary" id="createAccountButton">Create Account</button>
        </div>

        <!-- Search Container -->
        <div class="search-container" id="searchContainer">
            <input type="text" id="searchInput" class="search-input" placeholder="Search scripts with keywords...">
        </div>

        <!-- Manage Scripts Container -->
        <div id="manageScriptsContainer" class="manage-container">
            <h2>Your Scripts</h2>
            <div id="userScriptsList"></div>
        </div>

        <!-- Upload Container -->
        <div class="upload-container" id="uploadContainer">
            <h2>Upload Your Script</h2>
            
            <div class="script-input-container">
                <textarea id="scriptText" placeholder="Paste your script here..." class="comment-input"></textarea>
            </div>

            <div class="tag-selector">
                <select multiple id="scriptTags" class="search-input">
                    <option value="mm2">MM2</option>
                    <option value="arsenal">Arsenal</option>
                    <option value="blox">Blox Fruits</option>
                    <option value="pet">Pet Simulator</option>
                    <option value="combat">Combat</option>
                    <option value="farm">Farm</option>
                    <option value="auto">Auto</option>
                    <option value="gui">GUI</option>
                </select>
            </div>

            <div class="version-input">
                <input type="text" id="scriptVersion" placeholder="Version (e.g., 1.0.0)" class="search-input">
                <textarea id="changelog" placeholder="Changelog (What's new in this version?)" class="comment-input"></textarea>
            </div>

            <input type="text" id="scriptName" placeholder="Script name..." class="search-input">
            <textarea id="scriptDescription" placeholder="Script description..." class="comment-input"></textarea>
            
            <button class="button button-primary upload-button">Upload Script</button>
        </div>

        <!-- Results Container -->
        <div class="results-container">
            <div id="resultMessage" class="message"></div>
            <div id="resultsMessage" class="results"></div>
        </div>
    </div>

    <!-- Login Modal -->
    <div id="loginModal" class="modal">
        <div class="modal-content">
            <span class="close-button" id="closeLoginModal">&times;</span>
            <h2>Login</h2>
            <input type="text" id="usernameInput" class="search-input" placeholder="Username">
            <input type="password" id="passwordInput" class="search-input" placeholder="Password">
            <button id="submitLogin" class="button button-primary">Login</button>
            <div id="loginErrorMessage" class="message"></div>
        </div>
    </div>

    <!-- Create Account Modal -->
    <div id="createAccountModal" class="modal">
        <div class="modal-content">
            <span class="close-button" id="closeCreateAccountModal">&times;</span>
            <h2>Create Account</h2>
            <input type="text" id="newUsernameInput" class="search-input" placeholder="New Username">
            <input type="password" id="newPasswordInput" class="search-input" placeholder="New Password">
            <button id="submitCreateAccount" class="button button-primary">Create Account</button>
            <div id="accountErrorMessage" class="message"></div>
            <div id="accountSuccessMessage" class="message"></div>
        </div>
    </div>

    <script>
        // Initialize storage objects
        const accounts = JSON.parse(localStorage.getItem('accounts')) || {};
        let loggedInUser = null;
        const scripts = JSON.parse(localStorage.getItem('scripts')) || [];
        const userFavorites = JSON.parse(localStorage.getItem('userFavorites')) || {};
        const scriptRatings = JSON.parse(localStorage.getItem('scriptRatings')) || {};
        const scriptComments = JSON.parse(localStorage.getItem('scriptComments')) || {};

        // DOM Elements
        const userDisplay = document.getElementById('userDisplay');
        const loginModal = document.getElementById('loginModal');
        const createAccountModal = document.getElementById('createAccountModal');
        const loginButton = document.getElementById('loginButton');
        const logoutButton = document.getElementById('logoutButton');
        const createAccountButton = document.getElementById('createAccountButton');
        const uploadScriptsButton = document.getElementById('uploadScriptsButton');
        const manageScriptsButton = document.getElementById('manageScriptsButton');
        const manageScriptsContainer = document.getElementById('manageScriptsContainer');
        const searchContainer = document.getElementById('searchContainer');
        const uploadContainer = document.getElementById('uploadContainer');
        const resultsContainer = document.querySelector('.results-container');

        // Check login state on page load
        function checkLoginState() {
            const savedUser = localStorage.getItem('loggedInUser');
            if (savedUser && accounts[savedUser]) {
                loggedInUser = savedUser;
                updateUIForLoggedInUser();
            }
        }

        // UI Update Functions
        function updateUIForLoggedInUser() {
            userDisplay.textContent = `Welcome, ${loggedInUser}!`;
            userDisplay.style.display = 'block';
            loginButton.style.display = 'none';
            createAccountButton.style.display = 'none';
            uploadScriptsButton.style.display = 'inline-block';
            logoutButton.style.display = 'inline-block';
            manageScriptsButton.style.display = 'block';
        }

        function logout() {
            loggedInUser = null;
            localStorage.removeItem('loggedInUser');
            userDisplay.style.display = 'none';
            loginButton.style.display = 'inline-block';
            createAccountButton.style.display = 'inline-block';
            uploadScriptsButton.style.display = 'none';
            logoutButton.style.display = 'none';
            manageScriptsButton.style.display = 'none';
            uploadContainer.style.display = 'none';
            manageScriptsContainer.style.display = 'none';
            searchContainer.style.display = 'block';
            resultsContainer.style.display = 'block';
        }

        // Event Listeners
        loginButton.addEventListener('click', () => loginModal.style.display = 'block');
        createAccountButton.addEventListener('click', () => createAccountModal.style.display = 'block');
        logoutButton.addEventListener('click', logout);

        // Close modal buttons
        document.querySelectorAll('.close-button').forEach(button => {
            button.addEventListener('click', () => {
                loginModal.style.display = 'none';
                createAccountModal.style.display = 'none';
            });
        });

        // Login functionality
        document.getElementById('submitLogin').addEventListener('click', () => {
            const username = document.getElementById('usernameInput').value.trim();
            const password = document.getElementById('passwordInput').value.trim();

            if (accounts[username] && accounts[username] === password) {
                loggedInUser = username;
                localStorage.setItem('loggedInUser', username);
                updateUIForLoggedInUser();
                loginModal.style.display = 'none';
                document.getElementById('loginErrorMessage').textContent = '';
            } else {
                document.getElementById('loginErrorMessage').textContent = 'Invalid username or password';
            }
        });

        // Create Account functionality
        document.getElementById('submitCreateAccount').addEventListener('click', () => {
            const newUsername = document.getElementById('newUsernameInput').value.trim();
            const newPassword = document.getElementById('newPasswordInput').value.trim();

            if (accounts[newUsername]) {
                document.getElementById('accountErrorMessage').textContent = 'Username already taken';
            } else {
                accounts[newUsername] = newPassword;
                localStorage.setItem('accounts', JSON.stringify(accounts));
                document.getElementById('accountSuccessMessage').textContent = 'Account created successfully!';
                setTimeout(() => {
                    createAccountModal.style.display = 'none';
                    document.getElementById('accountSuccessMessage').textContent = '';
                }, 1500);
            }
        });

        // Search functionality
        document.getElementById('searchInput').addEventListener('keyup', function(event) {
            if (event.key === 'Enter') {
                const searchTerm = this.value.toLowerCase().trim();
                const filteredScripts = scripts.filter(script => 
                    script.name.toLowerCase().includes(searchTerm) ||
                    script.tags.some(tag => tag.toLowerCase().includes(searchTerm))
                );
                displayScripts(filteredScripts);
            }
        });

        // Display scripts function
        function displayScripts(scriptsToDisplay) {
            const resultsDiv = document.getElementById('resultsMessage');
            resultsDiv.innerHTML = '';

            scriptsToDisplay.forEach(script => {
                const scriptCard = createScriptCard(script);
                resultsDiv.appendChild(scriptCard);
            });
        }

        // Create script card function
        function createScriptCard(script) {
            const card = document.createElement('div');
            card.className = 'script-card';
            
            const rating = calculateAverageRating(script.id);
            
            card.innerHTML = `
                <div class="script-header">
                    <h3>${script.name}</h3>
                    <button class="favorite-btn" onclick="toggleFavorite('${script.id}')">
                        <i class="fas fa-heart ${isScriptFavorited(script.id) ? 'favorited' : ''}"></i>
                    </button>
                </div>
                <p>${script.description}</p>
                <div class="tags-container">
                    ${script.tags.map(tag => `<span class="tag">${tag}</span>`).join('')}
                </div>
                <div class="rating-container">
                    <div class="stars" data-script-id="${script.id}">
                        ${generateStars(rating)}
                    </div>
                    <span>(${rating}/5)</span>
                </div>
                <div class="version-history">
                    <p>Version: ${script.version}</p>
                    <p>Updated: ${new Date(script.dateUploaded).toLocaleDateString()}</p>
                </div>
                <div class="comments-section">
                    <textarea class="comment-input" placeholder="Add a comment..."></textarea>
                    <button class="button button-primary" onclick="addComment('${script.id}')">Post Comment</button>
                    <div class="comments-list">
                        ${generateComments(script.id)}
                    </div>
                </div>
            `;
            
            return card;
        }

        // Utility functions
        function calculateAverageRating(scriptId) {
            const ratings = scriptRatings[scriptId] || [];
            if (ratings.length === 0) return 0;
            return (ratings.reduce((sum, r) => sum + r, 0) / ratings.length).toFixed(1);
        }

        function generateStars(rating) {
            return Array(5).fill(0).map((_, i) => 
                `<i class="fas fa-star ${i < rating ? 'filled' : ''}"></i>`
            ).join('');
        }

        function isScriptFavorited(scriptId) {
            return userFavorites[loggedInUser]?.includes(scriptId) || false;
        }

        function generateComments(scriptId) {
            const comments = scriptComments[scriptId] || [];
            return comments.map(comment => `
                <div class="comment">
                    <strong>${comment.user}</strong>
                    <span>${new Date(comment.date).toLocaleDateString()}</span>
                    <p>${comment.text}</p>
                </div>
            `).join('');
        }

        // Initialize the application
        checkLoginState();
    </script>
</body>
</html>
