<template>
  <div>
    <!-- Banner -->
    <div class="banner text-white">
      <img src="/curve.png" alt="" />
      <div class="text-xl h-16 px-5 flex justify-between items-center">
        <div>Coremenus</div>
      </div>
      <div class="w-full flex flex-col mt-10 text-center justify-center">
        <h2 class="text-4xl md:text-5xl">Let's Go</h2>
        <h1 class="font-bold text-5xl md:text-6xl">Contactless</h1>
      </div>
    </div>
    <section>
      <!-- Email -->
      <div
        v-if="sent"
        class="email rounded-lg flex flex-col items-center mt-10 md:w-160 right-0 left-0 mx-auto py-5 px-10 text-center"
      >
        <img src="/check.svg" alt="" />
        <h1 class="font-semibold">Done!</h1>
        <h2 class="text-sm font-light">We will notify you when we launch.</h2>
      </div>
      <form
        v-else
        class="email rounded-lg flex flex-col items-center mt-10 md:w-160 right-0 left-0 mx-auto py-5 px-10 text-center"
        @submit.prevent="submit"
      >
        <h1 class="font-semibold">Get Notified when we launch</h1>
        <h2 class="text-sm font-light">
          Submit your Email Address Below and we will notify you when we launch
        </h2>
        <input
          v-model="email"
          type="email"
          required
          class="mt-3 rounded-md p-1.5 w-full"
          placeholder="someone@example.com"
        />
        <button
          class="bg-gradient-to-r p-1.5 from-blue-600 to-pink-600 w-full hover:to-pink-800 hover:from-blue-800 rounded-md mt-3 text-white"
          type="submit"
        >
          Submit
        </button>
        <p v-if="error" class="text-red-500 text-center">
            An error has occured, please try again
        </p>
      </form>

      <!-- Features -->
      <section class="px-5 md:w-200 right-0 left-0 mx-auto">
        <!-- Customizable -->
        <div class="flex flex-col md:flex-row items-center mt-10">
          <div class="text-center md:text-right">
            <h1 class="text-2xl font-bold">Customizable Page</h1>
            <p class="font-light">
              Coremenus dashboard offers you full control over themes and
              branding
            </p>
          </div>
          <img class="w-80 h-80" src="/1.jpg" alt="" />
        </div>

        <div class="flex flex-col md:flex-row-reverse items-center mt-10">
          <div class="text-center md:text-left">
            <h1 class="text-2xl font-bold">Live Orders</h1>
            <p class="font-light">
              Recieve incoming orders without a waiter in your dashboard
            </p>
          </div>
          <img class="w-80 h-80" src="/3.jpg" alt="" />
        </div>

        <div class="flex flex-col md:flex-row items-center mt-10">
          <div class="text-center md:text-right">
            <h1 class="text-2xl font-bold">Multilingual</h1>
            <p class="font-light">
              Serve a wider range of customers by having multiple languages in
              your menu
            </p>
          </div>
          <img class="w-80 h-80" src="/2.jpg" alt="" />
        </div>

        <div class="flex flex-col md:flex-row-reverse items-center mt-10">
          <div class="text-center md:text-left">
            <h1 class="text-2xl font-bold">Analytics</h1>
            <p class="font-light">
              Know how your business is doing with Real-Time Analytics
            </p>
          </div>
          <img class="w-80 h-80" src="/4.jpg" alt="" />
        </div>
      </section>

      <section
        class="flex flex-col text-center bg-gradient-to-b from-indigo-200 to-pink-200 md:w-200 rounded-lg right-0 left-0 mx-auto p-10 gap-10"
      >
        <h1 class="font-bold text-3xl text-opacity-80">Why Coremenus</h1>
        <div class="flex flex-col md:flex-row gap-4 justify-center">
          <div
            class="bg-white p-10 rounded-md flex flex-col items-center gap-3"
          >
            <img class="w-7 h-7" src="/check.svg" alt="" />
            <div>
              Reduce
              <p>Printing Costs</p>
            </div>
          </div>
          <div
            class="bg-white p-10 rounded-md flex flex-col items-center gap-3"
          >
            <img class="w-7 h-7" src="/check.svg" alt="" />
            <div>
              Reduce
              <p>Operation Load</p>
            </div>
          </div>
          <div
            class="bg-white p-10 rounded-md flex flex-col items-center gap-3"
          >
            <img class="w-7 h-7" src="/check.svg" alt="" />
            <div>
              Updates
              <p>With Few Clicks</p>
            </div>
          </div>
        </div>
      </section>
    </section>

    <div class="h-20 text-center flex items-center justify-center">
      © 2022 Coremenus, LLC. All Rights Reserved.
    </div>
  </div>
</template>

<script>
export default {
  name: 'IndexPage',
  data() {
    return {
      email: '',
      sent: false,
      error: false,
    }
  },
  methods: {
    async submit() {
      try {
        await this.$fire.firestore.collection('emails').add({
          email: this.email,
        })
        this.email = ''
        this.sent = true
      } catch (error) {
        this.error = true
      }
    },
  },
}
</script>

<style>
html {
  font-family: 'Poppins', sans-serif !important;
}
.email {
  background: #e7edf3;
}
.banner {
  position: relative;
  margin: 0;
  padding: 0;
  background: #eb01a5;
  background-image: url('/background.jpg');
  background-image: linear-gradient(#eb01a5a9, #d1363194),
    url('/background.jpg');
  background-size: cover;
  background-position: center;
  width: 100%;
  height: 50vh;
}

.banner img {
  position: absolute;
  bottom: 0;
  margin-bottom: -2px;
  width: 100%;
}
</style>
