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
