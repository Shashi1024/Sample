# Lab Record / Exam Solutions

## 🛠️ MongoDB Windows Setup Guide

**Note:** This setup applies to all "Question 2" database problems below.

1. Open **Command Prompt (cmd)** or **PowerShell**.
2. Type the command: `mongosh`
3. You will see a prompt (e.g., `test>`).
4. **Common Commands** (Use these before running specific answers):
* `show dbs`
* `use <databaseName>`
* `show collections`



---

# 📘 CSE-A

## Set-1

### Question 1: Student Registration Form

**Requirement:** Separate HTML, CSS, and JavaScript files.

**index.html**

```html
<!DOCTYPE html>
<html>
<head>
    <link rel="stylesheet" href="style.css">
</head>
<body>
    <form onsubmit="return validateForm(event)">
        <h2>Student Registration</h2>
        Name: <input type="text" id="name"><br>
        <span id="nameError" class="error"></span><br>
        
        Email: <input type="text" id="email"><br>
        <span id="emailError" class="error"></span><br>
        
        Class: <input type="text" id="classVal"><br>
        <span id="classError" class="error"></span><br>
        
        Fav Subject: <input type="text" id="subject"><br>
        <span id="subjectError" class="error"></span><br>
        
        <button type="submit">Register</button>
    </form>
    <script src="script.js"></script>
</body>
</html>

```

**style.css**

```css
body { background-color: #f0f8ff; font-family: sans-serif; }
form { background-color: white; padding: 20px; width: 300px; border: 1px solid #ccc; }
.error { color: red; font-size: 12px; }
input { margin-bottom: 5px; }

```

**script.js**

```javascript
function validateForm(e) {
    e.preventDefault();
    
    document.getElementById("nameError").innerText = "";
    document.getElementById("emailError").innerText = "";
    
    let email = document.getElementById("email").value.trim();
    let name = document.getElementById("name").value.trim();
    let isValid = true;

    if (!name) {
        document.getElementById("nameError").innerText = "Name is required";
        isValid = false;
    }
    if (!email) {
        document.getElementById("emailError").innerText = "Email is required";
        isValid = false;
    }

    if(isValid) {
        alert("Form Submitted Successfully");
        return true;
    }
    return false;
}

```

### Question 2: Store Inventory Database

```javascript
// Open 'mongosh'
use storeDB

// a) Insert 5 products individually
db.products.insertOne({pid: 1, pname: "Pen", price: 10, stock: 100})
db.products.insertOne({pid: 2, pname: "Book", price: 50, stock: 50})
db.products.insertOne({pid: 3, pname: "Bag", price: 600, stock: 20})
db.products.insertOne({pid: 4, pname: "Box", price: 100, stock: 0})
db.products.insertOne({pid: 5, pname: "Ink", price: 20, stock: 10})

// b) Insert 3 products using array insertion
db.products.insertMany([
    {pid: 6, pname: "Calc", price: 700, stock: 5},
    {pid: 7, pname: "Eraser", price: 5, stock: 0},
    {pid: 8, pname: "Scale", price: 15, stock: 30}
])

// c) Update stock for products priced above 500
db.products.updateMany({ price: { $gt: 500 } }, { $inc: { stock: 10 } })

// d) Delete two products that are out of stock
db.products.deleteMany({ stock: 0 })

```

---

## Set-2

### Question 1: MNC Job Application Form

