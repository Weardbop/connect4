import numpy as np, pygame, sys, random

ROWS = 6
COLUMNS = 7
SQUARE_SIZE = 100

width = COLUMNS * SQUARE_SIZE
height = ROWS * SQUARE_SIZE
size = (width, height)
screen = pygame.display.set_mode(size)
board = None

RED = (255, 0, 0)
YELLOW = (255, 255, 0)
BLUE = (0, 0, 255)
WHITE = (255, 255, 255)
BLACK = (0, 0, 0)

RADIUS = int(SQUARE_SIZE / 2 - 10)

game_over = False
player_turn = 1


def create_board():
    global board
    board = np.zeros((ROWS, COLUMNS))


def drop_piece(row, col, piece):
    global board
    board[row][col] = piece


def is_full(col):
    if board[0][col] != 0:
        return True
    else:
        return False


def get_next_open_row(col):
    for r in range(ROWS - 1, -1, -1):
        if board[r][col] == 0:
            return r


def check_win(player):
    # Check horizontal win
    for c in range(COLUMNS - 3):
        for r in range(ROWS - 1, -1, -1):
            if board[r][c] == player and board[r][c + 1] == player and \
                    board[r][c + 2] == player and board[r][c + 3] == player:
                return True

    # Check vertical win
    for c in range(COLUMNS):
        for r in range(ROWS - 1, 1, -1):
            if board[r][c] == player and board[r - 1][c] == player and \
                    board[r - 2][c] == player and board[r - 3][c] == player:
                return True

    # Check positively sloped diagonal win
    for c in range(COLUMNS - 3):
        for r in range(ROWS-1, 1, -1):
            if board[r][c] == player and board[r - 1][c + 1] == player and \
                    board[r - 2][c + 2] == player and board[r - 3][c + 3] == player:
                return True

    # Check negatively sloped diagonal win
    for c in range(COLUMNS - 3):
        for r in range(2, 0, -1):
            if board[r][c] == player and board[r + 1][c + 1] == player and \
                    board[r + 2][c + 2] == player and board[r + 3][c + 3] == player:
                return True


def render_board():
    for c in range(COLUMNS):
        for r in range(ROWS):
            pygame.draw.rect(screen, BLUE, (c * SQUARE_SIZE, r * SQUARE_SIZE, SQUARE_SIZE, SQUARE_SIZE))
            if board[r][c] == 0:
                pygame.draw.circle(screen, WHITE, (int(c * SQUARE_SIZE + SQUARE_SIZE / 2),
                                                   int(r * SQUARE_SIZE + SQUARE_SIZE / 2)), RADIUS)
            elif board[r][c] == 1:
                pygame.draw.circle(screen, RED, (int(c * SQUARE_SIZE + SQUARE_SIZE / 2),
                                                 int(r * SQUARE_SIZE + SQUARE_SIZE / 2)), RADIUS)
            elif board[r][c] == 2:
                pygame.draw.circle(screen, YELLOW, (int(c * SQUARE_SIZE + SQUARE_SIZE / 2),
                                                    int(r * SQUARE_SIZE + SQUARE_SIZE / 2)), RADIUS)

    pygame.display.update()


def game_end():
    print("Game Over")


def process_event():
    global game_over, player_turn

    if player_turn == 1:
        for event in pygame.event.get():
            if event.type == pygame.KEYDOWN:
                placed = False
                if event.key == pygame.K_0 or event.key == pygame.K_1 or event.key == pygame.K_2 or event.key == pygame.K_3 \
                        or event.key == pygame.K_4 or event.key == pygame.K_5 or event.key == pygame.K_6:
                    col = int(pygame.key.name(event.key))

                    if not is_full(col):
                        row = get_next_open_row(col)
                        drop_piece(row, col, player_turn)
                        placed = True
                        if check_win(player_turn):
                            game_over = True

                #print(board)
                render_board()

                if placed:
                    if player_turn == 1:
                        player_turn = 2


            if event.type == pygame.QUIT:
                sys.exit()

    if player_turn == 2:
        col = random.randint(0,6)
        placed = False

        if not is_full(col):
            row = get_next_open_row(col)
            drop_piece(row, col, player_turn)
            placed = True
            if check_win(player_turn):
                game_over = True

        # print(board)
        render_board()

        if placed:
            if player_turn == 2:
                player_turn = 1



def main():
    pygame.init()
    pygame.display.set_caption("Connect-4")

    create_board()
    #print(board)
    render_board()

    pygame.display.update()

    while not game_over:
        process_event()
    else:
        game_end()


if __name__ == "__main__":
    main()
