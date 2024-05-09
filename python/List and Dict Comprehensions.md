Comprehensions - це зручний і лаконічний спосіб створити `list` або `dict`.
## List Comprehension
---
List Comprehension пропонує коротший синтаксис, коли ви хочете створити новий список на основі значень існуючого списку, списку діапазонів або рядка — загалом, на об’єктах, що повторюються. Це значно швидше, ніж обробка списку за допомогою циклу for.

List comprehension має таку структуру:
```python
result = [expression for element in iterable]
```

- `iterable` - це об'єкт по якому ми будемо проходитися
- `element` - це значення із `iterable` (Каждий елемент)
- `expression` - це модифікований елемент із `iterable`, який буде записаний в фінальний список.
- `result` - це змінна в якій буде записаний цей список

Розлянемо декілька прикладів:
```python
squared_list = [i ** 2 for i in range(5)]		# [0, 1, 4, 9, 16]
upper_letters = [char.upper() for char in "Hello!"]		# ["H", "E", "L", "L", "O", "!"]
double_list = [item * 2 for item in [1, 3, 5, 7]]		# [2, 6, 10, 14]
tuple_values = [fruit for fruit in ("apple", "banana", "orange")]	# ["apple", "banana", "orange"]
```

Давайте подивимося на різницю між створенням списку за допомогою List comprehension і простим циклом `for`.

Цикл `for` не поганий і найпопулярніший спосіб створення списків. Його ліпше використовувати коли модифікаця над елементом не проста, тоїсть складається і 2 сточок чи більше.

Розглянемо приклад задача де каждий елемент потрібно помножити на два, спочатку через цикл `for`:
```python
input_list = [1, 5, 3, 21]
double = []

for item in input_list:
	double.append(item * 2)

print(double)	# [2, 10, 6, 42]
```

Як бачите вийшов доволі громіський код як для такої простої задачі, то давайте подивимося як рішення виглядає із допомогою List comprehension:
```python
input_list = [1, 5, 3, 21]
double = [item * 2 for item in input_list]	# [2, 10, 6, 42]
```

Давайте розглянемо ще два приклада. Перший де буде більш доречно використовувати List comprehension, а другий де цикл `for`.

Перша задача - вам дається список словарів де є два ключа `name` і `age`, потрібно створити список `name` в яких `age` > 18:
```python
people = [ 
	{"name": "Ivan", "age": 18}, 
	{"name": "Mariia", "age": 20}, 
	{"name": "Dariia", "age": 15} 
] 
		  
result_1 = [] 

# рішення черз for
for person in people: 
	if person["age"] >= 18: 
		result_1.append(person["name"]) 

# List coprehension
result_2 = [person["name"] for person in people if person["age"] >= 18] 

# result_1 = result_2 = ["Ivan", "Mariia"]
```

Друга задача це замінити `age` на ключові слова:
- `age < 3` - `Baby`
- `3 <= age < 10` - `Child`
- `10 <= age < 18` - `Teenager`
- `age >= 18` - `adult`

```python
result_1 = [] 
for person in people: 
	if person["age"] < 3: 
		result_1.append({person["name"]: "Baby"}) 
	elif 3 <= person["age"] < 10: 
		result_1.append({person["name"]: "Child"}) 
	elif 10 <= person["age"] < 18:
		result_1.append({person["name"]: "Teenager"}) 
	else: result_1.append({person["name"]: "Adult"}) 
	
result_2 = [ 
	{ person["name"]: "Baby"} if person["age"] < 3 
	else {person["name"]: "Child"}
	if 3 <= person["age"] < 10
	else {person["name"]: "Teenager"}
	if 10 <= person["age"] < 18
	else {person["name"]: "Adult"}
	for person in people ] 
	
# result_1 = result_2 = [{"Ivan": "Adult"}, {"Mariia": "Adult"}, {"Dariia": "Teenager"}]
```
## Conditionals in List Comprehension
---
List comprehansion надає писати умови для елементів які ми хочемо додати до списку:
```python
result_1 = [expression for element in iterable if condition]
result_2 = [expression if condition else default_expression for element in iterable]
```

- `condition` - це умова за якою буде записаний елемент до списку
- `default_expression` - це значення яке буде записано до списку якщо `condition` не вірна

## Dict Comprehension
---
Dict Comprehension - це такийже удобний спосіб як і List comprehension тільи для `dict`. І його синтакси такий:
```python
result = {key: value for element in iterable}
```

