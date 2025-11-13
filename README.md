
#include <stdio.h>

int main() {
    int productID[10];
    char productName[10][50];
    int quantity[10];
    float price[10];
    int totalProducts = 0;
    int choice, i, searchID;
    float totalValue, highestValue, lowestValue;
    int highIndex, lowIndex;

    do {
        printf("\n========= INVENTORY MANAGEMENT SYSTEM =========\n");
        printf("1. Add Product\n");
        printf("2. Display All Products\n");
        printf("3. Show Total Inventory Value\n");
        printf("4. Show Product with Highest and Lowest Value\n");
        printf("5. Search Product by ID\n");
        printf("6. Exit\n");
        printf("Enter your choice: ");
        scanf("%d", &choice);

        if (choice == 1) {
            if (totalProducts >= 10) {
                printf("\nInventory full! Cannot add more products.\n");
            } else {
                printf("\nEnter Product ID: ");
                scanf("%d", &productID[totalProducts]);
                printf("Enter Product Name: ");
                scanf(" %[^\n]", productName[totalProducts]);
                printf("Enter Quantity: ");
                scanf("%d", &quantity[totalProducts]);
                printf("Enter Price per item: ");
                scanf("%f", &price[totalProducts]);

                totalProducts++;
                printf("\nProduct added successfully!\n");
            }
        }

        else if (choice == 2) {
            if (totalProducts == 0) {
                printf("\nNo products in inventory.\n");
            } else {
                printf("\n%-10s %-20s %-10s %-10s\n", "Prod ID", "Name", "Qty", "Price");
                for (i = 0; i < totalProducts; i++) {
                    printf("%-10d %-20s %-10d %-10.2f\n",
                           productID[i], productName[i], quantity[i], price[i]);
                }
            }
        }

        else if (choice == 3) {
            totalValue = 0;
            for (i = 0; i < totalProducts; i++) {
                totalValue += quantity[i] * price[i];
            }
            printf("\nTotal Inventory Value = %.2f\n", totalValue);
        }

        else if (choice == 4) {
            if (totalProducts == 0) {
                printf("\nNo products to analyze.\n");
            } else {
                highestValue = quantity[0] * price[0];
                lowestValue = quantity[0] * price[0];
                highIndex = 0;
                lowIndex = 0;

                for (i = 1; i < totalProducts; i++) {
                    float value = quantity[i] * price[i];
                    if (value > highestValue) {
                        highestValue = value;
                        highIndex = i;
                    }
                    if (value < lowestValue) {
                        lowestValue = value;
                        lowIndex = i;
                    }
                }

                printf("\nProduct with Highest Value:\n");
                printf("ID: %d | Name: %s | Qty: %d | Price: %.2f | Value: %.2f\n",
                       productID[highIndex], productName[highIndex],
                       quantity[highIndex], price[highIndex], highestValue);

                printf("\nProduct with Lowest Value:\n");
                printf("ID: %d | Name: %s | Qty: %d | Price: %.2f | Value: %.2f\n",
                       productID[lowIndex], productName[lowIndex],
                       quantity[lowIndex], price[lowIndex], lowestValue);
            }
        }

        else if (choice == 5) {
            if (totalProducts == 0) {
                printf("\nNo products in inventory.\n");
            } else {
                printf("\nEnter Product ID to search: ");
                scanf("%d", &searchID);
                int found = 0;

                for (i = 0; i < totalProducts; i++) {
                    if (productID[i] == searchID) {
                        printf("\nProduct Found!\n");
                        printf("ID: %d\nName: %s\nQuantity: %d\nPrice: %.2f\n",
                               productID[i], productName[i], quantity[i], price[i]);
                        found = 1;
                        break;
                    }
                }

                if (!found)
                    printf("\nProduct with ID %d not found.\n", searchID);
            }
        }

        else if (choice == 6) {
            printf("\nExiting program... Thank you!\n");
        }

        else {
            printf("\nInvalid choice! Please try again.\n");
        }

    } while (choice != 6);

    return 0;
}
