<template>
  <div>
    <div style="background: #2eaec3; color: #fff; padding: 1rem">
      <div>{{ compireValues }}</div>
      <div>{{ idIdentifier }}</div>
    </div>
    <div class="face-box">
      <div
        v-for="(item, index) in steps"
        :key="index"
        :class="{ 'btn-disable': isDisableButtons }"
        class="step-1"
      >
        <div v-show="item.selected && item.content === 'step1'">
          <div class="step-title-btn">
            <h2>Step 1 - Chin Shape</h2>
          </div>
          <div class="face-container">
            <div
              v-for="(val, idx) in item.chinShape"
              :key="idx"
              @click="nextStep(val, index, val.id)"
            >
              <div>
                <img :src="val.img" alt="rounded" />
              </div>
              <div class="btn-face">
                <button>{{ val.value }}</button>
              </div>
            </div>
          </div>
          <!-- <button @click="next(index)">Next</button> -->
        </div>

        <div v-show="item.selected && item.content === 'step2'">
          <div class="step-title-btn">
            <img
              @click="prev(index, item)"
              width="35"
              src="../assets/prev.png"
              alt="prev"
            />
            <h2>Step 2 - Forehead Size</h2>
          </div>
          <div class="face-container">
            <div
              v-for="(val, idx) in item.foreheadSize"
              :key="idx"
              @click="nextStep(val, index, val.id)"
            >
              <div>
                <img :src="val.img" alt="rounded" />
              </div>
              <div class="btn-face">
                <button>{{ val.value }}</button>
              </div>
            </div>
          </div>
          <!-- <button @click="next(index)">Next</button>
        <button @click="prev(index)">Prev</button> -->
        </div>

        <div v-show="item.selected && item.content === 'step3'">
          <div class="step-title-btn">
            <img
              @click="prev(index)"
              width="35"
              src="../assets/prev.png"
              alt="prev"
            />
            <h2>Step 3 - Face Length</h2>
          </div>
          <div class="face-container">
            <div
              v-for="(val, idx) in item.faceLength"
              :key="idx"
              @click="nextStep(val, index, val.id)"
            >
              <div>
                <img :src="val.img" alt="rounded" />
              </div>
              <div class="btn-face">
                <button>{{ val.value }}</button>
              </div>
            </div>
          </div>
          <!-- <button @click="prev(index)">Prev</button>
        <button @click="next(index)">Next</button> -->
        </div>
      </div>

      <div v-show="finalPage" class="final-page">
        <h3>
          Final page result is:
          <!-- <span style="text-transform: uppercase">{{ finalResult }}</span> -->
        </h3>
        <div>
          <div v-for="(value, index) in finalResult" :key="index">
            <h3>{{ value.title }}</h3>
            <div>
              <p>{{ value.description }}</p>
            </div>
            <div>
              <img :src="value.image" alt="" />
            </div>
            <div class="final-links">
              <a href="/">Go back</a>
              <a :href="value.link">Shop Frames</a>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      idIdentifier: [],
      compireValues: [],

      finalPage: false,

      finalResult: [
        {
          title: "",
          description: "",
          image: "",
          link: "",
        },
      ],

      isDisableButtons: false,

      steps: [
        {
          content: "step1",
          title: "Step 1",
          selected: true,
          chinShape: [
            {
              id: 1,
              value: "Defined",
              img: require("@/assets/images/Chin/defined.png"),
            },
            {
              id: 2,
              value: "Rounded",
              img: require("@/assets/images/Chin/rounded.png"),
            },
            {
              id: 3,
              value: "Pointed",
              img: require("@/assets/images/Chin/pointed.png"),
            },
          ],
        },
        {
          content: "step2",
          title: "Step 2",
          selected: false,
          foreheadSize: [
            {
              id: 1,
              value: "Equal",
              img: require("@/assets/images/Forehead/equal.png"),
            },
            {
              id: 2,
              value: "Wider",
              img: require("@/assets/images/Forehead/smaller.png"),
            },
            {
              id: 3,
              value: "Smaller",
              img: require("@/assets/images/Forehead/wider.png"),
            },
          ],
        },
        {
          content: "step3",
          title: "Step 3",
          selected: false,
          faceLength: [
            {
              id: 1,
              value: "Short",
              img: require("@/assets/images/FaceLength/short.png"),
            },
            {
              id: 2,
              value: "Long",
              img: require("@/assets/images/FaceLength/long.png"),
            },
          ],
        },
      ],

      squareContent: {
        title: "Square Face",
        description:
          "You have a square face with a defined jawline. Round and oval glasses add balance and structure to square faces.",
        img: "squareFace",
        link: "/square/face",
      },

      ovalContent: {
        title: "Oval Face",
        description:
          "Oval is considered the most versatile and proportionally balanced face shape, which means that almost any style will look good on you.",
        img: "ovalFace",
        link: "/oval/face",
      },

      heartContent: {
        title: "Heart Face",
        description:
          "You have a heart-shaped face with a narrower chin and higher cheekbones. Rectangle, round, and aviator frames bring softness and balance to angular heart faces.",
        img: "heartFace",
        link: "/heart/face",
      },

      triangleContent: {
        title: "Triangle Face",
        description:
          "Triangular face shapes have a broader jawline with less prominent cheekbones and narrow forehead. Flattering styles are browline and semi-rimless.",
        img: "triangleFace",
        link: "/triangle/face",
      },

      roundContent: {
        title: "Round Face",
        description:
          "Round faces are typically as wide as they are long without prominent cheekbones. Frames that are wider than deep and angular, like rectangle and geometric, will flatter the face.",
        img: "roundFace",
        link: "/round/face",
      },

      diamondContent: {
        title: "Diamond Face",
        description:
          "Diamond shaped faces are characterized by prominent cheekbones and a narrower forehead and jawline. Light and unobtrusive frames with rounded lens shapes bring balance and softness, delicate browlines widen the forehead.",
        img: "diamondFace",
        link: "/diamond/face",
      }
    };
  },

  methods: {
    // Steps
    nextStep(item, index, id) {
      this.idIdentifier.push(id);

      if (this.compireValues.length < this.steps.length - 1) {
        this.fillArray(item.value);
        this.next(index);
      } else {
        this.fillArray(item.value);

        this.steps.map((i) => (i.selected = false)); // Disable all steps when show final page

        this.arrayReduce(this.idIdentifier); // Calculate identifiers for the final result

        this.finalPage = true; // Show final page
        this.isDisableButtons = true;
      }
    },

    // Next Step
    next(index) {
      this.steps[index].selected = false;
      this.steps[index + 1].selected = true;
    },

    // Prev Step
    prev(index) {
      this.steps[index].selected = false;
      this.steps[index - 1].selected = true;

      this.isDisableButtons = false;

      this.compireValues.pop(); // Remove last value when prev
      this.idIdentifier.pop(); // Remove last value when prev
    },

    fillArray(item) {
      this.compireValues.push(item);
    },

    fillResult(objContent) {
      this.finalResult.forEach((item) => {
        item.title = objContent.title;
        item.description = objContent.description;
        item.image = require(`@/assets/images/KnowShape/${objContent.img}.png`);
        item.link = objContent.link;
      });
    },

    arrayReduce(arr) {
      switch (Number(arr.join(""))) {
        case 111:
          this.fillResult(this.squareContent);
          break;
        case 112:
          this.fillResult(this.ovalContent);
          break;
        case 121:
          this.fillResult(this.heartContent);
          break;
        case 122:
          this.fillResult(this.heartContent);
          break;
        case 131:
          this.fillResult(this.triangleContent);
          break;
        case 132:
          this.fillResult(this.triangleContent);
          break;
        case 211:
          this.fillResult(this.roundContent);
          break;
        case 212:
          this.fillResult(this.ovalContent);
          break;
        case 221:
          this.fillResult(this.heartContent);
          break;
        case 222:
          this.fillResult(this.heartContent);
          break;
        case 231:
          this.fillResult(this.triangleContent);
          break;
        case 232:
          this.fillResult(this.triangleContent);
          break;
        case 311:
          this.fillResult(this.diamondContent);
          break;
        case 312:
          this.fillResult(this.ovalContent);
          break;
        case 321:
          this.fillResult(this.heartContent);
          break;
        case 322:
          this.fillResult(this.heartContent);
          break;
        case 331:
          this.fillResult(this.diamondContent);
          break;
        case 332:
          this.fillResult(this.diamondContent);
          break;
        default:
          this.finalResult = "";
      }
    },
  },
};
</script>

<style>
@import "../assets/css/style.css";
</style>