ddwrt-adbp-to-privoxy
=====================

Download and convert Adblock Plus Filters to Privoxy Action- and Filterfiles<br>
for DD-WRT Builds above 25000 and Kong 's older Builds back to 23900 OLDD 

Based on the Original Script for OpenWRT by Andrwe:<br>
http://andrwe.org/scripting/bash/privoxy-blocklist

Modified to be used without Optware or any additional Binaries. 

<h3>Changelog</h3>
<ul>
<li><b>151012-1</b> 
<ul>
<li>Moved to Github</li>
<li>Fixed some Syntax Errors (possibly - tested with shellcheck.net). Please update to the newest Version</li>
</ul>
</li>
<li><b>141012-1</b> 
<ul>
<li>Added Domain-Based Blocking</li>
<li>Fixed Regex for Whitelisting (now properly working)</li>
</ul>
</li>
<li><b>142711-1</b>
<ul>
<li>Initial Release</li>
<li>Fixed Regex from original Script that would prevent the Filter- and Actionlists from working</li>
<li>Changed binaries that are used to be compatible with DD-WRT 25408 and similar</li>
</ul>
</li>
</ul>

<h3>Requirements:</h3>
<ul><li>DD-WRT Build BS 25408+, Kong 23900+ or similiar</li>
<li>/usr/sbin/privoxy</li>
<li>/jffs/</li>
</ul>

<h3>Install Instructions:</h3>
<ol><li>Create Folders /jffs/etc/privoxy and /jffs/tmp (if not already existing)</li>

<li>Create / Copy below Script-Contents into /jffs/privoxy-blocklist.sh</li>

<li>chmod +x privoxy-blocklist.sh</li>

<li>sh privoxy-blocklist.sh</li>

<li>Enable Privoxy in the DD-WRT Backend under Services -> Adblocking and also enable Custom Configuration.</li>

<li>Change the confdir to the place where you store your filterlists - by default: /jffs/etc/privoxy (as in: confdir /jffs/etc/privoxy)</li>

<li>Add all Filter- and Actionlists to your Custom Configuration like this<br>
(for each AdblockPlus-List one Filter- and one Actionlist will be generated):<br>
<br>
<img src="http://abload.de/img/filterlistsexeqj.jpg" width="50%">
</li>
<li>Click Save - then Apply Settings</li>

</li>Wait a bit (approx. 5 minutes) - now Privoxy should be restarted including your AdblockPlus Filters and Actions. You can verify this under [url]http://config.privoxy.org/show-status[/url] (you can only access this page if you're using Privoxy). <br>
<br>
It should look similar to this:<br>
<br>
<img src="http://abload.de/img/privoxy-config-succesf6udi.jpg" width="50%">
</li>
</ol>

<h3>Configuration (in privoxy-blocklist.sh):</h3>
<ul><li>Modify the following vars to your needs:<br>
<br>
<code>CONFDIR=/jffs/etc/privoxy</code><br>
<code>TMPDIR=/jffs/tmp/privoxy-blocklist</code><br>
<br>
<li><b>And specify the AdblockPlus Lists you want to grab and convert in the loop:</b>
<br>
<code>for url in</code><br>
<code>"https://easylist-downloads.adblockplus.org/easylist.txt"</code><br> <code>"https://easylist-downloads.adblockplus.org/easylistgermany.txt"</code><br> <code>"https://easylist-downloads.adblockplus.org/malwaredomains_full.txt"; do</code><br>
<br>
<b>Some AdblockPlus Blocklists can be found on the official Site:</b><br>
<br>
https://adblockplus.org/en/subscriptions<br>
(for the URL see the Link of the Subscription-Button for each List you want to use)
</li>
</ul>

<h3>Usage:</h3>

<code>sh privoxy-blocklist.sh</code> - everytime you want to Update the Lists (see Install-Instructions above)[/list]


<h3>Custom Configuration example:</h3>
<code>confdir /jffs/etc/privoxy </code><br>
<code>templdir /jffs/etc/privoxy/templates </code><br>
<code>logdir /var/log/privoxy </code><br>
<code>actionsfile match-all.action </code><br>
<code>actionsfile default.action </code><br>
<code>actionsfile user.action </code><br>
<code>filterfile default.filter </code><br>
<code>actionsfile liste_fr.script.action </code><br>
<code>actionsfile easylistchina.script.action </code><br>
<code>actionsfile easylist.script.action </code><br>
<code>filterfile liste_fr.script.filter </code><br>
<code>filterfile easylistchina.script.filter </code><br>
<code>filterfile easylist.script.filter </code><br>
<code>logfile logfile </code><br>
<code>tolerate-pipelining 1 </code><br>
<code>enable-compression 1 </code><br>
<code>enable-edit-actions 0 </code><br>
<code>accept-intercepted-requests 1 </code><br>
<code>listen-address 192.168.2.1:8118 </code><br>
<code>max-client-connections 256 </code><br>
<code>default-server-timeout 60 </code><br>
<code>keep-alive-timeout 300 </code><br>
<code>socket-timeout 120 </code><br>
<code>toggle 1 </code><br>

