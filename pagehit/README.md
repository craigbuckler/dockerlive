# PageHit (MySQL database)

A page hit counter service which saves data to a MySQL database.

This is an example project for the purposes of demonstration only. It is not recommended for production use!

Enter `docker-compose up` to start:

1. `pagehitdb`: MySQL database, <http://localhost:3306>
1. `adminer`: Adminer SQL client, <http://localhost:8080>
1. `pagehit`: web service, <http://localhost:8104>


## How to use the PageHit service

There are four ways to call the PageHit service from any web page to show the number of times it has been viewed.

### 1. Add an image

Add a counter image (SVG) to any page:

```html
<img src="http://localhost:8104/hit.svg" alt="hits" referrerpolicy="unsafe-url" />
```

Note: a `referrerpolicy` is required otherwise Chrome will not send the full URL with the domain and path.


### 2. Insert a script

Add a script to any page:

```html
<script src="http://localhost:8104/hit.js" referrerpolicy="unsafe-url"></script>
```

The following HTML is inserted into the page at the `<script>` location:

```html
<span class="pagehitjs">1</span>
```

This method uses `document.write()` which may affect page loading performance.


### 3. Insert a deferred script

Add a deferred script to any page:

```html
<script src="http://localhost:8104/hit-defer.js" referrerpolicy="unsafe-url" async defer></script>
```

The following HTML is inserted into the page at the `<script>` location:

```html
<span class="pagehitdefer">1</span>
```

This updates the page after the content has loaded so performance should not be affected.


### 4. Make an Ajax request

Fetch the current number of page hits using an Ajax request to <http://localhost:8104/hit.json>. This returns a single JSON-encoded object with a `hit` property, e.g. `{ hit: 1 }`. The value can be examined and presented in any way.

```html
<p>This page has been viewed <span class="hits"></span> times.</p>

<script type="module">
(async () => {

  try {

    const
      response = await fetch('http://localhost:8104/hit.json', { referrerPolicy: 'unsafe-url' }),
      json = await response.json(),
      pc = document.querySelectorAll('.hits');

    for (let i = 0; i < pc.length; i++) {
      pc[i].textContent = json.hit;
    }

  }
  catch(err) {
    console.log('fetch error', err);
  }

})();
</script>
```
