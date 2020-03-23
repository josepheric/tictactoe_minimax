# Tictactoe_MiniMax
Tic Tac Toe Ai with Minimax Algorithm

Penjelasan Source Code:
``
struct Move 
{ 
	int row, col; 
}; 

char player = 'x', opponent = 'o'; 
``
Ini merupakan struktur data dari pegerakan pada game tic-tac-toe. 
Pada kasus ini, player menggunakan x dan opponent/musuh akan menggunakan o dalam game tic-tac-toe
Player dapat mengisi x pada cel yg kosong, opponent mengisi o pada cel manapun yg kosong

```
bool isMovesLeft(char board[3][3]) 
{ 
	for (int i = 0; i<3; i++) 
		for (int j = 0; j<3; j++) 
			if (board[i][j]=='_') 
				return true; 
	return false; 
} 
```
Fungsi diatas digunakan untuk mencari tahu apakah ada cel yang kosong (masih memungkinkan adanya pegerakan).
Pada kasus ini, cel kosong ditandai dengan '_' dan besar papan adalah 3x3

```
int evaluate(char b[3][3]) 
{ 
	// Checking for Rows for X or O victory. 
	for (int row = 0; row<3; row++) 
	{ 
		if (b[row][0]==b[row][1] && 
			b[row][1]==b[row][2]) 
		{ 
			if (b[row][0]==player) 
				return +10; 
			else if (b[row][0]==opponent) 
				return -10; 
		} 
	} 

	// Checking for Columns for X or O victory. 
	for (int col = 0; col<3; col++) 
	{ 
		if (b[0][col]==b[1][col] && 
			b[1][col]==b[2][col]) 
		{ 
			if (b[0][col]==player) 
				return +10; 

			else if (b[0][col]==opponent) 
				return -10; 
		} 
	} 

	// Checking for Diagonals for X or O victory. 
	if (b[0][0]==b[1][1] && b[1][1]==b[2][2]) 
	{ 
		if (b[0][0]==player) 
			return +10; 
		else if (b[0][0]==opponent) 
			return -10; 
	} 

	if (b[0][2]==b[1][1] && b[1][1]==b[2][0]) 
	{ 
		if (b[0][2]==player) 
			return +10; 
		else if (b[0][2]==opponent) 
			return -10; 
	} 

	// Else if none of them have won then return 0 
	return 0; 
} 
```

Fungsi evaluate digunakan untuk menghitung "skor" suatu konfigurasi papan tertentu. 
Prosesnya sebagai berikut:
Misalkan x sebagai maximizer dan o sebagai minimizer

Apabila maximizer (x) menang, kita beri nilai +10
Apabila minimizer (o) menang, kita beri nilai -10
Apabila belum ada yang menang/draw, diberi nilai +0


