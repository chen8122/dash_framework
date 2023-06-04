# Dash_Framework
## Introduction  
This project aims to create **interactive dashboards for the front-end business operations of my company**. The data utilized in these dashboards is derived from complex factor calculations applied to time series stock data spanning from 2015 to 2023. Drawing inspiration from my previous visualizations, the initial requirement from the company was to create these interactive dashboards using popular tools such as Tableau or Power BI. The challenge lay in integrating the dynamically changing Python data with the interfaces of these commercial software.  

Through extensive exploration within the data analysis community, I discovered that Dash Plotly, an open-source Python library, presented a viable alternative for building interactive dashboards in the form of web applications.  Leveraging the power of code-based development, as opposed to relying on commercial software, offered notable advantages. Firstly, it proved to be more cost-effective. Additionally, Dash Plotly provided a unified platform where front-end quantitative analysts could access data and effortlessly invoke plotting code without requiring additional training in Tableau or Power BI. Moreover, the codebase could be refactored to accommodate new data sources, enhancing the platform's versatility.  

## My Responsibility
The first stage of my work involved designing the **layout of the app**, which included dual Y-axes for multiple line graphs and shaded area chart. Users can select their desired date range by adjusting a slider. 
In the second stage, I studied the documentation of Plotly to understand its plotting routines and how to use the **@callback decorator** to capture the user-selected time interval as real-time input. This input triggers the plotting function, which then runs the server to display the graphs in real-time on the web page.  
Next, I focused on extracting the common elements of graph configuation, such as plotting line graphs and shaded area charts based on input dataframes, dividing subplots, aligning dual Y-axes, and formatting the images.  
Finally, I expanded the creation of single-page interactive dashboards to include multi-tab dashboards with multiple data sources.  

## Dash Code Framework
1. **`read.py`**: to import report path 

2. **`pnl.py`**(date slider), **`risk_style.py`**(date slider), and **`risk_all`**(date slider and 4 tabs): to offer 3 usage scenarios  

3. **`applayout.py`**: to recycle the app layout       
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

## Chanllenges  
The project's primary challenge lay in abstracting reusable plotting modules. Three specific obstacles were encountered during this process:  
-Determining the optimal input data format proved crucial, as it set the foundation for subsequent code implementation. Initial attempts involved representing different data formats using an M*N array of dataframes; however, this approach was ultimately refined to employ a nested dictionary structure—a dictionary of two dictionaries of dataframes.  
-Abstracting the single-graph layout without tabs and the multi-graph layout with tabs required the creation of distinct classes inheriting from Dash objects, facilitating the assignment of different app layouts. This design approach effectively enabled the reuse of extracted single-graph plotting modules.  
-Maintaining meticulous version control using Git emerged as a critical consideration. Given the low tolerance for errors within the company's front-end business operations, each commit necessitated clear and well-defined task modifications, ensuring ease of retrieval and comparison by team members.  

## Reflection    
My internship was an incredibly immersive experience, particularly in the demanding front-end operations of the company. The high standards for programming logic and code style pushed me to refine my work style. Initially, I focused on efficiency and delivering results, but I soon learned to prioritize caution and attention to detail. Throughout the four-month internship, my Python programming skills underwent significant growth. Python evolved from a mere data manipulation tool to a language in which I actively consider how to make my code as readable and efficient as my dashboards. Overall, this Wall Street journey has been unforgettable and has enriched my professional development in numerous ways.
