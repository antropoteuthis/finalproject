# Final Project - Interactive Siphonophore Cnidomic Phylomorphospace

## Introduction

This is a final project for the [Interacting with Data](https://github.com/Brown-BIOL2430-S04-Fall2015/syllabus) seminar in fall 2015. This project targets the representation of dependence relationships between quantitative cnidomic traits in siphonophore species, while simultaneously keeping track of the phylogenetic relationships between the species. It will alternate views of the data by shifting the variables plotted in the scatterplot on demand, using movement and color to maintain the continuity of the identity of the species. A node-hinged polyline will connect the dots as they move through the phenotypic hyperspace.

To view this project, ... (embed visualization here or provide instructions on how to view the project).

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


