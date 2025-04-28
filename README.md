# ATM-MACHINE-JAVA


import java.util.Scanner;

public class ATMMachine {
    private static final double INITIAL_BALANCE = 1000.0;
    private static double balance = INITIAL_BALANCE;
    private static final int PIN = 9685; 

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        boolean running = true;

        while (running) {
            if (checkPin(scanner)) {
                displayMenu();
                int choice = scanner.nextInt();
                scanner.nextLine();

                switch (choice) {
                    case 1:
                        checkBalance();
                        break;
                    case 2:
                        deposit(scanner);
                        break;
                    case 3:
                        withdraw(scanner);
                        break;
                    case 4:
                        running = false;
                        System.out.println("Thank you for using the ATM. Goodbye!");
                        break;
                    default:
                        System.out.println("Invalid choice. Please try again.");
                        break;
                }
            } else {
                System.out.println("Invalid PIN. Please try again.");
            }
        }
    }

    private static boolean checkPin(Scanner scanner) {
        System.out.print("Enter your PIN: ");
        int enteredPin = scanner.nextInt();
        scanner.nextLine(); 
        return enteredPin == PIN;
    }

    private static void displayMenu() {
        System.out.println("Welcome to the ATM Machine!");
        System.out.println("Please select an option:");
        System.out.println("1. Check Balance");
        System.out.println("2. Deposit");
        System.out.println("3. Withdraw");
        System.out.println("4. Exit");
        System.out.print("Enter your choice: ");
    }

    private static void checkBalance() {
        System.out.println("Your current balance is: $" + balance);
    }

    private static void deposit(Scanner scanner) {
        System.out.print("Enter the amount to deposit: $");
        double amount = scanner.nextDouble();
        scanner.nextLine(); 
        balance += amount;
        System.out.println("Deposit successful. Your new balance is: $" + balance);
    }

    private static void withdraw(Scanner scanner) {
        System.out.print("Enter the amount to withdraw: $");
        double amount = scanner.nextDouble();
        scanner.nextLine(); 
        if (amount > balance) {
            System.out.println("Insufficient funds. Your current balance is: $" + balance);
        } else {
            balance -= amount;
            System.out.println("Withdrawal successful. Your new balance is: $" + balance);
        }
    }
}
