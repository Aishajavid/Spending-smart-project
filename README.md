#include <iostream>
#include <string>
#include <iomanip> // For formatting output=(Input/Output Manipulators)Control how things are shown on the screen 

using namespace std;

double getInput(string prompt) {
    double value;
    cout << prompt <<endl ;
    cin >> value;
    return value;
}

// Helper function to ask yes/no questions
bool askYesNo(string question) {
    char response;
    cout << question << " (y/n): ";
    cin >> response;
    return (response == 'y' || response == 'Y');
}

// Function to print the expense report in a table format
void printExpenseReportTable(
    const string &name,
    int age,
    const string &occupation,
    double rent,
    double electricity,
    double gas,
    double subscriptions,
    double entertainment,
    double groceries,
    double traveling,
    double transport,
    double personalCare,
    double selectedAmount,
    double totalExpenses,
    double budget 
) {
    cout << "\n--- Expense Report Table for " << name << " ---\n";
    cout << setw(25) << left << "Category" << "Amount\n";
    cout << string(35, '-') << "\n";

    cout << setw(25) << left << "Rent" << rent << "\n";// manipulators — special functions provided by the <iomanip>
    cout << setw(25) << left << "Electricity" << electricity << "\n";
    cout << setw(25) << left << "Gas" << gas << "\n";
    cout << setw(25) << left << "Subscriptions" << subscriptions << "\n";
    cout << setw(25) << left << "Entertainment" << entertainment << "\n";
    cout << setw(25) << left << "Groceries" << groceries << "\n";
    cout << setw(25) << left << "Traveling" << traveling << "\n";
    cout << setw(25) << left << "Transport" << transport << "\n";
    cout << setw(25) << left << "Personal Care" << personalCare << "\n";

    cout << setw(25) << left <<  "financialChoice" << selectedAmount << "\n";

    cout << string(35, '-') << "\n";
    cout << setw(25) << left << "Total Expenses" << totalExpenses << "\n";

    if (budget >= 0) {
        double remaining = budget - totalExpenses;
        cout << setw(25) << left << "Remaining Budget" << remaining << "\n";
        if (totalExpenses > budget) {
            cout << "Warning! You have exceeded your budget!\n";
        } else {
            cout << "You are within your budget!\n";
        }
    } else {
        cout << "Budget not set.\n";
    }

    cout << "----------------------------------------------\n";
    cout << "Thank you, " << name << "! Keep tracking your expenses.\n";
}

void runExpenseCalculator(string name, int age, string occupation, double budget) {
    double rent = 0, electricity = 0, gas = 0, subscriptions = 0;
    double entertainment = 0, groceries = 0, traveling = 0, transport = 0, personalCare = 0;
    double selectedAmount = 0, totalExpenses = 0;
    int financialChoice;

    if (askYesNo("Do you want to enter Rent amount?")) {
        rent = getInput("Enter Rent amount: ");
    }
    if (askYesNo("Do you want to enter Electricity bill amount?")) {
        electricity = getInput("Enter Electricity bill amount: ");
    }
    if (askYesNo("Do you want to enter Gas bill amount?")) {
        gas = getInput("Enter Gas bill amount: ");
    }
    if (askYesNo("Do you want to enter Subscription charges?")) {
        subscriptions = getInput("Enter Subscription charges: ");
    }
    if (askYesNo("Do you want to enter Entertainment budget?")) {
        entertainment = getInput("Enter Entertainment budget: ");
    }
    if (askYesNo("Do you want to enter Groceries budget?")) {
        groceries = getInput("Enter Groceries budget: ");
    }
    if (askYesNo("Do you want to enter Traveling budget?")) {
        traveling = getInput("Enter Traveling budget: ");
    }
    if (askYesNo("Do you want to enter Transport budget?")) {
        transport = getInput("Enter Transport budget: ");
    }
    if (askYesNo("Do you want to enter Personal Care budget?")) {
        personalCare = getInput("Enter Personal Care budget: ");
    }

    cout << "\nChoose one financial option:\n";
    cout << "1. Savings\n2. Insurance\n3. Investments\nEnter choice: ";
    cin >> financialChoice;
    
        // Show selected financial option
  

    switch (financialChoice) {
        case 1:
            if (askYesNo("Do you want to enter Savings amount?")) {
                selectedAmount = getInput("Enter Savings amount: ");
            }
            break;
        case 2:
            if (askYesNo("Do you want to enter Insurance amount?")) {
                selectedAmount = getInput("Enter Insurance amount: ");
            }
            break;
        case 3:
            if (askYesNo("Do you want to enter Investment amount?")) {
                selectedAmount = getInput("Enter Investment amount: ");
            }
            break;
        default:
            cout << "Invalid choice. Setting financial option to 0.\n";
            selectedAmount = 0;
    }

    totalExpenses = rent + electricity + gas + subscriptions +
                    entertainment + groceries + traveling + transport + personalCare +
                    selectedAmount;

    cout << "\n--- Expense Report for " << name << " ---\n";

    // Call the new report table function
    printExpenseReportTable(
        name, age, occupation,
        rent, electricity, gas, subscriptions,
        entertainment, groceries, traveling, transport, personalCare,
        selectedAmount,
        totalExpenses,
        budget
    );
}

int main() {
    int choice;
    string name, occupation;
    int age;
    double budget;

    cout << "Welcome to Spending Smart!\n";
    cout << "Choose mode:\n1. Offline Mode\n2. Online Mode\nEnter choice: ";
    cin >> choice;
    cin.ignore(); // Avoid input skipping issues

    if (choice == 1) {
        cout << "--- OFFLINE MODE ---\n";
        cout << "Enter Name: ";
        getline(cin, name);
        cout << "Enter Age: ";
        cin >> age;
        cin.ignore();
        cout << "Enter Occupation: ";
        getline(cin, occupation);
    } else if (choice == 2) {
        cout << "--- ONLINE MODE ---\n";
        string email, accNum, pin;
        cout << "Enter Email/Phone: ";
        cin >> email;
        cout << "Enter Account Number: ";
        cin >> accNum;
        cout << "Enter PIN: ";
        cin >> pin;
        cout << "[Sign In Successful]\n";

        name = "User 1";
        age = 18;
        occupation = "Student";
    } else {
        cout << "Invalid choice.\n";
        return 1;
    }

    // Ask if user wants to enter budget
    char budgetChoice;
    cout << "Do you want to enter your total budget? (y/n): ";
    cin >> budgetChoice;

    if (budgetChoice == 'y' || budgetChoice == 'Y') {
        budget = getInput("Enter your total budget: ");
    } else {
        budget = -1;  // special value indicating no budget
    }

    runExpenseCalculator(name, age, occupation, budget);
    return 0;
}
