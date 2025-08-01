

# API仕様書（recruiting_platform）

## 認証系エンドポイント

### POST /auth/register
- 概要: ユーザー登録（求職者・企業共通）
- リクエストボディ:
  ```json
  {
    "email": "user@example.com",
    "password": "password123",
    "role": "JOB_SEEKER" // または "EMPLOYER"
  }
  ```
- レスポンス: 201 Created

---

### POST /auth/login
- 概要: ログイン（JWTトークンを取得）
- リクエストボディ:
  ```json
  {
    "email": "user@example.com",
    "password": "password123"
  }
  ```
- レスポンス:
  ```json
  {
    "token": "JWT_TOKEN_HERE"
  }
  ```

---

## 求職者関連エンドポイント

### GET /jobseekers/me
- 概要: ログイン中の求職者プロフィールを取得
- 認証: 必須（JWT）

---

### PUT /jobseekers/me
- 概要: プロフィール更新
- 認証: 必須（JWT）
- リクエストボディ:
  ```json
  {
    "name": "山田太郎",
    "bio": "エンジニア歴5年...",
    "skills": ["Java", "Spring Boot"],
    "desiredLocation": "東京",
    "desiredPosition": "バックエンドエンジニア"
  }
  ```

---

## 求人関連エンドポイント

### GET /jobpostings
- 概要: 公開求人の一覧を取得（フィルタ対応予定）

---

### GET /jobpostings/{id}
- 概要: 求人詳細の取得

---

### POST /jobpostings
- 概要: 求人の新規作成（企業ユーザー）
- 認証: 必須（JWT）
- リクエストボディ:
  ```json
  {
    "title": "Webエンジニア",
    "description": "Webアプリ開発に関わる業務...",
    "location": "フルリモート",
    "salary": "年収500〜700万円",
    "requiredSkills": ["Java", "React"]
  }
  ```

---

## 応募関連エンドポイント

### POST /applications/{jobPostingId}
- 概要: 求職者が求人に応募する
- 認証: 必須（JWT）

---

### GET /applications/my
- 概要: ログイン中の求職者の応募一覧を取得

---

### GET /applications/received
- 概要: 企業が受け取った応募一覧を取得（求人ごとに集約）
- 認証: 必須（JWT）