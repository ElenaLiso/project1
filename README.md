def greet():
    print('Добро пожаловать в игру "Крестики-нолики"')
    print("Формат ввода: x y")
    print("x - номер строки")
    print("y - номер столбца")

greet()
tabl=[[' ']*3 for i in range(3)]
def show():
    print(f'  0 1 2')
    for i in range(3):
        row_info = ' '.join(tabl[i])
        print(f'{i} {row_info}')

def ask():
    while True:
        cords = input('Ваш ход: ').split()

        if len(cords) != 2:
            print('Введите 2 координаты! ')
            continue

        x, y = cords

        if not(x.isdigit()) or not(y.isdigit()):
            print('Введите числа! ')
            continue

        x, y = int(x), int(y)

        if 0 > x or x > 2 or 0 > y or y > 2:
            print('Координаты вне диапазона! ')
            continue

        if tabl[x][y] != " ":
            print('Клетка занята! ')
            continue

        return x,y

def chek_win():
    for i in range(3):
        symbols = []
        for j in range(3):
          symbols.append(tabl[i][j])
        if symbols == ["X","X","X"]:
            print("Выиграл Х!!! ")
            return True
        if symbols == ["0","0","0"]:
            print("Выиграл 0!!! ")
            return True

    for i in range(3):
        symbols = []
        for j in range(3):
            symbols.append(tabl[j][i])
        if symbols == ["X", "X", "X"]:
            print("Выиграл Х!!! ")
            return True
        if symbols == ["0","0","0"]:
            print("Выиграл 0!!! ")
            return True

    symbols = []
    for i in range(3):
        symbols.append(tabl[i][i])
    if symbols == ["X", "X", "X"]:
        print("Выиграл Х!!! ")
        return True
    if symbols == ["0", "0", "0"]:
        print("Выиграл 0!!! ")
        return True

    symbols = []
    for i in range(3):
        symbols.append(tabl[i][2-i])
    if symbols == ["X", "X", "X"]:
        print("Выиграл Х!!! ")
        return True
    if symbols == ["0", "0", "0"]:
        print("Выиграл 0!!! ")
        return True
    return False

num = 0
while True:
    num += 1

    show()

    if num % 2 == 1:
        print('Ходит крестик ')
    else:
        print('Ходит нолик ')

    x, y = ask()

    if num % 2 == 1:
        tabl[x][y] = 'X'
    else:
        tabl[x][y] = '0'

    if chek_win():
        break

    if num == 9:
        print('Ничья! ')
        break
