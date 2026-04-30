# KTN XAU MT5 Project Core

Nguon tong hop:
- C:\Kevin Toan Nang\KTN_SYSTEM\CORE\[CORE_1] SCALPING_LIQUIDITY_SYSTEM.txt
- C:\Kevin Toan Nang\KTN_SYSTEM\CORE\[CORE_2] XAU_STRATEGY_CHEAT_SHEET.txt
- C:\Kevin Toan Nang\KTN_SYSTEM\CORE\[CORE_3] TRADING_XAU_CORE.txt
- GitHub references: GOLD_ORB, blackXAU_AUTOMATED-BOT-TRADE, EarnForex PositionSizer, geraked/metatrader5, EA31337.

## 1. Trading Philosophy

Bot khong duoc trade cam xuc, khong trade indicator don le, khong vao lenh chi vi gia chay manh.

Core mindset:
- XAUUSD la thi truong volatility cao, phu hop scalping va intraday neu co ky luat.
- Market co xu huong hunt liquidity: quet stoploss truoc khi di huong that.
- Indicator chi la bo loc/phu kien. Quyet dinh chinh la liquidity, structure, session, risk.
- Thieu setup ro rang thi khong trade.

## 2. Market Context Filters

Bot phai danh gia context truoc khi tim entry:
- Symbol: XAUUSD / GOLD.
- Session uu tien: London, New York open, London-New York overlap.
- Khung gio manh: 9:30-11:30 AM EST neu broker/session phu hop.
- Tranh trade khi rollover, thanh khoan thap, spread gian, sau tin manh.
- Tin can canh bao/tat bot: CPI, NFP, rate decision, FOMC, high-impact USD news.
- Correlation filter tuy chon:
  - DXY tang: uu tien bearish gold.
  - DXY giam: uu tien bullish gold.
  - XAGUSD chay truoc co the lam confirmation phu.

## 3. Core Entry Logic

Entry chat luong cao can toi thieu 3 dieu kien:
1. Liquidity sweep.
2. Reclaim.
3. Structure shift.

Liquidity zones:
- Swing high / swing low.
- Equal highs / equal lows.
- PDH / PDL.
- Range high / range low.
- Supply / demand zone.
- Order block truoc cu breakout/dump/pump manh.

Trap model:
- Gia pha dinh/day.
- Khong giu duoc breakout.
- Quay dau manh va reclaim level.
- Entry tai reclaim hoac pullback sau reclaim.

Structure model:
- Bullish shift: sweep day, reclaim len, tao higher high.
- Bearish shift: sweep dinh, reclaim xuong, tao lower low.

## 4. Trend And Zone Logic

Trend filter:
- M15 de xac dinh xu huong ngan.
- H1 de xac nhan cau truc lon hon.
- Bullish: Higher High + Higher Low.
- Bearish: Lower High + Lower Low.

Buy setup:
- Trend bullish.
- Gia hoi ve demand/discount zone duoi 50% Fibo.
- Co sweep/reclaim/confirmation M1.
- SL duoi demand/support/sweep low.
- TP tai supply/liquidity tiep theo hoac RR >= 1:2.

Sell setup:
- Trend bearish.
- Gia hoi ve supply/premium zone tren 50% Fibo.
- Co sweep/reclaim/confirmation M1.
- SL tren supply/resistance/sweep high.
- TP tai demand/liquidity tiep theo hoac RR >= 1:2.

## 5. Indicator Policy

Bot duoc dung indicator don gian, khong lam nhieu lop gay nhieu:
- EMA20: rubber-band scalping, gia lech xa EMA co xu huong hoi ve.
- EMA50/EMA200: trend filter, dynamic support/resistance.
- ATR: volatility filter, SL/TP adaptive, tranh thi truong qua yeu hoac qua nhiu.
- Fibonacci:
  - 50% pullback cho continuation.
  - 0.25/0.5 lam TP scalping.
  - Extension -1/-1.5/-2 cho TP dai.

Rule: indicator khong duoc tu mo lenh neu khong co liquidity/structure context.

## 6. Risk And Trade Management

