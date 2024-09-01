#include <stdio.h>
#include <stdlib.h>
#include <ctype.h>
#include <string.h>

// Function to calculate the area of a triangle
float calculateArea(float base, float height) {
    printf("\nStep 3: Calculating the area of the triangle...\n");
    float area = (base * height) / 2;
    printf("Formula used: Area = (base * height) / 2\n");
    printf("Calculation: Area = (%.2f * %.2f) / 2\n", base, height);
    return area;
}

// Function to validate numeric input
float getValidFloat(const char* prompt) {
    char input[100];
    float value;
    int isValid = 0;

    while (!isValid) {
        printf("%s", prompt);
        scanf("%s", input);

        // Check if input is a valid float
        isValid = 1;
        for (int i = 0; i < strlen(input); i++) {
            if (!isdigit(input[i]) && input[i] != '.' && input[i] != '-') {
                isValid = 0;
                break;
            }
        }

        if (isValid) {
            value = atof(input);
        } else {
            printf("Invalid input! Please enter a valid number.\n");
        }
    }

    return value;
}

// Function to convert height to meters based on unit
float convertToMeters(float height, int unit) {
    printf("\nStep 2: Converting height to meters based on the selected unit...\n");
    switch (unit) {
        case 1: 
            printf("Height in meters: %.2f\n", height);
            return height;               // Meters
        case 2: 
            printf("Height in centimeters: %.2f. Converting to meters...\n", height);
            return height / 100.0;       // Centimeters to meters
        case 3: 
            printf("Height in feet: %.2f. Converting to meters...\n", height);
            return height * 0.3048;      // Feet to meters
        default: 
            return height;
    }
}

int main() {
    float base, height, area;
    int unit;

    // Welcome message
    printf("=====================================\n");
    printf("   Triangle Area Calculator Program  \n");
    printf("=====================================\n\n");

    // Step 1: Get valid base input
    printf("Step 1: Getting input for the base of the triangle.\n");
    base = getValidFloat("Enter the base of the triangle (in units): ");

    // Step 1: Get valid height input
    printf("\nStep 1: Getting input for the height of the triangle.\n");
    height = getValidFloat("Enter the height of the triangle (in units): ");

    // Select unit for height
    printf("\nSelect the unit for height:\n");
    printf("1. Meters\n");
    printf("2. Centimeters\n");
    printf("3. Feet\n");
    printf("Enter your choice (1/2/3): ");
    scanf("%d", &unit);

    // Convert height to meters
    height = convertToMeters(height, unit);

    // Calculate the area
    area = calculateArea(base, height);

    // Step 4: Display the result in ASCII style
    printf("\nStep 4: Displaying the calculated area in ASCII style.\n");
    printf("-------------------------------------\n");
    printf("The area of the triangle is: \n\n");

    // ASCII Art for the area
    printf("  ___ ___                   _       _ \n");
    printf(" /   |   \\  _   _ _ __  ___| |_ ___| |\n");
    printf("/ /| | |  || | | | '_ \\/ __| __/ _ \\ |\n");
    printf("/ / | | | || |_| | | | \\__ \\ ||  __/ |\n");
    printf("\\/  |_| |_| \\__,_|_| |_|___/\\__\\___|_|\n\n");
    printf("                %.2f square meters\n", area);
    printf("-------------------------------------\n");

    return 0;
}
