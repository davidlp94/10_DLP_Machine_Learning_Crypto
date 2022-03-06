# SQL ETF Analyzer
## Introduction
An application designed to analyze a hypothethical FinTech ETF using SQL and database queries. This analysis involves the overall returns of both the entire ETF as well as each individual asset.

---

## Technologies

The following technology/software was used for this application:


-Python 3.7.11 (Programming language)

    Imported Python Libraries/Packages:
    
    -import pandas as pd
    
    -import hvplot.pandas
    
    -from pathlib import Path
    
    -import sqlalchemy as sql
    
-JupyterLab

-Git version 2.34.11.windows.1

-Windows 10 Operating System

-Voila

---

## Installation Guide

To install this application on your machine, download (or clone using http link) all files contained in this repository davidlp94/07_DLP_SQL_ETF_Analyzer.

Next, open GitBash (terminal for MacOS), change your directory to the davidlp94/07_DLP_SQL_ETF_Analyzer, open JupyterLab in a dev environment and open/run the etf_analyzer.ipynb file.

---

## Main Source Code
(Please refer to Jupyter Notebook for full source-code)
## Analyze the ETF Portfolio

The first step in this application is to establish a database connection string and query the ETF assets into a DataBase using SQL for further analysis.

```
import numpy as np
import pandas as pd
import hvplot.pandas
import sqlalchemy as sql
from pathlib import Path

database_connection_string = 'sqlite:///etf.db'
engine = sql.create_engine(database_connection_string)

query = """
SELECT GDOT.time, GDOT.daily_returns, GS.daily_returns, PYPL.daily_returns, SQ.daily_returns
FROM GDOT
INNER JOIN GS
ON GDOT.time = GS.time
INNER JOIN PYPL
ON GS.time = PYPL.time
INNER JOIN SQ
ON PYPL.time = SQ.time
"""

etf_portfolio = pd.read_sql_query(query, con=engine)

etf_portfolio.columns = ["time", "GDOT_daily_returns", "GS_daily_returns", "PYPL_Daily_returns", "SQ_daily_returns"]
display(etf_portfolio)
```

![image](https://user-images.githubusercontent.com/96163075/154754794-bca18ea1-ea8e-4697-a609-d8b7aff39cae.png)

```
etf_portfolio_returns = etf_portfolio.mean(axis=0)
annualized_etf_portfolio_returns = (etf_portfolio_returns.mean() +1)**252
etf_cumulative_returns = (1+etf_portfolio_returns.mean())**(252*4)

etf_portfolio[["GDOT_cum_return", "GS_cum_return", "PYPL_cum_return", "SQ_cum_return"]] = (etf_portfolio.iloc[:, 1:5]+1).cumprod()
etf_portfolio.hvplot(x="time", y=["GDOT_cum_return", "GS_cum_return", "PYPL_cum_return", "SQ_cum_return"], ylabel="Cumulative Return", \
                    title="Cumulative Return of Assets in the ETF")
                    
etf_portfolio["ETF_cum_return"] = etf_portfolio.iloc[:, 5:9].mean(axis=1)
etf_portfolio.hvplot(x="time", y="ETF_cum_return", ylabel="Cumulative Return", title="Cumulative Return of Entire ETF")                    
```

![image](https://user-images.githubusercontent.com/96163075/154754978-6431ec47-5dcf-4bf4-84d1-d943bb3ce0ab.png)
![image](https://user-images.githubusercontent.com/96163075/154754997-1d75434d-2935-4243-9681-147a060c8459.png)

The above generated plots show the cumulative returns on each ETF asset as well as the entire equally weighted ETF portfolio.

---

## Contributors

David Lee Ping

email: davidleeping@gmail.com

Phone: 570.269.5973

LinkedIn: https://www.linkedin.com/in/david-lee-ping/

---

## License

MIT License

Copyright (c) [2022] [David Lee Ping]

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.


