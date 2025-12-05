# Web Technologies Lab Solutions

## Part 1: First Iteration

### Set-1

**1. Create a HTML webpage to display an application form for Adhaar registration.**

```html
<!DOCTYPE html>
<html>
<head>
    <title>Aadhaar Registration</title>
</head>
<body>
    <h2>Aadhaar Registration Form</h2>
    <form>
        <label>First Name:</label> <input type="text" name="fname"><br><br>
        <label>Last Name:</label> <input type="text" name="lname"><br><br>
        
        <label>Gender:</label>
        <input type="radio" name="gender" value="Male"> Male
        <input type="radio" name="gender" value="Female"> Female<br><br>
        
        <label>Mobile Number:</label> <input type="tel" name="mobile"><br><br>
        
        <label>Education:</label>
        <select name="education">
            <option value="10th">10th Pass</option>
            <option value="12th">12th Pass</option>
            <option value="Graduate">Graduate</option>
        </select><br><br>
        
        <label>Address:</label> <textarea name="address"></textarea><br><br>
        
        <label>Marital Status:</label>
        <input type="radio" name="status" value="Single"> Single
        <input type="radio" name="status" value="Married"> Married<br><br>
        
        <label>Spouse Name:</label> <input type="text" name="spouse"><br><br>
        <label>Children:</label> <input type="number" name="children"><br><br>
        
        <input type="submit" value="Submit">
        <input type="reset" value="Reset">
    </form>
</body>
</html>
```

\
**2. Write a JavaScript program to swap two numbers without using a third variable.**

Mathematical Logic:
$$a = a + b$$
$$b = a - b$$
$$a = a - b$$

```html
<!DOCTYPE html>
<html>
<body>
    <h3>Swap Two Numbers (No 3rd Variable)</h3>
    <p id="output"></p>
    
    <script>
        let a = 10;
        let b = 20;
        let initial = "Before Swap: a = " + a + ", b = " + b;
        
        // Swapping logic
        a = a + b;  // a becomes 30
        b = a - b;  // b becomes 10
        a = a - b;  // a becomes 20
        
        let final = "After Swap: a = " + a + ", b = " + b;
        document.getElementById("output").innerHTML = initial + "<br>" + final;
    </script>
</body>
</html>
```

---

### Set-2

**3. Create a HTML webpage to display an application form to apply for a MNC job.**

```html
<!DOCTYPE html>
<html>
<head>
    <title>MNC Job Application</title>
</head>
<body>
    <h2>MNC Job Application Form</h2>
    <form>
        <label>First Name:</label> <input type="text" name="fname"><br><br>
        <label>Last Name:</label> <input type="text" name="lname"><br><br>
        <label>Gender:</label> <input type="radio" name="gender" value="M"> Male <input type="radio" name="gender" value="F"> Female<br><br>
        <label>Mobile:</label> <input type="tel" name="mobile"><br><br>
        
        <label>Education Details:</label><br>
        <input type="checkbox" name="edu" value="10th"> 10th
        <input type="checkbox" name="edu" value="Inter"> Inter
        <input type="checkbox" name="edu" value="BTech"> B.Tech
        <input type="checkbox" name="edu" value="MTech"> M.Tech<br><br>
        
        <label>Languages Known:</label> <input type="text" name="languages"><br><br>
        <label>Passport Number:</label> <input type="text" name="passport"><br><br>
        <label>Job Experience (Years):</label> <input type="number" name="exp"><br><br>
        <label>Address:</label> <textarea name="addr"></textarea><br><br>
        
        <label>Marital Status:</label> <input type="text" name="marital"><br><br>
        <label>Spouse Name:</label> <input type="text" name="spouse"><br><br>
        <label>Children:</label> <input type="number" name="children"><br><br>
        
        <input type="submit" value="Apply">
    </form>
</body>
</html>
```

\
**4. Write a Java Script program to find whether a number is even or odd.**