```html
<!DOCTYPE html>
<html>
<body>
    <div style="width: 500px; margin: auto; border: 1px solid black; padding: 20px;">
        <h2 style="text-align: center; text-decoration: underline;">MNC Job Application</h2>
        <form>
            <div style="margin-bottom: 10px;">
                <label style="width: 150px; display: inline-block;">First Name:</label>
                <input type="text">
            </div>
            <div style="margin-bottom: 10px;">
                <label style="width: 150px; display: inline-block;">Last Name:</label>
                <input type="text">
            </div>
            <div style="margin-bottom: 10px;">
                <label style="width: 150px; display: inline-block;">Gender:</label>
                <input type="radio" name="g"> Male <input type="radio" name="g"> Female
            </div>
            <div style="margin-bottom: 10px;">
                <label style="width: 150px; display: inline-block;">Mobile:</label>
                <input type="number">
            </div>
            
            <h4 style="border-bottom: 1px solid #ccc;">Education Details</h4>
            <div style="margin-bottom: 5px;">10th: <input type="text"></div>
            <div style="margin-bottom: 5px;">Inter: <input type="text"></div>
            <div style="margin-bottom: 5px;">B.Tech: <input type="text"></div>
            
            <div style="margin-top: 10px;">
                <label>Job Experience:</label><br>
                <textarea style="width: 100%;"></textarea>
            </div>
            
            <button type="submit" style="margin-top: 10px; padding: 5px 15px;">Submit</button>
        </form>
    </div>
</body>
</html>

```

### Question 2: Student Database

```javascript
// Open 'mongosh'
use studentDB

// a) Insert 5 documents individually
db.students.insertOne({studentID: 101, Name: "Arun", Branch: "CSE", CGPA: 8.5})
db.students.insertOne({studentID: 102, Name: "Balu", Branch: "ECE", CGPA: 7.0})
db.students.insertOne({studentID: 103, Name: "Cat", Branch: "CSE", CGPA: 9.1})
db.students.insertOne({studentID: 104, Name: "Dev", Branch: "EEE", CGPA: 6.5})
db.students.insertOne({studentID: 105, Name: "Eva", Branch: "MECH", CGPA: 7.5})

// b) Insert 2 documents at a time
db.students.insertMany([
    {studentID: 106, Name: "Fay", Branch: "CSE", CGPA: 8.0},
    {studentID: 107, Name: "Guy", Branch: "IT", CGPA: 7.8}
])

// c) Update values in existing documents
db.students.updateOne({ studentID: 101 }, { $set: { CGPA: 9.0 } })

// d) Delete any 2 student records
db.students.deleteMany({ studentID: { $in: [104, 105] } })

```

---

## Set-3

### Question 1: HTML Calendar

```html
<!DOCTYPE html>
<html>
<body>
    <h2 style="text-align: center;">December 2025</h2>
    <table style="width: 50%; margin: auto; border-collapse: collapse; text-align: center;">
        <tr style="background-color: lightgray;">
            <th style="border: 1px solid black; padding: 10px;">Sun</th>
            <th style="border: 1px solid black; padding: 10px;">Mon</th>
            <th style="border: 1px solid black; padding: 10px;">Tue</th>
            <th style="border: 1px solid black; padding: 10px;">Wed</th>
            <th style="border: 1px solid black; padding: 10px;">Thu</th>
            <th style="border: 1px solid black; padding: 10px;">Fri</th>
            <th style="border: 1px solid black; padding: 10px;">Sat</th>
        </tr>
        <tr>
            <td style="border: 1px solid black; padding: 10px;"></td>
            <td style="border: 1px solid black; padding: 10px;">1</td>
            <td style="border: 1px solid black; padding: 10px;">2</td>
            <td style="border: 1px solid black; padding: 10px;">3</td>
            <td style="border: 1px solid black; padding: 10px;">4</td>
            <td style="border: 1px solid black; padding: 10px;">5</td>
            <td style="border: 1px solid black; padding: 10px;">6</td>
        </tr>
        <tr>
            <td style="border: 1px solid black; padding: 10px;">7</td>
            <td style="border: 1px solid black; padding: 10px;">8</td>
            <td style="border: 1px solid black; padding: 10px;">9</td>
            <td style="border: 1px solid black; padding: 10px;">10</td>
            <td style="border: 1px solid black; padding: 10px;">11</td>
            <td style="border: 1px solid black; padding: 10px;">12</td>
            <td style="border: 1px solid black; padding: 10px;">13</td>
        </tr>
    </table>
</body>
</html>

```

