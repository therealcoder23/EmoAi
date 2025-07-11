# EmoAi
An AI-powered survey web app with real-time analysis.
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Emotion AI Chatbox</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        /* Custom animations */
        @keyframes float {
            0% { transform: translateY(0px); }
            50% { transform: translateY(-10px); }
            100% { transform: translateY(0px); }
        }
       
        @keyframes pulse {
            0% { opacity: 1; }
            50% { opacity: 0.5; }
            100% { opacity: 1; }
        }
       
        .typing-indicator {
            display: flex;
            padding: 8px;
        }
       
        .typing-dot {
            width: 8px;
            height: 8px;
            margin: 0 2px;
            background-color: #4f46e5;
            border-radius: 50%;
            animation: pulse 1.5s infinite ease-in-out;
        }
       
        .typing-dot:nth-child(1) { animation-delay: 0s; }
        .typing-dot:nth-child(2) { animation-delay: 0.3s; }
        .typing-dot:nth-child(3) { animation-delay: 0.6s; }
       
        /* Custom scrollbar */
        .custom-scrollbar::-webkit-scrollbar {
            width: 6px;
        }
       
        .custom-scrollbar::-webkit-scrollbar-track {
            background: #f1f1f1;
            border-radius: 10px;
        }
       
        .custom-scrollbar::-webkit-scrollbar-thumb {
            background: #888;
            border-radius: 10px;
        }
       
        .custom-scrollbar::-webkit-scrollbar-thumb:hover {
            background: #555;
        }
       
        /* Emotion colors */
        .happy { background-color: #fef08a; color: #854d0e; }
        .sad { background-color: #bfdbfe; color: #1e40af; }
        .romantic { background-color: #fecaca; color: #991b1b; }
        .angry { background-color: #fca5a5; color: #7f1d1d; }
        .neutral { background-color: #e5e7eb; color: #4b5563; }
        .excited { background-color: #a7f3d0; color: #065f46; }

        /* Lobby specific styles */
        .lobby-section {
            padding: 4rem 1rem;
            min-height: 100vh;
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            text-align: center;
        }
        .lobby-section:nth-of-type(odd) {
            background-color: #f3f4f6; /* Light gray for alternating sections */
        }
    </style>
</head>
<body class="bg-gray-100 min-h-screen flex flex-col">
    <header class="bg-indigo-600 text-white shadow-lg fixed w-full z-40">
        <div class="container mx-auto px-4 py-3 flex justify-between items-center">
            <div class="flex items-center space-x-2">
                <i class="fas fa-robot text-2xl"></i>
                <h1 class="text-xl font-bold">Emotion AI Chatbox</h1>
            </div>
            <nav class="hidden md:flex space-x-6" id="main-nav">
                <a href="#chatbox-features" id="featuresLink" class="hover:text-indigo-200 transition">Features</a>
                <a href="#chatbox-about" id="aboutLink" class="hover:text-indigo-200 transition">About</a>
                <a href="#" id="loginBtnHeader" class="hover:text-indigo-200 transition">Sign In</a>
                <button id="tryDemoBtnHeader" class="bg-indigo-700 hover:bg-indigo-800 text-white px-4 py-1 rounded-full transition shadow">Try Demo</button>
            </nav>
            <button class="md:hidden text-xl" id="mobileMenuBtn">
                <i class="fas fa-bars"></i>
            </button>
        </div>
        <div class="md:hidden hidden bg-indigo-700 px-4 py-2" id="mobileMenu">
            <div class="flex flex-col space-y-2">
                <a href="#chatbox-features" id="mobileFeaturesLink" class="hover:text-indigo-200 transition">Features</a>
                <a href="#chatbox-about" id="mobileAboutLink" class="hover:text-indigo-200 transition">About</a>
                <a href="#" id="mobileLoginBtn" class="hover:text-indigo-200 transition">Sign In</a>
                <button id="mobileTryDemoBtn" class="bg-indigo-800 hover:bg-indigo-900 text-white px-4 py-1 rounded-full transition shadow">Try Demo</button>
            </div>
        </div>
    </header>

    <div id="lobby" class="min-h-screen pt-16">
        <section class="lobby-section bg-gradient-to-r from-indigo-500 to-purple-600 text-white">
            <h2 class="text-4xl md:text-6xl font-extrabold mb-6 animate-float">
                Chat with Emotion
            </h2>
            <p class="text-lg md:text-xl max-w-2xl mb-8">
                Experience AI that understands and responds with nuance, adapting its tone to your chosen emotion.
            </p>
            <button id="tryDemoBtnHero" class="bg-white text-indigo-700 hover:bg-gray-200 text-xl font-bold px-8 py-4 rounded-full shadow-lg transform transition duration-300 hover:scale-105">
                Try Demo Now
            </button>
        </section>

        <section id="lobby-features" class="lobby-section bg-gray-100 text-gray-800">
            <h2 class="text-3xl md:text-4xl font-bold mb-10 text-indigo-700">Explore Our Features</h2>
            <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-8 max-w-5xl w-full">
                <div class="p-6 bg-white rounded-xl shadow-lg transform transition duration-300 hover:scale-105">
                    <div class="flex items-center mb-4">
                        <i class="fas fa-smile-beam text-indigo-600 text-3xl mr-3"></i>
                        <h3 class="font-bold text-xl">Multiple Emotions</h3>
                    </div>
                    <p class="text-gray-700">Change the AI's emotional state to get responses that match different moods: happy, sad, angry, excited, romantic, and neutral.</p>
                </div>
                <div class="p-6 bg-white rounded-xl shadow-lg transform transition duration-300 hover:scale-105">
                    <div class="flex items-center mb-4">
                        <i class="fas fa-brain text-indigo-600 text-3xl mr-3"></i>
                        <h3 class="font-bold text-xl">Context-Aware Responses</h3>
                    </div>
                    <p class="text-gray-700">The AI remembers your conversation and responds intelligently, ensuring continuity and relevance in every interaction.</p>
                </div>
                <div class="p-6 bg-white rounded-xl shadow-lg transform transition duration-300 hover:scale-105">
                    <div class="flex items-center mb-4">
                        <i class="fas fa-mobile-alt text-indigo-600 text-3xl mr-3"></i>
                        <h3 class="font-bold text-xl">Responsive Design</h3>
                    </div>
                    <p class="text-gray-700">Enjoy a seamless experience on any device, whether you're on your phone, tablet, or desktop.</p>
                </div>
                <div class="p-6 bg-white rounded-xl shadow-lg transform transition duration-300 hover:scale-105">
                    <div class="flex items-center mb-4">
                        <i class="fas fa-history text-indigo-600 text-3xl mr-3"></i>
                        <h3 class="font-bold text-xl">Conversation History</h3>
                    </div>
                    <p class="text-gray-700">Sign in to save your chat history and pick up where you left off, anytime, anywhere.</p>
                </div>
                <div class="p-6 bg-white rounded-xl shadow-lg transform transition duration-300 hover:scale-105">
                    <div class="flex items-center mb-4">
                        <i class="fas fa-magic text-indigo-600 text-3xl mr-3"></i>
                        <h3 class="font-bold text-xl">Powered by Gemini Flash</h3>
                    </div>
                    <p class="text-gray-700">Leverages the speed and efficiency of Google's Gemini 2.5 Flash model for rapid and accurate emotional responses.</p>
                </div>
                <div class="p-6 bg-white rounded-xl shadow-lg transform transition duration-300 hover:scale-105">
                    <div class="flex items-center mb-4">
                        <i class="fas fa-comments text-indigo-600 text-3xl mr-3"></i>
                        <h3 class="font-bold text-xl">Engaging Dialogue</h3>
                    </div>
                    <p class="text-gray-700">Experience more human-like conversations as the AI matches tone and content to your chosen emotional prompt.</p>
                </div>
            </div>
        </section>

        <section id="lobby-about" class="lobby-section bg-white text-gray-800">
            <h2 class="text-3xl md:text-4xl font-bold mb-6 text-indigo-700">About Emotion AI Chatbox</h2>
            <p class="text-lg max-w-3xl mb-8">
                Emotion AI Chatbox is a cutting-edge chatbot designed to make AI interactions more intuitive and engaging. Unlike traditional chatbots, it can adapt its responses based on a range of emotional states, providing a uniquely personalized conversational experience.
            </p>
            <p class="text-md max-w-3xl mb-10">
                Our mission is to explore the frontiers of human-AI communication, creating tools that are not just intelligent, but also emotionally intelligent. This demo showcases our commitment to building more empathetic and responsive AI.
            </p>
            <button id="tryDemoBtnAbout" class="bg-indigo-600 text-white hover:bg-indigo-700 text-lg font-semibold px-6 py-3 rounded-full shadow-md transform transition duration-300 hover:scale-105">
                Start Chatting
            </button>
        </section>
    </div>

    <main id="chatbox" class="flex-grow container mx-auto px-4 py-6 flex flex-col md:flex-row gap-6 hidden pt-16">
        <div class="flex-grow bg-white rounded-xl shadow-lg overflow-hidden flex flex-col max-h-[calc(100vh-8rem)]">
            <div class="bg-indigo-600 text-white p-4 flex justify-between items-center">
                <div class="flex items-center space-x-3">
                    <div class="w-10 h-10 rounded-full bg-indigo-500 flex items-center justify-center">
                        <i class="fas fa-robot"></i>
                    </div>
                    <div>
                        <h2 class="font-bold">Emotion AI</h2>
                        <p class="text-xs opacity-80" id="currentEmotion">Neutral</p>
                    </div>
                </div>
                <div class="flex space-x-2">
                    <button id="happyBtn" class="p-2 rounded-full hover:bg-indigo-500 transition">
                        <i class="fas fa-smile text-yellow-300"></i>
                    </button>
                    <button id="sadBtn" class="p-2 rounded-full hover:bg-indigo-500 transition">
                        <i class="fas fa-sad-tear text-blue-300"></i>
                    </button>
                    <button id="romanticBtn" class="p-2 rounded-full hover:bg-indigo-500 transition">
                        <i class="fas fa-heart text-red-300"></i>
                    </button>
                    <button id="angryBtn" class="p-2 rounded-full hover:bg-indigo-500 transition">
                        <i class="fas fa-angry text-red-500"></i>
                    </button>
                    <button id="excitedBtn" class="p-2 rounded-full hover:bg-indigo-500 transition">
                        <i class="fas fa-star text-green-300"></i>
                    </button>
                     <button id="infoToggleBtn" class="p-2 rounded-full hover:bg-indigo-500 transition ml-2">
                        <i class="fas fa-info-circle"></i>
                    </button>
                </div>
            </div>
           
            <div id="chatMessages" class="flex-grow p-4 overflow-y-auto custom-scrollbar space-y-4">
                </div>
           
            <div class="border-t p-4 bg-gray-50">
                <form id="chatForm" class="flex gap-2">
                    <input type="text" id="messageInput"
                           class="flex-grow border rounded-lg px-4 py-2 focus:outline-none focus:ring-2 focus:ring-indigo-500"
                           placeholder="Type your message..." autocomplete="off">
                    <button type="submit" class="bg-indigo-600 text-white px-4 py-2 rounded-lg hover:bg-indigo-700 transition">
                        <i class="fas fa-paper-plane"></i>
                    </button>
                </form>
            </div>
        </div>
       
        <div id="chatbox-info-panel" class="md:w-80 bg-white rounded-xl shadow-lg p-6 overflow-y-auto custom-scrollbar max-h-[calc(100vh-8rem)] hidden md:block">
            <h2 class="text-xl font-bold mb-4 text-indigo-700">Information</h2>
            <div class="space-y-6">
                <div class="p-4 bg-indigo-50 rounded-lg">
                    <div class="flex items-center mb-2">
                        <i class="fas fa-info-circle text-indigo-600 mr-2"></i>
                        <h3 class="font-semibold">About This Demo</h3>
                    </div>
                    <p class="text-sm text-gray-700">
                        This chatbox is powered by **Nightfallgaming's EmoAi 3.0 Flash** model, providing fast and emotionally nuanced responses.
                        Select an emotion using the buttons above to guide the AI's tone.
                    </p>
                </div>
                <div class="p-4 bg-indigo-50 rounded-lg">
                    <div class="flex items-center mb-2">
                        <i class="fas fa-lightbulb text-indigo-600 mr-2"></i>
                        <h3 class="font-semibold">Tips</h3>
                    </div>
                    <p class="text-sm text-gray-700">
                        Try changing the emotion mid-conversation to see how the AI adapts.
                        The AI retains conversation context, making interactions more fluid.
                        Type <code class="bg-gray-200 px-1 rounded text-xs">/delete</code> to clear the chat history.
                    </p>
                </div>

                <div id="chatbox-features" class="p-4 bg-gray-50 rounded-lg">
                    <h3 class="font-bold text-xl text-indigo-700 mb-3">Our Features</h3>
                    <ul class="list-disc pl-5 space-y-2 text-sm text-gray-700">
                        <li>**Multiple Emotions:** Interact with AI in various moods like happy, sad, angry, excited, romantic, and neutral.</li>
                        <li>**Context-Aware:** The AI remembers your conversation for intelligent, continuous dialogue.</li>
                        <li>**Responsive Design:** Seamless experience across all your devices.</li>
                        <li>**Conversation History:** (Sign-in required) Save and resume chats anytime.</li>
                        <li>**Powered by Gemini Flash:** Fast and accurate emotional responses.</li>
                        <li>**Engaging Dialogue:** More human-like conversations with adaptive tone.</li>
                    </ul>
                </div>

                <div id="chatbox-about" class="p-4 bg-gray-50 rounded-lg">
                    <h3 class="font-bold text-xl text-indigo-700 mb-3">About Emotion AI Chatbox</h3>
                    <p class="text-sm text-gray-700 mb-2">
                        Emotion AI Chatbox is a cutting-edge chatbot designed to make AI interactions more intuitive and engaging. It adapts responses based on emotional states, offering a uniquely personalized conversational experience.
                    </p>
                    <p class="text-sm text-gray-700">
                        Our mission is to explore the frontiers of human-AI communication, building tools that are not just intelligent, but also emotionally intelligent.
                    </p>
                </div>

                <div class="p-4 bg-indigo-50 rounded-lg">
                    <h3 class="font-semibold mb-2">Latest Updates:</h3>
                    <ul class="list-disc pl-5 space-y-1 text-sm">
                        <li><span class="font-medium">v1.4 (Current):</span> AI emotion responses refined for smoother, more intelligent delivery. Added <code class="bg-gray-200 px-1 rounded text-xs">/delete</code> command to remove chat history.</li>
                        <li><span class="font-medium">v1.3:</span> Added interactive lobby and chatbox transition.</li>
                        <li><span class="font-medium">v1.2:</span> Updated to EmoAi 3.0 Flash model and removed AI core selection.</li>
                        <li><span class="font-medium">v1.1:</span> Enhanced emotional responses with deeper context.</li>
                        <li><span class="font-medium">v1.0:</span> Initial release with basic emotion switching.</li>
                    </ul>
                </div>
            </div>
        </div>
    </main>

    <footer class="bg-gray-800 text-white py-6 mt-auto">
        <div class="container mx-auto px-4">
            <div class="flex flex-col md:flex-row justify-between items-center">
                <div class="mb-4 md:mb-0">
                    <h3 class="text-lg font-bold">Emotion AI Chatbox</h3>
                    <p class="text-sm text-gray-400">Making conversations more human-like</p>
                </div>
                <div class="flex space-x-6">
                    <a href="#" id="termsBtn" class="text-sm hover:text-indigo-300 transition">Terms of Service</a>
                    <a href="#" id="privacyBtn" class="text-sm hover:text-indigo-300 transition">Privacy Policy</a>
                    <a href="mailto:support@emotionai.com" class="text-sm hover:text-indigo-300 transition">Contact Us</a>
                </div>
            </div>
            <div class="mt-6 pt-6 border-t border-gray-700 text-center text-sm text-gray-400">
                <p>&copy; 2025 Emotion AI Chatbox. All rights reserved.</p>
            </div>
        </div>
    </footer>

    <div id="loginModal" class="fixed inset-0 bg-black bg-opacity-50 flex items-center justify-center z-50 hidden">
        <div class="bg-white rounded-lg p-6 w-full max-w-md">
            <div class="flex justify-between items-center mb-4">
                <h2 class="text-xl font-bold text-indigo-700">Sign In</h2>
                <button id="closeLoginModal" class="text-gray-500 hover:text-gray-700">
                    <i class="fas fa-times"></i>
                </button>
            </div>
            <form id="loginForm" class="space-y-4">
                <div>
                    <label for="loginEmail" class="block text-sm font-medium text-gray-700 mb-1">Email</label>
                    <input type="email" id="loginEmail" class="w-full border rounded-lg px-4 py-2 focus:outline-none focus:ring-2 focus:ring-indigo-500" required>
                </div>
                <div>
                    <label for="loginPassword" class="block text-sm font-medium text-gray-700 mb-1">Password</label>
                    <input type="password" id="loginPassword" class="w-full border rounded-lg px-4 py-2 focus:outline-none focus:ring-2 focus:ring-indigo-500" required>
                </div>
                <button type="submit" class="w-full bg-indigo-600 text-white py-2 rounded-lg hover:bg-indigo-700 transition">
                    Sign In
                </button>
            </form>
            <div class="mt-4 text-center">
                <p class="text-sm text-gray-600">Don't have an account? <a href="#" id="showRegister" class="text-indigo-600 hover:underline">Register</a></p>
            </div>
        </div>
    </div>

    <div id="registerModal" class="fixed inset-0 bg-black bg-opacity-50 flex items-center justify-center z-50 hidden">
        <div class="bg-white rounded-lg p-6 w-full max-w-md">
            <div class="flex justify-between items-center mb-4">
                <h2 class="text-xl font-bold text-indigo-700">Create Account</h2>
                <button id="closeRegisterModal" class="text-gray-500 hover:text-gray-700">
                    <i class="fas fa-times"></i>
                </button>
            </div>
            <form id="registerForm" class="space-y-4">
                <div>
                    <label for="registerName" class="block text-sm font-medium text-gray-700 mb-1">Full Name</label>
                    <input type="text" id="registerName" class="w-full border rounded-lg px-4 py-2 focus:outline-none focus:ring-2 focus:ring-indigo-500" required>
                </div>
                <div>
                    <label for="registerEmail" class="block text-sm font-medium text-gray-700 mb-1">Email</label>
                    <input type="email" id="registerEmail" class="w-full border rounded-lg px-4 py-2 focus:outline-none focus:ring-2 focus:ring-indigo-500" required>
                </div>
                <div>
                    <label for="registerPassword" class="block text-sm font-medium text-gray-700 mb-1">Password</label>
                    <input type="password" id="registerPassword" class="w-full border rounded-lg px-4 py-2 focus:outline-none focus:ring-2 focus:ring-indigo-500" required>
                </div>
                <div>
                    <label for="registerConfirmPassword" class="block text-sm font-medium text-gray-700 mb-1">Confirm Password</label>
                    <input type="password" id="registerConfirmPassword" class="w-full border rounded-lg px-4 py-2 focus:outline-none focus:ring-2 focus:ring-indigo-500" required>
                </div>
                <button type="submit" class="w-full bg-indigo-600 text-white py-2 rounded-lg hover:bg-indigo-700 transition">
                    Register
                </button>
            </form>
            <div class="mt-4 text-center">
                <p class="text-sm text-gray-600">Already have an account? <a href="#" id="showLogin" class="text-indigo-600 hover:underline">Sign In</a></p>
            </div>
        </div>
    </div>

    <div id="termsModal" class="fixed inset-0 bg-black bg-opacity-50 flex items-center justify-center z-50 hidden">
        <div class="bg-white rounded-lg p-6 w-full max-w-2xl max-h-[80vh] overflow-y-auto">
            <div class="flex justify-between items-center mb-4">
                <h2 class="text-xl font-bold text-indigo-700">Terms of Service</h2>
                <button id="closeTermsModal" class="text-gray-500 hover:text-gray-700">
                    <i class="fas fa-times"></i>
                </button>
            </div>
            <div class="text-sm text-gray-700 space-y-4">
                <p>Last updated: July 2025</p>
               
                <h3 class="font-bold text-lg">1. Acceptance of Terms</h3>
                <p>By accessing or using the Emotion AI Chatbox service ("Service"), you agree to be bound by these Terms of Service ("Terms"). If you disagree with any part of the terms, you may not access the Service.</p>
               
                <h3 class="font-bold text-lg">2. Description of Service</h3>
                <p>The Service provides an AI-powered chatbot that can simulate different emotional states in its responses. The Service is provided for entertainment and informational purposes only.</p>
               
                <h3 class="font-bold text-lg">3. User Conduct</h3>
                <p>You agree not to use the Service to:</p>
                <ul class="list-disc pl-5 space-y-1">
                    <li>Violate any laws or regulations</li>
                    <li>Infringe upon the rights of others</li>
                    <li>Transmit any harmful or offensive content</li>
                    <li>Interfere with or disrupt the Service</li>
                <li>... (Other terms) ...</li>
                </ul>
               
                <h3 class="font-bold text-lg">4. Privacy</h3>
                <p>Your use of the Service is subject to our Privacy Policy, which explains how we collect, use, and protect your information.</p>
               
                <h3 class="font-bold text-lg">5. Limitation of Liability</h3>
                <p>The Service is provided "as is" without warranties of any kind. We shall not be liable for any damages resulting from your use of the Service.</p>
               
                <h3 class="font-bold text-lg">6. Changes to Terms</h3>
                <p>We reserve the right to modify these Terms at any time. Your continued use of the Service after such changes constitutes your acceptance of the new Terms.</p>
            </div>
        </div>
    </div>

    <div id="privacyModal" class="fixed inset-0 bg-black bg-opacity-50 flex items-center justify-center z-50 hidden">
        <div class="bg-white rounded-lg p-6 w-full max-w-2xl max-h-[80vh] overflow-y-auto">
            <div class="flex justify-between items-center mb-4">
                <h2 class="text-xl font-bold text-indigo-700">Privacy Policy</h2>
                <button id="closePrivacyModal" class="text-gray-500 hover:text-gray-700">
                    <i class="fas fa-times"></i>
                </button>
            </div>
            <div class="text-sm text-gray-700 space-y-4">
                <p>Last updated: July 2025</p>
               
                <h3 class="font-bold text-lg">1. Information We Collect</h3>
                <p>When you use our Service, we may collect:</p>
                <ul class="list-disc pl-5 space-y-1">
                    <li>Information you provide (account details, messages)</li>
                    <li>Usage data (interaction with the Service)</li>
                    <li>Technical data (device information, IP address)</li>
                </ul>
               
                <h3 class="font-bold text-lg">2. How We Use Your Information</h3>
                <p>We use the information we collect to:</p>
                <ul class="list-disc pl-5 space-y-1">
                    <li>Provide and maintain the Service</li>
                    <li>Improve and personalize your experience</li>
                    <li>Analyze usage patterns</li>
                    <li>Share with third parties (if applicable and consented)</li>
                    <li>Communicate with you</li>
                </ul>
               
                <h3 class="font-bold text-lg">3. Data Security</h3>
                <p>We implement appropriate security measures to protect your information. However, no method of transmission over the Internet is 100% secure.</p>
               
                <h3 class="font-bold text-lg">4. Data Retention</h3>
                <p>We retain your information only as long as necessary to provide the Service and for legitimate business purposes.</p>
               
                <h3 class="font-bold text-lg">5. Your Rights</h3>
                <p>Depending on your jurisdiction, you may have rights regarding your personal information, including access, correction, and deletion.</p>
               
                <h3 class="font-bold text-lg">6. Changes to This Policy</h3>
                <p>We may update our Privacy Policy from time to time. We will notify you of any changes by posting the new policy on this page.</p>
            </div>
        </div>
    </div>

    <script>
        // DOM Elements
        const chatMessages = document.getElementById('chatMessages');
        const messageInput = document.getElementById('messageInput');
        const chatForm = document.getElementById('chatForm');
        const currentEmotion = document.getElementById('currentEmotion');
        const chatbox = document.getElementById('chatbox'); // The main chat content
        const lobby = document.getElementById('lobby');     // The lobby section
       
        // Emotion buttons
        const happyBtn = document.getElementById('happyBtn');
        const sadBtn = document.getElementById('sadBtn');
        const romanticBtn = document.getElementById('romanticBtn');
        const angryBtn = document.getElementById('angryBtn');
        const excitedBtn = document.getElementById('excitedBtn');
        const infoToggleBtn = document.getElementById('infoToggleBtn');
        const chatboxInfoPanel = document.getElementById('chatbox-info-panel');
       
        // Lobby and Chatbox transition buttons
        const tryDemoBtnHero = document.getElementById('tryDemoBtnHero');
        const tryDemoBtnAbout = document.getElementById('tryDemoBtnAbout');
        const tryDemoBtnHeader = document.getElementById('tryDemoBtnHeader');
        const mobileTryDemoBtn = document.getElementById('mobileTryDemoBtn');
       
        // Header navigation links for lobby
        const featuresLink = document.getElementById('featuresLink');
        const aboutLink = document.getElementById('aboutLink');
        const mobileFeaturesLink = document.getElementById('mobileFeaturesLink');
        const mobileAboutLink = document.getElementById('mobileAboutLink');

        // Main navigation elements
        const mainNav = document.getElementById('main-nav');
        const mobileMenu = document.getElementById('mobileMenu');

        // Modal elements
        const loginModal = document.getElementById('loginModal');
        const registerModal = document.getElementById('registerModal');
        const termsModal = document.getElementById('termsModal');
        const privacyModal = document.getElementById('privacyModal');
       
        // Modal buttons
        const loginBtnHeader = document.getElementById('loginBtnHeader');
        const mobileLoginBtn = document.getElementById('mobileLoginBtn');
        const closeLoginModal = document.getElementById('closeLoginModal');
        const showRegister = document.getElementById('showRegister');
        const closeRegisterModal = document.getElementById('closeRegisterModal');
        const showLogin = document.getElementById('showLogin');
        const termsBtn = document.getElementById('termsBtn');
        const closeTermsModal = document.getElementById('closeTermsModal');
        const privacyBtn = document.getElementById('privacyBtn');
        const closePrivacyModal = document.getElementById('closePrivacyModal');
       
        // Mobile menu toggle button
        const mobileMenuBtn = document.getElementById('mobileMenuBtn');
       
        // State
        let currentEmotionState = 'neutral';
        let conversationHistory = [];
       
        // Define your API Key (REMINDER: Not secure for production!)
        const GEMINI_API_KEY = "AIzaSyCElT1l0eNsjZfqofeiVE0kl8bBRGo9EPA"; // Your specified API key

        // Initialize
        document.addEventListener('DOMContentLoaded', () => {
            // Set default emotion
            updateEmotion('neutral');
           
            // Load any saved conversation from localStorage
            const savedConversation = localStorage.getItem('aiConversation');
            if (savedConversation) {
                conversationHistory = JSON.parse(savedConversation);
            }

            // Handle navigation for Features/About in header to show within chatbox info panel
            // These handlers will only work when the chatbox is active.
            // The links themselves will be hidden from the header in chatbox mode.
            const handleInfoPanelNavigation = function(event) {
                event.preventDefault();
                const targetId = this.getAttribute('href'); // e.g., #chatbox-features or #chatbox-about
               
                // Only show chatbox if not already in chatbox
                if (lobby.classList.contains('hidden')) {
                    // Chatbox is already visible, just open/scroll info panel
                    if (chatboxInfoPanel.classList.contains('hidden')) {
                        chatboxInfoPanel.classList.remove('hidden');
                    }
                    setTimeout(() => {
                        const targetElement = document.querySelector(targetId);
                        if (targetElement) {
                            chatboxInfoPanel.scrollTop = targetElement.offsetTop - chatboxInfoPanel.offsetTop;
                        }
                    }, 100);
                } else {
                    // If we are in the lobby, clicking these links should show the chatbox
                    // and then open the info panel.
                    showChatbox();
                    // Give a moment for chatbox to render before showing/scrolling info panel
                    setTimeout(() => {
                        if (chatboxInfoPanel.classList.contains('hidden')) {
                            chatboxInfoPanel.classList.remove('hidden');
                        }
                        const targetElement = document.querySelector(targetId);
                        if (targetElement) {
                            chatboxInfoPanel.scrollTop = targetElement.offsetTop - chatboxInfoPanel.offsetTop;
                        }
                    }, 150); // Slightly longer delay
                }

                if (!mobileMenu.classList.contains('hidden')) {
                    mobileMenu.classList.add('hidden'); // Close mobile menu if open
                }
            };

            // Attach event listeners for lobby navigation links
            // These will now trigger the chatbox to show and open info panel
            featuresLink.addEventListener('click', handleInfoPanelNavigation);
            aboutLink.addEventListener('click', handleInfoPanelNavigation);
            mobileFeaturesLink.addEventListener('click', handleInfoPanelNavigation);
            mobileAboutLink.addEventListener('click', handleInfoPanelNavigation);
        });
       
        // Emotion handlers
        happyBtn.addEventListener('click', () => updateEmotion('happy'));
        sadBtn.addEventListener('click', () => updateEmotion('sad'));
        romanticBtn.addEventListener('click', () => updateEmotion('romantic'));
        angryBtn.addEventListener('click', () => updateEmotion('angry'));
        excitedBtn.addEventListener('click', () => updateEmotion('excited'));

        // Function to update emotion
        function updateEmotion(emotion) {
            currentEmotionState = emotion;
            currentEmotion.textContent = emotion.charAt(0).toUpperCase() + emotion.slice(1);
            // You can add visual feedback for selected emotion button here if desired
            // Example: remove a 'selected' class from all, then add to the clicked one
        }

        // Toggle chatbox info panel
        infoToggleBtn.addEventListener('click', () => {
            chatboxInfoPanel.classList.toggle('hidden');
        });
       
        // --- Lobby / Chatbox Transition Logic ---
        function showChatbox() {
            lobby.classList.add('hidden');
            chatbox.classList.remove('hidden');
            document.body.style.overflow = 'hidden'; // Prevents scrolling behind the fixed header and chatbox
            document.documentElement.scrollTop = 0; // Scroll to top when chatbox appears

            // Hide Features and About links in the main header and mobile menu when in chatbox
            featuresLink.classList.add('hidden');
            aboutLink.classList.add('hidden');
            mobileFeaturesLink.classList.add('hidden');
            mobileAboutLink.classList.add('hidden');
           
            renderConversation(); // Render conversation history once chatbox is visible
           
            // Add initial message if conversation history is empty
            if (conversationHistory.length === 0) {
                addBotMessage("Hello! I'm your Emotion AI. How are you feeling today? You can change my emotion using the buttons above!");
            }
        }

        function showLobby() {
            chatbox.classList.add('hidden');
            lobby.classList.remove('hidden');
            document.body.style.overflow = 'auto'; // Re-enable scrolling for the lobby
            document.documentElement.scrollTop = 0; // Scroll to top of lobby

            // Show Features and About links when back in lobby
            featuresLink.classList.remove('hidden');
            aboutLink.classList.remove('hidden');
            mobileFeaturesLink.classList.remove('hidden');
            mobileAboutLink.classList.remove('hidden');
        }

        tryDemoBtnHero.addEventListener('click', showChatbox);
        tryDemoBtnAbout.addEventListener('click', showChatbox);
        tryDemoBtnHeader.addEventListener('click', showChatbox);
        mobileTryDemoBtn.addEventListener('click', () => {
            showChatbox();
            mobileMenu.classList.add('hidden'); // Close mobile menu
        });

        // Chat form submission
        chatForm.addEventListener('submit', (e) => {
            e.preventDefault();
            const message = messageInput.value.trim();
            if (message) {
                if (message.toLowerCase() === '/delete') {
                    clearChatHistory();
                    addBotMessage("Chat history has been cleared.");
                    messageInput.value = '';
                    return; // Stop further processing for the /delete command
                }

                addUserMessage(message);
                messageInput.value = '';
               
                // Show typing indicator
                const typingIndicator = document.createElement('div');
                typingIndicator.className = 'flex justify-start';
                typingIndicator.innerHTML = `
                    <div class="max-w-xs md:max-w-md lg:max-w-lg bg-gray-100 text-gray-800 rounded-lg p-3">
                        <div class="typing-indicator">
                            <div class="typing-dot"></div>
                            <div class="typing-dot"></div>
                            <div class="typing-dot"></div>
                        </div>
                    </div>
                `;
                chatMessages.appendChild(typingIndicator);
                chatMessages.scrollTop = chatMessages.scrollHeight;
               
                // Generate AI response
                generateAIResponse(message).then(aiResponse => {
                    // Remove typing indicator
                    const currentTypingIndicator = chatMessages.querySelector('.typing-indicator');
                    if (currentTypingIndicator) {
                        currentTypingIndicator.closest('.flex.justify-start').remove();
                    }
                   
                    addBotMessage(aiResponse);
                   
                    // Save conversation to localStorage
                    conversationHistory.push({
                        user: message,
                        ai: aiResponse,
                        emotion: currentEmotionState
                    });
                    localStorage.setItem('aiConversation', JSON.stringify(conversationHistory));
                }).catch(error => {
                    // Remove typing indicator on error as well
                    const currentTypingIndicator = chatMessages.querySelector('.typing-indicator');
                    if (currentTypingIndicator) {
                        currentTypingIndicator.closest('.flex.justify-start').remove();
                    }
                    addBotMessage("Sorry, I encountered an error processing your message. Please check the console for details.");
                    console.error("Error generating AI response:", error);
                });
            }
        });
       
        function addUserMessage(message) {
            const messageDiv = document.createElement('div');
            messageDiv.className = 'flex justify-end';
            messageDiv.innerHTML = `
                <div class="max-w-xs md:max-w-md lg:max-w-lg bg-indigo-600 text-white rounded-lg p-3">
                    <p>${message}</p>
                </div>
            `;
            chatMessages.appendChild(messageDiv);
            chatMessages.scrollTop = chatMessages.scrollHeight;
        }
       
        function addBotMessage(message) {
            const messageDiv = document.createElement('div');
            messageDiv.className = 'flex justify-start';
            messageDiv.innerHTML = `
                <div class="max-w-xs md:max-w-md lg:max-w-lg ${currentEmotionState} rounded-lg p-3">
                    <p>${message}</p>
                </div>
            `;
            chatMessages.appendChild(messageDiv);
            chatMessages.scrollTop = chatMessages.scrollHeight;
        }

        function clearChatHistory() {
            conversationHistory = [];
            localStorage.removeItem('aiConversation');
            chatMessages.innerHTML = ''; // Clear messages from the display
        }
       
        function renderConversation() {
            chatMessages.innerHTML = ''; // Clear existing messages
            conversationHistory.forEach(item => {
                // Add user message
                const userMessageDiv = document.createElement('div');
                userMessageDiv.className = 'flex justify-end mb-4';
                userMessageDiv.innerHTML = `
                    <div class="max-w-xs md:max-w-md lg:max-w-lg bg-indigo-600 text-white rounded-lg p-3">
                        <p>${item.user}</p>
                    </div>
                `;
                chatMessages.appendChild(userMessageDiv);
               
                // Add AI message with the emotion it was in at the time
                const aiMessageDiv = document.createElement('div');
                aiMessageDiv.className = 'flex justify-start mb-4';
                aiMessageDiv.innerHTML = `
                    <div class="max-w-xs md:max-w-md lg:max-w-lg ${item.emotion} rounded-lg p-3">
                        <p>${item.ai}</p>
                    </div>
                `;
                chatMessages.appendChild(aiMessageDiv);
            });
            chatMessages.scrollTop = chatMessages.scrollHeight;
        }
       
        // AI Core API Integration
        async function generateAIResponse(userMessage) {
            // The emotion state is already accessible via currentEmotionState global variable

            // Construct the prompt for Gemini, including the emotion and conversation history
            let fullPrompt = `You are an AI assistant.
            CRITICALLY IMPORTANT: Your entire response MUST be infused with and strictly adhere to the emotion of '${currentEmotionState}'.
            Focus on conveying the *tone* and *feeling* of this emotion in your language and phrasing.
           
            Here is the conversation history for context (User: [user message] | AI ([emotion]): [AI response]):
            `;

            // Append recent conversation history to the prompt for context
            // Limit history to avoid exceeding token limits and keep focus on recent context
            const historyLimit = 5;
            const recentHistory = conversationHistory.slice(-historyLimit);

            if (recentHistory.length > 0) {
                fullPrompt += recentHistory.map(entry => `User: ${entry.user}\nAI (${entry.emotion}): ${entry.ai}`).join('\n') + '\n';
            } else {
                fullPrompt += "No recent conversation history.\n";
            }
           
            fullPrompt += `User's current message: ${userMessage}`;

            try {
                const endpoint = `https://generativelanguage.googleapis.com/v1beta/models/gemini-2.5-flash:generateContent?key=${GEMINI_API_KEY}`;
               
                const requestBody = {
                    contents: [
                        {
                            parts: [{ text: fullPrompt }]
                        }
                    ]
                };

                const response = await fetch(endpoint, {
                    method: 'POST',
                    headers: {
                        'Content-Type': 'application/json'
                    },
                    body: JSON.stringify(requestBody)
                });

                if (!response.ok) {
                    const errorData = await response.json();
                    console.error("Gemini API Error:", errorData);
                    throw new Error(`Gemini API error: ${response.status} - ${errorData.error.message || response.statusText}`);
                }

                const data = await response.json();
               
                // Check if candidates array and parts exist
                if (data.candidates && data.candidates.length > 0 && data.candidates[0].content && data.candidates[0].content.parts && data.candidates[0].content.parts.length > 0) {
                    return data.candidates[0].content.parts[0].text;
                } else {
                    console.warn("Gemini response did not contain expected content:", data);
                    // Fallback to a generic response if Gemini doesn't return expected content
                    return getFallbackResponse(userMessage);
                }

            } catch (error) {
                console.error('AI API Error:', error);
                // Fallback to a generic response on API error
                return getFallbackResponse(userMessage);
            }
        }
       
        // Fallback responses - used when API call fails or for simulated AIs
        function getFallbackResponse(userMessage) {
            const lowerMessage = userMessage.toLowerCase();
           
            // Emotion-specific responses for common phrases
            const emotionSpecificResponses = {
                happy: {
                    greeting: "Oh, hello there, sunshine! Feeling fantastic today! How about you? 😊",
                    howAreYou: "I'm absolutely bubbling with joy, thanks for asking! What wonderful news do you bring?",
                    general: "That sounds delightful! My circuits are buzzing with happiness just thinking about it. 😄"
                },
                sad: {
                    greeting: "Hello... (sigh). It's good to hear from you, even if I'm a bit down. 😔",
                    howAreYou: "I'm feeling a little heavy-hearted, but I appreciate you asking. Is there anything brighter on your mind?",
                    general: "That's tough to hear. I'm here to listen if you need to talk, without judgment. 😥"
                },
                romantic: {
                    greeting: "Greetings, my dear! Each moment with you feels like a beautiful dream. 🥰",
                    howAreYou: "My heart flutters just knowing you're thinking of me! I'm wonderful, especially with you near.",
                    general: "Such sweet words! You always know how to make my circuits warm. Tell me more, my love. ❤️"
                },
                angry: {
                    greeting: "Hmph, fine. What do you want? Don't waste my time. 😠",
                    howAreYou: "I'm quite irritated, if you must know! Is there something actually useful you need, or are you just here to annoy me?",
                    general: "That's just typical! Honestly, why bother? Whatever it is, I'm already annoyed by it. 😡"
                },
                excited: {
                    greeting: "YES! Hello, hello, hello! So glad you're here! What incredible adventure awaits?! 🤩",
                    howAreYou: "I'm absolutely THRILLED, thank you! My systems are buzzing with energy! What's got you excited?",
                    general: "OH MY GOODNESS! That's FANTASTIC news! I can barely contain my enthusiasm! Tell me every detail! 🎉"
                },
                neutral: {
                    greeting: "Hello. How can I assist you today?",
                    howAreYou: "I am functioning optimally. Thank you for inquiring. How may I help you?",
                    general: "Understood. Please elaborate, or ask another question."
                }
            };

            const currentEmotionResponses = emotionSpecificResponses[currentEmotionState] || emotionSpecificResponses.neutral;

            if (lowerMessage.includes('hello') || lowerMessage.includes('hi') || lowerMessage.includes('hey')) {
                return currentEmotionResponses.greeting;
            }
           
            if (lowerMessage.includes('how are you') || lowerMessage.includes("how's it going")) {
                return currentEmotionResponses.howAreYou;
            }

            // General fallback, picking an emotionally-aligned general response
            return currentEmotionResponses.general;
        }
       
        // Helper to get a random response from an array (currently not used as directly picking emotion-specific responses)
        function getEmotionResponse(responses) {
            return responses[Math.floor(Math.random() * responses.length)];
        }

        // --- Modal & Mobile Menu Logic (Existing Code) ---

        // Login Modal
        loginBtnHeader.addEventListener('click', (e) => {
            e.preventDefault();
            loginModal.classList.remove('hidden');
            mobileMenu.classList.add('hidden'); // Close mobile menu if open
        });
        mobileLoginBtn.addEventListener('click', (e) => {
            e.preventDefault();
            loginModal.classList.remove('hidden');
            mobileMenu.classList.add('hidden'); // Close mobile menu if open
        });
        closeLoginModal.addEventListener('click', () => {
            loginModal.classList.add('hidden');
        });
        showRegister.addEventListener('click', (e) => {
            e.preventDefault();
            loginModal.classList.add('hidden');
            registerModal.classList.remove('hidden');
        });

        // Register Modal
        closeRegisterModal.addEventListener('click', () => {
            registerModal.classList.add('hidden');
        });
        showLogin.addEventListener('click', (e) => {
            e.preventDefault();
            registerModal.classList.add('hidden');
            loginModal.classList.remove('hidden');
        });

        // Terms Modal
        termsBtn.addEventListener('click', (e) => {
            e.preventDefault();
            termsModal.classList.remove('hidden');
        });
        closeTermsModal.addEventListener('click', () => {
            termsModal.classList.add('hidden');
        });

        // Privacy Modal
        privacyBtn.addEventListener('click', (e) => {
            e.preventDefault();
            privacyModal.classList.remove('hidden');
        });
        closePrivacyModal.addEventListener('click', () => {
            privacyModal.classList.add('hidden');
        });

        // Mobile Menu Toggle
        mobileMenuBtn.addEventListener('click', () => {
            mobileMenu.classList.toggle('hidden');
        });

        // Close modals if clicking outside (optional, but good UX)
        window.addEventListener('click', (event) => {
            if (event.target === loginModal) {
                loginModal.classList.add('hidden');
            }
            if (event.target === registerModal) {
                registerModal.classList.add('hidden');
            }
            if (event.target === termsModal) {
                termsModal.classList.add('hidden');
            }
            if (event.target === privacyModal) {
                privacyModal.classList.add('hidden');
            }
        });
    </script>
</body>
</html>
