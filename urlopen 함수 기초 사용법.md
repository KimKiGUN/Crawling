>> ## urlopen 함수 기초 사용법

***



```python
import urllib.request as req
from urllib.error import URLError, HTTPError
```


```python
# 다운로드 경로 및 파일명
path_list = ['c:\\MyExam\\test1.jpg', 'c:\\Myexam\\index.html']
```


```python
# 다운로드 리소스 URL
target_url = ['https://images.unsplash.com/photo-1436491865332-7a61a109cc05?ixlib=rb-4.0.3&ixid=MnwxMjA3fDB8MHxzZWFyY2h8Nnx8YWlycG9ydHxlbnwwfHwwfHw%3D&auto=format&fit=crop&w=500&q=60',
             'http://google.com']
```


```python
for i, url in enumerate(target_url):
    # 예외 처리
    try:
        # 웹 수신 정보 읽기
        response = req.urlopen(url)
        # 수신 내용
        contents = response.read()
        
        print('------------------------------------')
        
        # 상태 정보 중간 출력
        print('Header Info-{} : {} '.format(i, response.info()))
        print('HTTP Status Code : {}'. format(response.getcode()))
        print()
        
        # 파일 쓰기
        with open(path_list[i], 'wb') as c:
            c.write(contents)
            
        # HTTP 에러 발생 시
    except HTTPError as e:
        print("Download failed.")
        print("URL Error Reason : ", e.reason)
        
        # 성공
    else:
        print()
        print("Download Succeed.")
```

    ------------------------------------
    Header Info-0 : Connection: close
    Content-Length: 21169
    Last-Modified: Wed, 09 Nov 2022 15:36:07 GMT
    Cache-Control: public, max-age=315360000
    Server: imgix
    X-Imgix-ID: d7810e70f5bb2b17b173a563b387d3e4a555f94e
    X-Imgix-Render-Farm: 01.1096
    X-Imgix-Original-Status: 200
    Date: Tue, 17 Jan 2023 12:35:27 GMT
    Age: 5950760
    Accept-Ranges: bytes
    Set-Cookie: ugid=d135a2962728e515e0ab74af5cf5c7aa5579863;domain=.unsplash.com;path=/;expires=Wed, 17 Jan 2024 12:35:27 GMT;SameSite=None;Secure
    Content-Type: image/jpeg
    Access-Control-Allow-Origin: *
    Cross-Origin-Resource-Policy: cross-origin
    X-Content-Type-Options: nosniff
    X-Served-By: cache-sjc10065-SJC, cache-icn1450090-ICN
    X-Cache: HIT, HIT
    Vary: Accept, User-Agent
    
     
    HTTP Status Code : 200
    
    
    Download Succeed.
    ------------------------------------
    Header Info-1 : Date: Tue, 17 Jan 2023 12:35:27 GMT
    Expires: -1
    Cache-Control: private, max-age=0
    Content-Type: text/html; charset=ISO-8859-1
    Cross-Origin-Opener-Policy-Report-Only: same-origin-allow-popups; report-to="gws"
    Report-To: {"group":"gws","max_age":2592000,"endpoints":[{"url":"https://csp.withgoogle.com/csp/report-to/gws/other"}]}
    P3P: CP="This is not a P3P policy! See g.co/p3phelp for more info."
    Server: gws
    X-XSS-Protection: 0
    X-Frame-Options: SAMEORIGIN
    Set-Cookie: 1P_JAR=2023-01-17-12; expires=Thu, 16-Feb-2023 12:35:27 GMT; path=/; domain=.google.com; Secure
    Set-Cookie: AEC=ARSKqsJbzCqirUwc2vRjDTX0R8eOLpcsr2TqDHSaLKP5gEnMa7i5EffejA; expires=Sun, 16-Jul-2023 12:35:27 GMT; path=/; domain=.google.com; Secure; HttpOnly; SameSite=lax
    Set-Cookie: NID=511=WpNQE2-OgsZTPGWy3f987TCzpitCYWbQcYhcJ2Miz7ZeAlXnBaSHfvpSgDGrvaKvxjiCXwIQXkUktVIvv6IqDFtaekUZf1RvBZfjvY1j017XltFn9JzCVEe8rEEK7cB4OaYzLKyklsVJhv4i9sHWXDCYw3XI4tNOIIiliMhCTt0; expires=Wed, 19-Jul-2023 12:35:27 GMT; path=/; domain=.google.com; HttpOnly
    Accept-Ranges: none
    Vary: Accept-Encoding
    Connection: close
    Transfer-Encoding: chunked
    
     
    HTTP Status Code : 200
    
    
    Download Succeed.
    

