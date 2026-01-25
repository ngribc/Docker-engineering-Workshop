#!/usr/bin/env python
# coding: utf-8

# In[1]:

import pandas as pd
from sqlalchemy import create_engine
from tqdm.auto import tqdm

# In[2]:


prefix = 'https://github.com/DataTalksClub/nyc-tlc-data/releases/download/yellow/'
url = f'{prefix}/yellow_tripdata_{year}-{month:02d}.csv.gz'
url


# In[3]:


'https://github.com/DataTalksClub/nyc-tlc-data/releases/download/yellow/'


# In[4]:


dtype = {
    "VendorID": "Int64",
    "passenger_count": "Int64",
    "trip_distance": "float64",
    "RatecodeID": "Int64",
    "store_and_fwd_flag": "string",
    "PULocationID": "Int64",
    "DOLocationID": "Int64",
    "payment_type": "Int64",
    "fare_amount": "float64",
    "extra": "float64",
    "mta_tax": "float64",
    "tip_amount": "float64",
    "tolls_amount": "float64",
    "improvement_surcharge": "float64",
    "total_amount": "float64",
    "congestion_surcharge": "float64"
}

parse_dates = [
    "tpep_pickup_datetime",
    "tpep_dropoff_datetime"
]

df = pd.read_csv(
    prefix + '/yellow_tripdata_2021-01.csv.gz',
    nrows=100,
    dtype=dtype,
    parse_dates=parse_dates
)


# In[5]:


df = pd.read_csv(url)(
    url,
    nrows=100,
    dtype=dtype,
    parse_dates=parse_dates,
)


# In[6]:


# Display first rows
df.head()


# In[7]:


len(df)


# In[8]:


df


# In[9]:


df['VendorID']


# In[10]:


df['tpep_pickup_datetime']


# In[13]:


# Display first rows
df.head()


# In[11]:


# Check data types
df.dtypes


# In[12]:


# Check data shape
df.shape


# In[14]:


get_ipython().system('uv add sqlalchemy')


# In[15]:


get_ipython().system('uv add psycopg2-binary')


# In[119]:


#Create engine

engine = create_engine('postgresql://{pg_user}:{pg_pass}@{pg_host}:{5432}/{pg_db}')


# In[120]:


df.head(0)


# In[137]:


# Get DDL schema for the database:
print(pd.io.sql.get_schema(df, name='yellow_taxi_data', con=engine))


# In[138]:


#Create the table:
df.head(n=0).to_sql(name='yellow_taxi_data', con=engine, if_exists='replace')


# In[145]:


#Iterate over it:
for df_chunk in df_iter:
    print(len(df_chunk))


# In[140]:

    def run():
        pg_user = 'root'
        pg_pass= 'root'
        pg_host= 'localhost'
        pg_port= '5432'
        pg_db= 'ny_taxi'
        year= 2021
        month=1
        chunksize = 100000
    )
    first = True    
    for df_chunk in tqdm(df_iter):
        df_chunk.to_sql(name='yellow_taxi_data', con=engine, if_exists='append')
 
#We don't want to insert all the data at once. Let's do it in batches and use an iterator for that:
df_iter = pd.read_csv(
    url,
    dtype=dtype,
    parse_dates=parse_dates,
    iterator=True,
    chunksize=100000,
)


# In[141]:


#Add tqdm to see progress:
get_ipython().system('uv add tqdm')


# In[142]:


#Put it around the iterable:
from tqdm.auto import tqdm


# In[ ]:


#Inserting data:
df_chunk.to_sql(name='yellow_taxi_data', con=engine, if_exists='append')


# In[143]:


#for df_chunk in tqdm(df_iter):
#        df_chunk.to_sql(name='yellow_taxi_data', con=engine, if_exists='append')


# In[ ]:
