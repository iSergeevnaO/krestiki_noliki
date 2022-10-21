# krestiki_noliki
<print("_" * 9, "КРЕСТИКИ-НОЛИКИ.", "_" * 9)
#1. Создаем иговое поле
field = list(range(1, 10))
#создаем функцию для рисования игры
def draw_field(field):
    print('-' * 13)
    for i in range(3):
        print('|', field[0 + i * 3], '|', field[1 + i * 3], '|', field[2 + i * 3], '|')
        print('-' * 13)

#2. Создаем функцию для ввода аргументов (крестиков и ноликов) в игровое поле.
def take_input(player_token):
    valid = False
    while not valid:
        player_answer = input("Ваш ход " + player_token + "? ")
        try:
            player_answer = int(player_answer)
        except:
            print("Некорректный ввод. Вы уверены, что ввели число?")
            continue
        if player_answer >= 1 and player_answer <= 9:
            if (str(field[player_answer - 1]) not in "XO"):
                field[player_answer - 1] = player_token
                valid = True
            else:
                print("Эта клетка уже занята!")
        else:
            print("Некорректный ввод. Введите число от 1 до 9.")

#3. Создаем функцию, которая проверяет игровое поле.
# Создаем кортеж с выигрышными координатами и проходимся циклом for по нему.
#Если символы во всех трех заданных клетках равны – возвращаем выигрышный символ, иначе – возвращаем значение False.
# Непустая строка(выигрышный символ) при приведении ее к логическому типу вернет True.
def check_win(field):
    win_coord = ((0, 1, 2), (3, 4, 5), (6, 7, 8), (0, 3, 6), (1, 4, 7), (2, 5, 8), (0, 4, 8), (2, 4, 6))
    for each in win_coord:
        if field[each[0]] == field[each[1]] == field[each[2]]:
            return field[each[0]]
    return False
#4. В данной функции создаем цикл while.
# Цикл выполняется пока один из игроков не выиграл.
# В данном цикле мы выводим игровое поле, принимаем ввод пользователя, при этом определяя токен(икс или нолик) игрока.
# Ждем, когда переменная counter станет больше 4 для того, чтобы избежать заведомо ненужного вызова функции check_win.
# Переменная tmp была создана для того, чтобы лишний раз не вызывать функцию check_win.
def main(field):
    counter = 0
    win = False
    while not win:
        draw_field(field)
        if counter % 2 == 0:
            take_input("X")
        else:
            take_input("O")
        counter += 1
        if counter > 4:
            tmp = check_win(field)
            if tmp:
                print(tmp, "Выиграл!!!")
                win = True
                break
        if counter == 9:
            print("Ничья!")
            break
    draw_field(field)

main(field)

input("Нажмите Enter для выхода!")>
