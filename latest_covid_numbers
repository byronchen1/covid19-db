import pandas as pd
import numpy as np
import plotly.express as px
import plotly.graph_objects as go

df = pd.read_csv('https://health-infobase.canada.ca/src/data/covidLive/covid19.csv')
df['DT']=pd.to_datetime(df['date'], format='%d-%m-%Y')
cols=['DT','prname','numtested','numtotal','numrecover','numdeaths','numactive',
                    'testedtoday','numtoday','numrecoveredtoday','deathstoday']
df_provinces = df[(df['prname']=='Ontario') | (df['prname']=='British Columbia') | (df['prname']=='Alberta')]
df_provinces = df_provinces[cols]
df_provinces=df_provinces.reset_index()[cols]
df_provinces=df_provinces[df_provinces['DT']>='2020-05-01']
def create_plot(df,x_axis,y_axis,facet_row,title,b_colour):
    fig = px.bar(df, x=x_axis, y=y_axis, facet_row=facet_row,hover_data=cols[1:])
    fig.for_each_annotation(lambda a: a.update(text=a.text.split("=")[1]))
    fig.update_layout(
        title={
            'text': title,
            'y':0.95,
            'x':0.5,
            'xanchor': 'center',
            'yanchor': 'top'})
    fig.update_traces(marker_color=b_colour)
    fig.show()
    
   
create_plot(df=df_provinces,x_axis="DT",y_axis="numtoday",facet_row="prname",title="New Cases",b_colour="blue")
create_plot(df=df_provinces,x_axis="DT",y_axis="numrecoveredtoday",facet_row="prname",title="Recovered Cases",b_colour="green")
create_plot(df=df_provinces,x_axis="DT",y_axis="numactive",facet_row="prname",title="Active Cases",b_colour="red")
