# llm-study

1. python 가상환경 세팅

   ```
   python -m venv env
   ```

2. 가상환경 실행

   ```
   source env/bin/activate
   ```

   - 가상환경 종료

     ```
     deactivate
     ```

3. 파이썬 라이브러리 설치

   ```
   pip install -r requirements.txt
   ```

# BeautifulSoup과 Selenium을 같이 쓰는 이유

### Selenium의 기능

동적 콘텐츠 로딩: Selenium은 웹 브라우저를 자동화하여 JavaScript에 의해 동적으로 생성된 콘텐츠를 로딩할 수 있습니다. 이는 단순한 HTTP 요청으로는 접근할 수 없는 콘텐츠를 스크랩할 때 유용합니다.
사용자 인터랙션: 버튼 클릭, 폼 제출, 스크롤 등 사용자의 동작을 시뮬레이션할 수 있습니다.

### BeautifulSoup의 기능

HTML 파싱 및 탐색: BeautifulSoup은 HTML 및 XML 파일을 파싱하고, 트리 구조를 통해 원하는 데이터를 쉽게 탐색할 수 있게 해줍니다.
데이터 추출: 특정 태그, 속성 등을 사용하여 필요한 데이터를 효율적으로 추출할 수 있습니다.

### Selenium만 사용할 때의 한계

Selenium만으로도 페이지의 소스 코드에 접근하고 특정 요소를 찾을 수 있지만, 복잡한 HTML 구조를 탐색하고 원하는 데이터를 추출하는 데 있어서는 BeautifulSoup이 더 유용하고 직관적입니다. Selenium의 기본 제공 메서드만으로는 다음과 같은 작업이 복잡해질 수 있습니다:

- 여러 레벨의 중첩된 HTML 태그를 탐색하는 경우

- 특정 클래스나 ID를 가진 다수의 요소를 탐색하는 경우

### Selenium과 BeautifulSoup을 함께 사용하는 이유

Selenium으로 동적으로 로딩된 페이지를 처리한 후 BeautifulSoup을 사용하여 효율적으로 HTML을 파싱하고 데이터를 추출하는 것이 일반적입니다. 다음은 그 예입니다:

Selenium으로 동적 콘텐츠 로딩: JavaScript로 로딩된 콘텐츠를 포함한 전체 페이지 소스를 얻습니다.
BeautifulSoup으로 HTML 파싱 및 데이터 추출: 페이지 소스를 BeautifulSoup에 전달하여 복잡한 HTML 구조를 쉽게 탐색하고 데이터를 추출합니다.
