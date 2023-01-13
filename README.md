# TradingView-Indicator-Codes
Tradingview indicators code

// Name RSI / STOCH OVERLAY 

study(title="RSI / STOCH RSI OVERLAY", shorttitle="STOCH V RSI")
src = close, len = input(14, minval=1, title="Length")
up = rma(max(change(src), 0), len)
down = rma(-min(change(src), 0), len)
rsi = down == 0 ? 100 : up == 0 ? 0 : 100 - (100 / (1 + up / down))
plot(rsi, color=green, linewidth=3)
band1 = hline(70, linestyle=solid)
band0 = hline(30, linestyle=solid)
fill(band1, band0, color=purple, transp=80)


smoothK = input(3, minval=1)
smoothD = input(3, minval=1)
lengthRSI = input(14, minval=1)
lengthStoch = input(14, minval=1)
src1 = input(close, title="RSI Source")

rsi1 = rsi(src, lengthRSI)
k = sma(stoch(rsi1, rsi1, rsi1, lengthStoch), smoothK)
d = sma(k, smoothD)
plot(k, color=white)
plot(d, color=orange)
h0 = hline(80)
h1 = hline(20)
fill(h0, h1, color=black, transp=100)


/////////////////////////////////////////////////////////////////////////////////////////
//@version=2
//@Author: poison

//This indicator was made to allow three moving averages to be displayed without needing to use up 3 charting indicators individually

study(title="Triple Moving Averages", shorttitle="TEMA", overlay=true)

// Checkbox's for the other 2 MA's
a = input(true, title="Enable 2nd MA")
b = input(true, title="Enable 3rd MA")

len = input(50, minval=1, title="Length")
len2 = input(100, minval=1, title="Length2")
len3 = input(200, minval=1, title="Length3")

src = input(close, title="Source")
src2 = input(close, title="Source2")
src3 = input(close, title="Source3")

out = ema(src, len)
out2 = ema(src2, len2)
out3 = ema(src3, len3)

plot(out, title="EMA", color=red)
plot(a and out2 ? out2: na, title="EMA2", color=green)
plot(b and out3 ? out3: na, title="EMA3", color=blue)
