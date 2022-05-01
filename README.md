#include <iostream>
#include <string>
#include <fstream>
#include <iomanip>
#include <string>
#include <cctype>
#include <ctime>
#define ROWS 6
#define SEATS 4

using namespace std;
string input, name, destination, date;
string destinations[] =
{
    "samarqand","buxoro","jizzax","xiva","xorazm","navoiy","namangan","andijon","qarshi","termiz","nukus"
};
void getname()
{
    bool correct = false;
    while (correct == false)
    {
        cout << "\nEnter your first name: ";

        cin >> input;

        //checking input for first name
        //Checking first name for typos
        correct = true;
        for (int i = 0; i < input.length(); i++)
        {
            if ((isalpha(input[i]) == 0) || (input.length() < 4))
            {
                correct = false;
                break;
            }
        }
        if (correct == false)
            cout << "Please, enter your name correctly." << endl;
        else
        {
            input[0] = toupper(input[0]);
            for (int i = 1; i < input.length(); i++)
                input[i] = tolower(input[i]);
            name += input;
        }
    }
    correct = false;
    while (correct == false)
    {
        cout << "\nEnter your last name: ";
        string input;
        cin >> input;


        correct = true;
        for (int i = 0; i < input.length(); i++)
        {
            if ((isalpha(input[i]) == 0) || (input.length() < 4))
            {
                correct = false;
                break;
            }
        }
        if (correct == false)
            cout << "Please, enter your name correctly." << endl;
        else
        {
            input[0] = toupper(input[0]);
            for (int i = 1; i < input.length(); i++)
                input[i] = tolower(input[i]);
            name += ' ' + input;
        }
    }
}
void Greeting()
{
    system("cls");
    cout << setfill('_') << setw(121) << '\n' << endl;
    cout << setfill(' ') << setw(70) << "Welcome to Delta!" << endl;
    cout << setfill('_') << setw(121) << '\n' << endl;
    cout << endl;
}
void InputDestination()
{
    bool correct = false;
    while (correct == false && destination == "")
    {

        cout << "\nEnter the destination: ";
        string input;
        cin >> input;

        correct = true;
        for (int i = 0; i < input.length(); i++)
        {
            if (isalpha(input[i]) == false || input.length() < 4)
            {
                correct = false;
                break;
            }
        }
        if (correct == false)
        {
            cout << "Please, enter distinct place." << endl;
            continue;
        }


        bool available = false;

        for (int i = 0; i < input.length(); i++)
            input[i] = tolower(input[i]);
        for (int i = 0; i < 100; i++)
        {
            if (input == destinations[i])
            {
                available = true;
                for (int j = 0; j < input.length(); j++)
                    destination += toupper(input[j]);
            }
        }
        if (available == false)
        {
            cout << "Unfortunately we don't fly to this destination." << endl;
            cout << "Choose another one." << endl;

            correct = false;
        }
    }
}
void pricelist()
{
    cout << setfill('_') << setw(121) << '\n' << endl;
    cout << setfill(' ') << setw(70) << "Price list" << endl;
    cout << setfill('_') << setw(121) << '\n' << endl;
    cout <<endl<< " 1.Nukus(40 $)\n 2.Xiva(38 $)\n 3.Xorazm(35 $)\n 4.Buxoro(30 $)\n 5.Navoiy(27 $)\n 6.Buxoro(25 $)\n 7.Samarqand(20 $)\n 8.Jizzax(15 $)\n 9.Namangan(13 $)\n 10.Andijon(15 $)\n 11.Qarshi(27 $)\n 12.Termiz(30 $)\n " << endl;
}
void InputDate()
{
    string input, name, destination, date;
    bool correct = false;
    while (correct == false && date == "")
    {
        cout << "\nEnter the day of departure in this month: ";
        string input;
        cin >> input;

        //checking input
        //Checking date for typo or for existence
        if (input.length() == 1)
        {
            input += input[0];
            input[0] = '0';
        }
        int date = 0;
        if (isdigit(input[0]) && isdigit(input[1]) && (input.length() < 3))
            date = stoi(input);
        if (date < 1 || date > 31)
            correct = false;
        else
            correct = true;
        if (correct == false)
            cout << "Please, enter valid date." << endl;
        else
            cout << input << ".05.22" << endl;
    }
}

