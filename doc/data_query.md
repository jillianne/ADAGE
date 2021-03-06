#ADAGE Client Data Queries

These queries have been set up to be useful from a client to retrieve data stored by that game. Requests must come from an authenticated client with a valid and authenticated account. 

##GET /data/get_events.json

General query to get events logged for a game.


###Request
<table>
    <tr> 
        <th>params</th>
        <th>type</th>
        <th>description</th>
    </tr>
    <tr>
        <td>app_token</td>
        <td>string</td>
        <td>Token that identifies the client application</td>
    </tr>
     <tr>
        <td>time_range</td>
        <td>string</td>
        <td>How far back in time to query. Can contain a timestamp or the following keywords "hour", "day", "week", "month". For all events pass 0</td>
    </tr>
    <tr>
        <td>events_list (optional)</td>
        <td>list of strings</td>
        <td>A list of all the events to query. If not passed it will return all events</td>
    </tr>
    <tr>
        <td>game_id (optional)</td>
        <td>string</td>
        <td>scope the query just to a particular game id</td>
    </tr>
</table>

###Response

A list of all the logged events as json. Will be empty if no events were returned in the query and will return standard error structure if the application is not found or the player can not be authenticated.

##GET /data/get_sorted_and_limited_events.json

A query that will allow you to get a list of events sorted by the value of a field in the event and limit the number of events returned. 


###Request
<table>
    <tr> 
        <th>params</th>
        <th>type</th>
        <th>description</th>
    </tr>
    <tr>
        <td>app_token</td>
        <td>string</td>
        <td>Token that identifies the client application</td>
    </tr>
     <tr>
        <td>time_range</td>
        <td>string</td>
        <td>How far back in time to query. Can contain a timestamp or the following keywords "hour", "day", "week", "month". For all events pass 0</td>
    </tr>
    <tr>
        <td>key</td>
        <td>strings</td>
        <td>Name of the event you are querying for</td>
    </tr>
    <tr>
        <td>field_name</td>
        <td>string</td>
        <td>The name of the field on the event to sort by. Sort results for non-numeric values may not give the results you would expect.</td>
    </tr>
     <tr>
        <td>start</td>
        <td>integer</td>
        <td>The index you want to start the results with 0 would be the first result.</td>
    </tr>
     <tr>
        <td>limit</td>
        <td>integer</td>
        <td>The number of results you want returned.</td>
    </tr>
     <tr>
        <td>user_id (optional)</td>
        <td>integer</td>
        <td>Limit the query to only the user with this id</td>
    </tr>
</table>

###Response

A list of the requested events as json. Will be empty if no events were returned in the query and will return standard error structure if the application is not found or the player can not be authenticated.

##GET /data/get_game_ids

Query for all the game ids from the specificed time application and time range.


###Request
<table>
    <tr> 
        <th>params</th>
        <th>type</th>
        <th>description</th>
    </tr>
    <tr>
        <td>app_token</td>
        <td>string</td>
        <td>Token that identifies the client application</td>
    </tr>
     <tr>
        <td>time_range</td>
        <td>string</td>
        <td>How far back in time to query. Can contain a timestamp or the following keywords "hour", "day", "week", "month". For all events pass 0</td>
    </tr>
</table>

###Response

A list of all the game ids created for the application in the time given time range.

##GET /data/field_values

Get the values of a field from a key over a given time range time. Responds to the formats json or csv. Using the optional rickshaw=true param with the json format it will respond with json formated for a rickshaw graph.

###Request
<table>
    <tr> 
        <th>params</th>
        <th>type</th>
        <th>description</th>
    </tr>
    <tr>
        <td>app_token</td>
        <td>string</td>
        <td>Token that identifies the client application</td>
    </tr>
     <tr>
        <td>time_range</td>
        <td>string</td>
        <td>How far back in time to query. Can contain a timestamp or the following keywords "hour", "day", "week", "month". For all events pass 0</td>
    </tr>
     <tr>
        <td>key</td>
        <td>string</td>
        <td>The key of the event that has the field.</td>
    </tr>
    <tr>
        <td>field_names</td>
        <td>List of Strings</td>
        <td>This is a list of field names, this allows the option to dig down to a nested field using the names of all the fields along the way to the final desired field</td>
    </tr>
    <tr>
        <td>game_id</td>
        <td>string (optional)</td>
        <td>Restricts the query to just the game specified. Will also adjust the time range to be from the start of the game and will trigger a query for the ADAGEGameInformation. Rickshaw json will use the information about player color and player name form the ADAGEGameInformation if found.</td>
    </tr>
    <tr>
        <td>rickshaw (optional)</td>
        <td>bool</td>
        <td>If used in combo with a request for json it will return json formated for use with a rickshaw graph</td>
    </tr>
    
</table>


###Response

json or csv containing the values of the field over time. 
