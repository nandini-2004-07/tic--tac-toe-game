# tic--tac-toe-game


def print_board(board):
    print("\n")
    for row in board:
        print(" | ".join(row))
        print("-" * 5)

def check_winner(board, player):
    # Check rows, columns, and diagonals for a win
    for row in board:
        if all(s == player for s in row):
            return True
    for col in range(3):
        if all(board[row][col] == player for row in range(3)):
            return True
    if all(board[i][i] == player for i in range(3)) or all(board[i][2 - i] == player for i in range(3)):
        return True
    return False

def is_full(board):
    return all(cell != " " for row in board for cell in row)

def tic_tac_toe():
    # Initialize the board
    board = [[" " for _ in range(3)] for _ in range(3)]
    players = ["X", "O"]
    turn = 0

    print("Welcome to Tic Tac Toe!")
    print_board(board)

    while True:
        current_player = players[turn % 2]
        print(f"\nPlayer {current_player}'s turn.")
        try:
            row = int(input("Enter row (0-2): "))
            col = int(input("Enter column (0-2): "))
            if board[row][col] == " ":
                board[row][col] = current_player
                print_board(board)

                if check_winner(board, current_player):
                    print(f"\nPlayer {current_player} wins!")
                    break
                if is_full(board):
                    print("\nIt's a tie!")
                    break

                turn += 1
            else:
                print("Cell already taken! Choose another.")
        except (ValueError, IndexError):
            print("Invalid input! Enter a row and column between 0 and 2.")

if __name__ == "__main__":
    tic_tac_toe()