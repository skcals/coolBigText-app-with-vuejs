<template>
  <div class="home">
    <!-- navbar -->
    <nav class="navbar navbar-expand navbar-dark nav-background justify-content-between">
      <div href="/" class="navbar-brand">Cool Big Text</div>
      <div class>
        <a href="https://github.com/coolBigText-app-with-vuejs" target="_blank">
          <img src="../assets/github-logo.png" class="github-logo" alt>
          <span class="text-white ml-2">Skcals</span>
        </a>
      </div>
    </nav>

    <div class="container main-content mt-4">
      <div class="row">
        <div class="col-md-3 p-3" style="background:#3fada3;">
          <h3 class="text-light">Fonts</h3>
          <hr>
          <div class="list-scroller">
            <ul class="list-group">
              <li
                v-for="(font, index) in fonts"
                :class="[  fontName == font ?'active-font':'' ,'list-group-item', 'p-2', 'pl-3'  ]"
                :key="index"
                @click="changeFont(font)"
              >{{font}}</li>
            </ul>
          </div>
        </div>
        <div class="col-md-9 bg-light p-3">
          <div class="p-4">
            <input
              type="text"
              v-model="text"
              placeholder="type here..."
              class="form-control"
              @input="changeText()"
            >
          </div>
          <br>
          <h3 class="select-text">
            Your Text :-
            <code>{{text}}</code>
          </h3>
          <br>

          <pre v-if="hardCodeText">
 ________   ________   ________   ___               _________   _______       ___    ___  _________   
|\   ____\ |\   __  \ |\   __  \ |\  \             |\___   ___\|\  ___ \     |\  \  /  /||\___   ___\ 
\ \  \___| \ \  \|\  \\ \  \|\  \\ \  \            \|___ \  \_|\ \   __/|    \ \  \/  / /\|___ \  \_| 
 \ \  \     \ \  \\\  \\ \  \\\  \\ \  \                \ \  \  \ \  \_|/__   \ \    / /      \ \  \  
  \ \  \____ \ \  \\\  \\ \  \\\  \\ \  \____            \ \  \  \ \  \_|\ \   /     \/        \ \  \ 
   \ \_______\\ \_______\\ \_______\\ \_______\           \ \__\  \ \_______\ /  /\   \         \ \__\
    \|_______| \|_______| \|_______| \|_______|            \|__|   \|_______|/__/ /\ __\         \|__|
                                                                             |__|/ \|__|              
                                                                                                      
                                                                                                      
  </pre>
          <pre>{{funnyText}}</pre>
          <textarea v-model="funnyText" cols="0" rows="0" ref="selectText" class="hide-textarea"></textarea>
          <button
            class="copy-text"
            v-if=" !hardCodeText"
            @click="copyToClipboard()"
          >{{!copy?"Copy-to-Clipboard":"Copied !"}}</button>
        </div>
      </div>
    </div>
  </div>
</template>


