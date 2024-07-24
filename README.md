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

# `implicitly_wait`와 `WebDriverWait`의 차이

`implicitly_wait`와 `WebDriverWait`는 둘 다 Selenium에서 요소가 나타날 때까지 대기하는 방법을 제공하지만, 각각의 동작 방식과 사용 사례는 다릅니다. 아래는 두 가지 대기 방식의 차이점을 비교하여 정리한 내용입니다.

| **특징**                   | **implicitly_wait**                                                                         | **WebDriverWait**                                                                                                                 |
| -------------------------- | ------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------- |
| **설정 방식**              | 한 번 설정하면 WebDriver 인스턴스의 전체 수명 동안 적용됩니다.                              | 특정 조건이 충족될 때까지 대기하는 명시적 대기입니다.                                                                             |
| **대기 시간 설정**         | `driver.implicitly_wait(10)`                                                                | `WebDriverWait(driver, 10).until(EC.presence_of_element_located((By.ID, 'myElement')))`                                           |
| **대기 조건**              | 요소가 DOM에 나타날 때까지 대기합니다.                                                      | 특정 조건(예: 요소가 나타날 때까지, 텍스트가 특정 값이 될 때까지 등)을 만족할 때까지 대기합니다.                                  |
| **적용 범위**              | WebDriver 인스턴스 전체에 적용되며, 모든 요소 찾기 명령에 대기 시간을 적용합니다.           | 특정 요소나 조건에 대해서만 적용됩니다.                                                                                           |
| **대기 시간 초과 시 동작** | 대기 시간이 초과되면 `NoSuchElementException` 예외를 발생시킵니다.                          | 대기 시간이 초과되면 `TimeoutException` 예외를 발생시킵니다.                                                                      |
| **사용 사례**              | 간단한 페이지 로드 대기 및 요소가 DOM에 나타날 때까지 기본적인 대기를 설정할 때 적합합니다. | 특정 상황이나 조건을 기다려야 하는 복잡한 시나리오에 적합합니다. 예를 들어, JavaScript에 의해 동적으로 로드되는 요소를 기다릴 때. |
| **대기 조건의 유연성**     | 유연성이 낮습니다. 요소가 DOM에 추가되는 것을 기다리는 것이 전부입니다.                     | 매우 유연합니다. 다양한 조건을 설정할 수 있으며, 필요에 따라 사용자 정의 조건도 정의할 수 있습니다.                               |

### `implicitly_wait` 사용 예제

`implicitly_wait`는 WebDriver가 요소를 찾을 때 최대 대기 시간을 설정합니다. 이 시간 내에 요소가 발견되지 않으면 `NoSuchElementException`을 던집니다.

```python
from selenium import webdriver

driver = webdriver.Chrome()
driver.implicitly_wait(10)  # 최대 10초까지 대기

driver.get("https://example.com")
element = driver.find_element(By.ID, "myElement")
```

### `WebDriverWait` 사용 예제

`WebDriverWait`는 특정 조건이 충족될 때까지 기다립니다. 예를 들어, 요소가 DOM에 나타날 때까지 기다리거나, 특정 텍스트가 나타날 때까지 기다릴 수 있습니다.

```python
from selenium import webdriver
from selenium.webdriver.common.by import By
from selenium.webdriver.support.ui import WebDriverWait
from selenium.webdriver.support import expected_conditions as EC

driver = webdriver.Chrome()
driver.get("https://example.com")

# 최대 10초까지 대기하며, 특정 요소가 나타날 때까지 기다림
element = WebDriverWait(driver, 10).until(
    EC.presence_of_element_located((By.ID, "myElement"))
)
```

### 요약

implicitly_wait는 WebDriver 인스턴스 전체에 대해 한 번 설정되며, 요소를 찾을 때마다 설정된 대기 시간을 사용합니다. 주로 간단한 대기 시나리오에 사용됩니다.
WebDriverWait는 특정 조건이 만족될 때까지 기다리는 명시적 대기 방식으로, 특정 상황이나 조건을 기다릴 때 유용합니다. 더 유연하고 강력한 대기 메커니즘을 제공합니다.
