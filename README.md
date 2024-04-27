#include <iostream>
#include <vector>
#include <algorithm>

using namespace std;

struct Task {
    string description;
    bool completed;

    Task(string desc) : description(desc), completed(false) {}
};

class ToDoList {
private:
    vector<Task> tasks;

public:
    void addTask(const string& description) {
        Task newTask(description);
        tasks.push_back(newTask);
        cout << "Task added successfully.\n";
    }

    void markTaskAsCompleted(int index) {
        if (index >= 0 && index < tasks.size()) {
            tasks[index].completed = true;
            cout << "Task marked as completed.\n";
        } else {
            cout << "Invalid task index.\n";
        }
    }

    void displayTasks() {
        if (tasks.empty()) {
            cout << "No tasks to display.\n";
            return;
        }

        cout << "Current Tasks:\n";
        for (size_t i = 0; i < tasks.size(); i++) {
            cout << i + 1 << ". ";
            if (tasks[i].completed) {
                cout << "[X] ";
            } else {
                cout << "[ ] ";
            }
            cout << tasks[i].description << endl;
        }
    }
};

int main() {
    ToDoList toDoList;
    int choice;
    string taskDescription;

    do {
        cout << "\nTo-Do List Application\n";
        cout << "1. Add Task\n";
        cout << "2. Mark Task as Completed\n";
        cout << "3. Display Tasks\n";
        cout << "4. Exit\n";
        cout << "Enter your choice: ";
        cin >> choice;

        switch (choice) {
            case 1:
                cout << "Enter task description: ";
                cin.ignore();
                getline(cin, taskDescription);
                toDoList.addTask(taskDescription);
                break;
            case 2:
                int taskIndex;
                cout << "Enter task index to mark as completed: ";
                cin >> taskIndex;
                toDoList.markTaskAsCompleted(taskIndex - 1); // Adjusting for 0-based indexing
                break;
            case 3:
                toDoList.displayTasks();
                break;
            case 4:
                cout << "Exiting the program.\n";
                break;
            default:
                cout << "Invalid choice.\n";
                break;
        }
    } while (choice != 4);

    return 0;
}
