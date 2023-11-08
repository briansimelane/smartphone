<script setup>
import { ref, computed, reactive, VueElement } from "vue";
import cube from "@heroicons/vue";

const actionNames = {
  0: { name: "Blank", class: "class0" },
  1: { name: "Logistics", class: "class1" },
  2: { name: "Add Product", class: "class2" },
  3: { name: "Increase Price", class: "class3" },
  4: { name: "Reduce Price & Add Product", class: "class4" },
  5: { name: "Improvement", class: "class5" },
  6: { name: "Research", class: "class6" },
};

const layouts = {
  1: { bottom: [0, 1, 2, 3, 4], prod: 1 },
  2: { bottom: [0, 1, 2, 3], prod: 2 },
  3: { bottom: [0, 1, 2, 4], prod: 2 },
  4: { bottom: [0, 1], prod: 4 },
  5: { bottom: [0, 2, 4], prod: 3 },
  6: { bottom: [1, 2, 3, 4, 5], prod: 1 },
  7: { bottom: [2, 3, 4, 5], prod: 2 },
  8: { bottom: [1, 3, 4, 5], prod: 2 },
  9: { bottom: [4, 5], prod: 4 },
  10: { bottom: [1, 3, 5], prod: 3 },
};

const cardA1 = [0, 1, 5, 2, 0, 3];
const cardA2 = [4, 0, 5, 2, 0, 6];
const cardB1 = [4, 0, 6, 1, 0, 1];
const cardB2 = [0, 2, 1, 6, 0, 6];

const cardA1Notification = ref("");
const cardA2Notification = ref("");
const cardB1Notification = ref("");
const cardB2Notification = ref("");

const cardAarray = ref([]);
const cardBarray = ref([]);

const bottomCardArray = ref([]);
const topCardArray = ref([]);

const selectedArray = ref([]);

const layoutProducts = ref(0);

// Layout Arrays
const layout1BottomArray = computed(() => {
  return bottomCardArray.value.filter((el, i) =>
    layouts[1].bottom.some((j) => i === j)
  );
});

const layout2BottomArray = computed(() => {
  return bottomCardArray.value.filter((el, i) =>
    layouts[2].bottom.some((j) => i === j)
  );
});

const layout3BottomArray = computed(() => {
  return bottomCardArray.value.filter((el, i) =>
    layouts[3].bottom.some((j) => i === j)
  );
});

const layout4BottomArray = computed(() => {
  return bottomCardArray.value.filter((el, i) =>
    layouts[4].bottom.some((j) => i === j)
  );
});

const layout5BottomArray = computed(() => {
  return bottomCardArray.value.filter((el, i) =>
    layouts[5].bottom.some((j) => i === j)
  );
});

const layout6BottomArray = computed(() => {
  return bottomCardArray.value.filter((el, i) =>
    layouts[6].bottom.some((j) => i === j)
  );
});

const layout7BottomArray = computed(() => {
  return bottomCardArray.value.filter((el, i) =>
    layouts[7].bottom.some((j) => i === j)
  );
});

const layout8BottomArray = computed(() => {
  return bottomCardArray.value.filter((el, i) =>
    layouts[8].bottom.some((j) => i === j)
  );
});

const layout9BottomArray = computed(() => {
  return bottomCardArray.value.filter((el, i) =>
    layouts[9].bottom.some((j) => i === j)
  );
});

const layout10BottomArray = computed(() => {
  return bottomCardArray.value.filter((el, i) =>
    layouts[10].bottom.some((j) => i === j)
  );
});

const bottomCardClass = ref("white");
const topCardClass = ref("white");

const layout1ActiveClass = ref("");
const layout2ActiveClass = ref("");
const layout3ActiveClass = ref("");
const layout4ActiveClass = ref("");
const layout5ActiveClass = ref("");
const layout6ActiveClass = ref("");
const layout7ActiveClass = ref("");
const layout8ActiveClass = ref("");
const layout9ActiveClass = ref("");
const layout10ActiveClass = ref("");

const cardAcolor = "#000000";
const cardBcolor = "#a8a29e";

const bottomButtonA1 = ref(true);
const bottomButtonA2 = ref(true);
const bottomButtonB1 = ref(true);
const bottomButtonB2 = ref(true);

const cardABottom = ref(false);
const cardBBottom = ref(false);

const cardAtTheBottom = "";

function printBottomCard(theCard) {
  console.log(theCard);
}

