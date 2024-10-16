//# tic-tac-toe
#include<stdio.h>
char board[3][3];
void initialise(){
	for(int i=0;i<3;i++) {
		for(int j=0;j<3;j++) {
			board[i][j] = '_';
		}
	}
	return;
}
void printBoard(){
	printf("___________________\n");
	for(int i=0;i<3;i++) {
		printf("|");
		for(int j=0;j<3;j++){
			printf("  %c  |",board[i][j]);
		}
		printf("\n|_____|_____|_____|\n");
	}
	printf("\n\n");
	return;
}
void insertXO(int pos,int n){
	pos--;
	int i=pos/3;
	int j=pos%3;
	if(board[i][j]!='_'){
		printf("BOX IS ALREADY OCCUPIED,TRY AGAIN\n");
		play(n);
		return;
	} else{
		if(n%2!=0){
			board[i][j]='x';
		} else {
			board[i][j]='O';
		}
		printBoard();
		return;
	}
}
int winnerCheck(){
	for(int i=0;i<3;i++){
		if(board[i][0]==board[i][1]&&board[i][1]==board[i][2]&&board[i][0]!='_') {
			if(board[i][0]=='x'){
				printf("Player-1 is the winner\n");
			} else{
				printf("Player-2 is the winner\n");
			}
			return 1;
		}
		if(board[0][i]==board[1][i]&&board[1][i]==board[2][i]&&board[0][i]!='_'){
			if(board[0][i]=='x'){
				printf("Player-1 is the winner\n");
			} else{
				printf("Player-2 is the winner\n");
			}
			return 1;
		}
	}
	if(board[0][0]==board[1][1]&&board[1][1]==board[2][2]&&board[0][0]!='_'){
		if(board[0][0]=='x') {
			printf("Player-1 is the winner\n");
		} else{
			printf("Player-2 is the winner\n");
		}
		return 1;
	}
	if(board[0][2]==board[1][1]&&board[1][1]==board[2][0]&&board[0][2]!='_'){
		if(board[0][2]=='x') {
			printf("Player-1 is the winner\n");
		} else{
			printf("Player-2 is the winner\n");
		}
		return 1;
	}
	return 0;
}
int isDraw(){
	for(int i=0;i<3;i++){
		for(int j=0;j<3;j++){
			if(board[i][j]=='_'){
				return 0;
			}
		}
	}
	return 1;
}
void play(int turn){
	int pos,w;
	if(turn>9){
		printf("Game Over! It's a draw.\n");
		return;
	}
	if(turn%2!=0){
		printf("Player-1's turn : ");
		scanf("%d",&pos);
		insertXO(pos,turn);
	} else{
		printf("Player-2's turn : ");
		scanf("%d",&pos);
		insertXO(pos,turn);
	}
	if(turn>=5){
		w=winnerCheck();
		if(w==1){
			return;
		}
	}
	if(isDraw()){
		printf("Game Over! It's a draw.\n");
		return;
	}
	play(turn+1);
}
void ending(){
	int a;
	printf("\n\nEnter 1 to restart\nEnter 0 to exit\n");
	scanf("%d",&a);
	if(a==1){
		main();
	}
	else if(a==0){
		return;
	}
	else{
		printf("invalid");
		ending();
	}
}
void main(){
	printf("###Welcome to TicTacToe###\n>Player 1 --> X\n>Player 2 --> O\n");
	printf("Instructions:\nInsert the given numbers to the corresponding position as shown--->\n");
	int p=1;
	printf("___________________\n");
	for(int i=0; i<3; i++){
		printf("|");
		for(int j=0; j<3; j++){
			printf("  %d  |",p);
			p++;
		}
		printf("\n|_____|_____|_____|\n");
	}
	initialise();
	play(1);
	ending();
	return;
}
