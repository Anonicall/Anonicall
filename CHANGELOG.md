# Changelog
# Registro delle Modifiche

All notable user-facing changes to Anonicall are documented in this file.  
*Tutte le modifiche rilevanti per gli utenti di Anonicall sono documentate in questo file.*

The format follows [Keep a Changelog](https://keepachangelog.com/en/1.0.0/).  
Versioning follows [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

> **Note**: This changelog only covers user-facing features and fixes. Internal tooling changes are not listed here.  
> *Nota: Questo changelog copre solo funzionalità e correzioni visibili agli utenti. Le modifiche agli strumenti interni non sono elencate.*

---

## [2.1.0] — 2026-05-15

### Added / Aggiunto

- **Chat Circuits** — Telegram-style chat folders with a cyberpunk "circuit node" aesthetic. Create named circuits (with emoji and color), assign contacts to them, and filter your chat list instantly. Manage circuits from Settings → "Circuiti Chat".
  - *Circuiti Chat — cartelle chat in stile Telegram con estetica cyberpunk. Crea circuiti con nome, emoji e colore, aggiungi contatti e filtra la lista chat. Gestisci i circuiti da Impostazioni → "Circuiti Chat".*

- **Enhanced Chat Search** — Search results now split into three sections: "Chat" (contacts with active conversations), "⭐ Important Messages" (starred messages matching your query), and "Contacts" (contacts without active chats).
  - *Ricerca chat migliorata — i risultati sono ora divisi in tre sezioni: Chat, ⭐ Messaggi Importanti e Contatti.*

- **Wallet Activity Tab** — The Wallet section now includes an "Attività" tab showing your incoming BNB and BEP-20 transaction history (via BSCScan, updated every 60 seconds). A green badge appears on the tab and the Wallet menu item for new unseen transactions. Tap any transaction to see full details, an optional BSCScan inline preview, and a direct link to open it in the browser.
  - *Tab Attività Portafoglio — storico transazioni in entrata BNB/BEP-20 con badge verde per le nuove transazioni.*

- **Shop & Reseller Quick Access** — Users with store access now see a prominent "Il Mio Negozio" button directly in the Chat list. Reseller users also see a "Le Mie Licenze" banner for quick navigation.
  - *Accesso rapido a Negozio e Licenze direttamente dalla lista chat.*

- **Anonicall Marketplace** — Full marketplace platform with seller storefronts, digital products, services, and consultations. Includes a Reseller Hub with commission tracking, seller management, custom invite links, and marketing templates. New orders management page with buyer/seller roles and dispute resolution.
  - *Marketplace completo con vetrine, prodotti digitali, servizi, consulenze, hub reseller e gestione ordini.*

- **Voucher Redemption** — Users can now redeem one-time voucher codes (format `ANO-XXXX-XXXX-XXXX`) to activate reseller licenses and shop licenses. The redemption flow is available in the License purchase section.
  - *Riscossione voucher — usa codici monouso per attivare licenze reseller e negozio.*

- **Soft-Delete Account with Restore** — When an account is deleted, all personal data is erased for privacy. If the same BSC wallet re-registers, the account is transparently restored and JARVIS sends a personalized welcome-back message with a summary of the previous license history.
  - *Eliminazione soft con ripristino — i dati vengono cancellati ma il wallet può recuperare la licenza precedente alla riregistrazione.*

- **Bridge & Swap** — Cross-chain token bridge and swap functionality powered by LI.FI, accessible directly from the app after connecting your wallet.
  - *Bridge & Swap — conversione cross-chain di token tramite LI.FI.*

- **Phantom Chat** — Ephemeral anonymous 1-on-1 chat encounters. Connect with a random user for a private, temporary conversation with no history.
  - *Phantom Chat — conversazioni anonime ed effimere con utenti casuali, senza storico.*

### Improved / Migliorato

- **Hey Money** — Crypto payment requests now support multi-address wallets and additional networks (BNB, ETH, TRX, USDT, USDC across BSC, Ethereum, and Tron).
  - *Hey Money — supporto multi-wallet e reti aggiuntive per le richieste di pagamento crypto.*

- **AI Assistant (JARVIS / Anonicall AI)** — Improved voice and text interaction. Customizable assistant name and voice. Personalized responses based on your usage history.
  - *Assistente AI migliorato con nome e voce personalizzabili.*

- **Message Actions** — Messages can now be marked as important (starred), pinned in conversations, and deleted with confirmation.
  - *Azioni sui messaggi: contrassegna come importanti, blocca, elimina.*

- **Media Sharing** — File and media sharing now supports up to 25 MB per file with preview thumbnails for images and videos.
  - *Condivisione media fino a 25 MB con anteprime.*

- **Topic Groups** — Community discussion groups now support polls and ranking. Invite contacts directly to groups.
  - *Gruppi tematici con sondaggi, ranking e inviti.*

---

## [2.0.0] — 2026-01-01

### Added / Aggiunto

- **Voice & Video Calls** — Peer-to-peer encrypted calls via WebRTC with call history and duration tracking.
  - *Chiamate voce e video P2P cifrate con storico e durata.*

- **Group Meetings** — Group video conferences powered by Jitsi Meet / JaaS with JWT authentication.
  - *Riunioni di gruppo tramite Jitsi con autenticazione JWT.*

- **Multi-Language Support** — Interface available in 10 languages.
  - *Interfaccia disponibile in 10 lingue.*

- **Profile Photos** — Upload and optimize a profile photo visible to your contacts.
  - *Foto profilo con ottimizzazione immagine.*

- **Camera Switching** — Switch between front and rear cameras during video calls.
  - *Cambio fotocamera durante le videochiamate.*

- **Hey Money** — Crypto payment request system integrated directly in chat. Request and send BNB, ETH, and stablecoins without leaving the conversation.
  - *Hey Money — sistema di richiesta pagamento crypto integrato nella chat.*

- **AI Assistant** — GPT-4o powered voice and text assistant (JARVIS) trained on the Anonicall whitepaper.
  - *Assistente AI JARVIS basato su GPT-4o con input vocale e testuale.*

---

## [1.0.0] — 2025-06-01

### Added / Aggiunto

- **Initial release** — Private 1-on-1 encrypted chat with BSC wallet authentication.
  - *Primo rilascio — chat privata cifrata con autenticazione wallet BSC.*

- **End-to-end encryption** — All messages encrypted with ECDH key exchange and AES-GCM. Keys derived from wallet signatures for cross-device sync.
  - *Cifratura end-to-end con ECDH + AES-GCM, chiavi derivate dalla firma wallet.*

- **Anonymous profiles** — No email, no phone number. Your wallet is your identity.
  - *Profili anonimi — nessuna email, nessun numero di telefono. Il wallet è la tua identità.*

- **Contact requests** — Add contacts by wallet address with a contact request flow.
  - *Richieste di contatto tramite indirizzo wallet.*

- **Typing indicators & read receipts** — Real-time indicators for a natural chat experience.
  - *Indicatori di digitazione e ricevute di lettura in tempo reale.*

- **Online status** — See when your contacts are online.
  - *Stato online dei contatti in tempo reale.*

---

*For security vulnerability reports, see [SECURITY.md](./SECURITY.md).*  
*Per segnalazioni di vulnerabilità di sicurezza, consulta [SECURITY.md](./SECURITY.md).*
