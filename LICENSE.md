#include <iostream>
#include <string>
#include <fstream>

using namespace std;

class room
{
public:
	string roomType;
	int roomNumber;

	room(string type = "null", int number = 0)
		: roomType(type), roomNumber(number)
	{
	}

	string getterRoomtype()
	{
		return roomType;
	}

	int RoomNumber()
	{
		return roomNumber;
	}
};

class Person
{
private:
	string name;
	string cnicNumber;
	string address;
	string contactNumber;
	string email;

public:
	Person(string name = "null", string cnic = "N-A", string add = "null", string contact = "N-A", string email = "null")
		: name(name), cnicNumber(cnic), address(add), contactNumber(contact), email(email)
	{
	}

	virtual string getName()
	{
		return name;
	}

	virtual string getCnic()
	{
		return cnicNumber;
	}

	virtual string getAddress()
	{
		return address;
	}

	virtual string getNumber()
	{
		return contactNumber;
	}

	virtual string getEmail()
	{
		return email;
	}
};
// for the epception of integer
int readInteger() {
	int value;
	while (!(cin >> value)) {
		cout << "\t\tInvalid input. Please enter an integer: ";
		cin.clear();

		cin.ignore(numeric_limits<streamsize>::max(), '\n');
	}
	return value;
}

// Function to safely read a double from input
double readDouble() {
	double value;
	while (!(cin >> value)) {
		cout << "\t\tInvalid input. Please enter a number: ";
		cin.clear();
		cin.ignore(numeric_limits<streamsize>::max(), '\n');
	}
	return value;
}


// employee class


class Employee : public Person
{
private:
	int empId;
	string rank;
	double salary;

public:
	Employee(int id = 0, string renk = "null", double salary = 0, string name = "null", string cnic = "N-A", string add = "null", string contact = "N-A")
		: Person(name, cnic, add, contact), empId(id), salary(salary), rank(renk)
	{
	}

	string getterRank()
	{
		return rank;
	}
	int getterEmpId()
	{
		return empId;
	}
	double getterEmpSalary()
	{
		return salary;
	}
};














class Clark : public Employee
{
public:
	Clark(int id = 0, string renk = "null", double salary = 0, string name = "null", string cnic = "N-A", string add = "null", string contact = "N-A")
		: Employee(id, renk, salary, name, cnic, add, contact)
	{
	}

	int convertStringToInt(const string& str) {
		try {
			return stoi(str);
		}
		catch (const invalid_argument& e) {
			//cerr << "Error converting string to int: " << e.what() << endl;
			return -1;                                                           // Indicate an error
		}
		catch (const out_of_range& e) {
			//cerr << "Error converting string to int (out of range): " << e.what() << endl;
			return -1;                                                // Indicate an error
		}
	}

	void searcCustomer(string fileName) {
		cout << "\t\tEnter ID: ";
		string uc;
		cin >> uc;


		// Convert string to int
		string path = "D:\\" + fileName + "hassanandasadClarkEmployeeDetail.txt";
		int searchId = convertStringToInt(uc);

		if (searchId != -1) {
			// Check if the file exists
			ifstream file(path);
			if (file.good()) {
				string line;
				while (getline(file, line)) {
					// Convert the line containing ID to int
					int id = convertStringToInt(line);

					if (id == searchId) {

						cout << "\t\t----------------------------------------" << endl;
						getline(file, line);
						cout << line << endl;
						getline(file, line);
						cout << line << endl;
						getline(file, line);
						cout << line << endl;
						getline(file, line);
						cout << line << endl;
						getline(file, line);
						cout << line << endl;
						getline(file, line);
						cout << line << endl;
						getline(file, line);
						cout << line << endl << endl;
						cout << "\t\t----------------------------------------" << endl;
						return;
					}
				}
				cout << "\t\tNo Employee found with ID: " << searchId << endl;
			}
			else {
				cout << path + " \t\tfile does not exist" << endl;
			}
		}
	}



