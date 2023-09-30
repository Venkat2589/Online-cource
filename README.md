# database-of-food-ordering-app


CREATE DATABASE FoodOrderingDB3;

-- Use the database
USE FoodOrderingDB3;

-- Create a table for users
CREATE TABLE Users (
    UserID INT AUTO_INCREMENT PRIMARY KEY,
    Username VARCHAR(50) UNIQUE,
    Password VARCHAR(255),
    Email VARCHAR(100) UNIQUE,
    FirstName VARCHAR(50),
    LastName VARCHAR(50)
);

-- Insert sample data into the Users table
INSERT INTO Users (Username, Password, Email, FirstName, LastName)
VALUES
    ('john_doe', 'password123', 'john.doe@example.com', 'John', 'Doe'),
    ('jane_smith', 'password456', 'jane.smith@example.com', 'Jane', 'Smith'),
    ('alice_smith', 'password789', 'alice.smith@example.com', 'Alice', 'Smith'),
    ('bob_jones', 'password321', 'bob.jones@example.com', 'Bob', 'Jones');

-- Create a table for restaurants
CREATE TABLE Restaurants (
    RestaurantID INT AUTO_INCREMENT PRIMARY KEY,
    Name VARCHAR(100),
    Description TEXT,
    Address TEXT,
    PhoneNumber VARCHAR(20)
);

-- Insert sample data into the Restaurants table
INSERT INTO Restaurants (Name, Description, Address, PhoneNumber)
VALUES
    ('Tasty Pizza Place', 'Delicious pizza and more', '789 Oak St, Restaurant City', '555-123-4567'),
    ('Burger Barn', 'Home of the best burgers', '567 Maple Dr, Burger Town', '555-987-6543'),
    ('Sushi Delight', 'Authentic Japanese cuisine', '123 Sakura St, Sushi City', '555-111-2222'),
    ('Pizza Haven', 'The best pizza in town', '456 Pepperoni Dr, Pizza Town', '555-333-4444');

-- Create a table for menu items
CREATE TABLE MenuItems (
    MenuItemID INT AUTO_INCREMENT PRIMARY KEY,
    RestaurantID INT,
    Name VARCHAR(100),
    Description TEXT,
    Price DECIMAL(10, 2),
    Category VARCHAR(50),
    FOREIGN KEY (RestaurantID) REFERENCES Restaurants(RestaurantID)
);

-- Insert sample data into the MenuItems table
INSERT INTO MenuItems (RestaurantID, Name, Description, Price, Category)
VALUES
    (1, 'Pepperoni Pizza', 'Classic pizza with pepperoni', 12.99, 'Pizza'),
    (1, 'Margherita Pizza', 'Fresh mozzarella, tomato, and basil', 11.99, 'Pizza'),
    (2, 'Bacon Cheeseburger', 'Juicy burger with bacon and cheese', 8.49, 'Burger'),
    (2, 'Veggie Burger', 'Grilled vegetable patty with toppings', 7.99, 'Burger'),
    (3, 'Sashimi Platter', 'Assortment of fresh sashimi', 22.99, 'Sushi'),
    (3, 'Tempura Roll', 'Shrimp tempura, avocado, and cucumber', 14.99, 'Sushi'),
    (4, 'Margherita Pizza', 'Classic tomato, mozzarella, and basil', 12.99, 'Pizza'),
    (4, 'Meat Lover\'s Pizza', 'Pepperoni, sausage, bacon, and ham', 15.99, 'Pizza');

-- Create a table for orders
CREATE TABLE Orders (
    OrderID INT AUTO_INCREMENT PRIMARY KEY,
    UserID INT,
    OrderDate DATETIME,
    TotalAmount DECIMAL(10, 2),
    Status VARCHAR(20),
    FOREIGN KEY (UserID) REFERENCES Users(UserID)
);

-- Insert sample data into the Orders table
INSERT INTO Orders (UserID, OrderDate, TotalAmount, Status)
VALUES
    (1, NOW(), 24.98, 'Pending'),
    (2, NOW(), 16.48, 'Delivered'),
    (3, NOW(), 37.98, 'Delivered'),
    (4, NOW(), 28.98, 'Pending');

-- Create a table for order items
CREATE TABLE OrderItems (
    OrderItemID INT AUTO_INCREMENT PRIMARY KEY,
    OrderID INT,
    MenuItemID INT,
    Quantity INT,
    FOREIGN KEY (OrderID) REFERENCES Orders(OrderID),
    FOREIGN KEY (MenuItemID) REFERENCES MenuItems(MenuItemID)
);

-- Insert sample data into the OrderItems table
INSERT INTO OrderItems (OrderID, MenuItemID, Quantity)
VALUES
    (1, 1, 2),
    (1, 3, 1),
    (2, 2, 1),
    (2, 4, 2),
    (3, 5, 1),
    (3, 6, 2),
    (4, 7, 1),
    (4, 8, 2);
