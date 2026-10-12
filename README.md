# University Information Centre — x86 Assembly

A console-based university information management system written entirely in 16-bit x86 Assembly (MASM/TASM) for the MS-DOS environment. The project simulates an interactive campus information kiosk, demonstrating low-level memory management, DOS interrupt handling, arithmetic beyond 16-bit register limits, and structured control flow without high-level programming language abstractions.

---

## Technical Highlights

- **Pure x86 Assembly**: Implemented completely in assembly without runtime libraries or high-level abstractions.
- **Direct DOS Interrupt Handling**: Relies directly on MS-DOS services (`INT 21h`) for character and string I/O (`AH=01h`, `AH=02h`, `AH=09h`) and process termination (`AH=4Ch`).
- **Low-Level Memory Management & Addressing**: Implements manual pointer manipulation and indexed addressing using CPU registers (`SI`, `DI`, `BX`, `BP`) to manage data arrays, strings, and multi-record state.
- **Extended Precision (32-Bit) Arithmetic**: Handles large numeric calculations (such as semester tuition totals) exceeding 16-bit limits by pairing the `DX:AX` registers, preserving high-order words across multiplication (`MUL`) and division (`DIV`), and propagating carry flags (`ADC`).
- **Custom Base-10 Stack Conversion**: Features a custom output routine (`PRINT_NUM_CORE`) that dynamically converts binary numeric values to ASCII digits using successive division by 10 and the hardware stack (`PUSH`/`POP`) before rendering to the console.
- **Modular Control Flow**: Built around a centralized hub-and-spoke dispatch loop (`HUB`) with label-based subroutine jumps, maintaining structured program flow and stack hygiene.

---

## Core Modules

### 1. Secure User Authentication
- **Domain Validation**: Restricts access to authorized university email accounts ending in `@g.bracu.ac.bd` using indexed string comparisons.
- **Credential Parsing**: Extracts user name, email, and the student's 3-digit ID suffix, storing them in memory buffers for session personalization and booking association.

### 2. Library Slot Management
- **Real-Time Booking Engine**: Tracks availability across 4 distinct study slots (10:00 AM, 11:30 AM, 1:00 PM, 2:30 PM).
- **Slot Visualization**: Displays live availability status and associates reserved slots with the booking student's ID.
- **Ownership Verification**: Validates slot occupancy and prevents cancellation of unreserved or unauthorized slots.

### 3. Canteen Point-of-Sale (POS) System
- **Categorized Menu**: Supports multiple categories (Snacks, Main Courses, Beverages) with individual unit pricing.
- **Cart Management**: Accumulates item quantities and computes running sub-totals dynamically.
- **Discount & Coupon System**: Implements coupon voucher validation across three tiers (Code A: 5%, Code B: 10%, Code C: 15%) using fixed-point integer arithmetic.
- **Payment Processing**: Verifies submitted cash amounts against the final total, prompting for additional cash if insufficient and calculating accurate change.

### 4. Student Tutor (ST) Availability Tracker
- **Capacity Tracking**: Monitors reservation counts (up to 3 students per tutor) for peer tutoring consultations (Mahmuda, Shafin, Zayed).
- **Overbooking Prevention**: Evaluates capacity boundaries prior to incrementing booking counters, preventing oversaturation of available slots.

### 5. Tuition Fee Calculator
- **Merit-Based Scholarship Waiver**: Evaluates academic CGPA against institutional scholarship tiers (30%, 20%, 10%, 5%) to adjust per-credit tuition rates.
- **Comprehensive Cost Aggregation**: Computes variable credit fees alongside fixed semester charges (Library Fee: 4,500 BDT, Lab Fee: 10,000 BDT).
- **32-Bit Precision**: Leverages `DX:AX` register pairing to prevent integer overflow during multi-course tuition summation.

---

## Source File Notice

The complete application source code is contained in:
- `Univeristy Information Centre.txt`

> **Note**: The source code is written in pure 16-bit x86 Assembly (`.asm`). For compilation with MASM or TASM, rename or copy this file with a `.asm` extension (e.g., `uic.asm` or `university_info_centre.asm`).

---

## How to Run

### Prerequisites
- [DOSBox](https://www.dosbox.com/) (or DOSBox-Staging / DOSBox-X)
- Turbo Assembler (**TASM**) & Turbo Linker (**TLINK**), or Microsoft Macro Assembler (**MASM**) & **LINK**

### Step-by-Step Instructions

1. **Prepare the Source File**:
   Copy or rename the file to an 8.3 DOS-compatible filename in your working folder:
   ```bash
   copy "Univeristy Information Centre.txt" UIC.ASM
   ```

2. **Mount and Open DOSBox**:
   ```text
   Z:\> mount c C:\dos_projects
   Z:\> c:
   ```

3. **Assemble and Link with TASM**:
   ```text
   C:\> tasm uic.asm
   C:\> tlink uic.obj
   C:\> uic.exe
   ```

4. **Alternative: Assemble and Link with MASM**:
   ```text
   C:\> masm uic.asm;
   C:\> link uic.obj;
   C:\> uic.exe
   ```

---

## Technical Specifications

| Parameter | Specification |
| :--- | :--- |
| **Architecture** | Intel 8086 / x86 (16-bit Real Mode) |
| **Assembler** | MASM / TASM (`.MODEL SMALL`) |
| **Runtime Environment** | MS-DOS / DOSBox |
| **Stack Allocation** | 256 bytes (`.STACK 100H`) |
| **System Calls** | MS-DOS Interrupt 21h (`AH=01h`, `AH=02h`, `AH=09h`, `AH=4Ch`) |
| **Registers Utilized** | AX, BX, CX, DX, SI, DI, BP, SP, DS, CS, SS |

---

## Built With

- **x86 Assembly** (Intel 8086 Instruction Set)
- **MASM / TASM** (Assembler & Linker)
- **MS-DOS / DOSBox** (Execution Environment)

---

## License

This project is licensed under the MIT License — see the [LICENSE](LICENSE) file for details.
