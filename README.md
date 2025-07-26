-by Asifa
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>VUI Survey: Interactive Product Experience</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <style>
        body {
            font-family: 'Inter', sans-serif;
        }
        .product-card {
            transition: all 0.3s ease;
        }
        .product-card:hover {
            transform: translateY(-5px);
            box-shadow: 0 10px 20px rgba(0,0,0,0.1);
        }
        .nav-button.active {
            background-color: #2563eb;
            color: white;
            box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
        }
        .voice-active {
            animation: pulse 2s infinite;
        }
        @keyframes pulse {
            0% { box-shadow: 0 0 0 0 rgba(37, 99, 235, 0.4); }
            70% { box-shadow: 0 0 0 10px rgba(37, 99, 235, 0); }
            100% { box-shadow: 0 0 0 0 rgba(37, 99, 235, 0); }
        }
        .speech-text {
            animation: fadeIn 0.5s ease-in-out;
        }
        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(10px); }
            to { opacity: 1; transform: translateY(0); }
        }
        .speech-display-container {
            position: sticky;
            top: 0;
            z-index: 10;
            background-color: white;
            padding: 1rem;
            border-bottom: 1px solid #e5e7eb;
        }
        @media (max-width: 640px) {
            .product-card img {
                height: 120px;
            }
            .nav-button {
                padding: 0.5rem 0.8rem;
                font-size: 0.8rem;
            }
        }
        @media (min-width: 641px) and (max-width: 1024px) {
            .product-card img {
                height: 150px;
            }
        }
    </style>
