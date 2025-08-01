

# エンティティ定義（recruiting_platform）

## User（ユーザー共通）

| フィールド名     | 型         | 説明                     |
|------------------|------------|--------------------------|
| id               | UUID       | 主キー                   |
| email            | String     | ログイン用メールアドレス |
| passwordHash     | String     | ハッシュ化されたパスワード |
| role             | Enum       | `JOB_SEEKER`, `EMPLOYER` |

---

## JobSeeker（求職者）

| フィールド名     | 型         | 説明                     |
|------------------|------------|--------------------------|
| id               | UUID       | 主キー                   |
| userId           | UUID       | Userへの外部キー         |
| name             | String     | 氏名                     |
| bio              | Text       | 自己紹介                 |
| skills           | Text[]     | スキル一覧               |
| desiredLocation  | String     | 希望勤務地               |
| desiredPosition  | String     | 希望職種                 |

---

## Employer（企業）

| フィールド名     | 型         | 説明                     |
|------------------|------------|--------------------------|
| id               | UUID       | 主キー                   |
| userId           | UUID       | Userへの外部キー         |
| companyName      | String     | 会社名                   |
| description      | Text       | 会社・事業の説明         |
| websiteUrl       | String     | 企業のWebサイトURL       |

---

## JobPosting（求人）

| フィールド名     | 型         | 説明                     |
|------------------|------------|--------------------------|
| id               | UUID       | 主キー                   |
| employerId       | UUID       | Employerへの外部キー     |
| title            | String     | 職種タイトル             |
| description      | Text       | 職務内容の詳細           |
| location         | String     | 勤務地                   |
| salary           | String     | 給与条件（表示用）       |
| requiredSkills   | Text[]     | 必須スキル一覧           |
| createdAt        | DateTime   | 投稿日時                 |

---

## Application（応募）

| フィールド名     | 型         | 説明                     |
|------------------|------------|--------------------------|
| id               | UUID       | 主キー                   |
| jobSeekerId      | UUID       | 求職者のID               |
| jobPostingId     | UUID       | 求人ID                   |
| status           | Enum       | `APPLIED`, `REVIEWING`, `REJECTED`, `HIRED` |
| appliedAt        | DateTime   | 応募日時                 |