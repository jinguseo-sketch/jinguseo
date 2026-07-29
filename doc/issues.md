# 문제 해결 및 트러블슈팅 기록 (Issues Log)

이 문서는 Hugo Blox 웹사이트 구축 및 커스터마이징 과정에서 발생한 오류/이슈 및 해결 방안, 그리고 향후 유지보수 시 예방법을 기록한 문서입니다.

---

## 1. 발생했던 오류 및 해결 내역

### 🔴 Issue 1: Git Push 403 Forbidden 권한 오류
- **증상**: `git push -u origin main` 실행 시 아래 에러 발생
  ```text
  remote: Permission to ccumgol/jinguseo.git denied to jinguseo-sketch.
  fatal: unable to access 'https://github.com/ccumgol/jinguseo.git/': The requested URL returned error: 403
  ```
- **원인**: Windows 자격 증명 관리자(Credential Manager)에 기존 `jinguseo-sketch` 계정이 저장되어 있어 타 계정 저장소 접근이 거부됨.
- **해결 방법**:
  1. Windows 자격 증명 삭제: `cmdkey /delete:LegacyGeneric:target=git:https://github.com`
  2. 원격 저장소 URL을 본인 소유 저장소로 변경:
     ```powershell
     git remote set-url origin https://github.com/jinguseo-sketch/jinguseo.git
     git push -u origin main
     ```

---

### 🔴 Issue 2: Hugo defaultContentLanguage "ko" Not Found
- **증상**: `hugo.yaml`에서 `defaultContentLanguage: ko`로 설정 후 빌드 실패
  ```text
  ERROR failed to create config from result: failed to decode "languages": failed to decode languages config: defaultContentLanguage "ko" not found in languages configuration
  ```
- **원인**: `config/_default/languages.yaml`에 `en` 설정만 존재하여 `ko` 언어 키를 찾지 못함.
- **해결 방법**: `config/_default/languages.yaml` 파일에 `ko` 라벨 및 로캘 정의 추가:
  ```yaml
  ko:
    label: 한국어
    locale: ko-kr
    weight: 1
  ```

---

### 🔴 Issue 3: Hugo v0.163+ Deprecation Warning (`imaging.quality` & `imaging.hint`)
- **증상**: Hugo 빌드 실행 시 Deprecated 경고 메시지 출력
  ```text
  INFO deprecated: project config key imaging.quality was deprecated in Hugo v0.163.0...
  INFO deprecated: project config key imaging.hint was deprecated in Hugo v0.163.0...
  ```
- **원인**: Hugo v0.163 이상에서 `imaging` 설정의 최상위 `quality` 및 `hint` 키가 포맷별 서브키로 분리됨.
- **해결 방법**: `config/_default/hugo.yaml`의 `imaging` 구조를 포맷별 하위 설정으로 변경:
  ```yaml
  imaging:
    resampleFilter: lanczos
    anchor: smart
    jpeg:
      quality: 90
    webp:
      quality: 90
      hint: picture
    avif:
      quality: 90
      hint: picture
  ```

---

### 🔴 Issue 4: PowerShell Script Execution Policy & Node 종속성 누락
- **증상**: `npm install` 실행 시 `.ps1` 스크립트 실행 제한 에러 또는 Preact / TailwindCSS 빌드 모듈 부재 에러
- **원인**: Windows PowerShell 보안 정책으로 인해 `.ps1` 래퍼 스크립트 실행 제한 및 node_modules 미설치 상태.
- **해결 방법**: `cmd.exe /c "npm install"`을 사용하여 의존성 패키지를 동기화 설치.

---

## 2. 향후 발생 가능한 문제 및 예방법

1. **Hugo 버전에 따른 Deprecated 구문 주의**:
   - `hugo build --logLevel debug` 명령어를 활용하여 폐지 예정 경고(Deprecation Warnings)를 사전에 점검하세요.
2. **블로그 포스트 작성 시 Front Matter 유효성**:
   - 새 글 작성 시 YAML Front Matter(`---` 사이의 설정) 형식이 깨지지 않도록 유의하세요.
3. **이미지 파일 경로**:
   - 포스트 내 이미지는 `assets/media/` 디렉토리에 넣고 상대 파일명을 사용하거나, 포스트 폴더 내부(`content/blog/포스트명/featured.jpg`)에 배치하세요.
