import java.util.Scanner;

public class InventoryManagement {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        System.out.print("Enter number of products: ");
        int n = sc.nextInt();
        sc.nextLine(); // consume newline

        int[] productID = new int[n];
        String[] productName = new String[n];
        double[] quantityKg = new double[n];   // quantity in kilograms
        double[] pricePerKg = new double[n];   // price per kilogram

        // Input product records
        for (int i = 0; i < n; i++) {
            System.out.println("\nEnter details for Product " + (i+1));
            System.out.print("ID: ");
            productID[i] = sc.nextInt();
            sc.nextLine();
            System.out.print("Name: ");
            productName[i] = sc.nextLine();
            System.out.print("Quantity (in kg): ");
            quantityKg[i] = sc.nextDouble();
            System.out.print("Price per kg (in money): ");
            pricePerKg[i] = sc.nextDouble();
            sc.nextLine();
        }

        // Display all products
        System.out.println("\n--- Inventory Records ---");
        for (int i = 0; i < n; i++) {
            double totalValue = quantityKg[i] * pricePerKg[i];
            System.out.println("ID: " + productID[i] +
                               ", Name: " + productName[i] +
                               ", Quantity: " + quantityKg[i] + " kg" +
                               ", Price per kg: ₹" + pricePerKg[i] +
                               ", Total Value: ₹" + totalValue);
        }

        // Search product by ID
        System.out.print("\nEnter Product ID to search: ");
        int searchID = sc.nextInt();
        boolean found = false;
        for (int i = 0; i < n; i++) {
            if (productID[i] == searchID) {
                double totalValue = quantityKg[i] * pricePerKg[i];
                System.out.println("Product Found: " + productName[i] +
                                   ", Quantity: " + quantityKg[i] + " kg" +
                                   ", Price per kg: ₹" + pricePerKg[i] +
                                   ", Total Value: ₹" + totalValue);
                found = true;
                break;
            }
        }
        if (!found) {
            System.out.println("Product with ID " + searchID + " not found.");
        }

        // Update stock (simulate sale)
        System.out.print("\nEnter Product ID to sell: ");
        int sellID = sc.nextInt();
        System.out.print("Enter quantity sold (in kg): ");
        double soldQty = sc.nextDouble();
        for (int i = 0; i < n; i++) {
            if (productID[i] == sellID) {
                if (quantityKg[i] >= soldQty) {
                    quantityKg[i] -= soldQty;
                    double totalValue = quantityKg[i] * pricePerKg[i];
                    System.out.println("Sale successful! Remaining stock: " + quantityKg[i] + " kg" +
                                       ", New Total Value: ₹" + totalValue);
                } else {
                    System.out.println("Not enough stock available!");
                }
            }
        }

        // Find product with highest stock
        double maxStock = quantityKg[0];
        String maxProduct = productName[0];
        for (int i = 1; i < n; i++) {
            if (quantityKg[i] > maxStock) {
                maxStock = quantityKg[i];
                maxProduct = productName[i];
            }
        }
        System.out.println("\nProduct with highest stock: " + maxProduct + " (" + maxStock + " kg)");

        sc.close();
    }
}
