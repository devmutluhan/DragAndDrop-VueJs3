<template>
  <v-container fluid>
    <v-card
      v-for="lineData in selectedData"
      :key="lineData.id"
      class="elevation-0"
      @drop="onDropData($event, lineData)"
      @dragover.prevent
      @dragenter.prevent
    >
      <v-col
        @mouseover="mouseHoverIn(lineData)"
        @mouseleave="mouseHoverOut(lineData)"
        @dragstart="handleDragStart($event, lineData)"
        draggable="true"
        class="pt-8"
      >
        <v-row
          align="center"
          justify="center"
          class="border-bottom"
          v-if="
            hoverDataLine.hoverId == lineData.id && hoverDataLine.hover == true
          "
        >
          <span class="icon-container">
            <v-icon
              icon="mdi-plus"
              @click.prevent="addLine(lineData)"
              variant="text"
              size="small"
            ></v-icon>
            <v-icon icon="mdi-dock-window" size="small" variant="text"></v-icon>
            <v-icon
              icon="mdi-close"
              variant="text"
              size="small"
              @click="deleteLine(lineData)"
            ></v-icon>
          </span>
        </v-row>
        <v-row
          :class="
            hoverDataLine.hoverId == lineData.id && hoverDataLine.hover == true
              ? `border-bottom`
              : ''
          "
        >
          <v-col
            v-for="(colomnData, index) in lineData.kolon"
            :key="index"
            draggable="true"
            class="pb-0"
            @dragstart="handleDragStart($event, colomnData)"
          >
            <v-icon
              icon="mdi-dock-window"
              style="position: fixed"
              v-if="
                hoverDataColomn.hoverId == colomnData.id &&
                hoverDataColomn.hover == true &&
                hoverDataLine.hoverId == lineData.id
              "
            ></v-icon>
            <v-card
              class="text-center"
              variant="plain"
              style="border: dashed"
              @mouseover="mouseHoverIn(colomnData)"
              @mouseleave="mouseHoverOut(colomnData)"
            >
              <v-icon icon="mdi-plus" variant="text" size="3vh"></v-icon>
            </v-card>
          </v-col>
        </v-row>
      </v-col>
    </v-card>
    <v-card
      class="mx-auto elevation-0 text-center mt-16"
      width="80%"
      height="38vh"
      variant="plain"
      style="border: dashed"
    >
      <v-card-text>
        <add-component @addClick="emit" v-if="!currentPage"></add-component>
        <row-structure
          v-if="currentPage"
          :sectionData="sectionData"
          @addClick="emit"
        ></row-structure>
      </v-card-text>
    </v-card>
  </v-container>
</template>

<script>
import AddComponent from "./AddComponent.vue";
import RowStructure from "./RowStructure.vue";