const makeCardABottom = (event) => {
  const targetCardName = event.target.getAttribute("data-card");
  const targetCardID = event.target.getAttribute("data-ID");
  const bottomCardEl = document.querySelector("#bottom-card");
  const targetCardinArray = cards.find((card) => card.name === targetCardName);
  const targetCard = document.getElementById(targetCardID);

  // create bottom card

  //Mark Card A Bottom
  cardABottom.value = true;
  cardBBottom.value = false;
  bottomCardArray.value = cardAarray.value;
  topCardArray.value = cardBarray.value;

  bottomCardClass.value = cardAcolor;
  topCardClass.value = cardBcolor;

  // hide buttons under A cards
  bottomButtonA1.value = false;
  bottomButtonA2.value = false;
  bottomButtonB1.value = true;
  bottomButtonB2.value = true;

  console.log(targetCardinArray, targetCard.innerHTML);
};

const makeCardBBottom = () => {
  //Mark Card B Bottom
  cardABottom.value = false;
  cardBBottom.value = true;
  bottomCardArray.value = cardBarray.value;
  topCardArray.value = cardAarray.value;

  bottomCardClass.value = cardBcolor;
  topCardClass.value = cardAcolor;

  // hide buttons under B cards
  bottomButtonA1.value = true;
  bottomButtonA2.value = true;
  bottomButtonB1.value = false;
  bottomButtonB2.value = false;
};

const cardAselect = (cardAselected) => {
  if (cardAselected == "A1") {
    cardA2Notification.value = "";
    cardA1Notification.value = "Selected";
    cardAarray.value = cardA1;
    if (cardABottom.value == true) {
      bottomCardArray.value = cardAarray.value;
    } else {
      topCardArray.value = cardAarray.value;
    }
  } else {
    cardA2Notification.value = "Selected";
    cardA1Notification.value = "";
    cardAarray.value = cardA2;
    if (cardABottom.value == true) {
      bottomCardArray.value = cardAarray.value;
    } else {
      topCardArray.value = cardAarray.value;
    }
  }
};

const cardBselect = (cardAselected) => {
  if (cardAselected == "B1") {
    cardB2Notification.value = "";
    cardB1Notification.value = "Selected";
    cardBarray.value = cardB1;
    if (cardBBottom.value == true) {
      bottomCardArray.value = cardBarray.value;
    } else {
      topCardArray.value = cardBarray.value;
    }
  } else {
    cardB2Notification.value = "Selected";
    cardB1Notification.value = "";
    cardBarray.value = cardB2;
    if (cardBBottom.value == true) {
      bottomCardArray.value = cardBarray.value;
    } else {
      topCardArray.value = cardBarray.value;
    }
  }
};

