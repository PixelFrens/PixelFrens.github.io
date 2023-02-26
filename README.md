# PixelFrens.github.io
<html>
  <head>
    <meta charset="UTF-8">
    <h2>Pixel Frens</h2>
  </head>
  <body>
    <h1>Welcome to Pixel Frens!</h1>
  </body>
</html>
<img src="pixelfrens_twitter_header.png" alt="PIXELFRENS.github.io" width="1675" height="500">

</body>
</html>

<button type="button" onclick="connectWallet()">Connect Wallet</button>
    <form>
      <label for="tokenId">Token ID:</label>
      <input type="text" id="tokenId" name="tokenId"><br><br>
      <button type="button" onclick="mintNFT()">Mint NFT</button>
    </form>
    <div id="nftList"></div>

    <script src="https://cdn.jsdelivr.net/gh/WalletConnect/walletconnect-monorepo/packages/web3-provider/dist/web3-provider.min.js"></script>
    <script src="https://cdn.jsdelivr.net/npm/@walletconnect/client@1.7.7/dist/walletconnect.min.js"></script>
    <script src="https://cdn.jsdelivr.net/npm/qrcode-modal@1.0.1/dist/qrcode-modal.min.js"></script>
    <script src="https://cdn.jsdelivr.net/npm/web3@1.5.2/dist/web3.min.js"></script>
    <script>
      // Replace with your own contract address and ABI
      const contractAddress = "0x1234567890123456789012345678901234567890";
      const contractABI = [ /* ABI goes here */ ];

      const connector = new WalletConnect({
        bridge: "https://bridge.walletconnect.org",
        qrcodeModal: QRCodeModal,
      });

      // Connect to the Ethereum network using Web3.js
      const web3 = new Web3(Web3.givenProvider || "https://mainnet.infura.io/v3/your-infura-project-id");

      // Load the smart contract using its ABI and address
      const contract = new web3.eth.Contract(contractABI, contractAddress);

      // Connect the wallet
      const connectWallet = async () => {
        try {
          await connector.connect();
          console.log("Connected to wallet!");
        } catch (error) {
          console.error(error);
        }
      };

      // Mint the NFT
      const mintNFT = async () => {
        try {
          // Get the token ID from the input field
          const tokenId = document.getElementById("tokenId").value;
          if (!tokenId) {
            throw new Error("Token ID is required");
          }
          // Check if the wallet is connected
          if (!connector.connected) {
            throw new Error("Wallet is not connected");
          }
          // Get the account address from the connected wallet
          const accounts = await web3.eth.getAccounts();
          const account = accounts[0];
          if (!account) {
            throw new Error("No account found in connected wallet");
          }
          // Call the smart contract function to mint the NFT
          const result = await contract.methods.mintNFT(tokenId).send({ from: account });
          console.log(result);
          // Display the minted NFT in the "nftList" div
          const nftList = document.getElementById("nftList");
          const nft = document.createElement("div");
          nft.innerText = `Minted NFT with token ID ${tokenId}`;
          nftList.appendChild(nft);
        } catch (error) {
          console.error(error);
        }
      };
    </script>
  </body>
</html>