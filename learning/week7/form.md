# Week 7

## Menu

<ul>
<li><button id="hello">Hello</button> Display Hello </li>
<li><button id="hi">Hi</button> Display Hi </li>
<li><button id="taller">Taller</button> Make it taller</li>
<li><button id="shorter">Shorter</button> Make it shorter</li>
<li><button id="red">Red</button> Set background color to red</li>
<li><button id="green">Green</button> Set background color to green</li>
</ul>

<ul>
<li><button id="show">Show</button><input id="show-text" type="text" value="hello"/> Set background color to green</li>
</ul>

## Viz

<div class="myviz" style="width:100%; height:100px; border: 1px black solid;">
</div>


{% script %}

console.log('hello')

$('button#hello').click(function(){
    console.log('hello button is clicked')
    $('.myviz').html("hello")
})

$('button#hi').click(function(){
    console.log('hello button is clicked')
    $('.myviz').html("hi")
})

$('button#taller').click(function(){
    console.log('taller button is clicked')
    $('.myviz').height(500)
})

$('button#shorter').click(function(){
    console.log('shorter button is clicked')
    $('.myviz').height(100)
})

{% endscript %}
