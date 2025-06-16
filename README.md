# Fire_help
Firefox Console script



```

Firefox Console script to check pages 1–19 on the given site for the word "dada" and log which pages contain it:



https://moviesda.it.com/tamil-2023-movies/?page=1

to

https://moviesda.it.com/tamil-2023-movies/?page=19


```





```
(async () => {
  const baseURL = "https://moviesda.it.com/tamil-2023-movies/?page=";
  const keyword = "dada";
  const foundPages = [];

  for (let i = 1; i <= 19; i++) {
    try {
      const response = await fetch(baseURL + i);
      const text = await response.text();
      if (text.toLowerCase().includes(keyword.toLowerCase())) {
        console.log(`Found "${keyword}" on page ${i}`);
        foundPages.push(i);
      } else {
        console.log(`Not found on page ${i}`);
      }
    } catch (e) {
      console.log(`Error loading page ${i}:`, e);
    }
  }

  console.log("Pages with the word 'dada':", foundPages);
})();

```

