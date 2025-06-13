import java.util.Scanner;

public class app11 {
    static class BankAccount {
        private String accountNumber;
        private String accountHolderName;
        private double balance;

        public BankAccount(String accountNumber, String accountHolderName, double initialBalance) {
            this.accountNumber = accountNumber;
            this.accountHolderName = accountHolderName;
            this.balance = initialBalance;
        }

        public void deposit(double amount) {
            if (amount > 0) {
                balance += amount;
                System.out.println("Successfully deposited $" + String.format("%.2f", amount));
            } else {
                System.out.println("Invalid deposit amount.");
            }
        }

        public void withdraw(double amount) {
            if (amount <= 0) {
                System.out.println("Invalid withdrawal amount.");
            } else if (amount > balance) {
                System.out.println("Insufficient balance.");
            } else {
                balance -= amount;
                System.out.println("Successfully withdrew $" + String.format("%.2f", amount));
            }
        }

        public void displayAccountDetails() {
            System.out.println("\n--- Account Details ---");
            System.out.println("Account Number: " + accountNumber);
            System.out.println("Account Holder: " + accountHolderName);
            System.out.println("Current Balance: $" + String.format("%.2f", balance));
            System.out.println("------------------------\n");
        }
    }

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        System.out.println("Welcome to Simple Banking Application");

        System.out.print("Enter account number: ");
        String accNum = scanner.nextLine();

        System.out.print("Enter account holder name: ");
        String accHolder = scanner.nextLine();

        System.out.print("Enter initial deposit amount: ");
        double initialDeposit = 0;
        while (true) {
            try {
                initialDeposit = Double.parseDouble(scanner.nextLine());
                if (initialDeposit < 0) {
                    System.out.print("Initial deposit cannot be negative. Enter again: ");
                } else {
                    break;
                }
            } catch (NumberFormatException e) {
                System.out.print("Invalid input. Enter a valid amount: ");
            }
        }

        BankAccount account = new BankAccount(accNum, accHolder, initialDeposit);

        boolean exit = false;
        while (!exit) {
            System.out.println("\nMenu:");
            System.out.println("1. Deposit");
            System.out.println("2. Withdraw");
            System.out.println("3. Display Account Details");
            System.out.println("4. Exit");
            System.out.print("Choose an option: ");

            String choice = scanner.nextLine();

            switch (choice) {
                case "1":
                    System.out.print("Enter deposit amount: ");
                    try {
                        double depositAmount = Double.parseDouble(scanner.nextLine());
                        account.deposit(depositAmount);
                    } catch (NumberFormatException e) {
                        System.out.println("Invalid amount entered.");
                    }
                    break;

                case "2":
                    System.out.print("Enter withdrawal amount: ");
                    try {
                        double withdrawAmount = Double.parseDouble(scanner.nextLine());
                        account.withdraw(withdrawAmount);
                    } catch (NumberFormatException e) {
                        System.out.println("Invalid amount entered.");
                    }
                    break;

                case "3":
                    account.displayAccountDetails();
                    break;

                case "4":
                    exit = true;
                    System.out.println("Thank you for using Simple Banking Application.");
                    break;

                default:
                    System.out.println("Invalid choice. Please select 1-4.");
            }
        }

        scanner.close();
    }
}

