<template>
  <div class="container-fluid">
    <div class="d-flex">
      <svg
        class="fa fa-search"
        xmlns="http://www.w3.org/2000/svg"
        width="24"
        height="24"
        viewBox="0 0 24 24"
        fill="none"
      >
        <path
          d="M11.5 21C16.7467 21 21 16.7467 21 11.5C21 6.25329 16.7467 2 11.5 2C6.25329 2 2 6.25329 2 11.5C2 16.7467 6.25329 21 11.5 21Z"
          stroke="#546076"
          stroke-width="1.5"
          stroke-linecap="round"
          stroke-linejoin="round"
        />
        <path
          d="M22 22L20 20"
          stroke="#546076"
          stroke-width="1.5"
          stroke-linecap="round"
          stroke-linejoin="round"
        />
      </svg>
      <input
        type="text"
        v-model="searchQuery"
        class="form-input"
        placeholder="Search themes here"
      />
      <DropdownOptions :options="options[0]" />
    </div>

    <div class="d-flex theme-scroll" style="margin: 120px 0px 0px 0px">
      <div class="d-flex arrow">
        <p class="counter_location">{{ filteredThemes.length + " Themes" }}</p>
        <button class="scroll-button left" @click="scrollLeft">
          <img
            :src="
              require(isScrollAtStart
                ? '@/assets/images/arrow1.svg'
                : '@/assets/images/arrow2.svg')
            "
            alt="left-arrow"
            class="left-arrow"
            id="left-arrow-img"
            @contextmenu="preventContextMenu"
            draggable="false"
          />
        </button>
        <button class="scroll-button right" @click="scrollRight">
          <img
            :src="
              require(isScrollAtEnd
                ? '@/assets/images/arrow1.svg'
                : '@/assets/images/arrow2.svg')
            "
            alt="right-arrow"
            class="right-arrow"
            id="right-arrow-img"
            @contextmenu="preventContextMenu"
            draggable="false"
          />
        </button>
      </div>

      <ul class="cards">
        <div
          v-for="(theme, index) in filteredThemes"
          :key="index"
          class="d-inline-block"
          style="margin-right: 65px; text-align: center; width: 450px"
        >
          <label class="form-check-label mb-4">{{ theme.theme_name }}</label>
          <li class="card">
            <div class="loading">
              <img
                :src="theme.image"
                data-bs-toggle="modal"
                :data-bs-target="'#exampleModal-' + index"
                alt=""
                style="max-width: 100%"
                @contextmenu="preventContextMenu"
                draggable="false"
              />
            </div>

            <!-- Modal -->
            <div
              class="modal fade"
              :id="'exampleModal-' + index"
              tabindex="-1"
              aria-labelledby="exampleModalLabel"
              aria-hidden="true"
            >
              <div class="modal-dialog">
                <div
                  class="modal-content"
                  data-bs-toggle="modal"
                  :data-bs-target="'#exampleModal-' + index"
                >
                  <div class="modal-body">
                    <img
                      :src="theme.image"
                      alt=""
                      style="max-width: 100%"
                      @contextmenu="preventContextMenu"
                      draggable="false"
                    />
                  </div>
                </div>
              </div>
            </div>
          </li>
          <div class="d-flex">
            <div
              class="under_devlopment_circle"
              v-if="theme.tags && theme.tags.includes('')"
            >
              <p
                class="font_style"
                style="
                  color: var(--dark-red-color);
                  text-align: center;
                  padding-top: 16px;
                "
              >
                under development
              </p>
            </div>
            <div
              class="theme_leve"
              v-if="theme.tags && theme.tags.includes('free')"
            >
              <p class="font_style">free</p>
            </div>
            <div
              class="theme_leve red"
              v-if="theme.tags && theme.tags.includes('plus')"
            >
              <p class="font_style">plus</p>
            </div>
            <div
              class="theme_leve green"
              v-if="theme.tags && theme.tags.includes('pro')"
            >
              <p class="font_style">pro</p>
            </div>
          </div>

          <div class="d-flex" v-if="theme.tags && !theme.tags.includes('')">
            <button
              :id="'install-' + index"
              class="installingButton"
              style="background: var(--second-blue-color); border: none"
              @click="myFunction(theme)"
            >
              install
            </button>
            <button
              :id="'installed-' + index"
              class="installingButton"
              style="
                background: var(--light-gray);
                display: none;
                border: none;
                color: var(--white-color);
              "
            >
              installed
            </button>
            <button
              class="edit_previewButton"
              data-bs-toggle="modal"
              :data-bs-target="'#exampleModal-' + index"
            >
              preview
            </button>
            <button
              :id="'edit-' + index"
              class="edit_previewButton"
              style="display: none"
            >
              edit
            </button>
          </div>
        </div>
      </ul>
    </div>
  </div>
