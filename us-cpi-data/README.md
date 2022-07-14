## Import in R using the following code

```{r}
cpi_file_url <- "https://raw.githubusercontent.com/sureshlazaruspaul/misc-practice-datasets/main/us-cpi-data/cpi.txt"

cpi_data <- read.table(cpi_file_url, header = TRUE, sep = "|")
```

### Some charts

![Figure 1](https://github.com/sureshlazaruspaul/misc-practice-datasets/blob/main/us-cpi-data/cpi-trend.png)

- Code that produces the above ggplot graph is shown below:

```{r}
library(dplyr)
library(ggplot2)

# import cpi data

cpi_file_url <- "https://raw.githubusercontent.com/sureshlazaruspaul/misc-practice-datasets/main/us-cpi-data/cpi.txt"

cpi_data <- read.table(cpi_file_url, header = TRUE, sep = "|") 

# compute yearly means

cpi_yearly_means <-
  cpi_data %>%
  group_by(YEAR) %>%
  summarise(mean_yearly_cpi = mean(CPI_ANN))

# ggplot - cpi trend over time

cpi_yearly_means %>%
  ggplot(
    aes(
      x = YEAR,
      y = mean_yearly_cpi
    )
  ) +
  geom_point() +
  theme_light() +
  expand_limits(y = 0) +
  labs(
    x = "Year",
    y = "Average Annual CPI",
    title = "CPI over time",
    subtitle = paste(min(cpi_yearly_means$YEAR),
                     "to",
                     max(cpi_yearly_means$YEAR)),
    caption = "Data source: https://www.bls.gov"
  ) +
  geom_hline(yintercept = 100,
             linetype="dashed",
             color = "red") +
  geom_text(x = max(cpi_yearly_means$YEAR) - 5,
            y = 110,
            label = "Base = 100, Base period = 1982-84")
```





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
