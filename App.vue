<template>
  <div>
    <div class="card">
      <h1>TRAIN TICKETS</h1>
      <form @submit.prevent="submitData">
        <div>
          <input
            type="text"
            v-model="travelFrom"
            placeholder="From"
            class="place placeFrom"
          />
          <input
            type="text"
            v-model="travelTo"
            placeholder="To"
            class="place placeTo"
          />
        </div>
        <div class="flexRow">
          <div class="radio">
            <input
              type="radio"
              id="secondClass"
              name="travelclass"
              class="border-rad"
              value="2nd class"
              v-model="picked"
            />
            <label for="secondClass" class="radio__label">2nd class</label>
          </div>
          <div class="radio">
            <input
              type="radio"
              id="firstClass"
              name="travelclass"
              class="border-rad"
              value="1st class"
              v-model="picked"
            />
            <label for="firstClass" class="radio__label">1st class</label>
          </div>
        </div>

        <div class="flexRow">
          <div class="flexCol halfWidth">
            <label for="numberOfTickets">Number of tickets:</label>
            <input
              type="number"
              class="border-rad"
              v-model="numTickets"
              min="0"
            />
          </div>
          <div class="flexCol halfWidth">
            <label for="title">Title:</label>
            <select
              id="title"
              name="title"
              class="border-rad"
              v-model="selectedTitle"
            >
              <option value="Mrs">Mrs</option>
              <option value="Miss">Miss</option>
              <option value="Ms">Ms</option>
              <option value="Mr">Mr</option>
              <option value="Mx">Mx</option>
              <option value="Dr">Dr</option>
            </select>
          </div>
        </div>
        <div>
          <div class="flexCol">
            <label for="firstName">First name:</label>
            <input
              type="text"
              name="firstName"
              class="border-rad"
              v-model="fName"
            />
          </div>
          <div class="flexCol">
            <label for="lastName">Last name:</label>
            <input
              type="text"
              name="lastName"
              class="border-rad"
              v-model="lName"
            />
          </div>
          <div class="checkbox">
            <input type="checkbox" name="accept" v-model="checked" />
            <label for="accept">Accept terms and conditions</label>
            <p class="error" :class="errorMsg">
              Please make sure all fields are filled in
            </p>
          </div>
        </div>
        <button>Book tickets</button>
      </form>
    </div>
    <div class="card booking-card" v-if="submittedData.length > 0">
      <h3>Your booking details</h3>
      <p>
        <strong>Full Name:</strong> {{ submittedData[0].title }}
        {{ submittedData[0].fName }}
        {{ submittedData[0].lName }}
      </p>
      <p>
        <strong>From</strong> {{ submittedData[0].travelFrom }}
        <strong>to</strong>
        {{ submittedData[0].travelTo }}
      </p>
      <p><strong>Class:</strong> {{ submittedData[0].class }}</p>
      <p>
        <strong>Number of tickets:</strong> {{ submittedData[0].numTickets }}
      </p>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      travelFrom: "",
      travelTo: "",
      picked: "",
      numTickets: 0,
      selectedTitle: "",
      fName: "",
      lName: "",
      checked: false,
      submittedData: [],
      errorMsg: "hidden",
    };
  },
  methods: {
    submitData() {
      if (
        this.travelFrom.trim() !== "" &&
        this.travelTo.trim() !== "" &&
        this.picked !== "" &&
        this.numTickets > 0 &&
        this.selectedTitle.trim() !== "" &&
        this.fName.trim() !== "" &&
        this.lName.trim() !== "" &&
        this.checked
      ) {
        this.errorMsg = "hidden";
        this.submittedData.push({
          travelFrom: this.travelFrom,
          travelTo: this.travelTo,
          class: this.picked,
          numTickets: this.numTickets,
          title: this.selectedTitle,
          fName: this.fName,
          lName: this.lName,
          checked: this.checked,
        });
      } else {
        this.errorMsg = "visible";
      }
    },
  },
};
</script>

<style>
@import url("https://fonts.googleapis.com/css2?family=Roboto:wght@400;900&display=swap");
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}
body {
  background-color: goldenrod;

  font-family: "Roboto", sans-serif;
}
.card {
  background-color: white;
  max-width: 400px;
  margin: 20px auto;
  text-align: center;
}

h1 {
  background-color: #bdbdbd;
  padding: 1rem;
}

.flexRow {
  display: flex;
}

.flexCol {
  display: flex;
  flex-direction: column;
  text-align: left;
  padding: 1rem;
}
.place {
  width: 50%;
  padding: 1rem;
  border: none;
  text-transform: uppercase;
  color: black;
  font-size: 1.2rem;
  font-weight: bold;
  text-align: center;
}

.placeFrom {
  background-color: rgb(202, 202, 202);
}

.placeTo {
  background-color: #e0e0e0;
}

input,
select {
  padding: 0.8rem;
  border: 1px solid grey;
}

.halfWidth {
  width: 50%;
}

input::placeholder {
  text-transform: uppercase;
  color: black;
  font-size: 1.2rem;
  font-weight: bold;
  text-align: center;
}

.radio {
  width: 50%;
  padding: 1rem;
  text-align: left;
}

.radio__label {
  margin-left: 5px;
}

label {
  font-size: 0.8rem;
}

.checkbox {
  text-align: left;
  padding: 1rem;
}

button {
  width: 90%;

  margin: 1rem;
  padding: 1rem;
  background-color: black;
  color: white;
  letter-spacing: 1.1px;
}

.checkbox label {
  margin-left: 5px;
}

.border-rad {
  border-radius: 5px;
}

.hidden {
  display: none;
}

.visible {
  display: block;
}

.error {
  text-transform: uppercase;
  color: red;
  font-size: 0.8rem;
  margin-top: 0.5rem;
  font-weight: bold;
}

.booking-card {
  padding: 1rem;
}

.booking-card h3,
.booking-card p {
  margin-bottom: 1rem;
}
</style>
