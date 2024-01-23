# Pou vs Pou

## What is Pou vs Pou (PvP)?

Pou vs Pou is a way of playing Pou minigames with other people near you that have Pou app installed in their device.
The connection between the clients/players is faster and designed to make a consistent multiplayer match between a specified number of Pous.

Only certain games allow Pou vs Pou
- Beach Volley (max 2 players) (ID 31)
- Sky Hop (max 4 players) (ID 20)
- Water Hop (max 4 players) (ID 19)
- Pet Walk (max 2 players) (ID 24)

Unlike Tic Tac Pou and Four Pous, Pou vs Pou allows a faster data transmission between clients, and, therefore, a real time synchronization between the clients actions in the game that requires quicker action.

Pou vs Pou can be used with Wi-Fi or Bluetooth; in this documentation I only used Wi-Fi connection, so I don't exactly know how does PvP work in Bluetooth. The match creator can put a password to their match so only players who know the password can join the match.

## Connection

Pou vs Pou uses both UDP and TCP to make connections.

It uses UDP to get all the available matches from a specified game.

In this documentation, a Beach Volley connection will be used as example

### UDP connection

The client UDP uses the port 17110 to broadcast a message to all receivers with the port 27110.
The client sends the message to a broadcast IP, which could be 255.255.255.255

Let's see the following process:

Client with port 17110 broadcasts the following message to receivers with port 27110
```json
{"gI":31,"rN":123456,"mC":"78bc9e8656e98950a280fa30bd2e4c45"}
```
The previous JSON has these three following elements

| Name|Description|Example|
| -|-|-|
| gI|Is the Game ID|31|
| rN|Is a random number between 1 and 2147483647|31241441|
| mC|It's a MD5 hash of the string "p0v"+rN+"s"|78bc9e8656e98950a280fa30bd2e4c45|

As you can see, the third element (mC) is a bit complicated than the other elements.
The "mC" element can be explained as a function, like the one mentioned below.
```js
function client_mC(rN) {
	return MD5( "p0v"+rN+"s" )
}
```

The function above makes a MD5 hash of joined strings, the "+" symbol means, in this case, joining a string, so, the "rN" number should be converted to a string.

After the client broadcasted the message, a server should return another JSON data. In this case, it should send the data to the client IP and Port.

```json
{"n":"Beach Volley 123","mC":"ad4a70d68dd9fbf81e7cf9ab5c6eab64"}
```

| Name|Description|Example|
| -|-|-|
| n|The match name|Beach Volley 123|
| mC|It's a MD5 hash of the string "p0v"+rN+"m"|ad4a70d68dd9fbf81e7cf9ab5c6eab64|

But in this case, the "mC" hash element is different. Because instead of the previous string join (**"p0v"+rN+"s"**), it joins the strings **"p0v"+rN+"m"** (remember that rN should be converted to string).

```js
function server_mC(rN) {
	return MD5( "p0v"+rN+"m" )
}
```

Pou app uses the "n" element to display the match name in a list of available matches. And it checks if the "mC" element is equal to the previous MD5 hash.

The client also receives the IP of the server, that can be used for connecting (the IP is not directly in the JSON, instead, UDP receives it)

### TCP connection

Before starting, you must remember that Pou uses a specific formatting for its messages, to avoid issues like wrong formatted data due to accidentally joined fragments of data.

The message formatting goes like this:
```json
code|json#
```
In this case, "code" should be a number that specifies the type of message (connecting, disconnecting, kick, etc). And json should be replaced by a JSON string with the message data, this field should always be a JSON, even when you don't send data (you can use an empty JSON in this case).

The characters "|" and "#" act as separators, the vertical line ("|") separates the code and the json, and the hashtag ("#") separates the entire message.

Separating messages is important because in TCP you can send and receive the available data, so, the data received may be a lot of joined messages, that should be readed separately to avoid errors.

---

First, your TCP client can have any port, unlike the UDP client limited only to 17110.
Your TCP client should connect to the server IP, with its port being **37110**

After that you should start receiving the first message.

```json
211|{"pI":1,"mC":"de8fdcdf7639b0e1670e88a1acf3e09d"}#
```

| Item|Value|Description|
| -|-|-|
| Code|211|Handshake 1a (Server)|
| |||
| "pI"|1|Player ID? (used in next hash)|
| "mC"|de8fdcdf7639b0e1670e88a1acf3e09d|MD5 hash of joined strings "p0v"+pI+"m"|

Remember that the Pou app checks if the MD5 hashes are correct by recreating them.
After that message, the client should return the next message
```json
212|{"n":"username","mC":"MD5"}#
```

| Item|Value|Description|
| -|-|-|
| Code|212|Handshake 1a (Client)|
| |||
| "n"|username|Client Username (can be random if not logged in)|
| "mC"|c850985b4feec96795367cf9f6a67de4|MD5 hash of joined strings "p0v"+pI+"s"|

