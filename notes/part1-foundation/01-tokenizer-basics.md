# 01 - Tokenizer Basics

원본: [notebooks/part1-foundation/01-tokenizer-basics.ipynb](../../notebooks/part1-foundation/01-tokenizer-basics.ipynb)

## 요약

텍스트를 모델이 이해할 수 있도록 숫자로 바꾸는 것이 tokenizer의 역할이다. 텍스트를 분할하는 단위를 Character/Word/Subword 중 뭘로 하느냐가 어휘 크기, 시퀀스 길이, Out of Vocabulary의 빈도를 결정한다.

## 내가 이해한 내용

텍스트를 숫자(Token IDs)로 변경할 때, Character 단위로 자르면 어휘는 수십 개면 끝나고 Out of Vocabulary(이하 OOV)도 사실상 없지만, 시퀀스가 너무 길어진다. 길어진 시퀀스는 곧 비용 증가를 의미한다. 게다가 "cat"을 c,a,t로 쪼개놓으면 이 셋이 붙어 다닐 때만 "고양이"라는 뜻이 된다는 걸 모델이 처음부터 배워야 한다.

Word 단위로 자르면 반대의 상황이 펼쳐진다. 시퀀스는 짧게 유지할 수 있지만 어휘의 수가 너무 많이 증가한다. `cat`과 `cats`를 별개로 넣어야 하고, 오타나 신조어를 마주하면 에러가 발생한다. 

Subword는 이 둘의 절충안이다. 자주 나오는 단어는 통째로 하나의 토큰으로, 드물게 나오는 단어는 아는 단어(Vocabulary)의 조각들로 쪼갠다. `unbelievable`을 `un`, `believ`, `able`으로 쪼개는 식이다. OOV를 "쪼개면 아는 단어의 합"으로 우회한다는 게 핵심이다.
BPE(Byte Pair Encoding)는 가장 보편적으로 사용되는 Subword 알고리즘이다. 처음엔 문자 단위에서 시작해서, 가장 자주 붙어 나오는 인접 쌍을 하나로 병합하는 걸 반복한다. 그러면 `t`+`h` → `th`, `th`+`e` → `the` 같은 식으로 자주 쓰이는 어휘가 정립된다.

## 연습 문제 관련
- `<BOS>`, `<EOS>` 같은 특수 토큰은 문장 경계를 알리는 마커 역할을 한다. 모델에서는 당연히 이런 토큰들을 처리할 방법이 필요할 것.
- 배치 처리를 위해 padding을 사용한다. 아마도 tensor의 모양을 같게 해야 다루기 쉽기 때문이 아닐까 싶다.
- attention mask는 패딩을 구분하는 용도이다. 값의 경우 1, 패딩의 경우 0처럼 마스킹을 하여 1에만 신경쓸 수 있도록.
