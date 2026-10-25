---
{"dg-publish":true,"permalink":"/digital-garden/digital-garden-on-github-page/","dg-note-properties":{}}
---



### 전체 흐름

Obsidian에서 노트 발행 → 플러그인이 GitHub 저장소에 노트를 올림 → GitHub Actions가 사이트를 빌드 → GitHub Pages에 게시 (1~2분 소요)

---

### 1단계. GitHub 계정 준비

[github.com](https://github.com)에 가입합니다. 이후 내 GitHub 아이디를 `내아이디`로 표기하겠습니다.

### 2단계. 템플릿으로 저장소 만들기

1. 템플릿 저장소 [https://github.com/oleeskild/digitalgarden](https://github.com/oleeskild/digitalgarden) 에 접속합니다.
2. 오른쪽 위 초록색 **Use this template → Create a new repository**를 누릅니다.
3. 설정값을 입력합니다.
    - **Repository name**: `내아이디.github.io` ← **반드시 이 형식으로 지어주세요.** (이유는 아래 주의사항 1 참고)
    - **Public**을 선택합니다. 무료 계정은 Public 저장소에서만 Pages를 쓸 수 있습니다.
4. **Create repository**를 누릅니다.

### 3단계. 자동 배포 설정 파일 추가

1. 방금 만든 저장소 화면에서 **Add file → Create new file**을 누릅니다.
2. 파일 이름 칸에 `.github/workflows/deploy.yml`을 그대로 입력합니다. `/`를 입력하면 폴더가 자동으로 만들어집니다.
3. 아래 내용을 복사해서 붙여 넣습니다.

yaml

```yaml
name: Deploy Digital Garden to GitHub Pages

on:
  push:
    branches: [main]
  workflow_dispatch:

permissions:
  contents: read
  pages: write
  id-token: write

concurrency:
  group: pages
  cancel-in-progress: true

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v5
      - uses: actions/setup-node@v5
        with:
          node-version: 22
          cache: npm
      - run: npm install
      - run: npm run build
      - uses: actions/configure-pages@v6
      - uses: actions/upload-pages-artifact@v5
        with:
          path: ./dist

  deploy:
    needs: build
    runs-on: ubuntu-latest
    environment:
      name: github-pages
      url: ${{ steps.deployment.outputs.page_url }}
    steps:
      - id: deployment
        uses: actions/deploy-pages@v5
```

4. **Commit changes**를 눌러 저장합니다.

### 4단계. GitHub Pages 켜기

1. 저장소의 **Settings → Pages** 메뉴로 갑니다.
2. **Build and deployment → Source**를 **GitHub Actions**로 바꿉니다.
3. 저장소의 **Actions** 탭에서 워크플로가 실행되는지 확인합니다. 실행되지 않았다면 워크플로를 선택하고 **Run workflow**를 누르세요.
4. 초록색 체크가 뜨면 `https://내아이디.github.io`에 접속해 기본 페이지가 보이는지 확인합니다.

### 5단계. 플러그인용 GitHub 토큰 만들기

플러그인이 내 저장소에 노트를 올리려면 일종의 "열쇠"가 필요합니다.

1. GitHub 오른쪽 위 프로필 → **Settings → Developer settings → Personal access tokens → Fine-grained tokens → Generate new token**으로 들어갑니다.
2. 설정값을 입력합니다.
    - **Token name**: `digital-garden`
    - **Expiration**: 원하는 기간 (만료되면 새로 발급해야 합니다)
    - **Repository access**: **Only select repositories** → `내아이디.github.io` 선택
    - **Permissions → Repository permissions**:
        - **Contents**: Read and write
        - **Pull requests**: Read and write (템플릿 업데이트 기능에 필요)
3. **Generate token**을 누르고, 나온 토큰을 **바로 복사해 둡니다.** 이 화면을 벗어나면 다시 볼 수 없습니다.

### 6단계. Obsidian 플러그인 설치·설정

1. Obsidian **설정 → 커뮤니티 플러그인 → 탐색**에서 **Digital Garden**을 검색해 설치하고 **활성화**합니다.
2. 플러그인 설정에 다음 값을 입력합니다.
    - **GitHub Username**: `내아이디`
    - **GitHub repo name**: `내아이디.github.io`
    - **GitHub token**: 5단계에서 복사한 토큰
    - **Base URL**: `https://내아이디.github.io`
3. 입력 칸 옆에 연결 성공 표시(체크)가 뜨는지 확인합니다.

### 7단계. 첫 글 발행

1. 홈 화면으로 쓸 노트 맨 위에 다음 속성을 넣습니다.

markdown

```markdown
---
dg-home: true
dg-publish: true
---
```

2. 다른 글에는 `dg-publish: true`만 넣으면 됩니다. **이 속성이 없는 노트는 발행되지 않습니다.**
3. `Cmd + P`로 명령 팔레트를 열고 다음 중 하나를 실행합니다.
    - **Digital Garden: Publish Single Note**: 지금 열린 노트 하나만 발행
    - **Digital Garden: Publish Multiple Notes**: 발행 대상 전체를 확인하고 한꺼번에 발행
4. GitHub **Actions** 탭에서 빌드가 끝나면 1~2분 뒤 사이트에 반영됩니다.

### 8단계. 파일 트리(Filetree) 표시 설정 켜기

파일 트리는 기본으로 켜져 있지만 한 번 확인해 보세요.

1. Obsidian **설정 → Digital Garden → Note Settings → Edit**으로 들어갑니다.
2. **Show filetree sidebar**가 켜져 있는지 확인합니다.
3. 이 설정은 바꾸는 즉시 사이트에 반영되므로 노트를 다시 발행할 필요가 없습니다.

---

### 주의사항

1. **저장소 이름은 꼭 `내아이디.github.io`로 지어주세요.** 다른 이름(예: `blog`)으로 만들면 주소가 `내아이디.github.io/blog/`가 되는데, 템플릿이 사이트 최상위 경로를 기준으로 만들어져 있어서 CSS와 링크가 깨질 가능성이 높습니다. 커스텀 도메인을 연결하는 경우에는 이 문제가 없습니다.
2. **Public 저장소이므로 발행한 노트의 원본 마크다운도 공개됩니다.** 회사 내부 자료나 업무 노트에 실수로 `dg-publish: true`가 들어가지 않았는지 발행 전에 확인하세요.
3. **삭제나 수정도 반영해야 합니다.** 노트를 고친 뒤에는 다시 Publish해야 하고, 사이트에서 내린 글은 Publish Multiple Notes 화면에서 삭제 대상으로 처리됩니다.
4. **템플릿 업데이트**: 플러그인 설정의 템플릿 업데이트 기능을 쓰면 Pull Request가 생성됩니다. GitHub에서 그 PR을 Merge하면 반영되고, 3단계에서 만든 `deploy.yml`은 그대로 유지됩니다.
5. **커스텀 도메인**(선택): Settings → Pages → Custom domain에서 연결할 수 있습니다. 연결한 뒤에는 플러그인의 Base URL도 새 도메인으로 바꿔주세요.