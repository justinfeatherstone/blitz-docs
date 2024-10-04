_bico


#### Blitz - Dev Log Entry 01

Date: 2024-10-03

**Project Overview**

Blitz is a personal project aimed at creating a fantasy football app which usefully and elegantly leverages data-science in the User’s favor. The project involves developing a native app architecture and integrating real-time NFL statistics.

**Native App Architecture**

Currently working on the file structure for the native app
Need to further define the components and their interactions

**API Integration**

We're focusing on integrating real-time NFL statistics using the Tank01 API 1. Key endpoints we're working with include:

##### **In-Game Real Time NFL Statistics:**

> [!example] 
> 
> Get Fantasy Point Projections
> Get Player List
Get Player Information
Get General Game Information
Get NFL Games and Stats For a Single Player
Get NFL Team Roster
Get NFL Teams



The "Get NFL Teams" endpoint requires careful handling due to its extensive data return [2].


Current Focus Areas

Setting up the basic app structure
Implementing API calls to fetch real-time NFL data
Designing the user interface for displaying fantasy football information

Challenges and Considerations

Data Management: Handling large datasets returned by some API endpoints
Real-time Updates: Ensuring the app can handle frequent updates during live games
User Experience: Designing an intuitive interface for managing fantasy teams and viewing stats

Next Steps

Complete the basic app structure
Implement and test API integrations
Begin work on the user interface design
Consider adding features like player comparisons or team analytics

Notes

~~Explored the [[ESPN Fantasy Football API (v3)]] but noted potential legal concerns [3]. Will Need to investigate further before considering integration.~~

B

Yeah.... no thanks disney
