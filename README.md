# Tr_toko-bangunan
Tugas rancang ASD

#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <windows.h>
#include <conio.h>
#include <time.h>
#define MAX 100



	void gotoxy(int x, int y){
		COORD coord;
		coord.X =x;
		coord.Y =y;
		SetConsoleCursorPosition(GetStdHandle(STD_OUTPUT_HANDLE), coord);
	}



	struct admin{
		char username[MAX];
		char password[MAX];
	};
	
	
	struct Produk{
		char namabarang[MAX];
		char kode[20];
		int harga;
		int stok;
	};
	
			void buatData() {
		    struct Produk produk;
		    char filename[MAX];
		    FILE *file;
		
		    printf("\nMasukkan Kode Produk: ");
		    scanf("%s", produk.kode);
		
		    printf("Masukkan Nama Produk: ");
		    scanf(" %[^\n]s", produk.namabarang);
		
		    printf("Masukkan Harga: ");
		    scanf("%d", &produk.harga);
		
		    printf("Masukkan Stok: ");
		    scanf("%d", &produk.stok);
		
		    printf("\nData berhasil dimasukkan.\n");
		
		    // Buka file dan simpan data
		    printf("\nMasukkan nama file: ");
		    scanf("%s", filename);
		
		    file = fopen(filename, "a");
		    if (file == NULL) {
		        printf("\nTerjadi kesalahan saat membuka file.\n");
		        return;
		    }
		
		    fprintf(file, "%s;%s;%d;%d\n", produk.kode, produk.namabarang, produk.harga, produk.stok);
		
		    fclose(file);
		}
		
		
		
		void lihatData() {
    struct Produk produk;
    char filename[MAX];
    FILE *file;

    // Buka file dan tampilkan data
    printf("\nMasukkan nama file: ");
    scanf("%s", filename);

    file = fopen(filename, "r");
    if (file == NULL) {
        printf("\nfile yang di cari tidak ada\n");
        return;
    }

    printf("\nData:\n");
    printf("Kode\tNama\t\tHarga\tStok\n");

    while (fscanf(file, "%[^;];%[^;];%d;%d\n", produk.kode, produk.namabarang, &produk.harga, &produk.stok) != EOF) {
        printf("%s\t%s\t\t%d\t%d\n", produk.kode, produk.namabarang, produk.harga, produk.stok);
    }

    fclose(file);
}


	
	void display(){
		printf("\n\n\n\n\n\n");
		gotoxy(10,8);
		printf("=======================================================");
		gotoxy(10,9);
		printf("=                MENU TOKO BANGUNAN                   =");
		gotoxy(10,10);
		printf("=======================================================");
		gotoxy(10,11);
		printf("=  1. Tambah data barang                              =");
		gotoxy(10,12);
		printf("=  2. Cek data barang                                 =");
		gotoxy(10,13);
		printf("=  3. Update data barang                              =");
		gotoxy(10,14);
		printf("=  4. Cari barang                                     =");
		gotoxy(10,15);
		printf("=  5. Sorting barang                                  =");
		gotoxy(10,16);
		printf("=  6. Keluar                                          =");
		gotoxy(10,17);
		printf("=======================================================");
		gotoxy(10,18);
	}
		 
		 
		

	int main(){
		struct admin user;
		
		 	
		 	//set username dan pasword default
		 	strcpy(user.username, "admin");
		 	strcpy(user.password, "ganteng");
		 	
		 	
		 	
		 	//loop untuk pas 
		 	while (1){
		 		char username[20];
		 		char password[20];
		 		
		 		gotoxy(20,7);
		 		printf("=========================================");
		 		gotoxy(20,8);
		 		printf("|===============L O G I N===============|");
		 		gotoxy(20,9);
		 		printf("|                                       |");
		 		gotoxy(20,10);
		 		printf("|    username :                         |");
		 		gotoxy(20,11);
		 		printf("|                                       |");
		 		gotoxy(20,12);
		 		printf("|    password :                         |");
		 		gotoxy(20,13);
		 		printf("|                                       |");
		 		gotoxy(20,14);
		 		printf("=========================================");
		 		
		 		
		 		gotoxy(35,10);
		 		scanf("%s", username);
		 	
		 		
		 		gotoxy(35,12);
		 		
		 		scanf("%s", password);
		 
		 		
		 		//jika pass dan user name benar pergi ke display
		 		
		 		if(strcmp(username, user.username) == 0 && strcmp(password, user.password) == 0){
		 			gotoxy(20,17);
		 			printf("!!!S E L A M A T  D A T A N G!!!");
			system("cls");
		 			
		 			display();
					int pilihan;
					printf("masukan pilihan :");
					scanf("%d", &pilihan);
					
					switch(pilihan){
			case 1:
				system("cls");
		 	gotoxy(1,0);
			printf("\t\t\t\t\tTambah data\t\t\t\t\t");
		 		buatData();
		 		
		 	system("cls");
		 	break;
		 	
		 	case 2:
		 		system("cls");
		 	gotoxy(1,0);
			printf("\t\t\t\t\tTambah data\t\t\t\t\t");
				lihatData();
		
		 	break;
		 	case 3:
			printf("\t\t\t\t\tTambah data\t\t\t\t\t");
		 	gotoxy(1,13);
		 	break;
		 	case 4:
			printf("\t\t\t\t\tTambah data\t\t\t\t\t");
		 	gotoxy(1,13);
		 	break;
		 	case 5:
			printf("\t\t\t\t\tTambah data\t\t\t\t\t");
		 	gotoxy(1,13);
		 	break;
		 	case 6:
		 		system("cls");
		 		gotoxy(18,11);
			printf("terimakasih. anda keluar dari program");
		 	return 0;
		 	default:
		 		printf("\tpilihan tidak ada,coba lagi");
		 		break;
					
					}
					
				 }else {
				 	gotoxy(20,17);
				 	printf("password atau user name salah!!");
				 	
				 }
	
			 }
			 return 0;
		}
	
	
		
	
	
