---
layout: default
---

<style>
details {
  background: #161b22;
  border: 1px solid #30363d;
  border-radius: 6px;
  margin: 15px 0;
  padding: 10px;
}

summary {
  cursor: pointer;
  font-size: 1.3em;
  font-weight: bold;
  color: #58a6ff;
  padding: 10px;
}

summary:before {
  content: "▶ ";
}

details[open] summary:before {
  transform: rotate(90deg);
  content: "▼ ";
}

pre {
  background: #0d1117;
  border: 1px solid #30363d;
  padding: 16px;
}
</style>

# My Pentesting Notes

<details>
<summary>Section Name Here</summary>

### Subsection
```bash
command here
```

More content...

</details>

<details>
<summary>Another Section</summary>

Your content...

</details>
