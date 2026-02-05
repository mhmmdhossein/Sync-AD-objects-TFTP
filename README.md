# AD Phonebook Exporter (XML + HTML) + MikroTik Upload

Generate a phonebook from **Active Directory users** and export it as:

- ✅ `cn.xml` (phonebook format for VoIP/IP-Phone / MikroTik usage)
- ✅ `phonebook.html` (searchable + sortable phonebook page)
- ✅ `phonebook.log` (run logs)

Optionally uploads `cn.xml` to **MikroTik** via **FTP**.

---

## Features

- Reads enabled AD users (filters system mailboxes / health mailboxes)
- Extracts phone numbers from:
  - `telephoneNumber`
  - `otherTelephone`
- Cleans & normalizes phone values:
  - splits by `, ; | / \ space newline`
  - removes non-numeric chars (keeps `+`)
  - unique numbers only
- XML phone typing rule:
  - **1 number** → `Home`
  - **Multiple numbers** → first is `RingGroup`, others `Phone1`, `Phone2`, ...
- HTML output:
  - RTL layout (Persian-friendly)
  - Search box (live filter)
  - Clickable sorting on columns
  - Multiple phones displayed as a list with highlighted primary number (red)
  - Generates email links from `SamAccountName + domain`

---

## Output Files

- `C:\Reports\cn.xml`
- `C:\Users\Administrator\Desktop\share\req\phonebook.html`
- `C:\Reports\phonebook.log`

---

## Requirements

- Windows Server / Windows machine joined to domain
- PowerShell 5+ recommended
- ActiveDirectory module:
  - RSAT: Active Directory module for Windows PowerShell
- Permissions:
  - Read access to AD user attributes (standard domain user often enough)

---

## How it Works

1. Queries AD users:
   - enabled users only
   - excludes system/health mailboxes
2. Extracts and cleans phone numbers
3. Builds:
   - `cn.xml` for phonebook import
   - `phonebook.html` for human-friendly directory
4. Uploads `cn.xml` to MikroTik via FTP (optional)

---

## Configuration

Edit these variables in the script:

### Paths
```powershell
$logFile  = "C:\Reports\phonebook.log"
$outFile  = "C:\Reports\cn.xml"
$htmlFile = "C:\Users\Administrator\Desktop\share\req\phonebook.html"
