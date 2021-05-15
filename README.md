# simple-2-player-game


import random


'''
checks if there are four connected slots horizontally
'''
def horizontal(matrix, player1, player2):
    winning1 = False
    winning2 = False

    for line in matrix:
        wino1 = 0
        wino2 = 0
        if winning1 == True or winning2 == True:
            break
        for i in range(0, len(line) - 1):
            if line[i] != 0:
                if line[i] == player1:
                    if line[i] == line[i + 1]:
                        wino1 += 1
                        if wino1 == 3:
                            winning1 = True
                            break
                    else:
                        wino1 = 0
                else:
                    if line[i] == line[i + 1]:
                        wino2 += 1
                        if wino2 == 3:
                            winning2 = True
                            break
                    else:
                        wino2 = 0
    if winning1 == True:
        return player1
    if winning2 == True:
        return player2

'''
checks if there are 4 connected slots vertically

'''

def vertical(matrix, player1, player2):
    winning1 = False
    winning2 = False
    wino1 = 0
    wino2 = 0

    for i in range(0, len(matrix[0])):
        if winning1 == True or winning2 == True:
            break
        lino = 0
        lino1 = 0
        for j in range(0, len(matrix) - 1):
            if matrix[j][i] != 0:
                if matrix[j][i] == player1:
                    if matrix[j][i] == matrix[j + 1][i]:
                        lino += 1
                        if lino == 3:
                            winning1 = True
                            break
                    else:
                        lino = 0
                else:
                    if matrix[j][i] == matrix[j + 1][i]:
                        lino1 += 1
                        if lino1 == 3:
                            winning2 = True
                            break
                    else:
                        lino1 = 0


    if winning1 == True:
        return 1
    if winning2 == True:
        return 2

'''
checks if there are four connected slots diagonally

'''

def diagonal(matrix, player1, player2):
    winning1 = False
    winning2 = False
    winningback1 = False
    winningback2 = False
    max_col = len(matrix[0])
    max_row = len(matrix)
    fdiag = [[] for _ in range(max_row + max_col - 1)]
    bdiag = [[] for _ in range(len(fdiag))]
    min_bdiag = -max_row + 1
    for x in range(max_col):
        for y in range(max_row):
            fdiag[x + y].append(matrix[y][x])
            bdiag[x - y - min_bdiag].append(matrix[y][x])


    for line in fdiag:
        if winning2 == True or winning1 == True:
            break
        lino = 0
        lino1 = 0
        for i in range(0, len(line) - 1):
            if line[i] == player1:
                if line[i] == line[i + 1]:
                    lino += 1
                    if lino == 3:
                        winning1 = True
                        break
                else:
                    lino = 0
            else:
                if line[i] == player2:
                    if line[i] == line[i + 1]:
                        lino1 += 1
                        if lino1 == 3:
                            winning2 = True
                            break
                    else:
                        lino1 = 0

    if winning1 == True:
        return 1
    elif winning2 == True:
        return 2
    else:
        for line in bdiag:
            if winningback1 == True or winningback2 == True:
                break
            lino = 0
            lino1 = 0
            for i in range(0, len(line) - 1):
                if line[i] == player1:
                    if line[i] == line[i + 1]:
                        lino += 1
                        if lino == 3:
                            winningback1 = True
                            break
                    else:
                        lino = 0
                else:
                    if line[i] == player2:
                        if line[i] == line[i + 1]:
                            lino1 += 1
                            if lino1 == 3:
                                winningback2 = True
                                break
                        else:
                            lino1 = 0
        if winningback1 == True:
            return 1
        elif winningback2 == True:
            return 2



'''

test code

'''
matrix = []

for i in range(6):
    matrix.append([0, 0, 0, 0, 0, 0, 0])

#matrix.append([0, 0, 0, 0, 0, 0, 0] for i in range(6))

solved1 = False
solved2 = False
player1 = int(input())
player2 = int(input())


while solved1 == False and solved2 == False:
    print(f'Player 1, please choose a column: ')
    column1 = int(input())
    row1 = random.randint(0, len(matrix) - 1)
    if matrix[row1][column1] == 0:
        matrix[row1][column1] = player1
    print(matrix)
    horizontal1 = horizontal(matrix, player1, player2)
    if horizontal1 == 1:
        solved1 = True
        break
    vertical1 = vertical(matrix, player1, player2)
    if vertical1 == 1:
        solved1 = True
        break

    diagonal1 = diagonal(matrix, player1, player2)
    if diagonal1 == 1:
        solved1 = True
        break
    print(f'Player 2, please choose a column: ')
    column2 = int(input())
    row2 = random.randint(0, len(matrix) - 1)
    if matrix[row2][column2] == 0:
        matrix[row2][column2] = player2
    print(matrix)
    horizontal2 = horizontal(matrix, player1, player2)
    if horizontal2 == 2:
        solved2 = True
        break
    vertical2 = vertical(matrix, player1, player2)
    if vertical2 == 2:
        solved2 = True
        break

    diagonal2 = diagonal(matrix, player1, player2)
    if diagonal2 == 2:
        solved2 = True
        break



if solved1 == True:
    print('Player 1 wins')
if solved2 == True:
    print('Player 2 wins')