	//for the edit Clark information any change informtion 



// for the edit clarksdetaail
	void edit(string sfile)
	{
		cin.ignore();

		cout << "\t\tEnter ID: ";
		string uc;
		getline(cin, uc);

		int searchId = convertStringToInt(uc);

		string path = "D:\\" + sfile + "hassanandasadClarkEmployeeDetail.txt";
		if (searchId != -1)
		{
			ifstream file(path);
			if (file.good())
			{
				string line;
				string lines;
				bool employeeFound = false;

				while (getline(file, line))
				{
					int id = convertStringToInt(line);

					if (id == searchId)
					{
						employeeFound = true;

						lines += "\t\t" + to_string(id) + '\n';

						cout << "\t\tEnter the Employee new name: ";
						getline(cin, line);
						lines += "\t\tName          : " + line + '\n';

						cout << "\t\tEnter the Employee CNIC Number: ";
						getline(cin, line);
						lines += "\t\tCNIC Number   : " + line + '\n';

						cout << "\t\tEnter the Employee Address is: ";
						getline(cin, line);
						lines += "\t\tAddress       : " + line + '\n';

						cout << "\t\tEnter the Employee rank is: ";
						getline(cin, line);
						lines += "\t\tEmployee Rank : " + line + '\n';

						cout << "\t\tEnter the Employ salary is: ";
						getline(cin, line);
						lines += "\t\tSalary        : " + line + '\n';

						cout << "\t\tEnter the Employee phone number is: ";
						getline(cin, line);
						lines += "\t\tPhone Number  : " + line + '\n';

						getline(file, line);
						getline(file, line);
						break;
					}
					else
					{
						lines += line + '\n';
					}
				}

				if (employeeFound)
				{
					ofstream outFile(path);
					outFile << lines;

					cout << "\t\tEmployee details updated successfully." << endl;
				}
				else
				{
					cout << "\t\tNo Employee found with ID: " << searchId << endl;
				}
			}
			else
			{
				cout << "\t\tfile does not exist." << endl;
			}
		}
	}



























	// this is the save detail into the filing 

	void saveDetailFile(string fileName)
	{
		string path = "D:\\" + fileName + "hassanandasadClarkEmployeeDetail.txt";

		ofstream input(path, ios::app);
		input << "\t\t--------------------------------------------" << endl;
		input << "\t\t" << getterEmpId() << endl;
		input << "\t\tName          : " << getName() << endl;
		input << "\t\tEmployee ID   : " << getterEmpId() << endl;
		input << "\t\tCNIC          : " << getCnic() << endl;
		input << "\t\tAddress       : " << getAddress() << endl;
		input << "\t\tPhone Number  : " << getNumber() << endl;
		input << "\t\tEmployee Rank : " << getterRank() << endl;
		input << "\t\tSalary        :  " << getterEmpSalary() << endl << endl;
		input << "\t\t--------------------------------------------" << endl;

		input.close();

	}
	void showDetailsFromFile(string Sfile)
	{
		string path = "D:\\" + Sfile + "hassanandasadClarkEmployeeDetail.txt";

		ifstream file(path);
		if (file.good())
		{
			string line;

			while (getline(file, line))
			{

				cout << line << endl;

			}
			file.close();
		}
		else
		{
			cout << "\t\tFile does not exist." << endl;
		}
	}




};


// class for manager detail


class Manager : public Employee
{

public:
	Manager(int id = 0, string renk = "null", double salary = 0, string name = "null", string cnic = "N-A", string add = "null", string contact = "N-A")
		: Employee(id, renk, salary, name, cnic, add, contact)
	{
	}


	int convertStringToInt(const string& str) {
		try {
			return stoi(str);
		}
		catch (const invalid_argument& e) {
			//cerr << "Error converting string to int: " << e.what() << endl;
			return -1; // Indicate an error
		}
		catch (const out_of_range& e) {
			//cerr << "Error converting string to int (out of range): " << e.what() << endl;
			return -1; // Indicate an error
		}
	}

