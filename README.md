# 💹 CodeAlpha Stock Trading Platform

This project is a **console-based stock trading simulator** built in **Java**. It was developed as part of the **Java Programming Internship** at **CodeAlpha**. The app allows users to buy and sell stocks, view market data, and track their portfolio using Object-Oriented Programming concepts.

---

## 📌 Features

- 📈 View live market stock prices (predefined)
- 🛒 Buy and sell stocks using virtual cash
- 📊 Track your portfolio and balance
- 🧠 Object-Oriented Design: `Stock`, `Portfolio`, `Main`
- 💻 100% Console-based Java app

---

## 💡 Technologies Used

- Java (JDK 8+)
- Java Collections (Map, HashMap)
- Scanner for console input
- Conditionals and loops
- Any Java IDE or Online Compiler

---

## 📸 Code
import java.util.*;

// Represents a stock in the market
class Stock {
    String symbol;
    double price;

    public Stock(String symbol, double price) {
        this.symbol = symbol;
        this.price = price;
    }
}

// Represents the user's portfolio
class Portfolio {
    Map<String, Integer> holdings = new HashMap<>();
    double cash = 10000.00; // Starting cash

    public void buyStock(Stock stock, int quantity) {
        double cost = stock.price * quantity;
        if (cash >= cost) {
            cash -= cost;
            holdings.put(stock.symbol, holdings.getOrDefault(stock.symbol, 0) + quantity);
            System.out.println("✅ Bought " + quantity + " shares of " + stock.symbol);
        } else {
            System.out.println("❌ Not enough cash to buy.");
        }
    }

    public void sellStock(Stock stock, int quantity) {
        int owned = holdings.getOrDefault(stock.symbol, 0);
        if (owned >= quantity) {
            holdings.put(stock.symbol, owned - quantity);
            cash += stock.price * quantity;
            System.out.println("✅ Sold " + quantity + " shares of " + stock.symbol);
        } else {
            System.out.println("❌ Not enough shares to sell.");
        }
    }

    public void viewPortfolio(Map<String, Stock> market) {
        System.out.println("\n📊 --- Portfolio Summary ---");
        for (String symbol : holdings.keySet()) {
            int qty = holdings.get(symbol);
            double price = market.get(symbol).price;
            System.out.println(symbol + ": " + qty + " shares, Current Value: $" + (qty * price));
        }
        System.out.printf("💰 Cash Balance: $%.2f\n", cash);
    }
}

// Main class to run the trading simulator
public class Main {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        // Sample market data
        Map<String, Stock> market = new HashMap<>();
        market.put("AAPL", new Stock("AAPL", 180.50));
        market.put("GOOG", new Stock("GOOG", 2750.25));
        market.put("TSLA", new Stock("TSLA", 720.10));

        Portfolio portfolio = new Portfolio();

        while (true) {
            System.out.println("\n📈 --- Stock Trading Menu ---");
            System.out.println("1. View Market");
            System.out.println("2. Buy Stock");
            System.out.println("3. Sell Stock");
            System.out.println("4. View Portfolio");
            System.out.println("5. Exit");
            System.out.print("Select option (1-5): ");
            int choice = scanner.nextInt();

            if (choice == 1) {
                System.out.println("\n📈 --- Market Data ---");
                for (Stock s : market.values()) {
                    System.out.println(s.symbol + " : $" + s.price);
                }
            } else if (choice == 2) {
                System.out.print("Enter stock symbol to buy: ");
                String symbol = scanner.next().toUpperCase();
                if (!market.containsKey(symbol)) {
                    System.out.println("❌ Invalid stock symbol.");
                    continue;
                }
                System.out.print("Enter quantity: ");
                int qty = scanner.nextInt();
                portfolio.buyStock(market.get(symbol), qty);
            } else if (choice == 3) {
                System.out.print("Enter stock symbol to sell: ");
                String symbol = scanner.next().toUpperCase();
                if (!market.containsKey(symbol)) {
                    System.out.println("❌ Invalid stock symbol.");
                    continue;
                }
                System.out.print("Enter quantity: ");
                int qty = scanner.nextInt();
                portfolio.sellStock(market.get(symbol), qty);
            } else if (choice == 4) {
                portfolio.viewPortfolio(market);
            } else if (choice == 5) {
                System.out.println("👋 Exiting... Thank you for trading!");
                break;
            } else {
                System.out.println("❌ Invalid option. Try again.");
            }
        }

        scanner.close();
    }
}
## 📸 Sample Output
📈 --- Stock Trading Menu ---

View Market

Buy Stock

Sell Stock

View Portfolio

Exit
Select option: 1

AAPL : $180.5
GOOG : $2750.25
TSLA : $720.1

Select option: 2
Enter stock symbol to buy: AAPL
Enter quantity: 10
✅ Bought 10 shares of AAPL

Select option: 4

📊 --- Portfolio Summary ---
AAPL: 10 shares, Current Value: $1805.0
💰 Cash Balance: $8195.00

