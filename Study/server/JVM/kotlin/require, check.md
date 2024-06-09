- `require()` 는 안에 있는 구문이 `false`일때 `IllegalStateException`을 발생시킨다.
- `check()`는 안에 있는 구문이 `false`일 때 `IllegalArgumentException`을 발생시킨다.
- `checkNotNull` `requireNotNull`로 `null`체크를 할 수 있으며 이후 `null`이 아니라고 가정
	- 스마트 캐스트를 사용할 수 있다.

check 예시
```kotlin
fun viewReview(reviewId: Long){
  val review = reviewRepostiroy.findById(reviewId)
  review.addViewCount()
  return review
}
```

required 예시
```kotlin
fun validateReviewModifyForm(reviewModifyRequest: ReviewModifyForm){
  val review = reviewRepository.findById(reviewModifyRequest.reviewId)

  require(reviewModifyRequest.content.isNotBlank() && reviewModifyRequest.content.length < MAX_CONTENT_LENGTH) {
        "리뷰 내용은 공백이거나 1000자를 초과하면 안됩니다."
    }
    review.modify(content = reviewModifyRequest.content)
}
```

- [i] require: argument를 제한할때
	인자로 받은 값의 유효성을 검사하는 로직
- [i] check: 상태와 관련된 동작
	어떤 구제적인 조건을 만족할때만 함수를 사용할 수 있게 해야할 때 check를 사용
- [i] assert: 어떤 것이 true인지 확인할 수 있다. 
      assert 테스트 모드에서만 작동한다.

---
[Kotlin의 check()와 require()](https://velog.io/@eastperson/Kotlin%EC%9D%98-check%EC%99%80-require-ibg71b1z)