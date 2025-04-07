# 5--2
5주차 과제-2


(첫 번째 과제)

import pandas as pd
import numpy as np

data = {'2007': [7.71, 19.02, 10.47, 10.87, 4.04, 2.01],
        '2008': [7.95, 17.71, 8.45, 10.83, 3.78, 2.05],
        '2009': [11.96, 15.00, 5.58, 7.55, 3.45, 1.50],
        '2010': [15.84, 16.70, 7.60, 9.09, 4.20, 2.25],
        '2011': [16.33, 17.48, 8.40, 7.88, 4.62, 2.54]}
index = ['China', 'EU', 'US', 'Japan', 'Korea', 'Mexico']
df = pd.DataFrame(data, index=index)

total_row = df.select_dtypes(np.number).sum()
df = pd.concat([df, pd.DataFrame(total_row, columns=['Total']).T])

df['Average'] = df.select_dtypes(np.number).mean(axis=1)

print(df)


--> 실행 결과
2007  2008  2009  2010  2011   Total   Average
China   7.71  7.95  11.96  15.84  16.33   59.80  11.960
EU     19.02  17.71  15.00  16.70  17.48   85.91  17.182
US     10.47  8.45   5.58   7.60   8.40   40.50   8.100
Japan  10.87  10.83   7.55   9.09   7.88   46.22   9.244
Korea   4.04   3.78   3.45   4.20   4.62   20.09   4.018
Mexico  2.01   2.05   1.50   2.25   2.54   10.35   2.070
Total  54.12  50.77  45.04  55.68  57.25  262.86  52.572





(두 번쨰 과제)

import pandas as pd
import numpy as np
import matplotlib.pyplot as plt

weather_file = 'your_weather_data.csv'  

weather = pd.read_csv(weather_file, encoding='CP949')
weather['month'] = pd.DatetimeIndex(weather['일시']).month

monthly = [None for x in range(12)]  
monthly_wind = [[] for x in range(12)]

for i in range(12):
    monthly[i] = weather[weather['month'] == i + 1]
    monthly_wind[i] = monthly[i]['평균풍속'].mean()  

months = np.arange(1, 13)
plt.bar(months, monthly_wind, color='skyblue') 
plt.xlabel('Month')
plt.ylabel('Average Wind Speed (m/s)') 
plt.title('Monthly Average Wind Speed') 
plt.grid(axis='y', linestyle='--') 
plt.xticks(months)
plt.tight_layout() 
plt.show()


--> 실행 결과

[그래프 출력]
(가로축: Month (1, 2, 3, ..., 12), 세로축: Average Wind Speed (m/s))
각 월별로 평균 풍속을 나타내는 하늘색 막대 그래프
