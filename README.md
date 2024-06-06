#include <iostream>
#include <cstdlib>
#include <ctime>
#include <vector>

using namespace std;

const int BOARD_SIZE = 100;

class SnakeAndLadder {
private:
    vector<int> player_positions;
    vector<pair<int, int>> snakes;
    vector<pair<int, int>> ladders;

public:
    SnakeAndLadder() {
        player_positions = {0, 0};  // Initialize player positions to 0
        srand(time(NULL));

        // Initialize snakes and ladders
        snakes = {{17, 7}, {54, 34}, {62, 19}, {64, 60}, {87, 36}};
        ladders = {{1, 38}, {4, 14}, {9, 31}, {21, 42}, {28, 84}};
    }

    void play() {
        cout << "Welcome to Snake and Ladder!" << endl;

        while (player_positions[0] < BOARD_SIZE && player_positions[1] < BOARD_SIZE) {
            for (int player = 0; player < 2; player++) {
                cout << "Player " << player + 1 << ", press Enter to roll the dice...";
                cin.ignore();

                int dice_roll = rand() % 6 + 1;
                cout << "Player " << player + 1 << " rolled a " << dice_roll << "." << endl;

                int new_position = player_positions[player] + dice_roll;

                if (new_position > BOARD_SIZE) {
                    new_position = BOARD_SIZE;
                }

                cout << "Player " << player + 1 << "'s current position is " << player_positions[player] << "." << endl;

                // Check for snakes and ladders
                for (const auto& snake : snakes) {
                    if (new_position == snake.first) {
                        cout << "Oh no! Player " << player + 1 << " landed on a snake's head. They slide down to " << snake.second << "." << endl;
                        new_position = snake.second;
                        break;
                    }
                }

                for (const auto& ladder : ladders) {
                    if (new_position == ladder.first) {
                        cout << "Yay! Player " << player + 1 << " found a ladder. They climb up to " << ladder.second << "." << endl;
                        new_position = ladder.second;
                        break;
                    }
                }

                player_positions[player] = new_position;

                if (player_positions[player] == BOARD_SIZE) {
                    cout << "Congratulations, Player " << player + 1 << "! You won the game." << endl;
                    return;
                } else {
                    cout << "Player " << player + 1 << "'s new position is " << player_positions[player] << "." << endl;
                }
            }
        }
    }
};

int main() {
    SnakeAndLadder game;
    game.play();
    return 0;
}
