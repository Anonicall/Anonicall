# Security Policy
# Politica di Sicurezza

---

## English

### Supported Versions

| Version | Supported |
|---------|-----------|
| Latest (live app) | ✅ |
| Older / cached versions | ❌ |

We maintain a single, continuously updated production deployment at **[app.anonicall.com](https://app.anonicall.com)**. All security fixes are applied to the live platform immediately upon validation.

---

### Reporting a Vulnerability

We take the security of Anonicall and the privacy of our users very seriously.

**If you discover a security vulnerability, please do NOT open a public GitHub Issue.**

Instead, report it responsibly via email:

📧 **support@anonicall.com**

Please include in your report:
- A clear description of the vulnerability
- Steps to reproduce the issue
- The potential impact (what data or functionality is affected)
- Your suggested fix or mitigation (optional but appreciated)

We will acknowledge your report within **48 hours** and aim to provide a fix or mitigation timeline within **7 business days**.

We are committed to **not taking legal action** against researchers who report vulnerabilities responsibly and in good faith, following this policy.

---

### Scope — What is in scope

- The live web application at [app.anonicall.com](https://app.anonicall.com)
- Authentication flow (BSC wallet signature and nonce system)
- End-to-end encryption implementation
- API endpoints accessible by authenticated users
- WebSocket message handling
- Payment and crypto transaction flows (Hey Money, Bridge & Swap)
- Session management and access control

---

### Out of Scope

The following are **not** considered valid vulnerability reports:

- Attacks requiring physical access to a user's device
- Social engineering of platform users or staff
- Denial-of-service (DoS/DDoS) attacks
- Issues in third-party services we rely on (BSCScan, Jitsi, LI.FI, WalletConnect) — please report those to the respective vendors
- Theoretical vulnerabilities without a working proof-of-concept
- Issues in outdated or unsupported browsers
- Self-XSS that requires a user to run code in their own browser console
- Rate limiting or brute-force issues without demonstrated impact

---

### Responsible Disclosure Commitment

We follow a **coordinated disclosure** model:

1. You report the issue privately to us
2. We investigate and develop a fix
3. We deploy the fix to production
4. We publicly acknowledge the report (with your permission) after the fix is live

**We ask that you do not publicly disclose the vulnerability details until we have confirmed a fix is deployed.** We will work as quickly as possible to resolve confirmed issues.

---

### Recognition

We genuinely appreciate the work of security researchers. While we do not currently operate a formal bug bounty program, we will publicly credit researchers (with their consent) in our changelog for responsibly disclosed and confirmed vulnerabilities.

---

## Italiano

### Segnalazione di una Vulnerabilità

Se scopri una vulnerabilità di sicurezza, **non aprire una Issue pubblica su GitHub**.

Segnalala in modo responsabile via email:

📧 **support@anonicall.com**

Includi nella segnalazione:
- Una descrizione chiara della vulnerabilità
- I passi per riprodurre il problema
- L'impatto potenziale (quali dati o funzionalità sono interessati)
- Una soluzione suggerita (opzionale ma apprezzata)

Risponderemo entro **48 ore** e forniremo una tempistica per la correzione entro **7 giorni lavorativi**.

---

### Ambito di Applicazione

**In scope:**
- Applicazione web live su [app.anonicall.com](https://app.anonicall.com)
- Flusso di autenticazione tramite firma wallet BSC
- Implementazione della cifratura end-to-end
- Endpoint API accessibili dagli utenti autenticati
- Gestione sessioni e controllo accessi
- Flussi di pagamento crypto (Hey Money, Bridge & Swap)

**Fuori scope:**
- Attacchi che richiedono accesso fisico al dispositivo dell'utente
- Social engineering di utenti o staff
- Attacchi DoS/DDoS
- Problemi in servizi di terze parti (BSCScan, Jitsi, LI.FI, WalletConnect)
- Vulnerabilità teoriche senza proof-of-concept funzionante

---

### Impegno alla Divulgazione Responsabile

Seguiamo un modello di **divulgazione coordinata**: segnali il problema in privato, noi correggiamo, poi confermiamo pubblicamente (con il tuo consenso) dopo il rilascio della correzione.

**Ti chiediamo di non divulgare pubblicamente i dettagli della vulnerabilità fino a quando non confermiamo che la correzione è stata applicata in produzione.**