</template>

<script>
// Import the DropdownOptions component
import DropdownOptions from "./DropdownOptions.vue";

export default {
  name: "HelloWorld",
  props: {
    msg: String,
  },
  components: {
    DropdownOptions,
  },
  data() {
    return {
      searchQuery: "", // New data property for search query
      isScrollAtStart: true,
      isScrollAtEnd: false,
      // Dropdown options data
      themes: [
        {
          theme_name: "Defult theme",
          tags: ["free"],
          image: require("@/assets/images/card_images/Defult_theme.jpg"),
        },
        {
          theme_name: "glasses store",
          tags: ["free", "plus", "pro"],
          image: require("@/assets/images/card_images/glasses_store.jpg"),
        },
        {
          theme_name: "animal theme",
          tags: [""],
          image: require("@/assets/images/card_images/animal_store.jpg"),
        },
        {
          theme_name: "book theme",
          tags: ["free", "plus", "pro"],
          image: require("@/assets/images/card_images/book_theme.jpg"),
        },
        {
          theme_name: "hotels theme",
          tags: ["free"],
          image: require("@/assets/images/card_images/booking_hotels.jpg"),
        },
        {
          theme_name: "cards theme",
          tags: ["free", "plus", "pro"],
          image: require("@/assets/images/card_images/card_store.jpg"),
        },
        {
          theme_name: "packaging theme",
          tags: ["free", "pro"],
          image: require("@/assets/images/card_images/Cardboard_store.jpg"),
        },
        {
          theme_name: "coffee theme",
          tags: ["plus", "pro"],
          image: require("@/assets/images/card_images/coffee.jpg"),
        },
        {
          theme_name: "digital file theme",
          tags: ["free", "plus", "pro"],
          image: require("@/assets/images/card_images/Digital_File.jpg"),
        },
        {
          theme_name: "electronics store theme",
          tags: ["pro"],
          image: require("@/assets/images/card_images/electronics_store.jpg"),
        },
        {
          theme_name: "meat shop theme",
          tags: ["plus"],
          image: require("@/assets/images/card_images/meat_shop.jpg"),
        },
        {
          theme_name: "Nuts shop",
          tags: ["free", "plus", "pro"],
          image: require("@/assets/images/card_images/Nuts_shop.jpg"),
        },
        {
          theme_name: "Flower shop",
          tags: [""],
          image: require("@/assets/images/card_images/Flower_shop.jpg"),
        },
        {
          theme_name: "cars theme",
          tags: ["free", "plus", "pro"],
          image: require("@/assets/images/card_images/car.jpg"),
        },
        {
          theme_name: "petrol and diesel theme",
          tags: ["free", "pro"],
          image: require("@/assets/images/card_images/petrol.jpg"),
        },
        {
          theme_name: "Pharmacy store theme",
          tags: ["free"],
          image: require("@/assets/images/card_images/pharmacy_store.jpg"),
        },
        {
          theme_name: "plumbing store theme",
          tags: ["free", "pro"],
          image: require("@/assets/images/card_images/plumbing_store.jpg"),
        },
        {
          theme_name: "resturants theme",
          tags: ["free", "plus", "pro"],
          image: require("@/assets/images/card_images/resturants.jpg"),
        },
        {
          theme_name: "clothes theme",
          tags: ["plus", "pro"],
          image: require("@/assets/images/card_images/clothes.jpg"),
        },
        {
          theme_name: "Integrated store theme",
          tags: ["free", "plus"],
          image: require("@/assets/images/card_images/Integrated_store.jpg"),
        },
        {
          theme_name: "Sport store theme",
          tags: ["free", "plus", "pro"],
          image: require("@/assets/images/card_images/sport_store.jpg"),
        },
        {
          theme_name: "Supermarket theme",
          tags: ["free", "plus", "pro"],
          image: require("@/assets/images/card_images/Supermarket.jpg"),
        },
        {
          theme_name: "vegetable theme",
          tags: ["free", "plus"],
          image: require("@/assets/images/card_images/vegetable_theme.jpg"),
        },
        {
          theme_name: "Watches theme",
          tags: [""],
          image: require("@/assets/images/card_images/watches.jpg"),
        },
        {
          theme_name: "Makeup store theme",
          tags: ["free"],
          image: require("@/assets/images/card_images/Makeup_store.jpg"),
        },
        {
          theme_name: "resturant theme",
          tags: [""],
          image: require("@/assets/images/card_images/Resturant.jpg"),
        },
        {
          theme_name: "gold store theme",
          tags: ["free", "pro"],
          image: require("@/assets/images/card_images/gold.jpg"),
        },
        {
          theme_name: "hony shop theme",
          tags: ["plus", "pro"],
          image: require("@/assets/images/card_images/honey_shop.jpg"),
        },
        {
          theme_name: "home services theme",
          tags: ["free", "plus"],
          image: require("@/assets/images/card_images/home_services.jpg"),
        },
      ],
      options: [
        { option1: "free plan", option2: "plus plan", option3: "pro plan" },
      ],
    };
  },
  computed: {
    filteredThemes() {
      // Filter the themes based on the search query
      return this.themes.filter((theme) =>
        theme.theme_name.toLowerCase().includes(this.searchQuery.toLowerCase())
      );
    },
  },
  mounted() {
    this.updateScrollStatus();
    // Add the scroll event listener to update scroll status
    const cardsContainer = document.querySelector(".cards");
    cardsContainer.addEventListener("scroll", this.updateScrollStatus);
  },

  beforeUnmount() {
    // Clean up the scroll event listener
    const cardsContainer = document.querySelector(".cards");
    cardsContainer.removeEventListener("scroll", this.updateScrollStatus);
  },
  methods: {
    updateScrollStatus() {
      const cardsContainer = document.querySelector(".cards");
      if (cardsContainer) {
        this.isScrollAtStart = cardsContainer.scrollLeft === 0;
        const maxScrollPosition =
          cardsContainer.scrollWidth - cardsContainer.clientWidth;
        this.isScrollAtEnd = cardsContainer.scrollLeft >= maxScrollPosition;
      }
    },
    myFunction(theme) {
      const installButton = document.getElementById(
        "install-" + this.filteredThemes.indexOf(theme)
      );
      const installedButton = document.getElementById(
        "installed-" + this.filteredThemes.indexOf(theme)
      );
      const editButton = document.getElementById(
        "edit-" + this.filteredThemes.indexOf(theme)
      );

      installButton.style.display = "none";
      installedButton.style.display = "";
      editButton.style.display = "";
    },

    scrollLeft() {
      const cardsContainer = document.querySelector(".cards");
      const cardWidth = cardsContainer.querySelector(".card").clientWidth; // Get the width of a single card
      const scrollAmount = cardWidth + 10; // Adjust this value based on your card spacing

      // Calculate the new scroll position after scrolling to the left
      const newScrollPosition = Math.max(
        cardsContainer.scrollLeft - scrollAmount,
        0
      );
      cardsContainer.scrollLeft = newScrollPosition;
    },

    scrollRight() {
      const cardsContainer = document.querySelector(".cards");
      const cardWidth = cardsContainer.querySelector(".card").clientWidth; // Get the width of a single card
      const scrollAmount = cardWidth + 10; // Adjust this value based on your card spacing

      // Calculate the maximum scroll position to prevent scrolling too far
      const maxScrollPosition =
        cardsContainer.scrollWidth - cardsContainer.clientWidth;
      // Calculate the new scroll position after scrolling to the right
      const newScrollPosition = Math.min(
        cardsContainer.scrollLeft + scrollAmount,
        maxScrollPosition
      );
      cardsContainer.scrollLeft = newScrollPosition;
    },
    preventContextMenu(event) {
      event.preventDefault();
    },
  },
};
</script>

