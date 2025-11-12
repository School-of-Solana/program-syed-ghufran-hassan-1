# Project Description

**Deployed Frontend URL:** https://solana-dapp-notes-en3l8rv8n-syedghufranhassans-projects.vercel.app/

**Solana Program ID:** FrKpuTVXmWTmgrBEBv2xFUXQwNuPcpHjKF5fC3mPQH8L


## Project Overview

### Description
A decentralized note-taking application built on Solana that allows users to create and store personal notes directly on the blockchain. The application enables users to publish notes with unique identifiers, ensuring secure and permanent storage of their content. Each note is cryptographically linked to its author, providing verifiable ownership and data integrity.

### Key Features

- Feature 1: Create Personalized Notes - Users can publish notes with custom content and unique note IDs, creating a personal collection of on-chain notes.
- Feature 2: Content Validation - Automatic content length validation ensures notes don't exceed the 280-character limit, maintaining efficient blockchain storage.
 
### How to Use the dApp
 
1. **Main Action 1:** You need to add content
2. **Main Action 2:** You need to publish note
 

## Program Architecture
[TODO: Describe your Solana program's architecture. Explain the main instructions, account structures, and data flow.]

### PDA Usage
In my Solana Notes dApp, I implemented a PDA system to create unique, deterministic addresses for storing user notes on-chain. Each note gets its own PDA account derived from a specific seed pattern.

**PDAs Used:**

Seeds Used: [b"note", author.key().as_ref(), &note_id.to_le_bytes()]
-  `b"note"`- Constant prefix that namespaces all note accounts.
- Purpose: Distinguishes note accounts from other potential account types in the program
- Why: Provides a clear identifier that these accounts belong to the notes functionality
-  `author.key().as_ref()` - The author's public key as bytes
- Purpose: Ensures each user has their own isolated note namespace
- Why: Prevents conflicts between different users' notes and ensures only the author can manage their notes
- `&note_id.to_le_bytes()` - The note ID converted to little-endian bytes
- Purpose: Allows users to create multiple notes with different IDs
- Why: Enables note organization and retrieval by specific IDs within a user's collection



### Program Instructions
[TODO: List and describe all the instructions in your Solana program]

**Instructions Implemented:**
- Instruction 1: [Description of what it does]
- Instruction 2: [Description of what it does]
- ...

### Account Structure
[TODO: Describe your main account structures and their purposes]

```rust
// Example account structure (replace with your actual structs)
#[account]
pub struct YourAccountName {
    // Describe each field
}
```

## Testing

### Test Coverage
[TODO: Describe your testing approach and what scenarios you covered]

**Happy Path Tests:**
- Test 1: [Description]
- Test 2: [Description]
- ...

**Unhappy Path Tests:**
- Test 1: [Description of error scenario]
- Test 2: [Description of error scenario]
- ...

### Running Tests
```bash
# Commands to run your tests
anchor test
```

### Additional Notes for Evaluators

[TODO: Add any specific notes or context that would help evaluators understand your project better]
