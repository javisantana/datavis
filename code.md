
## 01 - loading JSON

[code](01.html) ·
[live](http://javisantana.com/data_vis_workshop/01.html)

```js
 async function run() {
      const url = 'https://api.tinybird.co/v0/pipes/madrid_no2.json?token=p.eyJ1IjogIjI0OTA1NjBmLWJkYTEtNDE0OC1iZmViLTNmYWEzODMzZGEzMyIsICJpZCI6ICJkOTYxMjk2YS1mZTllLTQ2MzEtYTJiMy02OTA1N2Y5M2RmODcifQ.NZqRDFnFQWu4ylTCVyLfQ8LGt0KN2JR6ILSANmSObBM'
      const response = await fetch(url)
      const data = await response.json();
      console.log(data)
}
run()
```

## 02 - Rendering a square

[code](01.html) ·
[live](http://javisantana.com/data_vis_workshop/02.html)


```js
function square(x, y, w, h, c) {
    var div = document.createElement('div')
    div.style.left = x + "px"
    div.style.top = y + "px"
    div.style.width = w + "px"
    div.style.height = h + "px"
    div.style.backgroundColor = c
    div.style.display = "inline-block"
    return div;
}
```

```js
var s = square(0,0, 100, 100, '#000')
var content = document.getElementById('content')
content.appendChild(s)
```

## 03 - Rendering an element

[code](03.html) ·
[live](http://javisantana.com/data_vis_workshop/03.html)

```js
    var content = document.getElementById('content')
    var estacion = data.data[0]
    for (var value of estacion.values) { 
      var color = `rgba(${value}, ${value}, ${value}, 1.0)`
      var s = square(0, 0, 1, 100, color)
      content.appendChild(s)
    }
```

## 04 - rendering all

[code](04.html) ·
[live](http://javisantana.com/data_vis_workshop/04.html)

```js
var H = 20
var content = document.getElementById('content')
for (var estacion of data.data) {
  var estacion_div = document.createElement('div')
  estacion_div.style.height = `${H}px`
  for (var value of estacion.values) { 
    var color = `rgba(${value}, ${value}, ${value}, 1.0)`
    var s = square(0, 0, 1, H, color)
    estacion_div.appendChild(s)
  }
  content.appendChild(estacion_div)
}
```

we see some missalignment

## 05 - fixing missing days

[code](05.html) ·
[live](http://javisantana.com/data_vis_workshop/05.html)

```js
var dates = {}
for (var [i, day] of Object.entries(estacion.days)) { 
  dates[day] = estacion.values[i]
}

for (var day = 0; day < 365; ++day) {
  var value = dates[day]
  var color = `rgba(${value}, ${value}, ${value}, 1.0)`
  var s = square(0, 0, 1, H, color)
  estacion_div.appendChild(s)
}
```

## 06 - adding some text

[code](06.html) ·
[live](http://javisantana.com/data_vis_workshop/06.html)

```js
var text = document.createElement('div')
text.style.display = 'inline-block';
text.style.width= '200px';
text.style.textAlign = 'right'
text.style.font = '11px sans-serif'
text.innerHTML = estacion.direccion;
estacion_div.appendChild(text)
```

## 07 - adding some color

[code](07.html) ·
[live](http://javisantana.com/data_vis_workshop/07.html)

```js
function color(v) {
  var stops = [15,20,29,40,58,85]
  var colors = ['#e4f1e1','#b4d9cc','#89c0b6','#63a6a0','#448c8a','#287274','#0d585f']

  if (v === undefined) return '#AAA'
  for (var i = 0; i < stops.length; ++i) {
    if (v < stops[i]) {
      return colors[i];
    }
  }
  return colors[colors.length - 1]
}
```

## 08 - improving the color

[code](08.html) ·
[live](http://javisantana.com/data_vis_workshop/08.html)

```js
function color(v) {
  var stops = [34,65,91,123,180,200,400]
  var colors = ['#3d5941','#778868','#b5b991','#f6edbd','#edbb8a','#de8a5a','#ca562c']
  //var colors = ['#e4f1e1','#b4d9cc','#89c0b6','#63a6a0','#448c8a','#ca5268','#b13f64']

  if (v === undefined) return '#EEE'
  for (var i = 0; i < stops.length; ++i) {
    if (v < stops[i]) {
      return colors[i];
    }
  }
  return colors[colors.length - 1]
}
```


