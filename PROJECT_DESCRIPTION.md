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
 

**Instructions Implemented:**
- `publish_note` - Creates and stores a new note on the Solana blockchain
- Purpose: Allows users to publish personal notes with unique identifiers
- Parameters:
- `note_id: u64` - Unique identifier for the note within user's collection
- `content: String` - The actual note content (max 280 characters)
- Validation: Ensures content doesn't exceed 280 characters to optimize storage
- Functionality: Initializes a new PDA account storing the author's public key, note ID, and content
- Security: Only the signing author can create notes in their own namespace


### Account Structure
 

```rust
#[account]
pub struct Note {
    pub author: Pubkey,    // Stores the wallet address of the note creator
    pub note_id: u64,      // Unique identifier for organizing multiple notes per user
    pub content: String,   // The actual note text content with 280-character limit
}

impl Note {
    pub const SIZE: usize = 8 +      // discriminator (Anchor internal use)
                            32 +     // author - stores the 32-byte public key
                            8 +      // note_id - 8 bytes for u64 identifier
                            4 + 280; // content - 4 bytes for string length + 280 chars max
}
```
- The Note account serves as persistent on-chain storage for user-generated content, providing:

- Data Persistence: Notes are permanently stored on Solana blockchain

- Ownership Verification: author field cryptographically links note to creator

- Organization: note_id enables users to manage multiple notes

- Efficient Storage: Fixed size allocation optimizes rent costs

### Context Account Structure:

```rust
pub struct PublishNote<'info> {
    pub note: Account<'info, Note>,      // The PDA note account being created
    pub author: Signer<'info>,           // The user creating/paying for the note
    pub system_program: Program<'info, System>, // Solana system program for account creation
}
```


## Testing

### Test Coverage

Comprehensive test suite covering both successful operations and error scenarios to ensure program reliability and security.

**Happy Path Tests:**

- Test 1: `Successful Note Publication` - Verifies that a note can be created with valid parameters including note ID and content, properly storing all data in the PDA account
- Test 2: `Multiple Notes per Author` - Confirms that users can create multiple distinct notes by using different note IDs, generating unique PDAs for each note
- Test 3: `PDA Deterministic Addressing` - Ensures that the same seeds always generate the same PDA address for consistent note retrieval


**Unhappy Path Tests:**
- Test 1: `Content Length Validation` - Verifies that notes exceeding 280 characters are properly rejected with the ContentTooLong error
- Test 2: `Unauthorized Access Prevention` - Ensures that users cannot modify or access notes belonging to other authors
- Test 3: `Duplicate Note Prevention` - Confirms that creating notes with the same ID for the same author properly handles account conflicts

### Running Tests
```bash
# Commands to run your tests
anchor test
```

### Additional Notes for Evaluators

This is my first Solana Dapp and it was excellent learning curve. Since solana was creating issue in compiling on my system so I used solana playground for development.
