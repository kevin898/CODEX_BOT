# KTN XAU GitHub Reference Notes

Ngay clone:
- C:\CODEX_BOT\github_refs\GOLD_ORB
- C:\CODEX_BOT\github_refs\blackXAU_AUTOMATED-BOT-TRADE
- C:\CODEX_BOT\github_refs\PositionSizer
- C:\CODEX_BOT\github_refs\geraked-metatrader5
- C:\CODEX_BOT\github_refs\EA31337-classes

## 1. GOLD_ORB

File chinh:
- C:\CODEX_BOT\github_refs\GOLD_ORB\GOLD_ORB\GOLD_ORB.mq5
- C:\CODEX_BOT\github_refs\GOLD_ORB\GOLD_ORB\Include\price_action.mqh
- C:\CODEX_BOT\github_refs\GOLD_ORB\GOLD_ORB\Include\MoneyManagement.mqh
- C:\CODEX_BOT\github_refs\GOLD_ORB\GOLD_ORB\Include\RiskManagement.mqh
- C:\CODEX_BOT\github_refs\GOLD_ORB\GOLD_ORB\Include\TrailingStops.mqh

Dang hoc:
- Open Range Breakout module: `Price_Action::Open_Range_Breakout()`.
- Box/range logic dung candle composition de tao support/resistance.
- Gio bat dau trade theo server time.
- Max trades/day.
- Real trade + virtual trade song song de theo doi performance.
- Equity drawdown guard va losing streak guard.

Nen lay:
- Cach tach module: `IndicatorModule()`, `ExecuteOrders()`, `RiskManagementModule()`, `TrailModule()`.
- Y tuong max trades/day va virtual monitoring.
- Mot phan `VerifyVolume()` trong `MoneyManagement.mqh`.

Can can than:
- Open range logic con tho, nhieu nguong hard-code.
- `MoneyManagement()` dung tick value don gian, can sua cho XAU theo tick size/point/value dung broker.
- Khong copy Alglib/Math folder, qua lon va khong can cho bot XAU core.

## 2. blackXAU_AUTOMATED-BOT-TRADE

File chinh:
- C:\CODEX_BOT\github_refs\blackXAU_AUTOMATED-BOT-TRADE\blackXAU2.mq5

Dang hoc:
- Zone mode:
  - `ZoneMode=0`: dung high/low ngay truoc.
  - `ZoneMode=1`: dung first N H4 bars.
- Breakout M5 qua `zoneHigh/zoneLow`.
- Cho retest trong `MaxWaitSeconds`.
- Session filter.
- MT5 economic calendar news filter.
- Spread filter.
- EMA50/EMA200 filter.
- ATR-based SL/TP.
- BE + trailing stop fixed/ATR.

Nen lay:
- `UpdateZoneIfNeeded()`.
- `IsInTradingSession()`.
- `IsNewsTime()`.
- `CheckMarketConditions()`.
- `ManageTrailingStops()`.
- State machine: `waitingRetest`, `breakoutDir`, `breakoutTime`.

Can can than:
- Short logic dang bi comment trong file clone.
- `CalculateLotByRisk()` con qua don gian: chia theo points*tickValue, chua dung tick size day du.
- Logic breakout/retest la continuation, khac voi Liquidity Trap Sniper reversal. Co the dung cho Open Range Bot, khong dung nguyen cho trap bot.

## 3. PositionSizer

File chinh:
- C:\CODEX_BOT\github_refs\PositionSizer\MQL5\Experts\Position Sizer\Position Sizer.mq5
- C:\CODEX_BOT\github_refs\PositionSizer\MQL5\Experts\Position Sizer\Position Sizer.mqh
- C:\CODEX_BOT\github_refs\PositionSizer\MQL5\Experts\Position Sizer\Position Sizer Trading.mqh

Dang hoc:
- Position sizing day du cho MT5.
- Xu ly account size, risk %, commission, margin, swaps, symbol settings.
- UI rat lon, khong can copy het.

