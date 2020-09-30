<template>
  <div class="container">
    <div class="progress-container">
      <progress min="0" max="100" value="0"></progress>
      <span v-for="n in parseInt(stepCount)" :key="n"></span>
      <div class="circle"></div>
      <div class="svg">
        <svg
          width="50"
          height="50"
          viewBox="0 0 21 20"
          fill="none"
          xmlns="http://www.w3.org/2000/svg"
        >
          <circle
            id="filled"
            cx="10.5996"
            cy="10"
            r="9"
            fill="white"
            stroke="#E9E9E9"
            stroke-width="2"
          />
          <path
            d="M10.3143 5.87812C10.4041 5.60172 10.7951 5.60172 10.8849 5.87812L11.6548 8.24762C11.695 8.37123 11.8102 8.45492 11.9401 8.45492H14.4316C14.7222 8.45492 14.843 8.8268 14.6079 8.99762L12.5923 10.4621C12.4871 10.5384 12.4431 10.6739 12.4833 10.7975L13.2532 13.167C13.343 13.4434 13.0267 13.6732 12.7916 13.5024L10.7759 12.0379C10.6708 11.9616 10.5284 11.9616 10.4233 12.0379L8.40764 13.5024C8.17252 13.6732 7.85618 13.4434 7.94598 13.167L8.71588 10.7975C8.75605 10.6739 8.71205 10.5384 8.6069 10.4621L6.59128 8.99762C6.35617 8.8268 6.477 8.45492 6.76762 8.45492H9.25906C9.38903 8.45492 9.50422 8.37123 9.54438 8.24762L10.3143 5.87812Z"
            fill="#ededed"
          />
        </svg>
      </div>
    </div>
    <div>
      <button id="btn">inc</button>
    </div>
  </div>
</template>

<script>
setTimeout(() => {
  const spans = document.querySelectorAll(".progress-container span");
  const allspans = spans.length;
  const progress = document.querySelector("progress");
  const circle = document.querySelector(".circle");
  const btn = document.querySelector("button");
  const filled = document.querySelector("#filled");
  console.log(filled);

  let cntstep = 100 / allspans,
    cnt = 0;

  let firstspan = 0;

  spans.forEach((t, i) => {
    if (firstspan == 0) {
      t.style.opacity = "0";
    }
    firstspan++;
    t.setAttribute("data-step", cnt);
    t.style.left = i * cntstep + "%";
    t.style.transform = "translate(-" + cnt + "%, -50%)";
  });

  btn.addEventListener("click", function () {
    cnt += cntstep;
    if (cnt < 100) {
      progress.setAttribute("value", cnt);
      circle.style.left = "calc(" + cnt + "% - 8px)";
      console.log(cnt);
    }
    if (cnt === 100) {
      progress.setAttribute("value", cnt);
      circle.style.left = "calc(" + cnt + "% - 8px)";
      filled.style.fill = "orange";
    }
  });
}, 0);

export default {
  name: "HelloWorld",
  props: {
    stepCount: String,
  },
};
</script>

<style scoped>
.container {
  width: 80%;
  height: 80%;
  background-color: #fff;
}

.progress-container {
  display: inline-flex;
  position: relative;
  height: 10px;
  width: 100%;
}

.progress-container span {
  position: absolute;
  top: 50%;
  height: 8px;
  width: 8px;
  z-index: 100;
  clip-path: ellipse(25% 40% at 50% 50%);
  background: white;
  cursor: pointer;
}
.circle {
  position: absolute;
  top: 50%;
  left: 0;
  transform: translateY(-50%);
  transition: left 0.5s;
  height: 20px;
  width: 20px;
  border-radius: 50%;
  background-color: #41b0c1;
  border: 1px solid white;
  z-index: 200;
}
.svg {
  overflow: hidden;
  width: 25px;
  height: 25px;
  clip-path: circle(50% at 50% 50%);
  background: white;
  position: absolute;
  top: 50%;
  transform: translateY(-50%);
  right: -14px;
  z-index: 210;
}
svg {
  fill: #eee;
  position: absolute;
  top: 50%;
  transform: translateY(-50%);
  z-index: 210;
  overflow: hidden;
  right: 0px;
  width: 25px;
  height: 25px;
  cursor: pointer;
  transition: 0.5;
}
svg.clicked {
  fill: #41b0c1;
}
progress[value] {
  /* Reset the default appearance */
  position: relative;
  -webkit-appearance: none;
  appearance: none;

  height: 10px;
  width: 100%;
  border-radius: 5px;
}

progress[value]::-webkit-progress-bar {
  border-radius: 5px;
  background: #eee;
}
progress[value]::-webkit-progress-value {
  transition: width 0.5s;
  border-radius: 5px;
  background: linear-gradient(to right, #a2e3d7, #41b0c1);
}
</style>
