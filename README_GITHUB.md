# 주택 매도/매수 자금 계산기

GitHub Pages + Firebase Authentication + Cloud Firestore 기반 웹 저장 버전입니다.

## 기능

- 브라우저에서 주택 매도/매수 자금 계산
- Google 로그인
- 로그인 사용자별 웹 저장
- 다른 PC/휴대폰에서도 같은 Google 계정으로 저장 데이터 불러오기
- 로그인 전에는 기존처럼 브라우저 LocalStorage에 저장

## 1. Firebase 프로젝트 생성

1. Firebase Console에서 프로젝트를 생성합니다.
2. Authentication > Sign-in method에서 Google provider를 활성화합니다.
3. Firestore Database를 생성합니다.
4. Firestore Rules에 `firestore.rules` 내용을 반영합니다.
5. Project settings > Your apps에서 Web app을 추가하고 Firebase config 값을 복사합니다.

## 2. index.html에 Firebase config 입력

`index.html`에서 아래 부분을 찾아 실제 값으로 교체합니다.

```js
window.firebaseConfigForHouseCalculator = {
  apiKey: "YOUR_FIREBASE_API_KEY",
  authDomain: "YOUR_PROJECT_ID.firebaseapp.com",
  projectId: "YOUR_PROJECT_ID",
  storageBucket: "YOUR_PROJECT_ID.firebasestorage.app",
  messagingSenderId: "YOUR_MESSAGING_SENDER_ID",
  appId: "YOUR_APP_ID"
};
```

## 3. GitHub Pages 배포

1. GitHub에 새 repository를 만듭니다.
2. 이 폴더의 파일을 업로드합니다.
3. Repository > Settings > Pages로 이동합니다.
4. Source를 `Deploy from a branch`로 선택합니다.
5. Branch를 `main`, folder를 `/root`로 선택합니다.
6. 표시되는 GitHub Pages URL로 접속합니다.

## 4. Firebase Auth Authorized domains 추가

Firebase Console > Authentication > Settings > Authorized domains에 GitHub Pages 도메인을 추가합니다.

예:
- `사용자명.github.io`
- 커스텀 도메인을 쓰면 해당 도메인도 추가

## 저장 구조

Firestore 경로:

```text
users/{uid}/houseMoveScenarios/{scenarioId}
```

사용자는 본인의 UID 하위 데이터만 읽고 쓸 수 있도록 보안 규칙을 구성했습니다.
