# uploadAPI/ doctor web
HTTP API that supports POST requests on: /download /delete /upload

Task requirements have been daemonizing server, specific storage structure. Serving GETs is not part of the doctor web task.

default (hardcoded):

uploadapi.py: localhost:5050, ~/Documents/

uploadapid.py: localhost:4040
# Structure
uploadapi.py: 

	UploadAPIHandler - requst handler for HTTPServer

d.py:
 
	Daemon - generic daemon class by Sander Marechal

uploadapid.py: 

	APIDaemon - daemonizing HTTPServer initialized with UploadAPIHandler
# Usage:
## start httpserver daemon:
```
python uploadapid.py start
```
 other commands:
```
[nuser@host0x428a2f98 temp-proj-a]$ python uploadapid.py
usage: uploadapid.py start|status|stop|restart
```
## /download:
```
curl -O -J -d file=<filehash> 127.0.0.1:<port>/download
 ```
 POST /download example:
```
[nuser@host0x428a2f98 Downloads]$ curl -O -J -d file=05698f7b1d3cc945aaa616d6edfc578d 127.0.0.1:5050/download
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100  1240    0  1203  100    37  1174k  37000 --:--:-- --:--:-- --:--:-- 1210k
[nuser@host0x428a2f98 Downloads]$ ls
README.md
```
## /delete:
```
curl -d file=<filehash> 127.0.0.1:<port>/delete
```
 POST /delete example:
```
[nuser@host0x428a2f98 Downloads]$ curl -d file=05698f7b1d3cc945aaa616d6edfc578d 127.0.0.1:5050/delete
README.md file deleted. /store/05/05698f7b1d3cc945aaa616d6edfc578d/ folder deleted.
```
## /upload:
```
curl -F file=@<filepath> 127.0.0.1:<port>/upload
``` 
 POST /upload :
```
[nuser@host0x428a2f98 Downloads]$ curl -F file=@README.md 127.0.0.1:5050/upload
upload endpoint. </br> file md5 hash: [05698f7b1d3cc945aaa616d6edfc578d]
```
## /:

 debug form on http://127.0.0.1/

 GET /:
```
[nuser@host0x428a2f98 Downloads]$ curl 127.0.0.1:5050/
<html>
<body>
GET method evoked
ver 0.2
</br>
<form enctype="multipart/form-data" method="post" action="upload">
<p>Upload File: <input type="file" name="file"></p>
<p><input type="submit" value="Upload"></p>
</form>
<form enctype="multipart/form-data" method="post" action="delete">
<p>Delete : <input type="text" name="file"></p>
<p><input type="submit" value="Delete"></p>
</form>
<form enctype="multipart/form-data" method="post" action="download">
<p>Download : <input type="text" name="file"></p>
<p><input type="submit" value="Download"></p>
</form>
<div> Files:
<p>05698f7b1d3cc945aaa616d6edfc578d</p>
</div>
</body>
</html>
```
