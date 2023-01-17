>> ## urllib 사용법 및 기본 스크래핑

***



```python
import urllib.request as req
```


```python
# 파일 URL
img_url = "https://images.unsplash.com/photo-1436491865332-7a61a109cc05?ixlib=rb-4.0.3&ixid=MnwxMjA3fDB8MHxzZWFyY2h8Nnx8YWlycG9ydHxlbnwwfHwwfHw%3D&auto=format&fit=crop&w=500&q=60"
html_url = 'http://www.google.com'
```


```python
# 다운받을 경로
save_path1 = "C:/Myexam/test1.jpg"
save_path2 = "C:/Myexam/index.html"
```


```python
# 예외처리
try:
    file1, header1 = req.urlretrieve(img_url, save_path1)
    file2, header2 = req.urlretrieve(html_url, save_path2)
except Exception as e:
    print("Download failed.")
    print(e)
else:
    # Header 정보 출력
        print(header1)
        print(header2)
        print("Download succeed.")
```

    Connection: close
    Content-Length: 21169
    Last-Modified: Wed, 09 Nov 2022 15:36:07 GMT
    Cache-Control: public, max-age=315360000
    Server: imgix
    X-Imgix-ID: d7810e70f5bb2b17b173a563b387d3e4a555f94e
    X-Imgix-Render-Farm: 01.1096
    X-Imgix-Original-Status: 200
    Date: Tue, 17 Jan 2023 12:25:55 GMT
    Age: 5950188
    Accept-Ranges: bytes
    Set-Cookie: ugid=d135a2962728e515e0ab74af5cf5c7aa5579861;domain=.unsplash.com;path=/;expires=Wed, 17 Jan 2024 12:25:55 GMT;SameSite=None;Secure
    Content-Type: image/jpeg
    Access-Control-Allow-Origin: *
    Cross-Origin-Resource-Policy: cross-origin
    X-Content-Type-Options: nosniff
    X-Served-By: cache-sjc10065-SJC, cache-icn1450032-ICN
    X-Cache: HIT, HIT
    Vary: Accept, User-Agent
    
    
    Date: Tue, 17 Jan 2023 12:25:55 GMT
    Expires: -1
    Cache-Control: private, max-age=0
    Content-Type: text/html; charset=ISO-8859-1
    Cross-Origin-Opener-Policy-Report-Only: same-origin-allow-popups; report-to="gws"
    Report-To: {"group":"gws","max_age":2592000,"endpoints":[{"url":"https://csp.withgoogle.com/csp/report-to/gws/other"}]}
    P3P: CP="This is not a P3P policy! See g.co/p3phelp for more info."
    Server: gws
    X-XSS-Protection: 0
    X-Frame-Options: SAMEORIGIN
    Set-Cookie: 1P_JAR=2023-01-17-12; expires=Thu, 16-Feb-2023 12:25:55 GMT; path=/; domain=.google.com; Secure
    Set-Cookie: AEC=ARSKqsKn6VLmkD0BNMcBmtvx8dLGxZi-S5ycgllZcch2uEDKft4YUdovtu4; expires=Sun, 16-Jul-2023 12:25:55 GMT; path=/; domain=.google.com; Secure; HttpOnly; SameSite=lax
    Set-Cookie: NID=511=mgHWu0XLeflKZZo0wczWJd_zBiuJa5gdWydOrsd6T7tQb2KuP_HWqvpdb-TF5BjldVC1KElrq3c-pCiRJxrwcDxI0Th73a6nmJ4yiKqGtB7JEy6xNsDRt_fTwXMYnajndHl8tO-04PgP_YqMJYrkymp-OSKISAeVaROEYPtth9Q; expires=Wed, 19-Jul-2023 12:25:55 GMT; path=/; domain=.google.com; HttpOnly
    Accept-Ranges: none
    Vary: Accept-Encoding
    Connection: close
    Transfer-Encoding: chunked
    
    
    Download succeed.
    


```python
print(help(req.urlretrieve))
```

    Help on function urlretrieve in module urllib.request:
    
    urlretrieve(url, filename=None, reporthook=None, data=None)
        Retrieve a URL into a temporary location on disk.
        
        Requires a URL argument. If a filename is passed, it is used as
        the temporary file location. The reporthook argument should be
        a callable that accepts a block number, a read size, and the
        total file size of the URL target. The data argument should be
        valid URL encoded data.
        
        If a filename is passed and the URL points to a local resource,
        the result is a copy from local file to new file.
        
        Returns a tuple containing the path to the newly created
        data file as well as the resulting HTTPMessage object.
    
    None
    

