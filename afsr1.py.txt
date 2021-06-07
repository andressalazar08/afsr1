
import dash
import dash_core_components as dcc
import dash_html_components as html
import pandas as pd
import plotly.express as px


app=dash.Dash(__name__)

datos=pd.read_csv('/home/andresusc2020/mysite/datosproduccion.csv',sep=";")

saludo=html.H2('Aplicación web basada en Dash para datos producción', style={'text-align':"center","color":"blue"})
autor=html.H3('Andrés Felipe Salazar Ramos', style={'text-align':"center","color":"black"})

#Este es un dataframe que me permitirá hacer un gráfico
tabla=datos.groupby('PT')['Cantidad_Orden'].sum().reset_index()

grafica1=dcc.Graph(figure=px.bar(tabla, x='PT', y='Cantidad_Orden'))
grafica2=dcc.Graph(figure=px.pie(tabla, values='Cantidad_Orden', names='PT', title='Population of European continent'))


app.layout=html.Div([saludo,autor,grafica1,grafica2])
