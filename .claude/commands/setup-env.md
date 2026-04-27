# 환경 변수 설정 가이드

프로젝트의 환경 변수를 단계별로 설정합니다.

## 1단계: .env 파일 확인

프로젝트 루트에 `.env.example` 파일이 있는지 확인하고, 없으면 아래 명령어로 복사합니다.

```bash
# .env.example이 있는 경우
cp .env.example .env

# 없는 경우 직접 생성
touch .env
```

## 2단계: 필수 환경 변수 목록

아래 환경 변수들을 `.env` 파일에 설정하세요.

### 앱 기본 설정
```env
NODE_ENV=development          # 실행 환경 (development | staging | production)
PORT=3000                     # 서버 포트
APP_URL=http://localhost:3000  # 앱 기본 URL
```

### 데이터베이스
```env
DATABASE_URL=postgresql://user:password@localhost:5432/mydb
DB_HOST=localhost
DB_PORT=5432
DB_NAME=mydb
DB_USER=user
DB_PASSWORD=password
```

### 인증 / 보안
```env
JWT_SECRET=your-super-secret-key-change-this   # 최소 32자 이상 권장
JWT_EXPIRES_IN=7d
SESSION_SECRET=your-session-secret
```

### 외부 서비스 (선택)
```env
# AWS
AWS_ACCESS_KEY_ID=
AWS_SECRET_ACCESS_KEY=
AWS_REGION=ap-northeast-2
AWS_S3_BUCKET=

# 이메일 (SMTP)
SMTP_HOST=smtp.gmail.com
SMTP_PORT=587
SMTP_USER=
SMTP_PASS=

# OAuth
GOOGLE_CLIENT_ID=
GOOGLE_CLIENT_SECRET=
```

## 3단계: 현재 설정 상태 점검

아래 내용을 확인하여 현재 프로젝트의 환경 변수 설정 상태를 점검해드리겠습니다.

$ARGUMENTS

현재 프로젝트에서 환경 변수 관련 파일을 확인합니다:

- `.env` 파일 존재 여부
- `.env.example` 파일 존재 여부
- `package.json`의 스크립트에서 참조하는 환경 변수
- 코드 내 `process.env` 사용 현황

## 4단계: 보안 주의사항

> **중요**: 아래 사항을 반드시 지켜주세요.

- `.env` 파일은 절대 Git에 커밋하지 마세요
- `.gitignore`에 `.env`가 포함되어 있는지 확인하세요
- 민감한 값(비밀번호, API 키)은 팀원과 직접 공유하거나 비밀 관리 도구(1Password, AWS Secrets Manager 등)를 사용하세요
- `.env.example`에는 실제 값 대신 placeholder만 기입하세요

```bash
# .gitignore 확인
grep -n "\.env" .gitignore

# 만약 없다면 추가
echo ".env" >> .gitignore
echo ".env.local" >> .gitignore
```

## 5단계: 설정 검증

```bash
# 환경 변수가 제대로 로드되는지 확인 (Node.js 기준)
node -e "require('dotenv').config(); console.log('NODE_ENV:', process.env.NODE_ENV)"

# 앱 실행하여 최종 확인
npm run dev
```

---

추가로 설정이 필요한 환경 변수가 있거나, 특정 서비스 연동 방법이 궁금하면 알려주세요.
