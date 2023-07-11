#include <iostream>
#include <string>
using namespace std;

class arrayy {
private:
    int* arr = nullptr;
    int size = 0;

public:

    arrayy(){}

    arrayy(int size) {
        this->size = size;
        arr = new int[size];
    }

    // Copy Constructor
    arrayy(const arrayy& obj) {
        size = obj.size;
        arr = new int[size];
        for (int i = 0; i < size; ++i) {
            arr[i] = obj.arr[i];
        }
    }

    // Move Constructor
    arrayy(arrayy&& obj) {
        size = obj.size;
        arr = obj.arr;
        obj.size = 0;
        obj.arr = nullptr;
        cout << "move constructor" << endl;
    }

    // Move Assignment Operator
    arrayy& operator=(arrayy&& obj){
        if (this != &obj) {
            delete[] arr;
            size = obj.size;
            arr = obj.arr;
            obj.size = 0;
            obj.arr = nullptr;
            cout << "move operator assigment" << endl;
        }
        return *this;
    }

    void get_element() {
        for (int i = 0; i < size; ++i) {
            arr[i] = 1;
        }

        for (int i = 0; i < size; ++i) {
            cout << arr[i];
        }
    }

    ~arrayy() {
        delete[] arr;
    }
};

int main() {
    int size;
    cin >> size;
    arrayy a(size);
    arrayy obj1 = a;
    a.get_element();
    arrayy obj = std::move(a);
    arrayy b;
    b = std::move(arrayy(2));
    return 0;
}
