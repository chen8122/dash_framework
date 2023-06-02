# dash_framework
1. **`enrivn.py`**: to import report path 

2. **`pnl.py`**(date slider), **`risk_style.py`**(date slider), and **`risk_all`**(date slider and 4 tabs): to offer 3 usage scenarios  

4. **`applayout.py`**: to recycle the app layout       
Typical dash flow：   
- Dash definition `app = Dash(__name__)` 
- Design layout: `app.layout`
- Connect to server and run:    
  `if __name__ == '__main__':  
  
    app.run_server(host='0.0.0.0', debug=True)`  

My project:  
-  Dash definition: **`class SingleGraphLayout(Dash)`** and **`class MultipleGraphLayout(Dash)`** in `applayout.py` are **custom classes** that define two `__Dash__` application objects. They inherit functionality of `__Dash__` class. The `super().__init__(__name__)` statement calls the `__init__` method of the parent class __Dash__ and passes the `__name__` parameter to the `__init__` method.  

`class Layout(Dash):  

    def __init__(self, **kwargs):  
    
      super().__init__(__name__)`  
        
- Design layout:  
  `SingleGraphLayout.layout = html.Div([dcc.RangeSlider(id=input_id,...),  
  
                                        dcc.Graph(id=output_id,...)])`  
  `MultipleGraphLayout.layout = html.Div([dcc.RangeSlider(id=input_id,...),  
  
                                          dcc.Tabs(id='Tabs', ..., children=[  
                                          
                                          dcc.Tab(label=oid, value=oid, children=[dcc.Graph(id=oid for oid in output_ids]])`  
- Connect to server and run in the end of main code

4. **`fig_config.py`**: to recycle shared figure configuration - line&shade subplots, create slider markers, transform slider markers to exact dates, align y axes, etc.  
**`def plots() --> Dash`** collects the input from slider, and pass the sliced data to **`def main_plots() --> go.Figure`** which return a figure as  `@app.callback()`'s output, finally return a Dash app. For example:     
     Scenario1: **`risk_style.py`** passed a dictionary of 20 (1910,2)dataframes  
     app layout: {list:2} RangerSlider+Graph    
     Scenario2: **`risk_all`** passed dictionary of 20 (1910,2)dataframes 4 times; each time trigger `@app.callback()` and output a figure whose output_id matches the ones in `app.layout`. When finish the iteration, app collects 4 figures and show on the server end.  
     nested app layout: {list:2} RangerSlider+Tab --> Tab.children = {list:1}` --> Graph




