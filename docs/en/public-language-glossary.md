# Public Language Glossary

Use this page when writing or reviewing public VaultPilot documentation. It keeps English and Turkish wording consistent without turning operator docs into marketing copy.

## English Style

- Say **VaultPilot** for the current product.
- Say **PassMan** only for legacy compatibility context, older installed services, data paths, headers, cookies, update aliases, protocol strings, or historical releases.
- Prefer direct operator language: install, verify, review, rotate, revoke, back up, restore, collect, redact.
- Avoid implying that this public repository contains product source code, release binaries, signing material, customer data, databases, or backups.

## Turkish Public Wording

| English source term | Preferred Turkish public wording | Notes |
| --- | --- | --- |
| public repository | public repo or public dokümantasyon reposu | Keep `public repo` when it is the repository boundary term. |
| release | release or yayın | Use `release` for GitHub Release names; use `yayın` in plain sentences when it reads naturally. |
| support | destek | Avoid `support` unless it is part of a product surface or channel name. |
| screenshot | ekran görüntüsü | Use `sanitize edilmiş UI görseli` when explaining public screenshots. |
| private source | private kaynak kod | Make clear that source code is not published here. |
| signing material | imza materyali | Use `private signing material` only when the security boundary needs the exact term. |
| artifact | artifact or çıktı | Use `release artifact` for GitHub Release assets; use `çıktı` for ordinary generated files. |
| placeholder | placeholder | Accepted technical term; pair with examples such as `<SERVER_HOST>`. |
| redacted | redakte edilmiş | Use this for safe public evidence. |
| issue | issue | Accepted GitHub term; write `public issue` for public intake. |
| evidence | kanıt | Use `kanıt paketi` for support evidence packs. |
| token | token | Keep as technical term. |
| endpoint | endpoint | Keep as technical API term. |
| client | client | Keep for API/client software contexts. |

## Cross-Language Rules

- Do not translate product names, asset names, package names, command flags, endpoint paths, or placeholder tokens.
- Keep Turkish docs natural but operator-focused. A short Turkish sentence is better than a literal English translation.
- Use English technical words only when they are the actual UI/API term or a common operator term in this product.
- When wording changes a safety boundary, update the paired English and Turkish pages together.

Related:

- [Public repository boundary](public-repository-boundary.md)
- [GitHub repository profile](github-repository-profile.md)
- [Support evidence pack](support-evidence-pack.md)
- [Turkish documentation home](../tr/README.md)
