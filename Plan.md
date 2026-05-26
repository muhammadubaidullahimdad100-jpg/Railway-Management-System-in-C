# Project Plan: Railway Management System in C

---

## 1. Project Title

**Railway Management System**

---

## 2. Project Objective

The objective of this project is to create a simple console-based railway ticket management system using the C programming language.

The system allows users to:
- View available trains with their routes and schedules
- Book train tickets with auto-generated ticket numbers
- View all currently booked tickets
- Update passenger name or train number on an existing ticket
- Cancel a booked ticket by ticket number
- Store all ticket data persistently using file handling

This project demonstrates key programming concepts including file I/O, structured data handling, input validation, and modular function design in C.

---

## 3. Technologies Used

| Technology | Description |
|---|---|
| Programming Language | C |
| Compiler | GCC (GNU Compiler Collection) |
| Storage Method | File Handling (`fprintf`, `fscanf`) |
| Data File | `tickets.txt` |
| Temp File | `temp.txt` (used during update/cancel) |
| Interface | Console-based (terminal menu) |
| Platform | Cross-platform (Windows / Linux / Mac) |

---

## 4. Project Scope

### In Scope
- Console-based interactive menu system
- File-based persistent storage of ticket records
- Auto ticket number generation
- Input validation for train numbers
- Update and cancel operations using temp file technique

### Out of Scope
- GUI or web interface
- Database integration (e.g., MySQL)
- Online payment processing
- User login / authentication system
- Network or multi-user access

---

## 5. Main Features

| # | Feature | Description |
|---|---|---|
| 1 | View Available Trains | Displays train number, name, source, destination, and departure time |
| 2 | Book Ticket | Takes passenger name and train number, saves to file |
| 3 | Auto Ticket Number | System automatically generates a unique ticket number |
| 4 | View Booked Tickets | Reads and displays all records from `tickets.txt` |
| 5 | Update Ticket | Allows editing of passenger name and train number |
| 6 | Cancel Ticket | Removes a specific ticket record from the file |
| 7 | Input Validation | Rejects invalid train numbers with an error message |
| 8 | File Storage | All data is saved and loaded from `tickets.txt` |

---

## 6. Available Trains

| Train No | Train Name     | From | To  | Departure Time |
|----------|----------------|------|-----|----------------|
| 101      | Green Line     | KHI  | ISB | 9:00 AM        |
| 102      | Pak Express    | LHR  | KHI | 10:30 AM       |
| 103      | Jinnah Express | RWP  | KHI | 11:00 AM       |

---

## 7. Modules / Functions

| Function | Return Type | Purpose |
|---|---|---|
| `menu()` | `void` | Displays the main navigation menu |
| `viewtrain()` | `void` | Shows all available trains with details |
| `bookTicket()` | `void` | Books a new ticket and saves to file |
| `generateTicketNumber()` | `int` | Reads file and returns next available ticket number |
| `viewBookedTickets()` | `void` | Reads and prints all booked tickets from file |
| `updateticket()` | `void` | Updates passenger name or train number by ticket ID |
| `cancelticket()` | `void` | Deletes a ticket record by ticket ID |
| `main()` | `int` | Entry point — runs the menu loop with switch-case |

---

## 8. Data Storage Plan

All ticket records are stored in a plain text file:

```
tickets.txt
```

### File Format (CSV style)

Each line represents one ticket in the following format:

```
TicketNumber,PassengerName,TrainNumber
```

### Example Data

```
1,Ali Hassan,101
2,Sara Khan,103
3,Ahmed Raza,102
```

### How Update & Cancel Work

Since C does not support deleting a line from a file directly, the system uses a **temp file technique**:

```
Step 1 → Read tickets.txt line by line
Step 2 → Write all records EXCEPT the target to temp.txt
Step 3 → Delete tickets.txt
Step 4 → Rename temp.txt → tickets.txt
```

---

## 9. Program Flow

```
START
  │
  ▼
Display Menu
  │
  ├──▶ 1. View Trains       → Print hardcoded train table
  │
  ├──▶ 2. Book Ticket       → Input name + train no
  │                            → generateTicketNumber()
  │                            → Save to tickets.txt
  │
  ├──▶ 3. View Tickets      → Read and display tickets.txt
  │
  ├──▶ 4. Update Ticket     → Input ticket ID
  │                            → Find in file → Edit → Rewrite
  │
  ├──▶ 5. Cancel Ticket     → Input ticket ID
  │                            → Skip record → Rewrite file
  │
  └──▶ 6. Exit              → Print goodbye message → END
```

---

## 10. Project Structure

```
railway-management-system/
│
├── main.c           ← Full source code (all functions)
├── README.md        ← Project documentation
└── .gitignore       ← Excludes compiled files and data files
```

> `tickets.txt` and `temp.txt` are created automatically at runtime and are **not included** in the repository.

---

## 11. How to Compile & Run

### Prerequisites
- GCC compiler must be installed

### Step 1 — Compile

```bash
gcc main.c -o railway
```

### Step 2 — Run

```bash
# Linux / Mac
./railway

# Windows
railway.exe
```

---

## 12. Sample Console Output

### Main Menu
```
=======================================================
        WELCOME TO RAILWAY MANAGEMENT SYSTEM
=======================================================
1. View Available Trains
2. Book Ticket
3. View Booked Tickets
4. Update Book Tickets
5. Cancel Ticket
6. Exit
=======================================================
```

### Booking a Ticket
```
--- BOOK TRAIN TICKET ---
Generated Ticket Number: 1
Enter passenger name: Ali Hassan
Enter train number (101/102/103): 101

Ticket Booked Successfully!
===========================
 Ticket No : 1
 Name      : Ali Hassan
 Train No  : 101
===========================
```

---

## 13. Input Validation

| Input | Validation Rule |
|---|---|
| Train Number | Must be 101, 102, or 103 — loops until valid |
| Passenger Name | Accepts full name with spaces using `%[^\n]` |
| Ticket ID | Searches file — shows error if not found |
| Menu Choice | Invalid number handled by `default` in switch-case |

---

## 14. Limitations

| # | Limitation |
|---|---|
| 1 | No login or user authentication |
| 2 | Train data is hardcoded (not stored in a file) |
| 3 | No seat availability tracking |
| 4 | No date or time field in ticket booking |
| 5 | Single user only — no multi-user support |

---

## 15. Future Improvements

| # | Improvement | Priority |
|---|---|---|
| 1 | Add travel date to ticket booking | High |
| 2 | Track seat availability per train | High |
| 3 | Search ticket by passenger name | Medium |
| 4 | Admin login with password | Medium |
| 5 | Load train data from a file | Low |
| 6 | Export ticket as a formatted receipt | Low |

---


