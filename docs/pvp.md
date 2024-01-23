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
|Name|Description|Example|
|-|-|-|
|gI|Is the Game ID|31|
|rN|Is a random number between 1 and 2147483647|31241441|
|mC|It's a MD5 hash of the string "p0v"+rN+"s"|78bc9e8656e98950a280fa30bd2e4c45|

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
|Name|Description|Example|
|-|-|-|
|n|The match name|Beach Volley 123|
|mC|It's a MD5 hash of the string "p0v"+rN+"m"|ad4a70d68dd9fbf81e7cf9ab5c6eab64|

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
|Item|Value|Description|
|-|-|-|
|Code|211|Handshake 1a (Server)|
||||
|"pI"|1|Player ID? (used in next hash)|
|"mC"|de8fdcdf7639b0e1670e88a1acf3e09d|MD5 hash of joined strings "p0v"+pI+"m"|

Remember that the Pou app checks if the MD5 hashes are correct by recreating them.
After that message, the client should return the next message
```json
212|{"n":"username","mC":"MD5"}#
```

|Item|Value|Description|
|-|-|-|
|Code|212|Handshake 1a (Client)|
||||
|"n"|username|Client Username (can be random if not logged in)|
|"mC"|c850985b4feec96795367cf9f6a67de4|MD5 hash of joined strings "p0v"+pI+"s"|

This hash creation uses the "pI" value of the previous server message (code 211).
After that, the server returns another message.

```json
213|{"n":"username2"}#
```

|Item|Value|Description|
|-|-|-|
|Code|213|Handshake 1b (Server)|
||||
|"n"|username2|Match creator Username|

The message tells the client about the creator name.

The client should reply with its own info (match, avatar, version)

```json
311|{"gI":31,"gV":1,"pD":{"sz":1,"ob":0,"bCo":1,"eCo":1,"ouf":0,"hat":0}}#
```

|Item|Value|Description|
|-|-|-|
|Code|311|Handshake 2 (Client)|
||||
|"gI"|31|The game ID|
|"gV"|1|Game Version (default is 1)|
|"pD"|JSON|Client Pou avatar (also known as "minI" or "minInfo")|

The "pD" value is a JSON containing the avatar, here are some possible values that you can add.

|Item|Value|Description|
|-|-|-|
|"sz"|1|Pou Size (from 0.5 to 1)|
|"ob"|0|Pou Obesity (from 0 to 1)|
|"bCo"|1|Body Color (ID)|
|"eCo"|1|Eye Color (ID)|
|"ouf"|0|Outfit (ID)||
|"hat"|0|Hat (ID)|

After that, the server should return data about the match (avatar, title, opponents)
```json
312|{"ok":true,"gT":"Beach Volley 123","mD":{"sz":0.7,"ob":1,"bCo":10,"eCo":2},"mNW":0,"oS":[]}#
```
|Item|Value|Description|
|-|-|-|
|Code|312|Handshake 2 (Server)|
||||
|"ok"|true/false|Success|
|"gT"|Beach Volley 123|The match title|
|"mD"|JSON|Match Creator Avatar|
|"mNW"|0|Unknown|
|"oS"|Array|Array of opponents|

TBD