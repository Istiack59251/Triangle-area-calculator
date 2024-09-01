#include <stdio.h>
#include <stdlib.h>
#include <math.h>
#include <string.h>
#include <ctype.h>

// Function declarations
float getLengthOrHeight(const char* prompt);
int getUnit(const char* prompt);
float convertLength(float length, int fromUnit, int toUnit);
float convertArea(float metersSquared, int toUnit);
float areaBaseHeight(float base, float height);
float areaHeron(float a, float b, float c);
float areaSAS(float a, float b, float angle);
float areaCoordinates(float x1, float y1, float x2, float y2, float x3, float y3);
float areaDeterminant(float x1, float y1, float x2, float y2, float x3, float y3);
float degreesToRadians(float degrees);

int main() {
    int method, baseUnit, heightUnit, unit;
    float base, height, sideA, sideB, angle, a, b, c, x1, y1, x2, y2, x3, y3;
    char recalculate;

    do {
        printf("\n*****************************************\n");
        printf("*      ISTIACK'S TRIANGLE AREA CALCULATOR\n");
        printf("*****************************************\n");

        // Method selection
        printf("\nSelect method to calculate area:\n");
        printf("[1] Base and Height: Use this method if you have the base and height of the triangle.\n");
        printf("[2] Heron's Formula: Use this method if you know all three sides of the triangle.\n");
        printf("[3] Side-Angle-Side (SAS): Use this method if you have two sides and the included angle.\n");
        printf("[4] Coordinates Formula: Use this method if you have the coordinates of the triangle's vertices.\n");
        printf("[5] Determinant (Matrix) Formula: Similar to coordinates formula, useful for vertices coordinates.\n");
        printf("Your choice (1-5): ");
        scanf("%d", &method);
        getchar(); // Consume newline character left in buffer

        switch (method) {
            case 1: // Base and Height
                base = getLengthOrHeight("Enter the base length:");
                baseUnit = getUnit("Choose the unit for base length:");
                height = getLengthOrHeight("Enter the height length:");
                heightUnit = getUnit("Choose the unit for height length:");

                if (baseUnit != heightUnit) {
                    base = convertLength(base, baseUnit, heightUnit);
                }

                float area = areaBaseHeight(base, height);
                printf("\n********************************************\n");
                printf("*              ANSWER                     *\n");
                printf("*        The area of the triangle is:    *\n");
                printf("********************************************\n");
                printf("Area in square meters: %.2f m²\n", convertArea(area, 1));
                printf("Area in square centimeters: %.2f cm²\n", convertArea(area, 2));
                printf("Area in square feet: %.2f ft²\n", convertArea(area, 3));
                printf("Area in square inches: %.2f in²\n", convertArea(area, 4));
                printf("Area in square yards: %.2f yd²\n", convertArea(area, 5));
                break;
            
            case 2: // Heron's Formula
                printf("Enter side a length:\n");
                sideA = getLengthOrHeight("Enter side a length:");
                a = getUnit("Choose the unit for side a:");
                printf("Enter side b length:\n");
                sideB = getLengthOrHeight("Enter side b length:");
                b = getUnit("Choose the unit for side b:");
                printf("Enter side c length:\n");
                c = getLengthOrHeight("Enter side c length:");
                c = getUnit("Choose the unit for side c:");

                if (a != b || b != c) {
                    sideA = convertLength(sideA, a, b);
                    sideB = convertLength(sideB, b, c);
                }

                area = areaHeron(sideA, sideB, c);
                printf("\n********************************************\n");
                printf("*              ANSWER                     *\n");
                printf("*        The area of the triangle is:    *\n");
                printf("********************************************\n");
                printf("Area in square meters: %.2f m²\n", convertArea(area, 1));
                printf("Area in square centimeters: %.2f cm²\n", convertArea(area, 2));
                printf("Area in square feet: %.2f ft²\n", convertArea(area, 3));
                printf("Area in square inches: %.2f in²\n", convertArea(area, 4));
                printf("Area in square yards: %.2f yd²\n", convertArea(area, 5));
                break;
            
            case 3: // Side-Angle-Side (SAS)
                printf("Enter side a length:\n");
                sideA = getLengthOrHeight("Enter side a length:");
                a = getUnit("Choose the unit for side a:");
                printf("Enter side b length:\n");
                sideB = getLengthOrHeight("Enter side b length:");
                b = getUnit("Choose the unit for side b:");
                printf("Enter angle in degrees:\n");
                angle = getLengthOrHeight("Enter angle in degrees:");

                if (a != b) {
                    sideA = convertLength(sideA, a, b);
                    sideB = convertLength(sideB, b, a);
                }

                angle = degreesToRadians(angle);
                area = areaSAS(sideA, sideB, angle);
                if (area < 0) {
                    printf("Error: Invalid input for angle.\n");
                    break;
                }
                printf("\n********************************************\n");
                printf("*              ANSWER                     *\n");
                printf("*        The area of the triangle is:    *\n");
                printf("********************************************\n");
                printf("Area in square meters: %.2f m²\n", convertArea(area, 1));
                printf("Area in square centimeters: %.2f cm²\n", convertArea(area, 2));
                printf("Area in square feet: %.2f ft²\n", convertArea(area, 3));
                printf("Area in square inches: %.2f in²\n", convertArea(area, 4));
                printf("Area in square yards: %.2f yd²\n", convertArea(area, 5));
                break;
            
            case 4: // Coordinates Formula
                printf("Enter coordinates for vertex 1 (x1 y1):\n");
                x1 = getLengthOrHeight("Enter x1:");
                y1 = getLengthOrHeight("Enter y1:");
                printf("Enter coordinates for vertex 2 (x2 y2):\n");
                x2 = getLengthOrHeight("Enter x2:");
                y2 = getLengthOrHeight("Enter y2:");
                printf("Enter coordinates for vertex 3 (x3 y3):\n");
                x3 = getLengthOrHeight("Enter x3:");
                y3 = getLengthOrHeight("Enter y3:");

                area = areaCoordinates(x1, y1, x2, y2, x3, y3);
                printf("\n********************************************\n");
                printf("*              ANSWER                     *\n");
                printf("*        The area of the triangle is:    *\n");
                printf("********************************************\n");
                printf("Area in square meters: %.2f m²\n", convertArea(area, 1));
                printf("Area in square centimeters: %.2f cm²\n", convertArea(area, 2));
                printf("Area in square feet: %.2f ft²\n", convertArea(area, 3));
                printf("Area in square inches: %.2f in²\n", convertArea(area, 4));
                printf("Area in square yards: %.2f yd²\n", convertArea(area, 5));
                break;
            
            case 5: // Determinant (Matrix) Formula
                printf("Enter coordinates for vertex 1 (x1 y1):\n");
                x1 = getLengthOrHeight("Enter x1:");
                y1 = getLengthOrHeight("Enter y1:");
                printf("Enter coordinates for vertex 2 (x2 y2):\n");
                x2 = getLengthOrHeight("Enter x2:");
                y2 = getLengthOrHeight("Enter y2:");
                printf("Enter coordinates for vertex 3 (x3 y3):\n");
                x3 = getLengthOrHeight("Enter x3:");
                y3 = getLengthOrHeight("Enter y3:");

                area = areaDeterminant(x1, y1, x2, y2, x3, y3);
                printf("\n********************************************\n");
                printf("*              ANSWER                     *\n");
                printf("*        The area of the triangle is:    *\n");
                printf("********************************************\n");
                printf("Area in square meters: %.2f m²\n", convertArea(area, 1));
                printf("Area in square centimeters: %.2f cm²\n", convertArea(area, 2));
                printf("Area in square feet: %.2f ft²\n", convertArea(area, 3));
                printf("Area in square inches: %.2f in²\n", convertArea(area, 4));
                printf("Area in square yards: %.2f yd²\n", convertArea(area, 5));
                break;

            default:
                printf("Invalid method selected.\n");
                break;
        }

        printf("\n=== Press Enter to calculate again ===\n");
        printf("Press any other key to exit.\n");
        recalculate = getchar();
        getchar(); // Consume newline character left in buffer

    } while (recalculate == '\n');

    return 0;
}

