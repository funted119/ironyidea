# 아이러니아이디어 배포 안내

이 폴더를 그대로 올리면 사이트가 뜹니다. 순서대로 따라 하시면 됩니다.

## 준비된 파일
| 파일 | 설명 |
|---|---|
| `index.html` | 사이트 전체 (사진·폰트 모두 내장) |
| `og-image.png` | 카카오톡·페이스북 공유 시 뜨는 썸네일 |
| `favicon.svg` | 브라우저 탭 아이콘 |
| `robots.txt` | 검색엔진 수집 허용 |
| `vercel.json` | 캐시 설정 (수정본이 바로 반영되게) |
| `.gitignore` | GitHub에 올릴 때 불필요 파일 제외 |

---

## 1단계 — 문의 메일 받기 (약 3분)

이미 쓰는 메일 주소가 있어도, 그 주소로 문의를 배달해 줄 중계 서비스가 하나 필요합니다.
HTML 파일은 혼자서 메일을 보낼 수 없기 때문입니다.
아래 방법은 **가입도 비밀번호도 없이** 이메일 입력만으로 끝납니다.

1. https://web3forms.com 접속
2. 첫 화면 입력칸에 **info@ironycombined.com** 입력 → **Create Access Key**
3. 그 주소로 도착한 메일에서 **액세스 키**를 복사
   (형태: `a1b2c3d4-e5f6-7890-abcd-ef1234567890`)
4. `index.html` 을 메모장이나 VS Code로 열고 `Ctrl+F` 로 `WEB3FORMS_KEY` 검색
5. 아래 한 줄을 찾아 따옴표 안에 키를 붙여넣고 저장

```js
const WEB3FORMS_KEY='';
↓
const WEB3FORMS_KEY='a1b2c3d4-e5f6-7890-abcd-ef1234567890';
```

이걸로 끝입니다. 문의가 오면 `[아이러니아이디어] 제작 문의 IC-260826-1234` 제목으로
info@ironycombined.com 받은편지함에 들어옵니다.

- 무료 월 250건, 스팸 차단과 hCaptcha 포함, 30일 보관
- 액세스 키는 공개되어도 안전합니다. 메일 주소의 별칭일 뿐이라 키만으로는
  다른 곳으로 메일을 보낼 수 없습니다

### 다른 서비스를 쓰고 싶다면
Formspree(월 50건 무료, 가입 필요)를 쓰려면 `FORM_ENDPOINT` 줄에
`https://formspree.io/f/xxxxxxxx` 주소를 넣으면 됩니다. 둘 중 하나만 채우면 됩니다.

---

## 2단계 — Vercel에 올리기

두 가지 방법 중 편한 쪽을 고르시면 됩니다.

### 방법 A. GitHub 연결 (추천 — 이후 수정이 편합니다)

1. https://github.com/new 에서 저장소 생성
   - 이름: `ironyidea` / **Public** 또는 Private 아무거나
   - README 체크는 해제
2. 생성된 화면에서 **uploading an existing file** 클릭
3. 이 폴더의 파일 6개를 끌어다 놓고 **Commit changes**
4. https://vercel.com 접속 → **Continue with GitHub** 으로 로그인
5. **Add New → Project** → 방금 만든 저장소 옆 **Import**
6. 설정은 손대지 않고 그대로 **Deploy** (Framework Preset은 Other로 자동 인식)
7. 1분 내 `https://ironyidea.vercel.app` 형태의 주소가 생성됩니다

이후에는 GitHub에서 `index.html` 을 수정하고 커밋하면 사이트가 자동으로 갱신됩니다.

### 방법 B. 명령어로 바로 올리기 (GitHub 없이)

컴퓨터에 Node.js가 설치돼 있어야 합니다.

```bash
cd 이_폴더_경로
npx vercel
```

- 처음 실행하면 로그인 안내가 나옵니다 (브라우저에서 승인)
- 질문은 모두 엔터로 넘기면 됩니다
- 실제 배포는 `npx vercel --prod`

---

## 3단계 — 구입한 도메인 연결

1. Vercel 프로젝트 → **Settings** → **Domains**
2. 구입한 도메인 입력 (예: `ironyidea.kr`) → **Add**
3. Vercel이 아래 둘 중 하나를 안내합니다

   **네임서버 방식 (권장)**
   도메인 구입처(가비아 등) → 네임서버 설정 →
   Vercel이 알려주는 `ns1.vercel-dns.com`, `ns2.vercel-dns.com` 입력

   **DNS 레코드 방식**
   구입처 DNS 관리에서
   - A 레코드: `@` → `76.76.21.21`
   - CNAME: `www` → `cname.vercel-dns.com`

4. 반영까지 보통 10분~24시간. HTTPS 인증서는 Vercel이 자동 발급합니다
5. 연결 후 Web3Forms 대시보드에서 Website URL을 실제 도메인으로 바꿔 두면 좋습니다

> 위 IP와 주소는 Vercel이 화면에 직접 알려주는 값을 그대로 쓰는 게 가장 정확합니다.

---

## 수정이 필요할 때

`index.html` 을 텍스트 편집기로 열면 됩니다.

- **품목 추가·수정**: `const items=[` 부분. 각 품목은 이름·설명·사양·사진으로 구성
- **사진 교체**: `thumb:IMG.xxx` 형태. 사진은 파일 안에 base64로 들어 있음
- **문구 수정**: 해당 한글 문장을 그대로 검색해서 고치면 됨
- **회사 정보**: 파일 하단 `<footer>` 부분

---

## 배포 전 확인할 것

- [ ] 문의 폼 실제 테스트 (배포 후 직접 한 번 보내 보고 메일 도착 확인)
- [ ] 하단 전화번호 — 현재 비어 있음, 필요 시 추가
- [ ] 사업자등록번호 217-24-22613 / 대표 김현창 / 주소 확인
- [ ] 통신판매업 신고번호 — 필요 시 추가
