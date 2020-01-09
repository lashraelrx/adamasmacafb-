#include <stdio.h>
#include <string.h>
#define MAXCHAR 1000
#include<locale.h>
int main() {
	setlocale(LC_ALL, "Turkish");
	time_t t;
	srand((unsigned)time(&t));

	int rastgele, count = 0, hak = 8;
	char string[MAXCHAR];
	char cevap[128];
	char str[128];
	//------Dosya açma 
	FILE* fp;
	char* filename = "c:\\kelimeler.txt"; //dosya konumunu
	fp = fopen(filename, "r");
	rastgele = rand() % 81; //Rastgele sayı üretiliyor.
	while (fgets(str, MAXCHAR, fp) != NULL) {
		count++;
		if (count == rastgele) {
			str[strlen(str) - 1] = '\0'; //Kelimenin sonundaki \n siliniyor.
			strcpy(cevap, str); //Döngüde rastgele cevap, tek bir değişkene atanıyor
			printf("%s", str); //bu satır kelimeyi gösteriyor, denemek için açabilirsin
			break;
		}
	}

	int i = 0, j, k, m;

	int N = strlen(cevap);
	int gizle[MAXCHAR];
	for (i; i < N; ++i) {
		gizle[i] = 0;
	}

	// Her tahminde döngü başa atıyor
	int bildimi = 0;
	while (!bildimi && hak > 0) {
		//Bulunamayan harfler yerine _ yazılıyor.
		printf("Kelime : ");
		for (j = 0; j < N; ++j) {
			if (gizle[j]) {
				printf("%c", cevap[j]);
			}
			else {
				printf("_");
			}
		}
		printf("\n");

		// Sonraki harf isteniyor
		char tahmin;
		printf("Harf Tahmini: ");
		
		scanf(" %c", &tahmin);

		int harfvarmi = 0;
		for (k = 0; k < N; ++k) {
			if (cevap[k] == tahmin) {
				harfvarmi = 1;
				gizle[k] = 1;
			}
		}
		if (!harfvarmi) {
			hak--;
			printf("Harf bulunamadi. Kalan hak: %d.\n\n", hak);
			switch (hak) {
			case 7: printf("      |\n\n"); break;
			case 6: printf("      |\n      |\n\n"); break;
			case 5: printf("      |\n      |\n      |\n\n"); break;
			case 4: printf(" ____\n      |\n      |\n      |\n\n"); break;
			case 3: printf(" ____\n  0   |\n      |\n      |\n\n"); break;
			case 2: printf(" ____\n  0   |\n /|\\  |\n      |\n\n"); break;
			case 1: printf(" ____\n  0   |\n /|\\  |\n  /   |\n\n"); break;
			case 0: printf(" ____\n  x   |\n /|\\  |\n / \\  |\n\n"); break;
			}
		}

	}

	if (bildimi) {
		printf("Kazandiniz!\n Kelime: %s", cevap);
	}
	else {
		printf("Kaybettiniz! \nKelime: %s ",cevap);
	}


	return 0;
}
