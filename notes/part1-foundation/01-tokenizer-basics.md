# 01 - Tokenizer Basics

원본: [notebooks/part1-foundation/01-tokenizer-basics.ipynb](../../../notebooks/part1-foundation/01-tokenizer-basics.ipynb)

## 요약

문자열을 정수 시퀀스로 바꿔주는 게 tokenizer. 자르는 단위를 Character/Word/Subword 중 뭘로 하느냐가 어휘 크기, 시퀀스 길이, OOV 빈도를 결정한다. 현대 LLM이 서브워드(BPE 계열)로 수렴한 이유가 여기서 나온다.

## 내가 이해한 것

텍스트를 숫자(Token IDs)로 변경할 때, Character 단위로 자르면 어휘는 수십 개면 끝나고 Out of Vocabulary(이하 OOV)도 사실상 없지만, 시퀀스가 너무 길어진다. attention이 O(n²)라 이게 그대로 비용이 된다. 게다가 "cat"을 c,a,t로 쪼개놓으면 이 셋이 붙어 다닐 때만 "고양이"라는 뜻이 된다는 걸 모델이 처음부터 배워야 한다.

Word 단위로 자르면 반대의 상황이 펼쳐진다. 시퀀스는 짧게 유지할 수 있지만 어휘의 수가 너무 많이 증가한다. `cat`과 `cats`를 별개로 넣어야 하고, 오타나 신조어를 마주하면 에러가 발생한다. 

Subword는 이 둘의 절충안이다. 자주 나오는 단어는 통째로 하나의 토큰으로, 드물게 나오는 단어는 아는 단어(Vocabulary)의 조각들로 쪼갠다. `unbelievable`을 `un`, `believ`, `able`으로 쪼개는 식이다. OOV를 "쪼개면 아는 단어의 합"으로 우회한다는 게 핵심이다..

BPE는 이 조각들을 만드는 알고리즘 중 하나. 처음엔 문자 단위에서 시작해서, 가장 자주 붙어 나오는 인접 쌍을 하나로 병합하는 걸 K번 반복한다. 그러면 `t`+`h` → `th`, `th`+`e` → `the` 같은 식으로 자주 쓰이는 조각이 자연스럽게 자라난다. 병합 규칙 자체가 tokenizer의 학습 결과다.

특수 토큰(`<BOS>`, `<EOS>`)은 문장 경계를 알리는 마커. padding은 배치로 묶기 위한 채움용. attention mask는 진짜 토큰(1)과 padding(0)을 구분해서 attention 계산에서 padding을 무시하게 해준다.

## 걸렸던 것

- tiktoken으로 GPT-2 인코더를 돌려보면 `cat`, `sat`이 `' cat'`, `' sat'`처럼 앞 공백이 붙은 채로 디코드된다. GPT-2 BPE는 공백을 다음 단어의 일부로 학습해서, `cat`과 ` cat`이 서로 다른 토큰 ID다. 문장 첫 단어와 중간 단어가 다르게 표현된다는 뜻.
- ID가 그냥 인덱스라면, 임베딩은 이 무의미한 정수에 어떻게 의미를 부여하나? → 임베딩 테이블의 행 인덱스로 쓰이고, 그 행 벡터를 학습으로 조정한다는 게 다음 챕터 예고편.

## 실험

노트북 돌리고 나서 채우기.

- BPE(tiktoken)에 학습 코퍼스에 없을 만한 신조어(`skibidi`, `rizz`, `yeet`) 넣어보고 몇 조각으로 쪼개지는지 보기. 흔한 접미사는 통째로, 특이 어근은 문자 단위까지 갈 거라 예상.
- 같은 문장을 영/한으로 각각 tiktoken 인코딩해서 토큰 수 비교. cl100k_base가 한국어에 얼마나 개선됐는지가 관전 포인트. API 비용이랑 직결되는 얘기라 실용적.
