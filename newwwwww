<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>3D Web3 Resume Builder</title>
    <link rel="icon" type="image/x-icon" href="https://cdn-icons-png.flaticon.com/512/2504/2504932.png">
    <script src="https://cdn.jsdelivr.net/npm/ethers@6.9.0/dist/ethers.min.js"></script>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }

        body {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            min-height: 100vh;
            color: #333;
        }

        .container {
            max-width: 1200px;
            margin: 0 auto;
            padding: 20px;
        }

        .header {
            text-align: center;
            padding: 30px 0;
            color: white;
        }

        .header h1 {
            font-size: 2.8rem;
            margin-bottom: 10px;
            background: linear-gradient(to right, #fff, #f0f0f0);
            background-clip: text;
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
        }

        .header p {
            font-size: 1.2rem;
            opacity: 0.9;
            margin-bottom: 20px;
        }

        /* Steps */
        .steps {
            display: flex;
            justify-content: center;
            gap: 30px;
            margin: 30px 0;
        }

        .step {
            display: flex;
            flex-direction: column;
            align-items: center;
            color: rgba(255, 255, 255, 0.6);
            transition: all 0.3s;
        }

        .step.active {
            color: white;
            transform: scale(1.05);
        }

        .step-number {
            width: 40px;
            height: 40px;
            border-radius: 50%;
            background: rgba(255, 255, 255, 0.2);
            display: flex;
            align-items: center;
            justify-content: center;
            margin-bottom: 8px;
            font-weight: bold;
            transition: all 0.3s;
        }

        .step.active .step-number {
            background: white;
            color: #667eea;
            box-shadow: 0 5px 15px rgba(0,0,0,0.2);
        }

        /* Wallet Connection */
        .wallet-button {
            background: white;
            color: #667eea;
            border: none;
            padding: 12px 25px;
            border-radius: 50px;
            cursor: pointer;
            font-weight: bold;
            font-size: 1.1rem;
            display: inline-flex;
            align-items: center;
            gap: 10px;
            transition: all 0.2s;
            margin: 10px;
        }

        .wallet-button:hover {
            background: #f0f0f0;
            transform: translateY(-2px);
            box-shadow: 0 5px 15px rgba(0,0,0,0.1);
        }

        .wallet-info {
            background: rgba(255, 255, 255, 0.1);
            backdrop-filter: blur(10px);
            border-radius: 15px;
            padding: 20px;
            margin: 20px auto;
            max-width: 600px;
            animation: slideIn 0.5s ease;
        }

        @keyframes slideIn {
            from { opacity: 0; transform: translateY(-20px); }
            to { opacity: 1; transform: translateY(0); }
        }

        /* Main Content */
        .main-content {
            background: white;
            border-radius: 20px;
            padding: 30px;
            box-shadow: 0 20px 60px rgba(0, 0, 0, 0.3);
            margin-bottom: 30px;
            animation: fadeIn 0.5s ease;
        }

        @keyframes fadeIn {
            from { opacity: 0; }
            to { opacity: 1; }
        }

        /* Form Styles */
        .form-group {
            margin-bottom: 20px;
        }

        .form-group label {
            display: block;
            margin-bottom: 8px;
            font-weight: 600;
            color: #444;
        }

        .form-group input,
        .form-group select,
        .form-group textarea {
            width: 100%;
            padding: 12px 15px;
            border: 2px solid #ddd;
            border-radius: 8px;
            font-size: 1rem;
            transition: all 0.2s;
        }

        .form-group input:focus,
        .form-group select:focus,
        .form-group textarea:focus {
            outline: none;
            border-color: #667eea;
            box-shadow: 0 0 0 3px rgba(102, 126, 234, 0.1);
        }

        /* 3D Preview */
        .canvas-container {
            width: 100%;
            height: 400px;
            background: linear-gradient(135deg, #1a1a1a 0%, #2d2d2d 100%);
            border-radius: 15px;
            overflow: hidden;
            position: relative;
            border: 3px solid #667eea;
            box-shadow: 0 10px 30px rgba(0,0,0,0.3);
        }

        .skill-sphere {
            width: 60px;
            height: 60px;
            background: linear-gradient(135deg, #667eea, #764ba2);
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            color: white;
            font-weight: bold;
            position: absolute;
            box-shadow: 0 10px 30px rgba(0,0,0,0.3);
            animation: float 3s ease-in-out infinite;
            cursor: pointer;
            transition: transform 0.3s;
        }

        .skill-sphere:hover {
            transform: scale(1.2);
        }

        @keyframes float {
            0%, 100% { transform: translateY(0px) rotate(0deg); }
            50% { transform: translateY(-20px) rotate(10deg); }
        }

        /* Payment Box */
        .payment-box {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: white;
            padding: 30px;
            border-radius: 15px;
            text-align: center;
            animation: pulse 2s infinite;
        }

        @keyframes pulse {
            0% { box-shadow: 0 10px 30px rgba(102, 126, 234, 0.3); }
            50% { box-shadow: 0 15px 40px rgba(102, 126, 234, 0.5); }
            100% { box-shadow: 0 10px 30px rgba(102, 126, 234, 0.3); }
        }

        /* Buttons */
        .pay-button {
            background: white;
            color: #667eea;
            border: none;
            padding: 15px 40px;
            font-size: 1.2rem;
            border-radius: 50px;
            cursor: pointer;
            font-weight: bold;
            margin-top: 20px;
            width: 100%;
            transition: all 0.3s;
        }

        .pay-button:hover:not(:disabled) {
            transform: translateY(-3px);
            box-shadow: 0 15px 30px rgba(0,0,0,0.2);
        }

        /* Status Messages */
        .status-message {
            position: fixed;
            bottom: 20px;
            right: 20px;
            background: #333;
            color: white;
            padding: 15px 25px;
            border-radius: 10px;
            box-shadow: 0 5px 15px rgba(0,0,0,0.3);
            z-index: 1000;
            animation: slideInRight 0.3s ease;
        }

        @keyframes slideInRight {
            from { transform: translateX(100%); opacity: 0; }
            to { transform: translateX(0); opacity: 1; }
        }

        /* Responsive Design */
        @media (max-width: 768px) {
            .editor-layout {
                grid-template-columns: 1fr;
            }
            
            .header h1 {
                font-size: 2rem;
            }
            
            .steps {
                gap: 15px;
            }
        }

        /* Loading Spinner */
        .spinner {
            border: 3px solid rgba(255,255,255,0.3);
            border-radius: 50%;
            border-top: 3px solid white;
            width: 20px;
            height: 20px;
            animation: spin 1s linear infinite;
            display: inline-block;
            margin-right: 10px;
        }

        @keyframes spin {
            0% { transform: rotate(0deg); }
            100% { transform: rotate(360deg); }
        }

        /* Tabs */
        .form-tabs {
            display: flex;
            gap: 10px;
            margin-bottom: 25px;
            flex-wrap: wrap;
        }

        .tab {
            padding: 10px 20px;
            background: #e0e0e0;
            border: none;
            border-radius: 8px;
            cursor: pointer;
            transition: all 0.2s;
            font-weight: 600;
        }

        .tab:hover {
            background: #d0d0d0;
        }

        .tab.active {
            background: #667eea;
            color: white;
            transform: translateY(-2px);
        }
    </style>
</head>
<body>
    <div class="container">
        <!-- Header -->
        <header class="header">
            <h1>🚀 3D Web3 Resume Builder</h1>
            <p>Create stunning 3D resumes. Pay 5 USDC. Own your data.</p>
            
            <div id="walletConnect">
                <button class="wallet-button" onclick="connectWallet()">
                    <span class="wallet-icon">🔗</span> Connect Wallet
                </button>
                <div id="installMetamask" style="display: none; margin-top: 15px;">
                    <p style="color: #ffdddd; margin-bottom: 10px;">MetaMask not detected. Please install it first.</p>
                    <a href="https://metamask.io/download/" target="_blank" style="color: white; text-decoration: underline;">
                        Download MetaMask
                    </a>
                </div>
            </div>
            
            <div id="walletInfo" style="display: none;" class="wallet-info">
                <div style="display: flex; justify-content: space-between; align-items: center; margin-bottom: 15px;">
                    <div>
                        <div id="networkStatus" style="color: #ff4444; font-weight: 600;">
                            ❌ Not connected to Polygon Amoy
                        </div>
                        <div style="font-size: 0.9em; margin-top: 5px;">
                            Wallet: <span id="walletAddress"></span>
                        </div>
                    </div>
                    <button class="wallet-button" onclick="switchToAmoy()" style="padding: 8px 16px; font-size: 0.9rem;">
                        🔄 Switch Network
                    </button>
                </div>
                
                <div style="display: flex; justify-content: space-between; align-items: center; padding: 15px; background: rgba(255,255,255,0.1); border-radius: 10px;">
                    <div>
                        <div style="font-size: 0.9em; color: #ccc;">USDC Balance</div>
                        <div style="font-size: 1.5rem; font-weight: bold;">
                            <span id="usdcBalance">0.00</span> <span style="font-size: 1rem;">USDC</span>
                        </div>
                    </div>
                    <button class="wallet-button" onclick="getTestUSDC()" style="background: #00c851; color: white; padding: 8px 16px;">
                        🚰 Get Test USDC
                    </button>
                </div>
                
                <div style="margin-top: 15px; display: flex; gap: 10px;">
                    <button class="wallet-button" onclick="disconnectWallet()" style="background: #ff4444; color: white; flex: 1;">
                        Disconnect
                    </button>
                    <button class="wallet-button" onclick="copyAddress()" style="flex: 1;">
                        📋 Copy Address
                    </button>
                </div>
            </div>
        </header>

        <!-- Steps -->
        <div class="steps">
            <div class="step active" id="step1">
                <div class="step-number">1</div>
                <div class="step-title">Build Resume</div>
            </div>
            <div class="step" id="step2">
                <div class="step-number">2</div>
                <div class="step-title">Pay 5 USDC</div>
            </div>
            <div class="step" id="step3">
                <div class="step-number">3</div>
                <div class="step-title">Share & Earn</div>
            </div>
        </div>

        <!-- Main Content -->
        <main class="main-content">
            <!-- Step 1: Build Resume -->
            <div id="step1Content">
                <h2 style="text-align: center; margin-bottom: 30px; color: #444;">Design Your 3D Resume</h2>
                
                <div style="display: grid; grid-template-columns: 1fr 1fr; gap: 30px;">
                    <!-- Left: Form -->
                    <div style="background: #f8f9fa; padding: 25px; border-radius: 15px;">
                        <div class="form-tabs">
                            <button class="tab active" onclick="showTab('personal')">👤 Personal</button>
                            <button class="tab" onclick="showTab('experience')">💼 Experience</button>
                            <button class="tab" onclick="showTab('skills')">⚡ Skills</button>
                            <button class="tab" onclick="showTab('design')">🎨 Design</button>
                        </div>
                        
                        <form id="resumeForm" onsubmit="event.preventDefault(); previewResume();">
                            <!-- Personal Info -->
                            <div id="personalTab" class="tab-content">
                                <div class="form-group">
                                    <label for="fullName">Full Name *</label>
                                    <input type="text" id="fullName" placeholder="John Doe" required 
                                           oninput="updatePreview()">
                                </div>
                                <div class="form-group">
                                    <label for="email">Email *</label>
                                    <input type="email" id="email" placeholder="john@example.com" required>
                                </div>
                                <div class="form-group">
                                    <label for="jobTitle">Current Position *</label>
                                    <input type="text" id="jobTitle" placeholder="Senior Web3 Developer" required
                                           oninput="updatePreview()">
                                </div>
                                <div class="form-group">
                                    <label for="bio">Short Bio</label>
                                    <textarea id="bio" placeholder="Passionate about Web3 and blockchain technology..." 
                                              rows="3"></textarea>
                                </div>
                            </div>
                            
                            <!-- Experience -->
                            <div id="experienceTab" class="tab-content" style="display: none;">
                                <div id="experienceContainer">
                                    <div class="experience-item">
                                        <h4 style="color: #667eea; margin-bottom: 15px;">💼 Experience #1</h4>
                                        <div class="form-group">
                                            <label>Job Title</label>
                                            <input type="text" placeholder="Senior Developer">
                                        </div>
                                        <div class="form-group">
                                            <label>Company</label>
                                            <input type="text" placeholder="Tech Corp Inc.">
                                        </div>
                                        <div class="form-group">
                                            <label>Duration</label>
                                            <input type="text" placeholder="2020 - Present">
                                        </div>
                                    </div>
                                </div>
                                <button type="button" onclick="addExperience()" 
                                        style="background: #00c851; color: white; border: none; padding: 10px 20px; border-radius: 8px; cursor: pointer; margin-top: 10px;">
                                    + Add Experience
                                </button>
                            </div>
                            
                            <!-- Skills -->
                            <div id="skillsTab" class="tab-content" style="display: none;">
                                <div id="skillsContainer">
                                    <div class="skill-form-item">
                                        <h4 style="color: #667eea; margin-bottom: 15px;">⚡ Skills</h4>
                                        <div class="form-group">
                                            <label>Skill Name</label>
                                            <input type="text" value="Solidity" oninput="updateSkills()">
                                        </div>
                                        <div class="form-group">
                                            <label>Level: <span id="skillLevel1">85</span>%</label>
                                            <input type="range" min="1" max="100" value="85" 
                                                   oninput="updateSkillLevel(this, 'skillLevel1')">
                                        </div>
                                    </div>
                                </div>
                                <button type="button" onclick="addSkill()"
                                        style="background: #00c851; color: white; border: none; padding: 10px 20px; border-radius: 8px; cursor: pointer; margin-top: 10px;">
                                    + Add Skill
                                </button>
                            </div>
                            
                            <!-- Design -->
                            <div id="designTab" class="tab-content" style="display: none;">
                                <div class="form-group">
                                    <label>🎨 Theme Color</label>
                                    <div style="display: flex; gap: 15px; margin-top: 10px;">
                                        <div class="color-option" onclick="selectTheme('purple')" 
                                             style="width: 50px; height: 50px; background: linear-gradient(135deg, #667eea, #764ba2); border-radius: 10px; cursor: pointer; border: 3px solid #667eea;"></div>
                                        <div class="color-option" onclick="selectTheme('green')"
                                             style="width: 50px; height: 50px; background: linear-gradient(135deg, #00b09b, #96c93d); border-radius: 10px; cursor: pointer; border: 3px solid transparent;"></div>
                                        <div class="color-option" onclick="selectTheme('orange')"
                                             style="width: 50px; height: 50px; background: linear-gradient(135deg, #ff7e5f, #feb47b); border-radius: 10px; cursor: pointer; border: 3px solid transparent;"></div>
                                    </div>
                                </div>
                                
                                <div class="form-group">
                                    <label style="display: flex; align-items: center; gap: 10px; cursor: pointer;">
                                        <input type="checkbox" id="enable3D" checked style="width: 18px; height: 18px;">
                                        <span>Enable 3D Effects</span>
                                    </label>
                                </div>
                                
                                <div class="form-group">
                                    <label>Template Style</label>
                                    <select style="padding: 10px; border-radius: 8px; width: 100%;">
                                        <option>Modern Professional</option>
                                        <option>Creative Portfolio</option>
                                        <option>Minimalist</option>
                                    </select>
                                </div>
                            </div>
                            
                            <div style="text-align: center; margin-top: 30px;">
                                <button type="submit" 
                                        style="background: linear-gradient(135deg, #667eea, #764ba2); color: white; border: none; padding: 15px 40px; border-radius: 50px; font-size: 1.1rem; cursor: pointer; font-weight: bold;">
                                    Continue to Payment →
                                </button>
                            </div>
                        </form>
                    </div>
                    
                    <!-- Right: 3D Preview -->
                    <div style="background: #f8f9fa; padding: 25px; border-radius: 15px;">
                        <h3 style="color: #444; margin-bottom: 20px;">🎮 Live 3D Preview</h3>
                        <div class="canvas-container" id="canvas3D">
                            <!-- 3D elements will be added here by JavaScript -->
                        </div>
                        <div style="margin-top: 20px; color: #666;">
                            <p>✨ <strong>Interactive 3D Visualization</strong> - Hover over skills</p>
                            <p>🎨 <strong>Real-time Updates</strong> - Changes appear instantly</p>
                            <p>🔗 <strong>Blockchain Stored</strong> - Secured on Polygon</p>
                        </div>
                    </div>
                </div>
            </div>
            
            <!-- Step 2: Payment -->
            <div id="step2Content" style="display: none;">
                <div style="max-width: 600px; margin: 0 auto;">
                    <h2 style="text-align: center; margin-bottom: 30px; color: #444;">💳 Payment & Deployment</h2>
                    
                    <div style="background: #f0f7ff; padding: 25px; border-radius: 15px; margin-bottom: 30px;">
                        <h3 style="color: #667eea; margin-bottom: 15px;">Resume Summary</h3>
                        <div style="display: grid; grid-template-columns: 1fr 1fr; gap: 15px;">
                            <div>
                                <strong>Name:</strong> <span id="summaryName">John Doe</span>
                            </div>
                            <div>
                                <strong>Position:</strong> <span id="summaryPosition">Senior Developer</span>
                            </div>
                            <div>
                                <strong>Skills:</strong> <span id="summarySkills">4</span>
                            </div>
                            <div>
                                <strong>Theme:</strong> <span id="summaryTheme">Professional</span>
                            </div>
                        </div>
                    </div>
                    
                    <div class="payment-box">
                        <h3 style="margin-bottom: 10px;">Total Cost: 5 USDC</h3>
                        <p style="opacity: 0.9; margin-bottom: 20px;">+ network gas fees</p>
                        
                        <div style="background: rgba(255,255,255,0.1); padding: 20px; border-radius: 10px; margin-bottom: 20px;">
                            <h4 style="margin-bottom: 15px;">Requirements:</h4>
                            <div id="requirementWallet" style="display: flex; align-items: center; gap: 10px; margin-bottom: 10px; color: #ff4444;">
                                <span>❌</span> <span>Connect Wallet</span>
                            </div>
                            <div id="requirementNetwork" style="display: flex; align-items: center; gap: 10px; margin-bottom: 10px; color: #ff4444;">
                                <span>❌</span> <span>Polygon Amoy Network</span>
                            </div>
                            <div id="requirementBalance" style="display: flex; align-items: center; gap: 10px; color: #ff4444;">
                                <span>❌</span> <span>5 USDC Balance</span>
                            </div>
                        </div>
                        
                        <button id="payButton" class="pay-button" onclick="processPayment()" disabled>
                            Pay 5 USDC to Create Resume
                        </button>
                        
                        <p style="margin-top: 15px; font-size: 0.9em; opacity: 0.8;">
                            Need test USDC? Use the "Get Test USDC" button above.
                        </p>
                    </div>
                    
                    <div id="paymentStatus" style="display: none; margin-top: 20px; text-align: center; padding: 15px; background: #f0f7ff; border-radius: 10px;">
                        <!-- Status messages will appear here -->
                    </div>
                </div>
            </div>
            
            <!-- Step 3: Success -->
            <div id="step3Content" style="display: none;">
                <div style="text-align: center; padding: 30px;">
                    <div style="font-size: 4rem; margin-bottom: 20px;">🎉</div>
                    <h2 style="color: #444; margin-bottom: 10px;">Resume Created Successfully!</h2>
                    <p style="color: #666; margin-bottom: 30px; font-size: 1.1rem;">
                        Your 3D resume is now stored on the Polygon blockchain
                    </p>
                    
                    <div style="display: grid; grid-template-columns: 1fr 1fr; gap: 30px; margin-bottom: 40px;">
                        <div style="text-align: left;">
                            <h3 style="color: #667eea; margin-bottom: 15px;">📄 Resume Details</h3>
                            <div style="background: #f8f9fa; padding: 20px; border-radius: 10px;">
                                <p><strong>Name:</strong> <span id="finalName">John Doe</span></p>
                                <p><strong>Resume ID:</strong> <span id="resumeId">#RES12345</span></p>
                                <p><strong>Contract:</strong> <span style="font-family: monospace;">0x115E26...C2F30</span></p>
                                <p><strong>Created:</strong> <span id="createdDate">Just now</span></p>
                                <p><strong>Cost:</strong> 5 USDC</p>
                            </div>
                        </div>
                        
                        <div style="text-align: left;">
                            <h3 style="color: #667eea; margin-bottom: 15px;">🔗 Share & Earn</h3>
                            <div style="background: #f8f9fa; padding: 20px; border-radius: 10px;">
                                <p style="margin-bottom: 15px;">Share your resume and earn 1 USDC per referral!</p>
                                <div style="display: flex; gap: 10px; margin-bottom: 15px;">
                                    <button onclick="copyResumeLink()" 
                                            style="flex: 1; background: #667eea; color: white; border: none; padding: 10px; border-radius: 8px; cursor: pointer;">
                                        📋 Copy Link
                                    </button>
                                    <button onclick="shareOnTwitter()"
                                            style="flex: 1; background: #1DA1F2; color: white; border: none; padding: 10px; border-radius: 8px; cursor: pointer;">
                                        🐦 Tweet
                                    </button>
                                </div>
                                <button onclick="downloadResume()"
                                        style="width: 100%; background: #00c851; color: white; border: none; padding: 12px; border-radius: 8px; cursor: pointer; font-weight: bold;">
                                    📥 Download Resume PDF
                                </button>
                            </div>
                        </div>
                    </div>
                    
                    <button onclick="createNewResume()" 
                            style="background: #667eea; color: white; border: none; padding: 15px 40px; border-radius: 50px; font-size: 1.1rem; cursor: pointer; font-weight: bold;">
                        🚀 Create Another Resume
                    </button>
                </div>
            </div>
        </main>
        
        <footer style="text-align: center; color: white; padding: 30px; opacity: 0.8;">
            <p>Smart Contract: 0x115E26CEA5D31a3bF4238B3053279F35De3C2F30</p>
            <p>Built on Polygon Amoy Testnet • 5 USDC per resume</p>
            <p style="margin-top: 20px; font-size: 0.9em;">
                <a href="https://faucet.polygon.technology/" target="_blank" style="color: white;">Get Test USDC</a> • 
                <a href="https://amoy.polygonscan.com/address/0x115E26CEA5D31a3bF4238B3053279F35De3C2F30" target="_blank" style="color: white;">View Contract</a>
            </p>
        </footer>
    </div>

    <script>
        // ===========================
        // APPLICATION STATE
        // ===========================
        let walletConnected = false;
        let currentNetwork = null;
        let walletAddress = "";
        let usdcBalance = "0";
        let currentStep = 1;
        let resumeData = {
            name: "John Doe",
            title: "Senior Web3 Developer",
            skills: ["Solidity", "React", "Web3", "3D"],
            theme: "purple"
        };

        // ===========================
        // INITIALIZATION
        // ===========================
        document.addEventListener('DOMContentLoaded', function() {
            console.log("3D Resume Builder Initialized");
            
            // Check if MetaMask is installed
            checkMetaMask();
            
            // Initialize 3D preview
            init3DPreview();
            
            // Set current date
            document.getElementById('createdDate').textContent = new Date().toLocaleDateString();
            
            // Generate random resume ID
            document.getElementById('resumeId').textContent = '#RES' + Math.floor(10000 + Math.random() * 90000);
        });

        // ===========================
        // METAMASK CONNECTION
        // ===========================
        async function checkMetaMask() {
            if (typeof window.ethereum !== 'undefined') {
                console.log("MetaMask detected");
                document.getElementById('installMetamask').style.display = 'none';
                
                // Check if already connected
                try {
                    const accounts = await window.ethereum.request({ method: 'eth_accounts' });
                    if (accounts.length > 0) {
                        walletAddress = accounts[0];
                        walletConnected = true;
                        updateWalletUI();
                        await checkNetwork();
                    }
                } catch (error) {
                    console.log("No existing connection");
                }
                
                // Set up event listeners
                window.ethereum.on('accountsChanged', handleAccountsChanged);
                window.ethereum.on('chainChanged', handleChainChanged);
                
            } else {
                console.log("MetaMask not installed");
                document.getElementById('installMetamask').style.display = 'block';
                showStatus("Please install MetaMask to continue", "error");
            }
        }

        async function connectWallet() {
            if (typeof window.ethereum === 'undefined') {
                showStatus("Please install MetaMask first", "error");
                return;
            }

            try {
                showStatus("Connecting to MetaMask...", "info");
                
                // Request account access
                const accounts = await window.ethereum.request({ 
                    method: 'eth_requestAccounts' 
                });
                
                walletAddress = accounts[0];
                walletConnected = true;
                
                updateWalletUI();
                await checkNetwork();
                
                showStatus("Wallet connected successfully!", "success");
                
            } catch (error) {
                console.error("Wallet connection error:", error);
                
                if (error.code === 4001) {
                    showStatus("Wallet connection rejected by user", "error");
                } else {
                    showStatus("Failed to connect wallet: " + error.message, "error");
                }
            }
        }

        async function checkNetwork() {
            try {
                const chainId = await window.ethereum.request({ method: 'eth_chainId' });
                currentNetwork = chainId;
                updateNetworkUI();
                
                if (walletConnected) {
                    await checkUSDCBalance();
                }
                
            } catch (error) {
                console.error("Network check error:", error);
            }
        }

        async function switchToAmoy() {
            const amoyChainId = "0x13882"; // Polygon Amoy
    
            try {
                await window.ethereum.request({
                    method: 'wallet_switchEthereumChain',
                    params: [{ chainId: amoyChainId }],
                });
                showStatus("Switched to Polygon Amoy", "success");
            } catch (switchError) {
                // This error code indicates that the chain has not been added to MetaMask
                if (switchError.code === 4902) {
                    try {
                        await window.ethereum.request({
                            method: 'wallet_addEthereumChain',
                            params: [
                                {
                                    chainId: amoyChainId,
                                    chainName: 'Polygon Amoy Testnet',
                                    nativeCurrency: {
                                        name: 'MATIC',
                                        symbol: 'MATIC',
                                        decimals: 18
                                    },
                                    rpcUrls: ['https://rpc-amoy.polygon.technology/'],
                                    blockExplorerUrls: ['https://amoy.polygonscan.com/']
                                },
                            ],
                        });
                        showStatus("Polygon Amoy network added", "success");
                    } catch (addError) {
                        console.error("Error adding network:", addError);
                        showStatus("Failed to add Polygon Amoy network", "error");
                    }
                } else {
                    console.error("Error switching network:", switchError);
                    showStatus("Failed to switch network", "error");
                }
            }
        }

        // ===========================
        // UI UPDATES
        // ===========================
        function updateWalletUI() {
            if (walletConnected) {
                document.getElementById('walletConnect').style.display = 'none';
                document.getElementById('walletInfo').style.display = 'block';
                
                // Shorten wallet address for display
                const shortAddress = walletAddress.substring(0, 6) + '...' + walletAddress.substring(walletAddress.length - 4);
                document.getElementById('walletAddress').textContent = shortAddress;
                
                // Update payment requirements
                updatePaymentRequirements();
            }
        }

        function updateNetworkUI() {
            const networkStatus = document.getElementById('networkStatus');
            const amoyChainId = "0x13882";
            
            if (currentNetwork === amoyChainId) {
                networkStatus.innerHTML = '✅ Connected to Polygon Amoy';
                networkStatus.style.color = '#00ff88';
            } else {
                networkStatus.innerHTML = '❌ Not connected to Polygon Amoy';
                networkStatus.style.color = '#ff4444';
            }
            
            updatePaymentRequirements();
        }

        async function checkUSDCBalance() {
            // For demo purposes, we'll use a mock balance
            // In production, you would connect to the USDC contract
            
            if (currentNetwork === "0x13882") { // Polygon Amoy
                // Simulate API call delay
                setTimeout(() => {
                    // Generate random balance between 0 and 20 for demo
                    usdcBalance = (Math.random() * 20).toFixed(2);
                    document.getElementById('usdcBalance').textContent = usdcBalance;
                    updatePaymentRequirements();
                }, 1000);
            }
        }

        function updatePaymentRequirements() {
            const amoyChainId = "0x13882";
            
            // Update requirement displays
            const reqWallet = document.getElementById('requirementWallet');
            const reqNetwork = document.getElementById('requirementNetwork');
            const reqBalance = document.getElementById('requirementBalance');
            const payButton = document.getElementById('payButton');
            
            // Wallet requirement
            if (walletConnected) {
                reqWallet.innerHTML = '<span>✅</span> <span>Wallet Connected</span>';
                reqWallet.style.color = '#00ff88';
            } else {
                reqWallet.innerHTML = '<span>❌</span> <span>Connect Wallet</span>';
                reqWallet.style.color = '#ff4444';
            }
            
            // Network requirement
            if (currentNetwork === amoyChainId) {
                reqNetwork.innerHTML = '<span>✅</span> <span>Polygon Amoy Network</span>';
                reqNetwork.style.color = '#00ff88';
            } else {
                reqNetwork.innerHTML = '<span>❌</span> <span>Polygon Amoy Network</span>';
                reqNetwork.style.color = '#ff4444';
            }
            
            // Balance requirement
            const hasEnoughBalance = parseFloat(usdcBalance) >= 5;
            if (hasEnoughBalance) {
                reqBalance.innerHTML = `<span>✅</span> <span>5 USDC Balance (You have: ${usdcBalance})</span>`;
                reqBalance.style.color = '#00ff88';
            } else {
                reqBalance.innerHTML = `<span>❌</span> <span>5 USDC Balance (You have: ${usdcBalance})</span>`;
                reqBalance.style.color = '#ff4444';
            }
            
            // Enable/disable pay button
            const canPay = walletConnected && currentNetwork === amoyChainId && hasEnoughBalance;
            payButton.disabled = !canPay;
        }

        // ===========================
        // 3D PREVIEW FUNCTIONS
        // ===========================
        function init3DPreview() {
            updatePreview();
        }

        function updatePreview() {
            const canvas = document.getElementById('canvas3D');
            const name = document.getElementById('fullName').value || 'Your Name';
            const title = document.getElementById('jobTitle').value || 'Web3 Developer';
            
            // Update summary
            document.getElementById('summaryName').textContent = name;
            document.getElementById('summaryPosition').textContent = title;
            document.getElementById('finalName').textContent = name;
            
            // Clear canvas
            canvas.innerHTML = '';
            
            // Add name display
            const nameDisplay = document.createElement('div');
            nameDisplay.className = 'name-display';
            nameDisplay.textContent = name;
            nameDisplay.style.cssText = `
                position: absolute;
                top: 30%;
                left: 50%;
                transform: translate(-50%, -50%);
                color: white;
                font-size: 2rem;
                font-weight: bold;
                text-align: center;
                width: 100%;
            `;
            canvas.appendChild(nameDisplay);
            
            // Add title display
            const titleDisplay = document.createElement('div');
            titleDisplay.className = 'title-display';
            titleDisplay.textContent = title;
            titleDisplay.style.cssText = `
                position: absolute;
                top: 40%;
                left: 50%;
                transform: translate(-50%, -50%);
                color: #ddd;
                font-size: 1.2rem;
                text-align: center;
                width: 100%;
            `;
            canvas.appendChild(titleDisplay);
            
            // Add skill spheres
            const skills = ['SOL', 'WEB3', 'REACT', '3D'];
            const colors = ['#667eea', '#00b09b', '#ff7e5f', '#9d50bb'];
            
            skills.forEach((skill, index) => {
                const sphere = document.createElement('div');
                sphere.className = 'skill-sphere';
                sphere.textContent = skill;
                sphere.title = `${skill} - ${Math.floor(Math.random() * 30) + 70}% proficiency`;
                
                // Position spheres in a circle
                const angle = (index / skills.length) * Math.PI * 2;
                const radius = 100;
                const centerX = 50; // percentage
                const centerY = 60; // percentage
                
                const x = centerX + radius * Math.cos(angle);
                const y = centerY + radius * Math.sin(angle);
                
                sphere.style.cssText = `
                    left: ${x}%;
                    top: ${y}%;
                    background: linear-gradient(135deg, ${colors[index]}, ${colors[(index + 1) % colors.length]});
                    animation-delay: ${index * 0.5}s;
                `;
                
                // Add hover effect
                sphere.onmouseenter = function() {
                    this.style.transform = 'scale(1.3)';
                    this.style.zIndex = '100';
                };
                
                sphere.onmouseleave = function() {
                    this.style.transform = 'scale(1)';
                    this.style.zIndex = '1';
                };
                
                canvas.appendChild(sphere);
            });
        }

        function updateSkills() {
            // Update skills in 3D preview
            updatePreview();
        }

        function updateSkillLevel(slider, spanId) {
            document.getElementById(spanId).textContent = slider.value;
        }

        function selectTheme(theme) {
            resumeData.theme = theme;
            
            // Update color option borders
            document.querySelectorAll('.color-option').forEach(option => {
                option.style.border = '3px solid transparent';
            });
            event.target.style.border = '3px solid #667eea';
            
            // Update summary
            document.getElementById('summaryTheme').textContent = 
                theme === 'purple' ? 'Professional' : 
                theme === 'green' ? 'Modern' : 'Creative';
        }

        // ===========================
        // FORM FUNCTIONS
        // ===========================
        function showTab(tabName) {
            // Update active tab button
            document.querySelectorAll('.tab').forEach(tab => {
                tab.classList.remove('active');
            });
            event.target.classList.add('active');
            
            // Show selected tab content
            document.querySelectorAll('.tab-content').forEach(content => {
                content.style.display = 'none';
            });
            document.getElementById(tabName + 'Tab').style.display = 'block';
        }

        function addExperience() {
            const container = document.getElementById('experienceContainer');
            const count = container.children.length + 1;
            
            const experience = document.createElement('div');
            experience.className = 'experience-item';
            experience.innerHTML = `
                <h4 style="color: #667eea; margin-bottom: 15px;">💼 Experience #${count}</h4>
                <div class="form-group">
                    <label>Job Title</label>
                    <input type="text" placeholder="Position Title">
                </div>
                <div class="form-group">
                    <label>Company</label>
                    <input type="text" placeholder="Company Name">
                </div>
                <div class="form-group">
                    <label>Duration</label>
                    <input type="text" placeholder="YYYY - YYYY">
                </div>
                <button type="button" onclick="removeExperience(this)"
                        style="background: #ff4444; color: white; border: none; padding: 8px 15px; border-radius: 5px; cursor: pointer; font-size: 0.9rem;">
                    Remove
                </button>
            `;
            
            container.appendChild(experience);
        }

        function removeExperience(button) {
            const container = document.getElementById('experienceContainer');
            if (container.children.length > 1) {
                button.parentElement.remove();
                
                // Update experience numbers
                const experiences = container.querySelectorAll('.experience-item');
                experiences.forEach((exp, index) => {
                    exp.querySelector('h4').textContent = `💼 Experience #${index + 1}`;
                });
            }
        }

        function addSkill() {
            const container = document.getElementById('skillsContainer');
            const count = container.children.length + 1;
            
            const skill = document.createElement('div');
            skill.className = 'skill-form-item';
            skill.innerHTML = `
                <h4 style="color: #667eea; margin-bottom: 15px;">⚡ Skill #${count}</h4>
                <div class="form-group">
                    <label>Skill Name</label>
                    <input type="text" placeholder="Skill Name" oninput="updateSkills()">
                </div>
                <div class="form-group">
                    <label>Level: <span id="skillLevel${count}">50</span>%</label>
                    <input type="range" min="1" max="100" value="50" 
                           oninput="updateSkillLevel(this, 'skillLevel${count}')">
                </div>
                <button type="button" onclick="removeSkill(this)"
                        style="background: #ff4444; color: white; border: none; padding: 8px 15px; border-radius: 5px; cursor: pointer; font-size: 0.9rem;">
                    Remove
                </button>
            `;
            
            container.appendChild(skill);
        }

        function removeSkill(button) {
            const container = document.getElementById('skillsContainer');
            if (container.children.length > 1) {
                button.parentElement.remove();
            }
        }

        // ===========================
        // STEP NAVIGATION
        // ===========================
        function previewResume() {
            // Validate form
            const name = document.getElementById('fullName').value;
            const email = document.getElementById('email').value;
            const title = document.getElementById('jobTitle').value;
            
            if (!name || !email || !title) {
                showStatus("Please fill in all required fields", "error");
                return;
            }
            
            // Count skills
            const skillCount = document.getElementById('skillsContainer').children.length;
            document.getElementById('summarySkills').textContent = skillCount;
            
            // Go to step 2
            goToStep(2);
        }

        function goToStep(step) {
            currentStep = step;
            
            // Update step indicators
            document.querySelectorAll('.step').forEach((stepEl, index) => {
                if (index + 1 === step) {
                    stepEl.classList.add('active');
                } else {
                    stepEl.classList.remove('active');
                }
            });
            
            // Show step content
            document.getElementById('step1Content').style.display = step === 1 ? 'block' : 'none';
            document.getElementById('step2Content').style.display = step === 2 ? 'block' : 'none';
            document.getElementById('step3Content').style.display = step === 3 ? 'block' : 'none';
            
            // Scroll to top
            window.scrollTo({ top: 0, behavior: 'smooth' });
        }

        // ===========================
        // PAYMENT PROCESSING
        // ===========================
        async function processPayment() {
            const amoyChainId = "0x13882";
            
            // Validate requirements
            if (!walletConnected) {
                showStatus("Please connect your wallet first", "error");
                return;
            }
            
            if (currentNetwork !== amoyChainId) {
                showStatus("Please switch to Polygon Amoy network", "error");
                return;
            }
            
            if (parseFloat(usdcBalance) < 5) {
                showStatus("Insufficient USDC balance. Get test USDC from faucet.", "error");
                return;
            }
            
            // Show payment status
            const statusEl = document.getElementById('paymentStatus');
            statusEl.style.display = 'block';
            statusEl.innerHTML = `
                <div style="display: flex; align-items: center; justify-content: center; gap: 10px;">
                    <div class="spinner"></div>
                    <span>Processing payment...</span>
                </div>
            `;
            
            try {
                // Simulate payment process (in production, this would call your smart contract)
                
                // Step 1: Approve USDC
                statusEl.innerHTML = `
                    <div style="display: flex; align-items: center; justify-content: center; gap: 10px;">
                        <div class="spinner"></div>
                        <span>Approving 5 USDC...</span>
                    </div>
                `;
                await sleep(2000);
                
                // Step 2: Processing payment
                statusEl.innerHTML = `
                    <div style="display: flex; align-items: center; justify-content: center; gap: 10px;">
                        <div class="spinner"></div>
                        <span>Processing payment on blockchain...</span>
                    </div>
                `;
                await sleep(3000);
                
                // Step 3: Creating resume
                statusEl.innerHTML = `
                    <div style="display: flex; align-items: center; justify-content: center; gap: 10px;">
                        <div class="spinner"></div>
                        <span>Creating your 3D resume...</span>
                    </div>
                `;
                await sleep(2000);
                
                // Step 4: Success
                statusEl.innerHTML = `
                    <div style="color: #00ff88; text-align: center;">
                        <div style="font-size: 2rem; margin-bottom: 10px;">✅</div>
                        <div style="font-weight: bold; margin-bottom: 5px;">Payment Successful!</div>
                        <div>Your resume has been created on the blockchain.</div>
                    </div>
                `;
                
                // Update USDC balance (simulate deduction)
                usdcBalance = (parseFloat(usdcBalance) - 5).toFixed(2);
                document.getElementById('usdcBalance').textContent = usdcBalance;
                
                // Go to step 3 after delay
                setTimeout(() => {
                    goToStep(3);
                    statusEl.style.display = 'none';
                    showStatus("Resume created successfully!", "success");
                }, 2000);
                
            } catch (error) {
                statusEl.innerHTML = `
                    <div style="color: #ff4444; text-align: center;">
                        <div style="font-size: 2rem; margin-bottom: 10px;">❌</div>
                        <div style="font-weight: bold; margin-bottom: 5px;">Payment Failed</div>
                        <div>${error.message || "Please try again"}</div>
                    </div>
                `;
                showStatus("Payment failed: " + error.message, "error");
            }
        }

        // ===========================
        // SUCCESS STEP FUNCTIONS
        // ===========================
        function copyResumeLink() {
            const link = `https://resume3d.app/resume/${walletAddress.substring(0, 8)}`;
            navigator.clipboard.writeText(link)
                .then(() => showStatus("Resume link copied to clipboard!", "success"))
                .catch(() => showStatus("Failed to copy link", "error"));
        }

        function shareOnTwitter() {
            const text = encodeURIComponent(`Just created my 3D Web3 resume on Polygon! 🚀 Built with @0xResumeBuilder`);
            const url = encodeURIComponent(`https://resume3d.app/resume/${walletAddress.substring(0, 8)}`);
            window.open(`https://twitter.com/intent/tweet?text=${text}&url=${url}`, '_blank');
        }

        function downloadResume() {
            // Create a JSON file with resume data
            const data = {
                ...resumeData,
                walletAddress: walletAddress,
                created: new Date().toISOString(),
                contract: "0x115E26CEA5D31a3bF4238B3053279F35De3C2F30",
                network: "Polygon Amoy"
            };
            
            const dataStr = JSON.stringify(data, null, 2);
            const dataBlob = new Blob([dataStr], { type: 'application/json' });
            
            const url = URL.createObjectURL(dataBlob);
            const link = document.createElement('a');
            link.href = url;
            link.download = `resume-${walletAddress.substring(0, 8)}.json`;
            document.body.appendChild(link);
            link.click();
            document.body.removeChild(link);
            URL.revokeObjectURL(url);
            
            showStatus("Resume downloaded as JSON file!", "success");
        }

        function createNewResume() {
            // Reset form
            document.getElementById('resumeForm').reset();
            
            // Reset skills and experience
            document.getElementById('skillsContainer').innerHTML = `
                <div class="skill-form-item">
                    <h4 style="color: #667eea; margin-bottom: 15px;">⚡ Skills</h4>
                    <div class="form-group">
                        <label>Skill Name</label>
                        <input type="text" value="Solidity" oninput="updateSkills()">
                    </div>
                    <div class="form-group">
                        <label>Level: <span id="skillLevel1">85</span>%</label>
                        <input type="range" min="1" max="100" value="85" 
                               oninput="updateSkillLevel(this, 'skillLevel1')">
                    </div>
                </div>
            `;
            
            document.getElementById('experienceContainer').innerHTML = `
                <div class="experience-item">
                    <h4 style="color: #667eea; margin-bottom: 15px;">💼 Experience #1</h4>
                    <div class="form-group">
                        <label>Job Title</label>
                        <input type="text" placeholder="Senior Developer">
                    </div>
                    <div class="form-group">
                        <label>Company</label>
                        <input type="text" placeholder="Tech Corp Inc.">
                    </div>
                    <div class="form-group">
                        <label>Duration</label>
                        <input type="text" placeholder="2020 - Present">
                    </div>
                </div>
            `;
            
            // Go back to step 1
            goToStep(1);
            updatePreview();
            showStatus("Ready to create a new resume!", "info");
        }

        // ===========================
        // UTILITY FUNCTIONS
        // ===========================
        function getTestUSDC() {
            window.open('https://faucet.polygon.technology/', '_blank');
            showStatus("Opening Polygon faucet in new tab...", "info");
        }

        function copyAddress() {
            navigator.clipboard.writeText(walletAddress)
                .then(() => showStatus("Wallet address copied!", "success"))
                .catch(() => showStatus("Failed to copy address", "error"));
        }

        function disconnectWallet() {
            walletConnected = false;
            walletAddress = "";
            currentNetwork = null;
            
            document.getElementById('walletConnect').style.display = 'block';
            document.getElementById('walletInfo').style.display = 'none';
            
            showStatus("Wallet disconnected", "info");
        }

        function showStatus(message, type = "info") {
            // Remove existing status messages
            const existing = document.querySelectorAll('.status-message');
            existing.forEach(el => el.remove());
            
            // Create new status message
            const status = document.createElement('div');
            status.className = 'status-message';
            status.textContent = message;
            
            // Set color based on type
            if (type === "error") {
                status.style.background = "#ff4444";
            } else if (type === "success") {
                status.style.background = "#00c851";
            } else {
                status.style.background = "#333";
            }
            
            document.body.appendChild(status);
            
            // Remove after 3 seconds
            setTimeout(() => {
                if (status.parentNode) {
                    status.style.animation = 'slideInRight 0.3s ease reverse';
                    setTimeout(() => {
                        if (status.parentNode) {
                            status.parentNode.removeChild(status);
                        }
                    }, 300);
                }
            }, 3000);
        }

        function sleep(ms) {
            return new Promise(resolve => setTimeout(resolve, ms));
        }

        // ===========================
        // EVENT HANDLERS
        // ===========================
        function handleAccountsChanged(accounts) {
            if (accounts.length === 0) {
                // User disconnected wallet
                walletConnected = false;
                walletAddress = "";
                document.getElementById('walletConnect').style.display = 'block';
                document.getElementById('walletInfo').style.display = 'none';
                showStatus("Wallet disconnected", "info");
            } else if (accounts[0] !== walletAddress) {
                // User switched accounts
                walletAddress = accounts[0];
                updateWalletUI();
                showStatus("Account switched", "info");
            }
        }

        function handleChainChanged(chainId) {
            currentNetwork = chainId;
            updateNetworkUI();
            showStatus("Network changed", "info");
        }

        // ===========================
        // FORM INPUT EVENT LISTENERS
        // ===========================
        document.getElementById('fullName').addEventListener('input', updatePreview);
        document.getElementById('jobTitle').addEventListener('input', updatePreview);
    </script>
</body>
</html>
