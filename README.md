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

// Kode dibawah ini digunakan untuk mengecek apakah ada o atau x yang menang pada suatu BARIS
```
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
```
// Kode dibawah ini untuk mengecek apakah ada colomn dimana o atau x menang
```
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
```
// Kode dibawah ini untuk mengecek apakah ada o atau x yang menang secara diagonal 
```
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

	// Bila tidak ada yg menang return 0
	return 0; 
```
#Fungsi Minimax
Fungsi ini digunakan untuk mengevaluasi suatu konfigurasi papan, dan akan menreturn value 
berdasarkan semua kemungkinan gerak dari posisi board tersebut.
```
int minimax(char board[3][3], int depth, bool isMax) 
{ 
	int score = evaluate(board); 

	// If Maximizer has won the game return his/her 
	// evaluated score 
	if (score == 10) 
		return score; 

	// If Minimizer has won the game return his/her 
	// evaluated score 
	if (score == -10) 
		return score; 

	// If there are no more moves and no winner then 
	// it is a tie 
	if (isMovesLeft(board)==false) 
		return 0; 

	// If this maximizer's move 
	if (isMax) 
	{ 
		int best = -1000; 

		// Traverse all cells 
		for (int i = 0; i<3; i++) 
		{ 
			for (int j = 0; j<3; j++) 
			{ 
				// Check if cell is empty 
				if (board[i][j]=='_') 
				{ 
					// Make the move 
					board[i][j] = player; 

					// Call minimax recursively and choose 
					// the maximum value 
					best = max( best, 
						minimax(board, depth+1, !isMax) ); 

					// Undo the move 
					board[i][j] = '_'; 
				} 
			} 
		} 
		return best; 
	} 

	// If this minimizer's move 
	else
	{ 
		int best = 1000; 

		// Traverse all cells 
		for (int i = 0; i<3; i++) 
		{ 
			for (int j = 0; j<3; j++) 
			{ 
				// Check if cell is empty 
				if (board[i][j]=='_') 
				{ 
					// Make the move 
					board[i][j] = opponent; 

					// Call minimax recursively and choose 
					// the minimum value 
					best = min(best, 
						minimax(board, depth+1, !isMax)); 

					// Undo the move 
					board[i][j] = '_'; 
				} 
			} 
		} 
		return best; 
	} 
} 
```
