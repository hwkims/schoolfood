![image](https://github.com/user-attachments/assets/eb99466d-cad5-4a4e-aacb-40e044f24010)
![image](https://github.com/user-attachments/assets/f6c2b5c5-4c01-4421-873b-a2b0db6ba835)

```markdown
# 마북초등학교 급식 달력 웹 애플리케이션

이 프로젝트는 **마북초등학교**의 급식 정보를 **NEIS Open API**를 통해 자동으로 불러와 월별 급식 식단을 확인할 수 있는 **달력 형식의 웹 애플리케이션**입니다. 사용자는 달력을 통해 각 날짜의 급식 정보를 확인하고, 이전/다음 달로 쉽게 이동할 수 있습니다.

## 배경

마북초등학교의 급식 식단 정보는 매주마다 홈페이지에서 업데이트됩니다. 이 웹 애플리케이션은 **마북초등학교 급식 정보**를 **NEIS(Open API)**를 활용하여 자동으로 불러오고, 이를 **달력 형식**으로 보여줍니다. 이렇게 함으로써 학부모나 학생들이 급식 정보를 더욱 쉽게 확인할 수 있도록 돕습니다.

- **마북초등학교 급식 정보 페이지**: [마북초등학교 급식 정보](https://mabuk-e.goeyi.kr/mabuk-e/ad/fm/foodmenu/selectFoodMenuView.do?mi=2075)
- **NEIS(Open API)**: [NEIS 급식 API 페이지](https://open.neis.go.kr/portal/data/service/selectServicePage.do?page=1&rows=10&sortColumn=&sortDirection=&infId=OPEN17320190722180924242823&infSeq=2)

## 주요 기능

1. **급식 달력 보기**  
   급식 정보를 월별 달력 형식으로 확인할 수 있습니다. 달력의 각 날짜를 클릭하면 그 날의 급식 정보를 확인할 수 있습니다.

2. **이전/다음 달 보기**  
   **이전 달**과 **다음 달** 버튼을 클릭하여 달력을 자유롭게 이동할 수 있습니다.

3. **오늘 날짜 강조**  
   현재 날짜는 **노란색 배경**으로 강조되어, 사용자가 쉽게 오늘 급식 정보를 확인할 수 있습니다.

4. **급식 정보 자동 불러오기**  
   급식 데이터는 **NEIS Open API**를 통해 자동으로 불러옵니다. 하루에 5일씩 급식 정보를 API로 요청하고, 이를 달력에 표시합니다.

## 기술 스택

- **HTML5**: 웹 페이지 구조를 위한 마크업 언어
- **CSS3**: 스타일링을 위한 스타일 시트 언어
- **JavaScript**: 동적 데이터 처리 및 API 요청을 위한 스크립트 언어
- **NEIS Open API**: 대한민국의 학교 급식 데이터를 제공하는 공공 API
- **GitHub Pages**: 웹 애플리케이션을 호스팅하는 플랫폼

## 사용 방법

1. **GitHub에서 다운로드**  
   이 프로젝트를 로컬에 클론하거나, [이곳](https://github.com/your-username/mabuk-meal-calendar)에서 다운로드하여 사용하실 수 있습니다.

   ```bash
   git clone https://github.com/your-username/mabuk-meal-calendar.git
   ```

2. **웹 페이지 열기**  
   다운로드한 파일을 로컬 서버에서 열거나, 웹 브라우저에서 `index.html` 파일을 더블클릭하여 실행할 수 있습니다.

3. **급식 정보 확인**  
   웹 페이지가 열리면, 달력에서 급식 정보를 확인하고, 이전/다음 달로 이동하여 다른 달의 급식 정보를 확인할 수 있습니다.

4. **네트워크 요청 확인**  
   급식 데이터는 **NEIS API**에서 제공하는 데이터를 기반으로 불러옵니다. 이 API의 응답 속도나 서버 상태에 따라 로딩 시간이 다를 수 있습니다.

## 코드 설명

### 1. **HTML 구조**

```html
<body>
    <div class="container">
        <!-- 달력 전환 버튼 -->
        <div class="month-switcher">
            <button class="month-button" id="prev-month">이전 달</button>
            <button class="month-button" id="next-month">다음 달</button>
        </div>

        <h1 id="calendar-title">2024년 11월 급식 달력</h1>
        <div class="calendar" id="calendar">
            <!-- 달력이 여기에 동적으로 생성됩니다. -->
        </div>
        <div class="loading" id="loading">급식 정보를 불러오는 중...</div>
    </div>
</body>
```

- **달력 전환 버튼**: 사용자가 이전 달 또는 다음 달로 이동할 수 있도록 돕는 버튼입니다. 이 버튼들은 `prev-month`와 `next-month` ID를 가지며, JavaScript에서 클릭 이벤트를 통해 달력을 전환할 수 있도록 설정됩니다.
- **급식 달력**: `calendar-title` 요소는 현재 달의 제목을 표시하고, `calendar` 요소는 실제 달력을 표시하는 컨테이너입니다.
- **로딩 메시지**: 급식 정보를 불러오는 동안 `loading` 메시지가 표시됩니다.

### 2. **CSS 스타일링**

```css
* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}

body {
    background-color: #f4f4f4;
    color: #333;
    padding: 20px;
}

.container {
    width: 80%;
    margin: 0 auto;
}

h1 {
    text-align: center;
    margin-bottom: 20px;
}

.calendar {
    display: grid;
    grid-template-columns: repeat(7, 1fr);
    gap: 10px;
    margin-bottom: 20px;
}

.calendar div {
    text-align: center;
    padding: 20px;
    background-color: #fff;
    border-radius: 8px;
    box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
    font-size: 16px;
    color: #333;
}

.calendar div.today {
    background-color: #ffeb3b;
    font-weight: bold;
}

.calendar .day {
    font-weight: bold;
}

.meal-info {
    margin-top: 10px;
    font-size: 12px;
    color: #555;
}

.loading {
    text-align: center;
    font-size: 18px;
    color: #555;
}

.month-switcher {
    text-align: center;
    margin-top: 20px;
}

.month-button {
    padding: 10px 20px;
    margin: 0 10px;
    background-color: #4caf50;
    color: white;
    border: none;
    border-radius: 5px;
    cursor: pointer;
}

.month-button:hover {
    background-color: #45a049;
}
```

- **스타일링**: 이 CSS는 달력의 디자인을 포함하고 있으며, 날짜를 표시하는 셀, 버튼, 로딩 메시지 등을 스타일링합니다. 주요 디자인 요소는 달력의 그리드, 배경색, 텍스트 스타일, 그리고 '오늘 날짜'를 강조하는 스타일입니다.

### 3. **JavaScript 동작**

```javascript
const monthDays = {
    1: 31,
    2: 29,
    3: 31,
    4: 30,
    5: 31,
    6: 30,
    7: 31,
    8: 31,
    9: 30,
    10: 31,
    11: 30,
    12: 31
};

let currentYear = 2024;
let currentMonth = 12;  // 12월부터 시작

const calendarDays = [];

function getMonthDateRange(year, month) {
    const daysInMonth = monthDays[month];
    const dateRanges = [];
    
    for (let i = 1; i <= daysInMonth; i += 5) {
        const startDate = `${year}${month.toString().padStart(2, '0')}${i.toString().padStart(2, '0')}`;
        const endDate = `${year}${month.toString().padStart(2, '0')}${Math.min(i + 4, daysInMonth).toString().padStart(2, '0')}`;
        dateRanges.push({ startDate, endDate });
    }
    return dateRanges;
}

function generateCalendar() {
    const calendarContainer = document.getElementById('calendar');
    calendarContainer.innerHTML = '';
    const title = document.getElementById('calendar-title');
    title.textContent = `${currentYear}년 ${currentMonth}월 급식 달력`;

    const daysOfWeek = ['일', '월', '화', '수', '목', '금', '토'];
    daysOfWeek.forEach(day => {
        const dayHeader = document.createElement('div');
        dayHeader.className = 'day';
        dayHeader.textContent = day;
        calendarContainer.appendChild(dayHeader);
    });

    const startDayOfWeek = new Date(currentYear, currentMonth - 1, 1).getDay();
    for (let i = 0;

 i < startDayOfWeek; i++) {
        const emptyDay = document.createElement('div');
        calendarContainer.appendChild(emptyDay);
    }

    for (let day = 1; day <= monthDays[currentMonth]; day++) {
        const dayCell = document.createElement('div');
        dayCell.className = 'calendar-day';
        dayCell.textContent = day;
        calendarContainer.appendChild(dayCell);
    }
}

document.getElementById('prev-month').addEventListener('click', () => {
    if (currentMonth === 1) {
        currentMonth = 12;
        currentYear--;
    } else {
        currentMonth--;
    }
    generateCalendar();
});

document.getElementById('next-month').addEventListener('click', () => {
    if (currentMonth === 12) {
        currentMonth = 1;
        currentYear++;
    } else {
        currentMonth++;
    }
    generateCalendar();
});

generateCalendar();
```

### 코드 동작 설명

1. **달력 데이터 생성**  
   `generateCalendar()` 함수는 현재 연도와 월에 맞는 달력을 생성합니다. 먼저, 주의 시작 요일을 계산하여 그에 맞게 빈 날짜를 추가하고, 각 날짜에 대한 셀을 생성합니다.

2. **급식 데이터 요청 및 처리**  
   `getMealData()` 함수는 NEIS API로부터 급식 데이터를 가져옵니다. 이 데이터는 날짜별로 급식 메뉴를 포함하고 있으며, 이를 달력의 각 날짜에 표시합니다.

3. **달력 전환**  
   `prev-month`와 `next-month` 버튼을 클릭하면 현재 달이 변경됩니다. 이때 `generateCalendar()` 함수를 호출하여 달력을 다시 그립니다.

4. **오늘 날짜 강조**  
   `today` 클래스는 오늘 날짜를 강조하는 데 사용됩니다. JavaScript에서 현재 날짜를 가져와 해당 날짜에 스타일을 적용합니다.

## 개선 사항

이 애플리케이션은 급식 정보를 보여주는 기본적인 기능을 제공합니다. 향후 개선할 수 있는 사항은 다음과 같습니다:

- **급식 메뉴 검색 기능**: 특정 메뉴가 포함된 날을 검색하는 기능 추가.
- **사용자 맞춤형 기능**: 학생들이 자신이 먹지 않는 메뉴를 제외하고 표시하는 기능 추가.
- **API 응답 최적화**: 더 빠르고 안정적인 API 응답을 위한 개선.
- **UI 개선**: 모바일 및 데스크탑 화면에서 더욱 편리하게 사용할 수 있도록 UI 디자인 개선.

## 기여 방법

이 프로젝트에 기여하고 싶으신 분들은 다음 절차를 따르세요:

1. 이 리포지토리를 포크(Fork)합니다.
2. 새로운 브랜치를 생성합니다.
3. 변경 사항을 커밋하고 푸시합니다.
4. 풀 리퀘스트(Pull Request)를 생성하여 기여 내용을 제출합니다.

## 라이선스

이 프로젝트는 MIT 라이선스를 따릅니다. 자세한 사항은 `LICENSE` 파일을 참고하세요.

---

마북초등학교 급식 달력 웹 애플리케이션을 통해 학부모나 학생들이 손쉽게 급식 정보를 확인하고, 일정을 관리하는 데 유용한 도구가 되기를 바랍니다.
```

### 설명
- **코드 설명** 부분은 HTML, CSS, JavaScript의 각 부분에 대해 자세히 설명하였습니다.
  - HTML 구조는 어떻게 달력을 구성하는지, 사용자 인터페이스가 어떻게 구성되는지 설명합니다.
  - CSS는 달력의 디자인을 정의하고, 어떻게 날짜 셀을 스타일링하는지 다룹니다.
  - JavaScript는 달력 생성, 급식 정보 API 요청, 달력 전환 등의 로직을 설명합니다.
