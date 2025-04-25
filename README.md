# react-hooks-


#Here is the list of React Hooks that you will learn in this react hooks course:

 useState Hook
 useEffect Hook
 useRef Hook
 useMemo Hook
 useCallback Hook
 useContext Hook
 useReducer Hook
 useLayoutEffect Hook
 Custom React Hook



 Sure, Nihal! Let’s break down the `useState` hook in React with a **real-life example**, explain **all conditions** (like how it behaves on update, re-renders, multiple states, etc.), and solve it step-by-step.

---

### 🔄 What is `useState`?

`useState` is a **React Hook** that lets you add **state** to functional components.  
Think of it as a way to make your component "remember" values over time.

---

### 🛍 Real-life Example: Shopping Cart Button

Imagine you're building a simple **shopping cart** feature on an e-commerce website.  
You have a button that says:

> 🛒 Add to Cart

When the user clicks it, it should change to:

> ✅ Added!

And maybe allow toggling it again to remove from cart.

---

### ✅ Solution using `useState`

```jsx
import React, { useState } from "react";

function AddToCartButton() {
  const [isAdded, setIsAdded] = useState(false); // Initial value is false

  const handleClick = () => {
    setIsAdded(!isAdded); // Toggle value
  };

  return (
    <button onClick={handleClick}>
      {isAdded ? "✅ Added!" : "🛒 Add to Cart"}
    </button>
  );
}
```

---

### 🔍 Explanation (Step-by-step):

| Concept | Real-life Analogy | Code Explanation |
|--------|--------------------|------------------|
| `useState(false)` | The item is *not* in the cart initially | You’re telling React to remember a value: `false` |
| `isAdded` | Is the item added or not? | React gives us this value to use inside the component |
| `setIsAdded` | How to change the cart state | It's a function to update the value |
| `setIsAdded(!isAdded)` | Toggle the value | It changes `true` to `false` and vice versa |
| Button text | What user sees | Conditionally shows "Add to Cart" or "Added" |

---

### ⚠️ All Conditions to Know About `useState`:

#### 1. **Initial value is set only once**
```js
const [count, setCount] = useState(0); // 0 is set only once
```

#### 2. **Component re-renders on update**
Every time you call `setCount`, the component re-renders.

#### 3. **Asynchronous update (not immediate)**
```js
setCount(count + 1);
console.log(count); // Still old value here
```

If you want the **latest** value:
```js
setCount(prev => prev + 1);
```

#### 4. **Multiple `useState` hooks**
You can use many states:
```js
const [likes, setLikes] = useState(0);
const [isLoggedIn, setIsLoggedIn] = useState(false);
```

#### 5. **State can be any data type**
```js
useState(0)          // number
useState("")         // string
useState([])         // array
useState({})         // object
```

#### 6. **Avoid directly modifying state**
❌ Wrong:
```js
cartItems.push("new item"); // don’t mutate state directly
```

✅ Right:
```js
setCartItems(prev => [...prev, "new item"]);
```

---

### 🧠 Tip for Interviews:
If someone asks you **"What is useState?"**, you can say:

> "`useState` is a React Hook that lets functional components maintain and update local state. It returns a stateful value and a function to update it, and causes the component to re-render when the state changes."




Absolutely, Nihal! Here are **3 real-life examples** of the `useState` hook — all small, simple, and ready to be tested in your **VS Code** or any React environment like CodeSandbox.

---

## ✅ Example 1: **Counter App (Click to Increase Count)**

📍 **Real-life Use Case**: Like tracking steps in a fitness app.

```jsx
import React, { useState } from "react";

function Counter() {
  const [count, setCount] = useState(0); // Initial count is 0

  return (
    <div>
      <h2>Step Counter: {count}</h2>
      <button onClick={() => setCount(count + 1)}>Increase</button>
    </div>
  );
}

export default Counter;
```

---

## ✅ Example 2: **Dark Mode Toggle**

📍 **Real-life Use Case**: Websites with light/dark mode toggle.

```jsx
import React, { useState } from "react";

function DarkModeToggle() {
  const [isDark, setIsDark] = useState(false);

  const toggleMode = () => {
    setIsDark(!isDark);
  };

  const style = {
    backgroundColor: isDark ? "#222" : "#fff",
    color: isDark ? "#fff" : "#000",
    padding: "20px",
    textAlign: "center",
  };

  return (
    <div style={style}>
      <h2>{isDark ? "Dark Mode" : "Light Mode"}</h2>
      <button onClick={toggleMode}>Toggle Mode</button>
    </div>
  );
}

export default DarkModeToggle;
```

---

## ✅ Example 3: **Login/Logout Button**

📍 **Real-life Use Case**: Like logging into a website.

```jsx
import React, { useState } from "react";

function LoginControl() {
  const [isLoggedIn, setIsLoggedIn] = useState(false);

  const handleClick = () => {
    setIsLoggedIn(!isLoggedIn);
  };

  return (
    <div>
      <h2>{isLoggedIn ? "Welcome back, Nihal!" : "Please log in"}</h2>
      <button onClick={handleClick}>
        {isLoggedIn ? "Logout" : "Login"}
      </button>
    </div>
  );
}

export default LoginControl;
```

---

## 🛠 How to Run These in VS Code:

1. Open a React project (`npx create-react-app my-app`)
2. Create a new component file like `Counter.js`, `DarkModeToggle.js`, etc.
3. Import and use the component in `App.js` like this:

```jsx
import Counter from './Counter';
// or
// import DarkModeToggle from './DarkModeToggle';
// import LoginControl from './LoginControl';

function App() {
  return (
    <div>
      <Counter />
    </div>
  );
}

export default App;

```




Awesome, Nihal! Let’s break down the `useEffect` hook in a beginner-friendly way with a **real-life example**, and then I’ll give you **10 mini-projects** using `useEffect` that you can practice in your VS Code.

---

## 🔄 What is `useEffect` in React?

`useEffect` is a React Hook that lets you **perform side effects** in function components.

Think of side effects as things like:
- Fetching data from an API
- Setting up event listeners
- Updating the document title
- Timer/intervals
- Anything outside rendering UI

---

## ✅ Real-life Example: Setting Page Title

📍 **Use Case**: Update the webpage title dynamically based on user activity.

```jsx
import React, { useState, useEffect } from "react";

function PageTitleUpdater() {
  const [name, setName] = useState("Nihal");

  useEffect(() => {
    document.title = `Hello, ${name}`;
  }, [name]); // Runs every time 'name' changes

  return (
    <div>
      <input
        type="text"
        value={name}
        onChange={(e) => setName(e.target.value)}
        placeholder="Enter your name"
      />
      <p>Check your browser tab title 👀</p>
    </div>
  );
}

export default PageTitleUpdater;
```

---

### 🔍 `useEffect` Syntax:

```js
useEffect(() => {
  // side-effect code here
}, [dependencies]);
```

- 🧠 Runs after every render **by default**
- 🎯 Runs only on mount if dependency array is empty `[]`
- 🔁 Runs only when specified dependencies change
- 🧹 Can return a cleanup function (for timers, listeners, etc.)

---

## 💡 10 Mini Projects Using `useEffect`

Here’s a list of real-life mini-projects that help you master `useEffect`:




Awesome, Nihal! Here's the **complete code** for all **10 mini React projects** using the `useEffect` hook. You can copy and run each one directly in your React setup (`npx create-react-app`).

---

## 🔢 1. **Digital Clock**

```jsx
// Clock.js
import React, { useState, useEffect } from 'react';

function Clock() {
  const [time, setTime] = useState(new Date());

  useEffect(() => {
    const interval = setInterval(() => setTime(new Date()), 1000);
    return () => clearInterval(interval);
  }, []);

  return <h2>Time: {time.toLocaleTimeString()}</h2>;
}

export default Clock;
```

---

## ☁️ 2. **Weather App (Dummy)**