	void searcCustomer(string fileName) {
		cout << "\t\tEnter ID: ";
		string uc;
		cin >> uc;


		// Convert string to int
		string path = "D:\\" + fileName + "hassanandasadMAnagerEmployeeDetail.txt";
		int searchId = convertStringToInt(uc);

		if (searchId != -1) {
			// Check if the file exists
			ifstream file(path);
			if (file.good()) {
				string line;
				while (getline(file, line)) {
					// Convert the line containing ID to int
					int id = convertStringToInt(line);

					if (id == searchId) {

						cout << "\t\t----------------------------------------" << endl;
						getline(file, line);
						cout << line << endl;
						getline(file, line);
						cout << line << endl;
						getline(file, line);
						cout << line << endl;
						getline(file, line);
						cout << line << endl;
						getline(file, line);
						cout << line << endl;
						getline(file, line);
						cout << line << endl;
						getline(file, line);
						cout << line << endl << endl;
						cout << "\t\t----------------------------------------" << endl;
						return;
					}
				}
				cout << "\t\tNo Manager found with ID: " << searchId << endl;
			}
			else {
				cout << path + " \t\tfile does not exist" << endl;
			}
		}
	}




	// for the edit Manager detaail
	void edit(string sfile)
	{
		cin.ignore();

		cout << "\t\tEnter ID: ";
		string uc;
		getline(cin, uc);

		int searchId = convertStringToInt(uc);

		string path = "D:\\" + sfile + "hassanandasadManagerEmployeeDetail.txt";
		if (searchId != -1)
		{
			ifstream file(path);
			if (file.good())
			{
				string line;
				string lines;
				bool employeeFound = false;

				while (getline(file, line))
				{
					int id = convertStringToInt(line);

					if (id == searchId)
					{
						employeeFound = true;

						lines += "\t\t" + to_string(id) + '\n';

						cout << "\t\tEnter the Employee new name: ";
						getline(cin, line);
						lines += "\t\tName          : " + line + '\n';

						cout << "\t\tEnter the Employee CNIC Number: ";
						getline(cin, line);
						lines += "\t\tCNIC Number   : " + line + '\n';

						cout << "\t\tEnter the Employee Address is: ";
						getline(cin, line);
						lines += "\t\tAddress       : " + line + '\n';

						cout << "\t\tEnter the Employee rank is: ";
						getline(cin, line);
						lines += "\t\tEmployee Rank : " + line + '\n';

						cout << "\t\tEnter the Employ salary is: ";
						getline(cin, line);
						lines += "\t\tSalary        : " + line + '\n';

						cout << "\t\tEnter the Employee phone number is: ";
						getline(cin, line);
						lines += "\t\tPhone Number  : " + line + '\n';

						getline(file, line);
						getline(file, line);
						break;
					}
					else
					{
						lines += line + '\n';
					}
				}

				if (employeeFound)
				{
					ofstream outFile(path);
					outFile << lines;

					cout << "\t\tEmployee details updated successfully." << endl;
				}
				else
				{
					cout << "\t\tNo employee found with ID: " << searchId << endl;
				}
			}
			else
			{
				cout << "\t\tfile does not exist." << endl;
			}
		}
	}














	void saveDetailFile(string file)
	{
		string path = "D:\\" + file + "hassanandasadManagerEmployeeDetail.txt";

		ofstream input(path, ios::app);
		input << "\t\t--------------------------------------------" << endl;
		input << "\t\t" << getterEmpId() << endl;
		input << "\t\tName           : " << getName() << endl;
		input << "\t\tEmployee ID    : " << getterEmpId() << endl;
		input << "\t\tCNIC           : " << getCnic() << endl;
		input << "\t\tAddress        : " << getAddress() << endl;
		input << "\t\tPhone Number   : " << getNumber() << endl;
		input << "\t\tEmployee Rank  : " << getterRank() << endl;
		input << "\t\tSalary         :  " << getterEmpSalary() << endl << endl;
		input << "\t\t--------------------------------------------" << endl;

		input.close();
	}

