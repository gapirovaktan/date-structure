#include <bits/stdc++.h>
using namespace std;

struct Date {
    int day, month, year;

    bool isValidDate() const {
        if (month < 1  month > 12  day < 1  year < 0)
            return false;

        if (month == 2) {
            if ((year % 4 == 0 && year % 100 != 0)  (year % 400 == 0)) {
                return day <= 29;
            } else {
                return day <= 28;
            }
        } else if (month == 4  month == 6  month == 9  month == 11) {
            return day <= 30;
        } else {
            return day <= 31;
        }
    }

    void newDate(int d, int m, int y) {
        day = d;
        month = m;
        year = y;
    }

    string getDayOfWeek() const {
        static const char* days[] = {"Sunday", "Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday"};
        static const int t[] = {0, 3, 2, 5, 0, 3, 5, 1, 4, 6, 2, 4};
        int y = year - (month < 3);
        int dayOfWeek = (y + y / 4 - y / 100 + y / 400 + t[month - 1] + day) % 7;
        return days[dayOfWeek];
    }

    int calculateDifference(const Date* date) const {
        return 0; 
    }

    void printDate() const {
        if (isValidDate()) {
            static const char* months[] = {"January", "February", "March", "April", "May", "June", "July", "August", "September", "October", "November", "December"};
            cout << months[month - 1] << " " << day << ", " << year;
        } else {
            cout << "Invalid Date";
        }
    }

    bool operator<(const Date& date) const {
        if (year != date.year)
            return year < date.year;
        if (month != date.month)
            return month < date.month;
        return day < date.day;
    }
};

int main() {
    vector<Date> dates;

    int day, month, year;

    cout << "Enter day, month, year first date(use space): ";
    cin >> day >> month >> year;

    while (day < 1  day > 31  month < 1  month > 12  year < 0) {
        cout << "Invalid Input. try again";
        cin >> day >> month >> year;
    }

    dates.push_back({day, month, year});

    cout << "Enter day, month, year second date (use space): ";
    cin >> day >> month >> year;

    while (day < 1  day > 31  month < 1  month > 12 || year < 0) {
        cout << "Invalid Input. try again: ";
        cin >> day >> month >> year;
    }

    dates.push_back({day, month, year});

    dates.erase(remove_if(dates.begin(), dates.end(), [](const Date& d) { return !d.isValidDate(); }), dates.end());

    sort(dates.begin(), dates.end());

    cout << "Dates\n";
    for (const auto& date : dates) {
        date.printDate();
        cout << ", " << date.getDayOfWeek() << endl;
    }

    return 0;
}
