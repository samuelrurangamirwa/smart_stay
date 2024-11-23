# Smart Stay Hotels Booking System

Smart Stay is a hotel booking system that allows users to register, log in, view available hotels and rooms, book stays, select amenities, create itineraries, and make payments. This system integrates with a MySQL database to store user information, hotel details, bookings, and itinerary data.

## Features

- **User Authentication**: Users can register, log in, and manage their accounts.
- **Hotel and Room Selection**: View available hotels and rooms, including prices and amenities.
- **Booking System**: Book rooms with check-in/check-out dates and calculate the total price based on the room and selected amenities.
- **Itinerary Management**: Add meals, activities, and costs to the itinerary for each booking.
- **Invoice Generation**: Generate a detailed invoice with booking and itinerary information.
- **Payment Integration**: Users can choose between Visa/Mastercard or PayPal for payment.

## Technologies Used

- Python
- MySQL
- datetime
- MySQL Connector

## Installation

### Prerequisites

1. **Python** (version 3.6 or later)
2. **MySQL** server
3. **MySQL Connector** for Python

### Steps to Set Up

1. Clone the repository:

    ```bash
    [git clone https://github.com/samuelrurangamirwa/smart_stay.git](https://github.com/samuelrurangamirwa/smart_stay.git)
    cd smart-stay-booking-system
    ```

2. Install the required Python libraries:

    ```bash
    pip install mysql-connector-python
    ```

3. Set up the MySQL database. You can create the database `smart_stay` and the necessary tables by running the following SQL commands:

    ```sql
    CREATE DATABASE smart_stay;

    USE smart_stay;

    CREATE TABLE users (
        id INT AUTO_INCREMENT PRIMARY KEY,
        username VARCHAR(255) NOT NULL,
        password VARCHAR(255) NOT NULL
    );

    CREATE TABLE hotels (
        id INT AUTO_INCREMENT PRIMARY KEY,
        name VARCHAR(255) NOT NULL,
        location VARCHAR(255) NOT NULL
    );

    CREATE TABLE rooms (
        id INT AUTO_INCREMENT PRIMARY KEY,
        hotel_id INT,
        name VARCHAR(255) NOT NULL,
        price DECIMAL(10, 2) NOT NULL,
        FOREIGN KEY (hotel_id) REFERENCES hotels(id)
    );

    CREATE TABLE amenities (
        id INT AUTO_INCREMENT PRIMARY KEY,
        room_id INT,
        name VARCHAR(255) NOT NULL,
        price DECIMAL(10, 2),
        FOREIGN KEY (room_id) REFERENCES rooms(id)
    );

    CREATE TABLE bookings (
        id INT AUTO_INCREMENT PRIMARY KEY,
        user_id INT,
        room_id INT,
        check_in DATE NOT NULL,
        check_out DATE NOT NULL,
        total_price DECIMAL(10, 2) NOT NULL,
        status VARCHAR(255) NOT NULL,
        FOREIGN KEY (user_id) REFERENCES users(id),
        FOREIGN KEY (room_id) REFERENCES rooms(id)
    );

    CREATE TABLE itinerary (
        id INT AUTO_INCREMENT PRIMARY KEY,
        booking_id INT,
        day INT NOT NULL,
        meal VARCHAR(255) NOT NULL,
        activity VARCHAR(255) NOT NULL,
        cost DECIMAL(10, 2),
        FOREIGN KEY (booking_id) REFERENCES bookings(id)
    );
    ```

4. Edit the MySQL connection details in the code (username, password, and host) to match your local MySQL configuration.

## Usage

1. **Run the script** to start the booking system:

    ```bash
    python booking_system.py
    ```

2. **Menu Options**:
    - **Login**: Enter your username and password to log into the system.
    - **Register**: Create a new account by entering a username and password.
    - **Exit**: Exit the system.

3. After logging in:
    - Choose a hotel from the available list.
    - Select a room and amenities.
    - Choose check-in and check-out dates.
    - Confirm the booking and generate the invoice.

4. **Payment Options**:
    - Choose between **Visa/Mastercard** or **PayPal** to make the payment.

## Contributing

Contributions are welcome! If you have any suggestions or improvements, feel free to open an issue or submit a pull request.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Contact

For any inquiries, contact Samuel Rurangamirwa at [samuelrurangamirwa@gmail.com](mailto:samuelrurangamirwa@gmail.com).
