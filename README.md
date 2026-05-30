# Telegram Proxy Saloon

# https://thechnopdive1169.github.io/tgpx/

A stylish **Red Dead Redemption 2-inspired Telegram MTProto proxy browser** that automatically fetches proxy links from a remote text file and displays them as clickable buttons.

Users can simply open the page, choose a proxy, and connect directly through Telegram using the `tg://proxy` protocol.

---

## Features

* 🤠 Red Dead Redemption 2 inspired UI
* 🔄 Automatically loads proxies from a remote source
* ⚡ No backend required
* 📱 Responsive design
* 🎯 One-click Telegram connection
* 📦 Pure HTML, CSS, and JavaScript
* 🌐 Can be hosted on GitHub Pages
* 🔢 Displays proxies as compact buttons in a grid layout

---

## Screenshot

The interface resembles an Old West saloon notice board with:

* Dark leather colors
* Gold accents
* Vintage typography
* Compact proxy buttons
* Responsive grid layout

---

## How It Works

The application fetches a text file containing MTProto proxy links.

Example source:

```text
tg://proxy?server=94.177.163.94&port=443&secret=eeNEgYdJvXrFGRMCIMJdCQ==
tg://proxy?server=85.133.194.34&port=8443&secret=eeNEgYdJvXrFGRMCIMJdCQ
tg://proxy?server=server-mania.ultrasam.info&port=443&secret=ee160301020001...
```

The script:

1. Downloads the file.
2. Splits it into lines.
3. Filters valid `tg://proxy` links.
4. Generates clickable buttons.
5. Opens Telegram when a button is clicked.

---

## Project Structure

```text
.
├── index.html
├── README.md
└── assets/
    └── screenshots/
```

---

## Installation

### Clone Repository

```bash
git clone https://github.com/yourusername/telegram-proxy-saloon.git
```

```bash
cd telegram-proxy-saloon
```

### Open Locally

Simply open:

```text
index.html
```

in your browser.

---

## Configuration

Locate:

```javascript
const url =
"https://raw.githubusercontent.com/Argh94/Proxy-List/refs/heads/main/MTProto.txt";
```

Replace it with your own proxy source:

```javascript
const url =
"https://example.com/proxies.txt";
```

---

## Proxy File Format

The application expects one proxy per line.

Example:

```text
tg://proxy?server=1.1.1.1&port=443&secret=abc
tg://proxy?server=2.2.2.2&port=443&secret=xyz
tg://proxy?server=mydomain.com&port=443&secret=123
```

Empty lines are ignored.

---

## Grid Layout

Default:

```css
grid-template-columns: repeat(6, 1fr);
```

Example:

```text
Proxy 1   Proxy 2   Proxy 3   Proxy 4   Proxy 5   Proxy 6
Proxy 7   Proxy 8   Proxy 9   Proxy10   Proxy11   Proxy12
```

Change the number of columns:

```css
grid-template-columns: repeat(4, 1fr);
```

---

## Deploying to GitHub Pages

### Create Repository

```bash
git init
git add .
git commit -m "Initial commit"
git branch -M main
git remote add origin https://github.com/USERNAME/REPO.git
git push -u origin main
```

### Enable Pages

1. Open repository settings.
2. Navigate to **Pages**.
3. Select:

```text
Deploy from branch
```

4. Choose:

```text
main / root
```

5. Save.

Your site will be available at:

```text
https://USERNAME.github.io/REPO/
```

---

## Telegram Protocol Support

The page uses Telegram's custom URL scheme:

```text
tg://proxy
```

When clicked:

* Telegram Desktop opens automatically.
* Telegram Android opens automatically.
* Telegram iOS opens automatically.

If Telegram is not installed, the browser will not know how to handle the link.

---

## Browser Compatibility

| Browser | Supported |
| ------- | --------- |
| Chrome  | ✅         |
| Edge    | ✅         |
| Firefox | ✅         |
| Safari  | ✅         |
| Brave   | ✅         |

---

## Customization

### Change Title

```html
<h1>Telegram Proxy Saloon</h1>
```

### Change Theme Color

```css
--gold:#c59a52;
```

### Change Background

```css
background:
linear-gradient(to bottom,#1a120d,#0d0907);
```

### Change Button Style

```css
.proxy {
    border-radius:6px;
}
```

---

## Performance

Typical performance:

| Proxy Count | Load Time          |
| ----------- | ------------------ |
| 100         | < 100ms            |
| 500         | < 300ms            |
| 1000        | < 1s               |
| 5000        | Depends on browser |

---

## Security Notes

* No user data is collected.
* No cookies are used.
* No analytics are included.
* No server-side processing is required.
* All proxy data is fetched directly from the configured source.

---

## Troubleshooting

### Proxies Not Loading

Possible causes:

* Invalid source URL
* CORS restrictions
* Network connectivity issues
* Source repository unavailable

### Telegram Does Not Open

Verify:

* Telegram is installed.
* The browser allows custom protocol handlers.
* The proxy link format is valid.

---

## Future Ideas

* Search proxies
* Sort proxies
* Copy proxy link button
* Dark/Light mode switch
* Proxy statistics
* Country flags
* Latency testing
* Favorites system
* Offline cache
* Automatic refresh

---

## License

MIT License

---

## Credits

Inspired by:

* Red Dead Redemption 2 UI design
* Telegram MTProto Proxy protocol
* Open-source proxy list maintainers

Happy trail riding, partner. 🤠
