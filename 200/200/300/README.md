# 300 - Cascading Style Sheets (CSS)

````
@import url('https://fonts.googleapis.com/css?family=Poppins:300,400,500,600,700,800,900&display=swap');
*
{
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: 'Poppins', sans-serif;
  scroll-behavior: smooth;
}
body
{
  background: linear-gradient(#2b1055,#7597de);
}
section
{
  position: relative;
  width: 100%;
  height: 100vh;
  padding: 100px;
  overflow: hidden;
  display: flex;
  justify-content: center;
  align-items: center;
}
header
{
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  padding: 30px 100px;
  display: flex;
  justify-content: space-between;
  align-items: center;
  z-index: 1000;
}
header .logo
{
  color: #fff;
  font-weight: 700;
  text-decoration: none;
  font-size: 2em;
  text-transform: uppercase;
  letter-spacing: 2px;
}
header ul
{
  display: flex;
  justify-content: center;
  align-items: center;
}
header ul li
{
  list-style: none;
  margin-left: 20px;
}
header ul li a
{
  text-decoration: none;
  padding: 6px 15px;
  color: #fff;
  border-radius: 20px;
}
header ul li a.active,
header ul li a:hover
{
  background: #fff;
  color: #2b1055;
}
section:before
{
  content: '';
  position: absolute;
  bottom: 0;
  width: 100%;
  height: 100px;
  background: linear-gradient(to top,#1c0522,transparent);
  z-index: 1000;
}
section img
{
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  object-fit: cover;
  pointer-events: none;
}
section img#moon
{
  mix-blend-mode: screen;
}
section img#mountains_front
{
  z-index: 10;
}
h2#text
{
  position: absolute;
  color: #fff;
  right: -350px;
  white-space: nowrap;
  font-size: 7.5vw;
  transform: translateY(0px);
}
#btn
{
  text-decoration: none;
  padding: 8px 30px;
  border-radius: 40px;
  background: #fff;
  color: #2b1055;
  transform: translateY(100px);
  font-size: 1.5em;
  z-index: 9;
}
.sec
{
  position: relative;
  min-height: 500px;
  padding: 100px;
  background: #1c0522;
}
.sec h2
{
  font-size: 3.5em;
  margin-bottom: 10px;
  color: #fff;
}
.sec p
{
  font-size: 1.2em;
  color: #fff;
}
````
style.css
