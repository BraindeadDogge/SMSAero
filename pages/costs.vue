<template>
<div>
  <v-sheet
    class="mx-auto targ_sheet"
    max-width="780"
  >
    <v-slide-group v-if="!isSmOrSmaller">
      <v-slide-item v-slot="{ active, toggle }">
        <v-btn
          class="mx-2"
          active-class="pink white--text"
          depressed
          rounded
          :input-value="active"
          @click="toggle"
        >
          SMS-рассылка
        </v-btn>
      </v-slide-item>
      <v-slide-item v-slot="{ active, toggle }">
        <v-btn
          class="mx-2"
          active-class="pink white--text"
          depressed
          rounded
          :input-value="active"
          @click="toggle"
        >
          Таргетированные SMS
        </v-btn>
      </v-slide-item>
      <v-slide-item v-slot="{ active, toggle }">
        <v-btn
          class="mx-2"
          active-class="pink white--text"
          depressed
          rounded
          :input-value="active"
          @click="toggle"
        >
          Viber рассылка
        </v-btn>
      </v-slide-item>
      <v-slide-item v-slot="{ active, toggle }">
        <v-btn
          class="mx-2"
          active-class="pink white--text"
          depressed
          rounded
          :input-value="active"
          @click="toggle"
        >
          HLR-проверка
        </v-btn>
      </v-slide-item>
    </v-slide-group>
  </v-sheet>

  <h1 class="big_title">
    От 1,54 до 2,69 ₽ за SMS
  </h1>

  <h3 class="sub_t">
    Цена SMS зависит от оператора связи,
    имени отправителя и суммы пополнения
  </h3>

  <v-row class="some_row" :style="isLgOrSmaller? 'width:85vw': ''">
    <v-col cols="12" align="center" style="transform: translateY(-8px)" v-if="isSmOrSmaller">
      <p class="p_small">
        Сумма пополнения:
      </p>
      <p>
        <v-text-field
          v-model="sum_value"
          placeholder="100 000"
          filled
          rounded
          dense
          suffix="₽"
          class="text_field_sum"
        ></v-text-field>
      </p>
    </v-col>
  </v-row>

  <v-row class="some_row" :style="isLgOrSmaller? 'width:85vw': ''">
    <v-col cols="2" align="end" style="transform: translateY(-8px)" v-if="!isMdOrSmaller">
      <p class="p_small">
        Сумма пополнения:
      </p>
      <p>
        <v-text-field
          v-model="sum_value"
          placeholder="100 000"
          filled
          rounded
          dense
          suffix="₽"
          class="text_field_sum"
          style="margin-left: auto"
        ></v-text-field>
      </p>
    </v-col>
    <v-col lg="8">
      <p>
        <v-row>
          <v-col
          v-for="(item,i) in items"
          :key="i"
          style="text-align:center"
          >
            <span class="num_text">
              {{i}}
            </span>
          </v-col>
        </v-row>
      </p>
      <p>
        <v-slider
          v-model="value"
          hide-details
          max="50000"
          min="0"
          color="pink"
        ></v-slider>
      </p>
    </v-col>
    <v-col cols="2" style="transform: translateY(-8px)" v-if="!isMdOrSmaller">
      <p class="p_small">
        Количество SMS:
      </p>
      <p>
        <v-text-field
          v-model="sms_value"
          placeholder="100 000"
          filled
          rounded
          dense
          prefix="~"
          class="text_field_sum"
        ></v-text-field>
      </p>
    </v-col>
  </v-row>

  <v-row class="some_row" :style="isLgOrSmaller? 'width:85vw': ''">
    <v-col cols="12" md="6" sm = "6" align="end" style="transform: translateY(-8px)" v-if="isMd">
      <p class="p_small">
        Сумма пополнения:
      </p>
      <p>
        <v-text-field
          v-model="sum_value"
          placeholder="100 000"
          filled
          rounded
          dense
          suffix="₽"
          class="text_field_sum"
          style="margin-left: auto"
        ></v-text-field>
      </p>
    </v-col>
    <v-col cols="12" md="6" sm = "6" :align="!isMd ? 'center': ''" style="transform: translateY(-8px)" v-if="isMdOrSmaller">
      <p class="p_small">
        Количество SMS:
      </p>
      <p>
        <v-text-field
          v-model="sms_value"
          placeholder="100 000"
          filled
          rounded
          dense
          prefix="~"
          class="text_field_sum"
        ></v-text-field>
      </p>
    </v-col>
  </v-row>

  <div :class="!isMdOrSmaller ? 'costs': 'costsAD' ">
    <v-row>
      <v-col></v-col>
      <v-col>Бесплатное имя</v-col>
      <v-col>Платное имя</v-col>
      <v-col>Сервисные SMS</v-col>
    </v-row>
    <v-divider></v-divider>
    <v-row 
      v-for="(cost,i) in costs"
      :key="i"
    >
      <v-col>
        <span class="costs_txt">{{i}}</span>
      </v-col>
      <v-col
        v-for="(c,i) in cost"
        :key="i"
      >
        <span class="costs_num">{{c}} ₽</span>
      </v-col>
    </v-row>
    <v-divider></v-divider>
    <v-row 
      v-for="(country,i) in countries"
      :key="i"
    >
      <v-col>
        <span class="costs_txt">{{i}}</span>
      </v-col>
      <v-col
        v-for="(c,i) in country"
        :key="i"
      >
        <span class="costs_num">{{c}} ₽</span>
      </v-col>
    </v-row>
    <v-divider></v-divider>
  </div>

  <div :class="!isMdOrSmaller ? 'links': 'linksAD' ">
    <p>
      <v-icon color="primary">mdi-tray-arrow-down</v-icon>
      <a
        href="https://google.com/"
        target="_blank"
        rel="noopener noreferrer"
        title="chat"
      >
        Презентация компании и цены в формате PDF
      </a>
    </p>
    <p>
      <v-icon color="primary">mdi-tray-arrow-down</v-icon>
      <a
        href="https://google.com/"
        target="_blank"
        rel="noopener noreferrer"
        title="chat"
      >
        Только прайс в формате XLS
      </a>
    </p>
    <p>
      <v-icon color="primary">mdi-information</v-icon>
      <a
        href="https://google.com/"
        target="_blank"
        rel="noopener noreferrer"
        title="chat"
      >
        Подробнее об имени и сервисных сообщениях
      </a>
    </p>
  </div>

  <v-row :class="!isMdOrSmaller? 'offers':'offersAD'">
    <v-col cols="12" md ="4" sm="6" lg="4" xl="4">
      <img src="/image125.svg" alt="сумка">
      <p>
        Никаких минимальных пакетов. Покупайте столько SMS, сколько вам нужно.
      </p>
    </v-col>
    <v-col cols="12" md ="4" sm="6" xs="4" xl="4">
      <img src="/image204.svg" alt="сумка">
      <p>
        Итоговая стоимость вашей рассылки будет видна перед её запуском в личном кабинете.
      </p>
    </v-col>
    <v-col cols="12" md ="4" sm="12" xs="4" xl="4">
      <img src="/image201.svg" alt="сумка">
      <p>
        Если рассылаете более 50 000 сообщений в месяц, 
          <a
            href="https://google.com/"
            target="_blank"
            rel="noopener noreferrer"
            title="chat"
          >
            договоримся
          </a>
        о специальных условиях.
      </p>
    </v-col>
  </v-row>
