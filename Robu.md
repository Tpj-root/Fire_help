



How to use:

Open your cart page in Firefox.

Press F12 → open Console tab.

Paste this script and press Enter.

Copy the CSV output from the console.



```
https://robu.in/cart/
```




```

(() => {
  const rows = document.querySelectorAll('tr.woocommerce-cart-form__cart-item');
  const data = [["Name", "URL", "Price", "Qty", "Subtotal"]];
  
  rows.forEach(row => {
    const nameEl = row.querySelector('.product-name a');
    const priceEl = row.querySelector('.product-price .amount bdi');
    const qtyEl = row.querySelector('input.qty');
    const subtotalEl = row.querySelector('.product-subtotal .amount bdi');
    
    const name = nameEl?.innerText.trim() || "";
    const url = nameEl?.href || "";
    const price = priceEl?.innerText.trim().replace(/\s+/g, " ") || "";
    const qty = qtyEl?.value || "0";
    const subtotal = subtotalEl?.innerText.trim().replace(/\s+/g, " ") || "";
    
    data.push([name, url, price, qty, subtotal]);
  });
  
  // Convert to CSV
  const csv = data.map(r => r.map(v => `"${v}"`).join(",")).join("\n");
  console.log(csv);
})();


```



Here’s the **modified version** — it will **auto-fetch all pages (1–10)** of the *Film Resistors* category, gather **URL + SKU**, and give you a full CSV at once:

```

(async () => {
    const totalPages = 2;
    let csv = "URL,SKU\n";

    for (let i = 1; i <= totalPages; i++) {
        let url = i === 1 
            ? "https://robu.in/product-category/electronic-components/resistors/film-resistors/"
            : `https://robu.in/product-category/electronic-components/resistors/film-resistors/page/${i}/`;
        console.log(`Fetching page ${i}: ${url}`);

        let html = await fetch(url).then(r => r.text());
        let doc = new DOMParser().parseFromString(html, "text/html");
        let products = doc.querySelectorAll('.woocommerce-loop-product__link');

        products.forEach(p => {
            let productUrl = p.href;
            let skuEl = p.querySelector('.product-sku');
            let sku = skuEl ? skuEl.textContent.replace('SKU:', '').trim() : '';
            csv += `"${productUrl}","${sku}"\n`;
        });
    }

    // Create and download CSV file
    let blob = new Blob([csv], { type: "text/csv" });
    let link = document.createElement("a");
    link.href = URL.createObjectURL(blob);
    link.download = "film_resistors.csv";
    document.body.appendChild(link);
    link.click();
    document.body.removeChild(link);

    alert("✅ film_resistors.csv downloaded!");
})();

```

**How to use:**

1. Open Firefox.
2. Go to **any one** of the Film Resistor pages.
3. Open **Console (F12 → Console tab)**.
4. Paste this full script and press **Enter**.
5. Wait a few seconds — when done, it’ll alert and the **CSV is copied to your clipboard**.

Then just paste it into a text editor and save as `film_resistors.csv`.




