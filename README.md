



#include iostream
using namespace std;

//function prototyping
void displayarray(char array[3][3]);

void player1(char array[3][3]); //player 1 selects position

void player2(char array[3][3]); //player 2 selects position

bool player1wins(char array[3][3], bool &); //the bool functions are to determine if winning conditions exist

bool player2wins(char array[3][3], bool &);

int main()
{


	char tictactoe[3][3] = { { '*','*', '*' },
	                           { '*','*', '*' },
				   { '*','*', '*' } }; // intializing to *

	displayarray(tictactoe); //displaying intialized array for first time

	player1(tictactoe);
	player2(tictactoe);
	player1(tictactoe);
	player2(tictactoe);
	player1(tictactoe); //minimum 5 moves must be made before even checking for wins or losses 

	int functioncall = 5; // functioncall keeps track of how many times function is called
						  //if function is called 9 times without a winner; all 9 spaces are full; program ends

	bool condition1 = false, condition2 = false;
	//condition1 true means player 1 wins and condition2 true means player 2 wins
	//both conditions intialized to losses 

	player1wins(tictactoe, condition1);


	while (condition1 != true && functioncall < 9)
	{
		{
			player2(tictactoe);
			functioncall++;
			player2wins(tictactoe, condition2);
			if (condition2 == true)
				break;
		}

		while (condition2 != true && functioncall < 9)

		{
			player1(tictactoe);
			functioncall++;
			player1wins(tictactoe, condition1);
			if (condition1 == true)
				break;
			break; //still break even if player 1 does not win to return to large loop 
		}

	}

	if (functioncall == 9 && condition1 != true && condition2 != true)
		cout << "It's a tie!" << endl;

	system("PAUSE");
	return 0;
}


void displayarray(char array[3][3])
{


	//nested for loops to display array

	for (int row = 0; row <= 2; row++)
	{
		for (int column = 0; column <= 2; column++)
			cout << array[row][column] << ' ';

		cout << endl;

	}

}

void player1(char array[3][3])
{

	int row1, column1;
	
	cout << "Player 1: Choose a location on the board by first entering the row (0-2) then column (0-2) number" << endl;
	
	cin >> row1 >> column1;



	while (row1 < 0 || row1 >2)
	{
		cout << "You've selected an invalid row number. Enter again" << endl;
		cin >> row1;
	}

	while (column1 < 0 || column1 >2)
	{
		cout << "You've selected an invalid column number. Enter again" << endl;
		cin >> column1;
	}

	while (array[row1][column1] != '*') //spot is taken
	{
		cout << "The spot you've chosen on the board is already full. Please reselect the row and column number." << endl;
		cin >> row1 >> column1;

		while (row1 < 0 || row1 >2)
		{
			cout << "You've selected an invalid row number. Enter again" << endl;
			cin >> row1;
		}

		while (column1 < 0 || column1 >2)
		{
			cout << "You've selected an invalid column number. Enter again" << endl;
			cin >> column1;
		}

	}

	array[row1][column1] = 'X'; // If spot is open, Player 1 inputs X into selected location on board

	displayarray(array); //showing updated board after player 1 makes a move

}

void player2(char array[3][3])
{


	int row2, column2;
	cout << "Player 2: Choose a location on the board by first entering the row (0-2) then column (0-2) number" << endl;
	cin >> row2 >> column2;

	while (row2 < 0 || row2 >2)
	{
		cout << "You've selected an invalid row number. Enter again" << endl;
		cin >> row2;
	}

	while (column2 < 0 || column2 >2)
	{
		cout << "You've selected an invalid column number. Enter again" << endl;
		cin >> column2;
	}

	while (array[row2][column2] != '*') //spot is taken
	{
		cout << "The spot you've chosen on the board is already full. Please reselect the row and column number." << endl;
		cin >> row2 >> column2;

		while (row2 < 0 || row2 >2)
		{
			cout << "You've selected an invalid row number. Enter again" << endl;
			cin >> row2;
		}

		while (column2 < 0 || column2 >2)
		{
			cout << "You've selected an invalid column number. Enter again" << endl;
			cin >> column2;
		}

	}

	array[row2][column2] = 'O'; //If spot is open, Player 2 inputs O into selected location on board 

	displayarray(array); //showing updated board after player 2 makes a move

}

bool player1wins(char array[3][3], bool &condition1) //winning combinations for player 1
{


	int row, column;

	for (row = 0; row <= 2; row++) //checking horizontal wins
	{

		if (array[row][0] == 'X' && array[row][1] == 'X' && array[row][2] == 'X')
		{
			cout << "Player 1 wins!" << endl;
			condition1 = true;
			break;
		}

	}
	for (column = 0; column <= 2; column++) //checking vertical wins
	{

		if (array[0][column] == 'X' && array[1][column] == 'X' && array[2][column] == 'X')
		{
			cout << "Player 1 wins!" << endl;
			condition1 = true;
			break;
		}

	}

	//checking two possible diagnol wins

	if (array[0][0] == 'X' && array[1][1] == 'X' && array[2][2] == 'X')
	{
		cout << "Player 1 wins!" << endl;
		condition1 = true;

	}

	if (array[2][0] == 'X' && array[1][1] == 'X' && array[0][2] == 'X')
	{
		cout << "Player 1 wins!" << endl;
		condition1 = true;

	}

	return condition1;

}

bool player2wins(char array[3][3], bool &condition2) //winning combinations for player 2
{


	int row, column;

	for (row = 0; row <= 2; row++) //checking horizontal wins
	{

		if (array[row][0] == 'O' && array[row][1] == 'O' && array[row][2] == 'O')
		{
			cout << "Player 2 wins!" << endl;
			condition2 = true;
			break;
		}

	}
	for (column = 0; column <= 2; column++) //checking vertical wins
	{

		if (array[0][column] == 'O' && array[1][column] == 'O' && array[2][column] == 'O')
		{
			cout << "Player 2 wins!" << endl;
			condition2 = true;
			break;
		}

	}

	//checking two possible diagnol wins

	if (array[0][0] == 'O' && array[1][1] == 'O' && array[2][2] == 'O')
	{
		cout << "Player 2 wins!" << endl;
		condition2 = true;

	}

	if (array[2][0] == 'O' && array[1][1] == 'O' && array[0][2] == 'O')
	{
		cout << "Player 2 wins!" << endl;
		condition2 = true;

	}

	return condition2;
}
# Tic-Tac-Toe
This program lets two users play tic-tac-toe.

