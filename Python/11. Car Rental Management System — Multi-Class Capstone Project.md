if __name__ == "__main__":
    # Create a single "company" (overall manager) object.
    class Car:

        total_cars = 0

        def __init__(self, car_id, model, base_fee):
            self.car_id = car_id
            self.model = model
            self.base_fee = base_fee
            self.is_available = True

            Car.total_cars += 1

        def rent_vehicle(self):
            if self.is_available:
                self.is_available = False
                return self.base_fee

            print("This vehicle is already rented.")
            return None

        def return_vehicle(self):
            self.is_available = True
            print("Vehicle returned successfully")

        @classmethod
        def get_total_cars(cls):
            print(f"Current number of vehicles: {cls.total_cars}")


    class ElectricCar(Car):

        def __init__(self,
                     car_id,
                     model,
                     base_fee,
                     battery_capacity,
                     driving_range):
            super().__init__(
                car_id,
                model,
                base_fee
            )

            self.battery_capacity = battery_capacity
            self.driving_range = driving_range

        def rent_vehicle(self):
            if self.is_available:
                self.is_available = False

                return int(self.base_fee * 0.8)

            print("This vehicle is already rented.")
            return None


    class Customer:

        def __init__(self, name):

            self.name = name
            self.rented_cars = []

        def show_my_rentals(self):

            print(f"\n{self.name}'s rented vehicles")

            if len(self.rented_cars) == 0:
                print("No vehicles currently rented.")
                return

            for car in self.rented_cars:
                print(
                    f"Vehicle ID: {car.car_id}, Model: {car.model}"
                )


    class RentalCompany:

        def __init__(self):

            self.car_storage = []

        def admin_login(self):

            pw = input("Enter admin password: ")

            if pw == "rental1234":
                return True

            print("Incorrect password.")
            return False

        def register_car(self):

            print("1. Standard vehicle")
            print("2. Electric vehicle")

            kind = input("Choose: ")

            car_id = input("Vehicle ID: ")
            model = input("Model name: ")
            fee = int(input("Rental fee: "))

            if kind == "1":

                car = Car(
                    car_id,
                    model,
                    fee
                )

            elif kind == "2":

                battery = int(
                    input("Battery capacity: ")
                )

                driving_range = int(
                    input("Driving range: ")
                )

                car = ElectricCar(
                    car_id,
                    model,
                    fee,
                    battery,
                    driving_range
                )

            else:

                print("Invalid input")
                return

            self.car_storage.append(car)

            print("Vehicle registered successfully")

        def search_car_info(self):

            car_id = input(
                "Vehicle ID to search: "
            )

            for car in self.car_storage:

                if car.car_id == car_id:

                    print(
                        f"Vehicle ID: {car.car_id}"
                    )

                    print(
                        f"Model: {car.model}"
                    )

                    print(
                        f"Rental fee: {car.base_fee}"
                    )

                    if car.is_available:
                        print("Status: Available")

                    else:
                        print("Status: Rented")

                    return

            print("Vehicle does not exist.")

        def process_rental(self, customer):

            car_id = input(
                "Vehicle ID to rent: "
            )

            for car in self.car_storage:

                if car.car_id == car_id:

                    fee = car.rent_vehicle()

                    if fee is None:
                        return

                    customer.rented_cars.append(car)

                    print(
                        f"Rental complete / Amount charged: {fee} won"
                    )

                    return

            print("Vehicle does not exist.")

        def process_return(self, customer):

            car_id = input(
                "Vehicle ID to return: "
            )

            for car in customer.rented_cars:

                if car.car_id == car_id:
                    car.return_vehicle()

                    customer.rented_cars.remove(car)

                    return

            print(
                "This vehicle is not in your rental list."
            )

    company = RentalCompany()

    while True:
        print("\n==================================")
        print("   Smart Rental Car Management System v1.0")
        print("==================================")
        print("1. Enter admin mode")
        print("2. Enter customer mode")
        print("3. Exit system")

        mode = input("Select a mode: ")

        if mode == "1":
            # Step 1: Verify password (using an encapsulated interface)
            if company.admin_login():
                while True:
                    print("\n====  Rental Car Admin System ====")
                    print("1. Register vehicle | 2. Search vehicle | 3. Total count | 4. Log out")

                    menu = input("Select an action: ")
                    if menu == "1":
                        company.register_car()
                    elif menu == "2":
                        company.search_car_info()
                    elif menu == "3":
                        Car.get_total_cars()  # Call the class method
                    elif menu == "4":
                        print("Exiting admin mode.")
                        break



        elif mode == "2":
            # [Dynamic creation] When a customer enters the menu, create a customer object on the fly and link it
            customer_name = input("Please enter your name: ")
            current_customer = Customer(customer_name)
            print(f"\nWelcome, {customer_name}!")

            while True:
                print(f"\n==== {customer_name}'s Customer Menu ====")
                print("1. Search vehicle | 2. Rent vehicle | 3. Return vehicle | 4. My rentals | 5. Log out")

                menu = input("Select an action: ")
                if menu == "1":
                    company.search_car_info()
                elif menu == "2":
                    company.process_rental(current_customer)  # Pass the current customer object as an argument
                elif menu == "3":
                    company.process_return(current_customer)  # Pass the current customer object as an argument
                elif menu == "4":
                    current_customer.show_my_rentals()
                elif menu == "5":
                    print("Exiting customer mode.")
                    break

        elif mode == "3":
            print("Shutting down the program completely. Thank you for using our service.")
            break
        else:
            print("Invalid input. Please choose again.")
