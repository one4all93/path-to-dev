<template>
  <!-- 1. 인트로 시작 :: 나의 히어로 아카데미아 처음 장면 참고** -->
  <Intro></Intro>
  <!-- 2.  -->
  <Section1></Section1>
  <!-- 3.  -->
  <Section2></Section2>
</template>

<script setup>
import Intro from '../components/Intro.vue'
import Section1 from '../components/Section1.vue'
import Section2 from '../components/Section2.vue'
</script>

<style>
html,
body {
  height: 100%;
  width: 100%;
  margin: 0;
}

.component {
  flex: 0 0 auto; /* 각 섹션의 높이를 고정 */
  min-height: 100vh; /* 각 섹션이 화면을 꽉 채우도록 */
}

#app {
  display: flex;
  flex-direction: column; /* 세로로 배치 */
  height: 100vh; /* 화면 높이를 100%로 설정 */
  width: 100vh; /* 화면 높이를 100%로 설정 */
  /* overflow-y: auto; 세로 스크롤 허용 */
}
</style>
