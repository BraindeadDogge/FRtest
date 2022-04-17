<template>
  <div>
    <v-breadcrumbs :items="breaditems">
      <template v-slot:divider>
        <v-icon>mdi-forward</v-icon>
      </template>
    </v-breadcrumbs>
      <v-stepper v-model="st">
    <v-stepper-header>
      <v-stepper-step
        :complete="st > 1"
        step="1"
      >
        Параметры
      </v-stepper-step>

      <v-divider></v-divider>

      <v-stepper-step
        :complete="st > 2"
        step="2"
      >
        Вопросы
      </v-stepper-step>

      <v-divider></v-divider>

      <v-stepper-step
        :complete="st > 3"
        step="3"
      >
        Логика
      </v-stepper-step>

      <v-divider></v-divider>

      <v-stepper-step
        :complete="st > 4"
        step="4"
      >
        Условия
      </v-stepper-step>

      <v-divider></v-divider>

      <v-stepper-step step="5">
        Респонденты
      </v-stepper-step>
    </v-stepper-header>

    <v-stepper-items>
      <v-stepper-content step="1">
        <v-card
          class="mb-12"
          color="grey lighten-1"
          height="200px"
        ></v-card>

        <v-row>
          <v-col cols="6">
            <v-btn outlined color="green">
              Протестировать опрос
            </v-btn>
          </v-col>
          <v-col cols="6" style="text-align: end;">
            <v-btn
              color="primary"
              @click="st = 2"
            >
              Далее
            </v-btn>
          </v-col>
        </v-row>
      </v-stepper-content>

      <v-stepper-content step="2">
        <v-card
          class="mb-12"
          color="grey lighten-1"
          height="200px"
        ></v-card>

        <v-row>
          <v-col cols="6">
            <v-btn outlined color="green">
              Протестировать опрос
            </v-btn>
          </v-col>
          <v-col cols="6" style="text-align: end;">
            <v-btn
              color="primary"
              @click="st = 3"
            >
              Далее
            </v-btn>
          </v-col>
        </v-row>
      </v-stepper-content>

      <v-stepper-content step="3">
        <v-card
          class="mb-12"
          color="grey lighten-1"
          height="200px"
        ></v-card>

        <v-row>
          <v-col cols="6">
            <v-btn outlined color="green">
              Протестировать опрос
            </v-btn>
          </v-col>
          <v-col cols="6" style="text-align: end;">
            <v-btn
              color="primary"
              @click="st = 4"
            >
              Далее
            </v-btn>
          </v-col>
        </v-row>
      </v-stepper-content>

      <v-stepper-content step="4">
        <v-card
          class="mb-12"
          color="grey lighten-1"
          height="200px"
        ></v-card>

        <v-row>
          <v-col cols="6">
            <v-btn outlined color="green">
              Протестировать опрос
            </v-btn>
          </v-col>
          <v-col cols="6" style="text-align: end;">
            <v-btn
              color="primary"
              @click="st = 5"
            >
              Далее
            </v-btn>
          </v-col>
        </v-row>
      </v-stepper-content>

      <v-stepper-content step="5">
        <p class="text--secondary">Добавить опрос</p>
        <v-card
          v-for="(item, i) in cards"
          :key="i"
          class="mb-12 innercard"
          :color="i % 2 === 0? 'green lighten-5': 'blue lighten-5'"
        >
          <v-row>
            <v-col cols="3"> <v-card-title>Условие {{i+1}}</v-card-title></v-col>
            <v-col cols="9">
              <v-select
                :items="Object.keys(states)"
                v-model="item.state"
                outlined
              ></v-select>
            </v-col> 
          </v-row>
          <v-row 
            v-for="(types, j) in item.type"
            :key="j"
          >             
            <v-col cols="3"> <v-card-subtitle> {{states[item.state][0]}} {{j+1}}</v-card-subtitle></v-col>
            <v-col cols="9">
              <v-row
                v-if="states[item.state][0] == 'Диапазон'"
                :items="states[item.state]"
                outlined
              >
                <v-col cols="6">
                  <v-text-field
                    label="От"
                    outlined
                    v-model="item.type[j][0]"
                  ></v-text-field>
                </v-col>
                <v-col cols="6">
                  <v-text-field
                    label="До"
                    outlined
                    v-model="item.type[j][1]"
                  ></v-text-field>
                </v-col>
              </v-row>
              <v-select
                v-if="states[item.state][0] == 'Тип'"
                :items="states[item.state][2]"
                v-model="item.type[j]"
                outlined
              ></v-select>
              <v-select
                v-if="states[item.state][0] == 'Статус'"
                :items="states[item.state][2]"
                v-model="item.type[j]"
                outlined
              ></v-select>
            </v-col>
          </v-row>
          <v-row>
            <v-col cols="3"></v-col>
            <v-col cols="9">
              <v-row>
              <v-col cols="6">
                <v-btn
                  outlined
                  color="success"
                  @click="item.type.push(states[item.state][1])"
                >
                  <v-icon left>
                    mdi-plus
                  </v-icon>
                  Добавить {{states[item.state][0]}}
                </v-btn>
              </v-col>
              <v-col cols="6" style="text-align: end;">
                <v-btn
                  outlined
                  color="error"
                  @click="cards.splice(i,1)"
                >
                  <v-icon left>
                    mdi-delete
                  </v-icon>
                  Удалить условие
                </v-btn>
              </v-col>
              </v-row>
            </v-col>
          </v-row>
        </v-card>
        <v-card
          class="mb-12 innercard"
          style="text-align: center"
          color="primary"
          dark
          tile
          @click="cards.push(cleared)"
        >
          <p>
            <v-icon x-large>
              mdi-plus
            </v-icon>
          </p>
          <p>Нажмите, чтобы добавить новое условие выборки.</p>
          <p>Все условия связываются между собой логическим "И"</p>
        </v-card>

        <v-row>
          <v-col cols="6">
            <v-btn outlined color="green">
              Протестировать опрос
            </v-btn>
          </v-col>
          <v-col cols="6" style="text-align: end;">
            <v-btn
              color="primary"
              @click="st = 1"
            >
              Далее
            </v-btn>
          </v-col>
        </v-row>
      </v-stepper-content>
    </v-stepper-items>
  </v-stepper>
  </div>
</template>

<script>
export default {
  name: 'PollsAdd',
  data: () => ({
    st: 5,
    breaditems: [
      {
        text: 'Home',
        disabled: false,
        href: '/',
      },
      {
        text: 'Опросы',
        disabled: false,
        href: '/polls',
      },
      {
        text: 'Добавить опрос',
        disabled: true,
        href: '/polls/add',
      },
    ],
    cards: [
      {
        state: "Возраст респондента",
        type:[
          [13, 20],
          [13, 20],
          [13, 20],
        ],
      },
      {
        state: "Тип карты лояльности",
        type: ["Gold"],
      },
      {
        state: "Стасус карты лояльности",
        type: ["Активна"],
      },
    ],
    states: {
      "Возраст респондента": ["Диапазон", []],
      "Тип карты лояльности": [
        "Тип",
        "",
        ["Silver", "Gold", "Platinum"]
      ],
      "Стасус карты лояльности": [
        "Статус",
        "",
        ["Активна", "Не активна"]
      ],
    },
    cleared: {
      state: "Возраст респондента",
      type:[],
    },
  }),
  
}
</script>

<style>
  .innercard {
    padding: 20px
  }
</style>