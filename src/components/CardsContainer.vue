<template>
  <section>
    <div class="profile-card">
      <div class="user-details">
        <img
          class="avatar-img"
          src="../assets/images/image-jeremy.png"
          alt="user profile picture"
        />
        <div class="user-name">
          <p>Report for</p>
          <div class="name">Jeremy Robson</div>
        </div>
      </div>
      <div class="navigation-buttons">
        <button
          :class="{ active: activeButton === 'daily' }"
          @click="selectDaily('daily')"
        >
          Daily
        </button>
        <button
          :class="{ active: activeButton === 'weekly' }"
          @click="selectWeekly('weekly')"
        >
          Weekly
        </button>
        <button
          :class="{ active: activeButton === 'monthly' }"
          @click="selectMonthly('monthly')"
        >
          Monthly
        </button>
      </div>
    </div>

    <div
      v-for="activity in activities"
      :key="activity.title"
      class="card"
      :class="activity.title"
    >
      <div class="card-front">
        <div class="activity">
          <p>{{ activity.title }}</p>
          <img src="../assets/images/icon-ellipsis.svg" alt="icon ellipsis" />
        </div>
        <div class="hours">
          <p class="current-hours">
            {{ activity.timeframes[currentTimeframe].current }}hrs
          </p>
          <p class="previous-hours">
            {{ timeframe }} -
            {{ activity.timeframes[currentTimeframe].previous }}hrs
          </p>
        </div>
      </div>
    </div>
  </section>
  <the-attribution></the-attribution>
</template>

<script>
import ActivityData from "../assets/data.json";
import TheAttribution from "./TheAttribution.vue";
export default {
  components: {
    TheAttribution,
  },
  data() {
    return {
      currentTimeframe: "daily",
      activeButton: "daily",
      timeframe: "Yesterday",
      activities: ActivityData,
    };
  },
  methods: {
    selectDaily() {
      this.activeButton = "daily";
      this.timeframe = "Yesterday";
      this.currentTimeframe = "daily";
    },
    selectWeekly() {
      this.activeButton = "weekly";
      this.timeframe = "Last Week";
      this.currentTimeframe = "weekly";
    },
    selectMonthly() {
      this.activeButton = "monthly";
      this.timeframe = "Last Month";
      this.currentTimeframe = "monthly";
    },
  },
};
</script>

<style lang="scss">
$radius: 17px;
$padding: 1.5rem;

@mixin card {
}

section {
  font-family: "Rubik", sans-serif;
  width: 100%;
  margin: auto;
  display: grid;
  grid-gap: 1.5rem;
  grid-template-columns: repeat(auto-fit, minmax(255px, 1fr));
  .profile-card {
    background-color: hsl(235, 46%, 20%);
    border-radius: 20px 20px $radius $radius;
    .user-details {
      border-radius: $radius;
      display: flex;
      align-items: center;
      padding: $padding;
      background-color: hsl(246, 80%, 60%);
      .avatar-img {
        width: 4rem;
        border-radius: 50%;
        border: 2px solid #fff;
        background-color: #fff;
        margin-right: 1rem;
      }
      .user-name {
        > p {
          font-size: 13px;
          color: hsl(236, 100%, 87%);
        }
        .name {
          color: #fff;
          font-size: 1.5rem;
          font-weight: 300;
        }
      }
    }
    .navigation-buttons {
      padding: $padding;
      display: flex;
      justify-content: space-between;
      align-items: center;
      button {
        color: hsl(235, 45%, 61%);
        font-size: 18px;
        border: unset;
        background-color: unset;
        cursor: pointer;
        &:hover {
          color: #fff;
        }
      }
      .active {
        color: #fff;
      }
    }
  }
  .card {
    border-radius: $radius $radius 20px 20px;
    padding-top: 2.3rem;
    background-repeat: no-repeat;
    background-position: 92% -0.6rem;
    background-size: 4.5rem;
    .card-front {
      width: 100%;
      background-color: hsl(235, 46%, 20%);
      padding: $padding;
      border-radius: $radius;
      height: 100%;
      cursor: pointer;
      &:hover {
        background-color: lighten(hsl(235, 46%, 20%), 10%);
      }
      .activity {
        display: flex;
        align-items: center;
        justify-content: space-between;
        margin-bottom: 0.5rem;
        > p {
          font-size: 18px;
          color: #fff;
        }
      }
      .hours {
        display: flex;
        align-items: center;
        justify-content: space-between;
        .current-hours {
          font-size: 2rem;
          color: #fff;
          font-weight: 300;
          margin-bottom: 0.5rem;
        }
        .previous-hours {
          color: hsl(236, 100%, 87%);
        }
      }
    }
  }
  .Work {
    background-color: hsl(15, 100%, 70%);
    background-image: url(../assets/images/icon-work.svg);
  }
  .Play {
    background-color: hsl(195, 74%, 62%);
    background-image: url(../assets/images/icon-play.svg);
    background-position: 92% -0.3rem;
  }
  .Study {
    background-color: hsl(348, 100%, 68%);
    background-image: url(../assets/images/icon-study.svg);
    background-position: 92% -0.3rem;
  }
  .Exercise {
    background-color: hsl(145, 58%, 55%);
    background-image: url(../assets/images/icon-exercise.svg);
    background-position: 92% 0;
    background-size: 5rem;
  }
  .Social {
    background-color: hsl(264, 64%, 52%);
    background-image: url(../assets/images/icon-social.svg);
    background-position: 92% -1rem;
  }
  .Selfcare {
    background-color: hsl(43, 84%, 65%);
    background-image: url(../assets/images/icon-self-care.svg);
    background-size: 3.8rem;
  }
  @media only screen and (min-width: 610px) {
    margin: unset;
    .profile-card {
      display: flex;
      flex-direction: column;
      grid-row: 1 / 3;
      .user-details {
        flex-basis: 70%;
        display: block;
        padding: 1.7rem;
        .avatar-img {
          width: 5.5rem;
          margin-bottom: 1.5rem;
        }
        .user-name {
          width: 80%;
          margin-bottom: 2rem;
          > p {
            font-size: 1rem;
          }
          .name {
            font-size: 2.6rem;
          }
        }
      }
      .navigation-buttons {
        flex-basis: 30%;
        flex-direction: column;
        align-items: flex-start;
        button:not(:last-child) {
          margin-bottom: 1.2rem;
        }
      }
    }
    .card {
      padding-top: 3rem;
      .card-front {
        .activity {
          margin-bottom: 1rem;
        }
        .hours {
          display: block;
          .current-hours {
            font-size: 3.2rem;
          }
          .previous-hours {
            margin-bottom: 0.7rem;
          }
        }
      }
    }
  }
}
</style>
