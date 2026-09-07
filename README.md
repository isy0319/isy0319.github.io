# EMLAB 홈페이지 (GitHub Pages)

관리자 1명이 로그인 없이 관리하는 정적 연구실 홈페이지입니다.
로그인/회원가입 기능은 없고, GitHub 저장소에 파일을 추가/수정하는 것 자체가
"게시글 작성"이 됩니다.

## 1. 먼저 내 정보로 바꾸기

`_config.yml` 파일을 열어 아래 값들을 실제 정보로 수정하세요.

```yaml
lab_full_name_en: "Energy Mechatronics Lab"
lab_full_name_kr: "에너지 메카트로닉스 연구실"
university: "OO National University"
pi_name: "OOO, Ph.D."
pi_email: "emlab@example.ac.kr"
pi_tel: "0XX-XXX-XXXX"
address: "..."
```

그 다음 아래 페이지들의 예시 문구(플레이스홀더)를 실제 내용으로 바꿔주세요.

| 파일 | 내용 |
|---|---|
| `index.html` | 홈 화면(Recent News) 소개 문구, 연구 분야 요약 |
| `about.html` | Introduction / Equipments / Contact / Visit Us |
| `team.html` | Professor / Ph.D. / M.S. / Alumni 명단 |
| `research.html` | 연구 개요, Projects / 논문(국내외 저널·학회) / 특허 |
| `news.html` | 게시판(전체 소식 목록) + Events |
| `pictures.html` | Conference / Graduation / Other Activities 사진 |
| `join.html` | 지원 방법, 모집 분야 |

## 2. 새 소식(게시글) 올리는 방법 — "게시판" 역할

학회 후기, 수상 소식 등은 `_posts` 폴더에 파일 하나를 추가하는 것으로 올립니다.

1. `_posts` 폴더 안의 예시 파일(`2026-08-20-mathworks-award.md`)을 복사
2. 파일 이름을 `YYYY-MM-DD-내용요약.md` 형식으로 저장 (날짜가 게시일이 됩니다)
   - 예: `2026-09-07-icra-2027-accepted.md`
3. 파일 맨 위 `---` 사이의 정보를 수정
   ```yaml
   ---
   title: "게시글 제목"
   tag: AWARDS        # AWARDS / CONFERENCE / EVENTS 등 원하는 태그
   excerpt: "목록에 보일 한 줄 요약"
   image: /assets/img/news/파일명.jpg   # 사진이 없으면 이 줄은 삭제
   ---
   ```
4. `---` 아래에 본문 내용을 마크다운으로 작성
5. 사진이 있다면 `assets/img/news/` 폴더에 넣고, `image:` 항목에 경로 입력
6. 파일을 GitHub 저장소에 커밋(push)하면 자동으로 사이트에 반영됩니다

> GitHub 웹사이트에서 직접 "Add file → Create new file"로도 작성 가능해서,
> 컴퓨터에 아무것도 설치하지 않고도 브라우저에서 새 글을 올릴 수 있습니다.

## 3. GitHub Pages로 배포하기

1. GitHub에 새 저장소를 만듭니다 (예: `emlab-site` 또는 `내계정.github.io`)
2. 이 폴더의 모든 파일을 그 저장소에 업로드(push)합니다
3. 저장소의 **Settings → Pages** 로 이동
4. **Source**를 `Deploy from a branch`, 브랜치는 `main`, 폴더는 `/(root)` 로 설정 후 저장
5. 몇 분 후 `https://내계정.github.io/emlab-site/` 형태의 주소로 접속 가능

### 저장소 이름이 `내계정.github.io`가 아닌 경우 (예: `emlab-site`)

`_config.yml`의 `baseurl` 값을 저장소 이름으로 바꿔주세요.

```yaml
baseurl: "/emlab-site"
```

### 커스텀 도메인을 쓰고 싶다면 (예: emlab.inu.ac.kr 같은 학교 서브도메인)

1. 저장소 최상위에 `CNAME` 파일을 만들고 도메인 하나만 적어서 저장 (예: `emlab.yourdomain.ac.kr`)
2. 학교/기관 DNS 관리자에게 해당 도메인을 GitHub Pages로 연결하는 CNAME 레코드 등록을 요청
3. Settings → Pages에서 Custom domain 항목에도 동일한 도메인 입력

## 4. 로컬에서 미리보기 (선택)

Ruby/Jekyll이 설치되어 있다면:

```bash
gem install bundler jekyll
bundle init
echo 'gem "github-pages", group: :jekyll_plugins' >> Gemfile
bundle install
bundle exec jekyll serve
```

설치가 번거롭다면 그냥 GitHub에 push한 뒤 실제 배포된 사이트에서 확인해도 됩니다.

## 폴더 구조

```
emlab-site/
├── _config.yml          # 연구실 이름, 연락처 등 기본 설정
├── _layouts/             # 페이지 틀 (직접 수정할 일 거의 없음)
├── _includes/            # 헤더(드롭다운 메뉴 포함)/푸터
├── _posts/               # 게시판 글 (여기에 새 글 추가)
├── assets/               # css, js, 이미지
├── index.html            # 홈 (Recent News)
├── about.html            # About Us
├── team.html             # Our Team
├── research.html         # Research (논문/특허 포함)
├── news.html             # News 게시판 전체 목록
├── pictures.html         # Pictures 갤러리
└── join.html             # Join Us
```
