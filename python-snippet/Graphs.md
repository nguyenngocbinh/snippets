---
title: Graphs
---

### Candlestick

```python
import yfinance as yf 
data = yf.download(tickers = 'ETH-USD', period = 'max', interval = '1d')
dfpl = data[0:100]
import plotly.graph_objects as go
fig = go.Figure(data=go.Candlestick(
    x = dfpl.index,
    open = dfpl.Open,
    high = dfpl.High,
    low = dfpl.Low,
    close = dfpl.Close    
))

fig.show()
```