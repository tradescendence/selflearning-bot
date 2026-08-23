# BTC Trading Bot — Projekt-Briefing für Claude Code

## Kontext
Self-learning Trading Bot. Entwickelt in Zusammenarbeit mit Claude (Chat).
Dieser PC (lokaler Trading-Server) ist der Haupt-Server mit NVIDIA GPU (CUDA).

## Ziel
Modulare Trading-Plattform die:
- Selbständig Backtests durchführt
- Strategien per Genetischem Algorithmus evolvet
- Multi-Asset: BTC → XAU/USD → Futures (stufenweise)
- Grafisches lokales Dashboard (localhost, RustDesk-tauglich)
- Autonome Lern-Engine (YouTube/PDF → Knowledge Base)
- KI-Agenten-Loop (Claude API + OpenAI/Groq)

## Broker
- Vantage (Zugangsdaten bereits in .env vorhanden vom alten Telegram-Bot)
- Erst Paper Trading, dann Live
- Später auch Binance für Krypto

## Tech Stack
- Python 3.11+
- FinBERT auf CUDA (Sentiment, einmalig laden)
- VADER als Fallback
- FastAPI + React für Dashboard
- ChromaDB für Knowledge Base (RAG)
- Whisper (lokal, CUDA) für YouTube-Transkription
- Chart.js / Plotly für grafische Backtests
- LangChain für KI-Agenten

## Vorhandene alte Bots (im Ordner analysieren!)
- Modulare Python-Bots bereits vorhanden
- Krypto-Datenabruf funktioniert bereits gut
- Modulare Bauweise schon vorhanden
- KEIN selbstständiges Lernen bisher
- Bestes davon übernehmen, Rest ersetzen

## Bereits erstellte Module (aus Chat)
- main.py — Einstiegspunkt, async
- config.py — BotConfig dataclass, lädt .env
- data_feed.py — yfinance, Indikatoren (EMA/RSI/MACD/BB/ATR)
- strategy_engine.py — StrategyParams dataclass, vektorisierte Signale
- backtest_engine.py — Sharpe, MaxDD, WinRate, Fitness-Score
- evolution_engine.py — Genetischer Algorithmus (Crossover/Mutation)
- sentiment_engine.py — FinBERT CUDA + VADER Fallback
- risk_manager.py — Circuit Breaker, Position Sizing
- telegram_notifier.py — optional, erstmal nicht wichtig
- bot_state.py — Persistenz JSON

## Architektur-Prinzipien
1. Jedes Modul ist austauschbar (Schaltzentrale)
2. Symbol ist nie hardcoded (BTC heute, XAU morgen)
3. Parallel-Betrieb mehrerer Assets möglich
4. Dashboard: grafische Toggle-Schalter für alle Module
5. Grafischer Backtest: Equity Curve + Trade Marker auf Chart

## Schaltzentrale (zu bauen)
- Web-Dashboard localhost:8080
- Toggle-Switches: FinBERT an/aus, Evolution an/aus, Live/Paper, etc.
- Grafische Equity Curves
- Live P&L Anzeige
- RustDesk-tauglich (läuft im Browser)

## Lern-Engine (Phase 3)
- YouTube URL eingeben → Whisper transkribiert → in ChromaDB
- PDF hochladen → PyMuPDF → in ChromaDB  
- Arxiv/Web scraping
- KI-Agent queried Knowledge Base → generiert Strategie-Code
- Auto-Backtest → wenn gut: deploy

## Nächste Schritte für Claude Code
1. Alte Bots im Ordner analysieren (was ist wiederverwendbar?)
2. Beste Module übernehmen / integrieren
3. Dashboard aufbauen (FastAPI Backend + einfaches HTML Frontend)
4. Vantage-Connector bauen (Zugangsdaten aus .env)
5. Grafischen Backtest implementieren

## Wichtige Hinweise
- NVIDIA CUDA vorhanden → immer torch.cuda nutzen
- RAM: 12-16 GB
- PC läuft 24/7 als Server
- RustDesk ID: <entfernt>
- Erst alles testen bevor Live-Trading!
