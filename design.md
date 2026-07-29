# Design Specification: jesusiswith.us (JIWU Mission Design System)

이 문서는 [https://jesusiswith.us/](https://jesusiswith.us/) 디자인 스튜디오 학습(Study)을 바탕으로 추출한 디자인 시스템 규격 및 스타일 가이드라인입니다.

---

## 1. Design Concept & Brand Personality

- **Concept**: 신뢰감 높은 에디토리얼 스타일 (Trustworthy, Professional, Clean Editorial Layout)
- **Mood**: 정갈함, 깊이감 있는 세련됨, 높은 가독성, 부드러운 여백(Padding/Margin)
- **Key Characteristics**:
  - 선명한 텍스트 대비와 가독성 중심 타이포그래피
  - 라운드 카드 레이아웃 (`rounded-xl`, `rounded-2xl`) 및 얇은 경계선(`border border-border`)
  - 다크모드/라이트모드 완벽 대응 (Light/Dark Mode Seamless Switcher)
  - 아이콘 인디케이터 배지 (`w-16 h-16 rounded-2xl bg-primary/10`) 및 그리드 카드시스탬

---

## 2. Color Palette & Dark Mode Rules

### Light Mode Colors
- **Background Main**: `#ffffff` (Pure White)
- **Background Sub (Theme Light)**: `#f8fafc` / `#f1f5f9` (Soft Gray Neutral)
- **Primary Accent**: `#1e3a8a` (Navy Blue) / `#2563eb` (Royal Blue)
- **Text Main (`text-dark`)**: `#0f172a` (Slate Dark)
- **Text Muted (`text-light`)**: `#64748b` (Slate Gray)
- **Border (`border`)**: `#e2e8f0` (Light Gray Divider)

### Dark Mode Colors
- **Dark Body (`dark:bg-darkmode-body`)**: `#0f172a` (Deep Slate / Dark Navy)
- **Dark Card Surface (`dark:bg-darkmode-theme-light`)**: `#1e293b` (Slate 800)
- **Dark Text Main**: `#f8fafc` (Pure White / Off-White)
- **Dark Text Muted**: `#94a3b8` (Light Slate Muted)
- **Dark Border**: `#334155` (Slate 700)

---

## 3. Typography & Hierarchy

- **Font Family**: `Noto Sans KR`, sans-serif (Weights: 400, 500, 600, 700, 800)
- **Hero Title (H1)**: `text-3xl lg:text-5xl font-bold leading-tight font-secondary`
- **Section Heading (H2)**: `text-2xl lg:text-4xl font-bold text-text-dark dark:text-white`
- **Sub-eyebrow Badge**: `text-xs font-mono uppercase tracking-widest text-primary`
- **Body Text**: `text-base md:text-lg leading-relaxed text-text-light dark:text-darkmode-text-light`

---

## 4. Component Design Patterns

### 1) Header & Navigation
- **Top Bar**: Sticky Top Navigation Bar (`sticky top-0 z-30`)
- **Branding**: 로고 텍스트/이미지 + 다크모드 대응 로고
- **Utility Items**: 언어 스위처 (`KR | EN`), 테마 토글, 서치 버튼, CTA 버튼 (`btn-outline-primary`)

### 2) Hero Section
- **Layout**: 2-Column Split (`col-12 lg:col-6` Content + `col-12 lg:col-6` Visual Image)
- **Action Buttons**:
  - Primary CTA (`btn-primary` - Solid Fill + Icon)
  - Secondary CTA (`btn-outline-primary` - Border Outline + Icon)

### 3) Core Strengths / Goal Cards
- **Indicator**: `MISSION GOAL 01`, `02`, `03` 형태의 트래킹 인디케이터
- **Icon Container**: `w-16 h-16 rounded-2xl bg-primary/10 dark:bg-primary/20 flex items-center justify-center`
- **Bullet Points**: `fa-check absolute left-0 top-1 text-primary` 가부 체크 아이콘 적용

### 4) Grid Card System (Services & Insights)
- **Grid Layout**: `grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6`
- **Card Style**: `rounded-xl bg-white dark:bg-darkmode-body border border-border dark:border-darkmode-border p-6 shadow-sm hover:shadow-lg transition-all`

### 5) Newsletter / Special Action Card
- **Layout**: 이미지/일러스트 픽처 영역 + 설명/구독 신청 버튼 폼 카드의 가로 분할 형태

---

## 5. Application Strategy for `C:\dev\myweb`

1. **디자인 테마 반영**: `params.yaml`에 `jesusiswith.us` 스펙 기반 다크모드, 서체(`geometric`/`Noto Sans KR`), 컬러 매핑 반영
2. **콘텐츠 구조 레이아웃**: `content/_index.md`에 `jesusiswith.us`의 Hero 2열 구조, 목표/강점 3단 카드, 3컬럼 서비스 그리드 및 뉴스레터 스페셜 카드를 적용
3. **스타일 동기화**: Hugo Blox Tailwind 스타일 및 컴포넌트 클래스를 규격에 맞춰 정리
