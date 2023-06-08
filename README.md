<!-- https://github.com/dreampulse/computer-modern-web-font
<head>
  <link rel="stylesheet" type="text/css" href="https://cdn.jsdelivr.net/gh/aaaakshat/cm-web-fonts@latest/fonts.css">
  <style>
    body {
      font-family: "Computer Modern Serif", Typewriter;
    }
  </style>
</head>

 https://stackoverflow.com/questions/71198520/adding-computer-modern-serif-to-jekyll-github-page 
<!--
<head>
    <meta charset="UTF-8" />
    <title>Test</title>
    <link rel="stylesheet" href="/fonts/Serif/cmun-serif.css"></link>
    body {
      font-family: "Computer Modern Serif", Typewriter;
    }
  </style>
</head>  
--> 



# Python code for Aggregate Group-Time Average Treatment Effects 

This code implements the Aggregate Group-Time Average Treatment Effects from the DiD with multiple time periods methodology of Callaway and Sant’Anna (2021).

## Description

I built the Python function for aggte function of the R package (and c++) from [Callaway and Sant’Anna (2021)](https://bcallaway11.github.io/did/index.html). This code is a function to take group-time average treatment effects and aggregate them into a smaller number of parameters.  There are several possible aggregations including "simple", "dynamic", "group", and "calendar.".


## Roadmap

- [x] Aggregate Group-Time Average Treatment Effects function (aggte)
- [x] Child function (compute_aggte)
- [x] Multipler bootstrapping (mboot)
    - [x] Clean and call for bootstrapping (mboot)
    - [x] Call for parallel computing or single computing for multiplier_bootstrap (run_multiplier_bootstrap)
- [x] Bmisc
    - [x] Execute bootstraiping (multiplier_bootstrap)
    - [x] Clean arrays for logical vectors (TorF)
- [x] Utils
    - [x] Compute influence function matrix(wif)
    - [x] Apply influence function for parameters (get_agg_inf_func)
    - [x] Return standard errors (get_se)
    - [x] Print results (AGGTEobj)


## Getting Started

### Executing program

* Download all the folder 
* Paste the path in folder_path
* Select the type of aggregation
    * out =  aggte(out,'simple')
    * out =  aggte(out,'group')
    * out =  aggte(out,'dynamic')
    * out =  aggte(out,'calendar')
* Run the following script
```
import os
import pickle

folder_path = r"" 
os.chdir(folder_path)

from aggte import *

pickle_file = "att_gt_object.pkl"
with open(pickle_file, "rb") as f:
    out = pickle.load(f)
    
out =  aggte(out)

```

## Outcome

### Group aggregation (deafult)
```
Overall summary of ATT's based on group/cohort aggregation:
   ATT Std. Error  [95.0%  Conf. Int.]
-0.031     0.0124 -0.0552      -0.0068 *

Group Effects:
   Group  Estimate  Std. Error   [95.0% Simult.   Conf. Band]
0   2004   -0.0797      0.0291      -0.1437     -0.0158  *
1   2006   -0.0229      0.0171      -0.0605      0.0147
2   2007   -0.0261      0.0165      -0.0624      0.0102
---
Signif. codes: `*' confidence band does not cover 0
Control Group:  Never Treated ,
Anticipation Periods:  0.0
Estimation Method:  Outcome Regression
```
### Simple aggregation
```
  ATT Std. Error  [95.0%  Conf. Int.]  
-0.04     0.0122 -0.0638      -0.0161 *

---
Signif. codes: `*' confidence band does not cover 0
Control Group:  Never Treated , 
Anticipation Periods:  0.0
Estimation Method:  Outcome Regression
```
### Dynamic aggregation
```
Overall summary of ATT's based on event-study/dynamic aggregation:
    ATT Std. Error  [95.0%  Conf. Int.]  
-0.0772     0.0204 -0.1173      -0.0372 *

Dynamic Effects:
   Event time  Estimate  Std. Error  [95.0% Simult.   Conf. Band]   
0          -3    0.0305      0.0152     -0.0080      0.0690   
1          -2   -0.0006      0.0128     -0.0329      0.0318   
2          -1   -0.0245      0.0141     -0.0600      0.0111   
3           0   -0.0199      0.0127     -0.0519      0.0120   
4           1   -0.0510      0.0167     -0.0931     -0.0088  *
5           2   -0.1373      0.0393     -0.2364     -0.0381  *
6           3   -0.1008      0.0339     -0.1864     -0.0152  *
---
Signif. codes: `*' confidence band does not cover 0
Control Group:  Never Treated , 
Anticipation Periods:  0.0
Estimation Method:  Outcome Regression
```

## References


[Callaway, Brantly and Pedro H.C. Sant’Anna. “Difference-in-Differences with Multiple Time Periods.” Journal of Econometrics, Vol. 225, No. 2, pp. 200-230, 2021.](https://www.sciencedirect.com/science/article/abs/pii/S0304407620303948?via%3Dihub)