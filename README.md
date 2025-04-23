# project-flow-add-issue-to-project

## 개요

이 액션은 이슈가 생성되었을 때 지정된 GitHub Project에 자동으로 등록하고, Status 필드를 사용자가 지정한 초기 컬럼으로 설정합니다.

---

## ✨ 주요 기능

- 생성된 이슈를 지정된 GitHub Project에 자동으로 추가합니다.
- 이슈의 Status 필드를 `Todo`, `In Progress` 등 특정 컬럼으로 설정할 수 있습니다.
- 사용자 소유(User-owned)와 조직 소유(Organization-owned) 프로젝트 모두 지원합니다.

---

## 🧾 입력값

| 이름             | 필수 여부 | 기본값 | 설명                                                             |
| ---------------- | --------- | ------ | ---------------------------------------------------------------- |
| `github_token`   | 예        | –      | `project` 권한이 포함된 GitHub Token (예: PAT 또는 GITHUB_TOKEN) |
| `project_owner`  | 예        | –      | 프로젝트를 소유한 사용자 또는 조직의 이름                        |
| `project_number` | 예        | –      | 프로젝트 번호 (ID가 아님)                                        |
| `target_column`  | 아니오    | `Todo` | 초기로 설정할 상태(Status) 컬럼 이름                             |

---

## ⚠️ 제약 사항 및 주의사항

- `github_token` project 접근 권한이 필요합니다.
- `target_column` 이름이 정확하지 않으면 Status 설정이 생략될 수 있습니다.

---

## 🔁 사용 예시

```yaml
on:
  issues:
    types: [opened]

jobs:
  add-issue-to-project:
    runs-on: ubuntu-latest
    steps:
      - uses: jinhokim98/project-flow-add-issue-to-project@v1
        with:
          github_token: ${{ secrets.PERSONAL_TOKEN }}
          project_owner: your-org
          project_number: 42
          target_column: 'Todo'
```

## Overview

This GitHub Action automatically adds a newly created issue to a specified GitHub Project and sets the issue's `Status` field to a designated column.

---

## ✨ Features

- Automatically adds newly opened issues to the specified GitHub Project.
- Sets the issue’s `Status` field to a target column (e.g., `Todo`, `In Progress`).
- Supports both **user-owned** and **organization-owned** projects.

---

## 🧾 Inputs

| Name             | Required | Default | Description                                                        |
| ---------------- | -------- | ------- | ------------------------------------------------------------------ |
| `github_token`   | Yes      | –       | GitHub token with `project` access (e.g., a PAT or `GITHUB_TOKEN`) |
| `project_owner`  | Yes      | –       | The user or organization name that owns the project                |
| `project_number` | Yes      | –       | The number of the project (not the ID)                             |
| `target_column`  | No       | `Todo`  | The column name to be set as the initial `Status` of the issue     |

---

## ⚠️ Limitations & Notes

- The provided `github_token` must have access to **Projects (beta)**.
- If `target_column` does not exactly match an existing option, the status field may not be set.
- **GitHub Projects (classic) are not supported.** This Action is compatible **only** with [Projects (beta)](https://github.com/features/issues).

---

## 🔁 Usage Example

```yaml
on:
  issues:
    types: [opened]

jobs:
  add-issue-to-project:
    runs-on: ubuntu-latest
    steps:
      - uses: jinhokim98/project-flow-add-issue-to-project@v1
        with:
          github_token: ${{ secrets.PERSONAL_TOKEN }}
          project_owner: your-org
          project_number: 42
          target_column: 'Todo'
```
