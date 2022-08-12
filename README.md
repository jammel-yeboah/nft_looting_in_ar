## 🎮 CREATING & MINTING NFTs - FROM LOOTBOXES IN AR! 🎮
This is a game demo currently built for Android. Using the Mumbai Testnet on the Polygon Network,
you can connect your decentralized crypto wallet to store minted NFTs you place in loot boxes in
the real world!
---
<br>


### Project Demo:
[![Project Demo](https://img.youtube.com/vi/I-IKt0VTCSI/0.jpg)](https://www.youtube.com/watch?v=I-IKt0VTCSI&target=_blank)
<br>
<br>
<br>

## **To Play the Demo:**
1. Download the [APK file](https://drive.google.com/file/d/1gHg93K5TzJXntXJ_jueZEU0DNkKE93BX/view?usp=sharing) on your Android device
2. Download [Metamask](https://metamask.io/) on your Android device and create an account
3. [Connect your Metamask wallet to the Mumbai Testnet](https://blog.polysynth.com/how-to-connect-polygon-testnet-to-metamask-wallet-472bca410d64)
3. Click on the game APK file on your Android device to install and run

<br>

## **To Use this Repo:**

### *Section 1 - Get started*
1. Download this repo (as zip or git)
2. Download [Unity](https://unity3d.com/unity/qa/lts-releases?version=2021.3)
3. Open this repo in Unity
4. [Have MetaMask installed both on your browser and your mobile device, with the Mumbai Testnet imported and some funds in both using the Polygon Faucet](https://medium.com/stakingbits/how-to-connect-polygon-mumbai-testnet-to-metamask-fc3487a3871f)
<br>
<br>


### *Section 2 - Deploy Smart Contract*
At this point, we will connect our application to the blockchain by deploying our smart contract

!! You need to have NodeJS installed: [https://nodejs.org/en/download/](https://nodejs.org/en/download/)

1. In a new external folder, install HardHat

    npm i -D hardhat
    npx hardhat

2. Install dependencies

    npm i -D @openzeppelin/contracts
    npm i -D @nomiclabs/hardhat-waffle
    npm i -D @nomiclabs/hardhat-etherscan

3. UNDER "contracts/", RENAME "Greeter.sol" TO YOUR DESIRED CONTRACT NAME

4. UNDER "scripts/" RENAME "sample_script.js" to "deploy{YourContractName}.js" (WITHOUT {})

5. ON "deploy{YourContractName}.sol" RENAME ALL THE "Greeter" AND "greeter" FIELDS WITH YOUR CONTRACT NAME. !! PRESERVE ORIGINAL CASE !!

6. MAKE SURE the "deploy()" function has the correct contract constructor parameters

7. UNDER "scripts/" MODIFY "deploy{YourContractName}.js" WITH YOUR NEEDS. FOR EXAMPLE, WE ADD ETHERSCAN VERIFICATION CODE JUST AFTER:
    ```
    await yourContractName.deployTransaction.wait(5);

    // We verify the contract
    await hre.run("verify:verify", {
        address: yourContractName.address,
        constructorArguments: [],
    });
    ```
8. ON "hardhat.config.js" ADD THIS REQUIRE TO THE TOP:

    require("@nomiclabs/hardhat-etherscan");

9. ON "hardhat.config.js" ADD THESE FIELDS BEFORE "module.exports" part:

    ```
    const PRIVATE_KEY = "";
    const MUMBAI_NETWORK_URL = "";
    const POLYGONSCAN_API_KEY = "";
    ```

    - *To get your PRIVATE_KEY:*  
    NOTE: This private key is that of the app deployer, not the user  
    **a.** Create a new [metamask](https://metamask.io/) account  
    **b.** Go to your account details and click on "Export your private key"  
    **c.** Copy it to your clipboard and set it to the appropriate field in hardhat.config  

    - *To get your mumbai network URL:*  
    **a.** Naviagte to [chainstack.com](https://chainstack.com/) and create an account  
    **b.** On your account home page, click on "Add a new Project"  
    **c.** After creating an empty project, click on add network  
    **d.** Select "Polygon" and follow the propts to add the mumbai testnet  
    **e.** After your node has been created, click on it  
    **f.** Scroll to the bottom of the page and copy the HTTPS endpoint under "Access and credentials"  
    **g.** Set your MUMBAI_NETWORK_URL to the HTTPS endpoint  

    - *To get a Polygonscan API key:*  
    **a.** Navigate to [polygonscan.com](https://polygonscan.com/) and create account  
    **b.** Hover over your profile icon in the top right corner and click on "API Keys"  
    **c.** Click on the add icon in the top left corner of the window  
    **d.** Copy your API key and set your POLYGONSCAN_API_KEY in hardhat.config to your API key  

10. MODIFY "module.exports" in "hardat.config.js" WITH YOUR NEEDS, LIKE THIS:
    ```
    module.exports = {
      solidity: "0.8.7",
      networks: {
        mumbai: {
          url: MUMBAI_NETWORK_URL,
          accounts: [PRIVATE_KEY]
        }
      },
      etherscan: {
        apiKey: POLYGONSCAN_API_KEY
      }
    };
    ```
11. COMPILE SMART CONTRACT:

    npx hardhat clean
    npx hardhat compile

13. RUN "scripts/deploy.js" TO DEPLOY SMART CONTRACT

    npx hardhat run scripts/deploy.js --network mumbai

************* CONTRACT DEPLOYED AND VERIFIED *************
<br>
<br>

### *Section 3 - Add your Contract address and Contract ABI to Unity*
14. After deploying to contract, navigate to https://mumbai.polygonscan.com/address/{Your contract address}#code
15. Copy your contract address and set the ContractAddress field in [Assets/_Project/Scripts/StateMachine/GameManager.cs](Assets/_Project/Scripts/StateMachine/GameManager.cs) to it
16. Back on Polygoncan, scroll down and copy your Contract ABI
17. Convert the JSON text to Python readable format by heading over to [jsonformatter.org]("jsonformatter.org") and replacing all ' " ' with ' \" '
18. Copy the output and set the ContractAbi in [Assets/_Project/Scripts/StateMachine/GameManager.cs](Assets/_Project/Scripts/StateMachine/GameManager.cs) to it
<br>
<br>

### *Section 4 - Additional Info*

**Configuration**
* `Platform Target` - Android
* `Unity Version` - [2021.3.4f1 LTS](https://unity3d.com/unity/qa/lts-releases?version=2021.3)
* `Render Pipeline` - [Built-in Render Pipeline](https://docs.unity3d.com/Manual/built-in-render-pipeline.html)

**Scenes**
* `Assets/_Project/Scenes/Main.unity` - Open scene and press 'Play'!

**Dependencies**
* [`Moralis Web3 Unity SDK`](https://github.com/MoralisWeb3/web3-unity-sdk)

----
