# Parking Slot Management System

A menu-driven **16-bit x86 Assembly** project for managing vehicle records, parking slots, and parking fees. Developed for **CSE341**, it demonstrates array-based storage, procedures, macros, register operations, and DOS interrupt services.

## Features

- Register a vehicle with an owner name and parking slot.
- Automatically assign a numeric vehicle ID.
- Update an owner's name, parking slot, or vehicle status.
- Search for a vehicle and display its details.
- Calculate a parking fee from a manually entered duration.
- Remove a vehicle, compact the remaining records, and renumber IDs.
- Check the current record count against a maximum capacity of 10.
- Return to the main menu after each operation.

## Menu

| Key | Action |
| --- | --- |
| `1` | Register a new vehicle |
| `2` | Update vehicle information |
| `3` | Search for a vehicle |
| `4` | Calculate the parking fee |
| `5` | Remove a vehicle |
| `6` | Run the parking capacity check |
| `0` | Exit |

## Technologies and concepts

- 16-bit x86 Assembly with MASM-style directives, including `.MODEL SMALL`.
- DOS `INT 21h` services for character input, text output, and termination.
- Parallel arrays for vehicle IDs, owner names, parking slots, and statuses.
- Procedures called using `CALL` and returned from using `RET`.
- Macros for repeated input, output, and record operations.
- Array indexing, loops, conditional jumps, ASCII conversion, and integer arithmetic.

## Source file

The supplied source is:

`Parking_Slot_Management_System_CSE341_menu_fixed_v3_updated.txt`

For a clean repository, save an identical copy as **`parking_slot_management.asm`** and place this README beside it. The `.asm` filename identifies the file as Assembly source; changing the extension does not change the code.

## Running the project

1. Download `parking_slot_management.asm`, or rename the supplied `.txt` source to that name. Ensure the file does not retain a hidden `.txt` extension.
2. Open it in the 16-bit x86 assembler/emulator used for the course. The environment must support the source's MASM-style macros and DOS `INT 21h` calls.
3. Assemble the source and run it in that environment's DOS-compatible execution mode.
4. Use the number keys shown in the menu to select an operation.
5. Exit using `0`.

The source is not a native modern Windows or Linux program. Assembly and execution have not been independently verified for a specific toolchain in this repository; use the original course environment as the starting point.

## Input guide

| Input | Expected value |
| --- | --- |
| Menu selection | A single key: `0`–`6` |
| Vehicle ID | An existing single-digit record ID: `0`–`9` |
| Owner name | Short text terminated by a backslash: `\` |
| Parking slot | Short text terminated by a backslash: `\` |
| Status update | `1` for Parked; `2` for Available |
| Parking duration | A single digit from `1` to `9` hours |

The same backslash terminator is used for owner and slot input, even though the slot prompt does not display that instruction. Menu choices, IDs, and durations use single-character input; an Enter key is not required by those input routines.

The arrays reserve 20 bytes per text field, including storage needed for the DOS string terminator. Keep owner names and slot labels below the advertised 20-character limit—**19 characters or fewer**—and finish with a backslash. The original routines need stronger boundary handling before accepting arbitrary input.

## Parking fee

The rate is fixed at **10 Taka per hour**:

```text
Parking fee = entered hours × 10 Taka
```

For example, entering `3` hours produces a fee of **30 Taka**. The program accepts durations from 1 to 9 hours. It does not measure elapsed time automatically or record a completed payment.

## Record storage

| Array or variable | Purpose |
| --- | --- |
| `VEHICLE_ID` | Up to 10 vehicle IDs |
| `VEHICLE_OWNER` | Owner names in 20-byte record segments |
| `PARKING_SLOT` | Slot labels in 20-byte record segments |
| `VEHICLE_STATUS` | Parked or Available status strings |
| `GLOBAL_INDEX` | Number of registered records |
| `MAX_CAPACITY` | Maximum record capacity: 10 |

Records are stored in memory for the current session. Deleting a record shifts later records left and renumbers the remaining IDs, so IDs are not permanent identifiers.

The capacity check uses the number of registered records. Changing a status to **Available** does not remove the record or reduce the capacity count; use the removal option to free a record position.

## Example demonstration

1. Choose `1` and enter a short owner name followed by `\`.
2. Enter a slot label such as `A1`, followed by `\`.
3. For the first vehicle in a fresh session, choose `3` and search for ID `0`.
4. Choose `4`, enter ID `0`, and enter `3` hours to calculate 30 Taka.
5. Choose `2` to update that record.
6. Choose `6` to display the capacity count.
7. Choose `5` and remove ID `0`.
8. Choose `0` to exit.

This is a suggested manual demonstration, not a record of an independently executed test.

## Scope and limitations

- Academic console prototype with a maximum of 10 records.
- Data is lost when the program exits; no file or database persistence is implemented.
- Parking slot labels are entered manually; duplicate slot assignments are not checked.
- Vehicle IDs change after deletion and compaction.
- Fee calculation uses manual whole-hour input and a fixed rate.
- Input validation and buffer handling should be improved before extending the program.

## Academic context

The source divides six features across three member roles:

| Role | Assigned features |
| --- | --- |
| Member 1 | Register vehicles and update information |
| Member 2 | Search vehicles and calculate fees |
| Member 3 | Remove vehicles and check capacity |

The supplied code does not name the contributors. This README preserves the documented role allocation without assigning names or individual credit.
