
## What It Does

This isn't just another Wayback scraper.

  **Archived URL Fetching** – Pull historical URLs from Wayback Machine.
  **Backup File Detection** – Find `.zip`, `.bak`, `.sql`, `.tar.gz`, `.old`, and other juicy files.
  **Historical Backups** - Looks for historical backups for the identified backup files.
  **Attack Mode** – Scan for vulnerable endpoints using patterns/signatures:
   - XSS
   - SQLi
   - LFI
   - Open Redirects
   - WordPress Vulns
   - JIRA-based misconfig
  **GET Parameter Mapping** – Map every GET parameter to where it appears. (Great for fuzzing automation.)
  **JWT Detection** – Detect and decode JWTs embedded in archived URLs.
  **Directory Listing Detection** – Find open indexed directories.
  **Subdomain Enumeration** – Pull subdomains seen in archived data.
  **Keyword Search** – Search custom keywords like `config`, `backup`, `.log`, etc.
  **Custom Payload Lists** – Use your own fuzz list or signatures for custom scans.

---

##  Installation

Tested on **Python 3** across Ubuntu/Kali/Windows.

```bash
git clone https://github.com/texech/recon-xp
````
```bash
cd recon-xp
````
```bash
pip3 install -r requirements.txt
````

---

##  Usage

```bash
python3 recon-xp.py <target.com> [OPTIONS]
```

**Note:** Don't use `http://` or `https://` in the domain — just pass `domain.com` or `sub.domain.com`.

---

##  Options

| Option            | Description                                                  |
| ----------------- | ------------------------------------------------------------ |
| `--fetch`         | Fetch archived URLs from Wayback                             |
| `--backups`       | Scan for exposed backup/config files                         |
| `--attack [type]` | Run attack mode (xss, sqli, lfi, redirect, jira, wp, custom) |
| `--jwt`           | Detect & decode JWT tokens                                   |
| `--subdomains`    | Extract subdomains from historical URLs                      |
| `--parameters`    | Extract GET parameters & map them to URLs                    |
| `--listings`      | Detect open directory listings                               |

---

##  Example Workflows


#### Fetch all Wayback URLs
```bash
python3 recon-xp.py example.com --fetch
```
#### Look for exposed backup files
```bash
python3 recon-xp.py example.com --backups
```
#### Look for directory listing
```bash
python3 recon-xp.py example.com --listings
```
#### Scan for possible XSS points
```bash
python3 recon-xp.py example.com --attack xss
```
#### Map parameters from archived data
```bash
python3 recon-xp.py example.com --parameters
```
### Extract JWTs
```bash
python3 recon-xp.py example.com --jwt
```
### And much more
```bash
usage: recon-xp.py [-h] [--fetch] [--jwt] [--backups] [--subdomains] [--listings] [--attack {xss,sqli,lfi,redirect,jira,wp,fuzz}] [--menu]
                         [--parameters]
                         target
```
---

##  Output Structure

All results are neatly saved under the `content/` directory:

```
content/
└── example.com/
    ├── example.com_URLs.txt
    ├── example.com_xss.txt
    ├── example.com_sqli.txt
    ├── example.com_parameters.txt
    ├── example.com_subdomain.txt
    └── ...
```

---

##  Add Your Own Payloads

You can fully customize the payloads for XSS, SQLi, fuzzing, etc. Just edit the respective `.txt` files inside the repo and fire away!




