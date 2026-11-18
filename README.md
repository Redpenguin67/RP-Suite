# Red Penguin OSINT Suite

Suite di strumenti **OSINT** e di sicurezza del progetto **Red Penguin**, per **Linux** e
**Windows**. Software **open source** con licenza **MIT**: il codice è pubblico e
verificabile.

I programmi sono indipendenti ma condividono lo stesso stile, il tema giorno/notte e la
gestione centralizzata delle chiavi API tramite **IGLOO**.

---

## I programmi

| Programma | Versione | A cosa serve |
|---|---|---|
| **IGLOO** | 1.2.3 | Gestore centralizzato delle **chiavi API** (servizi AI come Gemini/Groq, servizi come Shodan/VirusTotal) condiviso da tutta la suite. Custodisce le chiavi in un archivio locale per-macchina; gli altri programmi le leggono da lì. |
| **FALCO** | 1.7.4 | Strumento **OSINT** con catena AI multi-provider: ricerca per username, telefono, nome/cognome e social, controllo dei **data breach** di una mail, arricchimento Shodan/VirusTotal, profilo e indice di rischio, report stampabile. |
| **LINCE** | 3.1.8 | *Localizza Insidie Nascoste in Contenuti Elettronici*: analisi di **email** (esistenza, breach) estesa a **file, cartelle, immagini, QR, metadati e URL/domini**, con verifica via VirusTotal. |
| **VARCO** | 1.0.6 | *Verifica Attiva, Ricognizione e Classificazione Obiettivi*: scanner di **vulnerabilità** di host e rete, con arricchimento Shodan/VirusTotal. |

---

## Requisiti

- **Windows** 10 o 11 a 64 bit, **oppure** **Linux** su base Debian (Debian, Ubuntu, Linux
  Mint, Kali…).
- Alcune funzioni usano servizi esterni e richiedono **chiavi API gratuite o freemium**
  (es. Gemini, Groq, Shodan, VirusTotal). Si inseriscono una sola volta in **IGLOO**.

---

## Installazione

Scarica i file dalla pagina **[Releases](../../releases)**.