// Function implementations

float getLengthOrHeight(const char* prompt) {
    float value;
    printf("%s", prompt);
    while (scanf("%f", &value) != 1 || value <= 0) {
        printf("Invalid input. Please enter a positive number: ");
        while (getchar() != '\n'); // Clear the buffer
    }
    return value;
}

int getUnit(const char* prompt) {
    int unit;
    printf("%s\n", prompt);
    printf("1. Meters\n");
    printf("2. Centimeters\n");
    printf("3. Feet\n");
    printf("4. Inches\n");
    printf("5. Decimeters\n");
    printf("6. Millimeters\n");
    printf("Your choice (1-6): ");
    while (scanf("%d", &unit) != 1 || unit < 1 || unit > 6) {
        printf("Invalid input. Please select a valid option (1-6): ");
        while (getchar() != '\n'); // Clear the buffer
    }
    return unit;
}

float convertLength(float length, int fromUnit, int toUnit) {
    // Convert length from one unit to another
    // Implement the conversion logic here
    return length; // Placeholder
}

float convertArea(float metersSquared, int toUnit) {
    // Convert area from square meters to another unit
    // Implement the conversion logic here
    return metersSquared; // Placeholder
}

float areaBaseHeight(float base, float height) {
    return 0.5 * base * height;
}

float areaHeron(float a, float b, float c) {
    float s = (a + b + c) / 2;
    return sqrt(s * (s - a) * (s - b) * (s - c));
}

float areaSAS(float a, float b, float angle) {
    return 0.5 * a * b * sin(angle);
}

float areaCoordinates(float x1, float y1, float x2, float y2, float x3, float y3) {
    return fabs(x1*(y2 - y3) + x2*(y3 - y1) + x3*(y1 - y2)) / 2;
}

float areaDeterminant(float x1, float y1, float x2, float y2, float x3, float y3) {
    return fabs((x1*y2 + x2*y3 + x3*y1 - y1*x2 - y2*x3 - y3*x1) / 2.0);
}

float degreesToRadians(float degrees) {
    return degrees * M_PI / 180.0;
}
