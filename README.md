<html lang="vi" style="font-family: Sans-serif;">
<head>
        <meta charset="UTF-8">
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <link rel="icon" type="image/x-icon" href="https://mao-nek.000webhostapp.com/index.html/Nh%C3%B3m%202/logo.png">
        <link rel="stylesheet" type="text/css" href="https://github.com/PhiPhuongUyen/Team-5/blob/main/Group%205.css">
    </head>
    <body>
        <div class="background">
                <div class="navbar">
                    <img src="https://mao-nek.000webhostapp.com/index.html/Nh%C3%B3m%202/logo.png" alt="Logo" class="logo">
                    <nav>
                        <ul id="menu">
                            <li><a href="https://github.com/PhiPhuongUyen/Team-5/blob/main/Nh%C3%B3m%205%20Final.ipynb)">Trang chủ</a></li>
                            <li><a href="https://github.com/PhiPhuongUyen/Team-5/blob/main/Scatter%20chart.ipynb">Scatter chart</a></li>
                            <li><a href="https://github.com/PhiPhuongUyen/Team-5/blob/main/Bar%20chart.ipynb">Bar chart</a></li>
                            <li><a href="https://github.com/PhiPhuongUyen/Team-5/blob/main/Pie%20chart.ipynb">Pie chart</a></li>
                            <li><a href="https://github.com/PhiPhuongUyen/Team-5/blob/main/Pie%20chart.ipynb">Line charrt</a></li>
                            <li><a href="https://github.com/PhiPhuongUyen/Team-5/blob/main/Nh%C3%B3m%205%20Final.ipynb">Python_code_chart</a></li>
                        </ul>
                    </nav>
                </div>
            <div class="content">
                <h2>We are</h2>
                <h1>Group 5</h1>
                <p>Group 5 has six members: Phi Phuong Uyen, Dinh Xuan Lam, Nguyen Quynh Anh, Nguyen Duc Hai, Nguyen Quang Huy, Nguyen Khanh Ly. We are all students of class MAS1, the management and security major of the school of management and business. This is our team web where we will analyze for you "The global football tournament from 1872 to 2023" and through that, we want to show you which team is the strongest team.</p>
            </div>
        </div>
        <div class="section">
            <img src="https://github.com/Mao2003/Mao2003/blob/main/scatterchart.png?raw=true">
            <h>Scatter chart</h>
            <pre class="highlight">
                <code class="python">
                    import plotly.express as px
                    import pandas as pd
                    import matplotlib.pyplot as plt
                    from pandasql import sqldf
                    import numpy as np
                    url = "https://raw.githubusercontent.com/Mao2003/Mao2003/main/results.csv"
                    df= pd.read_csv(url,encoding = 'unicode_escape')
                    pysqldf = lambda q: sqldf(q, globals())
                    df4=pysqldf("SELECT date, home_team, SUM(home_score) AS [s_ht], SUM(away_score) AS [s_at],
                                COUNT(tournament) AS [cnt_t]\
                                FROM df\
                                GROUP BY home_team\
                                ORDER BY cnt_t DESC")
                    print(df4)
                    dfscatters=df4[['s_ht','s_at']]
                    plt.scatter(dfscatters['s_ht'], dfscatters['s_at'], color='orange', s=30, marker='*')

                    plt.ylabel("Away score")
                    plt.xlabel("Home score")
                    plt.title("Relationship between points scored and points conceded")
                    plt.show()
                    
                    
                    The scatterplot chart is used to analyze and compare the scores of the home team and the away team in matches.
                    
                    Each point on the chart represents a match, with the X-axis representing the home team's score and the Y-axis
                    representing the away team's score. By observing the density of points on the chart and the distribution pattern
                    of those points, we can assess the level of correlation between the scores of the home team and the away team.
                    From the chart, we can see that the points do not have a particular shape (such as straight lines or diagonals line).
                    Although they are mostly concentrated towards the bottom, there are still many scattered points throughout the chart
                    that do not follow a specific rule, making it impossible to determine the direction of the points clearly. Therefore,
                    based on the chart, we can conclude that the number of goals scored and the number of losses for the teams do not have
                    a correlation and do not affect each other.
                </code>
            </pre>
        </div>
        <div class="section">
            <img src="https://github.com/PhiPhuongUyen/Team-5/blob/main/379611435_242192875055863_6915571824627483977_n.png?raw=true">
            <h>Bar chart</h>
            <pre class="highlight">
                <code class="python">
                    import plotly.express as px
                    import pandas as pd
                    import matplotlib.pyplot as plt
                    from pandasql import sqldf
                    import numpy as np
                    url = "https://raw.githubusercontent.com/Mao2003/Mao2003/main/results.csv"
                    df= pd.read_csv(url,encoding = 'unicode_escape')
                    pysqldf = lambda q: sqldf(q, globals())
                    df1=pysqldf("SELECT date, home_team, AVG(home_score) AS [avg_hg], AVG(away_score) AS [avg_ac], 
                                COUNT(tournament) AS [cnt_t]\
                                FROM df\
                                GROUP BY home_team\
                                HAVING COUNT(tournament)>5\
                                ORDER BY cnt_t DESC")
                                df2=df1.head(5)
                    categories = df2['home_team']
                    values1 = df2['avg_hg']
                    values2 = df2['avg_ac']
                                
                    bar_width = 0.20
                    x = np.arange(len(categories))
                                
                    plt.bar(x - bar_width/2, values1, bar_width, label='Goal')
                    plt.bar(x + bar_width/2, values2, bar_width, label='Goals conceded')
                                
                    plt.xlabel('TEAM')
                    plt.ylabel('AVERAGE SCORES')
                    plt.title('Average points scored and points conceded of the 5 teams with the highest total matches from 1872')
                                
                    plt.xticks(x, categories)
                    plt.legend()
                    plt.show()
                    
                    
                    The column chart above is the average monthly goals statistics of the five teams with the most total matches from 1872 to September 12, 2023.

                     There are columns here about the number of goals scored and the number of goals lost by the teams, team names, average score, two columns
                     with two different colors for easy distinction. The goals conceded are only around 1.0. goals up to 2.5 This chart allows you to compare
                     the number of goals scored between different teams or players in a specific time frame. You can identify outstanding teams or players with
                     excellent scoring ability. For example, in Brazil and Germany. Depending on your specific goals and the data you have, you can conduct more
                     detailed analysis such as identifying the players who scored the most goals, creating a chart showing changes over time, or comparing performance.
                     scores of teams in different seasons.
                </code>
            </pre>
        </div>
        <div class="section">
            <img src="https://github.com/Mao2003/Mao2003/blob/main/piechart.png?raw=true">
            <h>Pie chart</h>
            <pre class="highlight">
                <code class="python">
                    import plotly.express as px
                    import pandas as pd
                    import matplotlib.pyplot as plt
                    from pandasql import sqldf
                    import numpy as np
                    url = "https://raw.githubusercontent.com/Mao2003/Mao2003/main/results.csv"
                    df= pd.read_csv(url,encoding = 'unicode_escape')
                    pysqldf = lambda q: sqldf(q, globals())
                    df3=pysqldf("SELECT date, COUNT(tournament) AS [cnt_t], tournament\
                                FROM df\
                                WHERE date>2023\
                                GROUP BY tournament\
                                ORDER BY [cnt_t] DESC")

                    labels = df3['tournament']
                    sizes = df3['cnt_t']
                                
                    plt.pie(sizes, autopct='%1.1f%%', pctdistance=1.15)
                    plt.axis('equal')
                    plt.title('Odds of matches by tournament')
                                
                    plt.legend(labels, loc='center left', bbox_to_anchor=(1, 0.5))
                                
                    plt.savefig('pie_chart.png')
                                
                    plt.show()
                    
                    
                    The pie chart shows the distribution rates of different tournaments.

                     Each patch in the chart represents a tournament, and the area of the patch represents the ratio
                     (percentage) of that tournament to the total number of tournaments. By looking at the chart, 
                     you can look at each league's percentage and see which leagues have the largest and smallest percentages.
                     You can determine the most popular tournament by looking at the piece with the largest area in the chart.
                     The slice representing this league has the highest percentage, showing that that league has a larger number
                     of teams than the other leagues in the data set. By comparing the area of the pieces in the chart, you can
                     see the difference in distribution between tournaments. Larger pieces represent tournaments with more numbers,
                     while smaller pieces represent tournaments with fewer numbers.
                </code>
            </pre>
        </div>
        <div class="section">
            <img src="https://github.com/Mao2003/Mao2003/blob/main/linechart.png?raw=true">
            <h>Line chart</h>
            <pre class="highlight">
                <code class="python">
                    import plotly.express as px
                    import pandas as pd
                    import matplotlib.pyplot as plt
                    from pandasql import sqldf
                    import numpy as np
                    url = "https://raw.githubusercontent.com/Mao2003/Mao2003/main/results.csv"
                    df= pd.read_csv(url,encoding = 'unicode_escape')
                    pysqldf = lambda q: sqldf(q, globals())
                    df5=pysqldf("SELECT date, home_team, home_score, away_score\
                                FROM df\
                                WHERE home_team='Brazil' AND date>2022\
                                GROUP BY date")
                    x=df5['date']
                    yhc=df5['home_score']
                    yac=df5['away_score']
                    
                    plt.plot(x,yhc,'-r',label='Goal')
                    plt.plot(x,yac,':k',label='Goal conceded')
                    
                    plt.xlabel('Month')
                    plt.ylabel('Score')
                    plt.title('Overview of Brazils points scored and conceded from 2022')
                    plt.xticks(rotation=45)
                    plt.legend()
                    plt.show()
                    
                    
                    The chart above shows the points scored and points conceded by the Brazilian team in matches after 2022.

                    The x-axis represents the month and year, while the y-axis represents the number of points.
                    The red line (-r) represents the number of points scored by the Brazilian team in each month.
                    The dotted black line (':k') represents the number of points conceded by the team.
                    The graph shows the evolution of points scored and points conceded over time for the Brazilian team.
                    And the data from the chart shows that the number of goals scored by the Brazilian team is almost
                    always greater than the number of goals conceded. Therefore, it can be seen that this is a very strong
                    team and its odds of being in the top are hard to argue with.
                </code>
            </pre>
        </div>
        </body>
</html>