> ⚠️ **Windows:** gli installer e gli eseguibili possono dare **falsi positivi**
> dell'antivirus. Prima di installare leggi la sezione
> **[Avviso antivirus](#avviso-antivirus-windows--falsi-positivi)** più in basso: trovi la
> spiegazione, le impronte SHA-256 e come verificarle.

### Windows

1. Scarica l'installer `*-setup.exe` del programma che ti serve.
2. Installa **IGLOO per primo**: crea la categoria **«Red Penguin Suite»** nel menu Start e
   prepara la gestione delle chiavi condivisa.
3. Installa gli altri programmi.

La disinstallazione si fa dall'installer stesso o dal **Pannello di controllo**.

### Linux (Debian / Ubuntu)

Scarica i pacchetti `.deb` e installali, per esempio:

```bash
sudo apt install ./rp-igloo_1.2.3_all.deb
```

Installa **IGLOO per primo**, poi gli altri `.deb`. Ogni pacchetto aggiunge la sua voce nel
menu, sotto **«Red Penguin Suite»**.

---

## Chiavi API

Le chiavi si gestiscono **solo in IGLOO**, che le salva in locale sulla tua macchina. Gli
altri programmi della suite le leggono in **sola lettura** e le usano quando servono. Senza
chiavi, le funzioni di base restano disponibili; quelle che dipendono da un servizio
esterno si attivano una volta inserita la relativa chiave.

---

## Avviso antivirus (Windows) — falsi positivi

I file Windows della suite (gli installer `*-setup.exe` e gli eseguibili `*.exe`) possono
essere segnalati come sospetti da alcuni motori antivirus. **Sono falsi positivi.**

### Perché succede

- Gli eseguibili sono creati con **PyInstaller**, che impacchetta l'interprete Python
  insieme al programma. Il suo componente di avvio è identico in migliaia di applicazioni
  Python, e il codice vero finisce in un blocco compresso ad alta entropia. Alcuni motori
  **euristici o basati su machine learning** segnalano questa *struttura*, a prescindere
  dal contenuto.
- I file **non sono firmati digitalmente** e sono **nuovi**: senza una reputazione già
  costruita, gli stessi motori tendono a essere prudenti.

Non c'è codice malevolo: il progetto è open source con licenza MIT e il codice è pubblico.
Solo una minoranza di motori (una manciata su circa 70) segnala i file, quasi tutti di tipo
euristico/ML. Il referto pubblico di VirusTotal lo mostra chiaramente.

### Come verificare

Confronta l'impronta **SHA-256** del file scaricato con quella in tabella, poi apri il
referto VirusTotal corrispondente.

- **Windows (PowerShell):** `Get-FileHash .\NOME_FILE.exe -Algorithm SHA256`
- **Linux / macOS:** `sha256sum NOME_FILE.exe`

**IGLOO 1.2.3**

| File | SHA-256 | VirusTotal |
|---|---|---|
| `IGLOO-1.2.3-setup.exe` | `b11b2974b4d9a7b73f78c4770d66e1d204f9343bf14a3185eb9261f7728049f7` | [Referto](https://www.virustotal.com/gui/file/b11b2974b4d9a7b73f78c4770d66e1d204f9343bf14a3185eb9261f7728049f7) |
| `IGLOO.exe` | `9bd9b06453b9ed53bbfc96a8f632523f4b45f1de295b468224826a0164783ea9` | [Referto](https://www.virustotal.com/gui/file/9bd9b06453b9ed53bbfc96a8f632523f4b45f1de295b468224826a0164783ea9) |

**FALCO 1.7.4**

| File | SHA-256 | VirusTotal |
|---|---|---|
| `FALCO-1.7.4-setup.exe` | `a2445c1955223c345f1206172a1aac14e21d8c613bc67185fee883e58c1c5355` | [Referto](https://www.virustotal.com/gui/file/a2445c1955223c345f1206172a1aac14e21d8c613bc67185fee883e58c1c5355) |
| `FALCO.exe` | `2ce327dab58432e3408b12f7fcd62bd90e573f0a12fa619830d16da9277e2c8b` | [Referto](https://www.virustotal.com/gui/file/2ce327dab58432e3408b12f7fcd62bd90e573f0a12fa619830d16da9277e2c8b) |

**LINCE 3.1.8**

| File | SHA-256 | VirusTotal |
|---|---|---|
| `LINCE-3.1.8-setup.exe` | `1cf33c96bff99b7a9450febac08c7108cb4b56d46cbdd086d17dded669c7ae2f` | [Referto](https://www.virustotal.com/gui/file/1cf33c96bff99b7a9450febac08c7108cb4b56d46cbdd086d17dded669c7ae2f) |
| `LINCE.exe` | `8833a74c1ce20a319378b85ae5962815f3a9d4a094b953441ffa64fd6044d4fb` | [Referto](https://www.virustotal.com/gui/file/8833a74c1ce20a319378b85ae5962815f3a9d4a094b953441ffa64fd6044d4fb) |

**VARCO 1.0.6**

| File | SHA-256 | VirusTotal |
|---|---|---|
| `VARCO-1.0.6-setup.exe` | `6a11ea270447d0563af23fccfb578d299a4765cca81460b09f01024f11c97c56` | [Referto](https://www.virustotal.com/gui/file/6a11ea270447d0563af23fccfb578d299a4765cca81460b09f01024f11c97c56) |
| `VARCO.exe` | `329b4afeb9a9f481fa40abbb340961c65a2e1de5802f461ca3abe199b071c27c` | [Referto](https://www.virustotal.com/gui/file/329b4afeb9a9f481fa40abbb340961c65a2e1de5802f461ca3abe199b071c27c) |

### Se un antivirus blocca un file

1. **Verifica l'SHA-256:** deve coincidere con quello in tabella. Se non coincide, non
   usarlo e riscaricalo dalla Release ufficiale.
2. **Guarda il referto VirusTotal:** i motori che segnalano sono pochi e di tipo
   euristico/ML.
3. Se ti fidi della verifica, aggiungi un'eccezione per quel file, **oppure** compila dai
   sorgenti.

Al primo avvio Windows può anche mostrare l'avviso SmartScreen *«Windows ha protetto il
PC»*, perché i file non sono firmati: verificato l'SHA-256, procedi con **Ulteriori
informazioni → Esegui comunque**.

> Le impronte qui sopra valgono per la release **`suite-2026.11.17`**. Ogni nuova release
> produce file diversi, quindi SHA-256 diversi: fai sempre riferimento alla tabella della
> versione che stai usando.

---

## Uso responsabile

Questi strumenti sono pensati per attività **OSINT** e di **sicurezza legittime**: ricerca
su dati pubblici, verifica di caselle e domini, audit di sicurezza. Usali **solo** su
obiettivi di tua proprietà o per i quali hai un'**autorizzazione esplicita** (per esempio
un mandato scritto del cliente). La scansione di reti e sistemi altrui senza permesso, e il
trattamento di dati personali fuori dai casi consentiti, possono essere **illegali**. La
responsabilità dell'uso è di chi utilizza i programmi.

---

## Licenza

Distribuito con licenza **MIT**. Vedi il file `LICENSE`.

## Contatti

Dubbi o segnalazioni: **IamRedPenguin@proton.me**
