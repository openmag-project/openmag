<p align="center">
  <img src="../../assets/logo.jpg" alt="openMAG logo" />
</p>

# Whitelist Overview

## Whitelisted REDMAG model numbers

These model numbers were extracted from DSMC firmware and verified through testing.

**IMPORTANT:** Copy these **exactly**. Spacing, capitalization, and even trailing spaces can matter.

---

## Smallest capacities

```
RED 16GB REV B
RED 32GB REV A1
RED 64GB REV A1
RED 55GB V1
RED 55GB V2
```

---

## 64GB models (TWO spaces before “64”)

```
RED  64GB Rev T1
RED  64GB Rev T2
RED  64GB Rev T3
```

---

## 128GB models

```
RED 128GB Rev T1
RED 128GB Rev T2
RED 128GB Rev T3
```

---

## 256GB models (recommended)

```
RED 256GB Rev T1
RED 256GB Rev T2
RED 256GB Rev T3
```

---

## 512GB models (maximum)

```
RED 512GB V1
RED 512GB V2
RED 512GB V3
RED 512GB V4
```

---

## “SSD” designation models

**Note:** These include an `SSD` suffix and may include a trailing space after `SSD`.

```
RED 55GB SSD 
RED 64GB SSD 
RED 128GB SSD 
RED 256GB SSD 
RED 512GB SSD 
```

---

## CompactFlash (legacy)

```
RED 16GB CF
RED 32GB CF
RED 64GB CF
LEXAR ATA FLASH CARD
```

---

## Recommended models for DIY conversions

These are the most practical targets based on common capacities and “newest” revisions:

### 256GB
```
RED 256GB Rev T3    ← Newest revision (recommended)
RED 256GB Rev T2
RED 256GB Rev T1
RED 256GB SSD       ← SSD variant (not tested yet)
```

### 512GB
```
RED 512GB V4        ← Newest revision (recommended)
RED 512GB V3
RED 512GB V2
RED 512GB V1
RED 512GB SSD       ← SSD variant (not tested yet)
```

### 128GB
```
RED 128GB Rev T3    ← Newest revision (recommended)
RED 128GB Rev T2
RED 128GB Rev T1
RED 128GB SSD       ← SSD variant (not tested yet)
```

---

## Spacing reference (critical)

**64GB models use TWO spaces between `RED` and `64`:**
```
RED  64GB Rev T1
RED  64GB Rev T2
RED  64GB Rev T3
   ↑↑ TWO spaces between RED and 64
```

**All other capacities use ONE space:**
```
RED 128GB Rev T1
RED 256GB Rev T1
RED 512GB V1
   ↑ ONE space between RED and capacity
```

**Verify your spacing:**
```
Wrong: RED 64GB Rev T1   (one space - will fail!)
Right: RED  64GB Rev T1  (two spaces - will work!)
```
---

⬅️ Prev: [REDMAG Validations Overview](redmag-validations-overview.md)  
➡️ Next: [Capacity Overview](capacity-overview.md)

