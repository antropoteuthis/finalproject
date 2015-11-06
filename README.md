# Final Project - Interactive Siphonophore Cnidomic Phylomorphospace

## Introduction

This is a final project for the [Interacting with Data](https://github.com/Brown-BIOL2430-S04-Fall2015/syllabus) seminar in fall 2015. This project targets the representation of dependence relationships between quantitative cnidomic traits in 5 siphonophore species, while simultaneously keeping track of the phylogenetic relationships between the species. It will alternate views of the data by shifting the variables plotted in the scatterplot on demand, using movement and color to maintain the continuity of the identity of the species. A node-hinged polyline will connect the dots as they move through the phenotypic hyperspace using a force layout.

To view this project, you can click the bold headers with the variable names to change the X/Y representative variables.

<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="utf-8">
<title>Interactive Siphonophore Cnidome Phylomorphospace</title>
<style type="text/css">

text {
  font: 10px sans-serif;
}

line {
  stroke: #999;
  stroke-width: 1.5px
  stroke-opacity: 0.6;
}

circle {
  stroke: #999;
  stroke-width: 1.5px;
}

.axis path,
			.axis line {
				fill: none;
				stroke: black;
				shape-rendering: crispEdges;
			}
			
			.axis text {
				font-family: sans-serif;
				font-size: 11px;
			}

</style>
<script src="https://cdnjs.cloudflare.com/ajax/libs/d3/3.5.5/d3.min.js">  
</script>
</head>
<body>
<h2> Interactive Siphonophore Cnidomic Phylomorphospace </h2>
<p>Alejandro Damian Serrano</p>
<br>
<p> This is a siphonophore phylogeny with 5 species.
You can click on the variable names below to turn it into a PHYLOMORPHOSPACE.
This allows you to compare variables of the nematocyst composition (cnidome) among these siphonophore species while preserving the topology of phylogenetic relationships (common descent)
to interpret the evolutionary history of thes variables (traits).
 </p>
<h3 class = "hets_x"> Heteroneme size (microns) -- (X Axis) </h3>
<h3 class = "haps_x"> Haploneme size (microns) -- (X Axis) </h3>
<h3 class = "rs_x"> Rhopaloneme size (microns) -- (X Axis) </h3>
<h3 class = "hapn_y"> Haploneme number -- (Y Axis) </h3>
<h3 class = "hetn_y"> Heteroneme number -- (Y Axis) </h3>
<script>

var w = 660,
    h = 500;
var padding = 50;

var colors = {"Nanomia bijuga":"blue", "Agalma elegans":"red", "Hippopodius hippopus":"green", "Muggiaea atlantica":"yellow", "Abylopsis tetragona":"purple", "Physonectae":"black", "Diphyidae":"black", "Calycophorae":"black", "Codonophora":"black"};

var headers = ["node","parent","branch_length","species","istip","Haploneme size (microns)","Haploneme number","Heteroneme size (microns)","Heteroneme number","Rhopaloneme size (microns)"];

var dataset = {

	nodes: [
		{ name: "Codonophora", istip: false, haps: 27.5, hapn: 5487.5, hets: 89, hetn: 20.75, rs: 7.625, defx: 660, defy: 200 },
		{ name: "Calycophorae", istip: false, haps: 26.25, hapn: 225, hets: 72, hetn: 9, rs: 6, defx: 990 , defy: 500 },
		{ name: "Diphyidae", istip: false, haps: 22.5, hapn: 250, hets: 60, hetn: 8, rs: 6, nn: 8.5, defx: 990, defy: 625},
		{ name: "Physonectae", istip: false, haps: 28.75, hapn: 10750, hets: 106, hetn: 32.5, rs: 9.25, defx: 330 , defy: 500 },
		{ name: "Abylopsis tetragona", istip: true, haps: 52.5, hapn: 800, hets: 155, hetn: 21, rs: 23, defx: 990, defy: 750 },
		{ name: "Muggiaea atlantica", istip: true, haps: 15, hapn: 300, hets: 36, hetn: 6, rs: 6, defx: 690, defy: 750 },
		{ name: "Hippopodius hippopus", istip: true, haps: 30, hapn: 200, hets: 84, hetn: 10, rs: 6, defx: 1290, defy: 750 },
		{ name: "Agalma elegans", istip: true, haps: 35, hapn: 17000, hets: 180, hetn: 30, rs: 7.5, defx: 230, defy: 750 },
		{ name: "Nanomia bijuga", istip: true, haps: 22.5, hapn: 4500, hets: 32, hetn: 35, rs: 11, defx: 430, defy: 750}
		
		],

	edges: [
		{ source: 0, target: 1 },
		{ source: 0, target: 3 },
		{ source: 2, target: 4 },
		{ source: 1, target: 2 },
		{ source: 2, target: 5 },
		{ source: 2, target: 6 },
		{ source: 3, target: 7 },
		{ source: 3, target: 8 }
		]

};

var minx = 0;
var maxx = 1300;
var miny = 0;
var maxy = 1000;

var nodes = dataset.nodes;
var links = dataset.edges;

var force = d3.layout.force()
    .nodes(nodes)
    .links(links)
    .size([w, h]);

var xScale = d3.scale.linear()
				.domain([minx, maxx])
				.range([padding, (w*2) - padding]);

var yScale = d3.scale.linear()
				.domain([miny, maxy])
				.range([(h*2) - padding, padding]);

var xAxis = d3.svg.axis()
    .scale(xScale)
    .orient("bottom")
    .ticks(8);

var yAxis = d3.svg.axis()
    .scale(yScale)
    .orient("left")
    .ticks(6);

var svg = d3.select("body").append("svg")
    .attr("width", (w*2)+100) 
    .attr("height", h*2);

var loading = svg.append("text")
    .attr("x", w / 2)
    .attr("y", h / 2)
    .attr("dy", ".35em")
    .style("text-anchor", "middle")
    .text("Simulating. One moment please…");

// Use a timeout to allow the rest of the page to load first.
setTimeout(function() {

  // Run the layout a fixed number of times.
  // The ideal number of times scales with graph complexity.
  // Of course, don't run too long—you'll hang the page!
  force.start();
  for (var i = 18; i > 0; --i) force.tick();
  force.stop();

	svg.selectAll("line")
	      .data(links)
	    .enter().append("line")
	      .attr("x1", function(d) { return xScale(d.source.defx); })
	      .attr("y1", function(d) { return yScale(d.source.defy); })
	      .attr("x2", function(d) { return xScale(d.target.defx); })
	      .attr("y2", function(d) { return yScale(d.target.defy); });

  svg.selectAll("circle")
      .data(nodes)
    .enter().append("circle")
      .attr("cx", function(d) { return xScale(d.defx); })
      .attr("cy", function(d) { return yScale(d.defy); })
      .attr("r", function(d) {if (d.istip == false) {return 4;} else {
        return 10;}})
      .attr("fill", function(d) { return colors[d.name]; })
      .attr("opacity", 0.8);

  svg.selectAll("text.lab")
   		.data(nodes)
   		.enter()
   		.append("text")
		.text(function(d) {return d.name;})
		.attr("class", "lab")
		.attr("x", function(d) {return xScale(d.defx);})
   		.attr("y", function(d) {return yScale(d.defy);})
		.attr("font-family", "arial-black")
   		.style("font-size", function(d) {if (d.istip == false) {return "10px";} else {
        return "14px";}})
   		.attr("fill", function(d) {if (d.istip == false) {return "grey";} else {
        return "black";}});

    svg.append("g")
   		.attr("class", "x axis")
   		.attr("transform", "translate(0," + (h*2 - padding) + ")")
   		.call(xAxis);

   	svg.append("g")
    .attr("class", "y axis")
    .attr("transform", "translate(" + padding + ",0)")
    .call(yAxis);

    svg.selectAll("text.axx")
    	.data(nodes)
    	.enter()
    	.append("text")
    	.text("Species")
    	.attr("class", "axx")
    	.attr("x", w)
   		.attr("y", h*1.95)
		.style("font-family", "arial")
   		.style("font-size", "13px")
   		.attr("fill", "black");

   	svg.selectAll("text.axy")
   		.data(nodes)
   		.enter()
   		.append("text")
    	.text("Evolutionary time (arbitrary)")
    	.attr("class","axy")
    	.attr("x", 10 + padding)
   		.attr("y", h)
		.style("font-family", "arial")
   		.style("font-size", "13px")
   		.attr("fill", "black")
   		.attr("transform", "rotate(-90 10 500)");


   	d3.select("h3.hets_x").on("click", function() {
   		durac = 2000;
	maxx = 180;
	xScale.domain([0, maxx]);
	
	
	svg.selectAll("circle")
			.data(nodes)
			.transition().duration(durac/2).ease("cubic-in-out").delay(100)
			.attr("cx", function(d) {return xScale(d.hets);});

   	svg.selectAll("line")
	      .data(links)
	      .transition().duration(durac/2).ease("cubic-in-out").delay(100)
	      .attr("x1", function(d) { return xScale(d.source.hets); })
	      .attr("x2", function(d) { return xScale(d.target.hets); });
   			
   	svg.selectAll("text.lab")
	   		.data(nodes)
	   		.transition().duration(durac/2).ease("cubic-in-out").delay(100)
	   		.attr("x", function(d) {return xScale(d.hets);});


   	xAxis.scale(xScale); 

   			//Update x-axis
		svg.select(".x.axis")
			.transition()
			.duration(durac/3)
			.call(xAxis);


		svg.selectAll("text.axx")
			.data(nodes)
			.text("Heteroneme size (microns)");

});

   	d3.select("h3.haps_x").on("click", function() {
   		durac = 2000;
	maxx = 52.5;
	xScale.domain([0, maxx]);
	
	
	svg.selectAll("circle")
			.data(nodes)
			.transition().duration(durac/2).ease("cubic-in-out").delay(100)
			.attr("cx", function(d) {return xScale(d.haps);});

   	svg.selectAll("line")
	      .data(links)
	      .transition().duration(durac/2).ease("cubic-in-out").delay(100)
	      .attr("x1", function(d) { return xScale(d.source.haps); })
	      .attr("x2", function(d) { return xScale(d.target.haps); });
   			
   	svg.selectAll("text.lab")
	   		.data(nodes)
	   		.transition().duration(durac/2).ease("cubic-in-out").delay(100)
	   		.attr("x", function(d) {return xScale(d.haps);});


   	xAxis.scale(xScale); 

   			//Update x-axis
		svg.select(".x.axis")
			.transition()
			.duration(durac/3)
			.call(xAxis);


		svg.selectAll("text.axx")
			.data(nodes)
			.text("Haploneme size (microns)");

});

d3.select("h3.rs_x").on("click", function() {
   	durac = 2000;
	maxx = 23;

	xScale.domain([0, maxx]);
	
	svg.selectAll("circle")
			.data(nodes)
			.transition().duration(durac/2).ease("cubic-in-out").delay(100)
			.attr("cx", function(d) {return xScale(d.rs);});

   	svg.selectAll("line")
	      .data(links)
	      .transition().duration(durac/2).ease("cubic-in-out").delay(100)
	      .attr("x1", function(d) { return xScale(d.source.rs); })
	      .attr("x2", function(d) { return xScale(d.target.rs); });

   			
   	svg.selectAll("text.lab")
	   		.data(nodes)
	   		.transition().duration(durac/2).ease("cubic-in-out").delay(100)
	   		.attr("x", function(d) {return xScale(d.rs);});


   	xAxis.scale(xScale);


		//Update y-axis
		svg.select(".x.axis")
			.transition()
			.duration(durac/3)
			.call(xAxis);

		svg.selectAll("text.axx")
			.data(nodes)
			.text("Rhopaloneme size (microns)");

});

d3.select("h3.hapn_y").on("click", function() {
   	durac = 2000;
	maxy = 17000;

	yScale.domain([0, maxy]);
	
	svg.selectAll("circle")
			.data(nodes)
			.transition().duration(durac/2).ease("cubic-in-out").delay(100)
			.attr("cy", function(d) {return yScale(d.hapn);});

   	svg.selectAll("line")
	      .data(links)
	      .transition().duration(durac/2).ease("cubic-in-out").delay(100)
	      .attr("y1", function(d) { return yScale(d.source.hapn); })
	      .attr("y2", function(d) { return yScale(d.target.hapn); });

   			
   	svg.selectAll("text.lab")
	   		.data(nodes)
	   		.transition().duration(durac/2).ease("cubic-in-out").delay(100)
	   		.attr("y", function(d) {return yScale(d.hapn);});


   	yAxis.scale(yScale);


		//Update y-axis
		svg.select(".y.axis")
			.transition()
			.duration(durac/3)
			.call(yAxis);

		svg.selectAll("text.axy")
			.data(nodes)
			.text("Haploneme number");

});

d3.select("h3.hetn_y").on("click", function() {
   	durac = 2000;
	maxy = 35;

	yScale.domain([0, maxy]);
	
	svg.selectAll("circle")
			.data(nodes)
			.transition().duration(durac/2).ease("cubic-in-out").delay(100)
			.attr("cy", function(d) {return yScale(d.hetn);});

   	svg.selectAll("line")
	      .data(links)
	      .transition().duration(durac/2).ease("cubic-in-out").delay(100)
	      .attr("y1", function(d) { return yScale(d.source.hetn); })
	      .attr("y2", function(d) { return yScale(d.target.hetn); });

   			
   	svg.selectAll("text.lab")
	   		.data(nodes)
	   		.transition().duration(durac/2).ease("cubic-in-out").delay(100)
	   		.attr("y", function(d) {return yScale(d.hetn);});


   	yAxis.scale(yScale);


		//Update y-axis
		svg.select(".y.axis")
			.transition()
			.duration(durac/3)
			.call(yAxis);

		svg.selectAll("text.axy")
			.data(nodes)
			.text("Heteroneme number");

});

  loading.remove();
}, 10);

</script>
</body>
</html>


## The data

The data includes node-parent realtionships, species names, determination of tip or node class, 5 quantitative cnidomic variables.
The parent node cnidomic variables were reconstructed using the mean values from the descendant nodes/tips.
Branch length will be flexibly adjusted by the x,y position of the nodes/tips.

- Data source:

	Trait measurements: Purcell, J. E. (1984). The functions of nematocysts in prey capture by epipelagic siphonophores (Coelenterata, Hydrozoa). The Biological Bulletin, 166(2), 310-327.


	Phylogenetic relationships: Dunn, C. W., Pugh, P. R., & Haddock, S. H. (2005). Molecular phylogenetics of the Siphonophora (Cnidaria), with implications for the evolution of functional specialization. Systematic Biology, 54(6), 916-935.

- Data structure: 

	Nodes:"name" species or clade name,"istip" whether if internal node or species,"Haploneme size (microns)","Haploneme number","Heteroneme size (microns)","Heteroneme number","Rhopaloneme size (microns)"


	Edges: Branches. Relationships between parent nodes and descendent nodes.

var dataset = {

	nodes: [
		{ name: "Codonophora", istip: false, haps: 27.5, hapn: 5487.5, hets: 89, hetn: 20.75, rs: 7.625},
		{ name: "Calycophorae", istip: false, haps: 26.25, hapn: 225, hets: 72, hetn: 9, rs: 6},
		{ name: "Diphyidae", istip: false, haps: 22.5, hapn: 250, hets: 60, hetn: 8, rs: 6},
		{ name: "Physonectae", istip: false, haps: 28.75, hapn: 10750, hets: 106, hetn: 32.5, rs: 9.25},
		{ name: "Abylopsis tetragona", istip: true, haps: 52.5, hapn: 800, hets: 155, hetn: 21, rs: 23},
		{ name: "Muggiaea atlantica", istip: true, haps: 15, hapn: 300, hets: 36, hetn: 6, rs: 6},
		{ name: "Hippopodius hippopus", istip: true, haps: 30, hapn: 200, hets: 84, hetn: 10, rs: 6},
		{ name: "Agalma elegans", istip: true, haps: 35, hapn: 17000, hets: 180, hetn: 30, rs: 7.5},
		{ name: "Nanomia bijuga", istip: true, haps: 22.5, hapn: 4500, hets: 32, hetn: 35, rs: 11}
		
		],

	edges: [
		{ source: 0, target: 1 },
		{ source: 0, target: 3 },
		{ source: 2, target: 4 },
		{ source: 1, target: 2 },
		{ source: 2, target: 5 },
		{ source: 2, target: 6 },
		{ source: 3, target: 7 },
		{ source: 3, target: 8 }
		]

};


## Background

Phylogenetic trees have been around since the 19th century, and naturalists have been tagging the species (tips) with relevant biological information to understand the evolutionary patterns and the nature of the clades.


Software like Mesquite or ggplot allows to trace particular characters, mapped as colors with a key, to tips and branches of tree after performing reconstructions using maximum parsimony or other models.


The concept of a phylomorphospace arises for the first time in the R package ['phytools'](http://www.inside-r.org/packages/cran/phytools/docs/phylomorphospace) .


It allows the plotting of a static scatterplot for two traits as present in a set of species (the dots) connected by branches and nodes of trivial length and position that represent the phylogenetic relationships between those species. If the author wants to add the branch length, a color gradient scale is included.

![Alt text](http://4.bp.blogspot.com/-mj1toWvpbjs/Ud3G9IX-XRI/AAAAAAAAChA/CUEOYifsVNY/s1600/time-phylomorphospace-2.png)

This approach produces a static image, the user (reader of the document containing the figure) has no ability to select what traits to contrast. 
It would require the utilization of more space in the form of multiple contiguous plots to show all the possible relationships.
The goal of this project is to provide the user with an interactive option to visualize phylomorphospaces.

## This project

### Mapping of data to aesthetics

Each node/tip is a circle, of fixed radius. The fill will be determined by a dictionary of colors dependent on the species name.


Each node is accompanied by a text label. Its content is the species/clade name.


X, Y position of node/tips and text labels represent two cnidomic variables on demand of the user.


Branch length represents the phenotypic distance between 2 nodes (internal and/or species) in the 2 components selected.


The axes are also scaled and updated with the cnidomic variables selected. They are labelled with the name of the variables selected.


### Filtering

The quantitative values plotted are a filtered subset of 2 properties that the user demands. 
The goal of filtering is to answer concrete questions about the relationship of each two variables.


Two more cnidomic variables could be represented by the radius and the fill color of the nodes. However, this idea would clutter the plot with excess information at a time, therefore a filtering 
2-at-a-time on demand approach is taken.

### Extra ink

The header and initial paragraph are not data-ink, but they are useful to explain the rationale of the project to the user, and give instruction on how to interact with it.

There are button elements that the user clicks on (event listeners). They provide a clear menu for interaction with the user.

Species identity is mapped as a color (fill) and a name tag (text), to aid the user in following the continuity of each transition.

### Motion

Motion serves the purpose of maintaining the continuity of each circle (species) identity as its position changes with the new cnidomic variables represented in its X,Y.

### Perspective

To what extent is perspective (eg mappings) controlled by users vs hard coded in advance? How does this project aid in exploration vs exposition?

## Assessment

Was the new visualization successful at providing insight that was not possible or more difficult with previous approaches?

What are the main limitations of new approach?

What are future directions this could go in?


