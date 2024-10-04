## NFL Live In-Game Real Time Statistics NFL ([[https://rapidapi.com/tank01/api/tank01-nfl-live-in-game-real-time-statistics-nfl|Docs]]) - Tank01 



### **API Endpoints/**
### Get NFL Teams

###### *****   **==WARNING: THIS CALL HAS MANY OPTIONS AND CAN RETURN A LOT OF DATA! Running this in the rapidAPI UI with all options set to "true" will most likely crash the UI.**== ***** 

###### This call will retrieve the list of NFL teams. Included is their name, city, abbreviation, and teamID which can be used in other calls. Their current record and current W/L streak is included as well. Optional data that can be included are the team rosters and their schedules. Included in team rosters is all players injuries. /getNFLTeams Optional parameters are ?schedules=true returns team schedule rosters=true includes current roster topPerformers=true This will return the best player for each statistical category on each team. teamStats=true This will return team level/season long stats for each team

###### **example GET**:

```js
import axios from 'axios'; const options = { method: 'GET', url: 'https://tank01-nfl-live-in-game-real-time-statistics-nfl.p.rapidapi.com/getNFLTeams', params: { sortBy: 'standings', rosters: 'false', schedules: 'false', topPerformers: 'true', teamStats: 'true', teamStatsSeason: '2023' }, headers: { 'x-rapidapi-key': 'Sign Up for Key', 'x-rapidapi-host': 'tank01-nfl-live-in-game-real-time-statistics-nfl.p.rapidapi.com' } }; try { const response = await axios.request(options); console.log(response.data); } catch (error) { console.error(error); }
```

example 


### Get Player List
#### 
### Get Weekly NFL Schedule
### Get Fantasy Point Projections
### Get NFL Team Roster
### Get ADP
### Get NFL Game Box Score
### Get General Game Information
### Get NFL Depth Charts
### Get NFL Betting Odds
### Get Top News and Headlines
### Get NFL Game Box Score - Live Real Time
### Get NFL Team Schedule
### Get Daily NFL Schedule
### Get Player Information
### Get NFL Games and Stats For a Single Player
