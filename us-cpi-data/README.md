## Import in R using the following code

```{r}
cpi_file_url <- "https://raw.githubusercontent.com/sureshlazaruspaul/misc-practice-datasets/main/us-cpi-data/cpi.txt"

cpi_data <- read.table(cpi_file_url, header = TRUE, sep = "|")
```

### Some charts

![Figure 1](https://github.com/sureshlazaruspaul/misc-practice-datasets/blob/main/us-cpi-data/cpi-trend.png)

- Code that produces the above ggplot graph is shown below:
  - https://raw.githubusercontent.com/sureshlazaruspaul/misc-practice-datasets/main/us-cpi-data/cpi-trend-graph.R





## Import in Stata using the following code

```{stata}
local cpi_file_url = "https://raw.githubusercontent.com/sureshlazaruspaul/misc-practice-datasets/main/us-cpi-data/cpi.txt"

import delimited `cpi_file_url', delim("|", collapse) clear
```





## Import in SAS using the following code

```{sas}
filename cpi_data temp;

/* fetch data from github */

proc http
  url = "https://raw.githubusercontent.com/sureshlazaruspaul/misc-practice-datasets/main/us-cpi-data/cpi.txt"
  method = "GET"
  out = cpi_data;
run;

/* import to a SAS data set */

proc import file = cpi_data
  out=work.cpi_data dbms = dlm replace;
  delimiter = "|";
  getnames = yes;
run;
```
