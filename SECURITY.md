# Security & Hardware Safety Review Guidelines (`SECURITY.md`)

**Target:** Hardware specifications, interface pinouts (`ADMPRO`, `PIOX LVDS`), memory mapping, and deployment workflows for `adp201p4-hardware-spec`.

When reviewing Pull Requests, enforce the following security and hardware safety checks:

## 1. Sensitive Data & Intellectual Property Protection
- **No Secrets or Credentials:** Ensure no API keys, tokens, passwords, private SSH keys, or internal webhook URLs are committed in Markdown files or `.github/workflows`.
- **Proprietary & NDA Boundaries:** Flag any accidental inclusion of confidential internal schematics, restricted vendor registers, serial numbers, or unapproved internal hostnames/IPs.

## 2. Hardware & Electrical Safety in Documentation
- **Voltage & Polarity Warnings:** Verify that any changes to power rails, `PIOX LVDS` pinouts, or `ADMPRO` debug interfaces do not introduce conflicting voltage levels or omit critical ESD / overvoltage protection warnings.
- **Debug Interface Exposure (`ADMPRO`):** Check that documentation for debug/JTAG/ADM interfaces clearly specifies access restrictions or production lock mechanisms where applicable.

## 3. CI/CD & GitHub Pages Workflow Security (`.github/workflows`)
- **Action Pinning & Permissions:** Ensure GitHub Actions workflows follow the principle of least privilege (`permissions: contents: read`) and do not expose write tokens to untrusted pull requests.
- **Script Injection:** Flag any unescaped user inputs or external variables inside workflow shell commands.

## 4. Reporting Security Issues
- If you discover a security vulnerability or a critical hardware safety error in this specification, please open a private security advisory or contact the repository maintainer (`@ekatmoz88-alt`) directly before public disclosure.
