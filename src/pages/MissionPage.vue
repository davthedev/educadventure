<template>
  <q-page class="course-page-wrapper">

    <div class="doc-page my-course-page">

    <div v-if="showSlide">
      <h2 class="q-mb-lg q-mt-sm">{{presentSlide.title}}</h2>
      <q-img v-if="presentSlide.img != null"
        :src="presentSlide.img" contain
        style="max-width: 800px; max-height: 300px;"
        class="q-mb-md"
      />
      <p>{{presentSlide.text}}</p>
    </div>

    <div v-if="showAssignment">

      <q-card class="q-mt-xl vertical-middle submit-card">
        <q-card-section>

        <div class="text-h6">Upload your work</div>

        </q-card-section>

        <q-card-section>

        <p>When you are done with your work, simply use this form to upload it. Your teacher will correct it and give you feedback.</p>

        <div class="q-gutter-y-md column" style="max-width: 300px; margin: auto;">
          <q-file  color="white" clearable outlined v-model="fileModel" label="Send your file here" class="q-mt-md q-mb-md">

          <template v-slot:prepend>
            <q-icon name="attach_file" />
          </template>
          </q-file>
          <q-btn
            rounded unelevated
            size="22px"
            class="q-px-xl q-py-xs"
            color="green-13"
            label="FINISH"
            icon="check" style="border-radius: 44px"
            @click="finishMission"
          />
        </div>

        </q-card-section> 
      </q-card>

    </div>

    </div>

    <q-page-sticky expand position="bottom" :offset="[0, 48]">
    
      <div>
        <template v-for="(n, k) in maxPagination">
          <q-btn v-if="n == currentSlideBaseOne && showSlide" round unelevated color="white" textColor="black" :key="k">{{n}}</q-btn>
          <q-btn v-else round flat color="white"  :key="k" @click="activateSlide(n - 1)">{{n}}</q-btn>
        </template>
        <q-btn v-if="showAssignment" round unelevated color="positive"  :key="k" icon="assignment" @click="activateShowAssignment"></q-btn>
        <q-btn v-else round flat color="white" :key="k" icon="assignment" @click="activateShowAssignment"></q-btn>
      </div>

    </q-page-sticky>
  </q-page>
</template>

<style lang="sass">

.course-page-wrapper
  background-color: $blue-grey-9
  //background-image: repeating-linear-gradient(45deg, transparent, transparent 35px, rgba(255,255,255,.02) 35px, rgba(255,255,255,.02) 70px)

    
    
  color: #fff

.doc-page
  padding: 16px 46px
  font-weight: 300
  max-width: 900px
  margin-left: auto
  margin-right: auto

.my-course-page h2
  text-align: center

.submit-card
  color: white
  background-color: $cyan-8

</style>

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

      missionId: 0,

      slides: [
        {
          title: "Placeholder",
          text: "Slide 1 text",
          img: 'https://placeimg.com/500/300/nature',
        },
      ],

      allDecks: [


        // MISSION 01 --------------------------------------------------------
        [
          

          {
            title: "Mission 1",
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
            img: 'https://placeimg.com/500/300/nature',
          },
          {
            title: "Slide 4 title",
            text: "Nulla congue ante, et laoreet est pretium et. Duis molestie id turpis ut commodo. Praesent vehicula metus quis libero rutrum, eget lacinia ante scelerisque. Fusce nibh odio, lacinia non ante sit amet, elementum feugiat eros. Nunc enim nisi, lobortis sit amet ligula eget, facilisis tempor lacus. Nunc faucibus fermentum mi sed fermentum. Cras fringilla nunc vel dui fermentum, ut malesuada urna malesuada. Maecenas malesuada urna vel turpis fringilla blandit. Ut pharetra molestie nibh. Integer pellentesque, massa nec blandit consectetur, orci quam pulvinar est, at ultricies mauris nisl non ipsum. Fusce malesuada tempor feugiat. ",
            img: null,
          },

        ],

        // MISSION 02 --------------------------------------------------------
        [
          

          {
            title: "Second mission",
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
            img: 'https://placeimg.com/500/300/nature',
          },
          {
            title: "Slide 4 title",
            text: "Nulla congue ante, et laoreet est pretium et. Duis molestie id turpis ut commodo. Praesent vehicula metus quis libero rutrum, eget lacinia ante scelerisque. Fusce nibh odio, lacinia non ante sit amet, elementum feugiat eros. Nunc enim nisi, lobortis sit amet ligula eget, facilisis tempor lacus. Nunc faucibus fermentum mi sed fermentum. Cras fringilla nunc vel dui fermentum, ut malesuada urna malesuada. Maecenas malesuada urna vel turpis fringilla blandit. Ut pharetra molestie nibh. Integer pellentesque, massa nec blandit consectetur, orci quam pulvinar est, at ultricies mauris nisl non ipsum. Fusce malesuada tempor feugiat. Now, mission 2 is over!",
            img: null,
          },

        ]


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
      this.activateSlide(0)
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
    },

    finishMission: function() {
      // TODO Mark as finished

      this.$router.push('/')
    }
  },
  mounted() {
    const missionId = this.$route.params.id
    this.currentSlideNum = 0
    this.slides = this.allDecks[missionId]
    this.missionId = missionId
    this.initSlideDeck()
    this.displaySlide()
  }
}
</script>
