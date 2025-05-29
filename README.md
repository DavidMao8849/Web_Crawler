
# ☕ 이디야 커피 웹사이트 정적 크롤링 프로젝트

**인공지능과 데이터과 PBL 프로젝트 - 인싸조**  
> 팀원: 백승원, 이민욱, 이은우, 우재윤, 강대현  
> 프로젝트 기간: 2024.04.28-06.18

---

## 📌 프로젝트 개요

이 프로젝트는 이디야 커피 웹사이트를 **정적 웹 크롤링 방식**으로 데이터를 수집하고, </br>
이를 분석 및 저장하는 과정을 통해 **웹 크롤링 기술을 실습**해보는 것을 목표로 합니다.  

### ✅ 선정 배경
- **정적 크롤링**: 구조가 단순하고 효율적인 수집 방식
- **이디야 커피**: 크롤링 구조가 명확하고, 음료 정보가 잘 정리되어 있음

---

## 🛠️ 사용 기술

- Python 3
- BeautifulSoup4
- requests / urllib
- pandas
- Jupyter Notebook

---

## 🧱 프로젝트 구조

```bash
📁 ediya-crawling/
├── ediya_crawling.ipynb    # 크롤링 코드 노트북
└── Ediya_menu.csv          # 크롤링 결과 저장 파일
```

---

## 🔍 크롤링 내용

이디야 공식 웹사이트([https://ediya.com/contents/drink.html](https://ediya.com/contents/drink.html))에서 다음 정보를 수집했습니다:

- 음료 이름 (`h2` 태그)
- 음료 설명 (`p` 태그)
- 영양 정보 (`div.pro_nutri`)
- 알러지 정보 (`div.pro_allergy`)

---

## 💻 주요 코드 예시

```python
import urllib.request
from bs4 import BeautifulSoup
import pandas as pd

def Ediya_menu(result):
    Ediya_url = 'https://ediya.com/contents/drink.html' # 가져올 url 문자열로 입력
    html = urllib.request.urlopen(Ediya_url) # url을 요청하여 응답받은 html이 담긴 자료를 받아와서 저장함.
    soupEdiya = BeautifulSoup(html, 'html.parser') #BeautifulSoup의 객체를 생성함.(html을 잘 정리된 형태로 변환)
    menu_items = soupEdiya.find_all('div', class_='pro_detail') #필요한 항목의 태그와 클래스를 분석하여 파싱한다.

    for menu in menu_items:
        if menu:
            menu_name = menu.find('h2').text.strip() # 음료 메뉴 항목에서 음료 이름에 해당하는 부분 추출
            menu_detail = menu.find('p').text.strip() # 음료 설명에 해당하는 부분 추출
            menu_nutri = menu.find('div', class_='pro_nutri').text.strip()  # 음료 영양분에 해당하는 부분 추출
            menu_allergy = menu.find('div', class_='pro_allergy').text.strip() # 알러지 성분에 해당하는 부분 추출
            result.append([menu_name, menu_detail, menu_nutri, menu_allergy]) # 추출한 결과들을 result에 추가 저장

def main():
    result = [] #추출한 결과들을 저장할 공간 생성
    Ediya_menu(result) #위의 Ediya_menu함수 호출
    Ediya_tbl = pd.DataFrame(result, columns=('name', 'detail', 'nutri', 'allergy')) #추출한 결과를 데이터프레임으로 저장
    Ediya_tbl.to_csv('Ediya_menu.csv', encoding='utf-8-sig', mode='w', index=False) # Ediya_menu.csv파일로 저장

if __name__ == '__main__':
    main()

```

---

## 📊 결과 예시 (CSV)

![image](https://github.com/user-attachments/assets/6aba4dac-4db7-462b-8718-dc316e0efefd)


---

## 💡 활용 방안

- **건강 정보 기반 음료 추천 시스템** 개발 가능성
- **음료 성분 기반 마케팅 전략 수립**
- **웹 크롤링 기술 실습 및 포트폴리오 구성**

---

## 🧠 팀원별 역할

| 이름     | 역할                      |
|----------|---------------------------|
| 백승원   | 프로젝트 총괄, 코드 통합     |
| 이은우   | HTML 파싱 및 크롤링 코드 작성 |
| 이민욱   | 보고서 작성 |
| 우재윤   | PPT 제작 및 발표   |
| 강대현   | 보고서 작성  |

---

## 🩹 프로젝트에서 겪었던 문제점
**발표자에게 개발에서 사용한 코드에 대해 이해 시키는 부분.**
   - 이 부분은 프로젝트를 진행하면 어느정도 공감하는 부분일테지만, 개발에 직접적으로 참여하지 않은 발표자에게 프로젝트에서 구현단계에 이용된 <br/> 코드나 동작과정을 이해시키는 부분은 저에게 있어 가장 어려웠던 부분인거같습니다.<br/>
     발표자 또한 이 웹 크롤링에 대한 개념을 이해하고있다면 문제가 없으나, 그렇지 않을때의 조건은 꽤나 까다롭습니다.<br/>
     <br/>
    **문제해결(실제 해결한 부분)**<br/>
       └─ 발표자가 해당 프로젝트의 개요/주제를 설명하고, 어떤 과정으로 진행하였는지에 대해 설명후, 개발 파트 부분은 개발자가 직접 발표하는 방식을 채택함.
    **다른 개선 방안**<br/>
       └─ 간단하게 코드의 동작과정을 그림으로 그려 표현하거나, 발표자가 알고 있는 개발 분야에 비유하며 설명해준다.<br/>
---

## 📝 느낀점

> HTML 구조를 파악하고 웹사이트에서 원하는 데이터를 추출하는 과정이 유익했으며, 실무에서 API 및 데이터 수집에 활용할 수 있다는 점에서 큰 의미가 있었습니다.  
> (팀원 공동 소감 요약)

---

## 📎 부록

- 📄 [PBL 결과보고서 PDF](https://github.com/DavidMao8849/Web_Crawler/blob/a832aefc29e70cc5bcf0ebabeb979df046783f9e/docs/%EC%9D%B8%EA%B3%B5%EC%A7%80%EB%8A%A5%EA%B3%BC%20%EB%8D%B0%EC%9D%B4%ED%84%B0%EA%B3%BC%ED%95%99%20PBL%20%EA%B2%B0%EA%B3%BC%EB%B3%B4%EA%B3%A0%EC%84%9C_%EC%9D%B8%EC%8B%B8%EC%A1%B0(0613).pdf)
- 📊 [발표 PPT](https://github.com/DavidMao8849/Web_Crawler/blob/a832aefc29e70cc5bcf0ebabeb979df046783f9e/docs/%EC%9D%B8%EA%B3%B5%EC%A7%80%EB%8A%A5%EA%B3%BC%20%EB%8D%B0%EC%9D%B4%ED%84%B0%EA%B3%BC%ED%95%99%20%EC%9D%B8%EC%8B%B8%EC%A1%B0%20%ED%8C%80%ED%94%84%EB%A1%9C%EC%A0%9D%ED%8A%B8%20%EB%B0%9C%ED%91%9C%20PPT.pptx)
