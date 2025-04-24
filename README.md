import random
import os
import logo
import game_database

print(logo.game_logo)
score = 0

def display_accountinfo(account):
    name = account["name"]
    description = account["description"]
    country = account["country"]
    return f"{name}, a {description}, from {country}"

def check_answer(guess, followers_1, followers_2):
    if followers_1 > followers_2:
        return guess == 1
    else:
        return guess == 2

continue_flag = True
while continue_flag:
    account_1 = random.choice(game_database.data)
    account_2 = random.choice(game_database.data)

    while account_1 == account_2:
        account_2 = random.choice(game_database.data)

    print(f"Compare 1: {display_accountinfo(account_1)}")
    print(logo.VS)
    print(f"Compare 2: {display_accountinfo(account_2)}")

    guess = int(input("Who has more followers? Type 1 or 2: "))

    followers_count_1 = account_1["followers_count"]
    followers_count_2 = account_2["followers_count"]

    print(f"Account 1 followers: {followers_count_1}")
    print(f"Account 2 followers: {followers_count_2}")

    is_correct = check_answer(guess, followers_count_1, followers_count_2)
    os.system('cls')
    print(logo.game_logo)
    
    if is_correct:
        score += 1
        print(f"You are right! Your score is: {score}")
    else:
        print(f"You are wrong! Final score: {score}")
        continue_flag = False
