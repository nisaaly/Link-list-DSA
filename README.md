#include <iostream>

using namespace std;

// Node structure for the linked list
struct Node {
    int data;
    Node* next;
};

// LinkedList class
class LinkedList {
private:
    Node* head;

public:
    // Constructor
    LinkedList() {
        head = NULL;
    }

    // Function to insert a new node at the nth position
    void insertAtN(int position, int value) {
        Node* newNode = new Node;
        newNode->data = value;
        newNode->next = NULL;

        if (position == 1) {
            newNode->next = head;
            head = newNode;
            return;
        }

        Node* temp = head;
        for (int i = 1; i < position - 1 && temp != NULL; ++i) {
            temp = temp->next;
        }

        if (temp == NULL) {
            cout << "Invalid position." << endl;
            return;
        }

        newNode->next = temp->next;
        temp->next = newNode;
    }

    // Function to update the value at the nth position
    void updateN(int position, int value) {
        Node* temp = head;
        for (int i = 1; i < position && temp != NULL; ++i) {
            temp = temp->next;
        }

        if (temp == NULL) {
            cout << "Invalid position." << endl;
            return;
        }

        temp->data = value;
    }

    // Function to search for a value in the linked list
    bool search(int value) {
        Node* temp = head;
        while (temp != NULL) {
            if (temp->data == value) {
                return true; // Value found
            }
            temp = temp->next;
        }
        return false; // Value not found
    }

    // Function to delete the first node
    void deleteFromBeginning() {
        if (head == NULL) {
            cout << "List is empty." << endl;
            return;
        }

        Node* temp = head;
        head = head->next;
        delete temp;
    }

    // Function to delete the last node
    void deleteFromEnd() {
        if (head == NULL) {
            cout << "List is empty." << endl;
            return;
        }

        if (head->next == NULL) {
            delete head;
            head = NULL;
            return;
        }

        Node* temp = head;
        while (temp->next->next != NULL) {
            temp = temp->next;
        }

        delete temp->next;
        temp->next = NULL;
    }

    // Function to delete a node from the nth position
    void deleteFromN(int position) {
        if (head == NULL) {
            cout << "List is empty." << endl;
            return;
        }

        if (position == 1) {
            Node* temp = head;
            head = head->next;
            delete temp;
            return;
        }

        Node* temp = head;
        for (int i = 1; i < position - 1 && temp != NULL; ++i) {
            temp = temp->next;
        }

        if (temp == NULL || temp->next == NULL) {
            cout << "Invalid position." << endl;
            return;
        }

        Node* toDelete = temp->next;
        temp->next = temp->next->next;
        delete toDelete;
    }

    // Function to display the linked list
    void display() {
        Node* temp = head;
        while (temp != NULL) {
            cout << temp->data << " ";
            temp = temp->next;
        }
        cout << endl;
    }
};

int main() {
    LinkedList myList;

    myList.insertAtN(1, 10);
    myList.insertAtN(2, 20);
    myList.insertAtN(3, 30);

    cout << "Original List: ";
    myList.display();

    myList.updateN(2, 25);

    cout << "List after updating at position 2: ";
    myList.display();

    if (myList.search(25)) {
        cout << "Value 25 found in the list." << endl;
    } else {
        cout << "Value 25 not found in the list." << endl;
    }

    myList.deleteFromBeginning();

    cout << "List after deleting from the beginning: ";
    myList.display();

    myList.deleteFromEnd();

    cout << "List after deleting from the end: ";
    myList.display();

    myList.deleteFromN(2);

    cout << "List after deleting from position 2: ";
    myList.display();

    return 0;
}