```html
<!DOCTYPE html>
<html>
<body>
    <h3>Even or Odd Checker</h3>
    <input type="number" id="numInput" placeholder="Enter a number">
    <button onclick="checkEvenOdd()">Check</button>
    <p id="result"></p>

    <script>
        function checkEvenOdd() {
            // Get value from input
            var num = document.getElementById("numInput").value;
            
            // Logic check
            if (num % 2 === 0) {
                document.getElementById("result").innerText = num + " is Even.";
            } else {
                document.getElementById("result").innerText = num + " is Odd.";
            }
        }
    </script>
</body>
</html>
```

---

### Set-3

**5. Create a login page with attractive design static website using HTML and CSS.**

```html
<!DOCTYPE html>
<html>
<head>
    <style>
        /* CSS Styling */
        body { 
            font-family: Arial, sans-serif; 
            background-color: #f0f2f5; 
            display: flex; 
            justify-content: center; 
            align-items: center; 
            height: 100vh; 
        }
        .login-container { 
            background-color: white; 
            padding: 30px; 
            border-radius: 8px; 
            box-shadow: 0 4px 8px rgba(0,0,0,0.1); 
            width: 300px; 
        }
        input[type=text], input[type=password] { 
            width: 100%; 
            padding: 12px 20px; 
            margin: 8px 0; 
            display: inline-block; 
            border: 1px solid #ccc; 
            box-sizing: border-box; 
        }
        button { 
            background-color: #4CAF50; 
            color: white; 
            padding: 14px 20px; 
            margin: 8px 0; 
            border: none; 
            width: 100%; 
            cursor: pointer; 
        }
        button:hover { opacity: 0.8; }
    </style>
</head>
<body>
    <div class="login-container">
        <h2 style="text-align:center">Login</h2>
        <form>
            <label>Username</label>
            <input type="text" placeholder="Enter Username" required>
            
            <label>Password</label>
            <input type="password" placeholder="Enter Password" required>
            
            <button type="submit">Login</button>
        </form>
    </div>
</body>
</html>
```

\
**6. Develop a dynamic website using JavaScript Event Handling.**

```html
<!DOCTYPE html>
<html>
<head>
    <style>
        body { transition: background-color 0.5s; text-align: center; padding-top: 50px; }
        #msg { font-size: 24px; font-weight: bold; }
    </style>
</head>
<body id="bodyParams">
    <h2 id="msg">Click the button to change theme!</h2>
    <button onclick="changeTheme()">Toggle Dark Mode</button>

    <script>
        function changeTheme() {
            var body = document.getElementById("bodyParams");
            var text = document.getElementById("msg");
            
            // Toggle Logic
            if (body.style.backgroundColor === "black") {
                body.style.backgroundColor = "white";
                body.style.color = "black";
                text.innerText = "Light Mode Active";
            } else {
                body.style.backgroundColor = "black";
                body.style.color = "white";
                text.innerText = "Dark Mode Active";
            }
        }
    </script>
</body>
</html>
```

---

### Set-4

**7. Create a static website for a school using HTML and CSS.**

```html
<!DOCTYPE html>
<html>
<head>
    <style>
        body { font-family: sans-serif; margin: 0; }
        header { background: #003366; color: white; padding: 20px; text-align: center; }
        nav { background: #ddd; padding: 10px; text-align: center; }
        nav a { margin: 0 15px; text-decoration: none; color: #333; }
        .container { padding: 20px; }
        footer { background: #333; color: white; text-align: center; padding: 10px; position: fixed; bottom: 0; width: 100%; }
    </style>
</head>
<body>
    <header>
        <h1>Green Valley High School</h1>
    </header>
    
    <nav>
        <a href="#">Home</a>
        <a href="#">Admissions</a>
        <a href="#">Academics</a>
        <a href="#">Contact</a>
    </nav>
    
    <div class="container">
        <h2>Welcome to our School</h2>
        <p>We provide world-class education with a focus on holistic development.</p>
        <h3>Upcoming Events</h3>
        <ul>
            <li>Science Fair - Dec 10</li>
            <li>Annual Sports Day - Dec 20</li>
        </ul>
    </div>

    <footer>
        <p>&copy; 2025 Green Valley High School</p>
    </footer>
</body>
</html>
```

