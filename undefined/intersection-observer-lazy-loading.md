# Intersection Observer \(Lazy Loading\)



```markup
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <meta http-equiv="X-UA-Compatible" content="ie=edge" />
    <title>Document</title>
    <style>
      li {
        margin-bottom: 50px;
      }
      img {
        width: 100%;
        height: 200px;
      }
    </style>
  </head>
  <body>
    <div id="app">
      <ul>
        <li>
          <img
            data-src="https://t1.daumcdn.net/friends/prod/category/RYAN_M.jpg"
          />
        </li>
        <li>
          <img
            data-src="https://t1.daumcdn.net/friends/prod/category/RYAN_M.jpg"
          />
        </li>
        <li>
          <img
            data-src="https://t1.daumcdn.net/friends/prod/category/RYAN_M.jpg"
          />
        </li>
        <li>
          <img
            data-src="https://t1.daumcdn.net/friends/prod/category/RYAN_M.jpg"
          />
        </li>
        <li>
          <img
            data-src="https://t1.daumcdn.net/friends/prod/category/RYAN_M.jpg"
          />
        </li>
        <li>
          <img
            data-src="https://t1.daumcdn.net/friends/prod/category/RYAN_M.jpg"
          />
        </li>
        <li>
          <img
            data-src="https://t1.daumcdn.net/friends/prod/category/RYAN_M.jpg"
          />
        </li>
        <li>
          <img
            data-src="https://t1.daumcdn.net/friends/prod/category/RYAN_M.jpg"
          />
        </li>
        <li>
          <img
            data-src="https://t1.daumcdn.net/friends/prod/category/RYAN_M.jpg"
          />
        </li>
      </ul>
    </div>
    <script src="./imges.js"></script>
  </body>
</html>

```



```javascript
const images = document.querySelectorAll('img')

const observer = new IntersectionObserver((entries, observer) => {
  entries.forEach(({ isIntersecting, target }) => {
    if (isIntersecting) {
      if (target.getAttribute('data-src')) {
        target.setAttribute('src', target.getAttribute('data-src'))
        target.removeAttribute('data-src')
      }
    }
  })
})

images.forEach(image => observer.observe(image))

```

