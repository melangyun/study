[utf8mb4 언어 셋 소개 및 표현 범위](https://blog.lael.be/post/917)
> - **Charset**: 문자 집합
> - **Collation**: 정렬
> 데이터 베이스도 *더 작은 공간을 사용하면서, 더 빠르게 처리할 수 있는* 방향으로 발전하였고, 해당 목적을 위해서 **데이터 자료형** 을 사용하게 되었다.

# UTF-8
실생활의 대부분 데이터는 텍스트 기반(text-centric)이다. 실생활의 모든 텍스트 데이터를 저장할 수 있는 자료형이 필요로 하게 되었고 이를 위해 charset UTF-8이 나오게 되었다.

전 세계 모든 언어가 21bit(3byte 이하)에 저장되기 때문에, MYSQL에서 utf8을 3바이트 가변 자료형으로 설계하였다.
따라서 4byte문자열(이모지의 경우) utf8에 저장하면 값 손실이 발생한다.
기존 널리 사용되던 charset은 utf-8, collation은 **utf8_general_ci**인데 이 경우 대부분의 환경에서 문제를 일으킨다.

## 4바이트 UTF-8
MySQL에서는 원래 설계대로 가변 4바이트 UTF-8문자열을 저장할 수 있도록 2010년 **utf8mb4**라는 charset이 추가되었다.

### Collation(정렬 방식)
Collation은 텍스트 데이터를 정렬할때 사용한다. 즉, text계열 자료형에서만 사용할 수 있는 속성이다.
- utf8_bin(or utf8mb4_bin)
	- 바이너리 저장 값 그대로 정렬
	- hex코드대로 정렬 (A -> B -> a -> b)
- utf8_general_ci (or utf8mb4_general_ci)
	- 텍스트 정렬할 때 a다음에 b가 나타나야 한다는 생각으로 정렬방식. 일반적으로 널리 사용된다.
	- A-> a-> B -> b
- utf_unicode_ci (or utf8mb4_unicode_ci)
	- general_ci보다 조금 더 사람에 맞게 정렬한다.
	- *한국어, 영어, 중국어, 일본어*사용환경에서는 general_ci와 unicode_ci의 결과가 동일하다.

MySQL5.5.3이전에는 utf8 charset, utf_general_ci collation사용 권장
이후에는 utfmb3 cahrset, utf8mb4_unicode_ci collation사용 권장

> 기존 utf8을 utf8mb4로 바꾸어도 값의 손실은 없으며, 이모지 문자열이 필요없다면 utf8로 사용해도 괜찮다.

