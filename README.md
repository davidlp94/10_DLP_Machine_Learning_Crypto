# Crypto Portfolio - Machine Learning
## Introduction
An application designed to apply machine learning (Unsupervised Learning) to historical data on cryptocurrencies to gather cluster data and form a cryptocurrency portfolio.

---

## Technologies

The following technology/software was used for this application:


-Python 3.7.11 (Programming language)

    Imported Python Libraries/Packages:
    
    -import pandas as pd
    
    -import hvplot.pandas
    
    -from pathlib import Path
    
    -from sklearn.cluster import KMeans
    
    -from sklearn.decomposition import PCA
    
    -from sklearn.preprocessing import StandardScaler
    
-JupyterLab

-Git version 2.34.11.windows.1

-Windows 10 Operating System

---

## Installation Guide

To install this application on your machine, download (or clone using http link) all files contained in this repository davidlp94/10_DLP_Machine_Learning_Crypto.

Next, open GitBash (terminal for MacOS), change your directory to the davidlp94/10_DLP_Machine_Learning_Crypto, open JupyterLab in a dev environment and open/run the crypto_investments.ipynb file.

---

## Main Source Code
(Please refer to Jupyter Notebook for full source-code)
## Prepare the Data

The first step in this application is to prepare the data by applying the StandardScaler module to the data to have scaled and uniform data to run K-means algorithm.

```
scaled_data = StandardScaler().fit_transform(df_market_data)

df_market_data_scaled = pd.DataFrame(
    scaled_data,
    columns=df_market_data.columns
)

df_market_data_scaled["coin_id"] = df_market_data.index
df_market_data_scaled = df_market_data_scaled.set_index("coin_id")
```

Next, to find the best value for k, we use the elbow method.

```
k = list(range(1, 11))

inertia = []

for i in k:
    model = KMeans(n_clusters=i, random_state=0)
    model.fit(df_market_data_scaled)
    inertia.append(model.inertia_)

elbow_data = {
    "k": k,
    "inertia": inertia
}

elbow_curve_standard = elbow_df.hvplot.line(x="k", y="inertia", title="Elbow Curve", xticks=k)
```
![image](https://user-images.githubusercontent.com/96163075/156944943-ddeb80b5-a10b-4ffa-8d9f-e2a05d536fab.png)

Based on the above plot, the best value for k=4.

Finally,

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