### Question 2: Library Database

```javascript
// Open 'mongosh'
use libraryDB

// a) Insert 5 book records
db.books.insertOne({bookId: 1, title: "C Prog", author: "Dennis", price: 500, qty: 10})
db.books.insertOne({bookId: 2, title: "Java", author: "James", price: 600, qty: 5})
db.books.insertOne({bookId: 3, title: "Python", author: "Guido", price: 400, qty: 8})
db.books.insertOne({bookId: 4, title: "HTML", author: "Tim", price: 300, qty: 15})
db.books.insertOne({bookId: 5, title: "OS", author: "Galvin", price: 700, qty: 4})

// b) Insert 2 records
db.books.insertMany([
    {bookId: 6, title: "Networks", author: "Tanenbaum", price: 800, qty: 6},
    {bookId: 7, title: "AI", author: "Russell", price: 900, qty: 3}
])

// c) Update quantity
db.books.updateOne({ title: "Java" }, { $inc: { qty: 5 } })

// d) Delete books by author
db.books.deleteMany({ author: "Galvin" })

```

---

## Set-4

### Question 1: Restaurant Menu

**Requirement:** Maintain separate HTML, CSS, and JS files.

**index.html**

```html
<!DOCTYPE html>
<html>
<head>
    <link rel="stylesheet" href="style.css">
</head>
<body>
    <div class="header">
        <h1>Spicy Bites</h1>
    </div>
    <div class="container">
        <button onclick="highlightVeg()">Highlight Veg</button>
        <table>
            <tr><th>Dish</th><th>Price</th><th>Category</th></tr>
            <tr class="veg"><td>Salad</td><td>100</td><td>Veg</td></tr>
            <tr class="non-veg"><td>Chicken</td><td>300</td><td>Non-Veg</td></tr>
            <tr class="veg"><td>Paneer</td><td>200</td><td>Veg</td></tr>
        </table>
    </div>
    <script src="script.js"></script>
</body>
</html>

```

**style.css**

```css
.header { position: fixed; top: 0; left: 0; width: 100%; background: orange; text-align: center; padding: 10px; }
.container { margin-top: 80px; padding: 20px; }
table { width: 100%; border-collapse: collapse; margin-top: 10px; }
th, td { border: 1px solid #ccc; padding: 8px; }
tr:hover { background-color: #f0f0f0; }
.highlight { background-color: lightgreen; }

```

**script.js**

```javascript
function highlightVeg() {
    let items = document.getElementsByClassName("veg");
    for(let i=0; i<items.length; i++) {
        items[i].classList.add("highlight");
    }
}

```

### Question 2: React Application

**Component1.css**

```css
.comp1 { background-color: lightblue; padding: 20px; text-align: center; }

```

**Component2.css**

```css
.comp2 { background-color: lightcoral; padding: 20px; text-align: center; }

```

**App.js**

```jsx
import React from 'react';
import './Component1.css';
import './Component2.css';

function Component1() {
    return <div className="comp1"><h1>I am Component 1</h1></div>;
}

function Component2() {
    return <div className="comp2"><h1>I am Component 2</h1></div>;
}

function App() {
    return (
        <div>
            <Component1 />
            <hr />
            <Component2 />
        </div>
    );
}
export default App;

```

---

---

# 📗 CSE-B, C

## Set-1

### Question 1: Time Table

