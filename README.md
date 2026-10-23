# Computer Networks Project

Course project for **Computer Communication Networks** at HIT (Holon Institute of Technology), group 61305-3.
By **Oriya Peretz** and **Orian Reuven**.

## What's inside

### Part 1: Packet encapsulation and capture
- `notebooks/csv_creator.ipynb` generates a CSV of simulated HTTP application-layer messages (browser ↔ web server).
- `data/group03_http_input.csv` is the generated input.
- `notebooks/traffic_simulator.ipynb` reads the CSV with Pandas, crafts IPv4/TCP packets carrying the HTTP messages with Scapy, and sends them so they can be captured and analyzed in Wireshark.
- `captures/capture1_loopback_simulation.pcapng` is the loopback capture of the simulation.

### Part 2: TCP chat server
A multi-client TCP chat server with private one-to-one conversations.

- `src/server.py` listens on port `5555`, keeps connected users in a `clients` dict (name → socket) and active conversations in a `chat_pairs` dict (socket ↔ socket).
- `src/client.py` connects to the server, picks a nickname and sends/receives messages on separate threads.

**Run:**
```bash
python src/server.py
python src/client.py   # in another terminal, set SERVER_IP in client.py first
```
In the client, type `/chat <name>` to start a private chat with a connected user.

Captures:
- `captures/capture2_chat_5_clients.zip` (+ `.z01`): five clients chatting. It's a split archive because the file is ~18 MB; download both parts and extract the `.zip` (7-Zip, or `zip -s 0 capture2_chat_5_clients.zip --out full.zip && unzip full.zip`).
- `captures/capture3_client_disconnect.pcapng`: a client disconnecting mid-chat.

## Docs
- `docs/project_report.pdf` – full project report (Hebrew)
- `docs/data_structure_definition.pdf` – server data-structure definition (Hebrew)

## Tech stack
- Python 3: `socket`, `threading`
- Scapy: packet crafting and TCP/IP encapsulation (IPv4, TCP, HTTP)
- Pandas: reading the CSV traffic scenario
- Jupyter
- Wireshark: capture and analysis (`.pcapng`)
