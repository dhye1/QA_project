# QA_project
AI Hub 일반상식 데이터 활용 QA 구현 프로젝트

[[정리 자료]](https://github.com/dhye1/QA_project/blob/main/%EB%B0%9C%ED%91%9C%20%EC%9E%90%EB%A3%8C/AI%20hub%20%EC%9D%BC%EB%B0%98%EC%83%81%EC%8B%9D%20%EB%B0%9C%ED%91%9C%20%EC%9E%90%EB%A3%8C.pdf)
[[정리 페이지]](https://velog.io/@hyeda/1222)
 <BR> 


## 구현 실습


 <BR> 

### AI hub의 일반상식 데이터
   - 한국어 위키백과내 주요 문서 15만개에 포함된 지식을 추출한 데이터이다. (KorQuAD 와 유사)
- 위키백과 본문내용과 관련한 질문과 질문에 대응되는 위키백과 본문 내의 정답 쌍으로 구성되어 있다.
- 질문-답 쌍 데이터셋은 Context, question, answer를 각각 포함한다.
- Paragraphs는 가장 상위의 클래스이며 질문-답 세트와 질문-답 세트의 근거 단락인 contex를 하위 클래스로 가진다.

- Answer_start는 Context에서 정답이 위치하는 글자 인덱스를 의미한다.
   
 ![](https://velog.velcdn.com/images/hyeda/post/5d98e432-87d7-4243-8bdd-52c70ec55913/image.png)

   
###     Token embedding
- Token Embedding BERT는 텍스트의 tokenizer 로 Word Piece 모델이라는 subword tokenizer를 사용한다.
   
- tokenizer를 통해서 입력 문장을 토큰단위로 쪼개고, 해당 토큰을 vocab에 매칭하여 id(숫자)로 입력한다.
   
- vocab의 사이즈는 보통 5만정도를 사용하고있고, 이것을 직접 입력하여 BERT 모델을 구축하면 학습해야하는 파라미터의 수가 엄청나게 많아지기 때문에 차원을 낮추기 위해서 embedding layer를 사용한다.
 <BR> 
   
### 다운로드 받은 Pretrained model 로드
### Fine-Tuning
 Pre-train된 BERT 모델을 이용해 수행하고자 하는 task를 추가 학습하는 것을 의미한다. 전이학습은 BERT의 언어 모델의 출력에 추가적인 모델을 쌓아 만든다.
조정 내용
-  BERT의 각 토큰마다 개별 Fully Connected layer를 붙여 한국어 용으로 미세 조정하기 위한 모델 클래스를 정의
- 작은 실습 환경에 맞춰 크기 조정
   -	레이어 : 12 -> 6
   - hidden neuron : 768 -> 512

- pretrained model을 활용해서 입력에 대한 답변을 생성하는 함수를 정의한 후 결과 및 성능을 확인  
 ![](https://velog.velcdn.com/images/hyeda/post/629ef8c8-19ae-44d8-b096-5ba3b1ed1487/image.png)

   ![](https://velog.velcdn.com/images/hyeda/post/277f9d87-0db5-4e04-bc4a-8a7777b73d59/image.png)
![](https://velog.velcdn.com/images/hyeda/post/e7302d95-67f5-4a01-bfc1-2bc88b5a89e4/image.png)
 <BR> 
[[정리 자료]](https://github.com/dhye1/QA_project/blob/main/%EB%B0%9C%ED%91%9C%20%EC%9E%90%EB%A3%8C/AI%20hub%20%EC%9D%BC%EB%B0%98%EC%83%81%EC%8B%9D%20%EB%B0%9C%ED%91%9C%20%EC%9E%90%EB%A3%8C.pdf)
[[정리 페이지]](https://velog.io/@hyeda/1222)
 <BR> 
