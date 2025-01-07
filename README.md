<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>TrumpBack Coin | MAGA Pre-Sale</title>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/ethers/5.7.2/ethers.umd.min.js"></script>
    <script src="https://cdn.jsdelivr.net/npm/@solana/web3.js@1.61.0/lib/index.iife.min.js"></script>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 0;
            padding: 0;
            background: linear-gradient(to bottom, #3C3B6E, #FFFFFF, #B22234);
            color: #000;
            text-align: center;
        }
        header {
            background: #B22234;
            color: #FFF;
            padding: 20px;
        }
        header img {
            height: 100px;
        }
        .content {
            padding: 20px;
        }
        .btn {
            display: inline-block;
            background: #3C3B6E;
            color: white;
            padding: 10px 20px;
            text-decoration: none;
            border-radius: 5px;
            font-size: 16px;
            cursor: pointer;
        }
        .btn:hover {
            background: #2a2a54;
        }
        footer {
            margin-top: 20px;
            padding: 10px;
            background: #B22234;
            color: white;
        }
        .wallet-address {
            font-weight: bold;
            color: #B22234;
            font-size: 18px;
        }
        .fomo {
            background: #FFD700;
            padding: 15px;
            font-size: 20px;
            font-weight: bold;
            margin: 20px auto;
            display: inline-block;
            border-radius: 5px;
        }
    </style>
</head>
<body>
    <header>
        <img src="https://upload.wikimedia.org/wikipedia/commons/a/a4/Flag_of_the_United_States.svg" alt="American Flag">
        <h1>TrumpBack Coin Pre-Sale</h1>
        <p><strong>MAGA: Make Altcoins Great Again!</strong></p>
    </header>

    <div class="content">
        <div class="fomo">$500,000 RAISED OUT OF $4,000,000 GOAL!</div>
        <div class="fomo">LIMITED TIME ONLY - DON’T MISS OUT!</div>
        <h2>Welcome to the Official TrumpBack Pre-Sale</h2>
        <p>The pre-sale is open now and ends on <strong>January 19</strong>. Get your TRUMP coins today!</p>
        <p><strong>Minimum Purchase:</strong> 0.1 SOL</p>
        <p><strong>Maximum Purchase:</strong> 1.5 SOL</p>

        <button id="connect-wallet" class="btn">Connect Wallet</button>
        <div id="wallet-section" style="display: none;">
            <p>Connected Wallet: <span id="wallet-address">Not Connected</span></p>
            <button id="buy-coins" class="btn">Buy TRUMP Coins</button>
        </div>
        <div id="claim-section" style="display: none; margin-top: 20px;">
            <button id="claim-coins" class="btn">Claim TRUMP Coins</button>
        </div>
    </div>

    <footer>
        <p>&copy; 2025 TrumpBack. All Rights Reserved. | MAGA Forever!</p>
    </footer>

    <script>
        const walletButton = document.getElementById("connect-wallet");
        const walletSection = document.getElementById("wallet-section");
        const walletAddressSpan = document.getElementById("wallet-address");
        const buyCoinsButton = document.getElementById("buy-coins");
        const claimSection = document.getElementById("claim-section");
        const claimCoinsButton = document.getElementById("claim-coins");

        let walletPublicKey = null;

        async function connectWallet() {
            if (window.solana && window.solana.isPhantom) {
                try {
                    const response = await window.solana.connect();
                    walletPublicKey = response.publicKey.toString();
                    walletAddressSpan.textContent = walletPublicKey;
                    walletButton.style.display = "none";
                    walletSection.style.display = "block";
                } catch (err) {
                    console.error("Wallet connection failed", err);
                }
            } else {
                alert("Phantom Wallet is not installed. Please install it to continue.");
            }
        }

        async function buyCoins() {
            if (!walletPublicKey) {
                alert("Connect your wallet first!");
                return;
            }

            const transaction = new solanaWeb3.Transaction();
            const recipient = "LZQmAoxs3suJrFRLfDtGbq7efdJx86moNofGxK6gWvh";
            const amount = 0.1 * solanaWeb3.LAMPORTS_PER_SOL; // Replace with user input

            transaction.add(
                solanaWeb3.SystemProgram.transfer({
                    fromPubkey: new solanaWeb3.PublicKey(walletPublicKey),
                    toPubkey: new solanaWeb3.PublicKey(recipient),
                    lamports: amount,
                })
            );

            try {
                const { signature } = await window.solana.signAndSendTransaction(transaction);
                alert(`Transaction sent! Signature: ${signature}`);
            } catch (err) {
                console.error("Transaction failed", err);
            }
        }

        function enableClaim() {
            const currentDate = new Date();
            const claimDate = new Date("2025-01-20");
            if (currentDate >= claimDate) {
                claimSection.style.display = "block";
            }
        }

        walletButton.addEventListener("click", connectWallet);
        buyCoinsButton.addEventListener("click", buyCoins);
        claimCoinsButton.addEventListener("click", () => {
            alert("Claim functionality will be implemented soon.");
        });

        enableClaim();
    </script>
</body>
</html>
