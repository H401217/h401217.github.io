# Pou 3D web API (WIP)
You can see Pou 2D API [here](./api.html)

The main endpoint for the API is `https://app.pou3d.me/app`
Current version for 1.0.84 is "84"

## Important notes
* IDs aren't numeric in Pou 3D, for example: `1Z5fK5yI` is the player ID for H40dev (my Pou 3D acc ^_^)
* There is an `s` value in the links that sometimes is the cookie and other times it's the cookie fused with the player ID
  * Cookie example: DzCy9k3ZIyXn324EOrUvNH
  * ID example: 1a2b3c4d
  * Sometimes the `s` value is `DzCy9k3ZIyXn324EOrUvNH1a2b3c4d` and other times just `DzCy9k3ZIyXn324EOrUvNH`. But in (almost) all the links it will use the cookie+ID fusing unless told otherwise.

## Links
Almost all links have the following queries

|Query|Description|Value|
|-|-|-|
|c|Main version|1|
|v|Subversion (or update)|84 (for 1.0.84)|
|s|Cookie or Cookie+ID|explained in [important notes](#important-notes)|

Example link with the default queries:

`https://app.pou3d.me/app/utl/genCap?c=1&v=84`

### Misc

`/eml/chkReg`

Checks if an email is registered in Pou 3D
|Query|Description|Example|
|-|-|-|
|em|Email to check|example%40example.com|
|ac|Action (defaults to "rg")|rg|

(This doesnt use cookies)
<br><br>

`/utl/genCap`

Generates a CAPTCHA for registration (idk how to read the image)

(This doesn't use cookies)
<br><br>

`/reg/emlCap`

Registers an account after completing a CAPTCHA
|Query|Description|Example|
|-|-|-|
|em|Email to check|example%40example.com|
|ac|Action (defaults to "rg")|rg|
|`cI`|CAPTCHA ID (from genCap)|x6ghlo|
|cA|CAPTCHA answer|vjomh|

(This doesn't use cookies)

---
### aPu (account Pou) -> (non dangerous account actions)
These links now require cookies

`/aPu/chgNik`

Changes Pou nickname
|Query|Description|Example|
|-|-|-|
|`pI`|Player ID|`1Z5fK5yI`|
|nk|New nickname|pou_abcdef|

(This uses Cookie without the ID)
<!-- Havent checked the statement above me-->
<br>

`/aPu/sav`

Saves Pou progress (idk if it uses HTTP POST like the 2D game)
|Query|Description|Example|
|-|-|-|
|gN|??? (defaults to 1)|1|
<br>

`/aPu/png`

Returns Pou PNG

---
### acc (other account actions)

`/acc/chgPwd`

Changes account password
|Query|Description|Example|
|-|-|-|
|pw|Password in MD5|5eb63bbbe01eeed093cb22bb8f5acdc3 (`hello world` hashed to MD5)|

(This uses Cookie without ID)
<br><br>

`/acc/inf`

Account info

(This uses Cookie without ID)

---
### pos (Pou searching and lists)
This uses cookie with ID

`/pos/pop`

Returns a list of most popular Pous (or top likes)
|Query|Description|Example|
|-|-|-|
|sp|List option|ppW (week popular)<br>ppM (month popular)<br>ppA (all time popular)<br>lkA (top likes)|

<br>

`/pos/sch`

Searches a Pou by nickname
|Query|Description|Example|
|-|-|-|
|nk|Nickname|Pou|

<br>

`/pos/rnd`

Returns a random Pou
|Query|Description|Example|
|-|-|-|
|vs|??? (defaults to 1)|1|
---
### pou (actions with other players)
`/pou/stt`

Pou status? (won't risk the ban xd)
|Query|Description|Example|
|-|-|-|
|pI|Player ID (probably own ID)|1Z5fK5yI|

<br>

**To simplify, all links below (in this section) have the following additional query:**

|Query|Description|Example|
|-|-|-|
|id|Player ID (can be your own or from other)|puDANxgE (Doradingo's ID)|

<br>

`/pou/vis`

Visits a Pou
<br><br>

`/pou/lik`

Likes a Pou
<br><br>

`/pou/ulk`

Unlikes a Pou
<br><br>

`/pou/mgR`

Returns messages the Player received
<br><br>

`/pou/mgS`

Returns messages the Player sent
<br><br>

`/pou/msg`

Sends a message to a Pou guest book
|Query|Description|Example|
|-|-|-|
|`mI`|Message ID (numerical)|1 (not sure about the other ones)|

<br>

`/pou/vtd`

Shows what Pous did the player visit
<br><br>

`/pou/vtr`

Shows what Pous visited the player
<br><br>

`/pou/lkd`

Shows what Pous the player likes
<br><br>

`/pou/lkr`

Shows whart Pous like the player
<br><br>

`/pou/fav`

Shows the favorite Pous from the player

---
### gam (Top Score)
`/gam/rkg`

Returns the minigame leaderboard
|Query|Description|Example|
|-|-|-|
|gm|Game ID|`3_1` (food drop)|
|sp|Time selection|`tpW` (week)<br>`tpM` (month)<br>`tpA` (all time)<br>`fvA` (favorites)|
|dt|??? maybe timestamp|`1a` for week (idk)<br>`19` for month (idk)<br>(this was made on august 31th 2026 so maybe it gives a hint)|

The links were found using memory dump
<!-- * /pou/mgS?id=puDANxgE&mI=1&c=1&v=60&s=COOKIEPLAYERID (visit id is from doradingo) -->
