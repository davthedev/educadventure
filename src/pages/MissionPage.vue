<template>
  <q-page class="">
    <div v-if="showSlide">
      <h2>{{presentSlide.title}}</h2>
      <q-img v-if="presentSlide.img != null"
        :src="presentSlide.img" contain
        style="max-width: 800px; max-height: 300px;"
      />
      <p>{{presentSlide.text}}</p>
    </div>

    <div v-if="showAssignment">

      <h2>Upload your work</h2>

      <p>When you are done with your work, simply use this form to upload it. Your teacher will correct it and give you feedback.</p>

      <div class="q-gutter-y-md column" style="max-width: 300px">
        <q-file clearable outlined v-model="fileModel" label="Send your file here">

        <template v-slot:prepend>
          <q-icon name="attach_file" />
        </template>
        </q-file>
        <q-btn
          size="22px"
          class="q-px-xl q-py-xs"
          color="positive"
          label="FINISH"
        />
      </div>

    </div>

    <div class="q-gutter-md">
    
      <div>
      <template v-for="(n, k) in maxPagination">
        <q-btn v-if="n == currentSlideBaseOne && showSlide" round unelevated color="primary"  :key="k">{{n}}</q-btn>
        <q-btn v-else round flat color="primary"  :key="k" @click="activateSlide(n - 1)">{{n}}</q-btn>
      </template>
      <q-btn v-if="showAssignment" round unelevated color="primary"  :key="k" icon="assignment" @click="activateShowAssignment"></q-btn>
      <q-btn v-else round outline color="primary"  :key="k" icon="assignment" @click="activateShowAssignment"></q-btn>
      </div>

    </div>
  </q-page>
</template>

<script>
export default {
  name: 'MissionPage',
  data() {
    return {


      presentSlide: {
        title: "Titre",
        text: "dfmskdfmsldfklds",
        img: 'https://placeimg.com/500/300/nature',
      },

      showSlide: true,
      showAssignment: false,

      currentSlideNum: 2,
      maxPagination: 10,

      fileModel: null,

      slides: [
        {
          title: "Slide 1 title",
          text: "Slide 1 text",
          img: 'https://placeimg.com/500/300/nature',
        },
        {
          title: "Slide 2 title",
          text: " Phasellus ut efficitur justo, sit amet suscipit dolor. Vivamus porttitor pretium nisl ut sagittis. Suspendisse et suscipit nisi. In sit amet quam venenatis turpis consequat pellentesque. Vivamus a massa faucibus, facilisis arcu ac, hendrerit eros. Proin ac eros ut dolor viverra elementum luctus egestas magna. Maecenas augue quam, ultrices et ornare sit amet, aliquam sed arcu. Mauris dignissim mauris nec finibus commodo. Integer malesuada imperdiet convallis. Praesent sollicitudin nulla id libero laoreet, non dictum ligula faucibus. Proin sed sodales eros. Sed quis fermentum ligula, quis rutrum justo. Maecenas feugiat porttitor tortor. Mauris volutpat lectus eget tortor euismod, sit amet bibendum ex accumsan. Etiam dignissim diam eget lacus ullamcorper iaculis. Donec et massa in sapien bibendum consequat. ",
          img: null,
        },
        {
          title: "Slide 3 title",
          text: "Nulla pharetra congue ante, et laoreet est pretium et. Duis molestie id turpis ut commodo. Praesent vehicula metus quis libero rutrum, eget lacinia ante scelerisque. Fusce nibh odio, lacinia non ante sit amet, elementum feugiat eros. Nunc enim nisi, lobortis sit amet ligula eget, facilisis tempor lacus. Nunc faucibus fermentum mi sed fermentum. Cras fringilla nunc vel dui fermentum, ut malesuada urna malesuada. Maecenas malesuada urna vel turpis fringilla blandit. Ut pharetra molestie nibh. Integer pellentesque, massa nec blandit consectetur, orci quam pulvinar est, at ultricies mauris nisl non ipsum. Fusce malesuada tempor feugiat. ",
          img: null,
        },
        {
          title: "Slide 4 title",
          text: "Nulla congue ante, et laoreet est pretium et. Duis molestie id turpis ut commodo. Praesent vehicula metus quis libero rutrum, eget lacinia ante scelerisque. Fusce nibh odio, lacinia non ante sit amet, elementum feugiat eros. Nunc enim nisi, lobortis sit amet ligula eget, facilisis tempor lacus. Nunc faucibus fermentum mi sed fermentum. Cras fringilla nunc vel dui fermentum, ut malesuada urna malesuada. Maecenas malesuada urna vel turpis fringilla blandit. Ut pharetra molestie nibh. Integer pellentesque, massa nec blandit consectetur, orci quam pulvinar est, at ultricies mauris nisl non ipsum. Fusce malesuada tempor feugiat. ",
          img: null,
        },
      ]
    }
  },
  computed: {
    currentSlideBaseOne: function() {
      return this.currentSlideNum + 1
    }
  },
  methods: {
    initSlideDeck() {
      this.maxPagination = this.slides.length
      this.currentSlideNum = 0
    },
    
    activateSlide: function(num) {
      this.showSlide = true
      this.showAssignment = false
      this.currentSlideNum = num
      this.presentSlide = this.slides[num]
    },

    activateShowAssignment: function() {
      this.showSlide = false
      this.showAssignment = true
    }
  },
  mounted() {
    this.currentSlideNum = 0
    this.initSlideDeck()
    this.displaySlide()
  }
}
</script>
