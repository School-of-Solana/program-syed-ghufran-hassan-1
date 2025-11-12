# Solana Notes Dapp

A decentralized notes application built on the Solana blockchain using the Anchor framework. Users can publish and store notes securely on-chain with a 280-character limit.

## Features

- **On-Chain Storage**: Notes are stored directly on the Solana blockchain
- **Character Limit**: 280 characters per note (similar to Twitter)
- **PDA-based Accounts**: Uses Program Derived Addresses for secure note storage
- **Author Verification**: Each note is cryptographically linked to its author

## Smart Contract Details

### Program ID

FrKpuTVXmWTmgrBEBv2xFUXQwNuPcpHjKF5fC3mPQH8L


### Instructions

#### `publish_note`
Publishes a new note to the blockchain.

**Parameters:**
- `note_id: u64` - Unique identifier for the note
- `content: String` - Note content (max 280 characters)

**Accounts:**
- `note` - PDA account to store the note
- `author` - Signer account publishing the note
- `system_program` - Solana System Program

### Account Structure

#### `Note` Account
```rust
pub struct Note {
    pub author: Pubkey,    // 32 bytes
    pub note_id: u64,      // 8 bytes
    pub content: String,   // 4 + 280 bytes (max)
}
```
Total Size: 324 bytes (including 8-byte discriminator)

The program is deployed on 

https://explorer.solana.com/address/BU6kzpyjQ8EjALky6Y95QKTfiYSttGoqwLoXxnzetQVJ?cluster=devnet


