# Google Dorks — OSINT Quick Reference

> Advanced search operators for recon, indexed files, exposed data, and targeted searching.

---

# Core Operators

## `site:`

Search only inside a domain.

```txt
site:example.com login
```

### Examples

```txt
site:gov.uk
site:github.com token
site:pastebin.com password
```

Best for:

- limiting noise
    
- domain recon
    
- finding hidden pages
    

---

## `filetype:` / `ext:`

Find specific indexed files.

```txt
site:example.com ext:pdf
```

### Common Extensions

```txt
pdf
docx
xlsx
sql
log
env
json
xml
zip
bak
```

### Examples

```txt
ext:sql "INSERT INTO"
ext:log password
ext:env DB_PASSWORD
```

Best for:

- leaks
    
- backups
    
- documentation
    
- configs
    

---

## `intitle:`

Search page titles.

```txt
intitle:"index of"
```

### Examples

```txt
intitle:admin
intitle:"login panel"
intitle:"dashboard"
```

Best for:

- open directories
    
- admin panels
    
- internal tools
    

---

## `inurl:`

Search inside URLs.

```txt
inurl:admin
```

### Examples

```txt
inurl:login
inurl:php?id=
inurl:api
```

Best for:

- parameters
    
- APIs
    
- vulnerable endpoints
    

---

## `intext:`

Search page content.

```txt
intext:"api_key"
```

### Examples

```txt
intext:"secret_key"
intext:"ssh-rsa"
intext:"password"
```

Best for:

- secrets
    
- credentials
    
- sensitive strings
    

---

## Exact Match `" "`

```txt
"internal use only"
```

Find exact phrases only.

---

## Exclude Results `-`

```txt
admin -demo
```

Remove noise from searches.

---

# High-Value Dorks

## Open Directories

```txt
intitle:"index of" backup
```

---

## Git Exposure

```txt
inurl:"/.git/config"
```

---

## Database Dumps

```txt
ext:sql "INSERT INTO"
```

---

## Logs

```txt
ext:log password
```

---

## Environment Files

```txt
ext:env
```

---

# URL Parameters

## Search Parameters

```txt
inurl:"?id="
```

Common parameters:

- id=
    
- page=
    
- search=
    
- query=
    
- lang=
    
- redirect=
    
- url=
    
- callback=
    

---

## Language Parameters

```txt
inurl:"lang=en"
```

Other examples:

```txt
inurl:"locale="
inurl:"language="
```

Useful for:

- multilingual apps
    
- localization testing
    

---

## Redirect Parameters

```txt
inurl:"redirect="
```

Useful for:

- open redirect testing
    
- OAuth/auth flows
    

---

## API Discovery

```txt
inurl:api
```

### Examples

```txt
inurl:/api/v1/
inurl:swagger
inurl:graphql
```

---

# Useful Recon Combos

## Find Admin Panels

```txt
site:example.com inurl:admin
```

---

## Find PDFs

```txt
site:example.com filetype:pdf
```

---

## Find Backups

```txt
site:example.com ext:zip
site:example.com ext:bak
```

---

## Find Secrets

```txt
intext:"secret_key"
```

---

# Search Engines

|Engine|Best For|
|---|---|
|Google|Best overall indexing|
|Bing|Alternative indexed results|
|Yandex|Reverse image recon|
|Shodan|Devices / IoT / ports|
|Censys|Infrastructure mapping|
|GitHub Search|Source code + secrets|
|PublicWWW|Search inside source code|
|Wayback Machine|Historical snapshots|

---

# Best Search Engine for Books

## Best Overall: Google

Best because:

- indexes massive amounts of PDFs/EPUBs
    
- academic + public uploads
    
- strongest dork support
    

### Useful Book Dorks

```txt
filetype:pdf "machine learning"
```

```txt
filetype:pdf "python handbook"
```

```txt
site:edu filetype:pdf cryptography
```

---

## Best Academic Search

### Google Scholar

Best for:

- research papers
    
- academic books
    
- citations
    

Example:

```txt
site:scholar.google.com deep learning
```

---

## Best Shadow Library Search

### Anna’s Archive

Best for:

- books
    
- papers
    
- mirrors
    
- metadata aggregation
    

---

## Other Good Sources

|Engine|Best For|
|---|---|
|Anna’s Archive|General books|
|LibGen|Technical books|
|Z-Library|Mixed collection|
|Internet Archive|Old/scanned books|
|Project Gutenberg|Public domain books|

---

# Best Book Search Strategy

## Technical Books

```txt
filetype:pdf "linux"
```

```txt
filetype:pdf "reverse engineering"
```

---

## Academic Material

```txt
site:edu filetype:pdf
```

---

## Old/Public Domain Books

Use:

- Project Gutenberg
    
- Internet Archive
    

Best for:

- classics
    
- old manuals
    
- historical documents
    

---

# Minimal Cheat Sheet

```txt
site:
ext:
filetype:
intitle:
inurl:
intext:
"exact"
-keyword
```

---

# Language Parameters — Quick Reference

> Useful for finding multilingual pages, localized content, translations, region-specific endpoints, and testing localization.

---

# Common Language Parameters

```txt
lang=
language=
locale=
hl=
setlang=
```

---

# Basic Examples

## English

```txt
inurl:"lang=en"
```

---

## Spanish

```txt
inurl:"lang=es"
```

---

## French

```txt
inurl:"lang=fr"
```

---

## German

```txt
inurl:"lang=de"
```

---

# Locale Examples

## US English

```txt
inurl:"locale=en_US"
```

---

## Spain Spanish

```txt
inurl:"locale=es_ES"
```

---

# Google Language Parameter

## Interface Language

```txt
hl=en
hl=es
hl=fr
```

Example:

```txt
https://google.com/search?q=test&hl=es
```

---

# Combined Dorks

## Find Spanish Admin Panels

```txt
inurl:"lang=es" inurl:admin
```

---

## Find English APIs

```txt
inurl:"locale=en_US" inurl:api
```

---

## Find Localized Login Pages

```txt
inurl:"lang=de" login
```

---

# Common Language Codes

|Language|Code|
|---|---|
|English|en|
|Spanish|es|
|French|fr|
|German|de|
|Italian|it|
|Portuguese|pt|
|Russian|ru|
|Chinese|zh|
|Japanese|ja|
|Korean|ko|

---

# Useful Recon Tip

Localization often exposes:

- forgotten admin panels
    
- untranslated pages
    
- staging environments
    
- debug endpoints
    
- alternate APIs