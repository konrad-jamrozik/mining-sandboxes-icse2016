# Data for the ICSE 2016 "Mining Sandboxes" publication

A repository containing input and output data from the ICSE 2016 "Mining Sandboxes" paper, as well as instructions on how to reproduce the results as faithfully as possible.

Note: this repository **does not contain tool source code**, only data. To get sources, please see the relevant link below.

Contact: jamrozik@st.cs.uni-saarland.de

Useful links:
* [Download the "Mining Sandboxes" publication](http://www.boxmate.org/files/boxmate-camera-ready.pdf)
* ["Mining Sandboxes" at the ACM Digital Library](http://dl.acm.org/citation.cfm?id=2884782)
* [Website of the tool used in the publication, BoxMate](http://www.boxmate.org)
* [GitHub repository with source code of BoxMate](https://github.com/konrad-jamrozik/droidmate)

## Publication data

All the experiments results data discussed in the publication is present in this repository. Sections below give the exact relationships between the figures in the publication and the data. All saturation charts on figures in the publication have been generated using [PGFPlots](http://pgfplots.sourceforge.net/). 

### Full API list

The full list of monitored AppGuard API calls is given in [AppGuard_apis_list.txt](AppGuard_apis_list.txt).

### Figure 2 data

The chart was generated from the file [saturation_chart-3.5h-com.snapchat.android.txt](results/saturation charts data snapchat 4.1.07 vs 5.0.34.6 3.5h/saturation_chart-3.5h-com.snapchat.android.txt), first and third columns. The third column has header `droidmate-run:com.snapchat.android-4.1.07`.

### Figure 3 data

The data is interpretation of the last two tables (starting at lines 96 and 115) from the file [summary-com.snapchat.android.txt](results/summaries for snapchat 4.1.07 vs 5.0.34.6 comparison/summary-com.snapchat.android.txt). Note that the interpretation required additional manual effort to account for the imprecision of the obtained logs. What we did manually:

* Some API calls were classified as `background` because they originated from a background thread. However, the thread was started because of an user action that is described in the figure. 
* Noisy API calls have been collapsed, like multiple calls to `getLastKnownLocation()`.
* Finally, we manually accounted for imprecise API call log time stamps. The imprecision was caused by reading the API call logs from logcat, which output the logs with various delays, possibly making them being classified to wrong user actions.

### Figure 5 data

The charts were generated from files in the [saturation charts data 12 apps 2h](results/saturation charts data 12 apps 2h) directory.

### Table 2 data

The data is interpretation of the tables from files in the [summaries for 18 uia tcs vs 2h runs (3.5h for snapchat)](results/summaries for 18 uia tcs vs 2h runs (3.5h for snapchat)) directory. The same kind of manual interpretation procedure has been applied as in case of [Figure 3 data](#figure-3-data). In addition, if consequitve sequence of previously unknown API calls has been observed, we assume user would be present with only one confirmation, as counted on the table.

### Figure 7 data

The chart was generated from the file [saturation_chart-3.5h-perEvent-com.snapchat.android.txt](results/saturation charts data snapchat 4.1.07 vs 5.0.34.6 3.5h/saturation_chart-3.5h-perEvent-com.snapchat.android.txt), first and third columns. The third column has header `droidmate-run:com.snapchat.android-4.1.07`.

### Figure 8 data

The charts were generated from files in the [saturation charts data 12 apps 2h per event](results/saturation charts data 12 apps 2h per event) directory.

### Figure 9 data

The chart was generated from the file [saturation_chart-3.5h-com.snapchat.android.txt](results/saturation charts data snapchat 4.1.07 vs 5.0.34.6 3.5h/saturation_chart-3.5h-com.snapchat.android.txt), all columns. The red line, i.e. snapchat 5.0.34.6, is based on first and second column. The blue line, i.e. snapchat 4.1.07, is based on first and third column. Note that the blue line is equivalent to the blue line on [Figure 2](#figure-2-data).

### Section 6 detailed analysis

The detailed analysis of API calls difference between Snapchat 4.1.07 and Snapchat 5.0.34.6 done in section _6. ASSESSING SANDBOXES_ is done based on the data given in [summary-com.snapchat.android.txt](results/summaries for snapchat 4.1.07 vs 5.0.34.6 comparison/summary-com.snapchat.android.txt). The same kind of manual interpretation procedure has been applied as in case of [Figure 3 data](#figure-3-data). 

## Reproducing publication data

Please see [howto_reproduce.md](howto_reproduce.md)
