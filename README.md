#include <iostream>
#include <iomanip>
#include <vector>
using namespace std;

struct TiketBioskop{
	string film;
	float harga;
	int jumlah;
};

void tampilkanMenu(){
	cout << "\nMenu Film:\n";
	cout << "1. Film A - Rp 50000\n";
	cout << "2. Film B - Rp 55000\n";
	cout << "3. Film C - Rp 60000\n";
	cout << "4. Film D - Rp 65000\n";
}

float hitungDiskon(int totalJumlah, float totalHarga){
	if (totalJumlah>=5){
		return totalHarga * 0.1; // Diskon 10% jika beli 5 tiket atau lebih
	}
	return 0;
}

int main() {
	vector<TiketBioskop>pesanan;
	int pilihan, jumlah, totalJumlah = 0;
	float totalHarga = 0;
	char lagi;
	
	cout << "Selamat Datang di Aplikasi Pembelian Tiket Bioskop!\n";
	
	do{
		tampilkanMenu();
		cout << "Pilih film (1-4): ";
		cin >> pilihan;
		
		TiketBioskop tiket;
		switch (pilihan){
			case 1:
				tiket={"Film A", 50000, 0};
				break;
			case 2:
				tiket={"Film B", 55000, 0};
				break;
			case 3:
				tiket={"Film C", 60000, 0};
				break;
			case 4:
				tiket={"Film D", 65000, 0};
				break;
			default:
				cout << "Pilihan tidak valid.\n";
				continue;
		}
		
		cout << "Masukkan jumlah tiket yang ingin dibeli:";
		cin >> jumlah;
		tiket.jumlah = jumlah;
		
		float subtotal = tiket.harga * jumlah;
		totalHarga += subtotal;
		totalJumlah += jumlah;
		pesanan.push_back(tiket);
		
		cout << "Subtotal untuk" << tiket.film << ":Rp" << subtotal << endl;
		
		cout << "Ingin membeli tiket film lain? (y/n): ";
		cin >> lagi;
		
	}while (lagi == 'y' || lagi == 'Y');
	
	float diskon = hitungDiskon(totalJumlah, totalHarga);
	float totalSetelahDiskon = totalHarga - diskon;
	
	cout << "\n--- Daftar Tiket yang Dibeli ---\n";
	cout << left << setw(15) << "Film" << setw(10) << "Harga" << setw(10) << "Jumlah" << setw(15) << "Subtotal" << endl;
	for (const TiketBioskop&t : pesanan){
		cout << left << setw(15) << t.film
			<< "Rp " << setw(8) << t.harga
			<< setw(10) << t.jumlah
			<< "Rp " << setw(10) << t.harga * t.jumlah << endl;
	}
	
	cout << "\nTotal Harga:Rp" << totalHarga << endl;
	cout << "Diskon: Rp " << diskon << endl;
	cout << "Total Setelah Diskon:Rp" << totalSetelahDiskon << endl;
	cout << "Terima kasih telat membeli tiket bioskop!\n";
	
	return 0;
	}
