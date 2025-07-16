🧾 Essae Weighing Scale & Label Printer – User Space Driver (RK3568)
This project contains a user-space Linux driver for the Essae Weighing Scale and Label Printer, developed for RK3568-based embedded platforms. It includes a C-based TCP server and a Python PyQt5-based GUI client for label printing and weighing tasks.

📦 Project Structure

Essae_WSLPR_Driver_Code/
├── Essae_WSLPR_server.c       # C server code (compiles to Essae_WSLPR_server)
├── Essae_WSLPR_client.py      # Python GUI to communicate with the server
├── config.json                # Sample JSON product data
├── SQL_LFT_Files.db           # SQLite DB for LFT label templates
├── .LFT files                 # Sample label template files
└── README.md                  # This documentation
⚙️ Requirements
Server (C)
Ubuntu 22.04+

gcc

libjson-c-dev

libsqlite3-dev

Install via:


sudo apt update
sudo apt install build-essential libjson-c-dev libsqlite3-dev
Client (Python GUI)
Python 3

PyQt5

SQLite browser (optional)

Install via:

sudo apt install python3 python3-pyqt5 sqlitebrowser
pip3 install PyQt5
🔧 Build & Run
1. Build the Server

gcc Essae_WSLPR_server.c -o Essae_WSLPR_server -ljson-c -lsqlite3 -lm
2. Run Server (CLI mode)

./Essae_WSLPR_server config.json demo.LFT
3. Run as TCP Server (port 8888)

./Essae_WSLPR_server
🔁 Run as a Service
Create systemd service file:

# /etc/systemd/system/essae_server.service
[Unit]
Description=Essae WSLPR TCP Server
After=network.target

[Service]
ExecStart=/home/essae/Documents/Essae_Data/Projects/Essae_Rockchip_RK3568_Seavo/Essae_WSLPR_Driver_Code/Essae_WSLPR_server
WorkingDirectory=/home/essae/Documents/Essae_Data/Projects/Essae_Rockchip_RK3568_Seavo/Essae_WSLPR_Driver_Code
Restart=always
User=essae

[Install]
WantedBy=multi-user.target
Enable and start:

sudo systemctl daemon-reload
sudo systemctl enable essae_server.service
sudo systemctl start essae_server.service
📌 You can check logs:


journalctl -u essae_server.service --no-pager
🖥️ Run the GUI Client

python3 Essae_WSLPR_client.py
GUI Features:

📂 Load .LFT label templates into SQLite

✏️ Edit/delete label templates

📦 Browse JSON config

🔢 Select barcode index (1–99)

🖨️ Print label via TCP

⚖️ Connect to Essae scale: Tare, Zero, Read, Calibrate

📋 View logs and responses per tab

🧾 LFT Label Format Commands
The printer reads .LFT files containing label commands like:

Command	Description
~S	Set label size
~T	Fixed text
~V	Variable text from JSON
~B	Barcode
~d	Bitmap image
~R	Rectangle
~C	Circle
~I	Intensity
~P	Print page

See full documentation in docs/ or inside this repo.

🔄 Communication Protocol
The server listens on TCP port 8888. It supports 2 modes:

Printer Mode:
MODE:PRINTER
<json_path>
<slot_number>
<barcode_id 1-99>

Scale Mode:
MODE:WEIGHT
RD_WEIGHT
🗃️ Label Template Storage
Templates are saved in SQL_LFT_Files.db:


CREATE TABLE lft_files (
  slot INTEGER PRIMARY KEY,
  name TEXT UNIQUE,
  content BLOB
);
View/edit with:


sqlitebrowser SQL_LFT_Files.db
✅ Tested Features
✅ Label prints via .LFT + config.json

✅ Barcode 1–99 via GUI selection

✅ Scale weight reads via serial

✅ Calibration and tare commands

✅ Service auto-start via systemd

🧑‍💻 Author
Developed By: Venkatesh M (Essae-Teraoka)
