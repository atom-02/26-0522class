# 🔥 Firebase 설정 안내 (5분 완성)

## 왜 Firebase가 필요한가요?
아이패드(학생)와 전자칠판(교사)이 **다른 기기**이기 때문에,
데이터를 실시간으로 주고받으려면 중간에 서버가 필요합니다.
Google Firebase는 **무료**로 사용 가능하고, 설정이 쉽습니다.

---

## Step 1. Firebase 프로젝트 만들기

1. 크롬북에서 [https://console.firebase.google.com](https://console.firebase.google.com) 접속
2. 구글 계정으로 로그인
3. **"프로젝트 추가"** 클릭
4. 프로젝트 이름 입력 (예: `my-math-class`)
5. Google Analytics → **"지금은 사용 안 함"** 선택 → **"프로젝트 만들기"**

---

## Step 2. Realtime Database 활성화

1. 왼쪽 메뉴 → **"빌드"** → **"Realtime Database"**
2. **"데이터베이스 만들기"** 클릭
3. 위치: **미국(기본값)** 선택
4. 보안 규칙: **"테스트 모드에서 시작"** 선택 (수업용이므로 OK)
5. **"사용 설정"** 클릭

> ⚠️ 테스트 모드는 30일 후 만료됩니다.
> 수업 후 연장하거나, 아래 규칙으로 교체하세요:
> ```json
> {
>   "rules": {
>     "class": {
>       ".read": true,
>       ".write": true
>     }
>   }
> }
> ```

---

## Step 3. API 키 확인하기

1. 왼쪽 상단 ⚙️ **"프로젝트 설정"** 클릭
2. **"일반"** 탭 → 아래로 스크롤
3. **"앱 추가"** → **웹(</> 아이콘)** 선택
4. 앱 닉네임 입력 (예: `class-app`) → **"앱 등록"**
5. 표시되는 코드에서 두 가지를 복사:

```
apiKey: "AIzaSyXXXXXXXXXXXXXXXXXXXXXXXXX"  ← 이것
projectId: "my-math-class-xxxxx"              ← 이것
```

---

## Step 4. 앱에 입력하기

### 학생 아이패드 (student_app.html)
1. 파일 열기 → **"학생 입장"** 탭
2. Firebase 설정 화면에서:
   - **프로젝트 ID**: `my-math-class-xxxxx`
   - **API Key**: `AIzaSyXXXXX...`
3. **"저장하고 계속"** 탭

### 전자칠판 (board.html)
1. 파일 열기 (자동으로 설정 화면 표시)
2. 동일한 값 입력
3. **"연결하고 수업 시작"** 클릭

> 💡 **한 번 입력하면 브라우저에 저장됩니다.**
> 다음 수업에는 바로 연결돼요!

---

## 파일 배포 방법 (학생 아이패드)

### 방법 A: 에어드롭 (가장 빠름)
1. `student_app.html` 파일을 에어드롭으로 아이패드에 전송
2. Safari로 열기

### 방법 B: 구글 드라이브
1. 구글 드라이브에 `student_app.html` 업로드
2. 공유 링크 생성
3. QR코드 생성 → 칠판에 띄워서 학생이 스캔

### 방법 C: 크롬북 로컬 서버 (고급)
크롬북에서 VS Code Live Server 또는 Python 서버 실행 후
같은 Wi-Fi 네트워크의 아이패드에서 IP 주소로 접속

---

## 자주 묻는 질문

**Q. 인터넷이 없으면?**
A. student_app.html은 인터넷 없이도 작동합니다 (로컬 저장).
단, Firebase 연동 및 전자칠판 표시는 인터넷이 필요합니다.

**Q. 무료인가요?**
A. Firebase Realtime Database 무료 한도:
- 동시 연결: 100개 (충분)
- 저장 용량: 1GB (충분)
- 다운로드: 10GB/월 (충분)
수업 용도로는 완전 무료입니다.

**Q. 데이터가 저장되나요?**
A. Firebase에 저장되므로 수업 후에도 볼 수 있습니다.
Firebase Console → Realtime Database → 데이터 탭에서 확인 가능.

---

## 파일 구성 요약

| 파일 | 용도 | 사용 기기 |
|------|------|---------|
| `student_app.html` | 학생 수업 앱 | 모둠별 아이패드 |
| `board.html` | 전자칠판 대시보드 | 전자칠판(크롬북) |

두 파일에 **동일한 Firebase 정보**를 입력하면 연동 완료!