</head>
<body class="bg-gradient-to-br from-blue-50 to-indigo-100 min-h-screen flex items-center justify-center py-4 sm:py-8 px-4 sm:px-6 lg:px-8">
    <div class="max-w-5xl w-full bg-white rounded-xl shadow-2xl overflow-hidden">
        <!-- Sticky Header -->
        <div class="speech-display-container">
            <div id="speechDisplay" class="w-full bg-white rounded-lg p-3 text-center text-sm sm:text-base text-gray-800 flex items-center justify-center min-h-[60px]">
                <span id="currentSpeechText">Welcome to voice experience. Hover over products or click the microphone.</span>
            </div>
        </div>

        <!-- Main Content -->
        <div class="p-4 md:p-8 lg:p-10 space-y-6 md:space-y-8 overflow-y-auto max-h-[80vh]">
            <header class="text-center space-y-2">
                <h1 class="text-2xl sm:text-3xl md:text-4xl font-bold text-gray-900">VUI Survey: Interactive Product Experience</h1>
                <p class="text-sm sm:text-base text-gray-600 max-w-2xl mx-auto">
                    Explore our products using two different interfaces. Your feedback will help improve voice technology.
                </p>
            </header>

            <nav class="flex justify-center gap-2 sm:gap-4">
                <button id="voiceEnabledBtn" class="nav-button px-4 sm:px-6 py-2 rounded-full text-sm sm:text-base font-medium transition-all bg-blue-600 text-white shadow hover:bg-blue-700 focus:outline-none focus:ring-2 focus:ring-blue-500 focus:ring-offset-2 active" onclick="showSection('voiceEnabledSection')">
                    <span class="flex items-center">
                        <svg xmlns="http://www.w3.org/2000/svg" class="h-4 w-4 mr-1" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19 11a7 7 0 01-7 7m0 0a7 7 0 01-7-7m7 7v4m0 0H8m4 0h4m-4-8a3 3 0 01-3-3V5a3 3 0 116 0v6a3 3 0 01-3 3z" />
                        </svg>
                        Voice Experience
                    </span>
                </button>
                <button id="standardBtn" class="nav-button px-4 sm:px-6 py-2 rounded-full text-sm sm:text-base font-medium transition-all bg-gray-200 text-gray-800 shadow hover:bg-gray-300 focus:outline-none focus:ring-2 focus:ring-gray-400 focus:ring-offset-2" onclick="showSection('standardSection')">
                    <span class="flex items-center">
                        <svg xmlns="http://www.w3.org/2000/svg" class="h-4 w-4 mr-1" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9.75 17L9 20l-1 1h8l-1-1-.75-3M3 13h18M5 17h14a2 2 0 002-2V5a2 2 0 00-2-2H5a2 2 0 00-2 2v10a2 2 0 002 2z" />
                        </svg>
                        Standard Experience
                    </span>
                </button>
            </nav>

            <!-- Voice Enabled Section -->
            <section id="voiceEnabledSection" class="section space-y-6">
                <div class="flex flex-col items-center space-y-4">
                    <button id="voiceControlBtn" class="px-6 py-3 rounded-full text-sm sm:text-base font-medium bg-blue-600 text-white shadow-lg hover:bg-blue-700 focus:outline-none focus:ring-2 focus:ring-blue-500 focus:ring-offset-2 flex items-center transition-all" onclick="toggleVoiceControl()">
                        <svg id="micIcon" xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 mr-2" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19 11a7 7 0 01-7 7m0 0a7 7 0 01-7-7m7 7v4m0 0H8m4 0h4m-4-8a3 3 0 01-3-3V5a3 3 0 116 0v6a3 3 0 01-3 3z" />
                        </svg>
                        <span id="voiceControlText">Start Voice Control</span>
                    </button>
                    
                    <div id="voiceStatus" class="text-xs sm:text-sm text-gray-600 flex items-center">
                        <svg xmlns="http://www.w3.org/2000/svg" class="h-4 w-4 mr-1" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M13 16h-1v-4h-1m1-4h.01M21 12a9 9 0 11-18 0 9 9 0 0118 0z" />
                        </svg>
                        <span>Click the microphone and speak clearly</span>
                    </div>
                </div>

                <div class="bg-blue-100 border border-blue-300 rounded-lg p-4">
                    <h3 class="font-semibold text-blue-800 text-sm sm:text-base mb-2 flex items-center">
                        <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 mr-1" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M8.228 9c.549-1.165 2.03-2 3.772-2 2.21 0 4 1.343 4 3 0 1.4-1.278 2.575-3.006 2.907-.542.104-.994.54-.994 1.093m0 3h.01M21 12a9 9 0 11-18 0 9 9 0 0118 0z" />
                        </svg>
                        Voice Command Guide
                    </h3>
                    <ul class="text-xs sm:text-sm text-blue-800 space-y-1">
                        <li><strong>"Show me [product]"</strong> - Hear product description</li>
                        <li><strong>"Add [product] to cart"</strong> - Add product to cart</li>
                        <li><strong>"How much is [product]?"</strong> - Hear product price</li>
                        <li><strong>"Help"</strong> - List all commands</li>
                        <li><strong>"Suggest something"</strong> - Get a recommendation</li>
                    </ul>
                </div>

                <div id="voiceProductGrid" class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-4 md:gap-6">
                    <!-- Product cards will be injected here by JavaScript -->
                </div>
            </section>

            <!-- Standard Web Section -->
            <section id="standardSection" class="section hidden space-y-6">
                <div class="bg-gray-50 border border-gray-200 rounded-lg p-4 text-center">
                    <h3 class="text-lg sm:text-xl font-medium text-gray-800 mb-2">Standard Product Browsing</h3>
                    <p class="text-xs sm:text-sm text-gray-600">Browse products using traditional clicks and taps</p>
                </div>

                <div id="standardProductGrid" class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-4 md:gap-6">
                    <!-- Product cards will be injected here by JavaScript -->
                </div>
            </section>

            <!-- Feedback Section -->
            <section class="bg-purple-50 border border-purple-200 rounded-lg p-4 md:p-6 text-center space-y-4">
                <div class="space-y-2">
                    <h3 class="text-lg sm:text-xl font-bold text-purple-800">Your Feedback Matters</h3>
                    <p class="text-xs sm:text-sm text-gray-700 max-w-2xl mx-auto">
                        Please share your experience with both interfaces to help improve voice technology.
                    </p>
                </div>
                <a href="https://docs.google.com/forms/d/e/1FAIpQLSeFCjyJuN3j2L4Yr8MUz5WsmNBHgoYkfszLmIFoUOVIj4QJOQ/viewform?usp=header" target="_blank" rel="noopener noreferrer" class="inline-flex items-center px-5 py-3 bg-purple-600 hover:bg-purple-700 text-white text-sm sm:text-base font-medium rounded-full shadow transition-all transform hover:scale-105 focus:outline-none focus:ring-2 focus:ring-purple-500 focus:ring-offset-2">
                    <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 mr-2" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 12h6m-6 4h6m2 5H7a2 2 0 01-2-2V5a2 2 0 012-2h5.586a1 1 0 01.707.293l5.414 5.414a1 1 0 01.293.707V19a2 2 0 01-2 2z" />
                    </svg>
                    Provide Feedback
                </a>
            </section>
        </div>
    </div>

    <script>
        // Product Data with working image URLs
        const products = [
            {
                id: 'p1',
                name: 'Smartwatch',
                keywords: ['watch', 'smart watch', 'smart watch', 'wrist watch', 'fitness tracker'],
                description: 'This smartwatch tracks your fitness, receives notifications, and makes calls directly from your wrist. It features a vibrant AMOLED display and a long-lasting battery.',
                price: '$199.99',
                image: 'https://images.unsplash.com/photo-1523275335684-37898b6baf30?ixlib=rb-1.2.1&auto=format&fit=crop&w=500&q=60'
            },
            {
                id: 'p2',
                name: 'Wireless Earbuds',
                keywords: ['earbuds', 'earphones', 'headphones', 'wireless headphones', 'bluetooth earbuds'],
                description: 'These wireless earbuds offer immersive sound with active noise cancellation. They are perfect for music lovers and calls on the go, and come with a portable charging case.',
                price: '$129.00',
                image: 'https://images.unsplash.com/photo-1590658268037-6bf12165a8df?ixlib=rb-1.2.1&auto=format&fit=crop&w=500&q=60'
            },
            {
                id: 'p3',
                name: 'Bluetooth Speaker',
                keywords: ['speaker', 'portable speaker', 'bluetooth speaker', 'wireless speaker', 'music speaker'],
                description: 'This portable Bluetooth speaker delivers powerful sound in a compact design. It is waterproof and durable, ideal for outdoor adventures, and connects seamlessly via Bluetooth.',
                price: '$79.50',
                image: 'https://images.unsplash.com/photo-1572569511254-d8f925fe2cbb?ixlib=rb-1.2.1&auto=format&fit=crop&w=500&q=60'
            },
            {
                id: 'p4',
                name: 'Office Chair',
                keywords: ['chair', 'desk chair', 'ergonomic chair', 'computer chair', 'work chair'],
                description: 'This ergonomic office chair is designed for maximum comfort and support during long working hours. It features adjustable lumbar support and breathable mesh material.',
                price: '$249.00',
                image: 'https://images.unsplash.com/photo-1517705008128-361805f42e86?ixlib=rb-1.2.1&auto=format&fit=crop&w=500&q=60'
            },
            {
                id: 'p5',
                name: 'Laptop',
                keywords: ['notebook', 'computer', 'macbook', 'ultrabook', 'portable computer'],
                description: 'This high-performance laptop features a blazing fast processor and a stunning display for both work and entertainment. It has a lightweight design for ultimate portability.',
                price: '$1199.00',
                image: 'https://images.unsplash.com/photo-1496181133206-80ce9b88a853?ixlib=rb-1.2.1&auto=format&fit=crop&w=500&q=60'
            },
            {
                id: 'p6',
                name: 'Smart Home Hub',
                keywords: ['hub', 'smart hub', 'home automation', 'smart home', 'iot hub'],
                description: 'This smart home hub allows you to control all your smart devices from one central hub. It is compatible with various smart home ecosystems for seamless integration.',
                price: '$89.99',
                image: 'https://images.unsplash.com/photo-1556740738-b6a63e27c4df?ixlib=rb-1.2.1&auto=format&fit=crop&w=500&q=60'
            }
        ];

        // Voice Interaction Variables
        let recognition = null;
        let isListening = false;
        let currentUtterance = null;
        const commandKeywords = {
            'show': 'describe',
            'view': 'describe',
            'describe': 'describe',
            'tell me about': 'describe',
            'what is': 'describe',
            'add': 'add_to_cart',
            'buy': 'add_to_cart',
            'purchase': 'add_to_cart',
            'price': 'get_price',
            'cost': 'get_price',
            'how much': 'get_price',
            'what does it cost': 'get_price',
            'suggest': 'suggest',
            'recommend': 'suggest',
            'help': 'help',
            'what can i say': 'help'
        };

        // Initialize the page
        document.addEventListener('DOMContentLoaded', function() {
            renderProductCards('voiceProductGrid', true);
            renderProductCards('standardProductGrid', false);
            showSection('voiceEnabledSection');
            
            // Welcome message
            setTimeout(() => {
                speakText("Welcome to the voice interactive experience. Hover over products to hear their descriptions or click the microphone button to use voice commands.", true);
            }, 1000);
        });

        // Render product cards
        function renderProductCards(containerId, isVoiceEnabled) {
            const container = document.getElementById(containerId);
            container.innerHTML = '';

            products.forEach(product => {
                const card = document.createElement('div');
                card.className = 'product-card bg-white rounded-lg p-4 shadow-md border border-gray-200 flex flex-col';
                
                if (isVoiceEnabled) {
                    card.onmouseenter = () => {
                        updateSpeechDisplay(product.description);
                        speakText(product.description, false);
                    };
                    card.onmouseleave = stopSpeaking;
                    card.classList.add('cursor-pointer');
                }

                card.innerHTML = `
                    <img src="${product.image}" alt="${product.name}" class="rounded-md mb-3 w-full h-40 sm:h-48 object-cover">
                    <h3 class="text-base sm:text-lg font-semibold text-gray-800 mb-1">${product.name}</h3>
                    <p class="text-xs sm:text-sm text-gray-600 mb-3 flex-grow">${product.description}</p>
                    <div class="mt-auto">
                        <p class="text-lg sm:text-xl font-bold text-blue-700 mb-3">${product.price}</p>
                        <div class="flex space-x-2">
                            <button class="flex-1 px-3 py-1 sm:px-4 sm:py-2 rounded-md bg-blue-500 text-white text-xs sm:text-sm font-medium hover:bg-blue-600 transition-colors"
                                onclick="handleButtonClick('view', '${product.id}', ${isVoiceEnabled})">
                                Details
                            </button>
                            <button class="flex-1 px-3 py-1 sm:px-4 sm:py-2 rounded-md bg-green-500 text-white text-xs sm:text-sm font-medium hover:bg-green-600 transition-colors"
                                onclick="handleButtonClick('add_to_cart', '${product.id}', ${isVoiceEnabled})">
                                Add to Cart
                            </button>
                        </div>
                    </div>
                `;
                container.appendChild(card);
            });
        }

        // Update speech display
        function updateSpeechDisplay(text) {
            const currentText = document.getElementById('currentSpeechText');
            currentText.textContent = text;
            currentText.classList.add('speech-text');
            
            setTimeout(() => {
                currentText.classList.remove('speech-text');
            }, 500);
        }

        // Text-to-speech function
        function speakText(text, isFinal = true) {
            if ('speechSynthesis' in window) {
                if (currentUtterance) {
                    window.speechSynthesis.cancel();
                }
                
                updateSpeechDisplay(text);
                
                currentUtterance = new SpeechSynthesisUtterance(text);
                currentUtterance.lang = 'en-US';
                currentUtterance.rate = 1.0; // Normal speed for better clarity
                currentUtterance.pitch = 1.0;
                
                if (isFinal) {
                    currentUtterance.onend = function() {
                        // Occasionally remind about feedback
                        if (Math.random() > 0.7) {
                            setTimeout(() => {
                                speakText("Remember to share your feedback about this experience. Kindly fill the form by clicking the link below when you're done.", true);
                            }, 2000);
                        }
                    };
                }
                
                window.speechSynthesis.speak(currentUtterance);
            } else {
                updateSpeechDisplay(text);
            }
        }

        function stopSpeaking() {
            if ('speechSynthesis' in window && currentUtterance) {
                window.speechSynthesis.cancel();
                currentUtterance = null;
            }
        }

        // Voice control toggle
        function toggleVoiceControl() {
            const voiceControlBtn = document.getElementById('voiceControlBtn');
            const voiceControlText = document.getElementById('voiceControlText');
            const micIcon = document.getElementById('micIcon');
            const voiceStatus = document.getElementById('voiceStatus');

            if (!('webkitSpeechRecognition' in window || 'SpeechRecognition' in window)) {
                voiceStatus.innerHTML = '<span class="text-red-600">Voice control not supported in your browser</span>';
                voiceControlBtn.disabled = true;
                speakText("Sorry, voice control is not supported in your browser.", true);
                return;
            }

            if (!recognition) {
                recognition = new (window.webkitSpeechRecognition || window.SpeechRecognition)();
                recognition.interimResults = false;
                recognition.lang = 'en-US';
                recognition.continuous = true;
                recognition.maxAlternatives = 3; // Get more alternatives for better matching

                recognition.onstart = () => {
                    isListening = true;
                    voiceControlBtn.classList.add('voice-active', 'bg-red-600', 'hover:bg-red-700');
                    voiceControlBtn.classList.remove('bg-blue-600', 'hover:bg-blue-700');
                    voiceControlText.textContent = 'Listening...';
                    micIcon.innerHTML = '<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15.536 8.464a5 5 0 010 7.072m2.828-9.9a9 9 0 010 12.728M5.586 15.536a5 5 0 001.414 1.414m9.9-2.828a9 9 0 001.414 1.414" />';
                    voiceStatus.innerHTML = '<span class="text-green-600">Speak now - I\'m listening</span>';
                    stopSpeaking();
                    speakText("I'm listening. You can speak now.", true);
                };

                recognition.onresult = (event) => {
                    const results = event.results[event.results.length - 1];
                    const transcript = results[0].transcript;
                    updateSpeechDisplay(transcript);
                    
                    // Try all alternatives for better matching
                    for (let i = 0; i < results.length; i++) {
                        const processed = processVoiceCommand(results[i].transcript.toLowerCase());
                        if (processed) break; // Stop if we found a match
                    }
                };

                recognition.onerror = (event) => {
                    console.error('Speech recognition error:', event.error);
                    voiceStatus.innerHTML = '<span class="text-red-600">Error: ' + event.error + '. Please try again.</span>';
                    isListening = false;
                    resetVoiceUI();
                    speakText("Sorry, there was an error. Please try again.", true);
                };

                recognition.onend = () => {
                    if (isListening) {
                        recognition.start(); // Continue listening
                    } else {
                        resetVoiceUI();
                    }
                };
            }

            if (isListening) {
                recognition.stop();
                isListening = false;
                speakText("Voice control turned off.", true);
            } else {
                recognition.start();
            }
        }

        function resetVoiceUI() {
            const voiceControlBtn = document.getElementById('voiceControlBtn');
            const voiceControlText = document.getElementById('voiceControlText');
            const micIcon = document.getElementById('micIcon');
            const voiceStatus = document.getElementById('voiceStatus');

            voiceControlBtn.classList.remove('voice-active', 'bg-red-600', 'hover:bg-red-700');
            voiceControlBtn.classList.add('bg-blue-600', 'hover:bg-blue-700');
            voiceControlText.textContent = 'Start Voice Control';
            micIcon.innerHTML = '<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19 11a7 7 0 01-7 7m0 0a7 7 0 01-7-7m7 7v4m0 0H8m4 0h4m-4-8a3 3 0 01-3-3V5a3 3 0 116 0v6a3 3 0 01-3 3z" />';
            voiceStatus.innerHTML = '<span>Click the microphone and speak clearly</span>';
        }

        // Process voice commands with better matching
        function processVoiceCommand(command) {
            console.log('Processing command:', command);
            stopSpeaking();

            // Check for help command first
            if (command.includes('help') || command.includes('what can i say')) {
                const helpText = "You can say commands like: 'Show me the smartwatch', 'Add earbuds to cart', " +
                    "'How much is the laptop?', 'What is the price of the chair?', or 'Suggest a product'. " +
                    "You can also use simpler terms like 'watch' for smartwatch or 'speaker' for bluetooth speaker.";
                speakText(helpText, true);
                return true;
            }

            // Check for suggestion command
            if (command.includes('suggest') || command.includes('recommend')) {
                const randomProduct = products[Math.floor(Math.random() * products.length)];
                speakText(`I recommend the ${randomProduct.name}. ${randomProduct.description} It costs ${randomProduct.price}.`, true);
                return true;
            }

            // Find the action and product
            let action = null;
            let product = null;
            
            // First find the action keyword
            for (const [keyword, actionType] of Object.entries(commandKeywords)) {
                if (command.includes(keyword)) {
                    action = actionType;
                    break;
                }
            }

            // Then find the product by checking both name and keywords
            for (const p of products) {
                // Check if command includes the product name (case insensitive)
                if (command.includes(p.name.toLowerCase())) {
                    product = p;
                    break;
                }
                
                // Check all keywords for this product
                for (const keyword of p.keywords) {
                    if (command.includes(keyword)) {
                        product = p;
                        break;
                    }
                }
                
                if (product) break;
            }

            // Execute the appropriate action
            if (product) {
                if (action === 'describe') {
                    speakText(`${product.name}. ${product.description} The price is ${product.price}.`, true);
                    return true;
                } else if (action === 'add_to_cart') {
                    speakText(`Added ${product.name} to your cart. The price is ${product.price}.`, true);
                    return true;
                } else if (action === 'get_price') {
                    speakText(`The price of ${product.name} is ${product.price}.`, true);
                    return true;
                } else {
                    // If we found a product but no clear action, describe it
                    speakText(`I found ${product.name}. ${product.description} The price is ${product.price}.`, true);
                    return true;
                }
            }

            // If we got this far, we didn't understand
            if (action && !product) {
                speakText(`I heard you want to ${action.replace('_', ' ')}, but I didn't recognize the product. Please try again.`, true);
            } else if (!action && product) {
                speakText(`I found ${product.name}. What would you like to know about it? You can ask for details or price.`, true);
            } else {
                speakText("I didn't understand that. You can say things like 'Show me the smartwatch', 'Add earbuds to cart', or 'How much is the laptop?'. Say 'Help' for more commands.", true);
            }
            return false;
        }

        // Handle button clicks
        function handleButtonClick(actionType, productId, isVoiceEnabledSection) {
            const product = products.find(p => p.id === productId);
            if (!product) return;

            if (isVoiceEnabledSection) {
                let voiceMessage = '';
                if (actionType === 'view') {
                    voiceMessage = `You viewed ${product.name}. ${product.description}`;
                } else if (actionType === 'add_to_cart') {
                    voiceMessage = `Added ${product.name} to your cart. The price is ${product.price}.`;
                }
                speakText(voiceMessage, true);
            }
        }

        // Switch between sections
        function showSection(sectionId) {
            document.querySelectorAll('.section').forEach(section => {
                section.classList.add('hidden');
            });
            document.getElementById(sectionId).classList.remove('hidden');

            document.getElementById('voiceEnabledBtn').classList.remove('active', 'bg-blue-600', 'text-white');
            document.getElementById('standardBtn').classList.remove('active', 'bg-blue-600', 'text-white');
            
            const activeButton = document.getElementById(sectionId === 'voiceEnabledSection' ? 'voiceEnabledBtn' : 'standardBtn');
            activeButton.classList.add('active', 'bg-blue-600', 'text-white');

            stopSpeaking();
            if (recognition && isListening) {
                recognition.stop();
                isListening = false;
                resetVoiceUI();
            }

            if (sectionId === 'voiceEnabledSection') {
                updateSpeechDisplay("Welcome to voice experience. Hover over products or click the microphone.");
            }
        }
    </script>
</body>
</html>
