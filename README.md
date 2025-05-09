# SQL-Progress-Journal-day-23

# Project: ROI Analysis for MLB Players (2001)

## Overview:
This project focuses on calculating and analyzing the Return on Investment (ROI) for Major League Baseball (MLB) players in the 2001 season. Specifically, the ROI is calculated based on the number of home runs hit by players in relation to their salary. The goal of this analysis is to identify which players were the most "efficient" in terms of performance (home runs) relative to the salary paid to them. This could provide valuable insights for team management in making salary decisions.

## Data Used:
- **Performances Table**: Contains the number of home runs (HR) for each player in 2001.
- **Salaries Table**: Contains the salary of each player for the 2001 season.
- **Players Table**: Contains player details, including names.

## Methodology:
1. **Data Extraction**: 
   - We joined the **performances** and **salaries** tables on the player_id, and filtered the data to include only players who performed in the 2001 season.
   - We joined the **players** table to obtain player names.

2. **ROI Calculation**: 
   - For each player, the ROI was calculated as the ratio of home runs (HR) to salary.
   - The ROI was then expressed as a percentage to make it easier to interpret.

3. **Final Result**: 
   - The top 10 players were ranked based on their ROI percentage, highlighting the players who provided the most value in terms of home runs for the money they earned.

## SQL Query:

```sql
SELECT pf.player_id, HR, pf.year, s.salary, p.first_name, p.last_name, 
ROUND((1.0 * HR) / s.salary * 100000, 4) AS efficiency_percentage
FROM performances pf
JOIN salaries s ON pf.player_id = s.player_id AND pf.year = s.year
JOIN players p ON s.player_id = p.id
WHERE pf.year = 2001
ORDER BY efficiency_percentage DESC
LIMIT 10;

| player_id | HR | year | salary | first_name | last_name | efficiency_percentage |
+-----------+----+------+--------+------------+-----------+-----------------------+
| 15102     | 37 | 2001 | 200000 | Albert     | Pujols    | 18.5                  |
| 15250     | 34 | 2001 | 285000 | Aramis     | Ramirez   | 11.9298               |
| 8885      | 27 | 2001 | 230000 | Torii      | Hunter    | 11.7391               |
| 1353      | 34 | 2001 | 305000 | Lance      | Berkman   | 11.1475               |
| 10956     | 25 | 2001 | 230000 | Paul       | Lo Duca   | 10.8696               |
| 1991      | 20 | 2001 | 219000 | Russell    | Branyan   | 9.1324                |
| 10154     | 26 | 2001 | 300000 | Corey      | Koskie    | 8.6667                |
| 6689      | 15 | 2001 | 200000 | Jay        | Gibbons   | 7.5                   |
| 18902     | 25 | 2001 | 335000 | Bubba      | Trammell  | 7.4627                |
| 5771      | 19 | 2001 | 255000 | Robert     | Fick      | 7.451                 |
+-----------+----+------+--------+------------+-----------+-----------------------+
