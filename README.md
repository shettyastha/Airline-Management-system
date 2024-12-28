# Airline-Management-system
import mysql.connector

def create_connection():
    connection = mysql.connector.connect(
        host='localhost',
        user='root',
        password='akshetty_10909',
        database='airline_management'
    )
    return connection

def add_flight(flight_number, destination, departure_time, arrival_time, status):
    connection = create_connection()
    cursor = connection.cursor()
    query = "INSERT INTO Flights (flight_number, destination, departure_time, arrival_time, status) VALUES (%s, %s, %s, %s, %s)"
    values = (flight_number, destination, departure_time, arrival_time, status)
    cursor.execute(query, values)
    connection.commit()
    cursor.close()
    connection.close()

def add_passenger(name, contact_info, passport_number):
    connection = create_connection()
    cursor = connection.cursor()
    query = "INSERT INTO Passengers (name, contact_info, passport_number) VALUES (%s, %s, %s)"
    values = (name, contact_info, passport_number)
    cursor.execute(query, values)
    connection.commit()
    cursor.close()
    connection.close()

def book_flight(passenger_id, flight_id, booking_date, seat_number):
    connection = create_connection()
    cursor = connection.cursor()
    query = "INSERT INTO Bookings (passenger_id, flight_id, booking_date, seat_number) VALUES (%s, %s, %s, %s)"
    values = (passenger_id, flight_id, booking_date, seat_number)
    cursor.execute(query, values)
    connection.commit()
    cursor.close()
    connection.close()

def main():
    while True:
        print("1. Add Flight")
        print("2. Add Passenger")
        print("3. Book Flight")
        print("4. Exit")
        choice = input("Enter your choice: ")

        if choice == '1':
            flight_number = input("Enter flight number: ")
            destination = input("Enter destination: ")
            departure_time = input("Enter departure time (YYYY-MM-DD HH:MM:SS): ")
            arrival_time = input("Enter arrival time (YYYY-MM-DD HH:MM:SS): ")
            status = input("Enter status: ")
            add_flight(flight_number, destination, departure_time, arrival_time, status)
        elif choice == '2':
            name = input("Enter passenger name: ")
            contact_info = input("Enter contact info: ")
            passport_number = input("Enter passport number: ")
            add_passenger(name, contact_info, passport_number)
        elif choice == '3':
            passenger_id = int(input("Enter passenger ID: "))
            flight_id = int(input("Enter flight ID: "))
            booking_date = input("Enter booking date (YYYY-MM-DD): ")
            seat_number = input("Enter seat number: ")
            book_flight(passenger_id, flight_id, booking_date, seat_number)
        elif choice == '4':
            break
        else:
            print("Invalid choice, please try again.")

if __name__ == "__main__":
    main()
    
