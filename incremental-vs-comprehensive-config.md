---
tags: [dependabot, incremental, comprehensive]
---

# Dependabot 설정하면서 생각해본 두 가지 개발 접근법

오픈소스 프로젝트에서 이미 Dependabot이 설정되어 있는 모습만 구경하다가 직접 참여하고 있는 오픈 소스 프로젝트에서 dependabot[^1]을 처음부터 도입할 일이 생겼다. “한 번에 완벽하게 끝내보자!”는 마음으로 방대한 PR을 올렸지만, 그 과정에서 오히려 두 가지 상반된 개발 접근법을 또렷이 인식하게 됐다. 이 글은 그 깨달음을 기록해 두려는 회고다.

## 수 많은 옵션들, 처음부터 다 고려하면 좋지 않나?

처음 올린 [dependabot 설정 PR](https://github.com/DaleStudy/daleui/commit/dedb235c2cb9128ab3ca0b4633bb4c0215295c29)은 과할 정도로 방대했다.

### dependabot.yml 핵심 설정 요약

- **업데이트 대상**

  - npm 패키지 (루트 디렉토리)
  - GitHub Actions 워크플로우 (`/.github/workflows`)

- **업데이트 주기**

  - npm: 매주(`weekly`)
  - GitHub Actions: 매월(`monthly`)

- **공통 설정**

  - PR 자동 라벨: `dependencies`
  - 동시에 열 수 있는 PR 수: 10개
  - 리뷰어 자동 지정: `DaleStudy/daleui`

- **패키지 그룹 설정**

  - `storybook`: `@storybook*`, `chromatic` 등
  - `react`: `react`, `react-dom`, `@types/react*`
  - `testing`: `@testing-library*`, `vitest`, `happy-dom`
  - `eslint`: `eslint*`, `@eslint*`, `typescript-eslint`
  - `typescript`: `typescript`, `@types/*`
  - `vite`: `vite`, `@vitejs/*`, `vite-plugin-*`
  - `ui-components`: `@radix-ui/*`, `lucide-react`
  - `css`: `@pandacss/*`
  - 모두 `minor`, `patch` 업데이트만 허용

- **GitHub Actions 추가 라벨**
  - `github-actions`

이것저것 고려했다. LLM을 통해 현재 프로젝트 의존성을 고려한 Dependabot 초안을 생성했다. 그리고 설정을 검토하고 이 정도면 됐겠다, 싶어 변경사항을 PR로 만들었다.

하지만 메인테이너의 [한마디](https://github.com/DaleStudy/daleui/pull/88#discussion_r2011058936)가 모든 걸 뒤집었다.

> "우리 기본값을 써보고 나중에 필요할 때 설정해도 늦지 않을까요? Convention over configuration! 😉"

이 피드백을 듣고 설정 파일을 아래와 같이 [변경](https://github.com/DaleStudy/daleui/compare/dedb235c2cb9128ab3ca0b4633bb4c0215295c29..a7cc22b47481d63bbacce1ec59a3030d398843f5)했다.

```yaml
version: 2
updates:
  - package-ecosystem: "npm"
    directory: "/"
    schedule:
      interval: "daily"

  - package-ecosystem: "github-actions"
    directory: "/.github/workflows"
    schedule:
      interval: "daily"
```

그리고 실제로 우리는 dependabot 설정 파일을 [지속적으로 변경했다](https://github.com/DaleStudy/daleui/commits/main/.github/dependabot.yml). 이 변경을 지켜보며 나는 아래 주제를 떠올렸다.

## 최소 설정으로 시작해 점진적으로 확장하기 vs. 처음부터 잘 설계하기

### 최소 설정으로 시작해 점진적으로 확장하기

- **장점**

  - PR 규모가 작아 리뷰·머지가 빠르다.
  - 실제 사용하는 옵션만 추가하니 ‘죽은 설정’이 적다.

- **단점**

  - 설정 공백 기간 동안 예상치 못한 불편·리스크가 생길 수 있다.
  - 커스터마이징 PR이 잦아져 커뮤니케이션 총량이 늘 수 있다.

### 처음부터 잘 설계하기

- **장점**

  - 한 번에 배포해도 큰 구조 변경이 드물다.
  - 중·장기적으로는 리뷰/회의 비용이 줄 수 있다.

- **단점**

  - 초기 합의·리뷰 시간이 길어져 ‘시작 속도’가 느려진다.
  - 과설계된 옵션이 레거시가 될 위험이 있다.

## 결국, 어떤 선택이 옳을까?

**정답은 없다.** 상황과 팀 성숙도에 따라 두 전략의 무게추가 달라진다.
- **최소 설정으로 시작해 점진적으로 확장하기**은 *불확실성이 큰 초기 단계*에서 유연성을 준다.
- **처음부터 잘 설계하기**는 *안정성이 중요한 성숙 단계*에서 유지·보수 비용을 낮춘다.

결국 “지금 우리 팀에 맞는 최소 결정”을 내리고, 주기적으로 **실제 데이터**(PR 알림 빈도·머지 지연 시간 등)로 전략을 재검증하는 게 중요하지 않을까 생각한다.

[^1]: Dependabot is a GitHub-integrated bot that automatically scans your repository’s dependency files (e.g., package.json, pom.xml, Gemfile) and raises pull requests (PRs) to keep those dependencies up to date and patch known vulnerabilities.
