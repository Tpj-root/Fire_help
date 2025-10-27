



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
