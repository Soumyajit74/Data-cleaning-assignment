# Data-cleaning-assignment
import pandas as pd
import numpy as np
df = pd.DataFrame({'From_To': ['LoNDon_paris', 'MAdrid_miLAN',
'londON_StockhOlm', 'Budapest_PaRis', 'Brussels_londOn'],
'FlightNumber': [10045, np.nan, 10065, np.nan, 10085],
'RecentDelays': [[23, 47], [], [24, 43, 87], [13], [67, 32]],
'Airline': ['KLM(!)', '<Air France> (12)', '(British Airways. )',
'12. Air France', '"Swiss Air"']})
  
df.head()
df=df.fillna(0.0)
df.dtypes
df['FlightNumber'][1]=10055.0
df['FlightNumber'][3]=10075.0
df['FlightNumber']= df['FlightNumber'].astype(int)
temp=pd.DataFrame()
temp['From']= df['From_To'].str.split('_').str[0]
temp['To'] = df['From_To'].str.split('_').str[1]

temp['From']=temp['From'].str.capitalize()
temp['To']= temp['To'].str.capitalize()
df=df.drop(['From_To'], axis=1)

right = df
left = temp

df1= left.join(right)
df1.head()

delay=pd.DataFrame()
df1[['Delay_1', 'Delay_2', 'Delay_3']]=pd.DataFrame(df1.RecentDelays.tolist())

df1.head()
df1.drop(['RecentDelays'], axis=1)