\
**8. Write a react application to create two components and render them in single file to display output. Each component should have different CSS properties and separate CSS file should be included.**

**Comp1.css**
```css
.box-one { background-color: lightblue; padding: 20px; border: 2px solid blue; }
```

**Comp2.css**
```css
.box-two { background-color: lightcoral; padding: 20px; border: 2px dashed red; }
```

**App.js**
```jsx
import React from 'react';
import './Comp1.css';
import './Comp2.css';

// Component 1
function ComponentOne() {
  return <div className="box-one"><h1>I am Component One</h1></div>;
}

// Component 2
function ComponentTwo() {
  return <div className="box-two"><h1>I am Component Two</h1></div>;
}

// Main App Component
function App() {
  return (
    <div>
      <ComponentOne />
      <hr />
      <ComponentTwo />
    </div>
  );
}

export default App;
```

---

## Part 2: Second Iteration

### Set-1 (Revisited)

**1. Create a HTML webpage to create time table.**

```html
<!DOCTYPE html>
<html>
<head>
    <style>
        table { border-collapse: collapse; width: 80%; margin: auto; }
        th, td { border: 1px solid black; padding: 10px; text-align: center; }
        th { background-color: #f2f2f2; }
    </style>
</head>
<body>
    <h2 style="text-align:center">Class Time Table</h2>
    <table>
        <tr>
            <th>Day</th>
            <th>9.30-10.20</th>
            <th>10.20-11.10</th>
            <th>11.10-12.00</th>
            <th>12.00-12.50</th>
            <th>12.50-1.40</th>
            <th>1.40-2.30</th>
            <th>2.30-3.20</th>
        </tr>
        <tr>
            <th>Mon</th>
            <td>DS</td>
            <td>IS</td>
            <td>IRS</td>
            <td>MAD</td>
            <td rowspan="6">LUNCH</td> <td colspan="2">WT Lab</td> </tr>
        <tr>
            <th>Tue</th>
            <td colspan="2">Project work</td>
            <td>MAD</td>
            <td>IRS</td>
            <td colspan="2">Games</td>
        </tr>
        <tr>
            <th>Wed</th>
            <td colspan="2">WT lab</td>
            <td>IS</td>
            <td>DS</td>
            <td colspan="2">Library</td>
        </tr>
        <tr>
            <th>Thurs</th>
            <td colspan="2">DS LAB</td>
            <td>MAD</td>
            <td>IS</td>
            <td colspan="2">Sports</td>
        </tr>
        <tr>
            <th>Fri</th>
            <td>MAD</td>
            <td>IS</td>
            <td>IRS</td>
            <td>DS</td>
            <td colspan="2">DS lab</td>
        </tr>
        <tr>
            <th>Sat</th>
            <td colspan="2">Project work</td>
            <td colspan="2">Games</td>
            <td colspan="2">Club Activity</td>
        </tr>
    </table>
</body>
</html>
```

\
**2. Write a JavaScript function to find the factorial of a given number.**

```html
<!DOCTYPE html>
<html>
<body>
    <h3>Factorial Calculator</h3>
    <input type="number" id="num" placeholder="Enter number">
    <button onclick="showFactorial()">Calculate</button>
    <p id="res"></p>

    <script>
        function showFactorial() {
            let n = parseInt(document.getElementById("num").value);
            let result = 1;
            
            if (n < 0) {
                result = "Invalid input";
            } else if (n === 0 || n === 1) {
                result = 1;
            } else {
                for(let i = 2; i <= n; i++) {
                    result = result * i;
                }
            }
            document.getElementById("res").innerText = "Factorial: " + result;
        }
    </script>
</body>
</html>
```

---

### Set-2 (Revisited)

**3. Create student Registration form apply various CSS attributes and style.**

