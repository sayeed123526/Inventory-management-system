#include <stdio.h>
#include <stdlib.h>
#include <string.h>


typedef struct {
    int id;
    char name[50];
    int quantity;
    float price;
} Item;


void addItem(Item items[], int *count) {
    printf("Enter Item ID: ");
    scanf("%d", &items[*count].id);
    printf("Enter Item Name: ");
    scanf(" %[^\n]", items[*count].name); 
    printf("Enter Quantity: ");
    scanf("%d", &items[*count].quantity);
    printf("Enter Price: ");
    scanf("%f", &items[*count].price);
    (*count)++;
    printf("Item added successfully!\n");
}

void displayItems(Item items[], int count) {
    printf("\nInventory Items:\n");
    printf("ID\tName\t\tQuantity\tPrice\n");
    printf("\n");
    for (int i = 0; i < count; i++) {
        printf("%d\t%-15s\t%d\t\t%.2f\n", items[i].id, items[i].name, items[i].quantity, items[i].price);
    }
}

void searchItem(Item items[], int count) {
    int id;
    printf("Enter Item ID to search: ");
    scanf("%d", &id);
    for (int i = 0; i < count; i++) {
        if (items[i].id == id) {
            printf("\nItem Found:\n");
            printf("ID: %d\nName: %s\nQuantity: %d\nPrice: %.2f\n", items[i].id, items[i].name, items[i].quantity, items[i].price);
            return;
        }
    }
    printf("Item with ID %d not found.\n", id);
}

void deleteItem(Item items[], int *count) {
    int id, found = 0;
    printf("Enter Item ID to delete: ");
    scanf("%d", &id);
    for (int i = 0; i < *count; i++) {
        if (items[i].id == id) {
            found = 1;
            for (int j = i; j < *count - 1; j++) {
                items[j] = items[j + 1];
            }
            (*count)--;
            printf("Item deleted successfully!\n");
            break;
        }
    }
    if (!found) {
        printf("Item with ID %d not found.\n", id);
    }
}

void updateItem(Item items[], int count) {
    int id, found = 0;
    printf("Enter Item ID to update: ");
    scanf("%d", &id);
    for (int i = 0; i < count; i++) {
        if (items[i].id == id) {
            found = 1;
            printf("Enter new Item Name: ");
            scanf(" %[^\n]", items[i].name);
            printf("Enter new Quantity: ");
            scanf("%d", &items[i].quantity);
            printf("Enter new Price: ");
            scanf("%f", &items[i].price);
            printf("Item updated successfully!\n");
            break;
        }
    }
    if (!found) {
        printf("Item with ID %d not found.\n", id);
    }
}

void viewTotalValue(Item items[], int count) {
    float totalValue = 0;
    for (int i = 0; i < count; i++) {
        totalValue += items[i].quantity * items[i].price;
    }
    printf("Total Value of Inventory: %.2f\n", totalValue);
}

int main() {
    Item items[100];
    int count = 0, choice;

while (1) {
        printf("\nInventory Management System\n");
        printf("1. Add Item\n");
        printf("2. Display Items\n");
        printf("3. Search Item\n");
        printf("4. Delete Item\n");
        printf("5. Update Item\n");
        printf("6. View Total Value\n");
        printf("7. Exit\n");
        printf("Enter your choice: ");
        scanf("%d", &choice);

  switch (choice) {
            case 1:
                addItem(items, &count);
                break;
            case 2:
                displayItems(items, count);
                break;
            case 3:
                searchItem(items, count);
                break;
            case 4:
                deleteItem(items, &count);
                break;
            case 5:
                updateItem(items, count);
                break;
            case 6:
                viewTotalValue(items, count);
                break;
            case 7:
                printf("Exiting...\n");
                exit(0);
            default:
                printf("Invalid choice. Please try again.\n");
        }
    }

 return 0;
}
