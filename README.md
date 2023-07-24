# project-3
Contact Management System :
It utilizes OOP principles to model contacts as objects with properties like name, email, phone number, etc. 



 
#include <iostream>
#include <unordered_map>
#include <string>

class Contact {
public:
    Contact() = default; // Default constructor

    Contact(const std::string& name, const std::string& email, const std::string& phone_number)
        : name(name), email(email), phone_number(phone_number) {}

    // Getters for contact properties
    const std::string& getName() const { return name; }
    const std::string& getEmail() const { return email; }
    const std::string& getPhoneNumber() const { return phone_number; }

private:
    std::string name;
    std::string email;
    std::string phone_number;
};

class ContactManager {
public:
    void addContact(const Contact& contact) {
        contacts[contact.getName()] = contact;
    }

    const Contact& getContact(const std::string& name) {
        static const Contact dummy_contact("", "", ""); // A dummy contact if not found
        auto it = contacts.find(name);
        if (it != contacts.end()) {
            return it->second;
        }
        return dummy_contact;
    }

    void deleteContact(const std::string& name) {
        contacts.erase(name);
    }

private:
    std::unordered_map<std::string, Contact> contacts; // Using unordered_map as a hash table
};

// Usage example:
int main() {
    ContactManager contactManager;

    // Adding contacts
    Contact contact1("John Doe", "john@example.com", "123-456-7890");
    Contact contact2("Jane Smith", "jane@example.com", "987-654-3210");

    contactManager.addContact(contact1);
    contactManager.addContact(contact2);

    // Getting a contact
    std::string search_name = "John Doe";
    const Contact& found_contact = contactManager.getContact(search_name);
    if (found_contact.getName() != "") {
        std::cout << "Contact Found: " << found_contact.getName() << ", "
                  << found_contact.getEmail() << ", " << found_contact.getPhoneNumber() << std::endl;
    } else {
        std::cout << "Contact not found." << std::endl;
    }

    return 0;
}