- `iterable` - це об'єкт по якому ми будемо проходитися
- `element` - це значення із `iterable` (Каждий елемент)
- `value` - це елемент який необхідний для створення словаря
- `key` - це ключ по якому буде досягатися `value` коли створеться словарь
- `result` - це змінна в якій буде записаний словарь

Приклад:
```python
double_list = {x: x * 2 for x in [1, 3, 5, 7]}	# {1: 2, 3: 6, 5: 10, 7: 14 }

tuple_values = {x: len(x) for x in ("apple", "banana", "orange")}	
# {"apple": 5, "banana": 6, "orange": 6}
```

Якщо ви хочете скопіювати `dict` щоб вони не були привязані до одної адреси в пам'яті то це можна зробити за допомогою `.items()`:
```python
result = {key: value for key, value in dictionary.items()}
```

Або і інші штуки, наприклад:
```python
my_dict  = {"Mariia": 18, "Ivan": 20, "Oleksii": 15}

new_dict = {name: age + 1 for name, age in my_dict.items()}
# {"Mariia": 19, "Ivan": 21, "Oleksii": 16}
```

## Conditionals in Dict Comprehension
---
Якщо ви хочете використовувати `if` в Dict comprehension то сміло використовуйте цей синтаксис:
```python
result = {key: value for element in iterable if condition}
```

`condition` - це умова при якій елемент буде добавлятися в словарь.

Наприклад:
```python
my_dict  = {"Mariia": 18, "Ivan": 20, "Oleksii": 15}
mew_dict = {name: age + 1 for name, age in my_dict.items() if age <= 18}
```

Но ви можете використовувати конструкцію `if-else`:
```python
result = {key: (value if condition else default_value) for element in iterable}
```

`default_expression` - це значення якщо `condition` буде не вірним

Розглянем приклад:
```python
people = [
    {"name": "Ivan", "age": 18}, 
    {"name": "Mariia", "age":20}, 
    {"name": "Dariia", "age": 15}
]

def is_adult(age: int) -> str:
	if age >= 18:
		return  "Yes"
	else:
		return  "No"

adult = {person["name"]: is_adult(person["age"]) for person in people}
# {"Ivan"': "Yes", "Mariia": "Yes", "Dariia": "No"}
```
## Практика
---
1. Double list items
Напиши функцію `double_list_items`, яка повертає список з подвоєнними значеннями зі списку `ls`.

Функція повинна містити **тільки** інструкцію `return`. Використовуй list comprehension.

Приклад:
```python
double_list_items([]) == []
double_list_items([0, -1, 3]) == [0, -2, 6]
```

2. Get user data
Тобі приходять дані про користувачів твоєї компанії. Але ці дані не впорядковані і, щоб полегшити роботу своїх колег, тобі треба їх структурувати. Було б не погано мати таку структуру даних, в якій ти можеш отримати інформацію про користувача, звертаючись за **id** цього користувача.

Напиши функцію `get_users_data`, яка отримує список з даними користувачів.

Список з даними користувачів це список, який складається з кортежів, кожний з яких складається з чотирьох значень: `id`, `username`, `email`, `password` конкретного користувача.

Функція повинна повертати словник, в якому ключі це `id` користувача, а значення цих ключів - також словник з рештою даних: **username**, **email**, **password**.

Функція повинна містити **тільки** інструкцію `return`. Використовуй dict comprehension.

Приклад:
```python
users = [
          (12, 'Maxim', 'maxim@example.com', 'UBg11eub42hge')
        ] # Тільки один користувач
get_users_data(users) == {
    12: {
          'username': 'Maxim',
          'email': 'maxim@example.com',
          'password': 'UBg11eub42hge'
        },
}  # В результаті словник з одним ключем - id користувача


users = [
            (12, 'Maxim', 'maxim@example.com', 'UBg11eub42hge'),
            (13, 'Dmitro', 'dmitro@example.com', 'sdTioT36723fw'),
            (14, 'Roman', 'roman@example.com', 'hbFEkj34NggE2'),
            (15, 'Ivan', 'ivan@example.com', 'sdTioT36723fw'),
        ] # Чотири користувачі

get_users_data(users) == {
    12: {'username': 'Maxim', 'email': 'maxim@example.com', 'password': 'UBg11eub42hge'},
    13: {'username': 'Dmitro', 'email': 'dmitro@example.com', 'password': 'sdTioT36723fw'},
    14: {'username': 'Roman', 'email': 'roman@example.com', 'password': 'hbFEkj34NggE2'},
    15: {'username': 'Ivan', 'email': 'ivan@example.com', 'password': 'sdTioT36723fw'},
} # В результаті словник з чотирьма ключами - id користувачів
```