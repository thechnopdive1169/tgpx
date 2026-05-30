```html
<div class="filters">
    <input
        type="text"
        id="search"
        placeholder="Search proxy..."
    >

    <select id="category-filter">
        <option value="">All Categories</option>
        <option value="fast">Fast</option>
        <option value="stable">Stable</option>
        <option value="new">New</option>
    </select>

    <select id="location-filter">
        <option value="">All Locations</option>
        <option value="Iran">Iran</option>
        <option value="Germany">Germany</option>
        <option value="Turkey">Turkey</option>
        <option value="Russia">Russia</option>
        <option value="Unknown">Unknown</option>
    </select>
</div>
```

```css
.filters{
    display:flex;
    gap:10px;
    flex-wrap:wrap;
    margin-bottom:20px;
}

.filters input,
.filters select{
    background:#1f140f;
    color:#f5e6c8;
    border:1px solid #c59a52;
    border-radius:6px;
    padding:10px;
    font-family:"Cinzel", serif;
}
```

```js
const allProxies = [];

function renderProxies() {

    const search =
        document.getElementById("search")
        .value
        .toLowerCase();

    const category =
        document.getElementById("category-filter")
        .value;

    const location =
        document.getElementById("location-filter")
        .value;

    const container =
        document.getElementById("proxy-list");

    container.innerHTML = "";

    const filtered = allProxies.filter(p => {

        const matchesSearch =
            p.url.toLowerCase().includes(search);

        const matchesCategory =
            !category || p.category === category;

        const matchesLocation =
            !location || p.location === location;

        return (
            matchesSearch &&
            matchesCategory &&
            matchesLocation
        );
    });

    filtered.forEach((proxy, i) => {

        const link =
            document.createElement("a");

        link.href = proxy.url;
        link.className = "proxy";

        link.textContent =
            `${proxy.location} • ${i + 1}`;

        link.addEventListener("click", () => {
            link.classList.add("clicked");
        });

        container.appendChild(link);
    });

    if (!filtered.length) {
        container.innerHTML =
            '<div class="loading">No matching proxies.</div>';
    }
}
```

```js
proxies.forEach(proxy => {

    allProxies.push({
        url: proxy,

        // placeholder metadata
        category: "new",
        location: "Unknown"
    });
});

renderProxies();

document
.getElementById("search")
.addEventListener("input", renderProxies);

document
.getElementById("category-filter")
.addEventListener("change", renderProxies);

document
.getElementById("location-filter")
.addEventListener("change", renderProxies);
```

```html
<div class="filters">
    <input
        id="search"
        type="text"
        placeholder="Search country..."
    >

    <select id="location-filter">
        <option value="">All Countries</option>
    </select>
</div>
```

```css
.filters{
    display:flex;
    gap:10px;
    margin-bottom:20px;
    flex-wrap:wrap;
}

.filters input,
.filters select{
    background:#1f140f;
    color:#f5e6c8;
    border:1px solid #c59a52;
    border-radius:6px;
    padding:10px;
    font-family:"Cinzel", serif;
}

.filters input{
    flex:1;
    min-width:220px;
}
```

```html
<script>
const url =
"https://raw.githubusercontent.com/Argh94/Proxy-List/refs/heads/main/MTProto.txt";

const proxyList = [];

const container =
    document.getElementById("proxy-list");

const countryFilter =
    document.getElementById("location-filter");

const searchInput =
    document.getElementById("search");

function getServer(proxyUrl){

    try{
        const params =
            proxyUrl.split("?")[1];

        const search =
            new URLSearchParams(params);

        return search.get("server");
    }
    catch{
        return null;
    }
}

async function getCountry(ip){

    try{

        const response =
            await fetch(
                `https://ipwho.is/${ip}`
            );

        const data =
            await response.json();

        if(data.success){
            return data.country;
        }

        return "Unknown";
    }
    catch{
        return "Unknown";
    }
}

function render(){

    const country =
        countryFilter.value;

    const search =
        searchInput.value
        .trim()
        .toLowerCase();

    container.innerHTML = "";

    const filtered =
        proxyList.filter(proxy=>{

            const countryMatch =
                !country ||
                proxy.country === country;

            const searchMatch =
                !search ||
                proxy.country
                    .toLowerCase()
                    .includes(search);

            return countryMatch &&
                   searchMatch;
        });

    filtered.forEach((proxy,index)=>{

        const link =
            document.createElement("a");

        link.href =
            proxy.url;

        link.className =
            "proxy";

        link.textContent =
            `${proxy.country} • ${index+1}`;

        link.addEventListener("click",()=>{
            link.classList.add("clicked");
        });

        container.appendChild(link);
    });

    if(!filtered.length){

        container.innerHTML =
            '<div class="loading">No proxies found.</div>';
    }
}

async function loadProxies(){

    container.innerHTML =
        '<div class="loading">Loading proxies...</div>';

    try{

        const response =
            await fetch(url);

        const text =
            await response.text();

        const proxies =
            text
            .split(/\r?\n/)
            .map(x=>x.trim())
            .filter(x=>
                x.startsWith("tg://proxy")
            );

        const countries =
            new Set();

        container.innerHTML =
            '<div class="loading">Detecting locations...</div>';

        const limited =
            proxies.slice(0,150);

        for(const proxy of limited){

            const ip =
                getServer(proxy);

            let country =
                "Unknown";

            if(ip){

                country =
                    await getCountry(ip);
            }

            proxyList.push({
                url:proxy,
                country
            });

            countries.add(country);
        }

        [...countries]
            .sort()
            .forEach(country=>{

                const option =
                    document.createElement("option");

                option.value =
                    country;

                option.textContent =
                    country;

                countryFilter.appendChild(option);
            });

        render();
    }
    catch{

        container.innerHTML =
            '<div class="loading">Failed to load proxies.</div>';
    }
}

countryFilter
.addEventListener(
    "change",
    render
);

searchInput
.addEventListener(
    "input",
    render
);

loadProxies();
</script>
```
