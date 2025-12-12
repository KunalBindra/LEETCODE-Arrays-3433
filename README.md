# LEETCODE-Arrays-3433
---

# ✅ **Given Input**

```
numberOfUsers = 2
events = [
    ["MESSAGE","10","id1 id0"],
    ["OFFLINE","11","0"],
    ["MESSAGE","71","HERE"]
]
```

# 📝 **Before Loop: Sorting Step**

Your sort comparator:

* Primary key → timestamp (ascending)
* If timestamps equal:

  * Compare the **second character** of event type
    (`'E'` for MESSAGE, `'F'` for OFFLINE; 'F' > 'E' so OFFLINE would come first if same time)

All timestamps are different, so sorting remains as:

1. ["MESSAGE","10","id1 id0"]
2. ["OFFLINE","11","0"]
3. ["MESSAGE","71","HERE"]

---

# 💾 **Initialize Arrays**

```
mentionCount = [0, 0]
offlineTime = [0, 0]
```

---

# 🚀 **Process Each Event**

---

## **1️⃣ Event: MESSAGE @10 → "id1 id0"**

Call `applyMessageEvent()`:

* timestamp = 10
* ids = ["id1", "id0"]

Loop:

### 👉 id1:

* userId = 1
* mentionCount → `[0, 1]`

### 👉 id0:

* userId = 0
* mentionCount → `[1, 1]`

📌 **Status After Event 1**

```
mentionCount = [1, 1]
offlineTime = [0, 0]
```

---

## **2️⃣ Event: OFFLINE @11 for user 0**

```
offlineTime[0] = 11
```

📌 **Status After Event 2**

```
mentionCount = [1, 1]
offlineTime = [11, 0]
```

---

## **3️⃣ Event: MESSAGE @71 → "HERE"**

Call `applyMessageEvent()`:

* timestamp = 71
* ids = ["HERE"]

This triggers:

```
if(offlineTime[i] == 0 OR offlineTime[i] + 60 <= timestamp)
```

Let’s check per user:

### 👤 User 0

* offlineTime[0] = 11
* 11 + 60 = 71
* Condition: `71 <= 71` → **true**

So user 0 gets a mention.

### 👤 User 1

* offlineTime[1] = 0 → still online (counts as “HERE”)
* Condition passes immediately.

So both users get +1.

📌 **Final After Event 3**

```
mentionCount = [2, 2]
offlineTime = [11, 0]
```

---

# 🎯 **FINAL OUTPUT**

```
[2, 2]
```

Both users end with **2 mentions each**.
