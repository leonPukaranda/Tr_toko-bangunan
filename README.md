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
    char pilihan[10];
    char filename[MAX];
    FILE *file;
    struct Produk produk;
    
    do {
        printf("\n\tMasukkan Kode Produk: ");
        scanf("%s", produk.kode);

        printf("\tMasukkan Nama Produk: ");
        scanf(" %[^\n]s", produk.namabarang);

        printf("\tMasukkan Harga:\tRp.");
        scanf("%d", &produk.harga);

        printf("\tMasukkan Stok: ");
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

        printf("\nApakah Anda ingin menambahkan produk lain? (ya/tidak)\n");
        printf("Masukan pilihan :");
        scanf("%s", pilihan);
    } while (strcmp(pilihan, "ya") == 0);
    
}
		
		
		
		void lihatData() {
    struct Produk produk;
    char pilihan[10];
    char filename[MAX];
    FILE *file;

    // Buka file dan tampilkan data
    do{
    	
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
    printf("ketik 'Tidak' jika ingin kembali :");
    scanf("%s",pilihan);

    fclose(file);
	}while (strcmp(pilihan, "ya") == 0);
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
		printf("=  4. Delete data barang                              =");
		gotoxy(10,15);
		printf("=  5. Cari barang                                     =");
		gotoxy(10,16);
		printf("=  6. Sorting barang                                  =");
		gotoxy(10,17);
		printf("=  7. Keluar                                          =");
		gotoxy(10,18);
		printf("=======================================================");
		gotoxy(10,19);
	}
		 
		void updateData() {
    struct Produk produk;
    char filename[MAX], code[MAX], choice;
    int found = 0;
    FILE *file, *temp;

    printf("\nMasukkan nama file: ");
    scanf("%s", filename);

    file = fopen(filename, "r");
    if (file == NULL) {
        printf("\nfile yang di cari tidak ada\n");
        return;
    }

    temp = fopen("temp.txt", "w");
    if (temp == NULL) {
        printf("\nTerjadi kesalahan saat membuka file sementara.\n");
        fclose(file);
        return;
    }

    printf("\nMasukkan Kode Barang yang ingin diupdate: ");
    scanf("%s", code);

    while (fscanf(file, "%[^;];%[^;];%d;%d\n", produk.kode, produk.namabarang, &produk.harga, &produk.stok) != EOF) {
        if (strcmp(code, produk.kode) == 0) {
            found = 1;

            printf("\nData sebelumnya:\n");
            printf("Kode\tNama\t\tHarga\tStok\n");
            printf("%s\t%s\t\t%d\t%d\n", produk.kode, produk.namabarang, produk.harga, produk.stok);

            printf("\nApakah Anda yakin ingin mengubah data ini? (Y/N): ");
            fflush(stdin);
            scanf("%c", &choice);

            if (choice == 'Y' || choice == 'y') {
                printf("\nMasukkan Nama Produk Baru: ");
                scanf(" %[^\n]s", produk.namabarang);

                printf("Masukkan Harga Baru: ");
                scanf("%d", &produk.harga);

                printf("Masukkan Stok Baru: ");
                scanf("%d", &produk.stok);

                printf("\nData berhasil diupdate.\n");
            } else {
                printf("\nData tidak diupdate.\n");
            }
        }

        fprintf(temp, "%s;%s;%d;%d\n", produk.kode, produk.namabarang, produk.harga, produk.stok);
    }

    fclose(file);
    fclose(temp);

    if (found == 0) {
        printf("\nData tidak ditemukan.\n");
        remove("temp.txt");
        return;
    }

    file = fopen(filename, "w");
    if (file == NULL) {
        printf("\nTerjadi kesalahan saat membuka file.\n");
        remove("temp.txt");
        return;
    }

    temp = fopen("temp.txt", "r");
    if (temp == NULL) {
        printf("\nTerjadi kesalahan saat membuka file sementara.\n");
        fclose(file);
        remove("temp.txt");
        return;
    }

    while (fscanf(temp, "%[^;];%[^;];%d;%d\n", produk.kode, produk.namabarang, &produk.harga, &produk.stok) != EOF) {
        fprintf(file, "%s;%s;%d;%d\n", produk.kode, produk.namabarang, produk.harga, produk.stok);
    }

    fclose(file);
    fclose(temp);
    remove("temp.txt");
}



 void deleteData() {
    struct Produk produk;
    char filename[MAX], tempFile[MAX];
    FILE *file, *temp;

    // Buka file dan buat file temporary
    printf("\nMasukkan nama file: ");
    scanf("%s", filename);

    file = fopen(filename, "r");
    if (file == NULL) {
        printf("\nfile yang di cari tidak ada\n");
        return;
    }

    sprintf(tempFile, "%s.tmp", filename);
    temp = fopen(tempFile, "w");
    if (temp == NULL) {
        printf("\nTerjadi kesalahan saat membuat file temporary.\n");
        return;
    }

    // Ambil kode produk yang ingin dihapus
    char kode[MAX];
    printf("Masukkan kode produk yang ingin dihapus: ");
    scanf("%s", kode);

    // Salin data ke file temporary kecuali data dengan kode produk yang dihapus
    int found = 0;
    while (fscanf(file, "%[^;];%[^;];%d;%d\n", produk.kode, produk.namabarang, &produk.harga, &produk.stok) != EOF) {
        if (strcmp(kode, produk.kode) == 0) {
            found = 1;
            continue;
        }
        fprintf(temp, "%s;%s;%d;%d\n", produk.kode, produk.namabarang, produk.harga, produk.stok);
    }

    fclose(file);
    fclose(temp);

    // Hapus file asli dan ganti dengan file temporary
    if (found) {
        remove(filename);
        rename(tempFile, filename);
        printf("\nData dengan kode %s berhasil dihapus.\n", kode);
    } else {
        remove(tempFile);
        printf("\nTidak ada data dengan kode %s.\n", kode);
    }
    
}


		
void cariData() {
    struct Produk produk;
    char filename[MAX], code[MAX];
    char pilihan[10];
    FILE *file;

	do{
		
    // Membuka File dan file temorary
    printf("\nMasukkan nama file: ");
    scanf("%s", filename);

    // Mencari Kode pada Barang
    printf("\nMasukkan kode barang yang ingin dicari: ");
    scanf("%s", code);

    file = fopen(filename, "r");
    if (file == NULL) {
        printf("\nTerjadi kesalahan saat membuka file.\n");
        return;
    }
    // Mengecek Kode Barang Ada Atau Tidak Ada
    int found = 0;
    loading();
    while (fscanf(file, "%[^;];%[^;];%d;%d\n", produk.kode, produk.namabarang, &produk.harga, &produk.stok) != EOF) {
        if (strcmp(code, produk.kode) == 0) {
            found = 1;
            printf("\nData ditemukan:\n");
            printf("Kode\tNama\t\tHarga\tStok\n");
            printf("%s\t%s\t\t%d\t%d\n", produk.kode, produk.namabarang, produk.harga, produk.stok);
            
            printf("ingin cari lagi :");
            scanf("%s", pilihan);
            fclose(file);
            
        }
    }

        if (!found) {
        printf("\nKode barang tidak ditemukan dalam file.\n");
    }
  

	}while (strcmp(pilihan, "iya") == 0);
	
	return display();
}


		void sortingData(){
    struct Produk produk[MAX];
    char filename[MAX];
    char pilihan[10];
    FILE *file;
    int i, j, n;
    struct Produk temp;
	
	do{
		
	
    printf("\nMasukkan nama file: ");
    scanf("%s", filename);

    file = fopen(filename, "r");
    if (file == NULL) {
        printf("\nTerjadi kesalahan saat membuka file.\n");
        return;
    }

    // Baca data dari file dan simpan ke array
    n = 0;
    while (fscanf(file, "%[^;];%[^;];%d;%d\n", produk[n].kode, produk[n].namabarang, &produk[n].harga, &produk[n].stok) != EOF) {
        n++;
    }
    

    fclose(file);

    // Lakukan sorting
    for (i = 0; i < n - 1; i++) {
        for (j = i + 1; j < n; j++) {
            if (produk[i].harga > produk[j].harga) {
                temp = produk[i];
                produk[i] = produk[j];
                produk[j] = temp;
            }
        }
    }

    // Tampilkan hasil sorting
    printf("\nData setelah diurutkan berdasarkan harga produk (dari yang terendah ke tertinggi):\n");
    printf("\n=============================================\n");
    printf("Kode\t\tNama\t\tHarga\t\tStok\n");
    for (i = 0; i < n; i++) {
        printf("%s\t\t%s\t\t%d\t\t%d\n", produk[i].kode, produk[i].namabarang, produk[i].harga, produk[i].stok);
    }
    printf("\n=============================================\n");
    printf("ingin cari lagi :");
            scanf("%s", pilihan);
            
	}while (strcmp(pilihan, "iya") == 0);
 system("cls");
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
		 			loading();
		 			display();
					int pilihan;
					printf("masukan pilihan :");
					scanf("%d", &pilihan);
					
					switch(pilihan){
			case 1:
				system("cls");
				loading();
		 	gotoxy(0,3);
			printf("\t\t\t\t\tTambah data\t\t\t\t\t");
		 		buatData();
		 		
		 	system("cls");
		 	break;
		 	
		 	case 2:
		 		system("cls");
		 		loading();
		 	gotoxy(0,3);
			printf("\t\t\t\t\tTambah data\t\t\t\t\t");
				lihatData();
			system("cls");
		 	break;
		 	case 3:
				system("cls");
				loading();
	 		gotoxy(0,3);
	 		printf("\t\t\t\t\tTambah data\t\t\t\t\t");
				updateData();
				system("cls");
			
		 	break;
		 	case 4:
				system("cls");
				loading();
	 		gotoxy(0,3);
	 		printf("\t\t\t\t\tDelete data\t\t\t\t\t");
				deleteData();
			
			system("cls");
		 	break;
		 	case 5:
			system("cls");
			loading();
			gotoxy(0,3);
			printf("\t\t\t\t\tCari data\t\t\t\t\t");
		 	cariData();
			system("cls");
		 	break;
			
			case 6:
		 	gotoxy(0,3);
		 	loading();
		 	system("cls");
			printf("\t\t\t\t\tsorting data\t\t\t\t\t");
			sortingData();
			
		//	system("cls");
		 	break;
			
		 	case 7:
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
		
		
		
		
		
		
		
		void loading(){
			
			for(int i = 0; i <= 100; i++){
				gotoxy(35,12);
        printf("loading %d%%",i);
        Sleep(5);
        system("cls");
    }
			
					
		}
		
		

		
		
		
