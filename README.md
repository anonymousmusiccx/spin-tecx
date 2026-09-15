# Spin Tecx Scan

A Termux CLI tool that checks a website's reputation using the [VirusTotal](https://www.virustotal.com) API.

```
   ▄▄▄▄▄▄▄▄▄▄▄  ▄▄▄▄▄▄▄▄▄▄▄  ▄▄▄▄▄▄▄▄▄▄▄  ▄▄       ▄▄
  ▐░░░░░░░░░░░▌▐░░░░░░░░░░░▌▐░░░░░░░░░░░▌▐░░▌     ▐░░▌
   SPIN TECX — url reputation scanner
```

## What it does

Submits a URL to VirusTotal, polls for the multi-vendor analysis, and prints a clean/suspicious/malicious verdict straight to the terminal — no logs, no dashboard, just a fast answer.

## Requirements

- [Termux](https://termux.dev) on Android (or any Linux shell with bash)
- `curl`
- `jq`
- A free VirusTotal API key: https://www.virustotal.com/gui/join-us

## Install

```bash
pkg install curl jq          # Termux; use your distro's package manager elsewhere
git clone https://github.com/<your-username>/spintecx-scan.git
cd spintecx-scan
chmod +x spintecx-scan
mv spintecx-scan $PREFIX/bin/        # Termux
# or: sudo mv spintecx-scan /usr/local/bin/   # regular Linux
```

**Before running any script from GitHub, open it and read it first.** This one is plain bash — open `spintecx-scan` in a text editor and check it does what this README says before you `chmod +x` and run it. That habit matters more than this specific script.

## Usage

```bash
spintecx-scan example.com
spintecx-scan https://example.com
```

First run asks for your VirusTotal API key and saves it to `~/.spintecx/config` (permissions locked to your user only).

## Output

- Verdict: CLEAN / SUSPICIOUS / MALICIOUS
- Vendor breakdown: malicious / suspicious / harmless / undetected counts
- Link to the full VirusTotal report

## Exit codes

| Code | Meaning |
|---|---|
| 0 | Clean |
| 1 | Malicious |
| 2 | Suspicious |

Useful for chaining into other scripts (`spintecx-scan "$url" || alert-something`).

## Limitations

VirusTotal's free public API is capped at **4 requests per minute**. Fine for manual, one-off checks; not built for scanning URLs in a loop.

## License

MIT
