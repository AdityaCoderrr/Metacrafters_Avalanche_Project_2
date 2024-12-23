# Building a Blockchain with HyperSDK

## Project Introduction
This project focuses on building a custom blockchain using HyperSDK to enable users to mint and transfer tokens. HyperSDK provides a robust framework for developing tailored blockchains, allowing you to define specific rules and functionalities. The project includes token minting, transfer capabilities, and managing order books for on-chain trading.

---

## What is TokenEVM?
TokenEVM, developed by the Metacrafters team, is an example application that demonstrates the use of HyperSDK for token minting and trading. It offers the following features:

- **Token Creation**: Create and manage custom assets.
- **Metadata Management**: Modify asset metadata to include or update relevant information.
- **On-Chain Exchange**: Facilitate the creation and fulfillment of trading orders.
- **CLI Tool and RPC Support**: Includes a command-line interface and in-memory order book to simplify interaction with the blockchain.

With TokenEVM, users can:
- Mint, transfer, and burn tokens.
- Update asset metadata.
- Trade assets via an on-chain exchange.

---

## Features of TokenEVM

### Arbitrary Token Minting
TokenEVM enables seamless creation, minting, and transferring of user-generated tokens. Key features include:
- **Admin Control**: Asset creators have full control over asset minting, metadata updates, and ownership transfers.
- **Optimized Storage**: Efficient storage format allowing parallel execution of transfers not involving the same accounts.

### On-Chain Trading
TokenEVM supports trading any two tokens via:
- **Order Creation**: Specify rates and tokens for trade offers.
- **Order Fulfillment**: Fill offers with matching criteria.
- **Optimized Storage for Orders**: Efficiently manage and parallelize order execution within trading pairs.

### In-Memory Order Book
TokenEVM maintains an in-memory order book that:
- Synchronizes with on-chain transactions.
- Arranges orders using a max-heap based on the best rates for assets.
- Supports RPC for client interactions.

---

## Steps to Reproduce
Follow these steps to set up and run the project:

### Initial Setup
1. **Clone the Repository**:
   ```bash
   git clone <repository_url>
   ```
2. **Install Dependencies**:
   ```bash
   go mod tidy
   ```
3. **Configure Constants**:
   - Edit `consts/consts.go` to define missing constants.
4. **Register Actions**:
   - Add `Create_Asset` and `Mint_Asset` actions in `registry/registry.go`.
5. **Run the VM Locally**:
   ```bash
   export PATH=$PATH:$(go env GOPATH)/bin
   MODE="run-single" ./scripts/run.sh
   ```
   If permissions are denied, use:
   ```bash
   bash ./scripts/run.sh
   ```
6. **Build the Project**:
   ```bash
   ./scripts/build.sh
   ```

### Load the Demo Private Key
1. Import the demo private key:
   ```bash
   ./build/token-cli key import demo.pk
   ```
2. Import the chain:
   ```bash
   ./build/token-cli chain import-anr
   ```

---

## Creating and Minting Assets

### Step 1: Create an Asset
Run the following command to create an asset:
```bash
./build/token-cli action create-asset
```
Output example:
```
database: .token-cli
address: token1...jzf3yp
chainID: Em2p...jy7BcWtaH9
metadata: MarioCoin
continue (y/n): y
✅ txID: 27grFs...
```
The `txID` serves as the `assetID` of your new asset.

### Step 2: Mint an Asset
Mint tokens for the created asset:
```bash
./build/token-cli action mint-asset
```
Output example:
```
assetID: 27grFs...
metadata: MarioCoin
amount: 10000
✅ txID: X1E5C...
```

### Step 3: View Your Balance
Check your balance:
```bash
./build/token-cli key balance
```
Output example:
```
assetID: 27grFs...
metadata: MarioCoin
balance: 10000
```

---

## Transferring Assets
Transfer assets between Subnets using:
```bash
./build/token-cli action export
```
Output example:
```
address: token1...jzf3yp
chainID: Em2p...jy7BcWtaH9
✅ txID: 24Y2z...
```
The `export` command automatically runs the `import` command on the destination. If needed, perform the import manually using:
```bash
./build/token-cli action import
```

---

## Conclusion
TokenEVM showcases the power and flexibility of HyperSDK, making it easy to create, manage, and trade custom assets. With its user-friendly CLI and efficient storage mechanisms, TokenEVM serves as an excellent starting point for building custom blockchain applications.
