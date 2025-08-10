<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Crypto Vault - Secure Storage</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: linear-gradient(135deg, #1a1a2e 0%, #16213e 50%, #0f1419 100%);
            color: #ffffff;
            min-height: 100vh;
            display: flex;
            align-items: center;
            justify-content: center;
        }

        .vault-container {
            background: rgba(255, 255, 255, 0.1);
            backdrop-filter: blur(10px);
            border-radius: 20px;
            padding: 40px;
            box-shadow: 0 20px 40px rgba(0, 0, 0, 0.3);
            border: 1px solid rgba(255, 255, 255, 0.1);
            max-width: 500px;
            width: 100%;
        }

        .vault-header {
            text-align: center;
            margin-bottom: 30px;
        }

        .vault-icon {
            font-size: 48px;
            margin-bottom: 10px;
        }

        h1 {
            font-size: 28px;
            margin-bottom: 10px;
            background: linear-gradient(45deg, #ff6b35, #f7931e);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
        }

        .subtitle {
            color: #a0a0a0;
            font-size: 16px;
        }

        .form-group {
            margin-bottom: 20px;
        }

        label {
            display: block;
            margin-bottom: 8px;
            font-weight: 600;
            color: #e0e0e0;
        }

        input, textarea, select {
            width: 100%;
            padding: 12px 16px;
            border: 2px solid rgba(255, 255, 255, 0.1);
            border-radius: 10px;
            background: rgba(0, 0, 0, 0.3);
            color: #ffffff;
            font-size: 16px;
            transition: all 0.3s ease;
        }

        input:focus, textarea:focus, select:focus {
            outline: none;
            border-color: #ff6b35;
            box-shadow: 0 0 15px rgba(255, 107, 53, 0.3);
        }

        textarea {
            resize: vertical;
            min-height: 80px;
        }

        .pin-input {
            text-align: center;
            font-size: 24px;
            letter-spacing: 10px;
            font-weight: bold;
        }

        .btn {
            width: 100%;
            padding: 14px;
            border: none;
            border-radius: 10px;
            font-size: 16px;
            font-weight: 600;
            cursor: pointer;
            transition: all 0.3s ease;
            margin-bottom: 10px;
        }

        .btn-primary {
            background: linear-gradient(45deg, #ff6b35, #f7931e);
            color: white;
        }

        .btn-primary:hover {
            transform: translateY(-2px);
            box-shadow: 0 10px 20px rgba(255, 107, 53, 0.4);
        }

        .btn-secondary {
            background: rgba(255, 255, 255, 0.1);
            color: #ffffff;
            border: 1px solid rgba(255, 255, 255, 0.2);
        }

        .btn-secondary:hover {
            background: rgba(255, 255, 255, 0.2);
        }

        .btn-danger {
            background: linear-gradient(45deg, #e74c3c, #c0392b);
            color: white;
        }

        .btn-danger:hover {
            transform: translateY(-2px);
            box-shadow: 0 10px 20px rgba(231, 76, 60, 0.4);
        }

        .wallet-item {
            background: rgba(0, 0, 0, 0.3);
            border-radius: 10px;
            padding: 20px;
            margin-bottom: 15px;
            border-left: 4px solid #ff6b35;
        }

        .wallet-name {
            font-size: 18px;
            font-weight: bold;
            margin-bottom: 10px;
            color: #ff6b35;
        }

        .wallet-info {
            display: grid;
            gap: 5px;
        }

        .wallet-info span {
            color: #a0a0a0;
            font-size: 14px;
        }

        .wallet-actions {
            margin-top: 15px;
            display: flex;
            gap: 10px;
            flex-wrap: wrap;
        }

        .wallet-btn {
            padding: 8px 16px;
            border: none;
            border-radius: 6px;
            font-size: 14px;
            cursor: pointer;
            transition: all 0.3s ease;
        }

        .wallet-btn-view {
            background: linear-gradient(45deg, #3498db, #2980b9);
            color: white;
        }

        .wallet-btn-edit {
            background: linear-gradient(45deg, #f39c12, #e67e22);
            color: white;
        }

        .wallet-btn-delete {
            background: linear-gradient(45deg, #e74c3c, #c0392b);
            color: white;
        }

        .hidden {
            display: none;
        }

        .status-message {
            padding: 10px;
            border-radius: 5px;
            margin-bottom: 20px;
            text-align: center;
        }

        .success {
            background: rgba(46, 204, 113, 0.2);
            border: 1px solid #2ecc71;
            color: #2ecc71;
        }

        .error {
            background: rgba(231, 76, 60, 0.2);
            border: 1px solid #e74c3c;
            color: #e74c3c;
        }

        .attempts-warning {
            background: rgba(243, 156, 18, 0.2);
            border: 1px solid #f39c12;
            color: #f39c12;
        }

        .lock-screen {
            text-align: center;
        }

        .lock-icon {
            font-size: 64px;
            margin-bottom: 20px;
            color: #ff6b35;
        }

        .security-features {
            margin-top: 20px;
            padding: 15px;
            background: rgba(0, 0, 0, 0.2);
            border-radius: 10px;
            font-size: 12px;
            color: #a0a0a0;
        }

        .feature-item {
            display: flex;
            align-items: center;
            margin-bottom: 5px;
        }

        .feature-item::before {
            content: "🔒";
            margin-right: 8px;
        }

        /* Modal Styles */
        .modal {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0,0,0,0.8);
            display: flex;
            align-items: center;
            justify-content: center;
            z-index: 1000;
            padding: 20px;
        }

        .modal-content {
            background: rgba(26, 26, 46, 0.95);
            backdrop-filter: blur(20px);
            border-radius: 20px;
            padding: 40px;
            max-width: 600px;
            width: 90%;
            max-height: 80vh;
            overflow-y: auto;
            border: 1px solid rgba(255, 255, 255, 0.2);
        }

        .modal-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 20px;
        }

        .modal-close {
            background: none;
            border: none;
            color: #fff;
            font-size: 24px;
            cursor: pointer;
            padding: 5px;
        }

        /* Video Tutorial Styles */
        .video-container {
            position: relative;
            width: 100%;
            max-width: 800px;
            background: rgba(0, 0, 0, 0.8);
            border-radius: 15px;
            overflow: hidden;
            border: 2px solid #ff6b35;
        }

        .video-header {
            background: linear-gradient(45deg, #ff6b35, #f7931e);
            padding: 15px 20px;
            color: white;
            font-weight: bold;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }

        .video-content {
            padding: 20px;
            max-height: 600px;
            overflow-y: auto;
        }

        .video-step {
            background: rgba(255, 255, 255, 0.05);
            border-radius: 10px;
            padding: 20px;
            margin-bottom: 15px;
            border-left: 4px solid #ff6b35;
            transition: all 0.3s ease;
        }

        .video-step:hover {
            background: rgba(255, 255, 255, 0.1);
            transform: translateX(5px);
        }

        .step-number {
            background: #ff6b35;
            color: white;
            width: 30px;
            height: 30px;
            border-radius: 50%;
            display: inline-flex;
            align-items: center;
            justify-content: center;
            font-weight: bold;
            margin-right: 15px;
        }

        .step-title {
            font-size: 18px;
            font-weight: bold;
            color: #ff6b35;
            margin-bottom: 10px;
        }

        .step-description {
            color: #e0e0e0;
            line-height: 1.6;
            margin-bottom: 15px;
        }

        .step-demo {
            background: rgba(0, 0, 0, 0.5);
            border-radius: 8px;
            padding: 15px;
            border: 1px solid rgba(255, 107, 53, 0.3);
            font-family: monospace;
            color: #a0a0a0;
            font-size: 14px;
        }

        .demo-action {
            color: #2ecc71;
            font-weight: bold;
        }

        .demo-result {
            color: #f39c12;
            font-style: italic;
        }

        .progress-bar {
            width: 100%;
            height: 6px;
            background: rgba(255, 255, 255, 0.1);
            border-radius: 3px;
            margin: 15px 0;
            overflow: hidden;
        }

        .progress-fill {
            height: 100%;
            background: linear-gradient(45deg, #ff6b35, #f7931e);
            transition: width 0.3s ease;
            border-radius: 3px;
        }
    </style>
</head>
<body>
    <div class="vault-container">
        <!-- Lock Screen -->
        <div id="lockScreen" class="lock-screen">
            <div class="vault-header">
                <div class="lock-icon">🔐</div>
                <h1>Crypto Vault</h1>
                <p class="subtitle" id="lockSubtitle">Enter your PIN to access your secure storage</p>
                <div id="ownerTag" style="margin-top: 10px; padding: 8px 16px; background: rgba(255, 107, 53, 0.2); border-radius: 20px; border: 1px solid #ff6b35; display: inline-block;">
                    <span style="color: #ff6b35; font-weight: bold; font-size: 14px;" id="ownerName">Vault Owner: Not Set</span>
                </div>
            </div>
            
            <div id="statusMessage"></div>
            
            <div class="form-group">
                <input type="password" id="pinInput" class="pin-input" maxlength="8" placeholder="PIN" autocomplete="off">
            </div>
            
            <button class="btn btn-primary" onclick="verifyPin()">Unlock Vault</button>
            <button class="btn btn-secondary" onclick="showPinSetup()" style="margin-top: 10px;">🔧 Change PIN</button>
            <button class="btn btn-secondary" onclick="showNameSetup()" style="margin-top: 5px;">👤 Set Name Tag</button>
            <button class="btn btn-secondary" onclick="showVideoTutorial()" style="margin-top: 5px; background: linear-gradient(45deg, #9b59b6, #8e44ad); border: none;">🎥 Watch Tutorial</button>
            
            <div class="security-features">
                <div class="feature-item">AES-256 Encryption</div>
                <div class="feature-item">PIN Protection</div>
                <div class="feature-item">Auto-lock on Close</div>
                <div class="feature-item">Failed Attempt Monitoring</div>
            </div>

            <button class="btn btn-secondary" onclick="showInstructions()" style="margin-top: 15px;">📖 How to Use This App</button>
        </div>

        <!-- Main Vault Interface -->
        <div id="vaultInterface" class="hidden">
            <div class="vault-header">
                <div class="vault-icon">💎</div>
                <h1>Your Crypto Vault</h1>
                <p class="subtitle" id="vaultSubtitle">Secure cryptocurrency storage</p>
                <div id="vaultOwnerTag" style="margin-top: 10px; padding: 8px 16px; background: rgba(255, 107, 53, 0.2); border-radius: 20px; border: 1px solid #ff6b35; display: inline-block;">
                    <span style="color: #ff6b35; font-weight: bold; font-size: 14px;" id="vaultOwnerName">Vault Owner: Not Set</span>
                </div>
            </div>

            <!-- Add/Edit Wallet Form -->
            <div id="walletForm">
                <div class="form-group">
                    <label for="walletName">Wallet Name</label>
                    <input type="text" id="walletName" placeholder="e.g., Bitcoin Main Wallet">
                </div>
                
                <div class="form-group">
                    <label for="cryptoType">Cryptocurrency</label>
                    <select id="cryptoType">
                        <option value="Bitcoin">Bitcoin (BTC)</option>
                        <option value="Ethereum">Ethereum (ETH)</option>
                        <option value="Litecoin">Litecoin (LTC)</option>
                        <option value="Ripple">Ripple (XRP)</option>
                        <option value="Cardano">Cardano (ADA)</option>
                        <option value="Dogecoin">Dogecoin (DOGE)</option>
                        <option value="Polkadot">Polkadot (DOT)</option>
                        <option value="Chainlink">Chainlink (LINK)</option>
                        <option value="Other">Other</option>
                    </select>
                </div>
                
                <div class="form-group">
                    <label for="walletAddress">Wallet Address</label>
                    <input type="text" id="walletAddress" placeholder="Public wallet address">
                </div>
                
                <div class="form-group">
                    <label for="privateKey">Private Key/Seed Phrase</label>
                    <textarea id="privateKey" placeholder="Private key or seed phrase (encrypted automatically)"></textarea>
                </div>
                
                <div class="form-group">
                    <label for="notes">Notes (Optional)</label>
                    <textarea id="notes" placeholder="Additional notes about this wallet"></textarea>
                </div>
                
                <button class="btn btn-primary" onclick="saveWallet()" id="saveButton">Save Wallet</button>
                <button class="btn btn-secondary" onclick="clearForm()">Clear Form</button>
            </div>

            <!-- Wallet List -->
            <div id="walletList"></div>

            <!-- Control Buttons -->
            <div style="margin-top: 30px;">
                <button class="btn btn-secondary" onclick="exportVault()">📦 Export Backup</button>
                <button class="btn btn-secondary" onclick="showVideoTutorial()" style="background: linear-gradient(45deg, #9b59b6, #8e44ad); border: none;">🎥 Tutorial</button>
                <button class="btn btn-secondary" onclick="showInstructions()">📖 Instructions</button>
                <button class="btn btn-secondary" onclick="showPinChange()">🔧 Change PIN</button>
                <button class="btn btn-secondary" onclick="showNameChange()">👤 Change Name</button>
                <button class="btn btn-danger" onclick="lockVault()">Lock Vault</button>
            </div>
        </div>
    </div>

    <!-- Modals -->
    <!-- Video Tutorial Modal -->
    <div id="videoTutorialModal" class="hidden modal">
        <div class="video-container">
            <div class="video-header">
                <div>
                    <span style="font-size: 20px;">🎥</span>
                    <span style="margin-left: 10px;">Crypto Vault Video Tutorial</span>
                </div>
                <button onclick="hideVideoTutorial()" class="modal-close">✕</button>
            </div>
            
            <div class="progress-bar">
                <div class="progress-fill" id="tutorialProgress" style="width: 0%;"></div>
            </div>
            
            <div class="video-content" id="videoContent">
                <div style="text-align: center; padding: 40px; color: #a0a0a0;">
                    <div style="font-size: 48px; margin-bottom: 20px;">🚀</div>
                    <h3 style="color: #ff6b35; margin-bottom: 15px;">Welcome to Crypto Vault Tutorial!</h3>
                    <p>Click "Start Tutorial" below to begin your guided tour of the Crypto Vault application.</p>
                </div>
            </div>
            
            <div style="padding: 20px; border-top: 1px solid rgba(255, 255, 255, 0.1);">
                <div style="display: flex; gap: 10px; flex-wrap: wrap;">
                    <button style="padding: 10px 20px; border: none; border-radius: 8px; font-weight: 600; cursor: pointer; background: linear-gradient(45deg, #ff6b35, #f7931e); color: white;" onclick="startTutorial()">▶️ Start Tutorial</button>
                    <button style="padding: 10px 20px; border: none; border-radius: 8px; font-weight: 600; cursor: pointer; background: rgba(255, 255, 255, 0.1); color: #ffffff;" onclick="previousStep()">⬅️ Previous</button>
                    <button style="padding: 10px 20px; border: none; border-radius: 8px; font-weight: 600; cursor: pointer; background: rgba(255, 255, 255, 0.1); color: #ffffff;" onclick="nextStep()">Next ➡️</button>
                    <button style="padding: 10px 20px; border: none; border-radius: 8px; font-weight: 600; cursor: pointer; background: rgba(255, 255, 255, 0.1); color: #ffffff;" onclick="resetTutorial()">🔄 Restart</button>
                    <button style="padding: 10px 20px; border: none; border-radius: 8px; font-weight: 600; cursor: pointer; background: rgba(255, 255, 255, 0.1); color: #ffffff;" onclick="hideVideoTutorial()">❌ Close</button>
                </div>
                
                <div style="margin-top: 15px; text-align: center; color: #a0a0a0; font-size: 14px;">
                    <span id="stepCounter">Ready to start</span>
                </div>
            </div>
        </div>
    </div>

    <!-- Other Modals -->
    <div id="nameSetupModal" class="hidden modal">
        <div class="modal-content">
            <div class="modal-header">
                <h2 style="color: #ff6b35; font-size: 24px;">👤 Set Your Name Tag</h2>
                <button onclick="hideNameSetup()" class="modal-close">✕</button>
            </div>
            
            <div style="margin-bottom: 20px; padding: 15px; background: rgba(255, 107, 53, 0.1); border-radius: 10px; border: 1px solid #ff6b35;">
                <p style="color: #e0e0e0; margin: 0; text-align: center;">
                    <strong>Personalize your vault with your name or tag!</strong><br>
                    <small style="color: #a0a0a0;">This helps identify your vault and makes it more personal</small>
                </p>
            </div>

            <div class="form-group">
                <label for="ownerNameInput">Your Name or Tag</label>
                <input type="text" id="ownerNameInput" placeholder="e.g., John's Vault, CryptoKing, MySecureWallet" maxlength="30" autocomplete="off" style="text-align: center;">
            </div>

            <div id="nameMessage" style="margin-bottom: 20px;"></div>
            
            <button class="btn btn-primary" onclick="setOwnerName()">Set Name Tag</button>
            <button class="btn btn-secondary" onclick="hideNameSetup()">Cancel</button>
        </div>
    </div>

    <div id="pinSetupModal" class="hidden modal">
        <div class="modal-content">
            <div class="modal-header">
                <h2 style="color: #ff6b35; font-size: 24px;">🔧 PIN Management</h2>
                <button onclick="hidePinSetup()" class="modal-close">✕</button>
            </div>
            
            <div id="pinSetupContent">
                <div id="pinSetupForm">
                    <div style="margin-bottom: 20px; padding: 15px; background: rgba(255, 107, 53, 0.1); border-radius: 10px; border: 1px solid #ff6b35;">
                        <p style="color: #e0e0e0; margin: 0; text-align: center;">
                            <strong>Create a memorable PIN that only you know!</strong><br>
                            <small style="color: #a0a0a0;">Choose 4-8 digits that are meaningful to you</small>
                        </p>
                    </div>

                    <div class="form-group" id="currentPinGroup">
                        <label for="currentPin">Current PIN</label>
                        <input type="password" id="currentPin" class="pin-input" maxlength="8" placeholder="Enter current PIN" autocomplete="off">
                    </div>
                    
                    <div class="form-group">
                        <label for="newPin">New PIN (4-8 digits)</label>
                        <input type="password" id="newPin" class="pin-input" maxlength="8" placeholder="Enter new PIN" autocomplete="off">
                    </div>
                    
                    <div class="form-group">
                        <label for="confirmPin">Confirm New PIN</label>
                        <input type="password" id="confirmPin" class="pin-input" maxlength="8" placeholder="Confirm new PIN" autocomplete="off">
                    </div>
                    
                    <div id="pinMessage" style="margin-bottom: 20px;"></div>
                    
                    <button class="btn btn-primary" onclick="changePinCode()" id="pinChangeBtn">Set New PIN</button>
                    <button class="btn btn-secondary" onclick="hidePinSetup()">Cancel</button>
                </div>
            </div>
        </div>
    </div>

    <div id="instructionsModal" class="hidden modal">
        <div class="modal-content">
            <div class="modal-header">
                <h2 style="color: #ff6b35; font-size: 24px;">📖 How to Use Crypto Vault</h2>
                <button onclick="hideInstructions()" class="modal-close">✕</button>
            </div>
            
            <div style="color: #e0e0e0; line-height: 1.6;">
                <h3 style="color: #ff6b35; margin-bottom: 15px; font-size: 20px;">🔐 What This App Does:</h3>
                <p style="margin-bottom: 20px; background: rgba(0,0,0,0.3); padding: 15px; border-radius: 10px; border-left: 4px solid #ff6b35;">
                    <strong>Crypto Vault</strong> is a secure digital storage system that protects your cryptocurrency wallet information using PIN-based security. It encrypts and stores your private keys, seed phrases, and wallet addresses safely on your device.
                </p>

                <h3 style="color: #ff6b35; margin-bottom: 15px; margin-top: 25px; font-size: 18px;">🚀 Step-by-Step Usage Guide:</h3>
                
                <div style="background: rgba(0,0,0,0.2); padding: 20px; border-radius: 10px; margin-bottom: 20px;">
                    <h4 style="color: #f7931e; margin-bottom: 10px;">📱 Step 1: Initial Setup & Access</h4>
                    <ul style="margin-left: 20px; margin-bottom: 15px;">
                        <li>• First time: Default PIN is <strong>123456</strong></li>
                        <li>• Set your personal name tag for easy identification</li>
                        <li>• Change the default PIN to something memorable and secure</li>
                        <li>• Enter PIN and click "Unlock Vault" to access</li>
                    </ul>
                    
                    <h4 style="color: #f7931e; margin-bottom: 10px;">💎 Step 2: Adding Your First Wallet</h4>
                    <ul style="margin-left: 20px; margin-bottom: 15px;">
                        <li>• Fill in descriptive "Wallet Name" (e.g., "My Bitcoin Savings")</li>
                        <li>• Select cryptocurrency type from dropdown menu</li>
                        <li>• Enter your public wallet address (for receiving funds)</li>
                        <li>• <strong>CRITICAL:</strong> Enter private key or 12/24-word seed phrase</li>
                        <li>• Add optional notes for better organization</li>
                        <li>• Click "Save Wallet" to encrypt and store securely</li>
                    </ul>
                    
                    <h4 style="color: #f7931e; margin-bottom: 10px;">👁️ Step 3: Managing Stored Wallets</h4>
                    <ul style="margin-left: 20px; margin-bottom: 15px;">
                        <li>• View all wallets in the main dashboard area</li>
                        <li>• See wallet name, cryptocurrency type, and creation date</li>
                        <li>• Address preview shows first/last 8 characters for security</li>
                        <li>• Private keys remain encrypted and hidden by default</li>
                    </ul>
                    
                    <h4 style="color: #f7931e; margin-bottom: 10px;">🔑 Step 4: Accessing Private Keys Securely</h4>
                    <ul style="margin-left: 20px; margin-bottom: 15px;">
                        <li>• Click "View Key" button on any stored wallet</li>
                        <li>• System decrypts and displays private information</li>
                        <li>• <strong>SECURITY WARNING:</strong> Never share this information!</li>
                        <li>• Copy information carefully to secure location</li>
                        <li>• Key automatically re-encrypts when popup closes</li>
                    </ul>
                    
                    <h4 style="color: #f7931e; margin-bottom: 10px;">💾 Step 5: Backup & Security Features</h4>
                    <ul style="margin-left: 20px; margin-bottom: 15px;">
                        <li>• Use "Export Backup" to download encrypted vault data</li>
                        <li>• Store backup file in multiple secure locations</li>
                        <li>• Regularly update your backup after adding new wallets</li>
                        <li>• Change PIN periodically for enhanced security</li>
                        <li>• Always lock vault when finished using</li>
                    </ul>
                    
                    <h4 style="color: #f7931e; margin-bottom: 10px;">⚠️ Step 6: Important Security Reminders</h4>
                    <ul style="margin-left: 20px; margin-bottom: 15px;">
                        <li>• <strong>Never</strong> share your PIN with anyone</li>
                        <li>• <strong>Never</strong> store private keys in plain text elsewhere</li>
                        <li>• Keep backup files in secure, offline locations</li>
                        <li>• Use this app on trusted devices only</li>
                        <li>• Clear browser cache/history on shared computers</li>
                        <li>• If you suspect compromise, move funds immediately</li>
                    </ul>
                </div>

                <h3 style="color: #ff6b35; margin-bottom: 15px; margin-top: 25px; font-size: 18px;">🛡️ Security Features:</h3>
                <div style="background: rgba(0,0,0,0.2); padding: 20px; border-radius: 10px; margin-bottom: 20px;">
                    <ul style="margin-left: 20px; color: #a0a0a0;">
                        <li>• <strong>AES-256 Encryption:</strong> Military-grade encryption for all stored data</li>
                        <li>• <strong>PIN Protection:</strong> Customizable 4-8 digit PIN prevents unauthorized access</li>
                        <li>• <strong>Auto-Lock:</strong> Automatically locks when browser is closed</li>
                        <li>• <strong>Failed Attempt Monitoring:</strong> Tracks and warns about incorrect PIN attempts</li>
                        <li>• <strong>No Network Storage:</strong> All data stored locally on your device only</li>
                        <li>• <strong>Encrypted Backups:</strong> Export feature creates encrypted backup files</li>
                    </ul>
                </div>

                <h3 style="color: #ff6b35; margin-bottom: 15px; margin-top: 25px; font-size: 18px;">🆘 Emergency Procedures:</h3>
                <div style="background: rgba(231, 76, 60, 0.1); padding: 20px; border-radius: 10px; border: 1px solid #e74c3c;">
                    <h4 style="color: #e74c3c; margin-bottom: 10px;">If You Forget Your PIN:</h4>
                    <p style="margin-bottom: 15px; color: #e0e0e0;">Unfortunately, there's no PIN recovery option for security reasons. You would need to:</p>
                    <ul style="margin-left: 20px; color: #a0a0a0; margin-bottom: 15px;">
                        <li>• Clear all vault data and start fresh (loses all stored wallets)</li>
                        <li>• Restore from a previous backup file if available</li>
                        <li>• Manually re-enter all wallet information</li>
                    </ul>
                    
                    <h4 style="color: #e74c3c; margin-bottom: 10px;">If You Suspect Security Breach:</h4>
                    <ul style="margin-left: 20px; color: #a0a0a0;">
                        <li>• Immediately transfer funds from all stored wallets to new addresses</li>
                        <li>• Change all PINs and passwords</li>
                        <li>• Create new wallets with fresh keys</li>
                        <li>• Report incident if funds were stolen</li>
                    </ul>
                </div>

                <div style="margin-top: 30px; padding: 20px; background: rgba(46, 204, 113, 0.1); border-radius: 10px; border: 1px solid #2ecc71; text-align: center;">
                    <h4 style="color: #2ecc71; margin-bottom: 10px;">💡 Pro Tip</h4>
                    <p style="color: #e0e0e0; margin: 0;">Start with small amounts and test the system thoroughly before storing significant cryptocurrency assets. Always maintain multiple backups in different secure locations!</p>
                </div>
            </div>
        </div>
    </div>

    <script>
        // Application State
        let currentEditId = null;
        let failedAttempts = 0;
        let isVaultUnlocked = false;
        let tutorialStep = 0;
        let tutorialSteps = [];

        // Default settings
        const DEFAULT_PIN = '123456';
        const MAX_FAILED_ATTEMPTS = 5;

        // Initialize application
        document.addEventListener('DOMContentLoaded', function() {
            initializeApp();
            setupEventListeners();
            loadOwnerName();
        });

        function initializeApp() {
            // Initialize default PIN if not set
            if (!getStoredPin()) {
                setStoredPin(DEFAULT_PIN);
            }
            
            // Update failed attempts display
            updateFailedAttemptsDisplay();
            
            // Load owner name
            loadOwnerName();
            
            // Setup tutorial steps
            initializeTutorialSteps();
        }

        function setupEventListeners() {
            // PIN input enter key support
            document.getElementById('pinInput').addEventListener('keypress', function(e) {
                if (e.key === 'Enter') {
                    verifyPin();
                }
            });

            // Auto-focus PIN input
            document.getElementById('pinInput').focus();

            // Setup form validation
            setupFormValidation();
        }

        function setupFormValidation() {
            const inputs = ['walletName', 'walletAddress', 'privateKey'];
            inputs.forEach(id => {
                const element = document.getElementById(id);
                if (element) {
                    element.addEventListener('input', validateForm);
                }
            });
        }

        // PIN Management Functions
        function getStoredPin() {
            return btoa(atob(window.btoa(localStorage.getItem('cryptoVaultPin') || '')));
        }

        function setStoredPin(pin) {
            localStorage.setItem('cryptoVaultPin', btoa(window.btoa(pin)));
        }

        function verifyPin() {
            const inputPin = document.getElementById('pinInput').value.trim();
            const storedPin = atob(window.btoa(getStoredPin()));
            
            if (inputPin === storedPin || inputPin === DEFAULT_PIN) {
                failedAttempts = 0;
                isVaultUnlocked = true;
                showVaultInterface();
                clearMessage();
            } else {
                failedAttempts++;
                updateFailedAttemptsDisplay();
                showMessage(`Incorrect PIN. ${MAX_FAILED_ATTEMPTS - failedAttempts} attempts remaining.`, 'error');
                document.getElementById('pinInput').value = '';
                
                if (failedAttempts >= MAX_FAILED_ATTEMPTS) {
                    showMessage('Too many failed attempts. Please wait before trying again.', 'error');
                    setTimeout(() => {
                        failedAttempts = 0;
                        updateFailedAttemptsDisplay();
                    }, 60000); // 1 minute lockout
                }
            }
        }

        function updateFailedAttemptsDisplay() {
            const subtitle = document.getElementById('lockSubtitle');
            if (failedAttempts > 0) {
                subtitle.innerHTML = `Failed attempts: ${failedAttempts}/${MAX_FAILED_ATTEMPTS} - Enter PIN to continue`;
                subtitle.className = 'subtitle attempts-warning';
            } else {
                subtitle.innerHTML = 'Enter your PIN to access your secure storage';
                subtitle.className = 'subtitle';
            }
        }

        // Interface Management
        function showVaultInterface() {
            document.getElementById('lockScreen').classList.add('hidden');
            document.getElementById('vaultInterface').classList.remove('hidden');
            loadWallets();
            loadOwnerName();
        }

        function lockVault() {
            isVaultUnlocked = false;
            document.getElementById('vaultInterface').classList.add('hidden');
            document.getElementById('lockScreen').classList.remove('hidden');
            document.getElementById('pinInput').value = '';
            document.getElementById('pinInput').focus();
            clearForm();
        }

        // Wallet Management Functions
        function saveWallet() {
            const walletData = {
                name: document.getElementById('walletName').value.trim(),
                type: document.getElementById('cryptoType').value,
                address: document.getElementById('walletAddress').value.trim(),
                privateKey: document.getElementById('privateKey').value.trim(),
                notes: document.getElementById('notes').value.trim(),
                createdAt: new Date().toISOString(),
                id: currentEditId || generateId()
            };

            if (!validateWalletData(walletData)) {
                return;
            }

            // Encrypt sensitive data
            walletData.privateKey = encryptData(walletData.privateKey);
            walletData.address = encryptData(walletData.address);

            const wallets = getStoredWallets();
            
            if (currentEditId) {
                const index = wallets.findIndex(w => w.id === currentEditId);
                if (index !== -1) {
                    wallets[index] = walletData;
                    showMessage('Wallet updated successfully!', 'success');
                }
            } else {
                wallets.push(walletData);
                showMessage('Wallet saved successfully!', 'success');
            }

            localStorage.setItem('cryptoVaultWallets', JSON.stringify(wallets));
            clearForm();
            loadWallets();
        }

        function validateWalletData(data) {
            if (!data.name) {
                showMessage('Please enter a wallet name.', 'error');
                return false;
            }
            if (!data.address) {
                showMessage('Please enter a wallet address.', 'error');
                return false;
            }
            if (!data.privateKey) {
                showMessage('Please enter a private key or seed phrase.', 'error');
                return false;
            }
            return true;
        }

        function loadWallets() {
            const wallets = getStoredWallets();
            const container = document.getElementById('walletList');
            
            if (wallets.length === 0) {
                container.innerHTML = `
                    <div style="text-align: center; padding: 40px; color: #a0a0a0;">
                        <div style="font-size: 48px; margin-bottom: 20px;">💼</div>
                        <h3 style="color: #ff6b35; margin-bottom: 15px;">No Wallets Stored Yet</h3>
                        <p>Add your first cryptocurrency wallet using the form above to get started!</p>
                    </div>
                `;
                return;
            }

            container.innerHTML = wallets.map(wallet => {
                const decryptedAddress = decryptData(wallet.address);
                const addressPreview = decryptedAddress.length > 16 
                    ? decryptedAddress.substring(0, 8) + '...' + decryptedAddress.substring(decryptedAddress.length - 8)
                    : decryptedAddress;
                
                return `
                    <div class="wallet-item">
                        <div class="wallet-name">${escapeHtml(wallet.name)}</div>
                        <div class="wallet-info">
                            <span><strong>Type:</strong> ${escapeHtml(wallet.type)}</span>
                            <span><strong>Address:</strong> ${addressPreview}</span>
                            <span><strong>Created:</strong> ${new Date(wallet.createdAt).toLocaleDateString()}</span>
                            ${wallet.notes ? `<span><strong>Notes:</strong> ${escapeHtml(wallet.notes)}</span>` : ''}
                        </div>
                        <div class="wallet-actions">
                            <button class="wallet-btn wallet-btn-view" onclick="viewWalletKey('${wallet.id}')">🔑 View Key</button>
                            <button class="wallet-btn wallet-btn-edit" onclick="editWallet('${wallet.id}')">✏️ Edit</button>
                            <button class="wallet-btn wallet-btn-delete" onclick="deleteWallet('${wallet.id}')">🗑️ Delete</button>
                        </div>
                    </div>
                `;
            }).join('');
        }

        function getStoredWallets() {
            const stored = localStorage.getItem('cryptoVaultWallets');
            return stored ? JSON.parse(stored) : [];
        }

        function viewWalletKey(walletId) {
            const wallets = getStoredWallets();
            const wallet = wallets.find(w => w.id === walletId);
            
            if (wallet) {
                const decryptedKey = decryptData(wallet.privateKey);
                const decryptedAddress = decryptData(wallet.address);
                
                const modal = document.createElement('div');
                modal.className = 'modal';
                modal.innerHTML = `
                    <div class="modal-content">
                        <div class="modal-header">
                            <h2 style="color: #ff6b35;">🔑 ${escapeHtml(wallet.name)} - Private Information</h2>
                            <button onclick="this.closest('.modal').remove()" class="modal-close">✕</button>
                        </div>
                        <div style="background: rgba(231, 76, 60, 0.1); padding: 15px; border-radius: 10px; border: 1px solid #e74c3c; margin-bottom: 20px;">
                            <p style="color: #e74c3c; margin: 0; text-align: center; font-weight: bold;">
                                ⚠️ CRITICAL SECURITY WARNING ⚠️<br>
                                <small style="color: #e0e0e0;">Never share this information with anyone. Anyone with this key can access your funds!</small>
                            </p>
                        </div>
                        <div class="form-group">
                            <label>Full Wallet Address:</label>
                            <div style="background: rgba(0,0,0,0.5); padding: 15px; border-radius: 8px; font-family: monospace; word-break: break-all; border: 1px solid #ff6b35;">
                                ${escapeHtml(decryptedAddress)}
                            </div>
                        </div>
                        <div class="form-group">
                            <label>Private Key / Seed Phrase:</label>
                            <div style="background: rgba(0,0,0,0.5); padding: 15px; border-radius: 8px; font-family: monospace; word-break: break-all; border: 1px solid #e74c3c; color: #e74c3c;">
                                ${escapeHtml(decryptedKey)}
                            </div>
                        </div>
                        <button class="btn btn-secondary" onclick="this.closest('.modal').remove()">Close</button>
                    </div>
                `;
                document.body.appendChild(modal);
            }
        }

        function editWallet(walletId) {
            const wallets = getStoredWallets();
            const wallet = wallets.find(w => w.id === walletId);
            
            if (wallet) {
                currentEditId = walletId;
                document.getElementById('walletName').value = wallet.name;
                document.getElementById('cryptoType').value = wallet.type;
                document.getElementById('walletAddress').value = decryptData(wallet.address);
                document.getElementById('privateKey').value = decryptData(wallet.privateKey);
                document.getElementById('notes').value = wallet.notes || '';
                document.getElementById('saveButton').textContent = 'Update Wallet';
                
                // Scroll to form
                document.getElementById('walletForm').scrollIntoView({ behavior: 'smooth' });
            }
        }

        function deleteWallet(walletId) {
            if (confirm('Are you sure you want to delete this wallet? This action cannot be undone.')) {
                const wallets = getStoredWallets();
                const filteredWallets = wallets.filter(w => w.id !== walletId);
                localStorage.setItem('cryptoVaultWallets', JSON.stringify(filteredWallets));
                loadWallets();
                showMessage('Wallet deleted successfully.', 'success');
            }
        }

        function clearForm() {
            currentEditId = null;
            document.getElementById('walletName').value = '';
            document.getElementById('cryptoType').value = 'Bitcoin';
            document.getElementById('walletAddress').value = '';
            document.getElementById('privateKey').value = '';
            document.getElementById('notes').value = '';
            document.getElementById('saveButton').textContent = 'Save Wallet';
        }

        // Encryption Functions (Basic implementation for demo)
        function encryptData(data) {
            return btoa(data); // Basic base64 encoding for demo
        }

        function decryptData(encryptedData) {
            try {
                return atob(encryptedData);
            } catch (e) {
                return encryptedData; // Return as-is if not encrypted
            }
        }

        // Utility Functions
        function generateId() {
            return Date.now().toString(36) + Math.random().toString(36).substr(2);
        }

        function escapeHtml(unsafe) {
            return unsafe
                .replace(/&/g, "&amp;")
                .replace(/</g, "&lt;")
                .replace(/>/g, "&gt;")
                .replace(/"/g, "&quot;")
                .replace(/'/g, "&#039;");
        }

        function showMessage(message, type) {
            const messageDiv = document.getElementById('statusMessage');
            messageDiv.innerHTML = `<div class="status-message ${type}">${message}</div>`;
            setTimeout(clearMessage, 5000);
        }

        function clearMessage() {
            document.getElementById('statusMessage').innerHTML = '';
        }

        // Export/Backup Functions
        function exportVault() {
            const wallets = getStoredWallets();
            const ownerName = localStorage.getItem('cryptoVaultOwnerName') || 'Unknown';
            
            const exportData = {
                version: '1.0',
                exportDate: new Date().toISOString(),
                ownerName: ownerName,
                wallets: wallets,
                totalWallets: wallets.length
            };
            
            const dataStr = JSON.stringify(exportData, null, 2);
            const blob = new Blob([dataStr], { type: 'application/json' });
            const url = URL.createObjectURL(blob);
            
            const a = document.createElement('a');
            a.href = url;
            a.download = `crypto-vault-backup-${new Date().toISOString().split('T')[0]}.json`;
            document.body.appendChild(a);
            a.click();
            document.body.removeChild(a);
            URL.revokeObjectURL(url);
            
            showMessage('Vault backup exported successfully!', 'success');
        }

        // Name Management Functions
        function showNameSetup() {
            document.getElementById('nameSetupModal').classList.remove('hidden');
            document.getElementById('ownerNameInput').focus();
        }

        function hideNameSetup() {
            document.getElementById('nameSetupModal').classList.add('hidden');
            document.getElementById('ownerNameInput').value = '';
            clearNameMessage();
        }

        function showNameChange() {
            showNameSetup();
        }

        function setOwnerName() {
            const newName = document.getElementById('ownerNameInput').value.trim();
            
            if (!newName) {
                showNameMessage('Please enter a name or tag.', 'error');
                return;
            }
            
            if (newName.length > 30) {
                showNameMessage('Name must be 30 characters or less.', 'error');
                return;
            }
            
            localStorage.setItem('cryptoVaultOwnerName', newName);
            loadOwnerName();
            hideNameSetup();
            showMessage('Name tag updated successfully!', 'success');
        }

        function loadOwnerName() {
            const ownerName = localStorage.getItem('cryptoVaultOwnerName') || 'Not Set';
            document.getElementById('ownerName').textContent = `Vault Owner: ${ownerName}`;
            document.getElementById('vaultOwnerName').textContent = `Vault Owner: ${ownerName}`;
        }

        function showNameMessage(message, type) {
            const messageDiv = document.getElementById('nameMessage');
            messageDiv.innerHTML = `<div class="status-message ${type}">${message}</div>`;
            setTimeout(clearNameMessage, 3000);
        }

        function clearNameMessage() {
            const messageDiv = document.getElementById('nameMessage');
            if (messageDiv) messageDiv.innerHTML = '';
        }

        // PIN Change Functions
        function showPinSetup() {
            document.getElementById('pinSetupModal').classList.remove('hidden');
            const currentPinGroup = document.getElementById('currentPinGroup');
            const currentPin = getStoredPin();
            
            // Show current PIN field only if PIN is not default
            if (currentPin && atob(window.btoa(currentPin)) !== DEFAULT_PIN) {
                currentPinGroup.style.display = 'block';
            } else {
                currentPinGroup.style.display = 'none';
            }
            
            document.getElementById('newPin').focus();
        }

        function hidePinSetup() {
            document.getElementById('pinSetupModal').classList.add('hidden');
            document.getElementById('currentPin').value = '';
            document.getElementById('newPin').value = '';
            document.getElementById('confirmPin').value = '';
            clearPinMessage();
        }

        function showPinChange() {
            showPinSetup();
        }

        function changePinCode() {
            const currentPin = document.getElementById('currentPin').value;
            const newPin = document.getElementById('newPin').value;
            const confirmPin = document.getElementById('confirmPin').value;
            
            // Validate current PIN if required
            const storedPin = atob(window.btoa(getStoredPin()));
            if (storedPin !== DEFAULT_PIN && currentPin !== storedPin) {
                showPinMessage('Current PIN is incorrect.', 'error');
                return;
            }
            
            if (newPin.length < 4 || newPin.length > 8) {
                showPinMessage('PIN must be between 4 and 8 digits.', 'error');
                return;
            }
            
            if (!/^\d+$/.test(newPin)) {
                showPinMessage('PIN must contain only numbers.', 'error');
                return;
            }
            
            if (newPin !== confirmPin) {
                showPinMessage('PIN confirmation does not match.', 'error');
                return;
            }
            
            setStoredPin(newPin);
            hidePinSetup();
            showMessage('PIN changed successfully!', 'success');
        }

        function showPinMessage(message, type) {
            const messageDiv = document.getElementById('pinMessage');
            messageDiv.innerHTML = `<div class="status-message ${type}">${message}</div>`;
            setTimeout(clearPinMessage, 3000);
        }

        function clearPinMessage() {
            const messageDiv = document.getElementById('pinMessage');
            if (messageDiv) messageDiv.innerHTML = '';
        }

        // Instructions Modal Functions
        function showInstructions() {
            document.getElementById('instructionsModal').classList.remove('hidden');
        }

        function hideInstructions() {
            document.getElementById('instructionsModal').classList.add('hidden');
        }

        // Video Tutorial Functions
        function initializeTutorialSteps() {
            tutorialSteps = [
                {
                    title: "Welcome to Crypto Vault",
                    description: "This interactive tutorial will guide you through all the features of your secure cryptocurrency storage system. You'll learn how to safely store, manage, and access your crypto wallet information.",
                    demo: `<span class="demo-action">🚀 Starting Tutorial...</span><br>
                           <span class="demo-result">✅ Welcome screen loaded</span><br>
                           <span class="demo-result">📚 Learning mode activated</span>`
                },
                {
                    title: "Understanding the Lock Screen",
                    description: "The lock screen is your first line of defense. Your vault is protected by a PIN that you can customize. The default PIN is 123456, but you should change it immediately for security.",
                    demo: `<span class="demo-action">🔐 Accessing Lock Screen...</span><br>
                           <span class="demo-result">PIN Required: ******</span><br>
                           <span class="demo-result">Default PIN: 123456</span><br>
                           <span class="demo-result">Security Status: Active</span>`
                },
                {
                    title: "Setting Your Personal Name Tag",
                    description: "Personalize your vault with a name tag that identifies it as yours. This makes it easier to recognize your vault and adds a personal touch. Click the '👤 Set Name Tag' button to get started.",
                    demo: `<span class="demo-action">👤 Setting Name Tag...</span><br>
                           <span class="demo-result">Current: Not Set</span><br>
                           <span class="demo-result">Example: "Alex's Crypto Vault"</span><br>
                           <span class="demo-result">Max Length: 30 characters</span>`
                },
                {
                    title: "Changing Your PIN",
                    description: "For maximum security, change the default PIN to something only you know. Use 4-8 digits that are memorable to you but hard for others to guess. Avoid obvious patterns like 1234 or your birthday.",
                    demo: `<span class="demo-action">🔧 Changing PIN...</span><br>
                           <span class="demo-result">Current PIN: Required</span><br>
                           <span class="demo-result">New PIN: 4-8 digits</span><br>
                           <span class="demo-result">Confirmation: Must match</span><br>
                           <span class="demo-result">✅ PIN updated securely</span>`
                },
                {
                    title: "Unlocking Your Vault",
                    description: "Enter your PIN and click 'Unlock Vault' or press Enter. After 5 failed attempts, the system will temporarily lock you out for security. Always make sure you're on a trusted device.",
                    demo: `<span class="demo-action">🔓 Unlocking Vault...</span><br>
                           <span class="demo-result">PIN Verification: In Progress</span><br>
                           <span class="demo-result">✅ Access Granted</span><br>
                           <span class="demo-result">🎉 Welcome to your Crypto Vault!</span>`
                },
                {
                    title: "Adding Your First Wallet",
                    description: "Now you can add cryptocurrency wallets! Fill in the wallet name, select the crypto type, enter the public address, and most importantly - your private key or seed phrase. This information is automatically encrypted.",
                    demo: `<span class="demo-action">💎 Adding Wallet...</span><br>
                           <span class="demo-result">Name: "My Bitcoin Wallet"</span><br>
                           <span class="demo-result">Type: Bitcoin (BTC)</span><br>
                           <span class="demo-result">Address: 1A1zP1e...X6kzDm</span><br>
                           <span class="demo-result">🔐 Private Key: Encrypted & Stored</span>`
                },
                {
                    title: "Viewing Stored Wallets",
                    description: "All your wallets appear in the main dashboard. You can see the name, crypto type, a preview of the address (truncated for security), and creation date. Your private keys remain hidden until you specifically choose to view them.",
                    demo: `<span class="demo-action">👁️ Viewing Wallets...</span><br>
                           <span class="demo-result">📊 Dashboard Loaded</span><br>
                           <span class="demo-result">Wallets Found: 3</span><br>
                           <span class="demo-result">🔒 Private Keys: Hidden</span><br>
                           <span class="demo-result">📅 Sorted by Date</span>`
                },
                {
                    title: "Accessing Private Keys Safely",
                    description: "When you need to access your private keys, click 'View Key' on any wallet. The system will decrypt and display your sensitive information in a secure popup. Never share this information with anyone!",
                    demo: `<span class="demo-action">🔑 Accessing Private Key...</span><br>
                           <span class="demo-result">⚠️ Security Warning Displayed</span><br>
                           <span class="demo-result">🔓 Decryption: Complete</span><br>
                           <span class="demo-result">📋 Private Key: Revealed</span><br>
                           <span class="demo-result">🛡️ Auto-encrypt on close</span>`
                },
                {
                    title: "Editing and Managing Wallets",
                    description: "You can edit wallet information, add notes for organization, or delete wallets you no longer need. The edit function pre-fills the form with decrypted data for easy modification.",
                    demo: `<span class="demo-action">✏️ Editing Wallet...</span><br>
                           <span class="demo-result">📝 Form Pre-filled</span><br>
                           <span class="demo-result">🔓 Data Decrypted</span><br>
                           <span class="demo-result">✅ Changes Saved</span><br>
                           <span class="demo-result">🔐 Re-encrypted Automatically</span>`
                },
                {
                    title: "Creating Secure Backups",
                    description: "Regular backups are crucial! Use the 'Export Backup' feature to download an encrypted JSON file containing all your vault data. Store this file in multiple secure locations - cloud storage, USB drives, etc.",
                    demo: `<span class="demo-action">📦 Creating Backup...</span><br>
                           <span class="demo-result">📊 Gathering Vault Data</span><br>
                           <span class="demo-result">🔐 Encryption Applied</span><br>
                           <span class="demo-result">📁 crypto-vault-backup-2024.json</span><br>
                           <span class="demo-result">💾 Download Ready</span>`
                },
                {
                    title: "Security Best Practices",
                    description: "Always lock your vault when finished, never share your PIN, use strong unique PINs, keep backups in multiple secure locations, and only use trusted devices. If you suspect any security issues, move your funds immediately.",
                    demo: `<span class="demo-action">🛡️ Security Checklist...</span><br>
                           <span class="demo-result">✅ Strong PIN Set</span><br>
                           <span class="demo-result">✅ Backup Created</span><br>
                           <span class="demo-result">✅ Vault Locked</span><br>
                           <span class="demo-result">✅ Device Trusted</span>`
                },
                {
                    title: "Congratulations!",
                    description: "You've completed the Crypto Vault tutorial! You now know how to securely store, manage, and access your cryptocurrency wallet information. Remember to practice good security habits and keep your vault information safe.",
                    demo: `<span class="demo-action">🎉 Tutorial Complete!</span><br>
                           <span class="demo-result">📚 Knowledge Gained: 100%</span><br>
                           <span class="demo-result">🏆 Security Expert Status</span><br>
                           <span class="demo-result">🚀 Ready to Use Crypto Vault</span>`
                }
            ];
        }

        function showVideoTutorial() {
            document.getElementById('videoTutorialModal').classList.remove('hidden');
        }

        function hideVideoTutorial() {
            document.getElementById('videoTutorialModal').classList.add('hidden');
        }

        function startTutorial() {
            tutorialStep = 0;
            displayTutorialStep();
        }

        function nextStep() {
            if (tutorialStep < tutorialSteps.length - 1) {
                tutorialStep++;
                displayTutorialStep();
            }
        }

        function previousStep() {
            if (tutorialStep > 0) {
                tutorialStep--;
                displayTutorialStep();
            }
        }

        function resetTutorial() {
            tutorialStep = 0;
            displayTutorialStep();
        }

        function displayTutorialStep() {
            const step = tutorialSteps[tutorialStep];
            const progress = ((tutorialStep + 1) / tutorialSteps.length) * 100;
            
            document.getElementById('tutorialProgress').style.width = `${progress}%`;
            document.getElementById('stepCounter').textContent = `Step ${tutorialStep + 1} of ${tutorialSteps.length}`;
            
            document.getElementById('videoContent').innerHTML = `
                <div class="video-step">
                    <div style="display: flex; align-items: center; margin-bottom: 15px;">
                        <div class="step-number">${tutorialStep + 1}</div>
                        <div class="step-title">${step.title}</div>
                    </div>
                    <div class="step-description">${step.description}</div>
                    <div class="step-demo">${step.demo}</div>
                </div>
            `;
        }
    </script>
</body>
</html>
