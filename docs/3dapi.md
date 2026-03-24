# Pou 3D web API (Beta)
(please dont ban me zakeh)

The main endpoint for the API is `https://app.pou3d.me/app`
Current version for 1.0.60 is "60"
player id is 0elidNcC (testingmods)

## Links
"s" value is the cookie (not confirmed), it has 22 characters

* /eml/chkReg?em=EMAIL&ac=rg&c=1&v=60
* /reg/emlCap?em=EMAIL&ac=rg&c=1&v=60&cI=x6ghlo&cA=vjomh
  * cI = captcha link
  * cA = captcha answer
* /aPu/chgNik?pI=PLAYERID&nk=NICKNAME&c=1&v=60&s=COOKIE
* /acc/chgPwd?pw=MD5PASSWORD&c=1&v=60&s=COOKIE
* /utl/genCap?c=1&v=60
* /aPu/sav?gN=1&c=1&v=60&s=&s=COOKIEPLAYERID
** the "s" value is fused with the player id (string)
* /aPu/sav?gN=1&c=1&v=60&s=&s=COOKIEPLAYERID
* /aPu/png?c=1&v=60&s=COOKIEPLAYERID
* /pou/stt?pI=0elidNcC&c=1&v=60&s=COOKIEPLAYERID
* /pos/pop?sp=ppW&c=1&v=60&s=COOKIEPLAYERID (popular by week)
* /pos/pop?sp=ppM&c=1&v=60&s=COOKIEPLAYERID (popular by month)
* /pos/pop?sp=ppA&c=1&v=60&s=COOKIEPLAYERID (popular all time)
* /pos/pop?sp=lkA&c=1&v=60&s=COOKIEPLAYERID (top likers?)
* /pou/vis?id=puDANxgE&c=1&v=60&s=COOKIEPLAYERID (visit id is from doradingo)
* /pou/lik?id=puDANxgE&c=1&v=60&s=COOKIEPLAYERID (visit id is from doradingo)
* /pou/ulk?id=puDANxgE&c=1&v=60&s=COOKIEPLAYERID (visit id is from doradingo)
* /pou/mgR?id=puDANxgE&c=1&v=60&s=COOKIEPLAYERID (visit id is from doradingo)
* /pou/msg?id=puDANxgE&mI=1&c=1&v=60&s=COOKIEPLAYERID (visit id is from doradingo)
* /pou/mgS?id=puDANxgE&mI=1&c=1&v=60&s=COOKIEPLAYERID (visit id is from doradingo)

The links are found using memory dump
