cola Report for recount2:SRP029880
==================

**Date**: 2019-12-25 23:50:35 CET, **cola version**: 1.3.2

----------------------------------------------------------------

<style type='text/css'>

body, td, th {
   font-family: Arial,Helvetica,sans-serif;
   background-color: white;
   font-size: 13px;
  max-width: 800px;
  margin: auto;
  margin-left:210px;
  padding: 0px 10px 0px 10px;
  border-left: 1px solid #EEEEEE;
  line-height: 150%;
}

tt, code, pre {
   font-family: 'DejaVu Sans Mono', 'Droid Sans Mono', 'Lucida Console', Consolas, Monaco, 

monospace;
}

h1 {
   font-size:2.2em;
}

h2 {
   font-size:1.8em;
}

h3 {
   font-size:1.4em;
}

h4 {
   font-size:1.0em;
}

h5 {
   font-size:0.9em;
}

h6 {
   font-size:0.8em;
}

a {
  text-decoration: none;
  color: #0366d6;
}

a:hover {
  text-decoration: underline;
}

a:visited {
   color: #0366d6;
}

pre, img {
  max-width: 100%;
}
pre {
  overflow-x: auto;
}
pre code {
   display: block; padding: 0.5em;
}

code {
  font-size: 92%;
  border: 1px solid #ccc;
}

code[class] {
  background-color: #F8F8F8;
}

table, td, th {
  border: 1px solid #ccc;
}

blockquote {
   color:#666666;
   margin:0;
   padding-left: 1em;
   border-left: 0.5em #EEE solid;
}

hr {
   height: 0px;
   border-bottom: none;
   border-top-width: thin;
   border-top-style: dotted;
   border-top-color: #999999;
}

@media print {
   * {
      background: transparent !important;
      color: black !important;
      filter:none !important;
      -ms-filter: none !important;
   }

   body {
      font-size:12pt;
      max-width:100%;
   }

   a, a:visited {
      text-decoration: underline;
   }

   hr {
      visibility: hidden;
      page-break-before: always;
   }

   pre, blockquote {
      padding-right: 1em;
      page-break-inside: avoid;
   }

   tr, img {
      page-break-inside: avoid;
   }

   img {
      max-width: 100% !important;
   }

   @page :left {
      margin: 15mm 20mm 15mm 10mm;
   }

   @page :right {
      margin: 15mm 10mm 15mm 20mm;
   }

   p, h2, h3 {
      orphans: 3; widows: 3;
   }

   h2, h3 {
      page-break-after: avoid;
   }
}
</style>




## Summary





All available functions which can be applied to this `res_list` object:


```r
res_list
```

```
#> A 'ConsensusPartitionList' object with 24 methods.
#>   On a matrix with 17171 rows and 54 columns.
#>   Top rows are extracted by 'SD, CV, MAD, ATC' methods.
#>   Subgroups are detected by 'hclust, kmeans, skmeans, pam, mclust, NMF' method.
#>   Number of partitions are tried for k = 2, 3, 4, 5, 6.
#>   Performed in total 30000 partitions by row resampling.
#> 
#> Following methods can be applied to this 'ConsensusPartitionList' object:
#>  [1] "cola_report"           "collect_classes"       "collect_plots"         "collect_stats"        
#>  [5] "colnames"              "functional_enrichment" "get_anno_col"          "get_anno"             
#>  [9] "get_classes"           "get_matrix"            "get_membership"        "get_stats"            
#> [13] "is_best_k"             "is_stable_k"           "ncol"                  "nrow"                 
#> [17] "rownames"              "show"                  "suggest_best_k"        "test_to_known_factors"
#> [21] "top_rows_heatmap"      "top_rows_overlap"     
#> 
#> You can get result for a single method by, e.g. object["SD", "hclust"] or object["SD:hclust"]
#> or a subset of methods by object[c("SD", "CV")], c("hclust", "kmeans")]
```

The call of `run_all_consensus_partition_methods()` was:


```
#> run_all_consensus_partition_methods(data = mat, mc.cores = 4)
```

Dimension of the input matrix:


```r
mat = get_matrix(res_list)
dim(mat)
```

```
#> [1] 17171    54
```

### Density distribution

The density distribution for each sample is visualized as in one column in the
following heatmap. The clustering is based on the distance which is the
Kolmogorov-Smirnov statistic between two distributions.




```r
library(ComplexHeatmap)
densityHeatmap(mat, ylab = "value", cluster_columns = TRUE, show_column_names = FALSE,
    mc.cores = 4)
```

![plot of chunk density-heatmap](figure_cola/density-heatmap-1.png)





### Suggest the best k



Folowing table shows the best `k` (number of partitions) for each combination
of top-value methods and partition methods. Clicking on the method name in
the table goes to the section for a single combination of methods.

[The cola vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13)
explains the definition of the metrics used for determining the best
number of partitions.


```r
suggest_best_k(res_list)
```


|                            | The best k| 1-PAC| Mean silhouette| Concordance|   |Optional k |
|:---------------------------|----------:|-----:|---------------:|-----------:|:--|:----------|
|[SD:kmeans](#SD-kmeans)     |          2| 1.000|           0.977|       0.985|** |           |
|[CV:NMF](#CV-NMF)           |          2| 1.000|           0.975|       0.990|** |           |
|[MAD:hclust](#MAD-hclust)   |          3| 1.000|           0.964|       0.983|** |           |
|[MAD:kmeans](#MAD-kmeans)   |          2| 1.000|           1.000|       1.000|** |           |
|[MAD:pam](#MAD-pam)         |          2| 1.000|           1.000|       1.000|** |           |
|[MAD:mclust](#MAD-mclust)   |          2| 1.000|           0.974|       0.989|** |           |
|[ATC:hclust](#ATC-hclust)   |          3| 1.000|           0.987|       0.994|** |2          |
|[ATC:skmeans](#ATC-skmeans) |          3| 1.000|           0.958|       0.983|** |2          |
|[ATC:mclust](#ATC-mclust)   |          3| 1.000|           0.994|       0.997|** |           |
|[ATC:NMF](#ATC-NMF)         |          2| 1.000|           0.974|       0.991|** |           |
|[SD:pam](#SD-pam)           |          4| 0.961|           0.936|       0.971|** |2,3        |
|[CV:pam](#CV-pam)           |          3| 0.951|           0.907|       0.963|** |           |
|[MAD:NMF](#MAD-NMF)         |          4| 0.944|           0.907|       0.955|*  |2,3        |
|[CV:skmeans](#CV-skmeans)   |          4| 0.940|           0.922|       0.966|*  |2,3        |
|[SD:NMF](#SD-NMF)           |          4| 0.929|           0.900|       0.954|*  |2,3        |
|[ATC:pam](#ATC-pam)         |          5| 0.921|           0.919|       0.966|*  |2,4        |
|[MAD:skmeans](#MAD-skmeans) |          3| 0.909|           0.929|       0.962|*  |2          |
|[ATC:kmeans](#ATC-kmeans)   |          3| 0.904|           0.932|       0.968|*  |2          |
|[SD:skmeans](#SD-skmeans)   |          4| 0.902|           0.861|       0.937|*  |2,3        |
|[CV:mclust](#CV-mclust)     |          4| 0.887|           0.893|       0.928|   |           |
|[CV:hclust](#CV-hclust)     |          4| 0.839|           0.882|       0.920|   |           |
|[SD:mclust](#SD-mclust)     |          4| 0.800|           0.899|       0.920|   |           |
|[CV:kmeans](#CV-kmeans)     |          2| 0.633|           0.936|       0.956|   |           |
|[SD:hclust](#SD-hclust)     |          3| 0.598|           0.829|       0.885|   |           |

\*\*: 1-PAC > 0.95, \*: 1-PAC > 0.9




### CDF of consensus matrices

Cumulative distribution function curves of consensus matrix for all methods.




```r
collect_plots(res_list, fun = plot_ecdf)
```

![plot of chunk collect-plots](figure_cola/collect-plots-1.png)



### Consensus heatmap

Consensus heatmaps for all methods. ([What is a consensus heatmap?](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_9))


<style type='text/css'>



.ui-helper-hidden {
	display: none;
}
.ui-helper-hidden-accessible {
	border: 0;
	clip: rect(0 0 0 0);
	height: 1px;
	margin: -1px;
	overflow: hidden;
	padding: 0;
	position: absolute;
	width: 1px;
}
.ui-helper-reset {
	margin: 0;
	padding: 0;
	border: 0;
	outline: 0;
	line-height: 1.3;
	text-decoration: none;
	font-size: 100%;
	list-style: none;
}
.ui-helper-clearfix:before,
.ui-helper-clearfix:after {
	content: "";
	display: table;
	border-collapse: collapse;
}
.ui-helper-clearfix:after {
	clear: both;
}
.ui-helper-zfix {
	width: 100%;
	height: 100%;
	top: 0;
	left: 0;
	position: absolute;
	opacity: 0;
	filter:Alpha(Opacity=0); 
}

.ui-front {
	z-index: 100;
}



.ui-state-disabled {
	cursor: default !important;
	pointer-events: none;
}



.ui-icon {
	display: inline-block;
	vertical-align: middle;
	margin-top: -.25em;
	position: relative;
	text-indent: -99999px;
	overflow: hidden;
	background-repeat: no-repeat;
}

.ui-widget-icon-block {
	left: 50%;
	margin-left: -8px;
	display: block;
}




.ui-widget-overlay {
	position: fixed;
	top: 0;
	left: 0;
	width: 100%;
	height: 100%;
}
.ui-accordion .ui-accordion-header {
	display: block;
	cursor: pointer;
	position: relative;
	margin: 2px 0 0 0;
	padding: .5em .5em .5em .7em;
	font-size: 100%;
}
.ui-accordion .ui-accordion-content {
	padding: 1em 2.2em;
	border-top: 0;
	overflow: auto;
}
.ui-autocomplete {
	position: absolute;
	top: 0;
	left: 0;
	cursor: default;
}
.ui-menu {
	list-style: none;
	padding: 0;
	margin: 0;
	display: block;
	outline: 0;
}
.ui-menu .ui-menu {
	position: absolute;
}
.ui-menu .ui-menu-item {
	margin: 0;
	cursor: pointer;
	
	list-style-image: url("data:image/gif;base64,R0lGODlhAQABAIAAAAAAAP///yH5BAEAAAAALAAAAAABAAEAAAIBRAA7");
}
.ui-menu .ui-menu-item-wrapper {
	position: relative;
	padding: 3px 1em 3px .4em;
}
.ui-menu .ui-menu-divider {
	margin: 5px 0;
	height: 0;
	font-size: 0;
	line-height: 0;
	border-width: 1px 0 0 0;
}
.ui-menu .ui-state-focus,
.ui-menu .ui-state-active {
	margin: -1px;
}


.ui-menu-icons {
	position: relative;
}
.ui-menu-icons .ui-menu-item-wrapper {
	padding-left: 2em;
}


.ui-menu .ui-icon {
	position: absolute;
	top: 0;
	bottom: 0;
	left: .2em;
	margin: auto 0;
}


.ui-menu .ui-menu-icon {
	left: auto;
	right: 0;
}
.ui-button {
	padding: .4em 1em;
	display: inline-block;
	position: relative;
	line-height: normal;
	margin-right: .1em;
	cursor: pointer;
	vertical-align: middle;
	text-align: center;
	-webkit-user-select: none;
	-moz-user-select: none;
	-ms-user-select: none;
	user-select: none;

	
	overflow: visible;
}

.ui-button,
.ui-button:link,
.ui-button:visited,
.ui-button:hover,
.ui-button:active {
	text-decoration: none;
}


.ui-button-icon-only {
	width: 2em;
	box-sizing: border-box;
	text-indent: -9999px;
	white-space: nowrap;
}


input.ui-button.ui-button-icon-only {
	text-indent: 0;
}


.ui-button-icon-only .ui-icon {
	position: absolute;
	top: 50%;
	left: 50%;
	margin-top: -8px;
	margin-left: -8px;
}

.ui-button.ui-icon-notext .ui-icon {
	padding: 0;
	width: 2.1em;
	height: 2.1em;
	text-indent: -9999px;
	white-space: nowrap;

}

input.ui-button.ui-icon-notext .ui-icon {
	width: auto;
	height: auto;
	text-indent: 0;
	white-space: normal;
	padding: .4em 1em;
}



input.ui-button::-moz-focus-inner,
button.ui-button::-moz-focus-inner {
	border: 0;
	padding: 0;
}
.ui-controlgroup {
	vertical-align: middle;
	display: inline-block;
}
.ui-controlgroup > .ui-controlgroup-item {
	float: left;
	margin-left: 0;
	margin-right: 0;
}
.ui-controlgroup > .ui-controlgroup-item:focus,
.ui-controlgroup > .ui-controlgroup-item.ui-visual-focus {
	z-index: 9999;
}
.ui-controlgroup-vertical > .ui-controlgroup-item {
	display: block;
	float: none;
	width: 100%;
	margin-top: 0;
	margin-bottom: 0;
	text-align: left;
}
.ui-controlgroup-vertical .ui-controlgroup-item {
	box-sizing: border-box;
}
.ui-controlgroup .ui-controlgroup-label {
	padding: .4em 1em;
}
.ui-controlgroup .ui-controlgroup-label span {
	font-size: 80%;
}
.ui-controlgroup-horizontal .ui-controlgroup-label + .ui-controlgroup-item {
	border-left: none;
}
.ui-controlgroup-vertical .ui-controlgroup-label + .ui-controlgroup-item {
	border-top: none;
}
.ui-controlgroup-horizontal .ui-controlgroup-label.ui-widget-content {
	border-right: none;
}
.ui-controlgroup-vertical .ui-controlgroup-label.ui-widget-content {
	border-bottom: none;
}


.ui-controlgroup-vertical .ui-spinner-input {

	
	width: 75%;
	width: calc( 100% - 2.4em );
}
.ui-controlgroup-vertical .ui-spinner .ui-spinner-up {
	border-top-style: solid;
}

.ui-checkboxradio-label .ui-icon-background {
	box-shadow: inset 1px 1px 1px #ccc;
	border-radius: .12em;
	border: none;
}
.ui-checkboxradio-radio-label .ui-icon-background {
	width: 16px;
	height: 16px;
	border-radius: 1em;
	overflow: visible;
	border: none;
}
.ui-checkboxradio-radio-label.ui-checkboxradio-checked .ui-icon,
.ui-checkboxradio-radio-label.ui-checkboxradio-checked:hover .ui-icon {
	background-image: none;
	width: 8px;
	height: 8px;
	border-width: 4px;
	border-style: solid;
}
.ui-checkboxradio-disabled {
	pointer-events: none;
}
.ui-datepicker {
	width: 17em;
	padding: .2em .2em 0;
	display: none;
}
.ui-datepicker .ui-datepicker-header {
	position: relative;
	padding: .2em 0;
}
.ui-datepicker .ui-datepicker-prev,
.ui-datepicker .ui-datepicker-next {
	position: absolute;
	top: 2px;
	width: 1.8em;
	height: 1.8em;
}
.ui-datepicker .ui-datepicker-prev-hover,
.ui-datepicker .ui-datepicker-next-hover {
	top: 1px;
}
.ui-datepicker .ui-datepicker-prev {
	left: 2px;
}
.ui-datepicker .ui-datepicker-next {
	right: 2px;
}
.ui-datepicker .ui-datepicker-prev-hover {
	left: 1px;
}
.ui-datepicker .ui-datepicker-next-hover {
	right: 1px;
}
.ui-datepicker .ui-datepicker-prev span,
.ui-datepicker .ui-datepicker-next span {
	display: block;
	position: absolute;
	left: 50%;
	margin-left: -8px;
	top: 50%;
	margin-top: -8px;
}
.ui-datepicker .ui-datepicker-title {
	margin: 0 2.3em;
	line-height: 1.8em;
	text-align: center;
}
.ui-datepicker .ui-datepicker-title select {
	font-size: 1em;
	margin: 1px 0;
}
.ui-datepicker select.ui-datepicker-month,
.ui-datepicker select.ui-datepicker-year {
	width: 45%;
}
.ui-datepicker table {
	width: 100%;
	font-size: .9em;
	border-collapse: collapse;
	margin: 0 0 .4em;
}
.ui-datepicker th {
	padding: .7em .3em;
	text-align: center;
	font-weight: bold;
	border: 0;
}
.ui-datepicker td {
	border: 0;
	padding: 1px;
}
.ui-datepicker td span,
.ui-datepicker td a {
	display: block;
	padding: .2em;
	text-align: right;
	text-decoration: none;
}
.ui-datepicker .ui-datepicker-buttonpane {
	background-image: none;
	margin: .7em 0 0 0;
	padding: 0 .2em;
	border-left: 0;
	border-right: 0;
	border-bottom: 0;
}
.ui-datepicker .ui-datepicker-buttonpane button {
	float: right;
	margin: .5em .2em .4em;
	cursor: pointer;
	padding: .2em .6em .3em .6em;
	width: auto;
	overflow: visible;
}
.ui-datepicker .ui-datepicker-buttonpane button.ui-datepicker-current {
	float: left;
}


.ui-datepicker.ui-datepicker-multi {
	width: auto;
}
.ui-datepicker-multi .ui-datepicker-group {
	float: left;
}
.ui-datepicker-multi .ui-datepicker-group table {
	width: 95%;
	margin: 0 auto .4em;
}
.ui-datepicker-multi-2 .ui-datepicker-group {
	width: 50%;
}
.ui-datepicker-multi-3 .ui-datepicker-group {
	width: 33.3%;
}
.ui-datepicker-multi-4 .ui-datepicker-group {
	width: 25%;
}
.ui-datepicker-multi .ui-datepicker-group-last .ui-datepicker-header,
.ui-datepicker-multi .ui-datepicker-group-middle .ui-datepicker-header {
	border-left-width: 0;
}
.ui-datepicker-multi .ui-datepicker-buttonpane {
	clear: left;
}
.ui-datepicker-row-break {
	clear: both;
	width: 100%;
	font-size: 0;
}


.ui-datepicker-rtl {
	direction: rtl;
}
.ui-datepicker-rtl .ui-datepicker-prev {
	right: 2px;
	left: auto;
}
.ui-datepicker-rtl .ui-datepicker-next {
	left: 2px;
	right: auto;
}
.ui-datepicker-rtl .ui-datepicker-prev:hover {
	right: 1px;
	left: auto;
}
.ui-datepicker-rtl .ui-datepicker-next:hover {
	left: 1px;
	right: auto;
}
.ui-datepicker-rtl .ui-datepicker-buttonpane {
	clear: right;
}
.ui-datepicker-rtl .ui-datepicker-buttonpane button {
	float: left;
}
.ui-datepicker-rtl .ui-datepicker-buttonpane button.ui-datepicker-current,
.ui-datepicker-rtl .ui-datepicker-group {
	float: right;
}
.ui-datepicker-rtl .ui-datepicker-group-last .ui-datepicker-header,
.ui-datepicker-rtl .ui-datepicker-group-middle .ui-datepicker-header {
	border-right-width: 0;
	border-left-width: 1px;
}


.ui-datepicker .ui-icon {
	display: block;
	text-indent: -99999px;
	overflow: hidden;
	background-repeat: no-repeat;
	left: .5em;
	top: .3em;
}
.ui-dialog {
	position: absolute;
	top: 0;
	left: 0;
	padding: .2em;
	outline: 0;
}
.ui-dialog .ui-dialog-titlebar {
	padding: .4em 1em;
	position: relative;
}
.ui-dialog .ui-dialog-title {
	float: left;
	margin: .1em 0;
	white-space: nowrap;
	width: 90%;
	overflow: hidden;
	text-overflow: ellipsis;
}
.ui-dialog .ui-dialog-titlebar-close {
	position: absolute;
	right: .3em;
	top: 50%;
	width: 20px;
	margin: -10px 0 0 0;
	padding: 1px;
	height: 20px;
}
.ui-dialog .ui-dialog-content {
	position: relative;
	border: 0;
	padding: .5em 1em;
	background: none;
	overflow: auto;
}
.ui-dialog .ui-dialog-buttonpane {
	text-align: left;
	border-width: 1px 0 0 0;
	background-image: none;
	margin-top: .5em;
	padding: .3em 1em .5em .4em;
}
.ui-dialog .ui-dialog-buttonpane .ui-dialog-buttonset {
	float: right;
}
.ui-dialog .ui-dialog-buttonpane button {
	margin: .5em .4em .5em 0;
	cursor: pointer;
}
.ui-dialog .ui-resizable-n {
	height: 2px;
	top: 0;
}
.ui-dialog .ui-resizable-e {
	width: 2px;
	right: 0;
}
.ui-dialog .ui-resizable-s {
	height: 2px;
	bottom: 0;
}
.ui-dialog .ui-resizable-w {
	width: 2px;
	left: 0;
}
.ui-dialog .ui-resizable-se,
.ui-dialog .ui-resizable-sw,
.ui-dialog .ui-resizable-ne,
.ui-dialog .ui-resizable-nw {
	width: 7px;
	height: 7px;
}
.ui-dialog .ui-resizable-se {
	right: 0;
	bottom: 0;
}
.ui-dialog .ui-resizable-sw {
	left: 0;
	bottom: 0;
}
.ui-dialog .ui-resizable-ne {
	right: 0;
	top: 0;
}
.ui-dialog .ui-resizable-nw {
	left: 0;
	top: 0;
}
.ui-draggable .ui-dialog-titlebar {
	cursor: move;
}
.ui-draggable-handle {
	-ms-touch-action: none;
	touch-action: none;
}
.ui-resizable {
	position: relative;
}
.ui-resizable-handle {
	position: absolute;
	font-size: 0.1px;
	display: block;
	-ms-touch-action: none;
	touch-action: none;
}
.ui-resizable-disabled .ui-resizable-handle,
.ui-resizable-autohide .ui-resizable-handle {
	display: none;
}
.ui-resizable-n {
	cursor: n-resize;
	height: 7px;
	width: 100%;
	top: -5px;
	left: 0;
}
.ui-resizable-s {
	cursor: s-resize;
	height: 7px;
	width: 100%;
	bottom: -5px;
	left: 0;
}
.ui-resizable-e {
	cursor: e-resize;
	width: 7px;
	right: -5px;
	top: 0;
	height: 100%;
}
.ui-resizable-w {
	cursor: w-resize;
	width: 7px;
	left: -5px;
	top: 0;
	height: 100%;
}
.ui-resizable-se {
	cursor: se-resize;
	width: 12px;
	height: 12px;
	right: 1px;
	bottom: 1px;
}
.ui-resizable-sw {
	cursor: sw-resize;
	width: 9px;
	height: 9px;
	left: -5px;
	bottom: -5px;
}
.ui-resizable-nw {
	cursor: nw-resize;
	width: 9px;
	height: 9px;
	left: -5px;
	top: -5px;
}
.ui-resizable-ne {
	cursor: ne-resize;
	width: 9px;
	height: 9px;
	right: -5px;
	top: -5px;
}
.ui-progressbar {
	height: 2em;
	text-align: left;
	overflow: hidden;
}
.ui-progressbar .ui-progressbar-value {
	margin: -1px;
	height: 100%;
}
.ui-progressbar .ui-progressbar-overlay {
	background: url("data:image/gif;base64,R0lGODlhKAAoAIABAAAAAP///yH/C05FVFNDQVBFMi4wAwEAAAAh+QQJAQABACwAAAAAKAAoAAACkYwNqXrdC52DS06a7MFZI+4FHBCKoDeWKXqymPqGqxvJrXZbMx7Ttc+w9XgU2FB3lOyQRWET2IFGiU9m1frDVpxZZc6bfHwv4c1YXP6k1Vdy292Fb6UkuvFtXpvWSzA+HycXJHUXiGYIiMg2R6W459gnWGfHNdjIqDWVqemH2ekpObkpOlppWUqZiqr6edqqWQAAIfkECQEAAQAsAAAAACgAKAAAApSMgZnGfaqcg1E2uuzDmmHUBR8Qil95hiPKqWn3aqtLsS18y7G1SzNeowWBENtQd+T1JktP05nzPTdJZlR6vUxNWWjV+vUWhWNkWFwxl9VpZRedYcflIOLafaa28XdsH/ynlcc1uPVDZxQIR0K25+cICCmoqCe5mGhZOfeYSUh5yJcJyrkZWWpaR8doJ2o4NYq62lAAACH5BAkBAAEALAAAAAAoACgAAAKVDI4Yy22ZnINRNqosw0Bv7i1gyHUkFj7oSaWlu3ovC8GxNso5fluz3qLVhBVeT/Lz7ZTHyxL5dDalQWPVOsQWtRnuwXaFTj9jVVh8pma9JjZ4zYSj5ZOyma7uuolffh+IR5aW97cHuBUXKGKXlKjn+DiHWMcYJah4N0lYCMlJOXipGRr5qdgoSTrqWSq6WFl2ypoaUAAAIfkECQEAAQAsAAAAACgAKAAAApaEb6HLgd/iO7FNWtcFWe+ufODGjRfoiJ2akShbueb0wtI50zm02pbvwfWEMWBQ1zKGlLIhskiEPm9R6vRXxV4ZzWT2yHOGpWMyorblKlNp8HmHEb/lCXjcW7bmtXP8Xt229OVWR1fod2eWqNfHuMjXCPkIGNileOiImVmCOEmoSfn3yXlJWmoHGhqp6ilYuWYpmTqKUgAAIfkECQEAAQAsAAAAACgAKAAAApiEH6kb58biQ3FNWtMFWW3eNVcojuFGfqnZqSebuS06w5V80/X02pKe8zFwP6EFWOT1lDFk8rGERh1TTNOocQ61Hm4Xm2VexUHpzjymViHrFbiELsefVrn6XKfnt2Q9G/+Xdie499XHd2g4h7ioOGhXGJboGAnXSBnoBwKYyfioubZJ2Hn0RuRZaflZOil56Zp6iioKSXpUAAAh+QQJAQABACwAAAAAKAAoAAACkoQRqRvnxuI7kU1a1UU5bd5tnSeOZXhmn5lWK3qNTWvRdQxP8qvaC+/yaYQzXO7BMvaUEmJRd3TsiMAgswmNYrSgZdYrTX6tSHGZO73ezuAw2uxuQ+BbeZfMxsexY35+/Qe4J1inV0g4x3WHuMhIl2jXOKT2Q+VU5fgoSUI52VfZyfkJGkha6jmY+aaYdirq+lQAACH5BAkBAAEALAAAAAAoACgAAAKWBIKpYe0L3YNKToqswUlvznigd4wiR4KhZrKt9Upqip61i9E3vMvxRdHlbEFiEXfk9YARYxOZZD6VQ2pUunBmtRXo1Lf8hMVVcNl8JafV38aM2/Fu5V16Bn63r6xt97j09+MXSFi4BniGFae3hzbH9+hYBzkpuUh5aZmHuanZOZgIuvbGiNeomCnaxxap2upaCZsq+1kAACH5BAkBAAEALAAAAAAoACgAAAKXjI8By5zf4kOxTVrXNVlv1X0d8IGZGKLnNpYtm8Lr9cqVeuOSvfOW79D9aDHizNhDJidFZhNydEahOaDH6nomtJjp1tutKoNWkvA6JqfRVLHU/QUfau9l2x7G54d1fl995xcIGAdXqMfBNadoYrhH+Mg2KBlpVpbluCiXmMnZ2Sh4GBqJ+ckIOqqJ6LmKSllZmsoq6wpQAAAh+QQJAQABACwAAAAAKAAoAAAClYx/oLvoxuJDkU1a1YUZbJ59nSd2ZXhWqbRa2/gF8Gu2DY3iqs7yrq+xBYEkYvFSM8aSSObE+ZgRl1BHFZNr7pRCavZ5BW2142hY3AN/zWtsmf12p9XxxFl2lpLn1rseztfXZjdIWIf2s5dItwjYKBgo9yg5pHgzJXTEeGlZuenpyPmpGQoKOWkYmSpaSnqKileI2FAAACH5BAkBAAEALAAAAAAoACgAAAKVjB+gu+jG4kORTVrVhRlsnn2dJ3ZleFaptFrb+CXmO9OozeL5VfP99HvAWhpiUdcwkpBH3825AwYdU8xTqlLGhtCosArKMpvfa1mMRae9VvWZfeB2XfPkeLmm18lUcBj+p5dnN8jXZ3YIGEhYuOUn45aoCDkp16hl5IjYJvjWKcnoGQpqyPlpOhr3aElaqrq56Bq7VAAAOw==");
	height: 100%;
	filter: alpha(opacity=25); 
	opacity: 0.25;
}
.ui-progressbar-indeterminate .ui-progressbar-value {
	background-image: none;
}
.ui-selectable {
	-ms-touch-action: none;
	touch-action: none;
}
.ui-selectable-helper {
	position: absolute;
	z-index: 100;
	border: 1px dotted black;
}
.ui-selectmenu-menu {
	padding: 0;
	margin: 0;
	position: absolute;
	top: 0;
	left: 0;
	display: none;
}
.ui-selectmenu-menu .ui-menu {
	overflow: auto;
	overflow-x: hidden;
	padding-bottom: 1px;
}
.ui-selectmenu-menu .ui-menu .ui-selectmenu-optgroup {
	font-size: 1em;
	font-weight: bold;
	line-height: 1.5;
	padding: 2px 0.4em;
	margin: 0.5em 0 0 0;
	height: auto;
	border: 0;
}
.ui-selectmenu-open {
	display: block;
}
.ui-selectmenu-text {
	display: block;
	margin-right: 20px;
	overflow: hidden;
	text-overflow: ellipsis;
}
.ui-selectmenu-button.ui-button {
	text-align: left;
	white-space: nowrap;
	width: 14em;
}
.ui-selectmenu-icon.ui-icon {
	float: right;
	margin-top: 0;
}
.ui-slider {
	position: relative;
	text-align: left;
}
.ui-slider .ui-slider-handle {
	position: absolute;
	z-index: 2;
	width: 1.2em;
	height: 1.2em;
	cursor: default;
	-ms-touch-action: none;
	touch-action: none;
}
.ui-slider .ui-slider-range {
	position: absolute;
	z-index: 1;
	font-size: .7em;
	display: block;
	border: 0;
	background-position: 0 0;
}


.ui-slider.ui-state-disabled .ui-slider-handle,
.ui-slider.ui-state-disabled .ui-slider-range {
	filter: inherit;
}

.ui-slider-horizontal {
	height: .8em;
}
.ui-slider-horizontal .ui-slider-handle {
	top: -.3em;
	margin-left: -.6em;
}
.ui-slider-horizontal .ui-slider-range {
	top: 0;
	height: 100%;
}
.ui-slider-horizontal .ui-slider-range-min {
	left: 0;
}
.ui-slider-horizontal .ui-slider-range-max {
	right: 0;
}

.ui-slider-vertical {
	width: .8em;
	height: 100px;
}
.ui-slider-vertical .ui-slider-handle {
	left: -.3em;
	margin-left: 0;
	margin-bottom: -.6em;
}
.ui-slider-vertical .ui-slider-range {
	left: 0;
	width: 100%;
}
.ui-slider-vertical .ui-slider-range-min {
	bottom: 0;
}
.ui-slider-vertical .ui-slider-range-max {
	top: 0;
}
.ui-sortable-handle {
	-ms-touch-action: none;
	touch-action: none;
}
.ui-spinner {
	position: relative;
	display: inline-block;
	overflow: hidden;
	padding: 0;
	vertical-align: middle;
}
.ui-spinner-input {
	border: none;
	background: none;
	color: inherit;
	padding: .222em 0;
	margin: .2em 0;
	vertical-align: middle;
	margin-left: .4em;
	margin-right: 2em;
}
.ui-spinner-button {
	width: 1.6em;
	height: 50%;
	font-size: .5em;
	padding: 0;
	margin: 0;
	text-align: center;
	position: absolute;
	cursor: default;
	display: block;
	overflow: hidden;
	right: 0;
}

.ui-spinner a.ui-spinner-button {
	border-top-style: none;
	border-bottom-style: none;
	border-right-style: none;
}
.ui-spinner-up {
	top: 0;
}
.ui-spinner-down {
	bottom: 0;
}
.ui-tabs {
	position: relative;
	padding: .2em;
}
.ui-tabs .ui-tabs-nav {
	margin: 0;
	padding: .2em .2em 0;
}
.ui-tabs .ui-tabs-nav li {
	list-style: none;
	float: left;
	position: relative;
	top: 0;
	margin: 1px .2em 0 0;
	border-bottom-width: 0;
	padding: 0;
	white-space: nowrap;
}
.ui-tabs .ui-tabs-nav .ui-tabs-anchor {
	float: left;
	padding: .5em 1em;
	text-decoration: none;
}
.ui-tabs .ui-tabs-nav li.ui-tabs-active {
	margin-bottom: -1px;
	padding-bottom: 1px;
}
.ui-tabs .ui-tabs-nav li.ui-tabs-active .ui-tabs-anchor,
.ui-tabs .ui-tabs-nav li.ui-state-disabled .ui-tabs-anchor,
.ui-tabs .ui-tabs-nav li.ui-tabs-loading .ui-tabs-anchor {
	cursor: text;
}
.ui-tabs-collapsible .ui-tabs-nav li.ui-tabs-active .ui-tabs-anchor {
	cursor: pointer;
}
.ui-tabs .ui-tabs-panel {
	display: block;
	border-width: 0;
	padding: 1em 1.4em;
	background: none;
}
.ui-tooltip {
	padding: 8px;
	position: absolute;
	z-index: 9999;
	max-width: 300px;
}
body .ui-tooltip {
	border-width: 2px;
}

.ui-widget {
	font-family: Arial,Helvetica,sans-serif;
	font-size: 1em;
}
.ui-widget .ui-widget {
	font-size: 1em;
}
.ui-widget input,
.ui-widget select,
.ui-widget textarea,
.ui-widget button {
	font-family: Arial,Helvetica,sans-serif;
	font-size: 1em;
}
.ui-widget.ui-widget-content {
	border: 1px solid #c5c5c5;
}
.ui-widget-content {
	border: 1px solid #dddddd;
	background: #ffffff;
	color: #333333;
}
.ui-widget-content a {
	color: #333333;
}
.ui-widget-header {
	border: 1px solid #dddddd;
	background: #e9e9e9;
	color: #333333;
	font-weight: bold;
}
.ui-widget-header a {
	color: #333333;
}


.ui-state-default,
.ui-widget-content .ui-state-default,
.ui-widget-header .ui-state-default,
.ui-button,


html .ui-button.ui-state-disabled:hover,
html .ui-button.ui-state-disabled:active {
	border: 1px solid #c5c5c5;
	background: #f6f6f6;
	font-weight: normal;
	color: #454545;
}
.ui-state-default a,
.ui-state-default a:link,
.ui-state-default a:visited,
a.ui-button,
a:link.ui-button,
a:visited.ui-button,
.ui-button {
	color: #454545;
	text-decoration: none;
}
.ui-state-hover,
.ui-widget-content .ui-state-hover,
.ui-widget-header .ui-state-hover,
.ui-state-focus,
.ui-widget-content .ui-state-focus,
.ui-widget-header .ui-state-focus,
.ui-button:hover,
.ui-button:focus {
	border: 1px solid #cccccc;
	background: #ededed;
	font-weight: normal;
	color: #2b2b2b;
}
.ui-state-hover a,
.ui-state-hover a:hover,
.ui-state-hover a:link,
.ui-state-hover a:visited,
.ui-state-focus a,
.ui-state-focus a:hover,
.ui-state-focus a:link,
.ui-state-focus a:visited,
a.ui-button:hover,
a.ui-button:focus {
	color: #2b2b2b;
	text-decoration: none;
}

.ui-visual-focus {
	box-shadow: 0 0 3px 1px rgb(94, 158, 214);
}
.ui-state-active,
.ui-widget-content .ui-state-active,
.ui-widget-header .ui-state-active,
a.ui-button:active,
.ui-button:active,
.ui-button.ui-state-active:hover {
	border: 1px solid #003eff;
	background: #007fff;
	font-weight: normal;
	color: #ffffff;
}
.ui-icon-background,
.ui-state-active .ui-icon-background {
	border: #003eff;
	background-color: #ffffff;
}
.ui-state-active a,
.ui-state-active a:link,
.ui-state-active a:visited {
	color: #ffffff;
	text-decoration: none;
}


.ui-state-highlight,
.ui-widget-content .ui-state-highlight,
.ui-widget-header .ui-state-highlight {
	border: 1px solid #dad55e;
	background: #fffa90;
	color: #777620;
}
.ui-state-checked {
	border: 1px solid #dad55e;
	background: #fffa90;
}
.ui-state-highlight a,
.ui-widget-content .ui-state-highlight a,
.ui-widget-header .ui-state-highlight a {
	color: #777620;
}
.ui-state-error,
.ui-widget-content .ui-state-error,
.ui-widget-header .ui-state-error {
	border: 1px solid #f1a899;
	background: #fddfdf;
	color: #5f3f3f;
}
.ui-state-error a,
.ui-widget-content .ui-state-error a,
.ui-widget-header .ui-state-error a {
	color: #5f3f3f;
}
.ui-state-error-text,
.ui-widget-content .ui-state-error-text,
.ui-widget-header .ui-state-error-text {
	color: #5f3f3f;
}
.ui-priority-primary,
.ui-widget-content .ui-priority-primary,
.ui-widget-header .ui-priority-primary {
	font-weight: bold;
}
.ui-priority-secondary,
.ui-widget-content .ui-priority-secondary,
.ui-widget-header .ui-priority-secondary {
	opacity: .7;
	filter:Alpha(Opacity=70); 
	font-weight: normal;
}
.ui-state-disabled,
.ui-widget-content .ui-state-disabled,
.ui-widget-header .ui-state-disabled {
	opacity: .35;
	filter:Alpha(Opacity=35); 
	background-image: none;
}
.ui-state-disabled .ui-icon {
	filter:Alpha(Opacity=35); 
}




.ui-icon {
	width: 16px;
	height: 16px;
}
.ui-icon,
.ui-widget-content .ui-icon {
	background-image: url("images/ui-icons_444444_256x240.png");
}
.ui-widget-header .ui-icon {
	background-image: url("images/ui-icons_444444_256x240.png");
}
.ui-state-hover .ui-icon,
.ui-state-focus .ui-icon,
.ui-button:hover .ui-icon,
.ui-button:focus .ui-icon {
	background-image: url("images/ui-icons_555555_256x240.png");
}
.ui-state-active .ui-icon,
.ui-button:active .ui-icon {
	background-image: url("images/ui-icons_ffffff_256x240.png");
}
.ui-state-highlight .ui-icon,
.ui-button .ui-state-highlight.ui-icon {
	background-image: url("images/ui-icons_777620_256x240.png");
}
.ui-state-error .ui-icon,
.ui-state-error-text .ui-icon {
	background-image: url("images/ui-icons_cc0000_256x240.png");
}
.ui-button .ui-icon {
	background-image: url("images/ui-icons_777777_256x240.png");
}


.ui-icon-blank { background-position: 16px 16px; }
.ui-icon-caret-1-n { background-position: 0 0; }
.ui-icon-caret-1-ne { background-position: -16px 0; }
.ui-icon-caret-1-e { background-position: -32px 0; }
.ui-icon-caret-1-se { background-position: -48px 0; }
.ui-icon-caret-1-s { background-position: -65px 0; }
.ui-icon-caret-1-sw { background-position: -80px 0; }
.ui-icon-caret-1-w { background-position: -96px 0; }
.ui-icon-caret-1-nw { background-position: -112px 0; }
.ui-icon-caret-2-n-s { background-position: -128px 0; }
.ui-icon-caret-2-e-w { background-position: -144px 0; }
.ui-icon-triangle-1-n { background-position: 0 -16px; }
.ui-icon-triangle-1-ne { background-position: -16px -16px; }
.ui-icon-triangle-1-e { background-position: -32px -16px; }
.ui-icon-triangle-1-se { background-position: -48px -16px; }
.ui-icon-triangle-1-s { background-position: -65px -16px; }
.ui-icon-triangle-1-sw { background-position: -80px -16px; }
.ui-icon-triangle-1-w { background-position: -96px -16px; }
.ui-icon-triangle-1-nw { background-position: -112px -16px; }
.ui-icon-triangle-2-n-s { background-position: -128px -16px; }
.ui-icon-triangle-2-e-w { background-position: -144px -16px; }
.ui-icon-arrow-1-n { background-position: 0 -32px; }
.ui-icon-arrow-1-ne { background-position: -16px -32px; }
.ui-icon-arrow-1-e { background-position: -32px -32px; }
.ui-icon-arrow-1-se { background-position: -48px -32px; }
.ui-icon-arrow-1-s { background-position: -65px -32px; }
.ui-icon-arrow-1-sw { background-position: -80px -32px; }
.ui-icon-arrow-1-w { background-position: -96px -32px; }
.ui-icon-arrow-1-nw { background-position: -112px -32px; }
.ui-icon-arrow-2-n-s { background-position: -128px -32px; }
.ui-icon-arrow-2-ne-sw { background-position: -144px -32px; }
.ui-icon-arrow-2-e-w { background-position: -160px -32px; }
.ui-icon-arrow-2-se-nw { background-position: -176px -32px; }
.ui-icon-arrowstop-1-n { background-position: -192px -32px; }
.ui-icon-arrowstop-1-e { background-position: -208px -32px; }
.ui-icon-arrowstop-1-s { background-position: -224px -32px; }
.ui-icon-arrowstop-1-w { background-position: -240px -32px; }
.ui-icon-arrowthick-1-n { background-position: 1px -48px; }
.ui-icon-arrowthick-1-ne { background-position: -16px -48px; }
.ui-icon-arrowthick-1-e { background-position: -32px -48px; }
.ui-icon-arrowthick-1-se { background-position: -48px -48px; }
.ui-icon-arrowthick-1-s { background-position: -64px -48px; }
.ui-icon-arrowthick-1-sw { background-position: -80px -48px; }
.ui-icon-arrowthick-1-w { background-position: -96px -48px; }
.ui-icon-arrowthick-1-nw { background-position: -112px -48px; }
.ui-icon-arrowthick-2-n-s { background-position: -128px -48px; }
.ui-icon-arrowthick-2-ne-sw { background-position: -144px -48px; }
.ui-icon-arrowthick-2-e-w { background-position: -160px -48px; }
.ui-icon-arrowthick-2-se-nw { background-position: -176px -48px; }
.ui-icon-arrowthickstop-1-n { background-position: -192px -48px; }
.ui-icon-arrowthickstop-1-e { background-position: -208px -48px; }
.ui-icon-arrowthickstop-1-s { background-position: -224px -48px; }
.ui-icon-arrowthickstop-1-w { background-position: -240px -48px; }
.ui-icon-arrowreturnthick-1-w { background-position: 0 -64px; }
.ui-icon-arrowreturnthick-1-n { background-position: -16px -64px; }
.ui-icon-arrowreturnthick-1-e { background-position: -32px -64px; }
.ui-icon-arrowreturnthick-1-s { background-position: -48px -64px; }
.ui-icon-arrowreturn-1-w { background-position: -64px -64px; }
.ui-icon-arrowreturn-1-n { background-position: -80px -64px; }
.ui-icon-arrowreturn-1-e { background-position: -96px -64px; }
.ui-icon-arrowreturn-1-s { background-position: -112px -64px; }
.ui-icon-arrowrefresh-1-w { background-position: -128px -64px; }
.ui-icon-arrowrefresh-1-n { background-position: -144px -64px; }
.ui-icon-arrowrefresh-1-e { background-position: -160px -64px; }
.ui-icon-arrowrefresh-1-s { background-position: -176px -64px; }
.ui-icon-arrow-4 { background-position: 0 -80px; }
.ui-icon-arrow-4-diag { background-position: -16px -80px; }
.ui-icon-extlink { background-position: -32px -80px; }
.ui-icon-newwin { background-position: -48px -80px; }
.ui-icon-refresh { background-position: -64px -80px; }
.ui-icon-shuffle { background-position: -80px -80px; }
.ui-icon-transfer-e-w { background-position: -96px -80px; }
.ui-icon-transferthick-e-w { background-position: -112px -80px; }
.ui-icon-folder-collapsed { background-position: 0 -96px; }
.ui-icon-folder-open { background-position: -16px -96px; }
.ui-icon-document { background-position: -32px -96px; }
.ui-icon-document-b { background-position: -48px -96px; }
.ui-icon-note { background-position: -64px -96px; }
.ui-icon-mail-closed { background-position: -80px -96px; }
.ui-icon-mail-open { background-position: -96px -96px; }
.ui-icon-suitcase { background-position: -112px -96px; }
.ui-icon-comment { background-position: -128px -96px; }
.ui-icon-person { background-position: -144px -96px; }
.ui-icon-print { background-position: -160px -96px; }
.ui-icon-trash { background-position: -176px -96px; }
.ui-icon-locked { background-position: -192px -96px; }
.ui-icon-unlocked { background-position: -208px -96px; }
.ui-icon-bookmark { background-position: -224px -96px; }
.ui-icon-tag { background-position: -240px -96px; }
.ui-icon-home { background-position: 0 -112px; }
.ui-icon-flag { background-position: -16px -112px; }
.ui-icon-calendar { background-position: -32px -112px; }
.ui-icon-cart { background-position: -48px -112px; }
.ui-icon-pencil { background-position: -64px -112px; }
.ui-icon-clock { background-position: -80px -112px; }
.ui-icon-disk { background-position: -96px -112px; }
.ui-icon-calculator { background-position: -112px -112px; }
.ui-icon-zoomin { background-position: -128px -112px; }
.ui-icon-zoomout { background-position: -144px -112px; }
.ui-icon-search { background-position: -160px -112px; }
.ui-icon-wrench { background-position: -176px -112px; }
.ui-icon-gear { background-position: -192px -112px; }
.ui-icon-heart { background-position: -208px -112px; }
.ui-icon-star { background-position: -224px -112px; }
.ui-icon-link { background-position: -240px -112px; }
.ui-icon-cancel { background-position: 0 -128px; }
.ui-icon-plus { background-position: -16px -128px; }
.ui-icon-plusthick { background-position: -32px -128px; }
.ui-icon-minus { background-position: -48px -128px; }
.ui-icon-minusthick { background-position: -64px -128px; }
.ui-icon-close { background-position: -80px -128px; }
.ui-icon-closethick { background-position: -96px -128px; }
.ui-icon-key { background-position: -112px -128px; }
.ui-icon-lightbulb { background-position: -128px -128px; }
.ui-icon-scissors { background-position: -144px -128px; }
.ui-icon-clipboard { background-position: -160px -128px; }
.ui-icon-copy { background-position: -176px -128px; }
.ui-icon-contact { background-position: -192px -128px; }
.ui-icon-image { background-position: -208px -128px; }
.ui-icon-video { background-position: -224px -128px; }
.ui-icon-script { background-position: -240px -128px; }
.ui-icon-alert { background-position: 0 -144px; }
.ui-icon-info { background-position: -16px -144px; }
.ui-icon-notice { background-position: -32px -144px; }
.ui-icon-help { background-position: -48px -144px; }
.ui-icon-check { background-position: -64px -144px; }
.ui-icon-bullet { background-position: -80px -144px; }
.ui-icon-radio-on { background-position: -96px -144px; }
.ui-icon-radio-off { background-position: -112px -144px; }
.ui-icon-pin-w { background-position: -128px -144px; }
.ui-icon-pin-s { background-position: -144px -144px; }
.ui-icon-play { background-position: 0 -160px; }
.ui-icon-pause { background-position: -16px -160px; }
.ui-icon-seek-next { background-position: -32px -160px; }
.ui-icon-seek-prev { background-position: -48px -160px; }
.ui-icon-seek-end { background-position: -64px -160px; }
.ui-icon-seek-start { background-position: -80px -160px; }

.ui-icon-seek-first { background-position: -80px -160px; }
.ui-icon-stop { background-position: -96px -160px; }
.ui-icon-eject { background-position: -112px -160px; }
.ui-icon-volume-off { background-position: -128px -160px; }
.ui-icon-volume-on { background-position: -144px -160px; }
.ui-icon-power { background-position: 0 -176px; }
.ui-icon-signal-diag { background-position: -16px -176px; }
.ui-icon-signal { background-position: -32px -176px; }
.ui-icon-battery-0 { background-position: -48px -176px; }
.ui-icon-battery-1 { background-position: -64px -176px; }
.ui-icon-battery-2 { background-position: -80px -176px; }
.ui-icon-battery-3 { background-position: -96px -176px; }
.ui-icon-circle-plus { background-position: 0 -192px; }
.ui-icon-circle-minus { background-position: -16px -192px; }
.ui-icon-circle-close { background-position: -32px -192px; }
.ui-icon-circle-triangle-e { background-position: -48px -192px; }
.ui-icon-circle-triangle-s { background-position: -64px -192px; }
.ui-icon-circle-triangle-w { background-position: -80px -192px; }
.ui-icon-circle-triangle-n { background-position: -96px -192px; }
.ui-icon-circle-arrow-e { background-position: -112px -192px; }
.ui-icon-circle-arrow-s { background-position: -128px -192px; }
.ui-icon-circle-arrow-w { background-position: -144px -192px; }
.ui-icon-circle-arrow-n { background-position: -160px -192px; }
.ui-icon-circle-zoomin { background-position: -176px -192px; }
.ui-icon-circle-zoomout { background-position: -192px -192px; }
.ui-icon-circle-check { background-position: -208px -192px; }
.ui-icon-circlesmall-plus { background-position: 0 -208px; }
.ui-icon-circlesmall-minus { background-position: -16px -208px; }
.ui-icon-circlesmall-close { background-position: -32px -208px; }
.ui-icon-squaresmall-plus { background-position: -48px -208px; }
.ui-icon-squaresmall-minus { background-position: -64px -208px; }
.ui-icon-squaresmall-close { background-position: -80px -208px; }
.ui-icon-grip-dotted-vertical { background-position: 0 -224px; }
.ui-icon-grip-dotted-horizontal { background-position: -16px -224px; }
.ui-icon-grip-solid-vertical { background-position: -32px -224px; }
.ui-icon-grip-solid-horizontal { background-position: -48px -224px; }
.ui-icon-gripsmall-diagonal-se { background-position: -64px -224px; }
.ui-icon-grip-diagonal-se { background-position: -80px -224px; }





.ui-corner-all,
.ui-corner-top,
.ui-corner-left,
.ui-corner-tl {
	border-top-left-radius: 3px;
}
.ui-corner-all,
.ui-corner-top,
.ui-corner-right,
.ui-corner-tr {
	border-top-right-radius: 3px;
}
.ui-corner-all,
.ui-corner-bottom,
.ui-corner-left,
.ui-corner-bl {
	border-bottom-left-radius: 3px;
}
.ui-corner-all,
.ui-corner-bottom,
.ui-corner-right,
.ui-corner-br {
	border-bottom-right-radius: 3px;
}


.ui-widget-overlay {
	background: #aaaaaa;
	opacity: .3;
	filter: Alpha(Opacity=30); 
}
.ui-widget-shadow {
	-webkit-box-shadow: 0px 0px 5px #666666;
	box-shadow: 0px 0px 5px #666666;
} 
</style>
<script src='js/jquery-1.12.4.js'></script>
<script src='js/jquery-ui.js'></script>

<script>
$( function() {
	$( '#tabs-collect-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-collect-consensus-heatmap'>
<ul>
<li><a href='#tab-collect-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-collect-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-collect-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-collect-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-collect-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-collect-consensus-heatmap-1'>
<pre><code class="r">collect_plots(res_list, k = 2, fun = consensus_heatmap, mc.cores = 4)
</code></pre>

<p><img src="figure_cola/tab-collect-consensus-heatmap-1-1.png" alt="plot of chunk tab-collect-consensus-heatmap-1"/></p>

</div>
<div id='tab-collect-consensus-heatmap-2'>
<pre><code class="r">collect_plots(res_list, k = 3, fun = consensus_heatmap, mc.cores = 4)
</code></pre>

<p><img src="figure_cola/tab-collect-consensus-heatmap-2-1.png" alt="plot of chunk tab-collect-consensus-heatmap-2"/></p>

</div>
<div id='tab-collect-consensus-heatmap-3'>
<pre><code class="r">collect_plots(res_list, k = 4, fun = consensus_heatmap, mc.cores = 4)
</code></pre>

<p><img src="figure_cola/tab-collect-consensus-heatmap-3-1.png" alt="plot of chunk tab-collect-consensus-heatmap-3"/></p>

</div>
<div id='tab-collect-consensus-heatmap-4'>
<pre><code class="r">collect_plots(res_list, k = 5, fun = consensus_heatmap, mc.cores = 4)
</code></pre>

<p><img src="figure_cola/tab-collect-consensus-heatmap-4-1.png" alt="plot of chunk tab-collect-consensus-heatmap-4"/></p>

</div>
<div id='tab-collect-consensus-heatmap-5'>
<pre><code class="r">collect_plots(res_list, k = 6, fun = consensus_heatmap, mc.cores = 4)
</code></pre>

<p><img src="figure_cola/tab-collect-consensus-heatmap-5-1.png" alt="plot of chunk tab-collect-consensus-heatmap-5"/></p>

</div>
</div>



### Membership heatmap

Membership heatmaps for all methods. ([What is a membership heatmap?](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_12))


<script>
$( function() {
	$( '#tabs-collect-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-collect-membership-heatmap'>
<ul>
<li><a href='#tab-collect-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-collect-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-collect-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-collect-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-collect-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-collect-membership-heatmap-1'>
<pre><code class="r">collect_plots(res_list, k = 2, fun = membership_heatmap, mc.cores = 4)
</code></pre>

<p><img src="figure_cola/tab-collect-membership-heatmap-1-1.png" alt="plot of chunk tab-collect-membership-heatmap-1"/></p>

</div>
<div id='tab-collect-membership-heatmap-2'>
<pre><code class="r">collect_plots(res_list, k = 3, fun = membership_heatmap, mc.cores = 4)
</code></pre>

<p><img src="figure_cola/tab-collect-membership-heatmap-2-1.png" alt="plot of chunk tab-collect-membership-heatmap-2"/></p>

</div>
<div id='tab-collect-membership-heatmap-3'>
<pre><code class="r">collect_plots(res_list, k = 4, fun = membership_heatmap, mc.cores = 4)
</code></pre>

<p><img src="figure_cola/tab-collect-membership-heatmap-3-1.png" alt="plot of chunk tab-collect-membership-heatmap-3"/></p>

</div>
<div id='tab-collect-membership-heatmap-4'>
<pre><code class="r">collect_plots(res_list, k = 5, fun = membership_heatmap, mc.cores = 4)
</code></pre>

<p><img src="figure_cola/tab-collect-membership-heatmap-4-1.png" alt="plot of chunk tab-collect-membership-heatmap-4"/></p>

</div>
<div id='tab-collect-membership-heatmap-5'>
<pre><code class="r">collect_plots(res_list, k = 6, fun = membership_heatmap, mc.cores = 4)
</code></pre>

<p><img src="figure_cola/tab-collect-membership-heatmap-5-1.png" alt="plot of chunk tab-collect-membership-heatmap-5"/></p>

</div>
</div>



### Signature heatmap

Signature heatmaps for all methods. ([What is a signature heatmap?](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_22))


Note in following heatmaps, rows are scaled.



<script>
$( function() {
	$( '#tabs-collect-get-signatures' ).tabs();
} );
</script>
<div id='tabs-collect-get-signatures'>
<ul>
<li><a href='#tab-collect-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-collect-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-collect-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-collect-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-collect-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-collect-get-signatures-1'>
<pre><code class="r">collect_plots(res_list, k = 2, fun = get_signatures, mc.cores = 4)
</code></pre>

<p><img src="figure_cola/tab-collect-get-signatures-1-1.png" alt="plot of chunk tab-collect-get-signatures-1"/></p>

</div>
<div id='tab-collect-get-signatures-2'>
<pre><code class="r">collect_plots(res_list, k = 3, fun = get_signatures, mc.cores = 4)
</code></pre>

<p><img src="figure_cola/tab-collect-get-signatures-2-1.png" alt="plot of chunk tab-collect-get-signatures-2"/></p>

</div>
<div id='tab-collect-get-signatures-3'>
<pre><code class="r">collect_plots(res_list, k = 4, fun = get_signatures, mc.cores = 4)
</code></pre>

<p><img src="figure_cola/tab-collect-get-signatures-3-1.png" alt="plot of chunk tab-collect-get-signatures-3"/></p>

</div>
<div id='tab-collect-get-signatures-4'>
<pre><code class="r">collect_plots(res_list, k = 5, fun = get_signatures, mc.cores = 4)
</code></pre>

<p><img src="figure_cola/tab-collect-get-signatures-4-1.png" alt="plot of chunk tab-collect-get-signatures-4"/></p>

</div>
<div id='tab-collect-get-signatures-5'>
<pre><code class="r">collect_plots(res_list, k = 6, fun = get_signatures, mc.cores = 4)
</code></pre>

<p><img src="figure_cola/tab-collect-get-signatures-5-1.png" alt="plot of chunk tab-collect-get-signatures-5"/></p>

</div>
</div>



### Statistics table

The statistics used for measuring the stability of consensus partitioning.
([How are they
defined?](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13))


<script>
$( function() {
	$( '#tabs-get-stats-from-consensus-partition-list' ).tabs();
} );
</script>
<div id='tabs-get-stats-from-consensus-partition-list'>
<ul>
<li><a href='#tab-get-stats-from-consensus-partition-list-1'>k = 2</a></li>
<li><a href='#tab-get-stats-from-consensus-partition-list-2'>k = 3</a></li>
<li><a href='#tab-get-stats-from-consensus-partition-list-3'>k = 4</a></li>
<li><a href='#tab-get-stats-from-consensus-partition-list-4'>k = 5</a></li>
<li><a href='#tab-get-stats-from-consensus-partition-list-5'>k = 6</a></li>
</ul>
<div id='tab-get-stats-from-consensus-partition-list-1'>
<pre><code class="r">get_stats(res_list, k = 2)
</code></pre>

<pre><code>#&gt;             k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#&gt; SD:NMF      2 1.000           0.944       0.980          0.506 0.493   0.493
#&gt; CV:NMF      2 1.000           0.975       0.990          0.509 0.491   0.491
#&gt; MAD:NMF     2 1.000           0.993       0.996          0.504 0.497   0.497
#&gt; ATC:NMF     2 1.000           0.974       0.991          0.508 0.491   0.491
#&gt; SD:skmeans  2 1.000           0.970       0.988          0.506 0.497   0.497
#&gt; CV:skmeans  2 1.000           0.969       0.989          0.509 0.491   0.491
#&gt; MAD:skmeans 2 1.000           0.991       0.996          0.504 0.497   0.497
#&gt; ATC:skmeans 2 1.000           1.000       1.000          0.510 0.491   0.491
#&gt; SD:mclust   2 0.547           0.933       0.938          0.450 0.547   0.547
#&gt; CV:mclust   2 0.509           0.797       0.859          0.438 0.560   0.560
#&gt; MAD:mclust  2 1.000           0.974       0.989          0.460 0.547   0.547
#&gt; ATC:mclust  2 0.829           0.898       0.957          0.478 0.502   0.502
#&gt; SD:kmeans   2 1.000           0.977       0.985          0.502 0.497   0.497
#&gt; CV:kmeans   2 0.633           0.936       0.956          0.491 0.491   0.491
#&gt; MAD:kmeans  2 1.000           1.000       1.000          0.504 0.497   0.497
#&gt; ATC:kmeans  2 1.000           1.000       1.000          0.510 0.491   0.491
#&gt; SD:pam      2 0.961           0.948       0.978          0.506 0.497   0.497
#&gt; CV:pam      2 0.858           0.960       0.974          0.501 0.491   0.491
#&gt; MAD:pam     2 1.000           1.000       1.000          0.504 0.497   0.497
#&gt; ATC:pam     2 1.000           1.000       1.000          0.510 0.491   0.491
#&gt; SD:hclust   2 0.280           0.407       0.750          0.365 0.628   0.628
#&gt; CV:hclust   2 0.537           0.731       0.878          0.200 0.927   0.927
#&gt; MAD:hclust  2 0.855           0.948       0.975          0.509 0.491   0.491
#&gt; ATC:hclust  2 1.000           1.000       1.000          0.510 0.491   0.491
</code></pre>

</div>
<div id='tab-get-stats-from-consensus-partition-list-2'>
<pre><code class="r">get_stats(res_list, k = 3)
</code></pre>

<pre><code>#&gt;             k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#&gt; SD:NMF      3 0.905           0.916       0.959          0.251 0.860   0.725
#&gt; CV:NMF      3 0.862           0.857       0.930          0.254 0.840   0.682
#&gt; MAD:NMF     3 1.000           0.968       0.987          0.244 0.867   0.734
#&gt; ATC:NMF     3 0.807           0.782       0.894          0.198 0.911   0.821
#&gt; SD:skmeans  3 0.925           0.926       0.966          0.302 0.843   0.685
#&gt; CV:skmeans  3 1.000           0.950       0.978          0.288 0.820   0.646
#&gt; MAD:skmeans 3 0.909           0.929       0.962          0.277 0.868   0.734
#&gt; ATC:skmeans 3 1.000           0.958       0.983          0.155 0.929   0.857
#&gt; SD:mclust   3 0.700           0.727       0.840          0.479 0.776   0.591
#&gt; CV:mclust   3 0.595           0.792       0.861          0.464 0.762   0.584
#&gt; MAD:mclust  3 0.738           0.857       0.929          0.425 0.808   0.649
#&gt; ATC:mclust  3 1.000           0.994       0.997          0.384 0.781   0.586
#&gt; SD:kmeans   3 0.722           0.834       0.872          0.266 0.843   0.685
#&gt; CV:kmeans   3 0.781           0.860       0.890          0.309 0.772   0.568
#&gt; MAD:kmeans  3 0.768           0.795       0.907          0.226 0.867   0.734
#&gt; ATC:kmeans  3 0.904           0.932       0.968          0.166 0.929   0.857
#&gt; SD:pam      3 0.940           0.891       0.959          0.287 0.820   0.650
#&gt; CV:pam      3 0.951           0.907       0.963          0.278 0.877   0.749
#&gt; MAD:pam     3 0.809           0.894       0.928          0.285 0.816   0.642
#&gt; ATC:pam     3 0.856           0.829       0.917          0.160 0.965   0.929
#&gt; SD:hclust   3 0.598           0.829       0.885          0.617 0.603   0.437
#&gt; CV:hclust   3 0.586           0.683       0.814          1.359 0.706   0.683
#&gt; MAD:hclust  3 1.000           0.964       0.983          0.138 0.936   0.869
#&gt; ATC:hclust  3 1.000           0.987       0.994          0.078 0.965   0.929
</code></pre>

</div>
<div id='tab-get-stats-from-consensus-partition-list-3'>
<pre><code class="r">get_stats(res_list, k = 4)
</code></pre>

<pre><code>#&gt;             k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#&gt; SD:NMF      4 0.929           0.900       0.954        0.05891 0.940   0.844
#&gt; CV:NMF      4 0.851           0.836       0.921        0.08928 0.892   0.725
#&gt; MAD:NMF     4 0.944           0.907       0.955        0.05484 0.956   0.884
#&gt; ATC:NMF     4 0.799           0.828       0.902        0.13679 0.859   0.663
#&gt; SD:skmeans  4 0.902           0.861       0.937        0.08852 0.918   0.769
#&gt; CV:skmeans  4 0.940           0.922       0.966        0.11081 0.918   0.766
#&gt; MAD:skmeans 4 0.781           0.756       0.889        0.08471 0.904   0.746
#&gt; ATC:skmeans 4 0.898           0.845       0.929        0.12789 0.886   0.736
#&gt; SD:mclust   4 0.800           0.899       0.920        0.10176 0.931   0.786
#&gt; CV:mclust   4 0.887           0.893       0.928        0.15871 0.869   0.638
#&gt; MAD:mclust  4 0.697           0.672       0.827        0.10130 0.825   0.564
#&gt; ATC:mclust  4 0.857           0.778       0.895        0.07664 0.940   0.825
#&gt; SD:kmeans   4 0.759           0.708       0.850        0.10559 0.918   0.780
#&gt; CV:kmeans   4 0.761           0.729       0.851        0.10099 0.901   0.734
#&gt; MAD:kmeans  4 0.671           0.666       0.822        0.12913 0.953   0.877
#&gt; ATC:kmeans  4 0.815           0.846       0.892        0.12815 0.874   0.707
#&gt; SD:pam      4 0.961           0.936       0.971        0.10167 0.855   0.625
#&gt; CV:pam      4 0.794           0.731       0.855        0.10677 0.869   0.662
#&gt; MAD:pam     4 0.797           0.811       0.895        0.11480 0.909   0.751
#&gt; ATC:pam     4 0.981           0.936       0.977        0.13463 0.877   0.730
#&gt; SD:hclust   4 0.772           0.873       0.923        0.07114 0.968   0.917
#&gt; CV:hclust   4 0.839           0.882       0.920        0.40363 0.695   0.518
#&gt; MAD:hclust  4 0.995           0.958       0.982        0.00636 0.997   0.993
#&gt; ATC:hclust  4 0.821           0.761       0.857        0.15285 0.874   0.724
</code></pre>

</div>
<div id='tab-get-stats-from-consensus-partition-list-4'>
<pre><code class="r">get_stats(res_list, k = 5)
</code></pre>

<pre><code>#&gt;             k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#&gt; SD:NMF      5 0.790           0.749       0.868         0.0966 0.928   0.788
#&gt; CV:NMF      5 0.857           0.787       0.895         0.0834 0.923   0.762
#&gt; MAD:NMF     5 0.824           0.759       0.838         0.0935 0.898   0.714
#&gt; ATC:NMF     5 0.758           0.693       0.831         0.0405 0.954   0.850
#&gt; SD:skmeans  5 0.815           0.695       0.838         0.0513 0.979   0.927
#&gt; CV:skmeans  5 0.797           0.729       0.838         0.0586 0.994   0.980
#&gt; MAD:skmeans 5 0.799           0.626       0.832         0.0722 0.948   0.833
#&gt; ATC:skmeans 5 0.858           0.850       0.897         0.0507 0.939   0.815
#&gt; SD:mclust   5 0.733           0.773       0.847         0.0273 0.892   0.638
#&gt; CV:mclust   5 0.880           0.891       0.864         0.0499 0.966   0.860
#&gt; MAD:mclust  5 0.732           0.601       0.793         0.0536 0.905   0.675
#&gt; ATC:mclust  5 0.860           0.818       0.893         0.0607 0.899   0.673
#&gt; SD:kmeans   5 0.691           0.633       0.791         0.0678 1.000   1.000
#&gt; CV:kmeans   5 0.725           0.728       0.771         0.0688 0.957   0.862
#&gt; MAD:kmeans  5 0.657           0.589       0.775         0.0843 0.908   0.743
#&gt; ATC:kmeans  5 0.689           0.747       0.834         0.0824 0.954   0.854
#&gt; SD:pam      5 0.892           0.785       0.894         0.0453 0.970   0.894
#&gt; CV:pam      5 0.884           0.741       0.885         0.0513 0.932   0.773
#&gt; MAD:pam     5 0.749           0.736       0.856         0.0323 0.918   0.749
#&gt; ATC:pam     5 0.921           0.919       0.966         0.0490 0.968   0.903
#&gt; SD:hclust   5 0.805           0.833       0.831         0.1193 0.922   0.779
#&gt; CV:hclust   5 0.793           0.806       0.866         0.0850 0.951   0.851
#&gt; MAD:hclust  5 0.778           0.780       0.878         0.1955 0.874   0.703
#&gt; ATC:hclust  5 0.846           0.893       0.951         0.0785 0.904   0.741
</code></pre>

</div>
<div id='tab-get-stats-from-consensus-partition-list-5'>
<pre><code class="r">get_stats(res_list, k = 6)
</code></pre>

<pre><code>#&gt;             k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#&gt; SD:NMF      6 0.773           0.724       0.827         0.0683 0.911   0.692
#&gt; CV:NMF      6 0.732           0.550       0.741         0.0657 0.924   0.703
#&gt; MAD:NMF     6 0.757           0.719       0.833         0.0724 0.928   0.743
#&gt; ATC:NMF     6 0.729           0.676       0.826         0.0377 0.891   0.663
#&gt; SD:skmeans  6 0.722           0.600       0.732         0.0442 0.943   0.794
#&gt; CV:skmeans  6 0.779           0.694       0.731         0.0452 0.921   0.710
#&gt; MAD:skmeans 6 0.722           0.628       0.772         0.0480 0.941   0.786
#&gt; ATC:skmeans 6 0.889           0.865       0.932         0.0427 0.992   0.970
#&gt; SD:mclust   6 0.787           0.742       0.825         0.0543 0.971   0.874
#&gt; CV:mclust   6 0.831           0.813       0.868         0.0297 0.983   0.920
#&gt; MAD:mclust  6 0.752           0.656       0.801         0.0407 0.920   0.674
#&gt; ATC:mclust  6 0.778           0.652       0.814         0.0267 0.900   0.642
#&gt; SD:kmeans   6 0.721           0.530       0.716         0.0545 0.927   0.784
#&gt; CV:kmeans   6 0.722           0.437       0.659         0.0479 0.973   0.901
#&gt; MAD:kmeans  6 0.718           0.533       0.736         0.0462 0.933   0.768
#&gt; ATC:kmeans  6 0.731           0.710       0.813         0.0506 0.979   0.924
#&gt; SD:pam      6 0.845           0.789       0.893         0.0400 0.964   0.866
#&gt; CV:pam      6 0.889           0.736       0.895         0.0335 0.959   0.847
#&gt; MAD:pam     6 0.740           0.712       0.812         0.0719 0.892   0.631
#&gt; ATC:pam     6 0.893           0.912       0.928         0.0542 0.958   0.860
#&gt; SD:hclust   6 0.867           0.813       0.899         0.0434 0.991   0.967
#&gt; CV:hclust   6 0.863           0.781       0.881         0.0433 0.985   0.948
#&gt; MAD:hclust  6 0.851           0.780       0.899         0.0495 0.948   0.838
#&gt; ATC:hclust  6 0.746           0.752       0.871         0.0759 0.947   0.833
</code></pre>

</div>
</div>

Following heatmap plots the partition for each combination of methods and the
lightness correspond to the silhouette scores for samples in each method. On
top the consensus subgroup is inferred from all methods by taking the mean
silhouette scores as weight.


<script>
$( function() {
	$( '#tabs-collect-stats-from-consensus-partition-list' ).tabs();
} );
</script>
<div id='tabs-collect-stats-from-consensus-partition-list'>
<ul>
<li><a href='#tab-collect-stats-from-consensus-partition-list-1'>k = 2</a></li>
<li><a href='#tab-collect-stats-from-consensus-partition-list-2'>k = 3</a></li>
<li><a href='#tab-collect-stats-from-consensus-partition-list-3'>k = 4</a></li>
<li><a href='#tab-collect-stats-from-consensus-partition-list-4'>k = 5</a></li>
<li><a href='#tab-collect-stats-from-consensus-partition-list-5'>k = 6</a></li>
</ul>
<div id='tab-collect-stats-from-consensus-partition-list-1'>
<pre><code class="r">collect_stats(res_list, k = 2)
</code></pre>

<p><img src="figure_cola/tab-collect-stats-from-consensus-partition-list-1-1.png" alt="plot of chunk tab-collect-stats-from-consensus-partition-list-1"/></p>

</div>
<div id='tab-collect-stats-from-consensus-partition-list-2'>
<pre><code class="r">collect_stats(res_list, k = 3)
</code></pre>

<p><img src="figure_cola/tab-collect-stats-from-consensus-partition-list-2-1.png" alt="plot of chunk tab-collect-stats-from-consensus-partition-list-2"/></p>

</div>
<div id='tab-collect-stats-from-consensus-partition-list-3'>
<pre><code class="r">collect_stats(res_list, k = 4)
</code></pre>

<p><img src="figure_cola/tab-collect-stats-from-consensus-partition-list-3-1.png" alt="plot of chunk tab-collect-stats-from-consensus-partition-list-3"/></p>

</div>
<div id='tab-collect-stats-from-consensus-partition-list-4'>
<pre><code class="r">collect_stats(res_list, k = 5)
</code></pre>

<p><img src="figure_cola/tab-collect-stats-from-consensus-partition-list-4-1.png" alt="plot of chunk tab-collect-stats-from-consensus-partition-list-4"/></p>

</div>
<div id='tab-collect-stats-from-consensus-partition-list-5'>
<pre><code class="r">collect_stats(res_list, k = 6)
</code></pre>

<p><img src="figure_cola/tab-collect-stats-from-consensus-partition-list-5-1.png" alt="plot of chunk tab-collect-stats-from-consensus-partition-list-5"/></p>

</div>
</div>

### Partition from all methods



Collect partitions from all methods:


<script>
$( function() {
	$( '#tabs-collect-classes-from-consensus-partition-list' ).tabs();
} );
</script>
<div id='tabs-collect-classes-from-consensus-partition-list'>
<ul>
<li><a href='#tab-collect-classes-from-consensus-partition-list-1'>k = 2</a></li>
<li><a href='#tab-collect-classes-from-consensus-partition-list-2'>k = 3</a></li>
<li><a href='#tab-collect-classes-from-consensus-partition-list-3'>k = 4</a></li>
<li><a href='#tab-collect-classes-from-consensus-partition-list-4'>k = 5</a></li>
<li><a href='#tab-collect-classes-from-consensus-partition-list-5'>k = 6</a></li>
</ul>
<div id='tab-collect-classes-from-consensus-partition-list-1'>
<pre><code class="r">collect_classes(res_list, k = 2)
</code></pre>

<p><img src="figure_cola/tab-collect-classes-from-consensus-partition-list-1-1.png" alt="plot of chunk tab-collect-classes-from-consensus-partition-list-1"/></p>

</div>
<div id='tab-collect-classes-from-consensus-partition-list-2'>
<pre><code class="r">collect_classes(res_list, k = 3)
</code></pre>

<p><img src="figure_cola/tab-collect-classes-from-consensus-partition-list-2-1.png" alt="plot of chunk tab-collect-classes-from-consensus-partition-list-2"/></p>

</div>
<div id='tab-collect-classes-from-consensus-partition-list-3'>
<pre><code class="r">collect_classes(res_list, k = 4)
</code></pre>

<p><img src="figure_cola/tab-collect-classes-from-consensus-partition-list-3-1.png" alt="plot of chunk tab-collect-classes-from-consensus-partition-list-3"/></p>

</div>
<div id='tab-collect-classes-from-consensus-partition-list-4'>
<pre><code class="r">collect_classes(res_list, k = 5)
</code></pre>

<p><img src="figure_cola/tab-collect-classes-from-consensus-partition-list-4-1.png" alt="plot of chunk tab-collect-classes-from-consensus-partition-list-4"/></p>

</div>
<div id='tab-collect-classes-from-consensus-partition-list-5'>
<pre><code class="r">collect_classes(res_list, k = 6)
</code></pre>

<p><img src="figure_cola/tab-collect-classes-from-consensus-partition-list-5-1.png" alt="plot of chunk tab-collect-classes-from-consensus-partition-list-5"/></p>

</div>
</div>



### Top rows overlap


Overlap of top rows from different top-row methods:


<script>
$( function() {
	$( '#tabs-top-rows-overlap-by-euler' ).tabs();
} );
</script>
<div id='tabs-top-rows-overlap-by-euler'>
<ul>
<li><a href='#tab-top-rows-overlap-by-euler-1'>top_n = 1000</a></li>
<li><a href='#tab-top-rows-overlap-by-euler-2'>top_n = 2000</a></li>
<li><a href='#tab-top-rows-overlap-by-euler-3'>top_n = 3000</a></li>
<li><a href='#tab-top-rows-overlap-by-euler-4'>top_n = 4000</a></li>
<li><a href='#tab-top-rows-overlap-by-euler-5'>top_n = 5000</a></li>
</ul>
<div id='tab-top-rows-overlap-by-euler-1'>
<pre><code class="r">top_rows_overlap(res_list, top_n = 1000, method = &quot;euler&quot;)
</code></pre>

<p><img src="figure_cola/tab-top-rows-overlap-by-euler-1-1.png" alt="plot of chunk tab-top-rows-overlap-by-euler-1"/></p>

</div>
<div id='tab-top-rows-overlap-by-euler-2'>
<pre><code class="r">top_rows_overlap(res_list, top_n = 2000, method = &quot;euler&quot;)
</code></pre>

<p><img src="figure_cola/tab-top-rows-overlap-by-euler-2-1.png" alt="plot of chunk tab-top-rows-overlap-by-euler-2"/></p>

</div>
<div id='tab-top-rows-overlap-by-euler-3'>
<pre><code class="r">top_rows_overlap(res_list, top_n = 3000, method = &quot;euler&quot;)
</code></pre>

<p><img src="figure_cola/tab-top-rows-overlap-by-euler-3-1.png" alt="plot of chunk tab-top-rows-overlap-by-euler-3"/></p>

</div>
<div id='tab-top-rows-overlap-by-euler-4'>
<pre><code class="r">top_rows_overlap(res_list, top_n = 4000, method = &quot;euler&quot;)
</code></pre>

<p><img src="figure_cola/tab-top-rows-overlap-by-euler-4-1.png" alt="plot of chunk tab-top-rows-overlap-by-euler-4"/></p>

</div>
<div id='tab-top-rows-overlap-by-euler-5'>
<pre><code class="r">top_rows_overlap(res_list, top_n = 5000, method = &quot;euler&quot;)
</code></pre>

<p><img src="figure_cola/tab-top-rows-overlap-by-euler-5-1.png" alt="plot of chunk tab-top-rows-overlap-by-euler-5"/></p>

</div>
</div>

Also visualize the correspondance of rankings between different top-row methods:


<script>
$( function() {
	$( '#tabs-top-rows-overlap-by-correspondance' ).tabs();
} );
</script>
<div id='tabs-top-rows-overlap-by-correspondance'>
<ul>
<li><a href='#tab-top-rows-overlap-by-correspondance-1'>top_n = 1000</a></li>
<li><a href='#tab-top-rows-overlap-by-correspondance-2'>top_n = 2000</a></li>
<li><a href='#tab-top-rows-overlap-by-correspondance-3'>top_n = 3000</a></li>
<li><a href='#tab-top-rows-overlap-by-correspondance-4'>top_n = 4000</a></li>
<li><a href='#tab-top-rows-overlap-by-correspondance-5'>top_n = 5000</a></li>
</ul>
<div id='tab-top-rows-overlap-by-correspondance-1'>
<pre><code class="r">top_rows_overlap(res_list, top_n = 1000, method = &quot;correspondance&quot;)
</code></pre>

<p><img src="figure_cola/tab-top-rows-overlap-by-correspondance-1-1.png" alt="plot of chunk tab-top-rows-overlap-by-correspondance-1"/></p>

</div>
<div id='tab-top-rows-overlap-by-correspondance-2'>
<pre><code class="r">top_rows_overlap(res_list, top_n = 2000, method = &quot;correspondance&quot;)
</code></pre>

<p><img src="figure_cola/tab-top-rows-overlap-by-correspondance-2-1.png" alt="plot of chunk tab-top-rows-overlap-by-correspondance-2"/></p>

</div>
<div id='tab-top-rows-overlap-by-correspondance-3'>
<pre><code class="r">top_rows_overlap(res_list, top_n = 3000, method = &quot;correspondance&quot;)
</code></pre>

<p><img src="figure_cola/tab-top-rows-overlap-by-correspondance-3-1.png" alt="plot of chunk tab-top-rows-overlap-by-correspondance-3"/></p>

</div>
<div id='tab-top-rows-overlap-by-correspondance-4'>
<pre><code class="r">top_rows_overlap(res_list, top_n = 4000, method = &quot;correspondance&quot;)
</code></pre>

<p><img src="figure_cola/tab-top-rows-overlap-by-correspondance-4-1.png" alt="plot of chunk tab-top-rows-overlap-by-correspondance-4"/></p>

</div>
<div id='tab-top-rows-overlap-by-correspondance-5'>
<pre><code class="r">top_rows_overlap(res_list, top_n = 5000, method = &quot;correspondance&quot;)
</code></pre>

<p><img src="figure_cola/tab-top-rows-overlap-by-correspondance-5-1.png" alt="plot of chunk tab-top-rows-overlap-by-correspondance-5"/></p>

</div>
</div>


Heatmaps of the top rows:



<script>
$( function() {
	$( '#tabs-top-rows-heatmap' ).tabs();
} );
</script>
<div id='tabs-top-rows-heatmap'>
<ul>
<li><a href='#tab-top-rows-heatmap-1'>top_n = 1000</a></li>
<li><a href='#tab-top-rows-heatmap-2'>top_n = 2000</a></li>
<li><a href='#tab-top-rows-heatmap-3'>top_n = 3000</a></li>
<li><a href='#tab-top-rows-heatmap-4'>top_n = 4000</a></li>
<li><a href='#tab-top-rows-heatmap-5'>top_n = 5000</a></li>
</ul>
<div id='tab-top-rows-heatmap-1'>
<pre><code class="r">top_rows_heatmap(res_list, top_n = 1000)
</code></pre>

<p><img src="figure_cola/tab-top-rows-heatmap-1-1.png" alt="plot of chunk tab-top-rows-heatmap-1"/></p>

</div>
<div id='tab-top-rows-heatmap-2'>
<pre><code class="r">top_rows_heatmap(res_list, top_n = 2000)
</code></pre>

<p><img src="figure_cola/tab-top-rows-heatmap-2-1.png" alt="plot of chunk tab-top-rows-heatmap-2"/></p>

</div>
<div id='tab-top-rows-heatmap-3'>
<pre><code class="r">top_rows_heatmap(res_list, top_n = 3000)
</code></pre>

<p><img src="figure_cola/tab-top-rows-heatmap-3-1.png" alt="plot of chunk tab-top-rows-heatmap-3"/></p>

</div>
<div id='tab-top-rows-heatmap-4'>
<pre><code class="r">top_rows_heatmap(res_list, top_n = 4000)
</code></pre>

<p><img src="figure_cola/tab-top-rows-heatmap-4-1.png" alt="plot of chunk tab-top-rows-heatmap-4"/></p>

</div>
<div id='tab-top-rows-heatmap-5'>
<pre><code class="r">top_rows_heatmap(res_list, top_n = 5000)
</code></pre>

<p><img src="figure_cola/tab-top-rows-heatmap-5-1.png" alt="plot of chunk tab-top-rows-heatmap-5"/></p>

</div>
</div>



 
## Results for each method


---------------------------------------------------




### SD:hclust






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["SD", "hclust"]
# you can also extract it by
# res = res_list["SD:hclust"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 17171 rows and 54 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'SD' method.
#>   Subgroups are detected by 'hclust' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 3.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk SD-hclust-collect-plots](figure_cola/SD-hclust-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk SD-hclust-select-partition-number](figure_cola/SD-hclust-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 0.280           0.407       0.750         0.3651 0.628   0.628
#> 3 3 0.598           0.829       0.885         0.6174 0.603   0.437
#> 4 4 0.772           0.873       0.923         0.0711 0.968   0.917
#> 5 5 0.805           0.833       0.831         0.1193 0.922   0.779
#> 6 6 0.867           0.813       0.899         0.0434 0.991   0.967
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 3
```


Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-SD-hclust-get-classes' ).tabs();
} );
</script>
<div id='tabs-SD-hclust-get-classes'>
<ul>
<li><a href='#tab-SD-hclust-get-classes-1'>k = 2</a></li>
<li><a href='#tab-SD-hclust-get-classes-2'>k = 3</a></li>
<li><a href='#tab-SD-hclust-get-classes-3'>k = 4</a></li>
<li><a href='#tab-SD-hclust-get-classes-4'>k = 5</a></li>
<li><a href='#tab-SD-hclust-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-SD-hclust-get-classes-1'>
<p><a id='tab-SD-hclust-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2
#&gt; SRR975551     2   0.996     0.0475 0.464 0.536
#&gt; SRR975552     2   0.996     0.0475 0.464 0.536
#&gt; SRR975554     2   0.996     0.0475 0.464 0.536
#&gt; SRR975553     2   0.000     0.6474 0.000 1.000
#&gt; SRR975555     2   0.996     0.0475 0.464 0.536
#&gt; SRR975556     2   0.000     0.6474 0.000 1.000
#&gt; SRR975557     2   0.644     0.4167 0.164 0.836
#&gt; SRR975558     2   0.973     0.1704 0.404 0.596
#&gt; SRR975559     2   0.973     0.1704 0.404 0.596
#&gt; SRR975560     2   0.000     0.6474 0.000 1.000
#&gt; SRR975561     2   0.000     0.6474 0.000 1.000
#&gt; SRR975562     2   0.996     0.0475 0.464 0.536
#&gt; SRR975563     2   0.000     0.6474 0.000 1.000
#&gt; SRR975564     2   0.996     0.0475 0.464 0.536
#&gt; SRR975565     2   0.996     0.0475 0.464 0.536
#&gt; SRR975566     2   0.996     0.0475 0.464 0.536
#&gt; SRR975567     2   0.973     0.1704 0.404 0.596
#&gt; SRR975568     2   0.996     0.0475 0.464 0.536
#&gt; SRR975569     2   0.000     0.6474 0.000 1.000
#&gt; SRR975570     2   0.000     0.6474 0.000 1.000
#&gt; SRR975571     2   0.000     0.6474 0.000 1.000
#&gt; SRR975572     2   0.000     0.6474 0.000 1.000
#&gt; SRR975573     2   0.000     0.6474 0.000 1.000
#&gt; SRR975574     2   0.000     0.6474 0.000 1.000
#&gt; SRR975575     2   0.000     0.6474 0.000 1.000
#&gt; SRR975576     2   0.000     0.6474 0.000 1.000
#&gt; SRR975577     2   0.000     0.6474 0.000 1.000
#&gt; SRR975578     2   0.000     0.6474 0.000 1.000
#&gt; SRR975579     2   0.644     0.4167 0.164 0.836
#&gt; SRR975580     2   0.000     0.6474 0.000 1.000
#&gt; SRR975581     2   0.000     0.6474 0.000 1.000
#&gt; SRR975582     2   0.000     0.6474 0.000 1.000
#&gt; SRR975583     2   0.000     0.6474 0.000 1.000
#&gt; SRR975584     2   0.000     0.6474 0.000 1.000
#&gt; SRR975585     2   0.000     0.6474 0.000 1.000
#&gt; SRR975586     2   0.000     0.6474 0.000 1.000
#&gt; SRR975587     1   0.987     0.4589 0.568 0.432
#&gt; SRR975588     2   0.000     0.6474 0.000 1.000
#&gt; SRR975589     1   0.949     0.4103 0.632 0.368
#&gt; SRR975590     1   0.975     0.3567 0.592 0.408
#&gt; SRR975591     1   0.987     0.4589 0.568 0.432
#&gt; SRR975592     1   0.855     0.4483 0.720 0.280
#&gt; SRR975593     1   0.949     0.4103 0.632 0.368
#&gt; SRR975594     1   0.980     0.2498 0.584 0.416
#&gt; SRR975595     1   0.980     0.3421 0.584 0.416
#&gt; SRR975597     1   0.980     0.3421 0.584 0.416
#&gt; SRR975596     2   0.973     0.1704 0.404 0.596
#&gt; SRR975598     1   0.980     0.3421 0.584 0.416
#&gt; SRR975599     2   0.963     0.2043 0.388 0.612
#&gt; SRR975600     2   0.992    -0.3257 0.448 0.552
#&gt; SRR975601     1   0.987     0.4589 0.568 0.432
#&gt; SRR975602     2   0.996     0.0475 0.464 0.536
#&gt; SRR975603     1   0.987     0.4589 0.568 0.432
#&gt; SRR975604     1   0.987     0.4589 0.568 0.432
</code></pre>

<script>
$('#tab-SD-hclust-get-classes-1-a').parent().next().next().hide();
$('#tab-SD-hclust-get-classes-1-a').click(function(){
  $('#tab-SD-hclust-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-hclust-get-classes-2'>
<p><a id='tab-SD-hclust-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3
#&gt; SRR975551     1   0.312      0.824 0.892 0.108 0.000
#&gt; SRR975552     1   0.312      0.824 0.892 0.108 0.000
#&gt; SRR975554     1   0.216      0.820 0.936 0.064 0.000
#&gt; SRR975553     2   0.000      0.963 0.000 1.000 0.000
#&gt; SRR975555     1   0.348      0.815 0.872 0.128 0.000
#&gt; SRR975556     2   0.000      0.963 0.000 1.000 0.000
#&gt; SRR975557     2   0.934      0.374 0.208 0.512 0.280
#&gt; SRR975558     1   0.493      0.697 0.768 0.232 0.000
#&gt; SRR975559     1   0.341      0.797 0.876 0.124 0.000
#&gt; SRR975560     2   0.000      0.963 0.000 1.000 0.000
#&gt; SRR975561     2   0.000      0.963 0.000 1.000 0.000
#&gt; SRR975562     1   0.216      0.820 0.936 0.064 0.000
#&gt; SRR975563     2   0.000      0.963 0.000 1.000 0.000
#&gt; SRR975564     1   0.348      0.815 0.872 0.128 0.000
#&gt; SRR975565     1   0.341      0.817 0.876 0.124 0.000
#&gt; SRR975566     1   0.216      0.820 0.936 0.064 0.000
#&gt; SRR975567     1   0.493      0.697 0.768 0.232 0.000
#&gt; SRR975568     1   0.348      0.815 0.872 0.128 0.000
#&gt; SRR975569     2   0.000      0.963 0.000 1.000 0.000
#&gt; SRR975570     2   0.000      0.963 0.000 1.000 0.000
#&gt; SRR975571     2   0.000      0.963 0.000 1.000 0.000
#&gt; SRR975572     2   0.000      0.963 0.000 1.000 0.000
#&gt; SRR975573     2   0.000      0.963 0.000 1.000 0.000
#&gt; SRR975574     2   0.000      0.963 0.000 1.000 0.000
#&gt; SRR975575     2   0.000      0.963 0.000 1.000 0.000
#&gt; SRR975576     2   0.000      0.963 0.000 1.000 0.000
#&gt; SRR975577     2   0.000      0.963 0.000 1.000 0.000
#&gt; SRR975578     2   0.000      0.963 0.000 1.000 0.000
#&gt; SRR975579     2   0.934      0.374 0.208 0.512 0.280
#&gt; SRR975580     2   0.000      0.963 0.000 1.000 0.000
#&gt; SRR975581     2   0.000      0.963 0.000 1.000 0.000
#&gt; SRR975582     2   0.000      0.963 0.000 1.000 0.000
#&gt; SRR975583     2   0.000      0.963 0.000 1.000 0.000
#&gt; SRR975584     2   0.000      0.963 0.000 1.000 0.000
#&gt; SRR975585     2   0.000      0.963 0.000 1.000 0.000
#&gt; SRR975586     2   0.000      0.963 0.000 1.000 0.000
#&gt; SRR975587     3   0.573      0.875 0.324 0.000 0.676
#&gt; SRR975588     2   0.000      0.963 0.000 1.000 0.000
#&gt; SRR975589     1   0.355      0.683 0.868 0.000 0.132
#&gt; SRR975590     1   0.393      0.744 0.880 0.028 0.092
#&gt; SRR975591     3   0.573      0.875 0.324 0.000 0.676
#&gt; SRR975592     1   0.480      0.532 0.780 0.000 0.220
#&gt; SRR975593     1   0.355      0.683 0.868 0.000 0.132
#&gt; SRR975594     3   0.141      0.590 0.036 0.000 0.964
#&gt; SRR975595     1   0.377      0.752 0.888 0.028 0.084
#&gt; SRR975597     1   0.377      0.752 0.888 0.028 0.084
#&gt; SRR975596     1   0.341      0.797 0.876 0.124 0.000
#&gt; SRR975598     1   0.377      0.752 0.888 0.028 0.084
#&gt; SRR975599     1   0.806      0.247 0.532 0.068 0.400
#&gt; SRR975600     3   0.629      0.593 0.468 0.000 0.532
#&gt; SRR975601     3   0.573      0.875 0.324 0.000 0.676
#&gt; SRR975602     1   0.216      0.820 0.936 0.064 0.000
#&gt; SRR975603     3   0.573      0.875 0.324 0.000 0.676
#&gt; SRR975604     3   0.573      0.875 0.324 0.000 0.676
</code></pre>

<script>
$('#tab-SD-hclust-get-classes-2-a').parent().next().next().hide();
$('#tab-SD-hclust-get-classes-2-a').click(function(){
  $('#tab-SD-hclust-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-hclust-get-classes-3'>
<p><a id='tab-SD-hclust-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3   p4
#&gt; SRR975551     1   0.130      0.836 0.956 0.044 0.000 0.00
#&gt; SRR975552     1   0.130      0.836 0.956 0.044 0.000 0.00
#&gt; SRR975554     1   0.000      0.834 1.000 0.000 0.000 0.00
#&gt; SRR975553     2   0.000      1.000 0.000 1.000 0.000 0.00
#&gt; SRR975555     1   0.172      0.826 0.936 0.064 0.000 0.00
#&gt; SRR975556     2   0.000      1.000 0.000 1.000 0.000 0.00
#&gt; SRR975557     4   0.000      1.000 0.000 0.000 0.000 1.00
#&gt; SRR975558     1   0.406      0.748 0.832 0.108 0.000 0.06
#&gt; SRR975559     1   0.164      0.811 0.940 0.000 0.000 0.06
#&gt; SRR975560     2   0.000      1.000 0.000 1.000 0.000 0.00
#&gt; SRR975561     2   0.000      1.000 0.000 1.000 0.000 0.00
#&gt; SRR975562     1   0.000      0.834 1.000 0.000 0.000 0.00
#&gt; SRR975563     2   0.000      1.000 0.000 1.000 0.000 0.00
#&gt; SRR975564     1   0.172      0.826 0.936 0.064 0.000 0.00
#&gt; SRR975565     1   0.164      0.829 0.940 0.060 0.000 0.00
#&gt; SRR975566     1   0.000      0.834 1.000 0.000 0.000 0.00
#&gt; SRR975567     1   0.406      0.748 0.832 0.108 0.000 0.06
#&gt; SRR975568     1   0.172      0.826 0.936 0.064 0.000 0.00
#&gt; SRR975569     2   0.000      1.000 0.000 1.000 0.000 0.00
#&gt; SRR975570     2   0.000      1.000 0.000 1.000 0.000 0.00
#&gt; SRR975571     2   0.000      1.000 0.000 1.000 0.000 0.00
#&gt; SRR975572     2   0.000      1.000 0.000 1.000 0.000 0.00
#&gt; SRR975573     2   0.000      1.000 0.000 1.000 0.000 0.00
#&gt; SRR975574     2   0.000      1.000 0.000 1.000 0.000 0.00
#&gt; SRR975575     2   0.000      1.000 0.000 1.000 0.000 0.00
#&gt; SRR975576     2   0.000      1.000 0.000 1.000 0.000 0.00
#&gt; SRR975577     2   0.000      1.000 0.000 1.000 0.000 0.00
#&gt; SRR975578     2   0.000      1.000 0.000 1.000 0.000 0.00
#&gt; SRR975579     4   0.000      1.000 0.000 0.000 0.000 1.00
#&gt; SRR975580     2   0.000      1.000 0.000 1.000 0.000 0.00
#&gt; SRR975581     2   0.000      1.000 0.000 1.000 0.000 0.00
#&gt; SRR975582     2   0.000      1.000 0.000 1.000 0.000 0.00
#&gt; SRR975583     2   0.000      1.000 0.000 1.000 0.000 0.00
#&gt; SRR975584     2   0.000      1.000 0.000 1.000 0.000 0.00
#&gt; SRR975585     2   0.000      1.000 0.000 1.000 0.000 0.00
#&gt; SRR975586     2   0.000      1.000 0.000 1.000 0.000 0.00
#&gt; SRR975587     3   0.433      0.876 0.288 0.000 0.712 0.00
#&gt; SRR975588     2   0.000      1.000 0.000 1.000 0.000 0.00
#&gt; SRR975589     1   0.327      0.724 0.832 0.000 0.168 0.00
#&gt; SRR975590     1   0.276      0.770 0.872 0.000 0.128 0.00
#&gt; SRR975591     3   0.433      0.876 0.288 0.000 0.712 0.00
#&gt; SRR975592     1   0.410      0.576 0.744 0.000 0.256 0.00
#&gt; SRR975593     1   0.327      0.724 0.832 0.000 0.168 0.00
#&gt; SRR975594     3   0.000      0.353 0.000 0.000 1.000 0.00
#&gt; SRR975595     1   0.265      0.777 0.880 0.000 0.120 0.00
#&gt; SRR975597     1   0.265      0.777 0.880 0.000 0.120 0.00
#&gt; SRR975596     1   0.164      0.811 0.940 0.000 0.000 0.06
#&gt; SRR975598     1   0.265      0.777 0.880 0.000 0.120 0.00
#&gt; SRR975599     1   0.503      0.246 0.596 0.004 0.400 0.00
#&gt; SRR975600     3   0.493      0.586 0.432 0.000 0.568 0.00
#&gt; SRR975601     3   0.433      0.876 0.288 0.000 0.712 0.00
#&gt; SRR975602     1   0.000      0.834 1.000 0.000 0.000 0.00
#&gt; SRR975603     3   0.433      0.876 0.288 0.000 0.712 0.00
#&gt; SRR975604     3   0.433      0.876 0.288 0.000 0.712 0.00
</code></pre>

<script>
$('#tab-SD-hclust-get-classes-3-a').parent().next().next().hide();
$('#tab-SD-hclust-get-classes-3-a').click(function(){
  $('#tab-SD-hclust-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-hclust-get-classes-4'>
<p><a id='tab-SD-hclust-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3   p4    p5
#&gt; SRR975551     1   0.418      0.583 0.600 0.000 0.000 0.00 0.400
#&gt; SRR975552     1   0.418      0.583 0.600 0.000 0.000 0.00 0.400
#&gt; SRR975554     1   0.400      0.640 0.656 0.000 0.000 0.00 0.344
#&gt; SRR975553     2   0.000      1.000 0.000 1.000 0.000 0.00 0.000
#&gt; SRR975555     5   0.260      0.776 0.148 0.000 0.000 0.00 0.852
#&gt; SRR975556     2   0.000      1.000 0.000 1.000 0.000 0.00 0.000
#&gt; SRR975557     4   0.141      1.000 0.000 0.000 0.000 0.94 0.060
#&gt; SRR975558     5   0.128      0.744 0.004 0.044 0.000 0.00 0.952
#&gt; SRR975559     5   0.238      0.744 0.128 0.000 0.000 0.00 0.872
#&gt; SRR975560     2   0.000      1.000 0.000 1.000 0.000 0.00 0.000
#&gt; SRR975561     2   0.000      1.000 0.000 1.000 0.000 0.00 0.000
#&gt; SRR975562     5   0.366      0.628 0.276 0.000 0.000 0.00 0.724
#&gt; SRR975563     2   0.000      1.000 0.000 1.000 0.000 0.00 0.000
#&gt; SRR975564     5   0.260      0.776 0.148 0.000 0.000 0.00 0.852
#&gt; SRR975565     1   0.423      0.554 0.580 0.000 0.000 0.00 0.420
#&gt; SRR975566     1   0.356      0.697 0.740 0.000 0.000 0.00 0.260
#&gt; SRR975567     5   0.128      0.744 0.004 0.044 0.000 0.00 0.952
#&gt; SRR975568     5   0.260      0.776 0.148 0.000 0.000 0.00 0.852
#&gt; SRR975569     2   0.000      1.000 0.000 1.000 0.000 0.00 0.000
#&gt; SRR975570     2   0.000      1.000 0.000 1.000 0.000 0.00 0.000
#&gt; SRR975571     2   0.000      1.000 0.000 1.000 0.000 0.00 0.000
#&gt; SRR975572     2   0.000      1.000 0.000 1.000 0.000 0.00 0.000
#&gt; SRR975573     2   0.000      1.000 0.000 1.000 0.000 0.00 0.000
#&gt; SRR975574     2   0.000      1.000 0.000 1.000 0.000 0.00 0.000
#&gt; SRR975575     2   0.000      1.000 0.000 1.000 0.000 0.00 0.000
#&gt; SRR975576     2   0.000      1.000 0.000 1.000 0.000 0.00 0.000
#&gt; SRR975577     2   0.000      1.000 0.000 1.000 0.000 0.00 0.000
#&gt; SRR975578     2   0.000      1.000 0.000 1.000 0.000 0.00 0.000
#&gt; SRR975579     4   0.141      1.000 0.000 0.000 0.000 0.94 0.060
#&gt; SRR975580     2   0.000      1.000 0.000 1.000 0.000 0.00 0.000
#&gt; SRR975581     2   0.000      1.000 0.000 1.000 0.000 0.00 0.000
#&gt; SRR975582     2   0.000      1.000 0.000 1.000 0.000 0.00 0.000
#&gt; SRR975583     2   0.000      1.000 0.000 1.000 0.000 0.00 0.000
#&gt; SRR975584     2   0.000      1.000 0.000 1.000 0.000 0.00 0.000
#&gt; SRR975585     2   0.000      1.000 0.000 1.000 0.000 0.00 0.000
#&gt; SRR975586     2   0.000      1.000 0.000 1.000 0.000 0.00 0.000
#&gt; SRR975587     3   0.428      0.837 0.032 0.000 0.724 0.00 0.244
#&gt; SRR975588     2   0.000      1.000 0.000 1.000 0.000 0.00 0.000
#&gt; SRR975589     1   0.407      0.628 0.752 0.000 0.032 0.00 0.216
#&gt; SRR975590     1   0.304      0.736 0.836 0.000 0.012 0.00 0.152
#&gt; SRR975591     3   0.509      0.850 0.084 0.000 0.672 0.00 0.244
#&gt; SRR975592     1   0.455      0.645 0.752 0.000 0.124 0.00 0.124
#&gt; SRR975593     1   0.407      0.628 0.752 0.000 0.032 0.00 0.216
#&gt; SRR975594     3   0.328      0.348 0.092 0.000 0.848 0.06 0.000
#&gt; SRR975595     1   0.281      0.738 0.844 0.000 0.004 0.00 0.152
#&gt; SRR975597     1   0.281      0.738 0.844 0.000 0.004 0.00 0.152
#&gt; SRR975596     5   0.238      0.744 0.128 0.000 0.000 0.00 0.872
#&gt; SRR975598     1   0.281      0.738 0.844 0.000 0.004 0.00 0.152
#&gt; SRR975599     1   0.693      0.264 0.556 0.000 0.244 0.06 0.140
#&gt; SRR975600     3   0.655      0.617 0.248 0.000 0.476 0.00 0.276
#&gt; SRR975601     3   0.428      0.837 0.032 0.000 0.724 0.00 0.244
#&gt; SRR975602     1   0.356      0.697 0.740 0.000 0.000 0.00 0.260
#&gt; SRR975603     3   0.509      0.850 0.084 0.000 0.672 0.00 0.244
#&gt; SRR975604     3   0.509      0.850 0.084 0.000 0.672 0.00 0.244
</code></pre>

<script>
$('#tab-SD-hclust-get-classes-4-a').parent().next().next().hide();
$('#tab-SD-hclust-get-classes-4-a').click(function(){
  $('#tab-SD-hclust-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-hclust-get-classes-5'>
<p><a id='tab-SD-hclust-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3    p4    p5 p6
#&gt; SRR975551     1  0.5102      0.583 0.620 0.000 0.000 0.240 0.140  0
#&gt; SRR975552     1  0.5102      0.583 0.620 0.000 0.000 0.240 0.140  0
#&gt; SRR975554     1  0.4881      0.592 0.656 0.000 0.000 0.136 0.208  0
#&gt; SRR975553     2  0.0000      1.000 0.000 1.000 0.000 0.000 0.000  0
#&gt; SRR975555     4  0.2340      0.774 0.148 0.000 0.000 0.852 0.000  0
#&gt; SRR975556     2  0.0000      1.000 0.000 1.000 0.000 0.000 0.000  0
#&gt; SRR975557     6  0.0000      1.000 0.000 0.000 0.000 0.000 0.000  1
#&gt; SRR975558     4  0.1007      0.733 0.000 0.044 0.000 0.956 0.000  0
#&gt; SRR975559     4  0.3385      0.701 0.032 0.000 0.000 0.788 0.180  0
#&gt; SRR975560     2  0.0000      1.000 0.000 1.000 0.000 0.000 0.000  0
#&gt; SRR975561     2  0.0000      1.000 0.000 1.000 0.000 0.000 0.000  0
#&gt; SRR975562     4  0.5067      0.659 0.184 0.000 0.000 0.636 0.180  0
#&gt; SRR975563     2  0.0000      1.000 0.000 1.000 0.000 0.000 0.000  0
#&gt; SRR975564     4  0.2340      0.774 0.148 0.000 0.000 0.852 0.000  0
#&gt; SRR975565     1  0.4951      0.571 0.620 0.000 0.000 0.276 0.104  0
#&gt; SRR975566     1  0.3714      0.561 0.656 0.000 0.000 0.004 0.340  0
#&gt; SRR975567     4  0.1007      0.733 0.000 0.044 0.000 0.956 0.000  0
#&gt; SRR975568     4  0.2340      0.774 0.148 0.000 0.000 0.852 0.000  0
#&gt; SRR975569     2  0.0000      1.000 0.000 1.000 0.000 0.000 0.000  0
#&gt; SRR975570     2  0.0000      1.000 0.000 1.000 0.000 0.000 0.000  0
#&gt; SRR975571     2  0.0000      1.000 0.000 1.000 0.000 0.000 0.000  0
#&gt; SRR975572     2  0.0000      1.000 0.000 1.000 0.000 0.000 0.000  0
#&gt; SRR975573     2  0.0000      1.000 0.000 1.000 0.000 0.000 0.000  0
#&gt; SRR975574     2  0.0000      1.000 0.000 1.000 0.000 0.000 0.000  0
#&gt; SRR975575     2  0.0000      1.000 0.000 1.000 0.000 0.000 0.000  0
#&gt; SRR975576     2  0.0000      1.000 0.000 1.000 0.000 0.000 0.000  0
#&gt; SRR975577     2  0.0000      1.000 0.000 1.000 0.000 0.000 0.000  0
#&gt; SRR975578     2  0.0000      1.000 0.000 1.000 0.000 0.000 0.000  0
#&gt; SRR975579     6  0.0000      1.000 0.000 0.000 0.000 0.000 0.000  1
#&gt; SRR975580     2  0.0000      1.000 0.000 1.000 0.000 0.000 0.000  0
#&gt; SRR975581     2  0.0000      1.000 0.000 1.000 0.000 0.000 0.000  0
#&gt; SRR975582     2  0.0000      1.000 0.000 1.000 0.000 0.000 0.000  0
#&gt; SRR975583     2  0.0000      1.000 0.000 1.000 0.000 0.000 0.000  0
#&gt; SRR975584     2  0.0000      1.000 0.000 1.000 0.000 0.000 0.000  0
#&gt; SRR975585     2  0.0000      1.000 0.000 1.000 0.000 0.000 0.000  0
#&gt; SRR975586     2  0.0000      1.000 0.000 1.000 0.000 0.000 0.000  0
#&gt; SRR975587     3  0.1594      0.820 0.016 0.000 0.932 0.000 0.052  0
#&gt; SRR975588     2  0.0000      1.000 0.000 1.000 0.000 0.000 0.000  0
#&gt; SRR975589     1  0.3221      0.595 0.828 0.000 0.076 0.096 0.000  0
#&gt; SRR975590     1  0.0777      0.698 0.972 0.000 0.024 0.000 0.004  0
#&gt; SRR975591     3  0.0865      0.840 0.036 0.000 0.964 0.000 0.000  0
#&gt; SRR975592     1  0.2668      0.624 0.828 0.000 0.168 0.004 0.000  0
#&gt; SRR975593     1  0.3221      0.595 0.828 0.000 0.076 0.096 0.000  0
#&gt; SRR975594     3  0.3854      0.212 0.000 0.000 0.536 0.000 0.464  0
#&gt; SRR975595     1  0.0458      0.698 0.984 0.000 0.016 0.000 0.000  0
#&gt; SRR975597     1  0.0458      0.698 0.984 0.000 0.016 0.000 0.000  0
#&gt; SRR975596     4  0.3385      0.701 0.032 0.000 0.000 0.788 0.180  0
#&gt; SRR975598     1  0.0458      0.698 0.984 0.000 0.016 0.000 0.000  0
#&gt; SRR975599     5  0.2300      0.000 0.144 0.000 0.000 0.000 0.856  0
#&gt; SRR975600     3  0.3163      0.624 0.232 0.000 0.764 0.004 0.000  0
#&gt; SRR975601     3  0.1594      0.820 0.016 0.000 0.932 0.000 0.052  0
#&gt; SRR975602     1  0.3714      0.561 0.656 0.000 0.000 0.004 0.340  0
#&gt; SRR975603     3  0.0865      0.840 0.036 0.000 0.964 0.000 0.000  0
#&gt; SRR975604     3  0.0865      0.840 0.036 0.000 0.964 0.000 0.000  0
</code></pre>

<script>
$('#tab-SD-hclust-get-classes-5-a').parent().next().next().hide();
$('#tab-SD-hclust-get-classes-5-a').click(function(){
  $('#tab-SD-hclust-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-SD-hclust-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-SD-hclust-consensus-heatmap'>
<ul>
<li><a href='#tab-SD-hclust-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-SD-hclust-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-SD-hclust-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-SD-hclust-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-SD-hclust-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-SD-hclust-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-consensus-heatmap-1-1.png" alt="plot of chunk tab-SD-hclust-consensus-heatmap-1"/></p>

</div>
<div id='tab-SD-hclust-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-consensus-heatmap-2-1.png" alt="plot of chunk tab-SD-hclust-consensus-heatmap-2"/></p>

</div>
<div id='tab-SD-hclust-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-consensus-heatmap-3-1.png" alt="plot of chunk tab-SD-hclust-consensus-heatmap-3"/></p>

</div>
<div id='tab-SD-hclust-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-consensus-heatmap-4-1.png" alt="plot of chunk tab-SD-hclust-consensus-heatmap-4"/></p>

</div>
<div id='tab-SD-hclust-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-consensus-heatmap-5-1.png" alt="plot of chunk tab-SD-hclust-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-SD-hclust-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-SD-hclust-membership-heatmap'>
<ul>
<li><a href='#tab-SD-hclust-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-SD-hclust-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-SD-hclust-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-SD-hclust-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-SD-hclust-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-SD-hclust-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-membership-heatmap-1-1.png" alt="plot of chunk tab-SD-hclust-membership-heatmap-1"/></p>

</div>
<div id='tab-SD-hclust-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-membership-heatmap-2-1.png" alt="plot of chunk tab-SD-hclust-membership-heatmap-2"/></p>

</div>
<div id='tab-SD-hclust-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-membership-heatmap-3-1.png" alt="plot of chunk tab-SD-hclust-membership-heatmap-3"/></p>

</div>
<div id='tab-SD-hclust-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-membership-heatmap-4-1.png" alt="plot of chunk tab-SD-hclust-membership-heatmap-4"/></p>

</div>
<div id='tab-SD-hclust-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-membership-heatmap-5-1.png" alt="plot of chunk tab-SD-hclust-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-SD-hclust-get-signatures' ).tabs();
} );
</script>
<div id='tabs-SD-hclust-get-signatures'>
<ul>
<li><a href='#tab-SD-hclust-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-SD-hclust-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-SD-hclust-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-SD-hclust-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-SD-hclust-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-SD-hclust-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-get-signatures-1-1.png" alt="plot of chunk tab-SD-hclust-get-signatures-1"/></p>

</div>
<div id='tab-SD-hclust-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-get-signatures-2-1.png" alt="plot of chunk tab-SD-hclust-get-signatures-2"/></p>

</div>
<div id='tab-SD-hclust-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-get-signatures-3-1.png" alt="plot of chunk tab-SD-hclust-get-signatures-3"/></p>

</div>
<div id='tab-SD-hclust-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-get-signatures-4-1.png" alt="plot of chunk tab-SD-hclust-get-signatures-4"/></p>

</div>
<div id='tab-SD-hclust-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-get-signatures-5-1.png" alt="plot of chunk tab-SD-hclust-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-SD-hclust-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-SD-hclust-get-signatures-no-scale'>
<ul>
<li><a href='#tab-SD-hclust-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-SD-hclust-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-SD-hclust-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-SD-hclust-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-SD-hclust-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-SD-hclust-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-SD-hclust-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-SD-hclust-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-SD-hclust-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-SD-hclust-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-SD-hclust-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-SD-hclust-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-SD-hclust-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-SD-hclust-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-SD-hclust-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk SD-hclust-signature_compare](figure_cola/SD-hclust-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-SD-hclust-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-SD-hclust-dimension-reduction'>
<ul>
<li><a href='#tab-SD-hclust-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-SD-hclust-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-SD-hclust-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-SD-hclust-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-SD-hclust-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-SD-hclust-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-dimension-reduction-1-1.png" alt="plot of chunk tab-SD-hclust-dimension-reduction-1"/></p>

</div>
<div id='tab-SD-hclust-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-dimension-reduction-2-1.png" alt="plot of chunk tab-SD-hclust-dimension-reduction-2"/></p>

</div>
<div id='tab-SD-hclust-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-dimension-reduction-3-1.png" alt="plot of chunk tab-SD-hclust-dimension-reduction-3"/></p>

</div>
<div id='tab-SD-hclust-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-dimension-reduction-4-1.png" alt="plot of chunk tab-SD-hclust-dimension-reduction-4"/></p>

</div>
<div id='tab-SD-hclust-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-dimension-reduction-5-1.png" alt="plot of chunk tab-SD-hclust-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk SD-hclust-collect-classes](figure_cola/SD-hclust-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### SD:kmeans**






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["SD", "kmeans"]
# you can also extract it by
# res = res_list["SD:kmeans"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 17171 rows and 54 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'SD' method.
#>   Subgroups are detected by 'kmeans' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 2.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk SD-kmeans-collect-plots](figure_cola/SD-kmeans-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk SD-kmeans-select-partition-number](figure_cola/SD-kmeans-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 1.000           0.977       0.985         0.5016 0.497   0.497
#> 3 3 0.722           0.834       0.872         0.2656 0.843   0.685
#> 4 4 0.759           0.708       0.850         0.1056 0.918   0.780
#> 5 5 0.691           0.633       0.791         0.0678 1.000   1.000
#> 6 6 0.721           0.530       0.716         0.0545 0.927   0.784
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 2
```


Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-SD-kmeans-get-classes' ).tabs();
} );
</script>
<div id='tabs-SD-kmeans-get-classes'>
<ul>
<li><a href='#tab-SD-kmeans-get-classes-1'>k = 2</a></li>
<li><a href='#tab-SD-kmeans-get-classes-2'>k = 3</a></li>
<li><a href='#tab-SD-kmeans-get-classes-3'>k = 4</a></li>
<li><a href='#tab-SD-kmeans-get-classes-4'>k = 5</a></li>
<li><a href='#tab-SD-kmeans-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-SD-kmeans-get-classes-1'>
<p><a id='tab-SD-kmeans-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2
#&gt; SRR975551     1   0.204      0.971 0.968 0.032
#&gt; SRR975552     1   0.204      0.971 0.968 0.032
#&gt; SRR975554     1   0.204      0.971 0.968 0.032
#&gt; SRR975553     2   0.000      1.000 0.000 1.000
#&gt; SRR975555     1   0.204      0.971 0.968 0.032
#&gt; SRR975556     2   0.000      1.000 0.000 1.000
#&gt; SRR975557     1   0.204      0.971 0.968 0.032
#&gt; SRR975558     1   0.722      0.785 0.800 0.200
#&gt; SRR975559     1   0.204      0.971 0.968 0.032
#&gt; SRR975560     2   0.000      1.000 0.000 1.000
#&gt; SRR975561     2   0.000      1.000 0.000 1.000
#&gt; SRR975562     1   0.204      0.971 0.968 0.032
#&gt; SRR975563     2   0.000      1.000 0.000 1.000
#&gt; SRR975564     1   0.204      0.971 0.968 0.032
#&gt; SRR975565     1   0.204      0.971 0.968 0.032
#&gt; SRR975566     1   0.204      0.971 0.968 0.032
#&gt; SRR975567     1   0.722      0.785 0.800 0.200
#&gt; SRR975568     1   0.204      0.971 0.968 0.032
#&gt; SRR975569     2   0.000      1.000 0.000 1.000
#&gt; SRR975570     2   0.000      1.000 0.000 1.000
#&gt; SRR975571     2   0.000      1.000 0.000 1.000
#&gt; SRR975572     2   0.000      1.000 0.000 1.000
#&gt; SRR975573     2   0.000      1.000 0.000 1.000
#&gt; SRR975574     2   0.000      1.000 0.000 1.000
#&gt; SRR975575     2   0.000      1.000 0.000 1.000
#&gt; SRR975576     2   0.000      1.000 0.000 1.000
#&gt; SRR975577     2   0.000      1.000 0.000 1.000
#&gt; SRR975578     2   0.000      1.000 0.000 1.000
#&gt; SRR975579     2   0.000      1.000 0.000 1.000
#&gt; SRR975580     2   0.000      1.000 0.000 1.000
#&gt; SRR975581     2   0.000      1.000 0.000 1.000
#&gt; SRR975582     2   0.000      1.000 0.000 1.000
#&gt; SRR975583     2   0.000      1.000 0.000 1.000
#&gt; SRR975584     2   0.000      1.000 0.000 1.000
#&gt; SRR975585     2   0.000      1.000 0.000 1.000
#&gt; SRR975586     2   0.000      1.000 0.000 1.000
#&gt; SRR975587     1   0.000      0.972 1.000 0.000
#&gt; SRR975588     2   0.000      1.000 0.000 1.000
#&gt; SRR975589     1   0.000      0.972 1.000 0.000
#&gt; SRR975590     1   0.000      0.972 1.000 0.000
#&gt; SRR975591     1   0.000      0.972 1.000 0.000
#&gt; SRR975592     1   0.000      0.972 1.000 0.000
#&gt; SRR975593     1   0.000      0.972 1.000 0.000
#&gt; SRR975594     1   0.000      0.972 1.000 0.000
#&gt; SRR975595     1   0.000      0.972 1.000 0.000
#&gt; SRR975597     1   0.000      0.972 1.000 0.000
#&gt; SRR975596     1   0.204      0.971 0.968 0.032
#&gt; SRR975598     1   0.000      0.972 1.000 0.000
#&gt; SRR975599     1   0.000      0.972 1.000 0.000
#&gt; SRR975600     1   0.000      0.972 1.000 0.000
#&gt; SRR975601     1   0.000      0.972 1.000 0.000
#&gt; SRR975602     1   0.204      0.971 0.968 0.032
#&gt; SRR975603     1   0.000      0.972 1.000 0.000
#&gt; SRR975604     1   0.000      0.972 1.000 0.000
</code></pre>

<script>
$('#tab-SD-kmeans-get-classes-1-a').parent().next().next().hide();
$('#tab-SD-kmeans-get-classes-1-a').click(function(){
  $('#tab-SD-kmeans-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-kmeans-get-classes-2'>
<p><a id='tab-SD-kmeans-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3
#&gt; SRR975551     1  0.5098     0.8809 0.752 0.000 0.248
#&gt; SRR975552     1  0.5098     0.8809 0.752 0.000 0.248
#&gt; SRR975554     1  0.5098     0.8809 0.752 0.000 0.248
#&gt; SRR975553     2  0.0592     0.9769 0.012 0.988 0.000
#&gt; SRR975555     1  0.5098     0.8809 0.752 0.000 0.248
#&gt; SRR975556     2  0.0000     0.9787 0.000 1.000 0.000
#&gt; SRR975557     1  0.5948     0.0912 0.640 0.000 0.360
#&gt; SRR975558     1  0.3412     0.7549 0.876 0.000 0.124
#&gt; SRR975559     1  0.4974     0.8760 0.764 0.000 0.236
#&gt; SRR975560     2  0.3412     0.8908 0.124 0.876 0.000
#&gt; SRR975561     2  0.3192     0.9007 0.112 0.888 0.000
#&gt; SRR975562     1  0.4974     0.8760 0.764 0.000 0.236
#&gt; SRR975563     2  0.0000     0.9787 0.000 1.000 0.000
#&gt; SRR975564     1  0.5098     0.8809 0.752 0.000 0.248
#&gt; SRR975565     1  0.5098     0.8809 0.752 0.000 0.248
#&gt; SRR975566     1  0.5098     0.8809 0.752 0.000 0.248
#&gt; SRR975567     1  0.3412     0.7549 0.876 0.000 0.124
#&gt; SRR975568     1  0.5098     0.8809 0.752 0.000 0.248
#&gt; SRR975569     2  0.0000     0.9787 0.000 1.000 0.000
#&gt; SRR975570     2  0.0000     0.9787 0.000 1.000 0.000
#&gt; SRR975571     2  0.0592     0.9769 0.012 0.988 0.000
#&gt; SRR975572     2  0.0000     0.9787 0.000 1.000 0.000
#&gt; SRR975573     2  0.0592     0.9769 0.012 0.988 0.000
#&gt; SRR975574     2  0.0592     0.9769 0.012 0.988 0.000
#&gt; SRR975575     2  0.0000     0.9787 0.000 1.000 0.000
#&gt; SRR975576     2  0.0000     0.9787 0.000 1.000 0.000
#&gt; SRR975577     2  0.0592     0.9769 0.012 0.988 0.000
#&gt; SRR975578     2  0.0592     0.9769 0.012 0.988 0.000
#&gt; SRR975579     2  0.4974     0.7868 0.236 0.764 0.000
#&gt; SRR975580     2  0.0000     0.9787 0.000 1.000 0.000
#&gt; SRR975581     2  0.0000     0.9787 0.000 1.000 0.000
#&gt; SRR975582     2  0.0592     0.9769 0.012 0.988 0.000
#&gt; SRR975583     2  0.0000     0.9787 0.000 1.000 0.000
#&gt; SRR975584     2  0.0592     0.9769 0.012 0.988 0.000
#&gt; SRR975585     2  0.0000     0.9787 0.000 1.000 0.000
#&gt; SRR975586     2  0.0592     0.9732 0.012 0.988 0.000
#&gt; SRR975587     3  0.0000     0.7550 0.000 0.000 1.000
#&gt; SRR975588     2  0.0000     0.9787 0.000 1.000 0.000
#&gt; SRR975589     3  0.4842     0.6797 0.224 0.000 0.776
#&gt; SRR975590     3  0.5529     0.5856 0.296 0.000 0.704
#&gt; SRR975591     3  0.0000     0.7550 0.000 0.000 1.000
#&gt; SRR975592     3  0.4605     0.6923 0.204 0.000 0.796
#&gt; SRR975593     3  0.4842     0.6797 0.224 0.000 0.776
#&gt; SRR975594     3  0.3038     0.6460 0.104 0.000 0.896
#&gt; SRR975595     3  0.5905     0.4783 0.352 0.000 0.648
#&gt; SRR975597     3  0.5905     0.4783 0.352 0.000 0.648
#&gt; SRR975596     1  0.4974     0.8760 0.764 0.000 0.236
#&gt; SRR975598     3  0.5905     0.4783 0.352 0.000 0.648
#&gt; SRR975599     1  0.5497     0.5423 0.708 0.000 0.292
#&gt; SRR975600     3  0.0000     0.7550 0.000 0.000 1.000
#&gt; SRR975601     3  0.0000     0.7550 0.000 0.000 1.000
#&gt; SRR975602     1  0.5098     0.8809 0.752 0.000 0.248
#&gt; SRR975603     3  0.0000     0.7550 0.000 0.000 1.000
#&gt; SRR975604     3  0.0000     0.7550 0.000 0.000 1.000
</code></pre>

<script>
$('#tab-SD-kmeans-get-classes-2-a').parent().next().next().hide();
$('#tab-SD-kmeans-get-classes-2-a').click(function(){
  $('#tab-SD-kmeans-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-kmeans-get-classes-3'>
<p><a id='tab-SD-kmeans-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3    p4
#&gt; SRR975551     1  0.0000     0.7726 1.000 0.000 0.000 0.000
#&gt; SRR975552     1  0.0000     0.7726 1.000 0.000 0.000 0.000
#&gt; SRR975554     1  0.0000     0.7726 1.000 0.000 0.000 0.000
#&gt; SRR975553     2  0.2596     0.8944 0.000 0.908 0.024 0.068
#&gt; SRR975555     1  0.0000     0.7726 1.000 0.000 0.000 0.000
#&gt; SRR975556     2  0.0000     0.9095 0.000 1.000 0.000 0.000
#&gt; SRR975557     4  0.6563     0.2919 0.208 0.000 0.160 0.632
#&gt; SRR975558     1  0.5155     0.1263 0.528 0.000 0.004 0.468
#&gt; SRR975559     1  0.3444     0.6672 0.816 0.000 0.000 0.184
#&gt; SRR975560     2  0.4977     0.0801 0.000 0.540 0.000 0.460
#&gt; SRR975561     2  0.4431     0.5219 0.000 0.696 0.000 0.304
#&gt; SRR975562     1  0.1474     0.7549 0.948 0.000 0.000 0.052
#&gt; SRR975563     2  0.0000     0.9095 0.000 1.000 0.000 0.000
#&gt; SRR975564     1  0.0000     0.7726 1.000 0.000 0.000 0.000
#&gt; SRR975565     1  0.0000     0.7726 1.000 0.000 0.000 0.000
#&gt; SRR975566     1  0.1557     0.7583 0.944 0.000 0.000 0.056
#&gt; SRR975567     1  0.5155     0.1263 0.528 0.000 0.004 0.468
#&gt; SRR975568     1  0.0000     0.7726 1.000 0.000 0.000 0.000
#&gt; SRR975569     2  0.0188     0.9094 0.000 0.996 0.004 0.000
#&gt; SRR975570     2  0.0188     0.9094 0.000 0.996 0.004 0.000
#&gt; SRR975571     2  0.2596     0.8944 0.000 0.908 0.024 0.068
#&gt; SRR975572     2  0.0000     0.9095 0.000 1.000 0.000 0.000
#&gt; SRR975573     2  0.2596     0.8944 0.000 0.908 0.024 0.068
#&gt; SRR975574     2  0.2596     0.8944 0.000 0.908 0.024 0.068
#&gt; SRR975575     2  0.0000     0.9095 0.000 1.000 0.000 0.000
#&gt; SRR975576     2  0.0000     0.9095 0.000 1.000 0.000 0.000
#&gt; SRR975577     2  0.2596     0.8944 0.000 0.908 0.024 0.068
#&gt; SRR975578     2  0.2596     0.8944 0.000 0.908 0.024 0.068
#&gt; SRR975579     4  0.5546     0.3825 0.000 0.292 0.044 0.664
#&gt; SRR975580     2  0.2868     0.8342 0.000 0.864 0.000 0.136
#&gt; SRR975581     2  0.0000     0.9095 0.000 1.000 0.000 0.000
#&gt; SRR975582     2  0.2596     0.8944 0.000 0.908 0.024 0.068
#&gt; SRR975583     2  0.0000     0.9095 0.000 1.000 0.000 0.000
#&gt; SRR975584     2  0.2596     0.8944 0.000 0.908 0.024 0.068
#&gt; SRR975585     2  0.0000     0.9095 0.000 1.000 0.000 0.000
#&gt; SRR975586     2  0.2345     0.8303 0.000 0.900 0.000 0.100
#&gt; SRR975587     3  0.3071     0.7970 0.068 0.000 0.888 0.044
#&gt; SRR975588     2  0.0188     0.9094 0.000 0.996 0.004 0.000
#&gt; SRR975589     3  0.6730     0.6168 0.276 0.000 0.592 0.132
#&gt; SRR975590     3  0.7379     0.3850 0.364 0.000 0.468 0.168
#&gt; SRR975591     3  0.1792     0.8041 0.068 0.000 0.932 0.000
#&gt; SRR975592     3  0.6274     0.7091 0.184 0.000 0.664 0.152
#&gt; SRR975593     3  0.6730     0.6168 0.276 0.000 0.592 0.132
#&gt; SRR975594     3  0.2775     0.7224 0.020 0.000 0.896 0.084
#&gt; SRR975595     1  0.7099     0.1741 0.552 0.000 0.280 0.168
#&gt; SRR975597     1  0.7099     0.1741 0.552 0.000 0.280 0.168
#&gt; SRR975596     1  0.3444     0.6672 0.816 0.000 0.000 0.184
#&gt; SRR975598     1  0.7099     0.1741 0.552 0.000 0.280 0.168
#&gt; SRR975599     1  0.5339     0.5115 0.688 0.000 0.040 0.272
#&gt; SRR975600     3  0.3398     0.7958 0.068 0.000 0.872 0.060
#&gt; SRR975601     3  0.3071     0.7970 0.068 0.000 0.888 0.044
#&gt; SRR975602     1  0.2530     0.7238 0.888 0.000 0.000 0.112
#&gt; SRR975603     3  0.1792     0.8041 0.068 0.000 0.932 0.000
#&gt; SRR975604     3  0.1792     0.8041 0.068 0.000 0.932 0.000
</code></pre>

<script>
$('#tab-SD-kmeans-get-classes-3-a').parent().next().next().hide();
$('#tab-SD-kmeans-get-classes-3-a').click(function(){
  $('#tab-SD-kmeans-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-kmeans-get-classes-4'>
<p><a id='tab-SD-kmeans-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3    p4 p5
#&gt; SRR975551     1  0.0162     0.6907 0.996 0.000 0.000 0.000 NA
#&gt; SRR975552     1  0.0324     0.6915 0.992 0.000 0.000 0.004 NA
#&gt; SRR975554     1  0.1082     0.6900 0.964 0.000 0.000 0.008 NA
#&gt; SRR975553     2  0.4003     0.7431 0.000 0.704 0.000 0.008 NA
#&gt; SRR975555     1  0.1106     0.6880 0.964 0.000 0.000 0.012 NA
#&gt; SRR975556     2  0.0898     0.7992 0.000 0.972 0.000 0.008 NA
#&gt; SRR975557     4  0.4308     0.6762 0.104 0.000 0.040 0.804 NA
#&gt; SRR975558     1  0.6696    -0.0634 0.388 0.000 0.000 0.372 NA
#&gt; SRR975559     1  0.5107     0.5572 0.688 0.000 0.000 0.108 NA
#&gt; SRR975560     2  0.6534     0.1266 0.000 0.460 0.000 0.328 NA
#&gt; SRR975561     2  0.5197     0.5221 0.000 0.680 0.000 0.204 NA
#&gt; SRR975562     1  0.3656     0.6384 0.800 0.000 0.000 0.032 NA
#&gt; SRR975563     2  0.0000     0.8129 0.000 1.000 0.000 0.000 NA
#&gt; SRR975564     1  0.1670     0.6858 0.936 0.000 0.000 0.012 NA
#&gt; SRR975565     1  0.0324     0.6913 0.992 0.000 0.000 0.004 NA
#&gt; SRR975566     1  0.3844     0.6376 0.792 0.000 0.000 0.044 NA
#&gt; SRR975567     1  0.6696    -0.0634 0.388 0.000 0.000 0.372 NA
#&gt; SRR975568     1  0.1012     0.6884 0.968 0.000 0.000 0.012 NA
#&gt; SRR975569     2  0.0290     0.8130 0.000 0.992 0.000 0.000 NA
#&gt; SRR975570     2  0.0290     0.8130 0.000 0.992 0.000 0.000 NA
#&gt; SRR975571     2  0.4003     0.7431 0.000 0.704 0.000 0.008 NA
#&gt; SRR975572     2  0.0000     0.8129 0.000 1.000 0.000 0.000 NA
#&gt; SRR975573     2  0.3730     0.7469 0.000 0.712 0.000 0.000 NA
#&gt; SRR975574     2  0.3730     0.7469 0.000 0.712 0.000 0.000 NA
#&gt; SRR975575     2  0.0000     0.8129 0.000 1.000 0.000 0.000 NA
#&gt; SRR975576     2  0.0000     0.8129 0.000 1.000 0.000 0.000 NA
#&gt; SRR975577     2  0.3730     0.7469 0.000 0.712 0.000 0.000 NA
#&gt; SRR975578     2  0.3730     0.7469 0.000 0.712 0.000 0.000 NA
#&gt; SRR975579     4  0.2588     0.7165 0.000 0.100 0.008 0.884 NA
#&gt; SRR975580     2  0.5264     0.6221 0.000 0.676 0.000 0.128 NA
#&gt; SRR975581     2  0.0000     0.8129 0.000 1.000 0.000 0.000 NA
#&gt; SRR975582     2  0.3730     0.7469 0.000 0.712 0.000 0.000 NA
#&gt; SRR975583     2  0.0000     0.8129 0.000 1.000 0.000 0.000 NA
#&gt; SRR975584     2  0.3730     0.7469 0.000 0.712 0.000 0.000 NA
#&gt; SRR975585     2  0.0000     0.8129 0.000 1.000 0.000 0.000 NA
#&gt; SRR975586     2  0.4450     0.6282 0.000 0.760 0.000 0.132 NA
#&gt; SRR975587     3  0.3210     0.7474 0.008 0.000 0.860 0.040 NA
#&gt; SRR975588     2  0.0290     0.8130 0.000 0.992 0.000 0.000 NA
#&gt; SRR975589     3  0.5814     0.6080 0.136 0.000 0.652 0.016 NA
#&gt; SRR975590     3  0.6902     0.1891 0.324 0.000 0.392 0.004 NA
#&gt; SRR975591     3  0.0290     0.7749 0.008 0.000 0.992 0.000 NA
#&gt; SRR975592     3  0.4818     0.6767 0.100 0.000 0.720 0.000 NA
#&gt; SRR975593     3  0.5814     0.6080 0.136 0.000 0.652 0.016 NA
#&gt; SRR975594     3  0.3579     0.7085 0.000 0.000 0.828 0.072 NA
#&gt; SRR975595     1  0.6665     0.1948 0.480 0.000 0.244 0.004 NA
#&gt; SRR975597     1  0.6665     0.1948 0.480 0.000 0.244 0.004 NA
#&gt; SRR975596     1  0.5197     0.5486 0.680 0.000 0.000 0.116 NA
#&gt; SRR975598     1  0.6665     0.1948 0.480 0.000 0.244 0.004 NA
#&gt; SRR975599     1  0.6280     0.3902 0.560 0.000 0.008 0.160 NA
#&gt; SRR975600     3  0.1628     0.7679 0.008 0.000 0.936 0.000 NA
#&gt; SRR975601     3  0.3229     0.7465 0.008 0.000 0.860 0.044 NA
#&gt; SRR975602     1  0.4104     0.5870 0.748 0.000 0.000 0.032 NA
#&gt; SRR975603     3  0.0290     0.7749 0.008 0.000 0.992 0.000 NA
#&gt; SRR975604     3  0.0290     0.7749 0.008 0.000 0.992 0.000 NA
</code></pre>

<script>
$('#tab-SD-kmeans-get-classes-4-a').parent().next().next().hide();
$('#tab-SD-kmeans-get-classes-4-a').click(function(){
  $('#tab-SD-kmeans-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-kmeans-get-classes-5'>
<p><a id='tab-SD-kmeans-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3    p4 p5    p6
#&gt; SRR975551     1  0.0000     0.6382 1.000 0.000 0.000 0.000 NA 0.000
#&gt; SRR975552     1  0.0146     0.6383 0.996 0.000 0.000 0.000 NA 0.004
#&gt; SRR975554     1  0.1909     0.6283 0.920 0.000 0.000 0.004 NA 0.052
#&gt; SRR975553     2  0.4169     0.5570 0.000 0.532 0.000 0.012 NA 0.000
#&gt; SRR975555     1  0.1003     0.6333 0.964 0.000 0.000 0.004 NA 0.028
#&gt; SRR975556     2  0.2803     0.5613 0.000 0.872 0.000 0.012 NA 0.052
#&gt; SRR975557     4  0.3390     0.7994 0.032 0.000 0.008 0.808 NA 0.152
#&gt; SRR975558     6  0.3473     0.2404 0.192 0.000 0.004 0.024 NA 0.780
#&gt; SRR975559     1  0.6042     0.4033 0.532 0.000 0.004 0.108 NA 0.320
#&gt; SRR975560     6  0.5610     0.3060 0.004 0.252 0.000 0.016 NA 0.600
#&gt; SRR975561     2  0.5454    -0.2994 0.000 0.460 0.000 0.020 NA 0.452
#&gt; SRR975562     1  0.5304     0.4770 0.620 0.000 0.000 0.060 NA 0.280
#&gt; SRR975563     2  0.0291     0.6778 0.000 0.992 0.000 0.004 NA 0.000
#&gt; SRR975564     1  0.2214     0.6170 0.892 0.000 0.000 0.004 NA 0.092
#&gt; SRR975565     1  0.0551     0.6368 0.984 0.000 0.000 0.004 NA 0.008
#&gt; SRR975566     1  0.5469     0.5087 0.640 0.000 0.004 0.096 NA 0.228
#&gt; SRR975567     6  0.3534     0.2405 0.200 0.000 0.004 0.024 NA 0.772
#&gt; SRR975568     1  0.1080     0.6330 0.960 0.000 0.000 0.004 NA 0.032
#&gt; SRR975569     2  0.0260     0.6819 0.000 0.992 0.000 0.000 NA 0.000
#&gt; SRR975570     2  0.0260     0.6819 0.000 0.992 0.000 0.000 NA 0.000
#&gt; SRR975571     2  0.4169     0.5570 0.000 0.532 0.000 0.012 NA 0.000
#&gt; SRR975572     2  0.0146     0.6802 0.000 0.996 0.000 0.004 NA 0.000
#&gt; SRR975573     2  0.3851     0.5645 0.000 0.540 0.000 0.000 NA 0.000
#&gt; SRR975574     2  0.3851     0.5645 0.000 0.540 0.000 0.000 NA 0.000
#&gt; SRR975575     2  0.0146     0.6802 0.000 0.996 0.000 0.004 NA 0.000
#&gt; SRR975576     2  0.0000     0.6812 0.000 1.000 0.000 0.000 NA 0.000
#&gt; SRR975577     2  0.3851     0.5645 0.000 0.540 0.000 0.000 NA 0.000
#&gt; SRR975578     2  0.3851     0.5645 0.000 0.540 0.000 0.000 NA 0.000
#&gt; SRR975579     4  0.3678     0.7855 0.000 0.016 0.000 0.748 NA 0.228
#&gt; SRR975580     6  0.6181     0.0654 0.000 0.396 0.000 0.016 NA 0.408
#&gt; SRR975581     2  0.0146     0.6802 0.000 0.996 0.000 0.004 NA 0.000
#&gt; SRR975582     2  0.3851     0.5645 0.000 0.540 0.000 0.000 NA 0.000
#&gt; SRR975583     2  0.0146     0.6802 0.000 0.996 0.000 0.004 NA 0.000
#&gt; SRR975584     2  0.3851     0.5645 0.000 0.540 0.000 0.000 NA 0.000
#&gt; SRR975585     2  0.0000     0.6812 0.000 1.000 0.000 0.000 NA 0.000
#&gt; SRR975586     2  0.5358    -0.1037 0.000 0.544 0.000 0.020 NA 0.368
#&gt; SRR975587     3  0.2979     0.7452 0.000 0.000 0.868 0.044 NA 0.036
#&gt; SRR975588     2  0.0260     0.6819 0.000 0.992 0.000 0.000 NA 0.000
#&gt; SRR975589     3  0.7006     0.5061 0.064 0.000 0.544 0.068 NA 0.224
#&gt; SRR975590     1  0.7900     0.0190 0.316 0.000 0.280 0.060 NA 0.060
#&gt; SRR975591     3  0.0000     0.7786 0.000 0.000 1.000 0.000 NA 0.000
#&gt; SRR975592     3  0.6089     0.5980 0.088 0.000 0.648 0.048 NA 0.052
#&gt; SRR975593     3  0.7006     0.5061 0.064 0.000 0.544 0.068 NA 0.224
#&gt; SRR975594     3  0.4235     0.6787 0.000 0.000 0.780 0.064 NA 0.052
#&gt; SRR975595     1  0.7595     0.2593 0.400 0.000 0.196 0.060 NA 0.048
#&gt; SRR975597     1  0.7539     0.2632 0.408 0.000 0.196 0.060 NA 0.044
#&gt; SRR975596     1  0.6100     0.4000 0.528 0.000 0.004 0.108 NA 0.320
#&gt; SRR975598     1  0.7595     0.2593 0.400 0.000 0.196 0.060 NA 0.048
#&gt; SRR975599     1  0.6868     0.2921 0.452 0.000 0.000 0.120 NA 0.120
#&gt; SRR975600     3  0.2345     0.7562 0.000 0.000 0.904 0.028 NA 0.028
#&gt; SRR975601     3  0.2985     0.7435 0.000 0.000 0.868 0.048 NA 0.040
#&gt; SRR975602     1  0.5389     0.5221 0.664 0.000 0.000 0.060 NA 0.084
#&gt; SRR975603     3  0.0000     0.7786 0.000 0.000 1.000 0.000 NA 0.000
#&gt; SRR975604     3  0.0000     0.7786 0.000 0.000 1.000 0.000 NA 0.000
</code></pre>

<script>
$('#tab-SD-kmeans-get-classes-5-a').parent().next().next().hide();
$('#tab-SD-kmeans-get-classes-5-a').click(function(){
  $('#tab-SD-kmeans-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-SD-kmeans-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-SD-kmeans-consensus-heatmap'>
<ul>
<li><a href='#tab-SD-kmeans-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-SD-kmeans-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-SD-kmeans-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-SD-kmeans-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-SD-kmeans-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-SD-kmeans-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-consensus-heatmap-1-1.png" alt="plot of chunk tab-SD-kmeans-consensus-heatmap-1"/></p>

</div>
<div id='tab-SD-kmeans-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-consensus-heatmap-2-1.png" alt="plot of chunk tab-SD-kmeans-consensus-heatmap-2"/></p>

</div>
<div id='tab-SD-kmeans-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-consensus-heatmap-3-1.png" alt="plot of chunk tab-SD-kmeans-consensus-heatmap-3"/></p>

</div>
<div id='tab-SD-kmeans-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-consensus-heatmap-4-1.png" alt="plot of chunk tab-SD-kmeans-consensus-heatmap-4"/></p>

</div>
<div id='tab-SD-kmeans-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-consensus-heatmap-5-1.png" alt="plot of chunk tab-SD-kmeans-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-SD-kmeans-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-SD-kmeans-membership-heatmap'>
<ul>
<li><a href='#tab-SD-kmeans-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-SD-kmeans-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-SD-kmeans-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-SD-kmeans-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-SD-kmeans-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-SD-kmeans-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-membership-heatmap-1-1.png" alt="plot of chunk tab-SD-kmeans-membership-heatmap-1"/></p>

</div>
<div id='tab-SD-kmeans-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-membership-heatmap-2-1.png" alt="plot of chunk tab-SD-kmeans-membership-heatmap-2"/></p>

</div>
<div id='tab-SD-kmeans-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-membership-heatmap-3-1.png" alt="plot of chunk tab-SD-kmeans-membership-heatmap-3"/></p>

</div>
<div id='tab-SD-kmeans-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-membership-heatmap-4-1.png" alt="plot of chunk tab-SD-kmeans-membership-heatmap-4"/></p>

</div>
<div id='tab-SD-kmeans-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-membership-heatmap-5-1.png" alt="plot of chunk tab-SD-kmeans-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-SD-kmeans-get-signatures' ).tabs();
} );
</script>
<div id='tabs-SD-kmeans-get-signatures'>
<ul>
<li><a href='#tab-SD-kmeans-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-SD-kmeans-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-SD-kmeans-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-SD-kmeans-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-SD-kmeans-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-SD-kmeans-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-get-signatures-1-1.png" alt="plot of chunk tab-SD-kmeans-get-signatures-1"/></p>

</div>
<div id='tab-SD-kmeans-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-get-signatures-2-1.png" alt="plot of chunk tab-SD-kmeans-get-signatures-2"/></p>

</div>
<div id='tab-SD-kmeans-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-get-signatures-3-1.png" alt="plot of chunk tab-SD-kmeans-get-signatures-3"/></p>

</div>
<div id='tab-SD-kmeans-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-get-signatures-4-1.png" alt="plot of chunk tab-SD-kmeans-get-signatures-4"/></p>

</div>
<div id='tab-SD-kmeans-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-get-signatures-5-1.png" alt="plot of chunk tab-SD-kmeans-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-SD-kmeans-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-SD-kmeans-get-signatures-no-scale'>
<ul>
<li><a href='#tab-SD-kmeans-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-SD-kmeans-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-SD-kmeans-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-SD-kmeans-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-SD-kmeans-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-SD-kmeans-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-SD-kmeans-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-SD-kmeans-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-SD-kmeans-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-SD-kmeans-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-SD-kmeans-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-SD-kmeans-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-SD-kmeans-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-SD-kmeans-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-SD-kmeans-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk SD-kmeans-signature_compare](figure_cola/SD-kmeans-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-SD-kmeans-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-SD-kmeans-dimension-reduction'>
<ul>
<li><a href='#tab-SD-kmeans-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-SD-kmeans-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-SD-kmeans-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-SD-kmeans-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-SD-kmeans-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-SD-kmeans-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-dimension-reduction-1-1.png" alt="plot of chunk tab-SD-kmeans-dimension-reduction-1"/></p>

</div>
<div id='tab-SD-kmeans-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-dimension-reduction-2-1.png" alt="plot of chunk tab-SD-kmeans-dimension-reduction-2"/></p>

</div>
<div id='tab-SD-kmeans-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-dimension-reduction-3-1.png" alt="plot of chunk tab-SD-kmeans-dimension-reduction-3"/></p>

</div>
<div id='tab-SD-kmeans-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-dimension-reduction-4-1.png" alt="plot of chunk tab-SD-kmeans-dimension-reduction-4"/></p>

</div>
<div id='tab-SD-kmeans-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-dimension-reduction-5-1.png" alt="plot of chunk tab-SD-kmeans-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk SD-kmeans-collect-classes](figure_cola/SD-kmeans-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### SD:skmeans*






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["SD", "skmeans"]
# you can also extract it by
# res = res_list["SD:skmeans"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 17171 rows and 54 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'SD' method.
#>   Subgroups are detected by 'skmeans' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 4.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk SD-skmeans-collect-plots](figure_cola/SD-skmeans-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk SD-skmeans-select-partition-number](figure_cola/SD-skmeans-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 1.000           0.970       0.988         0.5056 0.497   0.497
#> 3 3 0.925           0.926       0.966         0.3025 0.843   0.685
#> 4 4 0.902           0.861       0.937         0.0885 0.918   0.769
#> 5 5 0.815           0.695       0.838         0.0513 0.979   0.927
#> 6 6 0.722           0.600       0.732         0.0442 0.943   0.794
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 4
#> attr(,"optional")
#> [1] 2 3
```

There is also optional best $k$ = 2 3 that is worth to check.

Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-SD-skmeans-get-classes' ).tabs();
} );
</script>
<div id='tabs-SD-skmeans-get-classes'>
<ul>
<li><a href='#tab-SD-skmeans-get-classes-1'>k = 2</a></li>
<li><a href='#tab-SD-skmeans-get-classes-2'>k = 3</a></li>
<li><a href='#tab-SD-skmeans-get-classes-3'>k = 4</a></li>
<li><a href='#tab-SD-skmeans-get-classes-4'>k = 5</a></li>
<li><a href='#tab-SD-skmeans-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-SD-skmeans-get-classes-1'>
<p><a id='tab-SD-skmeans-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2
#&gt; SRR975551     1   0.000      0.977 1.000 0.000
#&gt; SRR975552     1   0.000      0.977 1.000 0.000
#&gt; SRR975554     1   0.000      0.977 1.000 0.000
#&gt; SRR975553     2   0.000      1.000 0.000 1.000
#&gt; SRR975555     1   0.000      0.977 1.000 0.000
#&gt; SRR975556     2   0.000      1.000 0.000 1.000
#&gt; SRR975557     1   0.000      0.977 1.000 0.000
#&gt; SRR975558     1   0.955      0.417 0.624 0.376
#&gt; SRR975559     1   0.000      0.977 1.000 0.000
#&gt; SRR975560     2   0.000      1.000 0.000 1.000
#&gt; SRR975561     2   0.000      1.000 0.000 1.000
#&gt; SRR975562     1   0.000      0.977 1.000 0.000
#&gt; SRR975563     2   0.000      1.000 0.000 1.000
#&gt; SRR975564     1   0.000      0.977 1.000 0.000
#&gt; SRR975565     1   0.000      0.977 1.000 0.000
#&gt; SRR975566     1   0.000      0.977 1.000 0.000
#&gt; SRR975567     1   0.866      0.604 0.712 0.288
#&gt; SRR975568     1   0.000      0.977 1.000 0.000
#&gt; SRR975569     2   0.000      1.000 0.000 1.000
#&gt; SRR975570     2   0.000      1.000 0.000 1.000
#&gt; SRR975571     2   0.000      1.000 0.000 1.000
#&gt; SRR975572     2   0.000      1.000 0.000 1.000
#&gt; SRR975573     2   0.000      1.000 0.000 1.000
#&gt; SRR975574     2   0.000      1.000 0.000 1.000
#&gt; SRR975575     2   0.000      1.000 0.000 1.000
#&gt; SRR975576     2   0.000      1.000 0.000 1.000
#&gt; SRR975577     2   0.000      1.000 0.000 1.000
#&gt; SRR975578     2   0.000      1.000 0.000 1.000
#&gt; SRR975579     2   0.000      1.000 0.000 1.000
#&gt; SRR975580     2   0.000      1.000 0.000 1.000
#&gt; SRR975581     2   0.000      1.000 0.000 1.000
#&gt; SRR975582     2   0.000      1.000 0.000 1.000
#&gt; SRR975583     2   0.000      1.000 0.000 1.000
#&gt; SRR975584     2   0.000      1.000 0.000 1.000
#&gt; SRR975585     2   0.000      1.000 0.000 1.000
#&gt; SRR975586     2   0.000      1.000 0.000 1.000
#&gt; SRR975587     1   0.000      0.977 1.000 0.000
#&gt; SRR975588     2   0.000      1.000 0.000 1.000
#&gt; SRR975589     1   0.000      0.977 1.000 0.000
#&gt; SRR975590     1   0.000      0.977 1.000 0.000
#&gt; SRR975591     1   0.000      0.977 1.000 0.000
#&gt; SRR975592     1   0.000      0.977 1.000 0.000
#&gt; SRR975593     1   0.000      0.977 1.000 0.000
#&gt; SRR975594     1   0.000      0.977 1.000 0.000
#&gt; SRR975595     1   0.000      0.977 1.000 0.000
#&gt; SRR975597     1   0.000      0.977 1.000 0.000
#&gt; SRR975596     1   0.000      0.977 1.000 0.000
#&gt; SRR975598     1   0.000      0.977 1.000 0.000
#&gt; SRR975599     1   0.000      0.977 1.000 0.000
#&gt; SRR975600     1   0.000      0.977 1.000 0.000
#&gt; SRR975601     1   0.000      0.977 1.000 0.000
#&gt; SRR975602     1   0.000      0.977 1.000 0.000
#&gt; SRR975603     1   0.000      0.977 1.000 0.000
#&gt; SRR975604     1   0.000      0.977 1.000 0.000
</code></pre>

<script>
$('#tab-SD-skmeans-get-classes-1-a').parent().next().next().hide();
$('#tab-SD-skmeans-get-classes-1-a').click(function(){
  $('#tab-SD-skmeans-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-skmeans-get-classes-2'>
<p><a id='tab-SD-skmeans-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1 p2    p3
#&gt; SRR975551     1  0.0000      1.000 1.000  0 0.000
#&gt; SRR975552     1  0.0000      1.000 1.000  0 0.000
#&gt; SRR975554     1  0.0000      1.000 1.000  0 0.000
#&gt; SRR975553     2  0.0000      1.000 0.000  1 0.000
#&gt; SRR975555     1  0.0000      1.000 1.000  0 0.000
#&gt; SRR975556     2  0.0000      1.000 0.000  1 0.000
#&gt; SRR975557     3  0.6062      0.380 0.384  0 0.616
#&gt; SRR975558     1  0.0000      1.000 1.000  0 0.000
#&gt; SRR975559     1  0.0000      1.000 1.000  0 0.000
#&gt; SRR975560     2  0.0000      1.000 0.000  1 0.000
#&gt; SRR975561     2  0.0000      1.000 0.000  1 0.000
#&gt; SRR975562     1  0.0000      1.000 1.000  0 0.000
#&gt; SRR975563     2  0.0000      1.000 0.000  1 0.000
#&gt; SRR975564     1  0.0000      1.000 1.000  0 0.000
#&gt; SRR975565     1  0.0000      1.000 1.000  0 0.000
#&gt; SRR975566     1  0.0000      1.000 1.000  0 0.000
#&gt; SRR975567     1  0.0000      1.000 1.000  0 0.000
#&gt; SRR975568     1  0.0000      1.000 1.000  0 0.000
#&gt; SRR975569     2  0.0000      1.000 0.000  1 0.000
#&gt; SRR975570     2  0.0000      1.000 0.000  1 0.000
#&gt; SRR975571     2  0.0000      1.000 0.000  1 0.000
#&gt; SRR975572     2  0.0000      1.000 0.000  1 0.000
#&gt; SRR975573     2  0.0000      1.000 0.000  1 0.000
#&gt; SRR975574     2  0.0000      1.000 0.000  1 0.000
#&gt; SRR975575     2  0.0000      1.000 0.000  1 0.000
#&gt; SRR975576     2  0.0000      1.000 0.000  1 0.000
#&gt; SRR975577     2  0.0000      1.000 0.000  1 0.000
#&gt; SRR975578     2  0.0000      1.000 0.000  1 0.000
#&gt; SRR975579     2  0.0000      1.000 0.000  1 0.000
#&gt; SRR975580     2  0.0000      1.000 0.000  1 0.000
#&gt; SRR975581     2  0.0000      1.000 0.000  1 0.000
#&gt; SRR975582     2  0.0000      1.000 0.000  1 0.000
#&gt; SRR975583     2  0.0000      1.000 0.000  1 0.000
#&gt; SRR975584     2  0.0000      1.000 0.000  1 0.000
#&gt; SRR975585     2  0.0000      1.000 0.000  1 0.000
#&gt; SRR975586     2  0.0000      1.000 0.000  1 0.000
#&gt; SRR975587     3  0.0000      0.868 0.000  0 1.000
#&gt; SRR975588     2  0.0000      1.000 0.000  1 0.000
#&gt; SRR975589     3  0.0747      0.865 0.016  0 0.984
#&gt; SRR975590     3  0.4654      0.725 0.208  0 0.792
#&gt; SRR975591     3  0.0000      0.868 0.000  0 1.000
#&gt; SRR975592     3  0.0592      0.866 0.012  0 0.988
#&gt; SRR975593     3  0.0592      0.866 0.012  0 0.988
#&gt; SRR975594     3  0.0000      0.868 0.000  0 1.000
#&gt; SRR975595     3  0.6126      0.464 0.400  0 0.600
#&gt; SRR975597     3  0.6126      0.464 0.400  0 0.600
#&gt; SRR975596     1  0.0000      1.000 1.000  0 0.000
#&gt; SRR975598     3  0.6126      0.464 0.400  0 0.600
#&gt; SRR975599     3  0.1031      0.858 0.024  0 0.976
#&gt; SRR975600     3  0.0000      0.868 0.000  0 1.000
#&gt; SRR975601     3  0.0000      0.868 0.000  0 1.000
#&gt; SRR975602     1  0.0000      1.000 1.000  0 0.000
#&gt; SRR975603     3  0.0000      0.868 0.000  0 1.000
#&gt; SRR975604     3  0.0000      0.868 0.000  0 1.000
</code></pre>

<script>
$('#tab-SD-skmeans-get-classes-2-a').parent().next().next().hide();
$('#tab-SD-skmeans-get-classes-2-a').click(function(){
  $('#tab-SD-skmeans-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-skmeans-get-classes-3'>
<p><a id='tab-SD-skmeans-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3    p4
#&gt; SRR975551     1  0.0000      0.897 1.000 0.000 0.000 0.000
#&gt; SRR975552     1  0.0000      0.897 1.000 0.000 0.000 0.000
#&gt; SRR975554     1  0.0000      0.897 1.000 0.000 0.000 0.000
#&gt; SRR975553     2  0.0336      0.982 0.000 0.992 0.000 0.008
#&gt; SRR975555     1  0.0000      0.897 1.000 0.000 0.000 0.000
#&gt; SRR975556     2  0.0000      0.983 0.000 1.000 0.000 0.000
#&gt; SRR975557     4  0.2676      0.862 0.092 0.000 0.012 0.896
#&gt; SRR975558     4  0.1792      0.897 0.068 0.000 0.000 0.932
#&gt; SRR975559     1  0.4804      0.345 0.616 0.000 0.000 0.384
#&gt; SRR975560     4  0.1792      0.876 0.000 0.068 0.000 0.932
#&gt; SRR975561     2  0.3610      0.751 0.000 0.800 0.000 0.200
#&gt; SRR975562     1  0.0817      0.883 0.976 0.000 0.000 0.024
#&gt; SRR975563     2  0.0000      0.983 0.000 1.000 0.000 0.000
#&gt; SRR975564     1  0.0000      0.897 1.000 0.000 0.000 0.000
#&gt; SRR975565     1  0.0000      0.897 1.000 0.000 0.000 0.000
#&gt; SRR975566     1  0.0469      0.891 0.988 0.000 0.000 0.012
#&gt; SRR975567     4  0.1792      0.897 0.068 0.000 0.000 0.932
#&gt; SRR975568     1  0.0000      0.897 1.000 0.000 0.000 0.000
#&gt; SRR975569     2  0.0000      0.983 0.000 1.000 0.000 0.000
#&gt; SRR975570     2  0.0000      0.983 0.000 1.000 0.000 0.000
#&gt; SRR975571     2  0.0336      0.982 0.000 0.992 0.000 0.008
#&gt; SRR975572     2  0.0000      0.983 0.000 1.000 0.000 0.000
#&gt; SRR975573     2  0.0336      0.982 0.000 0.992 0.000 0.008
#&gt; SRR975574     2  0.0336      0.982 0.000 0.992 0.000 0.008
#&gt; SRR975575     2  0.0000      0.983 0.000 1.000 0.000 0.000
#&gt; SRR975576     2  0.0000      0.983 0.000 1.000 0.000 0.000
#&gt; SRR975577     2  0.0336      0.982 0.000 0.992 0.000 0.008
#&gt; SRR975578     2  0.0336      0.982 0.000 0.992 0.000 0.008
#&gt; SRR975579     4  0.2401      0.864 0.000 0.092 0.004 0.904
#&gt; SRR975580     2  0.0336      0.982 0.000 0.992 0.000 0.008
#&gt; SRR975581     2  0.0000      0.983 0.000 1.000 0.000 0.000
#&gt; SRR975582     2  0.0336      0.982 0.000 0.992 0.000 0.008
#&gt; SRR975583     2  0.0000      0.983 0.000 1.000 0.000 0.000
#&gt; SRR975584     2  0.0336      0.982 0.000 0.992 0.000 0.008
#&gt; SRR975585     2  0.0000      0.983 0.000 1.000 0.000 0.000
#&gt; SRR975586     2  0.1867      0.917 0.000 0.928 0.000 0.072
#&gt; SRR975587     3  0.0000      0.850 0.000 0.000 1.000 0.000
#&gt; SRR975588     2  0.0000      0.983 0.000 1.000 0.000 0.000
#&gt; SRR975589     3  0.1059      0.841 0.016 0.000 0.972 0.012
#&gt; SRR975590     3  0.4331      0.646 0.288 0.000 0.712 0.000
#&gt; SRR975591     3  0.0000      0.850 0.000 0.000 1.000 0.000
#&gt; SRR975592     3  0.0188      0.850 0.004 0.000 0.996 0.000
#&gt; SRR975593     3  0.0657      0.845 0.004 0.000 0.984 0.012
#&gt; SRR975594     3  0.0469      0.844 0.000 0.000 0.988 0.012
#&gt; SRR975595     3  0.4916      0.455 0.424 0.000 0.576 0.000
#&gt; SRR975597     3  0.4916      0.455 0.424 0.000 0.576 0.000
#&gt; SRR975596     1  0.4817      0.335 0.612 0.000 0.000 0.388
#&gt; SRR975598     3  0.4933      0.438 0.432 0.000 0.568 0.000
#&gt; SRR975599     1  0.4761      0.659 0.764 0.000 0.192 0.044
#&gt; SRR975600     3  0.0000      0.850 0.000 0.000 1.000 0.000
#&gt; SRR975601     3  0.0000      0.850 0.000 0.000 1.000 0.000
#&gt; SRR975602     1  0.0000      0.897 1.000 0.000 0.000 0.000
#&gt; SRR975603     3  0.0000      0.850 0.000 0.000 1.000 0.000
#&gt; SRR975604     3  0.0000      0.850 0.000 0.000 1.000 0.000
</code></pre>

<script>
$('#tab-SD-skmeans-get-classes-3-a').parent().next().next().hide();
$('#tab-SD-skmeans-get-classes-3-a').click(function(){
  $('#tab-SD-skmeans-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-skmeans-get-classes-4'>
<p><a id='tab-SD-skmeans-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3    p4    p5
#&gt; SRR975551     1  0.0404     0.7622 0.988 0.000 0.000 0.000 0.012
#&gt; SRR975552     1  0.0162     0.7664 0.996 0.000 0.000 0.000 0.004
#&gt; SRR975554     1  0.0794     0.7655 0.972 0.000 0.000 0.000 0.028
#&gt; SRR975553     2  0.1851     0.9018 0.000 0.912 0.000 0.000 0.088
#&gt; SRR975555     1  0.1041     0.7548 0.964 0.000 0.000 0.004 0.032
#&gt; SRR975556     2  0.1485     0.8812 0.000 0.948 0.000 0.032 0.020
#&gt; SRR975557     4  0.4295     0.1097 0.032 0.000 0.012 0.760 0.196
#&gt; SRR975558     5  0.5525     0.9863 0.124 0.000 0.000 0.240 0.636
#&gt; SRR975559     1  0.5032     0.1287 0.520 0.000 0.000 0.032 0.448
#&gt; SRR975560     4  0.4227     0.1383 0.000 0.016 0.000 0.692 0.292
#&gt; SRR975561     4  0.4900     0.1029 0.000 0.464 0.000 0.512 0.024
#&gt; SRR975562     1  0.3928     0.5525 0.700 0.000 0.000 0.004 0.296
#&gt; SRR975563     2  0.0162     0.9143 0.000 0.996 0.000 0.004 0.000
#&gt; SRR975564     1  0.1357     0.7586 0.948 0.000 0.000 0.004 0.048
#&gt; SRR975565     1  0.0566     0.7664 0.984 0.000 0.000 0.004 0.012
#&gt; SRR975566     1  0.3508     0.5947 0.748 0.000 0.000 0.000 0.252
#&gt; SRR975567     5  0.5531     0.9862 0.120 0.000 0.000 0.248 0.632
#&gt; SRR975568     1  0.0955     0.7652 0.968 0.000 0.000 0.004 0.028
#&gt; SRR975569     2  0.0000     0.9145 0.000 1.000 0.000 0.000 0.000
#&gt; SRR975570     2  0.0000     0.9145 0.000 1.000 0.000 0.000 0.000
#&gt; SRR975571     2  0.1851     0.9018 0.000 0.912 0.000 0.000 0.088
#&gt; SRR975572     2  0.0162     0.9143 0.000 0.996 0.000 0.004 0.000
#&gt; SRR975573     2  0.1851     0.9018 0.000 0.912 0.000 0.000 0.088
#&gt; SRR975574     2  0.1851     0.9018 0.000 0.912 0.000 0.000 0.088
#&gt; SRR975575     2  0.0162     0.9143 0.000 0.996 0.000 0.004 0.000
#&gt; SRR975576     2  0.0162     0.9143 0.000 0.996 0.000 0.004 0.000
#&gt; SRR975577     2  0.1851     0.9018 0.000 0.912 0.000 0.000 0.088
#&gt; SRR975578     2  0.1851     0.9018 0.000 0.912 0.000 0.000 0.088
#&gt; SRR975579     4  0.2104     0.3985 0.000 0.060 0.000 0.916 0.024
#&gt; SRR975580     2  0.4528     0.7364 0.000 0.752 0.000 0.144 0.104
#&gt; SRR975581     2  0.0162     0.9143 0.000 0.996 0.000 0.004 0.000
#&gt; SRR975582     2  0.1851     0.9018 0.000 0.912 0.000 0.000 0.088
#&gt; SRR975583     2  0.0162     0.9143 0.000 0.996 0.000 0.004 0.000
#&gt; SRR975584     2  0.1851     0.9018 0.000 0.912 0.000 0.000 0.088
#&gt; SRR975585     2  0.0162     0.9143 0.000 0.996 0.000 0.004 0.000
#&gt; SRR975586     2  0.4861    -0.0591 0.000 0.548 0.000 0.428 0.024
#&gt; SRR975587     3  0.0510     0.7789 0.000 0.000 0.984 0.000 0.016
#&gt; SRR975588     2  0.0000     0.9145 0.000 1.000 0.000 0.000 0.000
#&gt; SRR975589     3  0.3086     0.6720 0.004 0.000 0.816 0.000 0.180
#&gt; SRR975590     3  0.5864     0.5285 0.300 0.000 0.572 0.000 0.128
#&gt; SRR975591     3  0.0000     0.7791 0.000 0.000 1.000 0.000 0.000
#&gt; SRR975592     3  0.1582     0.7703 0.028 0.000 0.944 0.000 0.028
#&gt; SRR975593     3  0.2891     0.6782 0.000 0.000 0.824 0.000 0.176
#&gt; SRR975594     3  0.1300     0.7692 0.000 0.000 0.956 0.028 0.016
#&gt; SRR975595     3  0.6567     0.3638 0.360 0.000 0.432 0.000 0.208
#&gt; SRR975597     3  0.6567     0.3638 0.360 0.000 0.432 0.000 0.208
#&gt; SRR975596     1  0.5100     0.1169 0.516 0.000 0.000 0.036 0.448
#&gt; SRR975598     3  0.6582     0.3284 0.376 0.000 0.416 0.000 0.208
#&gt; SRR975599     1  0.7572     0.3331 0.500 0.000 0.104 0.168 0.228
#&gt; SRR975600     3  0.0000     0.7791 0.000 0.000 1.000 0.000 0.000
#&gt; SRR975601     3  0.0510     0.7789 0.000 0.000 0.984 0.000 0.016
#&gt; SRR975602     1  0.3003     0.6518 0.812 0.000 0.000 0.000 0.188
#&gt; SRR975603     3  0.0000     0.7791 0.000 0.000 1.000 0.000 0.000
#&gt; SRR975604     3  0.0000     0.7791 0.000 0.000 1.000 0.000 0.000
</code></pre>

<script>
$('#tab-SD-skmeans-get-classes-4-a').parent().next().next().hide();
$('#tab-SD-skmeans-get-classes-4-a').click(function(){
  $('#tab-SD-skmeans-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-skmeans-get-classes-5'>
<p><a id='tab-SD-skmeans-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3    p4    p5    p6
#&gt; SRR975551     1  0.1141      0.715 0.948 0.000 0.000 0.000 0.052 0.000
#&gt; SRR975552     1  0.1010      0.726 0.960 0.000 0.000 0.000 0.036 0.004
#&gt; SRR975554     1  0.0865      0.729 0.964 0.000 0.000 0.000 0.036 0.000
#&gt; SRR975553     2  0.0000      0.724 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR975555     1  0.1812      0.702 0.912 0.000 0.000 0.000 0.080 0.008
#&gt; SRR975556     2  0.3864      0.385 0.000 0.520 0.000 0.000 0.000 0.480
#&gt; SRR975557     4  0.0551      0.827 0.000 0.000 0.004 0.984 0.008 0.004
#&gt; SRR975558     5  0.6812     -0.108 0.048 0.000 0.008 0.180 0.436 0.328
#&gt; SRR975559     1  0.7088      0.324 0.436 0.000 0.000 0.140 0.284 0.140
#&gt; SRR975560     6  0.5409     -0.247 0.000 0.008 0.000 0.176 0.204 0.612
#&gt; SRR975561     6  0.5542      0.526 0.000 0.232 0.000 0.188 0.004 0.576
#&gt; SRR975562     1  0.6206      0.451 0.552 0.000 0.000 0.056 0.252 0.140
#&gt; SRR975563     2  0.3330      0.751 0.000 0.716 0.000 0.000 0.000 0.284
#&gt; SRR975564     1  0.2019      0.715 0.900 0.000 0.000 0.000 0.088 0.012
#&gt; SRR975565     1  0.0632      0.727 0.976 0.000 0.000 0.000 0.024 0.000
#&gt; SRR975566     1  0.4372      0.628 0.744 0.000 0.000 0.040 0.176 0.040
#&gt; SRR975567     5  0.6716     -0.105 0.048 0.000 0.004 0.180 0.440 0.328
#&gt; SRR975568     1  0.1434      0.719 0.940 0.000 0.000 0.000 0.048 0.012
#&gt; SRR975569     2  0.3266      0.761 0.000 0.728 0.000 0.000 0.000 0.272
#&gt; SRR975570     2  0.3266      0.761 0.000 0.728 0.000 0.000 0.000 0.272
#&gt; SRR975571     2  0.0000      0.724 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR975572     2  0.3266      0.761 0.000 0.728 0.000 0.000 0.000 0.272
#&gt; SRR975573     2  0.0000      0.724 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR975574     2  0.0000      0.724 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR975575     2  0.3266      0.761 0.000 0.728 0.000 0.000 0.000 0.272
#&gt; SRR975576     2  0.3309      0.755 0.000 0.720 0.000 0.000 0.000 0.280
#&gt; SRR975577     2  0.0000      0.724 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR975578     2  0.0000      0.724 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR975579     4  0.2146      0.815 0.000 0.004 0.000 0.880 0.000 0.116
#&gt; SRR975580     2  0.3872     -0.088 0.000 0.604 0.000 0.004 0.000 0.392
#&gt; SRR975581     2  0.3288      0.758 0.000 0.724 0.000 0.000 0.000 0.276
#&gt; SRR975582     2  0.0000      0.724 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR975583     2  0.3266      0.761 0.000 0.728 0.000 0.000 0.000 0.272
#&gt; SRR975584     2  0.0000      0.724 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR975585     2  0.3266      0.761 0.000 0.728 0.000 0.000 0.000 0.272
#&gt; SRR975586     6  0.4989      0.487 0.000 0.248 0.000 0.108 0.004 0.640
#&gt; SRR975587     3  0.1806      0.842 0.000 0.000 0.908 0.000 0.088 0.004
#&gt; SRR975588     2  0.3266      0.761 0.000 0.728 0.000 0.000 0.000 0.272
#&gt; SRR975589     3  0.3182      0.774 0.012 0.000 0.852 0.016 0.096 0.024
#&gt; SRR975590     3  0.5625      0.114 0.192 0.000 0.532 0.000 0.276 0.000
#&gt; SRR975591     3  0.0000      0.862 0.000 0.000 1.000 0.000 0.000 0.000
#&gt; SRR975592     3  0.1812      0.838 0.008 0.000 0.912 0.000 0.080 0.000
#&gt; SRR975593     3  0.3131      0.773 0.008 0.000 0.852 0.016 0.100 0.024
#&gt; SRR975594     3  0.2493      0.826 0.000 0.000 0.884 0.036 0.076 0.004
#&gt; SRR975595     5  0.6034      0.290 0.260 0.000 0.328 0.000 0.412 0.000
#&gt; SRR975597     5  0.6044      0.290 0.264 0.000 0.328 0.000 0.408 0.000
#&gt; SRR975596     1  0.7198      0.319 0.432 0.000 0.004 0.136 0.288 0.140
#&gt; SRR975598     5  0.6039      0.296 0.264 0.000 0.324 0.000 0.412 0.000
#&gt; SRR975599     5  0.6740     -0.064 0.288 0.000 0.036 0.244 0.428 0.004
#&gt; SRR975600     3  0.0000      0.862 0.000 0.000 1.000 0.000 0.000 0.000
#&gt; SRR975601     3  0.2001      0.838 0.000 0.000 0.900 0.004 0.092 0.004
#&gt; SRR975602     1  0.3508      0.493 0.704 0.000 0.000 0.004 0.292 0.000
#&gt; SRR975603     3  0.0000      0.862 0.000 0.000 1.000 0.000 0.000 0.000
#&gt; SRR975604     3  0.0000      0.862 0.000 0.000 1.000 0.000 0.000 0.000
</code></pre>

<script>
$('#tab-SD-skmeans-get-classes-5-a').parent().next().next().hide();
$('#tab-SD-skmeans-get-classes-5-a').click(function(){
  $('#tab-SD-skmeans-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-SD-skmeans-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-SD-skmeans-consensus-heatmap'>
<ul>
<li><a href='#tab-SD-skmeans-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-SD-skmeans-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-SD-skmeans-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-SD-skmeans-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-SD-skmeans-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-SD-skmeans-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-consensus-heatmap-1-1.png" alt="plot of chunk tab-SD-skmeans-consensus-heatmap-1"/></p>

</div>
<div id='tab-SD-skmeans-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-consensus-heatmap-2-1.png" alt="plot of chunk tab-SD-skmeans-consensus-heatmap-2"/></p>

</div>
<div id='tab-SD-skmeans-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-consensus-heatmap-3-1.png" alt="plot of chunk tab-SD-skmeans-consensus-heatmap-3"/></p>

</div>
<div id='tab-SD-skmeans-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-consensus-heatmap-4-1.png" alt="plot of chunk tab-SD-skmeans-consensus-heatmap-4"/></p>

</div>
<div id='tab-SD-skmeans-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-consensus-heatmap-5-1.png" alt="plot of chunk tab-SD-skmeans-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-SD-skmeans-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-SD-skmeans-membership-heatmap'>
<ul>
<li><a href='#tab-SD-skmeans-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-SD-skmeans-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-SD-skmeans-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-SD-skmeans-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-SD-skmeans-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-SD-skmeans-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-membership-heatmap-1-1.png" alt="plot of chunk tab-SD-skmeans-membership-heatmap-1"/></p>

</div>
<div id='tab-SD-skmeans-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-membership-heatmap-2-1.png" alt="plot of chunk tab-SD-skmeans-membership-heatmap-2"/></p>

</div>
<div id='tab-SD-skmeans-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-membership-heatmap-3-1.png" alt="plot of chunk tab-SD-skmeans-membership-heatmap-3"/></p>

</div>
<div id='tab-SD-skmeans-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-membership-heatmap-4-1.png" alt="plot of chunk tab-SD-skmeans-membership-heatmap-4"/></p>

</div>
<div id='tab-SD-skmeans-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-membership-heatmap-5-1.png" alt="plot of chunk tab-SD-skmeans-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-SD-skmeans-get-signatures' ).tabs();
} );
</script>
<div id='tabs-SD-skmeans-get-signatures'>
<ul>
<li><a href='#tab-SD-skmeans-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-SD-skmeans-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-SD-skmeans-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-SD-skmeans-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-SD-skmeans-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-SD-skmeans-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-get-signatures-1-1.png" alt="plot of chunk tab-SD-skmeans-get-signatures-1"/></p>

</div>
<div id='tab-SD-skmeans-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-get-signatures-2-1.png" alt="plot of chunk tab-SD-skmeans-get-signatures-2"/></p>

</div>
<div id='tab-SD-skmeans-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-get-signatures-3-1.png" alt="plot of chunk tab-SD-skmeans-get-signatures-3"/></p>

</div>
<div id='tab-SD-skmeans-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-get-signatures-4-1.png" alt="plot of chunk tab-SD-skmeans-get-signatures-4"/></p>

</div>
<div id='tab-SD-skmeans-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-get-signatures-5-1.png" alt="plot of chunk tab-SD-skmeans-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-SD-skmeans-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-SD-skmeans-get-signatures-no-scale'>
<ul>
<li><a href='#tab-SD-skmeans-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-SD-skmeans-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-SD-skmeans-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-SD-skmeans-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-SD-skmeans-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-SD-skmeans-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-SD-skmeans-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-SD-skmeans-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-SD-skmeans-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-SD-skmeans-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-SD-skmeans-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-SD-skmeans-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-SD-skmeans-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-SD-skmeans-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-SD-skmeans-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk SD-skmeans-signature_compare](figure_cola/SD-skmeans-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-SD-skmeans-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-SD-skmeans-dimension-reduction'>
<ul>
<li><a href='#tab-SD-skmeans-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-SD-skmeans-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-SD-skmeans-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-SD-skmeans-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-SD-skmeans-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-SD-skmeans-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-dimension-reduction-1-1.png" alt="plot of chunk tab-SD-skmeans-dimension-reduction-1"/></p>

</div>
<div id='tab-SD-skmeans-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-dimension-reduction-2-1.png" alt="plot of chunk tab-SD-skmeans-dimension-reduction-2"/></p>

</div>
<div id='tab-SD-skmeans-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-dimension-reduction-3-1.png" alt="plot of chunk tab-SD-skmeans-dimension-reduction-3"/></p>

</div>
<div id='tab-SD-skmeans-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-dimension-reduction-4-1.png" alt="plot of chunk tab-SD-skmeans-dimension-reduction-4"/></p>

</div>
<div id='tab-SD-skmeans-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-dimension-reduction-5-1.png" alt="plot of chunk tab-SD-skmeans-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk SD-skmeans-collect-classes](figure_cola/SD-skmeans-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### SD:pam**






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["SD", "pam"]
# you can also extract it by
# res = res_list["SD:pam"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 17171 rows and 54 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'SD' method.
#>   Subgroups are detected by 'pam' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 4.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk SD-pam-collect-plots](figure_cola/SD-pam-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk SD-pam-select-partition-number](figure_cola/SD-pam-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 0.961           0.948       0.978         0.5062 0.497   0.497
#> 3 3 0.940           0.891       0.959         0.2866 0.820   0.650
#> 4 4 0.961           0.936       0.971         0.1017 0.855   0.625
#> 5 5 0.892           0.785       0.894         0.0453 0.970   0.894
#> 6 6 0.845           0.789       0.893         0.0400 0.964   0.866
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 4
#> attr(,"optional")
#> [1] 2 3
```

There is also optional best $k$ = 2 3 that is worth to check.

Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-SD-pam-get-classes' ).tabs();
} );
</script>
<div id='tabs-SD-pam-get-classes'>
<ul>
<li><a href='#tab-SD-pam-get-classes-1'>k = 2</a></li>
<li><a href='#tab-SD-pam-get-classes-2'>k = 3</a></li>
<li><a href='#tab-SD-pam-get-classes-3'>k = 4</a></li>
<li><a href='#tab-SD-pam-get-classes-4'>k = 5</a></li>
<li><a href='#tab-SD-pam-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-SD-pam-get-classes-1'>
<p><a id='tab-SD-pam-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2
#&gt; SRR975551     1   0.000      0.958 1.000 0.000
#&gt; SRR975552     1   0.680      0.778 0.820 0.180
#&gt; SRR975554     1   0.000      0.958 1.000 0.000
#&gt; SRR975553     2   0.000      1.000 0.000 1.000
#&gt; SRR975555     1   0.000      0.958 1.000 0.000
#&gt; SRR975556     2   0.000      1.000 0.000 1.000
#&gt; SRR975557     1   0.706      0.762 0.808 0.192
#&gt; SRR975558     1   0.971      0.389 0.600 0.400
#&gt; SRR975559     1   0.000      0.958 1.000 0.000
#&gt; SRR975560     2   0.000      1.000 0.000 1.000
#&gt; SRR975561     2   0.000      1.000 0.000 1.000
#&gt; SRR975562     1   0.000      0.958 1.000 0.000
#&gt; SRR975563     2   0.000      1.000 0.000 1.000
#&gt; SRR975564     1   0.000      0.958 1.000 0.000
#&gt; SRR975565     1   0.000      0.958 1.000 0.000
#&gt; SRR975566     1   0.000      0.958 1.000 0.000
#&gt; SRR975567     1   0.971      0.389 0.600 0.400
#&gt; SRR975568     1   0.000      0.958 1.000 0.000
#&gt; SRR975569     2   0.000      1.000 0.000 1.000
#&gt; SRR975570     2   0.000      1.000 0.000 1.000
#&gt; SRR975571     2   0.000      1.000 0.000 1.000
#&gt; SRR975572     2   0.000      1.000 0.000 1.000
#&gt; SRR975573     2   0.000      1.000 0.000 1.000
#&gt; SRR975574     2   0.000      1.000 0.000 1.000
#&gt; SRR975575     2   0.000      1.000 0.000 1.000
#&gt; SRR975576     2   0.000      1.000 0.000 1.000
#&gt; SRR975577     2   0.000      1.000 0.000 1.000
#&gt; SRR975578     2   0.000      1.000 0.000 1.000
#&gt; SRR975579     2   0.000      1.000 0.000 1.000
#&gt; SRR975580     2   0.000      1.000 0.000 1.000
#&gt; SRR975581     2   0.000      1.000 0.000 1.000
#&gt; SRR975582     2   0.000      1.000 0.000 1.000
#&gt; SRR975583     2   0.000      1.000 0.000 1.000
#&gt; SRR975584     2   0.000      1.000 0.000 1.000
#&gt; SRR975585     2   0.000      1.000 0.000 1.000
#&gt; SRR975586     2   0.000      1.000 0.000 1.000
#&gt; SRR975587     1   0.000      0.958 1.000 0.000
#&gt; SRR975588     2   0.000      1.000 0.000 1.000
#&gt; SRR975589     1   0.000      0.958 1.000 0.000
#&gt; SRR975590     1   0.000      0.958 1.000 0.000
#&gt; SRR975591     1   0.000      0.958 1.000 0.000
#&gt; SRR975592     1   0.000      0.958 1.000 0.000
#&gt; SRR975593     1   0.000      0.958 1.000 0.000
#&gt; SRR975594     1   0.000      0.958 1.000 0.000
#&gt; SRR975595     1   0.000      0.958 1.000 0.000
#&gt; SRR975597     1   0.000      0.958 1.000 0.000
#&gt; SRR975596     1   0.000      0.958 1.000 0.000
#&gt; SRR975598     1   0.000      0.958 1.000 0.000
#&gt; SRR975599     1   0.163      0.939 0.976 0.024
#&gt; SRR975600     1   0.000      0.958 1.000 0.000
#&gt; SRR975601     1   0.000      0.958 1.000 0.000
#&gt; SRR975602     1   0.000      0.958 1.000 0.000
#&gt; SRR975603     1   0.000      0.958 1.000 0.000
#&gt; SRR975604     1   0.000      0.958 1.000 0.000
</code></pre>

<script>
$('#tab-SD-pam-get-classes-1-a').parent().next().next().hide();
$('#tab-SD-pam-get-classes-1-a').click(function(){
  $('#tab-SD-pam-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-pam-get-classes-2'>
<p><a id='tab-SD-pam-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3
#&gt; SRR975551     1  0.0000      0.929 1.000 0.000 0.000
#&gt; SRR975552     1  0.0000      0.929 1.000 0.000 0.000
#&gt; SRR975554     1  0.0000      0.929 1.000 0.000 0.000
#&gt; SRR975553     2  0.0000      0.981 0.000 1.000 0.000
#&gt; SRR975555     1  0.0000      0.929 1.000 0.000 0.000
#&gt; SRR975556     2  0.0000      0.981 0.000 1.000 0.000
#&gt; SRR975557     3  0.6126      0.292 0.400 0.000 0.600
#&gt; SRR975558     2  0.6225      0.233 0.432 0.568 0.000
#&gt; SRR975559     1  0.0000      0.929 1.000 0.000 0.000
#&gt; SRR975560     2  0.0000      0.981 0.000 1.000 0.000
#&gt; SRR975561     2  0.0000      0.981 0.000 1.000 0.000
#&gt; SRR975562     1  0.0000      0.929 1.000 0.000 0.000
#&gt; SRR975563     2  0.0000      0.981 0.000 1.000 0.000
#&gt; SRR975564     1  0.0000      0.929 1.000 0.000 0.000
#&gt; SRR975565     1  0.0000      0.929 1.000 0.000 0.000
#&gt; SRR975566     1  0.0000      0.929 1.000 0.000 0.000
#&gt; SRR975567     1  0.1529      0.891 0.960 0.040 0.000
#&gt; SRR975568     1  0.0000      0.929 1.000 0.000 0.000
#&gt; SRR975569     2  0.0000      0.981 0.000 1.000 0.000
#&gt; SRR975570     2  0.0000      0.981 0.000 1.000 0.000
#&gt; SRR975571     2  0.0000      0.981 0.000 1.000 0.000
#&gt; SRR975572     2  0.0000      0.981 0.000 1.000 0.000
#&gt; SRR975573     2  0.0000      0.981 0.000 1.000 0.000
#&gt; SRR975574     2  0.0000      0.981 0.000 1.000 0.000
#&gt; SRR975575     2  0.0000      0.981 0.000 1.000 0.000
#&gt; SRR975576     2  0.0000      0.981 0.000 1.000 0.000
#&gt; SRR975577     2  0.0000      0.981 0.000 1.000 0.000
#&gt; SRR975578     2  0.0000      0.981 0.000 1.000 0.000
#&gt; SRR975579     2  0.0000      0.981 0.000 1.000 0.000
#&gt; SRR975580     2  0.0000      0.981 0.000 1.000 0.000
#&gt; SRR975581     2  0.0000      0.981 0.000 1.000 0.000
#&gt; SRR975582     2  0.0000      0.981 0.000 1.000 0.000
#&gt; SRR975583     2  0.0000      0.981 0.000 1.000 0.000
#&gt; SRR975584     2  0.0000      0.981 0.000 1.000 0.000
#&gt; SRR975585     2  0.0000      0.981 0.000 1.000 0.000
#&gt; SRR975586     2  0.0000      0.981 0.000 1.000 0.000
#&gt; SRR975587     3  0.0000      0.918 0.000 0.000 1.000
#&gt; SRR975588     2  0.0000      0.981 0.000 1.000 0.000
#&gt; SRR975589     3  0.0000      0.918 0.000 0.000 1.000
#&gt; SRR975590     3  0.6111      0.283 0.396 0.000 0.604
#&gt; SRR975591     3  0.0000      0.918 0.000 0.000 1.000
#&gt; SRR975592     3  0.0424      0.912 0.008 0.000 0.992
#&gt; SRR975593     3  0.0000      0.918 0.000 0.000 1.000
#&gt; SRR975594     3  0.0000      0.918 0.000 0.000 1.000
#&gt; SRR975595     1  0.5327      0.602 0.728 0.000 0.272
#&gt; SRR975597     1  0.6026      0.373 0.624 0.000 0.376
#&gt; SRR975596     1  0.0592      0.922 0.988 0.000 0.012
#&gt; SRR975598     1  0.2625      0.862 0.916 0.000 0.084
#&gt; SRR975599     1  0.5470      0.718 0.796 0.036 0.168
#&gt; SRR975600     3  0.0000      0.918 0.000 0.000 1.000
#&gt; SRR975601     3  0.0000      0.918 0.000 0.000 1.000
#&gt; SRR975602     1  0.0000      0.929 1.000 0.000 0.000
#&gt; SRR975603     3  0.0000      0.918 0.000 0.000 1.000
#&gt; SRR975604     3  0.0000      0.918 0.000 0.000 1.000
</code></pre>

<script>
$('#tab-SD-pam-get-classes-2-a').parent().next().next().hide();
$('#tab-SD-pam-get-classes-2-a').click(function(){
  $('#tab-SD-pam-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-pam-get-classes-3'>
<p><a id='tab-SD-pam-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3    p4
#&gt; SRR975551     4  0.3569      0.798 0.196 0.000 0.000 0.804
#&gt; SRR975552     1  0.0000      0.931 1.000 0.000 0.000 0.000
#&gt; SRR975554     1  0.0336      0.926 0.992 0.000 0.000 0.008
#&gt; SRR975553     2  0.0000      1.000 0.000 1.000 0.000 0.000
#&gt; SRR975555     4  0.4898      0.420 0.416 0.000 0.000 0.584
#&gt; SRR975556     2  0.0000      1.000 0.000 1.000 0.000 0.000
#&gt; SRR975557     1  0.0000      0.931 1.000 0.000 0.000 0.000
#&gt; SRR975558     1  0.0524      0.924 0.988 0.008 0.000 0.004
#&gt; SRR975559     1  0.0000      0.931 1.000 0.000 0.000 0.000
#&gt; SRR975560     1  0.3610      0.690 0.800 0.200 0.000 0.000
#&gt; SRR975561     2  0.0000      1.000 0.000 1.000 0.000 0.000
#&gt; SRR975562     1  0.0000      0.931 1.000 0.000 0.000 0.000
#&gt; SRR975563     2  0.0000      1.000 0.000 1.000 0.000 0.000
#&gt; SRR975564     1  0.3444      0.700 0.816 0.000 0.000 0.184
#&gt; SRR975565     1  0.0188      0.930 0.996 0.000 0.000 0.004
#&gt; SRR975566     1  0.0000      0.931 1.000 0.000 0.000 0.000
#&gt; SRR975567     1  0.0000      0.931 1.000 0.000 0.000 0.000
#&gt; SRR975568     1  0.0188      0.930 0.996 0.000 0.000 0.004
#&gt; SRR975569     2  0.0000      1.000 0.000 1.000 0.000 0.000
#&gt; SRR975570     2  0.0000      1.000 0.000 1.000 0.000 0.000
#&gt; SRR975571     2  0.0000      1.000 0.000 1.000 0.000 0.000
#&gt; SRR975572     2  0.0000      1.000 0.000 1.000 0.000 0.000
#&gt; SRR975573     2  0.0000      1.000 0.000 1.000 0.000 0.000
#&gt; SRR975574     2  0.0000      1.000 0.000 1.000 0.000 0.000
#&gt; SRR975575     2  0.0000      1.000 0.000 1.000 0.000 0.000
#&gt; SRR975576     2  0.0000      1.000 0.000 1.000 0.000 0.000
#&gt; SRR975577     2  0.0000      1.000 0.000 1.000 0.000 0.000
#&gt; SRR975578     2  0.0000      1.000 0.000 1.000 0.000 0.000
#&gt; SRR975579     1  0.3610      0.690 0.800 0.200 0.000 0.000
#&gt; SRR975580     2  0.0000      1.000 0.000 1.000 0.000 0.000
#&gt; SRR975581     2  0.0000      1.000 0.000 1.000 0.000 0.000
#&gt; SRR975582     2  0.0000      1.000 0.000 1.000 0.000 0.000
#&gt; SRR975583     2  0.0000      1.000 0.000 1.000 0.000 0.000
#&gt; SRR975584     2  0.0000      1.000 0.000 1.000 0.000 0.000
#&gt; SRR975585     2  0.0000      1.000 0.000 1.000 0.000 0.000
#&gt; SRR975586     2  0.0000      1.000 0.000 1.000 0.000 0.000
#&gt; SRR975587     3  0.0000      0.996 0.000 0.000 1.000 0.000
#&gt; SRR975588     2  0.0000      1.000 0.000 1.000 0.000 0.000
#&gt; SRR975589     3  0.0000      0.996 0.000 0.000 1.000 0.000
#&gt; SRR975590     4  0.0188      0.863 0.000 0.000 0.004 0.996
#&gt; SRR975591     3  0.0000      0.996 0.000 0.000 1.000 0.000
#&gt; SRR975592     3  0.1022      0.964 0.000 0.000 0.968 0.032
#&gt; SRR975593     3  0.0000      0.996 0.000 0.000 1.000 0.000
#&gt; SRR975594     3  0.0000      0.996 0.000 0.000 1.000 0.000
#&gt; SRR975595     4  0.0188      0.863 0.000 0.000 0.004 0.996
#&gt; SRR975597     4  0.0188      0.863 0.000 0.000 0.004 0.996
#&gt; SRR975596     1  0.0000      0.931 1.000 0.000 0.000 0.000
#&gt; SRR975598     4  0.0188      0.863 0.000 0.000 0.004 0.996
#&gt; SRR975599     4  0.1940      0.856 0.076 0.000 0.000 0.924
#&gt; SRR975600     3  0.0000      0.996 0.000 0.000 1.000 0.000
#&gt; SRR975601     3  0.0000      0.996 0.000 0.000 1.000 0.000
#&gt; SRR975602     4  0.3610      0.797 0.200 0.000 0.000 0.800
#&gt; SRR975603     3  0.0000      0.996 0.000 0.000 1.000 0.000
#&gt; SRR975604     3  0.0000      0.996 0.000 0.000 1.000 0.000
</code></pre>

<script>
$('#tab-SD-pam-get-classes-3-a').parent().next().next().hide();
$('#tab-SD-pam-get-classes-3-a').click(function(){
  $('#tab-SD-pam-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-pam-get-classes-4'>
<p><a id='tab-SD-pam-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3    p4    p5
#&gt; SRR975551     5  0.3707      0.669 0.284 0.000 0.000 0.000 0.716
#&gt; SRR975552     1  0.4359      0.533 0.584 0.000 0.000 0.412 0.004
#&gt; SRR975554     1  0.1831      0.548 0.920 0.000 0.000 0.076 0.004
#&gt; SRR975553     2  0.1671      0.945 0.000 0.924 0.000 0.076 0.000
#&gt; SRR975555     1  0.4287     -0.440 0.540 0.000 0.000 0.000 0.460
#&gt; SRR975556     2  0.0000      0.959 0.000 1.000 0.000 0.000 0.000
#&gt; SRR975557     4  0.2179      0.428 0.112 0.000 0.000 0.888 0.000
#&gt; SRR975558     1  0.4283      0.492 0.644 0.008 0.000 0.348 0.000
#&gt; SRR975559     1  0.4015      0.592 0.652 0.000 0.000 0.348 0.000
#&gt; SRR975560     1  0.5995      0.142 0.468 0.112 0.000 0.420 0.000
#&gt; SRR975561     2  0.1043      0.936 0.000 0.960 0.000 0.040 0.000
#&gt; SRR975562     1  0.4015      0.592 0.652 0.000 0.000 0.348 0.000
#&gt; SRR975563     2  0.0000      0.959 0.000 1.000 0.000 0.000 0.000
#&gt; SRR975564     1  0.3318      0.339 0.800 0.000 0.000 0.008 0.192
#&gt; SRR975565     1  0.0162      0.528 0.996 0.000 0.000 0.000 0.004
#&gt; SRR975566     1  0.3752      0.596 0.708 0.000 0.000 0.292 0.000
#&gt; SRR975567     1  0.4283      0.486 0.544 0.000 0.000 0.456 0.000
#&gt; SRR975568     1  0.0162      0.528 0.996 0.000 0.000 0.000 0.004
#&gt; SRR975569     2  0.0000      0.959 0.000 1.000 0.000 0.000 0.000
#&gt; SRR975570     2  0.0000      0.959 0.000 1.000 0.000 0.000 0.000
#&gt; SRR975571     2  0.1671      0.945 0.000 0.924 0.000 0.076 0.000
#&gt; SRR975572     2  0.0000      0.959 0.000 1.000 0.000 0.000 0.000
#&gt; SRR975573     2  0.1671      0.945 0.000 0.924 0.000 0.076 0.000
#&gt; SRR975574     2  0.1671      0.945 0.000 0.924 0.000 0.076 0.000
#&gt; SRR975575     2  0.0000      0.959 0.000 1.000 0.000 0.000 0.000
#&gt; SRR975576     2  0.0000      0.959 0.000 1.000 0.000 0.000 0.000
#&gt; SRR975577     2  0.1671      0.945 0.000 0.924 0.000 0.076 0.000
#&gt; SRR975578     2  0.1671      0.945 0.000 0.924 0.000 0.076 0.000
#&gt; SRR975579     4  0.2377      0.555 0.000 0.128 0.000 0.872 0.000
#&gt; SRR975580     2  0.2179      0.921 0.000 0.888 0.000 0.112 0.000
#&gt; SRR975581     2  0.0000      0.959 0.000 1.000 0.000 0.000 0.000
#&gt; SRR975582     2  0.1671      0.945 0.000 0.924 0.000 0.076 0.000
#&gt; SRR975583     2  0.0000      0.959 0.000 1.000 0.000 0.000 0.000
#&gt; SRR975584     2  0.1671      0.945 0.000 0.924 0.000 0.076 0.000
#&gt; SRR975585     2  0.0000      0.959 0.000 1.000 0.000 0.000 0.000
#&gt; SRR975586     2  0.0963      0.939 0.000 0.964 0.000 0.036 0.000
#&gt; SRR975587     3  0.0000      0.996 0.000 0.000 1.000 0.000 0.000
#&gt; SRR975588     2  0.0000      0.959 0.000 1.000 0.000 0.000 0.000
#&gt; SRR975589     3  0.0000      0.996 0.000 0.000 1.000 0.000 0.000
#&gt; SRR975590     5  0.0000      0.813 0.000 0.000 0.000 0.000 1.000
#&gt; SRR975591     3  0.0000      0.996 0.000 0.000 1.000 0.000 0.000
#&gt; SRR975592     3  0.0880      0.962 0.000 0.000 0.968 0.000 0.032
#&gt; SRR975593     3  0.0000      0.996 0.000 0.000 1.000 0.000 0.000
#&gt; SRR975594     3  0.0000      0.996 0.000 0.000 1.000 0.000 0.000
#&gt; SRR975595     5  0.0000      0.813 0.000 0.000 0.000 0.000 1.000
#&gt; SRR975597     5  0.0000      0.813 0.000 0.000 0.000 0.000 1.000
#&gt; SRR975596     1  0.4015      0.592 0.652 0.000 0.000 0.348 0.000
#&gt; SRR975598     5  0.0000      0.813 0.000 0.000 0.000 0.000 1.000
#&gt; SRR975599     5  0.6031      0.452 0.352 0.000 0.000 0.128 0.520
#&gt; SRR975600     3  0.0000      0.996 0.000 0.000 1.000 0.000 0.000
#&gt; SRR975601     3  0.0000      0.996 0.000 0.000 1.000 0.000 0.000
#&gt; SRR975602     5  0.3852      0.691 0.220 0.000 0.000 0.020 0.760
#&gt; SRR975603     3  0.0000      0.996 0.000 0.000 1.000 0.000 0.000
#&gt; SRR975604     3  0.0000      0.996 0.000 0.000 1.000 0.000 0.000
</code></pre>

<script>
$('#tab-SD-pam-get-classes-4-a').parent().next().next().hide();
$('#tab-SD-pam-get-classes-4-a').click(function(){
  $('#tab-SD-pam-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-pam-get-classes-5'>
<p><a id='tab-SD-pam-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3    p4    p5    p6
#&gt; SRR975551     1  0.3330    0.64464 0.716 0.000 0.000 0.000 0.284 0.000
#&gt; SRR975552     6  0.3152    0.45098 0.196 0.000 0.000 0.004 0.008 0.792
#&gt; SRR975554     5  0.3797    0.19283 0.000 0.000 0.000 0.000 0.580 0.420
#&gt; SRR975553     2  0.3288    0.78836 0.000 0.724 0.000 0.276 0.000 0.000
#&gt; SRR975555     5  0.0632    0.83083 0.024 0.000 0.000 0.000 0.976 0.000
#&gt; SRR975556     2  0.0000    0.86621 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR975557     4  0.3555    0.55434 0.000 0.000 0.000 0.712 0.008 0.280
#&gt; SRR975558     6  0.3398    0.43403 0.000 0.000 0.000 0.008 0.252 0.740
#&gt; SRR975559     6  0.2738    0.68486 0.000 0.000 0.000 0.004 0.176 0.820
#&gt; SRR975560     6  0.5244    0.00469 0.000 0.336 0.000 0.112 0.000 0.552
#&gt; SRR975561     2  0.0508    0.86089 0.000 0.984 0.000 0.012 0.000 0.004
#&gt; SRR975562     6  0.2738    0.68486 0.000 0.000 0.000 0.004 0.176 0.820
#&gt; SRR975563     2  0.0000    0.86621 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR975564     5  0.0806    0.83365 0.020 0.000 0.000 0.000 0.972 0.008
#&gt; SRR975565     5  0.0632    0.83471 0.000 0.000 0.000 0.000 0.976 0.024
#&gt; SRR975566     6  0.2948    0.67124 0.000 0.000 0.000 0.008 0.188 0.804
#&gt; SRR975567     6  0.0260    0.59209 0.000 0.000 0.000 0.008 0.000 0.992
#&gt; SRR975568     5  0.0632    0.83471 0.000 0.000 0.000 0.000 0.976 0.024
#&gt; SRR975569     2  0.0000    0.86621 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR975570     2  0.0000    0.86621 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR975571     2  0.3288    0.78836 0.000 0.724 0.000 0.276 0.000 0.000
#&gt; SRR975572     2  0.0000    0.86621 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR975573     2  0.3221    0.79286 0.000 0.736 0.000 0.264 0.000 0.000
#&gt; SRR975574     2  0.3266    0.79007 0.000 0.728 0.000 0.272 0.000 0.000
#&gt; SRR975575     2  0.0000    0.86621 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR975576     2  0.0000    0.86621 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR975577     2  0.3288    0.78836 0.000 0.724 0.000 0.276 0.000 0.000
#&gt; SRR975578     2  0.3288    0.78836 0.000 0.724 0.000 0.276 0.000 0.000
#&gt; SRR975579     4  0.1251    0.62252 0.000 0.012 0.000 0.956 0.008 0.024
#&gt; SRR975580     2  0.3448    0.78269 0.000 0.716 0.000 0.280 0.000 0.004
#&gt; SRR975581     2  0.0000    0.86621 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR975582     2  0.3266    0.79007 0.000 0.728 0.000 0.272 0.000 0.000
#&gt; SRR975583     2  0.0000    0.86621 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR975584     2  0.3288    0.78836 0.000 0.724 0.000 0.276 0.000 0.000
#&gt; SRR975585     2  0.0000    0.86621 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR975586     2  0.0291    0.86158 0.000 0.992 0.000 0.004 0.000 0.004
#&gt; SRR975587     3  0.0000    0.99526 0.000 0.000 1.000 0.000 0.000 0.000
#&gt; SRR975588     2  0.0000    0.86621 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR975589     3  0.0000    0.99526 0.000 0.000 1.000 0.000 0.000 0.000
#&gt; SRR975590     1  0.0000    0.86334 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR975591     3  0.0000    0.99526 0.000 0.000 1.000 0.000 0.000 0.000
#&gt; SRR975592     3  0.0865    0.95631 0.036 0.000 0.964 0.000 0.000 0.000
#&gt; SRR975593     3  0.0000    0.99526 0.000 0.000 1.000 0.000 0.000 0.000
#&gt; SRR975594     3  0.0000    0.99526 0.000 0.000 1.000 0.000 0.000 0.000
#&gt; SRR975595     1  0.0000    0.86334 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR975597     1  0.0000    0.86334 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR975596     6  0.2738    0.68486 0.000 0.000 0.000 0.004 0.176 0.820
#&gt; SRR975598     1  0.0000    0.86334 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR975599     5  0.2915    0.65384 0.184 0.000 0.000 0.008 0.808 0.000
#&gt; SRR975600     3  0.0000    0.99526 0.000 0.000 1.000 0.000 0.000 0.000
#&gt; SRR975601     3  0.0000    0.99526 0.000 0.000 1.000 0.000 0.000 0.000
#&gt; SRR975602     1  0.3652    0.70502 0.760 0.000 0.000 0.008 0.212 0.020
#&gt; SRR975603     3  0.0000    0.99526 0.000 0.000 1.000 0.000 0.000 0.000
#&gt; SRR975604     3  0.0000    0.99526 0.000 0.000 1.000 0.000 0.000 0.000
</code></pre>

<script>
$('#tab-SD-pam-get-classes-5-a').parent().next().next().hide();
$('#tab-SD-pam-get-classes-5-a').click(function(){
  $('#tab-SD-pam-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-SD-pam-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-SD-pam-consensus-heatmap'>
<ul>
<li><a href='#tab-SD-pam-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-SD-pam-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-SD-pam-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-SD-pam-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-SD-pam-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-SD-pam-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-consensus-heatmap-1-1.png" alt="plot of chunk tab-SD-pam-consensus-heatmap-1"/></p>

</div>
<div id='tab-SD-pam-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-consensus-heatmap-2-1.png" alt="plot of chunk tab-SD-pam-consensus-heatmap-2"/></p>

</div>
<div id='tab-SD-pam-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-consensus-heatmap-3-1.png" alt="plot of chunk tab-SD-pam-consensus-heatmap-3"/></p>

</div>
<div id='tab-SD-pam-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-consensus-heatmap-4-1.png" alt="plot of chunk tab-SD-pam-consensus-heatmap-4"/></p>

</div>
<div id='tab-SD-pam-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-consensus-heatmap-5-1.png" alt="plot of chunk tab-SD-pam-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-SD-pam-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-SD-pam-membership-heatmap'>
<ul>
<li><a href='#tab-SD-pam-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-SD-pam-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-SD-pam-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-SD-pam-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-SD-pam-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-SD-pam-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-membership-heatmap-1-1.png" alt="plot of chunk tab-SD-pam-membership-heatmap-1"/></p>

</div>
<div id='tab-SD-pam-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-membership-heatmap-2-1.png" alt="plot of chunk tab-SD-pam-membership-heatmap-2"/></p>

</div>
<div id='tab-SD-pam-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-membership-heatmap-3-1.png" alt="plot of chunk tab-SD-pam-membership-heatmap-3"/></p>

</div>
<div id='tab-SD-pam-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-membership-heatmap-4-1.png" alt="plot of chunk tab-SD-pam-membership-heatmap-4"/></p>

</div>
<div id='tab-SD-pam-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-membership-heatmap-5-1.png" alt="plot of chunk tab-SD-pam-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-SD-pam-get-signatures' ).tabs();
} );
</script>
<div id='tabs-SD-pam-get-signatures'>
<ul>
<li><a href='#tab-SD-pam-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-SD-pam-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-SD-pam-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-SD-pam-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-SD-pam-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-SD-pam-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-get-signatures-1-1.png" alt="plot of chunk tab-SD-pam-get-signatures-1"/></p>

</div>
<div id='tab-SD-pam-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-get-signatures-2-1.png" alt="plot of chunk tab-SD-pam-get-signatures-2"/></p>

</div>
<div id='tab-SD-pam-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-get-signatures-3-1.png" alt="plot of chunk tab-SD-pam-get-signatures-3"/></p>

</div>
<div id='tab-SD-pam-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-get-signatures-4-1.png" alt="plot of chunk tab-SD-pam-get-signatures-4"/></p>

</div>
<div id='tab-SD-pam-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-get-signatures-5-1.png" alt="plot of chunk tab-SD-pam-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-SD-pam-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-SD-pam-get-signatures-no-scale'>
<ul>
<li><a href='#tab-SD-pam-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-SD-pam-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-SD-pam-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-SD-pam-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-SD-pam-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-SD-pam-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-SD-pam-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-SD-pam-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-SD-pam-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-SD-pam-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-SD-pam-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-SD-pam-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-SD-pam-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-SD-pam-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-SD-pam-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk SD-pam-signature_compare](figure_cola/SD-pam-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-SD-pam-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-SD-pam-dimension-reduction'>
<ul>
<li><a href='#tab-SD-pam-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-SD-pam-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-SD-pam-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-SD-pam-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-SD-pam-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-SD-pam-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-dimension-reduction-1-1.png" alt="plot of chunk tab-SD-pam-dimension-reduction-1"/></p>

</div>
<div id='tab-SD-pam-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-dimension-reduction-2-1.png" alt="plot of chunk tab-SD-pam-dimension-reduction-2"/></p>

</div>
<div id='tab-SD-pam-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-dimension-reduction-3-1.png" alt="plot of chunk tab-SD-pam-dimension-reduction-3"/></p>

</div>
<div id='tab-SD-pam-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-dimension-reduction-4-1.png" alt="plot of chunk tab-SD-pam-dimension-reduction-4"/></p>

</div>
<div id='tab-SD-pam-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-dimension-reduction-5-1.png" alt="plot of chunk tab-SD-pam-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk SD-pam-collect-classes](figure_cola/SD-pam-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### SD:mclust






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["SD", "mclust"]
# you can also extract it by
# res = res_list["SD:mclust"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 17171 rows and 54 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'SD' method.
#>   Subgroups are detected by 'mclust' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 4.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk SD-mclust-collect-plots](figure_cola/SD-mclust-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk SD-mclust-select-partition-number](figure_cola/SD-mclust-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 0.547           0.933       0.938         0.4503 0.547   0.547
#> 3 3 0.700           0.727       0.840         0.4788 0.776   0.591
#> 4 4 0.800           0.899       0.920         0.1018 0.931   0.786
#> 5 5 0.733           0.773       0.847         0.0273 0.892   0.638
#> 6 6 0.787           0.742       0.825         0.0543 0.971   0.874
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 4
```


Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-SD-mclust-get-classes' ).tabs();
} );
</script>
<div id='tabs-SD-mclust-get-classes'>
<ul>
<li><a href='#tab-SD-mclust-get-classes-1'>k = 2</a></li>
<li><a href='#tab-SD-mclust-get-classes-2'>k = 3</a></li>
<li><a href='#tab-SD-mclust-get-classes-3'>k = 4</a></li>
<li><a href='#tab-SD-mclust-get-classes-4'>k = 5</a></li>
<li><a href='#tab-SD-mclust-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-SD-mclust-get-classes-1'>
<p><a id='tab-SD-mclust-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2
#&gt; SRR975551     1   0.634      0.908 0.840 0.160
#&gt; SRR975552     1   0.634      0.908 0.840 0.160
#&gt; SRR975554     1   0.634      0.908 0.840 0.160
#&gt; SRR975553     2   0.000      1.000 0.000 1.000
#&gt; SRR975555     1   0.634      0.908 0.840 0.160
#&gt; SRR975556     1   0.730      0.869 0.796 0.204
#&gt; SRR975557     1   0.634      0.908 0.840 0.160
#&gt; SRR975558     1   0.634      0.908 0.840 0.160
#&gt; SRR975559     1   0.634      0.908 0.840 0.160
#&gt; SRR975560     1   0.634      0.908 0.840 0.160
#&gt; SRR975561     1   0.730      0.869 0.796 0.204
#&gt; SRR975562     1   0.634      0.908 0.840 0.160
#&gt; SRR975563     2   0.000      1.000 0.000 1.000
#&gt; SRR975564     1   0.634      0.908 0.840 0.160
#&gt; SRR975565     1   0.634      0.908 0.840 0.160
#&gt; SRR975566     1   0.634      0.908 0.840 0.160
#&gt; SRR975567     1   0.634      0.908 0.840 0.160
#&gt; SRR975568     1   0.634      0.908 0.840 0.160
#&gt; SRR975569     2   0.000      1.000 0.000 1.000
#&gt; SRR975570     2   0.000      1.000 0.000 1.000
#&gt; SRR975571     2   0.000      1.000 0.000 1.000
#&gt; SRR975572     2   0.000      1.000 0.000 1.000
#&gt; SRR975573     2   0.000      1.000 0.000 1.000
#&gt; SRR975574     2   0.000      1.000 0.000 1.000
#&gt; SRR975575     2   0.000      1.000 0.000 1.000
#&gt; SRR975576     2   0.000      1.000 0.000 1.000
#&gt; SRR975577     2   0.000      1.000 0.000 1.000
#&gt; SRR975578     2   0.000      1.000 0.000 1.000
#&gt; SRR975579     1   0.634      0.908 0.840 0.160
#&gt; SRR975580     1   0.644      0.905 0.836 0.164
#&gt; SRR975581     2   0.000      1.000 0.000 1.000
#&gt; SRR975582     2   0.000      1.000 0.000 1.000
#&gt; SRR975583     2   0.000      1.000 0.000 1.000
#&gt; SRR975584     2   0.000      1.000 0.000 1.000
#&gt; SRR975585     2   0.000      1.000 0.000 1.000
#&gt; SRR975586     1   0.730      0.869 0.796 0.204
#&gt; SRR975587     1   0.000      0.895 1.000 0.000
#&gt; SRR975588     2   0.000      1.000 0.000 1.000
#&gt; SRR975589     1   0.000      0.895 1.000 0.000
#&gt; SRR975590     1   0.000      0.895 1.000 0.000
#&gt; SRR975591     1   0.000      0.895 1.000 0.000
#&gt; SRR975592     1   0.000      0.895 1.000 0.000
#&gt; SRR975593     1   0.000      0.895 1.000 0.000
#&gt; SRR975594     1   0.000      0.895 1.000 0.000
#&gt; SRR975595     1   0.000      0.895 1.000 0.000
#&gt; SRR975597     1   0.000      0.895 1.000 0.000
#&gt; SRR975596     1   0.634      0.908 0.840 0.160
#&gt; SRR975598     1   0.000      0.895 1.000 0.000
#&gt; SRR975599     1   0.000      0.895 1.000 0.000
#&gt; SRR975600     1   0.000      0.895 1.000 0.000
#&gt; SRR975601     1   0.000      0.895 1.000 0.000
#&gt; SRR975602     1   0.000      0.895 1.000 0.000
#&gt; SRR975603     1   0.000      0.895 1.000 0.000
#&gt; SRR975604     1   0.000      0.895 1.000 0.000
</code></pre>

<script>
$('#tab-SD-mclust-get-classes-1-a').parent().next().next().hide();
$('#tab-SD-mclust-get-classes-1-a').click(function(){
  $('#tab-SD-mclust-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-mclust-get-classes-2'>
<p><a id='tab-SD-mclust-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3
#&gt; SRR975551     1  0.6062      0.614 0.616 0.000 0.384
#&gt; SRR975552     1  0.6095      0.609 0.608 0.000 0.392
#&gt; SRR975554     1  0.5138      0.646 0.748 0.000 0.252
#&gt; SRR975553     2  0.0000      0.994 0.000 1.000 0.000
#&gt; SRR975555     1  0.6079      0.609 0.612 0.000 0.388
#&gt; SRR975556     1  0.1643      0.615 0.956 0.000 0.044
#&gt; SRR975557     1  0.6140     -0.365 0.596 0.000 0.404
#&gt; SRR975558     1  0.1643      0.615 0.956 0.000 0.044
#&gt; SRR975559     1  0.4750      0.647 0.784 0.000 0.216
#&gt; SRR975560     1  0.1643      0.615 0.956 0.000 0.044
#&gt; SRR975561     1  0.1950      0.613 0.952 0.008 0.040
#&gt; SRR975562     1  0.4702      0.649 0.788 0.000 0.212
#&gt; SRR975563     2  0.0000      0.994 0.000 1.000 0.000
#&gt; SRR975564     1  0.6079      0.606 0.612 0.000 0.388
#&gt; SRR975565     1  0.6095      0.609 0.608 0.000 0.392
#&gt; SRR975566     1  0.5968      0.438 0.636 0.000 0.364
#&gt; SRR975567     1  0.1643      0.615 0.956 0.000 0.044
#&gt; SRR975568     1  0.6154      0.602 0.592 0.000 0.408
#&gt; SRR975569     2  0.0000      0.994 0.000 1.000 0.000
#&gt; SRR975570     2  0.0000      0.994 0.000 1.000 0.000
#&gt; SRR975571     2  0.0000      0.994 0.000 1.000 0.000
#&gt; SRR975572     2  0.0000      0.994 0.000 1.000 0.000
#&gt; SRR975573     2  0.0000      0.994 0.000 1.000 0.000
#&gt; SRR975574     2  0.2796      0.890 0.092 0.908 0.000
#&gt; SRR975575     2  0.0000      0.994 0.000 1.000 0.000
#&gt; SRR975576     2  0.0000      0.994 0.000 1.000 0.000
#&gt; SRR975577     2  0.0000      0.994 0.000 1.000 0.000
#&gt; SRR975578     2  0.0000      0.994 0.000 1.000 0.000
#&gt; SRR975579     1  0.5835     -0.158 0.660 0.000 0.340
#&gt; SRR975580     1  0.1643      0.615 0.956 0.000 0.044
#&gt; SRR975581     2  0.0000      0.994 0.000 1.000 0.000
#&gt; SRR975582     2  0.0000      0.994 0.000 1.000 0.000
#&gt; SRR975583     2  0.0000      0.994 0.000 1.000 0.000
#&gt; SRR975584     2  0.0000      0.994 0.000 1.000 0.000
#&gt; SRR975585     2  0.0237      0.990 0.004 0.996 0.000
#&gt; SRR975586     1  0.4092      0.543 0.876 0.088 0.036
#&gt; SRR975587     3  0.6045      0.757 0.380 0.000 0.620
#&gt; SRR975588     2  0.0000      0.994 0.000 1.000 0.000
#&gt; SRR975589     3  0.4605      0.723 0.204 0.000 0.796
#&gt; SRR975590     3  0.4452      0.721 0.192 0.000 0.808
#&gt; SRR975591     3  0.6045      0.757 0.380 0.000 0.620
#&gt; SRR975592     3  0.4452      0.721 0.192 0.000 0.808
#&gt; SRR975593     3  0.4605      0.723 0.204 0.000 0.796
#&gt; SRR975594     3  0.6062      0.753 0.384 0.000 0.616
#&gt; SRR975595     3  0.1163      0.591 0.028 0.000 0.972
#&gt; SRR975597     3  0.1163      0.591 0.028 0.000 0.972
#&gt; SRR975596     1  0.4842      0.642 0.776 0.000 0.224
#&gt; SRR975598     3  0.1163      0.591 0.028 0.000 0.972
#&gt; SRR975599     3  0.6095      0.747 0.392 0.000 0.608
#&gt; SRR975600     3  0.6045      0.757 0.380 0.000 0.620
#&gt; SRR975601     3  0.6045      0.757 0.380 0.000 0.620
#&gt; SRR975602     3  0.4002      0.413 0.160 0.000 0.840
#&gt; SRR975603     3  0.6045      0.757 0.380 0.000 0.620
#&gt; SRR975604     3  0.6045      0.757 0.380 0.000 0.620
</code></pre>

<script>
$('#tab-SD-mclust-get-classes-2-a').parent().next().next().hide();
$('#tab-SD-mclust-get-classes-2-a').click(function(){
  $('#tab-SD-mclust-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-mclust-get-classes-3'>
<p><a id='tab-SD-mclust-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3    p4
#&gt; SRR975551     1  0.0000      0.940 1.000 0.000 0.000 0.000
#&gt; SRR975552     1  0.0000      0.940 1.000 0.000 0.000 0.000
#&gt; SRR975554     1  0.2759      0.921 0.904 0.000 0.044 0.052
#&gt; SRR975553     2  0.0000      0.989 0.000 1.000 0.000 0.000
#&gt; SRR975555     1  0.0336      0.941 0.992 0.000 0.000 0.008
#&gt; SRR975556     4  0.5657      0.855 0.220 0.048 0.016 0.716
#&gt; SRR975557     4  0.1557      0.753 0.000 0.000 0.056 0.944
#&gt; SRR975558     4  0.4399      0.874 0.224 0.000 0.016 0.760
#&gt; SRR975559     1  0.3037      0.901 0.880 0.000 0.020 0.100
#&gt; SRR975560     4  0.4364      0.876 0.220 0.000 0.016 0.764
#&gt; SRR975561     4  0.5337      0.872 0.200 0.036 0.020 0.744
#&gt; SRR975562     1  0.2271      0.926 0.916 0.000 0.008 0.076
#&gt; SRR975563     2  0.0000      0.989 0.000 1.000 0.000 0.000
#&gt; SRR975564     1  0.0921      0.940 0.972 0.000 0.000 0.028
#&gt; SRR975565     1  0.0000      0.940 1.000 0.000 0.000 0.000
#&gt; SRR975566     1  0.2751      0.914 0.904 0.000 0.056 0.040
#&gt; SRR975567     4  0.4399      0.874 0.224 0.000 0.016 0.760
#&gt; SRR975568     1  0.0000      0.940 1.000 0.000 0.000 0.000
#&gt; SRR975569     2  0.0000      0.989 0.000 1.000 0.000 0.000
#&gt; SRR975570     2  0.0000      0.989 0.000 1.000 0.000 0.000
#&gt; SRR975571     2  0.0000      0.989 0.000 1.000 0.000 0.000
#&gt; SRR975572     2  0.0000      0.989 0.000 1.000 0.000 0.000
#&gt; SRR975573     2  0.0000      0.989 0.000 1.000 0.000 0.000
#&gt; SRR975574     2  0.3048      0.838 0.108 0.876 0.000 0.016
#&gt; SRR975575     2  0.0000      0.989 0.000 1.000 0.000 0.000
#&gt; SRR975576     2  0.0000      0.989 0.000 1.000 0.000 0.000
#&gt; SRR975577     2  0.0000      0.989 0.000 1.000 0.000 0.000
#&gt; SRR975578     2  0.0000      0.989 0.000 1.000 0.000 0.000
#&gt; SRR975579     4  0.1389      0.756 0.000 0.000 0.048 0.952
#&gt; SRR975580     4  0.4364      0.876 0.220 0.000 0.016 0.764
#&gt; SRR975581     2  0.0000      0.989 0.000 1.000 0.000 0.000
#&gt; SRR975582     2  0.0000      0.989 0.000 1.000 0.000 0.000
#&gt; SRR975583     2  0.0000      0.989 0.000 1.000 0.000 0.000
#&gt; SRR975584     2  0.0000      0.989 0.000 1.000 0.000 0.000
#&gt; SRR975585     2  0.1209      0.952 0.032 0.964 0.000 0.004
#&gt; SRR975586     4  0.5515      0.813 0.120 0.104 0.016 0.760
#&gt; SRR975587     3  0.0000      0.880 0.000 0.000 1.000 0.000
#&gt; SRR975588     2  0.0000      0.989 0.000 1.000 0.000 0.000
#&gt; SRR975589     3  0.3444      0.822 0.184 0.000 0.816 0.000
#&gt; SRR975590     3  0.1867      0.875 0.072 0.000 0.928 0.000
#&gt; SRR975591     3  0.0000      0.880 0.000 0.000 1.000 0.000
#&gt; SRR975592     3  0.1792      0.876 0.068 0.000 0.932 0.000
#&gt; SRR975593     3  0.3311      0.829 0.172 0.000 0.828 0.000
#&gt; SRR975594     3  0.0000      0.880 0.000 0.000 1.000 0.000
#&gt; SRR975595     3  0.4252      0.781 0.252 0.000 0.744 0.004
#&gt; SRR975597     3  0.4188      0.788 0.244 0.000 0.752 0.004
#&gt; SRR975596     1  0.3215      0.900 0.876 0.000 0.032 0.092
#&gt; SRR975598     3  0.4103      0.779 0.256 0.000 0.744 0.000
#&gt; SRR975599     3  0.1411      0.872 0.020 0.000 0.960 0.020
#&gt; SRR975600     3  0.0000      0.880 0.000 0.000 1.000 0.000
#&gt; SRR975601     3  0.0000      0.880 0.000 0.000 1.000 0.000
#&gt; SRR975602     3  0.4977      0.407 0.460 0.000 0.540 0.000
#&gt; SRR975603     3  0.0000      0.880 0.000 0.000 1.000 0.000
#&gt; SRR975604     3  0.0000      0.880 0.000 0.000 1.000 0.000
</code></pre>

<script>
$('#tab-SD-mclust-get-classes-3-a').parent().next().next().hide();
$('#tab-SD-mclust-get-classes-3-a').click(function(){
  $('#tab-SD-mclust-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-mclust-get-classes-4'>
<p><a id='tab-SD-mclust-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3    p4    p5
#&gt; SRR975551     1  0.2648      0.682 0.848 0.000 0.000 0.000 0.152
#&gt; SRR975552     1  0.2732      0.674 0.840 0.000 0.000 0.000 0.160
#&gt; SRR975554     5  0.5926      0.630 0.164 0.000 0.204 0.008 0.624
#&gt; SRR975553     2  0.0898      0.952 0.000 0.972 0.000 0.020 0.008
#&gt; SRR975555     1  0.3857      0.394 0.688 0.000 0.000 0.000 0.312
#&gt; SRR975556     5  0.1568      0.695 0.000 0.036 0.000 0.020 0.944
#&gt; SRR975557     4  0.1750      1.000 0.000 0.000 0.028 0.936 0.036
#&gt; SRR975558     5  0.1408      0.718 0.044 0.000 0.008 0.000 0.948
#&gt; SRR975559     5  0.5809      0.647 0.164 0.000 0.188 0.008 0.640
#&gt; SRR975560     5  0.0609      0.702 0.000 0.000 0.000 0.020 0.980
#&gt; SRR975561     5  0.2270      0.662 0.000 0.076 0.000 0.020 0.904
#&gt; SRR975562     5  0.5778      0.645 0.184 0.000 0.164 0.008 0.644
#&gt; SRR975563     2  0.0290      0.963 0.000 0.992 0.000 0.000 0.008
#&gt; SRR975564     5  0.5315      0.494 0.332 0.000 0.068 0.000 0.600
#&gt; SRR975565     1  0.2648      0.682 0.848 0.000 0.000 0.000 0.152
#&gt; SRR975566     5  0.6032      0.615 0.164 0.000 0.220 0.008 0.608
#&gt; SRR975567     5  0.1408      0.718 0.044 0.000 0.008 0.000 0.948
#&gt; SRR975568     1  0.2648      0.682 0.848 0.000 0.000 0.000 0.152
#&gt; SRR975569     2  0.0000      0.968 0.000 1.000 0.000 0.000 0.000
#&gt; SRR975570     2  0.0000      0.968 0.000 1.000 0.000 0.000 0.000
#&gt; SRR975571     2  0.0898      0.952 0.000 0.972 0.000 0.020 0.008
#&gt; SRR975572     2  0.0000      0.968 0.000 1.000 0.000 0.000 0.000
#&gt; SRR975573     2  0.0000      0.968 0.000 1.000 0.000 0.000 0.000
#&gt; SRR975574     2  0.3366      0.685 0.000 0.768 0.000 0.000 0.232
#&gt; SRR975575     2  0.0000      0.968 0.000 1.000 0.000 0.000 0.000
#&gt; SRR975576     2  0.0000      0.968 0.000 1.000 0.000 0.000 0.000
#&gt; SRR975577     2  0.0000      0.968 0.000 1.000 0.000 0.000 0.000
#&gt; SRR975578     2  0.0290      0.964 0.000 0.992 0.000 0.000 0.008
#&gt; SRR975579     4  0.1750      1.000 0.000 0.000 0.028 0.936 0.036
#&gt; SRR975580     5  0.1568      0.695 0.000 0.036 0.000 0.020 0.944
#&gt; SRR975581     2  0.0898      0.952 0.000 0.972 0.000 0.020 0.008
#&gt; SRR975582     2  0.0000      0.968 0.000 1.000 0.000 0.000 0.000
#&gt; SRR975583     2  0.0000      0.968 0.000 1.000 0.000 0.000 0.000
#&gt; SRR975584     2  0.0000      0.968 0.000 1.000 0.000 0.000 0.000
#&gt; SRR975585     2  0.2329      0.836 0.000 0.876 0.000 0.000 0.124
#&gt; SRR975586     5  0.3106      0.562 0.000 0.140 0.000 0.020 0.840
#&gt; SRR975587     3  0.1671      0.839 0.076 0.000 0.924 0.000 0.000
#&gt; SRR975588     2  0.0000      0.968 0.000 1.000 0.000 0.000 0.000
#&gt; SRR975589     3  0.4127      0.811 0.156 0.000 0.792 0.028 0.024
#&gt; SRR975590     3  0.4021      0.780 0.200 0.000 0.764 0.036 0.000
#&gt; SRR975591     3  0.0000      0.858 0.000 0.000 1.000 0.000 0.000
#&gt; SRR975592     3  0.3099      0.840 0.124 0.000 0.848 0.028 0.000
#&gt; SRR975593     3  0.4127      0.811 0.156 0.000 0.792 0.028 0.024
#&gt; SRR975594     3  0.0162      0.856 0.004 0.000 0.996 0.000 0.000
#&gt; SRR975595     1  0.4829      0.315 0.660 0.000 0.300 0.036 0.004
#&gt; SRR975597     1  0.4829      0.315 0.660 0.000 0.300 0.036 0.004
#&gt; SRR975596     5  0.5809      0.647 0.164 0.000 0.188 0.008 0.640
#&gt; SRR975598     1  0.4809      0.323 0.664 0.000 0.296 0.036 0.004
#&gt; SRR975599     3  0.5792      0.372 0.404 0.000 0.528 0.028 0.040
#&gt; SRR975600     3  0.1671      0.862 0.076 0.000 0.924 0.000 0.000
#&gt; SRR975601     3  0.0703      0.857 0.024 0.000 0.976 0.000 0.000
#&gt; SRR975602     1  0.4228      0.673 0.788 0.000 0.068 0.008 0.136
#&gt; SRR975603     3  0.1121      0.864 0.044 0.000 0.956 0.000 0.000
#&gt; SRR975604     3  0.0000      0.858 0.000 0.000 1.000 0.000 0.000
</code></pre>

<script>
$('#tab-SD-mclust-get-classes-4-a').parent().next().next().hide();
$('#tab-SD-mclust-get-classes-4-a').click(function(){
  $('#tab-SD-mclust-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-mclust-get-classes-5'>
<p><a id='tab-SD-mclust-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3    p4    p5    p6
#&gt; SRR975551     1  0.4015      0.533 0.616 0.000 0.000 0.000 0.372 0.012
#&gt; SRR975552     1  0.4277      0.530 0.616 0.000 0.000 0.000 0.356 0.028
#&gt; SRR975554     5  0.0547      0.901 0.000 0.000 0.020 0.000 0.980 0.000
#&gt; SRR975553     2  0.1863      0.875 0.000 0.896 0.000 0.000 0.000 0.104
#&gt; SRR975555     1  0.4325      0.416 0.524 0.000 0.000 0.000 0.456 0.020
#&gt; SRR975556     6  0.3345      0.847 0.000 0.028 0.000 0.000 0.184 0.788
#&gt; SRR975557     4  0.0146      1.000 0.000 0.000 0.000 0.996 0.000 0.004
#&gt; SRR975558     6  0.3868      0.499 0.000 0.000 0.000 0.000 0.492 0.508
#&gt; SRR975559     5  0.0692      0.907 0.000 0.000 0.004 0.000 0.976 0.020
#&gt; SRR975560     6  0.3136      0.842 0.000 0.016 0.000 0.000 0.188 0.796
#&gt; SRR975561     6  0.3377      0.846 0.000 0.028 0.000 0.000 0.188 0.784
#&gt; SRR975562     5  0.0363      0.902 0.000 0.000 0.000 0.000 0.988 0.012
#&gt; SRR975563     2  0.0458      0.935 0.000 0.984 0.000 0.000 0.000 0.016
#&gt; SRR975564     5  0.3136      0.561 0.188 0.000 0.000 0.000 0.796 0.016
#&gt; SRR975565     1  0.4015      0.533 0.616 0.000 0.000 0.000 0.372 0.012
#&gt; SRR975566     5  0.1461      0.878 0.000 0.000 0.044 0.000 0.940 0.016
#&gt; SRR975567     6  0.3868      0.499 0.000 0.000 0.000 0.000 0.492 0.508
#&gt; SRR975568     1  0.4037      0.527 0.608 0.000 0.000 0.000 0.380 0.012
#&gt; SRR975569     2  0.0000      0.944 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR975570     2  0.0000      0.944 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR975571     2  0.1863      0.875 0.000 0.896 0.000 0.000 0.000 0.104
#&gt; SRR975572     2  0.0000      0.944 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR975573     2  0.0000      0.944 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR975574     2  0.4170      0.484 0.000 0.660 0.000 0.000 0.032 0.308
#&gt; SRR975575     2  0.0000      0.944 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR975576     2  0.0146      0.942 0.000 0.996 0.000 0.000 0.000 0.004
#&gt; SRR975577     2  0.0000      0.944 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR975578     2  0.0000      0.944 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR975579     4  0.0146      1.000 0.000 0.000 0.000 0.996 0.000 0.004
#&gt; SRR975580     6  0.3269      0.847 0.000 0.024 0.000 0.000 0.184 0.792
#&gt; SRR975581     2  0.1910      0.873 0.000 0.892 0.000 0.000 0.000 0.108
#&gt; SRR975582     2  0.0000      0.944 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR975583     2  0.0000      0.944 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR975584     2  0.0000      0.944 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR975585     2  0.2942      0.792 0.000 0.836 0.000 0.000 0.032 0.132
#&gt; SRR975586     6  0.3588      0.832 0.000 0.044 0.000 0.000 0.180 0.776
#&gt; SRR975587     3  0.1434      0.755 0.048 0.000 0.940 0.000 0.000 0.012
#&gt; SRR975588     2  0.0000      0.944 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR975589     3  0.6922      0.376 0.236 0.000 0.392 0.004 0.320 0.048
#&gt; SRR975590     3  0.5495      0.659 0.208 0.000 0.652 0.004 0.044 0.092
#&gt; SRR975591     3  0.0291      0.757 0.000 0.000 0.992 0.000 0.004 0.004
#&gt; SRR975592     3  0.4605      0.699 0.176 0.000 0.732 0.004 0.028 0.060
#&gt; SRR975593     3  0.6912      0.391 0.236 0.000 0.400 0.004 0.312 0.048
#&gt; SRR975594     3  0.0909      0.745 0.020 0.000 0.968 0.000 0.000 0.012
#&gt; SRR975595     1  0.5419      0.238 0.648 0.000 0.140 0.004 0.020 0.188
#&gt; SRR975597     1  0.5419      0.238 0.648 0.000 0.140 0.004 0.020 0.188
#&gt; SRR975596     5  0.0692      0.907 0.000 0.000 0.004 0.000 0.976 0.020
#&gt; SRR975598     1  0.5419      0.238 0.648 0.000 0.140 0.004 0.020 0.188
#&gt; SRR975599     3  0.6944      0.458 0.292 0.000 0.456 0.004 0.084 0.164
#&gt; SRR975600     3  0.2163      0.757 0.096 0.000 0.892 0.000 0.008 0.004
#&gt; SRR975601     3  0.1074      0.749 0.028 0.000 0.960 0.000 0.000 0.012
#&gt; SRR975602     1  0.4593      0.496 0.632 0.000 0.024 0.000 0.324 0.020
#&gt; SRR975603     3  0.1410      0.762 0.044 0.000 0.944 0.000 0.008 0.004
#&gt; SRR975604     3  0.0146      0.756 0.000 0.000 0.996 0.000 0.004 0.000
</code></pre>

<script>
$('#tab-SD-mclust-get-classes-5-a').parent().next().next().hide();
$('#tab-SD-mclust-get-classes-5-a').click(function(){
  $('#tab-SD-mclust-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-SD-mclust-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-SD-mclust-consensus-heatmap'>
<ul>
<li><a href='#tab-SD-mclust-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-SD-mclust-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-SD-mclust-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-SD-mclust-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-SD-mclust-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-SD-mclust-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-consensus-heatmap-1-1.png" alt="plot of chunk tab-SD-mclust-consensus-heatmap-1"/></p>

</div>
<div id='tab-SD-mclust-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-consensus-heatmap-2-1.png" alt="plot of chunk tab-SD-mclust-consensus-heatmap-2"/></p>

</div>
<div id='tab-SD-mclust-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-consensus-heatmap-3-1.png" alt="plot of chunk tab-SD-mclust-consensus-heatmap-3"/></p>

</div>
<div id='tab-SD-mclust-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-consensus-heatmap-4-1.png" alt="plot of chunk tab-SD-mclust-consensus-heatmap-4"/></p>

</div>
<div id='tab-SD-mclust-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-consensus-heatmap-5-1.png" alt="plot of chunk tab-SD-mclust-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-SD-mclust-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-SD-mclust-membership-heatmap'>
<ul>
<li><a href='#tab-SD-mclust-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-SD-mclust-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-SD-mclust-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-SD-mclust-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-SD-mclust-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-SD-mclust-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-membership-heatmap-1-1.png" alt="plot of chunk tab-SD-mclust-membership-heatmap-1"/></p>

</div>
<div id='tab-SD-mclust-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-membership-heatmap-2-1.png" alt="plot of chunk tab-SD-mclust-membership-heatmap-2"/></p>

</div>
<div id='tab-SD-mclust-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-membership-heatmap-3-1.png" alt="plot of chunk tab-SD-mclust-membership-heatmap-3"/></p>

</div>
<div id='tab-SD-mclust-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-membership-heatmap-4-1.png" alt="plot of chunk tab-SD-mclust-membership-heatmap-4"/></p>

</div>
<div id='tab-SD-mclust-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-membership-heatmap-5-1.png" alt="plot of chunk tab-SD-mclust-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-SD-mclust-get-signatures' ).tabs();
} );
</script>
<div id='tabs-SD-mclust-get-signatures'>
<ul>
<li><a href='#tab-SD-mclust-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-SD-mclust-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-SD-mclust-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-SD-mclust-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-SD-mclust-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-SD-mclust-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-get-signatures-1-1.png" alt="plot of chunk tab-SD-mclust-get-signatures-1"/></p>

</div>
<div id='tab-SD-mclust-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-get-signatures-2-1.png" alt="plot of chunk tab-SD-mclust-get-signatures-2"/></p>

</div>
<div id='tab-SD-mclust-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-get-signatures-3-1.png" alt="plot of chunk tab-SD-mclust-get-signatures-3"/></p>

</div>
<div id='tab-SD-mclust-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-get-signatures-4-1.png" alt="plot of chunk tab-SD-mclust-get-signatures-4"/></p>

</div>
<div id='tab-SD-mclust-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-get-signatures-5-1.png" alt="plot of chunk tab-SD-mclust-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-SD-mclust-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-SD-mclust-get-signatures-no-scale'>
<ul>
<li><a href='#tab-SD-mclust-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-SD-mclust-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-SD-mclust-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-SD-mclust-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-SD-mclust-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-SD-mclust-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-SD-mclust-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-SD-mclust-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-SD-mclust-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-SD-mclust-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-SD-mclust-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-SD-mclust-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-SD-mclust-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-SD-mclust-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-SD-mclust-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk SD-mclust-signature_compare](figure_cola/SD-mclust-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-SD-mclust-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-SD-mclust-dimension-reduction'>
<ul>
<li><a href='#tab-SD-mclust-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-SD-mclust-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-SD-mclust-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-SD-mclust-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-SD-mclust-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-SD-mclust-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-dimension-reduction-1-1.png" alt="plot of chunk tab-SD-mclust-dimension-reduction-1"/></p>

</div>
<div id='tab-SD-mclust-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-dimension-reduction-2-1.png" alt="plot of chunk tab-SD-mclust-dimension-reduction-2"/></p>

</div>
<div id='tab-SD-mclust-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-dimension-reduction-3-1.png" alt="plot of chunk tab-SD-mclust-dimension-reduction-3"/></p>

</div>
<div id='tab-SD-mclust-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-dimension-reduction-4-1.png" alt="plot of chunk tab-SD-mclust-dimension-reduction-4"/></p>

</div>
<div id='tab-SD-mclust-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-dimension-reduction-5-1.png" alt="plot of chunk tab-SD-mclust-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk SD-mclust-collect-classes](figure_cola/SD-mclust-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### SD:NMF*






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["SD", "NMF"]
# you can also extract it by
# res = res_list["SD:NMF"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 17171 rows and 54 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'SD' method.
#>   Subgroups are detected by 'NMF' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 4.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk SD-NMF-collect-plots](figure_cola/SD-NMF-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk SD-NMF-select-partition-number](figure_cola/SD-NMF-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 1.000           0.944       0.980         0.5065 0.493   0.493
#> 3 3 0.905           0.916       0.959         0.2509 0.860   0.725
#> 4 4 0.929           0.900       0.954         0.0589 0.940   0.844
#> 5 5 0.790           0.749       0.868         0.0966 0.928   0.788
#> 6 6 0.773           0.724       0.827         0.0683 0.911   0.692
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 4
#> attr(,"optional")
#> [1] 2 3
```

There is also optional best $k$ = 2 3 that is worth to check.

Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-SD-NMF-get-classes' ).tabs();
} );
</script>
<div id='tabs-SD-NMF-get-classes'>
<ul>
<li><a href='#tab-SD-NMF-get-classes-1'>k = 2</a></li>
<li><a href='#tab-SD-NMF-get-classes-2'>k = 3</a></li>
<li><a href='#tab-SD-NMF-get-classes-3'>k = 4</a></li>
<li><a href='#tab-SD-NMF-get-classes-4'>k = 5</a></li>
<li><a href='#tab-SD-NMF-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-SD-NMF-get-classes-1'>
<p><a id='tab-SD-NMF-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2
#&gt; SRR975551     1   0.000     0.9772 1.000 0.000
#&gt; SRR975552     1   0.662     0.7828 0.828 0.172
#&gt; SRR975554     1   0.000     0.9772 1.000 0.000
#&gt; SRR975553     2   0.000     0.9794 0.000 1.000
#&gt; SRR975555     1   0.184     0.9518 0.972 0.028
#&gt; SRR975556     2   0.000     0.9794 0.000 1.000
#&gt; SRR975557     1   0.000     0.9772 1.000 0.000
#&gt; SRR975558     2   0.998     0.0535 0.472 0.528
#&gt; SRR975559     1   0.000     0.9772 1.000 0.000
#&gt; SRR975560     2   0.000     0.9794 0.000 1.000
#&gt; SRR975561     2   0.000     0.9794 0.000 1.000
#&gt; SRR975562     1   0.000     0.9772 1.000 0.000
#&gt; SRR975563     2   0.000     0.9794 0.000 1.000
#&gt; SRR975564     1   0.000     0.9772 1.000 0.000
#&gt; SRR975565     1   0.000     0.9772 1.000 0.000
#&gt; SRR975566     1   0.000     0.9772 1.000 0.000
#&gt; SRR975567     1   0.980     0.2804 0.584 0.416
#&gt; SRR975568     1   0.000     0.9772 1.000 0.000
#&gt; SRR975569     2   0.000     0.9794 0.000 1.000
#&gt; SRR975570     2   0.000     0.9794 0.000 1.000
#&gt; SRR975571     2   0.000     0.9794 0.000 1.000
#&gt; SRR975572     2   0.000     0.9794 0.000 1.000
#&gt; SRR975573     2   0.000     0.9794 0.000 1.000
#&gt; SRR975574     2   0.000     0.9794 0.000 1.000
#&gt; SRR975575     2   0.000     0.9794 0.000 1.000
#&gt; SRR975576     2   0.000     0.9794 0.000 1.000
#&gt; SRR975577     2   0.000     0.9794 0.000 1.000
#&gt; SRR975578     2   0.000     0.9794 0.000 1.000
#&gt; SRR975579     2   0.000     0.9794 0.000 1.000
#&gt; SRR975580     2   0.000     0.9794 0.000 1.000
#&gt; SRR975581     2   0.000     0.9794 0.000 1.000
#&gt; SRR975582     2   0.000     0.9794 0.000 1.000
#&gt; SRR975583     2   0.000     0.9794 0.000 1.000
#&gt; SRR975584     2   0.000     0.9794 0.000 1.000
#&gt; SRR975585     2   0.000     0.9794 0.000 1.000
#&gt; SRR975586     2   0.000     0.9794 0.000 1.000
#&gt; SRR975587     1   0.000     0.9772 1.000 0.000
#&gt; SRR975588     2   0.000     0.9794 0.000 1.000
#&gt; SRR975589     1   0.000     0.9772 1.000 0.000
#&gt; SRR975590     1   0.000     0.9772 1.000 0.000
#&gt; SRR975591     1   0.000     0.9772 1.000 0.000
#&gt; SRR975592     1   0.000     0.9772 1.000 0.000
#&gt; SRR975593     1   0.000     0.9772 1.000 0.000
#&gt; SRR975594     1   0.000     0.9772 1.000 0.000
#&gt; SRR975595     1   0.000     0.9772 1.000 0.000
#&gt; SRR975597     1   0.000     0.9772 1.000 0.000
#&gt; SRR975596     1   0.000     0.9772 1.000 0.000
#&gt; SRR975598     1   0.000     0.9772 1.000 0.000
#&gt; SRR975599     1   0.000     0.9772 1.000 0.000
#&gt; SRR975600     1   0.000     0.9772 1.000 0.000
#&gt; SRR975601     1   0.000     0.9772 1.000 0.000
#&gt; SRR975602     1   0.000     0.9772 1.000 0.000
#&gt; SRR975603     1   0.000     0.9772 1.000 0.000
#&gt; SRR975604     1   0.000     0.9772 1.000 0.000
</code></pre>

<script>
$('#tab-SD-NMF-get-classes-1-a').parent().next().next().hide();
$('#tab-SD-NMF-get-classes-1-a').click(function(){
  $('#tab-SD-NMF-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-NMF-get-classes-2'>
<p><a id='tab-SD-NMF-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3
#&gt; SRR975551     1  0.0000      0.906 1.000 0.000 0.000
#&gt; SRR975552     1  0.0000      0.906 1.000 0.000 0.000
#&gt; SRR975554     1  0.0000      0.906 1.000 0.000 0.000
#&gt; SRR975553     2  0.0000      0.990 0.000 1.000 0.000
#&gt; SRR975555     1  0.0000      0.906 1.000 0.000 0.000
#&gt; SRR975556     2  0.0000      0.990 0.000 1.000 0.000
#&gt; SRR975557     1  0.6267      0.133 0.548 0.000 0.452
#&gt; SRR975558     1  0.1031      0.890 0.976 0.024 0.000
#&gt; SRR975559     1  0.0000      0.906 1.000 0.000 0.000
#&gt; SRR975560     2  0.0000      0.990 0.000 1.000 0.000
#&gt; SRR975561     2  0.0000      0.990 0.000 1.000 0.000
#&gt; SRR975562     1  0.0000      0.906 1.000 0.000 0.000
#&gt; SRR975563     2  0.0000      0.990 0.000 1.000 0.000
#&gt; SRR975564     1  0.0000      0.906 1.000 0.000 0.000
#&gt; SRR975565     1  0.0000      0.906 1.000 0.000 0.000
#&gt; SRR975566     1  0.0000      0.906 1.000 0.000 0.000
#&gt; SRR975567     1  0.0237      0.903 0.996 0.004 0.000
#&gt; SRR975568     1  0.0000      0.906 1.000 0.000 0.000
#&gt; SRR975569     2  0.0000      0.990 0.000 1.000 0.000
#&gt; SRR975570     2  0.0000      0.990 0.000 1.000 0.000
#&gt; SRR975571     2  0.0000      0.990 0.000 1.000 0.000
#&gt; SRR975572     2  0.0000      0.990 0.000 1.000 0.000
#&gt; SRR975573     2  0.0000      0.990 0.000 1.000 0.000
#&gt; SRR975574     2  0.0000      0.990 0.000 1.000 0.000
#&gt; SRR975575     2  0.0000      0.990 0.000 1.000 0.000
#&gt; SRR975576     2  0.0000      0.990 0.000 1.000 0.000
#&gt; SRR975577     2  0.0000      0.990 0.000 1.000 0.000
#&gt; SRR975578     2  0.0000      0.990 0.000 1.000 0.000
#&gt; SRR975579     2  0.4796      0.718 0.000 0.780 0.220
#&gt; SRR975580     2  0.0000      0.990 0.000 1.000 0.000
#&gt; SRR975581     2  0.0000      0.990 0.000 1.000 0.000
#&gt; SRR975582     2  0.0000      0.990 0.000 1.000 0.000
#&gt; SRR975583     2  0.0000      0.990 0.000 1.000 0.000
#&gt; SRR975584     2  0.0000      0.990 0.000 1.000 0.000
#&gt; SRR975585     2  0.0000      0.990 0.000 1.000 0.000
#&gt; SRR975586     2  0.0000      0.990 0.000 1.000 0.000
#&gt; SRR975587     3  0.0237      1.000 0.004 0.000 0.996
#&gt; SRR975588     2  0.0000      0.990 0.000 1.000 0.000
#&gt; SRR975589     1  0.1643      0.890 0.956 0.000 0.044
#&gt; SRR975590     1  0.5216      0.711 0.740 0.000 0.260
#&gt; SRR975591     3  0.0237      1.000 0.004 0.000 0.996
#&gt; SRR975592     1  0.6062      0.498 0.616 0.000 0.384
#&gt; SRR975593     1  0.1964      0.887 0.944 0.000 0.056
#&gt; SRR975594     3  0.0237      1.000 0.004 0.000 0.996
#&gt; SRR975595     1  0.4702      0.769 0.788 0.000 0.212
#&gt; SRR975597     1  0.4555      0.781 0.800 0.000 0.200
#&gt; SRR975596     1  0.0000      0.906 1.000 0.000 0.000
#&gt; SRR975598     1  0.4555      0.781 0.800 0.000 0.200
#&gt; SRR975599     1  0.3192      0.851 0.888 0.000 0.112
#&gt; SRR975600     3  0.0237      1.000 0.004 0.000 0.996
#&gt; SRR975601     3  0.0237      1.000 0.004 0.000 0.996
#&gt; SRR975602     1  0.0000      0.906 1.000 0.000 0.000
#&gt; SRR975603     3  0.0237      1.000 0.004 0.000 0.996
#&gt; SRR975604     3  0.0237      1.000 0.004 0.000 0.996
</code></pre>

<script>
$('#tab-SD-NMF-get-classes-2-a').parent().next().next().hide();
$('#tab-SD-NMF-get-classes-2-a').click(function(){
  $('#tab-SD-NMF-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-NMF-get-classes-3'>
<p><a id='tab-SD-NMF-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3    p4
#&gt; SRR975551     1  0.0000      0.892 1.000 0.000 0.000 0.000
#&gt; SRR975552     1  0.0000      0.892 1.000 0.000 0.000 0.000
#&gt; SRR975554     1  0.0000      0.892 1.000 0.000 0.000 0.000
#&gt; SRR975553     2  0.0000      0.999 0.000 1.000 0.000 0.000
#&gt; SRR975555     1  0.0336      0.890 0.992 0.000 0.000 0.008
#&gt; SRR975556     2  0.0336      0.992 0.000 0.992 0.000 0.008
#&gt; SRR975557     4  0.0336      0.618 0.008 0.000 0.000 0.992
#&gt; SRR975558     4  0.6714      0.550 0.360 0.100 0.000 0.540
#&gt; SRR975559     1  0.2149      0.817 0.912 0.000 0.000 0.088
#&gt; SRR975560     2  0.0000      0.999 0.000 1.000 0.000 0.000
#&gt; SRR975561     2  0.0000      0.999 0.000 1.000 0.000 0.000
#&gt; SRR975562     1  0.0000      0.892 1.000 0.000 0.000 0.000
#&gt; SRR975563     2  0.0000      0.999 0.000 1.000 0.000 0.000
#&gt; SRR975564     1  0.0000      0.892 1.000 0.000 0.000 0.000
#&gt; SRR975565     1  0.0000      0.892 1.000 0.000 0.000 0.000
#&gt; SRR975566     1  0.0000      0.892 1.000 0.000 0.000 0.000
#&gt; SRR975567     4  0.6233      0.507 0.388 0.060 0.000 0.552
#&gt; SRR975568     1  0.0000      0.892 1.000 0.000 0.000 0.000
#&gt; SRR975569     2  0.0000      0.999 0.000 1.000 0.000 0.000
#&gt; SRR975570     2  0.0000      0.999 0.000 1.000 0.000 0.000
#&gt; SRR975571     2  0.0000      0.999 0.000 1.000 0.000 0.000
#&gt; SRR975572     2  0.0000      0.999 0.000 1.000 0.000 0.000
#&gt; SRR975573     2  0.0000      0.999 0.000 1.000 0.000 0.000
#&gt; SRR975574     2  0.0000      0.999 0.000 1.000 0.000 0.000
#&gt; SRR975575     2  0.0000      0.999 0.000 1.000 0.000 0.000
#&gt; SRR975576     2  0.0000      0.999 0.000 1.000 0.000 0.000
#&gt; SRR975577     2  0.0000      0.999 0.000 1.000 0.000 0.000
#&gt; SRR975578     2  0.0000      0.999 0.000 1.000 0.000 0.000
#&gt; SRR975579     4  0.0592      0.616 0.000 0.016 0.000 0.984
#&gt; SRR975580     2  0.0336      0.992 0.000 0.992 0.000 0.008
#&gt; SRR975581     2  0.0000      0.999 0.000 1.000 0.000 0.000
#&gt; SRR975582     2  0.0000      0.999 0.000 1.000 0.000 0.000
#&gt; SRR975583     2  0.0000      0.999 0.000 1.000 0.000 0.000
#&gt; SRR975584     2  0.0000      0.999 0.000 1.000 0.000 0.000
#&gt; SRR975585     2  0.0000      0.999 0.000 1.000 0.000 0.000
#&gt; SRR975586     2  0.0000      0.999 0.000 1.000 0.000 0.000
#&gt; SRR975587     3  0.0000      1.000 0.000 0.000 1.000 0.000
#&gt; SRR975588     2  0.0000      0.999 0.000 1.000 0.000 0.000
#&gt; SRR975589     1  0.1716      0.865 0.936 0.000 0.064 0.000
#&gt; SRR975590     1  0.4431      0.580 0.696 0.000 0.304 0.000
#&gt; SRR975591     3  0.0000      1.000 0.000 0.000 1.000 0.000
#&gt; SRR975592     1  0.5000      0.170 0.504 0.000 0.496 0.000
#&gt; SRR975593     1  0.2469      0.834 0.892 0.000 0.108 0.000
#&gt; SRR975594     3  0.0000      1.000 0.000 0.000 1.000 0.000
#&gt; SRR975595     1  0.3444      0.753 0.816 0.000 0.184 0.000
#&gt; SRR975597     1  0.2760      0.816 0.872 0.000 0.128 0.000
#&gt; SRR975596     1  0.1637      0.844 0.940 0.000 0.000 0.060
#&gt; SRR975598     1  0.2011      0.856 0.920 0.000 0.080 0.000
#&gt; SRR975599     1  0.0336      0.890 0.992 0.000 0.008 0.000
#&gt; SRR975600     3  0.0000      1.000 0.000 0.000 1.000 0.000
#&gt; SRR975601     3  0.0000      1.000 0.000 0.000 1.000 0.000
#&gt; SRR975602     1  0.0000      0.892 1.000 0.000 0.000 0.000
#&gt; SRR975603     3  0.0000      1.000 0.000 0.000 1.000 0.000
#&gt; SRR975604     3  0.0000      1.000 0.000 0.000 1.000 0.000
</code></pre>

<script>
$('#tab-SD-NMF-get-classes-3-a').parent().next().next().hide();
$('#tab-SD-NMF-get-classes-3-a').click(function(){
  $('#tab-SD-NMF-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-NMF-get-classes-4'>
<p><a id='tab-SD-NMF-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3    p4    p5
#&gt; SRR975551     1  0.2561      0.725 0.856 0.000 0.000 0.000 0.144
#&gt; SRR975552     1  0.2852      0.722 0.828 0.000 0.000 0.000 0.172
#&gt; SRR975554     1  0.4302      0.186 0.520 0.000 0.000 0.000 0.480
#&gt; SRR975553     2  0.1121      0.943 0.000 0.956 0.000 0.000 0.044
#&gt; SRR975555     1  0.4283      0.252 0.544 0.000 0.000 0.000 0.456
#&gt; SRR975556     2  0.1908      0.912 0.000 0.908 0.000 0.000 0.092
#&gt; SRR975557     4  0.0000      0.845 0.000 0.000 0.000 1.000 0.000
#&gt; SRR975558     5  0.5025      0.144 0.020 0.028 0.000 0.288 0.664
#&gt; SRR975559     1  0.4101      0.501 0.664 0.000 0.000 0.332 0.004
#&gt; SRR975560     2  0.4360      0.743 0.184 0.752 0.000 0.000 0.064
#&gt; SRR975561     2  0.1544      0.926 0.000 0.932 0.000 0.000 0.068
#&gt; SRR975562     1  0.0162      0.705 0.996 0.000 0.000 0.000 0.004
#&gt; SRR975563     2  0.1671      0.922 0.000 0.924 0.000 0.000 0.076
#&gt; SRR975564     5  0.2605      0.650 0.148 0.000 0.000 0.000 0.852
#&gt; SRR975565     1  0.2966      0.714 0.816 0.000 0.000 0.000 0.184
#&gt; SRR975566     1  0.4503      0.554 0.664 0.000 0.000 0.024 0.312
#&gt; SRR975567     4  0.5091      0.623 0.016 0.072 0.000 0.712 0.200
#&gt; SRR975568     5  0.2690      0.648 0.156 0.000 0.000 0.000 0.844
#&gt; SRR975569     2  0.0510      0.946 0.000 0.984 0.000 0.000 0.016
#&gt; SRR975570     2  0.0000      0.946 0.000 1.000 0.000 0.000 0.000
#&gt; SRR975571     2  0.1121      0.943 0.000 0.956 0.000 0.000 0.044
#&gt; SRR975572     2  0.0404      0.945 0.000 0.988 0.000 0.000 0.012
#&gt; SRR975573     2  0.1121      0.943 0.000 0.956 0.000 0.000 0.044
#&gt; SRR975574     2  0.1121      0.943 0.000 0.956 0.000 0.000 0.044
#&gt; SRR975575     2  0.0404      0.945 0.000 0.988 0.000 0.000 0.012
#&gt; SRR975576     2  0.0794      0.942 0.000 0.972 0.000 0.000 0.028
#&gt; SRR975577     2  0.1121      0.943 0.000 0.956 0.000 0.000 0.044
#&gt; SRR975578     2  0.1121      0.943 0.000 0.956 0.000 0.000 0.044
#&gt; SRR975579     4  0.0000      0.845 0.000 0.000 0.000 1.000 0.000
#&gt; SRR975580     2  0.4113      0.804 0.140 0.784 0.000 0.000 0.076
#&gt; SRR975581     2  0.1043      0.938 0.000 0.960 0.000 0.000 0.040
#&gt; SRR975582     2  0.1121      0.943 0.000 0.956 0.000 0.000 0.044
#&gt; SRR975583     2  0.0404      0.945 0.000 0.988 0.000 0.000 0.012
#&gt; SRR975584     2  0.1121      0.943 0.000 0.956 0.000 0.000 0.044
#&gt; SRR975585     2  0.0510      0.945 0.000 0.984 0.000 0.000 0.016
#&gt; SRR975586     2  0.1908      0.912 0.000 0.908 0.000 0.000 0.092
#&gt; SRR975587     3  0.0000      0.916 0.000 0.000 1.000 0.000 0.000
#&gt; SRR975588     2  0.0162      0.946 0.000 0.996 0.000 0.000 0.004
#&gt; SRR975589     5  0.3163      0.645 0.164 0.000 0.012 0.000 0.824
#&gt; SRR975590     1  0.5848      0.533 0.604 0.000 0.228 0.000 0.168
#&gt; SRR975591     3  0.0000      0.916 0.000 0.000 1.000 0.000 0.000
#&gt; SRR975592     3  0.5393      0.222 0.080 0.000 0.608 0.000 0.312
#&gt; SRR975593     5  0.6949      0.160 0.388 0.000 0.144 0.032 0.436
#&gt; SRR975594     3  0.0000      0.916 0.000 0.000 1.000 0.000 0.000
#&gt; SRR975595     1  0.2583      0.640 0.864 0.000 0.132 0.000 0.004
#&gt; SRR975597     1  0.3601      0.722 0.820 0.000 0.052 0.000 0.128
#&gt; SRR975596     1  0.5334      0.395 0.672 0.000 0.000 0.148 0.180
#&gt; SRR975598     1  0.1571      0.691 0.936 0.000 0.060 0.000 0.004
#&gt; SRR975599     1  0.0324      0.705 0.992 0.000 0.004 0.000 0.004
#&gt; SRR975600     5  0.4227      0.137 0.000 0.000 0.420 0.000 0.580
#&gt; SRR975601     3  0.0000      0.916 0.000 0.000 1.000 0.000 0.000
#&gt; SRR975602     1  0.2377      0.728 0.872 0.000 0.000 0.000 0.128
#&gt; SRR975603     3  0.0290      0.909 0.000 0.000 0.992 0.000 0.008
#&gt; SRR975604     3  0.0000      0.916 0.000 0.000 1.000 0.000 0.000
</code></pre>

<script>
$('#tab-SD-NMF-get-classes-4-a').parent().next().next().hide();
$('#tab-SD-NMF-get-classes-4-a').click(function(){
  $('#tab-SD-NMF-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-NMF-get-classes-5'>
<p><a id='tab-SD-NMF-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3    p4    p5    p6
#&gt; SRR975551     1  0.4439      0.847 0.540 0.000 0.000 0.000 0.432 0.028
#&gt; SRR975552     1  0.4488      0.849 0.548 0.000 0.000 0.000 0.420 0.032
#&gt; SRR975554     1  0.5887      0.367 0.404 0.000 0.000 0.000 0.200 0.396
#&gt; SRR975553     2  0.1918      0.871 0.088 0.904 0.000 0.000 0.000 0.008
#&gt; SRR975555     6  0.4591      0.329 0.040 0.000 0.000 0.000 0.408 0.552
#&gt; SRR975556     2  0.3721      0.676 0.308 0.684 0.000 0.000 0.004 0.004
#&gt; SRR975557     4  0.0000      0.745 0.000 0.000 0.000 1.000 0.000 0.000
#&gt; SRR975558     6  0.3100      0.768 0.012 0.004 0.000 0.028 0.108 0.848
#&gt; SRR975559     4  0.4037      0.347 0.012 0.000 0.000 0.608 0.380 0.000
#&gt; SRR975560     5  0.6163      0.294 0.176 0.256 0.000 0.020 0.540 0.008
#&gt; SRR975561     2  0.3761      0.762 0.192 0.768 0.000 0.032 0.004 0.004
#&gt; SRR975562     5  0.0508      0.449 0.004 0.000 0.000 0.000 0.984 0.012
#&gt; SRR975563     2  0.3429      0.736 0.252 0.740 0.000 0.000 0.004 0.004
#&gt; SRR975564     6  0.0717      0.787 0.016 0.000 0.000 0.000 0.008 0.976
#&gt; SRR975565     1  0.4747      0.820 0.584 0.000 0.000 0.000 0.356 0.060
#&gt; SRR975566     1  0.5277      0.829 0.528 0.000 0.000 0.008 0.384 0.080
#&gt; SRR975567     4  0.5329      0.588 0.044 0.084 0.000 0.708 0.024 0.140
#&gt; SRR975568     6  0.0508      0.790 0.004 0.000 0.000 0.000 0.012 0.984
#&gt; SRR975569     2  0.0717      0.882 0.016 0.976 0.000 0.000 0.000 0.008
#&gt; SRR975570     2  0.0508      0.884 0.012 0.984 0.000 0.000 0.004 0.000
#&gt; SRR975571     2  0.1918      0.871 0.088 0.904 0.000 0.000 0.000 0.008
#&gt; SRR975572     2  0.0935      0.881 0.032 0.964 0.000 0.000 0.004 0.000
#&gt; SRR975573     2  0.1918      0.871 0.088 0.904 0.000 0.000 0.000 0.008
#&gt; SRR975574     2  0.1918      0.871 0.088 0.904 0.000 0.000 0.000 0.008
#&gt; SRR975575     2  0.0937      0.881 0.040 0.960 0.000 0.000 0.000 0.000
#&gt; SRR975576     2  0.1493      0.874 0.056 0.936 0.000 0.000 0.004 0.004
#&gt; SRR975577     2  0.1918      0.871 0.088 0.904 0.000 0.000 0.000 0.008
#&gt; SRR975578     2  0.1918      0.871 0.088 0.904 0.000 0.000 0.000 0.008
#&gt; SRR975579     4  0.0000      0.745 0.000 0.000 0.000 1.000 0.000 0.000
#&gt; SRR975580     5  0.5454      0.085 0.104 0.432 0.000 0.000 0.460 0.004
#&gt; SRR975581     2  0.1674      0.869 0.068 0.924 0.000 0.000 0.004 0.004
#&gt; SRR975582     2  0.1918      0.871 0.088 0.904 0.000 0.000 0.000 0.008
#&gt; SRR975583     2  0.1364      0.877 0.048 0.944 0.000 0.000 0.004 0.004
#&gt; SRR975584     2  0.1918      0.871 0.088 0.904 0.000 0.000 0.000 0.008
#&gt; SRR975585     2  0.1296      0.878 0.044 0.948 0.000 0.000 0.004 0.004
#&gt; SRR975586     2  0.3756      0.666 0.316 0.676 0.000 0.000 0.004 0.004
#&gt; SRR975587     3  0.0146      0.914 0.004 0.000 0.996 0.000 0.000 0.000
#&gt; SRR975588     2  0.0692      0.884 0.020 0.976 0.000 0.000 0.000 0.004
#&gt; SRR975589     6  0.1578      0.793 0.012 0.000 0.004 0.000 0.048 0.936
#&gt; SRR975590     1  0.5458      0.826 0.544 0.000 0.060 0.000 0.364 0.032
#&gt; SRR975591     3  0.0260      0.912 0.000 0.000 0.992 0.000 0.000 0.008
#&gt; SRR975592     3  0.4798      0.417 0.080 0.000 0.620 0.000 0.000 0.300
#&gt; SRR975593     6  0.4712      0.724 0.012 0.000 0.100 0.004 0.168 0.716
#&gt; SRR975594     3  0.0146      0.914 0.004 0.000 0.996 0.000 0.000 0.000
#&gt; SRR975595     5  0.4293      0.184 0.164 0.000 0.096 0.000 0.736 0.004
#&gt; SRR975597     1  0.5208      0.806 0.500 0.000 0.048 0.000 0.432 0.020
#&gt; SRR975596     5  0.4411      0.341 0.004 0.000 0.000 0.080 0.712 0.204
#&gt; SRR975598     5  0.2728      0.375 0.080 0.000 0.040 0.000 0.872 0.008
#&gt; SRR975599     5  0.1036      0.437 0.024 0.000 0.004 0.000 0.964 0.008
#&gt; SRR975600     6  0.3323      0.576 0.008 0.000 0.240 0.000 0.000 0.752
#&gt; SRR975601     3  0.0146      0.914 0.004 0.000 0.996 0.000 0.000 0.000
#&gt; SRR975602     1  0.4396      0.834 0.520 0.000 0.000 0.000 0.456 0.024
#&gt; SRR975603     3  0.1471      0.871 0.004 0.000 0.932 0.000 0.000 0.064
#&gt; SRR975604     3  0.0146      0.913 0.004 0.000 0.996 0.000 0.000 0.000
</code></pre>

<script>
$('#tab-SD-NMF-get-classes-5-a').parent().next().next().hide();
$('#tab-SD-NMF-get-classes-5-a').click(function(){
  $('#tab-SD-NMF-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-SD-NMF-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-SD-NMF-consensus-heatmap'>
<ul>
<li><a href='#tab-SD-NMF-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-SD-NMF-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-SD-NMF-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-SD-NMF-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-SD-NMF-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-SD-NMF-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-consensus-heatmap-1-1.png" alt="plot of chunk tab-SD-NMF-consensus-heatmap-1"/></p>

</div>
<div id='tab-SD-NMF-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-consensus-heatmap-2-1.png" alt="plot of chunk tab-SD-NMF-consensus-heatmap-2"/></p>

</div>
<div id='tab-SD-NMF-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-consensus-heatmap-3-1.png" alt="plot of chunk tab-SD-NMF-consensus-heatmap-3"/></p>

</div>
<div id='tab-SD-NMF-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-consensus-heatmap-4-1.png" alt="plot of chunk tab-SD-NMF-consensus-heatmap-4"/></p>

</div>
<div id='tab-SD-NMF-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-consensus-heatmap-5-1.png" alt="plot of chunk tab-SD-NMF-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-SD-NMF-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-SD-NMF-membership-heatmap'>
<ul>
<li><a href='#tab-SD-NMF-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-SD-NMF-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-SD-NMF-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-SD-NMF-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-SD-NMF-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-SD-NMF-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-membership-heatmap-1-1.png" alt="plot of chunk tab-SD-NMF-membership-heatmap-1"/></p>

</div>
<div id='tab-SD-NMF-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-membership-heatmap-2-1.png" alt="plot of chunk tab-SD-NMF-membership-heatmap-2"/></p>

</div>
<div id='tab-SD-NMF-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-membership-heatmap-3-1.png" alt="plot of chunk tab-SD-NMF-membership-heatmap-3"/></p>

</div>
<div id='tab-SD-NMF-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-membership-heatmap-4-1.png" alt="plot of chunk tab-SD-NMF-membership-heatmap-4"/></p>

</div>
<div id='tab-SD-NMF-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-membership-heatmap-5-1.png" alt="plot of chunk tab-SD-NMF-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-SD-NMF-get-signatures' ).tabs();
} );
</script>
<div id='tabs-SD-NMF-get-signatures'>
<ul>
<li><a href='#tab-SD-NMF-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-SD-NMF-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-SD-NMF-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-SD-NMF-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-SD-NMF-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-SD-NMF-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-get-signatures-1-1.png" alt="plot of chunk tab-SD-NMF-get-signatures-1"/></p>

</div>
<div id='tab-SD-NMF-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-get-signatures-2-1.png" alt="plot of chunk tab-SD-NMF-get-signatures-2"/></p>

</div>
<div id='tab-SD-NMF-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-get-signatures-3-1.png" alt="plot of chunk tab-SD-NMF-get-signatures-3"/></p>

</div>
<div id='tab-SD-NMF-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-get-signatures-4-1.png" alt="plot of chunk tab-SD-NMF-get-signatures-4"/></p>

</div>
<div id='tab-SD-NMF-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-get-signatures-5-1.png" alt="plot of chunk tab-SD-NMF-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-SD-NMF-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-SD-NMF-get-signatures-no-scale'>
<ul>
<li><a href='#tab-SD-NMF-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-SD-NMF-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-SD-NMF-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-SD-NMF-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-SD-NMF-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-SD-NMF-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-SD-NMF-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-SD-NMF-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-SD-NMF-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-SD-NMF-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-SD-NMF-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-SD-NMF-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-SD-NMF-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-SD-NMF-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-SD-NMF-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk SD-NMF-signature_compare](figure_cola/SD-NMF-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-SD-NMF-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-SD-NMF-dimension-reduction'>
<ul>
<li><a href='#tab-SD-NMF-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-SD-NMF-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-SD-NMF-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-SD-NMF-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-SD-NMF-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-SD-NMF-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-dimension-reduction-1-1.png" alt="plot of chunk tab-SD-NMF-dimension-reduction-1"/></p>

</div>
<div id='tab-SD-NMF-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-dimension-reduction-2-1.png" alt="plot of chunk tab-SD-NMF-dimension-reduction-2"/></p>

</div>
<div id='tab-SD-NMF-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-dimension-reduction-3-1.png" alt="plot of chunk tab-SD-NMF-dimension-reduction-3"/></p>

</div>
<div id='tab-SD-NMF-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-dimension-reduction-4-1.png" alt="plot of chunk tab-SD-NMF-dimension-reduction-4"/></p>

</div>
<div id='tab-SD-NMF-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-dimension-reduction-5-1.png" alt="plot of chunk tab-SD-NMF-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk SD-NMF-collect-classes](figure_cola/SD-NMF-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### CV:hclust






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["CV", "hclust"]
# you can also extract it by
# res = res_list["CV:hclust"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 17171 rows and 54 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'CV' method.
#>   Subgroups are detected by 'hclust' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 4.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk CV-hclust-collect-plots](figure_cola/CV-hclust-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk CV-hclust-select-partition-number](figure_cola/CV-hclust-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 0.537           0.731       0.878         0.2001 0.927   0.927
#> 3 3 0.586           0.683       0.814         1.3586 0.706   0.683
#> 4 4 0.839           0.882       0.920         0.4036 0.695   0.518
#> 5 5 0.793           0.806       0.866         0.0850 0.951   0.851
#> 6 6 0.863           0.781       0.881         0.0433 0.985   0.948
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 4
```


Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-CV-hclust-get-classes' ).tabs();
} );
</script>
<div id='tabs-CV-hclust-get-classes'>
<ul>
<li><a href='#tab-CV-hclust-get-classes-1'>k = 2</a></li>
<li><a href='#tab-CV-hclust-get-classes-2'>k = 3</a></li>
<li><a href='#tab-CV-hclust-get-classes-3'>k = 4</a></li>
<li><a href='#tab-CV-hclust-get-classes-4'>k = 5</a></li>
<li><a href='#tab-CV-hclust-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-CV-hclust-get-classes-1'>
<p><a id='tab-CV-hclust-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2
#&gt; SRR975551     1  0.2423      0.807 0.960 0.040
#&gt; SRR975552     1  0.2423      0.807 0.960 0.040
#&gt; SRR975554     1  0.2423      0.807 0.960 0.040
#&gt; SRR975553     1  0.0000      0.806 1.000 0.000
#&gt; SRR975555     1  0.2423      0.807 0.960 0.040
#&gt; SRR975556     1  0.0000      0.806 1.000 0.000
#&gt; SRR975557     2  0.9896      1.000 0.440 0.560
#&gt; SRR975558     1  0.2423      0.807 0.960 0.040
#&gt; SRR975559     1  0.2423      0.807 0.960 0.040
#&gt; SRR975560     1  0.0000      0.806 1.000 0.000
#&gt; SRR975561     1  0.0376      0.802 0.996 0.004
#&gt; SRR975562     1  0.2423      0.807 0.960 0.040
#&gt; SRR975563     1  0.0000      0.806 1.000 0.000
#&gt; SRR975564     1  0.2423      0.807 0.960 0.040
#&gt; SRR975565     1  0.2423      0.807 0.960 0.040
#&gt; SRR975566     1  0.2423      0.807 0.960 0.040
#&gt; SRR975567     1  0.2423      0.807 0.960 0.040
#&gt; SRR975568     1  0.2423      0.807 0.960 0.040
#&gt; SRR975569     1  0.0000      0.806 1.000 0.000
#&gt; SRR975570     1  0.0000      0.806 1.000 0.000
#&gt; SRR975571     1  0.0000      0.806 1.000 0.000
#&gt; SRR975572     1  0.0000      0.806 1.000 0.000
#&gt; SRR975573     1  0.0000      0.806 1.000 0.000
#&gt; SRR975574     1  0.0000      0.806 1.000 0.000
#&gt; SRR975575     1  0.0000      0.806 1.000 0.000
#&gt; SRR975576     1  0.0000      0.806 1.000 0.000
#&gt; SRR975577     1  0.0000      0.806 1.000 0.000
#&gt; SRR975578     1  0.0000      0.806 1.000 0.000
#&gt; SRR975579     2  0.9896      1.000 0.440 0.560
#&gt; SRR975580     1  0.0000      0.806 1.000 0.000
#&gt; SRR975581     1  0.0000      0.806 1.000 0.000
#&gt; SRR975582     1  0.0000      0.806 1.000 0.000
#&gt; SRR975583     1  0.0000      0.806 1.000 0.000
#&gt; SRR975584     1  0.0000      0.806 1.000 0.000
#&gt; SRR975585     1  0.0000      0.806 1.000 0.000
#&gt; SRR975586     1  0.0000      0.806 1.000 0.000
#&gt; SRR975587     1  0.9896      0.410 0.560 0.440
#&gt; SRR975588     1  0.0000      0.806 1.000 0.000
#&gt; SRR975589     1  0.9286      0.545 0.656 0.344
#&gt; SRR975590     1  0.9000      0.571 0.684 0.316
#&gt; SRR975591     1  0.9896      0.410 0.560 0.440
#&gt; SRR975592     1  0.9286      0.545 0.656 0.344
#&gt; SRR975593     1  0.9286      0.545 0.656 0.344
#&gt; SRR975594     1  0.9896      0.410 0.560 0.440
#&gt; SRR975595     1  0.9170      0.557 0.668 0.332
#&gt; SRR975597     1  0.9170      0.557 0.668 0.332
#&gt; SRR975596     1  0.2423      0.807 0.960 0.040
#&gt; SRR975598     1  0.9170      0.557 0.668 0.332
#&gt; SRR975599     1  0.5629      0.736 0.868 0.132
#&gt; SRR975600     1  0.9286      0.545 0.656 0.344
#&gt; SRR975601     1  0.9896      0.410 0.560 0.440
#&gt; SRR975602     1  0.2423      0.807 0.960 0.040
#&gt; SRR975603     1  0.9896      0.410 0.560 0.440
#&gt; SRR975604     1  0.9896      0.410 0.560 0.440
</code></pre>

<script>
$('#tab-CV-hclust-get-classes-1-a').parent().next().next().hide();
$('#tab-CV-hclust-get-classes-1-a').click(function(){
  $('#tab-CV-hclust-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-hclust-get-classes-2'>
<p><a id='tab-CV-hclust-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3
#&gt; SRR975551     2  0.6225      0.616 0.432 0.568 0.000
#&gt; SRR975552     2  0.6225      0.616 0.432 0.568 0.000
#&gt; SRR975554     2  0.6225      0.616 0.432 0.568 0.000
#&gt; SRR975553     2  0.0000      0.673 0.000 1.000 0.000
#&gt; SRR975555     2  0.6225      0.616 0.432 0.568 0.000
#&gt; SRR975556     2  0.0000      0.673 0.000 1.000 0.000
#&gt; SRR975557     1  0.6225      1.000 0.568 0.432 0.000
#&gt; SRR975558     2  0.5948      0.632 0.360 0.640 0.000
#&gt; SRR975559     2  0.6225      0.616 0.432 0.568 0.000
#&gt; SRR975560     2  0.1964      0.666 0.056 0.944 0.000
#&gt; SRR975561     2  0.0237      0.668 0.004 0.996 0.000
#&gt; SRR975562     2  0.6225      0.616 0.432 0.568 0.000
#&gt; SRR975563     2  0.0000      0.673 0.000 1.000 0.000
#&gt; SRR975564     2  0.6225      0.616 0.432 0.568 0.000
#&gt; SRR975565     2  0.6225      0.616 0.432 0.568 0.000
#&gt; SRR975566     2  0.6225      0.616 0.432 0.568 0.000
#&gt; SRR975567     2  0.5835      0.635 0.340 0.660 0.000
#&gt; SRR975568     2  0.6225      0.616 0.432 0.568 0.000
#&gt; SRR975569     2  0.0000      0.673 0.000 1.000 0.000
#&gt; SRR975570     2  0.0000      0.673 0.000 1.000 0.000
#&gt; SRR975571     2  0.0000      0.673 0.000 1.000 0.000
#&gt; SRR975572     2  0.0000      0.673 0.000 1.000 0.000
#&gt; SRR975573     2  0.0000      0.673 0.000 1.000 0.000
#&gt; SRR975574     2  0.0000      0.673 0.000 1.000 0.000
#&gt; SRR975575     2  0.0000      0.673 0.000 1.000 0.000
#&gt; SRR975576     2  0.0000      0.673 0.000 1.000 0.000
#&gt; SRR975577     2  0.0000      0.673 0.000 1.000 0.000
#&gt; SRR975578     2  0.0000      0.673 0.000 1.000 0.000
#&gt; SRR975579     1  0.6225      1.000 0.568 0.432 0.000
#&gt; SRR975580     2  0.1964      0.666 0.056 0.944 0.000
#&gt; SRR975581     2  0.0000      0.673 0.000 1.000 0.000
#&gt; SRR975582     2  0.0000      0.673 0.000 1.000 0.000
#&gt; SRR975583     2  0.0000      0.673 0.000 1.000 0.000
#&gt; SRR975584     2  0.0000      0.673 0.000 1.000 0.000
#&gt; SRR975585     2  0.0000      0.673 0.000 1.000 0.000
#&gt; SRR975586     2  0.0000      0.673 0.000 1.000 0.000
#&gt; SRR975587     3  0.0000      0.834 0.000 0.000 1.000
#&gt; SRR975588     2  0.0000      0.673 0.000 1.000 0.000
#&gt; SRR975589     3  0.6286      0.790 0.136 0.092 0.772
#&gt; SRR975590     2  0.8889      0.495 0.164 0.560 0.276
#&gt; SRR975591     3  0.1289      0.853 0.000 0.032 0.968
#&gt; SRR975592     3  0.6286      0.790 0.136 0.092 0.772
#&gt; SRR975593     3  0.6286      0.790 0.136 0.092 0.772
#&gt; SRR975594     3  0.0000      0.834 0.000 0.000 1.000
#&gt; SRR975595     2  0.8801      0.485 0.148 0.560 0.292
#&gt; SRR975597     2  0.8801      0.485 0.148 0.560 0.292
#&gt; SRR975596     2  0.6225      0.616 0.432 0.568 0.000
#&gt; SRR975598     2  0.8801      0.485 0.148 0.560 0.292
#&gt; SRR975599     2  0.8297      0.588 0.348 0.560 0.092
#&gt; SRR975600     3  0.6208      0.793 0.136 0.088 0.776
#&gt; SRR975601     3  0.0000      0.834 0.000 0.000 1.000
#&gt; SRR975602     2  0.6225      0.616 0.432 0.568 0.000
#&gt; SRR975603     3  0.1289      0.853 0.000 0.032 0.968
#&gt; SRR975604     3  0.1289      0.853 0.000 0.032 0.968
</code></pre>

<script>
$('#tab-CV-hclust-get-classes-2-a').parent().next().next().hide();
$('#tab-CV-hclust-get-classes-2-a').click(function(){
  $('#tab-CV-hclust-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-hclust-get-classes-3'>
<p><a id='tab-CV-hclust-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3    p4
#&gt; SRR975551     1  0.1022      0.895 0.968 0.032 0.000 0.000
#&gt; SRR975552     1  0.1022      0.895 0.968 0.032 0.000 0.000
#&gt; SRR975554     1  0.1022      0.895 0.968 0.032 0.000 0.000
#&gt; SRR975553     2  0.0000      0.990 0.000 1.000 0.000 0.000
#&gt; SRR975555     1  0.1022      0.895 0.968 0.032 0.000 0.000
#&gt; SRR975556     2  0.0000      0.990 0.000 1.000 0.000 0.000
#&gt; SRR975557     4  0.3610      1.000 0.000 0.200 0.000 0.800
#&gt; SRR975558     1  0.2469      0.813 0.892 0.108 0.000 0.000
#&gt; SRR975559     1  0.0707      0.877 0.980 0.020 0.000 0.000
#&gt; SRR975560     2  0.1557      0.912 0.056 0.944 0.000 0.000
#&gt; SRR975561     2  0.1211      0.944 0.000 0.960 0.000 0.040
#&gt; SRR975562     1  0.1474      0.885 0.948 0.052 0.000 0.000
#&gt; SRR975563     2  0.0000      0.990 0.000 1.000 0.000 0.000
#&gt; SRR975564     1  0.1022      0.895 0.968 0.032 0.000 0.000
#&gt; SRR975565     1  0.1022      0.895 0.968 0.032 0.000 0.000
#&gt; SRR975566     1  0.0707      0.877 0.980 0.020 0.000 0.000
#&gt; SRR975567     1  0.2760      0.789 0.872 0.128 0.000 0.000
#&gt; SRR975568     1  0.1022      0.895 0.968 0.032 0.000 0.000
#&gt; SRR975569     2  0.0000      0.990 0.000 1.000 0.000 0.000
#&gt; SRR975570     2  0.0000      0.990 0.000 1.000 0.000 0.000
#&gt; SRR975571     2  0.0000      0.990 0.000 1.000 0.000 0.000
#&gt; SRR975572     2  0.0000      0.990 0.000 1.000 0.000 0.000
#&gt; SRR975573     2  0.0000      0.990 0.000 1.000 0.000 0.000
#&gt; SRR975574     2  0.0000      0.990 0.000 1.000 0.000 0.000
#&gt; SRR975575     2  0.0000      0.990 0.000 1.000 0.000 0.000
#&gt; SRR975576     2  0.0000      0.990 0.000 1.000 0.000 0.000
#&gt; SRR975577     2  0.0000      0.990 0.000 1.000 0.000 0.000
#&gt; SRR975578     2  0.0000      0.990 0.000 1.000 0.000 0.000
#&gt; SRR975579     4  0.3610      1.000 0.000 0.200 0.000 0.800
#&gt; SRR975580     2  0.1557      0.912 0.056 0.944 0.000 0.000
#&gt; SRR975581     2  0.0000      0.990 0.000 1.000 0.000 0.000
#&gt; SRR975582     2  0.0000      0.990 0.000 1.000 0.000 0.000
#&gt; SRR975583     2  0.0000      0.990 0.000 1.000 0.000 0.000
#&gt; SRR975584     2  0.0000      0.990 0.000 1.000 0.000 0.000
#&gt; SRR975585     2  0.0000      0.990 0.000 1.000 0.000 0.000
#&gt; SRR975586     2  0.0000      0.990 0.000 1.000 0.000 0.000
#&gt; SRR975587     3  0.0000      0.758 0.000 0.000 1.000 0.000
#&gt; SRR975588     2  0.0000      0.990 0.000 1.000 0.000 0.000
#&gt; SRR975589     3  0.7058      0.649 0.228 0.000 0.572 0.200
#&gt; SRR975590     1  0.6367      0.697 0.692 0.032 0.076 0.200
#&gt; SRR975591     3  0.1022      0.767 0.032 0.000 0.968 0.000
#&gt; SRR975592     3  0.6790      0.666 0.228 0.000 0.604 0.168
#&gt; SRR975593     3  0.7058      0.649 0.228 0.000 0.572 0.200
#&gt; SRR975594     3  0.0000      0.758 0.000 0.000 1.000 0.000
#&gt; SRR975595     1  0.6609      0.678 0.676 0.032 0.092 0.200
#&gt; SRR975597     1  0.6609      0.678 0.676 0.032 0.092 0.200
#&gt; SRR975596     1  0.0707      0.877 0.980 0.020 0.000 0.000
#&gt; SRR975598     1  0.6609      0.678 0.676 0.032 0.092 0.200
#&gt; SRR975599     1  0.3215      0.842 0.876 0.032 0.092 0.000
#&gt; SRR975600     3  0.6761      0.669 0.224 0.000 0.608 0.168
#&gt; SRR975601     3  0.0000      0.758 0.000 0.000 1.000 0.000
#&gt; SRR975602     1  0.1022      0.895 0.968 0.032 0.000 0.000
#&gt; SRR975603     3  0.1022      0.767 0.032 0.000 0.968 0.000
#&gt; SRR975604     3  0.1022      0.767 0.032 0.000 0.968 0.000
</code></pre>

<script>
$('#tab-CV-hclust-get-classes-3-a').parent().next().next().hide();
$('#tab-CV-hclust-get-classes-3-a').click(function(){
  $('#tab-CV-hclust-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-hclust-get-classes-4'>
<p><a id='tab-CV-hclust-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3    p4    p5
#&gt; SRR975551     1  0.0609      0.705 0.980 0.000 0.000 0.000 0.020
#&gt; SRR975552     1  0.0609      0.705 0.980 0.000 0.000 0.000 0.020
#&gt; SRR975554     1  0.0290      0.711 0.992 0.000 0.000 0.000 0.008
#&gt; SRR975553     2  0.0000      0.988 0.000 1.000 0.000 0.000 0.000
#&gt; SRR975555     1  0.3395      0.586 0.764 0.000 0.000 0.000 0.236
#&gt; SRR975556     2  0.0000      0.988 0.000 1.000 0.000 0.000 0.000
#&gt; SRR975557     4  0.2377      1.000 0.000 0.128 0.000 0.872 0.000
#&gt; SRR975558     5  0.4280      0.726 0.140 0.088 0.000 0.000 0.772
#&gt; SRR975559     5  0.4101      0.794 0.372 0.000 0.000 0.000 0.628
#&gt; SRR975560     2  0.1484      0.927 0.008 0.944 0.000 0.000 0.048
#&gt; SRR975561     2  0.2074      0.865 0.000 0.896 0.000 0.104 0.000
#&gt; SRR975562     5  0.4201      0.756 0.408 0.000 0.000 0.000 0.592
#&gt; SRR975563     2  0.0000      0.988 0.000 1.000 0.000 0.000 0.000
#&gt; SRR975564     1  0.3983      0.406 0.660 0.000 0.000 0.000 0.340
#&gt; SRR975565     1  0.2516      0.678 0.860 0.000 0.000 0.000 0.140
#&gt; SRR975566     1  0.3305      0.351 0.776 0.000 0.000 0.000 0.224
#&gt; SRR975567     5  0.4617      0.715 0.148 0.108 0.000 0.000 0.744
#&gt; SRR975568     1  0.3395      0.586 0.764 0.000 0.000 0.000 0.236
#&gt; SRR975569     2  0.0000      0.988 0.000 1.000 0.000 0.000 0.000
#&gt; SRR975570     2  0.0000      0.988 0.000 1.000 0.000 0.000 0.000
#&gt; SRR975571     2  0.0000      0.988 0.000 1.000 0.000 0.000 0.000
#&gt; SRR975572     2  0.0000      0.988 0.000 1.000 0.000 0.000 0.000
#&gt; SRR975573     2  0.0000      0.988 0.000 1.000 0.000 0.000 0.000
#&gt; SRR975574     2  0.0000      0.988 0.000 1.000 0.000 0.000 0.000
#&gt; SRR975575     2  0.0000      0.988 0.000 1.000 0.000 0.000 0.000
#&gt; SRR975576     2  0.0000      0.988 0.000 1.000 0.000 0.000 0.000
#&gt; SRR975577     2  0.0000      0.988 0.000 1.000 0.000 0.000 0.000
#&gt; SRR975578     2  0.0000      0.988 0.000 1.000 0.000 0.000 0.000
#&gt; SRR975579     4  0.2377      1.000 0.000 0.128 0.000 0.872 0.000
#&gt; SRR975580     2  0.1484      0.927 0.008 0.944 0.000 0.000 0.048
#&gt; SRR975581     2  0.0000      0.988 0.000 1.000 0.000 0.000 0.000
#&gt; SRR975582     2  0.0000      0.988 0.000 1.000 0.000 0.000 0.000
#&gt; SRR975583     2  0.0000      0.988 0.000 1.000 0.000 0.000 0.000
#&gt; SRR975584     2  0.0000      0.988 0.000 1.000 0.000 0.000 0.000
#&gt; SRR975585     2  0.0000      0.988 0.000 1.000 0.000 0.000 0.000
#&gt; SRR975586     2  0.0000      0.988 0.000 1.000 0.000 0.000 0.000
#&gt; SRR975587     3  0.1732      0.682 0.000 0.000 0.920 0.000 0.080
#&gt; SRR975588     2  0.0000      0.988 0.000 1.000 0.000 0.000 0.000
#&gt; SRR975589     3  0.7586      0.576 0.160 0.000 0.512 0.128 0.200
#&gt; SRR975590     1  0.5322      0.645 0.708 0.000 0.016 0.128 0.148
#&gt; SRR975591     3  0.0880      0.713 0.000 0.000 0.968 0.000 0.032
#&gt; SRR975592     3  0.7325      0.601 0.160 0.000 0.544 0.108 0.188
#&gt; SRR975593     3  0.7586      0.576 0.160 0.000 0.512 0.128 0.200
#&gt; SRR975594     3  0.1732      0.682 0.000 0.000 0.920 0.000 0.080
#&gt; SRR975595     1  0.5620      0.641 0.696 0.000 0.032 0.128 0.144
#&gt; SRR975597     1  0.5620      0.641 0.696 0.000 0.032 0.128 0.144
#&gt; SRR975596     5  0.4114      0.792 0.376 0.000 0.000 0.000 0.624
#&gt; SRR975598     1  0.5620      0.641 0.696 0.000 0.032 0.128 0.144
#&gt; SRR975599     1  0.2473      0.702 0.896 0.000 0.032 0.000 0.072
#&gt; SRR975600     3  0.7295      0.605 0.156 0.000 0.548 0.108 0.188
#&gt; SRR975601     3  0.1732      0.682 0.000 0.000 0.920 0.000 0.080
#&gt; SRR975602     1  0.0000      0.711 1.000 0.000 0.000 0.000 0.000
#&gt; SRR975603     3  0.0880      0.713 0.000 0.000 0.968 0.000 0.032
#&gt; SRR975604     3  0.0880      0.713 0.000 0.000 0.968 0.000 0.032
</code></pre>

<script>
$('#tab-CV-hclust-get-classes-4-a').parent().next().next().hide();
$('#tab-CV-hclust-get-classes-4-a').click(function(){
  $('#tab-CV-hclust-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-hclust-get-classes-5'>
<p><a id='tab-CV-hclust-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3    p4    p5    p6
#&gt; SRR975551     1  0.0790      0.644 0.968 0.000 0.000 0.032 0.000 0.000
#&gt; SRR975552     1  0.0790      0.644 0.968 0.000 0.000 0.032 0.000 0.000
#&gt; SRR975554     1  0.1528      0.651 0.936 0.000 0.048 0.016 0.000 0.000
#&gt; SRR975553     2  0.0000      0.981 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR975555     1  0.3515      0.499 0.676 0.000 0.000 0.324 0.000 0.000
#&gt; SRR975556     2  0.0000      0.981 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR975557     5  0.0000      1.000 0.000 0.000 0.000 0.000 1.000 0.000
#&gt; SRR975558     4  0.0632      0.714 0.000 0.024 0.000 0.976 0.000 0.000
#&gt; SRR975559     4  0.3126      0.816 0.248 0.000 0.000 0.752 0.000 0.000
#&gt; SRR975560     2  0.1806      0.900 0.004 0.908 0.000 0.088 0.000 0.000
#&gt; SRR975561     2  0.2969      0.726 0.000 0.776 0.000 0.000 0.224 0.000
#&gt; SRR975562     4  0.3330      0.784 0.284 0.000 0.000 0.716 0.000 0.000
#&gt; SRR975563     2  0.0000      0.981 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR975564     1  0.3810      0.370 0.572 0.000 0.000 0.428 0.000 0.000
#&gt; SRR975565     1  0.2631      0.622 0.820 0.000 0.000 0.180 0.000 0.000
#&gt; SRR975566     1  0.3076      0.334 0.760 0.000 0.000 0.240 0.000 0.000
#&gt; SRR975567     4  0.1434      0.718 0.012 0.048 0.000 0.940 0.000 0.000
#&gt; SRR975568     1  0.3515      0.499 0.676 0.000 0.000 0.324 0.000 0.000
#&gt; SRR975569     2  0.0000      0.981 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR975570     2  0.0000      0.981 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR975571     2  0.0000      0.981 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR975572     2  0.0000      0.981 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR975573     2  0.0000      0.981 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR975574     2  0.0000      0.981 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR975575     2  0.0000      0.981 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR975576     2  0.0000      0.981 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR975577     2  0.0000      0.981 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR975578     2  0.0000      0.981 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR975579     5  0.0000      1.000 0.000 0.000 0.000 0.000 1.000 0.000
#&gt; SRR975580     2  0.1753      0.904 0.004 0.912 0.000 0.084 0.000 0.000
#&gt; SRR975581     2  0.0000      0.981 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR975582     2  0.0000      0.981 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR975583     2  0.0000      0.981 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR975584     2  0.0000      0.981 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR975585     2  0.0000      0.981 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR975586     2  0.0000      0.981 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR975587     6  0.0000      1.000 0.000 0.000 0.000 0.000 0.000 1.000
#&gt; SRR975588     2  0.0000      0.981 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR975589     3  0.0000      0.665 0.000 0.000 1.000 0.000 0.000 0.000
#&gt; SRR975590     1  0.3883      0.590 0.656 0.000 0.332 0.012 0.000 0.000
#&gt; SRR975591     3  0.3867      0.295 0.000 0.000 0.512 0.000 0.000 0.488
#&gt; SRR975592     3  0.0790      0.675 0.000 0.000 0.968 0.000 0.000 0.032
#&gt; SRR975593     3  0.0000      0.665 0.000 0.000 1.000 0.000 0.000 0.000
#&gt; SRR975594     6  0.0000      1.000 0.000 0.000 0.000 0.000 0.000 1.000
#&gt; SRR975595     1  0.3843      0.507 0.548 0.000 0.452 0.000 0.000 0.000
#&gt; SRR975597     1  0.3843      0.507 0.548 0.000 0.452 0.000 0.000 0.000
#&gt; SRR975596     4  0.3151      0.815 0.252 0.000 0.000 0.748 0.000 0.000
#&gt; SRR975598     1  0.3843      0.507 0.548 0.000 0.452 0.000 0.000 0.000
#&gt; SRR975599     1  0.3151      0.613 0.748 0.000 0.252 0.000 0.000 0.000
#&gt; SRR975600     3  0.0865      0.674 0.000 0.000 0.964 0.000 0.000 0.036
#&gt; SRR975601     6  0.0000      1.000 0.000 0.000 0.000 0.000 0.000 1.000
#&gt; SRR975602     1  0.0363      0.648 0.988 0.000 0.000 0.012 0.000 0.000
#&gt; SRR975603     3  0.3867      0.295 0.000 0.000 0.512 0.000 0.000 0.488
#&gt; SRR975604     3  0.3868      0.278 0.000 0.000 0.504 0.000 0.000 0.496
</code></pre>

<script>
$('#tab-CV-hclust-get-classes-5-a').parent().next().next().hide();
$('#tab-CV-hclust-get-classes-5-a').click(function(){
  $('#tab-CV-hclust-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-CV-hclust-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-CV-hclust-consensus-heatmap'>
<ul>
<li><a href='#tab-CV-hclust-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-CV-hclust-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-CV-hclust-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-CV-hclust-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-CV-hclust-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-CV-hclust-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-consensus-heatmap-1-1.png" alt="plot of chunk tab-CV-hclust-consensus-heatmap-1"/></p>

</div>
<div id='tab-CV-hclust-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-consensus-heatmap-2-1.png" alt="plot of chunk tab-CV-hclust-consensus-heatmap-2"/></p>

</div>
<div id='tab-CV-hclust-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-consensus-heatmap-3-1.png" alt="plot of chunk tab-CV-hclust-consensus-heatmap-3"/></p>

</div>
<div id='tab-CV-hclust-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-consensus-heatmap-4-1.png" alt="plot of chunk tab-CV-hclust-consensus-heatmap-4"/></p>

</div>
<div id='tab-CV-hclust-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-consensus-heatmap-5-1.png" alt="plot of chunk tab-CV-hclust-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-CV-hclust-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-CV-hclust-membership-heatmap'>
<ul>
<li><a href='#tab-CV-hclust-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-CV-hclust-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-CV-hclust-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-CV-hclust-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-CV-hclust-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-CV-hclust-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-membership-heatmap-1-1.png" alt="plot of chunk tab-CV-hclust-membership-heatmap-1"/></p>

</div>
<div id='tab-CV-hclust-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-membership-heatmap-2-1.png" alt="plot of chunk tab-CV-hclust-membership-heatmap-2"/></p>

</div>
<div id='tab-CV-hclust-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-membership-heatmap-3-1.png" alt="plot of chunk tab-CV-hclust-membership-heatmap-3"/></p>

</div>
<div id='tab-CV-hclust-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-membership-heatmap-4-1.png" alt="plot of chunk tab-CV-hclust-membership-heatmap-4"/></p>

</div>
<div id='tab-CV-hclust-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-membership-heatmap-5-1.png" alt="plot of chunk tab-CV-hclust-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-CV-hclust-get-signatures' ).tabs();
} );
</script>
<div id='tabs-CV-hclust-get-signatures'>
<ul>
<li><a href='#tab-CV-hclust-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-CV-hclust-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-CV-hclust-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-CV-hclust-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-CV-hclust-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-CV-hclust-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-get-signatures-1-1.png" alt="plot of chunk tab-CV-hclust-get-signatures-1"/></p>

</div>
<div id='tab-CV-hclust-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-get-signatures-2-1.png" alt="plot of chunk tab-CV-hclust-get-signatures-2"/></p>

</div>
<div id='tab-CV-hclust-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-get-signatures-3-1.png" alt="plot of chunk tab-CV-hclust-get-signatures-3"/></p>

</div>
<div id='tab-CV-hclust-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-get-signatures-4-1.png" alt="plot of chunk tab-CV-hclust-get-signatures-4"/></p>

</div>
<div id='tab-CV-hclust-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-get-signatures-5-1.png" alt="plot of chunk tab-CV-hclust-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-CV-hclust-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-CV-hclust-get-signatures-no-scale'>
<ul>
<li><a href='#tab-CV-hclust-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-CV-hclust-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-CV-hclust-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-CV-hclust-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-CV-hclust-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-CV-hclust-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-CV-hclust-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-CV-hclust-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-CV-hclust-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-CV-hclust-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-CV-hclust-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-CV-hclust-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-CV-hclust-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-CV-hclust-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-CV-hclust-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk CV-hclust-signature_compare](figure_cola/CV-hclust-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-CV-hclust-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-CV-hclust-dimension-reduction'>
<ul>
<li><a href='#tab-CV-hclust-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-CV-hclust-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-CV-hclust-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-CV-hclust-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-CV-hclust-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-CV-hclust-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-dimension-reduction-1-1.png" alt="plot of chunk tab-CV-hclust-dimension-reduction-1"/></p>

</div>
<div id='tab-CV-hclust-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-dimension-reduction-2-1.png" alt="plot of chunk tab-CV-hclust-dimension-reduction-2"/></p>

</div>
<div id='tab-CV-hclust-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-dimension-reduction-3-1.png" alt="plot of chunk tab-CV-hclust-dimension-reduction-3"/></p>

</div>
<div id='tab-CV-hclust-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-dimension-reduction-4-1.png" alt="plot of chunk tab-CV-hclust-dimension-reduction-4"/></p>

</div>
<div id='tab-CV-hclust-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-dimension-reduction-5-1.png" alt="plot of chunk tab-CV-hclust-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk CV-hclust-collect-classes](figure_cola/CV-hclust-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### CV:kmeans






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["CV", "kmeans"]
# you can also extract it by
# res = res_list["CV:kmeans"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 17171 rows and 54 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'CV' method.
#>   Subgroups are detected by 'kmeans' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 2.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk CV-kmeans-collect-plots](figure_cola/CV-kmeans-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk CV-kmeans-select-partition-number](figure_cola/CV-kmeans-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 0.633           0.936       0.956         0.4908 0.491   0.491
#> 3 3 0.781           0.860       0.890         0.3090 0.772   0.568
#> 4 4 0.761           0.729       0.851         0.1010 0.901   0.734
#> 5 5 0.725           0.728       0.771         0.0688 0.957   0.862
#> 6 6 0.722           0.437       0.659         0.0479 0.973   0.901
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 2
```


Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-CV-kmeans-get-classes' ).tabs();
} );
</script>
<div id='tabs-CV-kmeans-get-classes'>
<ul>
<li><a href='#tab-CV-kmeans-get-classes-1'>k = 2</a></li>
<li><a href='#tab-CV-kmeans-get-classes-2'>k = 3</a></li>
<li><a href='#tab-CV-kmeans-get-classes-3'>k = 4</a></li>
<li><a href='#tab-CV-kmeans-get-classes-4'>k = 5</a></li>
<li><a href='#tab-CV-kmeans-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-CV-kmeans-get-classes-1'>
<p><a id='tab-CV-kmeans-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2
#&gt; SRR975551     1   0.482      0.928 0.896 0.104
#&gt; SRR975552     1   0.781      0.766 0.768 0.232
#&gt; SRR975554     1   0.482      0.928 0.896 0.104
#&gt; SRR975553     2   0.118      0.976 0.016 0.984
#&gt; SRR975555     1   0.482      0.928 0.896 0.104
#&gt; SRR975556     2   0.118      0.976 0.016 0.984
#&gt; SRR975557     2   0.000      0.963 0.000 1.000
#&gt; SRR975558     2   0.961      0.329 0.384 0.616
#&gt; SRR975559     1   0.482      0.928 0.896 0.104
#&gt; SRR975560     2   0.118      0.976 0.016 0.984
#&gt; SRR975561     2   0.000      0.963 0.000 1.000
#&gt; SRR975562     1   0.482      0.928 0.896 0.104
#&gt; SRR975563     2   0.118      0.976 0.016 0.984
#&gt; SRR975564     1   0.482      0.928 0.896 0.104
#&gt; SRR975565     1   0.482      0.928 0.896 0.104
#&gt; SRR975566     1   0.482      0.928 0.896 0.104
#&gt; SRR975567     2   0.625      0.810 0.156 0.844
#&gt; SRR975568     1   0.482      0.928 0.896 0.104
#&gt; SRR975569     2   0.118      0.976 0.016 0.984
#&gt; SRR975570     2   0.118      0.976 0.016 0.984
#&gt; SRR975571     2   0.118      0.976 0.016 0.984
#&gt; SRR975572     2   0.118      0.976 0.016 0.984
#&gt; SRR975573     2   0.118      0.976 0.016 0.984
#&gt; SRR975574     2   0.118      0.976 0.016 0.984
#&gt; SRR975575     2   0.118      0.976 0.016 0.984
#&gt; SRR975576     2   0.118      0.976 0.016 0.984
#&gt; SRR975577     2   0.118      0.976 0.016 0.984
#&gt; SRR975578     2   0.118      0.976 0.016 0.984
#&gt; SRR975579     2   0.000      0.963 0.000 1.000
#&gt; SRR975580     2   0.118      0.976 0.016 0.984
#&gt; SRR975581     2   0.118      0.976 0.016 0.984
#&gt; SRR975582     2   0.118      0.976 0.016 0.984
#&gt; SRR975583     2   0.118      0.976 0.016 0.984
#&gt; SRR975584     2   0.118      0.976 0.016 0.984
#&gt; SRR975585     2   0.118      0.976 0.016 0.984
#&gt; SRR975586     2   0.118      0.976 0.016 0.984
#&gt; SRR975587     1   0.000      0.938 1.000 0.000
#&gt; SRR975588     2   0.118      0.976 0.016 0.984
#&gt; SRR975589     1   0.000      0.938 1.000 0.000
#&gt; SRR975590     1   0.000      0.938 1.000 0.000
#&gt; SRR975591     1   0.000      0.938 1.000 0.000
#&gt; SRR975592     1   0.000      0.938 1.000 0.000
#&gt; SRR975593     1   0.000      0.938 1.000 0.000
#&gt; SRR975594     1   0.000      0.938 1.000 0.000
#&gt; SRR975595     1   0.000      0.938 1.000 0.000
#&gt; SRR975597     1   0.000      0.938 1.000 0.000
#&gt; SRR975596     1   0.482      0.928 0.896 0.104
#&gt; SRR975598     1   0.000      0.938 1.000 0.000
#&gt; SRR975599     1   0.482      0.928 0.896 0.104
#&gt; SRR975600     1   0.000      0.938 1.000 0.000
#&gt; SRR975601     1   0.000      0.938 1.000 0.000
#&gt; SRR975602     1   0.482      0.928 0.896 0.104
#&gt; SRR975603     1   0.000      0.938 1.000 0.000
#&gt; SRR975604     1   0.000      0.938 1.000 0.000
</code></pre>

<script>
$('#tab-CV-kmeans-get-classes-1-a').parent().next().next().hide();
$('#tab-CV-kmeans-get-classes-1-a').click(function(){
  $('#tab-CV-kmeans-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-kmeans-get-classes-2'>
<p><a id='tab-CV-kmeans-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3
#&gt; SRR975551     1  0.5201     0.8231 0.760 0.004 0.236
#&gt; SRR975552     1  0.4575     0.8028 0.812 0.004 0.184
#&gt; SRR975554     1  0.5201     0.8231 0.760 0.004 0.236
#&gt; SRR975553     2  0.0000     0.9824 0.000 1.000 0.000
#&gt; SRR975555     1  0.5201     0.8231 0.760 0.004 0.236
#&gt; SRR975556     2  0.0000     0.9824 0.000 1.000 0.000
#&gt; SRR975557     1  0.6215    -0.0177 0.572 0.428 0.000
#&gt; SRR975558     1  0.2918     0.6919 0.924 0.044 0.032
#&gt; SRR975559     1  0.1525     0.7112 0.964 0.004 0.032
#&gt; SRR975560     1  0.5216     0.4752 0.740 0.260 0.000
#&gt; SRR975561     2  0.4399     0.8082 0.188 0.812 0.000
#&gt; SRR975562     1  0.5201     0.8231 0.760 0.004 0.236
#&gt; SRR975563     2  0.0000     0.9824 0.000 1.000 0.000
#&gt; SRR975564     1  0.5201     0.8231 0.760 0.004 0.236
#&gt; SRR975565     1  0.5201     0.8231 0.760 0.004 0.236
#&gt; SRR975566     1  0.5201     0.8231 0.760 0.004 0.236
#&gt; SRR975567     1  0.2918     0.6919 0.924 0.044 0.032
#&gt; SRR975568     1  0.5201     0.8231 0.760 0.004 0.236
#&gt; SRR975569     2  0.0000     0.9824 0.000 1.000 0.000
#&gt; SRR975570     2  0.0000     0.9824 0.000 1.000 0.000
#&gt; SRR975571     2  0.0000     0.9824 0.000 1.000 0.000
#&gt; SRR975572     2  0.0000     0.9824 0.000 1.000 0.000
#&gt; SRR975573     2  0.0000     0.9824 0.000 1.000 0.000
#&gt; SRR975574     2  0.0000     0.9824 0.000 1.000 0.000
#&gt; SRR975575     2  0.0000     0.9824 0.000 1.000 0.000
#&gt; SRR975576     2  0.0000     0.9824 0.000 1.000 0.000
#&gt; SRR975577     2  0.0000     0.9824 0.000 1.000 0.000
#&gt; SRR975578     2  0.0000     0.9824 0.000 1.000 0.000
#&gt; SRR975579     2  0.4974     0.7604 0.236 0.764 0.000
#&gt; SRR975580     2  0.0000     0.9824 0.000 1.000 0.000
#&gt; SRR975581     2  0.0000     0.9824 0.000 1.000 0.000
#&gt; SRR975582     2  0.0000     0.9824 0.000 1.000 0.000
#&gt; SRR975583     2  0.0000     0.9824 0.000 1.000 0.000
#&gt; SRR975584     2  0.0000     0.9824 0.000 1.000 0.000
#&gt; SRR975585     2  0.0000     0.9824 0.000 1.000 0.000
#&gt; SRR975586     2  0.0000     0.9824 0.000 1.000 0.000
#&gt; SRR975587     3  0.0237     0.8998 0.004 0.000 0.996
#&gt; SRR975588     2  0.0000     0.9824 0.000 1.000 0.000
#&gt; SRR975589     3  0.1753     0.8888 0.048 0.000 0.952
#&gt; SRR975590     3  0.4346     0.7792 0.184 0.000 0.816
#&gt; SRR975591     3  0.0000     0.8997 0.000 0.000 1.000
#&gt; SRR975592     3  0.1031     0.8968 0.024 0.000 0.976
#&gt; SRR975593     3  0.1753     0.8888 0.048 0.000 0.952
#&gt; SRR975594     3  0.0237     0.8998 0.004 0.000 0.996
#&gt; SRR975595     3  0.4750     0.7400 0.216 0.000 0.784
#&gt; SRR975597     3  0.4750     0.7400 0.216 0.000 0.784
#&gt; SRR975596     1  0.4784     0.8108 0.796 0.004 0.200
#&gt; SRR975598     3  0.5465     0.6004 0.288 0.000 0.712
#&gt; SRR975599     1  0.5201     0.8231 0.760 0.004 0.236
#&gt; SRR975600     3  0.0000     0.8997 0.000 0.000 1.000
#&gt; SRR975601     3  0.0237     0.8998 0.004 0.000 0.996
#&gt; SRR975602     1  0.5201     0.8231 0.760 0.004 0.236
#&gt; SRR975603     3  0.0000     0.8997 0.000 0.000 1.000
#&gt; SRR975604     3  0.0000     0.8997 0.000 0.000 1.000
</code></pre>

<script>
$('#tab-CV-kmeans-get-classes-2-a').parent().next().next().hide();
$('#tab-CV-kmeans-get-classes-2-a').click(function(){
  $('#tab-CV-kmeans-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-kmeans-get-classes-3'>
<p><a id='tab-CV-kmeans-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3    p4
#&gt; SRR975551     1  0.0188      0.769 0.996 0.000 0.000 0.004
#&gt; SRR975552     1  0.0592      0.766 0.984 0.000 0.000 0.016
#&gt; SRR975554     1  0.0188      0.769 0.996 0.000 0.000 0.004
#&gt; SRR975553     2  0.3071      0.901 0.000 0.888 0.044 0.068
#&gt; SRR975555     1  0.0188      0.769 0.996 0.000 0.000 0.004
#&gt; SRR975556     2  0.0336      0.917 0.000 0.992 0.000 0.008
#&gt; SRR975557     4  0.5977      0.360 0.220 0.080 0.008 0.692
#&gt; SRR975558     1  0.5093      0.423 0.640 0.012 0.000 0.348
#&gt; SRR975559     1  0.3801      0.606 0.780 0.000 0.000 0.220
#&gt; SRR975560     1  0.5898      0.332 0.604 0.048 0.000 0.348
#&gt; SRR975561     4  0.4999      0.368 0.000 0.492 0.000 0.508
#&gt; SRR975562     1  0.0336      0.768 0.992 0.000 0.000 0.008
#&gt; SRR975563     2  0.0000      0.923 0.000 1.000 0.000 0.000
#&gt; SRR975564     1  0.0707      0.768 0.980 0.000 0.000 0.020
#&gt; SRR975565     1  0.0188      0.769 0.996 0.000 0.000 0.004
#&gt; SRR975566     1  0.0336      0.768 0.992 0.000 0.000 0.008
#&gt; SRR975567     1  0.5110      0.413 0.636 0.012 0.000 0.352
#&gt; SRR975568     1  0.0707      0.768 0.980 0.000 0.000 0.020
#&gt; SRR975569     2  0.0000      0.923 0.000 1.000 0.000 0.000
#&gt; SRR975570     2  0.0000      0.923 0.000 1.000 0.000 0.000
#&gt; SRR975571     2  0.3071      0.901 0.000 0.888 0.044 0.068
#&gt; SRR975572     2  0.0000      0.923 0.000 1.000 0.000 0.000
#&gt; SRR975573     2  0.3071      0.901 0.000 0.888 0.044 0.068
#&gt; SRR975574     2  0.3071      0.901 0.000 0.888 0.044 0.068
#&gt; SRR975575     2  0.0000      0.923 0.000 1.000 0.000 0.000
#&gt; SRR975576     2  0.0000      0.923 0.000 1.000 0.000 0.000
#&gt; SRR975577     2  0.3071      0.901 0.000 0.888 0.044 0.068
#&gt; SRR975578     2  0.3071      0.901 0.000 0.888 0.044 0.068
#&gt; SRR975579     4  0.4836      0.635 0.000 0.320 0.008 0.672
#&gt; SRR975580     2  0.3037      0.900 0.000 0.888 0.036 0.076
#&gt; SRR975581     2  0.0000      0.923 0.000 1.000 0.000 0.000
#&gt; SRR975582     2  0.3071      0.901 0.000 0.888 0.044 0.068
#&gt; SRR975583     2  0.0000      0.923 0.000 1.000 0.000 0.000
#&gt; SRR975584     2  0.3071      0.901 0.000 0.888 0.044 0.068
#&gt; SRR975585     2  0.0000      0.923 0.000 1.000 0.000 0.000
#&gt; SRR975586     2  0.2149      0.810 0.000 0.912 0.000 0.088
#&gt; SRR975587     3  0.2759      0.863 0.052 0.000 0.904 0.044
#&gt; SRR975588     2  0.0000      0.923 0.000 1.000 0.000 0.000
#&gt; SRR975589     3  0.5376      0.813 0.088 0.000 0.736 0.176
#&gt; SRR975590     3  0.7762      0.224 0.380 0.000 0.384 0.236
#&gt; SRR975591     3  0.1474      0.864 0.052 0.000 0.948 0.000
#&gt; SRR975592     3  0.5076      0.823 0.072 0.000 0.756 0.172
#&gt; SRR975593     3  0.5334      0.814 0.088 0.000 0.740 0.172
#&gt; SRR975594     3  0.2759      0.863 0.052 0.000 0.904 0.044
#&gt; SRR975595     1  0.7745     -0.237 0.412 0.000 0.352 0.236
#&gt; SRR975597     1  0.7745     -0.237 0.412 0.000 0.352 0.236
#&gt; SRR975596     1  0.2281      0.723 0.904 0.000 0.000 0.096
#&gt; SRR975598     1  0.7679     -0.137 0.448 0.000 0.316 0.236
#&gt; SRR975599     1  0.2647      0.713 0.880 0.000 0.000 0.120
#&gt; SRR975600     3  0.3312      0.859 0.052 0.000 0.876 0.072
#&gt; SRR975601     3  0.2759      0.863 0.052 0.000 0.904 0.044
#&gt; SRR975602     1  0.2149      0.734 0.912 0.000 0.000 0.088
#&gt; SRR975603     3  0.1474      0.864 0.052 0.000 0.948 0.000
#&gt; SRR975604     3  0.1474      0.864 0.052 0.000 0.948 0.000
</code></pre>

<script>
$('#tab-CV-kmeans-get-classes-3-a').parent().next().next().hide();
$('#tab-CV-kmeans-get-classes-3-a').click(function(){
  $('#tab-CV-kmeans-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-kmeans-get-classes-4'>
<p><a id='tab-CV-kmeans-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3    p4    p5
#&gt; SRR975551     1  0.0162      0.804 0.996 0.000 0.000 0.004 0.000
#&gt; SRR975552     1  0.0898      0.808 0.972 0.000 0.000 0.008 0.020
#&gt; SRR975554     1  0.0693      0.806 0.980 0.000 0.000 0.012 0.008
#&gt; SRR975553     2  0.3999      0.711 0.000 0.656 0.000 0.000 0.344
#&gt; SRR975555     1  0.2233      0.789 0.904 0.000 0.000 0.016 0.080
#&gt; SRR975556     2  0.2280      0.688 0.000 0.880 0.000 0.000 0.120
#&gt; SRR975557     4  0.2584      0.653 0.052 0.032 0.008 0.904 0.004
#&gt; SRR975558     1  0.6120      0.568 0.580 0.004 0.000 0.172 0.244
#&gt; SRR975559     1  0.3810      0.755 0.812 0.000 0.000 0.088 0.100
#&gt; SRR975560     1  0.6841      0.494 0.552 0.044 0.000 0.156 0.248
#&gt; SRR975561     4  0.5889      0.395 0.000 0.392 0.000 0.504 0.104
#&gt; SRR975562     1  0.1768      0.804 0.924 0.000 0.000 0.004 0.072
#&gt; SRR975563     2  0.0000      0.779 0.000 1.000 0.000 0.000 0.000
#&gt; SRR975564     1  0.2208      0.804 0.908 0.000 0.000 0.020 0.072
#&gt; SRR975565     1  0.1018      0.807 0.968 0.000 0.000 0.016 0.016
#&gt; SRR975566     1  0.1638      0.804 0.932 0.000 0.000 0.004 0.064
#&gt; SRR975567     1  0.6326      0.507 0.552 0.004 0.000 0.216 0.228
#&gt; SRR975568     1  0.1943      0.801 0.924 0.000 0.000 0.020 0.056
#&gt; SRR975569     2  0.0162      0.779 0.000 0.996 0.000 0.000 0.004
#&gt; SRR975570     2  0.0162      0.779 0.000 0.996 0.000 0.000 0.004
#&gt; SRR975571     2  0.3999      0.711 0.000 0.656 0.000 0.000 0.344
#&gt; SRR975572     2  0.0000      0.779 0.000 1.000 0.000 0.000 0.000
#&gt; SRR975573     2  0.3999      0.711 0.000 0.656 0.000 0.000 0.344
#&gt; SRR975574     2  0.4015      0.710 0.000 0.652 0.000 0.000 0.348
#&gt; SRR975575     2  0.0000      0.779 0.000 1.000 0.000 0.000 0.000
#&gt; SRR975576     2  0.0000      0.779 0.000 1.000 0.000 0.000 0.000
#&gt; SRR975577     2  0.4015      0.710 0.000 0.652 0.000 0.000 0.348
#&gt; SRR975578     2  0.4015      0.710 0.000 0.652 0.000 0.000 0.348
#&gt; SRR975579     4  0.2179      0.709 0.000 0.100 0.000 0.896 0.004
#&gt; SRR975580     2  0.4150      0.642 0.000 0.612 0.000 0.000 0.388
#&gt; SRR975581     2  0.0000      0.779 0.000 1.000 0.000 0.000 0.000
#&gt; SRR975582     2  0.4015      0.710 0.000 0.652 0.000 0.000 0.348
#&gt; SRR975583     2  0.0000      0.779 0.000 1.000 0.000 0.000 0.000
#&gt; SRR975584     2  0.4015      0.710 0.000 0.652 0.000 0.000 0.348
#&gt; SRR975585     2  0.0000      0.779 0.000 1.000 0.000 0.000 0.000
#&gt; SRR975586     2  0.3184      0.614 0.000 0.852 0.000 0.048 0.100
#&gt; SRR975587     3  0.2769      0.749 0.000 0.000 0.876 0.032 0.092
#&gt; SRR975588     2  0.0162      0.779 0.000 0.996 0.000 0.000 0.004
#&gt; SRR975589     3  0.5329      0.502 0.036 0.000 0.684 0.044 0.236
#&gt; SRR975590     5  0.7547      0.917 0.268 0.000 0.324 0.040 0.368
#&gt; SRR975591     3  0.0000      0.784 0.000 0.000 1.000 0.000 0.000
#&gt; SRR975592     3  0.4775      0.575 0.028 0.000 0.740 0.040 0.192
#&gt; SRR975593     3  0.5275      0.509 0.036 0.000 0.692 0.044 0.228
#&gt; SRR975594     3  0.2769      0.749 0.000 0.000 0.876 0.032 0.092
#&gt; SRR975595     5  0.7540      0.939 0.268 0.000 0.316 0.040 0.376
#&gt; SRR975597     5  0.7540      0.939 0.268 0.000 0.316 0.040 0.376
#&gt; SRR975596     1  0.3255      0.774 0.848 0.000 0.000 0.052 0.100
#&gt; SRR975598     5  0.7534      0.857 0.328 0.000 0.260 0.040 0.372
#&gt; SRR975599     1  0.3438      0.613 0.808 0.000 0.000 0.020 0.172
#&gt; SRR975600     3  0.2409      0.749 0.000 0.000 0.900 0.032 0.068
#&gt; SRR975601     3  0.2769      0.749 0.000 0.000 0.876 0.032 0.092
#&gt; SRR975602     1  0.3399      0.620 0.812 0.000 0.000 0.020 0.168
#&gt; SRR975603     3  0.0000      0.784 0.000 0.000 1.000 0.000 0.000
#&gt; SRR975604     3  0.0000      0.784 0.000 0.000 1.000 0.000 0.000
</code></pre>

<script>
$('#tab-CV-kmeans-get-classes-4-a').parent().next().next().hide();
$('#tab-CV-kmeans-get-classes-4-a').click(function(){
  $('#tab-CV-kmeans-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-kmeans-get-classes-5'>
<p><a id='tab-CV-kmeans-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3    p4    p5    p6
#&gt; SRR975551     1  0.1141    0.71619 0.948 0.000 0.000 0.000 0.052 0.000
#&gt; SRR975552     1  0.2537    0.72346 0.872 0.000 0.000 0.000 0.096 0.032
#&gt; SRR975554     1  0.1890    0.71520 0.916 0.000 0.000 0.000 0.060 0.024
#&gt; SRR975553     2  0.0146    0.41600 0.000 0.996 0.000 0.000 0.000 0.004
#&gt; SRR975555     1  0.4261    0.68518 0.732 0.000 0.000 0.000 0.156 0.112
#&gt; SRR975556     6  0.4334    0.67235 0.000 0.408 0.000 0.000 0.024 0.568
#&gt; SRR975557     4  0.0508    0.64551 0.012 0.000 0.000 0.984 0.000 0.004
#&gt; SRR975558     1  0.6375    0.45314 0.480 0.000 0.000 0.028 0.252 0.240
#&gt; SRR975559     1  0.3956    0.68100 0.796 0.000 0.000 0.028 0.080 0.096
#&gt; SRR975560     1  0.7152    0.36362 0.424 0.032 0.000 0.036 0.208 0.300
#&gt; SRR975561     4  0.7053   -0.00791 0.000 0.164 0.000 0.404 0.104 0.328
#&gt; SRR975562     1  0.3286    0.69940 0.832 0.000 0.000 0.012 0.044 0.112
#&gt; SRR975563     2  0.3995   -0.19010 0.000 0.516 0.000 0.000 0.004 0.480
#&gt; SRR975564     1  0.3878    0.70316 0.772 0.000 0.000 0.000 0.112 0.116
#&gt; SRR975565     1  0.2586    0.72063 0.868 0.000 0.000 0.000 0.100 0.032
#&gt; SRR975566     1  0.1767    0.71579 0.932 0.000 0.000 0.012 0.036 0.020
#&gt; SRR975567     1  0.6990    0.39265 0.452 0.000 0.000 0.092 0.232 0.224
#&gt; SRR975568     1  0.3958    0.70021 0.764 0.000 0.000 0.000 0.128 0.108
#&gt; SRR975569     2  0.3991   -0.17453 0.000 0.524 0.000 0.000 0.004 0.472
#&gt; SRR975570     2  0.3991   -0.17453 0.000 0.524 0.000 0.000 0.004 0.472
#&gt; SRR975571     2  0.0146    0.41600 0.000 0.996 0.000 0.000 0.000 0.004
#&gt; SRR975572     2  0.3995   -0.19010 0.000 0.516 0.000 0.000 0.004 0.480
#&gt; SRR975573     2  0.0000    0.41828 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR975574     2  0.0000    0.41828 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR975575     2  0.3995   -0.19010 0.000 0.516 0.000 0.000 0.004 0.480
#&gt; SRR975576     2  0.3993   -0.18220 0.000 0.520 0.000 0.000 0.004 0.476
#&gt; SRR975577     2  0.0000    0.41828 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR975578     2  0.0146    0.41600 0.000 0.996 0.000 0.000 0.000 0.004
#&gt; SRR975579     4  0.0725    0.66084 0.000 0.012 0.000 0.976 0.000 0.012
#&gt; SRR975580     2  0.4687   -0.02939 0.000 0.684 0.000 0.000 0.136 0.180
#&gt; SRR975581     2  0.3866   -0.18860 0.000 0.516 0.000 0.000 0.000 0.484
#&gt; SRR975582     2  0.0000    0.41828 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR975583     2  0.3995   -0.19010 0.000 0.516 0.000 0.000 0.004 0.480
#&gt; SRR975584     2  0.0000    0.41828 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR975585     2  0.3995   -0.18792 0.000 0.516 0.000 0.000 0.004 0.480
#&gt; SRR975586     6  0.5672    0.71644 0.000 0.360 0.000 0.020 0.100 0.520
#&gt; SRR975587     3  0.3325    0.65979 0.000 0.000 0.820 0.000 0.096 0.084
#&gt; SRR975588     2  0.3991   -0.17453 0.000 0.524 0.000 0.000 0.004 0.472
#&gt; SRR975589     3  0.5871    0.38981 0.032 0.000 0.572 0.012 0.300 0.084
#&gt; SRR975590     5  0.5204    0.93890 0.128 0.000 0.204 0.000 0.652 0.016
#&gt; SRR975591     3  0.0000    0.71847 0.000 0.000 1.000 0.000 0.000 0.000
#&gt; SRR975592     3  0.5421    0.38940 0.024 0.000 0.612 0.012 0.292 0.060
#&gt; SRR975593     3  0.5798    0.39629 0.032 0.000 0.584 0.012 0.292 0.080
#&gt; SRR975594     3  0.3325    0.65979 0.000 0.000 0.820 0.000 0.096 0.084
#&gt; SRR975595     5  0.4653    0.96349 0.120 0.000 0.196 0.000 0.684 0.000
#&gt; SRR975597     5  0.4653    0.96349 0.120 0.000 0.196 0.000 0.684 0.000
#&gt; SRR975596     1  0.4061    0.68235 0.784 0.000 0.000 0.024 0.080 0.112
#&gt; SRR975598     5  0.4701    0.93185 0.148 0.000 0.168 0.000 0.684 0.000
#&gt; SRR975599     1  0.5074    0.31569 0.572 0.000 0.000 0.012 0.356 0.060
#&gt; SRR975600     3  0.3646    0.63063 0.000 0.000 0.800 0.008 0.132 0.060
#&gt; SRR975601     3  0.3325    0.65979 0.000 0.000 0.820 0.000 0.096 0.084
#&gt; SRR975602     1  0.4917    0.41294 0.620 0.000 0.000 0.012 0.308 0.060
#&gt; SRR975603     3  0.0000    0.71847 0.000 0.000 1.000 0.000 0.000 0.000
#&gt; SRR975604     3  0.0000    0.71847 0.000 0.000 1.000 0.000 0.000 0.000
</code></pre>

<script>
$('#tab-CV-kmeans-get-classes-5-a').parent().next().next().hide();
$('#tab-CV-kmeans-get-classes-5-a').click(function(){
  $('#tab-CV-kmeans-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-CV-kmeans-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-CV-kmeans-consensus-heatmap'>
<ul>
<li><a href='#tab-CV-kmeans-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-CV-kmeans-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-CV-kmeans-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-CV-kmeans-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-CV-kmeans-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-CV-kmeans-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-consensus-heatmap-1-1.png" alt="plot of chunk tab-CV-kmeans-consensus-heatmap-1"/></p>

</div>
<div id='tab-CV-kmeans-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-consensus-heatmap-2-1.png" alt="plot of chunk tab-CV-kmeans-consensus-heatmap-2"/></p>

</div>
<div id='tab-CV-kmeans-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-consensus-heatmap-3-1.png" alt="plot of chunk tab-CV-kmeans-consensus-heatmap-3"/></p>

</div>
<div id='tab-CV-kmeans-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-consensus-heatmap-4-1.png" alt="plot of chunk tab-CV-kmeans-consensus-heatmap-4"/></p>

</div>
<div id='tab-CV-kmeans-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-consensus-heatmap-5-1.png" alt="plot of chunk tab-CV-kmeans-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-CV-kmeans-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-CV-kmeans-membership-heatmap'>
<ul>
<li><a href='#tab-CV-kmeans-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-CV-kmeans-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-CV-kmeans-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-CV-kmeans-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-CV-kmeans-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-CV-kmeans-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-membership-heatmap-1-1.png" alt="plot of chunk tab-CV-kmeans-membership-heatmap-1"/></p>

</div>
<div id='tab-CV-kmeans-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-membership-heatmap-2-1.png" alt="plot of chunk tab-CV-kmeans-membership-heatmap-2"/></p>

</div>
<div id='tab-CV-kmeans-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-membership-heatmap-3-1.png" alt="plot of chunk tab-CV-kmeans-membership-heatmap-3"/></p>

</div>
<div id='tab-CV-kmeans-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-membership-heatmap-4-1.png" alt="plot of chunk tab-CV-kmeans-membership-heatmap-4"/></p>

</div>
<div id='tab-CV-kmeans-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-membership-heatmap-5-1.png" alt="plot of chunk tab-CV-kmeans-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-CV-kmeans-get-signatures' ).tabs();
} );
</script>
<div id='tabs-CV-kmeans-get-signatures'>
<ul>
<li><a href='#tab-CV-kmeans-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-CV-kmeans-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-CV-kmeans-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-CV-kmeans-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-CV-kmeans-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-CV-kmeans-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-get-signatures-1-1.png" alt="plot of chunk tab-CV-kmeans-get-signatures-1"/></p>

</div>
<div id='tab-CV-kmeans-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-get-signatures-2-1.png" alt="plot of chunk tab-CV-kmeans-get-signatures-2"/></p>

</div>
<div id='tab-CV-kmeans-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-get-signatures-3-1.png" alt="plot of chunk tab-CV-kmeans-get-signatures-3"/></p>

</div>
<div id='tab-CV-kmeans-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-get-signatures-4-1.png" alt="plot of chunk tab-CV-kmeans-get-signatures-4"/></p>

</div>
<div id='tab-CV-kmeans-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-get-signatures-5-1.png" alt="plot of chunk tab-CV-kmeans-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-CV-kmeans-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-CV-kmeans-get-signatures-no-scale'>
<ul>
<li><a href='#tab-CV-kmeans-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-CV-kmeans-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-CV-kmeans-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-CV-kmeans-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-CV-kmeans-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-CV-kmeans-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-CV-kmeans-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-CV-kmeans-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-CV-kmeans-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-CV-kmeans-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-CV-kmeans-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-CV-kmeans-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-CV-kmeans-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-CV-kmeans-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-CV-kmeans-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk CV-kmeans-signature_compare](figure_cola/CV-kmeans-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-CV-kmeans-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-CV-kmeans-dimension-reduction'>
<ul>
<li><a href='#tab-CV-kmeans-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-CV-kmeans-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-CV-kmeans-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-CV-kmeans-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-CV-kmeans-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-CV-kmeans-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-dimension-reduction-1-1.png" alt="plot of chunk tab-CV-kmeans-dimension-reduction-1"/></p>

</div>
<div id='tab-CV-kmeans-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-dimension-reduction-2-1.png" alt="plot of chunk tab-CV-kmeans-dimension-reduction-2"/></p>

</div>
<div id='tab-CV-kmeans-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-dimension-reduction-3-1.png" alt="plot of chunk tab-CV-kmeans-dimension-reduction-3"/></p>

</div>
<div id='tab-CV-kmeans-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-dimension-reduction-4-1.png" alt="plot of chunk tab-CV-kmeans-dimension-reduction-4"/></p>

</div>
<div id='tab-CV-kmeans-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-dimension-reduction-5-1.png" alt="plot of chunk tab-CV-kmeans-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk CV-kmeans-collect-classes](figure_cola/CV-kmeans-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### CV:skmeans*






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["CV", "skmeans"]
# you can also extract it by
# res = res_list["CV:skmeans"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 17171 rows and 54 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'CV' method.
#>   Subgroups are detected by 'skmeans' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 4.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk CV-skmeans-collect-plots](figure_cola/CV-skmeans-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk CV-skmeans-select-partition-number](figure_cola/CV-skmeans-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 1.000           0.969       0.989         0.5093 0.491   0.491
#> 3 3 1.000           0.950       0.978         0.2882 0.820   0.646
#> 4 4 0.940           0.922       0.966         0.1108 0.918   0.766
#> 5 5 0.797           0.729       0.838         0.0586 0.994   0.980
#> 6 6 0.779           0.694       0.731         0.0452 0.921   0.710
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 4
#> attr(,"optional")
#> [1] 2 3
```

There is also optional best $k$ = 2 3 that is worth to check.

Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-CV-skmeans-get-classes' ).tabs();
} );
</script>
<div id='tabs-CV-skmeans-get-classes'>
<ul>
<li><a href='#tab-CV-skmeans-get-classes-1'>k = 2</a></li>
<li><a href='#tab-CV-skmeans-get-classes-2'>k = 3</a></li>
<li><a href='#tab-CV-skmeans-get-classes-3'>k = 4</a></li>
<li><a href='#tab-CV-skmeans-get-classes-4'>k = 5</a></li>
<li><a href='#tab-CV-skmeans-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-CV-skmeans-get-classes-1'>
<p><a id='tab-CV-skmeans-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2
#&gt; SRR975551     1   0.000      0.999 1.000 0.000
#&gt; SRR975552     1   0.224      0.961 0.964 0.036
#&gt; SRR975554     1   0.000      0.999 1.000 0.000
#&gt; SRR975553     2   0.000      0.977 0.000 1.000
#&gt; SRR975555     1   0.000      0.999 1.000 0.000
#&gt; SRR975556     2   0.000      0.977 0.000 1.000
#&gt; SRR975557     2   0.000      0.977 0.000 1.000
#&gt; SRR975558     2   0.998      0.116 0.472 0.528
#&gt; SRR975559     1   0.000      0.999 1.000 0.000
#&gt; SRR975560     2   0.000      0.977 0.000 1.000
#&gt; SRR975561     2   0.000      0.977 0.000 1.000
#&gt; SRR975562     1   0.000      0.999 1.000 0.000
#&gt; SRR975563     2   0.000      0.977 0.000 1.000
#&gt; SRR975564     1   0.000      0.999 1.000 0.000
#&gt; SRR975565     1   0.000      0.999 1.000 0.000
#&gt; SRR975566     1   0.000      0.999 1.000 0.000
#&gt; SRR975567     2   0.506      0.861 0.112 0.888
#&gt; SRR975568     1   0.000      0.999 1.000 0.000
#&gt; SRR975569     2   0.000      0.977 0.000 1.000
#&gt; SRR975570     2   0.000      0.977 0.000 1.000
#&gt; SRR975571     2   0.000      0.977 0.000 1.000
#&gt; SRR975572     2   0.000      0.977 0.000 1.000
#&gt; SRR975573     2   0.000      0.977 0.000 1.000
#&gt; SRR975574     2   0.000      0.977 0.000 1.000
#&gt; SRR975575     2   0.000      0.977 0.000 1.000
#&gt; SRR975576     2   0.000      0.977 0.000 1.000
#&gt; SRR975577     2   0.000      0.977 0.000 1.000
#&gt; SRR975578     2   0.000      0.977 0.000 1.000
#&gt; SRR975579     2   0.000      0.977 0.000 1.000
#&gt; SRR975580     2   0.000      0.977 0.000 1.000
#&gt; SRR975581     2   0.000      0.977 0.000 1.000
#&gt; SRR975582     2   0.000      0.977 0.000 1.000
#&gt; SRR975583     2   0.000      0.977 0.000 1.000
#&gt; SRR975584     2   0.000      0.977 0.000 1.000
#&gt; SRR975585     2   0.000      0.977 0.000 1.000
#&gt; SRR975586     2   0.000      0.977 0.000 1.000
#&gt; SRR975587     1   0.000      0.999 1.000 0.000
#&gt; SRR975588     2   0.000      0.977 0.000 1.000
#&gt; SRR975589     1   0.000      0.999 1.000 0.000
#&gt; SRR975590     1   0.000      0.999 1.000 0.000
#&gt; SRR975591     1   0.000      0.999 1.000 0.000
#&gt; SRR975592     1   0.000      0.999 1.000 0.000
#&gt; SRR975593     1   0.000      0.999 1.000 0.000
#&gt; SRR975594     1   0.000      0.999 1.000 0.000
#&gt; SRR975595     1   0.000      0.999 1.000 0.000
#&gt; SRR975597     1   0.000      0.999 1.000 0.000
#&gt; SRR975596     1   0.000      0.999 1.000 0.000
#&gt; SRR975598     1   0.000      0.999 1.000 0.000
#&gt; SRR975599     1   0.000      0.999 1.000 0.000
#&gt; SRR975600     1   0.000      0.999 1.000 0.000
#&gt; SRR975601     1   0.000      0.999 1.000 0.000
#&gt; SRR975602     1   0.000      0.999 1.000 0.000
#&gt; SRR975603     1   0.000      0.999 1.000 0.000
#&gt; SRR975604     1   0.000      0.999 1.000 0.000
</code></pre>

<script>
$('#tab-CV-skmeans-get-classes-1-a').parent().next().next().hide();
$('#tab-CV-skmeans-get-classes-1-a').click(function(){
  $('#tab-CV-skmeans-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-skmeans-get-classes-2'>
<p><a id='tab-CV-skmeans-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3
#&gt; SRR975551     1  0.0237      0.962 0.996 0.000 0.004
#&gt; SRR975552     1  0.0237      0.962 0.996 0.000 0.004
#&gt; SRR975554     1  0.0237      0.962 0.996 0.000 0.004
#&gt; SRR975553     2  0.0000      0.981 0.000 1.000 0.000
#&gt; SRR975555     1  0.0237      0.962 0.996 0.000 0.004
#&gt; SRR975556     2  0.0000      0.981 0.000 1.000 0.000
#&gt; SRR975557     2  0.6001      0.740 0.176 0.772 0.052
#&gt; SRR975558     1  0.1163      0.941 0.972 0.000 0.028
#&gt; SRR975559     1  0.0000      0.960 1.000 0.000 0.000
#&gt; SRR975560     2  0.4796      0.729 0.220 0.780 0.000
#&gt; SRR975561     2  0.0237      0.979 0.004 0.996 0.000
#&gt; SRR975562     1  0.0237      0.962 0.996 0.000 0.004
#&gt; SRR975563     2  0.0000      0.981 0.000 1.000 0.000
#&gt; SRR975564     1  0.0237      0.962 0.996 0.000 0.004
#&gt; SRR975565     1  0.0237      0.962 0.996 0.000 0.004
#&gt; SRR975566     1  0.0237      0.962 0.996 0.000 0.004
#&gt; SRR975567     1  0.1163      0.941 0.972 0.000 0.028
#&gt; SRR975568     1  0.0237      0.962 0.996 0.000 0.004
#&gt; SRR975569     2  0.0000      0.981 0.000 1.000 0.000
#&gt; SRR975570     2  0.0000      0.981 0.000 1.000 0.000
#&gt; SRR975571     2  0.0000      0.981 0.000 1.000 0.000
#&gt; SRR975572     2  0.0000      0.981 0.000 1.000 0.000
#&gt; SRR975573     2  0.0000      0.981 0.000 1.000 0.000
#&gt; SRR975574     2  0.0000      0.981 0.000 1.000 0.000
#&gt; SRR975575     2  0.0000      0.981 0.000 1.000 0.000
#&gt; SRR975576     2  0.0000      0.981 0.000 1.000 0.000
#&gt; SRR975577     2  0.0000      0.981 0.000 1.000 0.000
#&gt; SRR975578     2  0.0000      0.981 0.000 1.000 0.000
#&gt; SRR975579     2  0.0237      0.979 0.004 0.996 0.000
#&gt; SRR975580     2  0.0000      0.981 0.000 1.000 0.000
#&gt; SRR975581     2  0.0000      0.981 0.000 1.000 0.000
#&gt; SRR975582     2  0.0000      0.981 0.000 1.000 0.000
#&gt; SRR975583     2  0.0000      0.981 0.000 1.000 0.000
#&gt; SRR975584     2  0.0000      0.981 0.000 1.000 0.000
#&gt; SRR975585     2  0.0000      0.981 0.000 1.000 0.000
#&gt; SRR975586     2  0.0000      0.981 0.000 1.000 0.000
#&gt; SRR975587     3  0.0000      0.985 0.000 0.000 1.000
#&gt; SRR975588     2  0.0000      0.981 0.000 1.000 0.000
#&gt; SRR975589     3  0.0000      0.985 0.000 0.000 1.000
#&gt; SRR975590     3  0.1163      0.970 0.028 0.000 0.972
#&gt; SRR975591     3  0.0000      0.985 0.000 0.000 1.000
#&gt; SRR975592     3  0.0000      0.985 0.000 0.000 1.000
#&gt; SRR975593     3  0.0000      0.985 0.000 0.000 1.000
#&gt; SRR975594     3  0.0000      0.985 0.000 0.000 1.000
#&gt; SRR975595     3  0.1860      0.955 0.052 0.000 0.948
#&gt; SRR975597     3  0.1860      0.955 0.052 0.000 0.948
#&gt; SRR975596     1  0.0000      0.960 1.000 0.000 0.000
#&gt; SRR975598     3  0.1860      0.955 0.052 0.000 0.948
#&gt; SRR975599     1  0.6252      0.176 0.556 0.000 0.444
#&gt; SRR975600     3  0.0000      0.985 0.000 0.000 1.000
#&gt; SRR975601     3  0.0000      0.985 0.000 0.000 1.000
#&gt; SRR975602     1  0.0237      0.962 0.996 0.000 0.004
#&gt; SRR975603     3  0.0000      0.985 0.000 0.000 1.000
#&gt; SRR975604     3  0.0000      0.985 0.000 0.000 1.000
</code></pre>

<script>
$('#tab-CV-skmeans-get-classes-2-a').parent().next().next().hide();
$('#tab-CV-skmeans-get-classes-2-a').click(function(){
  $('#tab-CV-skmeans-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-skmeans-get-classes-3'>
<p><a id='tab-CV-skmeans-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3    p4
#&gt; SRR975551     1  0.0000      0.967 1.000 0.000 0.000 0.000
#&gt; SRR975552     1  0.0188      0.965 0.996 0.000 0.000 0.004
#&gt; SRR975554     1  0.0000      0.967 1.000 0.000 0.000 0.000
#&gt; SRR975553     2  0.0000      0.977 0.000 1.000 0.000 0.000
#&gt; SRR975555     1  0.0188      0.965 0.996 0.000 0.000 0.004
#&gt; SRR975556     2  0.0000      0.977 0.000 1.000 0.000 0.000
#&gt; SRR975557     4  0.0188      0.955 0.000 0.004 0.000 0.996
#&gt; SRR975558     4  0.3400      0.770 0.180 0.000 0.000 0.820
#&gt; SRR975559     1  0.3569      0.750 0.804 0.000 0.000 0.196
#&gt; SRR975560     4  0.0188      0.955 0.000 0.004 0.000 0.996
#&gt; SRR975561     4  0.0707      0.945 0.000 0.020 0.000 0.980
#&gt; SRR975562     1  0.0000      0.967 1.000 0.000 0.000 0.000
#&gt; SRR975563     2  0.0000      0.977 0.000 1.000 0.000 0.000
#&gt; SRR975564     1  0.0000      0.967 1.000 0.000 0.000 0.000
#&gt; SRR975565     1  0.0000      0.967 1.000 0.000 0.000 0.000
#&gt; SRR975566     1  0.0188      0.965 0.996 0.000 0.000 0.004
#&gt; SRR975567     4  0.0188      0.953 0.004 0.000 0.000 0.996
#&gt; SRR975568     1  0.0000      0.967 1.000 0.000 0.000 0.000
#&gt; SRR975569     2  0.0000      0.977 0.000 1.000 0.000 0.000
#&gt; SRR975570     2  0.0000      0.977 0.000 1.000 0.000 0.000
#&gt; SRR975571     2  0.0000      0.977 0.000 1.000 0.000 0.000
#&gt; SRR975572     2  0.0000      0.977 0.000 1.000 0.000 0.000
#&gt; SRR975573     2  0.0000      0.977 0.000 1.000 0.000 0.000
#&gt; SRR975574     2  0.0000      0.977 0.000 1.000 0.000 0.000
#&gt; SRR975575     2  0.0000      0.977 0.000 1.000 0.000 0.000
#&gt; SRR975576     2  0.0000      0.977 0.000 1.000 0.000 0.000
#&gt; SRR975577     2  0.0000      0.977 0.000 1.000 0.000 0.000
#&gt; SRR975578     2  0.0000      0.977 0.000 1.000 0.000 0.000
#&gt; SRR975579     4  0.0336      0.954 0.000 0.008 0.000 0.992
#&gt; SRR975580     2  0.0000      0.977 0.000 1.000 0.000 0.000
#&gt; SRR975581     2  0.0000      0.977 0.000 1.000 0.000 0.000
#&gt; SRR975582     2  0.0000      0.977 0.000 1.000 0.000 0.000
#&gt; SRR975583     2  0.0000      0.977 0.000 1.000 0.000 0.000
#&gt; SRR975584     2  0.0000      0.977 0.000 1.000 0.000 0.000
#&gt; SRR975585     2  0.0000      0.977 0.000 1.000 0.000 0.000
#&gt; SRR975586     2  0.4941      0.210 0.000 0.564 0.000 0.436
#&gt; SRR975587     3  0.0000      0.929 0.000 0.000 1.000 0.000
#&gt; SRR975588     2  0.0000      0.977 0.000 1.000 0.000 0.000
#&gt; SRR975589     3  0.0000      0.929 0.000 0.000 1.000 0.000
#&gt; SRR975590     3  0.1022      0.910 0.032 0.000 0.968 0.000
#&gt; SRR975591     3  0.0000      0.929 0.000 0.000 1.000 0.000
#&gt; SRR975592     3  0.0000      0.929 0.000 0.000 1.000 0.000
#&gt; SRR975593     3  0.0000      0.929 0.000 0.000 1.000 0.000
#&gt; SRR975594     3  0.0000      0.929 0.000 0.000 1.000 0.000
#&gt; SRR975595     3  0.4018      0.752 0.224 0.000 0.772 0.004
#&gt; SRR975597     3  0.4018      0.752 0.224 0.000 0.772 0.004
#&gt; SRR975596     1  0.2921      0.827 0.860 0.000 0.000 0.140
#&gt; SRR975598     3  0.4699      0.605 0.320 0.000 0.676 0.004
#&gt; SRR975599     1  0.0188      0.965 0.996 0.000 0.000 0.004
#&gt; SRR975600     3  0.0000      0.929 0.000 0.000 1.000 0.000
#&gt; SRR975601     3  0.0000      0.929 0.000 0.000 1.000 0.000
#&gt; SRR975602     1  0.0188      0.965 0.996 0.000 0.000 0.004
#&gt; SRR975603     3  0.0000      0.929 0.000 0.000 1.000 0.000
#&gt; SRR975604     3  0.0000      0.929 0.000 0.000 1.000 0.000
</code></pre>

<script>
$('#tab-CV-skmeans-get-classes-3-a').parent().next().next().hide();
$('#tab-CV-skmeans-get-classes-3-a').click(function(){
  $('#tab-CV-skmeans-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-skmeans-get-classes-4'>
<p><a id='tab-CV-skmeans-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3    p4    p5
#&gt; SRR975551     1  0.0510      0.833 0.984 0.000 0.000 0.000 0.016
#&gt; SRR975552     1  0.1410      0.835 0.940 0.000 0.000 0.000 0.060
#&gt; SRR975554     1  0.0880      0.835 0.968 0.000 0.000 0.000 0.032
#&gt; SRR975553     2  0.3857      0.778 0.000 0.688 0.000 0.312 0.000
#&gt; SRR975555     1  0.3177      0.793 0.792 0.000 0.000 0.000 0.208
#&gt; SRR975556     2  0.1792      0.768 0.000 0.916 0.000 0.084 0.000
#&gt; SRR975557     4  0.4235      0.675 0.000 0.000 0.000 0.576 0.424
#&gt; SRR975558     5  0.5283      0.202 0.188 0.000 0.000 0.136 0.676
#&gt; SRR975559     1  0.4451      0.409 0.644 0.000 0.000 0.016 0.340
#&gt; SRR975560     4  0.4268      0.467 0.000 0.000 0.000 0.556 0.444
#&gt; SRR975561     4  0.5019      0.646 0.000 0.052 0.000 0.632 0.316
#&gt; SRR975562     1  0.1704      0.823 0.928 0.000 0.000 0.004 0.068
#&gt; SRR975563     2  0.0000      0.824 0.000 1.000 0.000 0.000 0.000
#&gt; SRR975564     1  0.2732      0.806 0.840 0.000 0.000 0.000 0.160
#&gt; SRR975565     1  0.1851      0.828 0.912 0.000 0.000 0.000 0.088
#&gt; SRR975566     1  0.1792      0.801 0.916 0.000 0.000 0.000 0.084
#&gt; SRR975567     5  0.4171     -0.531 0.000 0.000 0.000 0.396 0.604
#&gt; SRR975568     1  0.2852      0.803 0.828 0.000 0.000 0.000 0.172
#&gt; SRR975569     2  0.0000      0.824 0.000 1.000 0.000 0.000 0.000
#&gt; SRR975570     2  0.0000      0.824 0.000 1.000 0.000 0.000 0.000
#&gt; SRR975571     2  0.3857      0.778 0.000 0.688 0.000 0.312 0.000
#&gt; SRR975572     2  0.0000      0.824 0.000 1.000 0.000 0.000 0.000
#&gt; SRR975573     2  0.3857      0.778 0.000 0.688 0.000 0.312 0.000
#&gt; SRR975574     2  0.3857      0.778 0.000 0.688 0.000 0.312 0.000
#&gt; SRR975575     2  0.0000      0.824 0.000 1.000 0.000 0.000 0.000
#&gt; SRR975576     2  0.0000      0.824 0.000 1.000 0.000 0.000 0.000
#&gt; SRR975577     2  0.3857      0.778 0.000 0.688 0.000 0.312 0.000
#&gt; SRR975578     2  0.3857      0.778 0.000 0.688 0.000 0.312 0.000
#&gt; SRR975579     4  0.4341      0.704 0.000 0.004 0.000 0.592 0.404
#&gt; SRR975580     2  0.4367      0.723 0.000 0.620 0.000 0.372 0.008
#&gt; SRR975581     2  0.0000      0.824 0.000 1.000 0.000 0.000 0.000
#&gt; SRR975582     2  0.3857      0.778 0.000 0.688 0.000 0.312 0.000
#&gt; SRR975583     2  0.0000      0.824 0.000 1.000 0.000 0.000 0.000
#&gt; SRR975584     2  0.3857      0.778 0.000 0.688 0.000 0.312 0.000
#&gt; SRR975585     2  0.0000      0.824 0.000 1.000 0.000 0.000 0.000
#&gt; SRR975586     2  0.4235      0.129 0.000 0.576 0.000 0.424 0.000
#&gt; SRR975587     3  0.0510      0.881 0.000 0.000 0.984 0.000 0.016
#&gt; SRR975588     2  0.0000      0.824 0.000 1.000 0.000 0.000 0.000
#&gt; SRR975589     3  0.0566      0.881 0.000 0.000 0.984 0.004 0.012
#&gt; SRR975590     3  0.3229      0.805 0.032 0.000 0.840 0.000 0.128
#&gt; SRR975591     3  0.0162      0.881 0.000 0.000 0.996 0.004 0.000
#&gt; SRR975592     3  0.0404      0.881 0.000 0.000 0.988 0.000 0.012
#&gt; SRR975593     3  0.0566      0.881 0.000 0.000 0.984 0.004 0.012
#&gt; SRR975594     3  0.0510      0.881 0.000 0.000 0.984 0.000 0.016
#&gt; SRR975595     3  0.5871      0.598 0.184 0.000 0.604 0.000 0.212
#&gt; SRR975597     3  0.5841      0.602 0.180 0.000 0.608 0.000 0.212
#&gt; SRR975596     1  0.3961      0.601 0.736 0.000 0.000 0.016 0.248
#&gt; SRR975598     3  0.6315      0.463 0.260 0.000 0.528 0.000 0.212
#&gt; SRR975599     1  0.3616      0.719 0.768 0.000 0.004 0.004 0.224
#&gt; SRR975600     3  0.0162      0.881 0.000 0.000 0.996 0.004 0.000
#&gt; SRR975601     3  0.0510      0.881 0.000 0.000 0.984 0.000 0.016
#&gt; SRR975602     1  0.2773      0.771 0.836 0.000 0.000 0.000 0.164
#&gt; SRR975603     3  0.0162      0.881 0.000 0.000 0.996 0.004 0.000
#&gt; SRR975604     3  0.0162      0.881 0.000 0.000 0.996 0.004 0.000
</code></pre>

<script>
$('#tab-CV-skmeans-get-classes-4-a').parent().next().next().hide();
$('#tab-CV-skmeans-get-classes-4-a').click(function(){
  $('#tab-CV-skmeans-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-skmeans-get-classes-5'>
<p><a id='tab-CV-skmeans-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3    p4    p5    p6
#&gt; SRR975551     1  0.0717      0.661 0.976 0.008 0.000 0.000 0.000 0.016
#&gt; SRR975552     1  0.1588      0.647 0.924 0.004 0.000 0.000 0.000 0.072
#&gt; SRR975554     1  0.1714      0.653 0.908 0.000 0.000 0.000 0.000 0.092
#&gt; SRR975553     5  0.0146      0.954 0.000 0.000 0.000 0.004 0.996 0.000
#&gt; SRR975555     1  0.4598      0.502 0.592 0.048 0.000 0.000 0.000 0.360
#&gt; SRR975556     2  0.4018      0.683 0.000 0.656 0.000 0.000 0.324 0.020
#&gt; SRR975557     4  0.0458      0.678 0.000 0.000 0.000 0.984 0.000 0.016
#&gt; SRR975558     6  0.5225      0.000 0.112 0.012 0.000 0.248 0.000 0.628
#&gt; SRR975559     1  0.5235      0.217 0.612 0.016 0.000 0.088 0.000 0.284
#&gt; SRR975560     4  0.6374      0.288 0.004 0.184 0.000 0.492 0.028 0.292
#&gt; SRR975561     4  0.1493      0.660 0.000 0.056 0.000 0.936 0.004 0.004
#&gt; SRR975562     1  0.3829      0.601 0.760 0.060 0.000 0.000 0.000 0.180
#&gt; SRR975563     2  0.3854      0.900 0.000 0.536 0.000 0.000 0.464 0.000
#&gt; SRR975564     1  0.3938      0.515 0.660 0.016 0.000 0.000 0.000 0.324
#&gt; SRR975565     1  0.2558      0.625 0.840 0.004 0.000 0.000 0.000 0.156
#&gt; SRR975566     1  0.1765      0.642 0.924 0.024 0.000 0.000 0.000 0.052
#&gt; SRR975567     4  0.4399      0.210 0.004 0.028 0.000 0.616 0.000 0.352
#&gt; SRR975568     1  0.3867      0.512 0.660 0.012 0.000 0.000 0.000 0.328
#&gt; SRR975569     2  0.3857      0.904 0.000 0.532 0.000 0.000 0.468 0.000
#&gt; SRR975570     2  0.3857      0.904 0.000 0.532 0.000 0.000 0.468 0.000
#&gt; SRR975571     5  0.0146      0.954 0.000 0.000 0.000 0.004 0.996 0.000
#&gt; SRR975572     2  0.3857      0.904 0.000 0.532 0.000 0.000 0.468 0.000
#&gt; SRR975573     5  0.0000      0.957 0.000 0.000 0.000 0.000 1.000 0.000
#&gt; SRR975574     5  0.0000      0.957 0.000 0.000 0.000 0.000 1.000 0.000
#&gt; SRR975575     2  0.3857      0.904 0.000 0.532 0.000 0.000 0.468 0.000
#&gt; SRR975576     2  0.3857      0.904 0.000 0.532 0.000 0.000 0.468 0.000
#&gt; SRR975577     5  0.0000      0.957 0.000 0.000 0.000 0.000 1.000 0.000
#&gt; SRR975578     5  0.0146      0.954 0.000 0.004 0.000 0.000 0.996 0.000
#&gt; SRR975579     4  0.0000      0.683 0.000 0.000 0.000 1.000 0.000 0.000
#&gt; SRR975580     5  0.3695      0.648 0.000 0.184 0.000 0.004 0.772 0.040
#&gt; SRR975581     2  0.3857      0.904 0.000 0.532 0.000 0.000 0.468 0.000
#&gt; SRR975582     5  0.0000      0.957 0.000 0.000 0.000 0.000 1.000 0.000
#&gt; SRR975583     2  0.3857      0.904 0.000 0.532 0.000 0.000 0.468 0.000
#&gt; SRR975584     5  0.0000      0.957 0.000 0.000 0.000 0.000 1.000 0.000
#&gt; SRR975585     2  0.3857      0.904 0.000 0.532 0.000 0.000 0.468 0.000
#&gt; SRR975586     2  0.5583      0.327 0.000 0.600 0.000 0.244 0.136 0.020
#&gt; SRR975587     3  0.1334      0.806 0.000 0.020 0.948 0.000 0.000 0.032
#&gt; SRR975588     2  0.3857      0.904 0.000 0.532 0.000 0.000 0.468 0.000
#&gt; SRR975589     3  0.1838      0.787 0.000 0.016 0.916 0.000 0.000 0.068
#&gt; SRR975590     3  0.5761      0.617 0.052 0.156 0.628 0.000 0.000 0.164
#&gt; SRR975591     3  0.0146      0.806 0.000 0.004 0.996 0.000 0.000 0.000
#&gt; SRR975592     3  0.1257      0.807 0.000 0.020 0.952 0.000 0.000 0.028
#&gt; SRR975593     3  0.2030      0.786 0.000 0.028 0.908 0.000 0.000 0.064
#&gt; SRR975594     3  0.0891      0.808 0.000 0.008 0.968 0.000 0.000 0.024
#&gt; SRR975595     3  0.7050      0.416 0.080 0.244 0.412 0.000 0.000 0.264
#&gt; SRR975597     3  0.7040      0.419 0.080 0.244 0.416 0.000 0.000 0.260
#&gt; SRR975596     1  0.4907      0.361 0.636 0.020 0.000 0.052 0.000 0.292
#&gt; SRR975598     3  0.7234      0.373 0.100 0.244 0.384 0.000 0.000 0.272
#&gt; SRR975599     1  0.5894      0.303 0.472 0.244 0.000 0.000 0.000 0.284
#&gt; SRR975600     3  0.0000      0.807 0.000 0.000 1.000 0.000 0.000 0.000
#&gt; SRR975601     3  0.1168      0.807 0.000 0.016 0.956 0.000 0.000 0.028
#&gt; SRR975602     1  0.4792      0.521 0.668 0.132 0.000 0.000 0.000 0.200
#&gt; SRR975603     3  0.0146      0.806 0.000 0.004 0.996 0.000 0.000 0.000
#&gt; SRR975604     3  0.0146      0.806 0.000 0.004 0.996 0.000 0.000 0.000
</code></pre>

<script>
$('#tab-CV-skmeans-get-classes-5-a').parent().next().next().hide();
$('#tab-CV-skmeans-get-classes-5-a').click(function(){
  $('#tab-CV-skmeans-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-CV-skmeans-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-CV-skmeans-consensus-heatmap'>
<ul>
<li><a href='#tab-CV-skmeans-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-CV-skmeans-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-CV-skmeans-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-CV-skmeans-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-CV-skmeans-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-CV-skmeans-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-consensus-heatmap-1-1.png" alt="plot of chunk tab-CV-skmeans-consensus-heatmap-1"/></p>

</div>
<div id='tab-CV-skmeans-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-consensus-heatmap-2-1.png" alt="plot of chunk tab-CV-skmeans-consensus-heatmap-2"/></p>

</div>
<div id='tab-CV-skmeans-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-consensus-heatmap-3-1.png" alt="plot of chunk tab-CV-skmeans-consensus-heatmap-3"/></p>

</div>
<div id='tab-CV-skmeans-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-consensus-heatmap-4-1.png" alt="plot of chunk tab-CV-skmeans-consensus-heatmap-4"/></p>

</div>
<div id='tab-CV-skmeans-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-consensus-heatmap-5-1.png" alt="plot of chunk tab-CV-skmeans-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-CV-skmeans-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-CV-skmeans-membership-heatmap'>
<ul>
<li><a href='#tab-CV-skmeans-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-CV-skmeans-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-CV-skmeans-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-CV-skmeans-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-CV-skmeans-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-CV-skmeans-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-membership-heatmap-1-1.png" alt="plot of chunk tab-CV-skmeans-membership-heatmap-1"/></p>

</div>
<div id='tab-CV-skmeans-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-membership-heatmap-2-1.png" alt="plot of chunk tab-CV-skmeans-membership-heatmap-2"/></p>

</div>
<div id='tab-CV-skmeans-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-membership-heatmap-3-1.png" alt="plot of chunk tab-CV-skmeans-membership-heatmap-3"/></p>

</div>
<div id='tab-CV-skmeans-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-membership-heatmap-4-1.png" alt="plot of chunk tab-CV-skmeans-membership-heatmap-4"/></p>

</div>
<div id='tab-CV-skmeans-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-membership-heatmap-5-1.png" alt="plot of chunk tab-CV-skmeans-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-CV-skmeans-get-signatures' ).tabs();
} );
</script>
<div id='tabs-CV-skmeans-get-signatures'>
<ul>
<li><a href='#tab-CV-skmeans-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-CV-skmeans-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-CV-skmeans-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-CV-skmeans-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-CV-skmeans-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-CV-skmeans-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-get-signatures-1-1.png" alt="plot of chunk tab-CV-skmeans-get-signatures-1"/></p>

</div>
<div id='tab-CV-skmeans-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-get-signatures-2-1.png" alt="plot of chunk tab-CV-skmeans-get-signatures-2"/></p>

</div>
<div id='tab-CV-skmeans-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-get-signatures-3-1.png" alt="plot of chunk tab-CV-skmeans-get-signatures-3"/></p>

</div>
<div id='tab-CV-skmeans-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-get-signatures-4-1.png" alt="plot of chunk tab-CV-skmeans-get-signatures-4"/></p>

</div>
<div id='tab-CV-skmeans-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-get-signatures-5-1.png" alt="plot of chunk tab-CV-skmeans-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-CV-skmeans-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-CV-skmeans-get-signatures-no-scale'>
<ul>
<li><a href='#tab-CV-skmeans-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-CV-skmeans-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-CV-skmeans-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-CV-skmeans-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-CV-skmeans-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-CV-skmeans-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-CV-skmeans-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-CV-skmeans-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-CV-skmeans-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-CV-skmeans-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-CV-skmeans-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-CV-skmeans-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-CV-skmeans-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-CV-skmeans-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-CV-skmeans-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk CV-skmeans-signature_compare](figure_cola/CV-skmeans-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-CV-skmeans-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-CV-skmeans-dimension-reduction'>
<ul>
<li><a href='#tab-CV-skmeans-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-CV-skmeans-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-CV-skmeans-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-CV-skmeans-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-CV-skmeans-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-CV-skmeans-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-dimension-reduction-1-1.png" alt="plot of chunk tab-CV-skmeans-dimension-reduction-1"/></p>

</div>
<div id='tab-CV-skmeans-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-dimension-reduction-2-1.png" alt="plot of chunk tab-CV-skmeans-dimension-reduction-2"/></p>

</div>
<div id='tab-CV-skmeans-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-dimension-reduction-3-1.png" alt="plot of chunk tab-CV-skmeans-dimension-reduction-3"/></p>

</div>
<div id='tab-CV-skmeans-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-dimension-reduction-4-1.png" alt="plot of chunk tab-CV-skmeans-dimension-reduction-4"/></p>

</div>
<div id='tab-CV-skmeans-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-dimension-reduction-5-1.png" alt="plot of chunk tab-CV-skmeans-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk CV-skmeans-collect-classes](figure_cola/CV-skmeans-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### CV:pam**






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["CV", "pam"]
# you can also extract it by
# res = res_list["CV:pam"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 17171 rows and 54 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'CV' method.
#>   Subgroups are detected by 'pam' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 3.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk CV-pam-collect-plots](figure_cola/CV-pam-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk CV-pam-select-partition-number](figure_cola/CV-pam-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 0.858           0.960       0.974         0.5014 0.491   0.491
#> 3 3 0.951           0.907       0.963         0.2779 0.877   0.749
#> 4 4 0.794           0.731       0.855         0.1068 0.869   0.662
#> 5 5 0.884           0.741       0.885         0.0513 0.932   0.773
#> 6 6 0.889           0.736       0.895         0.0335 0.959   0.847
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 3
```


Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-CV-pam-get-classes' ).tabs();
} );
</script>
<div id='tabs-CV-pam-get-classes'>
<ul>
<li><a href='#tab-CV-pam-get-classes-1'>k = 2</a></li>
<li><a href='#tab-CV-pam-get-classes-2'>k = 3</a></li>
<li><a href='#tab-CV-pam-get-classes-3'>k = 4</a></li>
<li><a href='#tab-CV-pam-get-classes-4'>k = 5</a></li>
<li><a href='#tab-CV-pam-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-CV-pam-get-classes-1'>
<p><a id='tab-CV-pam-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2
#&gt; SRR975551     1   0.295      0.940 0.948 0.052
#&gt; SRR975552     1   0.730      0.811 0.796 0.204
#&gt; SRR975554     1   0.295      0.940 0.948 0.052
#&gt; SRR975553     2   0.000      1.000 0.000 1.000
#&gt; SRR975555     1   0.722      0.816 0.800 0.200
#&gt; SRR975556     2   0.000      1.000 0.000 1.000
#&gt; SRR975557     2   0.000      1.000 0.000 1.000
#&gt; SRR975558     2   0.000      1.000 0.000 1.000
#&gt; SRR975559     1   0.295      0.940 0.948 0.052
#&gt; SRR975560     2   0.000      1.000 0.000 1.000
#&gt; SRR975561     2   0.000      1.000 0.000 1.000
#&gt; SRR975562     1   0.295      0.940 0.948 0.052
#&gt; SRR975563     2   0.000      1.000 0.000 1.000
#&gt; SRR975564     1   0.689      0.832 0.816 0.184
#&gt; SRR975565     1   0.722      0.816 0.800 0.200
#&gt; SRR975566     1   0.295      0.940 0.948 0.052
#&gt; SRR975567     2   0.000      1.000 0.000 1.000
#&gt; SRR975568     1   0.722      0.816 0.800 0.200
#&gt; SRR975569     2   0.000      1.000 0.000 1.000
#&gt; SRR975570     2   0.000      1.000 0.000 1.000
#&gt; SRR975571     2   0.000      1.000 0.000 1.000
#&gt; SRR975572     2   0.000      1.000 0.000 1.000
#&gt; SRR975573     2   0.000      1.000 0.000 1.000
#&gt; SRR975574     2   0.000      1.000 0.000 1.000
#&gt; SRR975575     2   0.000      1.000 0.000 1.000
#&gt; SRR975576     2   0.000      1.000 0.000 1.000
#&gt; SRR975577     2   0.000      1.000 0.000 1.000
#&gt; SRR975578     2   0.000      1.000 0.000 1.000
#&gt; SRR975579     2   0.000      1.000 0.000 1.000
#&gt; SRR975580     2   0.000      1.000 0.000 1.000
#&gt; SRR975581     2   0.000      1.000 0.000 1.000
#&gt; SRR975582     2   0.000      1.000 0.000 1.000
#&gt; SRR975583     2   0.000      1.000 0.000 1.000
#&gt; SRR975584     2   0.000      1.000 0.000 1.000
#&gt; SRR975585     2   0.000      1.000 0.000 1.000
#&gt; SRR975586     2   0.000      1.000 0.000 1.000
#&gt; SRR975587     1   0.000      0.946 1.000 0.000
#&gt; SRR975588     2   0.000      1.000 0.000 1.000
#&gt; SRR975589     1   0.000      0.946 1.000 0.000
#&gt; SRR975590     1   0.000      0.946 1.000 0.000
#&gt; SRR975591     1   0.000      0.946 1.000 0.000
#&gt; SRR975592     1   0.000      0.946 1.000 0.000
#&gt; SRR975593     1   0.000      0.946 1.000 0.000
#&gt; SRR975594     1   0.000      0.946 1.000 0.000
#&gt; SRR975595     1   0.000      0.946 1.000 0.000
#&gt; SRR975597     1   0.000      0.946 1.000 0.000
#&gt; SRR975596     1   0.295      0.940 0.948 0.052
#&gt; SRR975598     1   0.000      0.946 1.000 0.000
#&gt; SRR975599     1   0.295      0.940 0.948 0.052
#&gt; SRR975600     1   0.000      0.946 1.000 0.000
#&gt; SRR975601     1   0.000      0.946 1.000 0.000
#&gt; SRR975602     1   0.295      0.940 0.948 0.052
#&gt; SRR975603     1   0.000      0.946 1.000 0.000
#&gt; SRR975604     1   0.000      0.946 1.000 0.000
</code></pre>

<script>
$('#tab-CV-pam-get-classes-1-a').parent().next().next().hide();
$('#tab-CV-pam-get-classes-1-a').click(function(){
  $('#tab-CV-pam-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-pam-get-classes-2'>
<p><a id='tab-CV-pam-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3
#&gt; SRR975551     1  0.0000      0.927 1.000 0.000 0.000
#&gt; SRR975552     1  0.0000      0.927 1.000 0.000 0.000
#&gt; SRR975554     1  0.0000      0.927 1.000 0.000 0.000
#&gt; SRR975553     2  0.0000      0.966 0.000 1.000 0.000
#&gt; SRR975555     1  0.0000      0.927 1.000 0.000 0.000
#&gt; SRR975556     2  0.0000      0.966 0.000 1.000 0.000
#&gt; SRR975557     2  0.1289      0.939 0.032 0.968 0.000
#&gt; SRR975558     2  0.6305      0.109 0.484 0.516 0.000
#&gt; SRR975559     1  0.0000      0.927 1.000 0.000 0.000
#&gt; SRR975560     2  0.0424      0.960 0.008 0.992 0.000
#&gt; SRR975561     2  0.0000      0.966 0.000 1.000 0.000
#&gt; SRR975562     1  0.0000      0.927 1.000 0.000 0.000
#&gt; SRR975563     2  0.0000      0.966 0.000 1.000 0.000
#&gt; SRR975564     1  0.0000      0.927 1.000 0.000 0.000
#&gt; SRR975565     1  0.0000      0.927 1.000 0.000 0.000
#&gt; SRR975566     1  0.0000      0.927 1.000 0.000 0.000
#&gt; SRR975567     2  0.5678      0.550 0.316 0.684 0.000
#&gt; SRR975568     1  0.0000      0.927 1.000 0.000 0.000
#&gt; SRR975569     2  0.0000      0.966 0.000 1.000 0.000
#&gt; SRR975570     2  0.0000      0.966 0.000 1.000 0.000
#&gt; SRR975571     2  0.0000      0.966 0.000 1.000 0.000
#&gt; SRR975572     2  0.0000      0.966 0.000 1.000 0.000
#&gt; SRR975573     2  0.0000      0.966 0.000 1.000 0.000
#&gt; SRR975574     2  0.0000      0.966 0.000 1.000 0.000
#&gt; SRR975575     2  0.0000      0.966 0.000 1.000 0.000
#&gt; SRR975576     2  0.0000      0.966 0.000 1.000 0.000
#&gt; SRR975577     2  0.0000      0.966 0.000 1.000 0.000
#&gt; SRR975578     2  0.0000      0.966 0.000 1.000 0.000
#&gt; SRR975579     2  0.0000      0.966 0.000 1.000 0.000
#&gt; SRR975580     2  0.0000      0.966 0.000 1.000 0.000
#&gt; SRR975581     2  0.0000      0.966 0.000 1.000 0.000
#&gt; SRR975582     2  0.0000      0.966 0.000 1.000 0.000
#&gt; SRR975583     2  0.0000      0.966 0.000 1.000 0.000
#&gt; SRR975584     2  0.0000      0.966 0.000 1.000 0.000
#&gt; SRR975585     2  0.0000      0.966 0.000 1.000 0.000
#&gt; SRR975586     2  0.0000      0.966 0.000 1.000 0.000
#&gt; SRR975587     3  0.0000      0.985 0.000 0.000 1.000
#&gt; SRR975588     2  0.0000      0.966 0.000 1.000 0.000
#&gt; SRR975589     3  0.0000      0.985 0.000 0.000 1.000
#&gt; SRR975590     3  0.2261      0.927 0.068 0.000 0.932
#&gt; SRR975591     3  0.0000      0.985 0.000 0.000 1.000
#&gt; SRR975592     3  0.2261      0.927 0.068 0.000 0.932
#&gt; SRR975593     3  0.0000      0.985 0.000 0.000 1.000
#&gt; SRR975594     3  0.0000      0.985 0.000 0.000 1.000
#&gt; SRR975595     1  0.6154      0.344 0.592 0.000 0.408
#&gt; SRR975597     1  0.6204      0.300 0.576 0.000 0.424
#&gt; SRR975596     1  0.2356      0.871 0.928 0.000 0.072
#&gt; SRR975598     1  0.3482      0.817 0.872 0.000 0.128
#&gt; SRR975599     1  0.0000      0.927 1.000 0.000 0.000
#&gt; SRR975600     3  0.0000      0.985 0.000 0.000 1.000
#&gt; SRR975601     3  0.0000      0.985 0.000 0.000 1.000
#&gt; SRR975602     1  0.0000      0.927 1.000 0.000 0.000
#&gt; SRR975603     3  0.0000      0.985 0.000 0.000 1.000
#&gt; SRR975604     3  0.0000      0.985 0.000 0.000 1.000
</code></pre>

<script>
$('#tab-CV-pam-get-classes-2-a').parent().next().next().hide();
$('#tab-CV-pam-get-classes-2-a').click(function(){
  $('#tab-CV-pam-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-pam-get-classes-3'>
<p><a id='tab-CV-pam-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3    p4
#&gt; SRR975551     1  0.0000     0.6070 1.000 0.000 0.000 0.000
#&gt; SRR975552     1  0.4072     0.3172 0.748 0.000 0.000 0.252
#&gt; SRR975554     1  0.2469     0.5292 0.892 0.000 0.000 0.108
#&gt; SRR975553     2  0.0188     0.9907 0.000 0.996 0.000 0.004
#&gt; SRR975555     1  0.0188     0.6066 0.996 0.000 0.000 0.004
#&gt; SRR975556     2  0.0000     0.9912 0.000 1.000 0.000 0.000
#&gt; SRR975557     4  0.5792     0.5280 0.056 0.296 0.000 0.648
#&gt; SRR975558     4  0.6454     0.4893 0.380 0.076 0.000 0.544
#&gt; SRR975559     4  0.4985     0.4032 0.468 0.000 0.000 0.532
#&gt; SRR975560     4  0.5263     0.3676 0.008 0.448 0.000 0.544
#&gt; SRR975561     2  0.2647     0.8545 0.000 0.880 0.000 0.120
#&gt; SRR975562     1  0.4697    -0.0233 0.644 0.000 0.000 0.356
#&gt; SRR975563     2  0.0000     0.9912 0.000 1.000 0.000 0.000
#&gt; SRR975564     1  0.1022     0.5938 0.968 0.000 0.000 0.032
#&gt; SRR975565     1  0.4877    -0.2027 0.592 0.000 0.000 0.408
#&gt; SRR975566     4  0.4985     0.4032 0.468 0.000 0.000 0.532
#&gt; SRR975567     4  0.7152     0.5397 0.284 0.172 0.000 0.544
#&gt; SRR975568     1  0.3610     0.4075 0.800 0.000 0.000 0.200
#&gt; SRR975569     2  0.0000     0.9912 0.000 1.000 0.000 0.000
#&gt; SRR975570     2  0.0000     0.9912 0.000 1.000 0.000 0.000
#&gt; SRR975571     2  0.0188     0.9907 0.000 0.996 0.000 0.004
#&gt; SRR975572     2  0.0000     0.9912 0.000 1.000 0.000 0.000
#&gt; SRR975573     2  0.0188     0.9907 0.000 0.996 0.000 0.004
#&gt; SRR975574     2  0.0188     0.9907 0.000 0.996 0.000 0.004
#&gt; SRR975575     2  0.0000     0.9912 0.000 1.000 0.000 0.000
#&gt; SRR975576     2  0.0000     0.9912 0.000 1.000 0.000 0.000
#&gt; SRR975577     2  0.0188     0.9907 0.000 0.996 0.000 0.004
#&gt; SRR975578     2  0.0188     0.9907 0.000 0.996 0.000 0.004
#&gt; SRR975579     4  0.4713     0.5010 0.000 0.360 0.000 0.640
#&gt; SRR975580     2  0.0336     0.9875 0.000 0.992 0.000 0.008
#&gt; SRR975581     2  0.0000     0.9912 0.000 1.000 0.000 0.000
#&gt; SRR975582     2  0.0188     0.9907 0.000 0.996 0.000 0.004
#&gt; SRR975583     2  0.0000     0.9912 0.000 1.000 0.000 0.000
#&gt; SRR975584     2  0.0188     0.9907 0.000 0.996 0.000 0.004
#&gt; SRR975585     2  0.0000     0.9912 0.000 1.000 0.000 0.000
#&gt; SRR975586     2  0.0336     0.9849 0.000 0.992 0.000 0.008
#&gt; SRR975587     3  0.0000     0.9181 0.000 0.000 1.000 0.000
#&gt; SRR975588     2  0.0000     0.9912 0.000 1.000 0.000 0.000
#&gt; SRR975589     3  0.3074     0.8440 0.000 0.000 0.848 0.152
#&gt; SRR975590     1  0.7760     0.1637 0.408 0.000 0.240 0.352
#&gt; SRR975591     3  0.0000     0.9181 0.000 0.000 1.000 0.000
#&gt; SRR975592     3  0.6893     0.3924 0.300 0.000 0.564 0.136
#&gt; SRR975593     3  0.3172     0.8390 0.000 0.000 0.840 0.160
#&gt; SRR975594     3  0.0000     0.9181 0.000 0.000 1.000 0.000
#&gt; SRR975595     1  0.6426     0.4791 0.568 0.000 0.080 0.352
#&gt; SRR975597     1  0.6186     0.4960 0.584 0.000 0.064 0.352
#&gt; SRR975596     4  0.4981     0.4041 0.464 0.000 0.000 0.536
#&gt; SRR975598     1  0.5420     0.5226 0.624 0.000 0.024 0.352
#&gt; SRR975599     1  0.3726     0.5710 0.788 0.000 0.000 0.212
#&gt; SRR975600     3  0.0592     0.9131 0.000 0.000 0.984 0.016
#&gt; SRR975601     3  0.0000     0.9181 0.000 0.000 1.000 0.000
#&gt; SRR975602     1  0.0000     0.6070 1.000 0.000 0.000 0.000
#&gt; SRR975603     3  0.0000     0.9181 0.000 0.000 1.000 0.000
#&gt; SRR975604     3  0.0000     0.9181 0.000 0.000 1.000 0.000
</code></pre>

<script>
$('#tab-CV-pam-get-classes-3-a').parent().next().next().hide();
$('#tab-CV-pam-get-classes-3-a').click(function(){
  $('#tab-CV-pam-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-pam-get-classes-4'>
<p><a id='tab-CV-pam-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3    p4    p5
#&gt; SRR975551     1  0.4397     0.5263 0.696 0.000 0.000 0.028 0.276
#&gt; SRR975552     1  0.5642     0.3954 0.636 0.000 0.000 0.184 0.180
#&gt; SRR975554     1  0.0865     0.7152 0.972 0.000 0.000 0.004 0.024
#&gt; SRR975553     2  0.0404     0.9479 0.000 0.988 0.000 0.012 0.000
#&gt; SRR975555     1  0.1444     0.7131 0.948 0.000 0.000 0.012 0.040
#&gt; SRR975556     2  0.0000     0.9493 0.000 1.000 0.000 0.000 0.000
#&gt; SRR975557     4  0.0404     0.4371 0.000 0.012 0.000 0.988 0.000
#&gt; SRR975558     1  0.5557    -0.5187 0.468 0.068 0.000 0.464 0.000
#&gt; SRR975559     4  0.4452     0.4753 0.496 0.000 0.000 0.500 0.004
#&gt; SRR975560     2  0.5177    -0.0111 0.040 0.488 0.000 0.472 0.000
#&gt; SRR975561     2  0.4287     0.3165 0.000 0.540 0.000 0.460 0.000
#&gt; SRR975562     1  0.2519     0.6486 0.884 0.000 0.000 0.100 0.016
#&gt; SRR975563     2  0.0000     0.9493 0.000 1.000 0.000 0.000 0.000
#&gt; SRR975564     1  0.1106     0.7161 0.964 0.000 0.000 0.012 0.024
#&gt; SRR975565     1  0.0000     0.7010 1.000 0.000 0.000 0.000 0.000
#&gt; SRR975566     4  0.4307     0.4713 0.500 0.000 0.000 0.500 0.000
#&gt; SRR975567     4  0.5276     0.4765 0.436 0.048 0.000 0.516 0.000
#&gt; SRR975568     1  0.1106     0.7161 0.964 0.000 0.000 0.012 0.024
#&gt; SRR975569     2  0.0000     0.9493 0.000 1.000 0.000 0.000 0.000
#&gt; SRR975570     2  0.0000     0.9493 0.000 1.000 0.000 0.000 0.000
#&gt; SRR975571     2  0.0404     0.9479 0.000 0.988 0.000 0.012 0.000
#&gt; SRR975572     2  0.0000     0.9493 0.000 1.000 0.000 0.000 0.000
#&gt; SRR975573     2  0.0404     0.9479 0.000 0.988 0.000 0.012 0.000
#&gt; SRR975574     2  0.0404     0.9479 0.000 0.988 0.000 0.012 0.000
#&gt; SRR975575     2  0.0000     0.9493 0.000 1.000 0.000 0.000 0.000
#&gt; SRR975576     2  0.0000     0.9493 0.000 1.000 0.000 0.000 0.000
#&gt; SRR975577     2  0.0404     0.9479 0.000 0.988 0.000 0.012 0.000
#&gt; SRR975578     2  0.0404     0.9479 0.000 0.988 0.000 0.012 0.000
#&gt; SRR975579     4  0.1792     0.4138 0.000 0.084 0.000 0.916 0.000
#&gt; SRR975580     2  0.0510     0.9456 0.000 0.984 0.000 0.016 0.000
#&gt; SRR975581     2  0.0000     0.9493 0.000 1.000 0.000 0.000 0.000
#&gt; SRR975582     2  0.0404     0.9479 0.000 0.988 0.000 0.012 0.000
#&gt; SRR975583     2  0.0000     0.9493 0.000 1.000 0.000 0.000 0.000
#&gt; SRR975584     2  0.0404     0.9479 0.000 0.988 0.000 0.012 0.000
#&gt; SRR975585     2  0.0000     0.9493 0.000 1.000 0.000 0.000 0.000
#&gt; SRR975586     2  0.0404     0.9421 0.000 0.988 0.000 0.012 0.000
#&gt; SRR975587     3  0.0000     0.9458 0.000 0.000 1.000 0.000 0.000
#&gt; SRR975588     2  0.0000     0.9493 0.000 1.000 0.000 0.000 0.000
#&gt; SRR975589     3  0.2891     0.7921 0.000 0.000 0.824 0.000 0.176
#&gt; SRR975590     5  0.0162     0.8515 0.004 0.000 0.000 0.000 0.996
#&gt; SRR975591     3  0.0000     0.9458 0.000 0.000 1.000 0.000 0.000
#&gt; SRR975592     5  0.4300    -0.0282 0.000 0.000 0.476 0.000 0.524
#&gt; SRR975593     3  0.2966     0.7829 0.000 0.000 0.816 0.000 0.184
#&gt; SRR975594     3  0.0000     0.9458 0.000 0.000 1.000 0.000 0.000
#&gt; SRR975595     5  0.0000     0.8544 0.000 0.000 0.000 0.000 1.000
#&gt; SRR975597     5  0.0000     0.8544 0.000 0.000 0.000 0.000 1.000
#&gt; SRR975596     4  0.4306     0.4734 0.492 0.000 0.000 0.508 0.000
#&gt; SRR975598     5  0.0000     0.8544 0.000 0.000 0.000 0.000 1.000
#&gt; SRR975599     1  0.4731     0.1912 0.528 0.000 0.000 0.016 0.456
#&gt; SRR975600     3  0.0510     0.9372 0.000 0.000 0.984 0.000 0.016
#&gt; SRR975601     3  0.0000     0.9458 0.000 0.000 1.000 0.000 0.000
#&gt; SRR975602     1  0.3214     0.6763 0.844 0.000 0.000 0.036 0.120
#&gt; SRR975603     3  0.0000     0.9458 0.000 0.000 1.000 0.000 0.000
#&gt; SRR975604     3  0.0000     0.9458 0.000 0.000 1.000 0.000 0.000
</code></pre>

<script>
$('#tab-CV-pam-get-classes-4-a').parent().next().next().hide();
$('#tab-CV-pam-get-classes-4-a').click(function(){
  $('#tab-CV-pam-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-pam-get-classes-5'>
<p><a id='tab-CV-pam-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3    p4    p5    p6
#&gt; SRR975551     1  0.6116     0.0408 0.360 0.000 0.000 0.000 0.340 0.300
#&gt; SRR975552     6  0.5554     0.2888 0.276 0.000 0.000 0.000 0.180 0.544
#&gt; SRR975554     1  0.2793     0.4694 0.800 0.000 0.000 0.000 0.000 0.200
#&gt; SRR975553     2  0.1176     0.9463 0.000 0.956 0.000 0.024 0.000 0.020
#&gt; SRR975555     1  0.0000     0.6310 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR975556     2  0.0146     0.9531 0.000 0.996 0.000 0.000 0.000 0.004
#&gt; SRR975557     4  0.0547     0.6416 0.000 0.000 0.000 0.980 0.000 0.020
#&gt; SRR975558     1  0.3944    -0.0195 0.568 0.004 0.000 0.000 0.000 0.428
#&gt; SRR975559     6  0.0547     0.7149 0.020 0.000 0.000 0.000 0.000 0.980
#&gt; SRR975560     2  0.4623     0.2170 0.016 0.540 0.000 0.016 0.000 0.428
#&gt; SRR975561     4  0.3727     0.3755 0.000 0.388 0.000 0.612 0.000 0.000
#&gt; SRR975562     6  0.4095    -0.0227 0.480 0.000 0.000 0.000 0.008 0.512
#&gt; SRR975563     2  0.0000     0.9536 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR975564     1  0.0000     0.6310 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR975565     1  0.0000     0.6310 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR975566     6  0.0632     0.7155 0.024 0.000 0.000 0.000 0.000 0.976
#&gt; SRR975567     6  0.3618     0.6191 0.124 0.032 0.000 0.032 0.000 0.812
#&gt; SRR975568     1  0.0000     0.6310 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR975569     2  0.0000     0.9536 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR975570     2  0.0000     0.9536 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR975571     2  0.1176     0.9463 0.000 0.956 0.000 0.024 0.000 0.020
#&gt; SRR975572     2  0.0000     0.9536 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR975573     2  0.0993     0.9479 0.000 0.964 0.000 0.024 0.000 0.012
#&gt; SRR975574     2  0.1176     0.9463 0.000 0.956 0.000 0.024 0.000 0.020
#&gt; SRR975575     2  0.0000     0.9536 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR975576     2  0.0000     0.9536 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR975577     2  0.1176     0.9463 0.000 0.956 0.000 0.024 0.000 0.020
#&gt; SRR975578     2  0.1176     0.9463 0.000 0.956 0.000 0.024 0.000 0.020
#&gt; SRR975579     4  0.0692     0.6424 0.000 0.004 0.000 0.976 0.000 0.020
#&gt; SRR975580     2  0.1261     0.9439 0.000 0.952 0.000 0.024 0.000 0.024
#&gt; SRR975581     2  0.0000     0.9536 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR975582     2  0.1176     0.9463 0.000 0.956 0.000 0.024 0.000 0.020
#&gt; SRR975583     2  0.0000     0.9536 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR975584     2  0.1176     0.9463 0.000 0.956 0.000 0.024 0.000 0.020
#&gt; SRR975585     2  0.0000     0.9536 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR975586     2  0.0000     0.9536 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR975587     3  0.0000     0.9463 0.000 0.000 1.000 0.000 0.000 0.000
#&gt; SRR975588     2  0.0000     0.9536 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR975589     3  0.2703     0.7948 0.004 0.000 0.824 0.000 0.172 0.000
#&gt; SRR975590     5  0.0000     0.8351 0.000 0.000 0.000 0.000 1.000 0.000
#&gt; SRR975591     3  0.0000     0.9463 0.000 0.000 1.000 0.000 0.000 0.000
#&gt; SRR975592     5  0.3862    -0.0346 0.000 0.000 0.476 0.000 0.524 0.000
#&gt; SRR975593     3  0.2664     0.7835 0.000 0.000 0.816 0.000 0.184 0.000
#&gt; SRR975594     3  0.0000     0.9463 0.000 0.000 1.000 0.000 0.000 0.000
#&gt; SRR975595     5  0.0000     0.8351 0.000 0.000 0.000 0.000 1.000 0.000
#&gt; SRR975597     5  0.0000     0.8351 0.000 0.000 0.000 0.000 1.000 0.000
#&gt; SRR975596     6  0.0713     0.7158 0.028 0.000 0.000 0.000 0.000 0.972
#&gt; SRR975598     5  0.0000     0.8351 0.000 0.000 0.000 0.000 1.000 0.000
#&gt; SRR975599     1  0.4385     0.2997 0.532 0.000 0.000 0.000 0.444 0.024
#&gt; SRR975600     3  0.0458     0.9378 0.000 0.000 0.984 0.000 0.016 0.000
#&gt; SRR975601     3  0.0000     0.9463 0.000 0.000 1.000 0.000 0.000 0.000
#&gt; SRR975602     1  0.5877     0.0819 0.428 0.000 0.000 0.000 0.200 0.372
#&gt; SRR975603     3  0.0000     0.9463 0.000 0.000 1.000 0.000 0.000 0.000
#&gt; SRR975604     3  0.0000     0.9463 0.000 0.000 1.000 0.000 0.000 0.000
</code></pre>

<script>
$('#tab-CV-pam-get-classes-5-a').parent().next().next().hide();
$('#tab-CV-pam-get-classes-5-a').click(function(){
  $('#tab-CV-pam-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-CV-pam-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-CV-pam-consensus-heatmap'>
<ul>
<li><a href='#tab-CV-pam-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-CV-pam-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-CV-pam-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-CV-pam-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-CV-pam-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-CV-pam-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-consensus-heatmap-1-1.png" alt="plot of chunk tab-CV-pam-consensus-heatmap-1"/></p>

</div>
<div id='tab-CV-pam-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-consensus-heatmap-2-1.png" alt="plot of chunk tab-CV-pam-consensus-heatmap-2"/></p>

</div>
<div id='tab-CV-pam-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-consensus-heatmap-3-1.png" alt="plot of chunk tab-CV-pam-consensus-heatmap-3"/></p>

</div>
<div id='tab-CV-pam-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-consensus-heatmap-4-1.png" alt="plot of chunk tab-CV-pam-consensus-heatmap-4"/></p>

</div>
<div id='tab-CV-pam-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-consensus-heatmap-5-1.png" alt="plot of chunk tab-CV-pam-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-CV-pam-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-CV-pam-membership-heatmap'>
<ul>
<li><a href='#tab-CV-pam-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-CV-pam-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-CV-pam-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-CV-pam-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-CV-pam-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-CV-pam-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-membership-heatmap-1-1.png" alt="plot of chunk tab-CV-pam-membership-heatmap-1"/></p>

</div>
<div id='tab-CV-pam-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-membership-heatmap-2-1.png" alt="plot of chunk tab-CV-pam-membership-heatmap-2"/></p>

</div>
<div id='tab-CV-pam-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-membership-heatmap-3-1.png" alt="plot of chunk tab-CV-pam-membership-heatmap-3"/></p>

</div>
<div id='tab-CV-pam-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-membership-heatmap-4-1.png" alt="plot of chunk tab-CV-pam-membership-heatmap-4"/></p>

</div>
<div id='tab-CV-pam-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-membership-heatmap-5-1.png" alt="plot of chunk tab-CV-pam-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-CV-pam-get-signatures' ).tabs();
} );
</script>
<div id='tabs-CV-pam-get-signatures'>
<ul>
<li><a href='#tab-CV-pam-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-CV-pam-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-CV-pam-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-CV-pam-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-CV-pam-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-CV-pam-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-get-signatures-1-1.png" alt="plot of chunk tab-CV-pam-get-signatures-1"/></p>

</div>
<div id='tab-CV-pam-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-get-signatures-2-1.png" alt="plot of chunk tab-CV-pam-get-signatures-2"/></p>

</div>
<div id='tab-CV-pam-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-get-signatures-3-1.png" alt="plot of chunk tab-CV-pam-get-signatures-3"/></p>

</div>
<div id='tab-CV-pam-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-get-signatures-4-1.png" alt="plot of chunk tab-CV-pam-get-signatures-4"/></p>

</div>
<div id='tab-CV-pam-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-get-signatures-5-1.png" alt="plot of chunk tab-CV-pam-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-CV-pam-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-CV-pam-get-signatures-no-scale'>
<ul>
<li><a href='#tab-CV-pam-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-CV-pam-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-CV-pam-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-CV-pam-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-CV-pam-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-CV-pam-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-CV-pam-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-CV-pam-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-CV-pam-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-CV-pam-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-CV-pam-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-CV-pam-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-CV-pam-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-CV-pam-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-CV-pam-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk CV-pam-signature_compare](figure_cola/CV-pam-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-CV-pam-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-CV-pam-dimension-reduction'>
<ul>
<li><a href='#tab-CV-pam-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-CV-pam-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-CV-pam-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-CV-pam-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-CV-pam-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-CV-pam-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-dimension-reduction-1-1.png" alt="plot of chunk tab-CV-pam-dimension-reduction-1"/></p>

</div>
<div id='tab-CV-pam-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-dimension-reduction-2-1.png" alt="plot of chunk tab-CV-pam-dimension-reduction-2"/></p>

</div>
<div id='tab-CV-pam-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-dimension-reduction-3-1.png" alt="plot of chunk tab-CV-pam-dimension-reduction-3"/></p>

</div>
<div id='tab-CV-pam-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-dimension-reduction-4-1.png" alt="plot of chunk tab-CV-pam-dimension-reduction-4"/></p>

</div>
<div id='tab-CV-pam-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-dimension-reduction-5-1.png" alt="plot of chunk tab-CV-pam-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk CV-pam-collect-classes](figure_cola/CV-pam-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### CV:mclust






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["CV", "mclust"]
# you can also extract it by
# res = res_list["CV:mclust"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 17171 rows and 54 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'CV' method.
#>   Subgroups are detected by 'mclust' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 4.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk CV-mclust-collect-plots](figure_cola/CV-mclust-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk CV-mclust-select-partition-number](figure_cola/CV-mclust-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 0.509           0.797       0.859         0.4384 0.560   0.560
#> 3 3 0.595           0.792       0.861         0.4645 0.762   0.584
#> 4 4 0.887           0.893       0.928         0.1587 0.869   0.638
#> 5 5 0.880           0.891       0.864         0.0499 0.966   0.860
#> 6 6 0.831           0.813       0.868         0.0297 0.983   0.920
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 4
```


Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-CV-mclust-get-classes' ).tabs();
} );
</script>
<div id='tabs-CV-mclust-get-classes'>
<ul>
<li><a href='#tab-CV-mclust-get-classes-1'>k = 2</a></li>
<li><a href='#tab-CV-mclust-get-classes-2'>k = 3</a></li>
<li><a href='#tab-CV-mclust-get-classes-3'>k = 4</a></li>
<li><a href='#tab-CV-mclust-get-classes-4'>k = 5</a></li>
<li><a href='#tab-CV-mclust-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-CV-mclust-get-classes-1'>
<p><a id='tab-CV-mclust-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2
#&gt; SRR975551     1   0.000      0.766 1.000 0.000
#&gt; SRR975552     1   0.000      0.766 1.000 0.000
#&gt; SRR975554     1   0.000      0.766 1.000 0.000
#&gt; SRR975553     2   0.973      0.870 0.404 0.596
#&gt; SRR975555     1   0.000      0.766 1.000 0.000
#&gt; SRR975556     1   0.358      0.681 0.932 0.068
#&gt; SRR975557     1   0.000      0.766 1.000 0.000
#&gt; SRR975558     1   0.000      0.766 1.000 0.000
#&gt; SRR975559     1   0.000      0.766 1.000 0.000
#&gt; SRR975560     1   0.118      0.751 0.984 0.016
#&gt; SRR975561     1   0.184      0.737 0.972 0.028
#&gt; SRR975562     1   0.000      0.766 1.000 0.000
#&gt; SRR975563     2   0.900      0.984 0.316 0.684
#&gt; SRR975564     1   0.000      0.766 1.000 0.000
#&gt; SRR975565     1   0.000      0.766 1.000 0.000
#&gt; SRR975566     1   0.000      0.766 1.000 0.000
#&gt; SRR975567     1   0.000      0.766 1.000 0.000
#&gt; SRR975568     1   0.000      0.766 1.000 0.000
#&gt; SRR975569     2   0.900      0.984 0.316 0.684
#&gt; SRR975570     2   0.900      0.984 0.316 0.684
#&gt; SRR975571     2   0.973      0.870 0.404 0.596
#&gt; SRR975572     2   0.900      0.984 0.316 0.684
#&gt; SRR975573     2   0.900      0.984 0.316 0.684
#&gt; SRR975574     1   0.992     -0.560 0.552 0.448
#&gt; SRR975575     2   0.900      0.984 0.316 0.684
#&gt; SRR975576     2   0.900      0.984 0.316 0.684
#&gt; SRR975577     2   0.900      0.984 0.316 0.684
#&gt; SRR975578     2   0.900      0.984 0.316 0.684
#&gt; SRR975579     1   0.141      0.747 0.980 0.020
#&gt; SRR975580     1   0.141      0.747 0.980 0.020
#&gt; SRR975581     2   0.904      0.980 0.320 0.680
#&gt; SRR975582     2   0.900      0.984 0.316 0.684
#&gt; SRR975583     2   0.900      0.984 0.316 0.684
#&gt; SRR975584     2   0.900      0.984 0.316 0.684
#&gt; SRR975585     2   0.900      0.984 0.316 0.684
#&gt; SRR975586     1   0.358      0.681 0.932 0.068
#&gt; SRR975587     1   0.900      0.750 0.684 0.316
#&gt; SRR975588     2   0.900      0.984 0.316 0.684
#&gt; SRR975589     1   0.900      0.750 0.684 0.316
#&gt; SRR975590     1   0.900      0.750 0.684 0.316
#&gt; SRR975591     1   0.900      0.750 0.684 0.316
#&gt; SRR975592     1   0.900      0.750 0.684 0.316
#&gt; SRR975593     1   0.900      0.750 0.684 0.316
#&gt; SRR975594     1   0.900      0.750 0.684 0.316
#&gt; SRR975595     1   0.900      0.750 0.684 0.316
#&gt; SRR975597     1   0.900      0.750 0.684 0.316
#&gt; SRR975596     1   0.000      0.766 1.000 0.000
#&gt; SRR975598     1   0.900      0.750 0.684 0.316
#&gt; SRR975599     1   0.900      0.750 0.684 0.316
#&gt; SRR975600     1   0.900      0.750 0.684 0.316
#&gt; SRR975601     1   0.900      0.750 0.684 0.316
#&gt; SRR975602     1   0.653      0.760 0.832 0.168
#&gt; SRR975603     1   0.900      0.750 0.684 0.316
#&gt; SRR975604     1   0.900      0.750 0.684 0.316
</code></pre>

<script>
$('#tab-CV-mclust-get-classes-1-a').parent().next().next().hide();
$('#tab-CV-mclust-get-classes-1-a').click(function(){
  $('#tab-CV-mclust-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-mclust-get-classes-2'>
<p><a id='tab-CV-mclust-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3
#&gt; SRR975551     1  0.0237      0.833 0.996 0.004 0.000
#&gt; SRR975552     1  0.4477      0.856 0.864 0.068 0.068
#&gt; SRR975554     1  0.2496      0.889 0.928 0.068 0.004
#&gt; SRR975553     2  0.1525      0.949 0.004 0.964 0.032
#&gt; SRR975555     1  0.2261      0.888 0.932 0.068 0.000
#&gt; SRR975556     3  0.7983      0.518 0.104 0.264 0.632
#&gt; SRR975557     3  0.6148      0.672 0.076 0.148 0.776
#&gt; SRR975558     3  0.6252      0.662 0.144 0.084 0.772
#&gt; SRR975559     1  0.7176      0.582 0.684 0.068 0.248
#&gt; SRR975560     3  0.6252      0.662 0.144 0.084 0.772
#&gt; SRR975561     3  0.6208      0.669 0.076 0.152 0.772
#&gt; SRR975562     1  0.2496      0.889 0.928 0.068 0.004
#&gt; SRR975563     2  0.0000      0.983 0.000 1.000 0.000
#&gt; SRR975564     1  0.2496      0.889 0.928 0.068 0.004
#&gt; SRR975565     1  0.2261      0.888 0.932 0.068 0.000
#&gt; SRR975566     1  0.5153      0.824 0.832 0.068 0.100
#&gt; SRR975567     3  0.6252      0.662 0.144 0.084 0.772
#&gt; SRR975568     1  0.2261      0.888 0.932 0.068 0.000
#&gt; SRR975569     2  0.0000      0.983 0.000 1.000 0.000
#&gt; SRR975570     2  0.0000      0.983 0.000 1.000 0.000
#&gt; SRR975571     2  0.1525      0.949 0.004 0.964 0.032
#&gt; SRR975572     2  0.0000      0.983 0.000 1.000 0.000
#&gt; SRR975573     2  0.0000      0.983 0.000 1.000 0.000
#&gt; SRR975574     2  0.3879      0.780 0.000 0.848 0.152
#&gt; SRR975575     2  0.0000      0.983 0.000 1.000 0.000
#&gt; SRR975576     2  0.0000      0.983 0.000 1.000 0.000
#&gt; SRR975577     2  0.0000      0.983 0.000 1.000 0.000
#&gt; SRR975578     2  0.0000      0.983 0.000 1.000 0.000
#&gt; SRR975579     3  0.6122      0.671 0.072 0.152 0.776
#&gt; SRR975580     3  0.7692      0.581 0.136 0.184 0.680
#&gt; SRR975581     2  0.0000      0.983 0.000 1.000 0.000
#&gt; SRR975582     2  0.0000      0.983 0.000 1.000 0.000
#&gt; SRR975583     2  0.0000      0.983 0.000 1.000 0.000
#&gt; SRR975584     2  0.0000      0.983 0.000 1.000 0.000
#&gt; SRR975585     2  0.0000      0.983 0.000 1.000 0.000
#&gt; SRR975586     3  0.7764      0.472 0.068 0.328 0.604
#&gt; SRR975587     3  0.3038      0.733 0.104 0.000 0.896
#&gt; SRR975588     2  0.0000      0.983 0.000 1.000 0.000
#&gt; SRR975589     3  0.5327      0.583 0.272 0.000 0.728
#&gt; SRR975590     3  0.5835      0.572 0.340 0.000 0.660
#&gt; SRR975591     3  0.1529      0.736 0.040 0.000 0.960
#&gt; SRR975592     3  0.5327      0.583 0.272 0.000 0.728
#&gt; SRR975593     3  0.5327      0.583 0.272 0.000 0.728
#&gt; SRR975594     3  0.1753      0.736 0.048 0.000 0.952
#&gt; SRR975595     3  0.5835      0.572 0.340 0.000 0.660
#&gt; SRR975597     3  0.5835      0.572 0.340 0.000 0.660
#&gt; SRR975596     1  0.7022      0.617 0.700 0.068 0.232
#&gt; SRR975598     3  0.5835      0.572 0.340 0.000 0.660
#&gt; SRR975599     3  0.4062      0.727 0.164 0.000 0.836
#&gt; SRR975600     3  0.1529      0.736 0.040 0.000 0.960
#&gt; SRR975601     3  0.3038      0.733 0.104 0.000 0.896
#&gt; SRR975602     1  0.2448      0.807 0.924 0.000 0.076
#&gt; SRR975603     3  0.1529      0.736 0.040 0.000 0.960
#&gt; SRR975604     3  0.1529      0.736 0.040 0.000 0.960
</code></pre>

<script>
$('#tab-CV-mclust-get-classes-2-a').parent().next().next().hide();
$('#tab-CV-mclust-get-classes-2-a').click(function(){
  $('#tab-CV-mclust-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-mclust-get-classes-3'>
<p><a id='tab-CV-mclust-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3    p4
#&gt; SRR975551     1  0.0188      0.930 0.996 0.000 0.000 0.004
#&gt; SRR975552     1  0.1211      0.926 0.960 0.000 0.000 0.040
#&gt; SRR975554     1  0.0937      0.936 0.976 0.000 0.012 0.012
#&gt; SRR975553     2  0.1022      0.969 0.000 0.968 0.000 0.032
#&gt; SRR975555     1  0.0469      0.937 0.988 0.000 0.000 0.012
#&gt; SRR975556     4  0.2313      0.906 0.044 0.032 0.000 0.924
#&gt; SRR975557     4  0.1792      0.924 0.068 0.000 0.000 0.932
#&gt; SRR975558     4  0.1792      0.924 0.068 0.000 0.000 0.932
#&gt; SRR975559     1  0.2300      0.910 0.924 0.000 0.028 0.048
#&gt; SRR975560     4  0.1792      0.924 0.068 0.000 0.000 0.932
#&gt; SRR975561     4  0.1792      0.924 0.068 0.000 0.000 0.932
#&gt; SRR975562     1  0.0937      0.936 0.976 0.000 0.012 0.012
#&gt; SRR975563     2  0.0000      0.993 0.000 1.000 0.000 0.000
#&gt; SRR975564     1  0.0469      0.937 0.988 0.000 0.000 0.012
#&gt; SRR975565     1  0.0469      0.937 0.988 0.000 0.000 0.012
#&gt; SRR975566     1  0.0469      0.937 0.988 0.000 0.000 0.012
#&gt; SRR975567     4  0.1792      0.924 0.068 0.000 0.000 0.932
#&gt; SRR975568     1  0.0469      0.937 0.988 0.000 0.000 0.012
#&gt; SRR975569     2  0.0000      0.993 0.000 1.000 0.000 0.000
#&gt; SRR975570     2  0.0000      0.993 0.000 1.000 0.000 0.000
#&gt; SRR975571     2  0.1022      0.969 0.000 0.968 0.000 0.032
#&gt; SRR975572     2  0.0000      0.993 0.000 1.000 0.000 0.000
#&gt; SRR975573     2  0.0000      0.993 0.000 1.000 0.000 0.000
#&gt; SRR975574     4  0.4898      0.303 0.000 0.416 0.000 0.584
#&gt; SRR975575     2  0.0000      0.993 0.000 1.000 0.000 0.000
#&gt; SRR975576     2  0.0000      0.993 0.000 1.000 0.000 0.000
#&gt; SRR975577     2  0.0000      0.993 0.000 1.000 0.000 0.000
#&gt; SRR975578     2  0.0000      0.993 0.000 1.000 0.000 0.000
#&gt; SRR975579     4  0.1902      0.923 0.064 0.004 0.000 0.932
#&gt; SRR975580     4  0.1902      0.923 0.064 0.004 0.000 0.932
#&gt; SRR975581     2  0.1022      0.969 0.000 0.968 0.000 0.032
#&gt; SRR975582     2  0.0000      0.993 0.000 1.000 0.000 0.000
#&gt; SRR975583     2  0.0000      0.993 0.000 1.000 0.000 0.000
#&gt; SRR975584     2  0.0000      0.993 0.000 1.000 0.000 0.000
#&gt; SRR975585     2  0.0000      0.993 0.000 1.000 0.000 0.000
#&gt; SRR975586     4  0.3082      0.862 0.032 0.084 0.000 0.884
#&gt; SRR975587     3  0.0469      0.848 0.000 0.000 0.988 0.012
#&gt; SRR975588     2  0.0000      0.993 0.000 1.000 0.000 0.000
#&gt; SRR975589     3  0.3908      0.816 0.212 0.000 0.784 0.004
#&gt; SRR975590     3  0.5500      0.795 0.224 0.000 0.708 0.068
#&gt; SRR975591     3  0.0000      0.850 0.000 0.000 1.000 0.000
#&gt; SRR975592     3  0.3908      0.816 0.212 0.000 0.784 0.004
#&gt; SRR975593     3  0.3908      0.816 0.212 0.000 0.784 0.004
#&gt; SRR975594     3  0.0000      0.850 0.000 0.000 1.000 0.000
#&gt; SRR975595     3  0.5500      0.795 0.224 0.000 0.708 0.068
#&gt; SRR975597     3  0.5500      0.795 0.224 0.000 0.708 0.068
#&gt; SRR975596     1  0.1733      0.924 0.948 0.000 0.024 0.028
#&gt; SRR975598     3  0.5500      0.795 0.224 0.000 0.708 0.068
#&gt; SRR975599     1  0.7638      0.150 0.448 0.000 0.220 0.332
#&gt; SRR975600     3  0.0000      0.850 0.000 0.000 1.000 0.000
#&gt; SRR975601     3  0.0336      0.849 0.000 0.000 0.992 0.008
#&gt; SRR975602     1  0.1209      0.914 0.964 0.000 0.032 0.004
#&gt; SRR975603     3  0.0000      0.850 0.000 0.000 1.000 0.000
#&gt; SRR975604     3  0.0000      0.850 0.000 0.000 1.000 0.000
</code></pre>

<script>
$('#tab-CV-mclust-get-classes-3-a').parent().next().next().hide();
$('#tab-CV-mclust-get-classes-3-a').click(function(){
  $('#tab-CV-mclust-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-mclust-get-classes-4'>
<p><a id='tab-CV-mclust-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3    p4    p5
#&gt; SRR975551     1  0.0693      0.864 0.980 0.000 0.000 0.012 0.008
#&gt; SRR975552     1  0.2605      0.866 0.852 0.000 0.000 0.148 0.000
#&gt; SRR975554     1  0.2233      0.902 0.904 0.000 0.000 0.080 0.016
#&gt; SRR975553     2  0.1800      0.958 0.000 0.932 0.048 0.020 0.000
#&gt; SRR975555     1  0.1478      0.900 0.936 0.000 0.000 0.064 0.000
#&gt; SRR975556     4  0.4256      0.809 0.004 0.052 0.160 0.780 0.004
#&gt; SRR975557     4  0.1612      0.852 0.024 0.000 0.016 0.948 0.012
#&gt; SRR975558     4  0.1124      0.856 0.036 0.000 0.000 0.960 0.004
#&gt; SRR975559     1  0.3656      0.803 0.784 0.000 0.000 0.196 0.020
#&gt; SRR975560     4  0.1285      0.856 0.036 0.000 0.004 0.956 0.004
#&gt; SRR975561     4  0.3545      0.835 0.020 0.008 0.140 0.828 0.004
#&gt; SRR975562     1  0.2110      0.902 0.912 0.000 0.000 0.072 0.016
#&gt; SRR975563     2  0.0290      0.980 0.000 0.992 0.008 0.000 0.000
#&gt; SRR975564     1  0.2020      0.899 0.900 0.000 0.000 0.100 0.000
#&gt; SRR975565     1  0.1608      0.901 0.928 0.000 0.000 0.072 0.000
#&gt; SRR975566     1  0.2017      0.903 0.912 0.000 0.000 0.080 0.008
#&gt; SRR975567     4  0.1124      0.856 0.036 0.000 0.000 0.960 0.004
#&gt; SRR975568     1  0.1732      0.901 0.920 0.000 0.000 0.080 0.000
#&gt; SRR975569     2  0.0693      0.977 0.000 0.980 0.008 0.012 0.000
#&gt; SRR975570     2  0.0404      0.979 0.000 0.988 0.012 0.000 0.000
#&gt; SRR975571     2  0.1800      0.958 0.000 0.932 0.048 0.020 0.000
#&gt; SRR975572     2  0.0000      0.979 0.000 1.000 0.000 0.000 0.000
#&gt; SRR975573     2  0.0693      0.977 0.000 0.980 0.008 0.012 0.000
#&gt; SRR975574     4  0.6333      0.424 0.000 0.328 0.176 0.496 0.000
#&gt; SRR975575     2  0.0000      0.979 0.000 1.000 0.000 0.000 0.000
#&gt; SRR975576     2  0.0162      0.979 0.000 0.996 0.004 0.000 0.000
#&gt; SRR975577     2  0.0807      0.977 0.000 0.976 0.012 0.012 0.000
#&gt; SRR975578     2  0.1907      0.956 0.000 0.928 0.044 0.028 0.000
#&gt; SRR975579     4  0.1679      0.856 0.020 0.004 0.016 0.948 0.012
#&gt; SRR975580     4  0.2426      0.854 0.008 0.016 0.064 0.908 0.004
#&gt; SRR975581     2  0.1626      0.962 0.000 0.940 0.044 0.016 0.000
#&gt; SRR975582     2  0.0703      0.977 0.000 0.976 0.024 0.000 0.000
#&gt; SRR975583     2  0.0000      0.979 0.000 1.000 0.000 0.000 0.000
#&gt; SRR975584     2  0.1106      0.974 0.000 0.964 0.024 0.012 0.000
#&gt; SRR975585     2  0.0000      0.979 0.000 1.000 0.000 0.000 0.000
#&gt; SRR975586     4  0.5065      0.769 0.004 0.120 0.148 0.724 0.004
#&gt; SRR975587     3  0.3274      0.992 0.000 0.000 0.780 0.000 0.220
#&gt; SRR975588     2  0.0404      0.979 0.000 0.988 0.012 0.000 0.000
#&gt; SRR975589     5  0.3482      0.813 0.012 0.000 0.168 0.008 0.812
#&gt; SRR975590     5  0.0404      0.881 0.012 0.000 0.000 0.000 0.988
#&gt; SRR975591     3  0.3242      0.994 0.000 0.000 0.784 0.000 0.216
#&gt; SRR975592     5  0.3399      0.809 0.012 0.000 0.172 0.004 0.812
#&gt; SRR975593     5  0.3482      0.813 0.012 0.000 0.168 0.008 0.812
#&gt; SRR975594     3  0.3242      0.994 0.000 0.000 0.784 0.000 0.216
#&gt; SRR975595     5  0.0404      0.881 0.012 0.000 0.000 0.000 0.988
#&gt; SRR975597     5  0.0404      0.881 0.012 0.000 0.000 0.000 0.988
#&gt; SRR975596     1  0.2616      0.893 0.880 0.000 0.000 0.100 0.020
#&gt; SRR975598     5  0.0404      0.881 0.012 0.000 0.000 0.000 0.988
#&gt; SRR975599     1  0.7213      0.120 0.448 0.000 0.028 0.248 0.276
#&gt; SRR975600     3  0.3491      0.977 0.000 0.000 0.768 0.004 0.228
#&gt; SRR975601     3  0.3274      0.992 0.000 0.000 0.780 0.000 0.220
#&gt; SRR975602     1  0.0992      0.862 0.968 0.000 0.000 0.008 0.024
#&gt; SRR975603     3  0.3242      0.994 0.000 0.000 0.784 0.000 0.216
#&gt; SRR975604     3  0.3242      0.994 0.000 0.000 0.784 0.000 0.216
</code></pre>

<script>
$('#tab-CV-mclust-get-classes-4-a').parent().next().next().hide();
$('#tab-CV-mclust-get-classes-4-a').click(function(){
  $('#tab-CV-mclust-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-mclust-get-classes-5'>
<p><a id='tab-CV-mclust-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3    p4    p5    p6
#&gt; SRR975551     1  0.1075      0.894 0.952 0.000 0.000 0.048 0.000 0.000
#&gt; SRR975552     1  0.2121      0.890 0.892 0.000 0.000 0.096 0.012 0.000
#&gt; SRR975554     1  0.1267      0.916 0.940 0.000 0.000 0.060 0.000 0.000
#&gt; SRR975553     2  0.2664      0.838 0.000 0.816 0.000 0.000 0.184 0.000
#&gt; SRR975555     1  0.0713      0.916 0.972 0.000 0.000 0.028 0.000 0.000
#&gt; SRR975556     5  0.4189      0.163 0.000 0.020 0.000 0.376 0.604 0.000
#&gt; SRR975557     4  0.3954      0.664 0.056 0.000 0.000 0.740 0.204 0.000
#&gt; SRR975558     4  0.1204      0.759 0.056 0.000 0.000 0.944 0.000 0.000
#&gt; SRR975559     1  0.2020      0.890 0.896 0.000 0.000 0.096 0.008 0.000
#&gt; SRR975560     4  0.2978      0.729 0.056 0.012 0.000 0.860 0.072 0.000
#&gt; SRR975561     5  0.6666      0.364 0.052 0.176 0.000 0.384 0.388 0.000
#&gt; SRR975562     1  0.0937      0.917 0.960 0.000 0.000 0.040 0.000 0.000
#&gt; SRR975563     2  0.1765      0.892 0.000 0.904 0.000 0.000 0.096 0.000
#&gt; SRR975564     1  0.1267      0.915 0.940 0.000 0.000 0.060 0.000 0.000
#&gt; SRR975565     1  0.0458      0.918 0.984 0.000 0.000 0.016 0.000 0.000
#&gt; SRR975566     1  0.0858      0.917 0.968 0.000 0.000 0.028 0.004 0.000
#&gt; SRR975567     4  0.1204      0.759 0.056 0.000 0.000 0.944 0.000 0.000
#&gt; SRR975568     1  0.1075      0.918 0.952 0.000 0.000 0.048 0.000 0.000
#&gt; SRR975569     2  0.0547      0.900 0.000 0.980 0.000 0.000 0.020 0.000
#&gt; SRR975570     2  0.0632      0.897 0.000 0.976 0.000 0.000 0.024 0.000
#&gt; SRR975571     2  0.2664      0.838 0.000 0.816 0.000 0.000 0.184 0.000
#&gt; SRR975572     2  0.0632      0.897 0.000 0.976 0.000 0.000 0.024 0.000
#&gt; SRR975573     2  0.0547      0.901 0.000 0.980 0.000 0.000 0.020 0.000
#&gt; SRR975574     5  0.5095      0.506 0.000 0.312 0.000 0.104 0.584 0.000
#&gt; SRR975575     2  0.0632      0.897 0.000 0.976 0.000 0.000 0.024 0.000
#&gt; SRR975576     2  0.1765      0.892 0.000 0.904 0.000 0.000 0.096 0.000
#&gt; SRR975577     2  0.2219      0.874 0.000 0.864 0.000 0.000 0.136 0.000
#&gt; SRR975578     2  0.3198      0.731 0.000 0.740 0.000 0.000 0.260 0.000
#&gt; SRR975579     4  0.5725      0.450 0.052 0.064 0.000 0.548 0.336 0.000
#&gt; SRR975580     4  0.3809      0.485 0.008 0.012 0.000 0.716 0.264 0.000
#&gt; SRR975581     2  0.1141      0.893 0.000 0.948 0.000 0.000 0.052 0.000
#&gt; SRR975582     2  0.1910      0.887 0.000 0.892 0.000 0.000 0.108 0.000
#&gt; SRR975583     2  0.0632      0.897 0.000 0.976 0.000 0.000 0.024 0.000
#&gt; SRR975584     2  0.2219      0.874 0.000 0.864 0.000 0.000 0.136 0.000
#&gt; SRR975585     2  0.0632      0.897 0.000 0.976 0.000 0.000 0.024 0.000
#&gt; SRR975586     5  0.6057      0.573 0.008 0.268 0.000 0.240 0.484 0.000
#&gt; SRR975587     3  0.0713      0.968 0.000 0.000 0.972 0.000 0.028 0.000
#&gt; SRR975588     2  0.0632      0.897 0.000 0.976 0.000 0.000 0.024 0.000
#&gt; SRR975589     6  0.4225      0.780 0.000 0.000 0.192 0.064 0.008 0.736
#&gt; SRR975590     6  0.0363      0.855 0.000 0.000 0.012 0.000 0.000 0.988
#&gt; SRR975591     3  0.0000      0.969 0.000 0.000 1.000 0.000 0.000 0.000
#&gt; SRR975592     6  0.3337      0.738 0.000 0.000 0.260 0.000 0.004 0.736
#&gt; SRR975593     6  0.4172      0.779 0.000 0.000 0.200 0.056 0.008 0.736
#&gt; SRR975594     3  0.0713      0.968 0.000 0.000 0.972 0.000 0.028 0.000
#&gt; SRR975595     6  0.0260      0.853 0.000 0.000 0.000 0.000 0.008 0.992
#&gt; SRR975597     6  0.0260      0.853 0.000 0.000 0.000 0.000 0.008 0.992
#&gt; SRR975596     1  0.1812      0.903 0.912 0.000 0.000 0.080 0.008 0.000
#&gt; SRR975598     6  0.0405      0.851 0.004 0.000 0.000 0.000 0.008 0.988
#&gt; SRR975599     1  0.5204      0.258 0.536 0.000 0.000 0.364 0.000 0.100
#&gt; SRR975600     3  0.1858      0.871 0.000 0.000 0.904 0.000 0.004 0.092
#&gt; SRR975601     3  0.0713      0.968 0.000 0.000 0.972 0.000 0.028 0.000
#&gt; SRR975602     1  0.1141      0.896 0.948 0.000 0.000 0.052 0.000 0.000
#&gt; SRR975603     3  0.0000      0.969 0.000 0.000 1.000 0.000 0.000 0.000
#&gt; SRR975604     3  0.0000      0.969 0.000 0.000 1.000 0.000 0.000 0.000
</code></pre>

<script>
$('#tab-CV-mclust-get-classes-5-a').parent().next().next().hide();
$('#tab-CV-mclust-get-classes-5-a').click(function(){
  $('#tab-CV-mclust-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-CV-mclust-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-CV-mclust-consensus-heatmap'>
<ul>
<li><a href='#tab-CV-mclust-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-CV-mclust-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-CV-mclust-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-CV-mclust-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-CV-mclust-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-CV-mclust-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-consensus-heatmap-1-1.png" alt="plot of chunk tab-CV-mclust-consensus-heatmap-1"/></p>

</div>
<div id='tab-CV-mclust-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-consensus-heatmap-2-1.png" alt="plot of chunk tab-CV-mclust-consensus-heatmap-2"/></p>

</div>
<div id='tab-CV-mclust-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-consensus-heatmap-3-1.png" alt="plot of chunk tab-CV-mclust-consensus-heatmap-3"/></p>

</div>
<div id='tab-CV-mclust-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-consensus-heatmap-4-1.png" alt="plot of chunk tab-CV-mclust-consensus-heatmap-4"/></p>

</div>
<div id='tab-CV-mclust-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-consensus-heatmap-5-1.png" alt="plot of chunk tab-CV-mclust-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-CV-mclust-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-CV-mclust-membership-heatmap'>
<ul>
<li><a href='#tab-CV-mclust-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-CV-mclust-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-CV-mclust-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-CV-mclust-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-CV-mclust-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-CV-mclust-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-membership-heatmap-1-1.png" alt="plot of chunk tab-CV-mclust-membership-heatmap-1"/></p>

</div>
<div id='tab-CV-mclust-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-membership-heatmap-2-1.png" alt="plot of chunk tab-CV-mclust-membership-heatmap-2"/></p>

</div>
<div id='tab-CV-mclust-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-membership-heatmap-3-1.png" alt="plot of chunk tab-CV-mclust-membership-heatmap-3"/></p>

</div>
<div id='tab-CV-mclust-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-membership-heatmap-4-1.png" alt="plot of chunk tab-CV-mclust-membership-heatmap-4"/></p>

</div>
<div id='tab-CV-mclust-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-membership-heatmap-5-1.png" alt="plot of chunk tab-CV-mclust-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-CV-mclust-get-signatures' ).tabs();
} );
</script>
<div id='tabs-CV-mclust-get-signatures'>
<ul>
<li><a href='#tab-CV-mclust-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-CV-mclust-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-CV-mclust-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-CV-mclust-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-CV-mclust-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-CV-mclust-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-get-signatures-1-1.png" alt="plot of chunk tab-CV-mclust-get-signatures-1"/></p>

</div>
<div id='tab-CV-mclust-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-get-signatures-2-1.png" alt="plot of chunk tab-CV-mclust-get-signatures-2"/></p>

</div>
<div id='tab-CV-mclust-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-get-signatures-3-1.png" alt="plot of chunk tab-CV-mclust-get-signatures-3"/></p>

</div>
<div id='tab-CV-mclust-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-get-signatures-4-1.png" alt="plot of chunk tab-CV-mclust-get-signatures-4"/></p>

</div>
<div id='tab-CV-mclust-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-get-signatures-5-1.png" alt="plot of chunk tab-CV-mclust-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-CV-mclust-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-CV-mclust-get-signatures-no-scale'>
<ul>
<li><a href='#tab-CV-mclust-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-CV-mclust-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-CV-mclust-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-CV-mclust-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-CV-mclust-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-CV-mclust-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-CV-mclust-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-CV-mclust-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-CV-mclust-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-CV-mclust-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-CV-mclust-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-CV-mclust-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-CV-mclust-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-CV-mclust-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-CV-mclust-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk CV-mclust-signature_compare](figure_cola/CV-mclust-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-CV-mclust-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-CV-mclust-dimension-reduction'>
<ul>
<li><a href='#tab-CV-mclust-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-CV-mclust-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-CV-mclust-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-CV-mclust-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-CV-mclust-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-CV-mclust-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-dimension-reduction-1-1.png" alt="plot of chunk tab-CV-mclust-dimension-reduction-1"/></p>

</div>
<div id='tab-CV-mclust-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-dimension-reduction-2-1.png" alt="plot of chunk tab-CV-mclust-dimension-reduction-2"/></p>

</div>
<div id='tab-CV-mclust-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-dimension-reduction-3-1.png" alt="plot of chunk tab-CV-mclust-dimension-reduction-3"/></p>

</div>
<div id='tab-CV-mclust-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-dimension-reduction-4-1.png" alt="plot of chunk tab-CV-mclust-dimension-reduction-4"/></p>

</div>
<div id='tab-CV-mclust-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-dimension-reduction-5-1.png" alt="plot of chunk tab-CV-mclust-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk CV-mclust-collect-classes](figure_cola/CV-mclust-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### CV:NMF**






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["CV", "NMF"]
# you can also extract it by
# res = res_list["CV:NMF"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 17171 rows and 54 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'CV' method.
#>   Subgroups are detected by 'NMF' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 2.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk CV-NMF-collect-plots](figure_cola/CV-NMF-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk CV-NMF-select-partition-number](figure_cola/CV-NMF-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 1.000           0.975       0.990         0.5092 0.491   0.491
#> 3 3 0.862           0.857       0.930         0.2541 0.840   0.682
#> 4 4 0.851           0.836       0.921         0.0893 0.892   0.725
#> 5 5 0.857           0.787       0.895         0.0834 0.923   0.762
#> 6 6 0.732           0.550       0.741         0.0657 0.924   0.703
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 2
```


Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-CV-NMF-get-classes' ).tabs();
} );
</script>
<div id='tabs-CV-NMF-get-classes'>
<ul>
<li><a href='#tab-CV-NMF-get-classes-1'>k = 2</a></li>
<li><a href='#tab-CV-NMF-get-classes-2'>k = 3</a></li>
<li><a href='#tab-CV-NMF-get-classes-3'>k = 4</a></li>
<li><a href='#tab-CV-NMF-get-classes-4'>k = 5</a></li>
<li><a href='#tab-CV-NMF-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-CV-NMF-get-classes-1'>
<p><a id='tab-CV-NMF-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2
#&gt; SRR975551     1   0.000      0.984 1.000 0.000
#&gt; SRR975552     1   0.204      0.954 0.968 0.032
#&gt; SRR975554     1   0.000      0.984 1.000 0.000
#&gt; SRR975553     2   0.000      0.995 0.000 1.000
#&gt; SRR975555     1   0.000      0.984 1.000 0.000
#&gt; SRR975556     2   0.000      0.995 0.000 1.000
#&gt; SRR975557     2   0.000      0.995 0.000 1.000
#&gt; SRR975558     1   0.966      0.350 0.608 0.392
#&gt; SRR975559     1   0.000      0.984 1.000 0.000
#&gt; SRR975560     2   0.000      0.995 0.000 1.000
#&gt; SRR975561     2   0.000      0.995 0.000 1.000
#&gt; SRR975562     1   0.000      0.984 1.000 0.000
#&gt; SRR975563     2   0.000      0.995 0.000 1.000
#&gt; SRR975564     1   0.000      0.984 1.000 0.000
#&gt; SRR975565     1   0.000      0.984 1.000 0.000
#&gt; SRR975566     1   0.000      0.984 1.000 0.000
#&gt; SRR975567     2   0.529      0.860 0.120 0.880
#&gt; SRR975568     1   0.000      0.984 1.000 0.000
#&gt; SRR975569     2   0.000      0.995 0.000 1.000
#&gt; SRR975570     2   0.000      0.995 0.000 1.000
#&gt; SRR975571     2   0.000      0.995 0.000 1.000
#&gt; SRR975572     2   0.000      0.995 0.000 1.000
#&gt; SRR975573     2   0.000      0.995 0.000 1.000
#&gt; SRR975574     2   0.000      0.995 0.000 1.000
#&gt; SRR975575     2   0.000      0.995 0.000 1.000
#&gt; SRR975576     2   0.000      0.995 0.000 1.000
#&gt; SRR975577     2   0.000      0.995 0.000 1.000
#&gt; SRR975578     2   0.000      0.995 0.000 1.000
#&gt; SRR975579     2   0.000      0.995 0.000 1.000
#&gt; SRR975580     2   0.000      0.995 0.000 1.000
#&gt; SRR975581     2   0.000      0.995 0.000 1.000
#&gt; SRR975582     2   0.000      0.995 0.000 1.000
#&gt; SRR975583     2   0.000      0.995 0.000 1.000
#&gt; SRR975584     2   0.000      0.995 0.000 1.000
#&gt; SRR975585     2   0.000      0.995 0.000 1.000
#&gt; SRR975586     2   0.000      0.995 0.000 1.000
#&gt; SRR975587     1   0.000      0.984 1.000 0.000
#&gt; SRR975588     2   0.000      0.995 0.000 1.000
#&gt; SRR975589     1   0.000      0.984 1.000 0.000
#&gt; SRR975590     1   0.000      0.984 1.000 0.000
#&gt; SRR975591     1   0.000      0.984 1.000 0.000
#&gt; SRR975592     1   0.000      0.984 1.000 0.000
#&gt; SRR975593     1   0.000      0.984 1.000 0.000
#&gt; SRR975594     1   0.000      0.984 1.000 0.000
#&gt; SRR975595     1   0.000      0.984 1.000 0.000
#&gt; SRR975597     1   0.000      0.984 1.000 0.000
#&gt; SRR975596     1   0.000      0.984 1.000 0.000
#&gt; SRR975598     1   0.000      0.984 1.000 0.000
#&gt; SRR975599     1   0.000      0.984 1.000 0.000
#&gt; SRR975600     1   0.000      0.984 1.000 0.000
#&gt; SRR975601     1   0.000      0.984 1.000 0.000
#&gt; SRR975602     1   0.000      0.984 1.000 0.000
#&gt; SRR975603     1   0.000      0.984 1.000 0.000
#&gt; SRR975604     1   0.000      0.984 1.000 0.000
</code></pre>

<script>
$('#tab-CV-NMF-get-classes-1-a').parent().next().next().hide();
$('#tab-CV-NMF-get-classes-1-a').click(function(){
  $('#tab-CV-NMF-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-NMF-get-classes-2'>
<p><a id='tab-CV-NMF-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3
#&gt; SRR975551     1  0.2356      0.890 0.928 0.000 0.072
#&gt; SRR975552     1  0.2356      0.890 0.928 0.000 0.072
#&gt; SRR975554     1  0.2356      0.890 0.928 0.000 0.072
#&gt; SRR975553     2  0.0000      0.983 0.000 1.000 0.000
#&gt; SRR975555     1  0.2356      0.890 0.928 0.000 0.072
#&gt; SRR975556     2  0.0000      0.983 0.000 1.000 0.000
#&gt; SRR975557     2  0.4291      0.815 0.180 0.820 0.000
#&gt; SRR975558     1  0.0000      0.853 1.000 0.000 0.000
#&gt; SRR975559     1  0.0000      0.853 1.000 0.000 0.000
#&gt; SRR975560     2  0.4002      0.821 0.160 0.840 0.000
#&gt; SRR975561     2  0.0000      0.983 0.000 1.000 0.000
#&gt; SRR975562     1  0.2356      0.890 0.928 0.000 0.072
#&gt; SRR975563     2  0.0000      0.983 0.000 1.000 0.000
#&gt; SRR975564     1  0.2356      0.890 0.928 0.000 0.072
#&gt; SRR975565     1  0.2356      0.890 0.928 0.000 0.072
#&gt; SRR975566     1  0.1289      0.872 0.968 0.000 0.032
#&gt; SRR975567     1  0.0000      0.853 1.000 0.000 0.000
#&gt; SRR975568     1  0.2356      0.890 0.928 0.000 0.072
#&gt; SRR975569     2  0.0000      0.983 0.000 1.000 0.000
#&gt; SRR975570     2  0.0000      0.983 0.000 1.000 0.000
#&gt; SRR975571     2  0.0000      0.983 0.000 1.000 0.000
#&gt; SRR975572     2  0.0000      0.983 0.000 1.000 0.000
#&gt; SRR975573     2  0.0000      0.983 0.000 1.000 0.000
#&gt; SRR975574     2  0.0000      0.983 0.000 1.000 0.000
#&gt; SRR975575     2  0.0000      0.983 0.000 1.000 0.000
#&gt; SRR975576     2  0.0000      0.983 0.000 1.000 0.000
#&gt; SRR975577     2  0.0000      0.983 0.000 1.000 0.000
#&gt; SRR975578     2  0.0000      0.983 0.000 1.000 0.000
#&gt; SRR975579     2  0.2356      0.926 0.072 0.928 0.000
#&gt; SRR975580     2  0.0000      0.983 0.000 1.000 0.000
#&gt; SRR975581     2  0.0000      0.983 0.000 1.000 0.000
#&gt; SRR975582     2  0.0000      0.983 0.000 1.000 0.000
#&gt; SRR975583     2  0.0000      0.983 0.000 1.000 0.000
#&gt; SRR975584     2  0.0000      0.983 0.000 1.000 0.000
#&gt; SRR975585     2  0.0000      0.983 0.000 1.000 0.000
#&gt; SRR975586     2  0.0000      0.983 0.000 1.000 0.000
#&gt; SRR975587     3  0.0000      0.846 0.000 0.000 1.000
#&gt; SRR975588     2  0.0000      0.983 0.000 1.000 0.000
#&gt; SRR975589     1  0.5216      0.686 0.740 0.000 0.260
#&gt; SRR975590     3  0.5882      0.430 0.348 0.000 0.652
#&gt; SRR975591     3  0.0237      0.843 0.004 0.000 0.996
#&gt; SRR975592     3  0.2261      0.805 0.068 0.000 0.932
#&gt; SRR975593     1  0.5678      0.590 0.684 0.000 0.316
#&gt; SRR975594     3  0.0000      0.846 0.000 0.000 1.000
#&gt; SRR975595     3  0.6062      0.342 0.384 0.000 0.616
#&gt; SRR975597     3  0.6168      0.255 0.412 0.000 0.588
#&gt; SRR975596     1  0.0000      0.853 1.000 0.000 0.000
#&gt; SRR975598     1  0.6274      0.186 0.544 0.000 0.456
#&gt; SRR975599     1  0.5650      0.598 0.688 0.000 0.312
#&gt; SRR975600     3  0.0000      0.846 0.000 0.000 1.000
#&gt; SRR975601     3  0.0000      0.846 0.000 0.000 1.000
#&gt; SRR975602     1  0.2356      0.890 0.928 0.000 0.072
#&gt; SRR975603     3  0.0000      0.846 0.000 0.000 1.000
#&gt; SRR975604     3  0.0000      0.846 0.000 0.000 1.000
</code></pre>

<script>
$('#tab-CV-NMF-get-classes-2-a').parent().next().next().hide();
$('#tab-CV-NMF-get-classes-2-a').click(function(){
  $('#tab-CV-NMF-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-NMF-get-classes-3'>
<p><a id='tab-CV-NMF-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3    p4
#&gt; SRR975551     1  0.0000      0.791 1.000 0.000 0.000 0.000
#&gt; SRR975552     1  0.0000      0.791 1.000 0.000 0.000 0.000
#&gt; SRR975554     1  0.0000      0.791 1.000 0.000 0.000 0.000
#&gt; SRR975553     2  0.0000      0.975 0.000 1.000 0.000 0.000
#&gt; SRR975555     1  0.2469      0.779 0.892 0.000 0.000 0.108
#&gt; SRR975556     2  0.0000      0.975 0.000 1.000 0.000 0.000
#&gt; SRR975557     4  0.0000      0.736 0.000 0.000 0.000 1.000
#&gt; SRR975558     1  0.3688      0.704 0.792 0.000 0.000 0.208
#&gt; SRR975559     4  0.4804      0.491 0.384 0.000 0.000 0.616
#&gt; SRR975560     2  0.2761      0.869 0.048 0.904 0.000 0.048
#&gt; SRR975561     2  0.4916      0.273 0.000 0.576 0.000 0.424
#&gt; SRR975562     1  0.0000      0.791 1.000 0.000 0.000 0.000
#&gt; SRR975563     2  0.0000      0.975 0.000 1.000 0.000 0.000
#&gt; SRR975564     1  0.2760      0.771 0.872 0.000 0.000 0.128
#&gt; SRR975565     1  0.2011      0.786 0.920 0.000 0.000 0.080
#&gt; SRR975566     1  0.1211      0.774 0.960 0.000 0.000 0.040
#&gt; SRR975567     4  0.3074      0.725 0.152 0.000 0.000 0.848
#&gt; SRR975568     1  0.2760      0.771 0.872 0.000 0.000 0.128
#&gt; SRR975569     2  0.0000      0.975 0.000 1.000 0.000 0.000
#&gt; SRR975570     2  0.0000      0.975 0.000 1.000 0.000 0.000
#&gt; SRR975571     2  0.0000      0.975 0.000 1.000 0.000 0.000
#&gt; SRR975572     2  0.0000      0.975 0.000 1.000 0.000 0.000
#&gt; SRR975573     2  0.0000      0.975 0.000 1.000 0.000 0.000
#&gt; SRR975574     2  0.0000      0.975 0.000 1.000 0.000 0.000
#&gt; SRR975575     2  0.0000      0.975 0.000 1.000 0.000 0.000
#&gt; SRR975576     2  0.0000      0.975 0.000 1.000 0.000 0.000
#&gt; SRR975577     2  0.0000      0.975 0.000 1.000 0.000 0.000
#&gt; SRR975578     2  0.0000      0.975 0.000 1.000 0.000 0.000
#&gt; SRR975579     4  0.2760      0.662 0.000 0.128 0.000 0.872
#&gt; SRR975580     2  0.0000      0.975 0.000 1.000 0.000 0.000
#&gt; SRR975581     2  0.0000      0.975 0.000 1.000 0.000 0.000
#&gt; SRR975582     2  0.0000      0.975 0.000 1.000 0.000 0.000
#&gt; SRR975583     2  0.0000      0.975 0.000 1.000 0.000 0.000
#&gt; SRR975584     2  0.0000      0.975 0.000 1.000 0.000 0.000
#&gt; SRR975585     2  0.0000      0.975 0.000 1.000 0.000 0.000
#&gt; SRR975586     2  0.0000      0.975 0.000 1.000 0.000 0.000
#&gt; SRR975587     3  0.0000      0.998 0.000 0.000 1.000 0.000
#&gt; SRR975588     2  0.0000      0.975 0.000 1.000 0.000 0.000
#&gt; SRR975589     1  0.4017      0.770 0.828 0.000 0.044 0.128
#&gt; SRR975590     1  0.4985      0.324 0.532 0.000 0.468 0.000
#&gt; SRR975591     3  0.0000      0.998 0.000 0.000 1.000 0.000
#&gt; SRR975592     3  0.0469      0.982 0.012 0.000 0.988 0.000
#&gt; SRR975593     1  0.4720      0.662 0.720 0.000 0.264 0.016
#&gt; SRR975594     3  0.0000      0.998 0.000 0.000 1.000 0.000
#&gt; SRR975595     1  0.4898      0.448 0.584 0.000 0.416 0.000
#&gt; SRR975597     1  0.4830      0.492 0.608 0.000 0.392 0.000
#&gt; SRR975596     1  0.4933      0.216 0.568 0.000 0.000 0.432
#&gt; SRR975598     1  0.3486      0.719 0.812 0.000 0.188 0.000
#&gt; SRR975599     1  0.1389      0.782 0.952 0.000 0.048 0.000
#&gt; SRR975600     3  0.0000      0.998 0.000 0.000 1.000 0.000
#&gt; SRR975601     3  0.0000      0.998 0.000 0.000 1.000 0.000
#&gt; SRR975602     1  0.0000      0.791 1.000 0.000 0.000 0.000
#&gt; SRR975603     3  0.0000      0.998 0.000 0.000 1.000 0.000
#&gt; SRR975604     3  0.0000      0.998 0.000 0.000 1.000 0.000
</code></pre>

<script>
$('#tab-CV-NMF-get-classes-3-a').parent().next().next().hide();
$('#tab-CV-NMF-get-classes-3-a').click(function(){
  $('#tab-CV-NMF-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-NMF-get-classes-4'>
<p><a id='tab-CV-NMF-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3    p4    p5
#&gt; SRR975551     1  0.0000     0.8137 1.000 0.000 0.000 0.000 0.000
#&gt; SRR975552     1  0.0000     0.8137 1.000 0.000 0.000 0.000 0.000
#&gt; SRR975554     1  0.2648     0.6866 0.848 0.000 0.000 0.000 0.152
#&gt; SRR975553     2  0.1851     0.9377 0.000 0.912 0.000 0.000 0.088
#&gt; SRR975555     5  0.4201     0.3772 0.408 0.000 0.000 0.000 0.592
#&gt; SRR975556     2  0.0162     0.9488 0.000 0.996 0.000 0.000 0.004
#&gt; SRR975557     4  0.0000     0.7432 0.000 0.000 0.000 1.000 0.000
#&gt; SRR975558     5  0.2130     0.7841 0.080 0.012 0.000 0.000 0.908
#&gt; SRR975559     4  0.3932     0.5119 0.328 0.000 0.000 0.672 0.000
#&gt; SRR975560     2  0.4703     0.6513 0.024 0.732 0.000 0.212 0.032
#&gt; SRR975561     4  0.2068     0.7012 0.000 0.092 0.000 0.904 0.004
#&gt; SRR975562     1  0.0000     0.8137 1.000 0.000 0.000 0.000 0.000
#&gt; SRR975563     2  0.0162     0.9488 0.000 0.996 0.000 0.000 0.004
#&gt; SRR975564     5  0.1965     0.7949 0.096 0.000 0.000 0.000 0.904
#&gt; SRR975565     1  0.3039     0.6585 0.808 0.000 0.000 0.000 0.192
#&gt; SRR975566     1  0.4227     0.0616 0.580 0.000 0.000 0.000 0.420
#&gt; SRR975567     4  0.4828     0.1765 0.012 0.008 0.000 0.572 0.408
#&gt; SRR975568     5  0.2020     0.7955 0.100 0.000 0.000 0.000 0.900
#&gt; SRR975569     2  0.0609     0.9475 0.000 0.980 0.000 0.000 0.020
#&gt; SRR975570     2  0.0162     0.9488 0.000 0.996 0.000 0.000 0.004
#&gt; SRR975571     2  0.1851     0.9377 0.000 0.912 0.000 0.000 0.088
#&gt; SRR975572     2  0.0000     0.9489 0.000 1.000 0.000 0.000 0.000
#&gt; SRR975573     2  0.1851     0.9377 0.000 0.912 0.000 0.000 0.088
#&gt; SRR975574     2  0.1851     0.9377 0.000 0.912 0.000 0.000 0.088
#&gt; SRR975575     2  0.0000     0.9489 0.000 1.000 0.000 0.000 0.000
#&gt; SRR975576     2  0.0162     0.9488 0.000 0.996 0.000 0.000 0.004
#&gt; SRR975577     2  0.1792     0.9388 0.000 0.916 0.000 0.000 0.084
#&gt; SRR975578     2  0.1792     0.9388 0.000 0.916 0.000 0.000 0.084
#&gt; SRR975579     4  0.0000     0.7432 0.000 0.000 0.000 1.000 0.000
#&gt; SRR975580     2  0.1792     0.9388 0.000 0.916 0.000 0.000 0.084
#&gt; SRR975581     2  0.0162     0.9488 0.000 0.996 0.000 0.000 0.004
#&gt; SRR975582     2  0.1851     0.9377 0.000 0.912 0.000 0.000 0.088
#&gt; SRR975583     2  0.0162     0.9488 0.000 0.996 0.000 0.000 0.004
#&gt; SRR975584     2  0.1851     0.9377 0.000 0.912 0.000 0.000 0.088
#&gt; SRR975585     2  0.0162     0.9488 0.000 0.996 0.000 0.000 0.004
#&gt; SRR975586     2  0.0162     0.9488 0.000 0.996 0.000 0.000 0.004
#&gt; SRR975587     3  0.0000     0.8969 0.000 0.000 1.000 0.000 0.000
#&gt; SRR975588     2  0.0162     0.9488 0.000 0.996 0.000 0.000 0.004
#&gt; SRR975589     5  0.2124     0.7956 0.096 0.000 0.004 0.000 0.900
#&gt; SRR975590     1  0.3177     0.7384 0.792 0.000 0.208 0.000 0.000
#&gt; SRR975591     3  0.0000     0.8969 0.000 0.000 1.000 0.000 0.000
#&gt; SRR975592     3  0.3003     0.7413 0.000 0.000 0.812 0.000 0.188
#&gt; SRR975593     5  0.4069     0.7098 0.096 0.000 0.112 0.000 0.792
#&gt; SRR975594     3  0.0000     0.8969 0.000 0.000 1.000 0.000 0.000
#&gt; SRR975595     1  0.3366     0.7138 0.768 0.000 0.232 0.000 0.000
#&gt; SRR975597     1  0.3143     0.7405 0.796 0.000 0.204 0.000 0.000
#&gt; SRR975596     5  0.6137     0.0714 0.132 0.000 0.000 0.392 0.476
#&gt; SRR975598     1  0.2329     0.7851 0.876 0.000 0.124 0.000 0.000
#&gt; SRR975599     1  0.0162     0.8137 0.996 0.000 0.004 0.000 0.000
#&gt; SRR975600     3  0.4287     0.2579 0.000 0.000 0.540 0.000 0.460
#&gt; SRR975601     3  0.0000     0.8969 0.000 0.000 1.000 0.000 0.000
#&gt; SRR975602     1  0.0000     0.8137 1.000 0.000 0.000 0.000 0.000
#&gt; SRR975603     3  0.0000     0.8969 0.000 0.000 1.000 0.000 0.000
#&gt; SRR975604     3  0.0000     0.8969 0.000 0.000 1.000 0.000 0.000
</code></pre>

<script>
$('#tab-CV-NMF-get-classes-4-a').parent().next().next().hide();
$('#tab-CV-NMF-get-classes-4-a').click(function(){
  $('#tab-CV-NMF-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-NMF-get-classes-5'>
<p><a id='tab-CV-NMF-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3    p4    p5    p6
#&gt; SRR975551     1  0.0000     0.7900 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR975552     1  0.0260     0.7908 0.992 0.000 0.000 0.000 0.008 0.000
#&gt; SRR975554     1  0.2340     0.7254 0.852 0.000 0.000 0.000 0.148 0.000
#&gt; SRR975553     2  0.0000     0.6605 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR975555     5  0.3912     0.4915 0.224 0.000 0.000 0.000 0.732 0.044
#&gt; SRR975556     6  0.3864     0.1211 0.000 0.480 0.000 0.000 0.000 0.520
#&gt; SRR975557     4  0.0000     0.7541 0.000 0.000 0.000 1.000 0.000 0.000
#&gt; SRR975558     5  0.0547     0.7234 0.000 0.000 0.000 0.000 0.980 0.020
#&gt; SRR975559     4  0.4074     0.6559 0.140 0.000 0.000 0.752 0.000 0.108
#&gt; SRR975560     6  0.4779     0.0911 0.000 0.308 0.000 0.016 0.044 0.632
#&gt; SRR975561     4  0.2841     0.6830 0.000 0.012 0.000 0.824 0.000 0.164
#&gt; SRR975562     1  0.3916     0.6578 0.680 0.000 0.000 0.000 0.020 0.300
#&gt; SRR975563     6  0.3864     0.1211 0.000 0.480 0.000 0.000 0.000 0.520
#&gt; SRR975564     5  0.0000     0.7232 0.000 0.000 0.000 0.000 1.000 0.000
#&gt; SRR975565     1  0.2941     0.6817 0.780 0.000 0.000 0.000 0.220 0.000
#&gt; SRR975566     1  0.5168     0.2672 0.552 0.000 0.000 0.004 0.360 0.084
#&gt; SRR975567     4  0.5911     0.3202 0.000 0.000 0.000 0.456 0.228 0.316
#&gt; SRR975568     5  0.0260     0.7208 0.000 0.000 0.000 0.000 0.992 0.008
#&gt; SRR975569     2  0.2996     0.5105 0.000 0.772 0.000 0.000 0.000 0.228
#&gt; SRR975570     2  0.3330     0.4456 0.000 0.716 0.000 0.000 0.000 0.284
#&gt; SRR975571     2  0.0000     0.6605 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR975572     2  0.3737     0.2319 0.000 0.608 0.000 0.000 0.000 0.392
#&gt; SRR975573     2  0.0000     0.6605 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR975574     2  0.0146     0.6603 0.000 0.996 0.000 0.000 0.000 0.004
#&gt; SRR975575     2  0.3774     0.1806 0.000 0.592 0.000 0.000 0.000 0.408
#&gt; SRR975576     2  0.3862    -0.1501 0.000 0.524 0.000 0.000 0.000 0.476
#&gt; SRR975577     2  0.0000     0.6605 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR975578     2  0.0146     0.6603 0.000 0.996 0.000 0.000 0.000 0.004
#&gt; SRR975579     4  0.0000     0.7541 0.000 0.000 0.000 1.000 0.000 0.000
#&gt; SRR975580     2  0.1967     0.5442 0.012 0.904 0.000 0.000 0.000 0.084
#&gt; SRR975581     2  0.3727     0.2405 0.000 0.612 0.000 0.000 0.000 0.388
#&gt; SRR975582     2  0.0000     0.6605 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR975583     6  0.3868     0.0591 0.000 0.496 0.000 0.000 0.000 0.504
#&gt; SRR975584     2  0.0632     0.6376 0.000 0.976 0.000 0.000 0.000 0.024
#&gt; SRR975585     2  0.3823     0.0661 0.000 0.564 0.000 0.000 0.000 0.436
#&gt; SRR975586     6  0.3864     0.1211 0.000 0.480 0.000 0.000 0.000 0.520
#&gt; SRR975587     3  0.0000     0.9615 0.000 0.000 1.000 0.000 0.000 0.000
#&gt; SRR975588     2  0.3482     0.3970 0.000 0.684 0.000 0.000 0.000 0.316
#&gt; SRR975589     5  0.2941     0.6429 0.000 0.000 0.000 0.000 0.780 0.220
#&gt; SRR975590     1  0.2219     0.7713 0.864 0.000 0.136 0.000 0.000 0.000
#&gt; SRR975591     3  0.0000     0.9615 0.000 0.000 1.000 0.000 0.000 0.000
#&gt; SRR975592     3  0.2871     0.7160 0.000 0.000 0.804 0.000 0.192 0.004
#&gt; SRR975593     5  0.4585     0.5849 0.000 0.000 0.068 0.000 0.648 0.284
#&gt; SRR975594     3  0.0000     0.9615 0.000 0.000 1.000 0.000 0.000 0.000
#&gt; SRR975595     1  0.4386     0.7211 0.708 0.000 0.200 0.000 0.000 0.092
#&gt; SRR975597     1  0.3971     0.7432 0.748 0.000 0.184 0.000 0.000 0.068
#&gt; SRR975596     6  0.6641    -0.5347 0.032 0.000 0.000 0.248 0.336 0.384
#&gt; SRR975598     1  0.3747     0.7757 0.784 0.000 0.104 0.000 0.000 0.112
#&gt; SRR975599     1  0.2703     0.7661 0.824 0.000 0.000 0.000 0.004 0.172
#&gt; SRR975600     5  0.4184    -0.0456 0.000 0.000 0.484 0.000 0.504 0.012
#&gt; SRR975601     3  0.0000     0.9615 0.000 0.000 1.000 0.000 0.000 0.000
#&gt; SRR975602     1  0.1075     0.7896 0.952 0.000 0.000 0.000 0.000 0.048
#&gt; SRR975603     3  0.0000     0.9615 0.000 0.000 1.000 0.000 0.000 0.000
#&gt; SRR975604     3  0.0000     0.9615 0.000 0.000 1.000 0.000 0.000 0.000
</code></pre>

<script>
$('#tab-CV-NMF-get-classes-5-a').parent().next().next().hide();
$('#tab-CV-NMF-get-classes-5-a').click(function(){
  $('#tab-CV-NMF-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-CV-NMF-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-CV-NMF-consensus-heatmap'>
<ul>
<li><a href='#tab-CV-NMF-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-CV-NMF-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-CV-NMF-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-CV-NMF-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-CV-NMF-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-CV-NMF-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-consensus-heatmap-1-1.png" alt="plot of chunk tab-CV-NMF-consensus-heatmap-1"/></p>

</div>
<div id='tab-CV-NMF-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-consensus-heatmap-2-1.png" alt="plot of chunk tab-CV-NMF-consensus-heatmap-2"/></p>

</div>
<div id='tab-CV-NMF-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-consensus-heatmap-3-1.png" alt="plot of chunk tab-CV-NMF-consensus-heatmap-3"/></p>

</div>
<div id='tab-CV-NMF-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-consensus-heatmap-4-1.png" alt="plot of chunk tab-CV-NMF-consensus-heatmap-4"/></p>

</div>
<div id='tab-CV-NMF-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-consensus-heatmap-5-1.png" alt="plot of chunk tab-CV-NMF-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-CV-NMF-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-CV-NMF-membership-heatmap'>
<ul>
<li><a href='#tab-CV-NMF-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-CV-NMF-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-CV-NMF-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-CV-NMF-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-CV-NMF-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-CV-NMF-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-membership-heatmap-1-1.png" alt="plot of chunk tab-CV-NMF-membership-heatmap-1"/></p>

</div>
<div id='tab-CV-NMF-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-membership-heatmap-2-1.png" alt="plot of chunk tab-CV-NMF-membership-heatmap-2"/></p>

</div>
<div id='tab-CV-NMF-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-membership-heatmap-3-1.png" alt="plot of chunk tab-CV-NMF-membership-heatmap-3"/></p>

</div>
<div id='tab-CV-NMF-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-membership-heatmap-4-1.png" alt="plot of chunk tab-CV-NMF-membership-heatmap-4"/></p>

</div>
<div id='tab-CV-NMF-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-membership-heatmap-5-1.png" alt="plot of chunk tab-CV-NMF-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-CV-NMF-get-signatures' ).tabs();
} );
</script>
<div id='tabs-CV-NMF-get-signatures'>
<ul>
<li><a href='#tab-CV-NMF-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-CV-NMF-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-CV-NMF-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-CV-NMF-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-CV-NMF-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-CV-NMF-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-get-signatures-1-1.png" alt="plot of chunk tab-CV-NMF-get-signatures-1"/></p>

</div>
<div id='tab-CV-NMF-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-get-signatures-2-1.png" alt="plot of chunk tab-CV-NMF-get-signatures-2"/></p>

</div>
<div id='tab-CV-NMF-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-get-signatures-3-1.png" alt="plot of chunk tab-CV-NMF-get-signatures-3"/></p>

</div>
<div id='tab-CV-NMF-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-get-signatures-4-1.png" alt="plot of chunk tab-CV-NMF-get-signatures-4"/></p>

</div>
<div id='tab-CV-NMF-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-get-signatures-5-1.png" alt="plot of chunk tab-CV-NMF-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-CV-NMF-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-CV-NMF-get-signatures-no-scale'>
<ul>
<li><a href='#tab-CV-NMF-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-CV-NMF-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-CV-NMF-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-CV-NMF-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-CV-NMF-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-CV-NMF-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-CV-NMF-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-CV-NMF-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-CV-NMF-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-CV-NMF-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-CV-NMF-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-CV-NMF-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-CV-NMF-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-CV-NMF-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-CV-NMF-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk CV-NMF-signature_compare](figure_cola/CV-NMF-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-CV-NMF-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-CV-NMF-dimension-reduction'>
<ul>
<li><a href='#tab-CV-NMF-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-CV-NMF-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-CV-NMF-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-CV-NMF-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-CV-NMF-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-CV-NMF-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-dimension-reduction-1-1.png" alt="plot of chunk tab-CV-NMF-dimension-reduction-1"/></p>

</div>
<div id='tab-CV-NMF-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-dimension-reduction-2-1.png" alt="plot of chunk tab-CV-NMF-dimension-reduction-2"/></p>

</div>
<div id='tab-CV-NMF-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-dimension-reduction-3-1.png" alt="plot of chunk tab-CV-NMF-dimension-reduction-3"/></p>

</div>
<div id='tab-CV-NMF-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-dimension-reduction-4-1.png" alt="plot of chunk tab-CV-NMF-dimension-reduction-4"/></p>

</div>
<div id='tab-CV-NMF-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-dimension-reduction-5-1.png" alt="plot of chunk tab-CV-NMF-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk CV-NMF-collect-classes](figure_cola/CV-NMF-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### MAD:hclust**






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["MAD", "hclust"]
# you can also extract it by
# res = res_list["MAD:hclust"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 17171 rows and 54 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'MAD' method.
#>   Subgroups are detected by 'hclust' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 3.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk MAD-hclust-collect-plots](figure_cola/MAD-hclust-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk MAD-hclust-select-partition-number](figure_cola/MAD-hclust-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 0.855           0.948       0.975        0.50852 0.491   0.491
#> 3 3 1.000           0.964       0.983        0.13771 0.936   0.869
#> 4 4 0.995           0.958       0.982        0.00636 0.997   0.993
#> 5 5 0.778           0.780       0.878        0.19555 0.874   0.703
#> 6 6 0.851           0.780       0.899        0.04948 0.948   0.838
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 3
```


Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-MAD-hclust-get-classes' ).tabs();
} );
</script>
<div id='tabs-MAD-hclust-get-classes'>
<ul>
<li><a href='#tab-MAD-hclust-get-classes-1'>k = 2</a></li>
<li><a href='#tab-MAD-hclust-get-classes-2'>k = 3</a></li>
<li><a href='#tab-MAD-hclust-get-classes-3'>k = 4</a></li>
<li><a href='#tab-MAD-hclust-get-classes-4'>k = 5</a></li>
<li><a href='#tab-MAD-hclust-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-MAD-hclust-get-classes-1'>
<p><a id='tab-MAD-hclust-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2
#&gt; SRR975551     1   0.000      0.977 1.000 0.000
#&gt; SRR975552     1   0.000      0.977 1.000 0.000
#&gt; SRR975554     1   0.000      0.977 1.000 0.000
#&gt; SRR975553     2   0.000      0.967 0.000 1.000
#&gt; SRR975555     1   0.000      0.977 1.000 0.000
#&gt; SRR975556     2   0.000      0.967 0.000 1.000
#&gt; SRR975557     2   0.722      0.774 0.200 0.800
#&gt; SRR975558     1   0.714      0.763 0.804 0.196
#&gt; SRR975559     1   0.000      0.977 1.000 0.000
#&gt; SRR975560     2   0.000      0.967 0.000 1.000
#&gt; SRR975561     2   0.000      0.967 0.000 1.000
#&gt; SRR975562     1   0.000      0.977 1.000 0.000
#&gt; SRR975563     2   0.000      0.967 0.000 1.000
#&gt; SRR975564     1   0.000      0.977 1.000 0.000
#&gt; SRR975565     1   0.000      0.977 1.000 0.000
#&gt; SRR975566     1   0.000      0.977 1.000 0.000
#&gt; SRR975567     1   0.714      0.763 0.804 0.196
#&gt; SRR975568     1   0.000      0.977 1.000 0.000
#&gt; SRR975569     2   0.000      0.967 0.000 1.000
#&gt; SRR975570     2   0.000      0.967 0.000 1.000
#&gt; SRR975571     2   0.000      0.967 0.000 1.000
#&gt; SRR975572     2   0.000      0.967 0.000 1.000
#&gt; SRR975573     2   0.000      0.967 0.000 1.000
#&gt; SRR975574     2   0.000      0.967 0.000 1.000
#&gt; SRR975575     2   0.000      0.967 0.000 1.000
#&gt; SRR975576     2   0.000      0.967 0.000 1.000
#&gt; SRR975577     2   0.000      0.967 0.000 1.000
#&gt; SRR975578     2   0.000      0.967 0.000 1.000
#&gt; SRR975579     2   0.722      0.774 0.200 0.800
#&gt; SRR975580     2   0.000      0.967 0.000 1.000
#&gt; SRR975581     2   0.000      0.967 0.000 1.000
#&gt; SRR975582     2   0.000      0.967 0.000 1.000
#&gt; SRR975583     2   0.000      0.967 0.000 1.000
#&gt; SRR975584     2   0.000      0.967 0.000 1.000
#&gt; SRR975585     2   0.000      0.967 0.000 1.000
#&gt; SRR975586     2   0.000      0.967 0.000 1.000
#&gt; SRR975587     1   0.184      0.962 0.972 0.028
#&gt; SRR975588     2   0.000      0.967 0.000 1.000
#&gt; SRR975589     1   0.000      0.977 1.000 0.000
#&gt; SRR975590     1   0.000      0.977 1.000 0.000
#&gt; SRR975591     1   0.184      0.962 0.972 0.028
#&gt; SRR975592     1   0.000      0.977 1.000 0.000
#&gt; SRR975593     1   0.000      0.977 1.000 0.000
#&gt; SRR975594     2   0.722      0.774 0.200 0.800
#&gt; SRR975595     1   0.000      0.977 1.000 0.000
#&gt; SRR975597     1   0.000      0.977 1.000 0.000
#&gt; SRR975596     1   0.000      0.977 1.000 0.000
#&gt; SRR975598     1   0.000      0.977 1.000 0.000
#&gt; SRR975599     2   0.722      0.774 0.200 0.800
#&gt; SRR975600     1   0.184      0.962 0.972 0.028
#&gt; SRR975601     1   0.184      0.962 0.972 0.028
#&gt; SRR975602     1   0.000      0.977 1.000 0.000
#&gt; SRR975603     1   0.184      0.962 0.972 0.028
#&gt; SRR975604     1   0.184      0.962 0.972 0.028
</code></pre>

<script>
$('#tab-MAD-hclust-get-classes-1-a').parent().next().next().hide();
$('#tab-MAD-hclust-get-classes-1-a').click(function(){
  $('#tab-MAD-hclust-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-hclust-get-classes-2'>
<p><a id='tab-MAD-hclust-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3
#&gt; SRR975551     1   0.000      0.962 1.000 0.000 0.000
#&gt; SRR975552     1   0.000      0.962 1.000 0.000 0.000
#&gt; SRR975554     1   0.000      0.962 1.000 0.000 0.000
#&gt; SRR975553     2   0.000      1.000 0.000 1.000 0.000
#&gt; SRR975555     1   0.000      0.962 1.000 0.000 0.000
#&gt; SRR975556     2   0.000      1.000 0.000 1.000 0.000
#&gt; SRR975557     3   0.000      0.974 0.000 0.000 1.000
#&gt; SRR975558     1   0.450      0.721 0.804 0.196 0.000
#&gt; SRR975559     1   0.000      0.962 1.000 0.000 0.000
#&gt; SRR975560     2   0.000      1.000 0.000 1.000 0.000
#&gt; SRR975561     2   0.000      1.000 0.000 1.000 0.000
#&gt; SRR975562     1   0.000      0.962 1.000 0.000 0.000
#&gt; SRR975563     2   0.000      1.000 0.000 1.000 0.000
#&gt; SRR975564     1   0.000      0.962 1.000 0.000 0.000
#&gt; SRR975565     1   0.000      0.962 1.000 0.000 0.000
#&gt; SRR975566     1   0.000      0.962 1.000 0.000 0.000
#&gt; SRR975567     1   0.450      0.721 0.804 0.196 0.000
#&gt; SRR975568     1   0.000      0.962 1.000 0.000 0.000
#&gt; SRR975569     2   0.000      1.000 0.000 1.000 0.000
#&gt; SRR975570     2   0.000      1.000 0.000 1.000 0.000
#&gt; SRR975571     2   0.000      1.000 0.000 1.000 0.000
#&gt; SRR975572     2   0.000      1.000 0.000 1.000 0.000
#&gt; SRR975573     2   0.000      1.000 0.000 1.000 0.000
#&gt; SRR975574     2   0.000      1.000 0.000 1.000 0.000
#&gt; SRR975575     2   0.000      1.000 0.000 1.000 0.000
#&gt; SRR975576     2   0.000      1.000 0.000 1.000 0.000
#&gt; SRR975577     2   0.000      1.000 0.000 1.000 0.000
#&gt; SRR975578     2   0.000      1.000 0.000 1.000 0.000
#&gt; SRR975579     3   0.000      0.974 0.000 0.000 1.000
#&gt; SRR975580     2   0.000      1.000 0.000 1.000 0.000
#&gt; SRR975581     2   0.000      1.000 0.000 1.000 0.000
#&gt; SRR975582     2   0.000      1.000 0.000 1.000 0.000
#&gt; SRR975583     2   0.000      1.000 0.000 1.000 0.000
#&gt; SRR975584     2   0.000      1.000 0.000 1.000 0.000
#&gt; SRR975585     2   0.000      1.000 0.000 1.000 0.000
#&gt; SRR975586     2   0.000      1.000 0.000 1.000 0.000
#&gt; SRR975587     1   0.245      0.920 0.924 0.000 0.076
#&gt; SRR975588     2   0.000      1.000 0.000 1.000 0.000
#&gt; SRR975589     1   0.000      0.962 1.000 0.000 0.000
#&gt; SRR975590     1   0.000      0.962 1.000 0.000 0.000
#&gt; SRR975591     1   0.245      0.920 0.924 0.000 0.076
#&gt; SRR975592     1   0.000      0.962 1.000 0.000 0.000
#&gt; SRR975593     1   0.000      0.962 1.000 0.000 0.000
#&gt; SRR975594     3   0.000      0.974 0.000 0.000 1.000
#&gt; SRR975595     1   0.000      0.962 1.000 0.000 0.000
#&gt; SRR975597     1   0.000      0.962 1.000 0.000 0.000
#&gt; SRR975596     1   0.000      0.962 1.000 0.000 0.000
#&gt; SRR975598     1   0.000      0.962 1.000 0.000 0.000
#&gt; SRR975599     3   0.245      0.917 0.076 0.000 0.924
#&gt; SRR975600     1   0.245      0.920 0.924 0.000 0.076
#&gt; SRR975601     1   0.245      0.920 0.924 0.000 0.076
#&gt; SRR975602     1   0.000      0.962 1.000 0.000 0.000
#&gt; SRR975603     1   0.245      0.920 0.924 0.000 0.076
#&gt; SRR975604     1   0.245      0.920 0.924 0.000 0.076
</code></pre>

<script>
$('#tab-MAD-hclust-get-classes-2-a').parent().next().next().hide();
$('#tab-MAD-hclust-get-classes-2-a').click(function(){
  $('#tab-MAD-hclust-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-hclust-get-classes-3'>
<p><a id='tab-MAD-hclust-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3    p4
#&gt; SRR975551     1  0.0000      0.959 1.000 0.000 0.000 0.000
#&gt; SRR975552     1  0.0000      0.959 1.000 0.000 0.000 0.000
#&gt; SRR975554     1  0.0000      0.959 1.000 0.000 0.000 0.000
#&gt; SRR975553     2  0.0000      1.000 0.000 1.000 0.000 0.000
#&gt; SRR975555     1  0.0188      0.958 0.996 0.000 0.004 0.000
#&gt; SRR975556     2  0.0000      1.000 0.000 1.000 0.000 0.000
#&gt; SRR975557     4  0.0000      1.000 0.000 0.000 0.000 1.000
#&gt; SRR975558     1  0.3751      0.700 0.800 0.196 0.004 0.000
#&gt; SRR975559     1  0.0188      0.958 0.996 0.000 0.004 0.000
#&gt; SRR975560     2  0.0000      1.000 0.000 1.000 0.000 0.000
#&gt; SRR975561     2  0.0000      1.000 0.000 1.000 0.000 0.000
#&gt; SRR975562     1  0.0188      0.958 0.996 0.000 0.004 0.000
#&gt; SRR975563     2  0.0000      1.000 0.000 1.000 0.000 0.000
#&gt; SRR975564     1  0.0188      0.958 0.996 0.000 0.004 0.000
#&gt; SRR975565     1  0.0000      0.959 1.000 0.000 0.000 0.000
#&gt; SRR975566     1  0.0000      0.959 1.000 0.000 0.000 0.000
#&gt; SRR975567     1  0.3751      0.700 0.800 0.196 0.004 0.000
#&gt; SRR975568     1  0.0188      0.958 0.996 0.000 0.004 0.000
#&gt; SRR975569     2  0.0000      1.000 0.000 1.000 0.000 0.000
#&gt; SRR975570     2  0.0000      1.000 0.000 1.000 0.000 0.000
#&gt; SRR975571     2  0.0000      1.000 0.000 1.000 0.000 0.000
#&gt; SRR975572     2  0.0000      1.000 0.000 1.000 0.000 0.000
#&gt; SRR975573     2  0.0000      1.000 0.000 1.000 0.000 0.000
#&gt; SRR975574     2  0.0000      1.000 0.000 1.000 0.000 0.000
#&gt; SRR975575     2  0.0000      1.000 0.000 1.000 0.000 0.000
#&gt; SRR975576     2  0.0000      1.000 0.000 1.000 0.000 0.000
#&gt; SRR975577     2  0.0000      1.000 0.000 1.000 0.000 0.000
#&gt; SRR975578     2  0.0000      1.000 0.000 1.000 0.000 0.000
#&gt; SRR975579     4  0.0000      1.000 0.000 0.000 0.000 1.000
#&gt; SRR975580     2  0.0000      1.000 0.000 1.000 0.000 0.000
#&gt; SRR975581     2  0.0000      1.000 0.000 1.000 0.000 0.000
#&gt; SRR975582     2  0.0000      1.000 0.000 1.000 0.000 0.000
#&gt; SRR975583     2  0.0000      1.000 0.000 1.000 0.000 0.000
#&gt; SRR975584     2  0.0000      1.000 0.000 1.000 0.000 0.000
#&gt; SRR975585     2  0.0000      1.000 0.000 1.000 0.000 0.000
#&gt; SRR975586     2  0.0000      1.000 0.000 1.000 0.000 0.000
#&gt; SRR975587     1  0.1940      0.918 0.924 0.000 0.076 0.000
#&gt; SRR975588     2  0.0000      1.000 0.000 1.000 0.000 0.000
#&gt; SRR975589     1  0.0000      0.959 1.000 0.000 0.000 0.000
#&gt; SRR975590     1  0.0000      0.959 1.000 0.000 0.000 0.000
#&gt; SRR975591     1  0.1940      0.918 0.924 0.000 0.076 0.000
#&gt; SRR975592     1  0.0000      0.959 1.000 0.000 0.000 0.000
#&gt; SRR975593     1  0.0000      0.959 1.000 0.000 0.000 0.000
#&gt; SRR975594     3  0.0188      0.803 0.000 0.000 0.996 0.004
#&gt; SRR975595     1  0.0000      0.959 1.000 0.000 0.000 0.000
#&gt; SRR975597     1  0.0000      0.959 1.000 0.000 0.000 0.000
#&gt; SRR975596     1  0.0188      0.958 0.996 0.000 0.004 0.000
#&gt; SRR975598     1  0.0000      0.959 1.000 0.000 0.000 0.000
#&gt; SRR975599     3  0.2125      0.808 0.076 0.000 0.920 0.004
#&gt; SRR975600     1  0.1940      0.918 0.924 0.000 0.076 0.000
#&gt; SRR975601     1  0.1940      0.918 0.924 0.000 0.076 0.000
#&gt; SRR975602     1  0.0000      0.959 1.000 0.000 0.000 0.000
#&gt; SRR975603     1  0.1940      0.918 0.924 0.000 0.076 0.000
#&gt; SRR975604     1  0.1940      0.918 0.924 0.000 0.076 0.000
</code></pre>

<script>
$('#tab-MAD-hclust-get-classes-3-a').parent().next().next().hide();
$('#tab-MAD-hclust-get-classes-3-a').click(function(){
  $('#tab-MAD-hclust-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-hclust-get-classes-4'>
<p><a id='tab-MAD-hclust-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3 p4    p5
#&gt; SRR975551     1   0.130      0.720 0.956 0.000 0.028  0 0.016
#&gt; SRR975552     1   0.130      0.720 0.956 0.000 0.028  0 0.016
#&gt; SRR975554     1   0.191      0.740 0.908 0.000 0.092  0 0.000
#&gt; SRR975553     2   0.000      0.995 0.000 1.000 0.000  0 0.000
#&gt; SRR975555     1   0.460      0.436 0.656 0.000 0.316  0 0.028
#&gt; SRR975556     2   0.000      0.995 0.000 1.000 0.000  0 0.000
#&gt; SRR975557     4   0.000      1.000 0.000 0.000 0.000  1 0.000
#&gt; SRR975558     3   0.587      0.429 0.092 0.140 0.692  0 0.076
#&gt; SRR975559     3   0.482      0.319 0.456 0.000 0.524  0 0.020
#&gt; SRR975560     2   0.152      0.944 0.000 0.944 0.012  0 0.044
#&gt; SRR975561     2   0.000      0.995 0.000 1.000 0.000  0 0.000
#&gt; SRR975562     1   0.332      0.624 0.820 0.000 0.160  0 0.020
#&gt; SRR975563     2   0.000      0.995 0.000 1.000 0.000  0 0.000
#&gt; SRR975564     1   0.472      0.381 0.628 0.000 0.344  0 0.028
#&gt; SRR975565     1   0.177      0.706 0.932 0.000 0.052  0 0.016
#&gt; SRR975566     1   0.191      0.740 0.908 0.000 0.092  0 0.000
#&gt; SRR975567     3   0.587      0.429 0.092 0.140 0.692  0 0.076
#&gt; SRR975568     1   0.460      0.436 0.656 0.000 0.316  0 0.028
#&gt; SRR975569     2   0.000      0.995 0.000 1.000 0.000  0 0.000
#&gt; SRR975570     2   0.000      0.995 0.000 1.000 0.000  0 0.000
#&gt; SRR975571     2   0.000      0.995 0.000 1.000 0.000  0 0.000
#&gt; SRR975572     2   0.000      0.995 0.000 1.000 0.000  0 0.000
#&gt; SRR975573     2   0.000      0.995 0.000 1.000 0.000  0 0.000
#&gt; SRR975574     2   0.000      0.995 0.000 1.000 0.000  0 0.000
#&gt; SRR975575     2   0.000      0.995 0.000 1.000 0.000  0 0.000
#&gt; SRR975576     2   0.000      0.995 0.000 1.000 0.000  0 0.000
#&gt; SRR975577     2   0.000      0.995 0.000 1.000 0.000  0 0.000
#&gt; SRR975578     2   0.000      0.995 0.000 1.000 0.000  0 0.000
#&gt; SRR975579     4   0.000      1.000 0.000 0.000 0.000  1 0.000
#&gt; SRR975580     2   0.152      0.944 0.000 0.944 0.012  0 0.044
#&gt; SRR975581     2   0.000      0.995 0.000 1.000 0.000  0 0.000
#&gt; SRR975582     2   0.000      0.995 0.000 1.000 0.000  0 0.000
#&gt; SRR975583     2   0.000      0.995 0.000 1.000 0.000  0 0.000
#&gt; SRR975584     2   0.000      0.995 0.000 1.000 0.000  0 0.000
#&gt; SRR975585     2   0.000      0.995 0.000 1.000 0.000  0 0.000
#&gt; SRR975586     2   0.000      0.995 0.000 1.000 0.000  0 0.000
#&gt; SRR975587     3   0.161      0.706 0.072 0.000 0.928  0 0.000
#&gt; SRR975588     2   0.000      0.995 0.000 1.000 0.000  0 0.000
#&gt; SRR975589     3   0.428      0.155 0.452 0.000 0.548  0 0.000
#&gt; SRR975590     1   0.223      0.731 0.884 0.000 0.116  0 0.000
#&gt; SRR975591     3   0.161      0.706 0.072 0.000 0.928  0 0.000
#&gt; SRR975592     1   0.366      0.598 0.724 0.000 0.276  0 0.000
#&gt; SRR975593     3   0.428      0.155 0.452 0.000 0.548  0 0.000
#&gt; SRR975594     5   0.167      0.870 0.000 0.000 0.076  0 0.924
#&gt; SRR975595     1   0.337      0.656 0.768 0.000 0.232  0 0.000
#&gt; SRR975597     1   0.337      0.656 0.768 0.000 0.232  0 0.000
#&gt; SRR975596     3   0.482      0.319 0.456 0.000 0.524  0 0.020
#&gt; SRR975598     1   0.334      0.657 0.772 0.000 0.228  0 0.000
#&gt; SRR975599     5   0.311      0.872 0.036 0.000 0.112  0 0.852
#&gt; SRR975600     3   0.161      0.706 0.072 0.000 0.928  0 0.000
#&gt; SRR975601     3   0.161      0.706 0.072 0.000 0.928  0 0.000
#&gt; SRR975602     1   0.191      0.740 0.908 0.000 0.092  0 0.000
#&gt; SRR975603     3   0.161      0.706 0.072 0.000 0.928  0 0.000
#&gt; SRR975604     3   0.161      0.706 0.072 0.000 0.928  0 0.000
</code></pre>

<script>
$('#tab-MAD-hclust-get-classes-4-a').parent().next().next().hide();
$('#tab-MAD-hclust-get-classes-4-a').click(function(){
  $('#tab-MAD-hclust-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-hclust-get-classes-5'>
<p><a id='tab-MAD-hclust-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3    p4    p5 p6
#&gt; SRR975551     1  0.2219      0.591 0.864 0.000 0.000 0.136 0.000  0
#&gt; SRR975552     1  0.2219      0.591 0.864 0.000 0.000 0.136 0.000  0
#&gt; SRR975554     1  0.0291      0.631 0.992 0.000 0.004 0.000 0.004  0
#&gt; SRR975553     2  0.0000      0.982 0.000 1.000 0.000 0.000 0.000  0
#&gt; SRR975555     1  0.3823      0.196 0.564 0.000 0.000 0.436 0.000  0
#&gt; SRR975556     2  0.0000      0.982 0.000 1.000 0.000 0.000 0.000  0
#&gt; SRR975557     6  0.0000      1.000 0.000 0.000 0.000 0.000 0.000  1
#&gt; SRR975558     4  0.0000      0.601 0.000 0.000 0.000 1.000 0.000  0
#&gt; SRR975559     4  0.3706      0.529 0.380 0.000 0.000 0.620 0.000  0
#&gt; SRR975560     2  0.2730      0.782 0.000 0.808 0.000 0.192 0.000  0
#&gt; SRR975561     2  0.0000      0.982 0.000 1.000 0.000 0.000 0.000  0
#&gt; SRR975562     1  0.3175      0.444 0.744 0.000 0.000 0.256 0.000  0
#&gt; SRR975563     2  0.0000      0.982 0.000 1.000 0.000 0.000 0.000  0
#&gt; SRR975564     1  0.3854      0.130 0.536 0.000 0.000 0.464 0.000  0
#&gt; SRR975565     1  0.2454      0.579 0.840 0.000 0.000 0.160 0.000  0
#&gt; SRR975566     1  0.0291      0.631 0.992 0.000 0.004 0.000 0.004  0
#&gt; SRR975567     4  0.0000      0.601 0.000 0.000 0.000 1.000 0.000  0
#&gt; SRR975568     1  0.3823      0.196 0.564 0.000 0.000 0.436 0.000  0
#&gt; SRR975569     2  0.0000      0.982 0.000 1.000 0.000 0.000 0.000  0
#&gt; SRR975570     2  0.0000      0.982 0.000 1.000 0.000 0.000 0.000  0
#&gt; SRR975571     2  0.0000      0.982 0.000 1.000 0.000 0.000 0.000  0
#&gt; SRR975572     2  0.0000      0.982 0.000 1.000 0.000 0.000 0.000  0
#&gt; SRR975573     2  0.0000      0.982 0.000 1.000 0.000 0.000 0.000  0
#&gt; SRR975574     2  0.0000      0.982 0.000 1.000 0.000 0.000 0.000  0
#&gt; SRR975575     2  0.0000      0.982 0.000 1.000 0.000 0.000 0.000  0
#&gt; SRR975576     2  0.0000      0.982 0.000 1.000 0.000 0.000 0.000  0
#&gt; SRR975577     2  0.0000      0.982 0.000 1.000 0.000 0.000 0.000  0
#&gt; SRR975578     2  0.0000      0.982 0.000 1.000 0.000 0.000 0.000  0
#&gt; SRR975579     6  0.0000      1.000 0.000 0.000 0.000 0.000 0.000  1
#&gt; SRR975580     2  0.2730      0.782 0.000 0.808 0.000 0.192 0.000  0
#&gt; SRR975581     2  0.0000      0.982 0.000 1.000 0.000 0.000 0.000  0
#&gt; SRR975582     2  0.0000      0.982 0.000 1.000 0.000 0.000 0.000  0
#&gt; SRR975583     2  0.0000      0.982 0.000 1.000 0.000 0.000 0.000  0
#&gt; SRR975584     2  0.0000      0.982 0.000 1.000 0.000 0.000 0.000  0
#&gt; SRR975585     2  0.0000      0.982 0.000 1.000 0.000 0.000 0.000  0
#&gt; SRR975586     2  0.0000      0.982 0.000 1.000 0.000 0.000 0.000  0
#&gt; SRR975587     3  0.0000      0.993 0.000 0.000 1.000 0.000 0.000  0
#&gt; SRR975588     2  0.0000      0.982 0.000 1.000 0.000 0.000 0.000  0
#&gt; SRR975589     1  0.5974      0.191 0.440 0.000 0.312 0.248 0.000  0
#&gt; SRR975590     1  0.0858      0.631 0.968 0.000 0.028 0.000 0.004  0
#&gt; SRR975591     3  0.0000      0.993 0.000 0.000 1.000 0.000 0.000  0
#&gt; SRR975592     1  0.3351      0.545 0.712 0.000 0.288 0.000 0.000  0
#&gt; SRR975593     1  0.5974      0.191 0.440 0.000 0.312 0.248 0.000  0
#&gt; SRR975594     5  0.0632      0.887 0.000 0.000 0.024 0.000 0.976  0
#&gt; SRR975595     1  0.3050      0.588 0.764 0.000 0.236 0.000 0.000  0
#&gt; SRR975597     1  0.3050      0.588 0.764 0.000 0.236 0.000 0.000  0
#&gt; SRR975596     4  0.3706      0.529 0.380 0.000 0.000 0.620 0.000  0
#&gt; SRR975598     1  0.3023      0.589 0.768 0.000 0.232 0.000 0.000  0
#&gt; SRR975599     5  0.1863      0.888 0.036 0.000 0.044 0.000 0.920  0
#&gt; SRR975600     3  0.0713      0.965 0.000 0.000 0.972 0.028 0.000  0
#&gt; SRR975601     3  0.0000      0.993 0.000 0.000 1.000 0.000 0.000  0
#&gt; SRR975602     1  0.0291      0.631 0.992 0.000 0.004 0.000 0.004  0
#&gt; SRR975603     3  0.0000      0.993 0.000 0.000 1.000 0.000 0.000  0
#&gt; SRR975604     3  0.0000      0.993 0.000 0.000 1.000 0.000 0.000  0
</code></pre>

<script>
$('#tab-MAD-hclust-get-classes-5-a').parent().next().next().hide();
$('#tab-MAD-hclust-get-classes-5-a').click(function(){
  $('#tab-MAD-hclust-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-MAD-hclust-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-MAD-hclust-consensus-heatmap'>
<ul>
<li><a href='#tab-MAD-hclust-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-MAD-hclust-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-MAD-hclust-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-MAD-hclust-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-MAD-hclust-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-hclust-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-consensus-heatmap-1-1.png" alt="plot of chunk tab-MAD-hclust-consensus-heatmap-1"/></p>

</div>
<div id='tab-MAD-hclust-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-consensus-heatmap-2-1.png" alt="plot of chunk tab-MAD-hclust-consensus-heatmap-2"/></p>

</div>
<div id='tab-MAD-hclust-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-consensus-heatmap-3-1.png" alt="plot of chunk tab-MAD-hclust-consensus-heatmap-3"/></p>

</div>
<div id='tab-MAD-hclust-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-consensus-heatmap-4-1.png" alt="plot of chunk tab-MAD-hclust-consensus-heatmap-4"/></p>

</div>
<div id='tab-MAD-hclust-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-consensus-heatmap-5-1.png" alt="plot of chunk tab-MAD-hclust-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-MAD-hclust-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-MAD-hclust-membership-heatmap'>
<ul>
<li><a href='#tab-MAD-hclust-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-MAD-hclust-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-MAD-hclust-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-MAD-hclust-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-MAD-hclust-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-hclust-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-membership-heatmap-1-1.png" alt="plot of chunk tab-MAD-hclust-membership-heatmap-1"/></p>

</div>
<div id='tab-MAD-hclust-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-membership-heatmap-2-1.png" alt="plot of chunk tab-MAD-hclust-membership-heatmap-2"/></p>

</div>
<div id='tab-MAD-hclust-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-membership-heatmap-3-1.png" alt="plot of chunk tab-MAD-hclust-membership-heatmap-3"/></p>

</div>
<div id='tab-MAD-hclust-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-membership-heatmap-4-1.png" alt="plot of chunk tab-MAD-hclust-membership-heatmap-4"/></p>

</div>
<div id='tab-MAD-hclust-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-membership-heatmap-5-1.png" alt="plot of chunk tab-MAD-hclust-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-MAD-hclust-get-signatures' ).tabs();
} );
</script>
<div id='tabs-MAD-hclust-get-signatures'>
<ul>
<li><a href='#tab-MAD-hclust-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-MAD-hclust-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-MAD-hclust-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-MAD-hclust-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-MAD-hclust-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-hclust-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-get-signatures-1-1.png" alt="plot of chunk tab-MAD-hclust-get-signatures-1"/></p>

</div>
<div id='tab-MAD-hclust-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-get-signatures-2-1.png" alt="plot of chunk tab-MAD-hclust-get-signatures-2"/></p>

</div>
<div id='tab-MAD-hclust-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-get-signatures-3-1.png" alt="plot of chunk tab-MAD-hclust-get-signatures-3"/></p>

</div>
<div id='tab-MAD-hclust-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-get-signatures-4-1.png" alt="plot of chunk tab-MAD-hclust-get-signatures-4"/></p>

</div>
<div id='tab-MAD-hclust-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-get-signatures-5-1.png" alt="plot of chunk tab-MAD-hclust-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-MAD-hclust-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-MAD-hclust-get-signatures-no-scale'>
<ul>
<li><a href='#tab-MAD-hclust-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-MAD-hclust-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-MAD-hclust-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-MAD-hclust-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-MAD-hclust-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-hclust-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-MAD-hclust-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-MAD-hclust-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-MAD-hclust-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-MAD-hclust-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-MAD-hclust-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-MAD-hclust-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-MAD-hclust-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-MAD-hclust-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-MAD-hclust-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk MAD-hclust-signature_compare](figure_cola/MAD-hclust-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-MAD-hclust-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-MAD-hclust-dimension-reduction'>
<ul>
<li><a href='#tab-MAD-hclust-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-MAD-hclust-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-MAD-hclust-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-MAD-hclust-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-MAD-hclust-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-hclust-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-dimension-reduction-1-1.png" alt="plot of chunk tab-MAD-hclust-dimension-reduction-1"/></p>

</div>
<div id='tab-MAD-hclust-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-dimension-reduction-2-1.png" alt="plot of chunk tab-MAD-hclust-dimension-reduction-2"/></p>

</div>
<div id='tab-MAD-hclust-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-dimension-reduction-3-1.png" alt="plot of chunk tab-MAD-hclust-dimension-reduction-3"/></p>

</div>
<div id='tab-MAD-hclust-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-dimension-reduction-4-1.png" alt="plot of chunk tab-MAD-hclust-dimension-reduction-4"/></p>

</div>
<div id='tab-MAD-hclust-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-dimension-reduction-5-1.png" alt="plot of chunk tab-MAD-hclust-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk MAD-hclust-collect-classes](figure_cola/MAD-hclust-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### MAD:kmeans**






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["MAD", "kmeans"]
# you can also extract it by
# res = res_list["MAD:kmeans"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 17171 rows and 54 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'MAD' method.
#>   Subgroups are detected by 'kmeans' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 2.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk MAD-kmeans-collect-plots](figure_cola/MAD-kmeans-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk MAD-kmeans-select-partition-number](figure_cola/MAD-kmeans-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 1.000           1.000       1.000         0.5036 0.497   0.497
#> 3 3 0.768           0.795       0.907         0.2259 0.867   0.734
#> 4 4 0.671           0.666       0.822         0.1291 0.953   0.877
#> 5 5 0.657           0.589       0.775         0.0843 0.908   0.743
#> 6 6 0.718           0.533       0.736         0.0462 0.933   0.768
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 2
```


Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-MAD-kmeans-get-classes' ).tabs();
} );
</script>
<div id='tabs-MAD-kmeans-get-classes'>
<ul>
<li><a href='#tab-MAD-kmeans-get-classes-1'>k = 2</a></li>
<li><a href='#tab-MAD-kmeans-get-classes-2'>k = 3</a></li>
<li><a href='#tab-MAD-kmeans-get-classes-3'>k = 4</a></li>
<li><a href='#tab-MAD-kmeans-get-classes-4'>k = 5</a></li>
<li><a href='#tab-MAD-kmeans-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-MAD-kmeans-get-classes-1'>
<p><a id='tab-MAD-kmeans-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;           class entropy silhouette p1 p2
#&gt; SRR975551     1       0          1  1  0
#&gt; SRR975552     1       0          1  1  0
#&gt; SRR975554     1       0          1  1  0
#&gt; SRR975553     2       0          1  0  1
#&gt; SRR975555     1       0          1  1  0
#&gt; SRR975556     2       0          1  0  1
#&gt; SRR975557     1       0          1  1  0
#&gt; SRR975558     1       0          1  1  0
#&gt; SRR975559     1       0          1  1  0
#&gt; SRR975560     2       0          1  0  1
#&gt; SRR975561     2       0          1  0  1
#&gt; SRR975562     1       0          1  1  0
#&gt; SRR975563     2       0          1  0  1
#&gt; SRR975564     1       0          1  1  0
#&gt; SRR975565     1       0          1  1  0
#&gt; SRR975566     1       0          1  1  0
#&gt; SRR975567     1       0          1  1  0
#&gt; SRR975568     1       0          1  1  0
#&gt; SRR975569     2       0          1  0  1
#&gt; SRR975570     2       0          1  0  1
#&gt; SRR975571     2       0          1  0  1
#&gt; SRR975572     2       0          1  0  1
#&gt; SRR975573     2       0          1  0  1
#&gt; SRR975574     2       0          1  0  1
#&gt; SRR975575     2       0          1  0  1
#&gt; SRR975576     2       0          1  0  1
#&gt; SRR975577     2       0          1  0  1
#&gt; SRR975578     2       0          1  0  1
#&gt; SRR975579     2       0          1  0  1
#&gt; SRR975580     2       0          1  0  1
#&gt; SRR975581     2       0          1  0  1
#&gt; SRR975582     2       0          1  0  1
#&gt; SRR975583     2       0          1  0  1
#&gt; SRR975584     2       0          1  0  1
#&gt; SRR975585     2       0          1  0  1
#&gt; SRR975586     2       0          1  0  1
#&gt; SRR975587     1       0          1  1  0
#&gt; SRR975588     2       0          1  0  1
#&gt; SRR975589     1       0          1  1  0
#&gt; SRR975590     1       0          1  1  0
#&gt; SRR975591     1       0          1  1  0
#&gt; SRR975592     1       0          1  1  0
#&gt; SRR975593     1       0          1  1  0
#&gt; SRR975594     1       0          1  1  0
#&gt; SRR975595     1       0          1  1  0
#&gt; SRR975597     1       0          1  1  0
#&gt; SRR975596     1       0          1  1  0
#&gt; SRR975598     1       0          1  1  0
#&gt; SRR975599     1       0          1  1  0
#&gt; SRR975600     1       0          1  1  0
#&gt; SRR975601     1       0          1  1  0
#&gt; SRR975602     1       0          1  1  0
#&gt; SRR975603     1       0          1  1  0
#&gt; SRR975604     1       0          1  1  0
</code></pre>

<script>
$('#tab-MAD-kmeans-get-classes-1-a').parent().next().next().hide();
$('#tab-MAD-kmeans-get-classes-1-a').click(function(){
  $('#tab-MAD-kmeans-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-kmeans-get-classes-2'>
<p><a id='tab-MAD-kmeans-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3
#&gt; SRR975551     1  0.0000      0.876 1.000 0.000 0.000
#&gt; SRR975552     1  0.0000      0.876 1.000 0.000 0.000
#&gt; SRR975554     1  0.0000      0.876 1.000 0.000 0.000
#&gt; SRR975553     2  0.0237      0.978 0.000 0.996 0.004
#&gt; SRR975555     1  0.0000      0.876 1.000 0.000 0.000
#&gt; SRR975556     2  0.1163      0.962 0.000 0.972 0.028
#&gt; SRR975557     3  0.1860      0.585 0.052 0.000 0.948
#&gt; SRR975558     1  0.3412      0.739 0.876 0.000 0.124
#&gt; SRR975559     1  0.0000      0.876 1.000 0.000 0.000
#&gt; SRR975560     2  0.3412      0.888 0.000 0.876 0.124
#&gt; SRR975561     2  0.3038      0.907 0.000 0.896 0.104
#&gt; SRR975562     1  0.0000      0.876 1.000 0.000 0.000
#&gt; SRR975563     2  0.0000      0.978 0.000 1.000 0.000
#&gt; SRR975564     1  0.0000      0.876 1.000 0.000 0.000
#&gt; SRR975565     1  0.0000      0.876 1.000 0.000 0.000
#&gt; SRR975566     1  0.0000      0.876 1.000 0.000 0.000
#&gt; SRR975567     1  0.3412      0.739 0.876 0.000 0.124
#&gt; SRR975568     1  0.0000      0.876 1.000 0.000 0.000
#&gt; SRR975569     2  0.0000      0.978 0.000 1.000 0.000
#&gt; SRR975570     2  0.0000      0.978 0.000 1.000 0.000
#&gt; SRR975571     2  0.0237      0.978 0.000 0.996 0.004
#&gt; SRR975572     2  0.0000      0.978 0.000 1.000 0.000
#&gt; SRR975573     2  0.0237      0.978 0.000 0.996 0.004
#&gt; SRR975574     2  0.0237      0.978 0.000 0.996 0.004
#&gt; SRR975575     2  0.0000      0.978 0.000 1.000 0.000
#&gt; SRR975576     2  0.0000      0.978 0.000 1.000 0.000
#&gt; SRR975577     2  0.0237      0.978 0.000 0.996 0.004
#&gt; SRR975578     2  0.0237      0.978 0.000 0.996 0.004
#&gt; SRR975579     3  0.6305     -0.315 0.000 0.484 0.516
#&gt; SRR975580     2  0.2878      0.913 0.000 0.904 0.096
#&gt; SRR975581     2  0.0000      0.978 0.000 1.000 0.000
#&gt; SRR975582     2  0.0237      0.978 0.000 0.996 0.004
#&gt; SRR975583     2  0.0000      0.978 0.000 1.000 0.000
#&gt; SRR975584     2  0.0237      0.978 0.000 0.996 0.004
#&gt; SRR975585     2  0.0000      0.978 0.000 1.000 0.000
#&gt; SRR975586     2  0.3038      0.907 0.000 0.896 0.104
#&gt; SRR975587     1  0.6307     -0.266 0.512 0.000 0.488
#&gt; SRR975588     2  0.0000      0.978 0.000 1.000 0.000
#&gt; SRR975589     1  0.3412      0.793 0.876 0.000 0.124
#&gt; SRR975590     1  0.3752      0.772 0.856 0.000 0.144
#&gt; SRR975591     3  0.6140      0.523 0.404 0.000 0.596
#&gt; SRR975592     1  0.3752      0.772 0.856 0.000 0.144
#&gt; SRR975593     1  0.3619      0.779 0.864 0.000 0.136
#&gt; SRR975594     3  0.3482      0.628 0.128 0.000 0.872
#&gt; SRR975595     1  0.1964      0.853 0.944 0.000 0.056
#&gt; SRR975597     1  0.1964      0.853 0.944 0.000 0.056
#&gt; SRR975596     1  0.0000      0.876 1.000 0.000 0.000
#&gt; SRR975598     1  0.1964      0.853 0.944 0.000 0.056
#&gt; SRR975599     3  0.3686      0.630 0.140 0.000 0.860
#&gt; SRR975600     1  0.6305     -0.260 0.516 0.000 0.484
#&gt; SRR975601     3  0.6126      0.525 0.400 0.000 0.600
#&gt; SRR975602     1  0.0237      0.875 0.996 0.000 0.004
#&gt; SRR975603     3  0.6140      0.523 0.404 0.000 0.596
#&gt; SRR975604     3  0.6126      0.525 0.400 0.000 0.600
</code></pre>

<script>
$('#tab-MAD-kmeans-get-classes-2-a').parent().next().next().hide();
$('#tab-MAD-kmeans-get-classes-2-a').click(function(){
  $('#tab-MAD-kmeans-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-kmeans-get-classes-3'>
<p><a id='tab-MAD-kmeans-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3    p4
#&gt; SRR975551     1  0.1118     0.7421 0.964 0.000 0.000 0.036
#&gt; SRR975552     1  0.0707     0.7445 0.980 0.000 0.000 0.020
#&gt; SRR975554     1  0.0817     0.7441 0.976 0.000 0.000 0.024
#&gt; SRR975553     2  0.2450     0.8752 0.000 0.912 0.072 0.016
#&gt; SRR975555     1  0.0592     0.7447 0.984 0.000 0.000 0.016
#&gt; SRR975556     2  0.3056     0.8158 0.000 0.888 0.072 0.040
#&gt; SRR975557     4  0.4511     0.4855 0.008 0.000 0.268 0.724
#&gt; SRR975558     1  0.7760     0.0728 0.392 0.000 0.236 0.372
#&gt; SRR975559     1  0.4458     0.6678 0.808 0.000 0.116 0.076
#&gt; SRR975560     2  0.6716     0.4338 0.000 0.568 0.112 0.320
#&gt; SRR975561     2  0.6167     0.5478 0.000 0.648 0.096 0.256
#&gt; SRR975562     1  0.2334     0.7302 0.908 0.000 0.004 0.088
#&gt; SRR975563     2  0.0000     0.8867 0.000 1.000 0.000 0.000
#&gt; SRR975564     1  0.0921     0.7450 0.972 0.000 0.000 0.028
#&gt; SRR975565     1  0.0707     0.7445 0.980 0.000 0.000 0.020
#&gt; SRR975566     1  0.4093     0.6845 0.832 0.000 0.096 0.072
#&gt; SRR975567     1  0.7760     0.0728 0.392 0.000 0.236 0.372
#&gt; SRR975568     1  0.0707     0.7448 0.980 0.000 0.000 0.020
#&gt; SRR975569     2  0.0188     0.8863 0.000 0.996 0.004 0.000
#&gt; SRR975570     2  0.0000     0.8867 0.000 1.000 0.000 0.000
#&gt; SRR975571     2  0.2450     0.8752 0.000 0.912 0.072 0.016
#&gt; SRR975572     2  0.0000     0.8867 0.000 1.000 0.000 0.000
#&gt; SRR975573     2  0.2450     0.8752 0.000 0.912 0.072 0.016
#&gt; SRR975574     2  0.2450     0.8752 0.000 0.912 0.072 0.016
#&gt; SRR975575     2  0.0000     0.8867 0.000 1.000 0.000 0.000
#&gt; SRR975576     2  0.0000     0.8867 0.000 1.000 0.000 0.000
#&gt; SRR975577     2  0.2450     0.8752 0.000 0.912 0.072 0.016
#&gt; SRR975578     2  0.2450     0.8752 0.000 0.912 0.072 0.016
#&gt; SRR975579     4  0.3400     0.4676 0.000 0.180 0.000 0.820
#&gt; SRR975580     2  0.6521     0.5415 0.000 0.620 0.124 0.256
#&gt; SRR975581     2  0.0000     0.8867 0.000 1.000 0.000 0.000
#&gt; SRR975582     2  0.2450     0.8752 0.000 0.912 0.072 0.016
#&gt; SRR975583     2  0.0000     0.8867 0.000 1.000 0.000 0.000
#&gt; SRR975584     2  0.2450     0.8752 0.000 0.912 0.072 0.016
#&gt; SRR975585     2  0.0000     0.8867 0.000 1.000 0.000 0.000
#&gt; SRR975586     2  0.6140     0.5484 0.000 0.652 0.096 0.252
#&gt; SRR975587     3  0.5337     0.7288 0.260 0.000 0.696 0.044
#&gt; SRR975588     2  0.0000     0.8867 0.000 1.000 0.000 0.000
#&gt; SRR975589     1  0.6393     0.0509 0.480 0.000 0.456 0.064
#&gt; SRR975590     1  0.5374     0.4798 0.704 0.000 0.244 0.052
#&gt; SRR975591     3  0.3311     0.8152 0.172 0.000 0.828 0.000
#&gt; SRR975592     1  0.5807     0.2250 0.596 0.000 0.364 0.040
#&gt; SRR975593     1  0.6395     0.0347 0.476 0.000 0.460 0.064
#&gt; SRR975594     3  0.5992    -0.2641 0.040 0.000 0.516 0.444
#&gt; SRR975595     1  0.3732     0.6823 0.852 0.000 0.092 0.056
#&gt; SRR975597     1  0.3486     0.6858 0.864 0.000 0.092 0.044
#&gt; SRR975596     1  0.4646     0.6629 0.796 0.000 0.120 0.084
#&gt; SRR975598     1  0.3732     0.6823 0.852 0.000 0.092 0.056
#&gt; SRR975599     4  0.6979     0.1039 0.120 0.000 0.376 0.504
#&gt; SRR975600     3  0.3539     0.8110 0.176 0.000 0.820 0.004
#&gt; SRR975601     3  0.4868     0.7475 0.256 0.000 0.720 0.024
#&gt; SRR975602     1  0.1940     0.7285 0.924 0.000 0.000 0.076
#&gt; SRR975603     3  0.3311     0.8152 0.172 0.000 0.828 0.000
#&gt; SRR975604     3  0.3311     0.8152 0.172 0.000 0.828 0.000
</code></pre>

<script>
$('#tab-MAD-kmeans-get-classes-3-a').parent().next().next().hide();
$('#tab-MAD-kmeans-get-classes-3-a').click(function(){
  $('#tab-MAD-kmeans-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-kmeans-get-classes-4'>
<p><a id='tab-MAD-kmeans-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3    p4    p5
#&gt; SRR975551     1  0.0955      0.783 0.968 0.000 0.000 0.004 0.028
#&gt; SRR975552     1  0.0324      0.784 0.992 0.000 0.000 0.004 0.004
#&gt; SRR975554     1  0.1043      0.785 0.960 0.000 0.000 0.000 0.040
#&gt; SRR975553     2  0.4465      0.726 0.000 0.736 0.060 0.000 0.204
#&gt; SRR975555     1  0.0865      0.784 0.972 0.000 0.000 0.004 0.024
#&gt; SRR975556     2  0.5025      0.420 0.000 0.704 0.000 0.124 0.172
#&gt; SRR975557     4  0.4024      0.567 0.000 0.000 0.220 0.752 0.028
#&gt; SRR975558     5  0.8003      0.528 0.228 0.000 0.108 0.248 0.416
#&gt; SRR975559     1  0.5542      0.562 0.632 0.000 0.084 0.008 0.276
#&gt; SRR975560     5  0.6756      0.171 0.000 0.268 0.000 0.344 0.388
#&gt; SRR975561     2  0.6724     -0.216 0.000 0.420 0.000 0.284 0.296
#&gt; SRR975562     1  0.4090      0.683 0.716 0.000 0.000 0.016 0.268
#&gt; SRR975563     2  0.0000      0.770 0.000 1.000 0.000 0.000 0.000
#&gt; SRR975564     1  0.1282      0.772 0.952 0.000 0.000 0.004 0.044
#&gt; SRR975565     1  0.0324      0.784 0.992 0.000 0.000 0.004 0.004
#&gt; SRR975566     1  0.4668      0.668 0.724 0.000 0.048 0.008 0.220
#&gt; SRR975567     5  0.8003      0.528 0.228 0.000 0.108 0.248 0.416
#&gt; SRR975568     1  0.0566      0.783 0.984 0.000 0.000 0.004 0.012
#&gt; SRR975569     2  0.0162      0.769 0.000 0.996 0.000 0.000 0.004
#&gt; SRR975570     2  0.0000      0.770 0.000 1.000 0.000 0.000 0.000
#&gt; SRR975571     2  0.4465      0.726 0.000 0.736 0.060 0.000 0.204
#&gt; SRR975572     2  0.0000      0.770 0.000 1.000 0.000 0.000 0.000
#&gt; SRR975573     2  0.4434      0.726 0.000 0.736 0.056 0.000 0.208
#&gt; SRR975574     2  0.4434      0.726 0.000 0.736 0.056 0.000 0.208
#&gt; SRR975575     2  0.0000      0.770 0.000 1.000 0.000 0.000 0.000
#&gt; SRR975576     2  0.0000      0.770 0.000 1.000 0.000 0.000 0.000
#&gt; SRR975577     2  0.4434      0.726 0.000 0.736 0.056 0.000 0.208
#&gt; SRR975578     2  0.4434      0.726 0.000 0.736 0.056 0.000 0.208
#&gt; SRR975579     4  0.1549      0.336 0.000 0.040 0.000 0.944 0.016
#&gt; SRR975580     2  0.6784     -0.247 0.000 0.368 0.000 0.280 0.352
#&gt; SRR975581     2  0.0000      0.770 0.000 1.000 0.000 0.000 0.000
#&gt; SRR975582     2  0.4434      0.726 0.000 0.736 0.056 0.000 0.208
#&gt; SRR975583     2  0.0000      0.770 0.000 1.000 0.000 0.000 0.000
#&gt; SRR975584     2  0.4434      0.726 0.000 0.736 0.056 0.000 0.208
#&gt; SRR975585     2  0.0000      0.770 0.000 1.000 0.000 0.000 0.000
#&gt; SRR975586     2  0.6715     -0.213 0.000 0.424 0.000 0.284 0.292
#&gt; SRR975587     3  0.4695      0.621 0.124 0.000 0.764 0.016 0.096
#&gt; SRR975588     2  0.0000      0.770 0.000 1.000 0.000 0.000 0.000
#&gt; SRR975589     3  0.5957      0.507 0.236 0.000 0.588 0.000 0.176
#&gt; SRR975590     1  0.6096      0.406 0.604 0.000 0.252 0.016 0.128
#&gt; SRR975591     3  0.1478      0.679 0.064 0.000 0.936 0.000 0.000
#&gt; SRR975592     3  0.6441      0.337 0.352 0.000 0.508 0.016 0.124
#&gt; SRR975593     3  0.5957      0.507 0.236 0.000 0.588 0.000 0.176
#&gt; SRR975594     3  0.5751     -0.301 0.004 0.000 0.516 0.404 0.076
#&gt; SRR975595     1  0.5451      0.660 0.700 0.000 0.104 0.024 0.172
#&gt; SRR975597     1  0.5009      0.671 0.736 0.000 0.104 0.016 0.144
#&gt; SRR975596     1  0.5704      0.550 0.616 0.000 0.084 0.012 0.288
#&gt; SRR975598     1  0.5451      0.660 0.700 0.000 0.104 0.024 0.172
#&gt; SRR975599     4  0.7745      0.318 0.076 0.000 0.280 0.428 0.216
#&gt; SRR975600     3  0.2426      0.672 0.064 0.000 0.900 0.000 0.036
#&gt; SRR975601     3  0.3977      0.637 0.100 0.000 0.812 0.008 0.080
#&gt; SRR975602     1  0.3944      0.734 0.768 0.000 0.000 0.032 0.200
#&gt; SRR975603     3  0.1478      0.679 0.064 0.000 0.936 0.000 0.000
#&gt; SRR975604     3  0.1638      0.678 0.064 0.000 0.932 0.004 0.000
</code></pre>

<script>
$('#tab-MAD-kmeans-get-classes-4-a').parent().next().next().hide();
$('#tab-MAD-kmeans-get-classes-4-a').click(function(){
  $('#tab-MAD-kmeans-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-kmeans-get-classes-5'>
<p><a id='tab-MAD-kmeans-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3    p4    p5    p6
#&gt; SRR975551     1  0.0717      0.705 0.976 0.000 0.000 0.008 0.016 0.000
#&gt; SRR975552     1  0.0260      0.707 0.992 0.000 0.000 0.000 0.008 0.000
#&gt; SRR975554     1  0.2186      0.701 0.908 0.000 0.000 0.008 0.048 0.036
#&gt; SRR975553     2  0.0551      0.574 0.000 0.984 0.000 0.008 0.004 0.004
#&gt; SRR975555     1  0.1552      0.701 0.940 0.000 0.000 0.004 0.020 0.036
#&gt; SRR975556     5  0.6169      0.000 0.000 0.336 0.000 0.008 0.428 0.228
#&gt; SRR975557     4  0.2448      0.607 0.000 0.000 0.052 0.884 0.000 0.064
#&gt; SRR975558     6  0.4535      0.276 0.140 0.000 0.096 0.024 0.000 0.740
#&gt; SRR975559     1  0.7663      0.435 0.448 0.000 0.084 0.064 0.144 0.260
#&gt; SRR975560     6  0.4854      0.440 0.000 0.188 0.000 0.012 0.112 0.688
#&gt; SRR975561     6  0.5956      0.151 0.000 0.256 0.000 0.012 0.208 0.524
#&gt; SRR975562     1  0.6415      0.522 0.520 0.000 0.000 0.052 0.184 0.244
#&gt; SRR975563     2  0.3647      0.522 0.000 0.640 0.000 0.000 0.360 0.000
#&gt; SRR975564     1  0.2015      0.689 0.916 0.000 0.000 0.016 0.012 0.056
#&gt; SRR975565     1  0.0146      0.706 0.996 0.000 0.000 0.000 0.004 0.000
#&gt; SRR975566     1  0.6844      0.547 0.576 0.000 0.060 0.060 0.136 0.168
#&gt; SRR975567     6  0.4535      0.276 0.140 0.000 0.096 0.024 0.000 0.740
#&gt; SRR975568     1  0.1590      0.694 0.936 0.000 0.000 0.008 0.008 0.048
#&gt; SRR975569     2  0.3563      0.543 0.000 0.664 0.000 0.000 0.336 0.000
#&gt; SRR975570     2  0.3578      0.541 0.000 0.660 0.000 0.000 0.340 0.000
#&gt; SRR975571     2  0.0551      0.574 0.000 0.984 0.000 0.008 0.004 0.004
#&gt; SRR975572     2  0.3634      0.530 0.000 0.644 0.000 0.000 0.356 0.000
#&gt; SRR975573     2  0.0000      0.581 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR975574     2  0.0000      0.581 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR975575     2  0.3634      0.530 0.000 0.644 0.000 0.000 0.356 0.000
#&gt; SRR975576     2  0.3647      0.522 0.000 0.640 0.000 0.000 0.360 0.000
#&gt; SRR975577     2  0.0000      0.581 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR975578     2  0.0000      0.581 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR975579     4  0.3166      0.520 0.000 0.008 0.000 0.800 0.008 0.184
#&gt; SRR975580     6  0.5539      0.273 0.000 0.292 0.000 0.008 0.136 0.564
#&gt; SRR975581     2  0.3647      0.522 0.000 0.640 0.000 0.000 0.360 0.000
#&gt; SRR975582     2  0.0000      0.581 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR975583     2  0.3634      0.530 0.000 0.644 0.000 0.000 0.356 0.000
#&gt; SRR975584     2  0.0000      0.581 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR975585     2  0.3634      0.530 0.000 0.644 0.000 0.000 0.356 0.000
#&gt; SRR975586     6  0.5918      0.165 0.000 0.252 0.000 0.012 0.204 0.532
#&gt; SRR975587     3  0.4193      0.639 0.052 0.000 0.780 0.016 0.136 0.016
#&gt; SRR975588     2  0.3578      0.541 0.000 0.660 0.000 0.000 0.340 0.000
#&gt; SRR975589     3  0.5702      0.590 0.092 0.000 0.688 0.032 0.064 0.124
#&gt; SRR975590     1  0.6713      0.134 0.436 0.000 0.300 0.024 0.228 0.012
#&gt; SRR975591     3  0.0000      0.740 0.000 0.000 1.000 0.000 0.000 0.000
#&gt; SRR975592     3  0.6105      0.476 0.220 0.000 0.560 0.016 0.192 0.012
#&gt; SRR975593     3  0.5649      0.591 0.092 0.000 0.692 0.032 0.060 0.124
#&gt; SRR975594     4  0.6213      0.326 0.000 0.000 0.400 0.444 0.108 0.048
#&gt; SRR975595     1  0.5652      0.585 0.588 0.000 0.068 0.024 0.304 0.016
#&gt; SRR975597     1  0.5124      0.602 0.644 0.000 0.068 0.020 0.264 0.004
#&gt; SRR975596     1  0.7776      0.420 0.428 0.000 0.084 0.068 0.152 0.268
#&gt; SRR975598     1  0.5652      0.585 0.588 0.000 0.068 0.024 0.304 0.016
#&gt; SRR975599     4  0.7427      0.524 0.060 0.000 0.140 0.488 0.236 0.076
#&gt; SRR975600     3  0.1269      0.732 0.000 0.000 0.956 0.012 0.012 0.020
#&gt; SRR975601     3  0.4025      0.644 0.032 0.000 0.796 0.016 0.128 0.028
#&gt; SRR975602     1  0.5125      0.634 0.656 0.000 0.000 0.060 0.244 0.040
#&gt; SRR975603     3  0.0000      0.740 0.000 0.000 1.000 0.000 0.000 0.000
#&gt; SRR975604     3  0.0146      0.738 0.000 0.000 0.996 0.000 0.004 0.000
</code></pre>

<script>
$('#tab-MAD-kmeans-get-classes-5-a').parent().next().next().hide();
$('#tab-MAD-kmeans-get-classes-5-a').click(function(){
  $('#tab-MAD-kmeans-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-MAD-kmeans-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-MAD-kmeans-consensus-heatmap'>
<ul>
<li><a href='#tab-MAD-kmeans-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-MAD-kmeans-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-MAD-kmeans-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-MAD-kmeans-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-MAD-kmeans-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-kmeans-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-consensus-heatmap-1-1.png" alt="plot of chunk tab-MAD-kmeans-consensus-heatmap-1"/></p>

</div>
<div id='tab-MAD-kmeans-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-consensus-heatmap-2-1.png" alt="plot of chunk tab-MAD-kmeans-consensus-heatmap-2"/></p>

</div>
<div id='tab-MAD-kmeans-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-consensus-heatmap-3-1.png" alt="plot of chunk tab-MAD-kmeans-consensus-heatmap-3"/></p>

</div>
<div id='tab-MAD-kmeans-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-consensus-heatmap-4-1.png" alt="plot of chunk tab-MAD-kmeans-consensus-heatmap-4"/></p>

</div>
<div id='tab-MAD-kmeans-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-consensus-heatmap-5-1.png" alt="plot of chunk tab-MAD-kmeans-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-MAD-kmeans-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-MAD-kmeans-membership-heatmap'>
<ul>
<li><a href='#tab-MAD-kmeans-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-MAD-kmeans-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-MAD-kmeans-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-MAD-kmeans-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-MAD-kmeans-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-kmeans-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-membership-heatmap-1-1.png" alt="plot of chunk tab-MAD-kmeans-membership-heatmap-1"/></p>

</div>
<div id='tab-MAD-kmeans-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-membership-heatmap-2-1.png" alt="plot of chunk tab-MAD-kmeans-membership-heatmap-2"/></p>

</div>
<div id='tab-MAD-kmeans-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-membership-heatmap-3-1.png" alt="plot of chunk tab-MAD-kmeans-membership-heatmap-3"/></p>

</div>
<div id='tab-MAD-kmeans-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-membership-heatmap-4-1.png" alt="plot of chunk tab-MAD-kmeans-membership-heatmap-4"/></p>

</div>
<div id='tab-MAD-kmeans-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-membership-heatmap-5-1.png" alt="plot of chunk tab-MAD-kmeans-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-MAD-kmeans-get-signatures' ).tabs();
} );
</script>
<div id='tabs-MAD-kmeans-get-signatures'>
<ul>
<li><a href='#tab-MAD-kmeans-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-MAD-kmeans-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-MAD-kmeans-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-MAD-kmeans-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-MAD-kmeans-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-kmeans-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-get-signatures-1-1.png" alt="plot of chunk tab-MAD-kmeans-get-signatures-1"/></p>

</div>
<div id='tab-MAD-kmeans-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-get-signatures-2-1.png" alt="plot of chunk tab-MAD-kmeans-get-signatures-2"/></p>

</div>
<div id='tab-MAD-kmeans-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-get-signatures-3-1.png" alt="plot of chunk tab-MAD-kmeans-get-signatures-3"/></p>

</div>
<div id='tab-MAD-kmeans-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-get-signatures-4-1.png" alt="plot of chunk tab-MAD-kmeans-get-signatures-4"/></p>

</div>
<div id='tab-MAD-kmeans-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-get-signatures-5-1.png" alt="plot of chunk tab-MAD-kmeans-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-MAD-kmeans-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-MAD-kmeans-get-signatures-no-scale'>
<ul>
<li><a href='#tab-MAD-kmeans-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-MAD-kmeans-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-MAD-kmeans-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-MAD-kmeans-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-MAD-kmeans-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-kmeans-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-MAD-kmeans-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-MAD-kmeans-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-MAD-kmeans-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-MAD-kmeans-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-MAD-kmeans-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-MAD-kmeans-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-MAD-kmeans-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-MAD-kmeans-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-MAD-kmeans-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk MAD-kmeans-signature_compare](figure_cola/MAD-kmeans-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-MAD-kmeans-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-MAD-kmeans-dimension-reduction'>
<ul>
<li><a href='#tab-MAD-kmeans-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-MAD-kmeans-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-MAD-kmeans-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-MAD-kmeans-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-MAD-kmeans-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-kmeans-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-dimension-reduction-1-1.png" alt="plot of chunk tab-MAD-kmeans-dimension-reduction-1"/></p>

</div>
<div id='tab-MAD-kmeans-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-dimension-reduction-2-1.png" alt="plot of chunk tab-MAD-kmeans-dimension-reduction-2"/></p>

</div>
<div id='tab-MAD-kmeans-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-dimension-reduction-3-1.png" alt="plot of chunk tab-MAD-kmeans-dimension-reduction-3"/></p>

</div>
<div id='tab-MAD-kmeans-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-dimension-reduction-4-1.png" alt="plot of chunk tab-MAD-kmeans-dimension-reduction-4"/></p>

</div>
<div id='tab-MAD-kmeans-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-dimension-reduction-5-1.png" alt="plot of chunk tab-MAD-kmeans-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk MAD-kmeans-collect-classes](figure_cola/MAD-kmeans-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### MAD:skmeans*






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["MAD", "skmeans"]
# you can also extract it by
# res = res_list["MAD:skmeans"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 17171 rows and 54 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'MAD' method.
#>   Subgroups are detected by 'skmeans' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 3.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk MAD-skmeans-collect-plots](figure_cola/MAD-skmeans-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk MAD-skmeans-select-partition-number](figure_cola/MAD-skmeans-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 1.000           0.991       0.996         0.5044 0.497   0.497
#> 3 3 0.909           0.929       0.962         0.2770 0.868   0.734
#> 4 4 0.781           0.756       0.889         0.0847 0.904   0.746
#> 5 5 0.799           0.626       0.832         0.0722 0.948   0.833
#> 6 6 0.722           0.628       0.772         0.0480 0.941   0.786
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 3
#> attr(,"optional")
#> [1] 2
```

There is also optional best $k$ = 2 that is worth to check.

Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-MAD-skmeans-get-classes' ).tabs();
} );
</script>
<div id='tabs-MAD-skmeans-get-classes'>
<ul>
<li><a href='#tab-MAD-skmeans-get-classes-1'>k = 2</a></li>
<li><a href='#tab-MAD-skmeans-get-classes-2'>k = 3</a></li>
<li><a href='#tab-MAD-skmeans-get-classes-3'>k = 4</a></li>
<li><a href='#tab-MAD-skmeans-get-classes-4'>k = 5</a></li>
<li><a href='#tab-MAD-skmeans-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-MAD-skmeans-get-classes-1'>
<p><a id='tab-MAD-skmeans-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2
#&gt; SRR975551     1   0.000      0.992 1.000 0.000
#&gt; SRR975552     1   0.000      0.992 1.000 0.000
#&gt; SRR975554     1   0.000      0.992 1.000 0.000
#&gt; SRR975553     2   0.000      1.000 0.000 1.000
#&gt; SRR975555     1   0.000      0.992 1.000 0.000
#&gt; SRR975556     2   0.000      1.000 0.000 1.000
#&gt; SRR975557     1   0.000      0.992 1.000 0.000
#&gt; SRR975558     1   0.722      0.752 0.800 0.200
#&gt; SRR975559     1   0.000      0.992 1.000 0.000
#&gt; SRR975560     2   0.000      1.000 0.000 1.000
#&gt; SRR975561     2   0.000      1.000 0.000 1.000
#&gt; SRR975562     1   0.000      0.992 1.000 0.000
#&gt; SRR975563     2   0.000      1.000 0.000 1.000
#&gt; SRR975564     1   0.000      0.992 1.000 0.000
#&gt; SRR975565     1   0.000      0.992 1.000 0.000
#&gt; SRR975566     1   0.000      0.992 1.000 0.000
#&gt; SRR975567     1   0.163      0.970 0.976 0.024
#&gt; SRR975568     1   0.000      0.992 1.000 0.000
#&gt; SRR975569     2   0.000      1.000 0.000 1.000
#&gt; SRR975570     2   0.000      1.000 0.000 1.000
#&gt; SRR975571     2   0.000      1.000 0.000 1.000
#&gt; SRR975572     2   0.000      1.000 0.000 1.000
#&gt; SRR975573     2   0.000      1.000 0.000 1.000
#&gt; SRR975574     2   0.000      1.000 0.000 1.000
#&gt; SRR975575     2   0.000      1.000 0.000 1.000
#&gt; SRR975576     2   0.000      1.000 0.000 1.000
#&gt; SRR975577     2   0.000      1.000 0.000 1.000
#&gt; SRR975578     2   0.000      1.000 0.000 1.000
#&gt; SRR975579     2   0.000      1.000 0.000 1.000
#&gt; SRR975580     2   0.000      1.000 0.000 1.000
#&gt; SRR975581     2   0.000      1.000 0.000 1.000
#&gt; SRR975582     2   0.000      1.000 0.000 1.000
#&gt; SRR975583     2   0.000      1.000 0.000 1.000
#&gt; SRR975584     2   0.000      1.000 0.000 1.000
#&gt; SRR975585     2   0.000      1.000 0.000 1.000
#&gt; SRR975586     2   0.000      1.000 0.000 1.000
#&gt; SRR975587     1   0.000      0.992 1.000 0.000
#&gt; SRR975588     2   0.000      1.000 0.000 1.000
#&gt; SRR975589     1   0.000      0.992 1.000 0.000
#&gt; SRR975590     1   0.000      0.992 1.000 0.000
#&gt; SRR975591     1   0.000      0.992 1.000 0.000
#&gt; SRR975592     1   0.000      0.992 1.000 0.000
#&gt; SRR975593     1   0.000      0.992 1.000 0.000
#&gt; SRR975594     1   0.000      0.992 1.000 0.000
#&gt; SRR975595     1   0.000      0.992 1.000 0.000
#&gt; SRR975597     1   0.000      0.992 1.000 0.000
#&gt; SRR975596     1   0.000      0.992 1.000 0.000
#&gt; SRR975598     1   0.000      0.992 1.000 0.000
#&gt; SRR975599     1   0.000      0.992 1.000 0.000
#&gt; SRR975600     1   0.000      0.992 1.000 0.000
#&gt; SRR975601     1   0.000      0.992 1.000 0.000
#&gt; SRR975602     1   0.000      0.992 1.000 0.000
#&gt; SRR975603     1   0.000      0.992 1.000 0.000
#&gt; SRR975604     1   0.000      0.992 1.000 0.000
</code></pre>

<script>
$('#tab-MAD-skmeans-get-classes-1-a').parent().next().next().hide();
$('#tab-MAD-skmeans-get-classes-1-a').click(function(){
  $('#tab-MAD-skmeans-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-skmeans-get-classes-2'>
<p><a id='tab-MAD-skmeans-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1 p2    p3
#&gt; SRR975551     1   0.000      0.891 1.000  0 0.000
#&gt; SRR975552     1   0.000      0.891 1.000  0 0.000
#&gt; SRR975554     1   0.000      0.891 1.000  0 0.000
#&gt; SRR975553     2   0.000      1.000 0.000  1 0.000
#&gt; SRR975555     1   0.000      0.891 1.000  0 0.000
#&gt; SRR975556     2   0.000      1.000 0.000  1 0.000
#&gt; SRR975557     3   0.000      1.000 0.000  0 1.000
#&gt; SRR975558     1   0.000      0.891 1.000  0 0.000
#&gt; SRR975559     1   0.000      0.891 1.000  0 0.000
#&gt; SRR975560     2   0.000      1.000 0.000  1 0.000
#&gt; SRR975561     2   0.000      1.000 0.000  1 0.000
#&gt; SRR975562     1   0.000      0.891 1.000  0 0.000
#&gt; SRR975563     2   0.000      1.000 0.000  1 0.000
#&gt; SRR975564     1   0.000      0.891 1.000  0 0.000
#&gt; SRR975565     1   0.000      0.891 1.000  0 0.000
#&gt; SRR975566     1   0.000      0.891 1.000  0 0.000
#&gt; SRR975567     1   0.000      0.891 1.000  0 0.000
#&gt; SRR975568     1   0.000      0.891 1.000  0 0.000
#&gt; SRR975569     2   0.000      1.000 0.000  1 0.000
#&gt; SRR975570     2   0.000      1.000 0.000  1 0.000
#&gt; SRR975571     2   0.000      1.000 0.000  1 0.000
#&gt; SRR975572     2   0.000      1.000 0.000  1 0.000
#&gt; SRR975573     2   0.000      1.000 0.000  1 0.000
#&gt; SRR975574     2   0.000      1.000 0.000  1 0.000
#&gt; SRR975575     2   0.000      1.000 0.000  1 0.000
#&gt; SRR975576     2   0.000      1.000 0.000  1 0.000
#&gt; SRR975577     2   0.000      1.000 0.000  1 0.000
#&gt; SRR975578     2   0.000      1.000 0.000  1 0.000
#&gt; SRR975579     2   0.000      1.000 0.000  1 0.000
#&gt; SRR975580     2   0.000      1.000 0.000  1 0.000
#&gt; SRR975581     2   0.000      1.000 0.000  1 0.000
#&gt; SRR975582     2   0.000      1.000 0.000  1 0.000
#&gt; SRR975583     2   0.000      1.000 0.000  1 0.000
#&gt; SRR975584     2   0.000      1.000 0.000  1 0.000
#&gt; SRR975585     2   0.000      1.000 0.000  1 0.000
#&gt; SRR975586     2   0.000      1.000 0.000  1 0.000
#&gt; SRR975587     3   0.000      1.000 0.000  0 1.000
#&gt; SRR975588     2   0.000      1.000 0.000  1 0.000
#&gt; SRR975589     1   0.593      0.594 0.644  0 0.356
#&gt; SRR975590     1   0.593      0.594 0.644  0 0.356
#&gt; SRR975591     3   0.000      1.000 0.000  0 1.000
#&gt; SRR975592     1   0.601      0.566 0.628  0 0.372
#&gt; SRR975593     1   0.595      0.588 0.640  0 0.360
#&gt; SRR975594     3   0.000      1.000 0.000  0 1.000
#&gt; SRR975595     1   0.455      0.775 0.800  0 0.200
#&gt; SRR975597     1   0.455      0.775 0.800  0 0.200
#&gt; SRR975596     1   0.000      0.891 1.000  0 0.000
#&gt; SRR975598     1   0.455      0.775 0.800  0 0.200
#&gt; SRR975599     3   0.000      1.000 0.000  0 1.000
#&gt; SRR975600     3   0.000      1.000 0.000  0 1.000
#&gt; SRR975601     3   0.000      1.000 0.000  0 1.000
#&gt; SRR975602     1   0.000      0.891 1.000  0 0.000
#&gt; SRR975603     3   0.000      1.000 0.000  0 1.000
#&gt; SRR975604     3   0.000      1.000 0.000  0 1.000
</code></pre>

<script>
$('#tab-MAD-skmeans-get-classes-2-a').parent().next().next().hide();
$('#tab-MAD-skmeans-get-classes-2-a').click(function(){
  $('#tab-MAD-skmeans-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-skmeans-get-classes-3'>
<p><a id='tab-MAD-skmeans-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3    p4
#&gt; SRR975551     1  0.0000     0.8472 1.000 0.000 0.000 0.000
#&gt; SRR975552     1  0.0000     0.8472 1.000 0.000 0.000 0.000
#&gt; SRR975554     1  0.0000     0.8472 1.000 0.000 0.000 0.000
#&gt; SRR975553     2  0.0000     0.9587 0.000 1.000 0.000 0.000
#&gt; SRR975555     1  0.0000     0.8472 1.000 0.000 0.000 0.000
#&gt; SRR975556     2  0.0188     0.9554 0.000 0.996 0.000 0.004
#&gt; SRR975557     3  0.5257     0.4567 0.008 0.000 0.548 0.444
#&gt; SRR975558     4  0.7058     0.2481 0.344 0.000 0.136 0.520
#&gt; SRR975559     1  0.3617     0.7455 0.860 0.000 0.076 0.064
#&gt; SRR975560     4  0.4382     0.3675 0.000 0.296 0.000 0.704
#&gt; SRR975561     2  0.4040     0.6649 0.000 0.752 0.000 0.248
#&gt; SRR975562     1  0.1474     0.8233 0.948 0.000 0.000 0.052
#&gt; SRR975563     2  0.0000     0.9587 0.000 1.000 0.000 0.000
#&gt; SRR975564     1  0.0188     0.8460 0.996 0.000 0.000 0.004
#&gt; SRR975565     1  0.0000     0.8472 1.000 0.000 0.000 0.000
#&gt; SRR975566     1  0.2089     0.8133 0.932 0.000 0.020 0.048
#&gt; SRR975567     4  0.6885     0.2023 0.372 0.000 0.112 0.516
#&gt; SRR975568     1  0.0000     0.8472 1.000 0.000 0.000 0.000
#&gt; SRR975569     2  0.0000     0.9587 0.000 1.000 0.000 0.000
#&gt; SRR975570     2  0.0000     0.9587 0.000 1.000 0.000 0.000
#&gt; SRR975571     2  0.0000     0.9587 0.000 1.000 0.000 0.000
#&gt; SRR975572     2  0.0000     0.9587 0.000 1.000 0.000 0.000
#&gt; SRR975573     2  0.0000     0.9587 0.000 1.000 0.000 0.000
#&gt; SRR975574     2  0.0000     0.9587 0.000 1.000 0.000 0.000
#&gt; SRR975575     2  0.0000     0.9587 0.000 1.000 0.000 0.000
#&gt; SRR975576     2  0.0000     0.9587 0.000 1.000 0.000 0.000
#&gt; SRR975577     2  0.0000     0.9587 0.000 1.000 0.000 0.000
#&gt; SRR975578     2  0.0000     0.9587 0.000 1.000 0.000 0.000
#&gt; SRR975579     4  0.4699     0.2809 0.000 0.320 0.004 0.676
#&gt; SRR975580     2  0.3907     0.6891 0.000 0.768 0.000 0.232
#&gt; SRR975581     2  0.0000     0.9587 0.000 1.000 0.000 0.000
#&gt; SRR975582     2  0.0000     0.9587 0.000 1.000 0.000 0.000
#&gt; SRR975583     2  0.0000     0.9587 0.000 1.000 0.000 0.000
#&gt; SRR975584     2  0.0000     0.9587 0.000 1.000 0.000 0.000
#&gt; SRR975585     2  0.0000     0.9587 0.000 1.000 0.000 0.000
#&gt; SRR975586     2  0.4040     0.6649 0.000 0.752 0.000 0.248
#&gt; SRR975587     3  0.2149     0.7302 0.088 0.000 0.912 0.000
#&gt; SRR975588     2  0.0000     0.9587 0.000 1.000 0.000 0.000
#&gt; SRR975589     3  0.6074     0.2339 0.340 0.000 0.600 0.060
#&gt; SRR975590     1  0.4697     0.4321 0.644 0.000 0.356 0.000
#&gt; SRR975591     3  0.0000     0.7630 0.000 0.000 1.000 0.000
#&gt; SRR975592     1  0.4996     0.0432 0.516 0.000 0.484 0.000
#&gt; SRR975593     3  0.5986     0.2898 0.320 0.000 0.620 0.060
#&gt; SRR975594     3  0.3907     0.6834 0.000 0.000 0.768 0.232
#&gt; SRR975595     1  0.3074     0.7548 0.848 0.000 0.152 0.000
#&gt; SRR975597     1  0.3074     0.7548 0.848 0.000 0.152 0.000
#&gt; SRR975596     1  0.3900     0.7270 0.844 0.000 0.084 0.072
#&gt; SRR975598     1  0.3074     0.7548 0.848 0.000 0.152 0.000
#&gt; SRR975599     3  0.4567     0.6699 0.016 0.000 0.740 0.244
#&gt; SRR975600     3  0.0188     0.7621 0.000 0.000 0.996 0.004
#&gt; SRR975601     3  0.2342     0.7500 0.008 0.000 0.912 0.080
#&gt; SRR975602     1  0.0000     0.8472 1.000 0.000 0.000 0.000
#&gt; SRR975603     3  0.0188     0.7621 0.000 0.000 0.996 0.004
#&gt; SRR975604     3  0.0336     0.7635 0.000 0.000 0.992 0.008
</code></pre>

<script>
$('#tab-MAD-skmeans-get-classes-3-a').parent().next().next().hide();
$('#tab-MAD-skmeans-get-classes-3-a').click(function(){
  $('#tab-MAD-skmeans-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-skmeans-get-classes-4'>
<p><a id='tab-MAD-skmeans-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3    p4    p5
#&gt; SRR975551     1  0.0451    0.79049 0.988 0.000 0.000 0.004 0.008
#&gt; SRR975552     1  0.0693    0.79090 0.980 0.000 0.000 0.008 0.012
#&gt; SRR975554     1  0.0510    0.78916 0.984 0.000 0.000 0.000 0.016
#&gt; SRR975553     2  0.1502    0.88258 0.000 0.940 0.000 0.056 0.004
#&gt; SRR975555     1  0.0404    0.79064 0.988 0.000 0.000 0.000 0.012
#&gt; SRR975556     2  0.2172    0.82742 0.000 0.908 0.000 0.076 0.016
#&gt; SRR975557     4  0.6137   -0.06114 0.000 0.000 0.392 0.476 0.132
#&gt; SRR975558     5  0.1281    0.38743 0.032 0.000 0.012 0.000 0.956
#&gt; SRR975559     5  0.4907    0.32650 0.488 0.000 0.000 0.024 0.488
#&gt; SRR975560     4  0.5456    0.25881 0.000 0.060 0.000 0.484 0.456
#&gt; SRR975561     2  0.4978    0.11538 0.000 0.496 0.000 0.476 0.028
#&gt; SRR975562     1  0.4243    0.35666 0.712 0.000 0.000 0.024 0.264
#&gt; SRR975563     2  0.0162    0.89017 0.000 0.996 0.000 0.000 0.004
#&gt; SRR975564     1  0.1768    0.74953 0.924 0.000 0.000 0.004 0.072
#&gt; SRR975565     1  0.0404    0.79059 0.988 0.000 0.000 0.000 0.012
#&gt; SRR975566     1  0.4404    0.24004 0.684 0.000 0.000 0.024 0.292
#&gt; SRR975567     5  0.1444    0.39827 0.040 0.000 0.012 0.000 0.948
#&gt; SRR975568     1  0.0703    0.78753 0.976 0.000 0.000 0.000 0.024
#&gt; SRR975569     2  0.0000    0.89024 0.000 1.000 0.000 0.000 0.000
#&gt; SRR975570     2  0.0000    0.89024 0.000 1.000 0.000 0.000 0.000
#&gt; SRR975571     2  0.1502    0.88258 0.000 0.940 0.000 0.056 0.004
#&gt; SRR975572     2  0.0162    0.89017 0.000 0.996 0.000 0.000 0.004
#&gt; SRR975573     2  0.1502    0.88258 0.000 0.940 0.000 0.056 0.004
#&gt; SRR975574     2  0.1502    0.88258 0.000 0.940 0.000 0.056 0.004
#&gt; SRR975575     2  0.0162    0.89017 0.000 0.996 0.000 0.000 0.004
#&gt; SRR975576     2  0.0162    0.89017 0.000 0.996 0.000 0.000 0.004
#&gt; SRR975577     2  0.1502    0.88258 0.000 0.940 0.000 0.056 0.004
#&gt; SRR975578     2  0.1502    0.88258 0.000 0.940 0.000 0.056 0.004
#&gt; SRR975579     4  0.3857    0.47069 0.000 0.088 0.052 0.832 0.028
#&gt; SRR975580     2  0.5176    0.20955 0.000 0.492 0.000 0.468 0.040
#&gt; SRR975581     2  0.0162    0.89017 0.000 0.996 0.000 0.000 0.004
#&gt; SRR975582     2  0.1502    0.88258 0.000 0.940 0.000 0.056 0.004
#&gt; SRR975583     2  0.0162    0.89017 0.000 0.996 0.000 0.000 0.004
#&gt; SRR975584     2  0.1502    0.88258 0.000 0.940 0.000 0.056 0.004
#&gt; SRR975585     2  0.0162    0.89017 0.000 0.996 0.000 0.000 0.004
#&gt; SRR975586     2  0.5296    0.08208 0.000 0.484 0.000 0.468 0.048
#&gt; SRR975587     3  0.1670    0.63818 0.052 0.000 0.936 0.012 0.000
#&gt; SRR975588     2  0.0000    0.89024 0.000 1.000 0.000 0.000 0.000
#&gt; SRR975589     3  0.5967    0.31990 0.056 0.000 0.508 0.024 0.412
#&gt; SRR975590     1  0.4971    0.42452 0.628 0.000 0.332 0.036 0.004
#&gt; SRR975591     3  0.2424    0.66811 0.000 0.000 0.868 0.000 0.132
#&gt; SRR975592     3  0.5338    0.00385 0.456 0.000 0.504 0.024 0.016
#&gt; SRR975593     3  0.5853    0.33424 0.048 0.000 0.516 0.024 0.412
#&gt; SRR975594     3  0.3424    0.36759 0.000 0.000 0.760 0.240 0.000
#&gt; SRR975595     1  0.4043    0.67792 0.792 0.000 0.160 0.036 0.012
#&gt; SRR975597     1  0.4012    0.67098 0.788 0.000 0.168 0.036 0.008
#&gt; SRR975596     5  0.4979    0.34455 0.480 0.000 0.000 0.028 0.492
#&gt; SRR975598     1  0.3962    0.68501 0.800 0.000 0.152 0.036 0.012
#&gt; SRR975599     3  0.4986    0.17863 0.032 0.000 0.608 0.356 0.004
#&gt; SRR975600     3  0.2605    0.66359 0.000 0.000 0.852 0.000 0.148
#&gt; SRR975601     3  0.0912    0.63177 0.012 0.000 0.972 0.016 0.000
#&gt; SRR975602     1  0.1153    0.78001 0.964 0.000 0.004 0.024 0.008
#&gt; SRR975603     3  0.2424    0.66811 0.000 0.000 0.868 0.000 0.132
#&gt; SRR975604     3  0.1608    0.66177 0.000 0.000 0.928 0.000 0.072
</code></pre>

<script>
$('#tab-MAD-skmeans-get-classes-4-a').parent().next().next().hide();
$('#tab-MAD-skmeans-get-classes-4-a').click(function(){
  $('#tab-MAD-skmeans-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-skmeans-get-classes-5'>
<p><a id='tab-MAD-skmeans-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3    p4    p5    p6
#&gt; SRR975551     1  0.0725     0.7243 0.976 0.000 0.000 0.012 0.000 0.012
#&gt; SRR975552     1  0.1226     0.7221 0.952 0.000 0.000 0.040 0.004 0.004
#&gt; SRR975554     1  0.1757     0.7075 0.916 0.000 0.000 0.076 0.000 0.008
#&gt; SRR975553     2  0.0000     0.7498 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR975555     1  0.1620     0.7190 0.940 0.000 0.000 0.024 0.012 0.024
#&gt; SRR975556     2  0.3869     0.2617 0.000 0.500 0.000 0.000 0.000 0.500
#&gt; SRR975557     5  0.2766     0.6280 0.000 0.000 0.124 0.020 0.852 0.004
#&gt; SRR975558     4  0.4348     0.4367 0.024 0.000 0.056 0.788 0.032 0.100
#&gt; SRR975559     4  0.4242     0.3029 0.412 0.000 0.012 0.572 0.004 0.000
#&gt; SRR975560     6  0.4660     0.1884 0.000 0.008 0.000 0.308 0.048 0.636
#&gt; SRR975561     6  0.4612     0.5245 0.000 0.284 0.000 0.008 0.052 0.656
#&gt; SRR975562     1  0.4415     0.0674 0.556 0.000 0.000 0.420 0.020 0.004
#&gt; SRR975563     2  0.3175     0.8007 0.000 0.744 0.000 0.000 0.000 0.256
#&gt; SRR975564     1  0.2306     0.6779 0.888 0.000 0.000 0.092 0.004 0.016
#&gt; SRR975565     1  0.0806     0.7216 0.972 0.000 0.000 0.020 0.000 0.008
#&gt; SRR975566     1  0.4032     0.4539 0.696 0.000 0.012 0.280 0.008 0.004
#&gt; SRR975567     4  0.4356     0.4560 0.040 0.000 0.044 0.792 0.032 0.092
#&gt; SRR975568     1  0.1605     0.7114 0.936 0.000 0.000 0.044 0.004 0.016
#&gt; SRR975569     2  0.3151     0.8002 0.000 0.748 0.000 0.000 0.000 0.252
#&gt; SRR975570     2  0.3175     0.8007 0.000 0.744 0.000 0.000 0.000 0.256
#&gt; SRR975571     2  0.0000     0.7498 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR975572     2  0.3175     0.8007 0.000 0.744 0.000 0.000 0.000 0.256
#&gt; SRR975573     2  0.0000     0.7498 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR975574     2  0.0000     0.7498 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR975575     2  0.3175     0.8007 0.000 0.744 0.000 0.000 0.000 0.256
#&gt; SRR975576     2  0.3175     0.8007 0.000 0.744 0.000 0.000 0.000 0.256
#&gt; SRR975577     2  0.0000     0.7498 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR975578     2  0.0000     0.7498 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR975579     5  0.2420     0.5230 0.000 0.004 0.000 0.004 0.864 0.128
#&gt; SRR975580     6  0.4790     0.5998 0.000 0.368 0.000 0.016 0.032 0.584
#&gt; SRR975581     2  0.3175     0.8007 0.000 0.744 0.000 0.000 0.000 0.256
#&gt; SRR975582     2  0.0000     0.7498 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR975583     2  0.3175     0.8007 0.000 0.744 0.000 0.000 0.000 0.256
#&gt; SRR975584     2  0.0000     0.7498 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR975585     2  0.3175     0.8007 0.000 0.744 0.000 0.000 0.000 0.256
#&gt; SRR975586     6  0.4075     0.6487 0.000 0.204 0.000 0.016 0.036 0.744
#&gt; SRR975587     3  0.3023     0.6768 0.008 0.000 0.872 0.032 0.052 0.036
#&gt; SRR975588     2  0.3175     0.8007 0.000 0.744 0.000 0.000 0.000 0.256
#&gt; SRR975589     3  0.4476     0.5929 0.012 0.000 0.680 0.276 0.012 0.020
#&gt; SRR975590     1  0.6170     0.3186 0.540 0.000 0.324 0.072 0.024 0.040
#&gt; SRR975591     3  0.0858     0.7484 0.000 0.000 0.968 0.028 0.004 0.000
#&gt; SRR975592     3  0.5743     0.4024 0.288 0.000 0.588 0.088 0.020 0.016
#&gt; SRR975593     3  0.4291     0.5834 0.008 0.000 0.676 0.292 0.012 0.012
#&gt; SRR975594     5  0.4786     0.2934 0.000 0.000 0.468 0.012 0.492 0.028
#&gt; SRR975595     1  0.6060     0.5973 0.664 0.000 0.116 0.104 0.048 0.068
#&gt; SRR975597     1  0.5903     0.5992 0.676 0.000 0.124 0.088 0.044 0.068
#&gt; SRR975596     4  0.4209     0.3078 0.396 0.000 0.012 0.588 0.004 0.000
#&gt; SRR975598     1  0.6060     0.5973 0.664 0.000 0.116 0.104 0.048 0.068
#&gt; SRR975599     5  0.5914     0.5501 0.032 0.000 0.228 0.068 0.628 0.044
#&gt; SRR975600     3  0.1364     0.7457 0.000 0.000 0.944 0.048 0.004 0.004
#&gt; SRR975601     3  0.3320     0.6388 0.000 0.000 0.844 0.032 0.076 0.048
#&gt; SRR975602     1  0.3300     0.6873 0.832 0.000 0.000 0.116 0.032 0.020
#&gt; SRR975603     3  0.0858     0.7484 0.000 0.000 0.968 0.028 0.004 0.000
#&gt; SRR975604     3  0.0653     0.7367 0.000 0.000 0.980 0.004 0.012 0.004
</code></pre>

<script>
$('#tab-MAD-skmeans-get-classes-5-a').parent().next().next().hide();
$('#tab-MAD-skmeans-get-classes-5-a').click(function(){
  $('#tab-MAD-skmeans-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-MAD-skmeans-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-MAD-skmeans-consensus-heatmap'>
<ul>
<li><a href='#tab-MAD-skmeans-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-MAD-skmeans-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-MAD-skmeans-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-MAD-skmeans-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-MAD-skmeans-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-skmeans-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-consensus-heatmap-1-1.png" alt="plot of chunk tab-MAD-skmeans-consensus-heatmap-1"/></p>

</div>
<div id='tab-MAD-skmeans-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-consensus-heatmap-2-1.png" alt="plot of chunk tab-MAD-skmeans-consensus-heatmap-2"/></p>

</div>
<div id='tab-MAD-skmeans-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-consensus-heatmap-3-1.png" alt="plot of chunk tab-MAD-skmeans-consensus-heatmap-3"/></p>

</div>
<div id='tab-MAD-skmeans-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-consensus-heatmap-4-1.png" alt="plot of chunk tab-MAD-skmeans-consensus-heatmap-4"/></p>

</div>
<div id='tab-MAD-skmeans-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-consensus-heatmap-5-1.png" alt="plot of chunk tab-MAD-skmeans-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-MAD-skmeans-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-MAD-skmeans-membership-heatmap'>
<ul>
<li><a href='#tab-MAD-skmeans-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-MAD-skmeans-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-MAD-skmeans-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-MAD-skmeans-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-MAD-skmeans-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-skmeans-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-membership-heatmap-1-1.png" alt="plot of chunk tab-MAD-skmeans-membership-heatmap-1"/></p>

</div>
<div id='tab-MAD-skmeans-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-membership-heatmap-2-1.png" alt="plot of chunk tab-MAD-skmeans-membership-heatmap-2"/></p>

</div>
<div id='tab-MAD-skmeans-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-membership-heatmap-3-1.png" alt="plot of chunk tab-MAD-skmeans-membership-heatmap-3"/></p>

</div>
<div id='tab-MAD-skmeans-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-membership-heatmap-4-1.png" alt="plot of chunk tab-MAD-skmeans-membership-heatmap-4"/></p>

</div>
<div id='tab-MAD-skmeans-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-membership-heatmap-5-1.png" alt="plot of chunk tab-MAD-skmeans-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-MAD-skmeans-get-signatures' ).tabs();
} );
</script>
<div id='tabs-MAD-skmeans-get-signatures'>
<ul>
<li><a href='#tab-MAD-skmeans-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-MAD-skmeans-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-MAD-skmeans-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-MAD-skmeans-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-MAD-skmeans-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-skmeans-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-get-signatures-1-1.png" alt="plot of chunk tab-MAD-skmeans-get-signatures-1"/></p>

</div>
<div id='tab-MAD-skmeans-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-get-signatures-2-1.png" alt="plot of chunk tab-MAD-skmeans-get-signatures-2"/></p>

</div>
<div id='tab-MAD-skmeans-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-get-signatures-3-1.png" alt="plot of chunk tab-MAD-skmeans-get-signatures-3"/></p>

</div>
<div id='tab-MAD-skmeans-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-get-signatures-4-1.png" alt="plot of chunk tab-MAD-skmeans-get-signatures-4"/></p>

</div>
<div id='tab-MAD-skmeans-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-get-signatures-5-1.png" alt="plot of chunk tab-MAD-skmeans-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-MAD-skmeans-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-MAD-skmeans-get-signatures-no-scale'>
<ul>
<li><a href='#tab-MAD-skmeans-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-MAD-skmeans-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-MAD-skmeans-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-MAD-skmeans-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-MAD-skmeans-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-skmeans-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-MAD-skmeans-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-MAD-skmeans-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-MAD-skmeans-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-MAD-skmeans-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-MAD-skmeans-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-MAD-skmeans-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-MAD-skmeans-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-MAD-skmeans-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-MAD-skmeans-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk MAD-skmeans-signature_compare](figure_cola/MAD-skmeans-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-MAD-skmeans-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-MAD-skmeans-dimension-reduction'>
<ul>
<li><a href='#tab-MAD-skmeans-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-MAD-skmeans-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-MAD-skmeans-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-MAD-skmeans-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-MAD-skmeans-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-skmeans-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-dimension-reduction-1-1.png" alt="plot of chunk tab-MAD-skmeans-dimension-reduction-1"/></p>

</div>
<div id='tab-MAD-skmeans-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-dimension-reduction-2-1.png" alt="plot of chunk tab-MAD-skmeans-dimension-reduction-2"/></p>

</div>
<div id='tab-MAD-skmeans-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-dimension-reduction-3-1.png" alt="plot of chunk tab-MAD-skmeans-dimension-reduction-3"/></p>

</div>
<div id='tab-MAD-skmeans-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-dimension-reduction-4-1.png" alt="plot of chunk tab-MAD-skmeans-dimension-reduction-4"/></p>

</div>
<div id='tab-MAD-skmeans-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-dimension-reduction-5-1.png" alt="plot of chunk tab-MAD-skmeans-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk MAD-skmeans-collect-classes](figure_cola/MAD-skmeans-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### MAD:pam**






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["MAD", "pam"]
# you can also extract it by
# res = res_list["MAD:pam"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 17171 rows and 54 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'MAD' method.
#>   Subgroups are detected by 'pam' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 2.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk MAD-pam-collect-plots](figure_cola/MAD-pam-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk MAD-pam-select-partition-number](figure_cola/MAD-pam-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 1.000           1.000       1.000         0.5037 0.497   0.497
#> 3 3 0.809           0.894       0.928         0.2848 0.816   0.642
#> 4 4 0.797           0.811       0.895         0.1148 0.909   0.751
#> 5 5 0.749           0.736       0.856         0.0323 0.918   0.749
#> 6 6 0.740           0.712       0.812         0.0719 0.892   0.631
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 2
```


Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-MAD-pam-get-classes' ).tabs();
} );
</script>
<div id='tabs-MAD-pam-get-classes'>
<ul>
<li><a href='#tab-MAD-pam-get-classes-1'>k = 2</a></li>
<li><a href='#tab-MAD-pam-get-classes-2'>k = 3</a></li>
<li><a href='#tab-MAD-pam-get-classes-3'>k = 4</a></li>
<li><a href='#tab-MAD-pam-get-classes-4'>k = 5</a></li>
<li><a href='#tab-MAD-pam-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-MAD-pam-get-classes-1'>
<p><a id='tab-MAD-pam-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2
#&gt; SRR975551     1  0.0000      1.000 1.000 0.000
#&gt; SRR975552     1  0.0000      1.000 1.000 0.000
#&gt; SRR975554     1  0.0000      1.000 1.000 0.000
#&gt; SRR975553     2  0.0000      1.000 0.000 1.000
#&gt; SRR975555     1  0.0000      1.000 1.000 0.000
#&gt; SRR975556     2  0.0000      1.000 0.000 1.000
#&gt; SRR975557     1  0.0000      1.000 1.000 0.000
#&gt; SRR975558     1  0.0672      0.992 0.992 0.008
#&gt; SRR975559     1  0.0000      1.000 1.000 0.000
#&gt; SRR975560     2  0.0000      1.000 0.000 1.000
#&gt; SRR975561     2  0.0000      1.000 0.000 1.000
#&gt; SRR975562     1  0.0000      1.000 1.000 0.000
#&gt; SRR975563     2  0.0000      1.000 0.000 1.000
#&gt; SRR975564     1  0.0000      1.000 1.000 0.000
#&gt; SRR975565     1  0.0000      1.000 1.000 0.000
#&gt; SRR975566     1  0.0000      1.000 1.000 0.000
#&gt; SRR975567     1  0.0000      1.000 1.000 0.000
#&gt; SRR975568     1  0.0000      1.000 1.000 0.000
#&gt; SRR975569     2  0.0000      1.000 0.000 1.000
#&gt; SRR975570     2  0.0000      1.000 0.000 1.000
#&gt; SRR975571     2  0.0000      1.000 0.000 1.000
#&gt; SRR975572     2  0.0000      1.000 0.000 1.000
#&gt; SRR975573     2  0.0000      1.000 0.000 1.000
#&gt; SRR975574     2  0.0000      1.000 0.000 1.000
#&gt; SRR975575     2  0.0000      1.000 0.000 1.000
#&gt; SRR975576     2  0.0000      1.000 0.000 1.000
#&gt; SRR975577     2  0.0000      1.000 0.000 1.000
#&gt; SRR975578     2  0.0000      1.000 0.000 1.000
#&gt; SRR975579     2  0.0000      1.000 0.000 1.000
#&gt; SRR975580     2  0.0000      1.000 0.000 1.000
#&gt; SRR975581     2  0.0000      1.000 0.000 1.000
#&gt; SRR975582     2  0.0000      1.000 0.000 1.000
#&gt; SRR975583     2  0.0000      1.000 0.000 1.000
#&gt; SRR975584     2  0.0000      1.000 0.000 1.000
#&gt; SRR975585     2  0.0000      1.000 0.000 1.000
#&gt; SRR975586     2  0.0000      1.000 0.000 1.000
#&gt; SRR975587     1  0.0000      1.000 1.000 0.000
#&gt; SRR975588     2  0.0000      1.000 0.000 1.000
#&gt; SRR975589     1  0.0000      1.000 1.000 0.000
#&gt; SRR975590     1  0.0000      1.000 1.000 0.000
#&gt; SRR975591     1  0.0000      1.000 1.000 0.000
#&gt; SRR975592     1  0.0000      1.000 1.000 0.000
#&gt; SRR975593     1  0.0000      1.000 1.000 0.000
#&gt; SRR975594     1  0.0000      1.000 1.000 0.000
#&gt; SRR975595     1  0.0000      1.000 1.000 0.000
#&gt; SRR975597     1  0.0000      1.000 1.000 0.000
#&gt; SRR975596     1  0.0000      1.000 1.000 0.000
#&gt; SRR975598     1  0.0000      1.000 1.000 0.000
#&gt; SRR975599     1  0.0000      1.000 1.000 0.000
#&gt; SRR975600     1  0.0000      1.000 1.000 0.000
#&gt; SRR975601     1  0.0000      1.000 1.000 0.000
#&gt; SRR975602     1  0.0000      1.000 1.000 0.000
#&gt; SRR975603     1  0.0000      1.000 1.000 0.000
#&gt; SRR975604     1  0.0000      1.000 1.000 0.000
</code></pre>

<script>
$('#tab-MAD-pam-get-classes-1-a').parent().next().next().hide();
$('#tab-MAD-pam-get-classes-1-a').click(function(){
  $('#tab-MAD-pam-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-pam-get-classes-2'>
<p><a id='tab-MAD-pam-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3
#&gt; SRR975551     1  0.0000      0.788 1.000 0.000 0.000
#&gt; SRR975552     1  0.0000      0.788 1.000 0.000 0.000
#&gt; SRR975554     1  0.5058      0.859 0.756 0.000 0.244
#&gt; SRR975553     2  0.0000      0.980 0.000 1.000 0.000
#&gt; SRR975555     1  0.0424      0.795 0.992 0.000 0.008
#&gt; SRR975556     2  0.0000      0.980 0.000 1.000 0.000
#&gt; SRR975557     3  0.0237      0.896 0.004 0.000 0.996
#&gt; SRR975558     2  0.7001      0.706 0.200 0.716 0.084
#&gt; SRR975559     1  0.5216      0.844 0.740 0.000 0.260
#&gt; SRR975560     2  0.4452      0.811 0.192 0.808 0.000
#&gt; SRR975561     2  0.0000      0.980 0.000 1.000 0.000
#&gt; SRR975562     1  0.5098      0.857 0.752 0.000 0.248
#&gt; SRR975563     2  0.0000      0.980 0.000 1.000 0.000
#&gt; SRR975564     1  0.4452      0.888 0.808 0.000 0.192
#&gt; SRR975565     1  0.1163      0.809 0.972 0.000 0.028
#&gt; SRR975566     3  0.3752      0.783 0.144 0.000 0.856
#&gt; SRR975567     3  0.5465      0.645 0.288 0.000 0.712
#&gt; SRR975568     1  0.4235      0.883 0.824 0.000 0.176
#&gt; SRR975569     2  0.0000      0.980 0.000 1.000 0.000
#&gt; SRR975570     2  0.0000      0.980 0.000 1.000 0.000
#&gt; SRR975571     2  0.0000      0.980 0.000 1.000 0.000
#&gt; SRR975572     2  0.0000      0.980 0.000 1.000 0.000
#&gt; SRR975573     2  0.0000      0.980 0.000 1.000 0.000
#&gt; SRR975574     2  0.0000      0.980 0.000 1.000 0.000
#&gt; SRR975575     2  0.0000      0.980 0.000 1.000 0.000
#&gt; SRR975576     2  0.0000      0.980 0.000 1.000 0.000
#&gt; SRR975577     2  0.0000      0.980 0.000 1.000 0.000
#&gt; SRR975578     2  0.0000      0.980 0.000 1.000 0.000
#&gt; SRR975579     2  0.2261      0.928 0.068 0.932 0.000
#&gt; SRR975580     2  0.0000      0.980 0.000 1.000 0.000
#&gt; SRR975581     2  0.0000      0.980 0.000 1.000 0.000
#&gt; SRR975582     2  0.0000      0.980 0.000 1.000 0.000
#&gt; SRR975583     2  0.0000      0.980 0.000 1.000 0.000
#&gt; SRR975584     2  0.0000      0.980 0.000 1.000 0.000
#&gt; SRR975585     2  0.0000      0.980 0.000 1.000 0.000
#&gt; SRR975586     2  0.0000      0.980 0.000 1.000 0.000
#&gt; SRR975587     3  0.1964      0.870 0.056 0.000 0.944
#&gt; SRR975588     2  0.0000      0.980 0.000 1.000 0.000
#&gt; SRR975589     3  0.0000      0.898 0.000 0.000 1.000
#&gt; SRR975590     1  0.4605      0.885 0.796 0.000 0.204
#&gt; SRR975591     3  0.0000      0.898 0.000 0.000 1.000
#&gt; SRR975592     3  0.3192      0.811 0.112 0.000 0.888
#&gt; SRR975593     3  0.0000      0.898 0.000 0.000 1.000
#&gt; SRR975594     3  0.0000      0.898 0.000 0.000 1.000
#&gt; SRR975595     1  0.4887      0.864 0.772 0.000 0.228
#&gt; SRR975597     1  0.4555      0.886 0.800 0.000 0.200
#&gt; SRR975596     3  0.4654      0.692 0.208 0.000 0.792
#&gt; SRR975598     1  0.4504      0.887 0.804 0.000 0.196
#&gt; SRR975599     3  0.5465      0.517 0.288 0.000 0.712
#&gt; SRR975600     3  0.0000      0.898 0.000 0.000 1.000
#&gt; SRR975601     3  0.1860      0.872 0.052 0.000 0.948
#&gt; SRR975602     1  0.4504      0.887 0.804 0.000 0.196
#&gt; SRR975603     3  0.0000      0.898 0.000 0.000 1.000
#&gt; SRR975604     3  0.0000      0.898 0.000 0.000 1.000
</code></pre>

<script>
$('#tab-MAD-pam-get-classes-2-a').parent().next().next().hide();
$('#tab-MAD-pam-get-classes-2-a').click(function(){
  $('#tab-MAD-pam-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-pam-get-classes-3'>
<p><a id='tab-MAD-pam-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3    p4
#&gt; SRR975551     1  0.0000     0.8842 1.000 0.000 0.000 0.000
#&gt; SRR975552     1  0.2149     0.8103 0.912 0.000 0.000 0.088
#&gt; SRR975554     4  0.7072     0.6189 0.336 0.000 0.140 0.524
#&gt; SRR975553     2  0.0336     0.9090 0.000 0.992 0.000 0.008
#&gt; SRR975555     1  0.0000     0.8842 1.000 0.000 0.000 0.000
#&gt; SRR975556     2  0.1716     0.8719 0.000 0.936 0.000 0.064
#&gt; SRR975557     3  0.1302     0.9082 0.000 0.000 0.956 0.044
#&gt; SRR975558     4  0.1474     0.6714 0.000 0.000 0.052 0.948
#&gt; SRR975559     4  0.7096     0.6237 0.332 0.000 0.144 0.524
#&gt; SRR975560     2  0.4941     0.5020 0.000 0.564 0.000 0.436
#&gt; SRR975561     2  0.3907     0.7360 0.000 0.768 0.000 0.232
#&gt; SRR975562     4  0.5985     0.7537 0.168 0.000 0.140 0.692
#&gt; SRR975563     2  0.0000     0.9094 0.000 1.000 0.000 0.000
#&gt; SRR975564     1  0.0895     0.8757 0.976 0.000 0.004 0.020
#&gt; SRR975565     1  0.0376     0.8833 0.992 0.000 0.004 0.004
#&gt; SRR975566     4  0.7109     0.5977 0.144 0.000 0.336 0.520
#&gt; SRR975567     4  0.1474     0.6714 0.000 0.000 0.052 0.948
#&gt; SRR975568     1  0.2053     0.8177 0.924 0.000 0.072 0.004
#&gt; SRR975569     2  0.0000     0.9094 0.000 1.000 0.000 0.000
#&gt; SRR975570     2  0.0000     0.9094 0.000 1.000 0.000 0.000
#&gt; SRR975571     2  0.0336     0.9090 0.000 0.992 0.000 0.008
#&gt; SRR975572     2  0.0000     0.9094 0.000 1.000 0.000 0.000
#&gt; SRR975573     2  0.0336     0.9090 0.000 0.992 0.000 0.008
#&gt; SRR975574     2  0.0336     0.9090 0.000 0.992 0.000 0.008
#&gt; SRR975575     2  0.0000     0.9094 0.000 1.000 0.000 0.000
#&gt; SRR975576     2  0.0000     0.9094 0.000 1.000 0.000 0.000
#&gt; SRR975577     2  0.0336     0.9090 0.000 0.992 0.000 0.008
#&gt; SRR975578     2  0.0336     0.9090 0.000 0.992 0.000 0.008
#&gt; SRR975579     2  0.4992     0.4428 0.000 0.524 0.000 0.476
#&gt; SRR975580     2  0.4933     0.5081 0.000 0.568 0.000 0.432
#&gt; SRR975581     2  0.0000     0.9094 0.000 1.000 0.000 0.000
#&gt; SRR975582     2  0.0336     0.9090 0.000 0.992 0.000 0.008
#&gt; SRR975583     2  0.0000     0.9094 0.000 1.000 0.000 0.000
#&gt; SRR975584     2  0.0336     0.9090 0.000 0.992 0.000 0.008
#&gt; SRR975585     2  0.0000     0.9094 0.000 1.000 0.000 0.000
#&gt; SRR975586     2  0.4916     0.5098 0.000 0.576 0.000 0.424
#&gt; SRR975587     3  0.3074     0.8045 0.152 0.000 0.848 0.000
#&gt; SRR975588     2  0.0000     0.9094 0.000 1.000 0.000 0.000
#&gt; SRR975589     3  0.0000     0.9248 0.000 0.000 1.000 0.000
#&gt; SRR975590     1  0.2469     0.7876 0.892 0.000 0.108 0.000
#&gt; SRR975591     3  0.0000     0.9248 0.000 0.000 1.000 0.000
#&gt; SRR975592     3  0.3074     0.7575 0.152 0.000 0.848 0.000
#&gt; SRR975593     3  0.0000     0.9248 0.000 0.000 1.000 0.000
#&gt; SRR975594     3  0.1489     0.9070 0.004 0.000 0.952 0.044
#&gt; SRR975595     1  0.0707     0.8808 0.980 0.000 0.020 0.000
#&gt; SRR975597     1  0.1211     0.8671 0.960 0.000 0.040 0.000
#&gt; SRR975596     4  0.5948     0.7552 0.160 0.000 0.144 0.696
#&gt; SRR975598     1  0.0469     0.8835 0.988 0.000 0.012 0.000
#&gt; SRR975599     1  0.7450    -0.0201 0.424 0.000 0.404 0.172
#&gt; SRR975600     3  0.0000     0.9248 0.000 0.000 1.000 0.000
#&gt; SRR975601     3  0.2921     0.8164 0.140 0.000 0.860 0.000
#&gt; SRR975602     1  0.0000     0.8842 1.000 0.000 0.000 0.000
#&gt; SRR975603     3  0.0000     0.9248 0.000 0.000 1.000 0.000
#&gt; SRR975604     3  0.0000     0.9248 0.000 0.000 1.000 0.000
</code></pre>

<script>
$('#tab-MAD-pam-get-classes-3-a').parent().next().next().hide();
$('#tab-MAD-pam-get-classes-3-a').click(function(){
  $('#tab-MAD-pam-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-pam-get-classes-4'>
<p><a id='tab-MAD-pam-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3    p4    p5
#&gt; SRR975551     1  0.0404      0.898 0.988 0.000 0.000 0.000 0.012
#&gt; SRR975552     1  0.2471      0.832 0.864 0.000 0.000 0.000 0.136
#&gt; SRR975554     3  0.6801      0.285 0.312 0.000 0.376 0.000 0.312
#&gt; SRR975553     2  0.2719      0.867 0.000 0.852 0.000 0.144 0.004
#&gt; SRR975555     1  0.0290      0.899 0.992 0.000 0.000 0.000 0.008
#&gt; SRR975556     2  0.1197      0.872 0.000 0.952 0.000 0.048 0.000
#&gt; SRR975557     4  0.5122      0.312 0.000 0.000 0.312 0.628 0.060
#&gt; SRR975558     3  0.6572      0.351 0.000 0.000 0.460 0.228 0.312
#&gt; SRR975559     3  0.4584      0.593 0.028 0.000 0.660 0.000 0.312
#&gt; SRR975560     2  0.5172      0.624 0.000 0.616 0.000 0.324 0.060
#&gt; SRR975561     2  0.2929      0.772 0.000 0.820 0.000 0.180 0.000
#&gt; SRR975562     3  0.4348      0.595 0.016 0.000 0.668 0.000 0.316
#&gt; SRR975563     2  0.0000      0.892 0.000 1.000 0.000 0.000 0.000
#&gt; SRR975564     1  0.0880      0.894 0.968 0.000 0.000 0.000 0.032
#&gt; SRR975565     1  0.3430      0.668 0.776 0.000 0.004 0.000 0.220
#&gt; SRR975566     3  0.5672      0.538 0.104 0.000 0.584 0.000 0.312
#&gt; SRR975567     3  0.6572      0.351 0.000 0.000 0.460 0.228 0.312
#&gt; SRR975568     1  0.2344      0.854 0.904 0.000 0.064 0.000 0.032
#&gt; SRR975569     2  0.0000      0.892 0.000 1.000 0.000 0.000 0.000
#&gt; SRR975570     2  0.0000      0.892 0.000 1.000 0.000 0.000 0.000
#&gt; SRR975571     2  0.2719      0.867 0.000 0.852 0.000 0.144 0.004
#&gt; SRR975572     2  0.0000      0.892 0.000 1.000 0.000 0.000 0.000
#&gt; SRR975573     2  0.2329      0.874 0.000 0.876 0.000 0.124 0.000
#&gt; SRR975574     2  0.2536      0.872 0.000 0.868 0.000 0.128 0.004
#&gt; SRR975575     2  0.0000      0.892 0.000 1.000 0.000 0.000 0.000
#&gt; SRR975576     2  0.0000      0.892 0.000 1.000 0.000 0.000 0.000
#&gt; SRR975577     2  0.2719      0.867 0.000 0.852 0.000 0.144 0.004
#&gt; SRR975578     2  0.2719      0.867 0.000 0.852 0.000 0.144 0.004
#&gt; SRR975579     4  0.0404      0.422 0.000 0.000 0.000 0.988 0.012
#&gt; SRR975580     2  0.4101      0.660 0.000 0.628 0.000 0.372 0.000
#&gt; SRR975581     2  0.0000      0.892 0.000 1.000 0.000 0.000 0.000
#&gt; SRR975582     2  0.2536      0.872 0.000 0.868 0.000 0.128 0.004
#&gt; SRR975583     2  0.0000      0.892 0.000 1.000 0.000 0.000 0.000
#&gt; SRR975584     2  0.2719      0.867 0.000 0.852 0.000 0.144 0.004
#&gt; SRR975585     2  0.0000      0.892 0.000 1.000 0.000 0.000 0.000
#&gt; SRR975586     2  0.3336      0.710 0.000 0.772 0.000 0.228 0.000
#&gt; SRR975587     5  0.5441      0.803 0.080 0.000 0.324 0.000 0.596
#&gt; SRR975588     2  0.0000      0.892 0.000 1.000 0.000 0.000 0.000
#&gt; SRR975589     3  0.0000      0.620 0.000 0.000 1.000 0.000 0.000
#&gt; SRR975590     1  0.1041      0.899 0.964 0.000 0.032 0.000 0.004
#&gt; SRR975591     3  0.0000      0.620 0.000 0.000 1.000 0.000 0.000
#&gt; SRR975592     3  0.3661      0.195 0.276 0.000 0.724 0.000 0.000
#&gt; SRR975593     3  0.0000      0.620 0.000 0.000 1.000 0.000 0.000
#&gt; SRR975594     5  0.4138      0.740 0.000 0.000 0.384 0.000 0.616
#&gt; SRR975595     1  0.2077      0.870 0.908 0.000 0.084 0.000 0.008
#&gt; SRR975597     1  0.2077      0.870 0.908 0.000 0.084 0.000 0.008
#&gt; SRR975596     3  0.4419      0.595 0.020 0.000 0.668 0.000 0.312
#&gt; SRR975598     1  0.2077      0.870 0.908 0.000 0.084 0.000 0.008
#&gt; SRR975599     5  0.7316      0.492 0.188 0.000 0.196 0.084 0.532
#&gt; SRR975600     3  0.0000      0.620 0.000 0.000 1.000 0.000 0.000
#&gt; SRR975601     5  0.5315      0.805 0.068 0.000 0.332 0.000 0.600
#&gt; SRR975602     1  0.0290      0.898 0.992 0.000 0.000 0.000 0.008
#&gt; SRR975603     3  0.0000      0.620 0.000 0.000 1.000 0.000 0.000
#&gt; SRR975604     3  0.0000      0.620 0.000 0.000 1.000 0.000 0.000
</code></pre>

<script>
$('#tab-MAD-pam-get-classes-4-a').parent().next().next().hide();
$('#tab-MAD-pam-get-classes-4-a').click(function(){
  $('#tab-MAD-pam-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-pam-get-classes-5'>
<p><a id='tab-MAD-pam-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3    p4    p5    p6
#&gt; SRR975551     1  0.0000      0.800 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR975552     1  0.4022      0.706 0.792 0.064 0.000 0.108 0.036 0.000
#&gt; SRR975554     1  0.6141     -0.250 0.400 0.000 0.352 0.004 0.244 0.000
#&gt; SRR975553     6  0.0000      0.827 0.000 0.000 0.000 0.000 0.000 1.000
#&gt; SRR975555     1  0.0458      0.802 0.984 0.000 0.000 0.000 0.016 0.000
#&gt; SRR975556     2  0.3911      0.925 0.000 0.624 0.000 0.008 0.000 0.368
#&gt; SRR975557     4  0.2536      0.733 0.000 0.000 0.116 0.864 0.020 0.000
#&gt; SRR975558     3  0.6976      0.230 0.000 0.372 0.380 0.144 0.104 0.000
#&gt; SRR975559     3  0.4237      0.638 0.048 0.000 0.704 0.004 0.244 0.000
#&gt; SRR975560     6  0.5571      0.150 0.000 0.372 0.000 0.144 0.000 0.484
#&gt; SRR975561     2  0.4292      0.779 0.000 0.628 0.000 0.032 0.000 0.340
#&gt; SRR975562     3  0.3872      0.642 0.020 0.000 0.712 0.004 0.264 0.000
#&gt; SRR975563     2  0.3684      0.936 0.000 0.628 0.000 0.000 0.000 0.372
#&gt; SRR975564     1  0.0603      0.799 0.980 0.000 0.004 0.000 0.016 0.000
#&gt; SRR975565     1  0.3011      0.640 0.800 0.004 0.004 0.000 0.192 0.000
#&gt; SRR975566     3  0.5576      0.517 0.184 0.000 0.568 0.004 0.244 0.000
#&gt; SRR975567     3  0.7262      0.263 0.000 0.320 0.380 0.144 0.156 0.000
#&gt; SRR975568     1  0.1659      0.790 0.940 0.020 0.028 0.004 0.008 0.000
#&gt; SRR975569     2  0.3684      0.936 0.000 0.628 0.000 0.000 0.000 0.372
#&gt; SRR975570     2  0.3684      0.936 0.000 0.628 0.000 0.000 0.000 0.372
#&gt; SRR975571     6  0.0000      0.827 0.000 0.000 0.000 0.000 0.000 1.000
#&gt; SRR975572     2  0.3684      0.936 0.000 0.628 0.000 0.000 0.000 0.372
#&gt; SRR975573     6  0.1444      0.765 0.000 0.072 0.000 0.000 0.000 0.928
#&gt; SRR975574     6  0.1141      0.791 0.000 0.052 0.000 0.000 0.000 0.948
#&gt; SRR975575     2  0.3684      0.936 0.000 0.628 0.000 0.000 0.000 0.372
#&gt; SRR975576     2  0.3684      0.936 0.000 0.628 0.000 0.000 0.000 0.372
#&gt; SRR975577     6  0.0000      0.827 0.000 0.000 0.000 0.000 0.000 1.000
#&gt; SRR975578     6  0.0000      0.827 0.000 0.000 0.000 0.000 0.000 1.000
#&gt; SRR975579     4  0.2100      0.749 0.000 0.004 0.000 0.884 0.000 0.112
#&gt; SRR975580     6  0.4316      0.395 0.000 0.312 0.000 0.040 0.000 0.648
#&gt; SRR975581     2  0.3684      0.936 0.000 0.628 0.000 0.000 0.000 0.372
#&gt; SRR975582     6  0.1141      0.791 0.000 0.052 0.000 0.000 0.000 0.948
#&gt; SRR975583     2  0.3684      0.936 0.000 0.628 0.000 0.000 0.000 0.372
#&gt; SRR975584     6  0.0000      0.827 0.000 0.000 0.000 0.000 0.000 1.000
#&gt; SRR975585     2  0.3684      0.936 0.000 0.628 0.000 0.000 0.000 0.372
#&gt; SRR975586     2  0.2250      0.440 0.000 0.896 0.000 0.040 0.000 0.064
#&gt; SRR975587     5  0.3595      0.843 0.008 0.000 0.288 0.000 0.704 0.000
#&gt; SRR975588     2  0.3684      0.936 0.000 0.628 0.000 0.000 0.000 0.372
#&gt; SRR975589     3  0.0000      0.680 0.000 0.000 1.000 0.000 0.000 0.000
#&gt; SRR975590     1  0.1124      0.807 0.956 0.000 0.036 0.000 0.008 0.000
#&gt; SRR975591     3  0.0000      0.680 0.000 0.000 1.000 0.000 0.000 0.000
#&gt; SRR975592     3  0.3309      0.310 0.280 0.000 0.720 0.000 0.000 0.000
#&gt; SRR975593     3  0.0000      0.680 0.000 0.000 1.000 0.000 0.000 0.000
#&gt; SRR975594     5  0.3351      0.843 0.000 0.000 0.288 0.000 0.712 0.000
#&gt; SRR975595     1  0.3381      0.739 0.800 0.000 0.156 0.000 0.044 0.000
#&gt; SRR975597     1  0.3381      0.739 0.800 0.000 0.156 0.000 0.044 0.000
#&gt; SRR975596     3  0.4117      0.645 0.032 0.004 0.716 0.004 0.244 0.000
#&gt; SRR975598     1  0.3381      0.739 0.800 0.000 0.156 0.000 0.044 0.000
#&gt; SRR975599     5  0.6416      0.457 0.068 0.124 0.156 0.036 0.616 0.000
#&gt; SRR975600     3  0.0000      0.680 0.000 0.000 1.000 0.000 0.000 0.000
#&gt; SRR975601     5  0.3489      0.845 0.004 0.000 0.288 0.000 0.708 0.000
#&gt; SRR975602     1  0.1549      0.801 0.936 0.000 0.020 0.000 0.044 0.000
#&gt; SRR975603     3  0.0000      0.680 0.000 0.000 1.000 0.000 0.000 0.000
#&gt; SRR975604     3  0.0000      0.680 0.000 0.000 1.000 0.000 0.000 0.000
</code></pre>

<script>
$('#tab-MAD-pam-get-classes-5-a').parent().next().next().hide();
$('#tab-MAD-pam-get-classes-5-a').click(function(){
  $('#tab-MAD-pam-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-MAD-pam-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-MAD-pam-consensus-heatmap'>
<ul>
<li><a href='#tab-MAD-pam-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-MAD-pam-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-MAD-pam-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-MAD-pam-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-MAD-pam-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-pam-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-consensus-heatmap-1-1.png" alt="plot of chunk tab-MAD-pam-consensus-heatmap-1"/></p>

</div>
<div id='tab-MAD-pam-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-consensus-heatmap-2-1.png" alt="plot of chunk tab-MAD-pam-consensus-heatmap-2"/></p>

</div>
<div id='tab-MAD-pam-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-consensus-heatmap-3-1.png" alt="plot of chunk tab-MAD-pam-consensus-heatmap-3"/></p>

</div>
<div id='tab-MAD-pam-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-consensus-heatmap-4-1.png" alt="plot of chunk tab-MAD-pam-consensus-heatmap-4"/></p>

</div>
<div id='tab-MAD-pam-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-consensus-heatmap-5-1.png" alt="plot of chunk tab-MAD-pam-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-MAD-pam-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-MAD-pam-membership-heatmap'>
<ul>
<li><a href='#tab-MAD-pam-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-MAD-pam-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-MAD-pam-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-MAD-pam-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-MAD-pam-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-pam-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-membership-heatmap-1-1.png" alt="plot of chunk tab-MAD-pam-membership-heatmap-1"/></p>

</div>
<div id='tab-MAD-pam-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-membership-heatmap-2-1.png" alt="plot of chunk tab-MAD-pam-membership-heatmap-2"/></p>

</div>
<div id='tab-MAD-pam-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-membership-heatmap-3-1.png" alt="plot of chunk tab-MAD-pam-membership-heatmap-3"/></p>

</div>
<div id='tab-MAD-pam-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-membership-heatmap-4-1.png" alt="plot of chunk tab-MAD-pam-membership-heatmap-4"/></p>

</div>
<div id='tab-MAD-pam-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-membership-heatmap-5-1.png" alt="plot of chunk tab-MAD-pam-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-MAD-pam-get-signatures' ).tabs();
} );
</script>
<div id='tabs-MAD-pam-get-signatures'>
<ul>
<li><a href='#tab-MAD-pam-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-MAD-pam-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-MAD-pam-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-MAD-pam-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-MAD-pam-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-pam-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-get-signatures-1-1.png" alt="plot of chunk tab-MAD-pam-get-signatures-1"/></p>

</div>
<div id='tab-MAD-pam-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-get-signatures-2-1.png" alt="plot of chunk tab-MAD-pam-get-signatures-2"/></p>

</div>
<div id='tab-MAD-pam-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-get-signatures-3-1.png" alt="plot of chunk tab-MAD-pam-get-signatures-3"/></p>

</div>
<div id='tab-MAD-pam-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-get-signatures-4-1.png" alt="plot of chunk tab-MAD-pam-get-signatures-4"/></p>

</div>
<div id='tab-MAD-pam-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-get-signatures-5-1.png" alt="plot of chunk tab-MAD-pam-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-MAD-pam-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-MAD-pam-get-signatures-no-scale'>
<ul>
<li><a href='#tab-MAD-pam-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-MAD-pam-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-MAD-pam-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-MAD-pam-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-MAD-pam-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-pam-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-MAD-pam-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-MAD-pam-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-MAD-pam-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-MAD-pam-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-MAD-pam-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-MAD-pam-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-MAD-pam-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-MAD-pam-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-MAD-pam-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk MAD-pam-signature_compare](figure_cola/MAD-pam-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-MAD-pam-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-MAD-pam-dimension-reduction'>
<ul>
<li><a href='#tab-MAD-pam-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-MAD-pam-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-MAD-pam-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-MAD-pam-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-MAD-pam-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-pam-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-dimension-reduction-1-1.png" alt="plot of chunk tab-MAD-pam-dimension-reduction-1"/></p>

</div>
<div id='tab-MAD-pam-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-dimension-reduction-2-1.png" alt="plot of chunk tab-MAD-pam-dimension-reduction-2"/></p>

</div>
<div id='tab-MAD-pam-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-dimension-reduction-3-1.png" alt="plot of chunk tab-MAD-pam-dimension-reduction-3"/></p>

</div>
<div id='tab-MAD-pam-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-dimension-reduction-4-1.png" alt="plot of chunk tab-MAD-pam-dimension-reduction-4"/></p>

</div>
<div id='tab-MAD-pam-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-dimension-reduction-5-1.png" alt="plot of chunk tab-MAD-pam-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk MAD-pam-collect-classes](figure_cola/MAD-pam-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### MAD:mclust**






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["MAD", "mclust"]
# you can also extract it by
# res = res_list["MAD:mclust"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 17171 rows and 54 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'MAD' method.
#>   Subgroups are detected by 'mclust' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 2.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk MAD-mclust-collect-plots](figure_cola/MAD-mclust-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk MAD-mclust-select-partition-number](figure_cola/MAD-mclust-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 1.000           0.974       0.989         0.4602 0.547   0.547
#> 3 3 0.738           0.857       0.929         0.4250 0.808   0.649
#> 4 4 0.697           0.672       0.827         0.1013 0.825   0.564
#> 5 5 0.732           0.601       0.793         0.0536 0.905   0.675
#> 6 6 0.752           0.656       0.801         0.0407 0.920   0.674
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 2
```


Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-MAD-mclust-get-classes' ).tabs();
} );
</script>
<div id='tabs-MAD-mclust-get-classes'>
<ul>
<li><a href='#tab-MAD-mclust-get-classes-1'>k = 2</a></li>
<li><a href='#tab-MAD-mclust-get-classes-2'>k = 3</a></li>
<li><a href='#tab-MAD-mclust-get-classes-3'>k = 4</a></li>
<li><a href='#tab-MAD-mclust-get-classes-4'>k = 5</a></li>
<li><a href='#tab-MAD-mclust-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-MAD-mclust-get-classes-1'>
<p><a id='tab-MAD-mclust-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2
#&gt; SRR975551     1   0.000      0.982 1.000 0.000
#&gt; SRR975552     1   0.000      0.982 1.000 0.000
#&gt; SRR975554     1   0.000      0.982 1.000 0.000
#&gt; SRR975553     2   0.000      1.000 0.000 1.000
#&gt; SRR975555     1   0.000      0.982 1.000 0.000
#&gt; SRR975556     1   0.541      0.858 0.876 0.124
#&gt; SRR975557     1   0.000      0.982 1.000 0.000
#&gt; SRR975558     1   0.000      0.982 1.000 0.000
#&gt; SRR975559     1   0.000      0.982 1.000 0.000
#&gt; SRR975560     1   0.000      0.982 1.000 0.000
#&gt; SRR975561     1   0.917      0.523 0.668 0.332
#&gt; SRR975562     1   0.000      0.982 1.000 0.000
#&gt; SRR975563     2   0.000      1.000 0.000 1.000
#&gt; SRR975564     1   0.000      0.982 1.000 0.000
#&gt; SRR975565     1   0.000      0.982 1.000 0.000
#&gt; SRR975566     1   0.000      0.982 1.000 0.000
#&gt; SRR975567     1   0.000      0.982 1.000 0.000
#&gt; SRR975568     1   0.000      0.982 1.000 0.000
#&gt; SRR975569     2   0.000      1.000 0.000 1.000
#&gt; SRR975570     2   0.000      1.000 0.000 1.000
#&gt; SRR975571     2   0.000      1.000 0.000 1.000
#&gt; SRR975572     2   0.000      1.000 0.000 1.000
#&gt; SRR975573     2   0.000      1.000 0.000 1.000
#&gt; SRR975574     2   0.000      1.000 0.000 1.000
#&gt; SRR975575     2   0.000      1.000 0.000 1.000
#&gt; SRR975576     2   0.000      1.000 0.000 1.000
#&gt; SRR975577     2   0.000      1.000 0.000 1.000
#&gt; SRR975578     2   0.000      1.000 0.000 1.000
#&gt; SRR975579     1   0.000      0.982 1.000 0.000
#&gt; SRR975580     1   0.000      0.982 1.000 0.000
#&gt; SRR975581     2   0.000      1.000 0.000 1.000
#&gt; SRR975582     2   0.000      1.000 0.000 1.000
#&gt; SRR975583     2   0.000      1.000 0.000 1.000
#&gt; SRR975584     2   0.000      1.000 0.000 1.000
#&gt; SRR975585     2   0.000      1.000 0.000 1.000
#&gt; SRR975586     1   0.644      0.808 0.836 0.164
#&gt; SRR975587     1   0.000      0.982 1.000 0.000
#&gt; SRR975588     2   0.000      1.000 0.000 1.000
#&gt; SRR975589     1   0.000      0.982 1.000 0.000
#&gt; SRR975590     1   0.000      0.982 1.000 0.000
#&gt; SRR975591     1   0.000      0.982 1.000 0.000
#&gt; SRR975592     1   0.000      0.982 1.000 0.000
#&gt; SRR975593     1   0.000      0.982 1.000 0.000
#&gt; SRR975594     1   0.000      0.982 1.000 0.000
#&gt; SRR975595     1   0.000      0.982 1.000 0.000
#&gt; SRR975597     1   0.000      0.982 1.000 0.000
#&gt; SRR975596     1   0.000      0.982 1.000 0.000
#&gt; SRR975598     1   0.000      0.982 1.000 0.000
#&gt; SRR975599     1   0.000      0.982 1.000 0.000
#&gt; SRR975600     1   0.000      0.982 1.000 0.000
#&gt; SRR975601     1   0.000      0.982 1.000 0.000
#&gt; SRR975602     1   0.000      0.982 1.000 0.000
#&gt; SRR975603     1   0.000      0.982 1.000 0.000
#&gt; SRR975604     1   0.000      0.982 1.000 0.000
</code></pre>

<script>
$('#tab-MAD-mclust-get-classes-1-a').parent().next().next().hide();
$('#tab-MAD-mclust-get-classes-1-a').click(function(){
  $('#tab-MAD-mclust-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-mclust-get-classes-2'>
<p><a id='tab-MAD-mclust-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3
#&gt; SRR975551     1  0.3752      0.830 0.856 0.000 0.144
#&gt; SRR975552     1  0.3752      0.830 0.856 0.000 0.144
#&gt; SRR975554     1  0.3686      0.832 0.860 0.000 0.140
#&gt; SRR975553     2  0.0000      0.997 0.000 1.000 0.000
#&gt; SRR975555     1  0.3752      0.830 0.856 0.000 0.144
#&gt; SRR975556     3  0.0237      0.892 0.000 0.004 0.996
#&gt; SRR975557     3  0.3752      0.822 0.144 0.000 0.856
#&gt; SRR975558     3  0.0000      0.893 0.000 0.000 1.000
#&gt; SRR975559     1  0.2356      0.860 0.928 0.000 0.072
#&gt; SRR975560     3  0.0000      0.893 0.000 0.000 1.000
#&gt; SRR975561     3  0.0592      0.886 0.000 0.012 0.988
#&gt; SRR975562     1  0.3267      0.842 0.884 0.000 0.116
#&gt; SRR975563     2  0.0000      0.997 0.000 1.000 0.000
#&gt; SRR975564     1  0.3752      0.830 0.856 0.000 0.144
#&gt; SRR975565     1  0.3752      0.830 0.856 0.000 0.144
#&gt; SRR975566     1  0.2261      0.860 0.932 0.000 0.068
#&gt; SRR975567     3  0.0000      0.893 0.000 0.000 1.000
#&gt; SRR975568     1  0.3752      0.830 0.856 0.000 0.144
#&gt; SRR975569     2  0.0000      0.997 0.000 1.000 0.000
#&gt; SRR975570     2  0.0000      0.997 0.000 1.000 0.000
#&gt; SRR975571     2  0.0000      0.997 0.000 1.000 0.000
#&gt; SRR975572     2  0.0000      0.997 0.000 1.000 0.000
#&gt; SRR975573     2  0.0000      0.997 0.000 1.000 0.000
#&gt; SRR975574     2  0.1643      0.951 0.000 0.956 0.044
#&gt; SRR975575     2  0.0000      0.997 0.000 1.000 0.000
#&gt; SRR975576     2  0.0000      0.997 0.000 1.000 0.000
#&gt; SRR975577     2  0.0000      0.997 0.000 1.000 0.000
#&gt; SRR975578     2  0.0000      0.997 0.000 1.000 0.000
#&gt; SRR975579     3  0.3686      0.825 0.140 0.000 0.860
#&gt; SRR975580     3  0.0000      0.893 0.000 0.000 1.000
#&gt; SRR975581     2  0.0000      0.997 0.000 1.000 0.000
#&gt; SRR975582     2  0.0000      0.997 0.000 1.000 0.000
#&gt; SRR975583     2  0.0000      0.997 0.000 1.000 0.000
#&gt; SRR975584     2  0.0000      0.997 0.000 1.000 0.000
#&gt; SRR975585     2  0.0237      0.993 0.000 0.996 0.004
#&gt; SRR975586     3  0.0237      0.892 0.000 0.004 0.996
#&gt; SRR975587     1  0.3192      0.798 0.888 0.000 0.112
#&gt; SRR975588     2  0.0000      0.997 0.000 1.000 0.000
#&gt; SRR975589     1  0.0592      0.857 0.988 0.000 0.012
#&gt; SRR975590     1  0.0000      0.858 1.000 0.000 0.000
#&gt; SRR975591     1  0.6026      0.337 0.624 0.000 0.376
#&gt; SRR975592     1  0.0592      0.857 0.988 0.000 0.012
#&gt; SRR975593     1  0.0592      0.857 0.988 0.000 0.012
#&gt; SRR975594     3  0.3941      0.815 0.156 0.000 0.844
#&gt; SRR975595     1  0.0000      0.858 1.000 0.000 0.000
#&gt; SRR975597     1  0.0000      0.858 1.000 0.000 0.000
#&gt; SRR975596     1  0.2356      0.860 0.928 0.000 0.072
#&gt; SRR975598     1  0.0000      0.858 1.000 0.000 0.000
#&gt; SRR975599     3  0.6286      0.171 0.464 0.000 0.536
#&gt; SRR975600     1  0.3192      0.798 0.888 0.000 0.112
#&gt; SRR975601     1  0.6026      0.337 0.624 0.000 0.376
#&gt; SRR975602     1  0.0424      0.858 0.992 0.000 0.008
#&gt; SRR975603     1  0.3192      0.798 0.888 0.000 0.112
#&gt; SRR975604     1  0.6026      0.337 0.624 0.000 0.376
</code></pre>

<script>
$('#tab-MAD-mclust-get-classes-2-a').parent().next().next().hide();
$('#tab-MAD-mclust-get-classes-2-a').click(function(){
  $('#tab-MAD-mclust-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-mclust-get-classes-3'>
<p><a id='tab-MAD-mclust-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3    p4
#&gt; SRR975551     1  0.6621      0.575 0.628 0.000 0.184 0.188
#&gt; SRR975552     1  0.6689      0.574 0.620 0.000 0.184 0.196
#&gt; SRR975554     1  0.6709      0.358 0.616 0.000 0.172 0.212
#&gt; SRR975553     2  0.0000      0.989 0.000 1.000 0.000 0.000
#&gt; SRR975555     1  0.6689      0.574 0.620 0.000 0.184 0.196
#&gt; SRR975556     3  0.1302      0.601 0.000 0.044 0.956 0.000
#&gt; SRR975557     3  0.3486      0.592 0.000 0.000 0.812 0.188
#&gt; SRR975558     3  0.0188      0.621 0.000 0.000 0.996 0.004
#&gt; SRR975559     4  0.6548      0.736 0.188 0.000 0.176 0.636
#&gt; SRR975560     3  0.0188      0.622 0.000 0.004 0.996 0.000
#&gt; SRR975561     3  0.3764      0.402 0.000 0.216 0.784 0.000
#&gt; SRR975562     1  0.6805      0.348 0.604 0.000 0.176 0.220
#&gt; SRR975563     2  0.0000      0.989 0.000 1.000 0.000 0.000
#&gt; SRR975564     1  0.6316      0.549 0.660 0.000 0.184 0.156
#&gt; SRR975565     1  0.6689      0.574 0.620 0.000 0.184 0.196
#&gt; SRR975566     4  0.6511      0.738 0.188 0.000 0.172 0.640
#&gt; SRR975567     3  0.0188      0.621 0.000 0.000 0.996 0.004
#&gt; SRR975568     1  0.6689      0.574 0.620 0.000 0.184 0.196
#&gt; SRR975569     2  0.0000      0.989 0.000 1.000 0.000 0.000
#&gt; SRR975570     2  0.0000      0.989 0.000 1.000 0.000 0.000
#&gt; SRR975571     2  0.0000      0.989 0.000 1.000 0.000 0.000
#&gt; SRR975572     2  0.0000      0.989 0.000 1.000 0.000 0.000
#&gt; SRR975573     2  0.0000      0.989 0.000 1.000 0.000 0.000
#&gt; SRR975574     2  0.3024      0.794 0.000 0.852 0.148 0.000
#&gt; SRR975575     2  0.0000      0.989 0.000 1.000 0.000 0.000
#&gt; SRR975576     2  0.0000      0.989 0.000 1.000 0.000 0.000
#&gt; SRR975577     2  0.0000      0.989 0.000 1.000 0.000 0.000
#&gt; SRR975578     2  0.0000      0.989 0.000 1.000 0.000 0.000
#&gt; SRR975579     3  0.3486      0.592 0.000 0.000 0.812 0.188
#&gt; SRR975580     3  0.0188      0.622 0.000 0.004 0.996 0.000
#&gt; SRR975581     2  0.0000      0.989 0.000 1.000 0.000 0.000
#&gt; SRR975582     2  0.0000      0.989 0.000 1.000 0.000 0.000
#&gt; SRR975583     2  0.0000      0.989 0.000 1.000 0.000 0.000
#&gt; SRR975584     2  0.0000      0.989 0.000 1.000 0.000 0.000
#&gt; SRR975585     2  0.0000      0.989 0.000 1.000 0.000 0.000
#&gt; SRR975586     3  0.1940      0.575 0.000 0.076 0.924 0.000
#&gt; SRR975587     3  0.6666      0.493 0.404 0.000 0.508 0.088
#&gt; SRR975588     2  0.0000      0.989 0.000 1.000 0.000 0.000
#&gt; SRR975589     4  0.4888      0.636 0.412 0.000 0.000 0.588
#&gt; SRR975590     1  0.2660      0.373 0.908 0.000 0.036 0.056
#&gt; SRR975591     3  0.6417      0.530 0.388 0.000 0.540 0.072
#&gt; SRR975592     1  0.6235     -0.425 0.524 0.000 0.420 0.056
#&gt; SRR975593     4  0.4898      0.631 0.416 0.000 0.000 0.584
#&gt; SRR975594     3  0.4988      0.605 0.236 0.000 0.728 0.036
#&gt; SRR975595     1  0.0188      0.483 0.996 0.000 0.004 0.000
#&gt; SRR975597     1  0.0376      0.480 0.992 0.000 0.004 0.004
#&gt; SRR975596     4  0.6511      0.738 0.188 0.000 0.172 0.640
#&gt; SRR975598     1  0.0188      0.483 0.996 0.000 0.004 0.000
#&gt; SRR975599     3  0.6212      0.542 0.380 0.000 0.560 0.060
#&gt; SRR975600     3  0.7701      0.289 0.388 0.000 0.392 0.220
#&gt; SRR975601     3  0.6417      0.530 0.388 0.000 0.540 0.072
#&gt; SRR975602     1  0.2222      0.402 0.924 0.000 0.060 0.016
#&gt; SRR975603     3  0.6635      0.512 0.388 0.000 0.524 0.088
#&gt; SRR975604     3  0.6417      0.530 0.388 0.000 0.540 0.072
</code></pre>

<script>
$('#tab-MAD-mclust-get-classes-3-a').parent().next().next().hide();
$('#tab-MAD-mclust-get-classes-3-a').click(function(){
  $('#tab-MAD-mclust-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-mclust-get-classes-4'>
<p><a id='tab-MAD-mclust-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3    p4    p5
#&gt; SRR975551     1  0.1410     0.7166 0.940 0.000 0.000 0.000 0.060
#&gt; SRR975552     1  0.1851     0.7082 0.912 0.000 0.000 0.000 0.088
#&gt; SRR975554     1  0.6075     0.0631 0.476 0.000 0.428 0.012 0.084
#&gt; SRR975553     2  0.0794     0.9578 0.000 0.972 0.000 0.000 0.028
#&gt; SRR975555     1  0.1410     0.7166 0.940 0.000 0.000 0.000 0.060
#&gt; SRR975556     5  0.4499     0.7861 0.004 0.136 0.000 0.096 0.764
#&gt; SRR975557     4  0.2424     0.2698 0.000 0.000 0.000 0.868 0.132
#&gt; SRR975558     5  0.5656     0.4167 0.008 0.000 0.064 0.376 0.552
#&gt; SRR975559     3  0.3752     0.4495 0.200 0.000 0.780 0.004 0.016
#&gt; SRR975560     5  0.4450     0.7841 0.004 0.080 0.000 0.152 0.764
#&gt; SRR975561     5  0.4452     0.7592 0.004 0.164 0.000 0.072 0.760
#&gt; SRR975562     1  0.6101     0.1938 0.520 0.000 0.380 0.016 0.084
#&gt; SRR975563     2  0.0000     0.9799 0.000 1.000 0.000 0.000 0.000
#&gt; SRR975564     1  0.2520     0.6963 0.896 0.000 0.056 0.000 0.048
#&gt; SRR975565     1  0.1410     0.7166 0.940 0.000 0.000 0.000 0.060
#&gt; SRR975566     3  0.3845     0.4371 0.224 0.000 0.760 0.004 0.012
#&gt; SRR975567     5  0.5656     0.4167 0.008 0.000 0.064 0.376 0.552
#&gt; SRR975568     1  0.1410     0.7166 0.940 0.000 0.000 0.000 0.060
#&gt; SRR975569     2  0.0000     0.9799 0.000 1.000 0.000 0.000 0.000
#&gt; SRR975570     2  0.0000     0.9799 0.000 1.000 0.000 0.000 0.000
#&gt; SRR975571     2  0.0794     0.9578 0.000 0.972 0.000 0.000 0.028
#&gt; SRR975572     2  0.0000     0.9799 0.000 1.000 0.000 0.000 0.000
#&gt; SRR975573     2  0.0000     0.9799 0.000 1.000 0.000 0.000 0.000
#&gt; SRR975574     2  0.3491     0.6515 0.004 0.768 0.000 0.000 0.228
#&gt; SRR975575     2  0.0000     0.9799 0.000 1.000 0.000 0.000 0.000
#&gt; SRR975576     2  0.0162     0.9777 0.000 0.996 0.000 0.000 0.004
#&gt; SRR975577     2  0.0000     0.9799 0.000 1.000 0.000 0.000 0.000
#&gt; SRR975578     2  0.0162     0.9777 0.000 0.996 0.000 0.000 0.004
#&gt; SRR975579     4  0.2424     0.2698 0.000 0.000 0.000 0.868 0.132
#&gt; SRR975580     5  0.4450     0.7841 0.004 0.080 0.000 0.152 0.764
#&gt; SRR975581     2  0.0000     0.9799 0.000 1.000 0.000 0.000 0.000
#&gt; SRR975582     2  0.0000     0.9799 0.000 1.000 0.000 0.000 0.000
#&gt; SRR975583     2  0.0000     0.9799 0.000 1.000 0.000 0.000 0.000
#&gt; SRR975584     2  0.0162     0.9774 0.000 0.996 0.000 0.000 0.004
#&gt; SRR975585     2  0.0000     0.9799 0.000 1.000 0.000 0.000 0.000
#&gt; SRR975586     5  0.4478     0.7815 0.004 0.144 0.000 0.088 0.764
#&gt; SRR975587     3  0.7019    -0.1085 0.080 0.000 0.456 0.384 0.080
#&gt; SRR975588     2  0.0000     0.9799 0.000 1.000 0.000 0.000 0.000
#&gt; SRR975589     3  0.1478     0.4606 0.064 0.000 0.936 0.000 0.000
#&gt; SRR975590     1  0.7104     0.1684 0.460 0.000 0.368 0.104 0.068
#&gt; SRR975591     4  0.5146     0.3326 0.012 0.000 0.432 0.536 0.020
#&gt; SRR975592     3  0.7810     0.0898 0.240 0.000 0.400 0.288 0.072
#&gt; SRR975593     3  0.1478     0.4606 0.064 0.000 0.936 0.000 0.000
#&gt; SRR975594     4  0.5968     0.3985 0.000 0.000 0.268 0.576 0.156
#&gt; SRR975595     1  0.4985     0.6557 0.744 0.000 0.152 0.028 0.076
#&gt; SRR975597     1  0.4985     0.6557 0.744 0.000 0.152 0.028 0.076
#&gt; SRR975596     3  0.3652     0.4512 0.200 0.000 0.784 0.004 0.012
#&gt; SRR975598     1  0.4985     0.6557 0.744 0.000 0.152 0.028 0.076
#&gt; SRR975599     3  0.6361    -0.4363 0.004 0.000 0.428 0.428 0.140
#&gt; SRR975600     3  0.4538    -0.1015 0.016 0.000 0.620 0.364 0.000
#&gt; SRR975601     4  0.6109     0.3289 0.016 0.000 0.416 0.488 0.080
#&gt; SRR975602     1  0.5631     0.5839 0.660 0.000 0.240 0.028 0.072
#&gt; SRR975603     3  0.4747    -0.3408 0.016 0.000 0.500 0.484 0.000
#&gt; SRR975604     4  0.5187     0.2660 0.016 0.000 0.484 0.484 0.016
</code></pre>

<script>
$('#tab-MAD-mclust-get-classes-4-a').parent().next().next().hide();
$('#tab-MAD-mclust-get-classes-4-a').click(function(){
  $('#tab-MAD-mclust-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-mclust-get-classes-5'>
<p><a id='tab-MAD-mclust-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3    p4    p5    p6
#&gt; SRR975551     1  0.1010      0.699 0.960 0.000 0.000 0.000 0.036 0.004
#&gt; SRR975552     1  0.0692      0.709 0.976 0.000 0.000 0.000 0.020 0.004
#&gt; SRR975554     5  0.4085      0.708 0.092 0.000 0.108 0.000 0.780 0.020
#&gt; SRR975553     2  0.0790      0.957 0.000 0.968 0.000 0.000 0.000 0.032
#&gt; SRR975555     1  0.0692      0.709 0.976 0.000 0.000 0.000 0.020 0.004
#&gt; SRR975556     6  0.1863      0.724 0.000 0.104 0.000 0.000 0.000 0.896
#&gt; SRR975557     4  0.4228      0.514 0.000 0.000 0.072 0.716 0.000 0.212
#&gt; SRR975558     6  0.5812      0.352 0.004 0.000 0.072 0.164 0.116 0.644
#&gt; SRR975559     5  0.1257      0.779 0.020 0.000 0.000 0.000 0.952 0.028
#&gt; SRR975560     6  0.1575      0.707 0.000 0.032 0.000 0.032 0.000 0.936
#&gt; SRR975561     6  0.2597      0.641 0.000 0.176 0.000 0.000 0.000 0.824
#&gt; SRR975562     5  0.5458      0.566 0.216 0.000 0.124 0.004 0.636 0.020
#&gt; SRR975563     2  0.0000      0.980 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR975564     1  0.4935      0.109 0.556 0.000 0.044 0.000 0.388 0.012
#&gt; SRR975565     1  0.0692      0.709 0.976 0.000 0.000 0.000 0.020 0.004
#&gt; SRR975566     5  0.1078      0.780 0.016 0.000 0.012 0.000 0.964 0.008
#&gt; SRR975567     6  0.5812      0.352 0.004 0.000 0.072 0.164 0.116 0.644
#&gt; SRR975568     1  0.0692      0.709 0.976 0.000 0.000 0.000 0.020 0.004
#&gt; SRR975569     2  0.0000      0.980 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR975570     2  0.0000      0.980 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR975571     2  0.0790      0.957 0.000 0.968 0.000 0.000 0.000 0.032
#&gt; SRR975572     2  0.0000      0.980 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR975573     2  0.0000      0.980 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR975574     2  0.2823      0.713 0.000 0.796 0.000 0.000 0.000 0.204
#&gt; SRR975575     2  0.0000      0.980 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR975576     2  0.0146      0.978 0.000 0.996 0.000 0.000 0.000 0.004
#&gt; SRR975577     2  0.0000      0.980 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR975578     2  0.0260      0.975 0.000 0.992 0.000 0.000 0.000 0.008
#&gt; SRR975579     4  0.5348      0.479 0.000 0.056 0.068 0.652 0.000 0.224
#&gt; SRR975580     6  0.0790      0.714 0.000 0.032 0.000 0.000 0.000 0.968
#&gt; SRR975581     2  0.0000      0.980 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR975582     2  0.0000      0.980 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR975583     2  0.0000      0.980 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR975584     2  0.0632      0.962 0.000 0.976 0.000 0.000 0.000 0.024
#&gt; SRR975585     2  0.0000      0.980 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR975586     6  0.1863      0.724 0.000 0.104 0.000 0.000 0.000 0.896
#&gt; SRR975587     3  0.3638      0.487 0.040 0.000 0.836 0.044 0.068 0.012
#&gt; SRR975588     2  0.0000      0.980 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR975589     5  0.2994      0.623 0.004 0.000 0.208 0.000 0.788 0.000
#&gt; SRR975590     3  0.5361      0.394 0.180 0.000 0.620 0.008 0.192 0.000
#&gt; SRR975591     3  0.6218      0.456 0.000 0.000 0.592 0.168 0.144 0.096
#&gt; SRR975592     3  0.4819      0.453 0.132 0.000 0.664 0.000 0.204 0.000
#&gt; SRR975593     5  0.2883      0.619 0.000 0.000 0.212 0.000 0.788 0.000
#&gt; SRR975594     4  0.4300     -0.152 0.000 0.000 0.444 0.540 0.008 0.008
#&gt; SRR975595     1  0.5574      0.377 0.480 0.000 0.428 0.044 0.048 0.000
#&gt; SRR975597     1  0.5519      0.380 0.484 0.000 0.428 0.040 0.048 0.000
#&gt; SRR975596     5  0.1232      0.781 0.016 0.000 0.004 0.000 0.956 0.024
#&gt; SRR975598     1  0.5578      0.368 0.472 0.000 0.436 0.044 0.048 0.000
#&gt; SRR975599     3  0.3728      0.249 0.000 0.000 0.652 0.344 0.000 0.004
#&gt; SRR975600     3  0.5447      0.472 0.000 0.000 0.580 0.076 0.316 0.028
#&gt; SRR975601     3  0.4857      0.313 0.000 0.000 0.688 0.200 0.016 0.096
#&gt; SRR975602     3  0.5491     -0.327 0.400 0.000 0.512 0.048 0.040 0.000
#&gt; SRR975603     3  0.6161      0.482 0.000 0.000 0.576 0.112 0.232 0.080
#&gt; SRR975604     3  0.6168      0.457 0.000 0.000 0.600 0.160 0.140 0.100
</code></pre>

<script>
$('#tab-MAD-mclust-get-classes-5-a').parent().next().next().hide();
$('#tab-MAD-mclust-get-classes-5-a').click(function(){
  $('#tab-MAD-mclust-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-MAD-mclust-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-MAD-mclust-consensus-heatmap'>
<ul>
<li><a href='#tab-MAD-mclust-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-MAD-mclust-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-MAD-mclust-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-MAD-mclust-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-MAD-mclust-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-mclust-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-consensus-heatmap-1-1.png" alt="plot of chunk tab-MAD-mclust-consensus-heatmap-1"/></p>

</div>
<div id='tab-MAD-mclust-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-consensus-heatmap-2-1.png" alt="plot of chunk tab-MAD-mclust-consensus-heatmap-2"/></p>

</div>
<div id='tab-MAD-mclust-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-consensus-heatmap-3-1.png" alt="plot of chunk tab-MAD-mclust-consensus-heatmap-3"/></p>

</div>
<div id='tab-MAD-mclust-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-consensus-heatmap-4-1.png" alt="plot of chunk tab-MAD-mclust-consensus-heatmap-4"/></p>

</div>
<div id='tab-MAD-mclust-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-consensus-heatmap-5-1.png" alt="plot of chunk tab-MAD-mclust-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-MAD-mclust-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-MAD-mclust-membership-heatmap'>
<ul>
<li><a href='#tab-MAD-mclust-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-MAD-mclust-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-MAD-mclust-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-MAD-mclust-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-MAD-mclust-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-mclust-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-membership-heatmap-1-1.png" alt="plot of chunk tab-MAD-mclust-membership-heatmap-1"/></p>

</div>
<div id='tab-MAD-mclust-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-membership-heatmap-2-1.png" alt="plot of chunk tab-MAD-mclust-membership-heatmap-2"/></p>

</div>
<div id='tab-MAD-mclust-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-membership-heatmap-3-1.png" alt="plot of chunk tab-MAD-mclust-membership-heatmap-3"/></p>

</div>
<div id='tab-MAD-mclust-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-membership-heatmap-4-1.png" alt="plot of chunk tab-MAD-mclust-membership-heatmap-4"/></p>

</div>
<div id='tab-MAD-mclust-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-membership-heatmap-5-1.png" alt="plot of chunk tab-MAD-mclust-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-MAD-mclust-get-signatures' ).tabs();
} );
</script>
<div id='tabs-MAD-mclust-get-signatures'>
<ul>
<li><a href='#tab-MAD-mclust-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-MAD-mclust-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-MAD-mclust-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-MAD-mclust-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-MAD-mclust-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-mclust-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-get-signatures-1-1.png" alt="plot of chunk tab-MAD-mclust-get-signatures-1"/></p>

</div>
<div id='tab-MAD-mclust-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-get-signatures-2-1.png" alt="plot of chunk tab-MAD-mclust-get-signatures-2"/></p>

</div>
<div id='tab-MAD-mclust-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-get-signatures-3-1.png" alt="plot of chunk tab-MAD-mclust-get-signatures-3"/></p>

</div>
<div id='tab-MAD-mclust-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-get-signatures-4-1.png" alt="plot of chunk tab-MAD-mclust-get-signatures-4"/></p>

</div>
<div id='tab-MAD-mclust-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-get-signatures-5-1.png" alt="plot of chunk tab-MAD-mclust-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-MAD-mclust-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-MAD-mclust-get-signatures-no-scale'>
<ul>
<li><a href='#tab-MAD-mclust-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-MAD-mclust-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-MAD-mclust-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-MAD-mclust-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-MAD-mclust-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-mclust-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-MAD-mclust-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-MAD-mclust-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-MAD-mclust-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-MAD-mclust-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-MAD-mclust-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-MAD-mclust-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-MAD-mclust-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-MAD-mclust-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-MAD-mclust-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk MAD-mclust-signature_compare](figure_cola/MAD-mclust-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-MAD-mclust-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-MAD-mclust-dimension-reduction'>
<ul>
<li><a href='#tab-MAD-mclust-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-MAD-mclust-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-MAD-mclust-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-MAD-mclust-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-MAD-mclust-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-mclust-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-dimension-reduction-1-1.png" alt="plot of chunk tab-MAD-mclust-dimension-reduction-1"/></p>

</div>
<div id='tab-MAD-mclust-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-dimension-reduction-2-1.png" alt="plot of chunk tab-MAD-mclust-dimension-reduction-2"/></p>

</div>
<div id='tab-MAD-mclust-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-dimension-reduction-3-1.png" alt="plot of chunk tab-MAD-mclust-dimension-reduction-3"/></p>

</div>
<div id='tab-MAD-mclust-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-dimension-reduction-4-1.png" alt="plot of chunk tab-MAD-mclust-dimension-reduction-4"/></p>

</div>
<div id='tab-MAD-mclust-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-dimension-reduction-5-1.png" alt="plot of chunk tab-MAD-mclust-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk MAD-mclust-collect-classes](figure_cola/MAD-mclust-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### MAD:NMF*






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["MAD", "NMF"]
# you can also extract it by
# res = res_list["MAD:NMF"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 17171 rows and 54 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'MAD' method.
#>   Subgroups are detected by 'NMF' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 4.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk MAD-NMF-collect-plots](figure_cola/MAD-NMF-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk MAD-NMF-select-partition-number](figure_cola/MAD-NMF-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 1.000           0.993       0.996         0.5043 0.497   0.497
#> 3 3 1.000           0.968       0.987         0.2443 0.867   0.734
#> 4 4 0.944           0.907       0.955         0.0548 0.956   0.884
#> 5 5 0.824           0.759       0.838         0.0935 0.898   0.714
#> 6 6 0.757           0.719       0.833         0.0724 0.928   0.743
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 4
#> attr(,"optional")
#> [1] 2 3
```

There is also optional best $k$ = 2 3 that is worth to check.

Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-MAD-NMF-get-classes' ).tabs();
} );
</script>
<div id='tabs-MAD-NMF-get-classes'>
<ul>
<li><a href='#tab-MAD-NMF-get-classes-1'>k = 2</a></li>
<li><a href='#tab-MAD-NMF-get-classes-2'>k = 3</a></li>
<li><a href='#tab-MAD-NMF-get-classes-3'>k = 4</a></li>
<li><a href='#tab-MAD-NMF-get-classes-4'>k = 5</a></li>
<li><a href='#tab-MAD-NMF-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-MAD-NMF-get-classes-1'>
<p><a id='tab-MAD-NMF-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2
#&gt; SRR975551     1   0.000      0.993 1.000 0.000
#&gt; SRR975552     1   0.000      0.993 1.000 0.000
#&gt; SRR975554     1   0.000      0.993 1.000 0.000
#&gt; SRR975553     2   0.000      1.000 0.000 1.000
#&gt; SRR975555     1   0.000      0.993 1.000 0.000
#&gt; SRR975556     2   0.000      1.000 0.000 1.000
#&gt; SRR975557     1   0.184      0.969 0.972 0.028
#&gt; SRR975558     1   0.552      0.857 0.872 0.128
#&gt; SRR975559     1   0.000      0.993 1.000 0.000
#&gt; SRR975560     2   0.000      1.000 0.000 1.000
#&gt; SRR975561     2   0.000      1.000 0.000 1.000
#&gt; SRR975562     1   0.000      0.993 1.000 0.000
#&gt; SRR975563     2   0.000      1.000 0.000 1.000
#&gt; SRR975564     1   0.000      0.993 1.000 0.000
#&gt; SRR975565     1   0.000      0.993 1.000 0.000
#&gt; SRR975566     1   0.000      0.993 1.000 0.000
#&gt; SRR975567     1   0.242      0.957 0.960 0.040
#&gt; SRR975568     1   0.000      0.993 1.000 0.000
#&gt; SRR975569     2   0.000      1.000 0.000 1.000
#&gt; SRR975570     2   0.000      1.000 0.000 1.000
#&gt; SRR975571     2   0.000      1.000 0.000 1.000
#&gt; SRR975572     2   0.000      1.000 0.000 1.000
#&gt; SRR975573     2   0.000      1.000 0.000 1.000
#&gt; SRR975574     2   0.000      1.000 0.000 1.000
#&gt; SRR975575     2   0.000      1.000 0.000 1.000
#&gt; SRR975576     2   0.000      1.000 0.000 1.000
#&gt; SRR975577     2   0.000      1.000 0.000 1.000
#&gt; SRR975578     2   0.000      1.000 0.000 1.000
#&gt; SRR975579     2   0.000      1.000 0.000 1.000
#&gt; SRR975580     2   0.000      1.000 0.000 1.000
#&gt; SRR975581     2   0.000      1.000 0.000 1.000
#&gt; SRR975582     2   0.000      1.000 0.000 1.000
#&gt; SRR975583     2   0.000      1.000 0.000 1.000
#&gt; SRR975584     2   0.000      1.000 0.000 1.000
#&gt; SRR975585     2   0.000      1.000 0.000 1.000
#&gt; SRR975586     2   0.000      1.000 0.000 1.000
#&gt; SRR975587     1   0.000      0.993 1.000 0.000
#&gt; SRR975588     2   0.000      1.000 0.000 1.000
#&gt; SRR975589     1   0.000      0.993 1.000 0.000
#&gt; SRR975590     1   0.000      0.993 1.000 0.000
#&gt; SRR975591     1   0.000      0.993 1.000 0.000
#&gt; SRR975592     1   0.000      0.993 1.000 0.000
#&gt; SRR975593     1   0.000      0.993 1.000 0.000
#&gt; SRR975594     1   0.000      0.993 1.000 0.000
#&gt; SRR975595     1   0.000      0.993 1.000 0.000
#&gt; SRR975597     1   0.000      0.993 1.000 0.000
#&gt; SRR975596     1   0.000      0.993 1.000 0.000
#&gt; SRR975598     1   0.000      0.993 1.000 0.000
#&gt; SRR975599     1   0.000      0.993 1.000 0.000
#&gt; SRR975600     1   0.000      0.993 1.000 0.000
#&gt; SRR975601     1   0.000      0.993 1.000 0.000
#&gt; SRR975602     1   0.000      0.993 1.000 0.000
#&gt; SRR975603     1   0.000      0.993 1.000 0.000
#&gt; SRR975604     1   0.000      0.993 1.000 0.000
</code></pre>

<script>
$('#tab-MAD-NMF-get-classes-1-a').parent().next().next().hide();
$('#tab-MAD-NMF-get-classes-1-a').click(function(){
  $('#tab-MAD-NMF-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-NMF-get-classes-2'>
<p><a id='tab-MAD-NMF-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3
#&gt; SRR975551     1  0.0000      0.980 1.000 0.000 0.000
#&gt; SRR975552     1  0.0000      0.980 1.000 0.000 0.000
#&gt; SRR975554     1  0.0000      0.980 1.000 0.000 0.000
#&gt; SRR975553     2  0.0000      1.000 0.000 1.000 0.000
#&gt; SRR975555     1  0.0000      0.980 1.000 0.000 0.000
#&gt; SRR975556     2  0.0000      1.000 0.000 1.000 0.000
#&gt; SRR975557     3  0.0000      0.955 0.000 0.000 1.000
#&gt; SRR975558     1  0.2165      0.904 0.936 0.064 0.000
#&gt; SRR975559     1  0.0000      0.980 1.000 0.000 0.000
#&gt; SRR975560     2  0.0000      1.000 0.000 1.000 0.000
#&gt; SRR975561     2  0.0000      1.000 0.000 1.000 0.000
#&gt; SRR975562     1  0.0000      0.980 1.000 0.000 0.000
#&gt; SRR975563     2  0.0000      1.000 0.000 1.000 0.000
#&gt; SRR975564     1  0.0000      0.980 1.000 0.000 0.000
#&gt; SRR975565     1  0.0000      0.980 1.000 0.000 0.000
#&gt; SRR975566     1  0.0000      0.980 1.000 0.000 0.000
#&gt; SRR975567     1  0.0000      0.980 1.000 0.000 0.000
#&gt; SRR975568     1  0.0000      0.980 1.000 0.000 0.000
#&gt; SRR975569     2  0.0000      1.000 0.000 1.000 0.000
#&gt; SRR975570     2  0.0000      1.000 0.000 1.000 0.000
#&gt; SRR975571     2  0.0000      1.000 0.000 1.000 0.000
#&gt; SRR975572     2  0.0000      1.000 0.000 1.000 0.000
#&gt; SRR975573     2  0.0000      1.000 0.000 1.000 0.000
#&gt; SRR975574     2  0.0000      1.000 0.000 1.000 0.000
#&gt; SRR975575     2  0.0000      1.000 0.000 1.000 0.000
#&gt; SRR975576     2  0.0000      1.000 0.000 1.000 0.000
#&gt; SRR975577     2  0.0000      1.000 0.000 1.000 0.000
#&gt; SRR975578     2  0.0000      1.000 0.000 1.000 0.000
#&gt; SRR975579     3  0.4504      0.751 0.000 0.196 0.804
#&gt; SRR975580     2  0.0000      1.000 0.000 1.000 0.000
#&gt; SRR975581     2  0.0000      1.000 0.000 1.000 0.000
#&gt; SRR975582     2  0.0000      1.000 0.000 1.000 0.000
#&gt; SRR975583     2  0.0000      1.000 0.000 1.000 0.000
#&gt; SRR975584     2  0.0000      1.000 0.000 1.000 0.000
#&gt; SRR975585     2  0.0000      1.000 0.000 1.000 0.000
#&gt; SRR975586     2  0.0000      1.000 0.000 1.000 0.000
#&gt; SRR975587     1  0.5905      0.454 0.648 0.000 0.352
#&gt; SRR975588     2  0.0000      1.000 0.000 1.000 0.000
#&gt; SRR975589     1  0.0000      0.980 1.000 0.000 0.000
#&gt; SRR975590     1  0.0000      0.980 1.000 0.000 0.000
#&gt; SRR975591     3  0.0000      0.955 0.000 0.000 1.000
#&gt; SRR975592     1  0.0000      0.980 1.000 0.000 0.000
#&gt; SRR975593     1  0.0424      0.973 0.992 0.000 0.008
#&gt; SRR975594     3  0.0000      0.955 0.000 0.000 1.000
#&gt; SRR975595     1  0.0000      0.980 1.000 0.000 0.000
#&gt; SRR975597     1  0.0000      0.980 1.000 0.000 0.000
#&gt; SRR975596     1  0.0000      0.980 1.000 0.000 0.000
#&gt; SRR975598     1  0.0000      0.980 1.000 0.000 0.000
#&gt; SRR975599     1  0.0000      0.980 1.000 0.000 0.000
#&gt; SRR975600     3  0.2356      0.903 0.072 0.000 0.928
#&gt; SRR975601     3  0.1289      0.938 0.032 0.000 0.968
#&gt; SRR975602     1  0.0000      0.980 1.000 0.000 0.000
#&gt; SRR975603     3  0.0000      0.955 0.000 0.000 1.000
#&gt; SRR975604     3  0.0000      0.955 0.000 0.000 1.000
</code></pre>

<script>
$('#tab-MAD-NMF-get-classes-2-a').parent().next().next().hide();
$('#tab-MAD-NMF-get-classes-2-a').click(function(){
  $('#tab-MAD-NMF-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-NMF-get-classes-3'>
<p><a id='tab-MAD-NMF-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3    p4
#&gt; SRR975551     1  0.0817      0.936 0.976 0.000 0.000 0.024
#&gt; SRR975552     1  0.0000      0.938 1.000 0.000 0.000 0.000
#&gt; SRR975554     1  0.0336      0.937 0.992 0.000 0.000 0.008
#&gt; SRR975553     2  0.0000      0.995 0.000 1.000 0.000 0.000
#&gt; SRR975555     1  0.0336      0.938 0.992 0.000 0.000 0.008
#&gt; SRR975556     2  0.0000      0.995 0.000 1.000 0.000 0.000
#&gt; SRR975557     4  0.2469      0.556 0.000 0.000 0.108 0.892
#&gt; SRR975558     4  0.7150      0.183 0.384 0.136 0.000 0.480
#&gt; SRR975559     1  0.2973      0.839 0.856 0.000 0.000 0.144
#&gt; SRR975560     2  0.1890      0.927 0.008 0.936 0.000 0.056
#&gt; SRR975561     2  0.0000      0.995 0.000 1.000 0.000 0.000
#&gt; SRR975562     1  0.1637      0.914 0.940 0.000 0.000 0.060
#&gt; SRR975563     2  0.0000      0.995 0.000 1.000 0.000 0.000
#&gt; SRR975564     1  0.0707      0.937 0.980 0.000 0.000 0.020
#&gt; SRR975565     1  0.0188      0.938 0.996 0.000 0.000 0.004
#&gt; SRR975566     1  0.0469      0.937 0.988 0.000 0.000 0.012
#&gt; SRR975567     1  0.5300      0.483 0.664 0.028 0.000 0.308
#&gt; SRR975568     1  0.0921      0.933 0.972 0.000 0.000 0.028
#&gt; SRR975569     2  0.0000      0.995 0.000 1.000 0.000 0.000
#&gt; SRR975570     2  0.0000      0.995 0.000 1.000 0.000 0.000
#&gt; SRR975571     2  0.0000      0.995 0.000 1.000 0.000 0.000
#&gt; SRR975572     2  0.0000      0.995 0.000 1.000 0.000 0.000
#&gt; SRR975573     2  0.0000      0.995 0.000 1.000 0.000 0.000
#&gt; SRR975574     2  0.0000      0.995 0.000 1.000 0.000 0.000
#&gt; SRR975575     2  0.0000      0.995 0.000 1.000 0.000 0.000
#&gt; SRR975576     2  0.0000      0.995 0.000 1.000 0.000 0.000
#&gt; SRR975577     2  0.0000      0.995 0.000 1.000 0.000 0.000
#&gt; SRR975578     2  0.0000      0.995 0.000 1.000 0.000 0.000
#&gt; SRR975579     4  0.3435      0.569 0.000 0.036 0.100 0.864
#&gt; SRR975580     2  0.1211      0.954 0.000 0.960 0.000 0.040
#&gt; SRR975581     2  0.0000      0.995 0.000 1.000 0.000 0.000
#&gt; SRR975582     2  0.0000      0.995 0.000 1.000 0.000 0.000
#&gt; SRR975583     2  0.0000      0.995 0.000 1.000 0.000 0.000
#&gt; SRR975584     2  0.0000      0.995 0.000 1.000 0.000 0.000
#&gt; SRR975585     2  0.0000      0.995 0.000 1.000 0.000 0.000
#&gt; SRR975586     2  0.0000      0.995 0.000 1.000 0.000 0.000
#&gt; SRR975587     3  0.2546      0.858 0.060 0.000 0.912 0.028
#&gt; SRR975588     2  0.0000      0.995 0.000 1.000 0.000 0.000
#&gt; SRR975589     1  0.0804      0.937 0.980 0.000 0.008 0.012
#&gt; SRR975590     1  0.1545      0.928 0.952 0.000 0.008 0.040
#&gt; SRR975591     3  0.0188      0.910 0.000 0.000 0.996 0.004
#&gt; SRR975592     1  0.1488      0.925 0.956 0.000 0.032 0.012
#&gt; SRR975593     1  0.1888      0.919 0.940 0.000 0.044 0.016
#&gt; SRR975594     3  0.0188      0.910 0.000 0.000 0.996 0.004
#&gt; SRR975595     1  0.1398      0.933 0.956 0.000 0.004 0.040
#&gt; SRR975597     1  0.0895      0.934 0.976 0.000 0.004 0.020
#&gt; SRR975596     1  0.3311      0.803 0.828 0.000 0.000 0.172
#&gt; SRR975598     1  0.1661      0.929 0.944 0.000 0.004 0.052
#&gt; SRR975599     1  0.2053      0.916 0.924 0.000 0.004 0.072
#&gt; SRR975600     3  0.4182      0.631 0.180 0.000 0.796 0.024
#&gt; SRR975601     3  0.1510      0.895 0.028 0.000 0.956 0.016
#&gt; SRR975602     1  0.0707      0.938 0.980 0.000 0.000 0.020
#&gt; SRR975603     3  0.0000      0.911 0.000 0.000 1.000 0.000
#&gt; SRR975604     3  0.0000      0.911 0.000 0.000 1.000 0.000
</code></pre>

<script>
$('#tab-MAD-NMF-get-classes-3-a').parent().next().next().hide();
$('#tab-MAD-NMF-get-classes-3-a').click(function(){
  $('#tab-MAD-NMF-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-NMF-get-classes-4'>
<p><a id='tab-MAD-NMF-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3    p4    p5
#&gt; SRR975551     1  0.1908      0.629 0.908 0.000 0.000 0.000 0.092
#&gt; SRR975552     1  0.1270      0.671 0.948 0.000 0.000 0.000 0.052
#&gt; SRR975554     1  0.1544      0.694 0.932 0.000 0.000 0.000 0.068
#&gt; SRR975553     2  0.0703      0.957 0.000 0.976 0.000 0.000 0.024
#&gt; SRR975555     1  0.2648      0.620 0.848 0.000 0.000 0.000 0.152
#&gt; SRR975556     2  0.1608      0.922 0.000 0.928 0.000 0.000 0.072
#&gt; SRR975557     4  0.0000      0.733 0.000 0.000 0.000 1.000 0.000
#&gt; SRR975558     4  0.6603      0.669 0.108 0.108 0.000 0.628 0.156
#&gt; SRR975559     1  0.6275     -0.185 0.480 0.000 0.000 0.364 0.156
#&gt; SRR975560     5  0.4974     -0.154 0.028 0.464 0.000 0.000 0.508
#&gt; SRR975561     2  0.0880      0.951 0.000 0.968 0.000 0.000 0.032
#&gt; SRR975562     5  0.4300      0.689 0.476 0.000 0.000 0.000 0.524
#&gt; SRR975563     2  0.0794      0.953 0.000 0.972 0.000 0.000 0.028
#&gt; SRR975564     1  0.3895      0.557 0.680 0.000 0.000 0.000 0.320
#&gt; SRR975565     1  0.0880      0.688 0.968 0.000 0.000 0.000 0.032
#&gt; SRR975566     1  0.2124      0.693 0.916 0.000 0.000 0.028 0.056
#&gt; SRR975567     4  0.5654      0.513 0.288 0.080 0.000 0.620 0.012
#&gt; SRR975568     1  0.3796      0.579 0.700 0.000 0.000 0.000 0.300
#&gt; SRR975569     2  0.0290      0.960 0.000 0.992 0.000 0.000 0.008
#&gt; SRR975570     2  0.0000      0.960 0.000 1.000 0.000 0.000 0.000
#&gt; SRR975571     2  0.0703      0.957 0.000 0.976 0.000 0.000 0.024
#&gt; SRR975572     2  0.0162      0.960 0.000 0.996 0.000 0.000 0.004
#&gt; SRR975573     2  0.0703      0.957 0.000 0.976 0.000 0.000 0.024
#&gt; SRR975574     2  0.0703      0.957 0.000 0.976 0.000 0.000 0.024
#&gt; SRR975575     2  0.0162      0.960 0.000 0.996 0.000 0.000 0.004
#&gt; SRR975576     2  0.0703      0.954 0.000 0.976 0.000 0.000 0.024
#&gt; SRR975577     2  0.0609      0.958 0.000 0.980 0.000 0.000 0.020
#&gt; SRR975578     2  0.0880      0.957 0.000 0.968 0.000 0.000 0.032
#&gt; SRR975579     4  0.0451      0.736 0.000 0.004 0.000 0.988 0.008
#&gt; SRR975580     2  0.4161      0.417 0.000 0.608 0.000 0.000 0.392
#&gt; SRR975581     2  0.0510      0.957 0.000 0.984 0.000 0.000 0.016
#&gt; SRR975582     2  0.0609      0.958 0.000 0.980 0.000 0.000 0.020
#&gt; SRR975583     2  0.0162      0.960 0.000 0.996 0.000 0.000 0.004
#&gt; SRR975584     2  0.0794      0.956 0.000 0.972 0.000 0.000 0.028
#&gt; SRR975585     2  0.0290      0.959 0.000 0.992 0.000 0.000 0.008
#&gt; SRR975586     2  0.1671      0.920 0.000 0.924 0.000 0.000 0.076
#&gt; SRR975587     3  0.0609      0.966 0.020 0.000 0.980 0.000 0.000
#&gt; SRR975588     2  0.0000      0.960 0.000 1.000 0.000 0.000 0.000
#&gt; SRR975589     1  0.3452      0.610 0.756 0.000 0.000 0.000 0.244
#&gt; SRR975590     1  0.1768      0.693 0.924 0.000 0.004 0.000 0.072
#&gt; SRR975591     3  0.0000      0.981 0.000 0.000 1.000 0.000 0.000
#&gt; SRR975592     1  0.2378      0.687 0.904 0.000 0.048 0.000 0.048
#&gt; SRR975593     1  0.3386      0.588 0.832 0.000 0.000 0.040 0.128
#&gt; SRR975594     3  0.0000      0.981 0.000 0.000 1.000 0.000 0.000
#&gt; SRR975595     5  0.4306      0.672 0.492 0.000 0.000 0.000 0.508
#&gt; SRR975597     1  0.2813      0.512 0.832 0.000 0.000 0.000 0.168
#&gt; SRR975596     5  0.4902      0.677 0.468 0.000 0.000 0.024 0.508
#&gt; SRR975598     5  0.4297      0.690 0.472 0.000 0.000 0.000 0.528
#&gt; SRR975599     5  0.4300      0.690 0.476 0.000 0.000 0.000 0.524
#&gt; SRR975600     1  0.6433      0.264 0.488 0.000 0.200 0.000 0.312
#&gt; SRR975601     3  0.0000      0.981 0.000 0.000 1.000 0.000 0.000
#&gt; SRR975602     1  0.2813      0.510 0.832 0.000 0.000 0.000 0.168
#&gt; SRR975603     3  0.1469      0.932 0.036 0.000 0.948 0.000 0.016
#&gt; SRR975604     3  0.0000      0.981 0.000 0.000 1.000 0.000 0.000
</code></pre>

<script>
$('#tab-MAD-NMF-get-classes-4-a').parent().next().next().hide();
$('#tab-MAD-NMF-get-classes-4-a').click(function(){
  $('#tab-MAD-NMF-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-NMF-get-classes-5'>
<p><a id='tab-MAD-NMF-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3    p4    p5    p6
#&gt; SRR975551     1  0.0692     0.7325 0.976 0.000 0.000 0.000 0.004 0.020
#&gt; SRR975552     1  0.1713     0.7179 0.928 0.000 0.000 0.000 0.028 0.044
#&gt; SRR975554     1  0.3707     0.4258 0.680 0.000 0.000 0.000 0.312 0.008
#&gt; SRR975553     2  0.1418     0.9147 0.000 0.944 0.000 0.000 0.024 0.032
#&gt; SRR975555     1  0.6077    -0.0898 0.400 0.000 0.000 0.000 0.304 0.296
#&gt; SRR975556     2  0.4853     0.6985 0.012 0.692 0.000 0.000 0.124 0.172
#&gt; SRR975557     4  0.0000     0.7665 0.000 0.000 0.000 1.000 0.000 0.000
#&gt; SRR975558     5  0.4849     0.4916 0.000 0.016 0.000 0.156 0.700 0.128
#&gt; SRR975559     4  0.4955     0.3630 0.296 0.000 0.000 0.608 0.000 0.096
#&gt; SRR975560     6  0.4105     0.4629 0.008 0.196 0.000 0.012 0.032 0.752
#&gt; SRR975561     2  0.2882     0.8641 0.000 0.860 0.000 0.004 0.060 0.076
#&gt; SRR975562     6  0.3617     0.7066 0.244 0.000 0.000 0.000 0.020 0.736
#&gt; SRR975563     2  0.3458     0.8225 0.000 0.808 0.000 0.000 0.080 0.112
#&gt; SRR975564     5  0.3253     0.7560 0.192 0.000 0.000 0.000 0.788 0.020
#&gt; SRR975565     1  0.2066     0.7125 0.904 0.000 0.000 0.000 0.072 0.024
#&gt; SRR975566     1  0.2848     0.6587 0.828 0.000 0.000 0.004 0.160 0.008
#&gt; SRR975567     4  0.4226     0.6790 0.036 0.088 0.000 0.796 0.064 0.016
#&gt; SRR975568     5  0.3259     0.7448 0.216 0.000 0.000 0.000 0.772 0.012
#&gt; SRR975569     2  0.0146     0.9210 0.000 0.996 0.000 0.000 0.000 0.004
#&gt; SRR975570     2  0.1074     0.9173 0.000 0.960 0.000 0.000 0.028 0.012
#&gt; SRR975571     2  0.1418     0.9147 0.000 0.944 0.000 0.000 0.024 0.032
#&gt; SRR975572     2  0.0405     0.9211 0.000 0.988 0.000 0.000 0.004 0.008
#&gt; SRR975573     2  0.1341     0.9158 0.000 0.948 0.000 0.000 0.024 0.028
#&gt; SRR975574     2  0.1341     0.9158 0.000 0.948 0.000 0.000 0.024 0.028
#&gt; SRR975575     2  0.0508     0.9208 0.000 0.984 0.000 0.000 0.004 0.012
#&gt; SRR975576     2  0.1720     0.9035 0.000 0.928 0.000 0.000 0.040 0.032
#&gt; SRR975577     2  0.1341     0.9158 0.000 0.948 0.000 0.000 0.024 0.028
#&gt; SRR975578     2  0.1418     0.9160 0.000 0.944 0.000 0.000 0.024 0.032
#&gt; SRR975579     4  0.0000     0.7665 0.000 0.000 0.000 1.000 0.000 0.000
#&gt; SRR975580     6  0.4004     0.3797 0.012 0.328 0.000 0.000 0.004 0.656
#&gt; SRR975581     2  0.1245     0.9153 0.000 0.952 0.000 0.000 0.016 0.032
#&gt; SRR975582     2  0.1341     0.9158 0.000 0.948 0.000 0.000 0.024 0.028
#&gt; SRR975583     2  0.0914     0.9193 0.000 0.968 0.000 0.000 0.016 0.016
#&gt; SRR975584     2  0.1492     0.9131 0.000 0.940 0.000 0.000 0.024 0.036
#&gt; SRR975585     2  0.0622     0.9205 0.000 0.980 0.000 0.000 0.012 0.008
#&gt; SRR975586     2  0.4865     0.6740 0.004 0.672 0.000 0.000 0.128 0.196
#&gt; SRR975587     3  0.3409     0.5723 0.300 0.000 0.700 0.000 0.000 0.000
#&gt; SRR975588     2  0.1245     0.9157 0.000 0.952 0.000 0.000 0.032 0.016
#&gt; SRR975589     5  0.3320     0.7494 0.212 0.000 0.000 0.000 0.772 0.016
#&gt; SRR975590     1  0.1151     0.7366 0.956 0.000 0.012 0.000 0.032 0.000
#&gt; SRR975591     3  0.1267     0.8292 0.000 0.000 0.940 0.000 0.060 0.000
#&gt; SRR975592     1  0.4993     0.1568 0.572 0.000 0.084 0.000 0.344 0.000
#&gt; SRR975593     5  0.6235     0.1480 0.364 0.000 0.000 0.016 0.424 0.196
#&gt; SRR975594     3  0.0000     0.8430 0.000 0.000 1.000 0.000 0.000 0.000
#&gt; SRR975595     6  0.3866     0.3584 0.484 0.000 0.000 0.000 0.000 0.516
#&gt; SRR975597     1  0.1584     0.7120 0.928 0.000 0.000 0.000 0.008 0.064
#&gt; SRR975596     6  0.4568     0.6950 0.232 0.000 0.000 0.036 0.032 0.700
#&gt; SRR975598     6  0.3729     0.6763 0.296 0.000 0.000 0.000 0.012 0.692
#&gt; SRR975599     6  0.3582     0.7057 0.252 0.000 0.000 0.000 0.016 0.732
#&gt; SRR975600     5  0.3551     0.7238 0.148 0.000 0.060 0.000 0.792 0.000
#&gt; SRR975601     3  0.0000     0.8430 0.000 0.000 1.000 0.000 0.000 0.000
#&gt; SRR975602     1  0.1524     0.7190 0.932 0.000 0.000 0.000 0.008 0.060
#&gt; SRR975603     3  0.3198     0.6132 0.000 0.000 0.740 0.000 0.260 0.000
#&gt; SRR975604     3  0.0405     0.8410 0.000 0.000 0.988 0.000 0.008 0.004
</code></pre>

<script>
$('#tab-MAD-NMF-get-classes-5-a').parent().next().next().hide();
$('#tab-MAD-NMF-get-classes-5-a').click(function(){
  $('#tab-MAD-NMF-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-MAD-NMF-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-MAD-NMF-consensus-heatmap'>
<ul>
<li><a href='#tab-MAD-NMF-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-MAD-NMF-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-MAD-NMF-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-MAD-NMF-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-MAD-NMF-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-NMF-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-consensus-heatmap-1-1.png" alt="plot of chunk tab-MAD-NMF-consensus-heatmap-1"/></p>

</div>
<div id='tab-MAD-NMF-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-consensus-heatmap-2-1.png" alt="plot of chunk tab-MAD-NMF-consensus-heatmap-2"/></p>

</div>
<div id='tab-MAD-NMF-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-consensus-heatmap-3-1.png" alt="plot of chunk tab-MAD-NMF-consensus-heatmap-3"/></p>

</div>
<div id='tab-MAD-NMF-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-consensus-heatmap-4-1.png" alt="plot of chunk tab-MAD-NMF-consensus-heatmap-4"/></p>

</div>
<div id='tab-MAD-NMF-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-consensus-heatmap-5-1.png" alt="plot of chunk tab-MAD-NMF-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-MAD-NMF-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-MAD-NMF-membership-heatmap'>
<ul>
<li><a href='#tab-MAD-NMF-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-MAD-NMF-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-MAD-NMF-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-MAD-NMF-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-MAD-NMF-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-NMF-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-membership-heatmap-1-1.png" alt="plot of chunk tab-MAD-NMF-membership-heatmap-1"/></p>

</div>
<div id='tab-MAD-NMF-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-membership-heatmap-2-1.png" alt="plot of chunk tab-MAD-NMF-membership-heatmap-2"/></p>

</div>
<div id='tab-MAD-NMF-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-membership-heatmap-3-1.png" alt="plot of chunk tab-MAD-NMF-membership-heatmap-3"/></p>

</div>
<div id='tab-MAD-NMF-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-membership-heatmap-4-1.png" alt="plot of chunk tab-MAD-NMF-membership-heatmap-4"/></p>

</div>
<div id='tab-MAD-NMF-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-membership-heatmap-5-1.png" alt="plot of chunk tab-MAD-NMF-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-MAD-NMF-get-signatures' ).tabs();
} );
</script>
<div id='tabs-MAD-NMF-get-signatures'>
<ul>
<li><a href='#tab-MAD-NMF-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-MAD-NMF-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-MAD-NMF-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-MAD-NMF-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-MAD-NMF-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-NMF-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-get-signatures-1-1.png" alt="plot of chunk tab-MAD-NMF-get-signatures-1"/></p>

</div>
<div id='tab-MAD-NMF-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-get-signatures-2-1.png" alt="plot of chunk tab-MAD-NMF-get-signatures-2"/></p>

</div>
<div id='tab-MAD-NMF-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-get-signatures-3-1.png" alt="plot of chunk tab-MAD-NMF-get-signatures-3"/></p>

</div>
<div id='tab-MAD-NMF-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-get-signatures-4-1.png" alt="plot of chunk tab-MAD-NMF-get-signatures-4"/></p>

</div>
<div id='tab-MAD-NMF-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-get-signatures-5-1.png" alt="plot of chunk tab-MAD-NMF-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-MAD-NMF-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-MAD-NMF-get-signatures-no-scale'>
<ul>
<li><a href='#tab-MAD-NMF-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-MAD-NMF-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-MAD-NMF-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-MAD-NMF-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-MAD-NMF-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-NMF-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-MAD-NMF-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-MAD-NMF-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-MAD-NMF-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-MAD-NMF-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-MAD-NMF-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-MAD-NMF-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-MAD-NMF-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-MAD-NMF-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-MAD-NMF-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk MAD-NMF-signature_compare](figure_cola/MAD-NMF-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-MAD-NMF-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-MAD-NMF-dimension-reduction'>
<ul>
<li><a href='#tab-MAD-NMF-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-MAD-NMF-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-MAD-NMF-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-MAD-NMF-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-MAD-NMF-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-NMF-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-dimension-reduction-1-1.png" alt="plot of chunk tab-MAD-NMF-dimension-reduction-1"/></p>

</div>
<div id='tab-MAD-NMF-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-dimension-reduction-2-1.png" alt="plot of chunk tab-MAD-NMF-dimension-reduction-2"/></p>

</div>
<div id='tab-MAD-NMF-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-dimension-reduction-3-1.png" alt="plot of chunk tab-MAD-NMF-dimension-reduction-3"/></p>

</div>
<div id='tab-MAD-NMF-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-dimension-reduction-4-1.png" alt="plot of chunk tab-MAD-NMF-dimension-reduction-4"/></p>

</div>
<div id='tab-MAD-NMF-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-dimension-reduction-5-1.png" alt="plot of chunk tab-MAD-NMF-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk MAD-NMF-collect-classes](figure_cola/MAD-NMF-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### ATC:hclust**






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["ATC", "hclust"]
# you can also extract it by
# res = res_list["ATC:hclust"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 17171 rows and 54 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'ATC' method.
#>   Subgroups are detected by 'hclust' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 3.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk ATC-hclust-collect-plots](figure_cola/ATC-hclust-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk ATC-hclust-select-partition-number](figure_cola/ATC-hclust-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 1.000           1.000       1.000         0.5099 0.491   0.491
#> 3 3 1.000           0.987       0.994         0.0780 0.965   0.929
#> 4 4 0.821           0.761       0.857         0.1529 0.874   0.724
#> 5 5 0.846           0.893       0.951         0.0785 0.904   0.741
#> 6 6 0.746           0.752       0.871         0.0759 0.947   0.833
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 3
#> attr(,"optional")
#> [1] 2
```

There is also optional best $k$ = 2 that is worth to check.

Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-ATC-hclust-get-classes' ).tabs();
} );
</script>
<div id='tabs-ATC-hclust-get-classes'>
<ul>
<li><a href='#tab-ATC-hclust-get-classes-1'>k = 2</a></li>
<li><a href='#tab-ATC-hclust-get-classes-2'>k = 3</a></li>
<li><a href='#tab-ATC-hclust-get-classes-3'>k = 4</a></li>
<li><a href='#tab-ATC-hclust-get-classes-4'>k = 5</a></li>
<li><a href='#tab-ATC-hclust-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-ATC-hclust-get-classes-1'>
<p><a id='tab-ATC-hclust-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;           class entropy silhouette p1 p2
#&gt; SRR975551     1       0          1  1  0
#&gt; SRR975552     1       0          1  1  0
#&gt; SRR975554     1       0          1  1  0
#&gt; SRR975553     2       0          1  0  1
#&gt; SRR975555     1       0          1  1  0
#&gt; SRR975556     2       0          1  0  1
#&gt; SRR975557     2       0          1  0  1
#&gt; SRR975558     1       0          1  1  0
#&gt; SRR975559     1       0          1  1  0
#&gt; SRR975560     2       0          1  0  1
#&gt; SRR975561     2       0          1  0  1
#&gt; SRR975562     1       0          1  1  0
#&gt; SRR975563     2       0          1  0  1
#&gt; SRR975564     1       0          1  1  0
#&gt; SRR975565     1       0          1  1  0
#&gt; SRR975566     1       0          1  1  0
#&gt; SRR975567     1       0          1  1  0
#&gt; SRR975568     1       0          1  1  0
#&gt; SRR975569     2       0          1  0  1
#&gt; SRR975570     2       0          1  0  1
#&gt; SRR975571     2       0          1  0  1
#&gt; SRR975572     2       0          1  0  1
#&gt; SRR975573     2       0          1  0  1
#&gt; SRR975574     2       0          1  0  1
#&gt; SRR975575     2       0          1  0  1
#&gt; SRR975576     2       0          1  0  1
#&gt; SRR975577     2       0          1  0  1
#&gt; SRR975578     2       0          1  0  1
#&gt; SRR975579     2       0          1  0  1
#&gt; SRR975580     2       0          1  0  1
#&gt; SRR975581     2       0          1  0  1
#&gt; SRR975582     2       0          1  0  1
#&gt; SRR975583     2       0          1  0  1
#&gt; SRR975584     2       0          1  0  1
#&gt; SRR975585     2       0          1  0  1
#&gt; SRR975586     2       0          1  0  1
#&gt; SRR975587     1       0          1  1  0
#&gt; SRR975588     2       0          1  0  1
#&gt; SRR975589     1       0          1  1  0
#&gt; SRR975590     1       0          1  1  0
#&gt; SRR975591     1       0          1  1  0
#&gt; SRR975592     1       0          1  1  0
#&gt; SRR975593     1       0          1  1  0
#&gt; SRR975594     2       0          1  0  1
#&gt; SRR975595     1       0          1  1  0
#&gt; SRR975597     1       0          1  1  0
#&gt; SRR975596     1       0          1  1  0
#&gt; SRR975598     1       0          1  1  0
#&gt; SRR975599     2       0          1  0  1
#&gt; SRR975600     1       0          1  1  0
#&gt; SRR975601     1       0          1  1  0
#&gt; SRR975602     1       0          1  1  0
#&gt; SRR975603     1       0          1  1  0
#&gt; SRR975604     1       0          1  1  0
</code></pre>

<script>
$('#tab-ATC-hclust-get-classes-1-a').parent().next().next().hide();
$('#tab-ATC-hclust-get-classes-1-a').click(function(){
  $('#tab-ATC-hclust-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-hclust-get-classes-2'>
<p><a id='tab-ATC-hclust-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;           class entropy silhouette p1    p2    p3
#&gt; SRR975551     1   0.000      1.000  1 0.000 0.000
#&gt; SRR975552     1   0.000      1.000  1 0.000 0.000
#&gt; SRR975554     1   0.000      1.000  1 0.000 0.000
#&gt; SRR975553     2   0.000      0.986  0 1.000 0.000
#&gt; SRR975555     1   0.000      1.000  1 0.000 0.000
#&gt; SRR975556     2   0.000      0.986  0 1.000 0.000
#&gt; SRR975557     2   0.510      0.679  0 0.752 0.248
#&gt; SRR975558     1   0.000      1.000  1 0.000 0.000
#&gt; SRR975559     1   0.000      1.000  1 0.000 0.000
#&gt; SRR975560     2   0.000      0.986  0 1.000 0.000
#&gt; SRR975561     2   0.000      0.986  0 1.000 0.000
#&gt; SRR975562     1   0.000      1.000  1 0.000 0.000
#&gt; SRR975563     2   0.000      0.986  0 1.000 0.000
#&gt; SRR975564     1   0.000      1.000  1 0.000 0.000
#&gt; SRR975565     1   0.000      1.000  1 0.000 0.000
#&gt; SRR975566     1   0.000      1.000  1 0.000 0.000
#&gt; SRR975567     1   0.000      1.000  1 0.000 0.000
#&gt; SRR975568     1   0.000      1.000  1 0.000 0.000
#&gt; SRR975569     2   0.000      0.986  0 1.000 0.000
#&gt; SRR975570     2   0.000      0.986  0 1.000 0.000
#&gt; SRR975571     2   0.000      0.986  0 1.000 0.000
#&gt; SRR975572     2   0.000      0.986  0 1.000 0.000
#&gt; SRR975573     2   0.000      0.986  0 1.000 0.000
#&gt; SRR975574     2   0.000      0.986  0 1.000 0.000
#&gt; SRR975575     2   0.000      0.986  0 1.000 0.000
#&gt; SRR975576     2   0.000      0.986  0 1.000 0.000
#&gt; SRR975577     2   0.000      0.986  0 1.000 0.000
#&gt; SRR975578     2   0.000      0.986  0 1.000 0.000
#&gt; SRR975579     2   0.245      0.912  0 0.924 0.076
#&gt; SRR975580     2   0.000      0.986  0 1.000 0.000
#&gt; SRR975581     2   0.000      0.986  0 1.000 0.000
#&gt; SRR975582     2   0.000      0.986  0 1.000 0.000
#&gt; SRR975583     2   0.000      0.986  0 1.000 0.000
#&gt; SRR975584     2   0.000      0.986  0 1.000 0.000
#&gt; SRR975585     2   0.000      0.986  0 1.000 0.000
#&gt; SRR975586     2   0.000      0.986  0 1.000 0.000
#&gt; SRR975587     1   0.000      1.000  1 0.000 0.000
#&gt; SRR975588     2   0.000      0.986  0 1.000 0.000
#&gt; SRR975589     1   0.000      1.000  1 0.000 0.000
#&gt; SRR975590     1   0.000      1.000  1 0.000 0.000
#&gt; SRR975591     1   0.000      1.000  1 0.000 0.000
#&gt; SRR975592     1   0.000      1.000  1 0.000 0.000
#&gt; SRR975593     1   0.000      1.000  1 0.000 0.000
#&gt; SRR975594     3   0.000      1.000  0 0.000 1.000
#&gt; SRR975595     1   0.000      1.000  1 0.000 0.000
#&gt; SRR975597     1   0.000      1.000  1 0.000 0.000
#&gt; SRR975596     1   0.000      1.000  1 0.000 0.000
#&gt; SRR975598     1   0.000      1.000  1 0.000 0.000
#&gt; SRR975599     3   0.000      1.000  0 0.000 1.000
#&gt; SRR975600     1   0.000      1.000  1 0.000 0.000
#&gt; SRR975601     1   0.000      1.000  1 0.000 0.000
#&gt; SRR975602     1   0.000      1.000  1 0.000 0.000
#&gt; SRR975603     1   0.000      1.000  1 0.000 0.000
#&gt; SRR975604     1   0.000      1.000  1 0.000 0.000
</code></pre>

<script>
$('#tab-ATC-hclust-get-classes-2-a').parent().next().next().hide();
$('#tab-ATC-hclust-get-classes-2-a').click(function(){
  $('#tab-ATC-hclust-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-hclust-get-classes-3'>
<p><a id='tab-ATC-hclust-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3    p4
#&gt; SRR975551     1   0.464      0.944 0.656 0.000 0.344 0.000
#&gt; SRR975552     1   0.464      0.944 0.656 0.000 0.344 0.000
#&gt; SRR975554     1   0.464      0.944 0.656 0.000 0.344 0.000
#&gt; SRR975553     2   0.000      0.958 0.000 1.000 0.000 0.000
#&gt; SRR975555     3   0.499     -0.539 0.476 0.000 0.524 0.000
#&gt; SRR975556     2   0.000      0.958 0.000 1.000 0.000 0.000
#&gt; SRR975557     2   0.778     -0.133 0.344 0.408 0.000 0.248
#&gt; SRR975558     3   0.000      0.693 0.000 0.000 1.000 0.000
#&gt; SRR975559     1   0.476      0.911 0.628 0.000 0.372 0.000
#&gt; SRR975560     2   0.000      0.958 0.000 1.000 0.000 0.000
#&gt; SRR975561     2   0.000      0.958 0.000 1.000 0.000 0.000
#&gt; SRR975562     3   0.130      0.668 0.044 0.000 0.956 0.000
#&gt; SRR975563     2   0.000      0.958 0.000 1.000 0.000 0.000
#&gt; SRR975564     3   0.498     -0.502 0.464 0.000 0.536 0.000
#&gt; SRR975565     1   0.464      0.944 0.656 0.000 0.344 0.000
#&gt; SRR975566     1   0.464      0.944 0.656 0.000 0.344 0.000
#&gt; SRR975567     3   0.000      0.693 0.000 0.000 1.000 0.000
#&gt; SRR975568     3   0.499     -0.515 0.468 0.000 0.532 0.000
#&gt; SRR975569     2   0.000      0.958 0.000 1.000 0.000 0.000
#&gt; SRR975570     2   0.000      0.958 0.000 1.000 0.000 0.000
#&gt; SRR975571     2   0.000      0.958 0.000 1.000 0.000 0.000
#&gt; SRR975572     2   0.000      0.958 0.000 1.000 0.000 0.000
#&gt; SRR975573     2   0.000      0.958 0.000 1.000 0.000 0.000
#&gt; SRR975574     2   0.000      0.958 0.000 1.000 0.000 0.000
#&gt; SRR975575     2   0.000      0.958 0.000 1.000 0.000 0.000
#&gt; SRR975576     2   0.000      0.958 0.000 1.000 0.000 0.000
#&gt; SRR975577     2   0.000      0.958 0.000 1.000 0.000 0.000
#&gt; SRR975578     2   0.000      0.958 0.000 1.000 0.000 0.000
#&gt; SRR975579     2   0.634      0.371 0.344 0.580 0.000 0.076
#&gt; SRR975580     2   0.000      0.958 0.000 1.000 0.000 0.000
#&gt; SRR975581     2   0.000      0.958 0.000 1.000 0.000 0.000
#&gt; SRR975582     2   0.000      0.958 0.000 1.000 0.000 0.000
#&gt; SRR975583     2   0.000      0.958 0.000 1.000 0.000 0.000
#&gt; SRR975584     2   0.000      0.958 0.000 1.000 0.000 0.000
#&gt; SRR975585     2   0.000      0.958 0.000 1.000 0.000 0.000
#&gt; SRR975586     2   0.000      0.958 0.000 1.000 0.000 0.000
#&gt; SRR975587     1   0.464      0.944 0.656 0.000 0.344 0.000
#&gt; SRR975588     2   0.000      0.958 0.000 1.000 0.000 0.000
#&gt; SRR975589     1   0.500      0.596 0.508 0.000 0.492 0.000
#&gt; SRR975590     1   0.464      0.944 0.656 0.000 0.344 0.000
#&gt; SRR975591     3   0.000      0.693 0.000 0.000 1.000 0.000
#&gt; SRR975592     1   0.464      0.944 0.656 0.000 0.344 0.000
#&gt; SRR975593     1   0.500      0.596 0.508 0.000 0.492 0.000
#&gt; SRR975594     4   0.000      1.000 0.000 0.000 0.000 1.000
#&gt; SRR975595     1   0.476      0.911 0.628 0.000 0.372 0.000
#&gt; SRR975597     1   0.464      0.944 0.656 0.000 0.344 0.000
#&gt; SRR975596     3   0.130      0.668 0.044 0.000 0.956 0.000
#&gt; SRR975598     1   0.468      0.934 0.648 0.000 0.352 0.000
#&gt; SRR975599     4   0.000      1.000 0.000 0.000 0.000 1.000
#&gt; SRR975600     3   0.498     -0.502 0.464 0.000 0.536 0.000
#&gt; SRR975601     3   0.000      0.693 0.000 0.000 1.000 0.000
#&gt; SRR975602     1   0.464      0.944 0.656 0.000 0.344 0.000
#&gt; SRR975603     3   0.000      0.693 0.000 0.000 1.000 0.000
#&gt; SRR975604     3   0.000      0.693 0.000 0.000 1.000 0.000
</code></pre>

<script>
$('#tab-ATC-hclust-get-classes-3-a').parent().next().next().hide();
$('#tab-ATC-hclust-get-classes-3-a').click(function(){
  $('#tab-ATC-hclust-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-hclust-get-classes-4'>
<p><a id='tab-ATC-hclust-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1   p2    p3   p4 p5
#&gt; SRR975551     1   0.000      0.874 1.000 0.00 0.000 0.00  0
#&gt; SRR975552     1   0.000      0.874 1.000 0.00 0.000 0.00  0
#&gt; SRR975554     1   0.000      0.874 1.000 0.00 0.000 0.00  0
#&gt; SRR975553     2   0.000      1.000 0.000 1.00 0.000 0.00  0
#&gt; SRR975555     1   0.377      0.680 0.704 0.00 0.296 0.00  0
#&gt; SRR975556     2   0.000      1.000 0.000 1.00 0.000 0.00  0
#&gt; SRR975557     4   0.000      0.530 0.000 0.00 0.000 1.00  0
#&gt; SRR975558     3   0.000      0.892 0.000 0.00 1.000 0.00  0
#&gt; SRR975559     1   0.265      0.806 0.848 0.00 0.152 0.00  0
#&gt; SRR975560     2   0.000      1.000 0.000 1.00 0.000 0.00  0
#&gt; SRR975561     2   0.000      1.000 0.000 1.00 0.000 0.00  0
#&gt; SRR975562     3   0.337      0.672 0.232 0.00 0.768 0.00  0
#&gt; SRR975563     2   0.000      1.000 0.000 1.00 0.000 0.00  0
#&gt; SRR975564     1   0.386      0.660 0.688 0.00 0.312 0.00  0
#&gt; SRR975565     1   0.000      0.874 1.000 0.00 0.000 0.00  0
#&gt; SRR975566     1   0.000      0.874 1.000 0.00 0.000 0.00  0
#&gt; SRR975567     3   0.000      0.892 0.000 0.00 1.000 0.00  0
#&gt; SRR975568     1   0.384      0.666 0.692 0.00 0.308 0.00  0
#&gt; SRR975569     2   0.000      1.000 0.000 1.00 0.000 0.00  0
#&gt; SRR975570     2   0.000      1.000 0.000 1.00 0.000 0.00  0
#&gt; SRR975571     2   0.000      1.000 0.000 1.00 0.000 0.00  0
#&gt; SRR975572     2   0.000      1.000 0.000 1.00 0.000 0.00  0
#&gt; SRR975573     2   0.000      1.000 0.000 1.00 0.000 0.00  0
#&gt; SRR975574     2   0.000      1.000 0.000 1.00 0.000 0.00  0
#&gt; SRR975575     2   0.000      1.000 0.000 1.00 0.000 0.00  0
#&gt; SRR975576     2   0.000      1.000 0.000 1.00 0.000 0.00  0
#&gt; SRR975577     2   0.000      1.000 0.000 1.00 0.000 0.00  0
#&gt; SRR975578     2   0.000      1.000 0.000 1.00 0.000 0.00  0
#&gt; SRR975579     4   0.293      0.572 0.000 0.18 0.000 0.82  0
#&gt; SRR975580     2   0.000      1.000 0.000 1.00 0.000 0.00  0
#&gt; SRR975581     2   0.000      1.000 0.000 1.00 0.000 0.00  0
#&gt; SRR975582     2   0.000      1.000 0.000 1.00 0.000 0.00  0
#&gt; SRR975583     2   0.000      1.000 0.000 1.00 0.000 0.00  0
#&gt; SRR975584     2   0.000      1.000 0.000 1.00 0.000 0.00  0
#&gt; SRR975585     2   0.000      1.000 0.000 1.00 0.000 0.00  0
#&gt; SRR975586     2   0.000      1.000 0.000 1.00 0.000 0.00  0
#&gt; SRR975587     1   0.000      0.874 1.000 0.00 0.000 0.00  0
#&gt; SRR975588     2   0.000      1.000 0.000 1.00 0.000 0.00  0
#&gt; SRR975589     1   0.307      0.775 0.804 0.00 0.196 0.00  0
#&gt; SRR975590     1   0.000      0.874 1.000 0.00 0.000 0.00  0
#&gt; SRR975591     3   0.000      0.892 0.000 0.00 1.000 0.00  0
#&gt; SRR975592     1   0.000      0.874 1.000 0.00 0.000 0.00  0
#&gt; SRR975593     1   0.307      0.775 0.804 0.00 0.196 0.00  0
#&gt; SRR975594     5   0.000      1.000 0.000 0.00 0.000 0.00  1
#&gt; SRR975595     1   0.265      0.806 0.848 0.00 0.152 0.00  0
#&gt; SRR975597     1   0.000      0.874 1.000 0.00 0.000 0.00  0
#&gt; SRR975596     3   0.337      0.672 0.232 0.00 0.768 0.00  0
#&gt; SRR975598     1   0.154      0.851 0.932 0.00 0.068 0.00  0
#&gt; SRR975599     5   0.000      1.000 0.000 0.00 0.000 0.00  1
#&gt; SRR975600     1   0.386      0.660 0.688 0.00 0.312 0.00  0
#&gt; SRR975601     3   0.000      0.892 0.000 0.00 1.000 0.00  0
#&gt; SRR975602     1   0.000      0.874 1.000 0.00 0.000 0.00  0
#&gt; SRR975603     3   0.000      0.892 0.000 0.00 1.000 0.00  0
#&gt; SRR975604     3   0.000      0.892 0.000 0.00 1.000 0.00  0
</code></pre>

<script>
$('#tab-ATC-hclust-get-classes-4-a').parent().next().next().hide();
$('#tab-ATC-hclust-get-classes-4-a').click(function(){
  $('#tab-ATC-hclust-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-hclust-get-classes-5'>
<p><a id='tab-ATC-hclust-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3   p4 p5    p6
#&gt; SRR975551     1  0.2048      0.789 0.880 0.000 0.000 0.00  0 0.120
#&gt; SRR975552     1  0.2048      0.789 0.880 0.000 0.000 0.00  0 0.120
#&gt; SRR975554     1  0.2048      0.789 0.880 0.000 0.000 0.00  0 0.120
#&gt; SRR975553     2  0.0000      0.885 0.000 1.000 0.000 0.00  0 0.000
#&gt; SRR975555     1  0.4281      0.668 0.704 0.000 0.228 0.00  0 0.068
#&gt; SRR975556     6  0.3851      0.991 0.000 0.460 0.000 0.00  0 0.540
#&gt; SRR975557     4  0.0000      0.530 0.000 0.000 0.000 1.00  0 0.000
#&gt; SRR975558     3  0.3244      0.706 0.000 0.000 0.732 0.00  0 0.268
#&gt; SRR975559     1  0.3626      0.736 0.788 0.000 0.144 0.00  0 0.068
#&gt; SRR975560     6  0.3847      0.997 0.000 0.456 0.000 0.00  0 0.544
#&gt; SRR975561     2  0.3620     -0.390 0.000 0.648 0.000 0.00  0 0.352
#&gt; SRR975562     3  0.3874      0.685 0.172 0.000 0.760 0.00  0 0.068
#&gt; SRR975563     2  0.0000      0.885 0.000 1.000 0.000 0.00  0 0.000
#&gt; SRR975564     1  0.4377      0.650 0.688 0.000 0.244 0.00  0 0.068
#&gt; SRR975565     1  0.2048      0.789 0.880 0.000 0.000 0.00  0 0.120
#&gt; SRR975566     1  0.0865      0.820 0.964 0.000 0.000 0.00  0 0.036
#&gt; SRR975567     3  0.3244      0.706 0.000 0.000 0.732 0.00  0 0.268
#&gt; SRR975568     1  0.4354      0.655 0.692 0.000 0.240 0.00  0 0.068
#&gt; SRR975569     2  0.0000      0.885 0.000 1.000 0.000 0.00  0 0.000
#&gt; SRR975570     2  0.0000      0.885 0.000 1.000 0.000 0.00  0 0.000
#&gt; SRR975571     2  0.0000      0.885 0.000 1.000 0.000 0.00  0 0.000
#&gt; SRR975572     2  0.0000      0.885 0.000 1.000 0.000 0.00  0 0.000
#&gt; SRR975573     2  0.0000      0.885 0.000 1.000 0.000 0.00  0 0.000
#&gt; SRR975574     2  0.0000      0.885 0.000 1.000 0.000 0.00  0 0.000
#&gt; SRR975575     2  0.0000      0.885 0.000 1.000 0.000 0.00  0 0.000
#&gt; SRR975576     2  0.0000      0.885 0.000 1.000 0.000 0.00  0 0.000
#&gt; SRR975577     2  0.3620     -0.390 0.000 0.648 0.000 0.00  0 0.352
#&gt; SRR975578     2  0.3620     -0.390 0.000 0.648 0.000 0.00  0 0.352
#&gt; SRR975579     4  0.2631      0.572 0.000 0.180 0.000 0.82  0 0.000
#&gt; SRR975580     6  0.3847      0.997 0.000 0.456 0.000 0.00  0 0.544
#&gt; SRR975581     2  0.0000      0.885 0.000 1.000 0.000 0.00  0 0.000
#&gt; SRR975582     2  0.0000      0.885 0.000 1.000 0.000 0.00  0 0.000
#&gt; SRR975583     2  0.0000      0.885 0.000 1.000 0.000 0.00  0 0.000
#&gt; SRR975584     2  0.0000      0.885 0.000 1.000 0.000 0.00  0 0.000
#&gt; SRR975585     2  0.0000      0.885 0.000 1.000 0.000 0.00  0 0.000
#&gt; SRR975586     6  0.3847      0.997 0.000 0.456 0.000 0.00  0 0.544
#&gt; SRR975587     1  0.0000      0.823 1.000 0.000 0.000 0.00  0 0.000
#&gt; SRR975588     2  0.0000      0.885 0.000 1.000 0.000 0.00  0 0.000
#&gt; SRR975589     1  0.3283      0.748 0.804 0.000 0.160 0.00  0 0.036
#&gt; SRR975590     1  0.2048      0.789 0.880 0.000 0.000 0.00  0 0.120
#&gt; SRR975591     3  0.0000      0.829 0.000 0.000 1.000 0.00  0 0.000
#&gt; SRR975592     1  0.0000      0.823 1.000 0.000 0.000 0.00  0 0.000
#&gt; SRR975593     1  0.3283      0.748 0.804 0.000 0.160 0.00  0 0.036
#&gt; SRR975594     5  0.0000      1.000 0.000 0.000 0.000 0.00  1 0.000
#&gt; SRR975595     1  0.3626      0.736 0.788 0.000 0.144 0.00  0 0.068
#&gt; SRR975597     1  0.0363      0.822 0.988 0.000 0.000 0.00  0 0.012
#&gt; SRR975596     3  0.3874      0.685 0.172 0.000 0.760 0.00  0 0.068
#&gt; SRR975598     1  0.2629      0.796 0.872 0.000 0.060 0.00  0 0.068
#&gt; SRR975599     5  0.0000      1.000 0.000 0.000 0.000 0.00  1 0.000
#&gt; SRR975600     1  0.4377      0.650 0.688 0.000 0.244 0.00  0 0.068
#&gt; SRR975601     3  0.0000      0.829 0.000 0.000 1.000 0.00  0 0.000
#&gt; SRR975602     1  0.0865      0.820 0.964 0.000 0.000 0.00  0 0.036
#&gt; SRR975603     3  0.0000      0.829 0.000 0.000 1.000 0.00  0 0.000
#&gt; SRR975604     3  0.0000      0.829 0.000 0.000 1.000 0.00  0 0.000
</code></pre>

<script>
$('#tab-ATC-hclust-get-classes-5-a').parent().next().next().hide();
$('#tab-ATC-hclust-get-classes-5-a').click(function(){
  $('#tab-ATC-hclust-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-ATC-hclust-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-ATC-hclust-consensus-heatmap'>
<ul>
<li><a href='#tab-ATC-hclust-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-ATC-hclust-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-ATC-hclust-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-ATC-hclust-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-ATC-hclust-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-hclust-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-consensus-heatmap-1-1.png" alt="plot of chunk tab-ATC-hclust-consensus-heatmap-1"/></p>

</div>
<div id='tab-ATC-hclust-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-consensus-heatmap-2-1.png" alt="plot of chunk tab-ATC-hclust-consensus-heatmap-2"/></p>

</div>
<div id='tab-ATC-hclust-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-consensus-heatmap-3-1.png" alt="plot of chunk tab-ATC-hclust-consensus-heatmap-3"/></p>

</div>
<div id='tab-ATC-hclust-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-consensus-heatmap-4-1.png" alt="plot of chunk tab-ATC-hclust-consensus-heatmap-4"/></p>

</div>
<div id='tab-ATC-hclust-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-consensus-heatmap-5-1.png" alt="plot of chunk tab-ATC-hclust-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-ATC-hclust-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-ATC-hclust-membership-heatmap'>
<ul>
<li><a href='#tab-ATC-hclust-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-ATC-hclust-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-ATC-hclust-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-ATC-hclust-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-ATC-hclust-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-hclust-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-membership-heatmap-1-1.png" alt="plot of chunk tab-ATC-hclust-membership-heatmap-1"/></p>

</div>
<div id='tab-ATC-hclust-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-membership-heatmap-2-1.png" alt="plot of chunk tab-ATC-hclust-membership-heatmap-2"/></p>

</div>
<div id='tab-ATC-hclust-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-membership-heatmap-3-1.png" alt="plot of chunk tab-ATC-hclust-membership-heatmap-3"/></p>

</div>
<div id='tab-ATC-hclust-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-membership-heatmap-4-1.png" alt="plot of chunk tab-ATC-hclust-membership-heatmap-4"/></p>

</div>
<div id='tab-ATC-hclust-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-membership-heatmap-5-1.png" alt="plot of chunk tab-ATC-hclust-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-ATC-hclust-get-signatures' ).tabs();
} );
</script>
<div id='tabs-ATC-hclust-get-signatures'>
<ul>
<li><a href='#tab-ATC-hclust-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-ATC-hclust-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-ATC-hclust-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-ATC-hclust-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-ATC-hclust-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-hclust-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-get-signatures-1-1.png" alt="plot of chunk tab-ATC-hclust-get-signatures-1"/></p>

</div>
<div id='tab-ATC-hclust-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-get-signatures-2-1.png" alt="plot of chunk tab-ATC-hclust-get-signatures-2"/></p>

</div>
<div id='tab-ATC-hclust-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-get-signatures-3-1.png" alt="plot of chunk tab-ATC-hclust-get-signatures-3"/></p>

</div>
<div id='tab-ATC-hclust-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-get-signatures-4-1.png" alt="plot of chunk tab-ATC-hclust-get-signatures-4"/></p>

</div>
<div id='tab-ATC-hclust-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-get-signatures-5-1.png" alt="plot of chunk tab-ATC-hclust-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-ATC-hclust-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-ATC-hclust-get-signatures-no-scale'>
<ul>
<li><a href='#tab-ATC-hclust-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-ATC-hclust-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-ATC-hclust-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-ATC-hclust-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-ATC-hclust-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-hclust-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-ATC-hclust-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-ATC-hclust-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-ATC-hclust-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-ATC-hclust-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-ATC-hclust-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-ATC-hclust-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-ATC-hclust-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-ATC-hclust-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-ATC-hclust-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk ATC-hclust-signature_compare](figure_cola/ATC-hclust-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-ATC-hclust-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-ATC-hclust-dimension-reduction'>
<ul>
<li><a href='#tab-ATC-hclust-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-ATC-hclust-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-ATC-hclust-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-ATC-hclust-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-ATC-hclust-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-hclust-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-dimension-reduction-1-1.png" alt="plot of chunk tab-ATC-hclust-dimension-reduction-1"/></p>

</div>
<div id='tab-ATC-hclust-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-dimension-reduction-2-1.png" alt="plot of chunk tab-ATC-hclust-dimension-reduction-2"/></p>

</div>
<div id='tab-ATC-hclust-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-dimension-reduction-3-1.png" alt="plot of chunk tab-ATC-hclust-dimension-reduction-3"/></p>

</div>
<div id='tab-ATC-hclust-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-dimension-reduction-4-1.png" alt="plot of chunk tab-ATC-hclust-dimension-reduction-4"/></p>

</div>
<div id='tab-ATC-hclust-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-dimension-reduction-5-1.png" alt="plot of chunk tab-ATC-hclust-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk ATC-hclust-collect-classes](figure_cola/ATC-hclust-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### ATC:kmeans*






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["ATC", "kmeans"]
# you can also extract it by
# res = res_list["ATC:kmeans"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 17171 rows and 54 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'ATC' method.
#>   Subgroups are detected by 'kmeans' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 3.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk ATC-kmeans-collect-plots](figure_cola/ATC-kmeans-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk ATC-kmeans-select-partition-number](figure_cola/ATC-kmeans-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 1.000           1.000       1.000         0.5099 0.491   0.491
#> 3 3 0.904           0.932       0.968         0.1661 0.929   0.857
#> 4 4 0.815           0.846       0.892         0.1281 0.874   0.707
#> 5 5 0.689           0.747       0.834         0.0824 0.954   0.854
#> 6 6 0.731           0.710       0.813         0.0506 0.979   0.924
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 3
#> attr(,"optional")
#> [1] 2
```

There is also optional best $k$ = 2 that is worth to check.

Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-ATC-kmeans-get-classes' ).tabs();
} );
</script>
<div id='tabs-ATC-kmeans-get-classes'>
<ul>
<li><a href='#tab-ATC-kmeans-get-classes-1'>k = 2</a></li>
<li><a href='#tab-ATC-kmeans-get-classes-2'>k = 3</a></li>
<li><a href='#tab-ATC-kmeans-get-classes-3'>k = 4</a></li>
<li><a href='#tab-ATC-kmeans-get-classes-4'>k = 5</a></li>
<li><a href='#tab-ATC-kmeans-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-ATC-kmeans-get-classes-1'>
<p><a id='tab-ATC-kmeans-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;           class entropy silhouette p1 p2
#&gt; SRR975551     1       0          1  1  0
#&gt; SRR975552     1       0          1  1  0
#&gt; SRR975554     1       0          1  1  0
#&gt; SRR975553     2       0          1  0  1
#&gt; SRR975555     1       0          1  1  0
#&gt; SRR975556     2       0          1  0  1
#&gt; SRR975557     2       0          1  0  1
#&gt; SRR975558     1       0          1  1  0
#&gt; SRR975559     1       0          1  1  0
#&gt; SRR975560     2       0          1  0  1
#&gt; SRR975561     2       0          1  0  1
#&gt; SRR975562     1       0          1  1  0
#&gt; SRR975563     2       0          1  0  1
#&gt; SRR975564     1       0          1  1  0
#&gt; SRR975565     1       0          1  1  0
#&gt; SRR975566     1       0          1  1  0
#&gt; SRR975567     1       0          1  1  0
#&gt; SRR975568     1       0          1  1  0
#&gt; SRR975569     2       0          1  0  1
#&gt; SRR975570     2       0          1  0  1
#&gt; SRR975571     2       0          1  0  1
#&gt; SRR975572     2       0          1  0  1
#&gt; SRR975573     2       0          1  0  1
#&gt; SRR975574     2       0          1  0  1
#&gt; SRR975575     2       0          1  0  1
#&gt; SRR975576     2       0          1  0  1
#&gt; SRR975577     2       0          1  0  1
#&gt; SRR975578     2       0          1  0  1
#&gt; SRR975579     2       0          1  0  1
#&gt; SRR975580     2       0          1  0  1
#&gt; SRR975581     2       0          1  0  1
#&gt; SRR975582     2       0          1  0  1
#&gt; SRR975583     2       0          1  0  1
#&gt; SRR975584     2       0          1  0  1
#&gt; SRR975585     2       0          1  0  1
#&gt; SRR975586     2       0          1  0  1
#&gt; SRR975587     1       0          1  1  0
#&gt; SRR975588     2       0          1  0  1
#&gt; SRR975589     1       0          1  1  0
#&gt; SRR975590     1       0          1  1  0
#&gt; SRR975591     1       0          1  1  0
#&gt; SRR975592     1       0          1  1  0
#&gt; SRR975593     1       0          1  1  0
#&gt; SRR975594     2       0          1  0  1
#&gt; SRR975595     1       0          1  1  0
#&gt; SRR975597     1       0          1  1  0
#&gt; SRR975596     1       0          1  1  0
#&gt; SRR975598     1       0          1  1  0
#&gt; SRR975599     2       0          1  0  1
#&gt; SRR975600     1       0          1  1  0
#&gt; SRR975601     1       0          1  1  0
#&gt; SRR975602     1       0          1  1  0
#&gt; SRR975603     1       0          1  1  0
#&gt; SRR975604     1       0          1  1  0
</code></pre>

<script>
$('#tab-ATC-kmeans-get-classes-1-a').parent().next().next().hide();
$('#tab-ATC-kmeans-get-classes-1-a').click(function(){
  $('#tab-ATC-kmeans-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-kmeans-get-classes-2'>
<p><a id='tab-ATC-kmeans-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3
#&gt; SRR975551     1  0.0000      0.947 1.000 0.000 0.000
#&gt; SRR975552     1  0.0000      0.947 1.000 0.000 0.000
#&gt; SRR975554     1  0.0000      0.947 1.000 0.000 0.000
#&gt; SRR975553     2  0.0000      0.985 0.000 1.000 0.000
#&gt; SRR975555     1  0.0000      0.947 1.000 0.000 0.000
#&gt; SRR975556     2  0.0000      0.985 0.000 1.000 0.000
#&gt; SRR975557     3  0.0424      0.959 0.000 0.008 0.992
#&gt; SRR975558     1  0.4002      0.819 0.840 0.000 0.160
#&gt; SRR975559     1  0.0000      0.947 1.000 0.000 0.000
#&gt; SRR975560     2  0.3551      0.863 0.000 0.868 0.132
#&gt; SRR975561     2  0.1529      0.955 0.000 0.960 0.040
#&gt; SRR975562     1  0.3340      0.859 0.880 0.000 0.120
#&gt; SRR975563     2  0.0000      0.985 0.000 1.000 0.000
#&gt; SRR975564     1  0.0000      0.947 1.000 0.000 0.000
#&gt; SRR975565     1  0.0000      0.947 1.000 0.000 0.000
#&gt; SRR975566     1  0.0000      0.947 1.000 0.000 0.000
#&gt; SRR975567     1  0.0424      0.942 0.992 0.000 0.008
#&gt; SRR975568     1  0.0000      0.947 1.000 0.000 0.000
#&gt; SRR975569     2  0.0000      0.985 0.000 1.000 0.000
#&gt; SRR975570     2  0.0000      0.985 0.000 1.000 0.000
#&gt; SRR975571     2  0.0000      0.985 0.000 1.000 0.000
#&gt; SRR975572     2  0.0000      0.985 0.000 1.000 0.000
#&gt; SRR975573     2  0.0000      0.985 0.000 1.000 0.000
#&gt; SRR975574     2  0.0000      0.985 0.000 1.000 0.000
#&gt; SRR975575     2  0.0000      0.985 0.000 1.000 0.000
#&gt; SRR975576     2  0.0000      0.985 0.000 1.000 0.000
#&gt; SRR975577     2  0.0000      0.985 0.000 1.000 0.000
#&gt; SRR975578     2  0.0000      0.985 0.000 1.000 0.000
#&gt; SRR975579     2  0.3879      0.841 0.000 0.848 0.152
#&gt; SRR975580     2  0.1529      0.955 0.000 0.960 0.040
#&gt; SRR975581     2  0.0000      0.985 0.000 1.000 0.000
#&gt; SRR975582     2  0.0000      0.985 0.000 1.000 0.000
#&gt; SRR975583     2  0.0000      0.985 0.000 1.000 0.000
#&gt; SRR975584     2  0.0000      0.985 0.000 1.000 0.000
#&gt; SRR975585     2  0.0000      0.985 0.000 1.000 0.000
#&gt; SRR975586     2  0.0000      0.985 0.000 1.000 0.000
#&gt; SRR975587     1  0.0000      0.947 1.000 0.000 0.000
#&gt; SRR975588     2  0.0000      0.985 0.000 1.000 0.000
#&gt; SRR975589     1  0.0000      0.947 1.000 0.000 0.000
#&gt; SRR975590     1  0.0000      0.947 1.000 0.000 0.000
#&gt; SRR975591     1  0.6008      0.475 0.628 0.000 0.372
#&gt; SRR975592     1  0.0000      0.947 1.000 0.000 0.000
#&gt; SRR975593     1  0.0000      0.947 1.000 0.000 0.000
#&gt; SRR975594     3  0.0237      0.961 0.000 0.004 0.996
#&gt; SRR975595     1  0.0000      0.947 1.000 0.000 0.000
#&gt; SRR975597     1  0.0000      0.947 1.000 0.000 0.000
#&gt; SRR975596     1  0.3340      0.859 0.880 0.000 0.120
#&gt; SRR975598     1  0.0000      0.947 1.000 0.000 0.000
#&gt; SRR975599     3  0.0000      0.960 0.000 0.000 1.000
#&gt; SRR975600     1  0.0000      0.947 1.000 0.000 0.000
#&gt; SRR975601     1  0.5988      0.483 0.632 0.000 0.368
#&gt; SRR975602     1  0.0000      0.947 1.000 0.000 0.000
#&gt; SRR975603     1  0.3340      0.859 0.880 0.000 0.120
#&gt; SRR975604     3  0.2796      0.881 0.092 0.000 0.908
</code></pre>

<script>
$('#tab-ATC-kmeans-get-classes-2-a').parent().next().next().hide();
$('#tab-ATC-kmeans-get-classes-2-a').click(function(){
  $('#tab-ATC-kmeans-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-kmeans-get-classes-3'>
<p><a id='tab-ATC-kmeans-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3    p4
#&gt; SRR975551     1  0.0188      0.948 0.996 0.000 0.000 0.004
#&gt; SRR975552     1  0.0188      0.948 0.996 0.000 0.000 0.004
#&gt; SRR975554     1  0.0188      0.948 0.996 0.000 0.000 0.004
#&gt; SRR975553     2  0.0000      0.931 0.000 1.000 0.000 0.000
#&gt; SRR975555     1  0.0188      0.947 0.996 0.000 0.004 0.000
#&gt; SRR975556     2  0.3616      0.821 0.000 0.852 0.036 0.112
#&gt; SRR975557     4  0.1398      0.723 0.000 0.004 0.040 0.956
#&gt; SRR975558     3  0.4741      0.885 0.328 0.000 0.668 0.004
#&gt; SRR975559     1  0.0524      0.944 0.988 0.000 0.008 0.004
#&gt; SRR975560     2  0.5383      0.605 0.000 0.672 0.036 0.292
#&gt; SRR975561     2  0.4621      0.651 0.000 0.708 0.008 0.284
#&gt; SRR975562     3  0.4855      0.896 0.352 0.000 0.644 0.004
#&gt; SRR975563     2  0.0000      0.931 0.000 1.000 0.000 0.000
#&gt; SRR975564     1  0.0188      0.947 0.996 0.000 0.004 0.000
#&gt; SRR975565     1  0.0188      0.948 0.996 0.000 0.000 0.004
#&gt; SRR975566     1  0.0000      0.949 1.000 0.000 0.000 0.000
#&gt; SRR975567     3  0.4713      0.893 0.360 0.000 0.640 0.000
#&gt; SRR975568     1  0.0188      0.947 0.996 0.000 0.004 0.000
#&gt; SRR975569     2  0.0000      0.931 0.000 1.000 0.000 0.000
#&gt; SRR975570     2  0.0000      0.931 0.000 1.000 0.000 0.000
#&gt; SRR975571     2  0.0000      0.931 0.000 1.000 0.000 0.000
#&gt; SRR975572     2  0.0000      0.931 0.000 1.000 0.000 0.000
#&gt; SRR975573     2  0.0000      0.931 0.000 1.000 0.000 0.000
#&gt; SRR975574     2  0.0000      0.931 0.000 1.000 0.000 0.000
#&gt; SRR975575     2  0.0000      0.931 0.000 1.000 0.000 0.000
#&gt; SRR975576     2  0.0524      0.926 0.000 0.988 0.004 0.008
#&gt; SRR975577     2  0.0524      0.926 0.000 0.988 0.004 0.008
#&gt; SRR975578     2  0.0524      0.926 0.000 0.988 0.004 0.008
#&gt; SRR975579     4  0.4193      0.460 0.000 0.268 0.000 0.732
#&gt; SRR975580     2  0.5383      0.605 0.000 0.672 0.036 0.292
#&gt; SRR975581     2  0.0524      0.926 0.000 0.988 0.004 0.008
#&gt; SRR975582     2  0.0000      0.931 0.000 1.000 0.000 0.000
#&gt; SRR975583     2  0.0000      0.931 0.000 1.000 0.000 0.000
#&gt; SRR975584     2  0.0000      0.931 0.000 1.000 0.000 0.000
#&gt; SRR975585     2  0.0000      0.931 0.000 1.000 0.000 0.000
#&gt; SRR975586     2  0.5052      0.677 0.000 0.720 0.036 0.244
#&gt; SRR975587     1  0.0000      0.949 1.000 0.000 0.000 0.000
#&gt; SRR975588     2  0.0000      0.931 0.000 1.000 0.000 0.000
#&gt; SRR975589     1  0.0817      0.924 0.976 0.000 0.024 0.000
#&gt; SRR975590     1  0.0188      0.948 0.996 0.000 0.000 0.004
#&gt; SRR975591     3  0.4836      0.890 0.320 0.000 0.672 0.008
#&gt; SRR975592     1  0.0000      0.949 1.000 0.000 0.000 0.000
#&gt; SRR975593     1  0.4994     -0.590 0.520 0.000 0.480 0.000
#&gt; SRR975594     4  0.4677      0.749 0.000 0.004 0.316 0.680
#&gt; SRR975595     1  0.0524      0.944 0.988 0.000 0.008 0.004
#&gt; SRR975597     1  0.0000      0.949 1.000 0.000 0.000 0.000
#&gt; SRR975596     3  0.4855      0.896 0.352 0.000 0.644 0.004
#&gt; SRR975598     1  0.0524      0.944 0.988 0.000 0.008 0.004
#&gt; SRR975599     4  0.4677      0.749 0.000 0.004 0.316 0.680
#&gt; SRR975600     3  0.4817      0.856 0.388 0.000 0.612 0.000
#&gt; SRR975601     3  0.4836      0.890 0.320 0.000 0.672 0.008
#&gt; SRR975602     1  0.0524      0.944 0.988 0.000 0.008 0.004
#&gt; SRR975603     3  0.4697      0.896 0.356 0.000 0.644 0.000
#&gt; SRR975604     3  0.1820      0.326 0.020 0.000 0.944 0.036
</code></pre>

<script>
$('#tab-ATC-kmeans-get-classes-3-a').parent().next().next().hide();
$('#tab-ATC-kmeans-get-classes-3-a').click(function(){
  $('#tab-ATC-kmeans-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-kmeans-get-classes-4'>
<p><a id='tab-ATC-kmeans-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3    p4    p5
#&gt; SRR975551     1  0.3039     0.7996 0.808 0.000 0.000 0.000 0.192
#&gt; SRR975552     1  0.3039     0.7996 0.808 0.000 0.000 0.000 0.192
#&gt; SRR975554     1  0.3039     0.7996 0.808 0.000 0.000 0.000 0.192
#&gt; SRR975553     2  0.0290     0.8861 0.000 0.992 0.008 0.000 0.000
#&gt; SRR975555     1  0.2233     0.8163 0.904 0.000 0.016 0.000 0.080
#&gt; SRR975556     2  0.4575     0.4695 0.000 0.736 0.040 0.012 0.212
#&gt; SRR975557     4  0.5646     0.3859 0.000 0.000 0.076 0.480 0.444
#&gt; SRR975558     3  0.4503     0.8272 0.124 0.000 0.756 0.000 0.120
#&gt; SRR975559     1  0.2818     0.7926 0.856 0.000 0.012 0.000 0.132
#&gt; SRR975560     5  0.4781     0.7583 0.000 0.428 0.000 0.020 0.552
#&gt; SRR975561     2  0.5179    -0.7076 0.000 0.496 0.012 0.020 0.472
#&gt; SRR975562     3  0.5109     0.7936 0.172 0.000 0.696 0.000 0.132
#&gt; SRR975563     2  0.0880     0.8836 0.000 0.968 0.032 0.000 0.000
#&gt; SRR975564     1  0.1872     0.8210 0.928 0.000 0.020 0.000 0.052
#&gt; SRR975565     1  0.3039     0.7996 0.808 0.000 0.000 0.000 0.192
#&gt; SRR975566     1  0.0609     0.8417 0.980 0.000 0.000 0.000 0.020
#&gt; SRR975567     3  0.4469     0.8386 0.148 0.000 0.756 0.000 0.096
#&gt; SRR975568     1  0.1800     0.8227 0.932 0.000 0.020 0.000 0.048
#&gt; SRR975569     2  0.0609     0.8840 0.000 0.980 0.020 0.000 0.000
#&gt; SRR975570     2  0.0609     0.8840 0.000 0.980 0.020 0.000 0.000
#&gt; SRR975571     2  0.0290     0.8861 0.000 0.992 0.008 0.000 0.000
#&gt; SRR975572     2  0.0609     0.8840 0.000 0.980 0.020 0.000 0.000
#&gt; SRR975573     2  0.0000     0.8867 0.000 1.000 0.000 0.000 0.000
#&gt; SRR975574     2  0.1168     0.8715 0.000 0.960 0.032 0.008 0.000
#&gt; SRR975575     2  0.0404     0.8874 0.000 0.988 0.012 0.000 0.000
#&gt; SRR975576     2  0.2584     0.8222 0.000 0.900 0.040 0.008 0.052
#&gt; SRR975577     2  0.2584     0.8222 0.000 0.900 0.040 0.008 0.052
#&gt; SRR975578     2  0.2584     0.8222 0.000 0.900 0.040 0.008 0.052
#&gt; SRR975579     5  0.7686     0.0902 0.000 0.208 0.076 0.272 0.444
#&gt; SRR975580     5  0.4781     0.7583 0.000 0.428 0.000 0.020 0.552
#&gt; SRR975581     2  0.2584     0.8222 0.000 0.900 0.040 0.008 0.052
#&gt; SRR975582     2  0.1168     0.8715 0.000 0.960 0.032 0.008 0.000
#&gt; SRR975583     2  0.0404     0.8861 0.000 0.988 0.012 0.000 0.000
#&gt; SRR975584     2  0.0000     0.8867 0.000 1.000 0.000 0.000 0.000
#&gt; SRR975585     2  0.0404     0.8861 0.000 0.988 0.012 0.000 0.000
#&gt; SRR975586     5  0.4443     0.6842 0.000 0.472 0.000 0.004 0.524
#&gt; SRR975587     1  0.1197     0.8414 0.952 0.000 0.000 0.000 0.048
#&gt; SRR975588     2  0.0609     0.8840 0.000 0.980 0.020 0.000 0.000
#&gt; SRR975589     1  0.1399     0.8306 0.952 0.000 0.020 0.000 0.028
#&gt; SRR975590     1  0.3039     0.7996 0.808 0.000 0.000 0.000 0.192
#&gt; SRR975591     3  0.2865     0.8532 0.132 0.000 0.856 0.008 0.004
#&gt; SRR975592     1  0.1965     0.8337 0.904 0.000 0.000 0.000 0.096
#&gt; SRR975593     1  0.5631    -0.2939 0.500 0.000 0.424 0.000 0.076
#&gt; SRR975594     4  0.0404     0.7701 0.000 0.000 0.012 0.988 0.000
#&gt; SRR975595     1  0.2771     0.7951 0.860 0.000 0.012 0.000 0.128
#&gt; SRR975597     1  0.0880     0.8429 0.968 0.000 0.000 0.000 0.032
#&gt; SRR975596     3  0.5109     0.7936 0.172 0.000 0.696 0.000 0.132
#&gt; SRR975598     1  0.2864     0.7962 0.852 0.000 0.012 0.000 0.136
#&gt; SRR975599     4  0.0404     0.7701 0.000 0.000 0.012 0.988 0.000
#&gt; SRR975600     3  0.5142     0.6387 0.348 0.000 0.600 0.000 0.052
#&gt; SRR975601     3  0.2865     0.8532 0.132 0.000 0.856 0.008 0.004
#&gt; SRR975602     1  0.2513     0.7967 0.876 0.000 0.008 0.000 0.116
#&gt; SRR975603     3  0.2648     0.8544 0.152 0.000 0.848 0.000 0.000
#&gt; SRR975604     3  0.3031     0.7046 0.020 0.000 0.856 0.120 0.004
</code></pre>

<script>
$('#tab-ATC-kmeans-get-classes-4-a').parent().next().next().hide();
$('#tab-ATC-kmeans-get-classes-4-a').click(function(){
  $('#tab-ATC-kmeans-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-kmeans-get-classes-5'>
<p><a id='tab-ATC-kmeans-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3    p4    p5 p6
#&gt; SRR975551     1  0.3371      0.711 0.708 0.000 0.000 0.000 0.000 NA
#&gt; SRR975552     1  0.3371      0.711 0.708 0.000 0.000 0.000 0.000 NA
#&gt; SRR975554     1  0.3489      0.712 0.708 0.000 0.000 0.004 0.000 NA
#&gt; SRR975553     2  0.0405      0.881 0.000 0.988 0.008 0.000 0.000 NA
#&gt; SRR975555     1  0.3042      0.740 0.852 0.000 0.020 0.028 0.000 NA
#&gt; SRR975556     2  0.5105     -0.115 0.000 0.488 0.000 0.432 0.000 NA
#&gt; SRR975557     4  0.6906     -0.161 0.000 0.000 0.048 0.336 0.300 NA
#&gt; SRR975558     3  0.4222      0.689 0.016 0.000 0.764 0.120 0.000 NA
#&gt; SRR975559     1  0.4339      0.690 0.736 0.000 0.004 0.140 0.000 NA
#&gt; SRR975560     4  0.3620      0.663 0.000 0.248 0.008 0.736 0.008 NA
#&gt; SRR975561     4  0.5311      0.516 0.000 0.344 0.000 0.556 0.008 NA
#&gt; SRR975562     3  0.5761      0.655 0.088 0.000 0.644 0.156 0.000 NA
#&gt; SRR975563     2  0.1757      0.865 0.000 0.916 0.000 0.008 0.000 NA
#&gt; SRR975564     1  0.2898      0.741 0.864 0.000 0.024 0.024 0.000 NA
#&gt; SRR975565     1  0.3489      0.712 0.708 0.000 0.000 0.004 0.000 NA
#&gt; SRR975566     1  0.0260      0.778 0.992 0.000 0.000 0.000 0.000 NA
#&gt; SRR975567     3  0.4468      0.737 0.076 0.000 0.764 0.060 0.000 NA
#&gt; SRR975568     1  0.2677      0.744 0.876 0.000 0.024 0.016 0.000 NA
#&gt; SRR975569     2  0.0603      0.880 0.000 0.980 0.004 0.000 0.000 NA
#&gt; SRR975570     2  0.0603      0.880 0.000 0.980 0.004 0.000 0.000 NA
#&gt; SRR975571     2  0.0405      0.881 0.000 0.988 0.008 0.000 0.000 NA
#&gt; SRR975572     2  0.0603      0.880 0.000 0.980 0.004 0.000 0.000 NA
#&gt; SRR975573     2  0.0146      0.882 0.000 0.996 0.004 0.000 0.000 NA
#&gt; SRR975574     2  0.2070      0.845 0.000 0.892 0.000 0.008 0.000 NA
#&gt; SRR975575     2  0.0865      0.880 0.000 0.964 0.000 0.000 0.000 NA
#&gt; SRR975576     2  0.3586      0.769 0.000 0.796 0.000 0.080 0.000 NA
#&gt; SRR975577     2  0.3586      0.769 0.000 0.796 0.000 0.080 0.000 NA
#&gt; SRR975578     2  0.3586      0.769 0.000 0.796 0.000 0.080 0.000 NA
#&gt; SRR975579     4  0.7943      0.221 0.000 0.120 0.048 0.344 0.156 NA
#&gt; SRR975580     4  0.3620      0.663 0.000 0.248 0.008 0.736 0.008 NA
#&gt; SRR975581     2  0.3586      0.769 0.000 0.796 0.000 0.080 0.000 NA
#&gt; SRR975582     2  0.1806      0.854 0.000 0.908 0.000 0.004 0.000 NA
#&gt; SRR975583     2  0.0363      0.882 0.000 0.988 0.000 0.000 0.000 NA
#&gt; SRR975584     2  0.0146      0.882 0.000 0.996 0.004 0.000 0.000 NA
#&gt; SRR975585     2  0.0363      0.882 0.000 0.988 0.000 0.000 0.000 NA
#&gt; SRR975586     4  0.3351      0.658 0.000 0.288 0.000 0.712 0.000 NA
#&gt; SRR975587     1  0.1285      0.779 0.944 0.000 0.000 0.004 0.000 NA
#&gt; SRR975588     2  0.0603      0.880 0.000 0.980 0.004 0.000 0.000 NA
#&gt; SRR975589     1  0.2249      0.753 0.900 0.000 0.032 0.004 0.000 NA
#&gt; SRR975590     1  0.3489      0.712 0.708 0.000 0.000 0.004 0.000 NA
#&gt; SRR975591     3  0.1471      0.785 0.064 0.000 0.932 0.000 0.004 NA
#&gt; SRR975592     1  0.2053      0.772 0.888 0.000 0.000 0.004 0.000 NA
#&gt; SRR975593     1  0.5841     -0.039 0.516 0.000 0.364 0.056 0.000 NA
#&gt; SRR975594     5  0.0458      0.998 0.000 0.000 0.016 0.000 0.984 NA
#&gt; SRR975595     1  0.4339      0.690 0.736 0.000 0.004 0.140 0.000 NA
#&gt; SRR975597     1  0.1297      0.781 0.948 0.000 0.000 0.012 0.000 NA
#&gt; SRR975596     3  0.5761      0.655 0.088 0.000 0.644 0.156 0.000 NA
#&gt; SRR975598     1  0.4563      0.687 0.712 0.000 0.004 0.152 0.000 NA
#&gt; SRR975599     5  0.0603      0.998 0.000 0.000 0.016 0.000 0.980 NA
#&gt; SRR975600     3  0.5652      0.393 0.372 0.000 0.516 0.024 0.000 NA
#&gt; SRR975601     3  0.1615      0.785 0.064 0.000 0.928 0.000 0.004 NA
#&gt; SRR975602     1  0.3660      0.705 0.800 0.000 0.004 0.096 0.000 NA
#&gt; SRR975603     3  0.1556      0.785 0.080 0.000 0.920 0.000 0.000 NA
#&gt; SRR975604     3  0.2187      0.725 0.004 0.000 0.908 0.012 0.064 NA
</code></pre>

<script>
$('#tab-ATC-kmeans-get-classes-5-a').parent().next().next().hide();
$('#tab-ATC-kmeans-get-classes-5-a').click(function(){
  $('#tab-ATC-kmeans-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-ATC-kmeans-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-ATC-kmeans-consensus-heatmap'>
<ul>
<li><a href='#tab-ATC-kmeans-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-ATC-kmeans-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-ATC-kmeans-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-ATC-kmeans-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-ATC-kmeans-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-kmeans-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-consensus-heatmap-1-1.png" alt="plot of chunk tab-ATC-kmeans-consensus-heatmap-1"/></p>

</div>
<div id='tab-ATC-kmeans-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-consensus-heatmap-2-1.png" alt="plot of chunk tab-ATC-kmeans-consensus-heatmap-2"/></p>

</div>
<div id='tab-ATC-kmeans-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-consensus-heatmap-3-1.png" alt="plot of chunk tab-ATC-kmeans-consensus-heatmap-3"/></p>

</div>
<div id='tab-ATC-kmeans-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-consensus-heatmap-4-1.png" alt="plot of chunk tab-ATC-kmeans-consensus-heatmap-4"/></p>

</div>
<div id='tab-ATC-kmeans-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-consensus-heatmap-5-1.png" alt="plot of chunk tab-ATC-kmeans-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-ATC-kmeans-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-ATC-kmeans-membership-heatmap'>
<ul>
<li><a href='#tab-ATC-kmeans-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-ATC-kmeans-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-ATC-kmeans-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-ATC-kmeans-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-ATC-kmeans-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-kmeans-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-membership-heatmap-1-1.png" alt="plot of chunk tab-ATC-kmeans-membership-heatmap-1"/></p>

</div>
<div id='tab-ATC-kmeans-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-membership-heatmap-2-1.png" alt="plot of chunk tab-ATC-kmeans-membership-heatmap-2"/></p>

</div>
<div id='tab-ATC-kmeans-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-membership-heatmap-3-1.png" alt="plot of chunk tab-ATC-kmeans-membership-heatmap-3"/></p>

</div>
<div id='tab-ATC-kmeans-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-membership-heatmap-4-1.png" alt="plot of chunk tab-ATC-kmeans-membership-heatmap-4"/></p>

</div>
<div id='tab-ATC-kmeans-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-membership-heatmap-5-1.png" alt="plot of chunk tab-ATC-kmeans-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-ATC-kmeans-get-signatures' ).tabs();
} );
</script>
<div id='tabs-ATC-kmeans-get-signatures'>
<ul>
<li><a href='#tab-ATC-kmeans-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-ATC-kmeans-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-ATC-kmeans-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-ATC-kmeans-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-ATC-kmeans-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-kmeans-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-get-signatures-1-1.png" alt="plot of chunk tab-ATC-kmeans-get-signatures-1"/></p>

</div>
<div id='tab-ATC-kmeans-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-get-signatures-2-1.png" alt="plot of chunk tab-ATC-kmeans-get-signatures-2"/></p>

</div>
<div id='tab-ATC-kmeans-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-get-signatures-3-1.png" alt="plot of chunk tab-ATC-kmeans-get-signatures-3"/></p>

</div>
<div id='tab-ATC-kmeans-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-get-signatures-4-1.png" alt="plot of chunk tab-ATC-kmeans-get-signatures-4"/></p>

</div>
<div id='tab-ATC-kmeans-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-get-signatures-5-1.png" alt="plot of chunk tab-ATC-kmeans-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-ATC-kmeans-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-ATC-kmeans-get-signatures-no-scale'>
<ul>
<li><a href='#tab-ATC-kmeans-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-ATC-kmeans-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-ATC-kmeans-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-ATC-kmeans-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-ATC-kmeans-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-kmeans-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-ATC-kmeans-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-ATC-kmeans-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-ATC-kmeans-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-ATC-kmeans-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-ATC-kmeans-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-ATC-kmeans-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-ATC-kmeans-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-ATC-kmeans-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-ATC-kmeans-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk ATC-kmeans-signature_compare](figure_cola/ATC-kmeans-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-ATC-kmeans-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-ATC-kmeans-dimension-reduction'>
<ul>
<li><a href='#tab-ATC-kmeans-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-ATC-kmeans-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-ATC-kmeans-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-ATC-kmeans-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-ATC-kmeans-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-kmeans-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-dimension-reduction-1-1.png" alt="plot of chunk tab-ATC-kmeans-dimension-reduction-1"/></p>

</div>
<div id='tab-ATC-kmeans-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-dimension-reduction-2-1.png" alt="plot of chunk tab-ATC-kmeans-dimension-reduction-2"/></p>

</div>
<div id='tab-ATC-kmeans-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-dimension-reduction-3-1.png" alt="plot of chunk tab-ATC-kmeans-dimension-reduction-3"/></p>

</div>
<div id='tab-ATC-kmeans-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-dimension-reduction-4-1.png" alt="plot of chunk tab-ATC-kmeans-dimension-reduction-4"/></p>

</div>
<div id='tab-ATC-kmeans-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-dimension-reduction-5-1.png" alt="plot of chunk tab-ATC-kmeans-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk ATC-kmeans-collect-classes](figure_cola/ATC-kmeans-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### ATC:skmeans**






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["ATC", "skmeans"]
# you can also extract it by
# res = res_list["ATC:skmeans"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 17171 rows and 54 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'ATC' method.
#>   Subgroups are detected by 'skmeans' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 3.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk ATC-skmeans-collect-plots](figure_cola/ATC-skmeans-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk ATC-skmeans-select-partition-number](figure_cola/ATC-skmeans-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 1.000           1.000       1.000         0.5099 0.491   0.491
#> 3 3 1.000           0.958       0.983         0.1546 0.929   0.857
#> 4 4 0.898           0.845       0.929         0.1279 0.886   0.736
#> 5 5 0.858           0.850       0.897         0.0507 0.939   0.815
#> 6 6 0.889           0.865       0.932         0.0427 0.992   0.970
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 3
#> attr(,"optional")
#> [1] 2
```

There is also optional best $k$ = 2 that is worth to check.

Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-ATC-skmeans-get-classes' ).tabs();
} );
</script>
<div id='tabs-ATC-skmeans-get-classes'>
<ul>
<li><a href='#tab-ATC-skmeans-get-classes-1'>k = 2</a></li>
<li><a href='#tab-ATC-skmeans-get-classes-2'>k = 3</a></li>
<li><a href='#tab-ATC-skmeans-get-classes-3'>k = 4</a></li>
<li><a href='#tab-ATC-skmeans-get-classes-4'>k = 5</a></li>
<li><a href='#tab-ATC-skmeans-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-ATC-skmeans-get-classes-1'>
<p><a id='tab-ATC-skmeans-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;           class entropy silhouette p1 p2
#&gt; SRR975551     1       0          1  1  0
#&gt; SRR975552     1       0          1  1  0
#&gt; SRR975554     1       0          1  1  0
#&gt; SRR975553     2       0          1  0  1
#&gt; SRR975555     1       0          1  1  0
#&gt; SRR975556     2       0          1  0  1
#&gt; SRR975557     2       0          1  0  1
#&gt; SRR975558     1       0          1  1  0
#&gt; SRR975559     1       0          1  1  0
#&gt; SRR975560     2       0          1  0  1
#&gt; SRR975561     2       0          1  0  1
#&gt; SRR975562     1       0          1  1  0
#&gt; SRR975563     2       0          1  0  1
#&gt; SRR975564     1       0          1  1  0
#&gt; SRR975565     1       0          1  1  0
#&gt; SRR975566     1       0          1  1  0
#&gt; SRR975567     1       0          1  1  0
#&gt; SRR975568     1       0          1  1  0
#&gt; SRR975569     2       0          1  0  1
#&gt; SRR975570     2       0          1  0  1
#&gt; SRR975571     2       0          1  0  1
#&gt; SRR975572     2       0          1  0  1
#&gt; SRR975573     2       0          1  0  1
#&gt; SRR975574     2       0          1  0  1
#&gt; SRR975575     2       0          1  0  1
#&gt; SRR975576     2       0          1  0  1
#&gt; SRR975577     2       0          1  0  1
#&gt; SRR975578     2       0          1  0  1
#&gt; SRR975579     2       0          1  0  1
#&gt; SRR975580     2       0          1  0  1
#&gt; SRR975581     2       0          1  0  1
#&gt; SRR975582     2       0          1  0  1
#&gt; SRR975583     2       0          1  0  1
#&gt; SRR975584     2       0          1  0  1
#&gt; SRR975585     2       0          1  0  1
#&gt; SRR975586     2       0          1  0  1
#&gt; SRR975587     1       0          1  1  0
#&gt; SRR975588     2       0          1  0  1
#&gt; SRR975589     1       0          1  1  0
#&gt; SRR975590     1       0          1  1  0
#&gt; SRR975591     1       0          1  1  0
#&gt; SRR975592     1       0          1  1  0
#&gt; SRR975593     1       0          1  1  0
#&gt; SRR975594     2       0          1  0  1
#&gt; SRR975595     1       0          1  1  0
#&gt; SRR975597     1       0          1  1  0
#&gt; SRR975596     1       0          1  1  0
#&gt; SRR975598     1       0          1  1  0
#&gt; SRR975599     2       0          1  0  1
#&gt; SRR975600     1       0          1  1  0
#&gt; SRR975601     1       0          1  1  0
#&gt; SRR975602     1       0          1  1  0
#&gt; SRR975603     1       0          1  1  0
#&gt; SRR975604     1       0          1  1  0
</code></pre>

<script>
$('#tab-ATC-skmeans-get-classes-1-a').parent().next().next().hide();
$('#tab-ATC-skmeans-get-classes-1-a').click(function(){
  $('#tab-ATC-skmeans-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-skmeans-get-classes-2'>
<p><a id='tab-ATC-skmeans-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3
#&gt; SRR975551     1  0.0000      0.963 1.000 0.000 0.000
#&gt; SRR975552     1  0.0000      0.963 1.000 0.000 0.000
#&gt; SRR975554     1  0.0000      0.963 1.000 0.000 0.000
#&gt; SRR975553     2  0.0000      0.999 0.000 1.000 0.000
#&gt; SRR975555     1  0.0000      0.963 1.000 0.000 0.000
#&gt; SRR975556     2  0.0000      0.999 0.000 1.000 0.000
#&gt; SRR975557     3  0.0000      0.997 0.000 0.000 1.000
#&gt; SRR975558     1  0.0000      0.963 1.000 0.000 0.000
#&gt; SRR975559     1  0.0000      0.963 1.000 0.000 0.000
#&gt; SRR975560     2  0.0424      0.993 0.000 0.992 0.008
#&gt; SRR975561     2  0.0424      0.993 0.000 0.992 0.008
#&gt; SRR975562     1  0.0000      0.963 1.000 0.000 0.000
#&gt; SRR975563     2  0.0000      0.999 0.000 1.000 0.000
#&gt; SRR975564     1  0.0000      0.963 1.000 0.000 0.000
#&gt; SRR975565     1  0.0000      0.963 1.000 0.000 0.000
#&gt; SRR975566     1  0.0000      0.963 1.000 0.000 0.000
#&gt; SRR975567     1  0.0000      0.963 1.000 0.000 0.000
#&gt; SRR975568     1  0.0000      0.963 1.000 0.000 0.000
#&gt; SRR975569     2  0.0000      0.999 0.000 1.000 0.000
#&gt; SRR975570     2  0.0000      0.999 0.000 1.000 0.000
#&gt; SRR975571     2  0.0000      0.999 0.000 1.000 0.000
#&gt; SRR975572     2  0.0000      0.999 0.000 1.000 0.000
#&gt; SRR975573     2  0.0000      0.999 0.000 1.000 0.000
#&gt; SRR975574     2  0.0000      0.999 0.000 1.000 0.000
#&gt; SRR975575     2  0.0000      0.999 0.000 1.000 0.000
#&gt; SRR975576     2  0.0000      0.999 0.000 1.000 0.000
#&gt; SRR975577     2  0.0000      0.999 0.000 1.000 0.000
#&gt; SRR975578     2  0.0000      0.999 0.000 1.000 0.000
#&gt; SRR975579     2  0.0424      0.993 0.000 0.992 0.008
#&gt; SRR975580     2  0.0424      0.993 0.000 0.992 0.008
#&gt; SRR975581     2  0.0000      0.999 0.000 1.000 0.000
#&gt; SRR975582     2  0.0000      0.999 0.000 1.000 0.000
#&gt; SRR975583     2  0.0000      0.999 0.000 1.000 0.000
#&gt; SRR975584     2  0.0000      0.999 0.000 1.000 0.000
#&gt; SRR975585     2  0.0000      0.999 0.000 1.000 0.000
#&gt; SRR975586     2  0.0000      0.999 0.000 1.000 0.000
#&gt; SRR975587     1  0.0000      0.963 1.000 0.000 0.000
#&gt; SRR975588     2  0.0000      0.999 0.000 1.000 0.000
#&gt; SRR975589     1  0.0000      0.963 1.000 0.000 0.000
#&gt; SRR975590     1  0.0000      0.963 1.000 0.000 0.000
#&gt; SRR975591     1  0.6095      0.395 0.608 0.000 0.392
#&gt; SRR975592     1  0.0000      0.963 1.000 0.000 0.000
#&gt; SRR975593     1  0.0000      0.963 1.000 0.000 0.000
#&gt; SRR975594     3  0.0000      0.997 0.000 0.000 1.000
#&gt; SRR975595     1  0.0000      0.963 1.000 0.000 0.000
#&gt; SRR975597     1  0.0000      0.963 1.000 0.000 0.000
#&gt; SRR975596     1  0.0000      0.963 1.000 0.000 0.000
#&gt; SRR975598     1  0.0000      0.963 1.000 0.000 0.000
#&gt; SRR975599     3  0.0000      0.997 0.000 0.000 1.000
#&gt; SRR975600     1  0.0000      0.963 1.000 0.000 0.000
#&gt; SRR975601     1  0.6095      0.395 0.608 0.000 0.392
#&gt; SRR975602     1  0.0000      0.963 1.000 0.000 0.000
#&gt; SRR975603     1  0.3267      0.850 0.884 0.000 0.116
#&gt; SRR975604     3  0.0424      0.991 0.008 0.000 0.992
</code></pre>

<script>
$('#tab-ATC-skmeans-get-classes-2-a').parent().next().next().hide();
$('#tab-ATC-skmeans-get-classes-2-a').click(function(){
  $('#tab-ATC-skmeans-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-skmeans-get-classes-3'>
<p><a id='tab-ATC-skmeans-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3    p4
#&gt; SRR975551     1  0.0000      0.988 1.000 0.000 0.000 0.000
#&gt; SRR975552     1  0.0000      0.988 1.000 0.000 0.000 0.000
#&gt; SRR975554     1  0.0000      0.988 1.000 0.000 0.000 0.000
#&gt; SRR975553     2  0.0000      0.941 0.000 1.000 0.000 0.000
#&gt; SRR975555     1  0.0000      0.988 1.000 0.000 0.000 0.000
#&gt; SRR975556     2  0.0000      0.941 0.000 1.000 0.000 0.000
#&gt; SRR975557     4  0.1118      0.529 0.000 0.000 0.036 0.964
#&gt; SRR975558     1  0.2402      0.892 0.912 0.000 0.076 0.012
#&gt; SRR975559     1  0.0000      0.988 1.000 0.000 0.000 0.000
#&gt; SRR975560     4  0.4955      0.106 0.000 0.444 0.000 0.556
#&gt; SRR975561     2  0.4746      0.361 0.000 0.632 0.000 0.368
#&gt; SRR975562     3  0.4817      0.634 0.388 0.000 0.612 0.000
#&gt; SRR975563     2  0.0000      0.941 0.000 1.000 0.000 0.000
#&gt; SRR975564     1  0.0000      0.988 1.000 0.000 0.000 0.000
#&gt; SRR975565     1  0.0000      0.988 1.000 0.000 0.000 0.000
#&gt; SRR975566     1  0.0000      0.988 1.000 0.000 0.000 0.000
#&gt; SRR975567     1  0.2402      0.892 0.912 0.000 0.076 0.012
#&gt; SRR975568     1  0.0000      0.988 1.000 0.000 0.000 0.000
#&gt; SRR975569     2  0.0000      0.941 0.000 1.000 0.000 0.000
#&gt; SRR975570     2  0.0000      0.941 0.000 1.000 0.000 0.000
#&gt; SRR975571     2  0.0000      0.941 0.000 1.000 0.000 0.000
#&gt; SRR975572     2  0.0000      0.941 0.000 1.000 0.000 0.000
#&gt; SRR975573     2  0.0000      0.941 0.000 1.000 0.000 0.000
#&gt; SRR975574     2  0.0000      0.941 0.000 1.000 0.000 0.000
#&gt; SRR975575     2  0.0000      0.941 0.000 1.000 0.000 0.000
#&gt; SRR975576     2  0.0000      0.941 0.000 1.000 0.000 0.000
#&gt; SRR975577     2  0.0000      0.941 0.000 1.000 0.000 0.000
#&gt; SRR975578     2  0.0188      0.937 0.000 0.996 0.000 0.004
#&gt; SRR975579     4  0.4103      0.526 0.000 0.256 0.000 0.744
#&gt; SRR975580     2  0.4817      0.311 0.000 0.612 0.000 0.388
#&gt; SRR975581     2  0.0000      0.941 0.000 1.000 0.000 0.000
#&gt; SRR975582     2  0.0000      0.941 0.000 1.000 0.000 0.000
#&gt; SRR975583     2  0.0000      0.941 0.000 1.000 0.000 0.000
#&gt; SRR975584     2  0.0000      0.941 0.000 1.000 0.000 0.000
#&gt; SRR975585     2  0.0000      0.941 0.000 1.000 0.000 0.000
#&gt; SRR975586     2  0.4193      0.588 0.000 0.732 0.000 0.268
#&gt; SRR975587     1  0.0000      0.988 1.000 0.000 0.000 0.000
#&gt; SRR975588     2  0.0000      0.941 0.000 1.000 0.000 0.000
#&gt; SRR975589     1  0.0188      0.985 0.996 0.000 0.004 0.000
#&gt; SRR975590     1  0.0000      0.988 1.000 0.000 0.000 0.000
#&gt; SRR975591     3  0.2216      0.679 0.092 0.000 0.908 0.000
#&gt; SRR975592     1  0.0000      0.988 1.000 0.000 0.000 0.000
#&gt; SRR975593     1  0.0188      0.985 0.996 0.000 0.004 0.000
#&gt; SRR975594     4  0.4356      0.460 0.000 0.000 0.292 0.708
#&gt; SRR975595     1  0.0000      0.988 1.000 0.000 0.000 0.000
#&gt; SRR975597     1  0.0000      0.988 1.000 0.000 0.000 0.000
#&gt; SRR975596     3  0.4817      0.634 0.388 0.000 0.612 0.000
#&gt; SRR975598     1  0.0000      0.988 1.000 0.000 0.000 0.000
#&gt; SRR975599     4  0.4356      0.460 0.000 0.000 0.292 0.708
#&gt; SRR975600     1  0.0592      0.973 0.984 0.000 0.016 0.000
#&gt; SRR975601     3  0.2281      0.681 0.096 0.000 0.904 0.000
#&gt; SRR975602     1  0.0000      0.988 1.000 0.000 0.000 0.000
#&gt; SRR975603     3  0.3975      0.708 0.240 0.000 0.760 0.000
#&gt; SRR975604     3  0.1978      0.525 0.004 0.000 0.928 0.068
</code></pre>

<script>
$('#tab-ATC-skmeans-get-classes-3-a').parent().next().next().hide();
$('#tab-ATC-skmeans-get-classes-3-a').click(function(){
  $('#tab-ATC-skmeans-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-skmeans-get-classes-4'>
<p><a id='tab-ATC-skmeans-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3    p4    p5
#&gt; SRR975551     1  0.0162      0.977 0.996 0.000 0.000 0.000 0.004
#&gt; SRR975552     1  0.0162      0.977 0.996 0.000 0.000 0.000 0.004
#&gt; SRR975554     1  0.0162      0.977 0.996 0.000 0.000 0.000 0.004
#&gt; SRR975553     2  0.0000      0.974 0.000 1.000 0.000 0.000 0.000
#&gt; SRR975555     1  0.0290      0.976 0.992 0.000 0.000 0.000 0.008
#&gt; SRR975556     2  0.0609      0.954 0.000 0.980 0.000 0.020 0.000
#&gt; SRR975557     4  0.5448      0.422 0.000 0.000 0.076 0.584 0.340
#&gt; SRR975558     5  0.4060      0.992 0.360 0.000 0.000 0.000 0.640
#&gt; SRR975559     1  0.0510      0.969 0.984 0.000 0.000 0.000 0.016
#&gt; SRR975560     4  0.3561      0.499 0.000 0.260 0.000 0.740 0.000
#&gt; SRR975561     2  0.3999      0.325 0.000 0.656 0.000 0.344 0.000
#&gt; SRR975562     3  0.4384      0.566 0.324 0.000 0.660 0.000 0.016
#&gt; SRR975563     2  0.0000      0.974 0.000 1.000 0.000 0.000 0.000
#&gt; SRR975564     1  0.0162      0.976 0.996 0.000 0.000 0.000 0.004
#&gt; SRR975565     1  0.0162      0.977 0.996 0.000 0.000 0.000 0.004
#&gt; SRR975566     1  0.0000      0.977 1.000 0.000 0.000 0.000 0.000
#&gt; SRR975567     5  0.4074      0.992 0.364 0.000 0.000 0.000 0.636
#&gt; SRR975568     1  0.0162      0.977 0.996 0.000 0.000 0.000 0.004
#&gt; SRR975569     2  0.0000      0.974 0.000 1.000 0.000 0.000 0.000
#&gt; SRR975570     2  0.0000      0.974 0.000 1.000 0.000 0.000 0.000
#&gt; SRR975571     2  0.0000      0.974 0.000 1.000 0.000 0.000 0.000
#&gt; SRR975572     2  0.0000      0.974 0.000 1.000 0.000 0.000 0.000
#&gt; SRR975573     2  0.0000      0.974 0.000 1.000 0.000 0.000 0.000
#&gt; SRR975574     2  0.0000      0.974 0.000 1.000 0.000 0.000 0.000
#&gt; SRR975575     2  0.0000      0.974 0.000 1.000 0.000 0.000 0.000
#&gt; SRR975576     2  0.0000      0.974 0.000 1.000 0.000 0.000 0.000
#&gt; SRR975577     2  0.0000      0.974 0.000 1.000 0.000 0.000 0.000
#&gt; SRR975578     2  0.0880      0.941 0.000 0.968 0.000 0.032 0.000
#&gt; SRR975579     4  0.6564      0.508 0.000 0.236 0.000 0.468 0.296
#&gt; SRR975580     4  0.3966      0.452 0.000 0.336 0.000 0.664 0.000
#&gt; SRR975581     2  0.0000      0.974 0.000 1.000 0.000 0.000 0.000
#&gt; SRR975582     2  0.0000      0.974 0.000 1.000 0.000 0.000 0.000
#&gt; SRR975583     2  0.0000      0.974 0.000 1.000 0.000 0.000 0.000
#&gt; SRR975584     2  0.0000      0.974 0.000 1.000 0.000 0.000 0.000
#&gt; SRR975585     2  0.0000      0.974 0.000 1.000 0.000 0.000 0.000
#&gt; SRR975586     4  0.4262      0.232 0.000 0.440 0.000 0.560 0.000
#&gt; SRR975587     1  0.0404      0.970 0.988 0.000 0.012 0.000 0.000
#&gt; SRR975588     2  0.0000      0.974 0.000 1.000 0.000 0.000 0.000
#&gt; SRR975589     1  0.0794      0.948 0.972 0.000 0.000 0.000 0.028
#&gt; SRR975590     1  0.0162      0.977 0.996 0.000 0.000 0.000 0.004
#&gt; SRR975591     3  0.2260      0.748 0.064 0.000 0.908 0.000 0.028
#&gt; SRR975592     1  0.0000      0.977 1.000 0.000 0.000 0.000 0.000
#&gt; SRR975593     1  0.0955      0.946 0.968 0.000 0.028 0.000 0.004
#&gt; SRR975594     4  0.6691      0.343 0.000 0.000 0.260 0.428 0.312
#&gt; SRR975595     1  0.0510      0.969 0.984 0.000 0.000 0.000 0.016
#&gt; SRR975597     1  0.0000      0.977 1.000 0.000 0.000 0.000 0.000
#&gt; SRR975596     3  0.4384      0.566 0.324 0.000 0.660 0.000 0.016
#&gt; SRR975598     1  0.0510      0.969 0.984 0.000 0.000 0.000 0.016
#&gt; SRR975599     4  0.6691      0.343 0.000 0.000 0.260 0.428 0.312
#&gt; SRR975600     1  0.2193      0.851 0.912 0.000 0.060 0.000 0.028
#&gt; SRR975601     3  0.1502      0.743 0.056 0.000 0.940 0.000 0.004
#&gt; SRR975602     1  0.0566      0.970 0.984 0.000 0.004 0.000 0.012
#&gt; SRR975603     3  0.3452      0.731 0.148 0.000 0.820 0.000 0.032
#&gt; SRR975604     3  0.0290      0.657 0.000 0.000 0.992 0.000 0.008
</code></pre>

<script>
$('#tab-ATC-skmeans-get-classes-4-a').parent().next().next().hide();
$('#tab-ATC-skmeans-get-classes-4-a').click(function(){
  $('#tab-ATC-skmeans-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-skmeans-get-classes-5'>
<p><a id='tab-ATC-skmeans-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3    p4    p5    p6
#&gt; SRR975551     1  0.0146      0.964 0.996 0.000 0.000 0.004 0.000 0.000
#&gt; SRR975552     1  0.0260      0.964 0.992 0.000 0.000 0.008 0.000 0.000
#&gt; SRR975554     1  0.0146      0.964 0.996 0.000 0.000 0.004 0.000 0.000
#&gt; SRR975553     2  0.0000      0.960 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR975555     1  0.0547      0.963 0.980 0.000 0.000 0.020 0.000 0.000
#&gt; SRR975556     2  0.1908      0.876 0.000 0.900 0.000 0.004 0.000 0.096
#&gt; SRR975557     5  0.1411      0.649 0.000 0.000 0.004 0.000 0.936 0.060
#&gt; SRR975558     4  0.1663      0.956 0.088 0.000 0.000 0.912 0.000 0.000
#&gt; SRR975559     1  0.1936      0.934 0.928 0.000 0.028 0.028 0.008 0.008
#&gt; SRR975560     6  0.0820      0.760 0.000 0.012 0.000 0.000 0.016 0.972
#&gt; SRR975561     2  0.4187      0.367 0.000 0.624 0.000 0.004 0.016 0.356
#&gt; SRR975562     3  0.5107      0.564 0.288 0.000 0.636 0.044 0.012 0.020
#&gt; SRR975563     2  0.0000      0.960 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR975564     1  0.0692      0.959 0.976 0.000 0.004 0.020 0.000 0.000
#&gt; SRR975565     1  0.0146      0.964 0.996 0.000 0.000 0.004 0.000 0.000
#&gt; SRR975566     1  0.0458      0.962 0.984 0.000 0.016 0.000 0.000 0.000
#&gt; SRR975567     4  0.1957      0.956 0.112 0.000 0.000 0.888 0.000 0.000
#&gt; SRR975568     1  0.0363      0.963 0.988 0.000 0.000 0.012 0.000 0.000
#&gt; SRR975569     2  0.0000      0.960 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR975570     2  0.0000      0.960 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR975571     2  0.0000      0.960 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR975572     2  0.0000      0.960 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR975573     2  0.0000      0.960 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR975574     2  0.0146      0.958 0.000 0.996 0.000 0.004 0.000 0.000
#&gt; SRR975575     2  0.0000      0.960 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR975576     2  0.1010      0.933 0.000 0.960 0.000 0.004 0.000 0.036
#&gt; SRR975577     2  0.0508      0.951 0.000 0.984 0.000 0.004 0.000 0.012
#&gt; SRR975578     2  0.2442      0.818 0.000 0.852 0.000 0.004 0.000 0.144
#&gt; SRR975579     5  0.4836      0.328 0.000 0.196 0.000 0.000 0.664 0.140
#&gt; SRR975580     6  0.0806      0.770 0.000 0.020 0.000 0.000 0.008 0.972
#&gt; SRR975581     2  0.0508      0.951 0.000 0.984 0.000 0.004 0.000 0.012
#&gt; SRR975582     2  0.0000      0.960 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR975583     2  0.0000      0.960 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR975584     2  0.0000      0.960 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR975585     2  0.0000      0.960 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR975586     6  0.3052      0.574 0.000 0.216 0.000 0.004 0.000 0.780
#&gt; SRR975587     1  0.0790      0.958 0.968 0.000 0.032 0.000 0.000 0.000
#&gt; SRR975588     2  0.0000      0.960 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR975589     1  0.0993      0.955 0.964 0.000 0.024 0.012 0.000 0.000
#&gt; SRR975590     1  0.0146      0.964 0.996 0.000 0.000 0.004 0.000 0.000
#&gt; SRR975591     3  0.1313      0.717 0.028 0.000 0.952 0.016 0.004 0.000
#&gt; SRR975592     1  0.0458      0.962 0.984 0.000 0.016 0.000 0.000 0.000
#&gt; SRR975593     1  0.1615      0.930 0.928 0.000 0.064 0.004 0.000 0.004
#&gt; SRR975594     5  0.4147      0.703 0.000 0.000 0.136 0.044 0.776 0.044
#&gt; SRR975595     1  0.1590      0.942 0.944 0.000 0.012 0.028 0.008 0.008
#&gt; SRR975597     1  0.0260      0.964 0.992 0.000 0.000 0.008 0.000 0.000
#&gt; SRR975596     3  0.5089      0.569 0.284 0.000 0.640 0.044 0.012 0.020
#&gt; SRR975598     1  0.2202      0.921 0.916 0.000 0.016 0.040 0.012 0.016
#&gt; SRR975599     5  0.4147      0.703 0.000 0.000 0.136 0.044 0.776 0.044
#&gt; SRR975600     1  0.2487      0.862 0.876 0.000 0.092 0.032 0.000 0.000
#&gt; SRR975601     3  0.1552      0.700 0.020 0.000 0.940 0.004 0.036 0.000
#&gt; SRR975602     1  0.1503      0.945 0.944 0.000 0.016 0.032 0.008 0.000
#&gt; SRR975603     3  0.2492      0.710 0.100 0.000 0.876 0.020 0.000 0.004
#&gt; SRR975604     3  0.1297      0.662 0.000 0.000 0.948 0.012 0.040 0.000
</code></pre>

<script>
$('#tab-ATC-skmeans-get-classes-5-a').parent().next().next().hide();
$('#tab-ATC-skmeans-get-classes-5-a').click(function(){
  $('#tab-ATC-skmeans-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-ATC-skmeans-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-ATC-skmeans-consensus-heatmap'>
<ul>
<li><a href='#tab-ATC-skmeans-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-ATC-skmeans-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-ATC-skmeans-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-ATC-skmeans-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-ATC-skmeans-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-skmeans-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-consensus-heatmap-1-1.png" alt="plot of chunk tab-ATC-skmeans-consensus-heatmap-1"/></p>

</div>
<div id='tab-ATC-skmeans-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-consensus-heatmap-2-1.png" alt="plot of chunk tab-ATC-skmeans-consensus-heatmap-2"/></p>

</div>
<div id='tab-ATC-skmeans-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-consensus-heatmap-3-1.png" alt="plot of chunk tab-ATC-skmeans-consensus-heatmap-3"/></p>

</div>
<div id='tab-ATC-skmeans-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-consensus-heatmap-4-1.png" alt="plot of chunk tab-ATC-skmeans-consensus-heatmap-4"/></p>

</div>
<div id='tab-ATC-skmeans-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-consensus-heatmap-5-1.png" alt="plot of chunk tab-ATC-skmeans-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-ATC-skmeans-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-ATC-skmeans-membership-heatmap'>
<ul>
<li><a href='#tab-ATC-skmeans-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-ATC-skmeans-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-ATC-skmeans-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-ATC-skmeans-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-ATC-skmeans-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-skmeans-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-membership-heatmap-1-1.png" alt="plot of chunk tab-ATC-skmeans-membership-heatmap-1"/></p>

</div>
<div id='tab-ATC-skmeans-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-membership-heatmap-2-1.png" alt="plot of chunk tab-ATC-skmeans-membership-heatmap-2"/></p>

</div>
<div id='tab-ATC-skmeans-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-membership-heatmap-3-1.png" alt="plot of chunk tab-ATC-skmeans-membership-heatmap-3"/></p>

</div>
<div id='tab-ATC-skmeans-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-membership-heatmap-4-1.png" alt="plot of chunk tab-ATC-skmeans-membership-heatmap-4"/></p>

</div>
<div id='tab-ATC-skmeans-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-membership-heatmap-5-1.png" alt="plot of chunk tab-ATC-skmeans-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-ATC-skmeans-get-signatures' ).tabs();
} );
</script>
<div id='tabs-ATC-skmeans-get-signatures'>
<ul>
<li><a href='#tab-ATC-skmeans-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-ATC-skmeans-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-ATC-skmeans-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-ATC-skmeans-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-ATC-skmeans-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-skmeans-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-get-signatures-1-1.png" alt="plot of chunk tab-ATC-skmeans-get-signatures-1"/></p>

</div>
<div id='tab-ATC-skmeans-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-get-signatures-2-1.png" alt="plot of chunk tab-ATC-skmeans-get-signatures-2"/></p>

</div>
<div id='tab-ATC-skmeans-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-get-signatures-3-1.png" alt="plot of chunk tab-ATC-skmeans-get-signatures-3"/></p>

</div>
<div id='tab-ATC-skmeans-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-get-signatures-4-1.png" alt="plot of chunk tab-ATC-skmeans-get-signatures-4"/></p>

</div>
<div id='tab-ATC-skmeans-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-get-signatures-5-1.png" alt="plot of chunk tab-ATC-skmeans-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-ATC-skmeans-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-ATC-skmeans-get-signatures-no-scale'>
<ul>
<li><a href='#tab-ATC-skmeans-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-ATC-skmeans-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-ATC-skmeans-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-ATC-skmeans-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-ATC-skmeans-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-skmeans-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-ATC-skmeans-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-ATC-skmeans-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-ATC-skmeans-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-ATC-skmeans-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-ATC-skmeans-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-ATC-skmeans-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-ATC-skmeans-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-ATC-skmeans-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-ATC-skmeans-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk ATC-skmeans-signature_compare](figure_cola/ATC-skmeans-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-ATC-skmeans-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-ATC-skmeans-dimension-reduction'>
<ul>
<li><a href='#tab-ATC-skmeans-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-ATC-skmeans-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-ATC-skmeans-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-ATC-skmeans-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-ATC-skmeans-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-skmeans-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-dimension-reduction-1-1.png" alt="plot of chunk tab-ATC-skmeans-dimension-reduction-1"/></p>

</div>
<div id='tab-ATC-skmeans-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-dimension-reduction-2-1.png" alt="plot of chunk tab-ATC-skmeans-dimension-reduction-2"/></p>

</div>
<div id='tab-ATC-skmeans-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-dimension-reduction-3-1.png" alt="plot of chunk tab-ATC-skmeans-dimension-reduction-3"/></p>

</div>
<div id='tab-ATC-skmeans-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-dimension-reduction-4-1.png" alt="plot of chunk tab-ATC-skmeans-dimension-reduction-4"/></p>

</div>
<div id='tab-ATC-skmeans-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-dimension-reduction-5-1.png" alt="plot of chunk tab-ATC-skmeans-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk ATC-skmeans-collect-classes](figure_cola/ATC-skmeans-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### ATC:pam*






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["ATC", "pam"]
# you can also extract it by
# res = res_list["ATC:pam"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 17171 rows and 54 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'ATC' method.
#>   Subgroups are detected by 'pam' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 5.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk ATC-pam-collect-plots](figure_cola/ATC-pam-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk ATC-pam-select-partition-number](figure_cola/ATC-pam-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 1.000           1.000       1.000         0.5099 0.491   0.491
#> 3 3 0.856           0.829       0.917         0.1602 0.965   0.929
#> 4 4 0.981           0.936       0.977         0.1346 0.877   0.730
#> 5 5 0.921           0.919       0.966         0.0490 0.968   0.903
#> 6 6 0.893           0.912       0.928         0.0542 0.958   0.860
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 5
#> attr(,"optional")
#> [1] 2 4
```

There is also optional best $k$ = 2 4 that is worth to check.

Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-ATC-pam-get-classes' ).tabs();
} );
</script>
<div id='tabs-ATC-pam-get-classes'>
<ul>
<li><a href='#tab-ATC-pam-get-classes-1'>k = 2</a></li>
<li><a href='#tab-ATC-pam-get-classes-2'>k = 3</a></li>
<li><a href='#tab-ATC-pam-get-classes-3'>k = 4</a></li>
<li><a href='#tab-ATC-pam-get-classes-4'>k = 5</a></li>
<li><a href='#tab-ATC-pam-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-ATC-pam-get-classes-1'>
<p><a id='tab-ATC-pam-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;           class entropy silhouette p1 p2
#&gt; SRR975551     1       0          1  1  0
#&gt; SRR975552     1       0          1  1  0
#&gt; SRR975554     1       0          1  1  0
#&gt; SRR975553     2       0          1  0  1
#&gt; SRR975555     1       0          1  1  0
#&gt; SRR975556     2       0          1  0  1
#&gt; SRR975557     2       0          1  0  1
#&gt; SRR975558     1       0          1  1  0
#&gt; SRR975559     1       0          1  1  0
#&gt; SRR975560     2       0          1  0  1
#&gt; SRR975561     2       0          1  0  1
#&gt; SRR975562     1       0          1  1  0
#&gt; SRR975563     2       0          1  0  1
#&gt; SRR975564     1       0          1  1  0
#&gt; SRR975565     1       0          1  1  0
#&gt; SRR975566     1       0          1  1  0
#&gt; SRR975567     1       0          1  1  0
#&gt; SRR975568     1       0          1  1  0
#&gt; SRR975569     2       0          1  0  1
#&gt; SRR975570     2       0          1  0  1
#&gt; SRR975571     2       0          1  0  1
#&gt; SRR975572     2       0          1  0  1
#&gt; SRR975573     2       0          1  0  1
#&gt; SRR975574     2       0          1  0  1
#&gt; SRR975575     2       0          1  0  1
#&gt; SRR975576     2       0          1  0  1
#&gt; SRR975577     2       0          1  0  1
#&gt; SRR975578     2       0          1  0  1
#&gt; SRR975579     2       0          1  0  1
#&gt; SRR975580     2       0          1  0  1
#&gt; SRR975581     2       0          1  0  1
#&gt; SRR975582     2       0          1  0  1
#&gt; SRR975583     2       0          1  0  1
#&gt; SRR975584     2       0          1  0  1
#&gt; SRR975585     2       0          1  0  1
#&gt; SRR975586     2       0          1  0  1
#&gt; SRR975587     1       0          1  1  0
#&gt; SRR975588     2       0          1  0  1
#&gt; SRR975589     1       0          1  1  0
#&gt; SRR975590     1       0          1  1  0
#&gt; SRR975591     1       0          1  1  0
#&gt; SRR975592     1       0          1  1  0
#&gt; SRR975593     1       0          1  1  0
#&gt; SRR975594     2       0          1  0  1
#&gt; SRR975595     1       0          1  1  0
#&gt; SRR975597     1       0          1  1  0
#&gt; SRR975596     1       0          1  1  0
#&gt; SRR975598     1       0          1  1  0
#&gt; SRR975599     2       0          1  0  1
#&gt; SRR975600     1       0          1  1  0
#&gt; SRR975601     1       0          1  1  0
#&gt; SRR975602     1       0          1  1  0
#&gt; SRR975603     1       0          1  1  0
#&gt; SRR975604     1       0          1  1  0
</code></pre>

<script>
$('#tab-ATC-pam-get-classes-1-a').parent().next().next().hide();
$('#tab-ATC-pam-get-classes-1-a').click(function(){
  $('#tab-ATC-pam-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-pam-get-classes-2'>
<p><a id='tab-ATC-pam-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3
#&gt; SRR975551     1   0.000      0.810 1.000 0.000 0.000
#&gt; SRR975552     1   0.000      0.810 1.000 0.000 0.000
#&gt; SRR975554     1   0.000      0.810 1.000 0.000 0.000
#&gt; SRR975553     2   0.000      0.980 0.000 1.000 0.000
#&gt; SRR975555     1   0.000      0.810 1.000 0.000 0.000
#&gt; SRR975556     2   0.000      0.980 0.000 1.000 0.000
#&gt; SRR975557     2   0.621      0.138 0.000 0.572 0.428
#&gt; SRR975558     1   0.618      0.526 0.584 0.000 0.416
#&gt; SRR975559     1   0.000      0.810 1.000 0.000 0.000
#&gt; SRR975560     2   0.000      0.980 0.000 1.000 0.000
#&gt; SRR975561     2   0.000      0.980 0.000 1.000 0.000
#&gt; SRR975562     1   0.618      0.526 0.584 0.000 0.416
#&gt; SRR975563     2   0.000      0.980 0.000 1.000 0.000
#&gt; SRR975564     1   0.000      0.810 1.000 0.000 0.000
#&gt; SRR975565     1   0.000      0.810 1.000 0.000 0.000
#&gt; SRR975566     1   0.000      0.810 1.000 0.000 0.000
#&gt; SRR975567     1   0.618      0.526 0.584 0.000 0.416
#&gt; SRR975568     1   0.000      0.810 1.000 0.000 0.000
#&gt; SRR975569     2   0.000      0.980 0.000 1.000 0.000
#&gt; SRR975570     2   0.000      0.980 0.000 1.000 0.000
#&gt; SRR975571     2   0.000      0.980 0.000 1.000 0.000
#&gt; SRR975572     2   0.000      0.980 0.000 1.000 0.000
#&gt; SRR975573     2   0.000      0.980 0.000 1.000 0.000
#&gt; SRR975574     2   0.000      0.980 0.000 1.000 0.000
#&gt; SRR975575     2   0.000      0.980 0.000 1.000 0.000
#&gt; SRR975576     2   0.000      0.980 0.000 1.000 0.000
#&gt; SRR975577     2   0.000      0.980 0.000 1.000 0.000
#&gt; SRR975578     2   0.000      0.980 0.000 1.000 0.000
#&gt; SRR975579     2   0.000      0.980 0.000 1.000 0.000
#&gt; SRR975580     2   0.000      0.980 0.000 1.000 0.000
#&gt; SRR975581     2   0.000      0.980 0.000 1.000 0.000
#&gt; SRR975582     2   0.000      0.980 0.000 1.000 0.000
#&gt; SRR975583     2   0.000      0.980 0.000 1.000 0.000
#&gt; SRR975584     2   0.000      0.980 0.000 1.000 0.000
#&gt; SRR975585     2   0.000      0.980 0.000 1.000 0.000
#&gt; SRR975586     2   0.000      0.980 0.000 1.000 0.000
#&gt; SRR975587     1   0.000      0.810 1.000 0.000 0.000
#&gt; SRR975588     2   0.000      0.980 0.000 1.000 0.000
#&gt; SRR975589     1   0.000      0.810 1.000 0.000 0.000
#&gt; SRR975590     1   0.000      0.810 1.000 0.000 0.000
#&gt; SRR975591     1   0.618      0.526 0.584 0.000 0.416
#&gt; SRR975592     1   0.000      0.810 1.000 0.000 0.000
#&gt; SRR975593     1   0.568      0.612 0.684 0.000 0.316
#&gt; SRR975594     3   0.000      1.000 0.000 0.000 1.000
#&gt; SRR975595     1   0.000      0.810 1.000 0.000 0.000
#&gt; SRR975597     1   0.000      0.810 1.000 0.000 0.000
#&gt; SRR975596     1   0.618      0.526 0.584 0.000 0.416
#&gt; SRR975598     1   0.000      0.810 1.000 0.000 0.000
#&gt; SRR975599     3   0.000      1.000 0.000 0.000 1.000
#&gt; SRR975600     1   0.613      0.541 0.600 0.000 0.400
#&gt; SRR975601     1   0.618      0.526 0.584 0.000 0.416
#&gt; SRR975602     1   0.000      0.810 1.000 0.000 0.000
#&gt; SRR975603     1   0.618      0.526 0.584 0.000 0.416
#&gt; SRR975604     1   0.618      0.526 0.584 0.000 0.416
</code></pre>

<script>
$('#tab-ATC-pam-get-classes-2-a').parent().next().next().hide();
$('#tab-ATC-pam-get-classes-2-a').click(function(){
  $('#tab-ATC-pam-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-pam-get-classes-3'>
<p><a id='tab-ATC-pam-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3    p4
#&gt; SRR975551     1  0.0000      0.971 1.000 0.000 0.000 0.000
#&gt; SRR975552     1  0.0000      0.971 1.000 0.000 0.000 0.000
#&gt; SRR975554     1  0.0000      0.971 1.000 0.000 0.000 0.000
#&gt; SRR975553     2  0.0000      0.983 0.000 1.000 0.000 0.000
#&gt; SRR975555     1  0.0000      0.971 1.000 0.000 0.000 0.000
#&gt; SRR975556     2  0.0000      0.983 0.000 1.000 0.000 0.000
#&gt; SRR975557     2  0.6816      0.371 0.000 0.604 0.212 0.184
#&gt; SRR975558     3  0.0000      0.927 0.000 0.000 1.000 0.000
#&gt; SRR975559     1  0.0000      0.971 1.000 0.000 0.000 0.000
#&gt; SRR975560     2  0.0000      0.983 0.000 1.000 0.000 0.000
#&gt; SRR975561     2  0.0000      0.983 0.000 1.000 0.000 0.000
#&gt; SRR975562     3  0.0000      0.927 0.000 0.000 1.000 0.000
#&gt; SRR975563     2  0.0000      0.983 0.000 1.000 0.000 0.000
#&gt; SRR975564     1  0.0000      0.971 1.000 0.000 0.000 0.000
#&gt; SRR975565     1  0.0000      0.971 1.000 0.000 0.000 0.000
#&gt; SRR975566     1  0.1022      0.939 0.968 0.000 0.032 0.000
#&gt; SRR975567     3  0.0000      0.927 0.000 0.000 1.000 0.000
#&gt; SRR975568     1  0.0000      0.971 1.000 0.000 0.000 0.000
#&gt; SRR975569     2  0.0000      0.983 0.000 1.000 0.000 0.000
#&gt; SRR975570     2  0.0000      0.983 0.000 1.000 0.000 0.000
#&gt; SRR975571     2  0.0000      0.983 0.000 1.000 0.000 0.000
#&gt; SRR975572     2  0.0000      0.983 0.000 1.000 0.000 0.000
#&gt; SRR975573     2  0.0000      0.983 0.000 1.000 0.000 0.000
#&gt; SRR975574     2  0.0000      0.983 0.000 1.000 0.000 0.000
#&gt; SRR975575     2  0.0000      0.983 0.000 1.000 0.000 0.000
#&gt; SRR975576     2  0.0000      0.983 0.000 1.000 0.000 0.000
#&gt; SRR975577     2  0.0000      0.983 0.000 1.000 0.000 0.000
#&gt; SRR975578     2  0.0000      0.983 0.000 1.000 0.000 0.000
#&gt; SRR975579     2  0.0000      0.983 0.000 1.000 0.000 0.000
#&gt; SRR975580     2  0.0000      0.983 0.000 1.000 0.000 0.000
#&gt; SRR975581     2  0.0000      0.983 0.000 1.000 0.000 0.000
#&gt; SRR975582     2  0.0000      0.983 0.000 1.000 0.000 0.000
#&gt; SRR975583     2  0.0000      0.983 0.000 1.000 0.000 0.000
#&gt; SRR975584     2  0.0000      0.983 0.000 1.000 0.000 0.000
#&gt; SRR975585     2  0.0000      0.983 0.000 1.000 0.000 0.000
#&gt; SRR975586     2  0.0000      0.983 0.000 1.000 0.000 0.000
#&gt; SRR975587     1  0.4500      0.497 0.684 0.000 0.316 0.000
#&gt; SRR975588     2  0.0000      0.983 0.000 1.000 0.000 0.000
#&gt; SRR975589     3  0.4790      0.377 0.380 0.000 0.620 0.000
#&gt; SRR975590     1  0.0000      0.971 1.000 0.000 0.000 0.000
#&gt; SRR975591     3  0.0000      0.927 0.000 0.000 1.000 0.000
#&gt; SRR975592     1  0.0000      0.971 1.000 0.000 0.000 0.000
#&gt; SRR975593     3  0.2345      0.819 0.100 0.000 0.900 0.000
#&gt; SRR975594     4  0.0000      1.000 0.000 0.000 0.000 1.000
#&gt; SRR975595     1  0.0000      0.971 1.000 0.000 0.000 0.000
#&gt; SRR975597     1  0.0000      0.971 1.000 0.000 0.000 0.000
#&gt; SRR975596     3  0.0000      0.927 0.000 0.000 1.000 0.000
#&gt; SRR975598     1  0.0000      0.971 1.000 0.000 0.000 0.000
#&gt; SRR975599     4  0.0000      1.000 0.000 0.000 0.000 1.000
#&gt; SRR975600     3  0.0592      0.914 0.016 0.000 0.984 0.000
#&gt; SRR975601     3  0.0000      0.927 0.000 0.000 1.000 0.000
#&gt; SRR975602     1  0.0000      0.971 1.000 0.000 0.000 0.000
#&gt; SRR975603     3  0.0000      0.927 0.000 0.000 1.000 0.000
#&gt; SRR975604     3  0.0000      0.927 0.000 0.000 1.000 0.000
</code></pre>

<script>
$('#tab-ATC-pam-get-classes-3-a').parent().next().next().hide();
$('#tab-ATC-pam-get-classes-3-a').click(function(){
  $('#tab-ATC-pam-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-pam-get-classes-4'>
<p><a id='tab-ATC-pam-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3    p4    p5
#&gt; SRR975551     1  0.0794      0.955 0.972 0.000 0.000 0.028 0.000
#&gt; SRR975552     1  0.0794      0.955 0.972 0.000 0.000 0.028 0.000
#&gt; SRR975554     1  0.0794      0.955 0.972 0.000 0.000 0.028 0.000
#&gt; SRR975553     2  0.0000      0.975 0.000 1.000 0.000 0.000 0.000
#&gt; SRR975555     1  0.0000      0.957 1.000 0.000 0.000 0.000 0.000
#&gt; SRR975556     2  0.0000      0.975 0.000 1.000 0.000 0.000 0.000
#&gt; SRR975557     4  0.3183      0.444 0.000 0.000 0.016 0.828 0.156
#&gt; SRR975558     3  0.0000      0.941 0.000 0.000 1.000 0.000 0.000
#&gt; SRR975559     1  0.0000      0.957 1.000 0.000 0.000 0.000 0.000
#&gt; SRR975560     2  0.2773      0.814 0.000 0.836 0.000 0.164 0.000
#&gt; SRR975561     2  0.0000      0.975 0.000 1.000 0.000 0.000 0.000
#&gt; SRR975562     3  0.0000      0.941 0.000 0.000 1.000 0.000 0.000
#&gt; SRR975563     2  0.0000      0.975 0.000 1.000 0.000 0.000 0.000
#&gt; SRR975564     1  0.0000      0.957 1.000 0.000 0.000 0.000 0.000
#&gt; SRR975565     1  0.0794      0.955 0.972 0.000 0.000 0.028 0.000
#&gt; SRR975566     1  0.0880      0.931 0.968 0.000 0.032 0.000 0.000
#&gt; SRR975567     3  0.0000      0.941 0.000 0.000 1.000 0.000 0.000
#&gt; SRR975568     1  0.0000      0.957 1.000 0.000 0.000 0.000 0.000
#&gt; SRR975569     2  0.0000      0.975 0.000 1.000 0.000 0.000 0.000
#&gt; SRR975570     2  0.0000      0.975 0.000 1.000 0.000 0.000 0.000
#&gt; SRR975571     2  0.0000      0.975 0.000 1.000 0.000 0.000 0.000
#&gt; SRR975572     2  0.0000      0.975 0.000 1.000 0.000 0.000 0.000
#&gt; SRR975573     2  0.0000      0.975 0.000 1.000 0.000 0.000 0.000
#&gt; SRR975574     2  0.0000      0.975 0.000 1.000 0.000 0.000 0.000
#&gt; SRR975575     2  0.0000      0.975 0.000 1.000 0.000 0.000 0.000
#&gt; SRR975576     2  0.0000      0.975 0.000 1.000 0.000 0.000 0.000
#&gt; SRR975577     2  0.0000      0.975 0.000 1.000 0.000 0.000 0.000
#&gt; SRR975578     2  0.0000      0.975 0.000 1.000 0.000 0.000 0.000
#&gt; SRR975579     4  0.3039      0.545 0.000 0.192 0.000 0.808 0.000
#&gt; SRR975580     2  0.2773      0.814 0.000 0.836 0.000 0.164 0.000
#&gt; SRR975581     2  0.0000      0.975 0.000 1.000 0.000 0.000 0.000
#&gt; SRR975582     2  0.0000      0.975 0.000 1.000 0.000 0.000 0.000
#&gt; SRR975583     2  0.0000      0.975 0.000 1.000 0.000 0.000 0.000
#&gt; SRR975584     2  0.0000      0.975 0.000 1.000 0.000 0.000 0.000
#&gt; SRR975585     2  0.0000      0.975 0.000 1.000 0.000 0.000 0.000
#&gt; SRR975586     2  0.2773      0.814 0.000 0.836 0.000 0.164 0.000
#&gt; SRR975587     1  0.3895      0.483 0.680 0.000 0.320 0.000 0.000
#&gt; SRR975588     2  0.0000      0.975 0.000 1.000 0.000 0.000 0.000
#&gt; SRR975589     3  0.3561      0.619 0.260 0.000 0.740 0.000 0.000
#&gt; SRR975590     1  0.0794      0.955 0.972 0.000 0.000 0.028 0.000
#&gt; SRR975591     3  0.0000      0.941 0.000 0.000 1.000 0.000 0.000
#&gt; SRR975592     1  0.0794      0.955 0.972 0.000 0.000 0.028 0.000
#&gt; SRR975593     3  0.2280      0.827 0.120 0.000 0.880 0.000 0.000
#&gt; SRR975594     5  0.0000      1.000 0.000 0.000 0.000 0.000 1.000
#&gt; SRR975595     1  0.0000      0.957 1.000 0.000 0.000 0.000 0.000
#&gt; SRR975597     1  0.0000      0.957 1.000 0.000 0.000 0.000 0.000
#&gt; SRR975596     3  0.0000      0.941 0.000 0.000 1.000 0.000 0.000
#&gt; SRR975598     1  0.0794      0.955 0.972 0.000 0.000 0.028 0.000
#&gt; SRR975599     5  0.0000      1.000 0.000 0.000 0.000 0.000 1.000
#&gt; SRR975600     3  0.1121      0.910 0.044 0.000 0.956 0.000 0.000
#&gt; SRR975601     3  0.0000      0.941 0.000 0.000 1.000 0.000 0.000
#&gt; SRR975602     1  0.0000      0.957 1.000 0.000 0.000 0.000 0.000
#&gt; SRR975603     3  0.0000      0.941 0.000 0.000 1.000 0.000 0.000
#&gt; SRR975604     3  0.0000      0.941 0.000 0.000 1.000 0.000 0.000
</code></pre>

<script>
$('#tab-ATC-pam-get-classes-4-a').parent().next().next().hide();
$('#tab-ATC-pam-get-classes-4-a').click(function(){
  $('#tab-ATC-pam-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-pam-get-classes-5'>
<p><a id='tab-ATC-pam-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3    p4    p5    p6
#&gt; SRR975551     1  0.3929      0.800 0.700 0.000 0.000 0.028 0.000 0.272
#&gt; SRR975552     1  0.2784      0.837 0.848 0.000 0.000 0.028 0.000 0.124
#&gt; SRR975554     1  0.3929      0.800 0.700 0.000 0.000 0.028 0.000 0.272
#&gt; SRR975553     2  0.0000      1.000 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR975555     1  0.0260      0.846 0.992 0.000 0.000 0.000 0.000 0.008
#&gt; SRR975556     2  0.0000      1.000 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR975557     4  0.0713      0.929 0.000 0.000 0.000 0.972 0.028 0.000
#&gt; SRR975558     3  0.2912      0.708 0.000 0.000 0.784 0.000 0.000 0.216
#&gt; SRR975559     1  0.3244      0.808 0.732 0.000 0.000 0.000 0.000 0.268
#&gt; SRR975560     6  0.3309      1.000 0.000 0.280 0.000 0.000 0.000 0.720
#&gt; SRR975561     2  0.0000      1.000 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR975562     3  0.0405      0.913 0.004 0.000 0.988 0.000 0.000 0.008
#&gt; SRR975563     2  0.0000      1.000 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR975564     1  0.0146      0.847 0.996 0.000 0.000 0.000 0.000 0.004
#&gt; SRR975565     1  0.3929      0.800 0.700 0.000 0.000 0.028 0.000 0.272
#&gt; SRR975566     1  0.3512      0.801 0.720 0.000 0.008 0.000 0.000 0.272
#&gt; SRR975567     3  0.0000      0.915 0.000 0.000 1.000 0.000 0.000 0.000
#&gt; SRR975568     1  0.0547      0.850 0.980 0.000 0.000 0.000 0.000 0.020
#&gt; SRR975569     2  0.0000      1.000 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR975570     2  0.0000      1.000 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR975571     2  0.0000      1.000 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR975572     2  0.0000      1.000 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR975573     2  0.0000      1.000 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR975574     2  0.0000      1.000 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR975575     2  0.0000      1.000 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR975576     2  0.0000      1.000 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR975577     2  0.0000      1.000 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR975578     2  0.0000      1.000 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR975579     4  0.0713      0.931 0.000 0.028 0.000 0.972 0.000 0.000
#&gt; SRR975580     6  0.3309      1.000 0.000 0.280 0.000 0.000 0.000 0.720
#&gt; SRR975581     2  0.0000      1.000 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR975582     2  0.0000      1.000 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR975583     2  0.0000      1.000 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR975584     2  0.0000      1.000 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR975585     2  0.0000      1.000 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR975586     6  0.3309      1.000 0.000 0.280 0.000 0.000 0.000 0.720
#&gt; SRR975587     1  0.3565      0.533 0.692 0.000 0.304 0.000 0.000 0.004
#&gt; SRR975588     2  0.0000      1.000 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR975589     3  0.3373      0.628 0.248 0.000 0.744 0.000 0.000 0.008
#&gt; SRR975590     1  0.3929      0.800 0.700 0.000 0.000 0.028 0.000 0.272
#&gt; SRR975591     3  0.0000      0.915 0.000 0.000 1.000 0.000 0.000 0.000
#&gt; SRR975592     1  0.0858      0.845 0.968 0.000 0.000 0.028 0.000 0.004
#&gt; SRR975593     3  0.2234      0.813 0.124 0.000 0.872 0.000 0.000 0.004
#&gt; SRR975594     5  0.0000      1.000 0.000 0.000 0.000 0.000 1.000 0.000
#&gt; SRR975595     1  0.0260      0.846 0.992 0.000 0.000 0.000 0.000 0.008
#&gt; SRR975597     1  0.0146      0.847 0.996 0.000 0.000 0.000 0.000 0.004
#&gt; SRR975596     3  0.0291      0.914 0.004 0.000 0.992 0.000 0.000 0.004
#&gt; SRR975598     1  0.0858      0.845 0.968 0.000 0.000 0.028 0.000 0.004
#&gt; SRR975599     5  0.0000      1.000 0.000 0.000 0.000 0.000 1.000 0.000
#&gt; SRR975600     3  0.1152      0.891 0.044 0.000 0.952 0.000 0.000 0.004
#&gt; SRR975601     3  0.0000      0.915 0.000 0.000 1.000 0.000 0.000 0.000
#&gt; SRR975602     1  0.0146      0.847 0.996 0.000 0.000 0.000 0.000 0.004
#&gt; SRR975603     3  0.0000      0.915 0.000 0.000 1.000 0.000 0.000 0.000
#&gt; SRR975604     3  0.0000      0.915 0.000 0.000 1.000 0.000 0.000 0.000
</code></pre>

<script>
$('#tab-ATC-pam-get-classes-5-a').parent().next().next().hide();
$('#tab-ATC-pam-get-classes-5-a').click(function(){
  $('#tab-ATC-pam-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-ATC-pam-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-ATC-pam-consensus-heatmap'>
<ul>
<li><a href='#tab-ATC-pam-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-ATC-pam-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-ATC-pam-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-ATC-pam-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-ATC-pam-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-pam-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-consensus-heatmap-1-1.png" alt="plot of chunk tab-ATC-pam-consensus-heatmap-1"/></p>

</div>
<div id='tab-ATC-pam-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-consensus-heatmap-2-1.png" alt="plot of chunk tab-ATC-pam-consensus-heatmap-2"/></p>

</div>
<div id='tab-ATC-pam-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-consensus-heatmap-3-1.png" alt="plot of chunk tab-ATC-pam-consensus-heatmap-3"/></p>

</div>
<div id='tab-ATC-pam-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-consensus-heatmap-4-1.png" alt="plot of chunk tab-ATC-pam-consensus-heatmap-4"/></p>

</div>
<div id='tab-ATC-pam-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-consensus-heatmap-5-1.png" alt="plot of chunk tab-ATC-pam-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-ATC-pam-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-ATC-pam-membership-heatmap'>
<ul>
<li><a href='#tab-ATC-pam-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-ATC-pam-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-ATC-pam-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-ATC-pam-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-ATC-pam-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-pam-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-membership-heatmap-1-1.png" alt="plot of chunk tab-ATC-pam-membership-heatmap-1"/></p>

</div>
<div id='tab-ATC-pam-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-membership-heatmap-2-1.png" alt="plot of chunk tab-ATC-pam-membership-heatmap-2"/></p>

</div>
<div id='tab-ATC-pam-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-membership-heatmap-3-1.png" alt="plot of chunk tab-ATC-pam-membership-heatmap-3"/></p>

</div>
<div id='tab-ATC-pam-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-membership-heatmap-4-1.png" alt="plot of chunk tab-ATC-pam-membership-heatmap-4"/></p>

</div>
<div id='tab-ATC-pam-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-membership-heatmap-5-1.png" alt="plot of chunk tab-ATC-pam-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-ATC-pam-get-signatures' ).tabs();
} );
</script>
<div id='tabs-ATC-pam-get-signatures'>
<ul>
<li><a href='#tab-ATC-pam-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-ATC-pam-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-ATC-pam-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-ATC-pam-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-ATC-pam-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-pam-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-get-signatures-1-1.png" alt="plot of chunk tab-ATC-pam-get-signatures-1"/></p>

</div>
<div id='tab-ATC-pam-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-get-signatures-2-1.png" alt="plot of chunk tab-ATC-pam-get-signatures-2"/></p>

</div>
<div id='tab-ATC-pam-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-get-signatures-3-1.png" alt="plot of chunk tab-ATC-pam-get-signatures-3"/></p>

</div>
<div id='tab-ATC-pam-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-get-signatures-4-1.png" alt="plot of chunk tab-ATC-pam-get-signatures-4"/></p>

</div>
<div id='tab-ATC-pam-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-get-signatures-5-1.png" alt="plot of chunk tab-ATC-pam-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-ATC-pam-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-ATC-pam-get-signatures-no-scale'>
<ul>
<li><a href='#tab-ATC-pam-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-ATC-pam-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-ATC-pam-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-ATC-pam-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-ATC-pam-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-pam-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-ATC-pam-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-ATC-pam-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-ATC-pam-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-ATC-pam-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-ATC-pam-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-ATC-pam-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-ATC-pam-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-ATC-pam-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-ATC-pam-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk ATC-pam-signature_compare](figure_cola/ATC-pam-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-ATC-pam-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-ATC-pam-dimension-reduction'>
<ul>
<li><a href='#tab-ATC-pam-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-ATC-pam-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-ATC-pam-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-ATC-pam-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-ATC-pam-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-pam-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-dimension-reduction-1-1.png" alt="plot of chunk tab-ATC-pam-dimension-reduction-1"/></p>

</div>
<div id='tab-ATC-pam-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-dimension-reduction-2-1.png" alt="plot of chunk tab-ATC-pam-dimension-reduction-2"/></p>

</div>
<div id='tab-ATC-pam-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-dimension-reduction-3-1.png" alt="plot of chunk tab-ATC-pam-dimension-reduction-3"/></p>

</div>
<div id='tab-ATC-pam-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-dimension-reduction-4-1.png" alt="plot of chunk tab-ATC-pam-dimension-reduction-4"/></p>

</div>
<div id='tab-ATC-pam-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-dimension-reduction-5-1.png" alt="plot of chunk tab-ATC-pam-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk ATC-pam-collect-classes](figure_cola/ATC-pam-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### ATC:mclust**






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["ATC", "mclust"]
# you can also extract it by
# res = res_list["ATC:mclust"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 17171 rows and 54 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'ATC' method.
#>   Subgroups are detected by 'mclust' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 3.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk ATC-mclust-collect-plots](figure_cola/ATC-mclust-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk ATC-mclust-select-partition-number](figure_cola/ATC-mclust-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 0.829           0.898       0.957         0.4777 0.502   0.502
#> 3 3 1.000           0.994       0.997         0.3840 0.781   0.586
#> 4 4 0.857           0.778       0.895         0.0766 0.940   0.825
#> 5 5 0.860           0.818       0.893         0.0607 0.899   0.673
#> 6 6 0.778           0.652       0.814         0.0267 0.900   0.642
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 3
```


Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-ATC-mclust-get-classes' ).tabs();
} );
</script>
<div id='tabs-ATC-mclust-get-classes'>
<ul>
<li><a href='#tab-ATC-mclust-get-classes-1'>k = 2</a></li>
<li><a href='#tab-ATC-mclust-get-classes-2'>k = 3</a></li>
<li><a href='#tab-ATC-mclust-get-classes-3'>k = 4</a></li>
<li><a href='#tab-ATC-mclust-get-classes-4'>k = 5</a></li>
<li><a href='#tab-ATC-mclust-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-ATC-mclust-get-classes-1'>
<p><a id='tab-ATC-mclust-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2
#&gt; SRR975551     1   0.000      1.000 1.000 0.000
#&gt; SRR975552     1   0.000      1.000 1.000 0.000
#&gt; SRR975554     1   0.000      1.000 1.000 0.000
#&gt; SRR975553     2   0.000      0.889 0.000 1.000
#&gt; SRR975555     1   0.000      1.000 1.000 0.000
#&gt; SRR975556     2   0.996      0.292 0.464 0.536
#&gt; SRR975557     1   0.000      1.000 1.000 0.000
#&gt; SRR975558     1   0.000      1.000 1.000 0.000
#&gt; SRR975559     1   0.000      1.000 1.000 0.000
#&gt; SRR975560     2   0.996      0.292 0.464 0.536
#&gt; SRR975561     2   0.996      0.292 0.464 0.536
#&gt; SRR975562     1   0.000      1.000 1.000 0.000
#&gt; SRR975563     2   0.000      0.889 0.000 1.000
#&gt; SRR975564     1   0.000      1.000 1.000 0.000
#&gt; SRR975565     1   0.000      1.000 1.000 0.000
#&gt; SRR975566     1   0.000      1.000 1.000 0.000
#&gt; SRR975567     1   0.000      1.000 1.000 0.000
#&gt; SRR975568     1   0.000      1.000 1.000 0.000
#&gt; SRR975569     2   0.000      0.889 0.000 1.000
#&gt; SRR975570     2   0.000      0.889 0.000 1.000
#&gt; SRR975571     2   0.000      0.889 0.000 1.000
#&gt; SRR975572     2   0.000      0.889 0.000 1.000
#&gt; SRR975573     2   0.000      0.889 0.000 1.000
#&gt; SRR975574     2   0.000      0.889 0.000 1.000
#&gt; SRR975575     2   0.000      0.889 0.000 1.000
#&gt; SRR975576     2   0.000      0.889 0.000 1.000
#&gt; SRR975577     2   0.000      0.889 0.000 1.000
#&gt; SRR975578     2   0.000      0.889 0.000 1.000
#&gt; SRR975579     1   0.000      1.000 1.000 0.000
#&gt; SRR975580     2   0.996      0.292 0.464 0.536
#&gt; SRR975581     2   0.000      0.889 0.000 1.000
#&gt; SRR975582     2   0.000      0.889 0.000 1.000
#&gt; SRR975583     2   0.000      0.889 0.000 1.000
#&gt; SRR975584     2   0.000      0.889 0.000 1.000
#&gt; SRR975585     2   0.000      0.889 0.000 1.000
#&gt; SRR975586     2   0.996      0.292 0.464 0.536
#&gt; SRR975587     1   0.000      1.000 1.000 0.000
#&gt; SRR975588     2   0.000      0.889 0.000 1.000
#&gt; SRR975589     1   0.000      1.000 1.000 0.000
#&gt; SRR975590     1   0.000      1.000 1.000 0.000
#&gt; SRR975591     1   0.000      1.000 1.000 0.000
#&gt; SRR975592     1   0.000      1.000 1.000 0.000
#&gt; SRR975593     1   0.000      1.000 1.000 0.000
#&gt; SRR975594     1   0.000      1.000 1.000 0.000
#&gt; SRR975595     1   0.000      1.000 1.000 0.000
#&gt; SRR975597     1   0.000      1.000 1.000 0.000
#&gt; SRR975596     1   0.000      1.000 1.000 0.000
#&gt; SRR975598     1   0.000      1.000 1.000 0.000
#&gt; SRR975599     1   0.000      1.000 1.000 0.000
#&gt; SRR975600     1   0.000      1.000 1.000 0.000
#&gt; SRR975601     1   0.000      1.000 1.000 0.000
#&gt; SRR975602     1   0.000      1.000 1.000 0.000
#&gt; SRR975603     1   0.000      1.000 1.000 0.000
#&gt; SRR975604     1   0.000      1.000 1.000 0.000
</code></pre>

<script>
$('#tab-ATC-mclust-get-classes-1-a').parent().next().next().hide();
$('#tab-ATC-mclust-get-classes-1-a').click(function(){
  $('#tab-ATC-mclust-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-mclust-get-classes-2'>
<p><a id='tab-ATC-mclust-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1 p2    p3
#&gt; SRR975551     1  0.0000      0.999 1.000  0 0.000
#&gt; SRR975552     1  0.0000      0.999 1.000  0 0.000
#&gt; SRR975554     1  0.0000      0.999 1.000  0 0.000
#&gt; SRR975553     2  0.0000      1.000 0.000  1 0.000
#&gt; SRR975555     1  0.0000      0.999 1.000  0 0.000
#&gt; SRR975556     3  0.0000      0.988 0.000  0 1.000
#&gt; SRR975557     3  0.0000      0.988 0.000  0 1.000
#&gt; SRR975558     3  0.0000      0.988 0.000  0 1.000
#&gt; SRR975559     1  0.0000      0.999 1.000  0 0.000
#&gt; SRR975560     3  0.0000      0.988 0.000  0 1.000
#&gt; SRR975561     3  0.0000      0.988 0.000  0 1.000
#&gt; SRR975562     1  0.0000      0.999 1.000  0 0.000
#&gt; SRR975563     2  0.0000      1.000 0.000  1 0.000
#&gt; SRR975564     1  0.0000      0.999 1.000  0 0.000
#&gt; SRR975565     1  0.0000      0.999 1.000  0 0.000
#&gt; SRR975566     1  0.0000      0.999 1.000  0 0.000
#&gt; SRR975567     3  0.0000      0.988 0.000  0 1.000
#&gt; SRR975568     1  0.0000      0.999 1.000  0 0.000
#&gt; SRR975569     2  0.0000      1.000 0.000  1 0.000
#&gt; SRR975570     2  0.0000      1.000 0.000  1 0.000
#&gt; SRR975571     2  0.0000      1.000 0.000  1 0.000
#&gt; SRR975572     2  0.0000      1.000 0.000  1 0.000
#&gt; SRR975573     2  0.0000      1.000 0.000  1 0.000
#&gt; SRR975574     2  0.0000      1.000 0.000  1 0.000
#&gt; SRR975575     2  0.0000      1.000 0.000  1 0.000
#&gt; SRR975576     2  0.0000      1.000 0.000  1 0.000
#&gt; SRR975577     2  0.0000      1.000 0.000  1 0.000
#&gt; SRR975578     2  0.0000      1.000 0.000  1 0.000
#&gt; SRR975579     3  0.0000      0.988 0.000  0 1.000
#&gt; SRR975580     3  0.0000      0.988 0.000  0 1.000
#&gt; SRR975581     2  0.0000      1.000 0.000  1 0.000
#&gt; SRR975582     2  0.0000      1.000 0.000  1 0.000
#&gt; SRR975583     2  0.0000      1.000 0.000  1 0.000
#&gt; SRR975584     2  0.0000      1.000 0.000  1 0.000
#&gt; SRR975585     2  0.0000      1.000 0.000  1 0.000
#&gt; SRR975586     3  0.0000      0.988 0.000  0 1.000
#&gt; SRR975587     1  0.0000      0.999 1.000  0 0.000
#&gt; SRR975588     2  0.0000      1.000 0.000  1 0.000
#&gt; SRR975589     1  0.0000      0.999 1.000  0 0.000
#&gt; SRR975590     1  0.0000      0.999 1.000  0 0.000
#&gt; SRR975591     3  0.1860      0.945 0.052  0 0.948
#&gt; SRR975592     1  0.0000      0.999 1.000  0 0.000
#&gt; SRR975593     1  0.0000      0.999 1.000  0 0.000
#&gt; SRR975594     3  0.0000      0.988 0.000  0 1.000
#&gt; SRR975595     1  0.0000      0.999 1.000  0 0.000
#&gt; SRR975597     1  0.0000      0.999 1.000  0 0.000
#&gt; SRR975596     1  0.0000      0.999 1.000  0 0.000
#&gt; SRR975598     1  0.0000      0.999 1.000  0 0.000
#&gt; SRR975599     3  0.0000      0.988 0.000  0 1.000
#&gt; SRR975600     1  0.0000      0.999 1.000  0 0.000
#&gt; SRR975601     1  0.0892      0.979 0.980  0 0.020
#&gt; SRR975602     1  0.0000      0.999 1.000  0 0.000
#&gt; SRR975603     1  0.0000      0.999 1.000  0 0.000
#&gt; SRR975604     3  0.2537      0.917 0.080  0 0.920
</code></pre>

<script>
$('#tab-ATC-mclust-get-classes-2-a').parent().next().next().hide();
$('#tab-ATC-mclust-get-classes-2-a').click(function(){
  $('#tab-ATC-mclust-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-mclust-get-classes-3'>
<p><a id='tab-ATC-mclust-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3    p4
#&gt; SRR975551     1  0.0000      0.925 1.000 0.000 0.000 0.000
#&gt; SRR975552     1  0.0000      0.925 1.000 0.000 0.000 0.000
#&gt; SRR975554     1  0.0000      0.925 1.000 0.000 0.000 0.000
#&gt; SRR975553     2  0.0000      0.953 0.000 1.000 0.000 0.000
#&gt; SRR975555     1  0.0000      0.925 1.000 0.000 0.000 0.000
#&gt; SRR975556     4  0.0000      0.717 0.000 0.000 0.000 1.000
#&gt; SRR975557     4  0.4998      0.634 0.000 0.000 0.488 0.512
#&gt; SRR975558     3  0.4245      0.345 0.020 0.000 0.784 0.196
#&gt; SRR975559     1  0.0000      0.925 1.000 0.000 0.000 0.000
#&gt; SRR975560     4  0.2469      0.737 0.000 0.000 0.108 0.892
#&gt; SRR975561     4  0.1022      0.695 0.000 0.032 0.000 0.968
#&gt; SRR975562     1  0.4804      0.191 0.616 0.000 0.384 0.000
#&gt; SRR975563     2  0.0188      0.952 0.000 0.996 0.004 0.000
#&gt; SRR975564     1  0.0000      0.925 1.000 0.000 0.000 0.000
#&gt; SRR975565     1  0.0000      0.925 1.000 0.000 0.000 0.000
#&gt; SRR975566     1  0.0000      0.925 1.000 0.000 0.000 0.000
#&gt; SRR975567     3  0.4348      0.353 0.024 0.000 0.780 0.196
#&gt; SRR975568     1  0.0000      0.925 1.000 0.000 0.000 0.000
#&gt; SRR975569     2  0.0000      0.953 0.000 1.000 0.000 0.000
#&gt; SRR975570     2  0.0000      0.953 0.000 1.000 0.000 0.000
#&gt; SRR975571     2  0.0000      0.953 0.000 1.000 0.000 0.000
#&gt; SRR975572     2  0.0000      0.953 0.000 1.000 0.000 0.000
#&gt; SRR975573     2  0.0000      0.953 0.000 1.000 0.000 0.000
#&gt; SRR975574     2  0.1902      0.916 0.000 0.932 0.004 0.064
#&gt; SRR975575     2  0.0188      0.952 0.000 0.996 0.004 0.000
#&gt; SRR975576     2  0.2197      0.904 0.000 0.916 0.004 0.080
#&gt; SRR975577     2  0.2944      0.858 0.000 0.868 0.004 0.128
#&gt; SRR975578     2  0.5167      0.139 0.000 0.508 0.004 0.488
#&gt; SRR975579     4  0.4972      0.654 0.000 0.000 0.456 0.544
#&gt; SRR975580     4  0.2469      0.737 0.000 0.000 0.108 0.892
#&gt; SRR975581     2  0.1109      0.938 0.000 0.968 0.004 0.028
#&gt; SRR975582     2  0.0188      0.952 0.000 0.996 0.004 0.000
#&gt; SRR975583     2  0.0000      0.953 0.000 1.000 0.000 0.000
#&gt; SRR975584     2  0.0000      0.953 0.000 1.000 0.000 0.000
#&gt; SRR975585     2  0.0000      0.953 0.000 1.000 0.000 0.000
#&gt; SRR975586     4  0.0000      0.717 0.000 0.000 0.000 1.000
#&gt; SRR975587     1  0.0000      0.925 1.000 0.000 0.000 0.000
#&gt; SRR975588     2  0.0000      0.953 0.000 1.000 0.000 0.000
#&gt; SRR975589     1  0.0000      0.925 1.000 0.000 0.000 0.000
#&gt; SRR975590     1  0.0000      0.925 1.000 0.000 0.000 0.000
#&gt; SRR975591     3  0.3404      0.588 0.104 0.000 0.864 0.032
#&gt; SRR975592     1  0.0000      0.925 1.000 0.000 0.000 0.000
#&gt; SRR975593     1  0.0000      0.925 1.000 0.000 0.000 0.000
#&gt; SRR975594     4  0.4972      0.637 0.000 0.000 0.456 0.544
#&gt; SRR975595     1  0.0000      0.925 1.000 0.000 0.000 0.000
#&gt; SRR975597     1  0.0000      0.925 1.000 0.000 0.000 0.000
#&gt; SRR975596     1  0.4804      0.191 0.616 0.000 0.384 0.000
#&gt; SRR975598     1  0.0000      0.925 1.000 0.000 0.000 0.000
#&gt; SRR975599     4  0.4972      0.637 0.000 0.000 0.456 0.544
#&gt; SRR975600     1  0.4855      0.171 0.600 0.000 0.400 0.000
#&gt; SRR975601     3  0.5649      0.390 0.392 0.000 0.580 0.028
#&gt; SRR975602     1  0.0000      0.925 1.000 0.000 0.000 0.000
#&gt; SRR975603     3  0.4961      0.241 0.448 0.000 0.552 0.000
#&gt; SRR975604     3  0.3149      0.576 0.088 0.000 0.880 0.032
</code></pre>

<script>
$('#tab-ATC-mclust-get-classes-3-a').parent().next().next().hide();
$('#tab-ATC-mclust-get-classes-3-a').click(function(){
  $('#tab-ATC-mclust-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-mclust-get-classes-4'>
<p><a id='tab-ATC-mclust-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3    p4    p5
#&gt; SRR975551     1  0.0000      0.960 1.000 0.000 0.000 0.000 0.000
#&gt; SRR975552     1  0.0000      0.960 1.000 0.000 0.000 0.000 0.000
#&gt; SRR975554     1  0.1341      0.960 0.944 0.000 0.056 0.000 0.000
#&gt; SRR975553     2  0.0290      0.961 0.000 0.992 0.000 0.000 0.008
#&gt; SRR975555     1  0.0162      0.959 0.996 0.000 0.004 0.000 0.000
#&gt; SRR975556     5  0.4074      0.136 0.000 0.000 0.000 0.364 0.636
#&gt; SRR975557     4  0.0000      0.865 0.000 0.000 0.000 1.000 0.000
#&gt; SRR975558     3  0.3934      0.478 0.008 0.000 0.716 0.276 0.000
#&gt; SRR975559     1  0.1341      0.960 0.944 0.000 0.056 0.000 0.000
#&gt; SRR975560     4  0.3975      0.892 0.000 0.000 0.144 0.792 0.064
#&gt; SRR975561     5  0.0404      0.473 0.000 0.000 0.000 0.012 0.988
#&gt; SRR975562     3  0.3636      0.680 0.272 0.000 0.728 0.000 0.000
#&gt; SRR975563     2  0.0000      0.962 0.000 1.000 0.000 0.000 0.000
#&gt; SRR975564     1  0.0000      0.960 1.000 0.000 0.000 0.000 0.000
#&gt; SRR975565     1  0.0000      0.960 1.000 0.000 0.000 0.000 0.000
#&gt; SRR975566     1  0.1341      0.960 0.944 0.000 0.056 0.000 0.000
#&gt; SRR975567     3  0.3934      0.478 0.008 0.000 0.716 0.276 0.000
#&gt; SRR975568     1  0.0000      0.960 1.000 0.000 0.000 0.000 0.000
#&gt; SRR975569     2  0.0290      0.961 0.000 0.992 0.000 0.000 0.008
#&gt; SRR975570     2  0.0162      0.962 0.000 0.996 0.000 0.000 0.004
#&gt; SRR975571     2  0.0290      0.961 0.000 0.992 0.000 0.000 0.008
#&gt; SRR975572     2  0.0290      0.961 0.000 0.992 0.000 0.000 0.008
#&gt; SRR975573     2  0.0000      0.962 0.000 1.000 0.000 0.000 0.000
#&gt; SRR975574     2  0.3774      0.430 0.000 0.704 0.000 0.000 0.296
#&gt; SRR975575     2  0.0000      0.962 0.000 1.000 0.000 0.000 0.000
#&gt; SRR975576     5  0.4015      0.535 0.000 0.348 0.000 0.000 0.652
#&gt; SRR975577     5  0.4015      0.535 0.000 0.348 0.000 0.000 0.652
#&gt; SRR975578     5  0.4201      0.554 0.000 0.328 0.000 0.008 0.664
#&gt; SRR975579     4  0.0000      0.865 0.000 0.000 0.000 1.000 0.000
#&gt; SRR975580     4  0.3975      0.892 0.000 0.000 0.144 0.792 0.064
#&gt; SRR975581     2  0.1544      0.885 0.000 0.932 0.000 0.000 0.068
#&gt; SRR975582     2  0.0000      0.962 0.000 1.000 0.000 0.000 0.000
#&gt; SRR975583     2  0.0000      0.962 0.000 1.000 0.000 0.000 0.000
#&gt; SRR975584     2  0.0000      0.962 0.000 1.000 0.000 0.000 0.000
#&gt; SRR975585     2  0.0000      0.962 0.000 1.000 0.000 0.000 0.000
#&gt; SRR975586     5  0.4101      0.116 0.000 0.000 0.000 0.372 0.628
#&gt; SRR975587     1  0.1341      0.960 0.944 0.000 0.056 0.000 0.000
#&gt; SRR975588     2  0.0290      0.961 0.000 0.992 0.000 0.000 0.008
#&gt; SRR975589     1  0.1341      0.960 0.944 0.000 0.056 0.000 0.000
#&gt; SRR975590     1  0.1341      0.960 0.944 0.000 0.056 0.000 0.000
#&gt; SRR975591     3  0.1408      0.658 0.008 0.000 0.948 0.044 0.000
#&gt; SRR975592     1  0.1341      0.960 0.944 0.000 0.056 0.000 0.000
#&gt; SRR975593     1  0.1410      0.958 0.940 0.000 0.060 0.000 0.000
#&gt; SRR975594     4  0.2280      0.904 0.000 0.000 0.120 0.880 0.000
#&gt; SRR975595     1  0.0162      0.959 0.996 0.000 0.004 0.000 0.000
#&gt; SRR975597     1  0.0162      0.959 0.996 0.000 0.004 0.000 0.000
#&gt; SRR975596     3  0.3684      0.676 0.280 0.000 0.720 0.000 0.000
#&gt; SRR975598     1  0.0963      0.941 0.964 0.000 0.036 0.000 0.000
#&gt; SRR975599     4  0.2424      0.901 0.000 0.000 0.132 0.868 0.000
#&gt; SRR975600     3  0.4161      0.493 0.392 0.000 0.608 0.000 0.000
#&gt; SRR975601     3  0.1399      0.667 0.020 0.000 0.952 0.028 0.000
#&gt; SRR975602     1  0.1851      0.936 0.912 0.000 0.088 0.000 0.000
#&gt; SRR975603     3  0.4114      0.689 0.272 0.000 0.712 0.016 0.000
#&gt; SRR975604     3  0.1408      0.658 0.008 0.000 0.948 0.044 0.000
</code></pre>

<script>
$('#tab-ATC-mclust-get-classes-4-a').parent().next().next().hide();
$('#tab-ATC-mclust-get-classes-4-a').click(function(){
  $('#tab-ATC-mclust-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-mclust-get-classes-5'>
<p><a id='tab-ATC-mclust-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3    p4    p5    p6
#&gt; SRR975551     1  0.0291      0.662 0.992 0.000 0.004 0.000 0.000 0.004
#&gt; SRR975552     1  0.0291      0.662 0.992 0.000 0.004 0.000 0.000 0.004
#&gt; SRR975554     1  0.2473      0.637 0.856 0.000 0.136 0.000 0.000 0.008
#&gt; SRR975553     2  0.0865      0.886 0.000 0.964 0.000 0.000 0.000 0.036
#&gt; SRR975555     1  0.1492      0.664 0.940 0.000 0.036 0.000 0.000 0.024
#&gt; SRR975556     5  0.1151      0.896 0.000 0.012 0.000 0.032 0.956 0.000
#&gt; SRR975557     4  0.0000      0.661 0.000 0.000 0.000 1.000 0.000 0.000
#&gt; SRR975558     3  0.5915      0.152 0.000 0.000 0.428 0.212 0.000 0.360
#&gt; SRR975559     1  0.4286      0.319 0.728 0.000 0.108 0.000 0.000 0.164
#&gt; SRR975560     4  0.7492      0.499 0.000 0.000 0.156 0.360 0.220 0.264
#&gt; SRR975561     5  0.1663      0.818 0.000 0.088 0.000 0.000 0.912 0.000
#&gt; SRR975562     1  0.4589      0.203 0.504 0.000 0.460 0.000 0.000 0.036
#&gt; SRR975563     2  0.0146      0.894 0.000 0.996 0.000 0.000 0.000 0.004
#&gt; SRR975564     1  0.0291      0.667 0.992 0.000 0.004 0.000 0.000 0.004
#&gt; SRR975565     1  0.0291      0.662 0.992 0.000 0.004 0.000 0.000 0.004
#&gt; SRR975566     6  0.4407      0.995 0.480 0.000 0.024 0.000 0.000 0.496
#&gt; SRR975567     3  0.5915      0.152 0.000 0.000 0.428 0.212 0.000 0.360
#&gt; SRR975568     1  0.0291      0.667 0.992 0.000 0.004 0.000 0.000 0.004
#&gt; SRR975569     2  0.1610      0.867 0.000 0.916 0.000 0.000 0.000 0.084
#&gt; SRR975570     2  0.0146      0.894 0.000 0.996 0.000 0.000 0.000 0.004
#&gt; SRR975571     2  0.0865      0.886 0.000 0.964 0.000 0.000 0.000 0.036
#&gt; SRR975572     2  0.0363      0.892 0.000 0.988 0.000 0.000 0.000 0.012
#&gt; SRR975573     2  0.0000      0.894 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR975574     2  0.3584      0.620 0.000 0.688 0.000 0.000 0.308 0.004
#&gt; SRR975575     2  0.0146      0.894 0.000 0.996 0.000 0.000 0.000 0.004
#&gt; SRR975576     2  0.3578      0.590 0.000 0.660 0.000 0.000 0.340 0.000
#&gt; SRR975577     2  0.3578      0.590 0.000 0.660 0.000 0.000 0.340 0.000
#&gt; SRR975578     2  0.3672      0.542 0.000 0.632 0.000 0.000 0.368 0.000
#&gt; SRR975579     4  0.0363      0.661 0.000 0.000 0.000 0.988 0.012 0.000
#&gt; SRR975580     4  0.7492      0.499 0.000 0.000 0.156 0.360 0.220 0.264
#&gt; SRR975581     2  0.1471      0.863 0.000 0.932 0.000 0.000 0.064 0.004
#&gt; SRR975582     2  0.0146      0.894 0.000 0.996 0.000 0.000 0.000 0.004
#&gt; SRR975583     2  0.0000      0.894 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR975584     2  0.0000      0.894 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR975585     2  0.0000      0.894 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR975586     5  0.0865      0.883 0.000 0.000 0.000 0.036 0.964 0.000
#&gt; SRR975587     6  0.4407      0.990 0.484 0.000 0.024 0.000 0.000 0.492
#&gt; SRR975588     2  0.1610      0.867 0.000 0.916 0.000 0.000 0.000 0.084
#&gt; SRR975589     6  0.4407      0.995 0.480 0.000 0.024 0.000 0.000 0.496
#&gt; SRR975590     1  0.2402      0.634 0.856 0.000 0.140 0.000 0.000 0.004
#&gt; SRR975591     3  0.1814      0.582 0.000 0.000 0.900 0.100 0.000 0.000
#&gt; SRR975592     1  0.2402      0.634 0.856 0.000 0.140 0.000 0.000 0.004
#&gt; SRR975593     1  0.5313     -0.788 0.508 0.000 0.108 0.000 0.000 0.384
#&gt; SRR975594     4  0.3027      0.671 0.000 0.000 0.148 0.824 0.000 0.028
#&gt; SRR975595     1  0.1367      0.661 0.944 0.000 0.044 0.000 0.000 0.012
#&gt; SRR975597     1  0.0363      0.669 0.988 0.000 0.012 0.000 0.000 0.000
#&gt; SRR975596     1  0.4589      0.203 0.504 0.000 0.460 0.000 0.000 0.036
#&gt; SRR975598     1  0.3168      0.614 0.804 0.000 0.172 0.000 0.000 0.024
#&gt; SRR975599     4  0.3776      0.638 0.000 0.000 0.196 0.756 0.000 0.048
#&gt; SRR975600     3  0.3742      0.083 0.348 0.000 0.648 0.000 0.000 0.004
#&gt; SRR975601     3  0.0260      0.648 0.008 0.000 0.992 0.000 0.000 0.000
#&gt; SRR975602     1  0.3261      0.578 0.780 0.000 0.204 0.000 0.000 0.016
#&gt; SRR975603     3  0.0777      0.644 0.024 0.000 0.972 0.000 0.000 0.004
#&gt; SRR975604     3  0.0405      0.646 0.004 0.000 0.988 0.008 0.000 0.000
</code></pre>

<script>
$('#tab-ATC-mclust-get-classes-5-a').parent().next().next().hide();
$('#tab-ATC-mclust-get-classes-5-a').click(function(){
  $('#tab-ATC-mclust-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-ATC-mclust-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-ATC-mclust-consensus-heatmap'>
<ul>
<li><a href='#tab-ATC-mclust-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-ATC-mclust-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-ATC-mclust-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-ATC-mclust-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-ATC-mclust-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-mclust-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-consensus-heatmap-1-1.png" alt="plot of chunk tab-ATC-mclust-consensus-heatmap-1"/></p>

</div>
<div id='tab-ATC-mclust-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-consensus-heatmap-2-1.png" alt="plot of chunk tab-ATC-mclust-consensus-heatmap-2"/></p>

</div>
<div id='tab-ATC-mclust-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-consensus-heatmap-3-1.png" alt="plot of chunk tab-ATC-mclust-consensus-heatmap-3"/></p>

</div>
<div id='tab-ATC-mclust-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-consensus-heatmap-4-1.png" alt="plot of chunk tab-ATC-mclust-consensus-heatmap-4"/></p>

</div>
<div id='tab-ATC-mclust-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-consensus-heatmap-5-1.png" alt="plot of chunk tab-ATC-mclust-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-ATC-mclust-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-ATC-mclust-membership-heatmap'>
<ul>
<li><a href='#tab-ATC-mclust-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-ATC-mclust-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-ATC-mclust-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-ATC-mclust-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-ATC-mclust-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-mclust-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-membership-heatmap-1-1.png" alt="plot of chunk tab-ATC-mclust-membership-heatmap-1"/></p>

</div>
<div id='tab-ATC-mclust-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-membership-heatmap-2-1.png" alt="plot of chunk tab-ATC-mclust-membership-heatmap-2"/></p>

</div>
<div id='tab-ATC-mclust-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-membership-heatmap-3-1.png" alt="plot of chunk tab-ATC-mclust-membership-heatmap-3"/></p>

</div>
<div id='tab-ATC-mclust-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-membership-heatmap-4-1.png" alt="plot of chunk tab-ATC-mclust-membership-heatmap-4"/></p>

</div>
<div id='tab-ATC-mclust-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-membership-heatmap-5-1.png" alt="plot of chunk tab-ATC-mclust-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-ATC-mclust-get-signatures' ).tabs();
} );
</script>
<div id='tabs-ATC-mclust-get-signatures'>
<ul>
<li><a href='#tab-ATC-mclust-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-ATC-mclust-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-ATC-mclust-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-ATC-mclust-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-ATC-mclust-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-mclust-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-get-signatures-1-1.png" alt="plot of chunk tab-ATC-mclust-get-signatures-1"/></p>

</div>
<div id='tab-ATC-mclust-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-get-signatures-2-1.png" alt="plot of chunk tab-ATC-mclust-get-signatures-2"/></p>

</div>
<div id='tab-ATC-mclust-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-get-signatures-3-1.png" alt="plot of chunk tab-ATC-mclust-get-signatures-3"/></p>

</div>
<div id='tab-ATC-mclust-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-get-signatures-4-1.png" alt="plot of chunk tab-ATC-mclust-get-signatures-4"/></p>

</div>
<div id='tab-ATC-mclust-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-get-signatures-5-1.png" alt="plot of chunk tab-ATC-mclust-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-ATC-mclust-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-ATC-mclust-get-signatures-no-scale'>
<ul>
<li><a href='#tab-ATC-mclust-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-ATC-mclust-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-ATC-mclust-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-ATC-mclust-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-ATC-mclust-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-mclust-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-ATC-mclust-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-ATC-mclust-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-ATC-mclust-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-ATC-mclust-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-ATC-mclust-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-ATC-mclust-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-ATC-mclust-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-ATC-mclust-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-ATC-mclust-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk ATC-mclust-signature_compare](figure_cola/ATC-mclust-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-ATC-mclust-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-ATC-mclust-dimension-reduction'>
<ul>
<li><a href='#tab-ATC-mclust-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-ATC-mclust-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-ATC-mclust-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-ATC-mclust-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-ATC-mclust-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-mclust-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-dimension-reduction-1-1.png" alt="plot of chunk tab-ATC-mclust-dimension-reduction-1"/></p>

</div>
<div id='tab-ATC-mclust-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-dimension-reduction-2-1.png" alt="plot of chunk tab-ATC-mclust-dimension-reduction-2"/></p>

</div>
<div id='tab-ATC-mclust-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-dimension-reduction-3-1.png" alt="plot of chunk tab-ATC-mclust-dimension-reduction-3"/></p>

</div>
<div id='tab-ATC-mclust-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-dimension-reduction-4-1.png" alt="plot of chunk tab-ATC-mclust-dimension-reduction-4"/></p>

</div>
<div id='tab-ATC-mclust-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-dimension-reduction-5-1.png" alt="plot of chunk tab-ATC-mclust-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk ATC-mclust-collect-classes](figure_cola/ATC-mclust-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### ATC:NMF**






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["ATC", "NMF"]
# you can also extract it by
# res = res_list["ATC:NMF"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 17171 rows and 54 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'ATC' method.
#>   Subgroups are detected by 'NMF' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 2.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk ATC-NMF-collect-plots](figure_cola/ATC-NMF-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk ATC-NMF-select-partition-number](figure_cola/ATC-NMF-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 1.000           0.974       0.991         0.5082 0.491   0.491
#> 3 3 0.807           0.782       0.894         0.1976 0.911   0.821
#> 4 4 0.799           0.828       0.902         0.1368 0.859   0.663
#> 5 5 0.758           0.693       0.831         0.0405 0.954   0.850
#> 6 6 0.729           0.676       0.826         0.0377 0.891   0.663
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 2
```


Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-ATC-NMF-get-classes' ).tabs();
} );
</script>
<div id='tabs-ATC-NMF-get-classes'>
<ul>
<li><a href='#tab-ATC-NMF-get-classes-1'>k = 2</a></li>
<li><a href='#tab-ATC-NMF-get-classes-2'>k = 3</a></li>
<li><a href='#tab-ATC-NMF-get-classes-3'>k = 4</a></li>
<li><a href='#tab-ATC-NMF-get-classes-4'>k = 5</a></li>
<li><a href='#tab-ATC-NMF-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-ATC-NMF-get-classes-1'>
<p><a id='tab-ATC-NMF-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2
#&gt; SRR975551     1   0.000      1.000 1.000 0.000
#&gt; SRR975552     1   0.000      1.000 1.000 0.000
#&gt; SRR975554     1   0.000      1.000 1.000 0.000
#&gt; SRR975553     2   0.000      0.980 0.000 1.000
#&gt; SRR975555     1   0.000      1.000 1.000 0.000
#&gt; SRR975556     2   0.000      0.980 0.000 1.000
#&gt; SRR975557     2   0.000      0.980 0.000 1.000
#&gt; SRR975558     1   0.000      1.000 1.000 0.000
#&gt; SRR975559     1   0.000      1.000 1.000 0.000
#&gt; SRR975560     2   0.000      0.980 0.000 1.000
#&gt; SRR975561     2   0.000      0.980 0.000 1.000
#&gt; SRR975562     1   0.000      1.000 1.000 0.000
#&gt; SRR975563     2   0.000      0.980 0.000 1.000
#&gt; SRR975564     1   0.000      1.000 1.000 0.000
#&gt; SRR975565     1   0.000      1.000 1.000 0.000
#&gt; SRR975566     1   0.000      1.000 1.000 0.000
#&gt; SRR975567     1   0.000      1.000 1.000 0.000
#&gt; SRR975568     1   0.000      1.000 1.000 0.000
#&gt; SRR975569     2   0.000      0.980 0.000 1.000
#&gt; SRR975570     2   0.000      0.980 0.000 1.000
#&gt; SRR975571     2   0.000      0.980 0.000 1.000
#&gt; SRR975572     2   0.000      0.980 0.000 1.000
#&gt; SRR975573     2   0.000      0.980 0.000 1.000
#&gt; SRR975574     2   0.000      0.980 0.000 1.000
#&gt; SRR975575     2   0.000      0.980 0.000 1.000
#&gt; SRR975576     2   0.000      0.980 0.000 1.000
#&gt; SRR975577     2   0.000      0.980 0.000 1.000
#&gt; SRR975578     2   0.000      0.980 0.000 1.000
#&gt; SRR975579     2   0.000      0.980 0.000 1.000
#&gt; SRR975580     2   0.000      0.980 0.000 1.000
#&gt; SRR975581     2   0.000      0.980 0.000 1.000
#&gt; SRR975582     2   0.000      0.980 0.000 1.000
#&gt; SRR975583     2   0.000      0.980 0.000 1.000
#&gt; SRR975584     2   0.000      0.980 0.000 1.000
#&gt; SRR975585     2   0.000      0.980 0.000 1.000
#&gt; SRR975586     2   0.000      0.980 0.000 1.000
#&gt; SRR975587     1   0.000      1.000 1.000 0.000
#&gt; SRR975588     2   0.000      0.980 0.000 1.000
#&gt; SRR975589     1   0.000      1.000 1.000 0.000
#&gt; SRR975590     1   0.000      1.000 1.000 0.000
#&gt; SRR975591     1   0.000      1.000 1.000 0.000
#&gt; SRR975592     1   0.000      1.000 1.000 0.000
#&gt; SRR975593     1   0.000      1.000 1.000 0.000
#&gt; SRR975594     2   0.999      0.062 0.484 0.516
#&gt; SRR975595     1   0.000      1.000 1.000 0.000
#&gt; SRR975597     1   0.000      1.000 1.000 0.000
#&gt; SRR975596     1   0.000      1.000 1.000 0.000
#&gt; SRR975598     1   0.000      1.000 1.000 0.000
#&gt; SRR975599     1   0.000      1.000 1.000 0.000
#&gt; SRR975600     1   0.000      1.000 1.000 0.000
#&gt; SRR975601     1   0.000      1.000 1.000 0.000
#&gt; SRR975602     1   0.000      1.000 1.000 0.000
#&gt; SRR975603     1   0.000      1.000 1.000 0.000
#&gt; SRR975604     1   0.000      1.000 1.000 0.000
</code></pre>

<script>
$('#tab-ATC-NMF-get-classes-1-a').parent().next().next().hide();
$('#tab-ATC-NMF-get-classes-1-a').click(function(){
  $('#tab-ATC-NMF-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-NMF-get-classes-2'>
<p><a id='tab-ATC-NMF-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3
#&gt; SRR975551     1  0.1289     0.8127 0.968 0.000 0.032
#&gt; SRR975552     1  0.1289     0.8127 0.968 0.000 0.032
#&gt; SRR975554     1  0.0747     0.8250 0.984 0.000 0.016
#&gt; SRR975553     2  0.0000     0.9827 0.000 1.000 0.000
#&gt; SRR975555     1  0.0892     0.8179 0.980 0.000 0.020
#&gt; SRR975556     2  0.0000     0.9827 0.000 1.000 0.000
#&gt; SRR975557     3  0.6421     0.2279 0.004 0.424 0.572
#&gt; SRR975558     1  0.4887     0.7349 0.772 0.000 0.228
#&gt; SRR975559     1  0.6154     0.5431 0.592 0.000 0.408
#&gt; SRR975560     2  0.5899     0.5053 0.020 0.736 0.244
#&gt; SRR975561     2  0.0000     0.9827 0.000 1.000 0.000
#&gt; SRR975562     1  0.6260     0.4869 0.552 0.000 0.448
#&gt; SRR975563     2  0.0000     0.9827 0.000 1.000 0.000
#&gt; SRR975564     1  0.1031     0.8164 0.976 0.000 0.024
#&gt; SRR975565     1  0.1289     0.8127 0.968 0.000 0.032
#&gt; SRR975566     1  0.2356     0.8204 0.928 0.000 0.072
#&gt; SRR975567     1  0.3038     0.8083 0.896 0.000 0.104
#&gt; SRR975568     1  0.1163     0.8146 0.972 0.000 0.028
#&gt; SRR975569     2  0.0000     0.9827 0.000 1.000 0.000
#&gt; SRR975570     2  0.0000     0.9827 0.000 1.000 0.000
#&gt; SRR975571     2  0.0000     0.9827 0.000 1.000 0.000
#&gt; SRR975572     2  0.0000     0.9827 0.000 1.000 0.000
#&gt; SRR975573     2  0.0000     0.9827 0.000 1.000 0.000
#&gt; SRR975574     2  0.0000     0.9827 0.000 1.000 0.000
#&gt; SRR975575     2  0.0000     0.9827 0.000 1.000 0.000
#&gt; SRR975576     2  0.0000     0.9827 0.000 1.000 0.000
#&gt; SRR975577     2  0.0000     0.9827 0.000 1.000 0.000
#&gt; SRR975578     2  0.0000     0.9827 0.000 1.000 0.000
#&gt; SRR975579     3  0.6309     0.0264 0.000 0.496 0.504
#&gt; SRR975580     2  0.0592     0.9675 0.000 0.988 0.012
#&gt; SRR975581     2  0.0000     0.9827 0.000 1.000 0.000
#&gt; SRR975582     2  0.0000     0.9827 0.000 1.000 0.000
#&gt; SRR975583     2  0.0000     0.9827 0.000 1.000 0.000
#&gt; SRR975584     2  0.0000     0.9827 0.000 1.000 0.000
#&gt; SRR975585     2  0.0000     0.9827 0.000 1.000 0.000
#&gt; SRR975586     2  0.0000     0.9827 0.000 1.000 0.000
#&gt; SRR975587     1  0.0237     0.8228 0.996 0.000 0.004
#&gt; SRR975588     2  0.0000     0.9827 0.000 1.000 0.000
#&gt; SRR975589     1  0.1964     0.8246 0.944 0.000 0.056
#&gt; SRR975590     1  0.1289     0.8127 0.968 0.000 0.032
#&gt; SRR975591     3  0.2625     0.4769 0.084 0.000 0.916
#&gt; SRR975592     1  0.0892     0.8261 0.980 0.000 0.020
#&gt; SRR975593     1  0.5988     0.5946 0.632 0.000 0.368
#&gt; SRR975594     3  0.1647     0.5006 0.036 0.004 0.960
#&gt; SRR975595     1  0.4399     0.7629 0.812 0.000 0.188
#&gt; SRR975597     1  0.1289     0.8268 0.968 0.000 0.032
#&gt; SRR975596     1  0.6267     0.4799 0.548 0.000 0.452
#&gt; SRR975598     1  0.5363     0.6962 0.724 0.000 0.276
#&gt; SRR975599     1  0.6280     0.4654 0.540 0.000 0.460
#&gt; SRR975600     1  0.0424     0.8240 0.992 0.000 0.008
#&gt; SRR975601     1  0.2165     0.8230 0.936 0.000 0.064
#&gt; SRR975602     1  0.1753     0.8261 0.952 0.000 0.048
#&gt; SRR975603     1  0.6267     0.4772 0.548 0.000 0.452
#&gt; SRR975604     3  0.6154    -0.2976 0.408 0.000 0.592
</code></pre>

<script>
$('#tab-ATC-NMF-get-classes-2-a').parent().next().next().hide();
$('#tab-ATC-NMF-get-classes-2-a').click(function(){
  $('#tab-ATC-NMF-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-NMF-get-classes-3'>
<p><a id='tab-ATC-NMF-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3    p4
#&gt; SRR975551     1  0.1109     0.8283 0.968 0.000 0.028 0.004
#&gt; SRR975552     1  0.0657     0.8238 0.984 0.000 0.012 0.004
#&gt; SRR975554     1  0.4992     0.0195 0.524 0.000 0.476 0.000
#&gt; SRR975553     2  0.0000     0.9904 0.000 1.000 0.000 0.000
#&gt; SRR975555     3  0.5055     0.4758 0.368 0.000 0.624 0.008
#&gt; SRR975556     2  0.0188     0.9886 0.000 0.996 0.000 0.004
#&gt; SRR975557     4  0.1114     0.8789 0.004 0.008 0.016 0.972
#&gt; SRR975558     3  0.4304     0.6760 0.284 0.000 0.716 0.000
#&gt; SRR975559     3  0.2530     0.8238 0.112 0.000 0.888 0.000
#&gt; SRR975560     3  0.4875     0.4176 0.008 0.296 0.692 0.004
#&gt; SRR975561     2  0.0336     0.9876 0.000 0.992 0.008 0.000
#&gt; SRR975562     3  0.2081     0.8183 0.084 0.000 0.916 0.000
#&gt; SRR975563     2  0.0000     0.9904 0.000 1.000 0.000 0.000
#&gt; SRR975564     1  0.4920     0.4303 0.628 0.000 0.368 0.004
#&gt; SRR975565     1  0.1004     0.8280 0.972 0.000 0.024 0.004
#&gt; SRR975566     1  0.3356     0.7615 0.824 0.000 0.176 0.000
#&gt; SRR975567     1  0.4222     0.6424 0.728 0.000 0.272 0.000
#&gt; SRR975568     1  0.0336     0.8231 0.992 0.000 0.008 0.000
#&gt; SRR975569     2  0.0000     0.9904 0.000 1.000 0.000 0.000
#&gt; SRR975570     2  0.0000     0.9904 0.000 1.000 0.000 0.000
#&gt; SRR975571     2  0.0000     0.9904 0.000 1.000 0.000 0.000
#&gt; SRR975572     2  0.0000     0.9904 0.000 1.000 0.000 0.000
#&gt; SRR975573     2  0.0000     0.9904 0.000 1.000 0.000 0.000
#&gt; SRR975574     2  0.0000     0.9904 0.000 1.000 0.000 0.000
#&gt; SRR975575     2  0.0000     0.9904 0.000 1.000 0.000 0.000
#&gt; SRR975576     2  0.0336     0.9876 0.000 0.992 0.008 0.000
#&gt; SRR975577     2  0.0336     0.9876 0.000 0.992 0.008 0.000
#&gt; SRR975578     2  0.0336     0.9876 0.000 0.992 0.008 0.000
#&gt; SRR975579     4  0.1406     0.8702 0.000 0.024 0.016 0.960
#&gt; SRR975580     2  0.3128     0.8388 0.004 0.864 0.128 0.004
#&gt; SRR975581     2  0.0336     0.9876 0.000 0.992 0.008 0.000
#&gt; SRR975582     2  0.0000     0.9904 0.000 1.000 0.000 0.000
#&gt; SRR975583     2  0.0000     0.9904 0.000 1.000 0.000 0.000
#&gt; SRR975584     2  0.0000     0.9904 0.000 1.000 0.000 0.000
#&gt; SRR975585     2  0.0000     0.9904 0.000 1.000 0.000 0.000
#&gt; SRR975586     2  0.0524     0.9853 0.000 0.988 0.008 0.004
#&gt; SRR975587     1  0.0921     0.8282 0.972 0.000 0.028 0.000
#&gt; SRR975588     2  0.0188     0.9884 0.000 0.996 0.000 0.004
#&gt; SRR975589     1  0.3219     0.7716 0.836 0.000 0.164 0.000
#&gt; SRR975590     1  0.0000     0.8174 1.000 0.000 0.000 0.000
#&gt; SRR975591     4  0.0817     0.8745 0.024 0.000 0.000 0.976
#&gt; SRR975592     1  0.3837     0.7125 0.776 0.000 0.224 0.000
#&gt; SRR975593     3  0.3764     0.7724 0.216 0.000 0.784 0.000
#&gt; SRR975594     4  0.0672     0.8787 0.008 0.000 0.008 0.984
#&gt; SRR975595     3  0.2921     0.8206 0.140 0.000 0.860 0.000
#&gt; SRR975597     3  0.3668     0.7961 0.188 0.000 0.808 0.004
#&gt; SRR975596     3  0.2149     0.8198 0.088 0.000 0.912 0.000
#&gt; SRR975598     3  0.2216     0.8215 0.092 0.000 0.908 0.000
#&gt; SRR975599     3  0.2011     0.8156 0.080 0.000 0.920 0.000
#&gt; SRR975600     1  0.0376     0.8207 0.992 0.000 0.004 0.004
#&gt; SRR975601     1  0.2494     0.8155 0.916 0.000 0.048 0.036
#&gt; SRR975602     3  0.3219     0.8123 0.164 0.000 0.836 0.000
#&gt; SRR975603     3  0.7236     0.4188 0.168 0.000 0.520 0.312
#&gt; SRR975604     4  0.6116     0.3687 0.068 0.000 0.320 0.612
</code></pre>

<script>
$('#tab-ATC-NMF-get-classes-3-a').parent().next().next().hide();
$('#tab-ATC-NMF-get-classes-3-a').click(function(){
  $('#tab-ATC-NMF-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-NMF-get-classes-4'>
<p><a id='tab-ATC-NMF-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3    p4 p5
#&gt; SRR975551     3  0.2144     0.7061 0.020 0.000 0.912 0.000 NA
#&gt; SRR975552     3  0.1341     0.7043 0.000 0.000 0.944 0.000 NA
#&gt; SRR975554     3  0.3790     0.4881 0.272 0.000 0.724 0.000 NA
#&gt; SRR975553     2  0.0000     0.9618 0.000 1.000 0.000 0.000 NA
#&gt; SRR975555     1  0.5798     0.4793 0.608 0.000 0.236 0.000 NA
#&gt; SRR975556     2  0.0703     0.9516 0.000 0.976 0.000 0.000 NA
#&gt; SRR975557     4  0.4291     0.6216 0.000 0.000 0.000 0.536 NA
#&gt; SRR975558     1  0.5752     0.4894 0.620 0.000 0.208 0.000 NA
#&gt; SRR975559     1  0.4138     0.4497 0.616 0.000 0.384 0.000 NA
#&gt; SRR975560     1  0.2992     0.5718 0.872 0.092 0.012 0.000 NA
#&gt; SRR975561     2  0.0162     0.9615 0.000 0.996 0.000 0.000 NA
#&gt; SRR975562     1  0.1502     0.6674 0.940 0.000 0.056 0.000 NA
#&gt; SRR975563     2  0.0000     0.9618 0.000 1.000 0.000 0.000 NA
#&gt; SRR975564     3  0.5990     0.4033 0.296 0.000 0.560 0.000 NA
#&gt; SRR975565     3  0.2293     0.6966 0.016 0.000 0.900 0.000 NA
#&gt; SRR975566     3  0.2127     0.6910 0.108 0.000 0.892 0.000 NA
#&gt; SRR975567     3  0.5384     0.5412 0.196 0.000 0.664 0.000 NA
#&gt; SRR975568     3  0.3123     0.6624 0.012 0.000 0.828 0.000 NA
#&gt; SRR975569     2  0.1671     0.9099 0.000 0.924 0.000 0.000 NA
#&gt; SRR975570     2  0.0000     0.9618 0.000 1.000 0.000 0.000 NA
#&gt; SRR975571     2  0.0000     0.9618 0.000 1.000 0.000 0.000 NA
#&gt; SRR975572     2  0.0000     0.9618 0.000 1.000 0.000 0.000 NA
#&gt; SRR975573     2  0.0000     0.9618 0.000 1.000 0.000 0.000 NA
#&gt; SRR975574     2  0.0162     0.9615 0.000 0.996 0.000 0.000 NA
#&gt; SRR975575     2  0.0000     0.9618 0.000 1.000 0.000 0.000 NA
#&gt; SRR975576     2  0.0162     0.9615 0.000 0.996 0.000 0.000 NA
#&gt; SRR975577     2  0.0162     0.9615 0.000 0.996 0.000 0.000 NA
#&gt; SRR975578     2  0.0162     0.9615 0.000 0.996 0.000 0.000 NA
#&gt; SRR975579     4  0.4291     0.6216 0.000 0.000 0.000 0.536 NA
#&gt; SRR975580     2  0.4794     0.2163 0.464 0.520 0.004 0.000 NA
#&gt; SRR975581     2  0.0162     0.9615 0.000 0.996 0.000 0.000 NA
#&gt; SRR975582     2  0.0162     0.9615 0.000 0.996 0.000 0.000 NA
#&gt; SRR975583     2  0.0000     0.9618 0.000 1.000 0.000 0.000 NA
#&gt; SRR975584     2  0.0290     0.9582 0.000 0.992 0.000 0.000 NA
#&gt; SRR975585     2  0.0000     0.9618 0.000 1.000 0.000 0.000 NA
#&gt; SRR975586     2  0.2067     0.9051 0.032 0.920 0.000 0.000 NA
#&gt; SRR975587     3  0.1901     0.7109 0.004 0.000 0.932 0.024 NA
#&gt; SRR975588     2  0.2127     0.8825 0.000 0.892 0.000 0.000 NA
#&gt; SRR975589     3  0.4057     0.6772 0.120 0.000 0.792 0.000 NA
#&gt; SRR975590     3  0.1502     0.7032 0.004 0.000 0.940 0.000 NA
#&gt; SRR975591     4  0.0290     0.6892 0.000 0.000 0.008 0.992 NA
#&gt; SRR975592     3  0.2900     0.6891 0.108 0.000 0.864 0.000 NA
#&gt; SRR975593     3  0.4827    -0.1968 0.476 0.000 0.504 0.000 NA
#&gt; SRR975594     4  0.0000     0.6892 0.000 0.000 0.000 1.000 NA
#&gt; SRR975595     1  0.4127     0.5571 0.680 0.000 0.312 0.000 NA
#&gt; SRR975597     1  0.4542     0.2844 0.536 0.000 0.456 0.000 NA
#&gt; SRR975596     1  0.1341     0.6690 0.944 0.000 0.056 0.000 NA
#&gt; SRR975598     1  0.3562     0.6458 0.788 0.000 0.196 0.000 NA
#&gt; SRR975599     1  0.0960     0.6465 0.972 0.000 0.016 0.008 NA
#&gt; SRR975600     3  0.4729     0.6214 0.024 0.000 0.748 0.048 NA
#&gt; SRR975601     4  0.6426     0.0365 0.012 0.000 0.372 0.488 NA
#&gt; SRR975602     1  0.4415     0.3318 0.552 0.000 0.444 0.000 NA
#&gt; SRR975603     3  0.7369     0.1368 0.260 0.000 0.448 0.252 NA
#&gt; SRR975604     4  0.5579     0.5144 0.172 0.000 0.084 0.700 NA
</code></pre>

<script>
$('#tab-ATC-NMF-get-classes-4-a').parent().next().next().hide();
$('#tab-ATC-NMF-get-classes-4-a').click(function(){
  $('#tab-ATC-NMF-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-NMF-get-classes-5'>
<p><a id='tab-ATC-NMF-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3    p4    p5    p6
#&gt; SRR975551     1  0.1881     0.5889 0.924 0.000 0.004 0.004 0.052 0.016
#&gt; SRR975552     1  0.1364     0.5855 0.944 0.000 0.004 0.004 0.048 0.000
#&gt; SRR975554     1  0.2667     0.6179 0.852 0.000 0.000 0.000 0.020 0.128
#&gt; SRR975553     2  0.0260     0.9576 0.000 0.992 0.000 0.000 0.008 0.000
#&gt; SRR975555     6  0.6268     0.3121 0.156 0.000 0.016 0.040 0.204 0.584
#&gt; SRR975556     2  0.2730     0.9013 0.000 0.872 0.004 0.024 0.092 0.008
#&gt; SRR975557     4  0.2932     0.9805 0.000 0.000 0.164 0.820 0.016 0.000
#&gt; SRR975558     5  0.5491     0.2650 0.092 0.004 0.000 0.008 0.532 0.364
#&gt; SRR975559     1  0.4253     0.4708 0.608 0.000 0.000 0.008 0.012 0.372
#&gt; SRR975560     6  0.2078     0.6509 0.000 0.040 0.000 0.012 0.032 0.916
#&gt; SRR975561     2  0.1297     0.9506 0.000 0.948 0.000 0.012 0.040 0.000
#&gt; SRR975562     6  0.1908     0.6771 0.096 0.000 0.004 0.000 0.000 0.900
#&gt; SRR975563     2  0.0363     0.9582 0.000 0.988 0.000 0.000 0.012 0.000
#&gt; SRR975564     5  0.6000     0.5786 0.332 0.000 0.004 0.004 0.476 0.184
#&gt; SRR975565     1  0.2840     0.5413 0.872 0.000 0.008 0.032 0.080 0.008
#&gt; SRR975566     1  0.2999     0.5846 0.840 0.000 0.000 0.000 0.112 0.048
#&gt; SRR975567     1  0.5984     0.1980 0.600 0.000 0.004 0.112 0.228 0.056
#&gt; SRR975568     5  0.3907     0.5186 0.408 0.000 0.004 0.000 0.588 0.000
#&gt; SRR975569     2  0.2765     0.8751 0.000 0.876 0.016 0.044 0.064 0.000
#&gt; SRR975570     2  0.0260     0.9560 0.000 0.992 0.000 0.000 0.008 0.000
#&gt; SRR975571     2  0.0260     0.9576 0.000 0.992 0.000 0.000 0.008 0.000
#&gt; SRR975572     2  0.0000     0.9573 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR975573     2  0.0000     0.9573 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR975574     2  0.0603     0.9574 0.000 0.980 0.000 0.004 0.016 0.000
#&gt; SRR975575     2  0.0000     0.9573 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR975576     2  0.1124     0.9527 0.000 0.956 0.000 0.008 0.036 0.000
#&gt; SRR975577     2  0.1124     0.9527 0.000 0.956 0.000 0.008 0.036 0.000
#&gt; SRR975578     2  0.1124     0.9527 0.000 0.956 0.000 0.008 0.036 0.000
#&gt; SRR975579     4  0.2491     0.9805 0.000 0.000 0.164 0.836 0.000 0.000
#&gt; SRR975580     6  0.3837     0.4700 0.000 0.224 0.000 0.016 0.016 0.744
#&gt; SRR975581     2  0.1124     0.9527 0.000 0.956 0.000 0.008 0.036 0.000
#&gt; SRR975582     2  0.1049     0.9535 0.000 0.960 0.000 0.008 0.032 0.000
#&gt; SRR975583     2  0.0000     0.9573 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR975584     2  0.0622     0.9545 0.000 0.980 0.000 0.008 0.012 0.000
#&gt; SRR975585     2  0.0146     0.9578 0.000 0.996 0.000 0.000 0.004 0.000
#&gt; SRR975586     2  0.3693     0.8066 0.000 0.800 0.000 0.016 0.136 0.048
#&gt; SRR975587     1  0.0458     0.6010 0.984 0.000 0.016 0.000 0.000 0.000
#&gt; SRR975588     2  0.3374     0.8345 0.000 0.836 0.024 0.048 0.092 0.000
#&gt; SRR975589     1  0.5071    -0.1499 0.552 0.000 0.004 0.004 0.380 0.060
#&gt; SRR975590     1  0.0972     0.6004 0.964 0.000 0.000 0.000 0.028 0.008
#&gt; SRR975591     3  0.4225     0.6510 0.084 0.000 0.784 0.060 0.072 0.000
#&gt; SRR975592     1  0.3062     0.5372 0.816 0.000 0.000 0.000 0.160 0.024
#&gt; SRR975593     1  0.5408     0.4359 0.616 0.000 0.004 0.004 0.168 0.208
#&gt; SRR975594     3  0.1204     0.5641 0.000 0.000 0.944 0.056 0.000 0.000
#&gt; SRR975595     1  0.4227     0.1603 0.500 0.000 0.008 0.000 0.004 0.488
#&gt; SRR975597     1  0.3895     0.5562 0.696 0.000 0.004 0.000 0.016 0.284
#&gt; SRR975596     6  0.2211     0.6769 0.080 0.000 0.004 0.008 0.008 0.900
#&gt; SRR975598     6  0.4118     0.0738 0.396 0.000 0.004 0.000 0.008 0.592
#&gt; SRR975599     6  0.1862     0.6663 0.012 0.000 0.008 0.032 0.016 0.932
#&gt; SRR975600     5  0.4273     0.5849 0.364 0.000 0.008 0.004 0.616 0.008
#&gt; SRR975601     3  0.4000     0.5949 0.192 0.000 0.756 0.032 0.020 0.000
#&gt; SRR975602     1  0.3738     0.5427 0.680 0.000 0.000 0.004 0.004 0.312
#&gt; SRR975603     1  0.6950     0.1047 0.512 0.000 0.124 0.012 0.236 0.116
#&gt; SRR975604     3  0.4668     0.6309 0.048 0.000 0.732 0.004 0.172 0.044
</code></pre>

<script>
$('#tab-ATC-NMF-get-classes-5-a').parent().next().next().hide();
$('#tab-ATC-NMF-get-classes-5-a').click(function(){
  $('#tab-ATC-NMF-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-ATC-NMF-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-ATC-NMF-consensus-heatmap'>
<ul>
<li><a href='#tab-ATC-NMF-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-ATC-NMF-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-ATC-NMF-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-ATC-NMF-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-ATC-NMF-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-NMF-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-consensus-heatmap-1-1.png" alt="plot of chunk tab-ATC-NMF-consensus-heatmap-1"/></p>

</div>
<div id='tab-ATC-NMF-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-consensus-heatmap-2-1.png" alt="plot of chunk tab-ATC-NMF-consensus-heatmap-2"/></p>

</div>
<div id='tab-ATC-NMF-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-consensus-heatmap-3-1.png" alt="plot of chunk tab-ATC-NMF-consensus-heatmap-3"/></p>

</div>
<div id='tab-ATC-NMF-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-consensus-heatmap-4-1.png" alt="plot of chunk tab-ATC-NMF-consensus-heatmap-4"/></p>

</div>
<div id='tab-ATC-NMF-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-consensus-heatmap-5-1.png" alt="plot of chunk tab-ATC-NMF-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-ATC-NMF-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-ATC-NMF-membership-heatmap'>
<ul>
<li><a href='#tab-ATC-NMF-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-ATC-NMF-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-ATC-NMF-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-ATC-NMF-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-ATC-NMF-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-NMF-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-membership-heatmap-1-1.png" alt="plot of chunk tab-ATC-NMF-membership-heatmap-1"/></p>

</div>
<div id='tab-ATC-NMF-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-membership-heatmap-2-1.png" alt="plot of chunk tab-ATC-NMF-membership-heatmap-2"/></p>

</div>
<div id='tab-ATC-NMF-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-membership-heatmap-3-1.png" alt="plot of chunk tab-ATC-NMF-membership-heatmap-3"/></p>

</div>
<div id='tab-ATC-NMF-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-membership-heatmap-4-1.png" alt="plot of chunk tab-ATC-NMF-membership-heatmap-4"/></p>

</div>
<div id='tab-ATC-NMF-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-membership-heatmap-5-1.png" alt="plot of chunk tab-ATC-NMF-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-ATC-NMF-get-signatures' ).tabs();
} );
</script>
<div id='tabs-ATC-NMF-get-signatures'>
<ul>
<li><a href='#tab-ATC-NMF-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-ATC-NMF-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-ATC-NMF-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-ATC-NMF-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-ATC-NMF-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-NMF-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-get-signatures-1-1.png" alt="plot of chunk tab-ATC-NMF-get-signatures-1"/></p>

</div>
<div id='tab-ATC-NMF-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-get-signatures-2-1.png" alt="plot of chunk tab-ATC-NMF-get-signatures-2"/></p>

</div>
<div id='tab-ATC-NMF-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-get-signatures-3-1.png" alt="plot of chunk tab-ATC-NMF-get-signatures-3"/></p>

</div>
<div id='tab-ATC-NMF-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-get-signatures-4-1.png" alt="plot of chunk tab-ATC-NMF-get-signatures-4"/></p>

</div>
<div id='tab-ATC-NMF-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-get-signatures-5-1.png" alt="plot of chunk tab-ATC-NMF-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-ATC-NMF-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-ATC-NMF-get-signatures-no-scale'>
<ul>
<li><a href='#tab-ATC-NMF-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-ATC-NMF-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-ATC-NMF-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-ATC-NMF-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-ATC-NMF-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-NMF-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-ATC-NMF-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-ATC-NMF-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-ATC-NMF-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-ATC-NMF-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-ATC-NMF-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-ATC-NMF-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-ATC-NMF-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-ATC-NMF-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-ATC-NMF-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk ATC-NMF-signature_compare](figure_cola/ATC-NMF-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-ATC-NMF-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-ATC-NMF-dimension-reduction'>
<ul>
<li><a href='#tab-ATC-NMF-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-ATC-NMF-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-ATC-NMF-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-ATC-NMF-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-ATC-NMF-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-NMF-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-dimension-reduction-1-1.png" alt="plot of chunk tab-ATC-NMF-dimension-reduction-1"/></p>

</div>
<div id='tab-ATC-NMF-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-dimension-reduction-2-1.png" alt="plot of chunk tab-ATC-NMF-dimension-reduction-2"/></p>

</div>
<div id='tab-ATC-NMF-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-dimension-reduction-3-1.png" alt="plot of chunk tab-ATC-NMF-dimension-reduction-3"/></p>

</div>
<div id='tab-ATC-NMF-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-dimension-reduction-4-1.png" alt="plot of chunk tab-ATC-NMF-dimension-reduction-4"/></p>

</div>
<div id='tab-ATC-NMF-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-dimension-reduction-5-1.png" alt="plot of chunk tab-ATC-NMF-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk ATC-NMF-collect-classes](figure_cola/ATC-NMF-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

## Session info


```r
sessionInfo()
```

```
#> R version 3.6.0 (2019-04-26)
#> Platform: x86_64-pc-linux-gnu (64-bit)
#> Running under: CentOS Linux 7 (Core)
#> 
#> Matrix products: default
#> BLAS:   /usr/lib64/libblas.so.3.4.2
#> LAPACK: /usr/lib64/liblapack.so.3.4.2
#> 
#> locale:
#>  [1] LC_CTYPE=en_GB.UTF-8       LC_NUMERIC=C               LC_TIME=en_GB.UTF-8       
#>  [4] LC_COLLATE=en_GB.UTF-8     LC_MONETARY=en_GB.UTF-8    LC_MESSAGES=en_GB.UTF-8   
#>  [7] LC_PAPER=en_GB.UTF-8       LC_NAME=C                  LC_ADDRESS=C              
#> [10] LC_TELEPHONE=C             LC_MEASUREMENT=en_GB.UTF-8 LC_IDENTIFICATION=C       
#> 
#> attached base packages:
#> [1] grid      stats     graphics  grDevices utils     datasets  methods   base     
#> 
#> other attached packages:
#> [1] genefilter_1.66.0    ComplexHeatmap_2.3.1 markdown_1.1         knitr_1.26          
#> [5] GetoptLong_0.1.7     cola_1.3.2          
#> 
#> loaded via a namespace (and not attached):
#>  [1] circlize_0.4.8       shape_1.4.4          xfun_0.11            slam_0.1-46         
#>  [5] lattice_0.20-38      splines_3.6.0        colorspace_1.4-1     vctrs_0.2.0         
#>  [9] stats4_3.6.0         blob_1.2.0           XML_3.98-1.20        survival_2.44-1.1   
#> [13] rlang_0.4.2          pillar_1.4.2         DBI_1.0.0            BiocGenerics_0.30.0 
#> [17] bit64_0.9-7          RColorBrewer_1.1-2   matrixStats_0.55.0   stringr_1.4.0       
#> [21] GlobalOptions_0.1.1  evaluate_0.14        memoise_1.1.0        Biobase_2.44.0      
#> [25] IRanges_2.18.3       parallel_3.6.0       AnnotationDbi_1.46.1 highr_0.8           
#> [29] Rcpp_1.0.3           xtable_1.8-4         backports_1.1.5      S4Vectors_0.22.1    
#> [33] annotate_1.62.0      skmeans_0.2-11       bit_1.1-14           microbenchmark_1.4-7
#> [37] brew_1.0-6           impute_1.58.0        rjson_0.2.20         png_0.1-7           
#> [41] digest_0.6.23        stringi_1.4.3        polyclip_1.10-0      clue_0.3-57         
#> [45] tools_3.6.0          bitops_1.0-6         magrittr_1.5         eulerr_6.0.0        
#> [49] RCurl_1.95-4.12      RSQLite_2.1.4        tibble_2.1.3         cluster_2.1.0       
#> [53] crayon_1.3.4         pkgconfig_2.0.3      zeallot_0.1.0        Matrix_1.2-17       
#> [57] xml2_1.2.2           httr_1.4.1           R6_2.4.1             mclust_5.4.5        
#> [61] compiler_3.6.0
```


