import java.util.HashMap;

class Bank {
    private HashMap<Integer, Account> accounts;

    public Bank() {
        accounts = new HashMap<>();
    }

    public void createAccount(int accountNumber, String accountHolder, double balance) {
        if (!accounts.containsKey(accountNumber)) {
            Account account = new Account(accountNumber, accountHolder, balance);
            accounts.put(accountNumber, account);
            System.out.println("Account created successfully.");
        } else {
            System.out.println("Account with the same account number already exists.");
        }
    }

    public void deposit(int accountNumber, double amount) {
        if (accounts.containsKey(accountNumber)) {
            Account account = accounts.get(accountNumber);
            account.deposit(amount);
            System.out.println("Deposit successful. New balance: " + account.getBalance());
        } else {
            System.out.println("Account not found.");
        }
    }

    public void withdraw(int accountNumber, double amount) {
        if (accounts.containsKey(accountNumber)) {
            Account account = accounts.get(accountNumber);
            if (account.withdraw(amount)) {
                System.out.println("Withdrawal successful. New balance: " + account.getBalance());
            } else {
                System.out.println("Insufficient funds.");
            }
        } else {
            System.out.println("Account not found.");
        }
    }

    public double checkBalance(int accountNumber) {
        if (accounts.containsKey(accountNumber)) {
            return accounts.get(accountNumber).getBalance();
        } else {
            System.out.println("Account not found.");
            return -1;
        }
    }
}

class Account {
    private int accountNumber;
    private String accountHolder;
    private double balance;

    public Account(int accountNumber, String accountHolder, double balance) {
        this.accountNumber = accountNumber;
        this.accountHolder = accountHolder;
        this.balance = balance;
    }

    public void deposit(double amount) {
        balance += amount;
    }

    public boolean withdraw(double amount) {
        if (balance >= amount) {
            balance -= amount;
            return true;
        }
        return false;
    }

    public double getBalance() {
        return balance;
    }
}

public class Main {
    public static void main(String[] args) {
        Bank bank = new Bank();
        bank.createAccount(12345, "John Doe", 1000.0);

        bank.deposit(12345, 500.0);
        bank.withdraw(12345, 200.0);

        double balance = bank.checkBalance(12345);
        System.out.println("Account balance: " + balance);
    }
}