	void showDetailsFromFile(string Sfile)
	{
		string path = "D:\\" + Sfile + "hassanandasadManagerEmployeeDetail.txt";

		ifstream file(path);

		if (file.good())
		{
			string line;

			while (getline(file, line))
			{

				cout << line << endl;

			}

			file.close();
		}
		else
		{
			cout << "File does not exist." << endl;
		}
	}




};







// customer class 


class CustomerInfo : public Person
{
private:
	int hotelId;
	static int numberCustomer;
	room *customerRooms; // Use dynamic array for rooms
	int numRooms;
	string bookingDate;
	string paymentMethod;

public:
	CustomerInfo(int id = 0, string name = "null", string cnic = "N-A", string add = "null", string contact = "N-A", string date = "null", string payment = "null", string email = "null")
		: Person(name, cnic, add, contact, email), hotelId(id), numRooms(0), customerRooms(nullptr), bookingDate(date), paymentMethod(payment)
	{
		numberCustomer++;
	}

	static int getter()
	{
		return numberCustomer;
	}


	CustomerInfo(const CustomerInfo &other)
		: Person(other), hotelId(other.hotelId), numRooms(other.numRooms), bookingDate(other.bookingDate), paymentMethod(other.paymentMethod)
	{
		numberCustomer++;
		if (numRooms > 0)
		{
			customerRooms = new room[numRooms];
			for (int i = 0; i < numRooms; i++)
			{
				customerRooms[i] = other.customerRooms[i];
			}
		}
		else
		{
			customerRooms = nullptr;
		}

	}

	~CustomerInfo()
	{
		delete[] customerRooms;
		numberCustomer--;
	}

	void addRoom(string roomType, int roomNumber)
	{
		// Resize the dynamic array and add the new room
		room *temp = new room[numRooms + 1];
		for (int i = 0; i < numRooms; i++)
		{
			temp[i] = customerRooms[i];
		}
		temp[numRooms] = room(roomType, roomNumber);

		delete[] customerRooms;
		customerRooms = temp;
		numRooms++;
	}

	void display()
	{
		cout << "\t\t--------------------------------------------" << endl;
		cout << "\t\tName           : " << getName() << endl;
		cout << "\t\tCNIC           : " << getCnic() << endl;
		cout << "\t\tPhone Number   : " << getNumber() << endl;
		cout << "\t\tEmail          : " << getEmail() << endl;
		cout << "\t\tAddress        : " << getAddress() << endl;
		cout << "\t\tHotel ID       : " << hotelId << endl;

		for (int i = 0; i < numRooms; i++)
		{
			cout << "\t\tRoom Type      : " << customerRooms[i].roomType << endl;
			cout << "\t\tRoom Number    : " << customerRooms[i].roomNumber << endl;
		}

		cout << "\t\tBooking Date   : " << bookingDate << endl;
		cout << "\t\tPayment Method : " << paymentMethod << endl;
		cout << "\t\t---------------------------------------------" << endl;
	}

