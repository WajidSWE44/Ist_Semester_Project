#include<iostream>
#include<conio.h>
using namespace std;
class ATM {
private:
    int balance;
    int pinCode,success;
public:
    ATM(int bal, int pin) {
        balance = bal;
        pinCode = pin;
    }
    int getBalance() {
        return balance;
    }
    bool withdraw(int amount, int pin) {
        if (pin != pinCode || amount > balance) {
            return false;
        }
        balance -= amount;
        return true;
    }
    void deposit(int amount) {
        balance += amount;
    }
    bool transfer(int amount, ATM receiver, int pin){
        if(pin != pinCode){
            return false;
        }
        success = withdraw(amount, pin);
        if(success){
            receiver.deposit(amount);
            return true;
        }
        else{
            return false;
        }
    }
   
};

class ATMInterface {
public:
    static void displayMenu() {
        cout << "\n\n\t\t\t\t\tWELCOME IN ATM MACHINE\n\n";
        cout << "\t\t\t\t ================================\n";
        cout << "\t\t\t\t| 1. VIEW BALANCE                |\n";
        cout << "\t\t\t\t| 2. CASH WITHDRAW               |\n";
        cout << "\t\t\t\t| 3. CASH DEPOSIT                |\n";
        cout << "\t\t\t\t| 4. CASH TRANSFER               |\n";
        cout << "\t\t\t\t| 5. EXIT                        |\n";
        cout << "\t\t\t\t ===============================\n";
    }

    static void performTransaction(ATM& atm) {
        int choice, amount, pin, success;
        char op;

        do {
            

            cout << "\n\tEnter your choice: ";
            cin >> choice;

            switch (choice) {
            case 1:
                cout << "Your Balance: " << atm.getBalance() << endl;
                break;

            case 2:
                cout << "Your Available Balance: " << atm.getBalance() << endl;
                cout << "Enter the Amount to Withdraw: ";
                cin >> amount;
                success = atm.withdraw(amount, 7867);
                if (success) {
                    cout << "Withdraw Successful..." << endl;
                }
                else {
                    cout << "Insufficient Balance..." << endl;
                }
                break;

            case 3:
                cout << "Enter the Amount to Deposit: ";
                cin >> amount;
                atm.deposit(amount);
                cout << "Deposit successful..." << endl;
                break;

            case 4:
                cout << "Your Balance: " << atm.getBalance() << endl;
                cout << "Enter the Amount to Transfer: ";
                cin >> amount;
                cout << "Enter Pin Code: ";
                cin >> pin;
                success = atm.transfer(amount, atm, pin);
                if (success) {
                    cout << "Transfer Successfully..." << endl;
                }
                else {
                    cout << "Invalid PinCode or Insufficient Balance..." << endl;
                }
                break;

            case 5:
                cout << "Thanks for using ATM" << endl;
                exit(0);
                break;

            default:
                cout << "Invalid choice." << endl;
            }
             
            cout << "\nDo You want to Try Another Transaction [Y / N]: ";
            cin >> op;
        } while (op == 'y' || op == 'Y');
    }
};

int main() {
    ATM atm(5000, 7867);

    cout << "\n\n\n\n\n\n\t\t\t\t =========================================================\n";
    cout << "\t\t\t\t|                                                         |\n";
    cout << "\t\t\t\t|                                                         |\n";
    cout << "\t\t\t\t|            PROJECT PROGRAMMING FUNDAMENTAL              |\n";
    cout << "\t\t\t\t|                                                         |\n";
    cout << "\t\t\t\t|               DEVELOPED BY: WAJID ALI                   |\n";
    cout << "\t\t\t\t|               ID NO     :  23SW044                      |\n";
    cout << "\t\t\t\t|                                                         |\n";
    cout << "\t\t\t\t =========================================================\n";
    getch();
    system("cls"); 
    
    ATMInterface::displayMenu();
    ATMInterface::performTransaction(atm);

    return 0;
}

