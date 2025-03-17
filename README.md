# EDA_With_Python
## Step-wise Working
import pandas as pd

import pandas as pd

df = pd.read_excel("flight_price (1).xlsx", engine="openpyxl")
print(df)



df.head()



df.tail()

# get the basic info



df.info()


df.describe()


df.head()



#feature Engineering
df['Date']=df['Date_of_Journey'].str.split('/').str[0]
df['Month']=df['Date_of_Journey'].str.split('/').str[1]
df['Year']=df['Date_of_Journey'].str.split('/').str[2]




df.head()






df.info()





df['Date']=df['Date'].astype(int)
df['Month']=df['Month'].astype(int)
df['Year']=df['Year'].astype(int)







df.info()






df.drop('Date_of_Journey',axis=1,inplace=True)







df.head()







df['Arrival_Time']=df['Arrival_Time'].apply(lambda x:x.split(' ')[0])








df['Arrival_hour']=df['Arrival_Time'].str.split(':').str[0]
df['Arrival_min']=df['Arrival_Time'].str.split(':').str[1]





df.head()








df['Arrival_hour']=df['Arrival_hour'].astype(int)
df['Arrival_min']=df['Arrival_min'].astype(int)



df.drop('Arrival_Time',axis=1,inplace=True)



df.head()




df['Departure_hour']=df['Dep_Time'].str.split(':').str[0]
df['Departure_min']=df['Dep_Time'].str.split(':').str[1]





df.head()




df.info()








df['Departure_hour']=df['Departure_hour'].astype(int)
df['Departure_min']=df['Departure_min'].astype(int)




df.info()






df.drop('Dep_Time',axis=1,inplace=True)





df.head(2)






df['Total_Stops'].unique()





import numpy as np






df['Total_Stops']=df['Total_Stops'].map({'non-stop': 0, '1 stop': 1, '2 stops': 2, '3 stops': 3, '4 stops': 4, np.nan: 1 })





df[df['Total_Stops'].isnull()]




df.drop('Route',axis=1,inplace=True)





df.head(10)





df['Duration_hour']=df['Duration'].str.split(':').str[0]
df['Duration_min']=df['Duration'].str.split(':').str[1]






df['Duration_hour']=df['Duration'].apply(lambda x:x.split(' ')[0])






df.head(2)






df.drop('Duration',axis=1,inplace=True)





df.head(2)





df['Airline'].unique()




df['Source'].unique()

df['Additional_Info'].unique()

from sklearn.preprocessing import OneHotEncoder

encoder=OneHotEncoder()

encoder.fit_transform(df[['Airline' , 'Source', 'Destination']]).toarray()

pd.DataFrame(encoder.fit_transform(df[['Airline' , 'Source', 'Destination']]).toarray(), columns=encoder.get_feature_names_out())
