# 🧾 Essae Weighing Scale & Label Printer – User Space Driver (RK3568)

This project contains a user-space Linux driver for the **Essae Weighing Scale** and **Label Printer**, developed for **RK3568-based embedded platforms**. It includes a **C-based TCP server** and a **Python PyQt5-based GUI client** for label printing and weighing tasks.

---

## 📦 Project Structure

Essae_WSLPR_Driver_Code/
├── Essae_WSLPR_server.c # C TCP server (builds to Essae_WSLPR_server)
├── Essae_WSLPR_client.py # Python PyQt5 GUI client
├── config.json # Sample product data
├── SQL_LFT_Files.db # SQLite DB to store .LFT templates
├── *.LFT # Sample label template files
└── README.md # This documentation


---

## ⚙️ Requirements

### 🖥 Server (C code)
- Ubuntu 22.04+
- GCC
- JSON-C
- SQLite3

Install:

sudo apt update
sudo apt install build-essential libjson-c-dev libsqlite3-dev
💻 Client (Python GUI)
Python 3

PyQt5

SQLite browser (optional for DB viewing)

Install:


sudo apt install python3 python3-pyqt5 sqlitebrowser
pip3 install PyQt5
🔧 Build & Run
1. Build the server

gcc Essae_WSLPR_server.c -o Essae_WSLPR_server -ljson-c -lsqlite3 -lm
2. Run server in CLI mode

./Essae_WSLPR_server config.json demo.LFT
3. Run server in TCP mode (port 8888)

./Essae_WSLPR_server
4. Run the GUI client

python3 Essae_WSLPR_client.py
🖥 GUI Features
📂 Add/Edit/Delete .LFT label files to SQLite

🔢 Select barcode data (1–99) from JSON

🖨️ Print label via TCP

⚖️ Scale operations:

Read weight

Tare / Zero / Restart

Full calibration workflow

Read/write technical & custom specs

📋 Logs and responses displayed in tabs

💾 Uses SQL_LFT_Files.db with table:


CREATE TABLE lft_files (
  slot INTEGER PRIMARY KEY,
  name TEXT UNIQUE,
  content BLOB
);
🔄 Communication Protocol (Port 8888)
Printer Mode

MODE:PRINTER
/path/to/config.json
<lft_slot_number>
<barcode_entry_number>
Scale Mode
makefile

MODE:WEIGHT
RD_WEIGHT
🧾 LFT Label Format Commands
The .LFT files sent to the printer contain commands like:

Command	Description
~S	Set label size
~T	Fixed text
~V	Variable text from JSON
~B	Barcode from JSON
~d	Bitmap image
~R	Draw rectangle
~C	Draw circle
~I	Set print intensity (100–140)
~P	Print label

💡 Full label language details: Label Report Description Language (R2)

✅ Tested Features
✅ Prints labels using .LFT + config.json

✅ Barcode entry selection (1–99)

✅ Weighing scale reads + calibration

✅ TCP communication with client & server

✅ SQLite-based template storage

✅ PyQt5 GUI with connection/status logging


🧑‍💻 Author
Developed By: Venkatesh M (Essae-Teraoka)

📎 Notes
Use sqlitebrowser SQL_LFT_Files.db to browse label templates.

Make sure both server and client are in the same network or localhost.

GUI will disable actions unless connected to the server at port 8888.

