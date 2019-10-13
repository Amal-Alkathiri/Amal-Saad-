# Investigate a Dataset (TMDb movie data) Analysis
#Introduction
#This data set contains information about 10,000 movies collected from The Movie Database (TMDb),including user ratings and revenue


# read the data file
#tmdb-movies.csv
mdb_df = pd.read_csv('https://d17h27t6h515a5.cloudfront.net/topher/2017/October/59dd1c4c_tmdb-movies/tmdb-movies.csv',encoding = 'latin-1')
mdb_df.head(10)

# get summery of the dataset
mdb_df.info()

# drop any duplicated data
mdb_df.drop_duplicates(inplace = True)
print("droping the dupicate values (rows,columns)",mdb_df.shape)

#remove zero values from (budget & revenue)
budget_revenue_list=['budget', 'revenue']

# replace all value of 0 to NAN 
mdb_df[budget_revenue_list] = mdb_df[budget_revenue_list].replace(0, np.NAN)

#remov all the row which has NAN value in temp_list
mdb_df.dropna(subset = budget_revenue_list, inplace = True)
rows, col =mdb_df.shape
print('the result is {} number of movies'.format(rows-1))


#drop unnecessary data
mdb_df.drop(['homepage','tagline'],axis =1, inplace = True)
print("Drop unnecessary Columns (Rows,Columns) : ",mdb_df.shape)


#min to find index most profit movie
def cal_max(x):
    high_index = mdb_df[x].idxmax()
    high = pd.DataFrame(mdb_df.loc[high_index,:])
    print("the highest"+ x + " : ",mdb_df['original_title'][high_index])
    return pd.concat([high],axis = 1)
cal_max('profit')
