// ============================================================
//  Bai2_MaTran2D.cpp
//  Noi dung: Nhan 2 ma tran n×n + Tinh dinh thuc 3×3
//  Giao trinh: Cau truc du lieu & Giai thuat
// ============================================================
#include <iostream>
#include <iomanip>
using namespace std;

// ============================================================
//  HAM TIEN ICH
// ============================================================

// Nhap ma tran n×n
void NhapMaTran(float a[][20], int n, const string &ten = "") {
    cout << "\n  Nhap ma tran " << ten << " (" << n << "x" << n << "):\n";
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < n; j++) {
            cout << "    " << ten << "[" << i << "][" << j << "] = ";
            cin >> a[i][j];
        }
    }
}

// Xuat ma tran n×n
void XuatMaTran(float a[][20], int n, const string &ten = "") {
    cout << "\n  Ma tran " << ten << " =\n";
    cout << "  ┌";
    for (int j = 0; j < n; j++) cout << "          ";
    cout << "┐\n";
    
    for (int i = 0; i < n; i++) {
        cout << "  │";
        for (int j = 0; j < n; j++) {
            cout << setw(10) << fixed << setprecision(2) << a[i][j];
        }
        cout << " │\n";
    }
    
    cout << "  └";
    for (int j = 0; j < n; j++) cout << "          ";
    cout << "┘\n";
}

// ============================================================
//  PHAN 1: NHAN HAI MA TRAN n×n - O(n^3)
// ============================================================

void NhanHaiMaTran(float a[][20], float b[][20], float c[][20], int n) {
    // Khoi tao ma tran C bang 0
    for (int i = 0; i < n; i++)
        for (int j = 0; j < n; j++)
            c[i][j] = 0;
    
    // Tinh C = A × B
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < n; j++) {
            for (int k = 0; k < n; k++) {
                c[i][j] += a[i][k] * b[k][j];
            }
        }
    }
}

void DemoNhanMaTran() {
    cout << "\n" << string(63, '=') << "\n";
    cout << "  DEMO 1: NHAN HAI MA TRAN n×n\n";
    cout << string(63, '=') << "\n";
    
    int n;
    cout << "\n  Nhap kich thuoc ma tran A va B (1-20): ";
    cin >> n;
    
    if (n <= 0 || n > 20) {
        cout << "  Kich thuoc khong hop le!\n";
        return;
    }
    
    float A[20][20], B[20][20], C[20][20];
    
    NhapMaTran(A, n, "A");
    NhapMaTran(B, n, "B");
    
    XuatMaTran(A, n, "A");
    XuatMaTran(B, n, "B");
    
    cout << "\n" << string(63, '-') << "\n";
    cout << "  PHEP NHAN: C = A × B\n";
    cout << string(63, '-') << "\n";
    
    NhanHaiMaTran(A, B, C, n);
    
    XuatMaTran(C, n, "C");
}

// ============================================================
//  PHAN 2: TINH DINH THUC MA TRAN 3��3
// ============================================================

// Tinh dinh thuc ma tran 2×2
float DinhThuc2x2(float a[][20], int i1, int j1, int i2, int j2) {
    return a[i1][j1] * a[i2][j2] - a[i1][j2] * a[i2][j1];
}

// Tinh dinh thuc ma tran 3×3 bang khai trien theo hang 1
float DinhThuc3x3(float a[][20]) {
    float det = 0;
    
    // M1 = a[1][1]*a[2][2] - a[1][2]*a[2][1]
    float M1 = DinhThuc2x2(a, 1, 1, 2, 2);
    
    // M2 = a[1][0]*a[2][2] - a[1][2]*a[2][0]
    float M2 = DinhThuc2x2(a, 1, 0, 2, 2);
    
    // M3 = a[1][0]*a[2][1] - a[1][1]*a[2][0]
    float M3 = DinhThuc2x2(a, 1, 0, 2, 1);
    
    // det = a[0][0]*M1 - a[0][1]*M2 + a[0][2]*M3
    det = a[0][0] * M1 - a[0][1] * M2 + a[0][2] * M3;
    
    cout << "\n  Cac buoc tinh:\n";
    cout << "    M1 = a[1][1]×a[2][2] - a[1][2]×a[2][1]\n";
    cout << "       = " << a[1][1] << "×" << a[2][2] << " - " << a[1][2] << "×" << a[2][1] 
         << " = " << M1 << "\n\n";
    
    cout << "    M2 = a[1][0]×a[2][2] - a[1][2]×a[2][0]\n";
    cout << "       = " << a[1][0] << "×" << a[2][2] << " - " << a[1][2] << "×" << a[2][0] 
         << " = " << M2 << "\n\n";
    
    cout << "    M3 = a[1][0]×a[2][1] - a[1][1]×a[2][0]\n";
    cout << "       = " << a[1][0] << "×" << a[2][1] << " - " << a[1][1] << "×" << a[2][0] 
         << " = " << M3 << "\n\n";
    
    cout << "    det(A) = a[0][0]×M1 - a[0][1]×M2 + a[0][2]×M3\n";
    cout << "           = " << a[0][0] << "×(" << M1 << ") - " << a[0][1] << "×(" << M2 
         << ") + " << a[0][2] << "×(" << M3 << ")\n";
    cout << "           = " << fixed << setprecision(2) << det << "\n";
    
    return det;
}

void DemoDinhThuc() {
    cout << "\n" << string(63, '=') << "\n";
    cout << "  DEMO 2: TINH DINH THUC MA TRAN 3×3\n";
    cout << string(63, '=') << "\n";
    
    float A[20][20];
    
    NhapMaTran(A, 3, "A");
    XuatMaTran(A, 3, "A");
    
    cout << "\n" << string(63, '-') << "\n";
    cout << "  TINH DINH THUC: det(A)\n";
    cout << string(63, '-') << "\n";
    
    float det = DinhThuc3x3(A);
    
    cout << "\n" << string(63, '-') << "\n";
    cout << "  KET QUA: det(A) = " << fixed << setprecision(2) << det << "\n";
    if (det != 0) {
        cout << "  => Ma tran A co nghich dao\n";
    } else {
        cout << "  => Ma tran A KHONG co nghich dao (dinh thuc = 0)\n";
    }
    cout << string(63, '-') << "\n";
}

// ============================================================
//  MAIN
// ============================================================
int main() {
    cout << "\n============================================================\n";
    cout << "  BAI 2: MA TRAN 2D - NHAN MA TRAN + DINH THUC\n";
    cout << "============================================================\n";
    
    int chon;
    do {
        cout << "\n  MENU:\n";
        cout << "    1. Nhan hai ma tran n×n\n";
        cout << "    2. Tinh dinh thuc ma tran 3×3\n";
        cout << "    3. Thoat\n";
        cout << "  Chon (1-3): ";
        cin >> chon;
        
        switch (chon) {
            case 1:
                DemoNhanMaTran();
                break;
            case 2:
                DemoDinhThuc();
                break;
            case 3:
                cout << "\n  Tam biet!\n";
                break;
            default:
                cout << "  Lua chon khong hop le!\n";
        }
    } while (chon != 3);
    
    cout << "\n============================================================\n";
    return 0;
}
