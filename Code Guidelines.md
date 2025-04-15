# Clean Code Guidelines

These rules help ensure readable, maintainable code. Follow them strictly. Code is read more often than it is written. Write for clarity, especially your future self.

---

## 1. Naming Conventions

### General Rules
- Use **descriptive, long, and meaningful names**.
- Use **snake_case** for variables and function names.
- Boolean variables should be **phrased as questions** or clear logical conditions.

### Good Examples
```python 
is_user_logged_in = True
number_of_failed_attempts = 3
max_retry_limit = 5
```

### Bad Examples
```python
logged = True 
fail = 3 
x = 5
```

---

## 2. Functions

### Rules
- A function should do **one thing only**.
- Function names should **explain their behavior**.
- Keep functions **short and focused**.
- Avoid side effects unless explicit.

### Good Example
```python
def send_confirmation_email(user_email: str) -> None:     
	# code to send email     
	pass
```

### Bad Example
```python
def do_stuff(x):     
	# sends email, writes to file, modifies global state...     
	pass
```

---

## 3. Single Responsibility Principle (SRP)

### Rules
- Each class/function should have **one reason to change**.
- Split logic across multiple focused modules.
### Good Example
```python
class UserRepository:     
	def save_user(self, user): pass  
class EmailService:     
	def send_welcome_email(self, user): pass
```
### Bad Example
```python
class UserService:     
	def save_user(self, user): pass     
	def send_welcome_email(self, user): pass
```

---

## 4. Comments
### Rules
- Use comments **only** to explain **why**, not **what**.
- If a comment is required to explain a line, the code needs better naming.
### Good Example
```python

# Retry the operation in case of intermittent connection 
retry_operation()
```

### Bad Example
```python
# Increment by 1 
i += 1`
```

---

## 5. DRY Principle (Don’t Repeat Yourself)

### Rules
- Reuse logic instead of duplicating.
- Extract repeated code into functions.

### Good Example
```python
def calculate_discount(price: float, rate: float) -> float:     
	return price * rate
```
### Bad Example
```python 
def regular_discount(price): 
	return price * 0.9 
def special_discount(price):
	return price * 0.85`
```
---
## 6. Avoid Magic Numbers and Strings
### Rules
- Use named constants to improve clarity.
### Good Example
```python
MAX_LOGIN_ATTEMPTS = 5  
if login_attempts > MAX_LOGIN_ATTEMPTS:     
	lock_account()
```
### Bad Example
```python
if login_attempts > 5:     
	lock_account()
```

---
## 7. Error Handling
### Rules
- Use **exceptions**, not return codes.
- Fail **early and loudly**.
### Good Example
```python
def process_order(order):     
	if order is None:         
		raise ValueError("Order cannot be None")     
	# continue
```
### Bad Example
```python
def process_order(order):     
	if order is None:         
		return -1
```

---
## 8. Simplicity (KISS Principle)
### Rules
- Avoid overengineering.
- Prefer clear, linear logic over clever tricks.
### Good Example
```python
def get_status(is_active: bool) -> str:     
	return "active" if is_active else "inactive"`
```
### Bad Example
```python
def get_status(is_active: bool) -> str:     
	if is_active == True:         
		return "active"     
	else:         
		return "inactive"`
```

---
## 9. Encapsulation
### Rules
- Hide internal state. Only expose what’s necessary.
### Good Example
```python
class BankAccount:     
	def __init__(self):         
		self.__balance = 0.0      
	
	def deposit(self, amount: float):         
		if amount > 0:             
			self.__balance += amount      
	
	def get_balance(self):         
		return self.__balance`
```
### Bad Example
```python
class BankAccount:     
	def __init__(self):         
		self.balance = 0.0  # public access`
```

---
## 10. Avoid Side Effects
### Rules
- Functions should not affect external/global state unless clearly documented and expected.
### Good Example
```python
class Order:     
	def add_item(self, item): pass  
class InventoryManager:     
	def update_inventory(self, item): pass
```
### Bad Example
```python
class Order:     
	def add_item(self, item):         
		self.update_inventory(item)  # hidden side effect`
```

---
## 11. Testing
### Rules
- Write unit tests.
- Prefer Test-Driven Development (TDD).
- Use descriptive test names.
### Good Example
```python
def test_calculate_discount_applies_correct_rate():     
	assert calculate_discount(100.0, 0.9) == 90.0`
```

---
## 12. Consistent Formatting
### Rules
- Uniform indentation, spacing, and line breaks.
- Use formatters (e.g., `black`) and linters (e.g., `flake8`).
### Good Example
```python
def calculate_discount(price: float) -> float:     
	if price > 100:         
		return price * 0.9     
	return price
```
### Bad Example
```python
def calculate_discount(price):if price>100:return price*0.9;return price
```

---
## 13. Refactor Often
### Rules
- Don’t wait. Refactor as soon as clarity can be improved.
### Good Example
```python
def process():     
	handle_authentication()     
	handle_transaction()
```
### Bad Example
```python
def process():     
	if condition1:         
		# logic 1     
	if condition2:         
		# logic 2`
```

---
## Summary
- **Clarity over brevity**.
- **Meaningful names** everywhere.
- **One purpose per unit** (function/class).
- **No repetition**.
- **Fail fast**.
- **Simple > clever**.