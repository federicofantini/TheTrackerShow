# Bruteforce Caesar Cipher

```python

ciphertext = "xlcdslw-ksfvzg.nzx"

for shift in range(1, 26):
    result = ""
    for c in ciphertext:
        if c.isalpha():
            base = ord('A') if c.isupper() else ord('a')
            result += chr((ord(c) - base + shift) % 26 + base)
        else:
            result += c
    if "marshal-zhukov.com" in result:
        print(f"ROT-{shift}: {result}")
        break
```

```

ROT-15: marshal-zhukov.com
```