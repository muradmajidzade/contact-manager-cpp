#include <iostream>
#include <fstream>
using namespace std;

struct Person {
	string name;
	string number;
};

int main() {
	Person person1 = { "Ilham", "0502111111" };
	Person person2 = { "Pasha", "0502110101" };
	Person person3 = { "Emin", "0999999999" };

	Person persons[] = { person1, person2, person3 };
	int arraysize = 3;

	ofstream startFile("namenum.txt", ios::out);

	for (int i = 0; i < arraysize; i++) {
		startFile << "Name: " << persons[i].name << " Number: " << persons[i].number << endl;
	}

	startFile.close();

	ifstream readFile("namenum.txt");
	string label1;
	string label2;
	Person p;

	while (readFile >> label1 >> p.name >> label2 >> p.number) {
		cout << "Name: " << p.name << " Number: " << p.number << endl;
	}

	readFile.close();


	while (true) {
		int choice;
		cout << "Input choice (1 - Add, 2 - Delete, 3 - Edit, 4 - Show 5 - close): ";
		cin >> choice;

		if (choice == 1) {
			ofstream addFile("namenum.txt", ios::app);

			string newname;
			string newnum;

			cout << "Input new name: ";
			cin >> newname;
			cout << "Input new number: ";
			cin >> newnum;

			Person newperson = { newname, newnum };
			addFile << "Name: " << newperson.name << " Number: " << newperson.number << endl;

			addFile.close();
		}

		else if (choice == 2) {
			ifstream addDelFile("namenum.txt");

			string nametodel;
			string numtodel;
			Person temp[100];
			string label1;
			string label2;
			Person p;
			int newsize = 0;

			cout << "Input name to delete: ";
			cin >> nametodel;
			cout << "Input num to delete: ";
			cin >> numtodel;

			while (addDelFile >> label1 >> p.name >> label2 >> p.number) {
				if (p.name == nametodel && p.number == numtodel) {
					newsize++;
					continue;
				}
				else {
					temp[newsize].name = p.name;
					temp[newsize].number = p.number;
					newsize++;
				}
			}

			addDelFile.close();

			ofstream writeDelFile("namenum.txt", ios::out);

			for (int i = 0; i < newsize; i++) {
				if (temp[i].name != "" && temp[i].number != "") {
					writeDelFile << "Name: " << temp[i].name << " Number: " << temp[i].number << endl;
				}
			}

			writeDelFile.close();
		}


		else if (choice == 3) {
			ifstream addEditFile("namenum.txt");

			string nametochange;
			string numtochange;
			string newnum;
			Person temp[100];
			string label1;
			string label2;
			Person p;
			int newsize = 0;

			cout << "Input name to change: ";
			cin >> nametochange;
			cout << "Input num to change: ";
			cin >> numtochange;
			cout << "Input new num: ";
			cin >> newnum;

			while (addEditFile >> label1 >> p.name >> label2 >> p.number) {
				if (p.name == nametochange && p.number == numtochange) {
					temp[newsize].name = p.name;
					temp[newsize].number = newnum;
					newsize++;
				}
				else {
					temp[newsize].name = p.name;
					temp[newsize].number = p.number;
					newsize++;
				}
			}

			addEditFile.close();

			ofstream writeEditFile("namenum.txt", ios::out);

			for (int i = 0; i < newsize; i++) {
				writeEditFile << "Name: " << temp[i].name << " Number: " << temp[i].number << endl;
			}

			writeEditFile.close();
		}

		else if (choice == 4) {
			ifstream showFile("namenum.txt");
			string label1;
			string label2;
			Person p;

			while (showFile >> label1 >> p.name >> label2 >> p.number) {
				cout << "Name: " << p.name << " Number: " << p.number << endl;
			}

			showFile.close();
		}


		else if (choice == 5) {
			break;
		}

		else {
			cout << "Wrong choice!";
		}

	}

	return 0;
}