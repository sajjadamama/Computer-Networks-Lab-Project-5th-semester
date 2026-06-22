# 🏫 NU-Information Exchange System

**Course:** CS3001 – Computer Networks · Fall 2025
**Instructor:** Dr. Ammar Rafiq & Ms Alisha Abid
**Members:** Amama Sajjad (23F-6014) · Kainat Zahra (23F-0713) · Mehreen Fatima (23F-0611)
**University:** NUCES, Department of Computer Science

---

## Overview

A two-part project simulating inter-campus communication across FAST-NUCES campuses:

- **Part 1** — A multi-client communication system built in C/C++ using socket programming
- **Part 2** — A multi-campus WAN topology designed in Cisco Packet Tracer

---

## Part 1 — Application (C/C++ Socket Programming)

### Architecture

- **Central Server** (Islamabad) — Acts as the hub; manages all campus client connections
- **Campus Clients** (Lahore, Karachi, Peshawar, CFD, Multan) — Connect to the central server and represent local campuses
- **Department Users** — Simulated via console: Admissions, Academics, IT, Sports

### Protocol Design

| Protocol | Used For |
|---|---|
| **TCP** | Campus authentication, direct campus-to-campus messages, admin commands |
| **UDP** | Periodic heartbeat/status from clients, server-wide broadcast announcements |

### How to Compile & Run

**Linux / macOS (g++):**
```bash
# Compile server
g++ -std=c++17 -pthread -o server server.cpp

# Compile client
g++ -std=c++17 -pthread -o client client.cpp

# Run server first
./server

# Run each campus client in a separate terminal
./client
```

**Windows (MinGW):**
```bash
g++ -std=c++17 -o server.exe server.cpp -lws2_32
g++ -std=c++17 -o client.exe client.cpp -lws2_32
```

### Usage

On the campus client console:
```
Press 1 to send a message
Press 2 to view received messages
Press 3 to exit

# Send message format:
send <TargetCampus> <TargetDept> <Message>
# Example:
send Karachi Admissions "Please send admission stats"
```

### Campus Credentials (hard-coded)

| Campus | Credential |
|---|---|
| Lahore | `Campus:Lahore,Pass:NU-LHR-123` |
| Karachi | `Campus:Karachi,Pass:NU-KHI-123` |
| Peshawar | `Campus:Peshawar,Pass:NU-PSW-123` |
| CFD | `Campus:CFD,Pass:NU-CFD-123` |
| Multan | `Campus:Multan,Pass:NU-MUL-123` |

---

## Part 2 — Network Architecture (Cisco Packet Tracer)

### File
`CN_Course_Project.pkt` — Open with Cisco Packet Tracer 8.x or later

### Topology

4+ FAST-NUCES campus LANs connected via a WAN. Each campus has:
- 1 Router (Cisco 2911)
- 1 Switch (Cisco 2960)
- 2+ Department PCs (PC-Admissions, PC-Academics)

### IP Addressing

| Campus | LAN Subnet |
|---|---|
| Islamabad | 192.168.10.0/24 |
| Lahore | 192.168.20.0/24 |
| Karachi | 192.168.30.0/24 |
| Peshawar | 192.168.40.0/24 |

WAN links between routers use /30 point-to-point subnets.

### Routing

**RIP** dynamic routing configured on all routers for full end-to-end connectivity.

**Verify connectivity:**
```bash
ping <destination-IP>   # From any PC to any other campus PC
```

---

## Project Structure

```
CN_Project/
├── server.cpp          # Central server (TCP + UDP listener, routing, admin)
├── client.cpp          # Campus client (TCP auth, UDP heartbeat, console menu)
├── CN_Course_Project.pkt   # Cisco Packet Tracer topology
└── report.pdf          # Technical report with screenshots and IP table
```

---

## Deliverables

- Fully commented C/C++ source code for server and client

