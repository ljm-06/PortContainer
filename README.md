import java.util.ArrayDeque;
import java.util.Scanner;

class Container {
    String id;
    String description;
    String weight;

    public Container(String id, String description, String weight) {
        this.id = id;
        this.description = description;
        this.weight = weight;
    }

    public String toString() {
        return id + " | " + description + " | " + weight;
    }
}

class Ship {
    String name;
    String captain;

    public Ship(String name, String captain) {
        this.name = name;
        this.captain = captain;
    }

    public String toString() {
        return name + " | Capt. " + captain;
    }
}

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        ArrayDeque<Container> containerStack = new ArrayDeque<>();
        ArrayDeque<Ship> shipQueue = new ArrayDeque<>();

        int choice = -1;

        while (choice != 0) {
            System.out.println("\n=== Port Container Management System ===");
            System.out.println("[1] Store container (push)");
            System.out.println("[2] View port containers");
            System.out.println("[3] Register arriving ship (enqueue)");
            System.out.println("[4] View waiting ships");
            System.out.println("[5] Load next ship (pop container + poll ship)");
            System.out.println("[0] Exit");
            System.out.print("Enter choice: ");
            choice = Integer.parseInt(sc.nextLine());

            if (choice == 1) {
                System.out.print("Enter container id: ");
                String id = sc.nextLine();
                System.out.print("Enter description: ");
                String desc = sc.nextLine();
                System.out.print("Enter weight: ");
                String w = sc.nextLine();

                Container c = new Container(id, desc, w);
                containerStack.push(c);
                System.out.println("Stored: " + c);

            } else if (choice == 2) {
                if (containerStack.isEmpty()) {
                    System.out.println("No containers at the port.");
                } else {
                    System.out.println("TOP →");
                    for (Container c : containerStack) {
                        System.out.println(c);
                    }
                    System.out.println("← BOTTOM");
                }

            } else if (choice == 3) {
                System.out.print("Enter ship name: ");
                String name = sc.nextLine();
                System.out.print("Enter captain: ");
                String cap = sc.nextLine();

                Ship s = new Ship(name, cap);
                shipQueue.offer(s);
                System.out.println("Registered: " + s);

            } else if (choice == 4) {
                if (shipQueue.isEmpty()) {
                    System.out.println("No ships waiting.");
                } else {
                    System.out.println("FRONT →");
                    for (Ship s : shipQueue) {
                        System.out.println(s);
                    }
                    System.out.println("← REAR");
                }

            } else if (choice == 5) {
                if (containerStack.isEmpty() || shipQueue.isEmpty()) {
                    System.out.println("Cannot load. Either no containers or no ships.");
                } else {
                    Container c = containerStack.pop();
                    Ship s = shipQueue.poll();
                    System.out.println("Loaded: " + c + " → " + s);
                    System.out.println("Remaining containers: " + containerStack.size());
                    System.out.println("Remaining ships waiting: " + shipQueue.size());
                }

            } else if (choice == 0) {
                System.out.println("Exiting program...");
            } else {
                System.out.println("Invalid choice. Try again.");
            }
        }
    }
}
