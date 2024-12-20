# Step-by-Step Guide: Building a Random Advice Web Application

If you're new to programming, don't worry!  

You can use this guide to do the task.

Check out the [demo here](https://neon-duckanoo-7458d7.netlify.app/).  

By the end of this guide, you’ll have your app up and running on your computer.

---

## **Step 1: Understand the Basic Idea**

This app will:
- Fetch random advice from a free API: [Advice Slip API](https://api.adviceslip.com/).
- Display the advice on the screen.
- Automatically refresh the advice every 20 seconds.
- Allow users to manually refresh the advice by clicking a button.

We'll use three separate files for clean organization:
- **HTML**: The app's structure (its "skeleton").
- **CSS**: The styles that make it look nice ("its clothes").
- **JavaScript**: Adds interactivity and functionality ("its brain").

---

## **Step 2: Set Up Your Project**

1. **Create a Folder**  
   Make a folder on your computer and name it `random-advice-app`. This will keep your files organized.

2. **Create the Required Files**  
   Inside the folder, create three files:
   - `index.html`
   - `style.css`
   - `script.js`

3. **You might need a text editor like [Notepad++](https://notepad-plus-plus.org/), [VSCode](https://code.visualstudio.com/), [Sublime Text](https://www.sublimetext.com/) or any other editor of your choice to open and edit the Files**  

---

## **Step 3: Write the HTML (Structure)**

Copy and paste the following code into `index.html`:

```html
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Random Advice</title>
  <link rel="stylesheet" href="style.css">
</head>

<body>
  <div class="container">
    <h2>Random Advice Every 20 Seconds</h2>
    <p id="advice" class="advice">Loading...</p>
    <button id="new-advice" class="btn">Get New Advice</button>
  </div>
  <script src="script.js"></script>
</body>

</html>
```

### **What This Code Does**
- Displays a heading (`<h2>`) for the app title.
- Includes a placeholder (`<p id="advice">`) to display the advice text.
- Adds a button for manually fetching advice.
- Links the CSS for styling and JavaScript for functionality.

---

## **Step 4: Write the CSS (Styling)**

Copy and paste the following code into `style.css`:

```css
body {
  font-family: Arial, sans-serif;
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
  background-color: #f7f7f7;
  margin: 0;
}

.container {
  text-align: center;
  background-color: #fff;
  padding: 30px;
  border-radius: 8px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
  width: 400px;
}

.advice {
  font-size: 18px;
  color: #333;
  margin-bottom: 20px;
  font-style: italic;
}

.btn {
  background-color: #007BFF;
  color: #fff;
  border: none;
  padding: 10px 20px;
  font-size: 16px;
  border-radius: 5px;
  cursor: pointer;
}

.btn:hover {
  background-color: #0056b3;
}
```

### **What This Code Does**
- Centers the content in the middle of the screen.
- Styles the text, button, and container for a clean and modern look.

---

## **Step 5: Write the JavaScript (Functionality)**

Copy and paste the following code into `script.js`:

```javascript
// Function to fetch advice from the API
const fetchAdvice = async () => {
  try {
    const response = await fetch('https://api.adviceslip.com/advice');
    const data = await response.json();
    const adviceText = data.slip.advice;
    document.getElementById('advice').textContent = adviceText;
  } catch (error) {
    console.error('Error fetching advice:', error);
    document.getElementById('advice').textContent = "Couldn't fetch advice. Please try again!";
  }
};

// Initial advice fetch when the page loads
fetchAdvice();

// Fetch new advice every 20 seconds (20,000 milliseconds)
setInterval(fetchAdvice, 20000);

// Button to fetch new advice on click
document.getElementById('new-advice').addEventListener('click', fetchAdvice);
```

### **What the JavaScript Code Does**

1. **Fetches Random Advice from the API:**

   ```javascript
   const fetchAdvice = async () => {
     try {
       const response = await fetch('https://api.adviceslip.com/advice');
       const data = await response.json();
       const adviceText = data.slip.advice;
       document.getElementById('advice').textContent = adviceText;
     } catch (error) {
       console.error('Error fetching advice:', error);
       document.getElementById('advice').textContent = "Couldn't fetch advice. Please try again!";
     }
   };
   ```

   - **`const fetchAdvice = async () => { ... }`**: This is an **asynchronous** function (hence `async`). It allows us to request the API and wait for a response without blocking the rest of the application. The code inside the function will be executed when called.
   
   - **`const response = await fetch('https://api.adviceslip.com/advice');`**: 
     - This line uses the **`fetch()`** function to send a request to the **Adviceslip API** (`https://api.adviceslip.com/advice`).
     - **`await`** ensures that the program waits for the response before continuing to the following line. This ensures we don't move forward until we have the needed data.
   
   - **`const data = await response.json();`**: 
     - Once we get the response from the API, it's in JSON format. The `.json()` method converts the response into a JavaScript object we can work with.
   
   - **`const adviceText = data.slip.advice;`**: 
     - The API returns the data in the form of a nested object. The advice is inside `data.slip.advice`. This line extracts the advice text from the data and stores it in the variable `adviceText`.
   
   - **`document.getElementById('advice').textContent = adviceText;`**: 
     - Now, we have the advice text stored in the `adviceText` variable. This line updates the content of the HTML element with the ID `advice` (the `<p>` tag in your HTML) to display the new advice.

   - **`catch (error) { ... }`**: 
     - This part of the code handles errors that might occur during the fetch operation (e.g. if the API is unavailable or there’s an issue with the request).
     - If there’s an error, it logs it to the console and updates the advice text with a user-friendly message like "Couldn't fetch advice. Please try again!".

---

2. **Automatically Updates the Advice Every 20 Seconds:**

   ```javascript
   setInterval(fetchAdvice, 20000);
   ```

   - **`setInterval()`**: This function repeatedly calls a specified function at fixed intervals (milliseconds). In this case, we call the `fetchAdvice` function every **20,000 milliseconds**, which equals **20 seconds**.
   
   - **Why 20 seconds?**: This means that every 20 seconds, the advice will automatically be refreshed with a new random piece of advice from the API. So, you don’t need to refresh the page manually.

   - **How it works**: After the first call to `fetchAdvice,` every 20 seconds, the browser automatically calls the function again and updates the displayed advice without requiring the user to do anything.

---

3. **Manually Fetches Advice When Button Is Clicked:**

   ```javascript
   document.getElementById('new-advice').addEventListener('click', fetchAdvice);
   ```

   - **`document.getElementById('new-advice')`**: This targets the HTML element with the ID `new-advice`, which is the **button** in your HTML.
   
   - **`addEventListener('click', fetchAdvice)`**: This attaches an event listener to the button so that when it’s clicked, the **`fetchAdvice`** function is called.
   
   - **What happens**: When the user clicks the "Get New Advice" button, the application immediately fetches new advice and updates the displayed advice on the page.

---

### **What This Achieves:**
- **Dynamic Advice**: The app continuously updates with fresh advice from the API without requiring the user to refresh the page.
- **User Interactivity**: Users can also manually click the "Get New Advice" button to fetch a new piece of advice.
- **Error Handling**: If there’s an issue fetching the advice (like no internet connection), the app gracefully handles it and displays an error message.


## **Step 6: Run Your App**

1. **Open the `index.html` File**  
   Double-click the `index.html` file to open it in a browser.  

2. **Test Your App**  
   - Wait 20 seconds to see the advice update automatically.  
   - Click the "Get New Advice" button to fetch advice manually.

---

### 🎉 **Congratulations!**
You’ve built a Web Application that can consume a RESTful API. Share it with friends, or use this as a stepping stone to explore more APIs and projects.

