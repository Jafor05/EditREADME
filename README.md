#Calculator
/*
 * Calculator.cpp
 *
 *  Date: [9/12/2024]
 *  Author: [Jafor Ahmed]
 */

#include <iostream>

using namespace std;

int main()  // Ensure that only one main() function exists in your project.
{
    char answer = 'Y';  // Initialize with character 'Y'
    int op1, op2;
    char operation;

    while (answer == 'Y' || answer == 'y')  // Allow both 'Y' and 'y'
    {
        cout << "Enter expression (e.g., 2 + 2): " << endl;
        cin >> op1 >> operation >> op2;  // Correct input sequence for operator and operands

        // Addition
        if (operation == '+')
            cout << op1 << " + " << op2 << " = " << op1 + op2 << endl;

        // Subtraction
        else if (operation == '-')
            cout << op1 << " - " << op2 << " = " << op1 - op2 << endl;

        // Multiplication
        else if (operation == '*')
            cout << op1 << " * " << op2 << " = " << op1 * op2 << endl;

        // Division
        else if (operation == '/')
        {
            if (op2 == 0)  // Check for division by zero
                cout << "Error: Division by zero is undefined." << endl;
            else
                cout << op1 << " / " << op2 << " = " << op1 / op2 << endl;
        }
        else
        {
            cout << "Error: Invalid operator entered." << endl;  // Handle invalid operator
        }

        // Ask if the user wants to continue
        cout << "Do you wish to evaluate another expression? (Y/N): " << endl;
        cin >> answer;
    }

    cout << "Program Finished." << endl;
    return 0;  // Return 0 indicating the program executed successfully
}

##ChadaTechClock

Clock.cpp
// Clock.cpp
// Author: Jafor Ahmed
// Date: 2024-09-18
// Description: Source file for Clock class.

#include "Clock.h"
#include <iostream>

Clock::Clock(int h, int m, int s) : hours(h), minutes(m), seconds(s) {}

void Clock::setTime(int h, int m, int s) {
    hours = h;
    minutes = m;
    seconds = s;
}

Clock.h

// Clock.h
// Author: Jafor Ahmed
// Date: 2024-09-18
// Description: Header file for Clock class.

#ifndef CLOCK_H
#define CLOCK_H

class Clock {
protected:
    int hours;
    int minutes;
    int seconds;

public:
    Clock(int h = 0, int m = 0, int s = 0);
    virtual void displayTime() const = 0; // Pure virtual function
    void setTime(int h, int m, int s);
};

#endif
#pragma once

main.cpp

// main.cpp
// Author: Jafor Ahmed
// Date: 2024-09-18
// Description: Source file for Clock class.

#include <iostream>
#include "TwelveHourClock.h"
#include "TwentyFourHourClock.h"

int main() {
    TwelveHourClock twelveClock(14, 30, 45);  // Example: 2:30:45 PM
    TwentyFourHourClock twentyFourClock(14, 30, 45);

    std::cout << "12-Hour Clock: ";
    twelveClock.displayTime();

    std::cout << "24-Hour Clock: ";
    twentyFourClock.displayTime();

    // Allow user to input new time and update clocks
    int h, m, s;
    std::cout << "Enter new time (hours minutes seconds): ";
    std::cin >> h >> m >> s;

    twelveClock.setTime(h, m, s);
    twentyFourClock.setTime(h, m, s);

    std::cout << "Updated 12-Hour Clock: ";
    twelveClock.displayTime();

    std::cout << "Updated 24-Hour Clock: ";
    twentyFourClock.displayTime();

    return 0;
}

TwelveHourClock.cpp

// TwelveHourClock.cpp
// Author: Jafor Ahmed
// Date: 2024-09-18
// Description: Source file for Clock class.

#include "TwelveHourClock.h"
#include <iostream>
#include <iomanip>

TwelveHourClock::TwelveHourClock(int h, int m, int s) : Clock(h, m, s) {}

void TwelveHourClock::displayTime() const {
    int displayHour = hours % 12;
    displayHour = (displayHour == 0) ? 12 : displayHour; // Adjust for 12-hour format
    std::cout << std::setfill('0') << std::setw(2) << displayHour << ":"
        << std::setfill('0') << std::setw(2) << minutes << ":"
        << std::setfill('0') << std::setw(2) << seconds
        << (hours >= 12 ? " PM" : " AM") << std::endl;
}

