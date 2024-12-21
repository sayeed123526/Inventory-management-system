# Inventory-management-system
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

typedef struct{
    int id;
    char name[50];
    int quantity;
    float price;

} Item;

void addItem(Item item[], int*count){
        printf("Enter item id : ");
        scanf("%d", &item[*count].id);
        printf("Enter item name : ");
        scanf(" %[^\n]", &item[*count].name);
        printf("Enter item quantity : ");
        scanf("%d", &item[*count].quantity);
        printf(" Enter item price : ");
        scanf("%f", &item[*count].price);
        (*count)++;
        printf("Items added successfully !\n ");


}

void displayItem(Item item[], int count){
    printf("\n Inventory items :\n");
    printf("id\tname\t\tquantity\tprice");
    printf(" \n");
    for (int i = 0; i<count; i++){
        printf("%d\t%-15s\t%d\t\t%.2f\n", item[i].id,item[i].name,item[i].quantity,item[i].price);
    }
}
void searchItem(Item item[], int count){
    int id;
    printf("Enter item id : ");
    scanf("%d", &id);
    for(int i = 0; i < count; i++){
        if (item[i].id == id){
            printf("Item with %d id has been found\n");
            printf("Id : %d\n , Name : %s\n, Quantity : %d\n, Price : %.2f\n ",
            item[i].id,item[i].name,item[i].quantity,item[i].price);
            return;
    
  }
    }
    printf("Item with %d id not found\n",id);
}

void deleteItem(Item item[],int *count){

  int id, found =0;
    printf("Enter the id of the item = ");
    scanf("%d", &id);
    for(int i =0; i<*count ; i++){
        if(item[i].id == id){
            found =  1;
            for(int j=i; j <*count-1;j++){
                item[j]= item[j+1];
                (*count)--;
                printf("Item deleted \n");
                break;
            }

  }
        if(!found){
            printf("Item with %d Id not found\n");
        }
    }
}
int main(){
    Item item [100];
    int count = 0, choice;
    while(1){
        printf("\n Inventory Management System\n");
        printf("Add Item\n");
        printf("Display Item\n");
        printf("Search Item\n");
        printf("Delete Item\n");
        printf("Exit\n");
        printf("Enter your choice = ");
        scanf("%d",&choice);
        switch (choice)
        {
        case 1:addItem(item, &count);break;
        case 2 : displayItem(item, count);break;
        case 3 : searchItem(item, count);break;
        case 4 : deleteItem (item, &count);break;
        case 5 : printf("Exiting...\n");
        exit(0);
       default:printf("Invalid \n");
            
}
    }
return 0;
}
