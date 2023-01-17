>> ## lxml 사용 기초 스크래핑

***



```python
from typing import get_args
import requests
from lxml.html import fromstring, tostring
```


```python
def main():
    """
    네이버 지식인 스크래핑 메인 함수
    """
    
    # 세션 사용
    session = requests.Session()
    
    # 스크랩핑 대상 URL (GET, POST)
    response = session.get('https://kin.naver.com/search/list.nhn?query=%ED%8C%8C%EC%9D%B4%EC%8D%AC')
    
    # 신문사 링크 리스트 획득
    urls = scrape_news_list_page(response)
    
    # 딕셔너리 확인
    # print(urls)
    
    # 결과 출력
    for name, url in urls.items():
        # url 출력
        print(name, url)
```


```python
def scrape_news_list_page(response):
    # url 리스트 선언
    urls = {}
    
    # 태그 정보 문자열 저장
    #print(response.content)
    root = fromstring(response.content)
    #print(root)
    
    for a in root.xpath('//ul[@class="basic1"]/li/dl/dt/a[@class="_nclicks:kin.txt _searchListTitleAnchor"]'):
        # a 구조 확인
        # print(a)
        
        # a 문자열 출력
        # print(tostring(a, pretty_print=True))
        
        name, url = extract_conents(a)
        # 딕셔너리 삽입
        urls[name] = url
        
    return urls
```


```python
def extract_conents(doc):
    # 링크 주소
    link = doc.get('href')
    name = doc.text_content()
    return name, link
```


```python
if __name__ == '__main__':
    main()
```

    플라스크에서 파이썬 실행 https://kin.naver.com/qna/detail.naver?d1id=1&dirId=10402&docId=436285489&qb=7YyM7J207I2s&enc=utf8&section=kin&rank=1&search_sort=0&spq=0
    v파이썬 파이썬 https://kin.naver.com/qna/detail.naver?d1id=1&dirId=10402&docId=433970253&qb=7YyM7J207I2s&enc=utf8&section=kin&rank=2&search_sort=0&spq=0
    파이썬 코딩 질문 https://kin.naver.com/qna/detail.naver?d1id=1&dirId=10402&docId=433475801&qb=7YyM7J207I2s&enc=utf8&section=kin&rank=3&search_sort=0&spq=0
    파이썬 공부방법 공유해주세요.... https://kin.naver.com/qna/detail.naver?d1id=1&dirId=1040105&docId=437004629&qb=7YyM7J207I2s&enc=utf8&section=kin&rank=4&search_sort=0&spq=0
    파이썬, 자바? https://kin.naver.com/qna/detail.naver?d1id=4&dirId=40608&docId=435292280&qb=7YyM7J207I2s&enc=utf8&section=kin&rank=5&search_sort=0&spq=0
    해킹 파이썬,칼리리눅스 https://kin.naver.com/qna/detail.naver?d1id=1&dirId=11001&docId=436726953&qb=7YyM7J207I2s&enc=utf8&section=kin&rank=6&search_sort=0&spq=0
    파이썬 식 좀 알려주세요 https://kin.naver.com/qna/detail.naver?d1id=1&dirId=10402&docId=434384411&qb=7YyM7J207I2s&enc=utf8&section=kin&rank=7&search_sort=0&spq=0
    파이썬 코드 https://kin.naver.com/qna/detail.naver?d1id=1&dirId=10402&docId=435106645&qb=7YyM7J207I2s&enc=utf8&section=kin&rank=8&search_sort=0&spq=0
    요새 파이썬으로 개발하는 이유 https://kin.naver.com/qna/detail.naver?d1id=1&dirId=10402&docId=424704487&qb=7YyM7J207I2s&enc=utf8&section=kin&rank=9&search_sort=0&spq=0
    파이썬 배우면 어떻게 적용할 수 있나요? https://kin.naver.com/qna/detail.naver?d1id=1&dirId=10402&docId=436900383&qb=7YyM7J207I2s&enc=utf8&section=kin&rank=10&search_sort=0&spq=0
    


