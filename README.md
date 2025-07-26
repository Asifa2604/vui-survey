-by Asifa
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>VUI Survey: Interactive Product Experience</title>
    <!-- Tailwind CSS CDN for advanced UI -->
    <script src="https://cdn.tailwindcss.com"></script>
    <style>
        /* Custom styles for better readability or specific overrides */
        body {
            font-family: 'Inter', sans-serif; /* A modern sans-serif font */
        }
        .product-card {
            transition: transform 0.2s ease-in-out, box-shadow 0.2s ease-in-out;
        }
        .product-card:hover {
            transform: translateY(-5px);
            box-shadow: 0 15px 25px rgba(0,0,0,0.15);
        }
        .product-card img {
            object-fit: cover;
            height: 200px; /* Fixed height for images */
            width: 100%;
            border-radius: 0.5rem; /* Rounded corners for images */
        }
        /* Custom active state for buttons */
        .nav-button.active {
            background-color: #0056b3; /* Darker blue for active */
            color: white;
            box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
        }
    </style>
</head>
<body class="bg-gradient-to-br from-blue-50 to-indigo-100 min-h-screen flex items-center justify-center py-12 px-4 sm:px-6 lg:px-8">
    <div class="max-w-5xl w-full bg-white rounded-xl shadow-2xl p-8 md:p-12 space-y-10">
        <header class="text-center">
            <h1 class="text-4xl font-extrabold text-gray-900 mb-4">VUI Survey: Interactive Product Experience</h1>
            <p class="text-lg text-gray-600 max-w-2xl mx-auto">
                Welcome! Explore our product catalog using two different interfaces. Your interactions will help us understand the usability of Voice User Interfaces.
            </p>
            <p class="text-md text-gray-500 mt-2">
                Please interact with both the "Voice Enabled" and "Standard" experiences, then provide your feedback via the Google Form link below.
            </p>
        </header>

        <nav class="flex flex-wrap justify-center gap-4 mb-8">
            <button id="voiceEnabledBtn" class="nav-button px-6 py-3 rounded-full text-lg font-semibold transition-all duration-300 ease-in-out bg-blue-600 text-white shadow-md hover:bg-blue-700 focus:outline-none focus:ring-2 focus:ring-blue-500 focus:ring-offset-2 active" onclick="showSection('voiceEnabledSection')">
                Voice Enabled Experience
            </button>
            <button id="standardBtn" class="nav-button px-6 py-3 rounded-full text-lg font-semibold transition-all duration-300 ease-in-out bg-gray-200 text-gray-800 shadow-md hover:bg-gray-300 focus:outline-none focus:ring-2 focus:ring-gray-400 focus:ring-offset-2" onclick="showSection('standardSection')">
                Standard Web Experience
            </button>
        </nav>

        <!-- Voice Enabled Section -->
        <section id="voiceEnabledSection" class="section bg-blue-50 border border-blue-200 rounded-lg p-6 md:p-8 shadow-inner">
            <h2 class="text-3xl font-bold text-blue-800 mb-6 text-center">Voice Enabled Product Catalog</h2>
            <p class="text-gray-700 mb-4 text-center">
                **Hover your mouse over any product card to hear its description.**
            </p>
            <p class="text-gray-700 mb-6 text-center font-semibold">
                Click "Start Voice Control" to use voice commands:
            </p>
            <div class="flex flex-col sm:flex-row items-center justify-center gap-4 mb-8">
                <button id="voiceControlBtn" class="px-6 py-3 rounded-full text-lg font-semibold transition-all duration-300 ease-in-out bg-blue-500 text-white shadow-md hover:bg-blue-600 focus:outline-none focus:ring-2 focus:ring-blue-500 focus:ring-offset-2" onclick="toggleVoiceControl()">
                    Start Voice Control
                </button>
                <span id="voiceStatus" class="text-gray-600 text-sm">Click to enable voice commands.</span>
            </div>
            <div class="bg-blue-100 border border-blue-300 text-blue-800 px-4 py-3 rounded-md mb-8">
                <p class="font-bold text-xl mb-3">How to use Voice Commands:</p>
                <ul class="list-disc list-inside space-y-2 text-lg">
                    <li>Say a **product name** (e.g., "Smartwatch") to hear its description.</li>
                    <li>Say "**[Product Name] add to cart**" (e.g., "Earbuds add to cart") to simulate adding to cart.</li>
                    <li>Say "**[Product Name] price**" (e.g., "Laptop price") to hear the product's price.</li>
                    <li>Say "**Help**" to hear a list of all commands.</li>
                    <li>Say "**Suggest**" or "**Suggest a product**" to get a random product recommendation.</li>
                </ul>
            </div>

            <div id="voiceProductGrid" class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-6">
                <!-- Product cards will be injected here by JavaScript -->
            </div>
        </section>

        <!-- Standard Web Section -->
        <section id="standardSection" class="section bg-gray-50 border border-gray-200 rounded-lg p-6 md:p-8 shadow-inner hidden">
            <h2 class="text-3xl font-bold text-gray-800 mb-6 text-center">Standard Product Catalog</h2>
            <p class="text-gray-700 mb-8 text-center">
                Browse products and interact using traditional clicks. No voice feedback or voice commands in this section.
            </p>

            <div id="standardProductGrid" class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-6">
                <!-- Product cards will be injected here by JavaScript -->
            </div>
        </section>

        <!-- Feedback Link Section -->
        <section class="section bg-purple-50 border border-purple-200 rounded-lg p-6 md:p-8 shadow-inner text-center">
            <h2 class="text-3xl font-bold text-purple-800 mb-6">Provide Your Feedback</h2>
            <p class="text-gray-700 mb-8 max-w-2xl mx-auto">
                Your detailed feedback on both experiences is invaluable for my research. Please click the button below to fill out the survey on Google Forms.
            </p>
            <a href="https://docs.google.com/forms/d/e/1FAIpQLSeFCjyJuN3j2L4Yr8MUz5WsmNBHgoYkfszLmIFoUOVIj4QJOQ/viewform?usp=header" target="_blank" rel="noopener noreferrer" class="inline-block px-8 py-4 bg-purple-600 text-white text-xl font-bold rounded-full shadow-lg hover:bg-purple-700 transition-all duration-300 ease-in-out transform hover:scale-105 focus:outline-none focus:ring-2 focus:ring-purple-500 focus:ring-offset-2">
                Go to Feedback Form
            </a>
                    </section>
    </div>

    <script>
        let recognition = null; // SpeechRecognition object
        let isListening = false;
        let currentUtterance = null; // For SpeechSynthesis

        const products = [
            {
                id: 'p1',
                name: 'Smartwatch',
                description: 'This smartwatch tracks your fitness, receives notifications, and makes calls directly from your wrist. It features a vibrant AMOLED display and a long-lasting battery.',
                price: '$199.99',
                image: 'https://i.ibb.co/XZdnsCVb/Apple-Watch-Mockup.jpg'
            },
            {
                id: 'p2',
                name: 'Earbuds',
                description: 'These wireless earbuds offer immersive sound with active noise cancellation. They are perfect for music lovers and calls on the go, and come with a portable charging case.',
                price: '$129.00',
                image: 'https://i.ibb.co/N2ZHDrxx/earbuds.jpg'
            },
            {
                id: 'p3',
                name: 'Speaker',
                description: 'This portable Bluetooth speaker delivers powerful sound in a compact design. It is waterproof and durable, ideal for outdoor adventures, and connects seamlessly via Bluetooth.',
                price: '$79.50',
                image: 'https://i.ibb.co/gbk97zW5/Wireless-Speakers.jpg'
            },
            {
                id: 'p4',
                name: 'Office Chair',
                description: 'This ergonomic office chair is designed for maximum comfort and support during long working hours. It features adjustable lumbar support and breathable mesh material.',
                price: '$249.00',
                image: 'https://i.ibb.co/T3vTG9V/office-chair.jpg'
            },
            {
                id: 'p5',
                name: 'Laptop',
                description: 'This high-performance laptop features a blazing fast processor and a stunning display for both work and entertainment. It has a lightweight design for ultimate portability.',
                price: '$1199.00',
                image: 'https://i.ibb.co/rBMG3ML/Apple.jpg'
            },
            {
                id: 'p6',
                name: 'Smart Hub',
                description: 'This smart home hub allows you to control all your smart devices from one central hub. It is compatible with various smart home ecosystems for seamless integration.',
                price: '$89.99',
                image: 'https://i.ibb.co/ZpfTqcR0/Smart-hub.jpg'
            }
        ];

        // --- Speech Synthesis (Voice Output) Functions ---
        function speakText(text) {
            if ('speechSynthesis' in window) {
                if (currentUtterance) {
                    window.speechSynthesis.cancel(); // Stop any ongoing speech
                }
                currentUtterance = new SpeechSynthesisUtterance(text);
                currentUtterance.lang = 'en-US';
                currentUtterance.rate = 1.0; // Adjust speech rate (0.1 to 10)
                currentUtterance.pitch = 1.0; // Adjust speech pitch (0 to 2)
                window.speechSynthesis.speak(currentUtterance);
            } else {
                console.warn("Speech Synthesis not supported in this browser.");
            }
        }

        function stopSpeaking() {
            if ('speechSynthesis' in window && currentUtterance) {
                window.speechSynthesis.cancel();
                currentUtterance = null;
            }
        }

        // --- Speech Recognition (Voice Input) Functions ---
        function toggleVoiceControl() {
            const voiceControlBtn = document.getElementById('voiceControlBtn');
            const voiceStatus = document.getElementById('voiceStatus');

            if (!('webkitSpeechRecognition' in window)) {
                voiceStatus.textContent = 'Speech Recognition not supported in this browser.';
                voiceControlBtn.disabled = true;
                speakText("Speech Recognition is not supported in your browser.");
                return;
            }

            if (!recognition) {
                recognition = new webkitSpeechRecognition();
                recognition.interimResults = false; // Only return final results
                recognition.lang = 'en-US';
                recognition.continuous = true; // Keep listening for multiple commands
                recognition.maxAlternatives = 1; // Get the most likely result

                recognition.onstart = () => {
                    isListening = true;
                    voiceControlBtn.textContent = 'Stop Voice Control';
                    voiceControlBtn.classList.remove('bg-blue-500', 'hover:bg-blue-600');
                    voiceControlBtn.classList.add('bg-red-500', 'hover:bg-red-600');
                    voiceStatus.textContent = 'Listening... Say a product name or command.';
                    voiceStatus.classList.remove('text-gray-600', 'text-red-600');
                    voiceStatus.classList.add('text-green-600');
                    stopSpeaking(); // Stop any existing speech synthesis
                    speakText("Voice control started. I am listening.");
                };

                recognition.onresult = (event) => {
                    const transcript = event.results[event.results.length - 1][0].transcript.toLowerCase();
                    processVoiceCommand(transcript);
                };

                recognition.onerror = (event) => {
                    console.error('Speech recognition error:', event.error);
                    voiceStatus.textContent = `Error: ${event.error}. Please ensure microphone access.`;
                    voiceStatus.classList.remove('text-green-600');
                    voiceStatus.classList.add('text-red-600');
                    isListening = false;
                    voiceControlBtn.textContent = 'Start Voice Control';
                    voiceControlBtn.classList.remove('bg-red-500', 'hover:bg-red-600');
                    voiceControlBtn.classList.add('bg-blue-500', 'hover:bg-blue-600');
                    speakText(`Speech recognition error: ${event.error}. Please check your microphone.`);
                };

                recognition.onend = () => {
                    if (isListening) {
                        // If continuous is true, onend means it stopped for some reason (error, or user agent stopped it).
                        // We should probably just reset the UI state and allow user to restart.
                        isListening = false;
                        voiceControlBtn.textContent = 'Start Voice Control';
                        voiceControlBtn.classList.remove('bg-red-500', 'hover:bg-red-600');
                        voiceControlBtn.classList.add('bg-blue-500', 'hover:bg-blue-600');
                        voiceStatus.textContent = 'Voice control stopped. Click to start.';
                        voiceStatus.classList.remove('text-green-600', 'text-red-600');
                        voiceStatus.classList.add('text-gray-600');
                    }
                };
            }

            if (isListening) {
                recognition.stop();
            } else {
                recognition.start();
            }
        }

        function getAvailableCommands() {
            return `You can say a product name like Smartwatch to hear its description. You can also say a product name followed by add to cart, for example, Earbuds add to cart. To hear the price, say a product name followed by price, for example, Laptop price. You can also say Help, or Suggest, or Suggest a product, to get a recommendation.`;
        }

        function suggestRandomProduct() {
            const randomIndex = Math.floor(Math.random() * products.length);
            const product = products[randomIndex];
            logInteraction('VUI_voice_suggest_product', product);
            speakText(`How about the ${product.name}? ${product.description}`);
        }

        function processVoiceCommand(command) {
            console.log('Voice Command Received:', command);
            stopSpeaking(); // Stop any current speech before responding

            // Global commands
            if (command.includes('help')) {
                logInteraction('VUI_voice_help_command', { command });
                speakText(getAvailableCommands());
                return;
            }
            if (command.includes('suggest') || command.includes('suggest a product')) {
                suggestRandomProduct();
                return;
            }

            let matchedProduct = null;
            for (const product of products) {
                const productNameLower = product.name.toLowerCase();
                if (command.includes(productNameLower)) {
                    matchedProduct = product;
                    break;
                }
            }

            if (matchedProduct) {
                if (command.includes('add to cart')) {
                    logInteraction('VUI_voice_add_to_cart', matchedProduct);
                    speakText(`${matchedProduct.name} added to your cart.`);
                } else if (command.includes('price')) {
                    logInteraction('VUI_voice_get_price', matchedProduct);
                    speakText(`The price of the ${matchedProduct.name} is ${matchedProduct.price}.`);
                } else {
                    // If just product name is said, or any other unrecognized command with product name, describe it
                    logInteraction('VUI_voice_describe_product', matchedProduct);
                    speakText(`${matchedProduct.name}. ${matchedProduct.description}`);
                }
            } else {
                speakText("I didn't understand that. Please say a product name like 'Smartwatch', or say 'Help' for a list of commands.");
                logInteraction('VUI_unrecognized_command', { command });
            }
        }

        // --- Interaction Logging ---
        function logInteraction(type, data) {
            const timestamp = new Date().toISOString();
            console.log(`[${timestamp}] Interaction: ${type}`, data);
        }

        // --- Product Card Rendering ---
        function renderProductCards(containerId, isVoiceEnabled) {
            const container = document.getElementById(containerId);
            container.innerHTML = ''; // Clear existing content

            products.forEach(product => {
                const card = document.createElement('div');
                card.className = 'product-card bg-white rounded-lg p-6 shadow-md border border-gray-200 flex flex-col';

                if (isVoiceEnabled) {
                    // Mouseover for initial description
                    card.setAttribute('data-voice-text', product.description);
                    card.onmouseover = () => speakText(product.description); // Only description on hover
                    card.onmouseout = stopSpeaking;
                    card.classList.add('cursor-pointer', 'hover:shadow-lg');
                } else {
                    card.classList.add('hover:shadow-lg'); // Still nice to have hover effect
                }

                card.innerHTML = `
                    <img src="${product.image}" alt="${product.name}" class="rounded-md mb-4">
                    <h3 class="text-xl font-semibold text-gray-800 mb-2">${product.name}</h3>
                    <p class="text-gray-600 text-sm mb-4 flex-grow">${product.description}</p>
                    <div class="mt-auto">
                        <p class="text-2xl font-bold text-blue-700 mb-4">${product.price}</p>
                        <div class="flex space-x-3">
                            <button class="flex-1 px-4 py-2 rounded-md bg-blue-500 text-white font-medium hover:bg-blue-600 transition-colors duration-200"
                                onclick="handleButtonClick('view', '${product.id}', ${isVoiceEnabled})">
                                View Details
                            </button>
                            <button class="flex-1 px-4 py-2 rounded-md bg-green-500 text-white font-medium hover:bg-green-600 transition-colors duration-200"
                                onclick="handleButtonClick('add_to_cart', '${product.id}', ${isVoiceEnabled})">
                                Add to Cart
                            </button>
                        </div>
                    </div>
                `;
                container.appendChild(card);
            });
        }

        function handleButtonClick(actionType, productId, isVoiceEnabledSection) {
            const product = products.find(p => p.id === productId);
            if (!product) return;

            if (isVoiceEnabledSection) {
                logInteraction(`VUI_click_${actionType}`, product);
                let voiceMessage = '';
                if (actionType === 'view') {
                    voiceMessage = `You clicked view details for ${product.name}.`;
                } else if (actionType === 'add_to_cart') {
                    voiceMessage = `You clicked add to cart for ${product.name}.`;
                }
                speakText(voiceMessage);
            } else {
                logInteraction(`Standard_click_${actionType}`, product);
                console.log(`Standard interaction: ${actionType} for ${product.name}`);
            }
        }

        // --- Section Switching Logic ---
        function showSection(sectionId) {
            const sections = ['voiceEnabledSection', 'standardSection'];
            sections.forEach(id => {
                document.getElementById(id).classList.add('hidden');
            });
            document.getElementById(sectionId).classList.remove('hidden');

            // Update active button styling
            document.getElementById('voiceEnabledBtn').classList.remove('active', 'bg-blue-600', 'text-white');
            document.getElementById('voiceEnabledBtn').classList.add('bg-gray-200', 'text-gray-800');
            document.getElementById('standardBtn').classList.remove('active', 'bg-blue-600', 'text-white');
            document.getElementById('standardBtn').classList.add('bg-gray-200', 'text-gray-800');

            const activeButton = document.getElementById(sectionId === 'voiceEnabledSection' ? 'voiceEnabledBtn' : 'standardBtn');
            activeButton.classList.add('active', 'bg-blue-600', 'text-white');
            activeButton.classList.remove('bg-gray-200', 'text-gray-800');

            // Stop any ongoing speech synthesis or recognition when switching sections
            stopSpeaking();
            if (recognition && isListening) {
                recognition.stop();
            }
            // Reset voice control button state if switching away from voice section
            if (sectionId !== 'voiceEnabledSection') {
                const voiceControlBtn = document.getElementById('voiceControlBtn');
                const voiceStatus = document.getElementById('voiceStatus');
                voiceControlBtn.textContent = 'Start Voice Control';
                voiceControlBtn.classList.remove('bg-red-500', 'hover:bg-red-600');
                voiceControlBtn.classList.add('bg-blue-500', 'hover:bg-blue-600');
                voiceStatus.textContent = 'Click to enable voice commands.';
                voiceStatus.classList.remove('text-green-600', 'text-red-600');
                voiceStatus.classList.add('text-gray-600');
                isListening = false;
            }
        }

        // Initial rendering and display on page load
        document.addEventListener('DOMContentLoaded', () => {
            renderProductCards('voiceProductGrid', true);
            renderProductCards('standardProductGrid', false);
            showSection('voiceEnabledSection'); // Show voice-enabled section by default
        });
    </script>
</body>
</html>
