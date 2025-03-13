# index.html
A <!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Name Rarity Checker</title>
    <style>
        :root {
            --primary: #4a6bff;
            --secondary: #3451d1;
            --background: #f5f7fa;
            --text: #2c3e50;
            --accent: #e74c3c;
            --light: #ecf0f1;
            --card-bg: rgba(255, 255, 255, 0.85);
        }
        
        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }
        
        body {
            color: var(--text);
            min-height: 100vh;
            display: flex;
            flex-direction: column;
            align-items: center;
            padding: 2rem 1rem;
            background: linear-gradient(135deg, #6e8efb, #a777e3);
            animation: gradientBG 15s ease infinite;
            background-size: 400% 400%;
            position: relative;
            overflow-x: hidden;
        }
        
        @keyframes gradientBG {
            0% { background-position: 0% 50%; }
            50% { background-position: 100% 50%; }
            100% { background-position: 0% 50%; }
        }
        
        /* Floating elements */
        .floating-element {
            position: absolute;
            background: rgba(255, 255, 255, 0.2);
            border-radius: 50%;
            z-index: -1;
            pointer-events: none;
        }
        
        .float-1 {
            width: 150px;
            height: 150px;
            top: 10%;
            left: 10%;
            animation: float 8s ease-in-out infinite;
        }
        
        .float-2 {
            width: 80px;
            height: 80px;
            top: 30%;
            right: 15%;
            animation: float 12s ease-in-out infinite;
        }
        
        .float-3 {
            width: 120px;
            height: 120px;
            bottom: 20%;
            left: 20%;
            animation: float 10s ease-in-out infinite;
        }
        
        .float-4 {
            width: 60px;
            height: 60px;
            bottom: 15%;
            right: 25%;
            animation: float 14s ease-in-out infinite;
        }
        
        .float-5 {
            width: 40px;
            height: 40px;
            top: 50%;
            left: 50%;
            animation: float 16s ease-in-out infinite;
        }
        
        @keyframes float {
            0% { transform: translateY(0) rotate(0deg); }
            50% { transform: translateY(-20px) rotate(5deg); }
            100% { transform: translateY(0) rotate(0deg); }
        }
        
        header {
            text-align: center;
            margin-bottom: 2rem;
            color: white;
            text-shadow: 0 2px 4px rgba(0, 0, 0, 0.2);
            animation: fadeIn 1s ease;
        }
        
        h1 {
            margin-bottom: 0.5rem;
            font-size: 2.5rem;
        }
        
        .container {
            max-width: 800px;
            width: 100%;
            background-color: var(--card-bg);
            backdrop-filter: blur(10px);
            border-radius: 16px;
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.15);
            padding: 2rem;
            border: 1px solid rgba(255, 255, 255, 0.3);
            animation: slideUp 0.8s ease;
            transition: transform 0.3s, box-shadow 0.3s;
        }
        
        .container:hover {
            transform: translateY(-5px);
            box-shadow: 0 15px 35px rgba(0, 0, 0, 0.2);
        }
        
        .name-form {
            display: flex;
            flex-direction: column;
            gap: 1rem;
            margin-bottom: 2rem;
        }
        
        .input-group {
            display: flex;
            flex-direction: column;
            gap: 0.5rem;
        }
        
        label {
            font-weight: 600;
            color: var(--text);
        }
        
        input {
            padding: 0.75rem;
            border: 2px solid rgba(0, 0, 0, 0.1);
            border-radius: 10px;
            font-size: 1rem;
            transition: all 0.3s;
            background: rgba(255, 255, 255, 0.9);
            box-shadow: 0 2px 10px rgba(0, 0, 0, 0.05);
        }
        
        input:focus {
            border-color: var(--primary);
            outline: none;
            box-shadow: 0 0 0 3px rgba(74, 107, 255, 0.3);
        }
        
        button {
            background-color: var(--primary);
            color: white;
            border: none;
            border-radius: 10px;
            padding: 0.75rem 1.5rem;
            font-size: 1rem;
            font-weight: 600;
            cursor: pointer;
            transition: all 0.3s;
            box-shadow: 0 4px 10px rgba(74, 107, 255, 0.3);
            position: relative;
            overflow: hidden;
        }
        
        button:hover {
            background-color: var(--secondary);
            transform: translateY(-2px);
            box-shadow: 0 6px 15px rgba(74, 107, 255, 0.4);
        }
        
        button:active {
            transform: translateY(1px);
        }
        
        button::after {
            content: '';
            position: absolute;
            top: 50%;
            left: 50%;
            width: 5px;
            height: 5px;
            background: rgba(255, 255, 255, 0.5);
            opacity: 0;
            border-radius: 100%;
            transform: scale(1, 1) translate(-50%, -50%);
            transform-origin: 50% 50%;
        }
        
        button:focus:not(:active)::after {
            animation: ripple 1s ease-out;
        }
        
        @keyframes ripple {
            0% {
                transform: scale(0, 0) translate(-50%, -50%);
                opacity: 0.5;
            }
            100% {
                transform: scale(20, 20) translate(-50%, -50%);
                opacity: 0;
            }
        }
        
        .result {
            display: none;
            margin-top: 2rem;
            padding: 1.5rem;
            border-radius: 12px;
            background-color: rgba(236, 240, 241, 0.8);
            text-align: center;
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.08);
            backdrop-filter: blur(5px);
            border: 1px solid rgba(255, 255, 255, 0.5);
        }
        
        .result.visible {
            display: block;
            animation: fadeIn 0.5s ease;
        }
        
        .rarity-meter {
            height: 2rem;
            background-color: rgba(238, 238, 238, 0.7);
            border-radius: 1rem;
            margin: 1rem 0;
            overflow: hidden;
            position: relative;
            box-shadow: inset 0 2px 5px rgba(0, 0, 0, 0.1);
        }
        
        .rarity-fill {
            height: 100%;
            background: linear-gradient(to right, #27ae60, #f39c12, #e74c3c);
            width: 0%;
            transition: width 1s ease-in-out;
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
        }
        
        .stats {
            display: flex;
            justify-content: space-around;
            margin-top: 1.5rem;
            flex-wrap: wrap;
            gap: 1rem;
        }
        
        .stat-card {
            background-color: rgba(255, 255, 255, 0.9);
            padding: 1.2rem;
            border-radius: 12px;
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.05);
            min-width: 120px;
            text-align: center;
            transition: transform 0.3s, box-shadow 0.3s;
            backdrop-filter: blur(5px);
            border: 1px solid rgba(255, 255, 255, 0.3);
        }
        
        .stat-card:hover {
            transform: translateY(-5px);
            box-shadow: 0 8px 25px rgba(0, 0, 0, 0.1);
        }
        
        .stat-number {
            font-size: 1.8rem;
            font-weight: 700;
            color: var(--primary);
            margin-bottom: 0.5rem;
        }
        
        .stat-label {
            font-size: 0.9rem;
            color: var(--text);
        }
        
        .history {
            margin-top: 2rem;
        }
        
        .history h3 {
            margin-bottom: 1rem;
            color: var(--text);
            position: relative;
            display: inline-block;
        }
        
        .history h3::after {
            content: '';
            position: absolute;
            width: 50%;
            height: 3px;
            background: var(--primary);
            bottom: -5px;
            left: 0;
            border-radius: 10px;
        }
        
        .name-tags {
            display: flex;
            flex-wrap: wrap;
            gap: 0.8rem;
        }
        
        .name-tag {
            background-color: rgba(255, 255, 255, 0.8);
            padding: 0.5rem 1rem;
            border-radius: 20px;
            font-size: 0.9rem;
            transition: all 0.3s;
            box-shadow: 0 2px 8px rgba(0, 0, 0, 0.05);
            border: 1px solid rgba(255, 255, 255, 0.5);
            cursor: pointer;
        }
        
        .name-tag:hover {
            transform: translateY(-3px) scale(1.05);
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.1);
            background-color: var(--primary);
            color: white;
        }
        
        .name-tag span {
            margin-left: 0.5rem;
            color: var(--primary);
            font-weight: 600;
            transition: color 0.3s;
        }
        
        .name-tag:hover span {
            color: white;
        }
        
        .clear-button {
            background-color: var(--accent);
            color: white;
            border: none;
            border-radius: 10px;
            padding: 0.5rem 1rem;
            font-size: 0.9rem;
            margin-top: 1rem;
            cursor: pointer;
            transition: all 0.3s;
        }
        
        .clear-button:hover {
            background-color: #c0392b;
        }
        
        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(10px); }
            to { opacity: 1; transform: translateY(0); }
        }
        
        @keyframes slideUp {
            from { opacity: 0; transform: translateY(30px); }
            to { opacity: 1; transform: translateY(0); }
        }
        
        footer {
            margin-top: 2rem;
            text-align: center;
            color: rgba(255, 255, 255, 0.8);
            font-size: 0.9rem;
            animation: fadeIn 1.5s ease;
        }
        
        .toast {
            position: fixed;
            bottom: 20px;
            left: 50%;
            transform: translateX(-50%);
            background-color: rgba(44, 62, 80, 0.9);
            color: white;
            padding: 1rem 2rem;
            border-radius: 30px;
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.2);
            z-index: 1000;
            opacity: 0;
            transition: opacity 0.3s;
        }
        
        .toast.visible {
            opacity: 1;
        }
    </style>