<style>
@import url("https://fonts.googleapis.com/css2?family=Poppins:wght@400;500;700&display=swap");

.fa-search {
  position: absolute;
  margin: 58px 0px 0px 12px;
}

/* Styling for form input */
.form-input {
  text-indent: 39px;
  border-radius: 10px;
  border: 1px solid var(--placeholder);
  width: 490px;
  height: 60px;
  margin: 40px 0px 10px 0px;
  background-color: var(--dark-blue-color);
}

.form-input:focus {
  outline: none;
  border-color: var(--second-blue-color);
  color: var(--white-color);
}

.form-check-label {
  color: var(--white-color);
  font-size: 18px;
  font-weight: 500;
}

.theme_leve {
  width: 101px;
  height: 40px;
  border-radius: 20px;
  background: var(--orange-color);
  margin: 15px 10px 0px 0px;
}

.font_style {
  color: var(--white-color);
  font-size: 16px;
  font-weight: 500;
  line-height: normal;
  text-align: center;
  padding-top: 7px;
}

.installingButton {
  width: 120px;
  height: 60px;
  border-radius: 10px;
  font-size: 20px;
  margin: 20px 45px 0px 0px;
  color: var(--white-color);
}

.edit_previewButton {
  width: 120px;
  height: 60px;
  border-radius: 10px;
  font-size: 20px;
  margin: 20px 45px 0px 0px;
  background: var(--dark-blue-color);
  border: 2px solid var(--second-blue-color);
  color: var(--second-blue-color);
}

