# NMAP Intelligence Console
### Advanced Network Reconnaissance & Port Intelligence Platform

## Overview

NMAP Intelligence Console is a GUI-based network reconnaissance and port intelligence platform designed to make Nmap scanning easier to operate, understand, and analyze.

The project transforms traditional command-line network scanning into an interactive graphical investigation environment. It provides target configuration, scan profiles, command previews, scan execution, structured results, service intelligence, and defensive security recommendations.

The application supports two execution modes:

- **Simulation Mode:** Demonstrates the interface using deterministic simulated scan results without sending network packets.
- **Live Nmap Mode:** Connects to a local Python backend that executes actual Nmap scans and returns structured results.

The goal is not just to identify open ports, but also to help users understand the services running on them and evaluate their potential security exposure.

---

## Key Features

### 1. Graphical Network Scanning
- User-friendly graphical scanning interface.
- Target IP address, hostname, or network input.
- Configurable port selection.
- Interactive scan controls.
- Live scan progress and status updates.

### 2. Multiple Nmap Scan Profiles

The application provides nine scan profiles:

| Profile | Purpose |
|---|---|
| Quick | Fast scan of commonly used ports |
| Common Ports | Scan the top 1,000 ports |
| Full Port Scan | Scan all TCP ports |
| Service Detection | Identify running services |
| Version Detection | Detect service versions |
| OS Detection | Attempt operating system identification |
| UDP | Scan selected UDP ports |
| Aggressive | Enable Nmap aggressive detection |
| Custom | Configure scanning options |

### 3. Advanced Scan Configuration
- Custom port ranges.
- Timing templates T0–T5.
- Service detection.
- OS detection.
- Default NSE scripts.
- Verbose output.
- Skip host discovery.
- Reverse DNS lookup.
- Output configuration.

### 4. Command Preview
- Automatically generates Nmap commands.
- Displays the exact command before execution.
- Allows command editing and copying.
- Maintains command history.

### 5. Scan Results Analysis
- Host discovery information.
- Open, closed, and filtered port counts.
- Service and version information.
- Port search, filtering, and sorting.
- Scan duration and host information.
- Visual result summaries and charts.
- Raw Nmap output inspection.

### 6. Port Intelligence System

The application includes detailed service intelligence for 16 commonly used ports:

- FTP (21)
- SSH (22)
- Telnet (23)
- SMTP (25)
- DNS (53)
- HTTP (80)
- POP3 (110)
- IMAP (143)
- HTTPS (443)
- SMB (445)
- MySQL (3306)
- RDP (3389)
- PostgreSQL (5432)
- Redis (6379)
- HTTP Alternative (8080)
- HTTPS Alternative (8443)

Each supported port includes:

- Service overview.
- Protocol information.
- How the service works.
- Protocol communication flow.
- Potential security exposure.
- Defensive recommendations.

Unknown services receive an informational fallback instead of an invented service description.

### 7. Security Intelligence

The application distinguishes between:

- **OPEN SERVICE:** A service is listening on a port.
- **POTENTIAL EXPOSURE:** A service may require security review.
- **CONFIRMED VULNERABILITY:** Requires supporting script, version, or CVE evidence; an open port alone is never sufficient.

Attention levels include Informational, Low, Medium, and High.

These levels prioritize investigation and do not represent a confirmed compromise.

### 8. Scan History and Reports
- Session-based scan history.
- Reopen previous scan results.
- Export scan information.
- Download raw scan output.
- Compare and review scan findings.

Scan history is maintained in memory and is not persisted across browser sessions.

### 9. User Interface
- Dark and light themes.
- Technical instrument-console design.
- Interactive port intelligence drawer.
- Animated protocol flow.
- Keyboard shortcuts.
- Responsive interaction and accessibility considerations.

---

## Technology Stack

### Frontend
- HTML5
- CSS3
- JavaScript
- Browser-based graphical interface

### Backend
- Python
- FastAPI
- Uvicorn
- Pydantic