```html
<!DOCTYPE html>
<html>
<body>
    <h2 style="text-align: center;">Class Time Table</h2>
    <table style="width: 80%; margin: auto; border-collapse: collapse; text-align: center;">
        <tr style="background-color: #eee;">
            <th style="border: 1px solid black; padding: 8px;">Day</th>
            <th style="border: 1px solid black; padding: 8px;">9:30-10:20</th>
            <th style="border: 1px solid black; padding: 8px;">10:20-11:10</th>
            <th style="border: 1px solid black; padding: 8px;">11:10-12:00</th>
            <th style="border: 1px solid black; padding: 8px;">Lunch</th>
            <th style="border: 1px solid black; padding: 8px;">1:40-2:30</th>
        </tr>
        <tr>
            <td style="border: 1px solid black; padding: 8px;">Mon</td>
            <td style="border: 1px solid black; padding: 8px;">DS</td>
            <td style="border: 1px solid black; padding: 8px;">IS</td>
            <td style="border: 1px solid black; padding: 8px;">IRS</td>
            <td rowspan="6" style="border: 1px solid black; padding: 8px; vertical-align: middle;">BREAK</td>
            <td style="border: 1px solid black; padding: 8px;">WT Lab</td>
        </tr>
        <tr>
            <td style="border: 1px solid black; padding: 8px;">Tue</td>
            <td colspan="2" style="border: 1px solid black; padding: 8px;">Project Work</td>
            <td style="border: 1px solid black; padding: 8px;">-</td>
            <td style="border: 1px solid black; padding: 8px;">MAD</td>
        </tr>
    </table>
</body>
</html>

```

### Question 2: Employee Database

```javascript
// Open 'mongosh'
use employeeDB

// a) Insert 4 employees
db.employees.insertOne({empId: 1, name: "Alice", salary: 40000, dept: "HR"})
db.employees.insertOne({empId: 2, name: "Bob", salary: 25000, dept: "IT"})
db.employees.insertOne({empId: 3, name: "Charlie", salary: 60000, dept: "Finance"})
db.employees.insertOne({empId: 4, name: "David", salary: 28000, dept: "HR"})

// b) Insert 3 together
db.employees.insertMany([
    {empId: 5, name: "Eve", salary: 35000, dept: "IT"},
    {empId: 6, name: "Frank", salary: 20000, dept: "Admin"},
    {empId: 7, name: "Grace", salary: 50000, dept: "HR"}
])

// c) Update HR salary
db.employees.updateMany({ dept: "HR" }, { $inc: { salary: 5000 } })

// d) Delete low salary
db.employees.deleteMany({ salary: { $lt: 30000 } })

```

---

## Set-2

### Question 1: School Website

**Requirement:** Keep HTML, CSS, and JavaScript in separate files.

**index.html**

```html
<!DOCTYPE html>
<html>
<head>
    <link rel="stylesheet" href="school_style.css">
</head>
<body>
    <div class="header"><h1>City High School</h1></div>
    <div class="content">
        <button onclick="changeColor()">Change Color</button>
        <table id="sportsTable">
            <tr><th>Sport</th><th>Coach</th></tr>
            <tr><td>Cricket</td><td>Mr. Raj</td></tr>
        </table>
    </div>
    <script src="school_script.js"></script>
</body>
</html>

```

**school_style.css**

```css
.header { position: fixed; top: 0; width: 100%; background: navy; color: white; text-align: center; padding: 10px; }
.content { position: relative; top: 80px; padding: 20px; }
table { border-collapse: collapse; border: 1px solid black; width: 50%; margin-top: 10px; }
th, td { border: 1px solid black; padding: 10px; }

```

**school_script.js**

```javascript
function changeColor() {
    document.getElementById("sportsTable").style.backgroundColor = "lightblue";
}

```

### Question 2: React Application

**Component1.css**

```css
.comp1 { background-color: lightblue; padding: 20px; text-align: center; }

```

**Component2.css**

```css
.comp2 { background-color: lightcoral; padding: 20px; text-align: center; }

```

**App.js**

```jsx
import React from 'react';
import './Component1.css';
import './Component2.css';

function Component1() {
    return <div className="comp1"><h1>I am Component 1</h1></div>;
}

function Component2() {
    return <div className="comp2"><h1>I am Component 2</h1></div>;
}

function App() {
    return (
        <div>
            <Component1 />
            <hr />
            <Component2 />
        </div>
    );
}
export default App;

```

