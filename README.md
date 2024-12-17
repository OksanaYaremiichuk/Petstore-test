Запит на додавання нової тваринки (https://petstore.swagger.io/v2/pet)
Disclaimer))
Тести написані згідно мого уявлення про вимоги до схожих запитів, а не згідно реальної реалізації, так як там мінімум валідації

1. Успішний запит тільки з обов'язковими полями
	Кроки:
	1. Заповнити поля ("id","photoUrls","tags") коректними даними
	2. Відправити запиті
	3. Перевірити запис в базі
	
	Очікуваний результат: Отримуємо статус код 200, в респонсі повертаються дані, що були передані в реквесті, 
	в базі додається запис з даними, що були передані в запиті
	
2. Успішний запит з усіма можливими полями
	Кроки:
	1. Заповнити всі поля в запиті коректними даними
	2. Відправити запит
	3. Перевірити запит в базі
	
	Очікуваний результат: Отримуємо статус код 200, в респонсі повертаються дані, що були передані в реквесті, 
	в базі додається запис з даними, що були передані в запиті
	
3. 409 помилка, при спробі реєстрації з існуючим Id
	Кроки:
	1. Заповнити всі поля унікальними даними
	2. Використати існуючий Id повторно
	3. Відправити запит
	
	Очікуваний результат: Отримуємо 409 помилку з описом, що переданий Id уже існує, інформація в базі по переданому Id не змінилася після запиту
	
4. Успішний запит, де усі обов'язкові поля окрім Id дублюються
	Кроки:
	1. Заповнити всі поля значеннями іншого об'єкту з бази
	2. Використати унікальний Id
	3. Відправити запит
	
	Очікуваний результат: Отримуємо статус код 200, в респонсі повертаються дані, що були передані в реквесті, 
	в базі додається запис з даними, що були передані в запиті

5. 400 помилка при запиті з невалідним для поля форматом даних (id) - окремі кейси для інших полів, тут для прикладу один тест
	Кроки: 
	1. В полі Id передати GUID
	2. Відправити запит
	
	Очікуваний результат: Отримуємо 400 помилку з описом, що переданий формат не відповідає int, додавання нового об'єкту в базі не відбулося

6. 400 помилка при вказуванні статусу не зі словника
	Кроки:
	1. Використати статус, що не передбачено для цього параметру в форматі string
	2. Відправити запит
	
	Очікуваний результат: Отримуємо 400 помилку з описом, що передане значення не відповідає допустим для цього параметру, 
	додавання нового об'єкту в базі не відбулося
	
7. 405 помилка при використанні невідповідного методу
	Кроки:
	1. Відправити запит змінивши метод
	
	Очікуваний результат: Отримуємо 405 помилку з описом - Invalid input (згідно свагеру),
	додавання нового об'єкту в базі не відбулося
	
8. Успішний запит з токеном користувача, який має права для додавання нових сутностей в стор (адмін)
	Кроки:
	1. Створити токен користувача з правом додавання нових сутностей
	2. Виконати запит на додавання нової тваринки з отриманим токеном
	
	Очікуваний результат: Отримуємо статус код 200, в респонсі повертаються дані, що були передані в реквесті, 
	в базі додається запис з даними, що були передані в запиті
	
9. 403 помилка на запит з невідповідним токеном (покупець)
	Кроки:
	1. Створити токен користувача без права додавання нових сутностей
	2. Виконати запит на додавання нової тваринки з отриманим токеном
	
	Очікуваний результат: Отримуємо 403 помилку з описом, що користувач не має доступу до даного функціоналу, додавання нового об'єкту в базі не відбулося

10. 401 помилка на запит без токена
	Кроки:
	1. Заповнити запит даними
	2. Відправити запит не використовуючи авторизації
	
	Очікуваний результат: Отримуємо 401 помилку, додавання нового об'єкту в базі не відбулося
