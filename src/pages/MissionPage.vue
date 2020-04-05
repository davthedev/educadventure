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
      <p style="white-space:pre-line;">{{presentSlide.text}}</p>
    </div>

    <div v-if="showAssignment">

      <q-card class="q-mt-xl vertical-middle submit-card" v-if="!noSubmission">
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

      <q-card class="q-mt-xl vertical-middle submit-card" v-if="noSubmission">
        <q-card-section>

        <div class="text-h6">Finish this mission</div>

        </q-card-section>

        <q-card-section>

        <p>You reached the last step of this mission. Now, move on to the next one!</p>

        <div class="q-gutter-y-md column" style="max-width: 300px; margin: auto;">
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
          <q-btn v-if="n == currentSlideBaseOne && showSlide" round unelevated color="accent" :key="k">{{n}}</q-btn>
          <q-btn v-else round flat color="white"  :key="k" @click="activateSlide(n - 1)">{{n}}</q-btn>
        </template>
        <q-btn v-if="showAssignment" round unelevated color="accent"  :key="k" icon="assignment" @click="activateShowAssignment"></q-btn>
        <q-btn v-else round flat color="white" :key="k" icon="assignment" @click="activateShowAssignment"></q-btn>
      </div>

    </q-page-sticky>
  </q-page>
</template>

<style lang="sass">

.course-page-wrapper
  background-color: $blue-grey-9
  background-image: repeating-linear-gradient(45deg, transparent, transparent 35px, rgba(255,255,255,.02) 35px, rgba(255,255,255,.02) 70px)

    
    
  color: #fff

.doc-page
  padding: 16px 46px
  font-weight: 400
  max-width: 900px
  margin-left: auto
  margin-right: auto