---

## Set-3

### Question 1: Adhaar Registration

```html
<!DOCTYPE html>
<html>
<body>
    <div style="width: 400px; margin: 20px auto; padding: 20px; border: 1px solid #ddd;">
        <h2 style="text-align: center;">Adhaar Registration</h2>
        <form>
            <label style="display:block; margin: 5px 0;">First Name:</label>
            <input type="text" style="width: 100%;">
            
            <label style="display:block; margin: 5px 0;">Last Name:</label>
            <input type="text" style="width: 100%;">
            
            <label style="display:block; margin: 5px 0;">Mobile:</label>
            <input type="number" style="width: 100%;">
            
            <label style="display:block; margin: 5px 0;">Address:</label>
            <textarea style="width: 100%;"></textarea>
            
            <div style="margin-top: 15px;">
                <button type="submit" style="background: green; color: white; padding: 5px 10px;">Submit</button>
                <button type="reset" style="background: orange; color: white; padding: 5px 10px;">Reset</button>
            </div>
        </form>
    </div>
</body>
</html>

```

### Question 2: React Counter

**App.js**

```jsx
import React, { useState } from 'react';

function App() {
  const [count, setCount] = useState(0);

  return (
    <div style={{textAlign: "center", marginTop: "50px"}}>
      <h1>Counter: {count}</h1>
      <button onClick={() => setCount(count + 1)}>Increment</button>
      <button onClick={() => setCount(count - 1)}>Decrement</button>
      <button onClick={() => setCount(0)}>Reset</button>
    </div>
  );
}
export default App;

```

---

## Set-4

### Question 1: Personal Portfolio

**Requirement:** Use separate HTML, CSS, and JS files.

**index.html**

```html
<!DOCTYPE html>
<html>
<head>
    <link rel="stylesheet" href="port_style.css">
</head>
<body>
    <div class="bio">
        <h1>John Doe</h1>
        <p>Web Developer.</p>
        <button onclick="showAlert()">Contact</button>
    </div>
    <div class="photo-box">
        <img src="photo.jpg" alt="Me" width="100">
    </div>
    <script src="port_script.js"></script>
</body>
</html>

```

**port_style.css**

```css
body { font-family: Arial; padding: 20px; }
.bio { width: 60%; }
.photo-box { position: absolute; top: 20px; right: 50px; border: 5px solid #333; }

```

**port_script.js**

```javascript
function showAlert() {
    alert("Hello from my Portfolio!");
}

```

### Question 2: Hospital Database

```javascript
// Open 'mongosh'
use hospitalDB

// a) Insert 6 patients
db.patients.insertOne({Id: 1, Name: "Amit", Age: 30, mobile: "99999", category: "OP"})
db.patients.insertOne({Id: 2, Name: "Sumit", Age: 45, mobile: "88888", category: "IP"})
db.patients.insertOne({Id: 3, Name: "Ravi", Age: 72, mobile: "77777", category: "OP"})
db.patients.insertOne({Id: 4, Name: "Kiran", Age: 25, mobile: "66666", category: "IP"})
db.patients.insertOne({Id: 5, Name: "Lata", Age: 75, mobile: "55555", category: "ICU"})
db.patients.insertOne({Id: 6, Name: "Mona", Age: 50, mobile: "44444", category: "OP"})

// b) Insert 2 patients
db.patients.insertMany([
    {Id: 7, Name: "Nikhil", Age: 80, mobile: "33333", category: "IP"},
    {Id: 8, Name: "Priya", Age: 20, mobile: "22222", category: "OP"}
])

// c) Update status
db.patients.updateMany({ Id: { $in: [1, 2, 4] } }, { $set: { category: "Discharged" } })

// d) Delete patients > 70
db.patients.deleteMany({ Age: { $gt: 70 } })

```
