# Intel-8086-Assembly-Project
University Info Centre Management System
Project Overview
This project is a comprehensive console-based management system developed in x86 Assembly Language (MASM/TASM). Designed to simulate a university information kiosk, the application integrates multiple administrative and student service modules into a single interface. It handles user authentication, resource booking, financial calculations, and billing systems using low-level memory management and DOS interrupts.

Key Features
1. Secure User Authentication
The system implements a login interface that validates user credentials before granting access to the main dashboard.


Domain Validation: Restricts access to university email addresses ending in @g.bracu.ac.bd.


Credential Parsing: Captures and stores the user's name, email, and the last three digits of their student ID for use in subsequent booking transactions.

2. Library Slot Management
A real-time booking system for university library study slots.


Slot Visualization: Displays four distinct time slots (e.g., 10:00 AM, 11:30 AM) with their current status.

Booking Engine: Allows users to book available slots. Upon booking, the slot is marked as "busy" and associated with the user's specific ID.


Cancellation: Includes logic to verify ownership before allowing users to cancel a previously booked slot.

3. Canteen Billing System
A dynamic point-of-sale (POS) module for the university canteen.


Categorized Menu: detailed sub-menus for Snacks, Main Courses, and Beverages with specific pricing.


Cart Management: Calculates subtotals based on item quantity and unit price.


Discount Logic: Features a coupon system supporting three tiers of discounts (Code A: 5%, Code B: 10%, Code C: 15%).


Payment Processing: Validates cash input against the final total and automatically calculates the change due.

4. ST (Student Tutor) Availability
A tracking system for Student Tutor (ST) sessions.


Capacity Tracking: Monitors booking ratios (e.g., 0/3) for specific tutors (Mahmuda, Shafin, Zayed).


Availability Logic: Prevents overbooking by checking current slot counts against the maximum limit before confirming a session.

5. Tuition Fee Calculator
An advanced financial module that estimates semester fees based on academic performance.

Scholarship Tiers: Automatically adjusts the "per-credit" cost based on the user's CGPA range:

3.85–4.00: 30% Waiver 

3.65–3.84: 20% Waiver 

3.50–3.64: 10% Waiver 

3.30–3.49: 5% Waiver 

Comprehensive Total: Aggregates variable course fees with fixed costs (Library Fee: 4500 BDT, Lab Fee: 10,000 BDT).

Technical Implementation
Arithmetic Handling
32-Bit Precision: The system employs DX:AX register pairing to handle large financial sums (up to tens of thousands) that exceed standard 16-bit register limits. This ensures accurate fee calculation without overflow errors.


Custom Printing Procedures: A dedicated procedure (PRINT_NUM_CORE) is implemented to convert and display multi-digit integers and 32-bit values to the console.

Control Flow

Modular Architecture: The code is structured into distinct labeled sections (e.g., LIB_FEAT, CAN_FEAT), allowing for a clean "hub-and-spoke" navigation model where users return to the main menu after completing tasks.


Input Validation: Extensive use of comparison instructions (CMP) ensures inputs for menus, IDs, and payment amounts are valid before processing.
