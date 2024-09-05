# githubthebus

This is code is in Python

# Passagerarklass: Definition och Initialisering
class Passenger:
    def __init__(self, name, age, gender, behavior):
        self.name = name
        self.age = age
        self.gender = gender
        self.behavior = behavior

    # Funktionen "poke" i passagerarklassen
    def poke(self):
        if self.age < 18:
            if self.gender == "male":
                print(self.name, "is a young boy. He giggles when poked.")
            elif self.gender == "female":
                print(self.name, "is a young girl. She laughs when poked.")
            else:
                print(self.name, "is underage. Their reaction depends on their gender.")
        else:
            if self.gender == "male":
                print(self.name, "is a man. He grunts when poked.")
            elif self.gender == "female":
                print(self.name, "is a woman. She gives a stern look when poked.")
            else:
                print(self.name, "is an adult. Their reaction depends on their gender.")

# Bussklass: Definition och Initialisering
class Bus:
    def __init__(self):
        self.passengers = []
        self.passenger_count = 0
        self.max_passengers = 25  # Maximalt antal tillåtna passagerare
        self.max_child_age = 17   # Maxålder för barnpassagerare

    # Funktionen "add_passenger" i Busklassen
    def add_passenger(self, passenger):
        if self.passenger_count < self.max_passengers:
            self.passengers.append(passenger)
            self.passenger_count += 1
            print(passenger.name, "boarded the bus. Passenger number:", self.passenger_count)
        else:
            print("The bus is full. Cannot add more passengers.")

    # Funktionen "print_passenger_ages" i Busklassen
    def print_passenger_ages(self):
        print("Passenger ages:")
        for i, passenger in enumerate(self.passengers, start=1):
            print("Passenger", i, ":", passenger.age, "-", passenger.name)

    # Funktionen "total_passenger_age" i Busklassen
    def total_passenger_age(self):
        total_age = sum(passenger.age for passenger in self.passengers)
        return total_age

    # Funktionen "poke_passenger" i Busklassen
    def poke_passenger(self):
        passenger_number = int(input("Enter passenger number to poke: "))
        if 1 <= passenger_number <= self.passenger_count:
            self.passengers[passenger_number - 1].poke()
        else:
            print("Invalid passenger number.")

    # Funktionen "remove_passenger" i Busklassen
    def remove_passenger(self):
        passenger_number = int(input("Enter passenger number to remove: "))
        if 1 <= passenger_number <= self.passenger_count:
            removed_passenger = self.passengers.pop(passenger_number - 1)
            self.passenger_count -= 1
            print(removed_passenger.name, "has left the bus. Have a great day and welcome back!")
        else:
            print("Invalid passenger number.")

    # Funktionen "sort_passengers_by_age" i Busklassen för att sortera passagerare baserat på ålder
    def sort_passengers_by_age(self):
        self.passengers.sort(key=lambda x: x.age)
        print("Passengers sorted by age.")

    # Funktionen "run" i Busklassen
    def run(self):
        print("Welcome to the awesome Bus Simulator!")
        while True:
            print("\nMENU:")
            print("1. Add Passenger")
            print("2. Print Passenger Ages")
            print("3. Calculate Total Passenger Age")
            print("4. Poke Passenger")
            print("5. Remove Passenger")
            print("6. Sort Passengers by Age")
            print("7. Set Simulator Settings")
            print("8. Exit")

            choice = input("Enter your choice: ")
            if choice == '1':
                name = input("Enter passenger's name: ")
                age = int(input("Enter passenger's age: "))
                gender = input("Enter passenger's gender (Male/Female): ")
                while gender.lower() not in ["male", "female"]:
                    print("Invalid input. Please enter 'Male' or 'Female'.")
                    gender = input("Enter passenger's gender (Male/Female): ")
                behavior = input("Enter passenger's behavior: ")
                passenger = Passenger(name, age, gender, behavior)
                self.add_passenger(passenger)
            elif choice == '2':
                self.print_passenger_ages()
            elif choice == '3':
                total_age = self.total_passenger_age()
                print("Total passenger age:", total_age)
            elif choice == '4':
                self.poke_passenger()
            elif choice == '5':
                self.remove_passenger()
            elif choice == '6':
                self.sort_passengers_by_age()
            elif choice == '7':
                self.set_simulator_settings()
            elif choice == '8':
                print("Exiting Bus Simulator. Goodbye!")
                break
            else:
                print("Invalid choice. Please enter a valid option.")

    # Funktionen "set_simulator_settings" i Busklassen för att justera inställningar
    def set_simulator_settings(self):
        print("\nSIMULATOR SETTINGS:")
        print("1. Set Max Number of Passengers (Current:", self.max_passengers, ")")
        print("2. Set Max Age for Child Passengers (Current:", self.max_child_age, ")")
        setting_choice = input("Enter your choice: ")
        if setting_choice == '1':
            new_max_passengers = int(input("Enter the new max number of passengers: "))
            self.max_passengers = new_max_passengers
            print("Max Passengers updated successfully.")
        elif setting_choice == '2':
            new_max_child_age = int(input("Enter the new max age for child passengers: "))
            self.max_child_age = new_max_child_age
            print("Max Child Age updated successfully.")
        else:
            print("Invalid setting number.")

# Bus Simulator Main Program
if __name__ == "__main__":
    bus = Bus()
    bus.run()