const selectLayout = (selectedBottom, layout) => {
  // Update selectedArray
  selectedArray.value = selectedBottom.concat(topCardArray.value);
  layoutProducts.value = layouts[layout].prod;

  // Update class to show last selected layout
  layout1ActiveClass.value = "activeLayout";

  switch (layout) {
    case 1:
      layout1ActiveClass.value = "activeLayout";
      layout2ActiveClass.value = "";
      layout3ActiveClass.value = "";
      layout4ActiveClass.value = "";
      layout5ActiveClass.value = "";
      layout6ActiveClass.value = "";
      layout7ActiveClass.value = "";
      layout8ActiveClass.value = "";
      layout9ActiveClass.value = "";
      layout10ActiveClass.value = "";
      break;
    case 2:
      layout1ActiveClass.value = "";
      layout2ActiveClass.value = "activeLayout";
      layout3ActiveClass.value = "";
      layout4ActiveClass.value = "";
      layout5ActiveClass.value = "";
      layout6ActiveClass.value = "";
      layout7ActiveClass.value = "";
      layout8ActiveClass.value = "";
      layout9ActiveClass.value = "";
      layout10ActiveClass.value = "";
      break;
    case 3:
      layout1ActiveClass.value = "";
      layout2ActiveClass.value = "";
      layout3ActiveClass.value = "activeLayout";
      layout4ActiveClass.value = "";
      layout5ActiveClass.value = "";
      layout6ActiveClass.value = "";
      layout7ActiveClass.value = "";
      layout8ActiveClass.value = "";
      layout9ActiveClass.value = "";
      layout10ActiveClass.value = "";
      break;
    case 4:
      layout1ActiveClass.value = "";
      layout2ActiveClass.value = "";
      layout3ActiveClass.value = "";
      layout4ActiveClass.value = "activeLayout";
      layout5ActiveClass.value = "";
      layout6ActiveClass.value = "";
      layout7ActiveClass.value = "";
      layout8ActiveClass.value = "";
      layout9ActiveClass.value = "";
      layout10ActiveClass.value = "";
      break;
    case 5:
      layout1ActiveClass.value = "";
      layout2ActiveClass.value = "";
      layout3ActiveClass.value = "";
      layout4ActiveClass.value = "";
      layout5ActiveClass.value = "activeLayout";
      layout6ActiveClass.value = "";
      layout7ActiveClass.value = "";
      layout8ActiveClass.value = "";
      layout9ActiveClass.value = "";
      layout10ActiveClass.value = "";
      break;
    case 6:
      layout1ActiveClass.value = "";
      layout2ActiveClass.value = "";
      layout3ActiveClass.value = "";
      layout4ActiveClass.value = "";
      layout5ActiveClass.value = "";
      layout6ActiveClass.value = "activeLayout";
      layout7ActiveClass.value = "";
      layout8ActiveClass.value = "";
      layout9ActiveClass.value = "";
      layout10ActiveClass.value = "";
      break;
    case 7:
      layout1ActiveClass.value = "";
      layout2ActiveClass.value = "";
      layout3ActiveClass.value = "";
      layout4ActiveClass.value = "";
      layout5ActiveClass.value = "";
      layout6ActiveClass.value = "";
      layout7ActiveClass.value = "activeLayout";
      layout8ActiveClass.value = "";
      layout9ActiveClass.value = "";
      layout10ActiveClass.value = "";
      break;
    case 8:
      layout1ActiveClass.value = "";
      layout2ActiveClass.value = "";
      layout3ActiveClass.value = "";
      layout4ActiveClass.value = "";
      layout5ActiveClass.value = "";
      layout6ActiveClass.value = "";
      layout7ActiveClass.value = "";
      layout8ActiveClass.value = "activeLayout";
      layout9ActiveClass.value = "";
      layout10ActiveClass.value = "";
      break;
    case 9:
      layout1ActiveClass.value = "";
      layout2ActiveClass.value = "";
      layout3ActiveClass.value = "";
      layout4ActiveClass.value = "";
      layout5ActiveClass.value = "";
      layout6ActiveClass.value = "";
      layout7ActiveClass.value = "";
      layout8ActiveClass.value = "";
      layout9ActiveClass.value = "activeLayout";
      layout10ActiveClass.value = "";
      break;
    case 10:
      layout1ActiveClass.value = "";
      layout2ActiveClass.value = "";
      layout3ActiveClass.value = "";
      layout4ActiveClass.value = "";
      layout5ActiveClass.value = "";
      layout6ActiveClass.value = "";
      layout7ActiveClass.value = "";
      layout8ActiveClass.value = "";
      layout9ActiveClass.value = "";
      layout10ActiveClass.value = "activeLayout";
      break;
    default:
      layout1ActiveClass.value = "";
      layout2ActiveClass.value = "";
      layout3ActiveClass.value = "";
      layout4ActiveClass.value = "";
      layout5ActiveClass.value = "";
      layout6ActiveClass.value = "";
      layout7ActiveClass.value = "";
      layout8ActiveClass.value = "";
      layout9ActiveClass.value = "";
      layout10ActiveClass.value = "";
  }
};

const logisticsCount = computed(() => {
  let count = selectedArray.value.filter((element) => {
    if (element == 1) {
      return true;
    }

    return false;
  }).length;

  return count;
});

const improvementCount = computed(() => {
  let count = selectedArray.value.filter((element) => {
    if (element == 5) {
      return true;
    }

    return false;
  }).length;

  return count;
});

const productsCount = computed(() => {
  let count = selectedArray.value.filter((element) => {
    if (element == 2) {
      return true;
    }

    return false;
  }).length;

  return count;
});

const increasePriceCount = computed(() => {
  let count = selectedArray.value.filter((element) => {
    if (element == 3) {
      return true;
    }

    return false;
  }).length;

  return count;
});

const reducePriceCount = computed(() => {
  let count = selectedArray.value.filter((element) => {
    if (element == 4) {
      return true;
    }

    return false;
  }).length;

  return count;
});

const totalProductsCount = computed(() => {
  return productsCount.value + reducePriceCount.value + layoutProducts.value;
});

const changePrice = computed(() => {
  return increasePriceCount.value - reducePriceCount.value;
});

const researchCount = computed(() => {
  let count = selectedArray.value.filter((element) => {
    if (element == 6) {
      return true;
    }

    return false;
  }).length;

  return count;
});

const cards = [
  {
    name: "Card A1",
    cardRef: "A1",
    cardID: "CardA1",
    classes:
      "container w-60 bg-black p-2 rounded-lg hover:bg-zinc-700 hover:cursor-pointer",
  },
  {
    name: "Card A2",
    cardRef: "A2",
    classes:
      "container w-60 bg-black p-2 rounded-lg hover:bg-zinc-700 hover:cursor-pointer",
  },
  {
    name: "Card B1",
    cardRef: "B1",
    classes:
      "container w-60 bg-stone-400 border border-black p-2 rounded-lg hover:bg-stone-500 hover:cursor-pointer",
  },
  {
    name: "Card B2",
    cardRef: "B2",
    classes:
      "container w-60 bg-stone-400 border border-black p-2 rounded-lg hover:bg-stone-500 hover:cursor-pointer",
  },
];
</script>

