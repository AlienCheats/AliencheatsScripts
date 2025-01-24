<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Script Search</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0/css/all.min.css">
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

        /* Base Styles */
        body {
            background: linear-gradient(135deg, var(--gradient-start), var(--gradient-end));
            background-attachment: fixed;
            min-height: 100vh;
            margin: 0;
            display: flex;
            flex-direction: column;
            align-items: center;
            padding: 40px 20px;
            position: relative;
            font-family: 'Inter', 'Segoe UI', sans-serif;
            color: var(--text-color);
        }

        /* Header Elements */
        .top-bar {
            position: fixed;
            top: 0;
            left: 0;
            right: 0;
            padding: 15px;
            display: flex;
            justify-content: space-between;
            align-items: center;
            background: rgba(255, 255, 255, 0.9);
            backdrop-filter: blur(10px);
            z-index: 1000;
            box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
        }

        .manage-scripts-button {
            position: fixed;
            top: 20px;
            left: 20px;
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
            z-index: 1000;
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

        /* Search Container */
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

        /* Script Cards */
        .script-card {
            background: rgba(255, 255, 255, 0.95);
            border-radius: 15px;
            padding: 20px;
            margin: 15px 0;
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.1);
            transition: all 0.3s ease;
        }

        .script-card:hover {
            transform: translateY(-3px);
            box-shadow: 0 8px 25px rgba(0, 0, 0, 0.15);
        }

        /* Rating System */
        .rating-container {
            margin: 10px 0;
        }

        .stars {
            color: #ffd700;
            font-size: 20px;
            cursor: pointer;
        }

        .stars i {
            margin-right: 2px;
        }

        /* Comments Section */
        .comments-section {
            margin-top: 15px;
            padding-top: 15px;
            border-top: 1px solid rgba(0, 0, 0, 0.1);
        }

        .comment-input {
            width: 100%;
            padding: 10px;
            border-radius: 10px;
            border: 1px solid rgba(0, 0, 0, 0.1);
            margin-bottom: 10px;
            resize: vertical;
        }

        /* Version History */
        .version-history {
            margin-top: 15px;
            padding: 10px;
            background: rgba(0, 0, 0, 0.05);
            border-radius: 10px;
        }

        .version-item {
            padding: 8px;
            border-bottom: 1px solid rgba(0, 0, 0, 0.1);
        }

        /* Favorites */
        .favorite-btn {
            background: none;
            border: none;
            color: var(--accent-color);
            font-size: 20px;
            cursor: pointer;
            transition: transform 0.3s ease;
        }

        .favorite-btn:hover {
            transform: scale(1.1);
        }

        /* Manage Scripts Container */
        .manage-container {
            background: rgba(255, 255, 255, 0.95);
            border-radius: 20px;
            padding: 30px;
            margin-top: 30px;
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.15);
            backdrop-filter: blur(10px);
            max-width: 800px;
            width: 100%;
            display: none;
        }

        /* Tags */
        .tags-container {
            display: flex;
            flex-wrap: wrap;
            gap: 5px;
            margin: 10px 0;
        }

        .tag {
            background: var(--primary-color);
            color: white;
            padding: 5px 10px;
            border-radius: 15px;
            font-size: 12px;
        }

        /* Existing styles remain unchanged */
        /* ... (keep all your existing styles) ... */
    </style>