```html
<!DOCTYPE html>
<html>
<head>
    <style>
        .reg-form {
            background-color: #e3f2fd;
            width: 350px;
            padding: 20px;
            border: 2px solid #2196F3;
            border-radius: 10px;
            margin: auto;
            font-family: verdana;
        }
        .reg-form h2 { text-align: center; color: #0d47a1; text-decoration: underline; }
        .reg-form input[type=text] { width: 90%; padding: 8px; margin: 5px 0; border: 1px solid #ccc; border-radius: 4px; }
        .reg-form input[type=submit] { background-color: #4CAF50; color: white; padding: 10px 15px; border: none; border-radius: 4px; cursor: pointer; width: 100%; }
        .reg-form input[type=submit]:hover { background-color: #45a049; }
    </style>
</head>
<body>
    <div class="reg-form">
        <h2>Student Registration</h2>
        <form>
            <label>Name:</label><br>
            <input type="text" name="name"><br>
            
            <label>Roll Number:</label><br>
            <input type="text" name="roll"><br>
            
            <label>Branch:</label><br>
            <input type="text" name="branch"><br><br>
            
            <input type="submit" value="Register">
        </form>
    </div>
</body>
</html>
```

\
**4. Write a react application to create two components and render them in single file...**

*(Same as Part 1, Set-4, Q8)*

```jsx
import React from 'react';

// Inline styles for simplicity in this example
const styleOne = { backgroundColor: 'yellow', padding: '10px', margin: '10px' };
const styleTwo = { backgroundColor: 'cyan', padding: '10px', margin: '10px' };

function CompOne() {
    return <div style={styleOne}><h2>Component A</h2></div>;
}

function CompTwo() {
    return <div style={styleTwo}><h2>Component B</h2></div>;
}

function App() {
    return (
        <div>
            <CompOne />
            <CompTwo />
        </div>
    );
}
export default App;
```

---

### Set-3 (Revisited)

**5. Create a HTML webpage to display an application form for Adhaar registration.**

*(Refer to Part 1, Set-1, Question 1 for the code)*

\
**6. Write a react application which implements number counter. (It should contain three buttons ‘increment’, ‘decrement’ and ‘reset’ to operate counter.)**

```jsx
import React, { useState } from 'react';

function CounterApp() {
  const [count, setCount] = useState(0);

  return (
    <div style={{ textAlign: 'center', marginTop: '50px' }}>
      <h1>Counter: {count}</h1>
      <button onClick={() => setCount(count + 1)} style={{ marginRight: '10px' }}>Increment</button>
      <button onClick={() => setCount(count - 1)} style={{ marginRight: '10px' }}>Decrement</button>
      <button onClick={() => setCount(0)}>Reset</button>
    </div>
  );
}

export default CounterApp;
```

---

### Set-4 (Revisited)

**7. Develop a student registration form with validation support using java script.**

```html
<!DOCTYPE html>
<html>
<head>
    <title>Form Validation</title>
</head>
<body>
    <h2>Registration with Validation</h2>
    <form onsubmit="return validateForm()">
        Name: <input type="text" id="sname"><br><br>
        Email: <input type="text" id="email"><br><br>
        <input type="submit" value="Register">
    </form>

    <script>
        function validateForm() {
            let name = document.getElementById("sname").value;
            let email = document.getElementById("email").value;
            
            // Check if empty
            if (name == "" || email == "") {
                alert("All fields must be filled out");
                return false;
            }
            
            // Simple Email Regex check
            let emailPattern = /^[a-zA-Z0-9._-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,4}$/;
            if (!email.match(emailPattern)) {
                alert("Please enter a valid email address");
                return false;
            }
            
            alert("Registration Successful!");
            return true;
        }
    </script>
</body>
</html>
```

\
**8. How do you remove duplicates from an array in JavaScript**

**Method 1: Using Set (Recommended)**
```javascript
let numbers = [1, 2, 2, 3, 4, 4, 5];
// Set automatically removes duplicates, spread operator converts back to array
let uniqueNumbers = [...new Set(numbers)];

console.log(uniqueNumbers); // Output: [1, 2, 3, 4, 5]
```

**Method 2: Using Filter**
```javascript
let numbers = [1, 2, 2, 3, 4, 4, 5];
let uniqueNumbers = numbers.filter((item, index) => {
    // Returns true only if the current index is the first occurrence of the item
    return numbers.indexOf(item) === index;
});

console.log(uniqueNumbers); // Output: [1, 2, 3, 4, 5]
```