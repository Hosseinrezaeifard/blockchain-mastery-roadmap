---

1. **💡 EIPs**
    
    **EIPs (Ethereum Improvement Proposals)** are design documents used to propose new features, standards, or improvements to the Ethereum blockchain. They are the formal mechanism through which Ethereum evolves and are vital to the platform’s decentralized governance and technical innovation.
    
    ---
    
2. **💡 ERCs**
    
    **ERCs (Ethereum Request for Comments)** are a **subset of EIPs** that define **application-level standards** on the Ethereum blockchain—especially for **smart contracts and tokens**.
    
    > Simply put: ERCs are blueprints for how certain things (like tokens) should behave in Ethereum so that developers can build interoperable apps.
    > 
    
    ---
    
3. 💡**ERC-20**
    
    **ERC-20** is a **token standard** on Ethereum that defines how **fungible tokens** should behave.
    
    It allows developers to create tokens that are **interchangeable** and work seamlessly with wallets, exchanges, and dApps.
    
    > Think of it like a template or interface for making your own crypto coin on Ethereum (like USDT, LINK, UNI, etc.).
    > 
    
    ---
    
4. **💡 URI vs URL**
    
    A URL provides the location of the resource. A URI identifies the resource by name at the specified location or URL.
    
    ---
    
5. **💡 IPFS — How It Works Under the Hood (Decentralization + Pinning)**
    
    ### ⚙️ 1. **Content-Based Addressing (CID)**
    
    - When you add a file to IPFS:
        - The file is **split into chunks** (typically 256 KB each).
        - Each chunk is **hashed using SHA-256**.
        - A **Merkle DAG** (a tree of hashes) is created where:
            - Leaf nodes = chunks.
            - Parent nodes = hash of children.
        - The top node (root hash) becomes the **CID (Content Identifier)** for the file.
    
    **📌 Why this matters?**
    
    > The hash ensures data integrity and content immutability. Any change to the file results in a completely new CID.
    > 
    
    ### 🌍 2. **Peer-to-Peer (P2P) Network**
    
    - IPFS nodes connect to each other via a **Distributed Hash Table (DHT)**.
    - Think of DHT as a **giant decentralized phone book**:
        - Key = CID (hash)
        - Value = IP address of the node(s) who have that data
    
    **💡 Note:**
    
    > Nodes announce they have certain data in the DHT. So when you search for a CID, the network finds which node has it.
    > 
    
    ### 📡 3. **Finding & Retrieving Files**
    
    - When you `ipfs get <CID>`:
        - Your node queries the DHT to find peers storing that CID.
        - It **fetches data directly** from them over a P2P connection (like BitTorrent).
        - The data is **verified** by recomputing its hash.
    
    ### 📌 4. **Pinning (Persistence)**
    
    - **By default**, data on a node is **not permanent**. It can be **garbage-collected**.
    - To ensure the file stays:
        - You **pin it** using:
            
            ```bash
            ipfs pin add <CID>
            ```
            
        - Pinning means: **"Keep this data, don’t delete it."**
    - You can use **your own node** or services like:
        - [Pinata](https://pinata.cloud/)
        - [Filebase](https://filebase.com/)
        - [web3.storage](https://web3.storage/)
    
    ---
    
6. **💡 There is still a better way to save NFTs (on-chain / SVG)**
    
    While IPFS is commonly used to store NFT metadata and media off-chain, it has critical **limitations** that make it a **risky choice as a permanent storage solution**:
    
    - **No Built-in Persistence**: IPFS nodes can garbage-collect unused files. Unless someone pins the data (e.g. via a pinning service like Pinata or Filebase), the content may **disappear** over time, leading to broken NFTs.
    - **No Availability Guarantees**: Unlike traditional cloud storage, IPFS **does not ensure uptime** or reliability unless additional infrastructure is added.
    - **Centralized Workarounds**: To make IPFS reliable, developers often rely on **centralized pinning services**, which defeats the goal of full decentralization and reintroduces a single point of failure.
    - **Slow Access Times**: Accessing files on IPFS can be **inconsistent and slow**, depending on the availability and proximity of the nodes that host the content.
    - **No Built-in Versioning or Immutability Guarantees for Metadata**: Unless versioned manually, NFT metadata can still be **mutable** if not properly structured or stored immutably.
    
    ---
    
7. **💡 What is an Airdrop in Blockchain?**
    
    **Airdrop** refers to the **free distribution of cryptocurrency tokens** to users' wallets, often as a **marketing strategy** or as part of **decentralized governance**.
    
    ### ✨ Key Points:
    
    - **Purpose**: Promote awareness, reward early users, or distribute governance power.
    - **Types**:
        - **Holder Airdrop**: Sent to users holding a specific token.
        - **Task-based Airdrop**: Requires users to complete tasks (e.g., follow, share, use a dApp).
        - **Retroactive Airdrop**: Rewards users based on past activity.
    - **Risks**: Some airdrops may be scams or phishing attempts—**always verify sources**.
    
    ---