# web-scraping
Module 11 Challenge Repo

My final submission files are titled "part_1_mars_news_final.ipynb" and "part_2_mars_weather_final.ipynb." 

## References

### AI Xpert Assistance

I utilized the AI Xpert Learning Assistant for a few Pandas function reminders instead of digging through prior weeks' work. As an example, here is an exchange to refresh my memory on the syntax for renaming a column:

--------


Xpert User Logo

If you are creating a Pandas DataFrame using a list of rows, you can specify the column names separately when creating the DataFrame. Here's an example of how to create a DataFrame from a list of rows while defining the column names:

import pandas as pd

# Define the list of rows
rows = [
    ['Alice', 25, 'New York'],
    ['Bob', 30, 'Los Angeles'],
    ['Charlie', 35, 'Chicago']
]

# Define the column names
columns = ['Name', 'Age', 'City']

# Create the DataFrame with defined columns
df = pd.DataFrame(rows, columns=columns)

# Print the DataFrame
print(df)


In this code snippet:


    We import Pandas as pd.

    We define a list of rows rows, where each element is a list representing a row of data.

    We define a list columns containing the column names ('Name', 'Age', 'City').

    We create a DataFrame df by passing the rows list and the columns list to the pd.DataFrame() constructor. This will create a DataFrame with the specified columns and data from the rows.

    Finally, we print the DataFrame df to see the data organized into columns as defined.


By specifying the columns parameter when creating the DataFrame, you can ensure that the DataFrame is created with the specified column names even when using a list of rows to populate the data.

Student User Logo
how do i change a single column's datatype in a pandas dataframe/
Xpert User Logo

To change the datatype of a single column in a Pandas DataFrame, you can use the astype() method on the specific column you want to convert. Here's an example of how to change the datatype of a single column in a Pandas DataFrame:

import pandas as pd

# Create a sample DataFrame
data = {'A': [1, 2, 3], 'B': ['4', '5', '6']}
df = pd.DataFrame(data)

# Print the DataFrame before datatype conversion
print("DataFrame before datatype conversion:")
print(df)

# Convert column 'B' to integer datatype
df['B'] = df['B'].astype(int)

# Print the DataFrame after datatype conversion
print("\nDataFrame after converting column 'B' to integer datatype:")
print(df)


In this code snippet:


    We import Pandas as pd.

    We create a sample DataFrame df with columns 'A' (integers) and 'B' (strings).

    We print the DataFrame before converting the datatype of column 'B'.

    We use the astype() method to convert column 'B' from string to integer datatype.

    We print the DataFrame after converting the datatype of column 'B' to see the changes.


By using df['B'] = df['B'].astype(int), you can change the datatype of column 'B' to integer. You can replace int with other datatypes like float, str, etc., depending on the desired conversion.

-------

I also had an extensive back-and-forth with the AI Assistant regarding plots, as I was initially having problems getting my graphs to plot correctly using the plt method. I have pasted an excerpt of the text:

--------

Student User Logo
I have the same code and it is showing the same graph as this, which it shouldn't: plt.bar(avg_low.index, avg_low.values, width=0.5) ax = plt.gca() ax.set_xlabel("month") ax.set_ylabel("Temperature in Celsius") ax.set_title("Average Temperature by Month") plt.show()
Xpert User Logo

If you are still seeing the same graph even after sorting the values and the index, there might be another factor affecting the order of the plot. One common issue could be related to the data types of the index values. If the index values are stored as strings instead of being sorted as categorical variables, the plot might not display in the expected order.

To address this issue, you can convert the index to categorical data before sorting and plotting the bar graph. Here's how you can do it:

import matplotlib.pyplot as plt

# Convert the index to categorical data
avg_low.index = pd.Categorical(avg_low.index, categories=avg_low.index, ordered=True)

# Sort the values in ascending order
sorted_averages = avg_low.sort_index()

