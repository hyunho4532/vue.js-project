<h3>뷰 컴포넌트 통신</h3>
<ul>
  <li>뷰는 컴포넌트로 화면을 구성하므로 같은 웹 페이지라도 데이터를 공유할 수 없다.</li>
  <ul>
    <li><strong>이유? 컴포넌트마다 자체적으로 고유한 유효 범위를 갖기 때문이다.</strong></li>
  </ul>
</ul>

<ul>
  <li>컴포넌트 전달 방법은 아래와 같다.</li>
  <ul>
    <li><strong>상위(부모) - 하위(자식) 컴포넌트 간의 데이터 전달 방법</strong></li>
    <ul>
      <li>상위에서 하위로는 props 라는 특별한 속성을 전달하고, 하위에서 상위로는 기본적으로 이벤트만 전달한다.</li>
      <li>이벤트 발생과 수신은 $emit()과 v-on: 속성을 사용하여 구현한다.</li>
    </ul>
  </ul>
</ul>

<hr>

<h3>같은 레벨의 컴포넌트 간 통신은 어떻게 할까?</h3>
<ul>
  <li>같은 레벨 간에 통신하기 위해 강제로 상위 컴포넌트를 두어야 하며, 이벤트 버스로 통해 해결할 수 있다.</li>
</ul>

<hr>

<h3>이벤트 버스란 무엇인가?</h3>
<ul>
  <li>개발자가 지정한 2개의 컴포넌트 간에 데이터를 주고받을 수 있는 방법이다.</li>
</ul>

<hr>

<code>this.$emit('이벤트명');</code><br>
<code><child-component v-on:이벤트명="상위 컴포넌트의 메서드명"></child-component></code><br><br>


<h3>이벤트 버스 형식은 다음과 같다.</h3><br>

이벤트 버스를 위한 추가 인스턴스 1개 생성
<code>var eventBus = new Vue();</code><br><br>

```
# 이벤트를 보내는 컴포넌트
methods: {
  메서드명: function() {
  eventBus.$emit('이벤트명', 데이터);
}
```

```
# 이벤트를 받는 컴포넌트
methods: {
  created: function() {
    eventBus.$on('이벤트명', function(데이터) {
      ...
    });
  }
}
```

<code>