unsigned int count_seats(char seats[ROWS][SEATS]);
void int_seats(char array[][SEATS], int elements)
{
    int i, j;
    for (i = 0; i < elements; i++)
    {
        for (j = 0; j < SEATS; j++)
        {
            array[i][j] = 'O';
        }
    }
    return;
}
unsigned int count_seats(char seats[ROWS][SEATS])
{
    unsigned int seat_count = 0, i, j;
    for (i = 0; i < ROWS; i++)
    {
        for (j = 0; j < SEATS; j++)
        {
            if (seats[i][j] == 'O')
            {
                seat_count++;
            }
        }
    }
    return seat_count;
}
void seat_map(char seats[ROWS][SEATS])
{
    unsigned int i, j;
    cout << setfill('_') << setw(121) << '\n' << endl;
    cout << setfill(' ') << setw(70) << "SEAT MAP" << endl;
    cout << setfill('_') << setw(121) << '\n' << endl;
    cout << "Seat ";
    for (j = 0; j < SEATS; j++)
    {
        if (j == 2)
            cout << "  ";
        cout << setw(2) << j + 1;
    }
    cout << endl << endl;
    for (i = 0; i < ROWS; i++)
    {
        cout << "Row";
        cout << setw(2) << i + 1;
        for (j = 0; j < SEATS; j++)
        {
            if (j == 2)
                cout << "  ";
            cout << setw(2) << seats[i][j];
        }
        cout << endl;
    }
    return;
}
class Person
{
private:


public:

    friend void getData();
    friend void InputDestination();
    friend void ShowDestinations();
    friend void Reserve_seat();


};
void getData()
{
    
    getname();
    InputDestination();
    InputDate();
}
void Reserve_seat()
{

    char section[ROWS][SEATS] = { 0 };
    unsigned int i = 0, j = 0, row = 0, seat = 0, seats_avialable = 0;
    string answer;
    int_seats(section, ROWS);
    seats_avialable = count_seats(section);
    if (seats_avialable == 0)
    {
        cout << "Sorry. This flight is full" << endl;

    }
    cout << endl << "Do you want to buy a ticket?" << endl;
    getline(cin, answer);

    while (answer == "YES" || answer == "yes")
    {
        system("cls");
        pricelist();
        cout << setfill('*') << setw(121) << '\n' << endl;
        cout << setfill(' ') << setw(70) << "NOTICE" << endl;
        cout << endl;
        cout << setfill('*') << setw(121) << '\n' << endl;
        cout << "You should pay shown amount of money within 2 days or your purchase will be cancelled" << endl;
        cout << endl;
        cout << "There are " << seats_avialable << " seats avialable." << endl;
        cout << endl;
        cout << "Select your Seat" << endl << endl;
        seat_map(section);
        cout << "Enter the row and seat number: " << endl;
        cin >> row >> seat;
        cin.ignore(100, '\n');
        if (section[row - 1][seat - 1] == 'O')
        {
            section[row - 1][seat - 1] = 'X';
            seats_avialable--;
            getData();
            cout << "You purchased seat " << seat << " in row " << row << endl
                << "Thank you for your order" << endl << endl;
        }
        else
        {
            cout << "Sorry the seat is almost reserved " << endl;
        }
        cout << endl << "Do you want to buy another ticket?" << endl;
        cin >> answer;
        
    }
    

}

void writeFile(Person& p)
{
    ofstream ofile("Person.dat", ios::binary | ios::app);
    
    Reserve_seat();
    ofile.write((char*)(&p), sizeof(p));
    ofile.close();
}

     
 int main()
{
     Person p;
     Greeting();
     writeFile(p);

}
