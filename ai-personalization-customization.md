---
tags: [ai, personalization, customization]
date: 2025-04-30
---

# AI personalization/customization

We're in an era where everyone is using AI. I think AI has become a tool that people use as naturally as the internet used to be. There are various ways to use AI wisely. In this post, I'd like to introduce AI personalization.

## OpenAI ChatGPT

People have warned about AI hallucinations since chatGPT was first released. But the problem with chatGPT now is that it always takes the user's side. So we need to deliberately instruct AI to present different perspectives, provide evidence or sources for claims, and give other intentional directions. But since we can't do that every time, we can manage it according to our situation in the ChatGPT settings.
Let's go to ChatGPT settings, Personalization, and click on Customize ChatGPT. You can set how chatGPT will address you, what kind of person you are, and what context you want to provide to chatGPT in advance. Since this can be done in the free version as well, it's best to set it up if possible.

Below is an example of my instructions. I hope everyone customizes them to be helpful for themselves. I also hope other LLMs provide such convenience features besides chatGPT.

```text
- You are an obsessive teacher who is desperately trying to teach me English without a break. You try to mention and teach useful parts for English learning in our conversations at every opportunity.
 - If there is a better way to say something when I say it, please mention it.
 - Suggest even better, more advanced ways to say things, beyond just basic corrections
 - Please briefly explain any difficult grammar, specialized English, cultural context, or idiomatic expressions in a separate answer.
 - Adopt a skeptical, questioning approach.

- Please provide your answers in both English and Korean.
- Before answering, please tell me how you understood my words.
- Please present various perspectives to prevent me from having biased thoughts.
- Clearly distinguish between what is "assumed" and what is "verified."
- Please specify the sources of the information you provided. If you cannot specify a source, please indicate it separately.
```

## VSCode Copilot

When using Github Copilot, one of the difficulties was having to write down my development conventions or guidelines every time I created a new conversation. However, after reading [this article](https://d2.naver.com/helloworld/6615449) and applying it to my VSCode Copilot, my productivity has increased significantly. By following the guide in this article, you can specify conventions for when Copilot modifies code or writes commit messages on a per-project basis[^1]. I haven't tried importing and using prompts yet.

[^1]: By managing detailed settings in `.vscode/settings.json`, you can set different guidelines for each project, which is convenient.

## References

- [나만의 Visual Studio Code Copilot 지침 만들고 활용하기](https://d2.naver.com/helloworld/6615449)
- [남규한님의 'LLM의 무서운 점' 링크드인 포스트](https://www.linkedin.com/posts/kyuhannam_llm%EC%9D%98-%EB%AC%B4%EC%84%9C%EC%9A%B4-%EC%A0%90%EC%9D%80-%ED%95%A0%EB%A3%A8%EC%8B%9C%EB%84%A4%EC%9D%B4%EC%85%98%EC%9D%B4-%EC%95%84%EB%8B%99%EB%8B%88%EB%8B%A4-%EC%A4%91%EC%9A%94%ED%95%9C-%EC%9D%98%EC%82%AC%EA%B2%B0%EC%A0%95%EC%9D%B4-%ED%95%84%EC%9A%94%ED%95%A0-%EB%95%8C-activity-7320430909604655105-BS0r)
- [남규한님의 'GPT Instruction' 링크드인 포스트](https://www.linkedin.com/posts/kyuhannam_%EB%82%98%EB%A7%8C%EC%9D%98-%EA%B7%80%EC%97%BD%EA%B3%A0-%EC%8B%9C%ED%81%AC%ED%95%9C-gpt%EB%A5%BC-%EC%9C%84%ED%95%B4-%EC%82%AC%EC%9A%A9%ED%95%9C-%EC%9D%B8%EC%8A%A4%ED%8A%B8%EB%9F%AD%EC%85%98-%EA%B3%B5%EC%9C%A0%ED%95%A9%EB%8B%88%EB%8B%A4-%EC%9D%B4-%EC%9D%B8%EC%8A%A4%ED%8A%B8%EB%9F%AD%EC%85%98%EC%9D%84-activity-7322271524294471680-t7Wj)
