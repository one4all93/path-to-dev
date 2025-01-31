<template>
  <div class="intro component" ref="introComponent">
    <!-- Video (Fixed Position) -->
    <video class="intro-video" src="../mp4/oneForAll.mp4" autoplay muted loop></video>
    <div class="overlay"></div>

    <!-- Scrolling Text -->
    <div class="scrolling-text">
      <br />
      <br />
      <br />
      <h1>이 이야기는</h1>
      <br />
      <br />
      <br />
      <h1>내가 개발자가 되기까지</h1>
      <br />
      <br />
      <br />
      <h1>그리고</h1>
      <br />
      <br />
      <br />
      <h1>개발자로 살아가는 이야기다</h1>
      <br />
      <br />
      <br />
      <h1>그 시작은 이렇다</h1>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Intro',
  mounted() {
    // 비디오와 텍스트 초기화
    this.initializeIntro()
    window.addEventListener('scroll', this.handleScroll)
  },
  methods: {
    initializeIntro() {
      const introElement = this.$refs.introComponent
      introElement.querySelector('.intro-video').style.opacity = 1 // 비디오 바로 보이게 설정
      const textElements = document.querySelectorAll('.scrolling-text h1')
      textElements.forEach((el) => {
        el.style.opacity = 0 // 초기 상태에서 텍스트는 숨김
      })
    },

    handleScroll() {
      const introElement = this.$refs.introComponent
      const scrollY = window.scrollY
      const introOffset = introElement.offsetTop
      const introHeight = introElement.offsetHeight

      // 비디오가 화면에 보이는지 체크
      if (scrollY >= introOffset && scrollY <= introOffset + introHeight) {
        introElement.querySelector('.intro-video').style.opacity = 1
      } else {
        introElement.querySelector('.intro-video').style.opacity = 0
      }

      this.handleTextScroll(scrollY) // 텍스트 애니메이션
    },

    handleTextScroll(scrollY) {
      const textElements = document.querySelectorAll('.scrolling-text h1')
      textElements.forEach((el, index) => {
        const startFade = 250 + index * 250
        const opacity = Math.max(1 - (scrollY - startFade) / 100, 0)
        const translateY = Math.max((scrollY - startFade) / 2, 0)

        if (scrollY >= startFade - 250 && scrollY < startFade + 250) {
          el.style.opacity = opacity
          el.style.transform = `translateY(-${translateY}px)`
          el.style.zIndex = 1
        } else {
          el.style.opacity = 0
          el.style.transform = 'translateY(0px)'
          el.style.zIndex = -1
        }
      })
    },
  },
  beforeDestroy() {
    window.removeEventListener('scroll', this.handleScroll)
  },
}
</script>

<style scoped>
.intro.component {
  position: relative;
  width: 100%;
  height: 200vh; /* 충분한 높이로 스크롤 테스트 */
}

.intro-video {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100vh;
  object-fit: cover;
  opacity: 1; /* 비디오가 처음부터 보이도록 설정 */
  z-index: -1;
}

.overlay {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: rgba(0, 0, 0, 0.5);
  pointer-events: none;
}

.scrolling-text {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  text-align: center;
  color: white;
  font-size: 2rem;
  width: 100%;
}

h1 {
  margin: 0;
  opacity: 0; /* 초기 상태에서 텍스트는 보이지 않음 */
  transform: translateY(50px); /* 처음엔 아래로 내려놓기 */
  transition:
    opacity 0.3s ease,
    transform 0.3s ease;
}
</style>
