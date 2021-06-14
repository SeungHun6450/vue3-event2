<template>
<!--
  핸들러는 체이닝형태로 동시 사용 가능하다 ex) @click.once.prevent
  @click.prevent : 기본 동작을 방지 
  @click.once : 단 한번만 실행, 이후 실행되지 않는다.
  @click.stop : 이벤트 버블링(특정한 요소를 선택했을 때 그 요소를 포함하고있는 부모요소에도 선택한 이벤트도 위쪽으로 전파되는 것)을 막기 위해 사용
  @click.capture : 해당 동작이 반대로 일어나게 함(캡처링)
  @click.self : 해당 영역을 정확하게 클릭 시 이벤트가 발생, 자기 자신에게만 이벤트 방생
  @wheel : 마우스 휠 사용 시 이벤트 출력
  @wheel.passive : 기본적인 로직의 처리와 화면의 위아래 스크롤을 완전히 독립시켜 부하를 줄여준다.
 -->

 <!-- exmaple 1 -->
  <!-- <a
    href="http://naver.com"
    target="_blank"
    @click.once="handler">
    NAVER
  </a> -->

  <!-- example2 -->
  <!-- <div
    class="parent"
    @click.capture.stop="handlerA">
    <div
      class="child"
      @click="handlerB"></div>
  </div> -->

  <!-- example3 -->
  <!-- <div
    class="parent"
    @click.self="handlerA">
    <div class="child"></div>
  </div> -->


  <!-- example4 -->
  <div
    class="parent"
    @wheel.passive="handler">
    <div class="child"></div>
  </div>
</template>

<script>
// https://v3.ko.vuejs.org/guide/events.html#%E1%84%8B%E1%85%B5%E1%84%87%E1%85%A6%E1%86%AB%E1%84%90%E1%85%B3-%E1%84%89%E1%85%AE%E1%84%89%E1%85%B5%E1%86%A8%E1%84%8B%E1%85%A5

// exmpale 1
// export default {
//   methods: {
//     handler() {
//       // event.preventDefault() // 기본 동작을 방지
//       console.log('ABC')
//     }
//   }
// }

// example 2
// export default {
//   methods: {
//     handlerA() {
//       console.log('A')
//     },
//     handlerB(event) {
//       // event.stopPropagation() // 버블링을 막기 위해
//       console.log('B')
//     }
//   }
// }

// example 3
// export default {
//   methods: {
//     handlerA(event) {
//       console.log(event.target) // 실제 클릭된 그 요소
//       console.log(event.currentTarget) // 타겟이 실행된 해당하는 함수에 연결되어있는 이벤트에 해당하는 요소
//       console.log('A')
//     },
//     handlerB() {
//       console.log('B')
//     }
//   }
// }


// example 4
export default {
  methods: {
    handler(e) {
      for(let i = 0; i < 10000; i += 1){
        console.log(e)
      }
    }
  }
}
</script>

<style scoped lang="scss">
  .parent {
    width: 200px;
    height: 100px;
    background-color: royalblue;
    margin: 10px;
    padding: 10px;
    // example 4
    overflow: auto;
    .child {
      width: 100px;
      // height: 100px;

      // example 4
      height: 2000px;
      background-color: orange;
    }

  }
</style>