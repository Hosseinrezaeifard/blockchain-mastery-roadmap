1. **💡`abi.encodePacked` to `string`**
    
    Here's a technical note on what happens behind the scenes with:
    
    ```solidity
    string(abi.encodePacked("Hello", "World!"))
    ```
    
    ### 🔍 **What it does:**
    
    This line concatenates the two string literals `"Hello"` and `"World!"`, then converts the resulting bytes back into a `string`.
    
    ### 🧠 **Behind the Scenes:**
    
    1. **`abi.encodePacked(...)`**
        - This function takes input arguments and tightly packs them into a single `bytes` array.
        - For string literals `"Hello"` and `"World!"`, it converts them into their UTF-8 byte representations and **concatenates** them without padding.
        - So:
            
            `"Hello"` → `0x48656c6c6f`
            
            `"World!"` → `0x576f726c6421`
            
            Together → `0x48656c6c6f576f726c6421`
            
    2. **`string(...)` Conversion**
        - The resulting `bytes` array is then cast back to a `string` type.
        - This is valid because UTF-8 is compatible with `string` in Solidity, as long as the bytes form a valid UTF-8 string.
    
    ### ✅ **Final Result:**
    
    The output is the string:
    
    ```
    "HelloWorld!"
    ```
    
    ---
    
2. **💡 `abi.encodeWithSelector`**
    
    Used in tests (or in contract calls) to **encode function arguments** using a specific function selector.
    
    ### 🔹 Example:
    
    ```solidity
    abi.encodeWithSelector(MyContract.MyCustomError.selector, arg1, arg2)
    ```
    
    - `MyCustomError.selector` gives the **4-byte selector** of the custom error.
    - Useful when mocking or testing reverts with custom errors.
    
    ---
    
3. **💡 Gas & Costs & EVM Opcodes**
    
    ### ⚡️ What is **Gas**?
    
    - **Gas** is the unit of **work** done on the Ethereum Virtual Machine (EVM).
    - Every operation (e.g. `add`, `store`, `call`, `create`) has a **gas cost**.
    
    Think of **gas** like **CPU cycles or energy units** — not money yet.
    
    ### 💰 Who Pays? And With What?
    
    You pay **gas × gas price** in **ETH**.
    
    ```solidity
    totalFee = gasUsed * gasPrice
    ```
    
    - `gasUsed`: How much work the transaction does
    - `gasPrice`: How much ETH you’re willing to pay per unit of gas (set in **Gwei**)
    
    ### 🧱 ETH Denominations
    
    | Unit | Value in Wei | Use Case |
    | --- | --- | --- |
    | `Wei` | `1` | Base unit (like "cents") |
    | `Gwei` | `1e9 Wei` | Gas price |
    | `Ether` | `1e18 Wei` | Human-scale payments |
    |  |  |  |
    
    ### ⚙️ Summary
    
    - **Gas** measures how much work.
    - **Gas price** is set in **Gwei** (how much you’re willing to pay per unit).
    - **Fee paid in ETH**: `gas * gasPrice`.
    
    In tests/scripts, you can also simulate different gas prices with `vm.txGasPrice()`, `--gas-price`, etc.
    
    ## 🧠 What are EVM Opcodes?
    
    The Ethereum Virtual Machine (EVM) runs **low-level instructions** called **opcodes** (operation codes). Each opcode performs a specific task, such as:
    
    - Arithmetic: `ADD`, `MUL`, `DIV`
    - Memory: `MLOAD`, `MSTORE`
    - Storage: `SLOAD`, `SSTORE`
    - Control flow: `JUMP`, `JUMPI`
    - Calls: `CALL`, `DELEGATECALL`, `STATICCALL`
    
    ---
    
    ## ⛽ Gas Cost of Opcodes
    
    Each opcode consumes **a certain amount of gas**. Gas is the fee paid to execute operations on the Ethereum network. The gas cost depends on the complexity and resource intensity of the opcode.
    
    | Opcode | Description | Gas Cost |
    | --- | --- | --- |
    | `ADD` | Adds two values | 3 gas |
    | `MLOAD` | Loads from memory | 3 gas |
    | `SLOAD` | Reads from storage | 100 gas |
    | `SSTORE` | Writes to storage | 100 gas |
    
    > ⚠️ SSTORE is one of the most expensive opcodes, due to persistent state changes.
    > 
    
    ---
    
    ## 🧪 Why It Matters
    
    - Understanding gas costs helps optimize smart contracts.
    - Reducing expensive opcodes (especially `SSTORE`) improves performance and saves ETH.
    - Good for gas golfing, audits, and understanding compiler output.
    
    ---
    
    ## 🔍 Explore Opcodes with [evm.codes](https://www.evm.codes/)
    
    [evm.codes](https://www.evm.codes/) is an **interactive opcode reference** site. You can:
    
    - See all opcodes and their **gas cost**
    - Read **descriptions and stack behavior**
    - Try **bytecode playground** and debug instructions
    
    📎 [Click here to explore](https://www.evm.codes/)
    
    ## 📌 Summary
    
    - Every EVM opcode has a defined gas cost.
    - Storage operations (`SLOAD`, `SSTORE`) are the most gas-heavy.
    - Use [evm.codes](https://www.evm.codes/) to explore, optimize, and understand EVM internals better.
    
    ---
    
4. **💡 Using Base64-Encoded SVGs in the Browser**
    
    You can embed SVG images directly in HTML or CSS using **Base64 encoding**. This allows the image to be delivered inline without needing an external file.
    
    ### ✅ Steps to Use:
    
    1. **Encode the SVG**:
        - Convert your `.svg` file or SVG XML content to a Base64 string.
        - Example using a terminal:
            
            ```bash
            base64 my-icon.svg
            ```
            
    2. **Use in HTML**:
        
        ```html
        <img src="data:image/svg+xml;base64,PHN2ZyB3aWR0aD0iMTAwIiBoZWlnaHQ9Ij...==" alt="icon" />
        ```
        
    
    ### ⚙️ Technical Notes:
    
    - **MIME Type**: Use `image/svg+xml` as the MIME type.
    - **Data URI Syntax**:
        
        ```
        data:[<mediatype>][;base64],<data>
        ```
        
        In this case:
        
        ```
        data:image/svg+xml;base64,<your_base64_encoded_svg>
        ```