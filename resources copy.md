---
title: Competition Map
---

<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="utf-8">
<title>Competitive Cyber Club</title>
<script src="https://unpkg.com/vue"></script>
<link rel="stylesheet" href="./public/css/btns.min.css">
<script src="https://d3js.org/d3.v3.min.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/moment.js/2.27.0/locale/af.min.js"></script>
<!-- <script src="https://d3js.org/d3.v4.js"></script> -->
<style type="text/css">
@import url('https://fonts.googleapis.com/css2?family=Ubuntu+Mono:ital,wght@0,400;0,700;1,400;1,700&display=swap');
* {
  margin: 0;
  padding: 0;
  border: 0;
  font-family: 'Ubuntu Mono', monospace;
}

/* On mouse hover, lighten state color */
path:hover {
	fill-opacity: .7;
}

/* Style for Custom Tooltip */
div.tooltip {   
 	position: absolute;           
	text-align: center;           
	width: 60px;                  
	height: 28px;                 
	padding: 2px;             
	font: 12px sans-serif;        
	background: white;   
	border: 0px;      
	border-radius: 8px;           
	pointer-events: none;         
}
        
/* Legend Font Style */
/* body {
	font: 11px sans-serif;
} */
        
/* Legend Position Style */
/* .legend {
	position:absolute;
	left:800px;
	top:350px;
} */
/* Start navbar */

.n1{grid-area: n1;}
.n2{grid-area: n2;}

.navbar{
    height: 40px;
    width: 100%;
    display: grid;
    grid-template-rows: 1fr;
    grid-template-columns: 1fr 2fr 2fr 1fr;
    grid-template-areas:
        ".   n1  n2  .";
}

.navbar h1{
    padding-left: 100px;
}

.s1{grid-area: s1;}
.s2{
    display: grid;
    grid-area: s2;
    grid-gap: 1em;
    grid-template-rows: 1fr 3fr;
    grid-template-columns: 1fr;
    grid-template-areas:
        "ss1"
        "ss2";
}
.ss1{grid-area: ss1;}
.ss2{grid-area: ss2;}

.s3{grid-area: s3;}

.mainGrid{
    display: grid;
    padding-top: 1em;
    padding: 1em;
    grid-gap: 1em;
    width: 100%;
    grid-template-rows: 1fr 1fr;
    grid-template-columns: 1fr 2fr 2fr 1fr;
    grid-template-areas:
        ".   s1  s2  ."
        ".   s3  s3  .";
}

/* Start Card */

.card{
  opacity: 100%;
  background-color: white;
  padding: 1em;
  box-shadow: 0 1px 3px rgba(0, 0, 0, 0.12), 0 1px 2px rgba(0, 0, 0, 0.24);
  border-radius: 5px;
  transition: all 0.3s cubic-bezier(.25,.8,.25,1);
}
.card:hover {
  opacity: 100%;
   box-shadow: 0 14px 28px rgba(0, 0, 0, 0.25), 0 10px 10px rgba(0, 0, 0, 0.22);;
}

.target{
    grid-area: target;
    display: grid;
    grid-template-rows: 1fr;
    grid-gap: 1em;
    grid-template-columns: 2fr 1fr;
    grid-template-areas:
        "c1 c2";
}

.eCard{
    border-radius:10px;
    padding: 1em;
    margin: 10px;
    border:1px solid black;
    background-color: white;
	display:inline-block;
}

table td{
    padding: .5em;
}

table th{
    padding: 1em;
}

table td:nth-child(odd){
    background-color: #d5ded9;
    opacity: 70%;
}
table td:nth-child(even){
    background-color: white;
    opacity: 70%;
}

.iCard{
    border-radius:10px;
    padding: 1em;
    margin: 10px;
    border:1px solid #a2a8a5;
    background-color: #d5ded9;
	display:inline-block;
}

