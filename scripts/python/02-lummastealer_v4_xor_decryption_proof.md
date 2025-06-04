# LummaStealer v4 xor decryption proof

```python

import base64

strings = [
  '4IrgDqe83BYkMRyaj6QCn2LHAVw1MDme0RvFNf4BP7yQ+IFpxsy1eApCfuk=', 
  '4IrgDqe83BYkMRyaj6QCn2LHAVw1MDme0RvFNf4BP7yS75Bh1Mi5dExEMunt1w==', 
  '4IrgDqe83BYkMRyaj6QCn2LHAVw1MDme0RvFNf4BP7yU4olgzMWleU9UdrT8xnE=', 
  '4IrgDqe83BYkMRyaj6QCn2LHAVw1MDme0RvFNf4BP7yE/4Nl1M61eENbd7T8xnE=', 
  '4IrgDqe83BYkMRyaj6QCn2LHAVw1MDme0RvFNf4BP7yF8pBixtWyYEFUb7T8xnE=', 
  '4IrgDqe83BYkMRyaj6QCn2LHAVw1MDme0RvFNf4BP7yC+I95ydW5b1FLMunt1w==', 
  '4IrgDqe83BYkMRyaj6QCn2LHAVw1MDme0RvFNf4BP7yS5ZR6ztmpcgpCfuk=', 
  '4IrgDqe83BYkMRyaj6QCn2LHAVw1MDme0RvFNf4BP7yS74xvy9WycU4fb/j8', 
  '4IrgDqe83BYkMRyaj6QCn2LHAVw1MDme0RvFNf4BP7yU641rw9u5c1dIMunt1w=='
]

for s in strings:
  s = s.encode("ascii")
  s = base64.b64decode(s)
  key = s[:32]
  encrypted_string = s[32:]
  # 32 bytes of key + encrypted bytes

  malware_decrypted_string = ['\x00'] * len(encrypted_string)
  simplified_decrypted_string = ['\x00'] * len(encrypted_string)
  for i in range(len(encrypted_string)):
    malware_decrypted_string[i] = encrypted_string[i] - (((key[i] & (encrypted_string[i] ^ key[i] ^ 0xff)) << 1) - key[i])
    simplified_decrypted_string[i] = encrypted_string[i] ^ key[i]
  assert malware_decrypted_string == simplified_decrypted_string
  print(bytes(simplified_decrypted_string))

# verification of the simplification -> exhaust all the input space
print()
is_xor = True
for key in range(255):
  for enc in range(255):
    if (key ^ enc) != (enc - (((key & (enc ^ key ^ 0xff)) << 1) - key)):
      is_xor = False
print(f"{is_xor=}")
```

<br><br>

```

b'pragapin.sbs'
b'repostebhu.sbs'
b'thinkyyokej.sbs'
b'ducksringjk.sbs'
b'explainvees.sbs'
b'brownieyuz.sbs'
b'rottieud.sbs'
b'relalingj.sbs'
b'tamedgeesy.sbs'

is_xor=True
```