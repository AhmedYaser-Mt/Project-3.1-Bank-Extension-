# 💳 Project 3.1 — Bank Client Management System (1st Extension)

> The same banking engine from Project 3 — now extended with a full Transactions Menu supporting Deposit, Withdraw, and Total Balance tracking.

---

## 🚀 Project Overview

This is the **first extension** of the Bank Client Management System built in C++.

The core system was already working:
clients registered, updated, deleted, and searched — all persisted in a file.

Now we add the financial layer.

A real bank terminal doesn't just manage client records.

It processes **money**.

This extension introduces a dedicated **Transactions Menu** that handles:

- Depositing funds into any account
- Withdrawing funds with balance validation
- Viewing all client balances with a total sum

No existing feature was touched.

No old code was broken.

The extension plugged in cleanly — because the base was built correctly.

---

## 🏗️ Architecture Design

The main menu now routes to a second menu:

```
Main Menu
 ├── [1] Show Client List
 ├── [2] Add New Client
 ├── [3] Delete Client
 ├── [4] Update Client Info
 ├── [5] Find Client
 ├── [6] Transactions ──► Transactions Menu
 │                         ├── [1] Deposit
 │                         ├── [2] Withdraw
 │                         ├── [3] Total Balances
 │                         └── [4] Back to Main Menu
 └── [7] Exit
```

Each screen is a single function.

Each function has one responsibility.

Navigation between menus is handled by dedicated `GoBack` functions.

---

## ⚙️ Core Functionalities

### Inherited from Project 3

| Operation | Description |
|---|---|
| 📋 Show All Clients | Display all clients in a formatted table |
| ➕ Add New Client | Register clients with full validation |
| 🗑️ Delete Client | Remove a client by account number |
| ✏️ Update Client Info | Modify existing client details |
| 🔍 Find Client | Search by account number |

### New in This Extension

| Operation | Description |
|---|---|
| 💰 Deposit | Add funds to a client's account with confirmation |
| 💸 Withdraw | Deduct funds with balance validation and confirmation |
| 📊 Total Balances | View all clients' balances + total bank balance |

---

## 🧠 Smart Design Decisions

### Withdraw reuses Deposit

Instead of writing a separate withdrawal function, withdraw passes a **negative amount** to the same deposit function:

```cpp
DepositBalanceToClientByAccountNumber(AccountNumber, Amount * -1, vClients);
```

One function handles both operations.

Less code. Less duplication. Easier maintenance.

This is Divide & Conquer thinking applied correctly.

---

### Withdraw Validation Loop

The system refuses to process a withdrawal that exceeds the available balance:

```cpp
while (Amount > Client.AccountBalance)
{
    cout << "Amount Exceeds the balance, you can withdraw up to : " << Client.AccountBalance;
    cout << "\nPlease enter another amount ? ";
    cin >> Amount;
}
```

The user is prompted again until a valid amount is entered.

No crash. No silent failure. Clean control flow.

---

### Total Balances Screen

A focused balance view — account number, name, and balance only:

```
| Account Number  | Client Name   | Balance
| A150            | Ahmed         | 9000
| A151            | Tarek         | 5000
                         Total = 14000
```

Implemented via a dedicated `PrintClientRecordBalanceLine()` function — separate from the full client record printer.

---

## 💾 Data Persistence

Same strategy as Project 3 — file-based persistence using a custom separator format.

All balance changes (deposit / withdraw) are saved to file **immediately** after confirmation.

No in-memory changes are lost.

---

## 🎯 What This Extension Teaches

- Extending an existing system without breaking anything
- Sub-menu design and navigation
- Reusing functions across different operations (deposit/withdraw)
- Input validation loops for financial operations
- Confirmation-before-action pattern
- Clean separation between display logic and business logic
- The power of Divide & Conquer when requirements grow

---

## 🛠️ Tech Stack

| | |
|---|---|
| **Language** | C++ |
| **IDE** | Visual Studio |
| **Type** | Console Application |
| **Paradigm** | Structured Programming — Divide & Conquer |
| **Storage** | Text File (File I/O) |
| **STL Used** | `vector`, `string`, `fstream`, `iomanip` |

---

## 📦 Project Versions

Each version lives in its **own dedicated repository** with its own full README.

| Version | Repo | Key Additions |
|---|---|---|
| **Bank 1** | *(separate repo)* | CRUD operations, file persistence, clean architecture |
| **Bank 1 — 1st Extension** *(you are here)* | ← this repo | Deposit, Withdraw, Total Balances |
| **Bank 1 — 2nd Extension** | *(separate repo)* | Role-based user permissions, login, input validation |

> Each extension builds directly on top of the previous version — same system, growing responsibilities.

---

## 🏁 Milestone

- ✅ First financial operations added to the banking system
- ✅ Part of **Course 7 — Algorithms & Problem Solving – Level 3**
- ✅ Proves that a well-structured base makes extensions simple and safe

---

## 🙏 Gratitude

Thank you to:

- **Programming Advices Platform**
- **Dr. Mohammed Abu-Hadhoud**

**[ https://programmingadvices.com ]**

Because clean code is not about the first version.

It is about every version that comes after.

---

## 🔥 Final Thought

This extension did not require rewriting anything.

It required understanding the base well enough to grow it correctly.

That is the real outcome of clean code and structured thinking.
