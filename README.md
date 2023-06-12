# Shopping-cart
Shopping cart
import java.util.ArrayList;
import java.util.List;
import java.util.Scanner;

public class ShoppingCart {
    private static List<Product> products = new ArrayList<>();
    private static List<Product> cart = new ArrayList<>();
    private static double totalCost = 0;

    public static void main(String[] args) {
        // create some sample products
        products.add(new Product("Product 1", 10.00));
        products.add(new Product("Product 2", 15.00));
        products.add(new Product("Product 3", 20.00));

        // display the products
        displayProducts();

        // prompt the user to add items to their cart
        Scanner scanner = new Scanner(System.in);
        String input;
        while (true) {
            System.out.print("Enter a product name to add to your cart (or 'done' to checkout): ");
            input = scanner.nextLine();
            if (input.equals("done")) {
                break;
            }
            addToCart(input);
        }

        // display the cart and total cost
        displayCart();
        System.out.println("Total cost: $" + String.format("%.2f", totalCost));
    }

    private static void displayProducts() {
        System.out.println("Products:");
        for (Product product : products) {
            System.out.println("- " + product.getName() + " ($" + String.format("%.2f", product.getPrice()) + ")");
        }
        System.out.println();
    }

    private static void addToCart(String productName) {
        // find the product in the list of products
        Product product = null;
        for (Product p : products) {
            if (p.getName().equalsIgnoreCase(productName)) {
                product = p;
                break;
            }
        }

        // add the product to the cart
        if (product != null) {
            cart.add(product);
            totalCost += product.getPrice();
            System.out.println(product.getName() + " added to cart.");
        } else {
            System.out.println("Product not found.");
        }
    }

    private static void displayCart() {
        System.out.println("Shopping Cart:");
        for (Product product : cart) {
            System.out.println("- " + product.getName() + " ($" + String.format("%.2f", product.getPrice()) + ")");
        }
        System.out.println();
    }
}

class Product {
    private String name;
    private double price;

    public Product(String name, double price) {
        this.name = name;
        this.price = price;
    }

    public String getName() {
        return name;
    }

    public double getPrice() {
        return price;
    }
}