	void editCustomerDetail(CustomerInfo customers[], int num)
	{
		int id;
		cout << "\t\tPlease input the customer id for customer edit detail  ";
		cin >> id;
		string name;
		string cnic;
		string address;
		string contact;
		string email;
		string bookingDate;
		string paymentMethod;
		string roomType;
		int roomNumber;

		bool found = false;

		for (int i = 0; i < num; i++)
		{
			if (customers[i].getHotelId() == id)
			{
				cout << "\t\tPlease input the updated customer details:" << endl << endl;;

				cout << "\t\tEnter updated customer name: ";

				cin >> name;

				cout << "\t\tEnter updated customer CNIC: ";
				cin >> cnic;

				cout << "\t\tEnter updated customer address: ";

				cin >> address;

				cout << "\t\tEnter updated customer contact number: ";
				cin >> contact;

				cout << "\t\tEnter updated customer email: ";
				cin >> email;

				cout << "\t\tEnter updated booking date (YYYY-MM-DD): ";
				cin >> bookingDate;

				cout << "\t\tEnter updated payment method: ";
				cin >> paymentMethod;

				cout << "\t\tEnter updated room type: ";
				cin >> roomType;


				cout << "\t\tEnter updated room number: ";
				roomNumber = readInteger();

				// Update the customer object
				customers[i] = CustomerInfo(id, name, cnic, address, contact, bookingDate, paymentMethod);
				customers[i].addRoom(roomType, roomNumber);

				cout << "\t\tCustomer details updated successfully!" << endl;
				found = true;
				break; // exit loop after finding the customer
			}


		}
		if (!false)
		{
			cout << "\t\tcustomer not found by this id" << endl;
		}
	}

	static int getNumberCustomers()
	{
		return numberCustomer;
	}

	int getHotelId()
	{
		return hotelId;
	}
};

int CustomerInfo::numberCustomer = 101;




void addNewCustomer(CustomerInfo customers[], int &customerCount);
void searchCustomerById(CustomerInfo customers[], int customerCount);
void deleteCustomerById(CustomerInfo customers[], int &customerCount);





