
# GridPlus

A lightweight Node.js wrapper for interacting with the **GridPlus AI Image Editing API** (unofficial).  
This class allows you to upload images and apply AI-powered edits using the `wn_aistyle_nano` method via the GridPlus web API.

> **Note**: This is an **unofficial** client. Use responsibly and in compliance with GridPlus's terms of service.

---

## Features

- Generate random device identifiers (`X-UniqueID`, `X-GhostID`, `X-DeviceID`)
- Automatic MIME type detection from buffer
- Secure image upload with signed pre-upload URL
- Polling-based task result retrieval with timeout
- Simple `.edit(buffer, prompt)` method for AI image styling

---

## Installation

```bash
npm install axios form-data file-type node:crypto
```

> All dependencies are lightweight and widely used.

---

## Usage

### How to use 

```js
const fs = require("fs")

const gp = new GridPlus()

const img = fs.readFileSync("./your-path-image.jpg")
const prompt = "Create a 1/7 scale commercialized figurine of the characters in the picture, in a realistic style, in a real environment. The figurine is placed on a computer desk. The figurine has a round transparent acrylic base, with no text on the base. The content on the computer screen is the brush modeling process of this figurine. Next to the computer screen is a BANDAl-style toy packaging box printed with the original artwork., The packaging features two-dimensional flat illustrations. Please turn this photo into afigure. Behind it, there should be a Model packaging box with the character from this photo printed on it. In front of thebox.on a round plastic baseplace the fiqure version of thephoto I gave you. I’d like the PVC material to be clearlyrepresented. It would be even better if the background is indoors"

const res = await gp.edit(img, prompt)

console.log(res)

```

---

## API Methods

### `new GridPlus()`
Creates a new instance with auto-generated device headers.

### `.edit(buffer, prompt)`
- `buffer`: `Buffer` — Image data
- `prompt`: `string` — Text description for AI transformation
- Returns: `Promise<string>` — URL of the processed image

---

## Configuration

| Header | Description |
|-------|-----------|
| `X-AppID` | Fixed to `808645` |
| `X-Platform` | `h5` (web mobile) |
| `X-Version` | `8.9.7` |
| `X-SessionToken` | Left empty (no login) |
| `X-UniqueID`, `X-GhostID`, `X-DeviceID` | Auto-generated UUIDs |
| `sig` | Custom signature using UID |

> These values mimic a legitimate mobile browser session.

---

## Error Handling

The `.edit()` method throws descriptive errors:
- Invalid buffer
- Upload failure
- Missing `task_id`
- Task timeout (60s)
- API error messages

---

## Disclaimer

This tool interacts with GridPlus's internal APIs without authentication.  
It may stop working if:
- Endpoints change
- Rate limits are enforced
- Client signatures are validated server-side

Use at your own risk.

---

## Portfolio

Created by **akhfhid**  
[https://akhfhid.my.id](https://akhfhid.my.id)

---
