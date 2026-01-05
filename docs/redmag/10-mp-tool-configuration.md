<p align="center">
  <img src="../../assets/logo.jpg" alt="openMAG logo" />
</p>

## MP Tool Configuration

Once the SSD is detected:

1. Open **Config**
2. Enter the configuration password  
   - For many SMI tools, this is **two spaces**
3. Editable fields will unlock

### Required Configuration Changes

#### Device Name / Model Number
- Must exactly match a **RED-whitelisted model**
- Case, spacing, and formatting must be perfect

### Whitelist Reference

Complete list of supported model names from DSMC firmware. **Copy these EXACTLY - spacing and capitalization matter!**
#### Smallest Capacities

```
RED 16GB REV B
RED 32GB REV A1
RED 64GB REV A1
RED 55GB V1
RED 55GB V2
```

#### 64GB Models (Note: TWO spaces before "64")

```
RED  64GB Rev T1
RED  64GB Rev T2
RED  64GB Rev T3
```

#### 128GB Models

```
RED 128GB Rev T1
RED 128GB Rev T2
RED 128GB Rev T3
```

#### 256GB Models (Recommended)

```
RED 256GB Rev T1
RED 256GB Rev T2
RED 256GB Rev T3
```

#### 512GB Models (Maximum Capacity)

```
RED 512GB V1
RED 512GB V2
RED 512GB V3
RED 512GB V4
```

### SSDs (SSD Designation)

**Note: These have "SSD" suffix and different spacing**

```
RED 55GB SSD 
RED 64GB SSD 
RED 128GB SSD 
RED 256GB SSD 
RED 512GB SSD 
```

**Note:** Some have trailing space after "SSD" - include it!

### CompactFlash Cards

```
RED 16GB CF
RED 32GB CF
RED 64GB CF
LEXAR ATA FLASH CARD
```

**Note:** CF cards are obsolete format, not recommended for new projects

### Recommended Models for DIY

**Best choices for generic SSD conversion:**

**For 256GB drive:**
```
RED 256GB Rev T3    ← Newest revision (recommended)
RED 256GB Rev T2
RED 256GB Rev T1
RED 256GB SSD       ← SSD variant (not tested yet)
```

**For 512GB drive (maximum):**
```
RED 512GB V4        ← Newest revision (recommended)
RED 512GB V3
RED 512GB V2
RED 512GB V1
RED 512GB SSD       ← SSD variant (not tested yet)
```

**For 128GB drive:**
```
RED 128GB Rev T3    ← Newest revision (recommended)
RED 128GB Rev T2
RED 128GB Rev T1
RED 128GB SSD       ← SSD variant (not tested yet)
```

### Spacing Reference

**CRITICAL:** Some models have unusual spacing!

**64GB models (TWO spaces):**
```
RED  64GB Rev T1
RED  64GB Rev T2
RED  64GB Rev T3
   ↑↑ TWO spaces between RED and 64
```

**All other capacities (ONE space):**
```
RED 128GB Rev T1
RED 256GB Rev T1
RED 512GB V1
   ↑ ONE space between RED and capacity
```

**To verify your spacing:**
```
Wrong: RED 64GB Rev T1   (one space - will fail!)
Right: RED  64GB Rev T1  (two spaces - will work!)
```

#### Capacity
- Must match the selected RED model exactly. Example, if you are using `RED 512GB V4` your capacity MUST be 512GB.
- In the Capacity section:
  - Select `IDEMA`
  - Choose the exact capacity from the dropdown

---

⬅️ Prev: [Running the MP Tool](09-running-mp-tool.md)  
➡️ Next: [Flashing the SSD](11-flashing.md)