</div>
</template>

<script>
export default {
  name: 'CostsPage',
  data () {
    return {
      value: 30000,
      sum_value: 500000,
      sms_value: 324000,
      items: {
        "1": "1", 
        "3K": "3 000", 
        "15K": "15 000", 
        "35K": "35 000", 
        "150K": "150 000", 
        "500K": "500 000", 
        "5 млн.": "5 млн.",
      },
      costs: {
        "МТС": [2.29, 2.07, 1.77],
        "Билайн": [2.67, 1.95, 1.95],
        "Мегафон": [2.19, 2.13, 1.59],
        "Теле2": [2.47, 2.31, 1.75],
        "Другие": [2.47, 2.47, 2.47],
      },
      countries: {
        "Украина": [3.5, 3.5, 3.5],
        "Белоруссия": [5.5, 5.5, 5.5],
        "Казахстан": [7.2, 7.2, 7.2]
      }
    }
  },
  computed: {
    isXs () { 
      return this.$breakpoints.xs 
    },
    isSmOrSmaller () { 
      return this.$breakpoints.sm || this.$breakpoints.xs
    },
    isMd () { 
      return this.$breakpoints.md
    },
    isMdOrSmaller () { 
      return this.$breakpoints.md || this.$breakpoints.sm || this.$breakpoints.xs 
    },
    isLgOrSmaller () { 
      return this.$breakpoints.lg || this.$breakpoints.md || this.$breakpoints.sm || this.$breakpoints.xs 
    },
    isXlOrlarger () { 
      return this.$breakpoints.xl
    },
    isLg() {
      return this.$breakpoints.lg
    }
  }
}
</script>

