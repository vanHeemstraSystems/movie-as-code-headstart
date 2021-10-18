# 200 - HyperText Markup Language (HTML)

````
<!doctype html>
<html>
  <head>
    <title>MoonLight Parallax Effects | Vanilla Javascript</title>
    <link rel="stylesheet" type="text/css" href="style.css">
  </head>
  <body>
    <header>
      <a href="#" class="logo">Logo</a>
      <ul>
        <li><a href="#" class="active">Home</a></li>
        <li><a href="#">About</a></li>
        <li><a href="#">Work</a></li>
        <li><a href="#">Contact</a></li>
      </ul>
    </header>
    <section>
      <img src="stars.png" id="stars">
      <img src="moon.png" id="moon">
      <img src="mountains_behind.png" id="mountains_behind">
      <h2 id="text">Moon Light</h2>
      <a href="#sec" id="btn">Explore</a>
      <img src="mountains_front.png" id="mountains_front">
      <div class="content">
    </section>
    <div class="sec" id="sec">
      <h2>Parallax Background Scrolling</h2>
      <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod
      tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam,
      quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo
      consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse
      cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non
      proident, sunt in culpa qui officia deserunt mollit anim id est laborum.Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod
      tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam,
      quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo
      consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse
      cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non
      proident, sunt in culpa qui officia deserunt mollit anim id est laborum.<br><br>Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod
      tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam,
      quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo
      consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse
      cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non
      proident, sunt in culpa qui officia deserunt mollit anim id est laborum.Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod
      tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam,
      quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo
      consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse
      cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non
      proident, sunt in culpa qui officia deserunt mollit anim id est laborum.Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod
      tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam,
      quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo
      consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse
      cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non
      proident, sunt in culpa qui officia deserunt mollit anim id est laborum.</p>
    </div class="sec">
    <script type="text/javascript">
      let moon = document.getElementById('moon');
      let stars = document.getElementById('stars');
      let mountains_behind = document.getElementById('mountains_behind');
      let mountains_front = document.getElementById('mountains_front');
      let text = document.getElementById('text');
      let btn = document.getElementById('btn');
      let header = document.querySelector('header');
      window.addEventListener('scroll', function() {
        var value = window.scrollY;
        moon.style.top = -value * -1.05 + 'px';
        stars.style.left = value * 0.25 + 'px';
        mountains_behind.style.top =-value * -0.5 + 'px';
        header.style.top =-value * -0.5 + 'px';
        mountains_front.style.top =-value * 0 + 'px';
        text.style.marginTop = value * 1.5 + 'px';
        btn.style.marginTop = value * 1.5 + 'px';
        text.style.marginRight = value * 4 + 'px';
      });
    </script>
  </body>
</html>
````
index.html
