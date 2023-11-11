#include <bits/stdc++.h>
#include <conio.h>
using namespace std;

// Structure for a candidate
struct Candidate {
    string name;
    int votes;
    Candidate* next;
};

// Structure for a student
struct Student {
    string name;
    string id;
    bool hasVoted;
    stack<int> voteHistory;  // Stack to store vote history
    Student* next;
};

// Function prototypes
Candidate* createCandidateList(int numCandidates);
void displayCandidates(Candidate* head);
Student* createStudentList(int numStudents);
void displayStudentStatus(Student* head);
bool checkValidStudent(Student* head, const string& studentID, const string& studentName);
bool hasStudentVoted(Student* head, const string& studentID);
void castVote(Candidate* head, Student* studentsHead, const string& studentID, int voteFor);
void displayResult(Candidate* head);
void undoLastVote(Student* studentsHead, Candidate* candidatesHead, int numCandidates);

int main() {
    int numCandidates, numStudents, voteFor, maxVotes = 0;
    string studentID, studentName, password;

    cout << endl << "                     Online Voting System / CR Election System                   " << endl;
    cout << "                     _________________________________________                   " << endl;
    cout << endl << "                        :::::::::: ADMIN PANEL ::::::::::" << endl;
    cout << "=================================================================================" << endl;
    cout << endl;
    cout << endl;
    cout << endl << "    Number of Candidate: ";
    cin >> numCandidates;

    // Create the linked list of candidates
    Candidate* candidatesHead = createCandidateList(numCandidates);

    cout << "    Number of Students: ";
    cin >> numStudents;

    // Create the linked list of students
    Student* studentsHead = createStudentList(numStudents);

    cout << endl << "  Thank You Admin! We are going to start our election with " << numStudents << " Students and " << numCandidates << " Candidates." << endl;
    cout << endl;
    cout << endl;
    cout << "=================================================================================" << endl;
    cout << endl;
    cout << endl;
    cout << "                            Enter The Password: ";
    cin >> password;

    while (password != "mypass") {
        cout << endl;
        cout << endl << "                            Wrong Password! Try Again." << endl;
        cout << endl;
        cout << "                       Enter The Correct Password: ";
        cin >> password;
        cout << endl;
    }

    system("CLS");

    for (int i = 1; i <= numStudents; i++) {
        cout << endl << "                     Online Voting System / CR Election System                   " << endl;
        cout << "                     _________________________________________                   " << endl;
        cout << endl << "                        :::::::::: VOTING PANEL ::::::::::" << endl;
        cout << endl << "                                   Student - " << i << endl;
        cout << "=================================================================================" << endl;
        cout << endl;
        cout << endl;

        // Display student vote status
        displayStudentStatus(studentsHead);

        cout << endl << "                  ===========================================" << endl;
        cout << endl;
        cout << endl;

        // Display candidates
        displayCandidates(candidatesHead);

        cout << endl << "                  ===========================================" << endl;
        cout << endl << "    Now, Please Put Your Vote:" << endl;

        // Take input for both name and ID
        cout << "    Enter Your Name: ";
        cin >> studentName;

        cout << "    Enter Your ID: ";
        cin >> studentID;

        // Check if the voteFor value is valid
        cout << "    Enter the candidate number you want to vote for: ";
        cin >> voteFor;

        while (voteFor < 1 || voteFor > numCandidates) {
            cout << "Invalid choice. Please enter a valid candidate number: ";
            cin >> voteFor;
        }

        // Check if the student has already voted
        while (!checkValidStudent(studentsHead, studentID, studentName) || hasStudentVoted(studentsHead, studentID)) {
            if (!checkValidStudent(studentsHead, studentID, studentName)) {
                cout << "Invalid ID or Name. Please enter a valid ID and Name." << endl;
            } else if (hasStudentVoted(studentsHead, studentID)) {
                cout << "You have already voted. Choose another ID." << endl;
            }

            // Take input again for both name and ID
            cout << "Enter Your Name: ";
            cin >> studentName;

            cout << "Enter Your ID: ";
            cin >> studentID;
        }

        // Cast the vote
        castVote(candidatesHead, studentsHead, studentID, voteFor);

        cout << endl;
        cout << endl;
        cout << endl << "                  Thanks " << studentName << " (" << studentID << ") For Your Vote. (Press Enter for Next)" << endl;
        cout << endl;
        cout << endl;
        cout << "=================================================================================" << endl;
        getch();
        system("CLS");

        // Offer the option to undo the last vote
        undoLastVote(studentsHead, candidatesHead, numCandidates);
    }

    // Display result
    displayResult(candidatesHead);

    getch();
}

// Function to create a linked list of candidates
Candidate* createCandidateList(int numCandidates) {
    Candidate* head = nullptr;
    Candidate* tail = nullptr;

    for (int i = 1; i <= numCandidates; i++) {
        Candidate* newCandidate = new Candidate;
        cout << "    Candidate-" << i << " Name: ";
        cin >> newCandidate->name;
        newCandidate->votes = 0;
        newCandidate->next = nullptr;

        if (head == nullptr) {
            head = newCandidate;
            tail = newCandidate;
        } else {
            tail->next = newCandidate;
            tail = newCandidate;
        }
    }

    return head;
}

// Function to display candidates
void displayCandidates(Candidate* head) {
    Candidate* current = head;
    int i = 1;

    while (current != nullptr) {
        cout << "                              Press " << i << " For " << current->name << endl;
        current = current->next;
        i++;
    }
}

