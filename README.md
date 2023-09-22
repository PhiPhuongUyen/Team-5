<html lang="vi" style="font-family: Sans-serif;">
<head>
        <meta charset="UTF-8">
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <link rel="icon" type="image/x-icon" href="https://mao-nek.000webhostapp.com/index.html/Nh%C3%B3m%202/logo.png">
        <link rel="stylesheet" type="text/css" href="[style.css](https://raw.githubusercontent.com/PhiPhuongUyen/Team-5/main/Group%205.css)">
    </head>
    <body>
        <div class="background">
                <div class="navbar">
                    <img src="https://mao-nek.000webhostapp.com/index.html/Nh%C3%B3m%202/logo.png" alt="Logo" class="logo">
                    <nav>
                        <ul id="menu">
                            <li><a href="[https://mao-nek.000webhostapp.com/index.html/Nh%C3%B3m%202/PHINEAS.html](https://github.com/PhiPhuongUyen/Team-5/blob/main/Nh%C3%B3m%205%20Final.ipynb)">Trang chủ</a></li>
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
                    </br>
                    </br>
                    The scatterplot chart is used to analyze and compare the scores of the home team and the away team in matches.
                </code>
            </pre>
        </div>
        <div class="section">
            <img src="https://github.com/Mao2003/Mao2003/blob/main/barchart.png?raw=true">
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
                    </br>
                    </br>
                    The column chart above is the average monthly goals statistics of the five teams with the most total matches from 1872 to September 12, 2023.
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
                    </br>
                    </br>
                    The pie chart shows the distribution rates of different tournaments.
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
                    </br>
                    </br>
                    The chart above shows the points scored and points conceded by the Brazilian team in matches after 2022.
                </code>
            </pre>
        </div>
        </body>
</html>
