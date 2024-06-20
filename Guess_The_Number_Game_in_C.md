
---

# Guess The Number Game in C

This is a simple console-based number guessing game written in C. The game randomly selects a secret number between 1 and 100, and the player tries to guess it within a limited number of attempts based on the chosen difficulty level.

## Features

- **Random Secret Number**: A random number between 1 and 100 is generated for each game session.
- **Difficulty Levels**: Choose from three difficulty levels with different maximum attempts:
  - Easy (12 chances)
  - Medium (9 chances)
  - Difficult (5 chances)
- **Input Validation**: Validates user input to ensure it's within the valid range (1-100).
- **Game Outcome**: Notifies the player if their guess is too high or too low and informs them when they win or lose.
- **Exit Option**: Provides an option to exit the game gracefully.

## Getting Started

### Prerequisites

- Make sure you have a C compiler installed. For example, [GCC](https://gcc.gnu.org/) on Linux or [MinGW](http://www.mingw.org/) on Windows.

### Installation and Usage

1. Clone the repository:
   ```bash
   git clone https://github.com/yourusername/Guess-The-Number-Game.git
   cd Guess-The-Number-Game
   ```

2. Compile the program:
   ```bash
   gcc main.c -o guess_number
   ```

3. Run the executable:
   ```bash
   ./guess_number
   ```

4. Follow the on-screen instructions to play the game.

## Code Overview

The main code (`main.c`) includes the game logic, random number generation, user input handling, and output messages. Below is the main structure of the code:

```c
#include <stdio.h>
#include <stdlib.h>
#include <time.h>

int main() {
    // Initialization
    int secret_num, guess, max_chances, chances_left;
    int choice;

    // Welcome message
    printf("\nWelcome to Guess The Number Game!\n");

    // Generate random number
    srand(time(0));
    secret_num = 1 + rand() % 100;

    // Difficulty level selection
    printf("Select Difficulty Level:\n");
    printf("1. Easy (12 chances)\n");
    printf("2. Medium (9 chances)\n");
    printf("3. Difficult (5 chances)\n");
    printf("4. Quit the game\n");

    scanf("%d", &choice);

    switch (choice) {
        case 1:
            max_chances = 12;
            break;
        case 2:
            max_chances = 9;
            break;
        case 3:
            max_chances = 5;
            break;
        case 4:
            printf("\nYou Have Exited the Game\n    THANK YOU!!\n");
            exit(0); // Exit the program cleanly
        default:
            printf("\nInvalid choice. Exiting the game.\n");
            exit(1); // Exit with an error code
    }

    chances_left = max_chances;

    // Game loop
    while (chances_left > 0) {
        printf("\nChances left: %d\n", chances_left);
        printf("Enter your guess (between 1 and 100): ");

        // Input validation
        if (scanf("%d", &guess) != 1) {
            printf("\nInvalid input. Please enter a number.\n");
            while (getchar() != '\n'); // Clear input buffer
            continue;
        }

        // Check if the guess is within valid range
        if (guess < 1 || guess > 100) {
            printf("\nYour guess should be between 1 and 100.\n");
            continue;
        }

        // Game logic
        if (guess == secret_num) {
            printf("\nCongratulations!!! You Won\n");
            break;
        } else if (guess < secret_num) {
            printf("Your guess is too low. Try again.\n");
        } else {
            printf("Your guess is too high. Try again.\n");
        }

        chances_left--;
    }

    // Game over message
    if (chances_left == 0) {
        printf("\nFailed!!!\nBetter Luck Next Time\nThe Secret Number was %d\n", secret_num);
    }

    return 0;
}
```

## Contribution

Contributions are welcome! If you have any ideas for improvements or find any issues, feel free to open an issue or create a pull request.

---

