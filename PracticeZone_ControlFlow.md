# 🧪 Practice Zone - Control Flow Exercises

Five practical exercises with complete solutions and detailed explanations.

---

## 1️⃣ Student Grade Logic

**Problem**: Print A, B, C, D, or F based on marks.

```javascript
function getGrade(marks) {
  if (marks >= 90) return "A";
  if (marks >= 80) return "B";
  if (marks >= 70) return "C";
  if (marks >= 60) return "D";
  return "F";
}

// Test cases
console.log(getGrade(95)); // "A"
console.log(getGrade(85)); // "B"
console.log(getGrade(75)); // "C"
console.log(getGrade(65)); // "D"
console.log(getGrade(45)); // "F"
```

**With switch-case (alternative)**:
```javascript
function getGrade(marks) {
  switch (true) {
    case marks >= 90:
      return "A";
    case marks >= 80:
      return "B";
    case marks >= 70:
      return "C";
    case marks >= 60:
      return "D";
    default:
      return "F";
  }
}
```

**Extended version (with percentage & description)**:
```javascript
function getGradeDetails(marks) {
  let grade, description;
  
  if (marks >= 90) {
    grade = "A";
    description = "Excellent performance";
  } else if (marks >= 80) {
    grade = "B";
    description = "Very good";
  } else if (marks >= 70) {
    grade = "C";
    description = "Good";
  } else if (marks >= 60) {
    grade = "D";
    description = "Satisfactory";
  } else {
    grade = "F";
    description = "Needs improvement";
  }
  
  return {
    marks: marks,
    grade: grade,
    description: description,
    status: marks >= 60 ? "✓ PASS" : "✗ FAIL"
  };
}

console.log(getGradeDetails(82));
// { marks: 82, grade: 'B', description: 'Very good', status: '✓ PASS' }
```

---

## 2️⃣ Rock-Paper-Scissors Game

**Problem**: Given player1 and player2's choice, print winner or draw.

```javascript
function playGame(player1, player2) {
  // Check for draw
  if (player1 === player2) {
    return "Draw! Both chose " + player1;
  }
  
  // Player 1 wins
  if (
    (player1 === "rock" && player2 === "scissors") ||
    (player1 === "paper" && player2 === "rock") ||
    (player1 === "scissors" && player2 === "paper")
  ) {
    return "Player 1 wins! " + player1 + " beats " + player2;
  }
  
  // Player 2 wins
  return "Player 2 wins! " + player2 + " beats " + player1;
}

// Test cases
console.log(playGame("rock", "scissors"));      // "Player 1 wins!"
console.log(playGame("paper", "paper"));        // "Draw!"
console.log(playGame("scissors", "rock"));      // "Player 2 wins!"
console.log(playGame("rock", "paper"));         // "Player 2 wins!"
```

**Using switch (cleaner approach)**:
```javascript
function playGame(p1, p2) {
  if (p1 === p2) return "Draw!";
  
  switch (p1 + "-" + p2) {
    case "rock-scissors":
    case "paper-rock":
    case "scissors-paper":
      return "Player 1 wins!";
    default:
      return "Player 2 wins!";
  }
}

console.log(playGame("rock", "scissors"));  // "Player 1 wins!"
console.log(playGame("paper", "paper"));    // "Draw!"
```

**Advanced version with details**:
```javascript
function playRockPaperScissors(p1, p2) {
  // Validation
  const valid = ["rock", "paper", "scissors"];
  if (!valid.includes(p1) || !valid.includes(p2)) {
    return "Invalid choice! Use rock, paper, or scissors";
  }
  
  // Draw
  if (p1 === p2) {
    return {
      result: "Draw",
      message: `Both chose ${p1}`,
      winner: null
    };
  }
  
  // Winning conditions
  const winConditions = {
    "rock-scissors": "rock crushes scissors",
    "paper-rock": "paper covers rock",
    "scissors-paper": "scissors cuts paper"
  };
  
  const key = p1 + "-" + p2;
  
  if (winConditions[key]) {
    return {
      result: "Player 1 wins",
      message: winConditions[key],
      winner: "player1"
    };
  } else {
    const reversedKey = p2 + "-" + p1;
    return {
      result: "Player 2 wins",
      message: winConditions[reversedKey],
      winner: "player2"
    };
  }
}

console.log(playRockPaperScissors("rock", "scissors"));
// { result: "Player 1 wins", message: "rock crushes scissors", winner: "player1" }
```

