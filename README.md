# OOP_for_Data-Analysis
Object-Oriented Programming (OOP) – Classes, Objects &amp; Methods

### Exercise 1
1. Create a Student class with:

 - attributes: name, course, marks (a list of numbers)
 - methods:
   - average() → returns the average mark
   - grade() → returns 'A' ≥70, 'B' 60–69, 'C' 50–59, 'D' <50

#### Solution
``` python
class Student:
    def __init__(self,name,course,marks):
        self.name =name
        self.course=course
        self.marks= marks
    
    def average(self):
        if len(self.marks)==0:
            return 0
        return sum(self.marks)/len(self.marks)
    
    def grade(self):
        avg=self.average()

        if avg >= 70:
            return 'A'
        elif avg >= 60:
            return 'B'
        elif avg >= 50:
            return 'C'
        else:
            return 'D'

student1 = Student("Carol", "Data Analytics", [65, 70, 80, 75])

print("Name:", student1.name)
print("Course:", student1.course)
print("Average:", student1.average())
print("Grade:", student1.grade())
```
#### Output 
```
student1 = Student("Carol", "Data Analytics", [65, 70, 80, 75])

print("Name:", student1.name)
print("Course:", student1.course)
print("Average:", student1.average())
print("Grade:", student1.grade())
```

### Exercise 2
2. Create Product and Store:

- Product same as earlier (sku, name, category, price, quantity).
- Store methods:
  - add_product(product)
  - sell(sku, qty) — reduce stock (raise if insufficient)
  - report() — prints each product: sku, name, qty, total_value
- Add error handling for selling more than in stock.
#### Solution
```python
class product:
    def __init__(self,sku,name,category,price,quantity):
        self.name=name
        self.sku= sku
        self.category=category
        self.price= price
        self.quantity=quantity
class store:
    def __init__(self,product):
        self.product =product

    def add_product(self):#Add product Item
       
        print(self.product.name)

    def sell(self,qty):
        if qty <= 0:
            print("Quantity Must be greater 0")
        elif self.product.quantity ==0:
            print("Quantity is out of stock")
        elif qty >self.product.quantity:
            print(f"Available quantity is:{self.product.quantity}")
        else:
            self.product.quantity = self.product.quantity - qty
            print(f"Remaining stock:{self.product.quantity} ")
        
    
    def report(self):
        print(f"product_sku {self.product.sku}")
        print(f"product_name {self.product.name}")
        print(f"product_qty {self.product.quantity}")
        print(f"product_totalvalue {self.product.price *self.product.quantity}")


item =product("SKU1232","Extension","Electricals",400,10)
store1= store(item)
store1.add_product()
store1.sell(12)
store1.report()
```
#### Output
```
item =product("SKU1232","Extension","Electricals",400,10)
store1= store(item)
store1.add_product()
store1.sell(12)
store1.report()
```

### Exercise 3
3. Build a small SalesReport class:

- It should accept a list of Transaction objects.
- Provide methods:
  - revenue_by_product() → returns a dict {sku: revenue}
  - top_n_products_by_revenue(n) → returns list of tuples [(sku, revenue), ...] sorted desc
#### Solution
```python
class Transaction:
    def __init__(self, sku, price, quantity):
        self.sku = sku
        self.price = price
        self.quantity = quantity

    def revenue(self):
        return self.price * self.quantity


class SalesReport:
    def __init__(self, transactions):
        self.transactions = transactions

    def revenue_by_product(self):
        totals = {}

        for t in self.transactions:
            sku = t.sku
            totals[sku] = totals.get(sku, 0) + t.revenue()

        return totals

    def top_n_products_by_revenue(self, n):
        totals = self.revenue_by_product()

        sorted_products = sorted(
            totals.items(),
            key=lambda x: x[1],
            reverse=True
        )

        return sorted_products[:n]

t1 = Transaction("SKU1", 100, 2)
t2 = Transaction("SKU2", 200, 1)
t3 = Transaction("SKU1", 100, 3)

transactions = [t1, t2, t3]

report = SalesReport(transactions)

print(report.revenue_by_product())
print(report.top_n_products_by_revenue(2))
```
#### Output
```
{'SKU1': 500, 'SKU2': 200}
[('SKU1', 500), ('SKU2', 200)]
```

