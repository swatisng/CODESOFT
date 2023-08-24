import random
HUMAN = 'X'
AI = 'O'
EMPTY = ' '
def print_board(board):
    for row in board:
        print('|'.join(row))
        print('-' * 5)

def empty_cells(board):
    return [(i, j) for i in range(3) for j in range(3) if board[i][j] == EMPTY]

def evaluate(board):
    for row in board:
        if row.count(row[0]) == 3 and row[0] != EMPTY:
            return 10 if row[0] == AI else -10

    for col in range(3):
        if board[0][col] == board[1][col] == board[2][col] and board[0][col] != EMPTY:
            return 10 if board[0][col] == AI else -10

    if board[0][0] == board[1][1] == board[2][2] and board[0][0] != EMPTY:
        return 10 if board[0][0] == AI else -10

    if board[0][2] == board[1][1] == board[2][0] and board[0][2] != EMPTY:
        return 10 if board[0][2] == AI else -10

    return 0

def minimax(board, depth, maximizing_player, alpha, beta):
    score = evaluate(board)

    if score == 10:
        return score - depth
    if score == -10:
        return score + depth
    if not empty_cells(board):
        return 0

    if maximizing_player:
        max_eval = float('-inf')
        for i, j in empty_cells(board):
            board[i][j] = AI
            eval = minimax(board, depth + 1, False, alpha, beta)
            board[i][j] = EMPTY
            max_eval = max(max_eval, eval)
            alpha = max(alpha, eval)
            if beta <= alpha:
                break
        return max_eval
    else:
        min_eval = float('inf')
        for i, j in empty_cells(board):
            board[i][j] = HUMAN
            eval = minimax(board, depth + 1, True, alpha, beta)
            board[i][j] = EMPTY
            min_eval = min(min_eval, eval)
            beta = min(beta, eval)
            if beta <= alpha:
                break
        return min_eval

def find_best_move(board):
    best_move = None
    best_score = float('-inf')
    alpha = float('-inf')
    beta = float('inf')

    for i, j in empty_cells(board):
        board[i][j] = AI
        move_score = minimax(board, 0, False, alpha, beta)
        board[i][j] = EMPTY

        if move_score > best_score:
            best_score = move_score
            best_move = (i, j)

    return best_move

def main():
    board = [[EMPTY] * 3 for _ in range(3)]
    print("Welcome to Tic-Tac-Toe!")
    print_board(board)

    while empty_cells(board):
        human_move = None
        while not human_move:
            try:
                i, j = map(int, input("Enter your move (row and column): ").split())
                if board[i][j] == EMPTY:
                    human_move = (i, j)
                else:
                    print("Cell is already occupied. Try again.")
            except (ValueError, IndexError):
                print("Invalid input. Please enter valid row and column.")

        board[i][j] = HUMAN
        print_board(board)

        if empty_cells(board):
            ai_move = find_best_move(board)
            board[ai_move[0]][ai_move[1]] = AI
            print("AI's move:")
            print_board(board)

    score = evaluate(board)
    if score == 10:
        print("AI wins!")
    elif score == -10:
        print("Human wins!")
    else:
        print("It's a draw!")

if __name__ == "__main__":
    main()

