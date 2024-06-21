# TrekLauncher
A Star Trek inspired Android Launcher/Homescreen

Getting distracted by all the icons on your desktop?
Did you know you put it up there on the right side, but the icon now moved because you uninstalled an unrelated app?
Are you panning through your various home screens clutter by too many icons?

## Then you need TrekLaucnher
Or not. But this is my solution. I've sucesssfully used and loved the Niagara Launcher, that gives you a simple list of your most used apps. However, on tablets it looks like crap, and the font is too small, and I don't want icons.

This laucner you can set as your Home Screen / Main Launcher, and it is Star Trek designed inspired.

Features:
- Colorful!
- Each app laucnh button is of different computed hash color, so as long as the name stays same it's same color
- Displays the current STARUSDATEs
- Built-in simple but capable Star Trekkie calculator (50 LOC)
- Access apps by name (A-Z buttons)
- Acesss apps by keyboard incremental search! Just start typing...

## Install
1. Download the APK in the main directory, install it
2. Download/copy this directory to a new directory in Android
3. Configure BridgeLauncher; navigate to the directory
4. Reload and test
5. Set it as main launcher (Android settings search launcher)
6. Hack!

## STARUDATE
Stardates are cool, but what do they mean? Actually, it's not all clear. All Star Trek series had different definitions. You can read more on the [Wikipedia Stardate Page](https://wikipedia.com/wiki/Stardate).

Here is my definition of StarUDates as I call them. Star Unixbased Dates.

      // STARUDATE yydd.tt
      // -----------------
      // This my variant of Star Trek's stardate. In the movies there were
      // at least 3 different definitions over time, neither really useful to us.
      // I've defined a format that is both intuitive and informative,
      //
      // Example: 2024-06-21 04:37 => 54472.19...
      //                              yyddd.TTttt
      
      // Read it as: YEAR= 2024-1970 = 54
      //             DAY = 472 permille (47.2%) of the year
      //             TIME= 19% of day (=04:37), 50% is noon (5 digits precision)
      //
      // yy is years since 1970, ddd promille of year, tt: 24h as % of day
      // as floating point number monotonically increasing but not perfectly "linear"
      // ( because: each real 24h have 2.7 "promille year" (ddd) per real day! )
      let zoff= new Date().getTimezoneOffset() * 60 * 1000;

      // Returns STARUDATE float as per above
      function starudate() {
	      let t= Date.now()-zoff, d= new Date(t), y= d.getFullYear(), s= Date.parse(""+y)+zoff;
	      let dayofyear= Math.round( (t-s)/1000/24/3600/365.25*1000 );
	      let decimals= d/1000/3600/24 % 1; // get decimals!
	      return (y-1970)*1000 + dayofyear + Math.round(decimals*100000)/100000;
	      return (y-1970)*1000 + dayofyear + Math.round(decimals*100)/100;
      }

## Could-Do:s?
