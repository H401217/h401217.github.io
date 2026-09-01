# Pou 3D web API (WIP)
You can see Pou 2D API [here](./api.html)

The main endpoint for the API is `https://app.pou3d.me/app`
Current version for 1.0.84 is "84"

## Important notes
* IDs aren't numeric in Pou 3D, for example: `1Z5fK5yI` is the player ID for H40dev (my Pou 3D alt acc ^_^)
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

`/acc/chgPwd`?pw=MD5PASSWORD&c=1&v=60&s=COOKIE

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
i gave up bc i have homework rn
* /pos/pop?sp=ppW&c=1&v=60&s=COOKIEPLAYERID (popular by week)
* /pos/pop?sp=ppM&c=1&v=60&s=COOKIEPLAYERID (popular by month)
* /pos/pop?sp=ppA&c=1&v=60&s=COOKIEPLAYERID (popular all time)
* /pos/pop?sp=lkA&c=1&v=60&s=COOKIEPLAYERID (top likers?)
* /pos/sch?nk=abc&c=1&v=84&s=CPID (search)
* /pos/rnd?vs=1&c=1&v=84&s=CPID (random)

* /pou/stt?pI=0elidNcC&c=1&v=60&s=COOKIEPLAYERID
* /pou/vis?id=puDANxgE&c=1&v=60&s=COOKIEPLAYERID (visit id is from doradingo)
* /pou/lik?id=puDANxgE&c=1&v=60&s=COOKIEPLAYERID (visit id is from doradingo)
* /pou/ulk?id=puDANxgE&c=1&v=60&s=COOKIEPLAYERID (visit id is from doradingo)
* /pou/mgR?id=puDANxgE&c=1&v=60&s=COOKIEPLAYERID (visit id is from doradingo)
* /pou/mgS?id=1Z5fK5yI&c=1&v=84&s=COOKIEPLAYERID (messages you sent?)
* /pou/msg?id=puDANxgE&mI=1&c=1&v=60&s=COOKIEPLAYERID (visit id is from doradingo)
* /pou/mgS?id=puDANxgE&mI=1&c=1&v=60&s=COOKIEPLAYERID (visit id is from doradingo)
* /pou/vtd?id=ID&c=1&v=84&s=COOKIEPLAYERID (who you visited)
* /pou/vtr?id=ID&c=1&v=84&s=COOKIEPLAYERID (visitors)
* /pou/lkd?id=l0VEGiAN&c=1&v=84&s=COOKIEPLAYERID (lista de Me gusta)
* /pou/lkr?id=l0VEGiAN&c=1&v=84&s=COOKIEPLAYERID (lista de simpatizantes)
* /pou/fav?id=ID&c=1&v=84&s=COOKIEPLAYERID




* /gam/rkg?gm=3_1&sp=tpW&dt=1a&c=1&v=84&s=COOKIEPLAYERID (food drop weekly)
* /gam/rkg?gm=3_1&sp=tpM&dt=19&c=1&v=84&s=COOKIEPLAYERID (food drop month)
* /gam/rkg?gm=3_1&sp=tpA&c=1&v=84&s=COOKIEPLAYERID (food drop all)
* /gam/rkg?gm=3_1&sp=fvA&c=1&v=84&s=COOKIEPLAYERID (food drop fav)

The links were found using memory dump