<template>
  <main class="">
    <div class="bg-blue-900 text-white mb-2 pl-2 pt-2 pb-2">
      <h2 class="font-bold text-lg">Smartphone Inc</h2>
      <h3 class="font-bold text-md">Phase 1: Planning</h3>
    </div>
    <!-- cards display-->

    <!-- @click="cardAselect(card.cardRef)" -->
    <div class="grid grid-cols-4 mx-auto ml-5" id="cardsArea">
      <div
        v-for="(card, index) in cards"
        :key="index"
        :class="card.classes"
        :id="card.cardID"
        @click="
          card.name === 'Card A1' || card.name === 'Card A2'
            ? cardAselect(card.cardRef)
            : cardBselect(card.cardRef)
        "
      >
        <h2 class="text-sm font-medium text-white">{{ card.name }}</h2>

        <div class="grid grid-cols-2 gap-2 mx-auto">
          <div
            class="h-24 w-24 border border-white rounded-md p-2 ml-2 mt-4 bg-white class0"
          ></div>
          <div
            class="h-24 w-24 border border-white rounded-md p-2 mt-4 bg-white class1"
          ></div>
          <div
            class="h-24 w-24 border border-white rounded-md p-2 ml-2 bg-white class2"
          ></div>
          <div
            class="h-24 w-24 border border-white rounded-md p-2 bg-white class3"
          ></div>
          <div
            class="h-24 w-24 border border-white rounded-md p-2 ml-2 bg-white class4"
          ></div>
          <div
            class="h-24 w-24 border border-white rounded-md p-2 bg-white class5"
          ></div>
        </div>
      </div>
    </div>

    <!-- notifications display-->
    <div class="grid grid-cols-4 mx-auto ml-5">
      <div>
        <div v-if="cardA1Notification">
          <p class="bg-green-50 mt-2 mb-2 p-2 rounded-lg w-60">
            {{ cardA1Notification }}
            <span v-if="cardABottom">(Bottom card)</span>
          </p>
          <div v-if="bottomButtonA1">
            <button
              type="button"
              data-card="Card A1"
              data-ID="CardA1"
              class="rounded-full bg-green-600 py-2.5 px-4 text-sm font-semibold text-white shadow-sm hover:bg-green-500 focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-green-600"
              @click="makeCardABottom"
            >
              Make bottom card
            </button>
          </div>
        </div>
      </div>

      <div>
        <div v-if="cardA2Notification">
          <p class="bg-green-50 mt-2 mb-2 p-2 rounded-lg w-60">
            {{ cardA2Notification }}
            <span v-if="cardABottom">(Bottom card)</span>
          </p>
          <div v-if="bottomButtonA2">
            <button
              type="button"
              class="rounded-full bg-green-600 py-2.5 px-4 text-sm font-semibold text-white shadow-sm hover:bg-green-500 focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-green-600"
              @click="makeCardABottom"
            >
              Make bottom card
            </button>
          </div>
        </div>
      </div>

      <div>
        <div v-if="cardB1Notification">
          <p class="bg-green-50 mt-2 mb-2 p-2 rounded-lg w-60">
            {{ cardB1Notification }}
            <span v-if="cardBBottom">(Bottom card)</span>
          </p>
          <div v-if="bottomButtonB1">
            <button
              type="button"
              class="rounded-full bg-green-600 py-2.5 px-4 text-sm font-semibold text-white shadow-sm hover:bg-green-500 focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-green-600"
              @click="makeCardBBottom"
            >
              Make bottom card
            </button>
          </div>
        </div>
      </div>

      <div>
        <div v-if="cardB2Notification">
          <p class="bg-green-50 mt-2 mb-2 p-2 rounded-lg w-60">
            {{ cardB2Notification }}
            <span v-if="cardBBottom">(Bottom card)</span>
          </p>
          <div v-if="bottomButtonB2">
            <button
              type="button"
              class="rounded-full bg-green-600 py-2.5 px-4 text-sm font-semibold text-white shadow-sm hover:bg-green-500 focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-green-600"
              @click="makeCardBBottom"
            >
              Make bottom card
            </button>
          </div>
        </div>
      </div>
    </div>

    <!-- Card layouts -->
    <div class="mx-auto ml-5 mt-5" v-if="cardABottom || cardBBottom">
      <hr class="mb-5" />
      <div>
        <p>Select a layout for the cards:</p>
        <div class="grid grid-cols-5 mr-2 mb-5">
          <!-- Layout 1-->
          <div
            class="border-2 rounded-lg mr-2 hover:bg-stone-200 hover:cursor-pointer"
            :class="layout1ActiveClass"
            @click="selectLayout(layout1BottomArray, 1)"
          >
            <p>Layout 1</p>
            <span>Bottom card: </span>
            <div id="bottom-card">
              <!-- <svg
                xmlns="http://www.w3.org/2000/svg"
                viewBox="0 0 24 24"
                class="w-6 h-6"
                :fill="bottomCardClass"
              >
                <path
                  fill-rule="evenodd"
                  d="M6.32 2.577a49.255 49.255 0 0111.36 0c1.497.174 2.57 1.46 2.57 2.93V21a.75.75 0 01-1.085.67L12 18.089l-7.165 3.583A.75.75 0 013.75 21V5.507c0-1.47 1.073-2.756 2.57-2.93z"
                  clip-rule="evenodd"
                />
              </svg> -->
              <span>{{ layout1BottomArray }}</span>
            </div>

            <span class="ml-2">Top card: </span>
            <div>
              <svg
                xmlns="http://www.w3.org/2000/svg"
                viewBox="0 0 24 24"
                class="w-6 h-6"
                :fill="topCardClass"
              >
                <path
                  fill-rule="evenodd"
                  d="M6.32 2.577a49.255 49.255 0 0111.36 0c1.497.174 2.57 1.46 2.57 2.93V21a.75.75 0 01-1.085.67L12 18.089l-7.165 3.583A.75.75 0 013.75 21V5.507c0-1.47 1.073-2.756 2.57-2.93z"
                  clip-rule="evenodd"
                />
              </svg>
            </div>
          </div>

          <!-- Layout 2-->
          <div
            class="border-2 rounded-lg mr-2 hover:bg-stone-200 hover:cursor-pointer"
            :class="layout2ActiveClass"
            @click="selectLayout(layout2BottomArray, 2)"
          >
            <p>Layout 2</p>
            <span>Bottom card: </span>
            <div>
              <svg
                xmlns="http://www.w3.org/2000/svg"
                viewBox="0 0 24 24"
                class="w-6 h-6"
                :fill="bottomCardClass"
              >
                <path
                  fill-rule="evenodd"
                  d="M6.32 2.577a49.255 49.255 0 0111.36 0c1.497.174 2.57 1.46 2.57 2.93V21a.75.75 0 01-1.085.67L12 18.089l-7.165 3.583A.75.75 0 013.75 21V5.507c0-1.47 1.073-2.756 2.57-2.93z"
                  clip-rule="evenodd"
                />
              </svg>
              <span>{{ layout2BottomArray }}</span>
            </div>

            <span class="ml-2">Top card: </span>
            <div>
              <svg
                xmlns="http://www.w3.org/2000/svg"
                viewBox="0 0 24 24"
                class="w-6 h-6"
                :fill="topCardClass"
              >
                <path
                  fill-rule="evenodd"
                  d="M6.32 2.577a49.255 49.255 0 0111.36 0c1.497.174 2.57 1.46 2.57 2.93V21a.75.75 0 01-1.085.67L12 18.089l-7.165 3.583A.75.75 0 013.75 21V5.507c0-1.47 1.073-2.756 2.57-2.93z"
                  clip-rule="evenodd"
                />
              </svg>
            </div>
          </div>

          <!-- Layout 3-->
          <div
            class="border-2 rounded-lg mr-2 hover:bg-stone-200 hover:cursor-pointer"
            :class="layout3ActiveClass"
            @click="selectLayout(layout3BottomArray, 3)"
          >
            <p>Layout 3</p>
            <span>Bottom card: </span>
            <div>
              <svg
                xmlns="http://www.w3.org/2000/svg"
                viewBox="0 0 24 24"
                class="w-6 h-6"
                :fill="bottomCardClass"
              >
                <path
                  fill-rule="evenodd"
                  d="M6.32 2.577a49.255 49.255 0 0111.36 0c1.497.174 2.57 1.46 2.57 2.93V21a.75.75 0 01-1.085.67L12 18.089l-7.165 3.583A.75.75 0 013.75 21V5.507c0-1.47 1.073-2.756 2.57-2.93z"
                  clip-rule="evenodd"
                />
              </svg>
              <span>{{ layout3BottomArray }}</span>
            </div>

            <span class="ml-2">Top card: </span>
            <div>
              <svg
                xmlns="http://www.w3.org/2000/svg"
                viewBox="0 0 24 24"
                class="w-6 h-6"
                :fill="topCardClass"
              >
                <path
                  fill-rule="evenodd"
                  d="M6.32 2.577a49.255 49.255 0 0111.36 0c1.497.174 2.57 1.46 2.57 2.93V21a.75.75 0 01-1.085.67L12 18.089l-7.165 3.583A.75.75 0 013.75 21V5.507c0-1.47 1.073-2.756 2.57-2.93z"
                  clip-rule="evenodd"
                />
              </svg>
            </div>
          </div>

          <!-- Layout 4-->
          <div
            class="border-2 rounded-lg mr-2 hover:bg-stone-200 hover:cursor-pointer"
            :class="layout4ActiveClass"
            @click="selectLayout(layout4BottomArray, 4)"
          >
            <p>Layout 4</p>
            <span>Bottom card: </span>
            <div>
              <svg
                xmlns="http://www.w3.org/2000/svg"
                viewBox="0 0 24 24"
                class="w-6 h-6"
                :fill="bottomCardClass"
              >
                <path
                  fill-rule="evenodd"
                  d="M6.32 2.577a49.255 49.255 0 0111.36 0c1.497.174 2.57 1.46 2.57 2.93V21a.75.75 0 01-1.085.67L12 18.089l-7.165 3.583A.75.75 0 013.75 21V5.507c0-1.47 1.073-2.756 2.57-2.93z"
                  clip-rule="evenodd"
                />
              </svg>
              <span>{{ layout4BottomArray }}</span>
            </div>

            <span class="ml-2">Top card: </span>
            <div>
              <svg
                xmlns="http://www.w3.org/2000/svg"
                viewBox="0 0 24 24"
                class="w-6 h-6"
                :fill="topCardClass"
              >
                <path
                  fill-rule="evenodd"
                  d="M6.32 2.577a49.255 49.255 0 0111.36 0c1.497.174 2.57 1.46 2.57 2.93V21a.75.75 0 01-1.085.67L12 18.089l-7.165 3.583A.75.75 0 013.75 21V5.507c0-1.47 1.073-2.756 2.57-2.93z"
                  clip-rule="evenodd"
                />
              </svg>
            </div>
          </div>

          <!-- Layout 5-->
          <div
            class="border-2 rounded-lg mr-2 hover:bg-stone-200 hover:cursor-pointer"
            :class="layout5ActiveClass"
            @click="selectLayout(layout5BottomArray, 5)"
          >
            <p>Layout 5</p>
            <span>Bottom card: </span>
            <div>
              <svg
                xmlns="http://www.w3.org/2000/svg"
                viewBox="0 0 24 24"
                class="w-6 h-6"
                :fill="bottomCardClass"
              >
                <path
                  fill-rule="evenodd"
                  d="M6.32 2.577a49.255 49.255 0 0111.36 0c1.497.174 2.57 1.46 2.57 2.93V21a.75.75 0 01-1.085.67L12 18.089l-7.165 3.583A.75.75 0 013.75 21V5.507c0-1.47 1.073-2.756 2.57-2.93z"
                  clip-rule="evenodd"
                />
              </svg>
              <span>{{ layout5BottomArray }}</span>
            </div>

            <span class="ml-2">Top card: </span>
            <div>
              <svg
                xmlns="http://www.w3.org/2000/svg"
                viewBox="0 0 24 24"
                class="w-6 h-6"
                :fill="topCardClass"
              >
                <path
                  fill-rule="evenodd"
                  d="M6.32 2.577a49.255 49.255 0 0111.36 0c1.497.174 2.57 1.46 2.57 2.93V21a.75.75 0 01-1.085.67L12 18.089l-7.165 3.583A.75.75 0 013.75 21V5.507c0-1.47 1.073-2.756 2.57-2.93z"
                  clip-rule="evenodd"
                />
              </svg>
            </div>
          </div>
        </div>

        <div class="grid grid-cols-5 mr-2 mb-5">
          <!-- Layout 6-->
          <div
            class="border-2 rounded-lg mr-2 hover:bg-stone-200 hover:cursor-pointer"
            :class="layout6ActiveClass"
            @click="selectLayout(layout6BottomArray, 6)"
          >
            <p>Layout 6</p>
            <span>Bottom card: </span>
            <div>
              <svg
                xmlns="http://www.w3.org/2000/svg"
                viewBox="0 0 24 24"
                class="w-6 h-6"
                :fill="bottomCardClass"
              >
                <path
                  fill-rule="evenodd"
                  d="M6.32 2.577a49.255 49.255 0 0111.36 0c1.497.174 2.57 1.46 2.57 2.93V21a.75.75 0 01-1.085.67L12 18.089l-7.165 3.583A.75.75 0 013.75 21V5.507c0-1.47 1.073-2.756 2.57-2.93z"
                  clip-rule="evenodd"
                />
              </svg>
              <span>{{ layout6BottomArray }}</span>
            </div>

            <span class="ml-2">Top card: </span>
            <div>
              <svg
                xmlns="http://www.w3.org/2000/svg"
                viewBox="0 0 24 24"
                class="w-6 h-6"
                :fill="topCardClass"
              >
                <path
                  fill-rule="evenodd"
                  d="M6.32 2.577a49.255 49.255 0 0111.36 0c1.497.174 2.57 1.46 2.57 2.93V21a.75.75 0 01-1.085.67L12 18.089l-7.165 3.583A.75.75 0 013.75 21V5.507c0-1.47 1.073-2.756 2.57-2.93z"
                  clip-rule="evenodd"
                />
              </svg>
            </div>
          </div>

          <!-- Layout 7-->
          <div
            class="border-2 rounded-lg mr-2 hover:bg-stone-200 hover:cursor-pointer"
            :class="layout7ActiveClass"
            @click="selectLayout(layout7BottomArray, 7)"
          >
            <p>Layout 7</p>
            <span>Bottom card: </span>
            <div>
              <svg
                xmlns="http://www.w3.org/2000/svg"
                viewBox="0 0 24 24"
                class="w-6 h-6"
                :fill="bottomCardClass"
              >
                <path
                  fill-rule="evenodd"
                  d="M6.32 2.577a49.255 49.255 0 0111.36 0c1.497.174 2.57 1.46 2.57 2.93V21a.75.75 0 01-1.085.67L12 18.089l-7.165 3.583A.75.75 0 013.75 21V5.507c0-1.47 1.073-2.756 2.57-2.93z"
                  clip-rule="evenodd"
                />
              </svg>
              <span>{{ layout7BottomArray }}</span>
            </div>

            <span class="ml-2">Top card: </span>
            <div>
              <svg
                xmlns="http://www.w3.org/2000/svg"
                viewBox="0 0 24 24"
                class="w-6 h-6"
                :fill="topCardClass"
              >
                <path
                  fill-rule="evenodd"
                  d="M6.32 2.577a49.255 49.255 0 0111.36 0c1.497.174 2.57 1.46 2.57 2.93V21a.75.75 0 01-1.085.67L12 18.089l-7.165 3.583A.75.75 0 013.75 21V5.507c0-1.47 1.073-2.756 2.57-2.93z"
                  clip-rule="evenodd"
                />
              </svg>
            </div>
          </div>

          <!-- Layout 8-->
          <div
            class="border-2 rounded-lg mr-2 hover:bg-stone-200 hover:cursor-pointer"
            :class="layout8ActiveClass"
            @click="selectLayout(layout8BottomArray, 8)"
          >
            <p>Layout 8</p>
            <span>Bottom card: </span>
            <div>
              <svg
                xmlns="http://www.w3.org/2000/svg"
                viewBox="0 0 24 24"
                class="w-6 h-6"
                :fill="bottomCardClass"
              >
                <path
                  fill-rule="evenodd"
                  d="M6.32 2.577a49.255 49.255 0 0111.36 0c1.497.174 2.57 1.46 2.57 2.93V21a.75.75 0 01-1.085.67L12 18.089l-7.165 3.583A.75.75 0 013.75 21V5.507c0-1.47 1.073-2.756 2.57-2.93z"
                  clip-rule="evenodd"
                />
              </svg>
              <span>{{ layout8BottomArray }}</span>
            </div>

            <span class="ml-2">Top card: </span>
            <div>
              <svg
                xmlns="http://www.w3.org/2000/svg"
                viewBox="0 0 24 24"
                class="w-6 h-6"
                :fill="topCardClass"
              >
                <path
                  fill-rule="evenodd"
                  d="M6.32 2.577a49.255 49.255 0 0111.36 0c1.497.174 2.57 1.46 2.57 2.93V21a.75.75 0 01-1.085.67L12 18.089l-7.165 3.583A.75.75 0 013.75 21V5.507c0-1.47 1.073-2.756 2.57-2.93z"
                  clip-rule="evenodd"
                />
              </svg>
            </div>
          </div>

          <!-- Layout 9-->
          <div
            class="border-2 rounded-lg mr-2 hover:bg-stone-200 hover:cursor-pointer"
            :class="layout9ActiveClass"
            @click="selectLayout(layout9BottomArray, 9)"
          >
            <p>Layout 9</p>
            <span>Bottom card: </span>
            <div>
              <svg
                xmlns="http://www.w3.org/2000/svg"
                viewBox="0 0 24 24"
                class="w-6 h-6"
                :fill="bottomCardClass"
              >
                <path
                  fill-rule="evenodd"
                  d="M6.32 2.577a49.255 49.255 0 0111.36 0c1.497.174 2.57 1.46 2.57 2.93V21a.75.75 0 01-1.085.67L12 18.089l-7.165 3.583A.75.75 0 013.75 21V5.507c0-1.47 1.073-2.756 2.57-2.93z"
                  clip-rule="evenodd"
                />
              </svg>
              <span>{{ layout9BottomArray }}</span>
            </div>

            <span class="ml-2">Top card: </span>
            <div>
              <svg
                xmlns="http://www.w3.org/2000/svg"
                viewBox="0 0 24 24"
                class="w-6 h-6"
                :fill="topCardClass"
              >
                <path
                  fill-rule="evenodd"
                  d="M6.32 2.577a49.255 49.255 0 0111.36 0c1.497.174 2.57 1.46 2.57 2.93V21a.75.75 0 01-1.085.67L12 18.089l-7.165 3.583A.75.75 0 013.75 21V5.507c0-1.47 1.073-2.756 2.57-2.93z"
                  clip-rule="evenodd"
                />
              </svg>
            </div>
          </div>

          <!-- Layout 10-->
          <div
            class="border-2 rounded-lg mr-2 hover:bg-stone-200 hover:cursor-pointer"
            :class="layout10ActiveClass"
            @click="selectLayout(layout10BottomArray, 10)"
          >
            <p>Layout 10</p>
            <span>Bottom card: </span>
            <div>
              <svg
                xmlns="http://www.w3.org/2000/svg"
                viewBox="0 0 24 24"
                class="w-6 h-6"
                :fill="bottomCardClass"
              >
                <path
                  fill-rule="evenodd"
                  d="M6.32 2.577a49.255 49.255 0 0111.36 0c1.497.174 2.57 1.46 2.57 2.93V21a.75.75 0 01-1.085.67L12 18.089l-7.165 3.583A.75.75 0 013.75 21V5.507c0-1.47 1.073-2.756 2.57-2.93z"
                  clip-rule="evenodd"
                />
              </svg>
              <span>{{ layout10BottomArray }}</span>
            </div>

            <span class="ml-2">Top card: </span>
            <div>
              <svg
                xmlns="http://www.w3.org/2000/svg"
                viewBox="0 0 24 24"
                class="w-6 h-6"
                :fill="topCardClass"
              >
                <path
                  fill-rule="evenodd"
                  d="M6.32 2.577a49.255 49.255 0 0111.36 0c1.497.174 2.57 1.46 2.57 2.93V21a.75.75 0 01-1.085.67L12 18.089l-7.165 3.583A.75.75 0 013.75 21V5.507c0-1.47 1.073-2.756 2.57-2.93z"
                  clip-rule="evenodd"
                />
              </svg>
            </div>
          </div>
        </div>
      </div>

      <div>
        Card A array: {{ cardAarray }}
        <span v-if="cardABottom">- - - Bottom card</span>
      </div>
      <div>
        Card B array: {{ cardBarray }}
        <span v-if="cardBBottom">- - - Bottom card</span>
      </div>

      <br />
      <hr />
      <div>
        Bottom card Array: {{ bottomCardArray }} <br />
        Top card Array: {{ topCardArray }}
      </div>

      <hr />
      <div class="mb-5">
        Selection Array: {{ selectedArray }}
        <br />
        Logistics: {{ logisticsCount }}
        <br />
        Improvement: {{ improvementCount }}
        <br />
        Price Increase: {{ increasePriceCount }}
        <br />
        Price Decrease: {{ reducePriceCount }}
        <br />
        Price change: {{ changePrice }}
        <br />
        Research: {{ researchCount }}
        <br />
        Products: {{ productsCount + reducePriceCount }}
        <br />
        Layout Products: {{ layoutProducts }}
        <br />
        Total Products: {{ totalProductsCount }}
      </div>
    </div>

    <div class="w-200">
      <div class="m-12 grid grid-cols-6 gap-4">
        <div class="col-start-1 col-span-2 bg-yellow-300">01</div>
      </div>
    </div>
  </main>
</template>

<style>
.class0 {
  background-color: transparent;
  /*font-size: x-small;*/
}

.class1 {
  background-image: url("../assets/logistics_icon.svg");
  background-color: #3c95d1;
  font-size: x-small;
}

.class2 {
  background-image: url("../assets/product_icon.svg");
  background-color: black;
  font-size: x-small;
  color: gray;
}

.class3 {
  background-image: url("../assets/pricing_increase_icon.svg");
  background-color: #db4125;
  font-size: x-small;
}

.class4 {
  background-image: url("../assets/product_price_icon.svg");
  background-color: gray;
  font-size: x-small;
}

.class5 {
  background-image: url("../assets/improvement_icon.svg");
  background-color: #f6af54;
  font-size: x-small;
}

.class6 {
  background-image: url("../assets/research_icon.svg");
  background-color: #8d7fb3;
  font-size: x-small;
}

.activeLayout {
  background-color: aquamarine;
  border: 3px solid green;
}
</style>
