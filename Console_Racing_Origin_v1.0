#include<iostream>
#include<conio.h>
#include<dos.h>
#include <windows.h>
#include <time.h>

#define SCREEN_WIDTH 90
#define SCREEN_HEIGHT 26
#define WIN_WIDTH 70

using namespace std;

HANDLE console = GetStdHandle(STD_OUTPUT_HANDLE);
COORD CursorPosition;

int enemyY[3];
int enemyX[3];
int enemyFlag[3];
char car[4][4] = { ' ','±','±',' ',
					'±','±','±','±',
					' ','±','±',' ',
					'±','±','±','±' };

int carPos = WIN_WIDTH/2;
int score = 0;

void gotoxy(int x, int y){
	CursorPosition.X = x;
	CursorPosition.Y = y;
	SetConsoleCursorPosition(console, CursorPosition);
}
void setcursor(bool visible, DWORD size) {
	if(size == 0)
		size = 20;

	CONSOLE_CURSOR_INFO lpCursor;
	lpCursor.bVisible = visible;
	lpCursor.dwSize = size;
	SetConsoleCursorInfo(console,&lpCursor);
}
void drawBorder(){
	for(int i=0; i<SCREEN_HEIGHT; i++){
		for(int j=0; j<17; j++){
			gotoxy(0+j,i); cout<<"±";
			gotoxy(WIN_WIDTH-j,i); cout<<"±";
		}
	}
	for(int i=0; i<SCREEN_HEIGHT; i++){
		gotoxy(SCREEN_WIDTH,i); cout<<"±";
	}
}
void genEnemy(int ind){
	enemyX[ind] = 17 + rand()%(33);
}
void drawEnemy(int ind){
	if( enemyFlag[ind] == true ){
		gotoxy(enemyX[ind], enemyY[ind]);   cout<<"****";
		gotoxy(enemyX[ind], enemyY[ind]+1); cout<<" ** ";
		gotoxy(enemyX[ind], enemyY[ind]+2); cout<<"****";
		gotoxy(enemyX[ind], enemyY[ind]+3); cout<<" ** ";
	}
}
void eraseEnemy(int ind){
	if( enemyFlag[ind] == true ){
		gotoxy(enemyX[ind], enemyY[ind]); cout<<"    ";
		gotoxy(enemyX[ind], enemyY[ind]+1); cout<<"    ";
		gotoxy(enemyX[ind], enemyY[ind]+2); cout<<"    ";
		gotoxy(enemyX[ind], enemyY[ind]+3); cout<<"    ";
	}
}
void resetEnemy(int ind){
	eraseEnemy(ind);
	enemyY[ind] = 1;
	genEnemy(ind);
}

void drawCar(){
	for(int i=0; i<4; i++){
		for(int j=0; j<4; j++){
			gotoxy(j+carPos, i+22); cout<<car[i][j];
		}
	}
}
void eraseCar(){
	for(int i=0; i<4; i++){
		for(int j=0; j<4; j++){
			gotoxy(j+carPos, i+22); cout<<" ";
		}
	}
}

int collision(){
	if( enemyY[0]+4 >= 23 ){
		if( enemyX[0] + 4 - carPos >= 0 && enemyX[0] + 4 - carPos < 9  ){
			return 1;
		}
	}
	return 0;
}
void gameover();
void updateScore(){
	gotoxy(WIN_WIDTH + 7, 5);cout<<"Score: "<<score<<endl;
}

void instructions(){
    setlocale(LC_ALL, "Russia");
	system("cls");
	cout <<"КАК ИГРАТЬ?";
	cout << "\n----------------";
	cout << "\n Убедись что клавиатура на английской раскладке";
	cout << "\n Представь что ты фараон, который догоняет наркоборонов или наркобарон линяющий от фараонов.";
	cout << "\n\n Нажимай 'a' что бы машина смещалась в лево";
	cout << "\n Нажимай 'd' что бы машина смещалась в право";
	cout << "\n Нажми 'escape' для выхода";
	cout << "\n\nНажимай любую клавишу, что бы вернуться в предыдущее меню";
	getch();
}

void play(){
	carPos = -1 + WIN_WIDTH/2;
	score = 0;
	enemyFlag[0] = 1;
	enemyFlag[1] = 0;
	enemyY[0] = enemyY[1] = 1;

	system("cls");
	drawBorder();
	updateScore();
	genEnemy(0);
	genEnemy(1);

	gotoxy(WIN_WIDTH + 7, 2);cout<<"Console_Racing_Origin_v1.0";
	gotoxy(WIN_WIDTH + 6, 4);cout<<"----------";
	gotoxy(WIN_WIDTH + 6, 6);cout<<"----------";
	gotoxy(WIN_WIDTH + 7, 12);cout<<"Управление ";
	gotoxy(WIN_WIDTH + 7, 13);cout<<"-------- ";
	gotoxy(WIN_WIDTH + 2, 14);cout<<" A - ЛЕВО";
	gotoxy(WIN_WIDTH + 2, 15);cout<<" D - ПРАВО";

	gotoxy(18, 5);cout<<"Нажми любую клавишу чтобы начать";
	getch();
	gotoxy(18, 5);cout<<"                      ";

	while(1){
		if(kbhit()){
			char ch = getch();
			if( ch=='a' || ch=='A' ){
				if( carPos > 18 )
					carPos -= 4;
			}
			if( ch=='d' || ch=='D' ){
				if( carPos < 50 )
					carPos += 4;
			}
			if(ch==27){
				break;
			}
		}

		drawCar();
		drawEnemy(0);
		drawEnemy(1);
		if( collision() == 1  ){
			gameover();
			return;
		}
		Sleep(50);
		eraseCar();
		eraseEnemy(0);
		eraseEnemy(1);

		if( enemyY[0] == 10 )
			if( enemyFlag[1] == 0 )
				enemyFlag[1] = 1;

		if( enemyFlag[0] == 1 )
			enemyY[0] += 1;

		if( enemyFlag[1] == 1 )
			enemyY[1] += 1;

		if( enemyY[0] > SCREEN_HEIGHT-4 ){
			resetEnemy(0);
			score++;
			updateScore();
		}
		if( enemyY[1] > SCREEN_HEIGHT-4 ){
			resetEnemy(1);
			score++;
			updateScore();
		}
	}
}

int main()
{
    setlocale(LC_ALL, "Russian");
	setcursor(0,0);
	srand( (unsigned)time(NULL));

	do{
		system("cls");
		gotoxy(10,5); cout<<" -------------------------------------------------";
		gotoxy(10,6); cout<<" |        Гонки, каких ты ещё не встречала        | ";
		gotoxy(10,7); cout<<" -------------------------------------------------";
		gotoxy(10,9); cout<<"1. Старт игры";
		gotoxy(10,10); cout<<"2. Инструкции";
		gotoxy(10,11); cout<<"3. Выход";
		gotoxy(10,13); cout<<"Выбери режим: ";
		char op = getche();

		if( op == '1') play();
		else if( op == '2') instructions();
		else if( op == '3') exit(0);

	}while(1);

	return 0;
};
void gameover(){
    setlocale(LC_ALL, "Russian");
	system("cls");
	cout << endl;
	cout << "\t\t----------------------------------------------------------------"  <<endl;
	cout << "\t\t--------- Game Over Agripina, be careful babyGirl --------------"  <<endl;
	cout << "\t\t--------- Конец игры Лена, будь бдительна девочка --------------" <<endl;
	cout << "\t\t----------------------------------------------------------------"  <<endl <<endl;
	cout << "\t\t       Нажми на любую клавишу, что бы вернуться в начальное меню.";
	getch();
}
