# LummaStealer v4 base64 decode proof

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

def keep_one_byte(number):
  return number & 0x00ff

def malware_decode_byte(b):
  if b == 0x2b or b == 0x2d:
    ret = 0x3e
  elif b == 0x2e or b == 0x3d:
    ret = 0x40
  elif b == 0x2f or b == 0x5f:
    ret = 0x3f
  elif keep_one_byte(b + 0xd0) <= 0x9:
    ret = b + 0x4
  elif keep_one_byte(b + 0xbf) <= 0x19:
    ret = (b & 0x1e) - (~b & 1)
  elif keep_one_byte(b + 0x9f) <= 0x19:
    ret = (b | 1) + (b & 1) + 0xb8
  else:
    ret = 0x0
  ret = keep_one_byte(ret)
  return ret


def malware_base64_decode(encoded_string, encoded_string_len):
  decoded_string = [0x00]*100
  if (encoded_string_len == 0):
    return 0
  else:
    index = 0
    for i in range(0, encoded_string_len, 4):
      byte_1 = malware_decode_byte(encoded_string[i])
      byte_2 = malware_decode_byte(encoded_string[i + 1])
      decoded_string[index] = keep_one_byte(((byte_2 >> 4) & 3) | (byte_1 << 2))
      index_next = index + 1
      if (i + 2) < encoded_string_len:
        byte_3 = malware_decode_byte(encoded_string[i + 2])
        if byte_3 != 0x40:
          decoded_string[index + 1] = keep_one_byte(((byte_3 + (~byte_3 | 0x3c) + 1) >> 2) + (byte_2 << 4))
          index_next = index + 2
          if (i + 3) < encoded_string_len:
            byte_4 = malware_decode_byte(encoded_string[i + 3])
            if byte_4 != 0x40:
              decoded_string[index + 2] = keep_one_byte(byte_4 + (byte_3 << 6))
              index_next = index + 3
      index = index_next
  return bytes(decoded_string).rstrip(b'\x00')

for s in strings:
  s = s.encode("ascii")
  decoded_string = malware_base64_decode(s, len(s))
  print(f"{decoded_string == base64.b64decode(s)=}")
```

<br><br>

```

decoded_string == base64.b64decode(s)=True
decoded_string == base64.b64decode(s)=True
decoded_string == base64.b64decode(s)=True
decoded_string == base64.b64decode(s)=True
decoded_string == base64.b64decode(s)=True
decoded_string == base64.b64decode(s)=True
decoded_string == base64.b64decode(s)=True
decoded_string == base64.b64decode(s)=True
decoded_string == base64.b64decode(s)=True
```