TwelveHourClock.h
// TwelveHourClock.h
// Author: Jafor Ahmed
// Date: 2024-09-18
// Description: Header file for Clock class.

#ifndef TWELVEHOURCLOCK_H
#define TWELVEHOURCLOCK_H

#include "Clock.h"

class TwelveHourClock : public Clock {
public:
    TwelveHourClock(int h = 0, int m = 0, int s = 0);
    void displayTime() const override;
};

#endif

TwentyFourHourClock.h

// TwentyFourHourClock.h
// Author: Jafor Ahmed
// Date: 2024-09-18
// Description: Header file for Clock class.

#ifndef TWENTYFOURHOURCLOCK_H
#define TWENTYFOURHOURCLOCK_H

#include "Clock.h"

class TwentyFourHourClock : public Clock {
public:
    TwentyFourHourClock(int h = 0, int m = 0, int s = 0);
    void displayTime() const override;
};

#endif

TwentyFourHourClock.cpp

// TwentyFourHourClock.cpp
// Author: Jafor Ahmed
// Date: 2024-09-18
// Description: Source file for Clock class.

#include "TwentyFourHourClock.h"
#include <iostream>
#include <iomanip>

TwentyFourHourClock::TwentyFourHourClock(int h, int m, int s) : Clock(h, m, s) {}

void TwentyFourHourClock::displayTime() const {
    std::cout << std::setfill('0') << std::setw(2) << hours << ":"
        << std::setfill('0') << std::setw(2) << minutes << ":"
        << std::setfill('0') << std::setw(2) << seconds << std::endl;
}

###CornerGrocerProject

GroceryTracker.h

#pragma#ifndef GROCERYTRACKER_H
#define GROCERYTRACKER_H

#include <iostream>
#include <fstream>
#include <map>
#include <string>

class GroceryTracker {
private:
    std::map<std::string, int> itemFrequencies;  // Map to store item frequencies

public:
    GroceryTracker();  // Constructor
    void loadItems(const std::string& inputFileName);  // Load items from input file
    int getItemFrequency(const std::string& item);  // Get the frequency of a specific item
    void displayAllFrequencies();  // Display all item frequencies
    void displayHistogram();  // Display a histogram of frequencies
    void createBackupFile(const std::string& backupFileName);  // Create a backup file
};
GroceryTracker.cpp
#include "GroceryTracker.h"

GroceryTracker::GroceryTracker() {
    // Constructor implementation (if necessary)
}

void GroceryTracker::loadItems(const std::string& inputFileName) {
    std::ifstream inputFile(inputFileName);
    std::string item;
    if (inputFile.is_open()) {
        while (inputFile >> item) {
            itemFrequencies[item]++;
        }
        inputFile.close();
    }
    else {
        std::cerr << "Error: Unable to open input file." << std::endl;
    }
}

int GroceryTracker::getItemFrequency(const std::string& item) {
    if (itemFrequencies.find(item) != itemFrequencies.end()) {
        return itemFrequencies[item];
    }
    else {
        return 0;
    }
}

void GroceryTracker::displayAllFrequencies() {
    for (const auto& pair : itemFrequencies) {
        std::cout << pair.first << ": " << pair.second << std::endl;
    }
}

void GroceryTracker::displayHistogram() {
    for (const auto& pair : itemFrequencies) {
        std::cout << pair.first << " ";
        for (int i = 0; i < pair.second; ++i) {
            std::cout << "*";
        }
        std::cout << std::endl;
    }
}

void GroceryTracker::createBackupFile(const std::string& backupFileName) {
    std::ofstream backupFile(backupFileName);
    if (backupFile.is_open()) {
        for (const auto& pair : itemFrequencies) {
            backupFile << pair.first << " " << pair.second << std::endl;
        }
        backupFile.close();
    }
    else {
        std::cerr << "Error: Unable to create backup file." << std::endl;
    }
}

main.cpp

#include "GroceryTracker.h"
#include <iostream>

int main() {
    GroceryTracker tracker;

    // Load items from the input file
    tracker.loadItems("CS210_Project_Three_Input_File.txt");

    // Create a backup of the item frequencies
    tracker.createBackupFile("frequency.dat");

    // Menu and logic here...

    return 0;
}

####TemperatureConversion

#include <iostream>
#include <fstream>
#include <string>

