# 🧩 JSON Modding Guide  
**Official Modding API v1**

Welcome to the JSON Modding system.

This document contains **everything in one place** that you need to create safe and compatible JSON mods for this bot.  
You can copy this file **as-is** and save it as:

JSON_MODDING_GUIDE.md

---

## 📌 Core Principles

This modding system is intentionally limited for safety and stability.

### ✅ Allowed
- JSON files only
- Custom commands
- Text responses
- Randomized messages
- Emoji reactions
- Message chains
- Roleplay and fun content

### ❌ Not Allowed
- Any programming code (Python, JS, etc.)
- Access to economy, XP, items, or database
- Persistent storage
- Conditions, loops, or logic
- Ads, links, mentions
- NSFW / 18+ content
- Unknown placeholders

If a mod violates these rules, it will **not be loaded**.

---

## 🧠 What Mods Can Do

Mods allow you to:
- Add new commands
- Create fun or roleplay interactions
- Simulate mini-games using text
- Use randomness for variety
- Add emoji reactions
- Create atmospheric sequences

Mods cannot:
- Save progress
- Modify user stats
- Interact with bot systems
- Execute logic or scripts

---

## 🗂 Mod File Structure

Every mod must follow this structure:

```json
{
  "meta": { ... },
  "limits": { ... },
  "commands": [ ... ]
}
```

## meta — Mod Information (Required)

```json
"meta": {
  "name": "my_mod",
  "version": "1.0.0",
  "author": "your_github_username",
  "description": "Short description of the mod",
  "min_bot_version": "1.0"
}
```

## meta fields

| Field           | Description                         |
| --------------- | ----------------------------------- |
| name            | Unique mod name (`a-z`, `0-9`, `_`) |
| version         | Mod version                         |
| author          | Author name                         |
| description     | Short description                   |
| min_bot_version | Minimum supported bot version       |


## limits — Optional Limits
```json
"limits": {
  "cooldown_default": 30
}
```

##commands — Command List

Rules:
1. Maximum 5 commands per mod
2. Command names must be unique
3. Do NOT include / in command names
4. Must not conflict with system commands

Command Structure
```json
{
  "name": "hello",
  "description": "Say hello",
  "cooldown": 10,
  "response": { ... }
}
```

##⏱ Cooldowns
```json
"cooldown": 10
```

Optional
Minimum: 5 seconds
If omitted, `cooldown_default` is used

## ⚙️ Response Types
1. Text Response
```json
"response": {
  "type": "text",
  "text": "Hello, {user}!"
}
```

2. Random Response
```json
"response": {
  "type": "random",
  "variants": [
    "{user} rolled 🎲 {random:1-6}",
    "Result: {random:1-6}"
  ]
}
```

3. Reaction Response
```json
"response": {
  "type": "reaction",
  "emoji": "🔥"
}
```

4. Reply Chain Response
```json
"response": {
  "type": "reply_chain",
  "messages": [
    "Processing...",
    "Almost done...",
    "Done ✅"
  ]
}
```
Rules:
1. Maximum 3 messages
2. Fixed delay
3. No loops

## 🧩 Supported Placeholders `{}`
| Placeholder    | Description                     |
| -------------- | ------------------------------- |
| `{user}`       | User display name               |
| `{user_id}`    | Telegram user ID                |
| `{chat_id}`    | Chat ID                         |
| `{args}`       | Arguments after the command     |
| `{random:X-Y}` | Random number (1 ≤ X < Y ≤ 100) |

Examples
`"{user} rolled {random:1-6}"`
`"Arguments: {args}"`

## 🚫 Forbidden Placeholders

These placeholders do NOT exist and will reject the mod:
{coins}
{money}
{xp}
{exp}
{level}
{inventory}
{items}
{vip}
{admin}
{db}
{time}
{date}

## 🚫 Forbidden Content

Mods will be rejected if they contain:
Links (http, https, t.me)
Mentions (@username)
Advertising
NSFW / 18+ content
Hate speech or insults
Fake system messages
Unknown placeholders

## 🧱 Modder Template (Copy & Use)
```json
{
  "meta": {
    "name": "my_first_mod",
    "version": "1.0.0",
    "author": "your_name",
    "description": "Describe what your mod does",
    "min_bot_version": "1.0"
  },
  "limits": {
    "cooldown_default": 30
  },
  "commands": [
    {
      "name": "hello",
      "description": "Say hello",
      "cooldown": 10,
      "response": {
        "type": "text",
        "text": "Hello, {user} 👋"
      }
    }
  ]
}
```

## 📚 Example Mods
### 🎲 Fun / Entertainment
