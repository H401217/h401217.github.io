# Pou 3D web API (Beta)
(please dont ban me zakeh)

The main endpoint for the API is `https://app.pou3d.me/app`
Current version for 1.0.60 is "60"
player id is 0elidNcC (testingmods)

## Links
"s" value is the cookie (not confirmed), it has 22 characters

* GET /eml/chkReg?em=EMAIL&ac=rg&c=1&v=60
* GET /reg/emlCap?em=EMAIL&ac=rg&c=1&v=60&cI=x6ghlo&cA=vjomh
  * cI = captcha link
  * cA = captcha answer
* GET /aPu/chgNik?pI=PLAYERID&nk=NICKNAME&c=1&v=60&s=COOKIE
* GET /acc/chgPwd?pw=MD5PASSWORD&c=1&v=60&s=COOKIE
* GET /utl/genCap?c=1&v=60
* GET /aPu/sav?gN=1&c=1&v=60&s=&s=COOKIEPLAYERID
** the "s" value is fused with the player id (string)

The links are found using memory dump
