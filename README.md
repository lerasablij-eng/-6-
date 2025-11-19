#include <windows.h>

BOOL APIENTRY DllMain(HMODULE hModule,
    DWORD  ul_reason_for_call,
    LPVOID lpReserved
)
{
    switch (ul_reason_for_call)
    {
    case DLL_PROCESS_ATTACH:
    case DLL_THREAD_ATTACH:
    case DLL_THREAD_DETACH:
    case DLL_PROCESS_DETACH:
        break;
    }
    return TRUE;
}

#define TRIANGLEDLL_EXPORTS
#include "TriangleDLL.h"
#include <iostream>
#include <cmath>

Triangle::Triangle() {
    std::cout << "Створено трикутник за замовчуванням\n";
}

Triangle::Triangle(double side) {
    std::cout << "Створено рівносторонній трикутник зі стороною: " << side << "\n";
}

Triangle::Triangle(double a, double b, double c) {
    std::cout << "Створено трикутник зі сторонами: " << a << ", " << b << ", " << c << "\n";
}

void Triangle::showInfo() {
    std::cout << "Інформація про трикутник\n";
}

#ifndef TRIANGLEDLL_H
#define TRIANGLEDLL_H

#ifdef TRIANGLEDLL_EXPORTS
#define TRIANGLEDLL_API __declspec(dllexport)
#else
#define TRIANGLEDLL_API __declspec(dllimport)
#endif

class TRIANGLEDLL_API Triangle {
public:
    Triangle();                              
    Triangle(double side);                   
    Triangle(double a, double b, double c);  

    void showInfo();
};

#endif

#pragma comment(lib, "TriangleDLL.lib")
#include <iostream>
#include <windows.h>
#include "TriangleDLL.h"

int main() {
    SetConsoleOutputCP(1251);
    SetConsoleCP(1251);

    std::cout << "Тестування DLL:\n\n";

    // Простий тест
    Triangle t1;
    t1.showInfo();

    Triangle t2(5.0);
    t2.showInfo();

    Triangle t3(3.0, 4.0, 5.0);
    t3.showInfo();

    system("pause");
    return 0;
}
