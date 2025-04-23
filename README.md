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

