---
layout: default
---

<style>
body {
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  min-height: 100vh;
  font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, "Helvetica Neue", sans-serif;
}

.container {
  max-width: 1000px;
  margin: 0 auto;
  padding: 40px 20px;
  background: rgba(255, 255, 255, 0.95);
  border-radius: 20px;
  box-shadow: 0 20px 60px rgba(0, 0, 0, 0.3);
  backdrop-filter: blur(10px);
}

h1 {
  text-align: center;
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  font-size: 2.5em;
  margin-bottom: 10px;
  font-weight: 800;
}

.disclaimer {
  background: linear-gradient(135deg, #ffeaa7 0%, #fdcb6e 100%);
  border-left: 4px solid #e17055;
  padding: 15px 20px;
  margin: 20px 0;
  border-radius: 10px;
  color: #2d3436;
  box-shadow: 0 4px 15px rgba(0, 0, 0, 0.1);
}

details {
  background: white;
  border: 2px solid #e1e8ed;
  border-radius: 12px;
  margin: 20px 0;
  padding: 15px;
  box-shadow: 0 4px 15px rgba(0, 0, 0, 0.08);
  transition: all 0.3s ease;
}

details:hover {
  box-shadow: 0 8px 25px rgba(102, 126, 234, 0.15);
  border-color: #667eea;
}

summary {
  cursor: pointer;
  font-size: 1.4em;
  font-weight: 700;
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  padding: 15px;
  border-radius: 8px;
  list-style: none;
  user-select: none;
  transition: all 0.2s ease;
}

summary::-webkit-details-marker {
  display: none;
}

summary:before {
  content: "▶ ";
  display: inline-block;
  transition: transform 0.3s ease;
  margin-right: 10px;
  color: #667eea;
}

details[open] summary:before {
  transform: rotate(90deg);
}

summary:hover {
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  -webkit-background-clip: text;
  transform: translateX(5px);
}

details h3 {
  color: #2d3436;
  margin-top: 25px;
  padding-bottom: 10px;
  border-bottom: 2px solid #dfe6e9;
  font-size: 1.3em;
}

details h4 {
  color: #636e72;
  margin-top: 20px;
  font-size: 1.1em;
}

pre {
  background: linear-gradient(135deg, #f8f9fa 0%, #e9ecef 100%);
  border: 2px solid #dee2e6;
  border-radius: 10px;
  padding: 20px;
  overflow-x: auto;
  position: relative;
  box-shadow: inset 0 2px 10px rgba(0, 0, 0, 0.05);
}

code {
  font-family: 'Monaco', 'Menlo', 'Courier New', monospace;
  font-size: 0.9em;
  color: #e83e8c;
  background: #f8f9fa;
  padding: 2px 6px;
  border-radius: 4px;
}

pre code {
  color: #2d3436;
  background: transparent;
  padding: 0;
}

.copy-btn {
  position: absolute;
  top: 10px;
  right: 10px;
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  color: white;
  border: none;
  padding: 8px 15px;
  border-radius: 8px;
  cursor: pointer;
  font-size: 0.85em;
  font-weight: 600;
  box-shadow: 0 4px 10px rgba(102, 126, 234, 0.3);
  transition: all 0.2s ease;
}

.copy-btn:hover {
  transform: translateY(-2px);
  box-shadow: 0 6px 15px rgba(102, 126, 234, 0.4);
}

.copy-btn:active {
  transform: translateY(0);
}

.search-box {
  width: 100%;
  padding: 15px 20px;
  margin: 25px 0;
  background: white;
  border: 2px solid #e1e8ed;
  border-radius: 50px;
  color: #2d3436;
  font-size: 16px;
  box-shadow: 0 4px 15px rgba(0, 0, 0, 0.08);
  transition: all 0.3s ease;
}

.search-box:focus {
  outline: none;
  border-color: #667eea;
  box-shadow: 0 6px 20px rgba(102, 126, 234, 0.2);
}

.top-nav {
  background: white;
  padding: 20px;
  border-radius: 15px;
  margin: 25px 0;
  display: flex;
  flex-wrap: wrap;
  gap: 12px;
  justify-content: center;
  box-shadow: 0 4px 15px rgba(0, 0, 0, 0.08);
}

.top-nav a {
  padding: 10px 20px;
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  border-radius: 25px;
  color: white;
  font-weight: 600;
  text-decoration: none;
  transition: all 0.3s ease;
  box-shadow: 0 4px 10px rgba(102, 126, 234, 0.3);
}

.top-nav a:hover {
  transform: translateY(-3px);
  box-shadow: 0 6px 20px rgba(102, 126, 234, 0.4);
}

a {
  color: #667eea;
  text-decoration: none;
  font-weight: 500;
  transition: color 0.2s ease;
}

a:hover {
  color: #764ba2;
}

/* Scrollbar */
::-webkit-scrollbar {
  width: 10px;
}

::-webkit-scrollbar-track {
  background: #f1f3f5;
  border-radius: 10px;
}

::-webkit-scrollbar-thumb {
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  border-radius: 10px;
}

::-webkit-scrollbar-thumb:hover {
  background: linear-gradient(135deg, #764ba2 0%, #667eea 100%);
}

/* Mobile responsive */
@media (max-width: 768px) {
  .container {
    padding: 20px 15px;
    border-radius: 15px;
  }
  
  h1 {
    font-size: 2em;
  }
  
  summary {
    font-size: 1.2em;
  }
  
  .top-nav {
    flex-direction: column;
  }
  
  .top-nav a {
    width: 100%;
    text-align: center;
  }
}
</style>

<div class="container">

# 🔐 Pentesting & Red Team Reference

<div class="disclaimer">
⚠️ <strong>LEGAL DISCLAIMER</strong>: For educational purposes and authorized testing only. Unauthorized access is illegal.
</div>

<input type="text" class="search-box" id="searchBox" placeholder="🔍 Search commands, techniques, tools..." onkeyup="searchContent()">

<div class="top-nav">
<a href="#recon">🎯 Reconnaissance</a>
<a href="#web">🌐 Web Apps</a>
<a href="#network">🔌 Network</a>
<a href="#privesc">⬆️ Privilege Escalation</a>
</div>

<div id="content">

<details id="recon">
<summary>Reconnaissance & Information Gathering</summary>

### Network Discovery
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

<details id="web">
<summary>Web Application Testing</summary>

### SQL Injection
```bash
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