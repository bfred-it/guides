# Find Elements Across a Site

When working on a large CMS, you might not have a clear view of where something appears across multiple page.

Use this to see where an element or text appears by requesting all the URLs in the site nav.

Copy it into your browser console and wait for it to open multiple tabs (they will be blocked by the browser, so whitelist your site)

## Search by selector

```js
var linksSelector = 'nav a';
var elementToLookFor = '.selector';
[...document.querySelectorAll(linksSelector)].forEach(a => {
	console.count('link')
	fetch(a.href).then(r => r.text()).then(html => {
		const root = document.createElement('html');
		root.innerHTML = html;
		const search = root.querySelector(elementToLookFor);
		if(search) {
			window.open(a.href)
		}

		console.count('executed')
	})
});
```

## Search by plain text

```js
var linksSelector = 'nav a';
var textToLookFor = 'whatever text you want';
[...document.querySelectorAll(linksSelector)].forEach(a => {
    console.count('link')
    fetch(a.href).then(r => r.text()).then(html => {
        if(html.indexOf(textToLookFor) > 0) {
            window.open(a.href)
        }
        console.count('executed')
    })
});
```