### Network Scanning
- Nmap
- Nmap XML output parsing
- TCP/IP networking concepts

### Additional Components
- Python socket programming
- PyQt6 (legacy standalone scanner in Nmap2.py)

---

## Project Architecture

The application consists of three main components:

1. **Frontend:** `nmap-console.html` provides the complete graphical interface, scan configuration, simulation engine, and results visualization.
2. **Execution Backend:** `backend/main.py` validates scan requests, constructs permitted Nmap commands, executes scans, and parses XML output.
3. **Legacy Scanner:** `Nmap2.py` contains an earlier PyQt6-based TCP port scanner implementation.

The frontend and backend communicate through a local HTTP API.

---

## Installation and Setup

### Requirements

- Windows 10/11 or another supported operating system.
- Python 3.9 or newer recommended.
- Nmap installed for live scanning.
- Modern web browser.

### Step 1: Install Nmap

Download Nmap:

https://nmap.org/download.html

Alternatively, on Windows:

```powershell
winget install Insecure.Nmap
```

### Step 2: Install Python Dependencies

Open PowerShell in the backend directory:

```powershell
pip install -r requirements.txt
```

### Step 3: Start the Backend

```powershell
python main.py
```

The backend starts locally at:

```text
http://127.0.0.1:8787
```

### Step 4: Open the Application

Open the following file in your browser:

```text
nmap-console.html
```

The application automatically checks whether the local backend is available.

If the backend is unavailable, the application can operate in simulation mode.

---

## Backend API

The backend exposes the following endpoints:

| Method | Endpoint | Description |
|---|---|---|
| GET | `/` | Backend information |
| GET | `/api/health` | Backend and Nmap availability |
| POST | `/api/scan` | Execute a validated Nmap scan |

The scan endpoint returns structured host information, port results, scan duration, command information, and raw output.

---

## Security Design

Security is an important part of this project.

The backend includes:

- Target validation using Python's `ipaddress` module.
- Hostname validation.
- Private, loopback, and link-local scope restrictions by default.
- Explicit public-target authorization configuration.
- Nmap flag allowlisting.
- No shell-based command execution.
- Argument-list-based subprocess execution.
- Scan timeout enforcement.
- Single-scan concurrency control.
- Per-client cooldown.
- Temporary XML output cleanup.
- Localhost-only backend binding by default.

The backend does not accept arbitrary Nmap flags from the frontend.

---

## Learning Objectives

This project demonstrates practical understanding of:

- Network reconnaissance.
- TCP/IP networking.
- Port scanning.
- Service identification.
- Nmap command construction.
- Network security assessment.
- Python programming.
- API development.
- Frontend and backend integration.
- Secure subprocess execution.
- XML parsing.
- Security-focused interface design.

---

## Project Limitations

- Simulation mode does not perform real network scanning.
- Live scanning requires Nmap to be installed.
- Some scan types require administrator/root privileges.
- OS detection and UDP scanning may require elevated privileges.
- Service intelligence currently contains detailed entries for 16 ports.
- Scan history is not permanently stored.
- Scan results depend on network accessibility, firewall rules, and target configuration.

---

## Legal Disclaimer

This project is developed for educational purposes, network administration, and authorized security testing.

Only scan systems, devices, and networks that you own or have explicit permission to assess.

Do not use this application for unauthorized scanning, disruption, or malicious activity.

The application is designed to support responsible network reconnaissance and defensive security analysis.

---

## Future Improvements

Potential future development directions:

- Additional service intelligence entries.
- Improved network topology visualization.
- Persistent scan history.
- More report export formats.
- Enhanced host discovery.
- Additional scan analysis and comparison tools.
- More detailed service fingerprinting.

---

## Author

Drashna Parmar

Cybersecurity | Ethical Hacking | Network Security | Python Development

GitHub: 


## Project Status

Active development / Educational Project

**If you use this project, please follow the legal and authorization guidelines above.**
