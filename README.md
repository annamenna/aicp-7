# aicp-7
#include <iostream>
#include <vector>
#include <iomanip>
#include <algorithm>

using namespace std;

// Constants
const int NUM_CHARITIES = 3;

// Structure to store charity information
struct Charity {
    string name;
    double totalDonations;
};

// Function to set up the donation system
void setupDonationSystem(vector<Charity>& charities) {
    cout << "TASK 1 - Set up the donation system\n";

    for (int i = 0; i < NUM_CHARITIES; ++i) {
        cout << "Enter the name of Charity " << i + 1 << ": ";
        cin >> charities[i].name;
        charities[i].totalDonations = 0.0;
    }

    cout << "\nCharities:\n";
    for (int i = 0; i < NUM_CHARITIES; ++i) {
        cout << i + 1 << ". " << charities[i].name << endl;
    }
}

// Function to record and total each donation
void recordAndTotalDonation(vector<Charity>& charities) {
    cout << "\nTASK 2 - Record and total each donation\n";

    int choice;
    double shoppingBill;

    cout << "Enter the charity choice (1, 2, or 3, -1 to show totals): ";
    cin >> choice;

    while (choice != -1) {
        if (choice < 1 || choice > NUM_CHARITIES) {
            cout << "Invalid charity choice. Please enter 1, 2, or 3: ";
        } else {
            cout << "Enter the value of the customer's shopping bill: $";
            cin >> shoppingBill;

            // Calculate donation
            double donation = shoppingBill * 0.01;
            
            // Update total donation for the chosen charity
            charities[choice - 1].totalDonations += donation;

            // Output donation information
            cout << "Donation of $" << fixed << setprecision(2) << donation << " recorded for "
                 << charities[choice - 1].name << "\n";
        }

        cout << "Enter the charity choice (1, 2, or 3, -1 to show totals): ";
        cin >> choice;
    }
}

// Function to show the totals so far
void showTotals(const vector<Charity>& charities) {
    cout << "\nTASK 3 - Show the totals so far\n";

    // Sort charities by total donations in descending order
    vector<Charity> sortedCharities = charities;
    sort(sortedCharities.begin(), sortedCharities.end(),
         [](const Charity& a, const Charity& b) { return a.totalDonations > b.totalDonations; });

    // Display totals
    for (const auto& charity : sortedCharities) {
        cout << charity.name << ": $" << fixed << setprecision(2) << charity.totalDonations << endl;
    }

    // Calculate and display grand total
    double grandTotal = accumulate(sortedCharities.begin(), sortedCharities.end(), 0.0,
                                   [](double sum, const Charity& charity) { return sum + charity.totalDonations; });

    cout << "\nGRAND TOTAL DONATED TO CHARITY: $" << fixed << setprecision(2) << grandTotal << endl;
}

int main() {
    vector<Charity> charities(NUM_CHARITIES);

    // TASK 1 - Set up the donation system
    setupDonationSystem(charities);

    // TASK 2 - Record and total each donation
    recordAndTotalDonation(charities);

    // TASK 3 - Show the totals so far
    showTotals(charities);

    return 0;
}
