# Anonicall Whitepaper

**Version 2.0**  
**January 2026**

---

## Table of Contents

1. [Executive Summary](#executive-summary)
2. [Introduction](#introduction)
3. [Platform Architecture](#platform-architecture)
4. [Authentication System](#authentication-system)
5. [End-to-End Encryption](#end-to-end-encryption)
6. [Contact Management](#contact-management)
7. [Real-Time Messaging](#real-time-messaging)
8. [Voice and Video Calls](#voice-and-video-calls)
9. [Group Meetings](#group-meetings)
10. [Internationalization](#internationalization)
11. [User Profiles](#user-profiles)
12. [Data Storage & Privacy](#data-storage--privacy)
13. [Security Model](#security-model)
14. [Technical Specifications](#technical-specifications)
15. [Future Roadmap](#future-roadmap)

---

## Executive Summary

Anonicall is a privacy-first, anonymous chat application that leverages blockchain wallet authentication and end-to-end encryption to provide secure communications. Built on the BNB Smart Chain (BSC) ecosystem, Anonicall enables users to communicate without revealing personal information while maintaining the highest standards of cryptographic security.

### Key Features

- **Wallet-Based Authentication**: No email, phone, or personal data required
- **End-to-End Encryption**: ECDH key exchange with AES-GCM encryption
- **Cross-Device Sync**: Encrypted messages stored in database, accessible from any device
- **Real-Time Communication**: WebSocket-based instant messaging
- **Voice and Video Calls**: Peer-to-peer WebRTC calling with camera switching
- **Group Meetings**: Jitsi Meet integration for multi-user video conferences
- **Privacy Controls**: Public/private profile visibility options
- **Contact Approval System**: Users must accept contact requests before messaging
- **Multi-Language Support**: Available in 10 languages worldwide
- **Profile Customization**: Optional profile photos with image optimization

---

## Introduction

### The Privacy Problem

Traditional messaging applications require personal information for registration and often store messages in plaintext on centralized servers. This creates privacy vulnerabilities and exposes user data to potential breaches.

### The Anonicall Solution

Anonicall addresses these concerns by:

1. **Eliminating Personal Data Requirements**: Users authenticate using their cryptocurrency wallet
2. **Implementing True E2E Encryption**: Messages are encrypted before leaving the user's device
3. **Decentralizing Identity**: Wallet addresses serve as unique identifiers without revealing personal information
4. **Private Profiles**: Complete untraceability for users who choose to remain hidden

---

## Platform Architecture

### Frontend Stack

| Component | Technology |
|-----------|------------|
| Framework | React 18 with TypeScript |
| Bundler | Vite |
| Routing | Wouter (lightweight router) |
| State Management | TanStack React Query + React Hooks |
| Styling | Tailwind CSS with custom cyberpunk theme |
| UI Components | shadcn/ui + Radix UI primitives |
| Animations | Framer Motion |
| Web3 Integration | RainbowKit + Wagmi |
| WebRTC | Native RTCPeerConnection API |
| Video Meetings | Jitsi Meet External API |

### Backend Stack

| Component | Technology |
|-----------|------------|
| Runtime | Node.js |
| Framework | Express.js |
| Language | TypeScript (tsx for development) |
| Database | PostgreSQL with Drizzle ORM |
| Real-Time | WebSocket (ws library) |
| Session Management | express-session with pg-store |

### Blockchain Integration

- **Network**: BNB Smart Chain (BSC) - Chain ID 56
- **Wallet Support**: MetaMask, Trust Wallet, WalletConnect
- **Signature Verification**: viem library for cryptographic verification

---

## Authentication System

### Wallet-Based Authentication Flow

```
1. User connects wallet via RainbowKit
2. Frontend requests nonce from backend
3. Backend generates unique nonce and stores with user record
4. User signs nonce message with wallet private key (once only)
5. Backend verifies signature using viem's verifyMessage
6. Session established on successful verification
```

### Technical Implementation

**Nonce Generation**:
```
Sign this message to login to Anonicall: [random 8-byte hex]
```

**Signature Verification**:
- Uses viem's `verifyMessage` function
- Validates signature against stored nonce
- Nonce rotated after each successful login

### Session Management

- Sessions stored in PostgreSQL via `connect-pg-simple`
- 30-day session expiration
- Session persists across navigation (single sign required)
- No repeated signature requests during active session

---

## End-to-End Encryption

### Cryptographic Protocol

Anonicall uses the Elliptic Curve Diffie-Hellman (ECDH) key exchange combined with AES-GCM symmetric encryption.

### Key Generation

1. Each user generates an ECDH key pair on first login
2. Keys stored in browser localStorage, tied to wallet address
3. Public key uploaded to server for key exchange

**Algorithm Specifications**:
- Curve: P-256 (NIST)
- Key Derivation: ECDH
- Encryption: AES-GCM with 256-bit keys
- IV: 12 bytes, randomly generated per message

### Encryption Flow

```
1. Sender retrieves recipient's public key from server
2. Sender derives shared secret using:
   - Sender's private key
   - Recipient's public key
3. AES-GCM key derived from shared secret
4. Message encrypted with random IV
5. Encrypted content + IV sent to server
```

### Decryption Flow

```
1. Recipient retrieves conversation partner's public key (cached locally)
2. Recipient derives identical shared secret using:
   - Recipient's private key
   - Partner's public key
3. Message decrypted using shared secret and IV

Note: Due to ECDH properties, both parties derive the same shared secret:
- User A: (A's private key) + (B's public key) = shared secret
- User B: (B's private key) + (A's public key) = same shared secret
This allows both encryption and decryption using the partner's public key.
```

### Security Properties

- **Zero Knowledge**: Server never sees plaintext messages
- **Unique IV**: Each message uses a random 12-byte IV
- **Key Caching**: Public keys cached locally to prevent network failures
- **Client-Side Encryption**: All encryption happens in browser before transmission

---

## Contact Management

### Contact Request System

Users must go through an approval process before messaging:

1. **Search**: Users search by nickname or wallet address (public profiles only)
2. **Request**: Sender initiates contact request
3. **Approval**: Recipient accepts or rejects
4. **Mutual Add**: On acceptance, both users added as contacts

### Request States

| State | Description |
|-------|-------------|
| pending | Awaiting recipient response |
| accepted | Request approved, contact added |
| rejected | Request denied, sender cannot re-request |

### Rejection Handling

When a request is rejected, the original sender cannot send another request. The recipient must initiate contact if they change their mind.

### Auto-Accept Logic

If User A sends a request to User B, and User B also sends a request to User A, the system auto-accepts both requests and adds mutual contacts.

---

## Real-Time Messaging

### WebSocket Architecture

All real-time communication uses WebSocket connections on the `/ws` endpoint.

### Message Types

| Type | Direction | Purpose |
|------|-----------|---------|
| join | Client -> Server | User identification on connect |
| chat | Bidirectional | Send/receive messages |
| typing | Bidirectional | Typing indicator status |
| connected | Server -> Client | Connection confirmation |
| online_status | Server -> Client | Contact online/offline status |

### Message Structure

```json
{
  "type": "chat",
  "id": "uuid-v4",
  "senderId": 1,
  "senderAddress": "0x...",
  "senderNickname": "User",
  "recipientId": 2,
  "content": "encrypted-content",
  "timestamp": 1706097600000
}
```

### Connection Management

- Auto-reconnect with exponential backoff (1s to 30s)
- Reconnection attempts on connection loss
- Online/offline status tracking
- Unread message badges per conversation

### Post-Call Messages

After a voice or video call ends, a system message is automatically inserted into the chat showing:
- Call type (voice or video)
- Call duration
- Timestamp

---

## Voice and Video Calls

### WebRTC Architecture

Anonicall implements peer-to-peer voice and video calls using WebRTC technology, ensuring calls remain as private as possible.

### Call Features

| Feature | Description |
|---------|-------------|
| Voice Calls | High-quality audio between contacts |
| Video Calls | Full HD video with audio |
| Camera Switching | Switch between front/rear cameras on mobile |
| Mute/Unmute | Toggle microphone during calls |
| Camera On/Off | Toggle video during calls |
| Call History | Complete log of all calls |

### Signaling Protocol

Call signaling uses the existing WebSocket infrastructure:

| Message Type | Purpose |
|--------------|---------|
| call_offer | Initiate call with SDP offer |
| call_answer | Accept call with SDP answer |
| ice_candidate | Exchange ICE candidates for connectivity |
| call_end | Terminate call |
| call_rejected | Decline incoming call |

### NAT Traversal

- Uses public STUN servers for NAT traversal
- Supports direct peer-to-peer connections when possible
- Falls back through relay when necessary

### Call History

All calls are logged with:
- Call type (voice/video)
- Duration
- Timestamp
- Direction (incoming/outgoing)
- Status (completed, missed, rejected)

---

## Group Meetings

### Jitsi Meet Integration

Anonicall leverages Jitsi Meet for group video meetings, providing:

| Feature | Description |
|---------|-------------|
| Create Meeting | Generate unique meeting room |
| Custom Titles | Name meetings for easy identification |
| Invite Contacts | Send meeting invitations to contacts |
| Accept/Decline | Respond to meeting invitations |
| Copy Link | Share meeting link externally |
| Join Meeting | Opens Jitsi Meet in new tab |

### Meeting Flow

```
1. User creates meeting with optional title
2. User invites selected contacts
3. Invited contacts receive invitation notification
4. Contacts can accept or decline invitation
5. All participants join via Jitsi Meet
```

### Meeting Invitations

Invitations are delivered in real-time via WebSocket and include:
- Meeting title
- Inviter's nickname
- Join link
- Accept/Decline actions

---

## Internationalization

### Multi-Language Support

Anonicall is available in 10 languages to serve users worldwide:

| Language | Code | Native Name |
|----------|------|-------------|
| English | en | English |
| Chinese (Simplified) | zh | 中文 |
| Spanish | es | Español |
| Hindi | hi | हिन्दी |
| Arabic | ar | العربية |
| Portuguese | pt | Português |
| Russian | ru | Русский |
| French | fr | Français |
| Italian | it | Italiano |
| German | de | Deutsch |

### Language Selection

- Default language: English
- User selects preferred language during profile setup
- Language can be changed anytime in Settings
- Preference stored both locally and in database
- Synced across devices for logged-in users

### Implementation

- Client-side translation system
- All UI strings support all 10 languages
- Dynamic language switching without page reload
- LocalStorage persistence for faster loading

---

## User Profiles

### Profile Setup

During registration, users configure:

1. **Nickname**: Display name (3-20 characters)
2. **Profile Photo**: Optional, resized to 200x200px
3. **Visibility**: Public or Private
4. **Language**: Preferred interface language

### Profile Photos

| Feature | Specification |
|---------|---------------|
| Format | JPEG (compressed) |
| Size | 200x200 pixels |
| Quality | 80% compression |
| Max Upload | 2MB |
| Storage | Base64 data URL |

### Profile Visibility

**Public Profiles**:
- Searchable by nickname and wallet address
- Can receive contact requests
- Appear in search results

**Private Profiles**:
- Completely untraceable
- Cannot be searched
- Cannot receive contact requests
- Only the user can initiate contact

---

## Data Storage & Privacy

### Database Schema

**Users Table**
| Field | Type | Description |
|-------|------|-------------|
| id | serial | Primary key |
| walletAddress | text | Unique wallet address |
| nickname | text | User display name |
| isPublic | boolean | Profile visibility |
| publicKey | text | ECDH public key (JSON) |
| profilePhoto | text | Base64 photo data |
| preferredLanguage | text | Language code |
| nonce | text | Auth nonce |

**Encrypted Messages Table**
| Field | Type | Description |
|-------|------|-------------|
| id | serial | Primary key |
| messageId | text | Unique message UUID |
| ownerUserId | integer | Message owner |
| partnerUserId | integer | Conversation partner |
| senderUserId | integer | Original sender |
| encryptedContent | text | AES-GCM ciphertext |
| iv | text | Initialization vector |
| timestamp | timestamp | Message time |

**Call History Table**
| Field | Type | Description |
|-------|------|-------------|
| id | serial | Primary key |
| callerId | integer | User who initiated call |
| recipientId | integer | User who received call |
| callType | text | voice or video |
| duration | integer | Duration in seconds |
| status | text | completed, missed, rejected |
| startedAt | timestamp | Call start time |
| endedAt | timestamp | Call end time |

**Meetings Table**
| Field | Type | Description |
|-------|------|-------------|
| id | serial | Primary key |
| creatorId | integer | User who created meeting |
| title | text | Meeting title |
| roomId | text | Jitsi room identifier |
| createdAt | timestamp | Creation time |

### Storage Model

- **Client-Side Storage**: Each user's client saves their own encrypted copy
- When a message is sent/received, the client encrypts and saves to database
- `ownerUserId` determines which user owns each encrypted copy
- `messageId` prevents duplicate storage of the same message
- Each user can only access and decrypt their own copies

### Privacy Guarantees

1. **No Plaintext Storage**: All messages encrypted before database storage
2. **User-Controlled Keys**: Encryption keys never leave user's browser
3. **Developer Cannot Decrypt**: Server has no access to private keys
4. **Data Minimization**: Only essential data stored
5. **Private Profile Protection**: Private users are completely invisible

---

## Security Model

### Threat Model

Anonicall protects against:

1. **Server Compromise**: Encrypted data useless without user keys
2. **Man-in-the-Middle**: ECDH provides key agreement without key transmission
3. **Replay Attacks**: Unique message IDs and timestamps
4. **Session Hijacking**: Secure session management with PostgreSQL store
5. **Tracking**: Private profiles cannot be discovered or monitored

### Encryption Failure Handling

- If encryption fails, message not saved (no plaintext fallback)
- If decryption fails, placeholder shown instead of corrupted data
- Failed conversations skipped from storage

### Key Storage

| Data | Storage | Protection |
|------|---------|------------|
| Private Keys | localStorage | Tied to wallet address |
| Public Keys | Server + localStorage cache | No security risk |
| Session | PostgreSQL | HTTP-only cookie |
| Profile Photo | PostgreSQL | Tied to user account |

---

## Technical Specifications

### API Endpoints

**Authentication**
- `POST /api/auth/nonce` - Request login nonce
- `POST /api/auth/verify` - Verify wallet signature
- `GET /api/auth/me` - Get current user
- `POST /api/auth/logout` - End session

**User Management**
- `POST /api/user/profile/setup` - Initial profile setup
- `PATCH /api/user/profile` - Update profile (nickname, photo, visibility)
- `GET /api/users/search?q=` - Search public users
- `POST /api/user/public-key` - Update encryption key
- `GET /api/user/:userId/public-key` - Get user's public key

**Contacts**
- `GET /api/contacts` - List contacts
- `POST /api/contacts` - Add contact
- `DELETE /api/contacts/:contactId` - Remove contact

**Contact Requests**
- `GET /api/contact-requests/pending` - Incoming requests
- `GET /api/contact-requests/sent` - Sent requests
- `POST /api/contact-requests` - Create request
- `POST /api/contact-requests/:id/respond` - Accept/reject

**Encrypted Messages**
- `POST /api/messages/encrypted` - Save encrypted message
- `GET /api/messages/encrypted/:partnerUserId` - Get conversation
- `GET /api/messages/conversations` - Get all conversations
- `DELETE /api/messages/encrypted` - Clear message history

**Calls**
- `GET /api/calls/history` - Get call history
- `POST /api/calls` - Log new call

**Meetings**
- `POST /api/meetings` - Create meeting
- `GET /api/meetings` - Get user's meetings
- `POST /api/meetings/:id/invite` - Invite contacts to meeting

**Settings**
- `GET /api/settings` - Get user settings
- `POST /api/settings` - Update settings

### Performance Characteristics

| Metric | Value |
|--------|-------|
| Message Delivery | Real-time (WebSocket) |
| Encryption Time | < 10ms per message |
| Database Sync | Async, non-blocking |
| Reconnection Delay | 1s - 30s exponential |
| Call Setup Time | < 2 seconds typical |
| Photo Processing | < 500ms client-side |

---

## Future Roadmap

### Completed Features (v2.0)

- Voice and Video Calls with WebRTC
- Call History with duration tracking
- Group Meetings via Jitsi Meet
- Multi-Language Support (10 languages)
- Profile Photos with optimization
- Camera switching during video calls

### Phase 2 Features

1. **Group Chat**: Encrypted group conversations
2. **Media Sharing**: End-to-end encrypted file transfers
3. **Message Expiration**: Self-destructing messages
4. **Multiple Wallet Support**: Link multiple wallets to one identity

### Phase 3 Features

1. **Mobile Applications**: Native iOS and Android apps
2. **Push Notifications**: Encrypted push notification system
3. **Token Integration**: BSC token-gated features
4. **Advanced Call Features**: Screen sharing, call recording

### Phase 4 Features

1. **Decentralized Storage**: IPFS integration for message storage
2. **Cross-Chain Support**: Multiple blockchain networks
3. **DAO Governance**: Community-driven development
4. **Zero-Knowledge Proofs**: Enhanced privacy features

---

## Conclusion

Anonicall represents a new paradigm in secure messaging and communication, combining the security of blockchain wallet authentication with state-of-the-art end-to-end encryption. By eliminating the need for personal information and ensuring that even the platform operators cannot access message contents, Anonicall provides true privacy for its users.

With the addition of voice and video calls, group meetings, and multi-language support, Anonicall now offers a complete communication platform that prioritizes privacy without sacrificing functionality.

The platform's architecture ensures that security and usability coexist, providing a seamless experience while maintaining the highest cryptographic standards.

---

**Document Version**: 2.0  
**Last Updated**: January 2026  
**Contact**: Visit the application at the deployed URL

---

*This whitepaper is for informational purposes only and does not constitute financial advice or a guarantee of features.*