</head>
<body>
    <!-- Floating elements -->
    <div class="floating-element float-1"></div>
    <div class="floating-element float-2"></div>
    <div class="floating-element float-3"></div>
    <div class="floating-element float-4"></div>
    <div class="floating-element float-5"></div>
    
    <header>
        <h1>Name Rarity Checker</h1>
        <p>Discover how unique your name really is</p>
    </header>
    
    <div class="container">
        <form class="name-form" id="nameForm">
            <div class="input-group">
                <label for="nameInput">Enter your name:</label>
                <input type="text" id="nameInput" required placeholder="e.g. John, Sarah, etc.">
            </div>
            <button type="submit">Check Rarity</button>
        </form>
        
        <div class="result" id="result">
            <h2>Name Analysis: <span id="nameDisplay"></span></h2>
            <p>Rarity score:</p>
            <div class="rarity-meter">
                <div class="rarity-fill" id="rarityFill"></div>
            </div>
            <p id="rarityText"></p>
            
            <div class="stats">
                <div class="stat-card">
                    <div class="stat-number" id="percentile">-</div>
                    <div class="stat-label">Percentile</div>
                </div>
                <div class="stat-card">
                    <div class="stat-number" id="occurrences">-</div>
                    <div class="stat-label">Occurrences</div>
                </div>
                <div class="stat-card">
                    <div class="stat-number" id="totalNames">0</div>
                    <div class="stat-label">Total Names</div>
                </div>
            </div>
        </div>
        
        <div class="history">
            <h3>Recently checked names:</h3>
            <div class="name-tags" id="recentNames"></div>
            <button class="clear-button" id="clearHistory">Clear History</button>
        </div>
    </div>
    
    <div class="toast" id="toast"></div>
    
    <footer>
        <p>© 2025 Name Rarity Checker | Data is stored locally in your browser</p>
    </footer>
    
    <script>
        // DOM elements
        const nameForm = document.getElementById('nameForm');
        const nameInput = document.getElementById('nameInput');
        const result = document.getElementById('result');
        const nameDisplay = document.getElementById('nameDisplay');
        const rarityFill = document.getElementById('rarityFill');
        const rarityText = document.getElementById('rarityText');
        const percentileEl = document.getElementById('percentile');
        const occurrencesEl = document.getElementById('occurrences');
        const totalNamesEl = document.getElementById('totalNames');
        const recentNames = document.getElementById('recentNames');
        const clearHistoryBtn = document.getElementById('clearHistory');
        const toast = document.getElementById('toast');
        
        // Debounce function to improve performance
        function debounce(func, wait = 300) {
            let timeout;
            return function(...args) {
                clearTimeout(timeout);
                timeout = setTimeout(() => func.apply(this, args), wait);
            };
        }
        
        // Initialize local storage if not already
        function initializeDatabase() {
            if (!localStorage.getItem('nameDatabase')) {
                try {
                    // Initialize with some sample data
                    const initialData = {
                        names: {
                            'john': 15,
                            'mary': 12,
                            'david': 10,
                            'sarah': 8,
                            'michael': 14,
                            'james': 13,
                            'emma': 9,
                            'olivia': 7,
                            'william': 11,
                            'sophia': 6
                        },
                        totalSubmissions: 105,
                        recentSearches: ['john', 'mary', 'david', 'sarah', 'michael']
                    };
                    localStorage.setItem('nameDatabase', JSON.stringify(initialData));
                } catch (error) {
                    console.error('Error initializing database:', error);
                    showToast('Error initializing database. Please try again.');
                }
            } else {
                try {
                    // Ensure the database has the recentSearches field
                    const data = JSON.parse(localStorage.getItem('nameDatabase'));
                    if (!data.recentSearches) {
                        data.recentSearches = [];
                    }
                    // Ensure all required properties exist
                    if (!data.names) {
                        data.names = {};
                    }
                    if (typeof data.totalSubmissions !== 'number') {
                        data.totalSubmissions = Object.values(data.names).reduce((sum, count) => sum + count, 0) || 0;
                    }
                    localStorage.setItem('nameDatabase', JSON.stringify(data));
                } catch (error) {
                    console.error('Error validating database:', error);
                    resetDatabase();
                }
            }
        }
        
        // Reset database if corrupted
        function resetDatabase() {
            try {
                const initialData = {
                    names: {},
                    totalSubmissions: 0,
                    recentSearches: []
                };
                localStorage.setItem('nameDatabase', JSON.stringify(initialData));
                showToast('Database reset due to corruption. Starting fresh.');
            } catch (error) {
                console.error('Failed to reset database:', error);
            }
        }
        
        // Safely get database
        function getDatabase() {
            try {
                return JSON.parse(localStorage.getItem('nameDatabase')) || { names: {}, totalSubmissions: 0, recentSearches: [] };
            } catch (error) {
                resetDatabase();
                return { names: {}, totalSubmissions: 0, recentSearches: [] };
            }
        }
        
        // Safely save database
        function saveDatabase(data) {
            try {
                localStorage.setItem('nameDatabase', JSON.stringify(data));
                return true;
            } catch (error) {
                console.error('Error saving to database:', error);
                showToast('Error saving data. Your browser storage might be full.');
                return false;
            }
        }
        
        // Show toast message
        function showToast(message, duration = 3000) {
            toast.textContent = message;
            toast.classList.add('visible');
            
            // Clear any existing timeouts
            if (toast.hideTimeout) {
                clearTimeout(toast.hideTimeout);
            }
            
            // Set new timeout
            toast.hideTimeout = setTimeout(() => {
                toast.classList.remove('visible');
            }, duration);
        }
        
        // Load and display recent names with performance optimization
        function loadRecentNames() {
            const data = getDatabase();
            
            // Use recent searches if available, otherwise use top names
            let namesToShow;
            if (data.recentSearches && data.recentSearches.length > 0) {
                namesToShow = data.recentSearches.map(name => [name, data.names[name] || 0]);
            } else {
                namesToShow = Object.entries(data.names || {})
                    .sort((a, b) => b[1] - a[1])
                    .slice(0, 8);
            }
            
            // Clear existing content
            recentNames.innerHTML = '';
            
            if (namesToShow.length === 0) {
                const noNames = document.createElement('p');
                noNames.textContent = 'No names checked yet.';
                recentNames.appendChild(noNames);
                return;
            }
            
            // Use document fragment for better performance
            const fragment = document.createDocumentFragment();
            
            namesToShow.forEach(([name, count]) => {
                if (!name) return; // Skip empty names
                
                const tag = document.createElement('div');
                tag.className = 'name-tag';
                tag.dataset.name = name;
                
                // Capitalize the name properly
                const displayName = name.split(' ')
                    .map(part => part.charAt(0).toUpperCase() + part.slice(1).toLowerCase())
                    .join(' ');
                
                tag.textContent = displayName;
                
                const countSpan = document.createElement('span');
                countSpan.textContent = count;
                tag.appendChild(countSpan);
                
                // Add click event to reuse the name
                tag.addEventListener('click', () => {
                    nameInput.value = displayName;
                    nameForm.dispatchEvent(new Event('submit'));
                });
                
                fragment.appendChild(tag);
            });
            
            recentNames.appendChild(fragment);
            totalNamesEl.textContent = data.totalSubmissions || 0;
        }
        
        // Calculate name rarity with validation
        function calculateRarity(name) {
            if (!name || !name.trim()) {
                return null;
            }
            
            const data = getDatabase();
            const normalizedName = name.toLowerCase().trim();
            
            // Add to recent searches
            if (!data.recentSearches) {
                data.recentSearches = [];
            }
            
            // Remove if already exists
            const existingIndex = data.recentSearches.indexOf(normalizedName);
            if (existingIndex !== -1) {
                data.recentSearches.splice(existingIndex, 1);
            }
            
            // Add to beginning of array
            data.recentSearches.unshift(normalizedName);
            
            // Keep only the 8 most recent
            if (data.recentSearches.length > 8) {
                data.recentSearches = data.recentSearches.slice(0, 8);
            }
            
            // Update the database with the new name
            if (!data.names) {
                data.names = {};
            }
            
            if (data.names[normalizedName]) {
                data.names[normalizedName]++;
            } else {
                data.names[normalizedName] = 1;
            }
            
            if (!data.totalSubmissions) {
                data.totalSubmissions = 0;
            }
            data.totalSubmissions++;
            
            // Save changes
            if (!saveDatabase(data)) {
                return null;
            }
            
            // Calculate rarity stats
            const occurrences = data.names[normalizedName];
            const frequency = occurrences / data.totalSubmissions;
            const percentile = Math.round((1 - frequency) * 100);
            
            // Interpret rarity
            let rarityDescription;
            if (percentile > 95) {
                rarityDescription = "Extremely rare! You have a truly unique name.";
            } else if (percentile > 85) {
                rarityDescription = "Very rare. Your name stands out from the crowd.";
            } else if (percentile > 70) {
                rarityDescription = "Uncommon. Your name is distinctive.";
            } else if (percentile > 50) {
                rarityDescription = "Moderately common. Your name has a good balance.";
            } else if (percentile > 30) {
                rarityDescription = "Common. Your name is familiar to many.";
            } else if (percentile > 10) {
                rarityDescription = "Very common. Your name is widely recognized.";
            } else {
                rarityDescription = "Extremely common. Your name is among the most popular.";
            }
            
            return {
                name: normalizedName,
                displayName: name.trim(),
                occurrences,
                percentile,
                rarityDescription,
                totalNames: data.totalSubmissions
            };
        }
        
        // Limit number of floating elements for better performance
        function addFloatingElements() {
            const maxElements = window.innerWidth < 768 ? 3 : 5; // Fewer on mobile
            const container = document.body;
            
            for (let i = 0; i < maxElements; i++) {
                const element = document.createElement('div');
                element.className = `floating-element float-extra-${i}`;
                element.style.width = `${20 + Math.random() * 40}px`;
                element.style.height = element.style.width;
                element.style.top = `${Math.random() * 100}%`;
                element.style.left = `${Math.random() * 100}%`;
                element.style.opacity = `${0.1 + Math.random() * 0.2}`;
                element.style.animation = `float ${8 + Math.random() * 10}s ease-in-out infinite`;
                element.style.animationDelay = `${Math.random() * 5}s`;
                container.appendChild(element);
            }
        }
        
        // Clear history handler with confirmation
        clearHistoryBtn.addEventListener('click', function() {
            try {
                const data = getDatabase();
                data.recentSearches = [];
                saveDatabase(data);
                loadRecentNames();
                showToast('Search history cleared!');
            } catch (error) {
                console.error('Error clearing history:', error);
                showToast('Error clearing history. Please try again.');
            }
        });
        
        // Form submission with validation and error handling
        nameForm.addEventListener('submit', function(e) {
            e.preventDefault();
            
            try {
                const name = nameInput.value;
                
                if (!name.trim()) {
                    showToast('Please enter a name');
                    return;
                }
                
                // Limit name length for performance
                if (name.length > 50) {
                    showToast('Name is too long. Please use a shorter name.');
                    return;
                }
                
                const rarityInfo = calculateRarity(name);
                
                if (!rarityInfo) {
                    showToast('Error calculating rarity. Please try again.');
                    return;
                }
                
                // Display results
                nameDisplay.textContent = rarityInfo.displayName;
                rarityFill.style.width = `${rarityInfo.percentile}%`;
                rarityText.textContent = rarityInfo.rarityDescription;
                percentileEl.textContent = `${rarityInfo.percentile}%`;
                occurrencesEl.textContent = rarityInfo.occurrences;
                totalNamesEl.textContent = rarityInfo.totalNames;
                
                result.classList.add('visible');
                
                // Refresh recent names
                loadRecentNames();
                
                // Scroll to results if they're not visible - with smooth scrolling fallback
                if (!isElementInViewport(result)) {
                    try {
                        result.scrollIntoView({ behavior: 'smooth', block: 'nearest' });
                    } catch (error) {
                        // Fallback for browsers that don't support smooth scrolling
                        result.scrollIntoView(false);
                    }
                }
            } catch (error) {
                console.error('Error processing form submission:', error);
                showToast('An unexpected error occurred. Please try again.');
            }
        });
        
        // Check if element is in viewport - improved version
        function isElementInViewport(el) {
            if (!el) return false;
            
            try {
                const rect = el.getBoundingClientRect();
                const windowHeight = window.innerHeight || document.documentElement.clientHeight;
                const windowWidth = window.innerWidth || document.documentElement.clientWidth;
                
                // Check if at least half of the element is in the viewport
                const vertInView = (rect.top <= windowHeight) && ((rect.top + rect.height/2) >= 0);
                const horInView = (rect.left <= windowWidth) && ((rect.left + rect.width/2) >= 0);
                
                return vertInView && horInView;
            } catch (error) {
                console.error('Error checking viewport visibility:', error);
                return false;
            }
        }
        
        // Handle input changes with debounce for better performance
        nameInput.addEventListener('input', debounce(function() {
            // Optional: implement real-time suggestions or validation here
        }, 300));
        
        // Add event listener for page load errors
        window.addEventListener('error', function(event) {
            console.error('Page error:', event.error);
            showToast('An error occurred. Please refresh the page.');
        });
        
        // Initialize app
        document.addEventListener('DOMContentLoaded', function() {
            try {
                initializeDatabase();
                loadRecentNames();
                
                // Delay adding floating elements for better initial page load
                setTimeout(addFloatingElements, 500);
                
                // Focus on input field for better UX
                nameInput.focus();
            } catch (error) {
                console.error('Error initializing app:', error);
                showToast('Error initializing the application. Please refresh the page.');
            }
        });
        
        // Initialize immediately in case DOMContentLoaded already fired
        if (document.readyState === 'complete' || document.readyState === 'interactive') {
            try {
                initializeDatabase();
                loadRecentNames();
                setTimeout(addFloatingElements, 500);
            } catch (error) {
                console.error('Error in immediate initialization:', error);
            }
        }
    </script>
</body>
</html>
Website which checks the Rarity of Your Name