void menu(string fileName)
{
	const int maxCustomers = 7;
	CustomerInfo customers[maxCustomers] = {
		CustomerInfo(CustomerInfo::getter(), "Hassan Akhtar", "921312-12331-2", "North Karachi", "0313232566", "2023-12-05", "Credit Card","akhtarhassan10@yahoo.com"),
		CustomerInfo(CustomerInfo::getter(), "Asad Anjum", "932432-15531-9", "Faisalabad chinot", "0300232344", "2023-12-06", "PayPal","asadanjum213@yahoo.com"),
		CustomerInfo(CustomerInfo::getter(), "Abdul Rehman", "945612-12221-1", "Lahore", "0432323442", "2023-12-07", "Cash","abdulrehma33@yahoo.com"),
		CustomerInfo(CustomerInfo::getter(), "Yahya Akhtar", "92333-98331-7", "North Karachi", "02224345455", "2023-12-08", "Credit Card","akhteryahya221@yahoo.com"),
		CustomerInfo(CustomerInfo::getter(), "Dehya Akhtar", "744312-11131-3", "North Karachi", "0432344232", "2023-12-09", "Cash","dehyaakhter219@yahoo.com") };

	// Initialize room type and room number for each customer
	customers[0].addRoom("Single", 101);
	customers[1].addRoom("Double", 202);
	customers[2].addRoom("Suite", 303);
	customers[3].addRoom("Single", 102);
	customers[4].addRoom("Double", 203);

	int customerCount = 5; // Initial number of customers




	int numManagers = 3;
	Manager *managers = new Manager[numManagers];

	managers[0] = Manager(21, "Assistant Manager", 50000, "Abdul Rehman ", "63142-34431-5", "Karachi", "0223223342");
	managers[1] = Manager(22, "Floor Manager", 70000, "Shahid Khan ", "999912-78131-2", "Karachi", "032132321231");
	managers[2] = Manager(33, "Finance Manager", 150000, "Jawad Khan ", "933322-13431-2", "Pindi", "03002564207");

	for (int i = 0; i < numManagers; i++)
	{
		managers[i].saveDetailFile(fileName);


	}
	// Clark employee data store in

	int numClark = 7;

	Clark *clarks = new Clark[numClark];

	clarks[0] = Clark(23, "Super vissor", 30000, "Yasir junior  ", "921312-12331-2", "Islamabad", "0454543343");
	clarks[1] = Clark(34, "Floor incharge", 40000, "Abdul Shkoor  ", "921312-12331-2", "Islamabad", "04545543432");
	clarks[2] = Clark(35, "office boy", 25000, "Abdullah  ", "921312-12331-2", "Islamabad", "04545433233");
	clarks[3] = Clark(36, "Hr coordinator", 30000, "Usman khan  ", "343312-12331-8", "Rawal Pindi");
	clarks[4] = Clark(37, "Recepnist", 35000, "Akmam  ", "34322-13331-7", "Lahore");
	clarks[5] = Clark(38, "Recepnist", 25000, "Abdul Sattar  ", "95552-133331-2", "Islamabad", "0456464433");
	clarks[6] = Clark(39, "Sales Person", 70000, "Mehmood ", "921312-12331-2", "Karachi", "0313734332");

	for (int i = 0; i < numClark; i++)
	{
		clarks[i].saveDetailFile(fileName);


	}

	bool stop = false;



	while (!stop)
	{
		cout << "\n \n \n ";
		cout << "\t\t            HOTEL MANAGEMNT SYSTEM" << endl;
		cout << "\t\t----------------------------------------------------- " << endl;
		cout << "\t\t*****************************************************" << endl;
		cout << "\t\t*    Press 1 to display all customers               * " << endl;
		cout << "\t\t*    Press 2 to add a new customer                  * " << endl;
		cout << "\t\t*    Press 3 to search for a customer by ID         * " << endl;
		cout << "\t\t*    Press 4 to delete a customer by ID             * " << endl;
		cout << "\t\t*    Press 5 to edit customer details               *" << endl; // Added option for editing
		cout << "\t\t*    Press 6 to display Managers Detail             *" << endl;
		cout << "\t\t*    Press 7 to edit Managers details               *" << endl;
		cout << "\t\t*    Press 8 to Search Manger details               *" << endl;
		cout << "\t\t*    Press 9 to Dispaly Clarks details              *" << endl;
		cout << "\t\t*    Press 10 to edit clarks details                *" << endl;
		cout << "\t\t*    Press 11 to Search clarks details              *" << endl;
		cout << "\t\t*    Press to exit                                  *" << endl;
		cout << "\t\t*****************************************************" << endl;

		int choice;
		cout << "\t\t";
		choice = readInteger();





		switch (choice)
		{
		case 1:
			// Display all customers
			for (int i = 0; i < customerCount; ++i)
			{
				customers[i].display();
			}
			break;

		case 2:
			// Add a new customer
			addNewCustomer(customers, customerCount);
			break;

		case 3:
			// Search for a customer by ID
			searchCustomerById(customers, customerCount);
			break;

		case 4:
			// Delete a customer by ID
			deleteCustomerById(customers, customerCount);
			break;

		case 5:
			// Edit customer details
			customers->editCustomerDetail(customers, customerCount);
			break;


		case 6:

			managers->showDetailsFromFile(fileName);

			break;
		case 7:
			managers->edit(fileName);
			break;

		case 8:
			managers->searcCustomer(fileName);
			break;

		case 9:

			clarks->showDetailsFromFile(fileName);

			break;


		case 10:
			clarks->edit(fileName);
			break;



		case 11:

			clarks->searcCustomer(fileName);
			break;
		case 12:
			// exit the programm
			cout << "\t\tAllah Hafiz" << endl;
			stop = true;
			break;

		default:
			cout << "\t\tInvalid choice. Please enter a valid option." << endl;
		}
	}


}








