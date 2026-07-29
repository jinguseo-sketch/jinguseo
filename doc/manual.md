# 서진구 부동산 블로그 & 포트폴리오 제작 매뉴얼

이 문서는 **Hugo Blox (Extended)** 기반으로 제작된 부동산 전문가(서진구) 웹사이트의 프로젝트 구조, 설정 방법 및 콘텐츠 관리 가이드를 담고 있습니다.

---

## 1. 프로젝트 개요 및 기술 스택

- **프레임워크**: Hugo (Extended v0.163+) & Hugo Blox Builder
- **스타일링 & 스크립트**: Vanilla CSS, TailwindCSS, Preact
- **배포 타겟**: GitHub Pages / Cloudflare Pages
- **사이트 주소**: [https://jinguseo.net/](https://jinguseo.net/)

---

## 2. 프로젝트 폴더 구조

```text
C:\dev\myweb\
├── assets/                  # 이미지, 로고, 커스텀 스타일 및 미디어 파일
│   └── media/               # 브랜드 로고 및 프로필/배경 이미지
├── config/                  # Hugo 사이트 설정 파일 폴더
│   └── _default/
│       ├── hugo.yaml        # Hugo 핵심 설정 (기본 언어, 이미지 가공, 빌드 옵션)
│       ├── params.yaml      # 사이트 메타데이터, 브랜드명, SEO, 소셜 링크
│       ├── menus.yaml       # 상단 내비게이션 메인 메뉴 및 푸터 링크
│       └── languages.yaml   # 다국어 및 로캘 설정 (ko)
├── content/                 # 페이지 및 블로그 콘텐츠
│   ├── _index.md            # 메인 랜딩 페이지 (Hero, About, Services, Insights 등)
│   ├── blog/                # 블로그 칼럼 포스트 폴더
│   │   ├── manhattan-commercial-prospects/
│   │   └── bergen-county-education-housing/
│   ├── privacy.md           # 개인정보 처리방침
│   └── terms.md             # 이용약관
├── data/                    # 데이터 파일
│   └── authors/
│       └── me.yaml          # 프로필/저자 정보 (서진구 프로필, 약력, 연락처)
└── doc/                     # 프로젝트 관리 문서
    ├── manual.md            # 제작 매뉴얼 (본 문서)
    └── issues.md            # 트러블슈팅 및 문제 해결 기록
```

---

## 3. 핵심 수정 파일 및 역할

| 파일 경로 | 파일 설명 및 주요 역할 |
| :--- | :--- |
| `config/_default/hugo.yaml` | 기본 언어(`ko`), CJK 지원, 이미지 품질(`jpeg`, `webp`, `avif`) 최신 규격 설정 |
| `config/_default/params.yaml` | 사이트 이름("서진구"), 한 줄 소개, SEO 태그, 소셜 링크(페이스북, 유튜브, 네이버 블로그, 인스타그램) |
| `config/_default/menus.yaml` | 상단 네비게이션 메뉴(`소개`, `전문 서비스`, `부동산 인사이트`, `상담 문의`) |
| `config/_default/languages.yaml` | `ko` 한국어 로캘 및 언어 라벨 지정 |
| `data/authors/me.yaml` | 프로필명, 역할("뉴욕 & 뉴저지 부동산 에이전트 / 자산 컨설턴트"), 이메일 |
| `content/_index.md` | 메인 랜딩 페이지 섹션 구성 (Hero, Stats, About, Services, Insights, Contact) |

---

## 4. 앞으로 내용/글을 수정할 때 다루는 파일

### ① 메인 랜딩 페이지 문구 및 섹션 변경
- 파일 위치: `content/_index.md`
- 수정 방법: 각 `block` 단위(hero, stats, cta-image-paragraph, features, cta-card)의 `title`, `text`, `items` 내용을 수정합니다.

### ② 새 블로그 칼럼/글 추가
- 파일 위치: `content/blog/` 아래에 새로운 폴더를 생성하고 `index.md` 작성
- 작성 형태:
  ```markdown
  ---
  title: '[맨해튼 인사이트] 글 제목'
  date: 2026-07-29
  summary: 글 요약 문구
  categories:
    - 맨해튼 인사이트
  authors:
    - me
  ---
  여기에 칼럼 본문을 작성합니다.
  ```

### ③ 프로필 정보 (약력, 연락처, 소셜 링크) 수정
- 프로필 및 연락처: `data/authors/me.yaml`
- 메인 소셜 아이콘 링크: `config/_default/params.yaml` (`identity.social.links`)

### ④ 상단/하단 메뉴 변경
- 파일 위치: `config/_default/menus.yaml`

---

## 5. 로컬 실행 및 빌드 방법

```powershell
# 1. 개발 서버 실행 (실시간 미리보기: http://localhost:1313/)
hugo server

# 2. 정적 웹사이트 생성 빌드
hugo
```