Risk:
- Mac dinh 0.25%-1% moi lenh.
- Hard cap: 1% moi lenh.
- Khong DCA khi sai.
- Khong gong lo.
- RR toi thieu 1:2, tot hon 1:3.

Management:
- Khi gia di dung, move SL ve BE theo rule.
- Chot partial 25% tai liquidity gan.
- Neu BOS tiep dien, co the giu phan con lai.
- Neu structure fail, thoat.

One-candle trailing rule:
- Long co loi nhuan: SL = low nen M1 truoc.
- Short co loi nhuan: SL = high nen M1 truoc.
- Trailing theo tung nen, khong ngoai le neu che do nay bat.

## 7. No-Trade Rules

Bot khong duoc trade khi:
- Khong co liquidity ro.
- Khong co sweep/reclaim/structure shift.
- Sideway qua hep hoac range khong co bien.
- Ngoai session chinh.
- Spread vuot nguong.
- Gan/sau tin manh neu news filter dang bat.
- Rollover/thanh khoan thap.
- RR < 1:2.
- Da cham daily loss limit hoac max trades/day.

## 8. GitHub Reference Mapping

Nen hoc/lien ket y tuong:
- yulz008/GOLD_ORB: open-range breakout cho XAUUSD, tot cho ORB/range module.
- phatnomenal/blackXAU_AUTOMATED-BOT-TRADE: H4 zone + M5 breakout/retest, news filter, trailing, risk lot.
- EarnForex/PositionSizer: risk-based lot sizing, margin/commission/symbol handling.
- geraked/metatrader5: cau truc EA/backtest va cac pattern strategy MQL5.
- EA31337/EA31337-classes: framework/class abstraction neu muon scale thanh nhieu strategy.
- aimaster-dev/mq5-trading-bot: panel/manual control, multi-TP, WAE confirmation.
- carlosrod723/MQL5-Trading-Bot: liquidity sweep, fib zones, order blocks, partial exits, optional ML.

## 9. Proposed Bot Families

Co the tach thanh 7 truong phai bot:

1. Liquidity Trap Sniper Bot
- Core: sweep -> reclaim -> structure shift.
- Timeframe: M1/M5 entry, M15/H1 context.
- Tot nhat cho scalping XAU trong gio manh.

2. Trend Pullback Continuation Bot
- Core: trend HH/HL hoac LH/LL + pullback ve Fibo 50%/EMA zone.
- Timeframe: M5/M15/H1.
- It nguoc trend, phu hop intraday on dinh hon.

3. Supply Demand Premium Discount Bot
- Core: buy demand/discount, sell supply/premium, confirmation bang reclaim.
- Timeframe: M5/M15/H1.
- Gan voi SMC/order-block logic.

4. Open Range Breakout Retest Bot
- Core: London/NY/open range, breakout, retest, vao theo huong pha that.
- GitHub reference: GOLD_ORB, blackXAU.
- Can spread/session filter tot.

5. EMA ATR Fibo Simple Trend Bot
- Core: EMA50/200 trend, ATR volatility, Fibo pullback.
- It SMC hon, de backtest, de toi uu.
- Phu hop lam baseline bot.

6. Strike And Recoil Scalper Bot
- Core: gia giat manh quet liquidity/gap/news impulse roi hoi nhanh.
- Timeframe: M1/M5.
- Can filter spread, slippage, news rat chat.

7. Hybrid Manager Bot
- Core: khong phai strategy rieng, la engine quan tri lenh.
- Module: risk lot, partial TP, BE, one-candle trailing, daily stop, max trades, telegram/report.
- Nen dung chung cho tat ca bot tren.

## 10. Recommended Build Order

Nen build theo thu tu:
1. Hybrid Manager Bot: risk, lot, spread, session, news, BE, partial, trailing.
2. Liquidity Trap Sniper Bot: dung nhat voi core GPT_KTN.
3. Trend Pullback Continuation Bot: baseline de so sanh backtest.
4. Open Range Breakout Retest Bot: lay y tuong GOLD_ORB/blackXAU.
5. Supply Demand Premium Discount Bot: nang cap SMC/order-block.

Quy tac vang: moi strategy phai co backtest rieng, set rieng, magic number rieng, daily risk rieng.
