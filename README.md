### **📌 README.md – RSS News Ticker**  

# **📰 RSS News Ticker**  

A **lightweight, real-time RSS ticker** that fetches **live news headlines** from RSS feeds and displays them in a **smooth-scrolling ticker** on any website or application.  

## **🚀 Use Case**  
This **RSS ticker** is ideal for **web developers, startups, and tech enthusiasts** who want to:  
✔️ Display **real-time news updates** from any RSS feed.  
✔️ Keep users engaged with **auto-updating headlines**.  
✔️ Ensure **smooth scrolling, customizable speed, and hover-to-pause** features.  
✔️ Integrate it into **various platforms** (HTML, JavaScript, React, PHP, etc.).  

---

## **✨ Features**  
✅ **Fetches latest news** from any RSS feed.  
✅ **Instantly displays headlines** on page load (no delay).  
✅ **Auto-refreshes every 5 minutes** to update with new articles.  
✅ **Starts scrolling from the extreme left** for immediate visibility.  
✅ **Smooth & adjustable scrolling speed (default: 80s)**.  
✅ **Pauses animation on hover** for better readability.  
✅ **Error handling** ensures the ticker never breaks.  
✅ **Minimal performance impact** for seamless integration.  

---

## **📥 Installation & Integration**  

### **1️⃣ Add the Script to Your Project**  
For **HTML / JavaScript-based projects**, paste the following **inside `<body>`**:  

```html
<script>
    function createTickerWidget() {
        const tickerContainer = document.createElement("div");
        tickerContainer.id = "rssTickerContainer";
        tickerContainer.style.whiteSpace = "nowrap";
        tickerContainer.style.overflow = "hidden";
        tickerContainer.style.background = "#fff478";
        tickerContainer.style.color = "black";
        tickerContainer.style.padding = "10px";
        tickerContainer.style.fontFamily = "Open Sans, sans-serif";
        tickerContainer.style.fontWeight = "100";
        tickerContainer.style.fontSize = "16px";

        const tickerContent = document.createElement("div");
        tickerContent.id = "rssTicker";
        tickerContent.style.display = "inline-block";
        tickerContent.style.animation = "scroll 80s linear infinite";
        tickerContent.innerHTML = "Fetching latest news...";
        tickerContent.style.fontWeight = "100";

        tickerContainer.appendChild(tickerContent);
        document.body.prepend(tickerContainer);

        fetchRSS();
        setInterval(fetchRSS, 300000); // Refresh every 5 minutes
    }

    async function fetchRSS() {
        try {
            const controller = new AbortController();
            const timeoutId = setTimeout(() => controller.abort(), 5000);

            // ✅ Encoded RSS API URL
            const rssApiUrl = "https://api.rss2json.com/v1/api.json?rss_url=https%3A%2F%2Fnews.google.com%2Frss%2Fsearch%3Fq%3Dhealth-technology%26hl%3Den-US%26gl%3DUS%26ceid%3DUS%3Aen%26count%3D20";
            
            const response = await fetch(rssApiUrl, { signal: controller.signal });

            clearTimeout(timeoutId);
            
            if (!response.ok) throw new Error("Network response was not ok");
            
            const data = await response.json();
            
            if (!data.items || data.items.length === 0) {
                throw new Error("No articles found in the feed.");
            }

            let headlines = data.items.map(item => 
                `<a href="${item.link}" style="color: black; text-decoration: none; font-weight: 100; font-size: 16px; margin-right: 20px;" target="_blank">${item.title}</a>`
            ).join(" • ");
            
            document.getElementById("rssTicker").innerHTML = `<span>${headlines}</span>`;
        } catch (error) {
            console.error("RSS Fetch Error:", error);
            document.getElementById("rssTicker").innerHTML = "Latest news unavailable. Please refresh.";
        }
    }

    window.addEventListener("DOMContentLoaded", createTickerWidget);
</script>
<style>
    @keyframes scroll {
        from { transform: translateX(0%); }  /* ✅ Starts at the extreme start */
        to { transform: translateX(-100%); }
    }
    #rssTickerContainer:hover #rssTicker {
        animation-play-state: paused !important;
    }
</style>
```

---

## **🛠️ Customization Guide**  

### **1️⃣ Change RSS Feed**  
By default, the ticker fetches **Health Technology news** from Google News.  
To change it, **modify the RSS URL** inside `fetchRSS()`:

```javascript
const rssApiUrl = "https://api.rss2json.com/v1/api.json?rss_url=YOUR_RSS_FEED_URL_HERE";
```

👉 **Replace `"YOUR_RSS_FEED_URL_HERE"`** with your preferred RSS feed.  

---

### **2️⃣ Adjust Scrolling Speed**  
- The **default scrolling speed is 80s** (slower for readability).  
- To make it **faster**, change the `80s` value in:  

```css
@keyframes scroll {
    from { transform: translateX(0%); }
    to { transform: translateX(-100%); }
}
```

👉 **Example:**  
- `50s` = Faster  
- `100s` = Slower  

---

## **🔄 Supported Platforms**  
This ticker is **platform-agnostic** and can be used in:  
✔️ **HTML / JavaScript Websites**  
✔️ **WordPress (via Custom JavaScript Widget)**  
✔️ **PHP Websites (via Embedded JavaScript)**  
✔️ **.Py Applications**  

---

## **🛠️ Troubleshooting**  

| Issue | Solution |
|----------------|-------------------------------------------------|
| Ticker not appearing | Ensure script is inside `<body>`. |
| News not loading | Wait 5 seconds; check console errors in Developer Tools (F12 → Console). |
| Scrolling too fast | Increase animation duration (e.g., `100s`). |
| Error: "Latest news unavailable" | RSS feed might be down. Try later. |

---

## **📜 License**  
This project is **open-source** and can be modified freely. Attribution is appreciated but not required.  

---

## **🎯 Final Notes**  
✔️ This **RSS ticker is lightweight, fast, and optimized** for various platforms.  
✔️ Works with **any RSS feed** (just modify the feed URL).  
✔️ **Fetches news instantly and updates every 5 minutes** without reloading the page.  

🚀 **Now your website or app will always have fresh, real-time headlines!** 🚀  

Let me know if you need **further improvements or customizations!** 😊  

---

Would you like me to add these features? 😊
