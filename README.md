# Python Sales Analysis

## Key Objectives
Companies involved in online sales or running e-commerce websites aim to maximize their sales results by determining what their customers need exactly. The sales dataset will be analyzed to find out the time of the day that has the highest customer activity in terms of transactions. Using Python Pandas and Matplotlib to analyze the sales dataset, we can gain useful insights into the busiest times (hours) of the day.

### Dataset Link : https://raw.githubusercontent.com/PlainChild/Python-Sales-Analysis/refs/heads/main/Order_details(masked).csv


## Workflow 
1. Import all necessary library (panda, numpy, and Matplotlib).

        import numpy as np
        import pandas as pd
        import matplotlib.pyplot as plt

2. Import the dataset.

        df = pd.read_csv('https://raw.githubusercontent.com/PlainChild/Python-Sales-Analysis/refs/heads/main/Order_details(masked).csv')
3. Data cleaning.
- Dataset information

        df.info()
- Data missing (there is no data missing)

        df.isna().sum()
- Data duplication (there is data duplication)

        df[df.duplicated()]
- Change 'Transacation Date' data types from string into datetime with format Year-Month-Day, not Year-Day-Month (So we can extract the hour of transactions)

        df['Transaction Date'] = pd.to_datetime(df['Transaction Date'], dayfirst=True)
4. Create new column 'Hour' to show the hour time the transaction happens

        df['Hour'] = (df['Transaction Date']).dt.hour
![Image](https://github.com/user-attachments/assets/a0d98efb-07a4-4d2c-be13-c1726de7863e)
5. Count the frequency of transactions on that hour.

        busyhour = df['Hour'].value_counts()
![Image](https://github.com/user-attachments/assets/6937ae05-d60d-42d6-ab2b-82dd1afd615e)
6. Create the data visualization
- Create the X-axis data (variable filled with index based on the hour in a day, 0-23)

        busyhour2 = []
                for i in range(0,23):
                busyhour2.append(i)
- Create the Y-axis data (only sort the index of busyhour since it was sort by descending, not by index)

        busyhour1 = busyhour.sort_index()

- Create bar chart

        plt.figure(figsize=(12, 6)) #Size of the chart
        plt.title('Sales Per Hour', #Title of the chart
                fontdict={'fontname': 'monospace', 'fontsize': 30}, y=1.05) #Font style
        plt.ylabel("Number Of Purchases", fontsize=18, labelpad=20) # Label on Y-axis
        plt.xlabel("Hour", fontsize=18, labelpad=20) # Label on X-axis
        plt.bar(busyhour2, busyhour1) #Type of the chart
        plt.grid() # Grid lines on the chart
        plt.show()
![Image](https://github.com/user-attachments/assets/de86cb9b-7072-449d-a42e-a1a2d5900b04)
## Insights & Findings
The line chart shows that sales are low in the morning, and starting to peak at high noon. And also, it is usually peak during late night hours. Therefore, it is advisable to hold a product promotion during that time specifically.

