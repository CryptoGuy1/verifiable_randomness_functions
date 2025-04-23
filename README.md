# 🏃‍♂️ Runners – Chainlink VRF-Powered Dynamic NFT Game

**Runners** is an interactive NFT game where characters compete in a race. Each character's progress is determined by randomness powered by [Chainlink VRF v2.5](https://docs.chain.link/vrf/v2-5/introduction). Every time you call `run(tokenId)`, Chainlink generates verifiable randomness to update that runner's **distance** and **round**—all stored and reflected on-chain as dynamic NFT metadata.

> Deployed on Avalanche Fuji Testnet, this contract combines **ERC-721 NFTs** with **Chainlink VRF randomness** to create a game-ready, on-chain experience.

---

## 🎮 Gameplay Overview

- Mint a character NFT (Elf, Knight, Orc, or Witch).
- Call `run(tokenId)` to generate a random running distance.
- Chainlink VRF provides randomness to determine how far your runner moves.
- The runner's metadata updates with new **distance** and **round**.
- View updated metadata via `tokenURI`.

---

## 🧠 Tech Stack

| Tool / Framework          | Description                                           |
|---------------------------|-------------------------------------------------------|
| **Solidity 0.8.19**       | Core smart contract logic                             |
| **Chainlink VRF v2.5**    | Verifiable on-chain randomness                        |
| **ERC-721 URIStorage**    | NFTs with dynamic metadata                           |
| **OpenZeppelin Contracts**| NFT and utility libraries (v4.6.0)                    |
| **Base64 Encoding**       | On-chain JSON metadata as base64 URIs                 |

---

## 🧪 How It Works

1. Deploy on **Fuji Testnet**
2. Mint an NFT using `safeMint(address, charId)`
   - `charId` options: `0=Elf`, `1=Knight`, `2=Orc`, `3=Witch`
3. Call `run(tokenId)` to generate a random number
   - Chainlink VRF returns a number between 10–100
4. Runner's distance increases, round is incremented
5. Token URI is dynamically updated with metadata

---

## 🔗 VRF Configuration (Fuji Testnet)

| Parameter               | Value                                                                 |
|-------------------------|------------------------------------------------------------------------|
| **Coordinator Address** | `0x5C210eF41CD1a72de73bF76eC39637bB0d3d7BEE`                            |
| **Key Hash**            | `0xc799bd1e3bd4d1a41cd4968997a4e03dfd2a3c7c04b695881138580163f42887`  |
| **Callback Gas Limit**  | `2,500,000`                                                            |
| **Confirmations**       | `3`                                                                    |
| **Words Returned**      | `1`                                                                    |

Make sure to fund your Chainlink VRF subscription and pass it into the constructor when deploying.

---

## 📦 Contract Summary

### `safeMint(address to, uint256 charId)`
Mints a new character NFT (Elf, Knight, Orc, Witch). Automatically sets metadata using IPFS-hosted image.

### `run(uint256 tokenId)`
Triggers a Chainlink VRF request to update the runner's distance and round.

### `fulfillRandomWords(...)`
Handles the VRF response, updates the runner state, and refreshes the on-chain token URI.

### `tokenURI(tokenId)`
Returns dynamic metadata for the runner NFT, including:
- `name`
- `image`
- `distance`
- `round`

---

## 🖼 Character Metadata

Character images are hosted on **IPFS**:

| Character | IPFS Image |
|----------|-------------|
| Elf      | `Chainlink_Elf.png` |
| Knight   | `Chainlink_Knight.png` |
| Orc      | `Chainlink_Orc.png` |
| Witch    | `Chainlink_Witch.png` |

Metadata is encoded using `Base64` and returned directly in the token URI.

---

## 📚 Learn More

- [Chainlink VRF v2.5 Documentation](https://docs.chain.link/vrf/v2-5/introduction)
- [Chainlink VRF Subscription Manager](https://vrf.chain.link/)
- [OpenZeppelin ERC721URIStorage](https://docs.openzeppelin.com/contracts/4.x/api/token/erc721#ERC721URIStorage)

---

## 🧠 Notes

- Ensure your Chainlink VRF **subscription is funded** with LINK on Fuji.
- `run()` will fail if your subscription is unfunded or incorrectly configured.
- You can extend this game by adding features like betting, PvP races, or staking!

---

## 👨‍💻 Author

Developed as part of a Chainlink learning project combining verifiable randomness, dynamic NFTs, and gameplay logic.

---

## 📜 License

MIT © 2025
```
