# stock-index-kpi-with-code
from datetime import date
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
%matplotlib inline
from pandas.plotting import scatter_matrix
pf=pd.read_csv('/content/project file 2 - Sheet1 (5).csv')
#pf = pf.replace(r'^\s*$', np.nan, regex=True)
pf.set_index("DATE", inplace=True)
#CAGR RATIOS
print(pf.head())
p0=3480;p1=2721;p2=1589;p3=999
init=1000
t0=4;t1=3;t2=2;t3=1
CAGR0=(((p0/init)**(1/t0))-1)*100
CAGR1=(((p1/init)**(1/t1))-1)*100
CAGR2=(((p2/init)**(1/t2))-1)*100
CAGR3=(((p3/init)**(1/t3))-1)*100
print('1.0 CUMULATIVE ANNUAL GROWTH RETURN FROM 2018 TO 2022 IS ',CAGR0,"%")
print('1.1 CUMULATIVE ANNUAL GROWTH RETURN FROM 2018 TO 2021 IS ',CAGR1,"%")
print('1.2 CUMULATIVE ANNUAL GROWTH RETURN FROM 2018 TO 202O IS ',CAGR2,"%")
print('1.3 CUMULATIVE ANNUAL GROWTH RETURN FROM 2018 TO 2019 IS ',CAGR3,"%")
#MAX DRAWDOWN
pf['Peak'] = pf['IPRICE'].cummax()
pf['Drawdown'] = (pf['Peak']-pf['IPRICE'])/pf['Peak']
print(pf.head())
print('Maximum Drawdown in pf is ', pf['Drawdown'].max())
#sharpe ratio
pf['Return'] = np.log(pf['IPRICE']) - np.log(pf['IPRICE'].shift(1))
dailyr = pf['Return'].dropna()
print(dailyr.head())
print('Daily Sharpe Ratio is ', dailyr.mean()/dailyr.std(ddof=1))
print('Yearly Sharpe Ratio is ', (252**0.5)*dailyr.mean()/dailyr.std(ddof=1))