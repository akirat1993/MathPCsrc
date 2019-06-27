[TOC]



[plotlyって何?](https://qiita.com/inoory/items/12028af62018bf367722)

## 描写例

### Stacked and Gouped Barplots

``` python
import plotly.graph_objs as go
import plotly

abc1 = go.Bar(
    x =["A", "B", "C"],
    y = [0, 0.35, 0.4],
    name = "abc1",
    xaxis = 'x1',
)

abc2 = go.Bar(
    x =["A", "B", "C"],
    y = [0.6, 0.5, 0.4],
    name = "abc2",
    xaxis = 'x1',
)

de1 = go.Bar(
    x =["D", "E"],
    y = [0.3, 0.35],
    name = "de1",
    xaxis = 'x2',
)

de2 = go.Bar(
    x =["D", "E"],
    y = [0.25, 0.15],
    name = "de2",
    xaxis = 'x2',
)
layout = go.Layout(
    barmode = "stack",
    #yaxis = dict(tickformat: '%'),
    xaxis = {
        "domain": [0, 0.5],
        "anchor": 'x1', 
        "title": 'ABC'
    },
    xaxis2 = {
        "domain": [0.5, 1],
        "anchor": 'x2', 
        "title": 'DE'
    }
)
fig = go.Figure(data=[abc1, abc2, de1, de2], layout=layout)

#plotlyをjupyter内部で表示
plotly.offline.init_notebook_mode(connected=False)

#draw
plotly.offline.iplot(
    fig, show_link=False, 
    # Hide botton to update figure to plotly 
    config={"displaylogo":False, "modeBarButtonsToRemove":["sendDataToCloud"]}
) 
```

!INCLUDE "../../html/StackGroupBars.html"



## 自分メモ


```python
import colorlover as cl
import plotly
from plotly import tools
import plotly.graph_objs as go
from IPython.display import display, HTML, Image

#jupyterでTexを使う
#https://github.com/plotly/plotly.py/issues/515

display(HTML(
    '<script>'
        'var waitForPlotly = setInterval( function() {'
            'if( typeof(window.Plotly) !== "undefined" ){'
                'MathJax.Hub.Config({ SVG: { font: "STIX-Web" }, displayAlign: "center" });'
                'MathJax.Hub.Queue(["setRenderer", MathJax.Hub, "SVG"]);'
                'clearInterval(waitForPlotly);'
            '}}, 250 );'
    '</script>'
))

#color bar
cl.scales.keys()
HTML(cl.to_html( cl.scales['12']['qual']['Paired'] ))

dic = go.Scatter/dict(
    x = [0,1],
    y = [0, 1],
    name = str, #データの名前(凡例の名前で標準でポップアップ表示の名前)
    xaxis = "x", 
    yaxis = "y2",
    showlegend=False,
    legendgroup = str, 
        #一致するとワンクリックで同時に消える
        #legendgroupが一緒でも凡例は別々に表示される(片方のみ表示させたい場合はshowlegend=False)
        #凡例の名前ではない(凡例の名前はname)
    text=str,
    hoverinfo='text',
        #ポップアップ表示の内容をstrに変更させたい場合
        #<br>で改行
        
    mode = "lines",　#折れ線
    line = dict(
        color = colors[in_c],
        width = 1
    ),
       
    mode = "markers", #散布図
    marker = dict(
        size = 7,
        color = cl.scales['12']['qual']['Paired'][i],
        ),
)

trace
    go.Bar(
        x=[0, 1],
        y=[3, 11],
        name="Births"
    )

layout = go.Layout( #fig["layout"]
    titel = str,
    x/yaxis2=dict(
        title = str,
        showgrid=False,
        zeroline=True,
        showticklabels=False, #座標の数値を非表示
        rangemode="nonnegative",
        tickformat =',d', #only show integer
        dtick = 1, #1,2,…#座標の数値の間隔
        overlaying="y", anchor="x",side= "right",
        range=[0,9],
        domain=[0, .35],
    ),
    legend = {"x":1, "y":0},
    font={"family":"Yu Gothic Bold, sans-selif", "size":20},
    width = 600,
    height = 800,
)

fig = go.Figure(data=[dic1, dic2,…,trace1, trace2,…], layout=layout)


fig
    tools.make_subplots(
        rows=2, cols=2, 
        print_grid=True, 
        horizontal_spacing=0.18, 
        subplot_titles=["sub_fig1", "sub_fig2"]
    )

#軸を共有する    
fig = tools.make_subplots(rows=2, cols=1)
# locate drawing place
fig.append_trace(trace1, 1, 1) #row, column
fig.append_trace(trace2, 1, 1)
fig.append_trace(trace3, 2, 1)

#デフォルトでtrace1とtrace2のy軸はy1で共有されているため、traceのy軸を新しい名前y3に変更する
fig["data"][1].update(yaxis="y3")

fig["layout"].update(
    #y3(yaxis3)をy(yaxis1)の右に配置する
    yaxis3 = dict(title= "yaxis3", overlaying="y", anchor="x",side= "right"),
)

#plotlyをjupyter内部で表示
plotly.offline.init_notebook_mode(connected=False)

plotly.offline.iplot(
    fig, show_link=False, 
    # Hide botton to update figure to plotly 
    config={"displaylogo":False, "modeBarButtonsToRemove":["sendDataToCloud"]}
)   

#HTMLで保存
plotly.offline.plot(fig,
    auto_open = False,
    show_link=False, 
    # Hide botton to update figure to plotly
    config={"displaylogo":False, "modeBarButtonsToRemove":["sendDataToCloud"]},
    filename= "/absolute or relative/path/to/file"
)

#Tex記号ありの図をHTMLで保存
#https://github.com/plotly/plotly.py/issues/515

def SaveTexPlotly(fig, filename):
    plot_div = plotly.offline.plot(
        fig, output_type = 'div',
        show_link=False,
        config={"displaylogo":False, "modeBarButtonsToRemove":["sendDataToCloud"]},        
    )
    template = """
    <head>
    <script type="text/javascript" async
      src="https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.1/MathJax.js?config=TeX-MML-AM_SVG">
    </script>
    </head>
    <body>
    {plot_div:s}
    </body>""".format(plot_div = plot_div)
    with open(filename, 'w') as fp:
        fp.write(template)
```