export default {
  name: "HomePage",
  data: () => ({
    currentPage: false,
    sectionData: [
      {
        id: 10,
        svgattr: "M100,0V50H0V0Z",
        kolon: [
          {
            id: "25yl85j",
            width: 100,
          },
        ],
      },
      {
        id: 20,
        svgattr: "M49,0V50H0V0Z M100,0V50H51V0Z",
        kolon: [
          {
            id: "r79ev3o",
            width: 50,
          },
          {
            id: "4m4im7j",
            width: 50,
          },
        ],
      },
      {
        id: 30,
        svgattr: "M32, 0V50H0V0Z M66, 0V50H34V0Z M100, 0V50H68V0Z",
        kolon: [
          {
            id: "jtm2zsp",
            width: 33,
          },
          {
            id: "t5jl0xn",
            width: 33,
          },
          {
            id: "w6kx27y",
            width: 33,
          },
        ],
      },
      {
        id: 40,
        svgattr:
          "M23.5,0V50H0V0Z M49,0V50H25.5V0Z M74.5,0V50H51V0Z M100,0V50H76.5V0Z",
        kolon: [
          {
            id: "0bz8jj1",
            width: 25,
          },
          {
            id: "p4fybdh",
            width: 25,
          },
          {
            id: "ffiosh2",
            width: 25,
          },
          {
            id: "fcnorwk",
            width: 25,
          },
        ],
      },
      {
        id: 21,
        svgattr: "M32.6667,0V50H0V0Z M100,0V50H34.6667V0Z",
        kolon: [
          {
            id: "j33w2jz",
            width: 33,
          },
          {
            id: "rj3g584",
            width: 66,
          },
        ],
      },
      {
        id: 22,
        svgattr: "M65.3333,0V50H0V0Z M100,0V50H67.3333V0Z",
        kolon: [
          {
            id: "vrltrrg",
            width: 66,
          },
          {
            id: "xw928p2",
            width: 33,
          },
        ],
      },
      {
        id: 31,
        svgattr: "M24,0V50H0V0Z M50,0V50H26V0Z M100,0V50H52V0Z",
        kolon: [
          {
            id: "hz8kkmu",
            width: 25,
          },
          {
            id: "02y2tgi",
            width: 25,
          },
          {
            id: "ggyvyuf",
            width: 50,
          },
        ],
      },
      {
        id: 32,
        svgattr: "M48,0V50H0V0Z M74,0V50H50V0Z M100,0V50H76V0Z",
        kolon: [
          {
            id: "i5rjm94",
            width: 50,
          },
          {
            id: "tx5xcin",
            width: 25,
          },
          {
            id: "o9fhpnq",
            width: 25,
          },
        ],
      },
      {
        id: 33,
        svgattr: "M24,0V50H0V0Z M74,0V50H26V0Z M100,0V50H76V0Z",
        kolon: [
          {
            id: "kmxv5sb",
            width: 25,
          },
          {
            id: "yaokxjc",
            width: 50,
          },
          {
            id: "1vojm7u",
            width: 25,
          },
        ],
      },
      {
        id: 50,
        svgattr:
          "M18.4,0V50H0V0Z M38.8,0V50H20.4V0Z M59.2,0V50H40.8V0Z M79.6,0V50H61.2V0Z M100,0V50H81.6V0Z",
        kolon: [
          {
            id: "3nzkwr3",
            width: 20,
          },
          {
            id: "f6wxqjm",
            width: 20,
          },
          {
            id: "zi9ez97",
            width: 20,
          },
          {
            id: "303zqdq",
            width: 20,
          },
          {
            id: "gih4omv",
            width: 20,
          },
        ],
      },
      {
        id: 60,
        svgattr:
          "M15,0V50H0V0Z M32,0V50H17V0Z M49,0V50H34V0Z M66,0V50H51V0Z M83,0V50H68V0Z M100,0V50H85V0Z",
        kolon: [
          {
            id: "26czmnf",
            width: 16,
          },
          {
            id: "siqjy6s",
            width: 16,
          },
          {
            id: "a5x2s94",
            width: 16,
          },
          {
            id: "js2dnp6",
            width: 16,
          },
          {
            id: "9ss96cy",
            width: 16,
          },
          {
            id: "qt3essn",
            width: 16,
          },
        ],
      },
      {
        id: 34,
        svgattr: "M16,0V50H0V0Z M82,0V50H18V0Z M100,0V50H84V0Z",
        kolon: [
          {
            id: "tenhw8n",
            width: 16,
          },
          {
            id: "xconz6z",
            width: 66,
          },
          {
            id: "vkilnfi",
            width: 16,
          },
        ],
      },
    ],
    selectedData: [],
    dragDataLine: {},
    dragDataColomn: {},
    hoverDataColomn: { hover: false, hoverId: 0 },
    hoverDataLine: { hover: false, hoverId: 0 },
    isColomn: false,
    swapLine: {},
  }),
  methods: {
    emit(emitData) {
      if (emitData == true || emitData == false)
        this.currentPage = emitData == true ? true : false;
      else {
        this.swapLine = {
          id: this.createUUID(),
          svgattr: emitData.svgattr,
          kolon: [],
        };
        emitData.kolon.map((g) => {
          this.swapLine.kolon.push({
            id: this.createUUID(),
            width: g.width,
          });
        });
        this.selectedData.push(this.swapLine);
        this.currentPage = false;
      }
    },

    mouseHoverIn(hoverInData) {
      if (hoverInData.svgattr == null) {
        this.hoverDataColomn = {
          hover: true,
          hoverId: hoverInData.id,
        };
      } else {
        this.hoverDataLine = {
          hover: true,
          hoverId: hoverInData.id,
        };
      }
    },

    mouseHoverOut(hoverOutData) {
      if (hoverOutData.svgattr == null) {
        this.hoverDataColomn = {
          hover: false,
          hoverId: hoverOutData.id,
        };
      } else {
        this.hoverDataLine = {
          hover: false,
          hoverId: hoverOutData.id,
        };
      }
    },

    handleDragStart(e, dragData) {
      this.dragDataLine = this.selectedData.find((g) => g.id == dragData.id);
      if (dragData.width != null) {
        this.isColomn = true;
        this.selectedData.forEach((element) => {
          if (element.kolon.some((g) => g.id === dragData.id)) {
            this.dragDataColomn = element.kolon.find(
              (g) => g.id === dragData.id
            );
          }
        });
      }
    },

    onDropData(e, dropData) {
      const dropLineIndex = this.selectedData.findIndex(
        (g) => g.id == dropData.id
      );
      const dragColomnIndex = this.selectedData.findIndex(
        (g) => g.id == this.dragDataLine.id
      );
      if (!this.isColomn) {
        this.selectedData.splice(dragColomnIndex, 1);
        this.selectedData.splice(dropLineIndex, 0, this.dragDataLine);
      } else if (this.isColomn && dropData.width == null) {
        this.selectedData[dropLineIndex].kolon.push(this.dragDataColomn);
        this.selectedData[dragColomnIndex].kolon.splice(
          this.selectedData[dragColomnIndex].kolon.findIndex(
            (g) => g.id == this.dragDataColomn.id
          ),
          1
        );
        if (this.selectedData[dragColomnIndex].kolon.length == 0) {
          this.selectedData.splice(dragColomnIndex, 1);
        }
        this.isColomn = false;
      }
    },

    createUUID() {
      return "xxxxxxxx-xxxx-4xxx-yxxx-xxxxxxxxxxxx".replace(
        /[xy]/g,
        function (c) {
          var r = (Math.random() * 16) | 0,
            v = c == "x" ? r : (r & 0x3) | 0x8;
          return v.toString(16);
        }
      );
    },

    deleteLine(lineData) {
      this.selectedData.splice(
        this.selectedData.findIndex((g) => g.id == lineData.id),
        1
      );
    },

    addLine(lineData) {
      this.swapLine = {
        id: this.createUUID(),
        svgattr: lineData.svgattr,
        kolon: [],
      };
      lineData.kolon.map((g) => {
        this.swapLine.kolon.push({
          id: this.createUUID(),
          width: g.width,
        });
      });
      this.selectedData.push(this.swapLine);
    },
  },
  components: { AddComponent, RowStructure },
};
</script>

<style scoped>
.icon-container {
  background-color: #90caf9;
  border-radius: 5px;
  margin-top: -20px;
}

.border-bottom {
  border-bottom: 2px solid #90caf9;
}
</style>

