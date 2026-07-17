# modern-llm-study

[walkinglabs/modern-llm-notebook](https://github.com/walkinglabs/modern-llm-notebook)을 학습하고 정리한 기록을 남긴다. 학습의 목표는 LLM의 동작 원리를 다른 사람에게 설명할 수 있을 정도로 이해도를 높이는 것이다.
각 노트북을 먼저 따라하며 이해도를 높인 후, 이해한 내용을 나의 언어로 정리하는 note를 추가한다. 추가적인 튜닝이나 실험은 experiment로 따로 정리한다. 추후 블로그로 남길 만한 주제가 있다면 초안을 작성하여 post로 남길 예정. 

## 구조

- `notebooks/` — modern-llm-notebook에서 가져온 원본 학습 노트북
- `notes/` — 각 노트북을 학습한 뒤 남기는 정리 노트
- `experiments/` — 각 노트북을 바탕으로 해보고 싶은 실험
- `posts/` — 블로그로 남길만한 주제의 초안

`notes/`와 `experiments/`는 `notebooks/`의 원본 주피터 노트북과 같은 파트 구조를 따른다.

## 학습 원칙

1. **따라만 치지 않는다.** [walkinglabs/modern-llm-notebook](https://github.com/walkinglabs/modern-llm-notebook)와 같은 학습 레포는 개인적으로 양날의 검이라고 생각한다. 잘 정리된 주피터 노트북은 '딸깍'을 반복함으로써, 해당 내용을 전부 이해했다는 착각을 종종 일으킨다. 
2. **파인만 공부법을 적극 활용한다.** 코드 없이 개념을 설명할 수 없으면 이해한 게 아니다. (심지어 원본 레퍼런스는 내가 작성한 코드도 아니다.) '이 내용을 초등학생에게 설명할 수 있을까?'를 자문해봤을 때, 답이 NO라면 이해도를 다시 높이는 방식으로 반복한다. 
3. **직접 타이핑한다.** 원본 주피터 노트북의 뒷 부분에는 homework 형식의 코드가 제공된다. 직접 코드를 짜는게 가장 좋겠지만, 최소한 해당 homework는 모두 작성하는 것을 목표로 한다. 추가적인 궁금증이 생기거나 실험이 필요하다면 반드시 진행한 후 다음 내용으로 넘어가자. 추후에 실험해보고 싶은 내용이 생각난다면 소급 적용을 꼭 하도록 하자.
4. **흥미진진한 주제가 있다면 블로그로.** 기술 블로그를 작성하다 수없이 실패했기에 이 4번 원칙이 가장 어려울 것 같다. 글을 쓴다는게 에너지를 엄청나게 소모한다는 것을 이제는 깨달았다... 그래도 다시 해보자. 안하는 것보단 낫잖아.. 

예시:

- `notebooks/part1-foundation/01-tokenizer-basics.ipynb`
- `notes/part1-foundation/01-tokenizer-basics.md`
- `experiments/part1-foundation/01-tokenizer-basics.md`
