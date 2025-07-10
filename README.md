# Mankind

# Hi-Finance

Hi-Finance는 금융 파생상품 투자 시나리오를 빠르고 직관적으로 확인할 수 있는 웹 애플리케이션입니다.  
PDF 약관을 업로드하면 주요 투자 조건을 자동으로 추출·검증하고, 대시보드에서 핵심 지표와 수익/상환 시나리오를 시각화합니다.

![Hi-Finance 스크린샷](./docs/screenshot.png)

---
✍️ 내가 맡은 주요 작업
PDF 업로드 UI/UX (UploadBox, ConfirmButton, React Query 연동)

VerifyPage 컴포넌트

InfoRow, SectionHeader, EditConfirmButtons 등 재사용 컴포넌트 작성

읽기/편집 모드 전환, 유효성 검사, localStorage 저장 로직 구현

Dashboard

IndexChart, RevenueStructure, RepaymentScenario 차트 구현 (Recharts)

Modal 확대 보기, 툴팁/범례 커스터마이징

Tailwind CSS 그리드 레이아웃 & 반응형 min-width 조정

TypeScript 타입 정의 (types.ts, InputProps, PdfValue, RoundKey 등)

유틸 함수

savedFile (localStorage 읽기/쓰기)

validationCheck (숫자/날짜 검사)

format (날짜 포매팅)

배포 설정: Vercel + monorepo 구조 (frontend 전용)




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

