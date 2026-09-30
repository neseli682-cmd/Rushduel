<!DOCTYPE html>
<html lang="pl">
<head>
<meta charset="UTF-8">

<meta name="viewport"
      content="width=device-width, initial-scale=1.0">

<meta name="theme-color" content="#101418">
<meta name="mobile-web-app-capable" content="yes">
<meta name="apple-mobile-web-app-capable" content="yes">

<title>GOALRUSH</title>

<style>

* {
    box-sizing: border-box;
}

body {
    margin: 0;
    font-family: Arial, sans-serif;
    background: #101418;
    color: white;
}

button {
    width: 100%;
    border: 0;
    border-radius: 12px;
    padding: 14px;
    margin-top: 10px;
    font-size: 16px;
    font-weight: bold;
    cursor: pointer;
    background: #2d3742;
    color: white;
}

button:active {
    transform: scale(.98);
}

.screen {
    display: none;
    min-height: 100vh;
}

.container {
    max-width: 600px;
    margin: auto;
    padding: 18px;
}

h1 {
    text-align: center;
    margin: 10px 0 20px;
}

h2 {
    margin-top: 0;
}

.card {
    background: #181e24;
    border-radius: 16px;
    padding: 18px;
    margin-bottom: 15px;
    box-shadow: 0 5px 20px rgba(0,0,0,.2);
}

.players {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 10px;
}

.player-box {
    background: #222a32;
    padding: 15px;
    border-radius: 12px;
}

.player-box label {
    display: flex;
    align-items: center;
    gap: 8px;
}

.player-box input {
    width: 20px;
    height: 20px;
}

.match-players {
    display: flex;
    align-items: center;
    justify-content: space-between;
    gap: 10px;
}

.match-player {
    flex: 1;
    text-align: center;
    font-size: 20px;
    font-weight: bold;
}

.vs {
    font-size: 18px;
    opacity: .6;
}

.score {
    text-align: center;
    font-size: 70px;
    font-weight: 900;
    margin: 15px 0;
}

.timer {
    text-align: center;
    font-size: 42px;
    font-weight: bold;
    margin: 10px 0;
}

.pause-text {
    text-align: center;
    color: #ffcc00;
    font-weight: bold;
    min-height: 22px;
}

.goal-buttons {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 10px;
}

.goal-buttons button {
    background: #16803c;
}

.undo {
    background: #8a5a00;
}

.end {
    background: #a52323;
}

.start {
    background: #16803c;
}

.pause {
    background: #805a00;
}

.back {
    background: #3a424b;
}

.chance-card {
    background: #222a32;
    border-radius: 14px;
    padding: 15px;
    margin: 12px 0;
    text-align: center;
}

.chances {
    display: grid;
    gap: 8px;
}

.chance {
    background: #2c353e;
    padding: 10px;
    border-radius: 10px;
}

.table-wrapper {
    overflow-x: auto;
}

table {
    width: 100%;
    border-collapse: collapse;
    min-width: 520px;
}

th,
td {
    padding: 10px 6px;
    text-align: center;
    border-bottom: 1px solid #303840;
}

th {
    background: #222a32;
}

.history-item {
    background: #222a32;
    border-radius: 12px;
    padding: 13px;
    margin-bottom: 10px;
}

.history-score {
    font-size: 24px;
    font-weight: bold;
    text-align: center;
    margin: 5px;
}

.result {
    text-align: center;
}

.result-score {
    font-size: 65px;
    font-weight: 900;
    margin: 20px 0;
}

input[type="text"] {
    width: 100%;
    padding: 13px;
    border-radius: 10px;
    border: 1px solid #3b444e;
    background: #222a32;
    color: white;
    font-size: 16px;
    margin: 8px 0;
}

.small {
    opacity: .7;
    font-size: 13px;
}

.stats-grid {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 10px;
}

.stats-grid > div {
    background: #222a32;
    border-radius: 12px;
    padding: 12px;
    text-align: center;
}

.stats-grid strong {
    display: block;
    font-size: 21px;
}

.stats-grid span {
    display: block;
    font-size: 12px;
    opacity: .7;
    margin-top: 4px;
}

.ranking-card {
    margin-bottom: 15px;
}

.trophy-player-grid {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 10px;
}

.player-trophy-button {
    display: flex;
    justify-content: space-between;
    align-items: center;
    background: #222a32;
}

.trophy-grid {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 12px;
}

.trophy-card {
    text-align: center;
    padding: 15px;
    background: #222a32;
    border-radius: 15px;
}

.trophy-big {
    font-size: 45px;
}

.record-grid {
    display: grid;
    gap: 15px;
}

.record-card {
    text-align: center;
}

.record-icon {
    font-size: 45px;
}

.record-value {
    font-size: 42px;
    font-weight: 900;
    margin: 8px 0;
}

@media (max-width: 500px) {

    .trophy-player-grid,
    .trophy-grid {
        grid-template-columns: 1fr;
    }

    .score {
        font-size: 60px;
    }

}

</style>
</head>

<body>


<!-- =========================
     TABELA
========================= -->

<div id="tableScreen" class="screen">

    <div class="container">

        <h1>⚽ GOALRUSH</h1>

        <div class="card">

            <h2 id="leagueTitle">
                GOALRUSH
            </h2>

            <div class="table-wrapper">

                <table>

                    <thead>

                        <tr>
                            <th>#</th>
                            <th>ZAWODNIK</th>
                            <th>M</th>
                            <th>W</th>
                            <th>R</th>
                            <th>P</th>
                            <th>GZ</th>
                            <th>GS</th>
                            <th>+/-</th>
                            <th>PKT</th>
                            <th>WR</th>
                        </tr>

                    </thead>

                    <tbody id="leagueTable"></tbody>

                </table>

            </div>

        </div>


        <button onclick="goToPlayers()">
            ⚽ NOWY MECZ
        </button>

        <button onclick="showStats()">
            📊 STATYSTYKI
        </button>

        <button onclick="showHistory()">
            📜 HISTORIA MECZÓW
        </button>

        <button onclick="showLeaderboards()">
            🏅 RANKINGI
        </button>

        <button onclick="showRecords()">
            🏆 REKORDY GOALRUSH
        </button>

        <button onclick="showTrophies()">
            🏆 TROFEA
        </button>

        <button onclick="newTable()">
            ➕ NOWA TABELA
        </button>

    </div>

</div>


<!-- =========================
     WYBÓR ZAWODNIKÓW
========================= -->

<div id="playersScreen" class="screen">

    <div class="container">

        <h1>👥 WYBIERZ ZAWODNIKÓW</h1>

        <div class="card">

            <p>
                Wybierz minimum 3 zawodników.
            </p>

            <div class="players">

                <div class="player-box">
                    <label>
                        <input type="checkbox" value="Kamil">
                        Kamil
                    </label>
                </div>

                <div class="player-box">
                    <label>
                        <input type="checkbox" value="Kuba">
                        Kuba
                    </label>
                </div>

                <div class="player-box">
                    <label>
                        <input type="checkbox" value="Michał">
                        Michał
                    </label>
                </div>

                <div class="player-box">
                    <label>
                        <input type="checkbox" value="Marcel">
                        Marcel
                    </label>
                </div>

            </div>

        </div>


        <button class="start" onclick="drawMatch()">
            🎲 LOSUJ MECZ
        </button>

        <button class="back" onclick="showTable()">
            ↩️ WRÓĆ DO TABELI
        </button>

    </div>

</div>