int main()
{
	bool stop = true;
	while (stop != false)
	{
		string admin;
		cout << "\n\n\n";
		cout << "|**********************************************************|" << endl << endl;
		cout << " Admin UserName            :" << " ";
		cin >> admin;
		cout << "\n|----------------------------------------------------------|" << endl;

		cout << "\n\n|**********************************************************|" << endl;
		cout << "\n";
		cout << " Please input the Password :" << "  ";
		string password;
		cin >> password;
		cout << "\n|----------------------------------------------------------|" << endl;

		if (password == "password" && admin == "admin")
		{
			cout << "\n\n____________________________________________________________" << endl;
			cout << "\n";

			cout << "please input the file you want to take information " << endl;
			string fileName;
			cin >> fileName;
			cout << "\n \n\n \n\n \n\n" << endl;
			menu(fileName);
			stop = false;
		}
		else {
			cout << "\t\t Please correct input " << endl;
		}

	}


	return 0;
}

void addNewCustomer(CustomerInfo customers[], int &customerCount)

{
	int id = CustomerInfo::getter();
	if (customerCount == 6) {
		CustomerInfo::getter();
		id++;
	}
	if (customerCount < 7)
	{

		// Get input for the new customer



		string name;
		string cnic;
		string address;
		string contact;
		string email;
		string bookingDate;
		string paymentMethod;
		string roomType;
		int roomNumber;

		cout << "\t\tEnter customer name: ";
		cin.ignore(); // Ignore any newline character left in the buffer
		getline(cin, name);

		cout << "\t\tEnter customer CNIC: ";
		cin >> cnic;

		cout << "\t\tEnter customer address: ";
		cin.ignore(); // Ignore any newline character left in the buffer
		getline(cin, address);

		cout << "\t\tEnter customer contact number: ";
		cin >> contact;

		cout << "\t\tEnter customer email: ";
		cin >> email;

		cout << "\t\tEnter booking date (YYYY-MM-DD): ";
		string date, mon, year;
		cout << "\t\tdate is " << " ";
		cin >> date;
		cout << "\t\tMonth is " << " ";
		cin >> mon;
		cout << "\t\tyear is " << " ";
		cin >> year;
		bookingDate = date + "/" + mon + "/" + year;

		cout << "\t\tEnter payment method: ";
		cin >> paymentMethod;

		cout << "\t\tEnter room type: ";
		cin >> roomType;

		cout << "\t\tEnter room number: ";
		roomNumber = readInteger();

		// Create a new CustomerInfo object and add it to the array
		customers[customerCount] = CustomerInfo(id, name, cnic, address, contact, bookingDate, paymentMethod, email + "@gmail.com");
		customers[customerCount].addRoom(roomType, roomNumber);
		customerCount++;

		cout << "\t\tNew customer added successfully!" << endl;
	}
	else
	{
		cout << "\t\tMaximum number of customers reached. Cannot add a new customer." << endl;
	}
}

void searchCustomerById(CustomerInfo customers[], int customerCount)
{
	int searchId;
	cout << "\t\tEnter customer ID to search: ";
	searchId = readInteger();

	bool found = false;
	for (int i = 0; i < customerCount; ++i)
	{
		if (customers[i].getHotelId() == searchId)
		{
			cout << "\t\tCustomer found! Details:" << endl;
			customers[i].display();
			found = true;
			break;
		}
	}

	if (!found)
	{
		cout << "\t\tCustomer with ID " << searchId << " not found." << endl;
	}
}

void deleteCustomerById(CustomerInfo customers[], int &customerCount)
{
	int deleteId;
	cout << "\t\tEnter customer ID to delete: ";
	deleteId = readInteger();

	bool found = false;
	for (int i = 0; i < customerCount; ++i)
	{
		if (customers[i].getHotelId() == deleteId)
		{
			// Shift the remaining elements to maintain continuity in the array
			for (int j = i; j < customerCount - 1; ++j)
			{
				customers[j] = customers[j + 1];
			}
			customerCount--;
			found = true;
			cout << "\t\tCustomer with ID " << deleteId << " deleted successfully." << endl;


			break;
		}
	}

	if (!found)
	{
		cout << "\t\tCustomer with ID " << deleteId << " not found." << endl;
	}
}
