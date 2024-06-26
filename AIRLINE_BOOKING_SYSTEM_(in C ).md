
# UT's Airline Reservation System (C-Based):

UT's Airline Reservation System is a console-based application written in C, designed to manage airline reservations. The system allows users to reserve seats, cancel reservations, and display booking records. It uses a linked list to manage bookings and ensures data persistence by saving records to a file.

## Features

- **Reservation**: Book a seat by entering personal and travel details.
- **Cancellation**: Cancel an existing booking using the passport number.
- **Display Records**: View all current reservations.
- **Data Persistence**: Save and load reservation records from a file.

## Getting Started

### Prerequisites

- GCC Compiler (for compiling the C program)
- Windows OS (since the program uses `windows.h`)

### Installation

1. **Clone the repository**:
   ```sh
   git clone https://github.com/yourusername/AirlineReservationSystem.git
   cd AirlineReservationSystem
   ```

2. **Compile the program**:
   ```sh
   gcc main.c -o AirlineReservationSystem.exe
   ```

3. **Run the program**:
   ```sh
   .\AirlineReservationSystem.exe
   ```

## Usage

1. **Reservation**: Follow the prompts to enter your booking details.
2. **Cancellation**: Enter the passport number associated with the booking you wish to cancel.
3. **Display Records**: View all current reservations.
4. **Exit**: Save all records to a file and exit the program.

## Code Overview

The system is implemented using a linked list to manage bookings. Below are the main components and functions:

### Structure

```c
struct book {
    char passport[10];
    char name[20];
    char departure[15];
    char destination[15];
    char depart_Date[11];
    int seat_num;
    char email[30];
    struct book *following;
};
```

### Global Variables

- `struct book *begin = NULL;` - Pointer to the start of the linked list of bookings.
- `struct book *stream = NULL;` - Pointer used for traversing the linked list.

### Functions

#### `void reserve(int x)`

Reserves a seat for a new booking.

#### `void getInput(struct book *current)`

Prompts the user for booking details.

#### `void display()`

Displays all current reservations.

#### `void cancel()`

Cancels an existing reservation.

#### `void saveToFile()`

Saves the reservation records to a file.

### Main Function

The main function provides a menu for users to choose between reservation, cancellation, displaying records, and exiting the program.

```c
int main() {
    int choice;
    int num = 1;

    do {
        // Display menu
        printf("\n\t\t\t\t   ================================================================");
        printf("\n\t\t\t\t   ||>>>            WELCOME TO UT's AIRLINE SYSTEM            <<<||");
        printf("\n\t\t\t\t   ================================================================");
        printf("\n\n\t\t Please enter your choice from [1 to 4] below:");
        printf("\n\n\t\t 1. RESERVATION");
        printf("\n\t\t 2. CANCEL");
        printf("\n\t\t 3. DISPLAY RECORDS");
        printf("\n\t\t 4. EXIT");
        printf("\n\n\t\t Enter your choice: ");
        scanf("%d", &choice);
        fflush(stdin);

        switch (choice) {
            case 1:
                reserve(num);
                num++;
                break;

            case 2:
                cancel();
                break;

            case 3:
                display();
                break;

            case 4:
                saveToFile();
                break;

            default:
                printf("\n\n\t\t SORRY INVALID CHOICE!");
                printf("\n\t\t PLEASE CHOOSE FROM 1-4");
        }
    } while (choice != 4);

    return 0;
}
```

## Contributing

Contributions are welcome! Please feel free to submit a pull request or open an issue with any suggestions or improvements.
```

This Markdown document provides a structured overview of your Airline Reservation System repository, including installation instructions, usage guidelines, code overview, and contribution details. Adjust the GitHub repository link (`https://github.com/yourusername/AirlineReservationSystem.git`) to your actual repository URL when publishing.
