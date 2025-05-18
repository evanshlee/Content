---
tags: [dependabot, incremental, comprehensive]
date: 2025-05-08
---

# Dependabot 설정 중 고민했던 두 가지 개발 접근 방식

그동안 오픈소스 프로젝트에서 이미 설정된 Dependabot만 관찰해왔는데, 직접 참여하고 있는 오픈소스 프로젝트에서 Dependabot을 처음부터 설정해야 하는 상황이 생겼다.
"한 번에 완벽하게 끝내자!"는 마음가짐으로 거대한 PR을 제출했지만, 그 과정을 통해 두 가지 상반된 개발 접근 방식의 차이를 뚜렷하게 인식하게 되었다.
이 글은 그 통찰을 기록하고자 하는 회고다.

## 수많은 선택지들, 처음부터 다 고려하는 게 낫지 않을까?

내가 처음 제출한 [dependabot 설정 PR](https://github.com/DaleStudy/daleui/commit/dedb235c2cb9128ab3ca0b4633bb4c0215295c29)은 지나치게 포괄적이었다.

### 주요 dependabot.yml 설정 요약

- **업데이트 대상**

  - npm 패키지 (루트 디렉토리)
  - GitHub Actions 워크플로우 (`/.github/workflows`)

- **업데이트 주기**

  - npm: 매주
  - GitHub Actions: 매월

- **공통 설정**

  - 자동 PR 라벨: `dependencies`
  - 동시에 열 수 있는 최대 PR 수: 10
  - 자동 리뷰어 지정: `DaleStudy/daleui`

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

- **추가 GitHub Actions 라벨**
  - `github-actions`

프로젝트의 현재 의존성들을 고려하여 LLM을 이용해 Dependabot 설정 초안을 만들고, 이를 검토한 후 충분하다고 판단해 PR을 생성했다.

하지만 프로젝트의 리더의 [한 마디](https://github.com/DaleStudy/daleui/pull/88#discussion_r2011058936)가 모든 것을 뒤바꿨다.

> "우리 기본값을 써보고 나중에 필요할 때 설정해도 늦지 않을까요? Convention over configuration! 😉"

이 피드백을 받고 나서, 설정 파일을 [다음과 같이 변경](https://github.com/DaleStudy/daleui/compare/dedb235c2cb9128ab3ca0b4633bb4c0215295c29..a7cc22b47481d63bbacce1ec59a3030d398843f5)했다:

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

실제로는 이후에도 [지속적으로 설정을 수정](https://github.com/DaleStudy/daleui/commits/main/.github/dependabot.yml)해 나갔다.
그 과정을 보면서 다음과 같은 주제를 고민하게 되었다.

## 처음부터 잘 설계해서 넣을까? vs 최소 설정으로 시작해서 점진적으로 확장할까?

### 최소 설정으로 시작하고 점진적으로 확장하는 방식

- **장점**

  - PR 크기가 작아 리뷰 및 병합 속도가 빠르다.
  - 실제 사용하는 옵션만 추가하게 되어 '죽은 설정(dead setting)'이 적다.

- **단점**

  - 설정 공백기에 예기치 않은 불편이나 위험이 발생할 수 있다.
  - 커스터마이징 PR이 자주 생겨 커뮤니케이션 비용이 늘어날 수 있다.

### 처음부터 잘 설계해서 넣는 방식

- **장점**

  - 한 번에 배포해도 구조적 변경은 드물어진다.
  - 중장기적으로 리뷰/회의 비용을 줄일 수 있다.

- **단점**

  - 초기 합의 및 리뷰 시간이 늘어나 시작 속도가 느려진다.
  - 과하게 설계된 설정이 나중에 레거시가 될 위험이 있다.

## 결국 어떤 선택이 정답일까?

**정답은 없다고 생각한다.** 두 전략 사이의 균형은 상황과 팀의 성숙도에 따라 달라진다.

- **불확실성이 큰 초기 단계**에는 유연성을 제공하는 점진적 확장 방식이 유리하고,
- **안정성이 중요한 성숙 단계**에서는 초기 설계에 집중하는 방식이 유지비용을 줄여준다고 생각.

결국 중요한 건 **지금 우리 팀에 맞는 최소한의 결정**을 내리고, 실제 데이터를 기반으로 주기적으로 전략을 재검토하는 것이지 않을까?
