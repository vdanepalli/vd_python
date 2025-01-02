# OpenEDG Python Institute: Programming with Python Professional Certificate

- [OpenEDG Python Institute: Programming with Python Professional Certificate](#openedg-python-institute-programming-with-python-professional-certificate)
  - [Python Essential Training](#python-essential-training)
  - [Python Object-Oriented Programming](#python-object-oriented-programming)
  - [Level Up: Python](#level-up-python)

## Python Essential Training

## Python Object-Oriented Programming

## Level Up: Python

```py
# Find Prime Factors

def get_prime_factors(number):
    factors = []
    divisor = 2
    while divisor <= number:
        if number % divisor == 0:
            factors.append(divisor)
            number = number // divisor
        else:
            divisor += 1
    return factors
```


```py
# Identify a Palindrome 

import re

def is_palindrome(phrase):
    forwards = ''.join(re.findall(r'[a-z]+', phrase.lower()))
    backwards = forwards[::-1]
    return forwards == backwards
```

```py
# Sort a string of words

def sort_words(input):
    words = input.split()
    words = [w.lower() + w for w in words]
    words.sort()
    words = [w[len(w)//2:] for w in words]
    return ' '.join(words)

def sort_words(words):
    return ' '.join(sorted(words.split(), key=str.casefold)) # str.casefold ensures case insensitive sort
```

```py
# Find all list items 

def index_all(search_list, item):
    index_list = []
    for index, value in enumerate(search_list):
        if value == item:
            index_list.append([index])
        elif isinstance(search_list[index], list):
            for i in index_all(search_list[index], item):
                index_list.append([index] + i)
    return index_list
```

```py
# Play the waiting game

import time 
import random

def waiting_game():
    target = random.randint(2, 4) # target seconds to wait
    print(f'\n Your target time is {target} secodns')

    input(' --- Press Enter to Begin ---')
    start = time.perf_counter()

    input(f'\n... Press Enter again after {target} seconds ...')
    elapsed = time.perf_counter() - start

    print(f'\n Elapsed time: {elapsed: .3f} seconds')
    
    if elapsed == target:
        print('(Unbelievable! Perfect timing!)')
    elif elapsed < target:
        print(f'({target - elapsed : .3f} seconds too fast)')
    else:
        print(f'({elapsed - target: .3f} seconds too slow)')
```

```py
# Save a dictionary

# pickling --> process that serializes the python object converting it into a bite stream that can be saved into a file

import pickle

def save_dict(dict_to_save, file_path):
    with open(file_path, 'wb') as file:
        pickle.dump(dict_to_save, file)
    
def load_dict(file_path):
    with open(file_path, 'rb') as file:
        retunr pickle.load(file)  

test_dict = {5: 'a', 3: 's', 9: 'h'}
save_dict(test_dict, 'ash.pickle')
recovered = load_dict('ash.pickle')
```


```py
# schedule a function 

import sched # general purpose event scheduler
import time 

def schedule_function(event_time, function, *args):
    s = sched.scheduler(time.time, time.sleep)
    s.enterabs(event_time, 1, function, argument=args)
    print(f'{function.__name__} () scheduled for {time.asctime(time.localtime(event_time))}')
    s.run()

schedule_function(time.time() + 1, print, 'Howdy!', 'How are you?')
```


```py
# Send an email 

import smtplib

SENDER_EMAIL = 'vdanepalli@gmail.com'
SENDED_PASSWORD = 'dkasjjkfascjnscj'

def send_email(receiver_email, subject, body):
    message = f'Subject: {subject} \n\n {body}'
    with smtplib.SMTP('smtp.office365.com', 587) as server: # context manager; automatically closes  
        server.starttls()
        server.login(SENDER_EMAIL, SENDER_PASSWORD)
        server.sendmail(SENDER_EMAIL, receiver_email, message)
```


```py
# Simulate Dice

from random import randint
from collections import Counter

def roll_dice(*dice, num_trials=1_000_000):
    counts = Counter()
    for _ in range(num_trials):
        counts[sum((randint(1, sides) for sides in dice))] += 1
    
    print('\n Outcome \t Probability')

    for outcome in range(len(dice), sum(dice)+1):
        print(f'{outcome} \t {counts[outcome] * 100 / num_trials: 0.2f}%')

roll_dice(4, 6, 6 ) # percentages for 4 to 16
```

```py
# count unique words

import re 
import collections

def count_words(path):
    with open(path, 'r', encoding='utf-8') as file:
        all_words = re.findall(r"[0-9a-zA-Z-']+", file.read())
        all_words = [word.upper() for word in all_words]
        print(f'\n Total Words: {len(all_words)}')

        word_counts = collections.Counter(all_words)

        print('\n Top 20 Words:')

        for word in word_counts.most_common(20):
            print(f'{word[0]}\t{word[1]}')
```