<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Medicine Schedule</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 0;
            padding: 20px;
            background-color: black;
            display: flex;
            justify-content: center;
            align-items: center;
            min-height: 100vh;
            color: white;
        }

        .table-container {
            width: 100%;
            max-width: 1200px;
            overflow-x: auto;
            overflow-y: auto;
            background-color: black;
            border-radius: 10px;
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
            padding: 10px;
            max-height: 80vh;
        }

        table {
            width: 100%;
            border-collapse: collapse;
            background-color: black;
            position: relative;
        }

        th, td {
            padding: 12px 15px;
            text-align: left;
            border: 1px solid #ddd;
            background-color: black;
            color: white;
        }

        th {
            background-color: #0078d7;
            color: white;
            font-size: 1rem;
            position: sticky;
            top: 0;
            z-index: 2;
        }

        tr {
            transition: all 0.3s ease;
        }
tr:hover {
    background-color: #5EDE9E !important;  /* Updated hover color */
    transform: scale(1.20);
}

td {
    background-color: black;  /* Ensure the individual td has no background color override */
}


        td {
            font-size: 0.9rem;
        }

        .highlight {
            background-color: #E993BE !important;
            animation: blink 1s linear 10;
        }

        @keyframes blink {
            50% {
                opacity: 0.5;
            }
        }

        @media (max-width: 768px) {
            th, td {
                font-size: 0.8rem;
                padding: 10px;
            }

            .table-container {
                padding: 5px;
            }
        }
    </style>
</head>
<body>
    <div class="table-container">
        <table>
            <thead>
                <tr>
                    <th>S.No</th>
                    <th>Tablet Name</th>
                    <th>Morning/Noon</th>
                    <th>Evening</th>
                </tr>
            </thead>
            <tbody>
                <tr>
                    <td>8</td>
                    <td>Pantocid 40mg</td>
                    <td>✔ Before Breakfast</td>
                    <td></td>
                </tr>
                <tr>
                    <td>2</td>
                    <td>Pan 40 (gas tablet)</td>
                    <td>✔ 7:00 AM</td>
                    <td></td>
                </tr>
                <tr>
                    <td>6</td>
                    <td>Stiloz 100mg</td>
                    <td>✔ 7:00 AM</td>
                    <td>✔ 7:00 PM</td>
                </tr>
                <tr>
                    <td>5</td>
                    <td>Trental 400mg</td>
                    <td>✔ 8:00 AM</td>
                    <td>✔ 8:00 PM</td>
                </tr>
                <tr>
                    <td>4</td>
                    <td>Meaxon Plus</td>
                    <td>✔ 9:00 AM</td>
                    <td></td>
                </tr>
                <tr>
                    <td>9</td>
                    <td>Bio D 3 Plus</td>
                    <td>✔ 11:00 AM</td>
                    <td></td>
                </tr>
                <tr>
                    <td>11</td>
                    <td>Cranpac</td>
                    <td>✔ After Lunch (1:00 PM)</td>
                    <td></td>
                </tr>
                <tr>
                    <td>7</td>
                    <td>A to Z</td>
                    <td>✔ 2:00 PM</td>
                    <td></td>
                </tr>
                <tr>
                    <td>12</td>
                    <td>Trajenta</td>
                    <td>✔ After Lunch (2:00 PM)</td>
                    <td></td>
                </tr>
                <tr>
                    <td>3</td>
                    <td>Eido Fe 100mg</td>
                    <td>✔ 4:00 PM</td>
                    <td></td>
                </tr>
                <tr>
                    <td>10</td>
                    <td>Razel or Rosuvas</td>
                    <td></td>
                    <td>✔ Bedtime</td>
                </tr>
                <tr>
                    <td>13</td>
                    <td>Tab 4 Abrad</td>
                    <td></td>
                    <td>✔ Before Dinner</td>
                </tr>
            </tbody>
        </table>
    </div>
    <script>
        function checkAndHighlight() {
            const now = new Date();
            const currentMinutes = now.getHours() * 60 + now.getMinutes();
            const rows = document.querySelectorAll("tbody tr");

            rows.forEach(row => {
                const cells = row.querySelectorAll("td");
                cells.forEach(cell => {
                    const timeMatch = cell.textContent.match(/(\d{1,2}):(\d{2}) (AM|PM)/);
                    if (timeMatch) {
                        let [_, hours, minutes, period] = timeMatch;
                        hours = parseInt(hours, 10);
                        minutes = parseInt(minutes, 10);
                        if (period === 'PM' && hours !== 12) hours += 12;
                        if (period === 'AM' && hours === 12) hours = 0;
                        const cellMinutes = hours * 60 + minutes;

                        if (Math.abs(currentMinutes - cellMinutes) <= 25) {
                            cell.classList.add("highlight");
                        }
                    }
                });
            });
        }

        setInterval(checkAndHighlight, 60000); // Check every minute
        checkAndHighlight(); // Initial check
    </script>
</body>
</html>


