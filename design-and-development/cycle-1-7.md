# 2.2.8 Cycle 8

### Design

In this cycle, the HUD will be designed and fully prepared. The main menu will be designed. A completion design will be added.

### Objectives

* [x] Menu

### Usability Features

Non-functional aspects: Make the menu fit the theme of the game

### Key Variables

| Variable Name | Use |
| ------------- | --- |
|               |     |
|               |     |
|               |     |

### Pseudocode

```
Create a readline interface for input and output
Clear the console
Display a header with a blue line and a game title
Display menu options:
  - Option 1: Start the game
  - Option 2: View high scores
  - Option 3: Quit
Prompt the user to choose an option with a cyan-colored message

Wait for the user's input and execute the following based on the input:
  If the input is '1':
    Display a message indicating the game is starting in green
    Close the readline interface
  Else, if the input is '2':
    Display a message indicating high scores are being shown in green
    Close the readline interface
  Else, if the input is '3':
    Display a message indicating the game is quitting in green
    Close the readline interface
  Else (if the input is not '1', '2', or '3'):
    Display an error message in red indicating an invalid option
    Close the readline interface
```

## Development

### Outcome



```javascript
const readline = require('readline').createInterface({
  input: process.stdin,
  output: process.stdout
})
console.clear();
console.log("\x1b[34m%s\x1b[0m", "======================================================================");
console.log("\x1b[34m%s\x1b[0m", "        The Boxing World Championship - Begin your Journey!");
console.log("\x1b[34m%s\x1b[0m", "======================================================================");
console.log("\x1b[33m%s\x1b[0m", "Press '1' to Start the game");
console.log("\x1b[33m%s\x1b[0m", "Press '2' to View high scores");
console.log("\x1b[33m%s\x1b[0m", "Press '3' to Quit");
readline.question(`\x1b[36m%s\x1b[0m`,"Choose an option: ", (option) => {
  if(option === '1'){
     console.log("\x1b[32m%s\x1b[0m","Starting the game...");
     readline.close()
  } else if (option === '2'){
     console.log("\x1b[32m%s\x1b[0m","Showing high scores...");
     readline.close()
  } else if (option === '3'){
     console.log("\x1b[32m%s\x1b[0m","Quitting game...");
     readline.close()
  } else {
     console.log("\x1b[31m%s\x1b[0m","Invalid Option. Please try again");
     readline.close()
  }
})
```



```javascript
```



```javascript
```



```javascript
```

### Challenges



## Testing

Evidence for testing

### Tests

<table><thead><tr><th width="87">Test</th><th width="127">Instructions</th><th width="223">What I expect</th><th width="208">What actually happens</th><th>Pass/Fail</th></tr></thead><tbody><tr><td>1</td><td></td><td></td><td></td><td></td></tr></tbody></table>

### Evidence

<figure><img src="../.gitbook/assets/image (18).png" alt=""><figcaption></figcaption></figure>
