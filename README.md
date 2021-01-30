# Canteen-Card
# This is my first Java code. I hope you will like it. :)

import java.util.Scanner;

public class CanteenSL {

    static double cardBalance;
    static Scanner scan;

    public static void main(String[] args) {
        scan = new Scanner(System.in);
        getCardBalance();
        Double costOfOrder = ordering();
        if (canUserPay(costOfOrder)) {
            cardBalance -= costOfOrder;
            System.out.println("Your order has been placed! Your new card balance is: " + cardBalance + "$");
        } else {
            System.out.println("Sorry, you don't have enough money, order will not be placed. Bye!");
        }

    }
    public static boolean canUserPay(double orderCost) {
        if (orderCost <= cardBalance) {
            return true;
        }
        double remainder = (orderCost - cardBalance);
        System.out.println("You don't have enough money, would you like to add extra " + remainder + "$" + "?" + "(type YES/NO)");
        String addToBalance = scan.nextLine().toLowerCase();
        if (addToBalance.equals("yes")) {
            cardBalance += remainder;
            return true;
        }
        return false;
    }
    public static double ordering() {
        String menu[] = {
            "Beef steak",
            "Pasta",
            "Chicken nuggets",
            "Burger",
            "Pizza",
            "Salad",
            "Coca-Cola",
            "Water"
        };
        double prizes[] = {
            7.50,
            6.00,
            5.00,
            4.00,
            4.00,
            3.50,
            2.00,
            1.50
        };
        double costsOfOrder = 0;
        System.out.println("\n____TODAY'S MENU____");
        for (int i = 0; i < menu.length; i++) {
            System.out.println("\n" + i + "." + menu[i] + "......" + prizes[i] + "$");
        }
        while (true) {
            System.out.println("\nPick the item number for making your order! (for submitting or quiting type 10)");
            int choice = Integer.parseInt(scan.nextLine());
            if (choice < menu.length) {
                System.out.println(menu[choice] + "......" + prizes[choice] + "$");
                costsOfOrder += getTotal(getQuantity(), prizes, choice, menu);
            } else if (choice != menu.length && choice != 10) {
                System.out.println("Please type right number of your item or type 10 for quiting!");
            } else if (choice == 10) {
                break;
            }
        }
        return costsOfOrder;
    }
    public static double getCardBalance() {
        System.out.println("Welcome to Canteen, please add some credit on your Canteen Card!");
        cardBalance = Double.parseDouble(scan.nextLine());
        return cardBalance;
    }

    public static int getQuantity() {
        System.out.println("Enter quantity: ");
        int quantity = Integer.parseInt(scan.nextLine());
        return quantity;
    }
    public static double getTotal(int getQuantity, double prizes[], int choice, String menu[]) {
        double total = getQuantity * prizes[choice];
        System.out.println("Your order costs: " + getQuantity + " x " + menu[choice] + "(" + prizes[choice] + "$" + ")" + " = " + total + "$");
        return total;

    }



}
