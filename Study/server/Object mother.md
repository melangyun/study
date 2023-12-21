---

---
> When you write tests in a reasonably sized system, you find you have to create a lot of example data. If I want to test a sick pay calculation on an employee, I need an employee. But this isn't just a simple object - I'll need the employee's marital status, number of dependents, some employment and payroll history. Potentially this can be a lot of objects to create. This set data is generally referred to as the `test fixture`.

시스템에서 테스트를 작성할 때 <u>많은</u> 예제 데이터가 필요하다.
이 세트 데이터를 일반적으로 데이터 픽스처(data fixture)라고 한다.

테스트에서 사용할 객체나 데이터를 생성하는데 도움을 주는 패턴으로, 반복적고 일정한 데이터를 테스트에서 사용할 때 유용하다. 특히 여러 테스트 케이스에서 동일한 초기 데이터가 필요한 경우 유용하다.

`Object mother`사용 시 데이터를 중앙에서 관리하고 필요할 때 쉽게 가져와서 사용할 수 있다.
(하지만 과용되면 코드의 가독성을 해치고 코드가 이해하기 어려워 질 수도 있다.)

구현 디테일은 -> [Mastering the Object Mother](https://jonasg.io/posts/object-mother/)
[Object Mother; java기반 도입 라이브러리](https://backendbrew.com/docs/pattern/object-mother) cf) easy-random

---
[ObjectMother; Martin Fowler](https://martinfowler.com/bliki/ObjectMother.html)

