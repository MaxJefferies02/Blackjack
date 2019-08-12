print("Hello!")
import os
import random


def user_name():

    name = ''
    while name == '':
        name = input("What is your name?: ").capitalize()

    if name != "":
         return ("Welcome, " + name + ". I will be your dealer today. Good luck!")

print(user_name())


deck = [2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14]*4


def deal(deck):
    hand = []
    for i in range(2):
        random.shuffle(deck)
        card = deck.pop()
        if card == 11:card = "J"
        if card == 12:card = "Q"
        if card == 13:card = "K"
        if card == 14:card = "A"
        hand.append(card)
    return hand


def play_again():
    
    again = input("Do you want to play again? (Y/N) : ").upper()
    if again == "Y":
        dealer_hand = []
        player_hand = []
        deck = [2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14]*4
        game()
    elif again == "N":
        exit()
        print("Bye!")


def total(hand):
    total = 0
    for card in hand:
        if card == "J" or card == "Q" or card =="K":
            total+=10
        elif card == "A":
            if total >= 11: total += 1
            else: total += 11
        else:
            total += card
    return total

def twist(hand):
    card = deck.pop()
    if card == 11:card = "J"
    if card == 12:card = "Q"
    if card == 13:card = "K"
    if card == 14:card = "A"
    hand.append(card)
    return hand


def clear():
    if os.name == "nt":
        os.system('CLS')
    if os.name == "posix":
        os.system('clear')



def print_results(dealer_hand, player_hand):
    clear()
    print("The dealer has a " + str(dealer_hand) + " for a total of " + str(total(dealer_hand)))
    print("You have a " + str(player_hand) + " for a total of " +str(total(player_hand)))


def blackjack(dealer_hand, player_hand):
    if total(player_hand) == 21:
        print_results(dealer_hand, player_hand)
        print ("Congratulaions!!! You got 21!\n")
        play_again()
    elif total(dealer_hand) == 21:
        print_results(dealer_hand, player_hand)
        print("I got 21! Get riggidy riggidy rekt m8")
        play_again()


def score(dealer_hand, player_hand):
    if total(player_hand) > 21:
        print_results(dealer_hand, player_hand)
        print("You went Bust. You lose!")
        play_again()
    elif total(dealer_hand) == 21:
        print_results(dealer_hand, player_hand)
        print("I got 21! Get riggidy riggidy rekt kid")
        play_again()
    elif total(player_hand) == 21:
        print_results(dealer_hand, player_hand)
        print ("Congratulaions!!! You got 21!\n")
        play_again()
    elif total(dealer_hand) > 21:
        print_results(dealer_hand, player_hand)
        print("I went bust. You Win!")
        play_again()
    elif total(player_hand) > total(dealer_hand):
        print_results(dealer_hand, player_hand)
        print("You are closer to 21. You Win!")
        play_again()
    elif total(player_hand) < total(dealer_hand):
        print_results(dealer_hand, player_hand)
        print("Sorry, I am closer to 21 than you! You lose")
        play_again()
    elif total(player_hand) == total(dealer_hand):
        print("It's a Tie!!")
        play_again()


def game():
    choice = 0
    clear()
    dealer_hand = deal(deck)
    player_hand = deal(deck)
    print("The Dealer is showing a " + str(dealer_hand[0]))
    print("You have a " + str(player_hand) + "  for a total of " + str(total(player_hand)))
    blackjack(dealer_hand, player_hand)

    while choice != "Q":
        choice = input("Do you want to Stick[S], Twist[T], or Quit[Q]").upper()
        if choice == "T":
            twist(player_hand)
            print("Your new hand is...")
            print(player_hand)
            if total(player_hand)>21:
                print("You went bust! You lose!")
                play_again()
        elif choice == 'S':
            while total(dealer_hand) < 17:
                twist(dealer_hand)
                print("Your hand is...")
                print(player_hand)
                print("My hand is...")
                print(dealer_hand)
                if total(dealer_hand) > 21:
                    print("I went bust. You win!")

            score(dealer_hand, player_hand)
            play_again
        elif choice == "Q":
            print("Bye!")
            exit()
            return ' '
print(game())