This hash creation uses the "pI" value of the previous server message (code 211).
After that, the server returns another message.

```json
213|{"n":"username2"}#
```

| Item|Value|Description|
| -|-|-|
| Code|213|Handshake 1b (Server)|
| |||
| "n"|username2|Match creator Username|

The message tells the client about the creator name.

The client should reply with its own info (match, avatar, version)

```json
311|{"gI":31,"gV":1,"pD":{"sz":1,"ob":0,"bCo":1,"eCo":1,"ouf":0,"hat":0}}#
```

| Item|Value|Description|
| -|-|-|
| Code|311|Handshake 2 (Client)|
| |||
| "gI"|31|The game ID|
| "gV"|1|Game Version (default is 1)|
| "pD"|JSON|Client Pou avatar (also known as "minI" or "minInfo")|
| "p"|5f4dcc3b5aa765d61d8327deb882cf99|Match Password in MD5 (only send if server asks you)|
The "pD" value is a JSON containing the avatar, here are some possible values that you can add. You can also set the value as an empty JSON "{}" but other players will only see you as 2 floating red eyes.

| Item|Value|Description|
| -|-|-|
| "sz"|1|Pou Size (from 0.5 to 1)|
| "ob"|0|Pou Obesity (from 0 to 1)|
| "bCo"|1|Body Color (ID)|
| "eCo"|1|Eye Color (ID)|
| "ouf"|0|Outfit (ID)||
| "hat"|0|Hat (ID)|

After that, the server should return data about the match (avatar, title, opponents)
```json
312|{"ok":true,"gT":"Beach Volley 123","mD":{"sz":0.7,"ob":1,"bCo":10,"eCo":2},"mNW":0,"oS":[]}#
```

| Item|Value|Description|
| -|-|-|
| Code|312|Handshake 2 (Server)|
| |||
| "wP"|true|WrongPassword/WithPassword. If true then you should send a password message (Code 311)|
| "bPD"|true|Wrong "pD" value sent error|
| "dGV"|true|Different game version (gV)|
| "wG"|true|Wrong Game ID (gI)|
| "gF"|true|Game is Full|
| |||
| "ok"|true/false|Success|
| "gT"|Beach Volley 123|The match title|
| "mD"|JSON|Match Creator Avatar|
| "mNW"|0|Unknown|
| "oS"|Array|Array of opponents|

The array of opponents can have a JSON
```json
{"i":1,"n":"stranger","d":{},"nW":0}
```

TBD

another server messages if you understand

```json
313|{"i":1,"n":"stranger","d":{}}#
```

| Item|Value|Description|
| -|-|-|
| Code|313|Player Joined|
| |||
| "i"|1|ID assigned by Host|
| "n"|"stranger"|Player Name|
| "d"|JSON|Player avatar/minInfo|

```json
321|{}#
```

| Item|Value|Description|
| -|-|-|
| Code|321|Match Close|

```json
322|{"pI":1}#
```

| Item|Value|Description|
| -|-|-|
| Code|321|Player leaved|
| |||
| "pI"|322|ID of Player who leaved|


```json
323|{}#
```

| Item|Value|Description|
| -|-|-|
| Code|323|You got Kicked|


```json
324|{"pI":1}#
```

| Item|Value|Description|
| -|-|-|
| Code|324|Other Player Kicked|
| |||
| "pI"|1|Player ID (assigned by host)|
---
```json
341|{}#
```
This is sky hop ready, it can contain data
```json
342|{}#
```
match start

```json
422|{}#
```
sky hop data update

---
more data
---

BEACH VOLLEY DATA

it is a json with the data update lol
```txt
note: rotation is anti clockwise and in radians
(client processes physics for smooth perfomance)

matcher = player who created match
opponent = player who joined

grid = 15x5 (y can be infinite)
speed = near 5.5

json data keys

mX = matcher X position
mY = matcher Y position
mVX = matcher X force (right)
mVY = matcher Y force (up)

oX = opponent X position
oY = opponent Y position
oVX = opponent X force
oVY = opponent Y force

bX = ball X position
bY = ball Y position
bVX = ball X force
bVY = ball Y force
bA = ball current angle
bAV = ball angle acceleration
bGS = ball gravity (integer) (default is 1)
```

note: these are the pvp games ordered from easiest to hardest to make a bot

* pet walk - you only need to put the right number (that represents an obstacle)
* water hop - you need to check if you can move 1 space or 2 if there isn't a floater
* sky hop - you need to check if you need to move to left or right, and the pattern goes 4-3-4-3-4-3 and so on, also the pattern can start with 4 or 3 depending of the available players
* beach volley - you need to recreate the game physics to get an aproximate of the ball and players position
