## Website Performance Optimization portfolio project

This is my Project 4 for the Udacity Frent End Web Development Nanodegree.

### Optimizations for PageSpeed Insights:
* add print media query to print css so it doesn't block DOM construction
* compress pizzeria image from 2.4MB to 516KB to save bandwith and time to/from server
* reduce image size to 320 x 240 to save bandwith and load time
* make Google analytics async so it doesn't block html parsing or DOM construction
* move entire styles.css file inline to reduce critical resource length
* only load subset Latin for google fonts to reduce critical bytes
* move google fonts to inline javascript
* minify css and javascript

### Optimizations for 60 FPS on the pizza.html page
* We don't need 200 pizzas. Nowhere near that many are even visible, so why waste resources rendering and updating something that isn't visible? I reduced the number of pizzas to only create enough to cover the visible page
* replace all instances of `querySelector` with `getElementBy....` as this is faster
* move `.mover` class height/width into CSS
* when adding all the `randomPizzas` to the `pizzasDiv`, We don't need to lookup the `pizzasDiv` each time through the `for` loop, as it doesn't change. We can look it up outside the `for` loop, which is much faster.

#### updatePositions
* Move the DOM lookup for class `.mover` out of the `for` loop and function, as it only
   needs ot happen once.
* Move the `scrollTop` DOM access out of the `for` loop, as it only needs to be done once.

#### resizePizzas
* I moved the DOM lookups for `pizzaSize` and `randomPizzas` out of the `for` loop because they only need to be looked up once, and fewer times accessing the DOM will speed things up
* for `changePizzaSizes` there is no need to calculate everything in the `for` loop, and certainly not to access the DOM looking up the class `randomPizzaContainer` each time. So those are moved outside the `for` loop so they only need to be looked up once. The only thing we must do in the `for` loop is what effects or is unique to each `pizzaContainer`, and that is change the width. The `pizzaContainers`, `numPizzaContainers`, `dx`, and `newwidth`, variables can all be pulled out of the `for` loop.

