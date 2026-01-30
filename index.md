---
layout: default
---

<style>
body {
  max-width: 900px;
  margin: 40px auto;
  padding: 0 20px;
  font-family: -apple-system, sans-serif;
  line-height: 1.6;
  color: #333;
  background: #fff;
}

h1 {
  border-bottom: 3px solid #000;
  padding-bottom: 10px;
}

details {
  border: 1px solid #ddd;
  border-radius: 4px;
  padding: 10px;
  margin: 15px 0;
}

summary {
  font-weight: bold;
  cursor: pointer;
  padding: 10px;
  font-size: 1.2em;
}

summary:hover {
  background: #f5f5f5;
}

pre {
  background: #f5f5f5;
  padding: 15px;
  border-left: 3px solid #000;
  overflow-x: auto;
}

code {
  font-family: monospace;
  font-size: 0.9em;
}
</style>

# Pentesting Notes

<details>
<summary>Reconnaissance</summary>
```bash
nmap -sn 192.168.1.0/24
nmap -sV -sC -p- <target>
```

### DNS Enumeration
```bash
dig @<dns-server> <domain> ANY
dnsenum <domain>
```

</details>

<details>
<summary>Web Application Testing</summary>
```bash
# SQL Injection
sqlmap -u "http://target.com/page?id=1" --dbs
```

### XSS
```html
<script>alert(1)</script>
<img src=x onerror=alert(1)>
```
</details>

</div>

</div>

<script>
function searchContent() {
  const input = document.getElementById('searchBox');
  const filter = input.value.toLowerCase();
  const content = document.getElementById('content');
  const details = content.getElementsByTagName('details');
  
  for (let i = 0; i < details.length; i++) {
    const text = details[i].textContent || details[i].innerText;
    if (text.toLowerCase().indexOf(filter) > -1) {
      details[i].style.display = "";
      if (filter.length > 2) {
        details[i].setAttribute('open', '');
      }
    } else {
      details[i].style.display = "none";
    }
  }
}

document.addEventListener('DOMContentLoaded', function() {
  const codeBlocks = document.querySelectorAll('pre code');
  
  codeBlocks.forEach(function(block) {
    const button = document.createElement('button');
    button.className = 'copy-btn';
    button.textContent = 'Copy';
    
    button.addEventListener('click', function() {
      navigator.clipboard.writeText(block.textContent);
      button.textContent = 'Copied!';
      setTimeout(() => button.textContent = 'Copy', 2000);
    });
    
    block.parentNode.insertBefore(button, block);
  });
});
</script>