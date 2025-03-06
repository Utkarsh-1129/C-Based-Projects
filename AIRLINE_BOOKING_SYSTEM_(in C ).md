
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
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <windows.h>

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

struct book *begin = NULL;
int seat_number = 1;

void getInput(struct book *current) {
    printf("Enter Passport Number: ");
    scanf("%s", current->passport);
    printf("Enter Name: ");
    scanf("%s", current->name);
    printf("Enter Departure Location: ");
    scanf("%s", current->departure);
    printf("Enter Destination: ");
    scanf("%s", current->destination);
    printf("Enter Departure Date (YYYY-MM-DD): ");
    scanf("%s", current->depart_Date);
    printf("Enter Email: ");
    scanf("%s", current->email);
    current->seat_num = seat_number++;
}

void reserve() {
    struct book *newNode = (struct book *)malloc(sizeof(struct book));
    getInput(newNode);
    newNode->following = begin;
    begin = newNode;
    printf("\nReservation Successful! Your Seat Number is: %d\n", newNode->seat_num);
}

void display() {
    struct book *temp = begin;
    if (!temp) {
        printf("No reservations found.\n");
        return;
    }
    printf("\nCurrent Reservations:\n");
    while (temp) {
        printf("\nName: %s, Passport: %s, From: %s, To: %s, Date: %s, Seat No: %d, Email: %s\n",
               temp->name, temp->passport, temp->departure, temp->destination, temp->depart_Date, temp->seat_num, temp->email);
        temp = temp->following;
    }
}

void cancel() {
    char pass[10];
    printf("Enter Passport Number to Cancel: ");
    scanf("%s", pass);
    struct book *temp = begin, *prev = NULL;
    while (temp) {
        if (strcmp(temp->passport, pass) == 0) {
            if (prev) {
                prev->following = temp->following;
            } else {
                begin = temp->following;
            }
            free(temp);
            printf("\nReservation Cancelled Successfully.\n");
            return;
        }
        prev = temp;
        temp = temp->following;
    }
    printf("\nNo matching reservation found.\n");
}

void saveToFile() {
    FILE *fp = fopen("reservations.txt", "w");
    if (!fp) {
        printf("\nError saving reservations!\n");
        return;
    }
    struct book *temp = begin;
    while (temp) {
        fprintf(fp, "%s %s %s %s %s %d %s\n", temp->passport, temp->name, temp->departure, temp->destination, temp->depart_Date, temp->seat_num, temp->email);
        temp = temp->following;
    }
    fclose(fp);
    printf("\nReservations Saved Successfully!\n");
}

int main() {
    int choice;
    do {
        printf("\n\tUT's Airline Reservation System\n");
        printf("1. RESERVATION\n2. CANCEL\n3. DISPLAY RECORDS\n4. EXIT\n");
        printf("Enter your choice: ");
        scanf("%d", &choice);

        switch (choice) {
            case 1:
                reserve();
                break;
            case 2:
                cancel();
                break;
            case 3:
                display();
                break;
            case 4:
                saveToFile();
                printf("Exiting...\n");
                break;
            default:
                printf("Invalid Choice!\n");
        }
    } while (choice != 4);
    return 0;
}

```

## Contributing

Contributions are welcome! Please feel free to submit a pull request or open an issue with any suggestions or improvements.
```
