# Data for the ICSE 2016 "Mining Sandboxes" publication

A repository containing input and output data from the ICSE 2016 "Mining Sandboxes" paper, as well as instructions on how to reproduce the results as faithfully as possible.

Note: this repository **does not contain tool source code**, only data. To get sources, please see the relevant link below.

Contact: jamrozik@st.cs.uni-saarland.de

Useful links:
* [Download the "Mining Sandboxes" publication](http://www.boxmate.org/files/boxmate-preprint.pdf)
* ["Mining Sandboxes" at the ACM Digital Library](http://dl.acm.org/citation.cfm?id=2884782)
* [Website of the tool used in the publication, BoxMate](http://www.boxmate.org)
* [GitHub repository with source code of BoxMate](https://github.com/konrad-jamrozik/droidmate)

## Publication data

All the experiments results data discussed in the publication is present in this repository. Sections below give the exact relationships between the figures in the publication and the data. All saturation charts on figures in the publication have been generated using [PGFPlots](http://pgfplots.sourceforge.net/). 

### Figure 2 data

The chart was generated from the file [saturation_chart-3.5h-com.snapchat.android.txt](results/saturation charts data snapchat 4.1.07 vs 5.0.34.6 3.5h/saturation_chart-3.5h-com.snapchat.android.txt), third column, having header `droidmate-run:com.snapchat.android-4.1.07`.

### Figure 3 data

The data is interpretation of the last two tables (starting at lines 96 and 115) from the file TODO. Note that the interpretation required additional manual effort to account for the imprecision of the obtained logs. What we did manually:

* Some API calls were classified as `background` because they originated from a background thread. However, the thread was started because of an user action that is described in the figure. 
* Noisy API calls have been  collapsed, like multiple calls to `getLastKnownLocation()`.
* Finally, we manually accounted for imprecise API call log time stamps. The imprecision was caused by reading the API call logs from logcat, which output the logs with various delays, possibly making them being classified to wrong user actions.
