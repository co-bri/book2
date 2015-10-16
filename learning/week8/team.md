# UI

Pick one question class and build an exploratory visualization interface for it.
The question class you pick must have at least three variables that can be changed.

## How many businesses are open on X day at Y hour?
Show distribution over states


<div style="border:1px grey solid; padding:5px;">
    <div><h5>Select day of the week</h5>
        <input id="day" type="text" value="Monday"/>
    </div>
    <div><h5>Select hour for being open (using xx:yy using 24 hour clock) </h5>
        <input id="hour" type="text" value="13:00"/>
    </div>
    <div><h5>Select sort order 'ascending' or 'descending'</h5>
        <input id="order" type="text" value="ascending"/>
    </div>    
    <div style="margin:20px;">
        <button id="viz">Vizualize</button>
    </div>
</div>

<div class="myviz" style="width:100%; height:500px; border: 1px black solid; padding: 5px;">
Data is not loaded yet
</div>

{% script %}
items = 'not loaded yet'

$.get('http://bigdatahci2015.github.io/data/yelp/yelp_academic_dataset_business.5000.json.lines.txt')
    .success(function(data){        
        var lines = data.trim().split('\n')

        // convert text lines to json arrays and save them in `items`
        items = _.map(lines, JSON.parse)

        console.log('number of items loaded:', items.length)

        console.log('first item', items[0])
     })
     .error(function(e){
         console.error(e)
     })

function viz(day, hour, order){    

    // define a template string
    var tplString = '<g transform="translate(0 ${d.y})"> \
                    <text y="20">${d.label}</text> \
                    <rect x="30"   \
                         width="${d.width}" \
                         height="20"    \
                         style="fill:${d.color};    \
                                stroke-width:3; \
                                stroke:rgb(0,0,0)" />   \
                    </g>'

    // compile the string to get a template function
    var template = _.template(tplString)

    function computeX(d, i) {
        return 0
    }

    function computeWidth(d, i) {        
        return d[1]/max * 600
    }

    function computeY(d, i) {
        return i * 20
    }

    function computeColor(d, i) {
        return 'red'
    }

    function computeLabel(d, i) {
        return d[0]
    }

    // Convert hour string to int
    function hourToInt(h) {
        var x = h.split(':')
        return x[0] * 3600 + x[1] * 60
    }

    // The input hour as an integer
    var hourAsInt = hourToInt(hour)
    console.log('hour', hour)

    // First filter all entries for the specified day and time
    open = _.filter(items, function(d) {
        return d.hours && d.hours[day] &&
            (hourToInt(d.hours[day].open) <= hourAsInt &&
             hourAsInt <= hourToInt(d.hours[day].close))
        })

    // Next group by state
    var groups = _.groupBy(open, 'state')

    // Take groups and attach counts to stat
    var counts = _.mapValues(groups, function(d){
	l = d.length
        return l
    })
    console.log(counts)
    
    countByState = _.pairs(counts)

    console.log(countByState)

    sortedStates = _.sortBy(countByState,function(d){
	if (order == 'ascending'){
		return d[1]
	}
	else{
		return -d[1]
	}

    })
    console.log(sortedStates)

    max = (_.max(countByState, function(d){
	return d[1]

    }))[1]
    
    console.log('max',max)
 
    // take the first 20 items to visualize    
    show = _.take(sortedStates,20 )

    var viz = _.map(show, function(d, i){                
                return {
                    x: computeX(d, i),
                    y: computeY(d, i),
                    width: computeWidth(d, i),
                    color: computeColor(d, i),
                    label: computeLabel(d, i)
                }
             })
    console.log('viz', viz)

    var result = _.map(viz, function(d){
             // invoke the compiled template function on each viz data
             return template({d: d})
         })
    console.log('result', result)

    $('.myviz').html('<svg width="100%" height="100%">' + result + '</svg>')
}

$('button#viz').click(function(){    
    var day = $('input#day').val()
    var hour = $('input#hour').val()
    var order = $('input#order').val()  
    console.log(day,hour,order)
    viz(day, hour, order)
})



{% endscript %}

# Authors

This UI is developed by
* [Brian McKean](http://co-bri.github.io/book2)
* [Karen Blakemore](https://github.com/kjblakemore/book2)
* [Ming Leiw](http://malaokia.github.io/book2/)
* [Matt Schroeder](http://mattschroeder97.github.io/book2)