```python
import requests
import lxml.html

#response = requests.get('https://news.nate.com/rank/?mid=n1000')
root = lxml.html.fromstring(response.content)

for a in root.cssselect('ul.mduSubject.mduRankSubject li a'):
    url = a.text_content()
    print(url)
```

    [단독] 육교에서 극단적 선택 20대 남성, 버스 정류장 위로 떨어져 생존
    "홍합 빼주세요"vs"손이 없냐"…싸움터 된 배달앱 댓글
    UAE 국빈방문 마치고 스위스 향하는 윤석열 대통령 내외
    "의자 좀 그만 젖혀요" 싸움 그만…비행기 '좌석 등받이 분쟁' 곧 사라질 ...
    [고진현의 창(窓)과 창(槍)]김보름의 눈물,누가 닦아줘야 하나?
    이태원서 떠난 27살 대학 새내기…장례식에 친구만 600명
    "실은 우리 아빠가"…장제원 아들, 2년마다 '父 사과문' 불러
    "저는 대한민국 영업사원"…윤 대통령, '경제 올인' 강조
    실내에서 마스크 벗을 수 있는 날, '오는 30일 0시' 유력
    이란 "윤 대통령, 완전히 무지하다"…'UAE의 적' 발언 파장
    日지식인도 이해 못하는 韓재단 대납…"가해기업은 한푼도 안내"
    이란, 尹 'UAE의 적' 발언에 "예의주시…한국 외교부 설명 필요"
    대통령실, 'UAE의 적' 尹발언에 "한-이란 관계 무관…장병 격려"
    "반려동물호텔 믿고 맡긴 반려견, 로드킬로 죽어서 왔다"
    "요즘 애들 다 그렇진 않아요"…풍자 콘텐츠 불편한 MZ들
    슈퍼챗 고래 김어준, 수입 전세계 톱…하루 9천, 한 주 2억3200만원 꿀꺽
    "한반도 전쟁때 생존확률 '0'보다 약간 높아…서울 탈출은 불가능"
    'UAE 적은 이란' 尹발언 논란에…외교부 "장병 격려 차원의 말"
    김정숙 여사도 입었는데…김건희 여사 군복에 野 "대통령 노릇"
    교역국인데 '적'?…한국-이란-UAE 관계로 본 '발언 논란'
    박항서의 쓴소리 "왜 외국인 만큼 지원 없나…한국인 감독도 능력 충분"
    韓, 자체 개발 초음속 항공기 보유국 됐다…KF-21 음속 돌파
    韓기업들, UAE와 7.5조원 규모 에너지·신산업 프로젝트 착수(종합)
    8개월만에 송환 김성태, 변호사비 대납의혹에 "사실 무근"
    "손흥민, 느려지고 있다"…커리어에 치명적인 혹평까지
    '17억→15억→10억' 수직 하락…3년전으로 리셋된 동탄 집값 [부동산360]
    고속도로 역주행하다 8.5t 트럭과 '쾅'…70대 승용차 운전자 사망
    러시아 귀화→중국 코치, 안현수는 왜 韓 '코치' 지원했을까
    '위안부, 자발적 매춘부' 램지어 교수…韓美 학자들 집단 반격
    쌍방울 전 회장 비서실장 "김성태, 이재명과 가까운 관계로 보여"
    [뉴스1 PICK] 국정조사 마지막 날 국회 찾은 유가족…'자식 잃은 슬픔에 ...
    카톡 또 먹통…"메시지 전송·카카오페이 안 돼요"
    [전세사기 실태추적]⑥"단지가 통째로" 무너진 인천 미추홀구
    '37조원 투자' 한·UAE 공동성명에 명시…원전 3국 공동진출
    '내가 차고 싶어, 내가 차게 해줘'…손흥민, 프리킥 요구했다
    이재명, 성남FC 의혹 檢진술서 공개…"후원금 아닌 광고비"
    22일부터 우회전 신호등 어기면 최고 20만원 벌금
    '보행자 없네' 빨간불서 바로 우회전…이러면 딱지 날아온다
    박항서 준우승이 아쉽다고? 베트남은 10년간 결승 못가던 팀[AFF컵]
    '해외 최초' 루브르 별관 찾은 윤 대통령 부부
    기자회견 중 하염없이 눈물만 흘린 이태원 참사 유가족 [TF사진관]
    文사저 욕설 시위자, 文부부 증인채택 안 되자 "법관 바꿔달라"
    민주, 'UAE의 적' 尹발언에 "외국만 나가면 사고…국격 무너져"
    [단독]"중년 아저씨 맞는 소리 들려요"…무차별 폭행 16세 긴급체포
    네팔서 잇단 비극…안나푸르나 등반 50대 한국여성, 숨진 채 발견
    
