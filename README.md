# Pythonchik
import random
znachok_player='\033[31m' + 'O' '\033[39m'
znachok_machina='\033[34m' + 'X' '\033[39m'
board = list(range(1, 10))
def doska(board):
    print("-" * 13)
    for i in range(3):
        print("|", board[0 + i * 3], "|", board[1 + i * 3], "|", board[2 + i * 3], "|")
        print("-" * 13)


def polzovatel():
    proverka = False
    while not proverka:
        player_answer = int(input("Куда поставим "+znachok_player+"?"))
        if 1 <= player_answer <= 9:
            if str(board[player_answer - 1])!=znachok_machina and str(board[player_answer - 1])!=znachok_player:
                board[player_answer - 1] = znachok_player
                proverka = True
            else:
                print("Эта клетка уже занята!")
        else:
            print("Некорректный ввод. Введите число от 1 до 9")


def check_pobeda(board):
    pobeda_coord = ((0, 1, 2), (3, 4, 5), (6, 7, 8), (0, 3, 6), (1, 4, 7), (2, 5, 8), (0, 4, 8), (2, 4, 6))
    for k in pobeda_coord:
        if board[k[0]]==board[k[1]]==board[k[2]]:
            if board[k[0]]==znachok_machina:
                return "победил я(компьютер)"
            else:
                return "Ты победил людишка"
    return "ничья"
def computer_move():
    pobeda_coord = ((0, 1, 2), (3, 4, 5), (6, 7, 8), (0, 3, 6), (1, 4, 7), (2, 5, 8), (0, 4, 8), (2, 4, 6))
    check=True
    for kk in pobeda_coord:
        if board[kk[0]]==board[kk[1]] and check==True and board[kk[2]]!=znachok_machina and board[kk[2]]!=znachok_player:
            board[kk[2]] = znachok_machina
            check=False
        elif board[kk[1]]==board[kk[2]] and check==True and board[kk[0]]!=znachok_machina and board[kk[0]]!=znachok_player:
            board[kk[0]] = znachok_machina
            check=False
        elif board[kk[0]]==board[kk[2]] and check==True and board[kk[1]]!=znachok_machina and board[kk[1]]!=znachok_player:
            board[kk[1]] = znachok_machina
            check=False
    if check==True :
        while check==True:
            randomchik = random.randint(0,8)
            if board[randomchik]!=znachok_machina and board[randomchik]!=znachok_player:
                board[randomchik]=znachok_machina
                check=False


def main(board):
    while check_pobeda(board)=="ничья":
        computer_move()
        if check_pobeda(board) != "ничья" :
            break
        doska(board)
        polzovatel()
        if check_pobeda(board) != "ничья":
            break


main(board)
doska(board)
print(check_pobeda(board))