<style scoped>
.v-text-field{
  width: 180px !important;
}
.targ_sheet {
  margin: 60px 0
}
.big_title {
  font-style: normal;
  font-weight: 800;
  font-size: 56px;
  line-height: 60px;
  text-align: center;
  background: linear-gradient(90deg, #FF4C5B 0%, #E55069 33.16%, #D94174 69.97%);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
}
.sub_t {
  font-style: normal;
  font-weight: 400;
  font-size: 26px;
  line-height: 30px;
  text-align: center;
  color: #253140;
  margin: 10px 0 100px;
}
.some_row {
  width:60vw;
  margin: 0 auto;
}
.some_row .col {
  padding: 0 20px
}
.some_row .col p {
  height: 40px;
  justify-content: center
}
.num_text {
  font-weight: 400;
  font-size: 17px;
  line-height: 25px;
}
.p_small {
  font-weight: 400;
  font-size: 13px;
  line-height: 20px;
  color: #253140;
}
.text_field_sum {
  text-align: right !important;
  font-style: normal;
  font-weight: 800;
  font-size: 24px;
  line-height: 40px;
  color: #253140;
  transform: translateY(-10px);
}
.costs {
  width: 600px;
  margin: 0 auto;
}
.costs .row {
  margin: 30px 0;
}
.costs .row .col {
  padding: 5px;
}
.costsAD {
  margin: 0 auto;
}
.costsAD .row {
  margin: 30px 0;
}
.costsAD .row .col {
  padding: 5px;
}
.costs_txt {
  font-weight: 400;
  font-size: 13px;
  color: #5D6978;
}
.costs_num {
  font-weight: 400;
  font-size: 17px;
  color: #253140;
}
.links {
  width: 600px;
  margin: 20px auto;
  font-weight: 400;
  font-size: 15px;
  line-height: 40px;
}
.linksAD {
  margin: 20px auto;
  font-weight: 400;
  font-size: 13px;
  line-height: 20px;
}
.offers {
  width: 920px;
  margin: 83px auto;
}
.offersAD {
  margin: 83px auto;
}
.offers .col-12 {
  text-align: center;
}
.offers .col-12 p {
  font-weight: 400;
  font-size: 17px;
  line-height: 25px;
  text-align: center;
  color: #253140;
  width: 280px !important;
  margin: 0 auto;
}
.offersAD .col-12 {
  text-align: center;
}
.offersAD .col-12 p {
  font-weight: 400;
  font-size: 17px;
  line-height: 25px;
  text-align: center;
  color: #253140;
  width: 280px !important;
  margin: 0 auto;

}
</style>