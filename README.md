<!DOCTYPE html>
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
            background: var(--background-color);
            color: var(--text-color);
            line-height: 1.5;
            min-height: 100vh;
        }

        .container {
            max-width: 1200px;
            margin: 0 auto;
            padding: 2rem 1rem;
        }

        /* Header Styles */
        .header {
            background: var(--card-bg);
            padding: 1rem;
            box-shadow: var(--shadow-sm);
            position: sticky;
            top: 0;
            z-index: 100;
        }

        .nav-container {
            display: flex;
            justify-content: space-between;
            align-items: center;
            max-width: 1200px;
            margin: 0 auto;
        }

        /* Button Styles */
        .button {
            display: inline-flex;
            align-items: center;
            padding: 0.75rem 1.5rem;
            border-radius: var(--radius-sm);
            font-weight: 500;
            border: none;
            cursor: pointer;
            transition: all 0.2s ease;
            gap: 0.5rem;
        }

        .button-primary {
            background: var(--primary-color);
            color: white;
        }

        .button-secondary {
            background: var(--secondary-color);
            color: white;
        }

        .button:hover {
            transform: translateY(-1px);
            box-shadow: var(--shadow-md);
        }

        /* Search Bar */
        .search-container {
            max-width: 600px;
            margin: 2rem auto;
        }

        .search-input {
            width: 100%;
            padding: 1rem;
            border: 2px solid #e5e7eb;
            border-radius: var(--radius-lg);
            font-size: 1rem;
            transition: all 0.2s ease;
        }

        .search-input:focus {
            outline: none;
            border-color: var(--primary-color);
            box-shadow: 0 0 0 3px rgba(79, 70, 229, 0.1);
        }

        /* Script Cards */
        .script-grid {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
            gap: 1.5rem;
            margin-top: 2rem;
        }

        .script-card {
            background: var(--card-bg);
            border-radius: var(--radius-md);
            padding: 1.5rem;
            box-shadow: var(--shadow-md);
            transition: transform 0.2s ease;
        }

        .script-card:hover {
            transform: translateY(-3px);
            box-shadow: var(--shadow-lg);
        }

        .script-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 1rem;
        }

        .script-title {
            font-size: 1.25rem;
            font-weight: 600;
            color: var(--text-color);
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
            align-items: center;
            justify-content: center;
            z-index: 1000;
        }

        .modal-content {
            background: var(--card-bg);
            padding: 2rem;
            border-radius: var(--radius-lg);
            max-width: 500px;
            width: 90%;
            animation: slideIn 0.3s ease;
        }

        @keyframes slideIn {
            from { transform: translateY(-20px); opacity: 0; }
            to { transform: translateY(0); opacity: 1; }
        }

        /* Form Elements */
        .form-group {
            margin-bottom: 1.5rem;
        }

        .input {
            width: 100%;
            padding: 0.75rem;
            border: 1px solid #e5e7eb;
            border-radius: var(--radius-sm);
            font-size: 1rem;
        }

        .textarea {
            min-height: 100px;
            resize: vertical;
        }

        /* Responsive Design */
        @media (max-width: 768px) {
            .container {
                padding: 1rem;
            }

            .script-grid {
                grid-template-columns: 1fr;
            }

            .nav-container {
                flex-direction: column;
                gap: 1rem;
            }
        }
    </style>
</head>
<body>
    <header class="header">
        <div class="nav-container">
            <div class="user-section">
                <span id="userDisplay" class="user-display"></span>
            </div>
            <div class="button-group">
                <button id="loginButton" class="button button-primary">Login</button>
                <button id="createAccountButton" class="button button-secondary">Create Account</button>
                <button id="uploadScriptsButton" class="button button-primary" style="display: none;">Upload Script</button>
                <button id="logoutButton" class="button button-secondary" style="display: none;">Logout</button>
            </div>
        </div>
    </header>

    <main class="container">
        <div class="search-container">
            <input type="text" id="searchInput" class="search-input" placeholder="Search scripts...">
        </div>

        <div id="resultsContainer" class="script-grid">
            <!-- Scripts will be dynamically inserted here -->
        </div>
    </main>

    <!-- Login Modal -->
    <div id="loginModal" class="modal">
        <div class="modal-content">
            <h2>Login</h2>
            <form class="form-group">
                <input type="text" id="usernameInput" class="input" placeholder="Username">
                <input type="password" id="passwordInput" class="input" placeholder="Password">
                <button id="submitLogin" class="button button-primary">Login</button>
            </form>
        </div>
    </div>

    <!-- Create Account Modal -->
    <div id="createAccountModal" class="modal">
        <div class="modal-content">
            <h2>Create Account</h2>
            <form class="form-group">
                <input type="text" id="newUsernameInput" class="input" placeholder="Username">
                <input type="password" id="newPasswordInput" class="input" placeholder="Password">
                <button id="submitCreateAccount" class="button button-primary">Create Account</button>
            </form>
        </div>
    </div>

    <!-- Upload Script Modal -->
    <div id="uploadModal" class="modal">
        <div class="modal-content">
            <h2>Upload Script</h2>
            <form class="form-group">
                <input type="text" id="scriptName" class="input" placeholder="Script Name">
                <textarea id="scriptDescription" class="input textarea" placeholder="Script Description"></textarea>
                <textarea id="scriptCode" class="input textarea" placeholder="Paste your script here"></textarea>
                <div class="tags-container">
                    <!-- Tags will be dynamically inserted here -->
                </div>
                <button id="submitUpload" class="button button-primary">Upload</button>
            </form>
        </div>
    </div>

    <script>
        // Your existing JavaScript code here
    </script>
</body>
</html>
