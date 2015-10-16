# JQuery Click Handler

<ol>
<li><button id="hello">Hello</button> Display Hello </li>
<li><button id="hi">Hi</button> Display Hi </li>
<li><button id="taller">Taller</button> Make it taller</li>
<li><button id="shorter">Shorter</button> Make it shorter</li>
<li><button id="red">Red</button> Set background color to red</li>
<li><button id="green">Green</button> Set background color to green</li>
<li><button id="onebar">One Bar</button></li>
<li><button id="twobars">Two Bars</button></li>
<li><button id="fivebars">Five Bars</button></li>
<li><button id="fivegreenbars">Five Green Bars</button></li>
</ol>

## Viz

<div class="myviz" style="width:100%; height:100px; border: 1px black solid; ">
</div>


{% script %}
console.log('adding click event handlers')

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

// TODO: add an event handler for the "Red" button to set the background color
// of the viz block to red
$('button#red').click(function(){
    console.log('red button is clicked')
    $('.myviz').css("background-color", "red")    
})

// TODO: add an event handler for the "Green" button to set the background color
// of the viz block to green
$('button#green').click(function(){
    console.log('green button is clicked')
    $('.myviz').css("background-color", "green")    
})

$('button#onebar').click(function(){
    var svg = "<svg><rect height='50' width='10'></rect></svg>"
    $('.myviz').html(svg)
})

$('button#twobars').click(function(){
    var svg = "<svg><rect height='50' width='10'/><rect height='50' width='10' x='20'/></svg>"
    $('.myviz').html(svg)
})

// TODO: add an event handler for the "Five Bars" button to display five bars
$('button#fivebars').click(function(){
    var svg = "<svg>  \
	<rect height='50' width='10'/>   \
	<rect height='50' width='10' x='20'/> \
	<rect height='50' width='10' x='40'/> \
	<rect height='50' width='10' x='60'/> \
	<rect height='50' width='10' x='80'/> \
	</svg>"
    $('.myviz').html(svg)
})

// TODO: add an event handler for the "Five Green Bars" button to display five green bars
$('button#fivegreenbars').click(function(){
    var svg = "<svg>  \
	<rect height='50' width='10' fill='green'/>   \
	<rect height='50' width='10' fill='green' x='20'/> \
	<rect height='50' width='10' fill='green' x='40'/> \
	<rect height='50' width='10' fill='green' x='60'/> \
	<rect height='50' width='10' fill='green' x='80'/> \
	</svg>"
    $('.myviz').html(svg)
})

{% endscript %}