// Function to create a linked list of students
Student* createStudentList(int numStudents) {
    Student* head = nullptr;
    Student* tail = nullptr;

    for (int i = 1; i <= numStudents; i++) {
        Student* newStudent = new Student;
        cout << "                             Student-" << i << " Name: ";
        cin >> newStudent->name;
        cout << "                             Enter Your ID: ";
        cin >> newStudent->id;
        newStudent->hasVoted = false;
        newStudent->next = nullptr;

        if (head == nullptr) {
            head = newStudent;
            tail = newStudent;
        } else {
            tail->next = newStudent;
            tail = newStudent;
        }
    }

    return head;
}

// Function to display student vote status
void displayStudentStatus(Student* head) {
    Student* current = head;

    while (current != nullptr) {
        cout << "    Name: " << current->name << " - ID: (Hidden) - Voted: " << (current->hasVoted ? "Yes" : "No") << endl;
        current = current->next;
    }
}

// Function to check if a student is valid
bool checkValidStudent(Student* head, const string& studentID, const string& studentName) {
    Student* current = head;

    while (current != nullptr) {
        if (current->id == studentID && current->name == studentName) {
            return true;  // Valid student
        }
        current = current->next;
    }

    return false;  // Invalid student
}

// Function to check if a student has already voted
bool hasStudentVoted(Student* head, const string& studentID) {
    Student* current = head;

    while (current != nullptr) {
        if (current->id == studentID && current->hasVoted) {
            return true;  // Student has already voted
        }
        current = current->next;
    }

    return false;  // Student has not voted yet
}

// Function to cast a vote
void castVote(Candidate* head, Student* studentsHead, const string& studentID, int voteFor) {
    Candidate* currentCandidate = head;
    Student* currentStudent = studentsHead;

    // Find the candidate to vote for
    for (int i = 1; i < voteFor; i++) {
        currentCandidate = currentCandidate->next;
    }

    // Cast the vote
    currentCandidate->votes++;

    // Mark the student as voted
    while (currentStudent != nullptr) {
        if (currentStudent->id == studentID) {
            currentStudent->hasVoted = true;
            currentStudent->voteHistory.push(voteFor);  // Store the vote in the history
            break;
        }
        currentStudent = currentStudent->next;
    }
}

// Function to display the election result
void displayResult(Candidate* head) {
    cout << endl << "                     Online Voting System / CR Election System                   " << endl;
    cout << "                     _________________________________________                   " << endl;
    cout << endl << "                        :::::::::: RESULT PANEL ::::::::::" << endl;
    cout << endl << "=================================================================================" << endl;
    cout << endl;
    cout << endl;
    cout << "                            Enter The Password: ";
    string password;
    cin >> password;

    while (password != "mypass") {
        cout << endl;
        cout << endl << "                            Wrong Password! Try Again." << endl;
        cout << endl;
        cout << "                       Enter The Correct Password: ";
        cin >> password;
        cout << endl;
    }

    cout << endl;
    cout << endl;
    cout << endl << "                  ===========================================" << endl;
    cout << endl;
    cout << endl;

    // Find the candidate with the maximum votes
    Candidate* current = head;
    Candidate* electedCandidate = head;

    while (current != nullptr) {
        cout << "                              " << current->name << " Get " << current->votes << " Vote." << endl;

        if (current->votes > electedCandidate->votes) {
            electedCandidate = current;
        }

        current = current->next;
    }

    cout << endl;
    cout << endl;
    cout << endl << "                  ===========================================" << endl;

    cout << endl;
    cout << endl << "           Congratulations " << electedCandidate->name << ". You are Elected as our new CR." << endl;
    cout << endl;
    cout << endl;
    cout << "=================================================================================" << endl;
}

// Function to undo the last vote
void undoLastVote(Student* studentsHead, Candidate* candidatesHead, int numCandidates) {
    // Get the last voted student
    Student* currentStudent = studentsHead;

    while (currentStudent != nullptr) {
        if (currentStudent->hasVoted) {
            cout << "Do you want to undo your last vote? (Y/N): ";
            char choice;
            cin >> choice;

            if (toupper(choice) == 'Y') {
                // Pop the last vote from the history
                if (!currentStudent->voteHistory.empty()) {
                    int lastVote = currentStudent->voteHistory.top();
                    currentStudent->voteHistory.pop();

                    // Find the candidate and decrement the vote
                    Candidate* currentCandidate = candidatesHead;

                    for (int i = 1; i < lastVote; i++) {
                        currentCandidate = currentCandidate->next;
                    }

                    currentCandidate->votes--;

                    cout << "Your last vote has been undone." << endl;

                    // Offer to vote again
                    cout << "Do you want to vote again? (Y/N): ";
                    cin >> choice;

                    if (toupper(choice) == 'Y') {
                        cout << "Enter the candidate number you want to vote for: ";
                        int revoteFor;
                        cin >> revoteFor;

                        while (revoteFor < 1 || revoteFor > numCandidates) {
                            cout << "Invalid choice. Please enter a valid candidate number: ";
                            cin >> revoteFor;
                        }

                        // Cast the new vote
                        currentStudent->voteHistory.push(revoteFor);
                        currentCandidate = candidatesHead;

                        for (int i = 1; i < revoteFor; i++) {
                            currentCandidate = currentCandidate->next;
                        }

                        currentCandidate->votes++;
                        cout << "Your vote has been cast for " << currentCandidate->name << "." << endl;
                    }
                }
            }
        }
        currentStudent = currentStudent->next;
    }
}