# Create a bar graph with sorted values and index
plt.bar(sorted_averages.index, sorted_averages.values, width=0.5)

# Set the x-axis label
plt.xlabel("Month")

# Set the y-axis label
plt.ylabel("Temperature in Celsius")

# Set the title
plt.title("Average Temperature by Month")

# Show the plot
plt.show()


In this updated code snippet:


    We convert the index of the avg_low DataFrame to categorical data using pd.Categorical() to ensure proper sorting.

    Then, we sort the values based on the sorted index.

    Finally, we create the bar graph with the sorted values and index, and display it with the correct order.


By converting the index to categorical data before sorting and plotting the bar graph, you should see the plot reflecting the correct order of the average temperatures by month.

Student User Logo
It is still showing the plot in the wrong order
Xpert User Logo

If the plot is still not showing in the correct order even after converting the index to categorical data and sorting it, there might be another factor affecting the order of the plot. One possibility is that the index values are being treated as strings instead of categorical data during the plotting process.

To ensure that the index is treated as categorical data when plotting the bar graph, you can explicitly specify the x-axis tick labels using the plt.xticks() function. Here's how you can modify your code to include this step:

import matplotlib.pyplot as plt

# Convert the index to categorical data
avg_low.index = pd.Categorical(avg_low.index, categories=avg_low.index, ordered=True)

# Sort the values in ascending order
sorted_averages = avg_low.sort_index()

# Create a bar graph with sorted values and index
plt.bar(range(len(sorted_averages)), sorted_averages.values, width=0.5)

# Set the x-axis tick labels to the sorted index values
plt.xticks(range(len(sorted_averages)), sorted_averages.index)

# Set the x-axis label
plt.xlabel("Month")

# Set the y-axis label
plt.ylabel("Temperature in Celsius")

# Set the title
plt.title("Average Temperature by Month")

# Show the plot
plt.show()


In this updated code snippet:


    We use plt.xticks() to explicitly set the x-axis tick labels to the sorted index values.

    By setting the x-axis tick labels explicitly, we ensure that the plot displays the bars in the correct order based on the sorted index values.


By including this step, the bar graph should now display the average temperatures by month in the correct order.

Student User Logo
how can i set xticks using ax?
Xpert User Logo

To set x-axis tick labels using the axes object (ax) in Matplotlib, you can use the set_xticks() and set_xticklabels() methods of the axes object. Here's how you can modify your code to set x-axis tick labels using the axes object:

import matplotlib.pyplot as plt

# Convert the index to categorical data
avg_low.index = pd.Categorical(avg_low.index, categories=avg_low.index, ordered=True)

# Sort the values in ascending order
sorted_averages = avg_low.sort_index()

# Create a bar graph with sorted values and index
plt.bar(range(len(sorted_averages)), sorted_averages.values, width=0.5)

# Get the current axes
ax = plt.gca()

# Set the x-axis tick locations
ax.set_xticks(range(len(sorted_averages)))

# Set the x-axis tick labels to the sorted index values
ax.set_xticklabels(sorted_averages.index)

# Set the x-axis label
ax.set_xlabel("Month")

# Set the y-axis label
ax.set_ylabel("Temperature in Celsius")

# Set the title
ax.set_title("Average Temperature by Month")

# Show the plot
plt.show()


In this code snippet:


    We first get the current axes using plt.gca() and store it in the ax variable.

    We then set the x-axis tick locations using ax.set_xticks() to specify where the ticks should be placed.

    Next, we set the x-axis tick labels to the sorted index values using ax.set_xticklabels().

    By setting the x-axis tick locations and labels using the axes object, you can customize the appearance of the x-axis ticks in your bar graph.


--------

Finally, I received help from my tutor Justin to solve my graph issues - he suggested plotting the dataframe directly using the Pandas plot function, which entails using dataframe.plot.

This ended up solving the issues I was having, so I no longer needed the information obtained from the AI Assistant!