.my-course-page
  font-size: 16px

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

      noSubmission: false,

      missionId: 0,

      slides: [
        {
          title: "Placeholder",
          text: "Slide 1 text",
          img: 'https://placeimg.com/500/300/nature',
        },
      ],

      allDecks: [


        // MISSION 00 --------------------------------------------------------
        [
          

          {
            title: "Here we go!",
            text: "It has been several weeks since the virus struck. The adults seem to be affected, but not we, the young. Also, I decided to take matters into my own hands. To prevent them from getting the virus, my parents are locked inside and it is up to me to protect the house from now on. Finally, there are lots of solutions to do better than previous generations!",
            img: 'statics/contents/emptystreet.jpg',
          },
          {
            title: "How to play",
            text: "With confinement, my apartment is my area of ​​experience, play and learning. Right now, only four areas are of interest to me, but other places will become important afterwards.",
            img: 'statics/contents/appart5.png',
          },
          {
            title: "How to play",
            text: "My main task is to make sure there is no indoor contamination. I don't want my family to be affected by this virus! My contamination indicator tells me if my apartment is safe or not.",
            img: 'statics/contents/screenshot_down_spread.png',
          },
          {
            title: "How to play",
            text: "If I'm not careful, germs will come home and the risk of contamination of my family will increase!",
            img: 'statics/contents/screenshot_down_spread.png',
          },
          {
            title: "How to play",
            text: "The more knowledge I have, the better I can fight the virus. My progress is represented by the knowledge indicator. With each new level of knowledge, I develop new specific talents.",
            img: 'statics/contents/screenshot_down_lvl.png',
          },
          {
            title: "How to play",
            text: "Creating a better world is a team effort. The improvement indicator shows how well the other young people and I are succeeding in changing the world. The higher this indicator, the more resources we have to complete our missions.",
            img: 'statics/contents/screenshot_down_goodwill.png',
          },
          {
            title: "How to play",
            text: "In case of problems, the menu gives me access to each day's news. These are written in the logbook. I can see on the map all missions that are yet to do and those already completed.",
            img: 'statics/contents/screenshot_up.png',
          },
          {
            title: "The current situation",
            text: "Today, the stores have been raided! All the hygiene products are gone! If I don't find a solution quickly, the contamination will quickly return to my home.",
            img: null,
          },

        ],

        // MISSION 01 --------------------------------------------------------
        [
          

          {
            title: "Soap Making",
            text: "The first solution to avoid contamination of the apartment is to wash your hands. Difficult to do without soap! So I have to stock up on soap for the next few days.",
            img: 'statics/contents/1-1A_1-SoapBar.png',
          },
          {
            title: "Goal",
            text: "Make your own soap using the protocol provided in the mission statement.",
            img: null,
          },
          {
            title: "Required skills",
            text: "Follow a protocol of experience\nPrecision and dexterity\nUnderstanding chemical reactions\nUnderstand what an atom and a molecule are",
            img: 'statics/contents/1-1A_3-Chemistry.jpg',
          },
          {
            title: "Material and reading prerequisites",
            text: "Chapter 14 of the manual Science of nature 9th - 11th: Microbes, useful or harmful?\n450g of oil (vegetal or olive)\n250g of butter (karite, coco, …)\n302 g of water\nIce or cold water\nEssential oil (optional)",
            img: 'statics/contents/1-1A_4-Oil.png',
          },
          {
            title: "Protocol",
            text: "1) Melt the butter in a bain-marie\n2) Prepare a container with cold water or ice. \n3) With the help of a parent, gloves, glasses and on a patio or beside a window poor the lye in a container of water. \n4) Put that container in ice or cold water and leave it cool to 29°c beside the window.\n5) Add the oil to the butter and heat it to 29°c\n6) Slowly pour the lye solution into the oil/butter solution while mixing with a spatula (Do not pour the oil/butter into the lye)\n7) Mix until it becomes like a paste and add a few drop of essential oil (optional)\n8) Pour it into the mold, let dry and harden for 24-48hour\n9) Unmold!",
            img: null,
          },
          {
            title: "To hand over",
            text: "A photo of your soaps with your personal indicator\nA photo of you during the mixing\nA short reflection of 50 words answering the question:\n How can soap dislodge fats?",
            img: null,
          },

        ]

        ,

        // MISSION 02 --------------------------------------------------------
        [
          

          {
            title: "Making the invisible grow",
            text: "I need to make sure my apartment is clean, but I need to identify the places that are still full of microbes. I need to take samples and make them grow to observe them!",
            img: 'statics/contents/2-1B_1-AgarBacteria.jpeg',
          },
          {
            title: "Goal",
            text: "Verify the presence of microorganism on different surface using the protocol provided in the mission statement.",
            img: null,
          },
          {
            title: "Required skills",
            text: "Follow a protocol of experience\nPrecision, patience and dexterity\nUnderstanding what a microbe is and their reproduction\nKnow the differences between bacteria, fungi and virus",
            img: 'statics/contents/bacteria.jpeg',
          },
          {
            title: "Material and reading prerequisites",
            text: "Chapter 14 of the manual Science of nature 9th - 11th: Microbes, useful or harmful?\n450g of oil (vegetal or olive)\n250g of butter (karite, coco, …)\n302 g of water\nIce or cold water\nEssential oil (optional)",
            img: 'statics/contents/2-1B_4-Agar.jpeg',
          },
          {
            title: "Protocol",
            text: "1) Pour 1 cup of water into the mixing bowl and make it boil.\n2) While the water is heating, add 1tbsp of agar or 12g of gelatine, the bouillon cube and 2 tsp of sugar.\n3) Let the solution cool a bit and pour it into the shallow container to have a thickness of around 0.5cm per container.\n4) Let the solution cool and solidify.\n5) When solidified, take a q-tip, brush a random surface with it and swab the q-tip onto your petri dish.\n6) Put the plates on your counter and wait a few days for the colony to grow.\n7) Observe the colonies obtained",
            img: null,
          },
          {
            title: "To hand over",
            text: "A photo of your petri dish\nA top 3 of the surfaces with the most microorganisms\nA short reflection of 50 words answering the question: How to differentiate fungi, bacteria and virus on the petri dish.",
            img: null,
          },

        ],
        // MISSION 03 --------------------------------------------------------
        [
          {
            title: "Mission 3",
            text: "Mission 3",
            img: 'https://placeimg.com/500/300/nature',
          },
        ],
        // MISSION 04 --------------------------------------------------------
        [
          {
            title: "Mission 4",
            text: "Mission 4",
            img: 'https://placeimg.com/500/300/nature',
          },
        ],
        // MISSION 05 --------------------------------------------------------
        [
          {
            title: "Fridge exploration",
            text: "During isolation, you have to know what are the rare commodities. So I'm going to check what is in my fridge and see where these foods come from!",
            img: 'statics/contents/5-2A_1-Fridge.jpg',
          },
          {
            title: "Goal",
            text: "Identify the contents of your fridge, sort the food, recognize where it comes from and the season",
            img: null,
          },
          {
            title: "Required skills",
            text: "Make a list\nKnow the seasonal fruits\nRead a card\nAnnotate a card",
            img: null,
          },
          {
            title: "Material and reading prerequisites",
            text: "World map (attached)\nManual: chapter on the seasons\nFilled fridge",
            img: 'statics/contents/5-2A_4-FruitWorldMap.jpeg',
          },
          {
            title: "Protocol",
            text: "Draw three columns on your page / open a spreadsheet if you prefer to work on the computer.\nIn the first column, write down all the fruits and vegetables present in your home (fridge, cupboard).\nIn the second column, write the seasons during which these fruits normally grow.\nIn the third column, enter the country of origin of these fruits and vegetables.\nThen take the map of the world and draw a line on it between each country listed and Switzerland.",
            img: 'statics/contents/5-2A_5-DocumentSample.PNG',
          },
          {
            title: "To hand over",
            text: "A photo of the fruits and vegetables grouped on the table, with your personal indicator\nA photo of the completed world map\nA short reflection of 100 words answering the question: Why choose seasonal vegetables or not?",
            img: null,
          },
        ],
        // MISSION 06 --------------------------------------------------------
        [
          {
            title: "Mens sana",
            text: "Hygiene is one thing, but you also have to keep me in shape! I set myself some daily physical challenges!",
            img: 'statics/contents/6-7A_1-Cup.png',
          },
          {
            title: "Goal",
            text: "Stay in shape, discover indoor games",
            img: null,
          },
          {
            title: "Required skills",
            text: "Keep in balance\nMove your legs",
            img: null,
          },
          {
            title: "Material and reqding prerequisites",
            text: "Non-slippery floor\nString\nWatch or stopwatch",
            img: 'statics/contents/6-7A_4-Chronometer.jpg',
          },
          {
            title: "Protocol",
            text: "With your string, draw a circle the size of your left foot on the ground.\nBalance yourself on the foot in the circle and hold your hands behind your back.\nTry to keep your balance for 30 seconds, without moving the string with your foot.\nWhen you have successfully completed this step with both feet, try the same thing but with your eyes closed.",
            img: 'statics/contents/6-7A_5-BalanceOneLeg.jpg',
          },
          {
            title: "To hand over",
            text: "A photo of the foot surrounded by string\nA photo of you during the exercise\nA short reflection of 50 words answering the question: What is the hardest? Eyes open or closed? Left or right foot? Why?",
            img: null,
          },
        ],
        // MISSION 07 --------------------------------------------------------
        [
          {
            title: "Mission 7",
            text: "Mission 7",
            img: 'https://placeimg.com/500/300/nature',
          },
        ],
        // MISSION 08 --------------------------------------------------------
        [
          {
            title: "Mission 8",
            text: "Mission 8",
            img: 'https://placeimg.com/500/300/nature',
          },
        ],
        // MISSION 09 --------------------------------------------------------
        [
          {
            title: "Bread Experiment",
            text: "Now I have my soap and I know how to identify the places full of microorganisms in my apartment. Now, I just need to know if my homemade soap is effective to get rid of the microorganisms!",
            img: 'statics/contents/9-1C_1-SoapWashing.jpg',
          },
          {
            title: "Goal",
            text: "Demonstrate the effciency of your homemade soap to defeat the microorganisms.",
            img: null,
          },
          {
            title: "Required skills",
            text: "Follow a protocol of experience\nPrecision, patience and dexterity\nUnderstanding what a microbe is and their reproduction\nKnow the difference between bacteria, fungi and virus\nUnderstand what an atom and a molecule are",
            img: 'statics/contents/bacteria.jpeg',
          },
          {
            title: "Material and reading prerequisites",
            text: "Chapter 14 of the manual Science of nature 9th - 11th: Microbes, useful or harmful?\n2 bread slices\n2 airtight containers\nHomemade soap\nKitchen pliers\nOptional : Foldscope (1€ microscope)",
            img: 'statics/contents/9-1C_4-Bread.jpg',
          },
          {
            title: "Protocol",
            text: "1) Wash the pliers and the airtight containers with soap and water.\n2) Put 1 bread slice in each airtight container with the pliers\n3) Put on hand on one piece of bread for a few second then close the container\n4) Wash the hand you just used with water and soap for 20 seconds at least\n5) Put your washed hand on the second slice of bread and close the container\n6) Let the container on your counter for 4-7 days without opening them\n7) Observe the difference between the two slices of bread",
            img: null,
          },
          {
            title: "To hand over",
            text: "A photo of your 2 slices of bread\nIs your soap effective to get rid of the microorganisms? Why?\nIf you don’t have any soap, what can you use to clean your hand?\nA short reflection of 50 words answering the question: How does soap protect your parents from microbes?",
            img: null,
          },
        ],
        // MISSION 10 --------------------------------------------------------
        [
          {
            title: "Keep the bond",
            text: "If I can no longer go to the library, I can still ask questions of the elderly who are still healthy. This is an opportunity to write a letter to my grandparents to ask them for news and tell about the routine that I have put in place!",
            img: 'statics/contents/10-3A_1-Grandparents.jpg',
          },
          {
            title: "Goal",
            text: "To express oneself clearly in writing, to create social and intellectual ties",
            img: null,
          },
          {
            title: "Required skills",
            text: "To write\nFormulate ideas\nTo ask questions\nDescribe a day\n",
            img: null,
          },
          {
            title: "Protocol",
            text: "In your text, take the time to greet your grandparents and find out how they are.\nThen describe their routine that you have set up and ask them for their opinion on it.\nAsk them for their own routine and offer to criticize it in a future letter.\nFind out if they have ever experienced confinements and if so, what are their tips to facilitate this period.",
            img: null,
          },
          {
            title: "To hand over",
            text: "The text of the letter sent to your grandparents\nTheir response when you receive it.",
            img: null,
          },
        ],
        // MISSION 11 --------------------------------------------------------
        [
          {
            title: "Mission 11",
            text: "Mission 11",
            img: 'https://placeimg.com/500/300/nature',
          },
        ],
        // MISSION 12 --------------------------------------------------------
        [
          {
            title: "Mission 12",
            text: "Mission 12",
            img: 'https://placeimg.com/500/300/nature',
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
      //this.presentSlide.text = "<p>" + this.slides[num].text.replace(/\n/g, '<br />') + "</p>"
    },

    activateShowAssignment: function() {
      this.showSlide = false
      this.showAssignment = true
    },

    finishMission: function() {
      this.markMissionComplete()
      this.$router.push('/')
    },

    markMissionComplete: function() {
      let completed_missions = this.$gameglobals.completed_missions
      completed_missions[this.missionId] = true
      this.$gameglobals.completed_missions = completed_missions
    }
  },
  mounted() {
    const missionId = this.$route.params.id
    this.currentSlideNum = 0
    this.slides = this.allDecks[missionId]
    this.missionId = missionId
    if (missionId == 0)
      this.noSubmission = true
    this.initSlideDeck()
    this.displaySlide()
  }
}
</script>