---

## 3️⃣ Login Message

**Problem**: Show different messages based on login status and admin privileges.

```javascript
function getLoginMessage(isLoggedIn, isAdmin) {
  if (isLoggedIn && isAdmin) {
    return "Welcome Admin! You have full access";
  } else if (isLoggedIn && !isAdmin) {
    return "Welcome User! You have limited access";
  } else if (!isLoggedIn) {
    return "Please log in first";
  }
}

// Test cases
console.log(getLoginMessage(true, true));   // "Welcome Admin! You have full access"
console.log(getLoginMessage(true, false));  // "Welcome User! You have limited access"
console.log(getLoginMessage(false, false)); // "Please log in first"
console.log(getLoginMessage(false, true));  // "Please log in first"
```

**Using switch with combined condition**:
```javascript
function getLoginMessage(isLoggedIn, isAdmin) {
  const status = isLoggedIn + "-" + isAdmin;
  
  switch (status) {
    case "true-true":
      return "Welcome Admin! Full access granted";
    case "true-false":
      return "Welcome User! Limited access";
    case "false-true":
    case "false-false":
      return "Please log in first";
  }
}
```

**Extended with permissions**:
```javascript
function getUserAccess(isLoggedIn, isAdmin, isPremium) {
  // Guard clause: not logged in
  if (!isLoggedIn) {
    return {
      canView: false,
      canEdit: false,
      canDelete: false,
      message: "Please log in first"
    };
  }
  
  // Logged in - determine permissions
  let canView = true;
  let canEdit = isAdmin || isPremium;
  let canDelete = isAdmin;
  let role = isAdmin ? "Admin" : isPremium ? "Premium" : "Regular";
  
  return {
    role: role,
    canView: canView,
    canEdit: canEdit,
    canDelete: canDelete,
    message: `Welcome ${role}!`
  };
}

console.log(getUserAccess(true, true, false));
// { role: 'Admin', canView: true, canEdit: true, canDelete: true, message: 'Welcome Admin!' }

console.log(getUserAccess(true, false, true));
// { role: 'Premium', canView: true, canEdit: true, canDelete: false, message: 'Welcome Premium!' }

console.log(getUserAccess(false, false, false));
// { canView: false, canEdit: false, canDelete: false, message: 'Please log in first' }
```

---

## 4️⃣ Weather Advice

**Problem**: Use switch-case to print what to wear based on weather.

```javascript
function getWeatherAdvice(weather) {
  switch (weather.toLowerCase()) {
    case "rainy":
      return "☔ Wear a raincoat and carry an umbrella";
    
    case "sunny":
      return "😎 Apply sunscreen, wear light clothes";
    
    case "cold":
      return "🧥 Wear warm clothes, jacket, and gloves";
    
    case "hot":
      return "👕 Wear light, breathable clothing";
    
    case "snowy":
      return "⛄ Wear heavy winter coat, boots, and hat";
    
    case "windy":
      return "💨 Secure loose items, wear windproof jacket";
    
    default:
      return "🤷 Check the forecast for more details";
  }
}

// Test cases
console.log(getWeatherAdvice("rainy"));   // "☔ Wear a raincoat..."
console.log(getWeatherAdvice("sunny"));   // "😎 Apply sunscreen..."
console.log(getWeatherAdvice("cold"));    // "🧥 Wear warm clothes..."
```

**Advanced with temperature**:
```javascript
function getWeatherAdvice(weather, temp) {
  // Guard clause
  if (!weather) return "Please specify weather";
  
  // First check extreme temperatures
  if (temp < 0) {
    return "❄️ Extreme cold! Wear heavy winter gear";
  } else if (temp > 40) {
    return "🔥 Extreme heat! Stay hydrated and wear light clothes";
  }
  
  // Then check weather type
  switch (weather) {
    case "rainy":
      return temp < 15 ? "☔ Cold rain - wear warm raincoat" : "☔ Wear light raincoat";
    case "sunny":
      return temp > 30 ? "😎 Hot and sunny - apply sunscreen" : "🌞 Nice weather";
    case "cloudy":
      return "☁️ Cloudy - bring a light jacket";
    case "snowy":
      return "⛄ Snow - wear winter clothes";
    default:
      return "Check the forecast";
  }
}

console.log(getWeatherAdvice("rainy", 10));   // "☔ Cold rain - wear warm raincoat"
console.log(getWeatherAdvice("sunny", 35));   // "😎 Hot and sunny - apply sunscreen"
```

