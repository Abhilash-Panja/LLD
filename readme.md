🎯 Single Responsibility Principle (SRP)
The Single Responsibility Principle (SRP) is the first principle of the SOLID design principles. It states that a class should have one reason to change. In essence, each class should only have one responsibility. This promotes clean, maintainable, and flexible code.

"A class should have only one reason to change."
— Robert C. Martin

🔍 What is SRP?
The Single Responsibility Principle asserts that a class should only have one job or reason to change. If a class handles more than one responsibility, these responsibilities become coupled, and changes to one might affect the others.

Benefits of SRP:
Reduces complexity: Smaller, focused classes are easier to understand and maintain.

Improves flexibility: Changes to one responsibility don’t risk breaking others.

Promotes reusability: Isolated classes can be reused across various parts of the application.

Simplifies testing: Testing becomes easier because classes focus on a single behavior.

🚨 How to Identify SRP Violations

1. Multiple Responsibilities
   A class is handling more than one task, such as logging, database interactions, or UI logic.

Example of Violation:

java
Copy
Edit
// 🚫 Violation: Student class manages data AND saves to DB AND prints details.
class Student {
private String name;

    public Student(String name) {
        this.name = name;
    }

    public void saveToDatabase() {
        // Database logic here
    }

    public void printDetails() {
        System.out.println("Student: " + name);
    }

}
🛠️ SRP in Practice: Java Code Examples
Example 1: Student Class
🚫 Bad Code
java
Copy
Edit
// Violation: Mixed responsibilities—data storage, database operations, and UI logic
class Student {
private String name;

    public Student(String name) {
        this.name = name;
    }

    public void saveToDatabase() {
        // Database logic
    }

    public void printDetails() {
        System.out.println("Student: " + name);
    }

}
✅ Good Code
java
Copy
Edit
// Student: Responsible for storing student data
class Student {
private String name;

    public Student(String name) {
        this.name = name;
    }

    public String getName() {
        return name;
    }

}

// StudentRepository: Responsible for handling database operations
class StudentRepository {
public void save(Student student) {
// Save student data to the database
}
}

// StudentPrinter: Responsible for printing student details (UI Logic)
class StudentPrinter {
public void printDetails(Student student) {
System.out.println("Student: " + student.getName());
}
}
Example 2: Order Processing
🚫 Bad Code
java
Copy
Edit
// Violation: Order class processes orders, saves to DB, and sends emails
class Order {
public void processOrder() {
// Processing logic
}

    public void saveToDatabase() {
        // Database logic
    }

    public void sendConfirmationEmail() {
        // Email logic
    }

}
✅ Good Code
java
Copy
Edit
// Order: Responsible for processing the order
class Order {
public void processOrder() {
// Order processing logic
}
}

// OrderRepository: Responsible for handling database operations related to orders
class OrderRepository {
public void save(Order order) {
// Save order to database
}
}

// EmailService: Responsible for sending confirmation emails
class EmailService {
public void sendConfirmationEmail(Order order) {
// Send confirmation email
}
}
Example 3: User Authentication
🚫 Bad Code
java
Copy
Edit
// Violation: UserAuthenticator mixes authentication logic with logging
class UserAuthenticator {
public boolean login(String username, String password) {
// Authentication logic
Logger.log("User logged in: " + username); // ❌ Logging inside authentication logic
return true;
}
}
✅ Good Code
java
Copy
Edit
// AuthService: Handles authentication logic
class AuthService {
public boolean login(String username, String password) {
// Authentication logic
return true;
}
}

// Logger: Manages logging separately
class Logger {
public static void log(String message) {
// Log the message
}
}
📌 Key Takeaways
Single Responsibility: Each class should have one, focused responsibility.

Separation of Concerns: Don’t mix business logic, UI, and database concerns in the same class.

Avoid God Classes: Don't create classes that handle too many responsibilities. Instead, break them down into smaller, more manageable classes.

❌ Common SRP Pitfalls
Mixing Different Layers: Avoid mixing business logic with infrastructure concerns (e.g., database or UI).

Adding Helper Methods to Data Classes: Don’t overload data classes with utility methods such as logging or validation.

Confusing Responsibilities: A responsibility is not just a single method—it's a high-level task that the class is dedicated to.

✅ Final Tip
When designing a class, always ask:
"What is the primary responsibility of this class?"
If it performs multiple unrelated tasks, it's time to split it into separate classes.