<script>
import axios from "axios";
export default {
  name: "home",
  data() {
    return {
      funnyText: "",
      figlet: "figlet",
      text: "Cool Text",
      fontName: "3D-ASCII",
      hardCodeText: true,
      copy: false,
      fonts: [
        "1Row",
        "3-D",
        "3D Diagonal",
        "3D-ASCII",
        "3x5",
        "4Max",
        "5 Line Oblique",
        "Acrobatic",
        "Alligator2",
        "Alpha",
        "Alphabet",
        "AMC 3 Line",
        "AMC 3 Liv1",
        "AMC AAA01",
        "AMC Neko",
        "AMC Razor",
        "AMC Razor2",
        "AMC Slash",
        "AMC Slider",
        "AMC Thin",
        "AMC Tubes",
        "AMC Untitled",
        "ANSI Shadow",
        "Arrows",
        "ASCII New Roman",
        "Avatar",
        "B1FF",
        "Banner",
        "Banner3-D",
        "Banner3",
        "Banner4",
        "Barbwire",
        "Basic",
        "Bear",
        "Bell",
        "Benjamin",
        "Big Chief",
        "Big Money-ne",
        "Big Money-nw",
        "Big Money-se",
        "Big Money-sw",
        "Big",
        "Bigfig",
        "Binary",
        "Block",
        "Blocks",
        "Bloody",
        "Bolger",
        "Braced",
        "Bright",
        "Broadway KB",
        "Broadway",
        "Bubble",
        "Bulbhead",
        "Caligraphy",
        "Caligraphy2",
        "Calvin S",
        "Cards",
        "Catwalk",
        "Chiseled",
        "Chunky",
        "Coinstak",
        "Cola",
        "Colossal",
        "Computer",
        "Contessa",
        "Contrast",
        "Cosmike",
        "Crawford",
        "Crawford2",
        "Crazy",
        "Cricket",
        "Cursive",
        "Cyberlarge",
        "Cybermedium",
        "Cybersmall",
        "Cygnet",
        "DANC4",
        "Dancing Font",
        "Decimal",
        "Def Leppard",
        "Delta Corps Priest 1",
        "Diamond",
        "Diet Cola",
        "Digital",
        "Doh",
        "Doom",
        "DOS Rebel",
        "Dot Matrix",
        "Double Shorts",
        "Double",
        "Dr Pepper",
        "DWhistled",
        "Efti Chess",
        "Efti Font",
        "Efti Italic",
        "Efti Piti",
        "Efti Robot",
        "Efti Wall",
        "Efti Water",
        "Electronic",
        "Elite",
        "Epic",
        "Fender",
        "Filter",
        "Fire Font-k",
        "Fire Font-s",
        "Flipped",
        "Flower Power",
        "Four Tops",
        "Fraktur",
        "Fun Face",
        "Fun Faces",
        "Fuzzy",
        "Georgi16",
        "Georgia11",
        "Ghost",
        "Ghoulish",
        "Glenyn",
        "Goofy",
        "Gothic",
        "Graceful",
        "Gradient",
        "Graffiti",
        "Greek",
        "Heart Left",
        "Heart Right",
        "Henry 3D",
        "Hex",
        "Hieroglyphs",
        "Hollywood",
        "Horizontal Left",
        "Horizontal Right",
        "ICL-1900",
        "Impossible",
        "Invita",
        "Isometric1",
        "Isometric2",
        "Isometric3",
        "Isometric4",
        "Italic",
        "Ivrit",
        "Jacky",
        "Jazmine",
        "Jerusalem",
        "JS Block Letters",
        "JS Bracket Letters",
        "JS Capital Curves",
        "JS Cursive",
        "JS Stick Letters",
        "Katakana",
        "Kban",
        "Keyboard",
        "Knob",
        "Konto Slant",
        "Konto",
        "Larry 3D 2",
        "Larry 3D",
        "LCD",
        "Lean",
        "Letters",
        "Lil Devil",
        "Line Blocks",
        "Linux",
        "Lockergnome",
        "Madrid",
        "Marquee",
        "Maxfour",
        "Merlin1",
        "Merlin2",
        "Mike",
        "Mini",
        "Mirror",
        "Mnemonic",
        "Modular",
        "Morse",
        "Morse2",
        "Moscow",
        "Mshebrew210",
        "Muzzle",
        "Nancyj-Fancy",
        "Nancyj-Improved",
        "Nancyj-Underlined",
        "Nancyj",
        "Nipples",
        "NScript",
        "NT Greek",
        "NV Script",
        "O8",
        "Octal",
        "Ogre",
        "Old Banner",
        "OS2",
        "Patorjk-HeX",
        "Patorjk's Cheese",
        "Pawp",
        "Peaks Slant",
        "Peaks",
        "Pebbles",
        "Pepper",
        "Poison",
        "Puffy",
        "Puzzle",
        "Pyramid",
        "Rammstein",
        "Rectangles",
        "Red Phoenix",
        "Relief",
        "Relief2",
        "Reverse",
        "Roman",
        "Rot13",
        "Rotated",
        "Rounded",
        "Rowan Cap",
        "Rozzo",
        "Runic",
        "Runyc",
        "S Blood",
        "Santa Clara",
        "Script",
        "Serifcap",
        "Shadow",
        "Shimrod",
        "Short",
        "SL Script",
        "Slant Relief",
        "Slant",
        "Slide",
        "Small Caps",
        "Small Isometric1",
        "Small Keyboard",
        "Small Poison",
        "Small Script",
        "Small Shadow",
        "Small Slant",
        "Small Tengwar",
        "Small",
        "Soft",
        "Speed",
        "Spliff",
        "Stacey",
        "Stampate",
        "Stampatello",
        "Standard",
        "Star Strips",
        "Star Wars",
        "Stellar",
        "Stforek",
        "Stick Letters",
        "Stop",
        "Straight",
        "Stronger Than All",
        "Sub-Zero",
        "Swamp Land",
        "Swan",
        "Sweet",
        "Tanja",
        "Tengwar",
        "Term",
        "Test1",
        "The Edge",
        "Thick",
        "Thin",
        "THIS",
        "Thorned",
        "Three Point",
        "Ticks Slant",
        "Ticks",
        "Tiles",
        "Tinker-Toy",
        "Tombstone",
        "Train",
        "Trek",
        "Tsalagi",
        "Tubular",
        "Twisted",
        "Two Point",
        "Univers",
        "USA Flag",
        "Varsity",
        "Wavy",
        "Weird",
        "Wet Letter",
        "Whimsy",
        "Wow"
      ]
    };
  },

  methods: {
    changeText: function() {
      axios
        .get(
          `https://figlet-api.herokuapp.com/figlet/?text=${this.text}&font=${
            this.fontName
          }`
        )
        .then(res => {
          this.hardCodeText = false;
          this.funnyText = res.data;
        })
        .catch(err => console.log("err..."));
    },
    changeFont: function(font) {
      this.loading = true;
      this.fontName = font;
      this.copy = false;
      this.changeText();
    },
    copyToClipboard: function() {
      this.copy = true;
      const copyText = this.$refs.selectText.select();
      document.execCommand("copy");
    }
  }
};
</script>


<style lang="css">
body {
  background: #eee !important;
}
pre {
  font-family: monospace !important;
}

.main-content {
  border: 1px solid rgba(0, 0, 0, 0.3);
}

.nav-background {
  background: #56a0c1 !important;
}

.github-logo {
  width: 30px;
  height: 30px;
}
ul li {
  cursor: pointer;
}
.active-font {
  background: #56a0c1 !important;
  color: #fff;
}
.hide-textarea {
  position: absolute;
  left: -9999px;
}

button.copy-text {
  position: absolute;
  bottom: 10px;
  right: 10px;
  background: #3fada3 !important;
  color: #fff;
  padding: 10px 20px;
  border: none;
  border-radius: none;
  cursor: pointer;
}

/* scrollbar */

.list-scroller {
  height: 550px;
  overflow-y: scroll;
  overflow-x: hidden;
}

::-webkit-scrollbar {
  width: 10px;
}
::-webkit-scrollbar-track {
  background: #eeeeee;
}
::-webkit-scrollbar-thumb {
  background: #56a0c1;
}
</style>


