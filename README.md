<html>
  <head>
    <meta charset="UTF-8">
    <h2>Pixel Frens NFT Collection</h2>
  </head>
  <body>
    <h1>Welcome to Pixel Frens!</h1>
  </body>
</html>
<img src="pixelfrens_twitter_header.png" alt="PIXELFRENS.github.io" width="2000" height="450">


<html>
   <head>
      <title>Connect to crypto wallet</title>
   <script src="https://cdnjs.cloudflare.com/ajax/libs/web3/1.7.4-rc.1/web3.min.js"></script>
 </head>
<body>
<script>
/* To connect using MetaMask */
async function connect() {
  if (window.ethereum) {
     await window.ethereum.request({ method: "eth_requestAccounts" });
     window.web3 = new Web3(window.ethereum);
     const account = web3.eth.accounts;
     //Get the current MetaMask selected/active wallet
     const walletAddress = account.givenProvider.selectedAddress;
     console.log(`Wallet: ${walletAddress}`);
  
  } else {
   console.log("No wallet");
  }
}
</script>
<input type="button" value="Connect Wallet" onclick="connect();">
</body>
</html>