</style>
</style>
</head>
<body>

    <div id="app">
        <div class="navbar">
            <h1 class="n1">Competitive Cyber Club</h1>
            <p class="n2">Current event map</p>
        </div>
        <div class="mainGrid">
            <div class="s1 card">
                <button v-on:click="drawMap()">ReDraw Map</button>
            </div>
            <div class="s2">
                <div class="ss1 card"></div>
                <div class="ss2 card">
                    <!-- <h1>Register an Event:</h1>
                    <input v-model='mInput.size' type="number" placeholder="0">Size</input>
                    <input v-model='mInput.location' type="text" placeholder="location">Location</input>
                    <input v-model='mInput.lat' type="number" placeholder="0">Long</input>
                    <input v-model='mInput.lon' type="number" placeholder="0">Lat</input>
                    <br>
                    <button v-on:click="drawInd()">Draw New Ind</button>
                    <div class="iCard">{{ mInput }}</div> -->
                    <a href="https://forms.gle/98mkZEw67cDwJ2UB9" class="btn"> Submit an event here! </a>
                </div>
            </div>
            <div class="s3 card">
                <h1>Current Events</h1>
                <table class="">
                    <thead>
                        <tr>
                        <th></th>
                        <th>Competition Name</th>
                        <th>Location</th>
                        <th>Host</th>
                        <th>Online/In Person</th>
                        <th>Competition Type</th>
                        <th>Website</th>
                        <th>Contact</th>
                        <th>Date Start</th>
                        <th>Date End</th>
                        <th></th>
                        </tr>
                    </thead>
                    <tbody>
                        <tr v-for="(item, index) in current_events"  :key="index">
                        <!-- <td>{{ index }}</td> -->
                        <td><img v-bind:src="item.comp_logo_url" alt="" width="32px" height="32px"></td>
                        <!-- <td scope="row">{{ item.size  }}</td>   -->
                        <td>{{  item.comp_name  }}</td>
                        <td>{{  item.location  }}</td>
                        <td>{{  item.host  }}</td>
                        <td>{{  item.is_online  }}</td>
                        <td>{{  item.is_redblue  }}</td> 
                        <td><a v-bind:href="item.site">{{  item.site  }}</a></td> 
                        <td>{{  item.contact  }}</td> 
                        <td>{{  item.start_date  }}</td>
                        <td>{{  item.end_date  }}</td>  
                        </tr>

                    </tbody>
                    </table>
            </div>
        </div>
        <!-- <button v-on:click="makeCSV">LocalStore</button> -->
      </div>
    
      <script>
        var app = new Vue({
          el: '#app',
          data: function() {
            return {
                current_events: null,
                states_data: null,
                ce_URI: 'http://3.130.69.51:8081/events',
                sd_URI: './public/json/states_data.json',
                mInput: {},
                message: 'test',
                textObject: {
                    "size": 2,
                    "location": "New York City2",
                    "lat": 50.71455,
                    "lon": -74.007124
                    },
            };
            },
          mounted: function() {
            this.drawMap();
            var that = this;

            d3.json(this.ce_URI,
                function(error, data) {
                if (error) throw error;

                    // Load the CSV data

                that.current_events = data;
                }
            );
            d3.json(this.sd_URI,
                function(error, data) {
                if (error) throw error;

                    // Load the CSV data
                
                that.states_data = data;
                }
            );
            },
            computed: {
                currentRouteName() {
                    return this.$route.name;
                }
            },
            methods: {
                findDistance: function(){
                },
                drawInd: function () {
                    // d3.json('current_events.json', function(data) {
                    // //that.cities_lived.forEach(data => {
                    //Width and height of map
                    var width = 960;
                    var height = 500;

                    var svg = d3.select(".s1");

                    var finalData = JSON.parse(JSON.stringify(this.textObject));
                    svg.selectAll("circle")
                        .data([{size: 5,lat: 20,lon: 20,location: 'hello'}])
                        .enter()
                        .append("circle")
                        // .attr("cx" , '40.71455')
                        // .attr("cy" , '-74.007124')
                        .attr("cx", function(d) {
                            console.log(d.lon + ' - ' + d.lat)
                            return projection([d.lon, d.lat])[0];
                        })
                        .attr("cy", function(d) {
                            return projection([d.lon, d.lat])[1];
                        })
                        .attr("r", function(d) {
                            return Math.sqrt(d.size) * 4;
                        })
                            .style("fill", "rgb(217,91,67)")	
                            .style("opacity", 0.85)	

                        .on("mouseover", function(d) {      
                            div.transition()        
                            .duration(200)      
                            .style("opacity", .9);      
                            div.text(d.location)
                            .style("left", (d3.event.pageX) + "px")     
                            .style("top", (d3.event.pageY - 28) + "px");    
                        })   

                        // fade out tooltip on mouse out               
                        .on("mouseout", function(d) {       
                            div.transition()        
                            .duration(500)      
                            .style("opacity", 0);   
                        });
                    // });
                },
                drawMap: function () { 
                     
                    //Delete Previous draw
                    d3.selectAll("svg").remove();
                    d3.selectAll(".tooltip").remove();
                    
                    //Width and height of map
                    var width = 960;
                    var height = 500;

                    // D3 Projection
                    var projection = d3.geo.albersUsa()
                                    .translate([width/2, height/2])    // translate to center of screen
                                    .scale([1000]);          // scale things down so see entire US
                            
                    // Define path generator
                    var path = d3.geo.path()               // path generator that will convert GeoJSON to SVG paths
                                .projection(projection);  // tell path generator to use albersUsa projection

                            
                    // Define linear scale for output
                    var color = d3.scale.linear()
                                .range(["rgb(213,222,217)","rgb(69,173,168)","rgb(84,36,55)","rgb(217,91,67)"]);

                    var legendText = ["Current Events", "Home State", "Involved States", "No Information"];

                    //Create SVG element and append map to the SVG
                    var svg = d3.select(".s1")
                                .append("svg")
                                .attr("width", width)
                                .attr("height", height);
                                // .call(d3.behavior.zoom().on("zoom", function () {
                                //     console.log('should zoom')
                                // svg.attr("transform", d3.event.transform)
                                // }))
                                // .append("g");

                    // append the svg object to the body of the page
                    // var svg = d3.select("#dataviz_basicZoom")
                    // .append("svg")
                    //     .attr("width",  460)
                    //     .attr("height",  460)
                    //     .call(d3.behavior.zoom().on("zoom", function () {
                    //     svg.attr("transform", d3.event.transform)
                    //     }))
                    // .append("g")
                            
                    // Append Div for tooltip to SVG
                    var div = d3.select("body")
                                .append("div")   
                                .attr("class", "tooltip")               
                                .style("opacity", 0);

                    // Load in my states data!
                    //console.log(this.states_data)
                    // this.makeCSV();
                    // d3.json("states_data.json").then( data => {
                    //     console.log(data);
                    // });
                    var ce = this.ce_URI

                    d3.json(this.sd_URI, function(data) {
                    color.domain([0,1,2,3]); // setting the range of the input data

                    // Load GeoJSON data and merge with states data
                    d3.json("./public/json/us-states.json", function(json) {

                    // Loop through each state data value in the .csv file
                    for (var i = 0; i < data.length; i++) {

                        // Grab State Name
                        var dataState = data[i].state;

                        // Grab data value 
                        var dataValue = data[i].value;

                        // Find the corresponding state inside the GeoJSON
                        for (var j = 0; j < json.features.length; j++)  {
                            var jsonState = json.features[j].properties.name;

                            if (dataState == jsonState) {

                            // Copy the data value into the JSON
                            json.features[j].properties.value = dataValue; 

                            // Stop looking through the JSON
                            break;
                            }
                        }
                    }
                            
                    // Bind the data to the SVG and create one path per GeoJSON feature
                    svg.selectAll("path")
                        .data(json.features)
                        .enter()
                        .append("path")
                        .attr("d", path)
                        .style("stroke", "#fff")
                        .style("stroke-width", "1")
                        .style("fill", function(d) {

                        // Get data value
                        var value = d.properties.value;

                        if (value) {
                        //If value exists…
                        return color(value);
                        } else {
                        //If value is undefined…
                        return "rgb(213,222,217)";
                        }
                    });

                            
                    // console.log(this._cities_lived)
                    // console.log(this.message)
                    //console.log(this._Oldcities_lived)
                    d3.json(ce, function(data) {
                    //that.cities_lived.forEach(data => {
                    // console.log('---vvv---')
                    // console.log(data)
                    svg.selectAll("circle")
                        .data(data)
                        .enter()
                        .append("circle")
                        // .attr("cx" , '40.71455')
                        // .attr("cy" , '-74.007124')
                        .attr("cx", function(d) {
                            return projection([d.lon, d.lat])[0];
                        })
                        .attr("cy", function(d) {
                            return projection([d.lon, d.lat])[1];
                        })
                        .attr("r", function(d) {
                            return Math.sqrt(d.size) * 4;
                        })
                            .style("fill", "rgb(217,91,67)")	
                            .style("opacity", 0.85)	

                        .on("mouseover", function(d) {      
                            div.transition()        
                            .duration(200)      
                            .style("opacity", .9);      
                            div.text(d.location)
                            .style("left", (d3.event.pageX) + "px")     
                            .style("top", (d3.event.pageY - 28) + "px");    
                        })   

                        // fade out tooltip on mouse out               
                        .on("mouseout", function(d) {       
                            div.transition()        
                            .duration(500)      
                            .style("opacity", 0);   
                        });
                    });  
                            
                    var legend = d3.select(".ss1").append("svg")
                                    .attr("class", "legend")
                                    .attr("width", 200)
                                    .attr("height", 100)
                                    .selectAll("g")
                                    .data(color.domain().slice().reverse())
                                    .enter()
                                    .append("g")
                                    .attr("transform", function(d, i) { return "translate(0," + i * 20 + ")"; });

                        legend.append("rect")
                            .attr("width", 18)
                            .attr("height", 18)
                            .style("fill", color);

                        legend.append("text")
                            .data(legendText)
                            .attr("x", 24)
                            .attr("y", 9)
                            .attr("dy", ".35em")
                            .text(function(d) { return d; });
                        });

                    });
                }
            }
        })
      </script>

<script type="text/javascript">


</script>
</body>

</html>
