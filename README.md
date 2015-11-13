# Final Project - Interactive Siphonophore Cnidomic Phylomorphospace

## Introduction

This is a final project for the [Interacting with Data](https://github.com/Brown-BIOL2430-S04-Fall2015/syllabus) seminar in fall 2015. This project targets the representation of dependence relationships between quantitative traits in 10 siphonophore species, while simultaneously keeping track of the phylogenetic relationships between the species. It will alternate views of the data by shifting the variables plotted in the scatterplot on demand, using movement and color to maintain the continuity of the identity of the species. A node-hinged polyline will connect the dots as they move through the phenotypic hyperspace using a force layout.

[Click here to access visualization](https://rawgit.com/antropoteuthis/finalproject/master/ISCPhylomorphospace_expanded.html)

Instructions are available within the visualization.


## The data

The data includes node-parent realtionships, species names, determination of tip or node class, 5 quantitative variables (cnidoband length, nematocyst sizes and numbers, prey size).
The parent node variables were reconstructed using the mean values from the descendant nodes/tips.
Branch length will be flexibly adjusted by the x,y position of the nodes/tips.

- Data source:

	Trait measurements: Purcell, J. E. (1984). The functions of nematocysts in prey capture by epipelagic siphonophores (Coelenterata, Hydrozoa). *The Biological Bulletin, 166(2), 310-327.*


	Phylogenetic relationships: Dunn, C. W., Pugh, P. R., & Haddock, S. H. (2005). Molecular phylogenetics of the Siphonophora (Cnidaria), with implications for the evolution of functional specialization. *Systematic Biology, 54(6), 916-935.*

- Data structure: 

	Node attributes: "name" species or clade name,"istip" whether if internal node or species, "Cnidoband length (um)" in the longest dimension, while still coiled (if coiled), Haploneme size (microns)","Haploneme number","Heteroneme size (microns)","Heteroneme number","Rhopaloneme size (microns)", "Prey size (mm)" length in the longest dimension of the copepod prey found in the gastrozooids.


		nodes: [
			{name: "Codonophora", istip: false, defx: 710, defy: 100, cbl: 249.88, haps: 26.94, hapn: 2517.19, hets: 67.06, hetn: 21.09, rs: 8.83, ps: 0.93 }, 
			{name: "Calycophorae", istip: false, defx: 960, defy: 250, cbl: 116.25, haps: 24.81, hapn: 184.38, hets: 71.88, hetn: 8.44, rs: 6.59, ps: 0.71 }, 
			{name: " ", istip: false, defx: 1010, defy: 400, cbl: 136.50, haps: 19.63, hapn: 168.75, hets: 59.75, hetn: 6.88, rs: 7.19, ps: 0.56 }, 
			{name: "Diphyidae", istip: false, defx: 1060, defy: 550, cbl: 225.00, haps: 27.25, hapn: 287.50, hets: 83.50, hetn: 9.75, rs: 10.38, ps: 0.76 }, 
			{name: " ", istip: false, defx: 960, defy: 700, cbl: 117.00, haps: 17.50, hapn: 250.00, hets: 41.75, hetn: 7.00, rs: 6.75, ps: 0.47 }, 
			{name: " ", istip: false, defx: 1160, defy: 700, cbl: 333.00, haps: 37.00, hapn: 325.00, hets: 125.25, hetn: 12.50, rs: 14.00, ps: 1.05 }, 
			{name: "Physonectae", istip: false, defx: 450, defy: 250, cbl: 383.50, haps: 29.06, hapn: 4850.00, hets: 62.25, hetn: 33.75, rs: 11.06, ps: 1.15 }, 
			{name: "Agalmatidae", istip: false, defx: 360, defy: 700, cbl: 347.00, haps: 28.13, hapn: 6700.00, hets: 86.50, hetn: 37.50, rs: 9.13, ps: 1.13 }, 
			{name: " ", istip: false, defx: 310, defy: 750, cbl: 249.00, haps: 33.75, hapn: 8900.00, hets: 141.00, hetn: 40.00, rs: 7.25, ps: 1.09 }, 
			{name: "Diphyes dispar", istip: true, defx: 1210, defy: 850, cbl: 270.00, haps: 20.00, hapn: 250.00, hets: 97.50, hetn: 12.00, rs: 15.00, ps: 0.99 }, 
			{name: "Abyla trigona", istip: true, defx: 1120, defy: 850, cbl: 396.00, haps: 54.00, hapn: 400.00, hets: 153.00, hetn: 13.00, rs: 13.00, ps: 1.10 }, 
			{name: "Sulculeolaria quadrivalvis", istip: true, defx: 1010, defy: 850, cbl: 114.00, haps: 20.00, hapn: 200.00, hets: 47.50, hetn: 8.00, rs: 7.50, ps: 0.57 }, 
			{name: "Muggiaea atlantica", istip: true, defx: 910, defy: 850, cbl: 120.00, haps: 15.00, hapn: 300.00, hets: 36.00, hetn: 6.00, rs: 6.00, ps: 0.36 }, 
			{name: "Sphaeronectes gracilis", istip: true, defx: 810, defy: 850, cbl: 48.00, haps: 12.00, hapn: 50.00, hets: 36.00, hetn: 4.00, rs: 4.00, ps: 0.36 }, 
			{name: "Hippopodius hippopus", istip: true, defx: 710, defy: 850, cbl: 96.00, haps: 30.00, hapn: 200.00, hets: 84.00, hetn: 10.00, rs: 6.00, ps: 0.86 }, 
			{name: "Forskalia edwardsii", istip: true, defx: 610, defy: 850, cbl: 420.00, haps: 30.00, hapn: 3000.00, hets: 38.00, hetn: 30.00, rs: 13.00, ps: 1.17 }, 
			{name: "Nanomia bijuga", istip: true, defx: 510, defy: 850, cbl: 445.00, haps: 22.50, hapn: 4500.00, hets: 32.00, hetn: 35.00, rs: 11.00, ps: 1.18 }, 
			{name: "Athorybia rosacea", istip: true, defx: 210, defy: 850, cbl: 102.00, haps: 32.50, hapn: 800.00, hets: 102.00, hetn: 50.00, rs: 7.00, ps: 0.84 }, 
			{name: "Agalma elegans", istip: true, defx: 410, defy: 850, cbl: 396.00, haps: 35.00, hapn: 17000.00, hets: 180.00, hetn: 30.00, rs: 7.50, ps: 1.33 }
		    ],

	
	Edges: Branches. Relationships between parent nodes and descendent nodes.

edges: [
			{ source: 0, target: 1 },
			{ source: 1, target: 2 },
			{ source: 2, target: 3 },
			{ source: 3, target: 4 },
			{ source: 3, target: 5 },
			{ source: 0, target: 6 },
			{ source: 6, target: 7 },
			{ source: 7, target: 8 },
			{ source: 5, target: 9 },
			{ source: 5, target: 10 },
			{ source: 4, target: 11 },
			{ source: 4, target: 12 },
			{ source: 2, target: 13 },
			{ source: 1, target: 14 },
			{ source: 6, target: 15 },
			{ source: 7, target: 16 },
			{ source: 8, target: 17 },
			{ source: 8, target: 18 }
		]


## Background

Phylogenetic trees have been around since the 19th century, and naturalists have been tagging the species (tips) with relevant biological information to understand the evolutionary patterns and the nature of the clades.


Software like Mesquite or ggplot allows to trace particular characters, mapped as colors with a key, to tips and branches of tree after performing reconstructions using maximum parsimony or other models.


The concept of a phylomorphospace arises for the first time in the R package ['phytools'](http://www.inside-r.org/packages/cran/phytools/docs/phylomorphospace).


It allows the plotting of a static scatterplot for two traits as present in a set of species (the dots) connected by branches and nodes of trivial length and position that represent the phylogenetic relationships between those species (Figure 1). If the author wants to add the branch length, a color gradient scale is included.

![Alt text](http://4.bp.blogspot.com/-mj1toWvpbjs/Ud3G9IX-XRI/AAAAAAAAChA/CUEOYifsVNY/s1600/time-phylomorphospace-2.png)

Figure 1. Phylomorphospace (Source: [blog.phytools.org](blog.phytools.org). Credit: Liam Revell)

This approach produces a static image, the user (reader of the document containing the figure) has no ability to select what traits to contrast. 
It would require the utilization of more space in the form of multiple contiguous plots to show all the possible relationships.
The goal of this project is to provide the user with an interactive option to visualize phylomorphospaces.

## This project

### Mapping of data to aesthetics

Each node/tip is a circle, of fixed radius. The fill will be determined by a dictionary of colors dependent on the species name.

Each node is accompanied by a text label. Its content is the species/clade name (if available).

The default view (overview) shows a spaced out cladogram with arbitrary X,Y mapping -- Species and nodes are evenly spaced, evolutionary time is shown arbitrarily from the roots to the tips.

On user demand, X, Y position of node/tips and text labels represent two cnidomic variables on demand of the user.

Branch length represents the phenotypic distance between 2 nodes (internal and/or species) in the 2 components selected.

The axes are also scaled and updated with the variables selected. They are labelled with the name of the variables selected.

### Filtering

The quantitative values plotted are a filtered subset of 2 properties that the user demands. 

The goal of filtering is to answer concrete questions about the relationship of each two variables.

Two more cnidomic variables could be represented by the radius and the fill color of the nodes. However, this idea would clutter the plot with excess information at a time, therefore a filtering 2-at-a-time on demand approach is taken.

### Extra ink

The header and initial paragraph are not data-ink, but they are useful to explain the rationale of the project to the user, and give instruction on how to interact with it.

There are button elements that the user clicks on (event listeners). They provide a clear menu for interaction with the user.

Species identity is constantly mapped as a color (fill) and a name tag (text), to aid the user in following the continuity of each transition.

### Motion

Motion serves the purpose of maintaining the continuity of each circle (species) identity as its position changes with the new cnidomic variables represented in its X,Y.

### Perspective

In this project the user has total control on the perspective of observation over the hyperspatial multidimensional morphospace, being abl to rotate it to show any 2 variables at a time.

## Assessment

The new visualization allows a novel way to visualize a siphonophore phylogeny together with morpho-ecological variables combined on user demand.

Limitations: It can only show 2 variables at a time. It does not show an acurate representation of evolutionary time of rates of change along the branches.

Future directions: A 3D visualization which the user could rotate 360º would provide more simultaneous information about variable relationships. More species and traits will be included after the data acquisition process of my PhD work. With a molecular clock it would be possible in the future to obtain evolutionary time data to plot on the branches as a color gradient.

## License

This visualization is distributed under the GNU General Public License version 3. For more information, see LICENSE or visit: http://www.gnu.org/licenses/gpl.html

## Acknowledgements

This visualization is a tribute to the invaluable work of Dr. Jennifer Purcell on siphonophore cnidomics and trophic ecology that has inspired me to pursue my career in ecoevolutionary planktology.