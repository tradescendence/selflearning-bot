# BTC Self-Learning Trading Bot

**Status: Konzeptphase.** Dieses Repo enthaelt bisher nur die
Architektur-Spezifikation, noch keinen lauffaehigen Code. Es dient als
Briefing-Dokument fuer die Umsetzung.

## Idee

Eine modulare Trading-Plattform, die nicht nur handelt, sondern ihre eigenen
Strategien weiterentwickelt:

- **Backtests** laufen selbstaendig
- **Genetischer Algorithmus** evolviert Strategieparameter (Crossover,
  Mutation, Fitness-Score aus Sharpe / MaxDD / WinRate)
- **Multi-Asset** stufenweise: BTC → XAUUSD → Futures
- **Lern-Engine**: YouTube und PDFs werden transkribiert bzw. extrahiert und
  in eine Vektordatenbank gelegt; ein Agent fragt diese Wissensbasis ab und
  generiert daraus neuen Strategie-Code, der automatisch gebacktestet wird
- **Dashboard** auf localhost mit Toggle-Schaltern je Modul und grafischen
  Equity-Curves

## Geplanter Stack

| Bereich | Wahl |
|---------|------|
| Sprache | Python 3.11+ |
| Sentiment | FinBERT auf CUDA, VADER als Fallback |
| Dashboard | FastAPI + React, Chart.js / Plotly |
| Wissensbasis | ChromaDB (RAG) |
| Transkription | Whisper lokal, CUDA |
| Agenten | LangChain, Claude API + OpenAI/Groq |
| Broker | Vantage (erst Paper, dann Live), spaeter Binance |

## Geplante Module

`main.py` (async Einstieg) · `config.py` (BotConfig aus .env) ·
`data_feed.py` (yfinance, EMA/RSI/MACD/BB/ATR) · `strategy_engine.py`
(vektorisierte Signale) · `backtest_engine.py` (Sharpe, MaxDD, WinRate,
Fitness) · `evolution_engine.py` (GA) · `sentiment_engine.py` ·
`risk_manager.py` (Circuit Breaker, Position Sizing) · `bot_state.py`
(JSON-Persistenz)

## Architekturprinzipien

1. Jedes Modul ist austauschbar
2. Das Symbol ist nie hardcoded — BTC heute, XAU morgen
3. Mehrere Assets laufen parallel
4. Alle Module sind im Dashboard schaltbar
5. Backtests sind grafisch: Equity Curve plus Trade-Marker im Chart

Vollstaendige Spezifikation: [`docs/ARCHITECTURE.md`](docs/ARCHITECTURE.md)

## Naechste Schritte

1. Vorhandene modulare Python-Bots sichten, Wiederverwendbares uebernehmen
2. Dashboard-Geruest (FastAPI + HTML)
3. Vantage-Connector, Zugangsdaten aus `.env`
4. Grafischen Backtest implementieren
5. Erst danach Evolution und Lern-Engine

## Lizenz

MIT — siehe [LICENSE](LICENSE).