```jsx
// Weather.js
import React, { useEffect, useState } from 'react';

function Weather() {
  const [weather, setWeather] = useState(null);

  useEffect(() => {
    fetch("https://api.weatherapi.com/v1/current.json?key=YOUR_API_KEY&q=London")
      .then(res => res.json())
      .then(data => setWeather(data));
  }, []);

  return (
    <div>
      {weather ? (
        <h2>Temperature in {weather.location.name}: {weather.current.temp_c}°C</h2>
      ) : (
        <p>Loading...</p>
      )}
    </div>
  );
}

export default Weather;
```

> 📝 Use your own free API key from [weatherapi.com](https://www.weatherapi.com/)

---

## 🟢 3. **Typing Indicator**

```jsx
// TypingIndicator.js
import React, { useState, useEffect } from 'react';

function TypingIndicator() {
  const [text, setText] = useState('');
  const [isTyping, setIsTyping] = useState(false);

  useEffect(() => {
    if (text !== '') {
      setIsTyping(true);
      const timeout = setTimeout(() => setIsTyping(false), 1000);
      return () => clearTimeout(timeout);
    }
  }, [text]);

  return (
    <div>
      <input value={text} onChange={(e) => setText(e.target.value)} />
      {isTyping && <p>User is typing...</p>}
    </div>
  );
}

export default TypingIndicator;
```

---

## 🔝 4. **Scroll to Top Button**

```jsx
// ScrollTop.js
import React, { useEffect, useState } from 'react';

function ScrollTop() {
  const [show, setShow] = useState(false);

  useEffect(() => {
    const onScroll = () => setShow(window.scrollY > 200);
    window.addEventListener("scroll", onScroll);
    return () => window.removeEventListener("scroll", onScroll);
  }, []);

  return (
    show && <button onClick={() => window.scrollTo({ top: 0, behavior: "smooth" })}>⬆️ Top</button>
  );
}

export default ScrollTop;
```

---

## 🌐 5. **Online/Offline Status**

```jsx
// NetworkStatus.js
import React, { useState, useEffect } from 'react';

function NetworkStatus() {
  const [isOnline, setIsOnline] = useState(navigator.onLine);

  useEffect(() => {
    const goOnline = () => setIsOnline(true);
    const goOffline = () => setIsOnline(false);

    window.addEventListener('online', goOnline);
    window.addEventListener('offline', goOffline);

    return () => {
      window.removeEventListener('online', goOnline);
      window.removeEventListener('offline', goOffline);
    };
  }, []);

  return <h2>{isOnline ? '✅ You are online' : '🚫 You are offline'}</h2>;
}

export default NetworkStatus;
```

---

## 🔍 6. **Live Search Filter**

```jsx
// SearchFilter.js
import React, { useState, useEffect } from 'react';

const data = ['Apple', 'Banana', 'Orange', 'Mango', 'Grapes'];

function SearchFilter() {
  const [search, setSearch] = useState('');
  const [result, setResult] = useState(data);

  useEffect(() => {
    const delay = setTimeout(() => {
      setResult(data.filter(item => item.toLowerCase().includes(search.toLowerCase())));
    }, 300);

    return () => clearTimeout(delay);
  }, [search]);

  return (
    <div>
      <input value={search} onChange={(e) => setSearch(e.target.value)} placeholder="Search fruit..." />
      <ul>{result.map((item, i) => <li key={i}>{item}</li>)}</ul>
    </div>
  );
}

export default SearchFilter;
```

---

## ✨ 7. **Quote of the Day**

```jsx
// Quote.js
import React, { useEffect, useState } from 'react';

function Quote() {
  const [quote, setQuote] = useState("");

  const fetchQuote = () => {
    fetch("https://api.quotable.io/random")
      .then(res => res.json())
      .then(data => setQuote(data.content));
  };

  useEffect(() => {
    fetchQuote();
  }, []);

  return (
    <div>
      <p>{quote}</p>
      <button onClick={fetchQuote}>New Quote</button>
    </div>
  );
}

export default Quote;
```

---

## 🌗 8. **Theme Switcher with LocalStorage**

```jsx
// ThemeSwitcher.js
import React, { useEffect, useState } from 'react';

function ThemeSwitcher() {
  const [theme, setTheme] = useState(localStorage.getItem("theme") || "light");

  useEffect(() => {
    document.body.style.background = theme === "dark" ? "#333" : "#fff";
    localStorage.setItem("theme", theme);
  }, [theme]);

  return (
    <button onClick={() => setTheme(prev => (prev === "light" ? "dark" : "light"))}>
      Switch to {theme === "light" ? "Dark" : "Light"} Mode
    </button>
  );
}

export default ThemeSwitcher;
```

---

## ⏳ 9. **Countdown Timer**

```jsx
// Countdown.js
import React, { useEffect, useState } from 'react';

function Countdown() {
  const [count, setCount] = useState(10);

  useEffect(() => {
    if (count > 0) {
      const timer = setTimeout(() => setCount(count - 1), 1000);
      return () => clearTimeout(timer);
    }
  }, [count]);

  return <h2>Countdown: {count}</h2>;
}

export default Countdown;
```

---

## 🖱️ 10. **Mouse Position Tracker**

```jsx
// MouseTracker.js
import React, { useState, useEffect } from 'react';

function MouseTracker() {
  const [pos, setPos] = useState({ x: 0, y: 0 });

  useEffect(() => {
    const updatePos = (e) => setPos({ x: e.clientX, y: e.clientY });
    window.addEventListener("mousemove", updatePos);
    return () => window.removeEventListener("mousemove", updatePos);
  }, []);

  return <p>Mouse Position: X = {pos.x}, Y = {pos.y}</p>;
}

export default MouseTracker;
```

---

## ✅ How to Run in `App.js`

```jsx
import React from "react";
import Clock from "./Clock"; // change to any component you want to test

function App() {
  return (
    <div style={{ padding: "20px" }}>
      <Clock />
    </div>
  );
}

export default App;
```



Perfect, Nihal bhai! 🔥 Let's dive deep into the **`useRef` hook** — I’ll break it down clearly, with **10 real-life mini projects**, full **code**, and detailed **why + how** explanations for each.

---

## 🧠 What is `useRef` in React?

- `useRef` lets you reference **DOM elements** or **store mutable values** that don’t trigger re-renders.
- Think of it as a **hidden storage** inside a component.

---

## 🤔 Why do we use `useRef`?

1. To **access DOM elements** directly (like `document.getElementById`)
2. To **store data** across renders without causing re-render
3. To **track previous values**
4. To **build timers, focus inputs, animations**, and more

---

## 📦 Here's what you're getting:

I'll now give you **Project 1** in full detail, and if you like the format, I’ll continue with the rest:

---

## ✅ **Project 1: Focus Input on Button Click**

### 🎯 Goal:
Clicking the button will **automatically focus the input field** using `useRef`.

---

### 💡 Why use `useRef` here?

You want to control the DOM **without re-rendering the component** — `useRef` lets you access the input element directly.

---

### 🔍 Real-life use:
- Search bar focus
- OTP or login forms
- Accessibility improvements

---

### 💻 Code:

```jsx
// FocusInput.js
import React, { useRef } from 'react';

function FocusInput() {
  const inputRef = useRef(null); // create a reference

  const handleFocus = () => {
    inputRef.current.focus(); // focus the input
  };

  return (
    <div style={{ padding: '20px' }}>
      <input ref={inputRef} placeholder="Click button to focus me" />
      <button onClick={handleFocus}>Focus Input</button>
    </div>
  );
}

export default FocusInput;
```

---

### 🧠 What's happening:

| Line | What it does |
|------|--------------|
| `useRef(null)` | Creates a reference to be assigned to input |
| `ref={inputRef}` | Ties the reference to that input element |
| `inputRef.current.focus()` | Directly accesses the DOM to focus |

---

## ✅ Run it in `App.js`

```jsx
import React from "react";
import FocusInput from "./FocusInput";

function App() {
  return (
    <div>
      <FocusInput />
    </div>
  );
}

export default App;
```

---
Here’s a **proper README file format** that you can use for your project:

---

# **React `useRef` Projects**

This repository contains **10 mini-projects** built using the `useRef` hook in React. Each project demonstrates how to use `useRef` for different scenarios like controlling DOM elements, storing mutable values, and more.

---

## **Table of Contents**

1. [Project 1: Focus Input on Button Click](#project-1-focus-input-on-button-click)
2. [Project 2: Auto Focus on Mount](#project-2-auto-focus-on-mount)
3. [Project 3: Timer App](#project-3-timer-app)
4. [Project 4: Track Previous Value](#project-4-track-previous-value)
5. [Project 5: Stopwatch](#project-5-stopwatch)
6. [Project 6: Scroll to Element](#project-6-scroll-to-element)
7. [Project 7: Save Form Value without Re-render](#project-7-save-form-value-without-re-render)
8. [Project 8: Detect Click Outside Modal](#project-8-detect-click-outside-modal)
9. [Project 9: Countdown Timer](#project-9-countdown-timer)
10. [Project 10: Video Player Controls](#project-10-video-player-controls)

---

## **Project 1: Focus Input on Button Click**

**Description:**  
This project demonstrates how to use `useRef` to focus an input field when a button is clicked.

**Usage:**
- Create a reference using `useRef`.
- Bind the reference to an input element.
- Focus the input when a button is clicked.

**Code Example:**

```jsx
import React, { useRef } from 'react';

function FocusInput() {
  const inputRef = useRef(null);

  const handleFocus = () => {
    inputRef.current.focus();
  };

  return (
    <div>
      <input ref={inputRef} placeholder="Click button to focus" />
      <button onClick={handleFocus}>Focus Input</button>
    </div>
  );
}

export default FocusInput;
```

---

## **Project 2: Auto Focus on Mount**

**Description:**  
This project demonstrates how to automatically focus an input field when the component mounts.

**Usage:**  
- Use `useRef` to create a reference to the input field.
- Use `useEffect` to focus the input field as soon as the component mounts.

**Code Example:**

```jsx
import React, { useEffect, useRef } from 'react';

function AutoFocusInput() {
  const inputRef = useRef(null);

  useEffect(() => {
    inputRef.current.focus();
  }, []);

  return <input ref={inputRef} placeholder="Auto-focused input" />;
}

export default AutoFocusInput;
```

---

## **Project 3: Timer App**

**Description:**  
This project implements a timer that starts and stops using `useRef` to maintain the interval.

**Usage:**  
- Use `useRef` to store a reference to the interval.
- Start and stop the timer by using `setInterval` and `clearInterval`.

**Code Example:**

```jsx
import { useState } from 'react';

function TimerApp() {
  const [count, setCount] = useState(0);
  const timerRef = useRef(null);

  const startTimer = () => {
    if (!timerRef.current) {
      timerRef.current = setInterval(() => setCount((c) => c + 1), 1000);
    }
  };

  const stopTimer = () => {
    clearInterval(timerRef.current);
    timerRef.current = null;
  };

  return (
    <div>
      <h2>Timer: {count}</h2>
      <button onClick={startTimer}>Start</button>
      <button onClick={stopTimer}>Stop</button>
    </div>
  );
}

export default TimerApp;
```

---

## **Project 4: Track Previous Value**

**Description:**  
This project tracks and displays the previous state value using `useRef`.

**Usage:**  
- Use `useRef` to store the previous state value.
- Update the reference whenever the state changes.

**Code Example:**

```jsx
import { useState, useEffect, useRef } from 'react';

function PreviousValue() {
  const [count, setCount] = useState(0);
  const prevCountRef = useRef();

  useEffect(() => {
    prevCountRef.current = count;
  }, [count]);

  return (
    <div>
      <h2>Current: {count}</h2>
      <h3>Previous: {prevCountRef.current}</h3>
      <button onClick={() => setCount(count + 1)}>Increment</button>
    </div>
  );
}

export default PreviousValue;
```

---

## **Project 5: Stopwatch**

**Description:**  
This project demonstrates how to implement a stopwatch using `useRef` to manage the interval.

**Usage:**  
- Use `useRef` to store the interval.
- Control the start, stop, and reset actions.

**Code Example:**

```jsx
import { useState, useRef } from 'react';

function Stopwatch() {
  const [time, setTime] = useState(0);
  const intervalRef = useRef(null);

  const start = () => {
    if (!intervalRef.current) {
      intervalRef.current = setInterval(() => setTime((t) => t + 1), 1000);
    }
  };

  const stop = () => {
    clearInterval(intervalRef.current);
    intervalRef.current = null;
  };

  const reset = () => {
    stop();
    setTime(0);
  };

  return (
    <div>
      <h2>Stopwatch: {time}</h2>
      <button onClick={start}>Start</button>
      <button onClick={stop}>Stop</button>
      <button onClick={reset}>Reset</button>
    </div>
  );
}

export default Stopwatch;
```

---

## **Project 6: Scroll to Element**

**Description:**  
This project demonstrates how to scroll smoothly to a target element using `useRef`.

**Usage:**  
- Use `useRef` to create a reference to the target element.
- Trigger `scrollIntoView` on a button click to scroll to the target.

**Code Example:**

```jsx
import React, { useRef } from 'react';

function ScrollToSection() {
  const sectionRef = useRef(null);

  const scrollToSection = () => {
    sectionRef.current.scrollIntoView({ behavior: 'smooth' });
  };

  return (
    <div>
      <button onClick={scrollToSection}>Go to Section</button>
      <div style={{ height: '1000px' }} />
      <div ref={sectionRef} style={{ background: 'lightblue', height: '100px' }}>
        Scroll Target
      </div>
    </div>
  );
}

export default ScrollToSection;
```

---

## **Project 7: Save Form Value without Re-render**

**Description:**  
This project uses `useRef` to store a form value without causing a re-render.

**Usage:**  
- Use `useRef` to store form values.
- Prevent re-rendering by not storing them in state.

**Code Example:**

```jsx
import React, { useRef } from 'react';

function SaveFormRef() {
  const nameRef = useRef();

  const handleSubmit = () => {
    alert('Name: ' + nameRef.current.value);
  };

  return (
    <div>
      <input ref={nameRef} placeholder="Enter name" />
      <button onClick={handleSubmit}>Submit</button>
    </div>
  );
}

export default SaveFormRef;
```

---

## **Project 8: Detect Click Outside Modal**

**Description:**  
Detect clicks outside a modal using `useRef`.

**Usage:**  
- Use `useRef` to reference the modal.
- Add an event listener to detect clicks outside the modal.

**Code Example:**

```jsx
import { useEffect, useRef } from 'react';

function OutsideClickDetector() {
  const modalRef = useRef();

  useEffect(() => {
    const handleClickOutside = (e) => {
      if (modalRef.current && !modalRef.current.contains(e.target)) {
        alert('Clicked outside modal');
      }
    };
    document.addEventListener('mousedown', handleClickOutside);
    return () => document.removeEventListener('mousedown', handleClickOutside);
  }, []);

  return (
    <div ref={modalRef} style={{ padding: 20, background: '#eee' }}>
      <h2>Modal</h2>
    </div>
  );
}

export default OutsideClickDetector;
```

---

## **Project 9: Countdown Timer**

**Description:**  
Implement a countdown timer using `useRef`.

**Usage:**  
- Use `useRef` to store the timer reference.
- Start the countdown and stop when it reaches 0.

**Code Example:**

```jsx
import React, { useState, useRef } from 'react';

function CountdownTimer() {
  const [timeLeft, setTimeLeft] = useState(10);
  const timerRef = useRef(null);

  const startCountdown = () => {
    if (!timerRef.current) {
      timerRef.current = setInterval(() => {
        setTimeLeft((prev) => {
          if (prev <= 1) {
            clearInterval(timerRef.current);
            timerRef.current = null;
            return 0;
          }
          return prev - 1;
        });
      }, 1000);
    }
  };

  return (
    <div>
      <h2>Countdown: {timeLeft}</h2>
      <button onClick={startCountdown}>Start Countdown</button>
    </div>
  );
}

export default CountdownTimer;
```

---

## **Project 

10: Video Player Controls**

**Description:**  
This project demonstrates controlling a video player using `useRef`.

**Usage:**  
- Use `useRef` to control the video element.
- Play/pause the video on button click.

**Code Example:**

```jsx
import React, { useRef } from 'react';

function VideoPlayer() {
  const videoRef = useRef();

  const playPauseVideo = () => {
    if (videoRef.current.paused) {
      videoRef.current.play();
    } else {
      videoRef.current.pause();
    }
  };

  return (
    <div>
      <video ref={videoRef} width="400" controls>
        <source src="video.mp4" type="video/mp4" />
      </video>
      <button onClick={playPauseVideo}>Play/Pause</button>
    </div>
  );
}

export default VideoPlayer;
```

---

Great! Let's dive into the `useMemo` hook first with a real-life explanation, and then I’ll provide you **10 practice projects with full code and explanations**.

---

## 🧠 What is `useMemo`?

### ✅ **Definition**:
`useMemo` is a React Hook that lets you **optimize performance** by **memoizing the result of a calculation**. This means it **remembers the output** of a function as long as its dependencies don’t change.

---

### 🛒 **Real-Life Example**:

Imagine you run a **grocery shop**. Every time a new customer comes in, you calculate the **total bill**. But if the items and their prices haven't changed, why calculate it again?

This is where `useMemo` helps — it remembers the total bill **until the items or prices change**.

---

## 📌 Syntax:

```jsx
const memoizedValue = useMemo(() => computeSomething(a, b), [a, b]);
```

---

## 🚀 10 Mini Projects Using `useMemo` (with Code + Explanation)

---

### 1. **Expensive Calculation Optimization**

#### 🔹 Purpose:
Avoid recalculating a slow function unless necessary.

#### ✅ Code:
```jsx
import React, { useState, useMemo } from 'react';

function ExpensiveCalc() {
  const [count, setCount] = useState(0);
  const [input, setInput] = useState('');

  const slowFunction = (num) => {
    console.log('Calculating...');
    for (let i = 0; i < 1e9; i++) {} // simulate heavy work
    return num * 2;
  };

  const doubleCount = useMemo(() => slowFunction(count), [count]);

  return (
    <div>
      <h2>Double Count: {doubleCount}</h2>
      <button onClick={() => setCount(count + 1)}>Increase Count</button>
      <input value={input} onChange={(e) => setInput(e.target.value)} placeholder="Type something" />
    </div>
  );
}

export default ExpensiveCalc;
```

🧠 **Why `useMemo`?**  
Typing in the input shouldn’t trigger the slow calculation. Thanks to `useMemo`, it only runs when `count` changes.

---

Awesome! Let’s get started. Below are **10 mini projects using `useMemo`** with full **code and explanation**, perfect for practicing in your VS Code.

---

### 🚀 1. **Expensive Calculation Optimization**

#### ✅ Purpose:
Avoid re-running a slow function on every render.

```jsx
import React, { useState, useMemo } from 'react';

function ExpensiveCalc() {
  const [count, setCount] = useState(0);
  const [input, setInput] = useState('');

  const slowFunction = (num) => {
    console.log('Calculating...');
    for (let i = 0; i < 1e9; i++) {} // simulate heavy work
    return num * 2;
  };

  const doubleCount = useMemo(() => slowFunction(count), [count]);

  return (
    <div>
      <h2>Double Count: {doubleCount}</h2>
      <button onClick={() => setCount(count + 1)}>Increase Count</button>
      <input value={input} onChange={(e) => setInput(e.target.value)} placeholder="Type here..." />
    </div>
  );
}
export default ExpensiveCalc;
```

🧠 **Why `useMemo`?**  
Typing in the input won't trigger recalculation. `useMemo` runs only when `count` changes.

---

### 🚀 2. **Filtered List**

#### ✅ Purpose:
Optimize filtering large data when search query changes.

```jsx
import React, { useState, useMemo } from 'react';

const users = [
  'Nihal', 'Aman', 'Ravi', 'Simran', 'Neha', 'Kiran', 'Aditya', 'Zoya'
];

function FilteredList() {
  const [search, setSearch] = useState('');

  const filteredUsers = useMemo(() => {
    return users.filter(user => user.toLowerCase().includes(search.toLowerCase()));
  }, [search]);

  return (
    <div>
      <input
        type="text"
        placeholder="Search user..."
        value={search}
        onChange={(e) => setSearch(e.target.value)}
      />
      <ul>
        {filteredUsers.map((user, index) => (
          <li key={index}>{user}</li>
        ))}
      </ul>
    </div>
  );
}
export default FilteredList;
```

🧠 **Why `useMemo`?**  
Filters the list only when the search query changes, not on every render.

---

### 🚀 3. **Cart Total Calculation**

#### ✅ Purpose:
Avoid recalculating total price unless cart changes.

```jsx
import React, { useState, useMemo } from 'react';

function Cart() {
  const [cart, setCart] = useState([
    { name: 'T-shirt', price: 300 },
    { name: 'Jeans', price: 1200 },
  ]);

  const total = useMemo(() => {
    console.log('Calculating total...');
    return cart.reduce((acc, item) => acc + item.price, 0);
  }, [cart]);

  return (
    <div>
      <h2>Total: ₹{total}</h2>
      <button onClick={() => setCart([...cart, { name: 'Cap', price: 200 }])}>
        Add Cap
      </button>
    </div>
  );
}
export default Cart;
```

🧠 **Why `useMemo`?**  
Recalculates total only when `cart` updates.

---

### 🚀 4. **Sorted List**

#### ✅ Purpose:
Sort a list of numbers and prevent sorting on every render.

```jsx
import React, { useState, useMemo } from 'react';

function SortedList() {
  const [numbers] = useState([42, 12, 99, 1, 73]);
  const [toggle, setToggle] = useState(false);

  const sortedNumbers = useMemo(() => {
    console.log('Sorting...');
    return [...numbers].sort((a, b) => a - b);
  }, [numbers]);

  return (
    <div>
      <h3>Sorted Numbers: {sortedNumbers.join(', ')}</h3>
      <button onClick={() => setToggle(!toggle)}>Re-render</button>
    </div>
  );
}
export default SortedList;
```

🧠 **Why `useMemo`?**  
Sorting runs once and skips unnecessary recalculations.

---

### 🚀 5. **Form Validation Memoized**

#### ✅ Purpose:
Validate only when form value changes.

```jsx
import React, { useState, useMemo } from 'react';

function EmailValidator() {
  const [email, setEmail] = useState('');

  const isValid = useMemo(() => {
    console.log('Validating...');
    return email.includes('@');
  }, [email]);

  return (
    <div>
      <input
        type="text"
        placeholder="Enter email"
        value={email}
        onChange={(e) => setEmail(e.target.value)}
      />
      <p>{isValid ? 'Valid Email' : 'Invalid Email'}</p>
    </div>
  );
}
export default EmailValidator;
```

🧠 **Why `useMemo`?**  
Validation runs only when `email` changes.

---

### 🚀 6. **Fibonacci Calculator**

#### ✅ Purpose:
Heavy calculation using recursion optimized with `useMemo`.

```jsx
import React, { useState, useMemo } from 'react';

function Fibonacci() {
  const [num, setNum] = useState(1);

  const fib = (n) => {
    if (n <= 1) return n;
    return fib(n - 1) + fib(n - 2);
  };

  const result = useMemo(() => fib(num), [num]);

  return (
    <div>
      <h2>Fibonacci of {num}: {result}</h2>
      <button onClick={() => setNum(num + 1)}>Next</button>
    </div>
  );
}
export default Fibonacci;
```

🧠 **Why `useMemo`?**  
Prevents recomputation unless the input `num` changes.

---

### 🚀 7. **Search Filter with Large List**

```jsx
import React, { useState, useMemo } from 'react';

const data = Array.from({ length: 1000 }, (_, i) => `Item ${i + 1}`);

function LargeListFilter() {
  const [query, setQuery] = useState('');

  const filtered = useMemo(() => {
    return data.filter((item) => item.toLowerCase().includes(query.toLowerCase()));
  }, [query]);

  return (
    <div>
      <input placeholder="Search item..." onChange={(e) => setQuery(e.target.value)} />
      <ul>
        {filtered.slice(0, 10).map((item, index) => (
          <li key={index}>{item}</li>
        ))}
      </ul>
    </div>
  );
}
export default LargeListFilter;
```

---

### 🚀 8. **Button Click Counter Comparison**

```jsx
import React, { useState, useMemo } from 'react';

function CounterMemo() {
  const [a, setA] = useState(0);
  const [b, setB] = useState(0);

  const isEven = useMemo(() => {
    console.log('Checking even...');
    return a % 2 === 0;
  }, [a]);

  return (
    <div>
      <h3>{a} is {isEven ? 'Even' : 'Odd'}</h3>
      <button onClick={() => setA(a + 1)}>Increment A</button>
      <button onClick={() => setB(b + 1)}>Increment B</button>
    </div>
  );
}
export default CounterMemo;
```

---

### 🚀 9. **Memoized Filter with Date Picker**

```jsx
import React, { useState, useMemo } from 'react';

const events = [
  { name: 'Meeting', date: '2024-04-20' },
  { name: 'Hackathon', date: '2024-04-25' },
  { name: 'Interview', date: '2024-04-30' },
];

function DateFilter() {
  const [selectedDate, setSelectedDate] = useState('');

  const filteredEvents = useMemo(() => {
    return events.filter((event) => event.date === selectedDate);
  }, [selectedDate]);

  return (
    <div>
      <input type="date" onChange={(e) => setSelectedDate(e.target.value)} />
      <ul>
        {filteredEvents.map((event, index) => (
          <li key={index}>{event.name}</li>
        ))}
      </ul>
    </div>
  );
}
export default DateFilter;
```

---

### 🚀 10. **Prime Number Checker**

```jsx
import React, { useState, useMemo } from 'react';

function PrimeChecker() {
  const [num, setNum] = useState(2);

  const isPrime = useMemo(() => {
    console.log('Checking prime...');
    for (let i = 2; i < num; i++) {
      if (num % i === 0) return false;
    }
    return true;
  }, [num]);

  return (
    <div>
      <h3>{num} is {isPrime ? 'Prime' : 'Not Prime'}</h3>
      <button onClick={() => setNum(num + 1)}>Next</button>
    </div>
  );
}
export default PrimeChecker;
```

---
Absolutely, Nihal! Let's delve into the `useCallback` hook in React with real-life examples and 10 practice projects, each accompanied by code snippets and explanations.

---

## 🔁 What is `useCallback`?

The `useCallback` hook in React returns a memoized version of a callback function that only changes if one of the dependencies has changed. This is particularly useful when passing callbacks to optimized child components that rely on reference equality to prevent unnecessary renders.

**Syntax:**

```javascript
const memoizedCallback = useCallback(() => {
  // Your callback logic here
}, [dependencies]);
```

**Key Points:**

- **Purpose:** Prevents unnecessary re-creations of functions on every render.
- **Use Case:** Passing stable function references to child components to avoid unnecessary re-renders.
- **Difference from `useMemo`:** While `useMemo` returns a memoized value, `useCallback` returns a memoized function.

---

## 🛠️ 10 Practice Projects Using `useCallback`

### 1. **Counter with Stable Increment Function**

**Objective:** Create a counter component where the increment function is memoized to prevent unnecessary re-renders.

**Code:**

```jsx
import React, { useState, useCallback } from 'react';

function Counter() {
  const [count, setCount] = useState(0);

  const increment = useCallback(() => {
    setCount(prevCount => prevCount + 1);
  }, []);

  return (
    <div>
      <p>Count: {count}</p>
      <button onClick={increment}>Increment</button>
    </div>
  );
}

export default Counter;
```

**Explanation:** The `increment` function is memoized using `useCallback`, ensuring that its reference remains stable across renders.

---

### 2. **Todo List with Memoized Add Function**

**Objective:** Build a todo list where the function to add a new todo is memoized.

**Code:**

```jsx
import React, { useState, useCallback } from 'react';

function TodoList() {
  const [todos, setTodos] = useState([]);

  const addTodo = useCallback(() => {
    setTodos(prevTodos => [...prevTodos, `New Todo ${prevTodos.length + 1}`]);
  }, []);

  return (
    <div>
      <button onClick={addTodo}>Add Todo</button>
      <ul>
        {todos.map((todo, index) => (
          <li key={index}>{todo}</li>
        ))}
      </ul>
    </div>
  );
}

export default TodoList;
```

**Explanation:** The `addTodo` function is memoized to maintain a stable reference, which is beneficial if passed to child components.

---

### 3. **Search Filter with Memoized Handler**

**Objective:** Implement a search filter where the input change handler is memoized.

**Code:**

```jsx
import React, { useState, useCallback } from 'react';

function SearchFilter() {
  const [query, setQuery] = useState('');

  const handleInputChange = useCallback((e) => {
    setQuery(e.target.value);
  }, []);

  return (
    <div>
      <input type="text" value={query} onChange={handleInputChange} />
      <p>Search Query: {query}</p>
    </div>
  );
}

export default SearchFilter;
```

**Explanation:** The `handleInputChange` function is memoized to prevent unnecessary re-creations on each render.

---

### 4. **Parent-Child Communication with Memoized Callback**

**Objective:** Pass a memoized callback from a parent to a child component to prevent unnecessary re-renders.

**Code:**

```jsx
import React, { useState, useCallback } from 'react';

function Child({ onClick }) {
  console.log('Child rendered');
  return <button onClick={onClick}>Click Me</button>;
}

function Parent() {
  const [count, setCount] = useState(0);

  const handleClick = useCallback(() => {
    console.log('Button clicked');
  }, []);

  return (
    <div>
      <p>Count: {count}</p>
      <Child onClick={handleClick} />
      <button onClick={() => setCount(count + 1)}>Increment Count</button>
    </div>
  );
}

export default Parent;
```

**Explanation:** The `handleClick` function is memoized to ensure that the `Child` component doesn't re-render unnecessarily when the `Parent` component re-renders.

---

### 5. **Form Submission with Memoized Handler**

**Objective:** Create a form where the submit handler is memoized.

**Code:**

```jsx
import React, { useState, useCallback } from 'react';

function Form() {
  const [inputValue, setInputValue] = useState('');

  const handleSubmit = useCallback((e) => {
    e.preventDefault();
    console.log('Form submitted with:', inputValue);
  }, [inputValue]);

  return (
    <form onSubmit={handleSubmit}>
      <input value={inputValue} onChange={(e) => setInputValue(e.target.value)} />
      <button type="submit">Submit</button>
    </form>
  );
}

export default Form;
```

**Explanation:** The `handleSubmit` function is memoized with `inputValue` as a dependency, ensuring it updates only when `inputValue` changes.

---

### 6. **Debounced Input with Memoized Handler**

**Objective:** Implement a debounced input field where the change handler is memoized.

**Code:**

```jsx
import React, { useState, useCallback } from 'react';
import debounce from 'lodash.debounce';

function DebouncedInput() {
  const [value, setValue] = useState('');

  const debouncedChangeHandler = useCallback(
    debounce((nextValue) => setValue(nextValue), 1000),
    []
  );

  const handleChange = (e) => {
    debouncedChangeHandler(e.target.value);
  };

  return (
    <div>
      <input onChange={handleChange} />
      <p>Debounced Value: {value}</p>
    </div>
  );
}

export default DebouncedInput;
```

**Explanation:** The `debouncedChangeHandler` is memoized to ensure that the debounce function maintains its identity across renders.

---

### 7. **Toggle Component with Memoized Handler**

**Objective:** Create a toggle component where the toggle function is memoized.

**Code:**

```jsx
import React, { useState, useCallback } from 'react';

function Toggle() {
  const [isOn, setIsOn] = useState(false);

  const toggle = useCallback(() => {
    setIsOn(prevIsOn => !prevIsOn);
  }, []);

  return (
    <div>
      <p>{isOn ? 'ON' : 'OFF'}</p>
      <button onClick={toggle}>Toggle</button>
    </div>
  );
}

export default Toggle;
```

**Explanation:** The `toggle` function is memoized to prevent unnecessary re-creations on each render.

---

Absolutely Nihal! Let's continue from project 8 and go up to 10, all using the `useCallback` hook in React with real-life examples and full code.

---

### **8. List Rendering with Memoized Item Renderer**

**Objective:** Render a list of items where the item renderer is memoized to avoid unnecessary re-renders.

**Code:**

```jsx
import React, { useState, useCallback } from 'react';

const ListItem = React.memo(({ item, onClick }) => {
  console.log('Rendering item:', item);
  return <li onClick={() => onClick(item)}>{item}</li>;
});

function ItemList() {
  const [items] = useState(['Apple', 'Banana', 'Cherry']);

  const handleClick = useCallback((item) => {
    alert(`You clicked on ${item}`);
  }, []);

  return (
    <ul>
      {items.map((item, index) => (
        <ListItem key={index} item={item} onClick={handleClick} />
      ))}
    </ul>
  );
}

export default ItemList;
```

**Explanation:** `handleClick` is memoized to ensure the `ListItem` component doesn't re-render unnecessarily when `ItemList` re-renders.

---

### **9. Favorite Button with useCallback**

**Objective:** Build a button to mark an item as favorite using a memoized click handler.

**Code:**

```jsx
import React, { useState, useCallback } from 'react';

function FavoriteItem({ name, onFavorite }) {
  return (
    <div>
      <span>{name}</span>
      <button onClick={() => onFavorite(name)}>❤️ Favorite</button>
    </div>
  );
}

function FavoriteList() {
  const [favorites, setFavorites] = useState([]);

  const handleFavorite = useCallback((item) => {
    setFavorites((prev) => [...prev, item]);
  }, []);

  return (
    <div>
      <FavoriteItem name="React" onFavorite={handleFavorite} />
      <FavoriteItem name="Node.js" onFavorite={handleFavorite} />
      <p>Favorites: {favorites.join(', ')}</p>
    </div>
  );
}

export default FavoriteList;
```

**Explanation:** `handleFavorite` is memoized to maintain a stable reference and improve performance when passed to multiple child components.

---

### **10. Theme Switcher with useCallback**

**Objective:** Build a theme switcher where the toggle function is memoized.

**Code:**

```jsx
import React, { useState, useCallback } from 'react';

function ThemeToggle({ onToggle }) {
  console.log('ThemeToggle rendered');
  return <button onClick={onToggle}>Toggle Theme</button>;
}

function ThemeApp() {
  const [theme, setTheme] = useState('light');

  const toggleTheme = useCallback(() => {
    setTheme((prev) => (prev === 'light' ? 'dark' : 'light'));
  }, []);

  return (
    <div style={{ backgroundColor: theme === 'light' ? '#fff' : '#333', color: theme === 'light' ? '#000' : '#fff', minHeight: '100vh', padding: '20px' }}>
      <h1>Current Theme: {theme}</h1>
      <ThemeToggle onToggle={toggleTheme} />
    </div>
  );
}

export default ThemeApp;
```

**Explanation:** The `toggleTheme` function is memoized so the `ThemeToggle` component only re-renders when it really needs to.

---

## ✅ Summary of `useCallback` Use Cases

| Project # | Real-Life Use Case                         | Purpose of `useCallback`                          |
|-----------|---------------------------------------------|---------------------------------------------------|
| 1         | Counter                                      | Stable increment function                         |
| 2         | Todo List                                    | Add todo function stability                       |
| 3         | Search Filter                                | Stable input change handler                       |
| 4         | Parent to Child communication                | Prevent child re-renders                          |
| 5         | Form submit                                  | Stable submit handler                             |
| 6         | Debounced input                              | Stable debounce logic                             |
| 7         | Toggle button                                | Toggle state with stable function                 |
| 8         | List rendering                               | Optimize re-renders with memoized child           |
| 9         | Favorite button                              | Memoized click handler for dynamic items          |
| 10        | Theme switcher                               | Stable theme toggle across components             |

---

Absolutely, Nihal! Let's delve into the **`useContext` hook** in React, providing a clear explanation, a real-life example, and 10 mini-projects complete with code and explanations.

---

## 🧠 Understanding `useContext`

The `useContext` hook in React allows components to access values from a context without the need to pass props through every level of the component tree. This is particularly useful for global data like themes, user information, or settings that many components need to access.

### 🔧 How It Works:

1. **Create a Context**: Use `React.createContext()` to create a context object.
2. **Provide the Context**: Wrap your component tree with the `Context.Provider` and pass the value you want to share.
3. **Consume the Context**: In any component, use the `useContext` hook to access the context value.

This approach helps in avoiding "prop drilling," where props are passed down through multiple layers of components.

---

## 📦 Real-Life Example: Theme Management

Imagine you have an application where users can toggle between light and dark themes. Instead of passing the theme state through props to every component, you can use `useContext` to manage this globally.

---

## 🔟 Mini Projects Using `useContext`

Here are 10 mini-projects to practice and understand the `useContext` hook:

### 1. **Theme Toggle App**

**Objective**: Implement a light/dark theme toggle using context.

**Code**:

```jsx
// ThemeContext.js
import React, { createContext, useState } from 'react';

export const ThemeContext = createContext();

export function ThemeProvider({ children }) {
  const [theme, setTheme] = useState('light');
  const toggleTheme = () => setTheme((prev) => (prev === 'light' ? 'dark' : 'light'));

  return (
    <ThemeContext.Provider value={{ theme, toggleTheme }}>
      {children}
    </ThemeContext.Provider>
  );
}
```

```jsx
// App.js
import React, { useContext } from 'react';
import { ThemeContext, ThemeProvider } from './ThemeContext';

function ThemedComponent() {
  const { theme, toggleTheme } = useContext(ThemeContext);
  return (
    <div style={{ background: theme === 'light' ? '#fff' : '#333', color: theme === 'light' ? '#000' : '#fff' }}>
      <p>Current Theme: {theme}</p>
      <button onClick={toggleTheme}>Toggle Theme</button>
    </div>
  );
}

function App() {
  return (
    <ThemeProvider>
      <ThemedComponent />
    </ThemeProvider>
  );
}

export default App;
```

**Explanation**: The `ThemeContext` provides the current theme and a function to toggle it. `ThemedComponent` consumes this context to display and change the theme.

---

### 2. **User Authentication Status**

**Objective**: Display user login status across components.

**Code**:

```jsx
// AuthContext.js
import React, { createContext, useState } from 'react';

export const AuthContext = createContext();

export function AuthProvider({ children }) {
  const [user, setUser] = useState(null);
  const login = (username) => setUser({ name: username });
  const logout = () => setUser(null);

  return (
    <AuthContext.Provider value={{ user, login, logout }}>
      {children}
    </AuthContext.Provider>
  );
}
```

```jsx
// App.js
import React, { useContext } from 'react';
import { AuthContext, AuthProvider } from './AuthContext';

function Navbar() {
  const { user, login, logout } = useContext(AuthContext);
  return (
    <nav>
      {user ? (
        <>
          <span>Welcome, {user.name}</span>
          <button onClick={logout}>Logout</button>
        </>
      ) : (
        <button onClick={() => login('Nihal')}>Login</button>
      )}
    </nav>
  );
}

function App() {
  return (
    <AuthProvider>
      <Navbar />
    </AuthProvider>
  );
}

export default App;
```

**Explanation**: The `AuthContext` manages user authentication state. The `Navbar` component consumes this context to display login status and provide login/logout functionality.

---

### 3. **Language Selector**

**Objective**: Implement a multilingual app with language selection.

**Code**:

```jsx
// LanguageContext.js
import React, { createContext, useState } from 'react';

export const LanguageContext = createContext();

export function LanguageProvider({ children }) {
  const [language, setLanguage] = useState('en');
  const switchLanguage = (lang) => setLanguage(lang);

  return (
    <LanguageContext.Provider value={{ language, switchLanguage }}>
      {children}
    </LanguageContext.Provider>
  );
}
```

```jsx
// App.js
import React, { useContext } from 'react';
import { LanguageContext, LanguageProvider } from './LanguageContext';

function Greeting() {
  const { language, switchLanguage } = useContext(LanguageContext);
  const greetings = { en: 'Hello', es: 'Hola', fr: 'Bonjour' };

  return (
    <div>
      <p>{greetings[language]}</p>
      <button onClick={() => switchLanguage('en')}>English</button>
      <button onClick={() => switchLanguage('es')}>Spanish</button>
      <button onClick={() => switchLanguage('fr')}>French</button>
    </div>
  );
}

function App() {
  return (
    <LanguageProvider>
      <Greeting />
    </LanguageProvider>
  );
}

export default App;
```

**Explanation**: The `LanguageContext` manages the current language. The `Greeting` component consumes this context to display greetings in the selected language.

---

Sure, Nihal! Let's continue from where we left off. We were in the middle of **Mini Project 4: Shopping Cart** using the `useContext` hook. Here's the rest of it:

---

### 4. **Shopping Cart** (continued)

```jsx
// Cart.js
import React, { useContext } from 'react';
import { CartContext } from './CartContext';

function Cart() {
  const { cart, removeItem } = useContext(CartContext);

  return (
    <div>
      <h3>Cart Items:</h3>
      <ul>
        {cart.map((item, index) => (
          <li key={index}>
            {item} <button onClick={() => removeItem(item)}>Remove</button>
          </li>
        ))}
      </ul>
    </div>
  );
}

export default Cart;
```

```jsx
// App.js
import React from 'react';
import { CartProvider } from './CartContext';
import ProductList from './ProductList';
import Cart from './Cart';

function App() {
  return (
    <CartProvider>
      <h1>My Shop</h1>
      <ProductList />
      <Cart />
    </CartProvider>
  );
}

export default App;
```

**Explanation**: The `CartContext` holds the state of cart items. Components like `ProductList` and `Cart` can add or remove items without props.

---

### 5. **Toggle Sidebar**

**Objective**: Control a sidebar’s open/close state using context.

```jsx
// SidebarContext.js
import React, { createContext, useState } from 'react';

export const SidebarContext = createContext();

export function SidebarProvider({ children }) {
  const [isOpen, setIsOpen] = useState(false);
  const toggleSidebar = () => setIsOpen((prev) => !prev);

  return (
    <SidebarContext.Provider value={{ isOpen, toggleSidebar }}>
      {children}
    </SidebarContext.Provider>
  );
}
```

```jsx
// Sidebar.js
import React, { useContext } from 'react';
import { SidebarContext } from './SidebarContext';

function Sidebar() {
  const { isOpen } = useContext(SidebarContext);
  return isOpen ? <div style={{ width: '200px', background: '#ddd' }}>Sidebar Content</div> : null;
}
```

```jsx
// App.js
import React, { useContext } from 'react';
import { SidebarProvider, SidebarContext } from './SidebarContext';
import Sidebar from './Sidebar';

function ToggleButton() {
  const { toggleSidebar } = useContext(SidebarContext);
  return <button onClick={toggleSidebar}>Toggle Sidebar</button>;
}

function App() {
  return (
    <SidebarProvider>
      <ToggleButton />
      <Sidebar />
    </SidebarProvider>
  );
}

export default App;
```

---

Absolutely Nihal! Here's the **continuation of useContext Hook mini-projects (6 to 10)** — with **questions (what to build), code**, and a short **explanation** for each.

---

## ✅ 6. **Dark Mode Blog App**

### **Question:**
Create a blog app where you can toggle between light and dark mode using `useContext`.

### **Answer:**

```jsx
// ThemeContext.js
import React, { createContext, useState } from 'react';

export const ThemeContext = createContext();

export function ThemeProvider({ children }) {
  const [darkMode, setDarkMode] = useState(false);
  const toggleTheme = () => setDarkMode((prev) => !prev);

  return (
    <ThemeContext.Provider value={{ darkMode, toggleTheme }}>
      {children}
    </ThemeContext.Provider>
  );
}
```

```jsx
// Blog.js
import React, { useContext } from 'react';
import { ThemeContext } from './ThemeContext';

function Blog() {
  const { darkMode } = useContext(ThemeContext);
  const themeStyle = {
    background: darkMode ? '#333' : '#fff',
    color: darkMode ? '#fff' : '#000',
    padding: '1rem',
    margin: '1rem'
  };

  return (
    <div style={themeStyle}>
      <h2>My Blog Post</h2>
      <p>This is a blog post content.</p>
    </div>
  );
}
```

```jsx
// App.js
import React, { useContext } from 'react';
import { ThemeProvider, ThemeContext } from './ThemeContext';
import Blog from './Blog';

function ToggleThemeButton() {
  const { toggleTheme } = useContext(ThemeContext);
  return <button onClick={toggleTheme}>Toggle Theme</button>;
}

function App() {
  return (
    <ThemeProvider>
      <ToggleThemeButton />
      <Blog />
    </ThemeProvider>
  );
}

export default App;
```

**What it teaches**: Using `useContext` to share and apply theme preferences globally.

---

## ✅ 7. **Form Wizard Manager**

### **Question:**
Build a multi-step form that shares user data across steps using `useContext`.

### **Answer:**

```jsx
// FormContext.js
import React, { createContext, useState } from 'react';

export const FormContext = createContext();

export function FormProvider({ children }) {
  const [formData, setFormData] = useState({ name: '', email: '' });

  const updateField = (field, value) => {
    setFormData((prev) => ({ ...prev, [field]: value }));
  };

  return (
    <FormContext.Provider value={{ formData, updateField }}>
      {children}
    </FormContext.Provider>
  );
}
```

```jsx
// Step1.js
import React, { useContext } from 'react';
import { FormContext } from './FormContext';

function Step1() {
  const { formData, updateField } = useContext(FormContext);

  return (
    <div>
      <h2>Step 1</h2>
      <input
        type="text"
        value={formData.name}
        onChange={(e) => updateField('name', e.target.value)}
        placeholder="Name"
      />
    </div>
  );
}
```

```jsx
// Step2.js
import React, { useContext } from 'react';
import { FormContext } from './FormContext';

function Step2() {
  const { formData, updateField } = useContext(FormContext);

  return (
    <div>
      <h2>Step 2</h2>
      <input
        type="email"
        value={formData.email}
        onChange={(e) => updateField('email', e.target.value)}
        placeholder="Email"
      />
    </div>
  );
}
```

```jsx
// App.js
import React from 'react';
import { FormProvider } from './FormContext';
import Step1 from './Step1';
import Step2 from './Step2';

function App() {
  return (
    <FormProvider>
      <Step1 />
      <Step2 />
    </FormProvider>
  );
}

export default App;
```

**What it teaches**: Use context to handle form state across multiple steps.

---

## ✅ 8. **Global Notification System**

### **Question:**
Create a toast notification system where you can trigger messages from anywhere in the app using `useContext`.

### **Answer:**

```jsx
// NotificationContext.js
import React, { createContext, useState } from 'react';

export const NotificationContext = createContext();

export function NotificationProvider({ children }) {
  const [message, setMessage] = useState('');

  const notify = (msg) => {
    setMessage(msg);
    setTimeout(() => setMessage(''), 3000);
  };

  return (
    <NotificationContext.Provider value={{ notify }}>
      {children}
      {message && <div className="toast">{message}</div>}
    </NotificationContext.Provider>
  );
}
```

```jsx
// SomeComponent.js
import React, { useContext } from 'react';
import { NotificationContext } from './NotificationContext';

function SomeComponent() {
  const { notify } = useContext(NotificationContext);
  return <button onClick={() => notify('Item added!')}>Add Item</button>;
}

export default SomeComponent;
```

```jsx
// App.js
import React from 'react';
import { NotificationProvider } from './NotificationContext';
import SomeComponent from './SomeComponent';

function App() {
  return (
    <NotificationProvider>
      <SomeComponent />
    </NotificationProvider>
  );
}

export default App;
```

**What it teaches**: Global toast messages from any part of the app using `useContext`.

---

## ✅ 9. **Quiz Score Tracker**

### **Question:**
Track and update quiz score globally using context.

### **Answer:**

```jsx
// QuizContext.js
import React, { createContext, useState } from 'react';

export const QuizContext = createContext();

export function QuizProvider({ children }) {
  const [score, setScore] = useState(0);

  const increaseScore = () => setScore((prev) => prev + 1);

  return (
    <QuizContext.Provider value={{ score, increaseScore }}>
      {children}
    </QuizContext.Provider>
  );
}
```

```jsx
// Question.js
import React, { useContext } from 'react';
import { QuizContext } from './QuizContext';

function Question() {
  const { increaseScore } = useContext(QuizContext);

  return (
    <div>
      <h2>What is 2 + 2?</h2>
      <button onClick={increaseScore}>4</button>
      <button>3</button>
    </div>
  );
}
```

```jsx
// Score.js
import React, { useContext } from 'react';
import { QuizContext } from './QuizContext';

function Score() {
  const { score } = useContext(QuizContext);
  return <div>Score: {score}</div>;
}
```

```jsx
// App.js
import React from 'react';
import { QuizProvider } from './QuizContext';
import Question from './Question';
import Score from './Score';

function App() {
  return (
    <QuizProvider>
      <Score />
      <Question />
    </QuizProvider>
  );
}

export default App;
```

**What it teaches**: Score tracking across quiz components.

---

## ✅ 10. **Favorite Articles Tracker**

### **Question:**
Track favorite articles in a blog app using context.

### **Answer:**

```jsx
// FavoriteContext.js
import React, { createContext, useState } from 'react';

export const FavoriteContext = createContext();

export function FavoriteProvider({ children }) {
  const [favorites, setFavorites] = useState([]);

  const toggleFavorite = (article) => {
    setFavorites((prev) =>
      prev.includes(article) ? prev.filter((a) => a !== article) : [...prev, article]
    );
  };

  return (
    <FavoriteContext.Provider value={{ favorites, toggleFavorite }}>
      {children}
    </FavoriteContext.Provider>
  );
}
```

```jsx
// Article.js
import React, { useContext } from 'react';
import { FavoriteContext } from './FavoriteContext';

function Article({ title }) {
  const { favorites, toggleFavorite } = useContext(FavoriteContext);

  return (
    <div>
      <h3>{title}</h3>
      <button onClick={() => toggleFavorite(title)}>
        {favorites.includes(title) ? 'Remove from Favorites' : 'Add to Favorites'}
      </button>
    </div>
  );
}

export default Article;
```

```jsx
// App.js
import React from 'react';
import { FavoriteProvider } from './FavoriteContext';
import Article from './Article';

function App() {
  return (
    <FavoriteProvider>
      <Article title="React Hooks Overview" />
      <Article title="Understanding useContext" />
    </FavoriteProvider>
  );
}

export default App;
```

**What it teaches**: Managing a list of favorites globally.




Absolutely, Nihal! Let's delve into the `useReducer` hook in React, exploring its purpose, usage, and practical applications through real-life examples and mini-projects.

---

## 🧠 Understanding `useReducer` Hook

### What is `useReducer`?

The `useReducer` hook is an alternative to `useState` for managing complex state logic in React components. It is particularly useful when:

- The state logic is complex and involves multiple sub-values.
- The next state depends on the previous one.
- You want to centralize state updates in a single function.

### Syntax

```jsx
const [state, dispatch] = useReducer(reducer, initialState);
```

- `reducer`: A function that determines how the state should change based on the action.
- `initialState`: The initial state value.
- `state`: The current state.
- `dispatch`: A function to dispatch actions to the reducer.

### Reducer Function

```jsx
function reducer(state, action) {
  switch (action.type) {
    case 'ACTION_TYPE':
      return { ...state, /* updated state */ };
    default:
      return state;
  }
}
```

---

## 🔟 Mini Projects Using `useReducer`

Let's explore 10 mini-projects that demonstrate the practical use of `useReducer`.

---

### 1. **Counter App**

**Objective**: Implement a simple counter with increment and decrement functionality.

**Code**:

```jsx
import React, { useReducer } from 'react';

const initialState = { count: 0 };

function reducer(state, action) {
  switch (action.type) {
    case 'increment':
      return { count: state.count + 1 };
    case 'decrement':
      return { count: state.count - 1 };
    default:
      return state;
  }
}

function Counter() {
  const [state, dispatch] = useReducer(reducer, initialState);
  return (
    <div>
      <p>Count: {state.count}</p>
      <button onClick={() => dispatch({ type: 'decrement' })}>-</button>
      <button onClick={() => dispatch({ type: 'increment' })}>+</button>
    </div>
  );
}

export default Counter;
```

**Explanation**: The reducer manages the count state, updating it based on the dispatched action type.

---

### 2. **Todo List**

**Objective**: Manage a list of todos with add and remove functionality.

**Code**:

```jsx
import React, { useReducer, useState } from 'react';

const initialState = [];

function reducer(state, action) {
  switch (action.type) {
    case 'add':
      return [...state, { id: Date.now(), text: action.payload }];
    case 'remove':
      return state.filter(todo => todo.id !== action.payload);
    default:
      return state;
  }
}

function TodoList() {
  const [state, dispatch] = useReducer(reducer, initialState);
  const [text, setText] = useState('');

  const addTodo = () => {
    dispatch({ type: 'add', payload: text });
    setText('');
  };

  return (
    <div>
      <input value={text} onChange={e => setText(e.target.value)} />
      <button onClick={addTodo}>Add</button>
      <ul>
        {state.map(todo => (
          <li key={todo.id}>
            {todo.text}
            <button onClick={() => dispatch({ type: 'remove', payload: todo.id })}>X</button>
          </li>
        ))}
      </ul>
    </div>
  );
}

export default TodoList;
```

**Explanation**: The reducer handles adding and removing todos from the list.

---

### 3. **Form Input Management**

**Objective**: Manage form inputs using `useReducer`.

**Code**:

```jsx
import React, { useReducer } from 'react';

const initialState = { name: '', email: '' };

function reducer(state, action) {
  switch (action.type) {
    case 'update':
      return { ...state, [action.field]: action.value };
    case 'reset':
      return initialState;
    default:
      return state;
  }
}

function Form() {
  const [state, dispatch] = useReducer(reducer, initialState);

  const handleChange = e => {
    dispatch({ type: 'update', field: e.target.name, value: e.target.value });
  };

  const handleSubmit = e => {
    e.preventDefault();
    console.log(state);
    dispatch({ type: 'reset' });
  };

  return (
    <form onSubmit={handleSubmit}>
      <input name="name" value={state.name} onChange={handleChange} />
      <input name="email" value={state.email} onChange={handleChange} />
      <button type="submit">Submit</button>
    </form>
  );
}

export default Form;
```

**Explanation**: The reducer updates form fields and resets the form upon submission.

---

### 4. **Shopping Cart**

**Objective**: Implement a shopping cart with add and remove item functionality.

**Code**:

```jsx
import React, { useReducer } from 'react';

const initialState = [];

function reducer(state, action) {
  switch (action.type) {
    case 'add':
      return [...state, action.item];
    case 'remove':
      return state.filter(item => item.id !== action.id);
    default:
      return state;
  }
}

function ShoppingCart() {
  const [state, dispatch] = useReducer(reducer, initialState);

  const addItem = item => {
    dispatch({ type: 'add', item });
  };

  const removeItem = id => {
    dispatch({ type: 'remove', id });
  };

  return (
    <div>
      <button onClick={() => addItem({ id: 1, name: 'Apple' })}>Add Apple</button>
      <ul>
        {state.map(item => (
          <li key={item.id}>
            {item.name}
            <button onClick={() => removeItem(item.id)}>X</button>
          </li>
        ))}
      </ul>
    </div>
  );
}

export default ShoppingCart;
```

**Explanation**: The reducer manages the cart items, allowing addition and removal.

---

### 5. **Authentication State**

**Objective**: Manage user authentication state.

**Code**:

```jsx
import React, { useReducer } from 'react';

const initialState = { isAuthenticated: false, user: null };

function reducer(state, action) {
  switch (action.type) {
    case 'login':
      return { isAuthenticated: true, user: action.user };
    case 'logout':
      return { isAuthenticated: false, user: null };
    default:
      return state;
  }
}

function Auth() {
  const [state, dispatch] = useReducer(reducer, initialState);

  const login = () => {
    dispatch({ type: 'login', user: { name: 'Nihal' } });
  };

  const logout = () => {
    dispatch({ type: 'logout' });
  };

  return (
    <div>
      {state.isAuthenticated ? (
        <div>
          <p>Welcome 