</head>
<body>
    <div class="top-bar">
        <button id="manageScriptsButton" class="manage-scripts-button" style="display: none;">
            <i class="fas fa-cog"></i> Manage Scripts
        </button>
        <div id="userDisplay" class="username-display" style="display: none;"></div>
    </div>

    <div class="button-container">
        <button class="upload-scripts-button" id="uploadScriptsButton" style="display: none;">Upload Scripts</button>
        <button class="logout-button" id="logoutButton" style="display: none;">Log Out</button>
    </div>

    <div class="rounded-rectangle" id="searchContainer">
        <input type="text" id="searchInput" placeholder="Search scripts with keywords...">
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
            <textarea id="scriptText" placeholder="Paste your script here..." class="script-textarea"></textarea>
        </div>

        <div class="tag-selector">
            <select multiple id="scriptTags" class="script-select">
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
            <input type="text" id="scriptVersion" placeholder="Version (e.g., 1.0.0)" class="script-input">
            <textarea id="changelog" placeholder="Changelog (What's new in this version?)" class="script-textarea"></textarea>
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
        // Initialize storage objects
        const accounts = JSON.parse(localStorage.getItem('accounts')) || {};
        let loggedInUser = null;
        const scripts = JSON.parse(localStorage.getItem('scripts')) || [];

        // Initialize favorites and ratings
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
        checkLoginState();

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
            searchContainer.style.display = 'flex';
            resultsContainer.style.display = 'block';
        }

        // Event Listeners for basic functionality
        loginButton.addEventListener('click', () => loginModal.style.display = 'flex');
        createAccountButton.addEventListener('click', () => createAccountModal.style.display = 'flex');
        logoutButton.addEventListener('click', logout);
        document.getElementById('closeLoginModal').addEventListener('click', () => loginModal.style.display = 'none');
        document.getElementById('closeCreateAccountModal').addEventListener('click', () => createAccountModal.style.display = 'none');

        // Login functionality
        document.getElementById('submitLogin').addEventListener('click', () => {
            const username = document.getElementById('usernameInput').value.trim();
            const password = document.getElementById('passwordInput').value.trim();

            if (accounts[username] && accounts[username] === password) {
                loggedInUser = username;
                localStorage.setItem('loggedInUser', username);
                updateUIForLoggedInUser();
                loginModal.style.display = 'none';
                document.getElementById('usernameInput').value = '';
                document.getElementById('passwordInput').value = '';
                document.getElementById('loginErrorMessage').textContent = '';
            } else {
                document.getElementById('loginErrorMessage').textContent = 'Username or password is incorrect.';
            }
        });

        // Create Account functionality
        document.getElementById('submitCreateAccount').addEventListener('click', () => {
            const newUsername = document.getElementById('newUsernameInput').value.trim();
            const newPassword = document.getElementById('newPasswordInput').value.trim();

            if (accounts[newUsername]) {
                document.getElementById('accountErrorMessage').textContent = 'Username already taken.';
                document.getElementById('accountSuccessMessage').textContent = '';
            } else {
                accounts[newUsername] = newPassword;
                localStorage.setItem('accounts', JSON.stringify(accounts));
                document.getElementById('accountSuccessMessage').textContent = 'Account created successfully!';
                document.getElementById('accountErrorMessage').textContent = '';
                document.getElementById('newUsernameInput').value = '';
                document.getElementById('newPasswordInput').value = '';
            }
        });

        // Manage Scripts Button functionality
        manageScriptsButton.addEventListener('click', () => {
            uploadContainer.style.display = 'none';
            searchContainer.style.display = 'none';
            resultsContainer.style.display = 'none';
            manageScriptsContainer.style.display = 'block';
            
            // Display user's scripts
            displayUserScripts();
        });

        function displayUserScripts() {
            const userScriptsList = document.getElementById('userScriptsList');
            userScriptsList.innerHTML = '';
            
            const userScripts = scripts.filter(script => script.uploader === loggedInUser);
            
            userScripts.forEach(script => {
                const scriptCard = document.createElement('div');
                scriptCard.className = 'script-card';
                scriptCard.innerHTML = `
                    <h3>${script.name}</h3>
                    <p>${script.description}</p>
                    <div class="script-stats">
                        <span>Rating: ${getAverageRating(script)}/5</span>
                        <span>Comments: ${getCommentCount(script)}</span>
                    </div>
                    <div class="script-actions">
                        <button class="edit-btn" onclick="editScript('${script.id}')">Edit</button>
                        <button class="delete-btn" onclick="deleteScript('${script.id}')">Delete</button>
                    </div>
                `;
                userScriptsList.appendChild(scriptCard);
            });
        }

        // Script management functions
        function getAverageRating(script) {
            const ratings = scriptRatings[script.id] || [];
            if (ratings.length === 0) return 0;
            const sum = ratings.reduce((acc, curr) => acc + curr.rating, 0);
            return (sum / ratings.length).toFixed(1);
        }

        function getCommentCount(script) {
            return (scriptComments[script.id] || []).length;
        }

        function editScript(scriptId) {
            // Implementation for editing script
            const script = scripts.find(s => s.id === scriptId);
            if (!script) return;
            
            // Populate edit form
            document.getElementById('scriptText').value = script.text;
            document.getElementById('scriptName').value = script.name;
            document.getElementById('scriptDescription').value = script.description;
            
            uploadContainer.style.display = 'block';
            manageScriptsContainer.style.display = 'none';
        }

        function deleteScript(scriptId) {
            if (confirm('Are you sure you want to delete this script?')) {
                const index = scripts.findIndex(s => s.id === scriptId);
                if (index !== -1) {
                    scripts.splice(index, 1);
                    localStorage.setItem('scripts', JSON.stringify(scripts));
                    displayUserScripts();
                }
            }
        }

        // Script upload functionality
        document.querySelector('.upload-button').addEventListener('click', function() {
            const scriptText = document.getElementById('scriptText').value;
            const tags = Array.from(document.getElementById('scriptTags').selectedOptions).map(option => option.value);
            const name = document.getElementById('scriptName').value;
            const description = document.getElementById('scriptDescription').value;
            const version = document.getElementById('scriptVersion').value;
            const changelog = document.getElementById('changelog').value;

            if (!scriptText || tags.length === 0 || !name || !description || !version) {
                alert('Please fill in all required fields');
                return;
            }

            const scriptId = 'script_' + Date.now();
            const newScript = {
                id: scriptId,
                text: scriptText,
                tags: tags,
                name: name,
                description: description,
                uploader: loggedInUser,
                version: version,
                changelog: changelog,
                dateUploaded: new Date().toISOString(),
                versions: [{
                    version: version,
                    text: scriptText,
                    changelog: changelog,
                    date: new Date().toISOString()
                }]
            };

            scripts.push(newScript);
            localStorage.setItem('scripts', JSON.stringify(scripts));
            
            alert('Script uploaded successfully!');
            resetUploadForm();
            displayUserScripts();
        });

        function resetUploadForm() {
            document.getElementById('scriptText').value = '';
            document.getElementById('scriptTags').value = '';
            document.getElementById('scriptName').value = '';
            document.getElementById('scriptDescription').value = '';
            document.getElementById('scriptVersion').value = '';
            document.getElementById('changelog').value = '';
            uploadContainer.style.display = 'none';
            searchContainer.style.display = 'flex';
            resultsContainer.style.display = 'block';
        }

        // Search functionality with enhanced display
        document.getElementById('searchInput').addEventListener('keypress', function(event) {
            if (event.key === 'Enter') {
                const searchTerm = this.value.trim().toLowerCase();
                const matchingScripts = scripts.filter(script => 
                    script.tags.some(tag => tag.toLowerCase().includes(searchTerm)) ||
                    script.name.toLowerCase().includes(searchTerm) ||
                    script.description.toLowerCase().includes(searchTerm)
                );

                displaySearchResults(matchingScripts);
                this.value = '';
            }
        });

        function displaySearchResults(matchingScripts) {
            const resultsContainer = document.getElementById('resultsMessage');
            resultsContainer.innerHTML = '';

            if (matchingScripts.length > 0) {
                matchingScripts.forEach(script => {
                    const scriptCard = createScriptCard(script);
                    resultsContainer.appendChild(scriptCard);
                });
            } else {
                resultsContainer.innerHTML = 'No scripts found';
            }
        }

        function createScriptCard(script) {
            const card = document.createElement('div');
            card.className = 'script-card';
            
            const rating = getAverageRating(script);
            const isFavorite = userFavorites[loggedInUser]?.includes(script.id);
            
            card.innerHTML = `
                <div class="script-header">
                    <h3>${script.name}</h3>
                    <button class="favorite-btn" onclick="toggleFavorite('${script.id}')">
                        <i class="fas fa-heart ${isFavorite ? 'favorited' : ''}"></i>
                    </button>
                </div>
                <p class="uploader-info">Uploaded by: ${script.uploader}</p>
                <div class="tags-container">
                    ${script.tags.map(tag => `<span class="tag">${tag}</span>`).join('')}
                </div>
                <div class="rating-container">
                    <div class="stars" data-script-id="${script.id}">
                        ${generateStars(rating)}
                    </div>
                    <span class="rating-count">(${rating} / 5)</span>
                </div>
                <div class="script-details">
                    <p>${script.description}</p>
                    <div class="version-info">
                        <span>Version: ${script.version}</span>
                        <span>Updated: ${formatDate(script.dateUploaded)}</span>
                    </div>
                    <button class="get-script-btn" onclick="copyScript('${script.id}')">Get Script</button>
                </div>
                <div class="comments-section" data-script-id="${script.id}">
                    <textarea class="comment-input" placeholder="Add a comment..."></textarea>
                    <button class="post-comment-btn" onclick="postComment('${script.id}')">Post</button>
                    <div class="comments-list">
                        ${generateComments(script.id)}
                    </div>
                </div>
            `;
            
            return card;
        }

        // Utility functions
        function generateStars(rating) {
            return Array(5).fill(0).map((_, index) => 
                `<i class="fas fa-star ${index < rating ? 'filled' : ''}"></i>`
            ).join('');
        }

        function formatDate(dateString) {
            return new Date(dateString).toLocaleDateString();
        }

        function generateComments(scriptId) {
            const comments = scriptComments[scriptId] || [];
            return comments.map(comment => `
                <div class="comment">
                    <strong>${comment.user}</strong>
                    <span>${formatDate(comment.date)}</span>
                    <p>${comment.text}</p>
                </div>
            `).join('');
        }

        // Initialize the application
        checkLoginState();
    </script>
</body>
</html>
