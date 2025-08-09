import random
import time

# Функция приветствия и введения в сюжет
def intro():
    print("Добро пожаловать в древний особняк, наполненный тайнами.\n")
    time.sleep(1)
    print("Вы очнулись в полной темноте и поняли, что оказались заперты здесь.\n")
    time.sleep(1)
    print("Вам предстоит пройти испытание и выбраться отсюда живым!\n")
    time.sleep(1)
    print("Ваш первый шаг — решить, куда идти дальше:\n")
    time.sleep(1)
    print("Вы видите перед собой три двери:")
    print("Библиотека, Кухня и Спальня.\n")

# Выбор первой комнаты
def choose_room():
    while True:
        room = input("Куда отправитесь первым делом?\n(a) Библиотека\n(b) Кухня\n(c) Спальня\n").strip().lower()
        
        if room in ['a', 'b', 'c']:
            break
        else:
            print("Некорректный ввод. Пожалуйста, выберите a, b или c.")
            
    return room

# Библиотека
def library_scene():
    print("\nВы входите в библиотеку. Здесь царит тишина и запах старых книг.\n")
    time.sleep(1)
    print("Посередине комнаты массивный стол с горящей свечой.\n")
    time.sleep(1)
    action = input("Что будете делать?\n(a) Осмотреть свечи\n(b) Прочитать книгу\n(c) Искать ключ\n").strip().lower()
    
    if action == 'a':
        print("\nСвеча внезапно гаснет, появляется призрак и предупреждает вас о скрытой ловушке впереди.\n")
        time.sleep(1)
        print("Вы решили вернуться назад.")
        return False
    elif action == 'b':
        print("\nКнига рассказывает легенду древнего замка и подсказывает секрет выхода...\n")
        time.sleep(1)
        print("Теперь вы знаете, что одна из дверей ведёт к свободе.")
        return True
    else:
        print("\nВы ищете ключ, но ничего не находите.")
        return False

# Кухня
def kitchen_scene():
    print("\nВы попадаете на кухню. Там темно и тихо.\n")
    time.sleep(1)
    print("На столе лежит нож и книга рецептов.\n")
    time.sleep(1)
    action = input("Что выберете?\n(a) Взять нож\n(b) Читать рецепт\n(c) Проверить шкафчики\n").strip().lower()
    
    if action == 'a':
        print("\nВы берёте нож, чувствуя себя увереннее.")
        return True
    elif action == 'b':
        print("\nРецепт обещает приготовить магический пирог, но ингредиентов нет.")
        return False
    else:
        print("\nШкафчик закрыт, а рядом вдруг слышится шёпот: 'Помоги мне!'")
        help_decision = input("Поддержите говорящего? (Да/Нет)\n").strip().lower()
        if help_decision == 'да':
            print("\nГолос благодарит вас и открывает проход к следующему этапу.")
            return True
        else:
            print("\nВы игнорируете голос, но чувствуете тревогу.")
            return False

# Спальня
def bedroom_scene():
    print("\nВы открываете дверь спальни. Комната мрачная и пустая.\n")
    time.sleep(1)
    print("Единственное освещение исходит от ночника возле кровати.\n")
    time.sleep(1)
    action = input("Что хотите сделать?\n(a) Заглянуть под кровать\n(b) Подойти к окну\n(c) Включить свет\n").strip().lower()
    
    if action == 'a':
        print("\nПод кроватью спрятан ключ от одной из комнат.")
        return True
    elif action == 'b':
        print("\nЗа окном виднеются зловещие тени, заставляя ваше сердце биться быстрее.")
        return False
    else:
        print("\nСвет включается, и вы замечаете картину на стене, изображающую побег из замка.")
        return True

# Финальная сцена
def final_challenge(found_items):
    print("\nВы дошли до последней комнаты.")
    time.sleep(1)
    print("Там большой сундук, покрытый пылью.")
    time.sleep(1)
    combination = ''.join(random.sample('ABCDEF', k=3)) # Случайная комбинация замков
    guess = input(f"Введите комбинацию из трех букв ({combination}) в верхнем регистре: ").upper()
    
    if guess == combination or found_items >= 2:
        print("\nВы открыли замок и нашли карту выхода из особняка.")
        print("Поздравляем! Вы спаслись!")
    else:
        print("\nЗамок не открылся. Ваш путь закончился здесь.")

# Главная функция игры
def main_game():
    intro()   # Приветствие и введение
    found_items = 0  # Количество найденных предметов
    
    first_room = choose_room()
    
    if first_room == 'a':
        result = library_scene()
        if result:
            found_items += 1
    elif first_room == 'b':
        result = kitchen_scene()
        if result:
            found_items += 1
    else:
        result = bedroom_scene()
        if result:
            found_items += 1
    
    second_room = choose_room()
    
    if second_room != first_room:
        if second_room == 'a':
            result = library_scene()
            if result:
                found_items += 1
        elif second_room == 'b':
            result = kitchen_scene()
            if result:
                found_items += 1
        else:
            result = bedroom_scene()
            if result:
                found_items += 1
                
    final_challenge(found_items)

# Запускаем игру
if __name__ == "__main__":
    main_game()
