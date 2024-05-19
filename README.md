# Resturant_Management_System
I developed a project using java in object oriented programming



package restaurantmanagementsystem;

import java.util.Scanner;
import java.util.ArrayList;

public class RestaurantManagementSystem {

    public static void main(String[] args) {
        int choice;
        Scanner scan = new Scanner(System.in);
        Menu m = new Menu();

        do {
            System.out.println("Restaurant");
            System.out.println("1) Admin");
            System.out.println("2) Customer");
            System.out.println("Enter a choice:");
            choice = scan.nextInt();

            switch (choice) {
                case 1 -> {
                    Admin a1 = new Admin();

                    if (a1.LogIn()) {
                        m.adminMenu();
                    }
                }
                case 2 -> {
                    m.customerMenu();
                }
                default -> System.out.println("Invalid choice!");
            }

        } while (true);
    }
}

class Admin {

    private String username;
    private String password;

    Scanner sc = new Scanner(System.in);

    public Admin() {
        this.username = "kaleem";
        this.password = "kaleem12";
    }

    public boolean LogIn() {
        System.out.print("Enter username: ");
        username = sc.nextLine();

        if (username.equals("kaleem")) {
            System.out.print("Enter password: ");
            password = sc.nextLine();

            if (password.equals("kaleem12")) {
                System.out.println("Login successful!");
                return true;
            } else {
                System.out.println("Incorrect password!");
                return false;
            }

        } else {
            System.out.println("User not found!");
            return false;
        }
    }
}

class Menu {
    private String name;
    private double price;

    Scanner sc = new Scanner(System.in);
    ArrayList<Cuisine> item = new ArrayList<>();
    ArrayList<Cuisine> order = new ArrayList<>();

    
    
    public void adminMenu() {
        boolean exit = false;
        int choice;
        do {
            System.out.println("Menu:");
            System.out.println("1. Add Cuisine");
            System.out.println("2. View Menu");
            System.out.println("3. Update price of a cuisine");
            System.out.println("4. Delete a cuisine");
            System.out.println("5. Exit");
            System.out.print("Enter your choice: ");
            choice = sc.nextInt();

            switch (choice) {
                case 1 -> addCuisine();
                case 2 -> viewMenu();
                case 3 -> updatePrice();
                case 4 -> deleteCuisine();
                case 5 -> exit = true;
                default -> System.out.println("Invalid choice! Please try again.");
            }
        } while (!exit);
    }

    
    
    void addCuisine() {
        
        System.out.print("Enter the name of the cuisine: ");
        name = sc.next();
        System.out.print("Enter the price of the cuisine: ");
        price = sc.nextDouble();

        item.add(new Cuisine(name, price));
    }

    
    
    void viewMenu() {
        if (item.isEmpty()) {
            System.out.println("No Cuisines Available...");
        } else {
            for (Cuisine cuisine : item) {
                System.out.println(cuisine);
            }
        }
    }
    
    

    void updatePrice() {
        if (item.isEmpty()) {
            System.out.println("No Cuisines Available... To add Cuisine choose option 1...");
        } else {
            System.out.print("Enter cuisine name whose price you want to update: ");
            String updatedCuisine = sc.next();
            boolean found = false;

            for (Cuisine cuisine : item) {
                if (cuisine.getName().equalsIgnoreCase(updatedCuisine)) {
                    System.out.print("Enter new price: ");
                    double updatedPrice = sc.nextDouble();
                    cuisine.setPrice(updatedPrice);
                    System.out.println("Cuisine's updated price: " + cuisine);
                    found = true;
                    break;
                }
            }

            if (!found) {
                System.out.println("Cuisine not found!");
            }
        }
    }

    
    
    void deleteCuisine() {
        
        if (item.isEmpty()) {
            System.out.println("No Cuisines Available... To add Cuisine choose option 1...");
        } else {
            System.out.print("Enter cuisine name you want to delete: ");
            String cuisineToDelete = sc.next();
            boolean found = false;

            for (Cuisine cuisine : item) {
                if (cuisine.getName().equalsIgnoreCase(cuisineToDelete)) {
                    item.remove(cuisine);
                    System.out.println("Cuisine deleted successfully.");
                    found = true;
                    break;
                }
            }

            if (!found) {
                System.out.println("Cuisine not found!");
            }
        }
    }

    
    
    public void customerMenu() {
        
        boolean exit = false;
        int choice;
        do {
            System.out.println("Menu:");
            System.out.println("1. View Menu");
            System.out.println("2. Add to Cart");
            System.out.println("3. Exit");
            System.out.print("Enter your choice: ");
            choice = sc.nextInt();

            switch (choice) {
                case 1 -> viewMenu();
                case 2 -> addCart();
                case 3 -> exit = true;
                default -> System.out.println("Invalid choice! Please try again.");
            }
        } while (!exit);
    }

    
    
    void addCart() {
        
        boolean exit = false;
        double bill = 0;
        if (item.isEmpty()) {
            System.out.println("No Cuisines Available... To add Cuisine choose option 1...");
        } else {
            do {
                System.out.println("Enter Cuisine to order...\nEnter \"Exit\" when order is complete...");
                String chosenCuisine = sc.next();
                if (chosenCuisine.equalsIgnoreCase("exit")) {
                    exit = true;
                } else {
                    boolean found = false;
                    for (Cuisine x : item) {
                        if (x.getName().equalsIgnoreCase(chosenCuisine)) {
                            order.add(new Cuisine(x.getName(), x.getPrice()));
                            bill += x.getPrice();
                            found = true;
                            break;
                        }
                    }
                    if (!found) {
                        System.out.println("Cuisine not found!");
                    }
                }
            } while (!exit);
            System.out.println("Items added to cart: " + order);
            System.out.println("Total Bill: " + bill);
        }
    }
}



class Cuisine {

    private String name;
    private double price;

    public Cuisine(String name, double price) {
        this.name = name;
        this.price = price;
    }

    
    public String getName() {
        return name;
    }

    
    public double getPrice() {
        return price;
    }

    
    public void setPrice(double price) {
        this.price = price;
    }

    
    @Override
    public String toString() {
        return name + " : Rs " + price;
    }
}