Nen lay:
- Cong thuc/tinh than tinh lot chuan theo symbol:
  - risk money
  - entry-SL distance
  - tick value
  - tick size
  - min/max/step lot
  - commission/margin check neu can
- Idea tach module lot sizing rieng cho Hybrid Manager.

Can can than:
- Code qua lon va UI-heavy. Khong nen import ca repo vao EA.
- Nen viet lai `KTN_PositionSizer.mqh` gon, lay concept thoi.

## 4. geraked/metatrader5

File chinh:
- C:\CODEX_BOT\github_refs\geraked-metatrader5\Experts\EATemplate.mq5
- C:\CODEX_BOT\github_refs\geraked-metatrader5\Experts\EATemplate2.mq5
- C:\CODEX_BOT\github_refs\geraked-metatrader5\Include\EAUtils.mqh
- C:\CODEX_BOT\github_refs\geraked-metatrader5\Indicators\OrderBlock.mq5
- C:\CODEX_BOT\github_refs\geraked-metatrader5\Indicators\DailyHighLow.mq5
- C:\CODEX_BOT\github_refs\geraked-metatrader5\Indicators\AtrSlFinder.mq5

Dang hoc:
- Template EA sach: inputs theo group, `OnInit`, `OnTimer`, `OnTick`, signal functions.
- `GerEA` class gom magic, risk, trailing, grid, equity, news.
- `calcVolume()` trong `EAUtils.mqh` dung risk mode va tick value.
- Spread/margin/multiple positions guard.

Nen lay:
- Khung EA template cho project KTN.
- `calcVolume()` concept.
- `order()` concept: normalize price, validate SL/TP, OrderCheck, filling type.
- `OnTimer()` de chay trailing/equity guard thay vi nhhoi vao moi tick.
- Indicator `DailyHighLow` va `OrderBlock` de tham khao level/liquidity.

Can can than:
- Co grid/martingale: khong dung cho core KTN neu risk rule cam DCA khi sai.
- `EAUtils.mqh` rat nhieu tinh nang, nen trich y tuong va viet lai gon.

## 5. EA31337-classes

Thu muc dang chu y:
- C:\CODEX_BOT\github_refs\EA31337-classes\Account
- C:\CODEX_BOT\github_refs\EA31337-classes\Trade
- C:\CODEX_BOT\github_refs\EA31337-classes\Indicator
- C:\CODEX_BOT\github_refs\EA31337-classes\Indicators
- C:\CODEX_BOT\github_refs\EA31337-classes\Tick
- C:\CODEX_BOT\github_refs\EA31337-classes\Task

Dang hoc:
- Framework reusable cho MQL4/MQL5.
- Trade signal structs/managers.
- Indicator abstraction.
- Account/SymbolInfo wrappers.

Nen lay:
- Y tuong kien truc neu project lon:
  - `Signal`
  - `Strategy`
  - `RiskManager`
  - `Execution`
  - `TradeManager`
- Cach dat ten va gom class.

Can can than:
- Qua lon cho buoc dau.
- Khong nen dua vao bot dau tien, se lam compile/debug phuc tap.

## Ket luan copy/use

Khong nen copy nguyen repo nao vao bot chinh.

Nen viet lai cac module KTN gon:
1. `KTN_RiskManager.mqh`
2. `KTN_PositionSizer.mqh`
3. `KTN_SessionNewsFilter.mqh`
4. `KTN_LevelEngine.mqh`
5. `KTN_TradeManager.mqh`
6. `KTN_LiquidityTrapSniper.mq5`

Thu tu uu tien code:
1. Hybrid Manager foundation.
2. Liquidity Trap Sniper Bot.
3. Open Range Breakout Retest Bot.
4. Trend Pullback Baseline Bot.

Nhac viec:
- Bot nen code truoc: Hybrid Manager foundation + Liquidity Trap Sniper Bot.
- Ly do: Hybrid Manager la xop song risk/execution; Liquidity Trap Sniper sat nhat voi 3 core GPT_KTN.