.under_devlopment_circle {
  border: 1px solid var(--dark-red-color);
  border-radius: 10px;
  width: 450px;
  height: 60px;
  margin-top: 25px;
  color: var(--dark-red-color);
}

.cards {
  display: flex;
  padding: 25px 0px;
  list-style: none;
  overflow-x: scroll;
  scroll-snap-type: x mandatory;
}

.card {
  border-radius: 12px;
  scroll-snap-align: start;
  transition: all 0.2s;
  background-color: transparent;
  width: 450px;
  height: 800px;
  overflow-y: auto; /* Enable vertical scrolling for taller content */
  border: 1px solid var(--second-blue-color);
}

.card::-webkit-scrollbar {
  width: 6px;
}

.card::-webkit-scrollbar-thumb,
.card::-webkit-scrollbar-track {
  border-radius: 92px;
}

.card::-webkit-scrollbar-thumb {
  background: var(--second-blue-color);
}

.card::-webkit-scrollbar-track {
  background: var(--thumb);
}

.card:not(:last-child) {
  margin-right: 10px;
}

.cards::-webkit-scrollbar {
  height: 12px;
  display: none;
}

.cards::-webkit-scrollbar-thumb,
.cards::-webkit-scrollbar-track {
  border-radius: 92px;
}

.cards::-webkit-scrollbar-thumb {
  background: var(--dark-red-color);
}

.cards::-webkit-scrollbar-track {
  background: var(--thumb);
}

.theme-scroll {
  width: 1490px;
}

.green {
  background-color: var(--green-color-bg);
}
.red {
  background-color: rgba(216, 85, 58, 0.5);
}

.scroll-button {
  position: absolute;
  top: 50%;
  transform: translateY(-50%);
  background: none;
  border: none;
  cursor: pointer;
}

.scroll-button.left {
  left: 10px;
}
.scroll-button {
  margin: -530px 0px 0px 1380px;
}
.scroll-button.right {
  left: 70px;
}
.counter_location {
  margin: 0px 0px 0px 1372px;
  position: absolute;
  height: 26px;
  width: 160px;
  color: var(--placeholder);
  font-size: large;
  padding-top: 7px;
  font-weight: 500;
}

.left-arrow,
.right-arrow {
  border-radius: 50%;
  width: 50px;
  height: 50px;
  cursor: pointer;
  transition: all 0.3s ease 0s;
  position: relative;
  transition: all 0.5s cubic-bezier(0.19, 1, 0.22, 1);
}

#right-arrow-img {
  transform: translate(-50%, -50%) rotate(0deg);
}

#left-arrow-img {
  transform: translate(-50%, -50%) rotate(180deg);
}

.arrow {
  position: relative;
}

.loading {
  background: transparent url(@/assets/images/loader.gif) center center
    no-repeat;
  width: 450;
  height: 800px;
}

.modal-content {
  width: 800px;
  margin-left: -150px;
  background: none;
  border: none;
}
</style>