---

## 5️⃣ Age Checker

**Problem**: Return "Kid", "Teen", "Adult", or "Senior" with all details.

```javascript
function getAgeCategory(age) {
  if (age < 13) {
    return "Kid";
  } else if (age < 18) {
    return "Teen";
  } else if (age < 65) {
    return "Adult";
  } else {
    return "Senior";
  }
}

// Test cases
console.log(getAgeCategory(10));  // "Kid"
console.log(getAgeCategory(15));  // "Teen"
console.log(getAgeCategory(30));  // "Adult"
console.log(getAgeCategory(70));  // "Senior"
```

**Using ternary (compact)**:
```javascript
const getAgeCategory = (age) =>
  age < 13 ? "Kid" :
  age < 18 ? "Teen" :
  age < 65 ? "Adult" :
  "Senior";
```

**Extended with full details**:
```javascript
function getAgeDetails(age) {
  // Validation
  if (age < 0 || age > 150) {
    return { error: "Invalid age" };
  }
  
  let category, activities, needs, restrictions;
  
  if (age < 13) {
    category = "Kid";
    activities = ["Play", "Learn", "Sports"];
    needs = ["Supervision", "Education"];
    restrictions = ["No work", "No voting", "No driving"];
  } else if (age < 18) {
    category = "Teen";
    activities = ["School", "Sports", "Socializing"];
    needs = ["Guidance", "Support"];
    restrictions = ["No voting", "Limited work", "No driving (most places)"];
  } else if (age < 65) {
    category = "Adult";
    activities = ["Work", "Family", "Hobbies"];
    needs = ["Career", "Responsibilities"];
    restrictions = ["None"];
  } else {
    category = "Senior";
    activities = ["Retirement", "Travel", "Hobbies"];
    needs = ["Healthcare", "Leisure"];
    restrictions = ["Age-dependent benefits"];
  }
  
  return {
    age: age,
    category: category,
    activities: activities,
    needs: needs,
    restrictions: restrictions
  };
}

console.log(getAgeDetails(15));
// {
//   age: 15,
//   category: 'Teen',
//   activities: ['School', 'Sports', 'Socializing'],
//   needs: ['Guidance', 'Support'],
//   restrictions: ['No voting', 'Limited work', 'No driving (most places)']
// }

console.log(getAgeDetails(70));
// {
//   age: 70,
//   category: 'Senior',
//   activities: ['Retirement', 'Travel', 'Hobbies'],
//   needs: ['Healthcare', 'Leisure'],
//   restrictions: ['Age-dependent benefits']
// }
```

**Switch-case approach**:
```javascript
function getAgeDetails(age) {
  let category;
  
  switch (true) {
    case age < 13:
      category = "Kid";
      break;
    case age < 18:
      category = "Teen";
      break;
    case age < 65:
      category = "Adult";
      break;
    default:
      category = "Senior";
  }
  
  return {
    age: age,
    category: category,
    eligible: {
      school: age < 30,
      work: age >= 18 && age < 65,
      voting: age >= 18,
      pension: age >= 65
    }
  };
}

console.log(getAgeDetails(25));
// { age: 25, category: 'Adult', eligible: { school: true, work: true, voting: true, pension: false } }
```

---

## 🎯 Practice Challenges

Try solving these on your own:

1. **Grade Logic**: Add '+' and '-' modifiers (A+, A, A-, B+, etc.)
2. **Rock-Paper-Scissors**: Add Lizard and Spock (5 options)
3. **Login Message**: Add different messages for "banned" accounts
4. **Weather**: Add humidity and wind speed to advice
5. **Age Checker**: Return eligibility for driving, voting, work

---

## 📊 Quick Comparison

| Exercise | Best Approach | Key Concept |
|----------|---------------|-------------|
| Grade Logic | if-else if | Multiple ranges |
| RPS Game | if with conditions OR | Winning patterns |
| Login | if-else if | Multiple conditions |
| Weather | switch-case | Single variable |
| Age Checker | if-else if or ternary | Simple ranges |

---

**Key Takeaways**:
- Use **if-else if** for ranges and complex logic
- Use **switch** for exact matches (weather, status codes)
- Use **early returns** to avoid nesting
- Always **validate input** first
- Return **objects** for rich information

---

**Keep Practicing! 🚀**
