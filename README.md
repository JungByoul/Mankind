# Mankind

# Hi-Finance

Hi-Finance는 금융 파생상품 투자 시나리오를 빠르고 직관적으로 확인할 수 있는 웹 애플리케이션입니다.  
PDF 약관을 업로드하면 주요 투자 조건을 자동으로 추출·검증하고, 대시보드에서 핵심 지표와 수익/상환 시나리오를 시각화합니다.

![image](https://github.com/user-attachments/assets/992ae447-8391-47ca-ac5c-920cd4794c2f)

---
## ✍️ 각자 역할 및 핵심 수행 작업

**🌟 정별**

## 1. Front-end
   **1-1 Dashboard 차트 구현**
      - 수익구조 분석 차트(RevenueStructure): 1~5차 조기상환 수익률 LineChart

      - 만기 상환 시나리오(RepaymentScenario): 조기상환 조건 및 수익률 vs. 만기상환 시나리오 비교 LineChart

      - Modal(확대 보기), 툴팁·범례 커스터마이징 및 Tailwind 기반 레이아웃 최적화

      - 데이터 흐르 및 상태 관리: 차트 컴포넌트 내부에서 getFileValue() 호출해 최신 파싱값을 기반으로 entries 배열 생성

   **1-2 Verify Page 구현**
      - SectionHeader, InfoRow, EditButton 등 재사용 가능한 컴포넌트 개발

      - 읽기/편집 모드 전환, 유효성 검사(숫자·날짜·빈값) 및 수정(에러 처리) 로직 구현

      - 데이터 흐름 및 상태관리: getFileValue() 로 저장된 파싱값 불러오기 → InfoRow 컴포넌트로 렌더링 및 수정
         ->수정 완료 시 setFileValue(editedData) → 다시 로컬스토리지에 저장 → navigate('/dashboard')

      - 페이지 전체 UI 구성



   ## 2. 데이터 전처리·분석 (Python)

      - 신한투자증권 파생상품 투자설명서(PDF): 주요 투자 조건 추출을 위한 파이썬 스크립트 작성

      - 기준값(낙인구간, 자동조기상환 조건, 수익률 등) 수립 로직 구현

      - 판다스(Pandas) 기반 전처리 파이프라인 설계 및 테스트 데이터 생성

---

## 🎯 주요 기능

1. **PDF 업로드 & 파싱**  
   - 사용자가 PDF 파일을 드래그&드롭 또는 클릭으로 업로드  
   - 서버(API)로 전송 → PDF 내부 텍스트/숫자 데이터 추출 → 클라이언트 로컬스토리지에 저장  

2. **값 확인(Verify) 페이지**  
   - 파싱된 지표(기초자산, 낙인구간, 만기일, 자동조기상환 조건 등) 일괄 렌더링  
   - 수정 모드: 입력값 유효성 검사(숫자, 빈 값, 날짜) 후 재저장  
   - “수정” · “확인” 플로팅 버튼으로 UX 개선  

3. **대시보드(Dashboard)**  
   - **지수 차트(IndexChart)**: KOSPI200, EURO STOXX50, S&P500 시계열 차트  
   - **수익구조 분석 차트(RevenueStructure)**: 1~5차 조기상환 수익률 LineChart  
   - **만기 상환 시나리오(RepaymentScenario)**: 조기상환 충족 조건 vs. 만기상환 시나리오 비교 LineChart  
   - Modal(확대 보기) 기능 제공  

4. **반응형 레이아웃 & 테마**  
   - Tailwind CSS + CSS 모듈 활용  
   - 최소 너비(min-width)로 컬럼 겹침 방지  
   - 고정(header/footer) 및 그리드 레이아웃  

5. **배포 & 인프라**  
   - Vite + React + TypeScript  
   - React Query로 API 상태 관리  
   - Vercel에 프론트엔드 배포 (백엔드는 별도 호스팅)  

---

## 🛠 Tech Stack

- **Frontend**: React, Vite, TypeScript, Tailwind CSS  
- **Data Fetching**: Axios, React Query  
- **Charts**: Recharts  
- **PDF 파싱 서버**: Node.js/Express 
- **배포**: Vercel  

---

## 📂 폴더 구조
/frontend
├─ /src
│ ├─ /apis # Axios instance & API 함수
│ ├─ /components # 전역 UI 컴포넌트(Spinner, Alert, Sidebar 등)
│ ├─ /pages
│ │ ├─ StartPage # PDF 업로드
│ │ ├─ VerifyPage # 추출값 확인 & 수정
│ │ └─ Dashboard # 지수, 수익구조, 상환시나리오
│ ├─ /utils # savedFile, validation, format 등
│ ├─ /hooks # useVerifyData, usePostFile 등
│ ├─ /typings # TypeScript 인터페이스/타입
│ └─ index.tsx / App.tsx
├─ tsconfig.json
└─ vite.config.ts

