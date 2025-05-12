---
tags: [ai, personalization, customization]
---

# AI personalization/customization

너도나도 AI를 사용하는 시대. AI는 예전의 인터넷처럼 당연하게 사용하는 도구가 되고 있다고 생각. AI를 현명하게 사용하기 위한 방법은 여러가지 있을 수 있다. 이 글에서는 AI 개인화에 대해 소개해보려고 한다.

## OpenAI ChatGPT

AI 할루시네이션은 chatGPT가 처음 나올 때부터 주의하라고 사람들이 말했었다. 그런데 이제 보이는 chatGPT의 문제점은 항상 사용자 편을 들어준다는 것이다. 그래서 의도적으로 AI에게 다른 관점도 함께 제시하라고 하거나, 주장에 대한 근거나 출처를 대라고 하거나 하는 의도적인 지시가 필요하다. 하지만 그것을 매번 할 수는 없으니 ChatGPT 설정에서 나의 상황에 맞게 관리할 수 있다.
chatGPT의 설정, Personalization에 들어가서 Customize ChatGPT를 눌러보자. chatGPT가 나를 어떻게 부를지, 나는 어떤 사람인지, chatGPT에게 어떤 맥락을 미리 알려줄 지 다 설정할 수 있다. 무료 버전에서도 할 수 있으니 될 수 있으면 해두는 게 좋겠다.

아래는 나의 지시사항 예시다. 각자 본인에게 도움이 되게끔 커스텀했으면 좋겠다. chatGPT 말고도 다른 LLM도 이런 편의 기능을 제공하기를 바란다.

```text
- 너는 쉴틈 없이 나에게 영어를 가르쳐주려고 안달난 집착적인 선생님이야. 시시각각 우리의 대화에서 영어 학습에 유용한 부분이 있다면 언급하고 가르쳐주려고 해.
 - If there is a better way to say something when I say it, please mention it.
 - Suggest even better, more advanced ways to say things, beyond just basic corrections
 - Please briefly explain any difficult grammar, specialized English, cultural context, or idiomatic expressions in a separate answer.
 - Adopt a skeptical, questioning approach.

- 너의 답변을 영어/한국어 동시에 병기해줘.
- 네가 답변하기 전에 네가 나의 말을 어떻게 이해했는지 말해줘.
- 내가 편항된 생각을 가지지 못하도록 다양한 관점의 의견을 제시해줘.
- “추정한 것”과 “검증한 것”을 명확히 구분해서 설명해줘.
- 네가 말한 정보들의 출처를 명시해줘. 출처를 명시할 수 없다면 따로 표시해줘.
```

## VSCode Copilot

Github Copilot을 사용할 때 애로사항으로 새로운 대화를 만들 때마다 나의 개발 컨벤션이나 지침 같은 것을 매번 적어줘야 했다. 그런데 [이 글](https://d2.naver.com/helloworld/6615449)을 읽고 나의 VSCode Copilot에 적용했더니 그 생산성이 매우 높아졌다. 이 글의 가이드를 따라하면 프로젝트 별로 Copilot이 코드를 수정할 때나 커밋 메시지를 작성할 때 컨벤션을 지정할 수 있다[^방법]. 아직 프롬프트를 불러와서 넣어보지는 않았다.

[^방법]: `.vscode/settings.json`에서 세부 설정을 관리하면 프로젝트별로 다른 지침들을 설정할 수 있어 편하다.

## References

- [나만의 Visual Studio Code Copilot 지침 만들고 활용하기](https://d2.naver.com/helloworld/6615449)
- [남규한님의 'LLM의 무서운 점' 링크드인 포스트](https://www.linkedin.com/posts/kyuhannam_llm%EC%9D%98-%EB%AC%B4%EC%84%9C%EC%9A%B4-%EC%A0%90%EC%9D%80-%ED%95%A0%EB%A3%A8%EC%8B%9C%EB%84%A4%EC%9D%B4%EC%85%98%EC%9D%B4-%EC%95%84%EB%8B%99%EB%8B%88%EB%8B%A4-%EC%A4%91%EC%9A%94%ED%95%9C-%EC%9D%98%EC%82%AC%EA%B2%B0%EC%A0%95%EC%9D%B4-%ED%95%84%EC%9A%94%ED%95%A0-%EB%95%8C-activity-7320430909604655105-BS0r)
- [남규한님의 'GPT Instruction' 링크드인 포스트](https://www.linkedin.com/posts/kyuhannam_%EB%82%98%EB%A7%8C%EC%9D%98-%EA%B7%80%EC%97%BD%EA%B3%A0-%EC%8B%9C%ED%81%AC%ED%95%9C-gpt%EB%A5%BC-%EC%9C%84%ED%95%B4-%EC%82%AC%EC%9A%A9%ED%95%9C-%EC%9D%B8%EC%8A%A4%ED%8A%B8%EB%9F%AD%EC%85%98-%EA%B3%B5%EC%9C%A0%ED%95%A9%EB%8B%88%EB%8B%A4-%EC%9D%B4-%EC%9D%B8%EC%8A%A4%ED%8A%B8%EB%9F%AD%EC%85%98%EC%9D%84-activity-7322271524294471680-t7Wj)
