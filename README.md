# dash_framework
## 1. `applayout.py`: recycle the app layout 
Typical dash flow：   
- Dash definition `app = Dash(__name__)` 
- Design layout: app.layout 
- Connect to server and run: `if __name__ == '__main__': app.run_server(host='0.0.0.0', debug=True)`
My project:  
- `class SingleGraphLayout(Dash)` and `class MultipleGraphLayout(Dash)` in `applayout.py` are **custom classes** that define two `__Dash__` application objects. They inherit functionality of `__Dash__` class. The `super().__init__(__name__)` statement calls the `__init__` method of the parent class __Dash__ and passes the `__name__` parameter to the `__init__` method.  
- `SingleGraphLayout.layout = html.Div([dcc.RangeSlider(id=input_id,...),  
                                        dcc.Graph(id=output_id,...)])`  
   `MultipleGraphLayout.layout = html.Div([dcc.RangeSlider(id=input_id,...),  
                                          dcc.Tabs(id='Tabs', ..., children=[  
                                          dcc.Tab(label=oid, value=oid, children=[dcc.Graph(id=oid for oid in output_ids]])`  
- Connect to server and run in the end of main code

## 2. `fig_config.py`: recycle the figure configuration - line&shade subplots, create slider markers, transform slider markers to exact dates, align y axes, etc.
'def plots() --> Dash` collect the input from slider, and pass the sliced data to 'def main_plots() --> go.Figure' which return 
return the Dash object app

## 3. File reading and dataframe preparation are stored seperately. We have 3 usage scenarios: pnl(date slider), risk_style(date slider), and risk_factors(date slider and 4 tabs)