int main() {
    // Open the input file (FahrenheitTemperature.txt) for reading
    std::ifstream inputFile("FahrenheitTemperature.txt");
    if (!inputFile) {
        std::cerr << "Error opening FahrenheitTemperature.txt!" << std::endl;
        return 1;
    }

    // Open the output file (CelsiusTemperature.txt) for writing
    std::ofstream outputFile("CelsiusTemperature.txt");
    if (!outputFile) {
        std::cerr << "Error creating CelsiusTemperature.txt!" << std::endl;
        return 1;
    }

    // Variables to store city name and temperature in Fahrenheit
    std::string city;
    int tempF;
    double tempC;

    // Read each line from the input file, convert the temperature, and write to the output file
    while (inputFile >> city >> tempF) {
        // Convert Fahrenheit to Celsius: (F - 32) * 5 / 9 = C
        tempC = (tempF - 32) * 5.0 / 9.0;
        // Write the city and temperature in Celsius to the output file
        outputFile << city << " " << tempC << std::endl;
    }

    // Close both files
    inputFile.close();
    outputFile.close();

    std::cout << "Temperature conversion completed. Check CelsiusTemperature.txt for results." << std::endl;

    return 0;
}

#####InvestmentCalculator

InvestmentCalculator.h
#pragma once
#ifndef AIRGEAD_BANKING_INVESTMENTCALCULATOR_H_
#define AIRGEAD_BANKING_INVESTMENTCALCULATOR_H_

class InvestmentCalculator {
private:
    // Private member variables to hold investment details
    double m_initialAmount;
    double m_monthlyDeposit;
    double m_annualInterest;
    int m_years;

    // Private methods for compound interest calculation
    double calculateMonthlyInterest(double balance, double monthlyDeposit);

public:
    // Constructor
    InvestmentCalculator(double initialAmount, double monthlyDeposit, double annualInterest, int years);

    // Method to calculate and display the investment growth without additional deposits
    void displayWithoutMonthlyDeposits();

    // Method to calculate and display the investment growth with monthly deposits
    void displayWithMonthlyDeposits();
};

#endif // AIRGEAD_BANKING_INVESTMENTCALCULATOR_H_


InvestmentCalculator

#include "InvestmentCalculator.h"
#include <iostream>

using namespace std;

// Function to get user input
double getInput(string prompt) {
    double value;
    cout << prompt;
    while (!(cin >> value) || value <= 0) {
        cout << "Please enter a valid positive number.\n";
        cin.clear();
        cin.ignore(1000, '\n');
        cout << prompt;
    }
    return value;
}

int main() {
    // Get user inputs
    double initialInvestment = getInput("Initial Investment Amount: ");
    double monthlyDeposit = getInput("Monthly Deposit: ");
    double annualInterest = getInput("Annual Interest (in %): ");
    int years = static_cast<int>(getInput("Number of Years: "));

    // Display a message to the user to continue
    cout << "\nPress any key to continue...\n";
    cin.ignore();
    cin.get();

    // Create an instance of InvestmentCalculator and display results
    InvestmentCalculator calculator(initialInvestment, monthlyDeposit, annualInterest, years);

    // Display results without additional monthly deposits
    calculator.displayWithoutMonthlyDeposits();

    // Display results with additional monthly deposits
    calculator.displayWithMonthlyDeposits();

    return 0;
}

Main.cpp

#include "InvestmentCalculator.h"
#include <iostream>

using namespace std;

// Function to get user input
double getInput(string prompt) {
    double value;
    cout << prompt;
    while (!(cin >> value) || value <= 0) {
        cout << "Please enter a valid positive number.\n";
        cin.clear();
        cin.ignore(1000, '\n');
        cout << prompt;
    }
    return value;
}

int main() {
    // Get user inputs
    double initialInvestment = getInput("Initial Investment Amount: ");
    double monthlyDeposit = getInput("Monthly Deposit: ");
    double annualInterest = getInput("Annual Interest (in %): ");
    int years = static_cast<int>(getInput("Number of Years: "));

    // Display a message to the user to continue
    cout << "\nPress any key to continue...\n";
    cin.ignore();
    cin.get();

    // Create an instance of InvestmentCalculator and display results
    InvestmentCalculator calculator(initialInvestment, monthlyDeposit, annualInterest, years);

    // Display results without additional monthly deposits
    calculator.displayWithoutMonthlyDeposits();

    // Display results with additional monthly deposits
    calculator.displayWithMonthlyDeposits();

    return 0;
}
