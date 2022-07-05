<script>
import feather from "feather-icons";
import EventRelatedEvents from "../../components/events/EventRelatedEvents.vue";
export default {
  scrollToTop: true,
  data: () => {
    return {
      // @todo
    };
  },
  computed: {
    event() {
      return this.$store.getters.getEventById(this.$route.params.id);
    },
  },
  mounted() {
    feather.replace();
  },
  updated() {
    feather.replace();
  },
  components: { EventRelatedEvents },
};
</script>

<template>
  <div class="container mx-auto">
    <!-- Check if there are events and then load -->
    <div v-if="event">
      <!-- Event heading and meta info -->
      <div>
        <p
          class="
            font-general-medium
            text-left text-3xl
            sm:text-4xl
            font-bold
            text-primary-dark
            dark:text-primary-light
            mt-14
            sm:mt-20
            mb-7
          "
        >
          {{ event.title }}
        </p>
        <div class="flex">
          <div class="flex items-center mr-10">
            <i
              data-feather="clock"
              class="w-4 h-4 text-ternary-dark dark:text-ternary-light"
            ></i>
            <span
              class="
                font-general-medium
                ml-2
                leading-none
                text-primary-dark
                dark:text-primary-light
              "
              >{{ event.publishDate }}</span
            >
          </div>
          <div class="flex items-center">
            <i
              data-feather="tag"
              class="w-4 h-4 text-ternary-dark dark:text-ternary-light"
            ></i>
            <span
              class="
                font-general-medium
                ml-2
                leading-none
                text-primary-dark
                dark:text-primary-light
              "
              >{{ event.tag }}</span
            >
          </div>
        </div>
      </div>

      <!-- Event gallery -->
      <div class="grid grid-cols-1 sm:grid-cols-3 sm:gap-10 mt-12">
        <div
          class="mb-10 sm:mb-0"
          v-for="eventImage in event.eventImages"
          :key="eventImage.id"
        >
          <img
            :src="eventImage.img"
            class="rounded-xl cursor-pointer shadow-lg sm:shadow-none"
          />
        </div>
      </div>

      <!-- Event info -->
      <div class="block sm:flex gap-0 sm:gap-10 mt-14">
        <!-- Single event left section details -->
        <div class="w-full sm:w-1/3 text-left">
          <!-- Single event client details -->
          <div class="mb-7">
            <p
              class="
                font-general-medium
                text-2xl text-secondary-dark
                dark:text-secondary-light
                mb-2
              "
            >
              {{ event.clientTitle }}
            </p>
            <ul class="leading-loose">
              <li
                v-for="info in event.companyInfos"
                :key="info.id"
                class="
                  font-general-regular
                  text-ternary-dark
                  dark:text-ternary-light
                "
              >
                <span>{{ info.title }}: </span>
                <a
                  href="#"
                  :class="
                    info.title == 'Website' || info.title == 'Phone'
                      ? 'hover:underline cursor-pointer'
                      : ''
                  "
                  aria-label="Event website and phone"
                  >{{ info.details }}</a
                >
              </li>
            </ul>
          </div>

          <!-- Single event objectives -->
          <div class="mb-7">
            <p
              class="
                font-general-medium
                text-2xl text-ternary-dark
                dark:text-ternary-light
                mb-2
              "
            >
              {{ event.objectivesTitle }}
            </p>
            <p
              class="
                font-general-regular
                text-primary-dark
                dark:text-ternary-light
              "
            >
              {{ event.objectivesDetails }}
            </p>
          </div>

          <!-- Single event technologies -->
          <div class="mb-7">
            <p
              class="
                font-general-medium
                text-2xl text-ternary-dark
                dark:text-ternary-light
                mb-2
              "
            >
              {{ event.techTitle }}
            </p>
            <p
              class="
                font-general-regular
                text-primary-dark
                dark:text-ternary-light
              "
            >
              {{ event.technologies.join(", ") }}
            </p>
          </div>

          <!-- Single event social sharing -->
          <div>
            <p
              class="
                font-general-medium
                text-2xl text-ternary-dark
                dark:text-ternary-light
                mb-2
              "
            >
              {{ event.socialTitle }}
            </p>
            <div class="flex items-center gap-3 mt-5">
              <a
                v-for="social in event.socialSharings"
                :key="social.id"
                :href="social.url"
                target="__blank"
                aria-label="Share Event"
                class="
                  bg-ternary-light
                  dark:bg-ternary-dark
                  text-gray-400
                  hover:text-primary-dark
                  dark:hover:text-primary-light
                  p-2
                  rounded-lg
                  shadow-sm
                  duration-500
                "
                ><i
                  :data-feather="social.icon"
                  class="w-4 lg:w-5 h-4 lg:h-5"
                ></i
              ></a>
            </div>
          </div>
        </div>

        <!-- Single event right section details -->
        <div class="w-full sm:w-2/3 text-left mt-10 sm:mt-0">
          <p
            class="
              font-general-medium
              text-primary-dark
              dark:text-primary-light
              text-2xl
              font-bold
              mb-7
            "
          >
            {{ event.detailsTitle }}
          </p>
          <p
            v-for="eventDetail in event.eventDetails"
            :key="eventDetail.id"
            class="
              font-general-regular
              mb-5
              text-lg text-ternary-dark
              dark:text-ternary-light
            "
          >
            {{ eventDetail.details }}
          </p>
        </div>
      </div>

      <!-- Event related events -->
      <EventRelatedEvents />
    </div>

    <!-- Load not found components if no event found -->
    <div v-else class="font-general-medium container mx-auto text-center">
      <h1>No events yet</h1>
    </div>
  </div>
</template>

<style lang="scss" scoped></style>
