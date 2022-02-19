# CNS Fails to Deliver (FTDs), sourced from SEC

This repo downloads, cleans and processes text file data (laid out as CSVs) from https://www.sec.gov/data/foiadocsfailsdatahtm to make is useable for further analysis.
The data encompasses Failures to Deliver (FTDs) of securities in the U.S. stock market, from 2004 to the present.
The SEC dataset provides the date of the failure, the name and quantity of the security that wasn't delivered, and the closing price on the day of the fail.
The contents of the dataset are millions of rows in 6 columns, and is very cumbersome to analyze over long periods of time in aggregate since it is split up in 100+ files. This repo makes the dataset more accessible by aggregation.


Said data is shown in the documentary series "Gaming Wall Street", for which we built the repo initially.
Another - no relation here - effort to visualize this data is https://sec.report/fails.php , which visualizes historical fail data for individual stocks, but offers no aggregate visualization.
As of early 2022, an average of $3Bn worth of stocks fail to deliver daily; the SEC has further information to the meaning of this data on their above referenced site.


## Instructions

Run the programs in the following order:
1. [download-and-sanitize-cnsfails](./download-and-sanitize-cnsfails.ipynb)
2. [download-symbol-data](./download-symbol-data.ipynb)
3. [process-and-visualize](./process-and-visualize.ipynb)

## Data Quality of the SEC Dataset

We found some broken entries in the files. Those look like OCR scanning issues (e.g. using `|` instead of `!`), which suggests that a portion of the data was submitted to the SEC in the form of paper, and scanned by the commission. Also, the price column is missing many entries in earlier years.

### Missing Price entries

Note from the Website:

> The price field includes the closing price of the security on the previous day as long as the price is available and is greater than one penny. When the price is not available or is less than a penny, the field is filled with a “.”. Even when prices are included in the data, we cannot guarantee that this price matches closing prices available from other sources.

Up to 2007-04 -> almost no price entries
2007-04: 15119 of 55118 prices missing (27.4%)
2009-01: 3232 of 135169 prices missing (2.4%)
2015-01: 951 of 54781 prices missing (1.7%)

### Broken entries

**cnsp_sec_fails_200408.txt**
21 times BAM| ENTMT INC instead of BAM! ENTMT INC
10 times BRAVO| FOODS INTERNATIONAL CP instead of BRAVO! FOODS INTERNATIONAL CP
4 times YUM| BRANDS, INC instead of YUM BRANDS, INC
2 times EZENIA| INC instead of EZENIA! INC

**cnsp_sec_fails_200409.txt**
15 times BAM| ENTMT INC instead of BAM! ENTMT INC
14 times BRAVO| FOODS INTERNATIONAL CP instead of BRAVO! FOODS INTERNATIONAL CP
3 times EZENIA| INC instead of EZENIA! INC

**cnsp_sec_fails_200410.txt**
20 times BAM| ENTMT INC instead of BAM! ENTMT INC
1 time BRAVO| FOODS INTERNATIONAL CP instead of BRAVO! FOODS INTERNATIONAL CP

**cnsp_sec_fails_200411.txt**
18 times BAM| ENTMT INC instead of BAM! ENTMT INC
2 times BRAVO| FOODS INTERNATIONAL CP instead of BRAVO! FOODS INTERNATIONAL CP
1 times EZENIA| INC instead of EZENIA! INC

**cnsp_sec_fails_200412.txt**
22 times BAM| ENTMT INC instead of BAM! ENTMT INC
14 times BRAVO| FOODS INTERNATIONAL CP instead of BRAVO! FOODS INTERNATIONAL CP
8 times POW| ENTERTAINMENT INC instead of POW! ENTERTAINMENT INC
6 times MAKEMUSIC| INC NEW instead of MAKEMUSIC! INC NEW

**cnsp_sec_fails_200501.txt**
8 times BAM| ENTMT INC instead of BAM! ENTMT INC
5 times BRAVO| FOODS INTERNATIONAL CP instead of BRAVO! FOODS INTERNATIONAL CP
5 times MAKEMUSIC| INC NEW instead of MAKEMUSIC! INC NEW

**cnsfails202104b.txt**
2 times DMY TECHNOLOGY GROUP INC IV | instead of DMY TECHNOLOGY GROUP INC IV WT
