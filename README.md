# -Tic-Tac-Toe-Game
```cpp
#include <iostream>
#include <vector>

using namespace std;

class TicTacToe {
private:
    char board[3][3];
    char current_player;

public:
    TicTacToe() { resetGame(); }

    // Task: Reset the board
    void resetGame() {
        char start_num = '1';
        for (int i = 0; i < 3; i++) {
            for (int j = 0; j < 3; j++) {
                board[i][j] = start_num++;
            }
        }
        current_player = 'X';
    }

    // Task: Display the state of the board
    void printBoard() {
        #ifdef _WIN32
            system("cls");
        #else
            system("clear");
        #endif
        cout << "\n  Tic-Tac-Toe \n\n";
        for (int i = 0; i < 3; i++) {
            cout << "  " << board[i][0] << " | " << board[i][1] << " | " << board[i][2] << endl;
            if (i < 2) cout << " ---|---|---" << endl;
        }
        cout << endl;
    }

    // Task: Place a mark on the board
    bool makeMove(int slot) {
        if (slot < 1 || slot > 9) return false;
        int row = (slot - 1) / 3;
        int col = (slot - 1) % 3;

        if (board[row][col] != 'X' && board[row][col] != 'O') {
            board[row][col] = current_player;
            return true;
        }
        return false;
    }

    // Task: Check for winner or draw
    char checkWinner() {
        for (int i = 0; i < 3; i++) {
            if (board[i][0] == board[i][1] && board[i][1] == board[i][2]) return board[i][0];
            if (board[0][i] == board[1][i] && board[1][i] == board[2][i]) return board[0][i];
        }
        if (board[0][0] == board[1][1] && board[1][1] == board[2][2]) return board[0][0];
        if (board[0][2] == board[1][1] && board[1][1] == board[2][0]) return board[0][2];
        return ' ';
    }

    void switchPlayer() { current_player = (current_player == 'X') ? 'O' : 'X'; }
    char getCurrentPlayer() { return current_player; }
};

int main() {
    TicTacToe game;
    int choice, moves = 0;

    while (true) {
        game.printBoard();
        cout << "Player " << game.getCurrentPlayer() << ", enter a slot (1-9): ";
        cin >> choice;

        if (game.makeMove(choice)) {
            moves++;
            char winner = game.checkWinner();
            if (winner != ' ') {
                game.printBoard();
                cout << "Player " << winner << " wins! 🎉\n";
                break;
            } else if (moves == 9) {
                game.printBoard();
                cout << "It's a draw! 🤝\n";
                break;
            }
            game.switchPlayer();
        } else {
            cout << "Invalid move! Press Enter to try again...";
            cin.ignore();
            cin.get();
        }
    }
    return 0;
}
