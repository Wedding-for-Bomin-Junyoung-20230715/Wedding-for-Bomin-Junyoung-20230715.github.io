<!-- 출력순서: 5 -->
<!-- 사진: X -->
<template>
  <div class="date-section">
    <div class="date-container" ref="startAnimation">
      <div class="date-month half">
        <span class="font-month animate-month"> {{ month }} <span class="date">월</span> {{ day }} <span class="date">일(토)</span></span>
      </div>
    </div>
  </div>
</template>
    
<script>
export default {
  name: 'DateCard',
  data() {
    return {
      month: '07',
      day: '15',
      isAnimate: false
    }
  },
  mounted() {
    const options = {
      rootMargin: '10px',
      threshold: 0.5, // 대상 엘리먼트가 뷰포트에 50% 이상 들어왔을 때 콜백 함수 호출
    };
    const observer = new IntersectionObserver(this.callback, options);
    observer.observe(this.$refs.startAnimation);
  },
  methods: {
    callback(entries, observer) {// eslint-disable-line no-unused-vars
      entries.forEach(entry => {
        if (entry.isIntersecting) {
          // 대상 엘리먼트가 뷰포트에 진입한 경우
          if (this.isAnimate) {
            // this.animateText();
            this.isAnimate = false;
          }
        } else {
          // 대상 엘리먼트가 뷰포트를 벗어난 경우
          this.isAnimate = true;
        }
      });
    },
    animateText() {
      const month = document.querySelector(".animate-month");
      const day = document.querySelector(".animate-day");

      // Animate month
      month.animate(
        [
          { transform: "translate(-50vw, 20vh)", opacity: 0 },
          { transform: "translate(0, 0)", opacity: 1 },
        ],
        { duration: 1000, easing: "ease-out", fill: "forwards" }
      );

      // Animate day
      day.animate(
        [
          { transform: "translate(50vw, -20vh)", opacity: 0 },
          { transform: "translate(0, 0)", opacity: 1 },
          
        ],
        { duration: 1000, easing: "ease-out", fill: "forwards" }
      );
    },
  }
}
</script>

<style scoped>
.date-section {
  /* height: 200px; */
  position: relative;
  display: flex;
  height: 100px;
}

.date {
  position: relative;
  display: flex;
  font-size: 25px;
}

.date-container {
  position: relative;
  display: flex;
  width: 100%;
  /* height: calc(var(--vh) * 100); */
  height: 100px;
  position: absolute;
  left: 0%;
  font-size: 35px;
}
.date-month {
  background-color: rgb(255, 255, 255);
  /* clip-path: polygon(0 0, 100% 0, 0 100%); */
  z-index: 1;
  widows: 100%;
}

.date-day {
  background-color: #f1efea;
  z-index: 0;
}

.font-month {
  align-items: flex-end;
  color: #55504f;
  position: absolute;
  display: flex;
  top: 45%;
  left: 50%;
  transform: translate(-50%, -50%);
}
</style>