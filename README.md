
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Background Image</title>
    <style>
        body {
            background-image: url(https://raw.githubusercontent.com/AlienCheats/AliencheatsScripts/refs/heads/main/wood-grain-texture-close-up-0410-5698738.webp');
            background-size: cover; /* Cover the entire viewport */
            background-position: center; /* Center the image */
            background-repeat: no-repeat; /* No repeat */
            height: 100vh; /* Full viewport height */
            margin: 0; /* Remove default margin */
            display: flex; /* Use flexbox for positioning */
            justify-content: center; /* Center horizontally */
            align-items: flex-start; /* Align items to the top */
            padding-top: 50px; /* Add padding to move the rectangle down */
            flex-direction: column; /* Stack items vertically */
        }

        .rounded-rectangle {
            background-color: rgba(255, 255, 255, 0.8); /* Semi-transparent white */
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
            background-color: rgba(255, 255, 255, 0.8); /* Semi-transparent white */
            border-radius: 10px; /* Rounded corners */
            text-align: center; /* Center text */
            margin-top: 10px; /* Margin above the label */
            padding: 10px; /* Padding inside the label */
            display: none; /* Initially hide the label */
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

    <script>
        const searchInput = document.getElementById('searchInput');
        const resultMessage = document.getElementById('resultMessage');
        const resultsMessage = document.getElementById('resultsMessage');
        const resultImage = document.getElementById('resultImage');
        const resultLabel = document.getElementById('resultLabel');

        searchInput.addEventListener('keypress', function(event) {
            if (event.key === 'Enter') {
                const keyword = searchInput.value.trim().toLowerCase();
                
                // Check for specific keywords
                if (keyword === '') {
                    resultMessage.textContent = ''; // Clear message if input is empty
                    resultsMessage.textContent = ''; // Clear results if input is empty
                    resultImage.style.display = 'none'; // Hide image if input is empty
                    resultLabel.style.display = 'none'; // Hide label if input is empty
                } else if (keyword === 'mm2') {
                    resultMessage.textContent = ''; // Clear previous messages
                    resultsMessage.textContent = `Results for "${keyword}"`; // Display results for the keyword
                    resultImage.style.display = 'block'; // Show image for mm2
                    resultLabel.style.display = 'block'; // Show label for mm2
                } else if (keyword === 'fisch') {
                    resultMessage.textContent = ''; // Clear previous messages
                    resultsMessage.textContent = `Results for "${keyword}"`; // Display results for the keyword
                    resultImage.style.display = 'none'; // Hide image for fisch (or you can set a different image if needed)
                    resultLabel.style.display = 'none'; // Hide label for fisch
                } else {
                    resultMessage.textContent = 'Nothing found here'; // Display message for no results
                    resultsMessage.textContent = ''; // Clear results if no match
                    resultImage.style.display = 'none'; // Hide image if no match
                    resultLabel.style.display = 'none'; // Hide label if no match
                }

                // Clear the input field after search
                searchInput.value = '';
            }
        });
    </script>
</body>
</html>
