<template>
  <v-app>
    <v-navigation-drawer
      v-model="drawer"
      fixed
      app
      temporary
    >
      <v-list>
        <v-list-item
          v-for="(item, i) in items"
          :key="i"
          :to="item.to"
          router
          exact
        >
          <v-list-item-action>
            <v-icon>{{ item.icon }}</v-icon>
          </v-list-item-action>
          <v-list-item-content>
            <v-list-item-title v-text="item.title" />
          </v-list-item-content>
        </v-list-item>
      </v-list>
    </v-navigation-drawer>

    <v-toolbar
      elevation="0"
      color="#F2F4F6"
      height="40px"
      v-if="isMd"
    >
    <v-spacer/>
      <span class="tb_text-number tb_txt">
        8 800 555 7 550
      </span>
      <span class="tb_txt">
        <v-icon color="primary">mdi-phone</v-icon>
        <a
          href="https://google.com/"
          target="_blank"
          rel="noopener noreferrer"
          title="chat"
        >
          Перезвоните!
        </a>
      </span>
      <span class="tb_txt">
        <v-icon color="primary">mdi-chat</v-icon>
        <a
          href="https://google.com/"
          target="_blank"
          rel="noopener noreferrer"
          title="chat"
        >
          smsaero
        </a>
      </span>
      <span class="tb_txt">
        <v-icon color="primary">mdi-email</v-icon>
        <a
          href="https://google.com/"
          target="_blank"
          rel="noopener noreferrer"
          title="chat"
        >
          support@smsaero.ru
        </a>
      </span>
      <span class="tb_txt">
        <v-icon color="primary">mdi-wechat</v-icon>
        <a
          href="https://google.com/"
          target="_blank"
          rel="noopener noreferrer"
          title="chat"
        >
          Начать чат
        </a>
      </span>
    <v-spacer/>
    </v-toolbar>

    <v-app-bar
      :class="!isSmOrSmaller ? 'mainbar': 'mainbarAD' "
      color="transparent"
      elevation="0"
    >
      <v-app-bar-nav-icon 
        @click.stop="drawer = !drawer" 
        v-if="isSmOrSmaller"
        class="nav_but"
      />
        <v-row>
          <v-col cols="12" class="logotemp">
            <img
              :class="!isSmOrSmaller ? 'logo': 'logoAD' "
              alt="Logo"
              src="/logo.png"
            >
          </v-col>
          <v-col cols="12" v-if="!isSmOrSmaller">
            <p class="text--secondary subtitle-1">
              Доставляем с 2010. Подключайтесь!
            </p>
          </v-col>
        </v-row>
        <v-spacer v-if="isXlOrlarger"/>
        <v-row class="nav_links">
          <v-col cols="3" v-if="!isMdOrSmaller" :class="isLg ? 'larg': ''">
            <p>
              <v-icon color="primary">mdi-wechat</v-icon>
              <a
                href="https://google.com/"
                target="_blank"
                rel="noopener noreferrer"
                title="chat"
              >
                Начать чат
              </a>
            </p>
            <p>
              <v-icon color="primary">mdi-chat</v-icon>
              <a
                href="https://google.com/"
                target="_blank"
                rel="noopener noreferrer"
                title="chat"
              >
                smsaero
              </a>
            </p>
            <p>
              <v-icon color="primary">mdi-email</v-icon>
              <a
                href="https://google.com/"
                target="_blank"
                rel="noopener noreferrer"
                title="chat"
              >
                support@smsaero.ru
              </a>
            </p>
          </v-col>
          <v-col cols="3" class="txtalignright" v-if="!isMdOrSmaller" :class="isLg ? 'larg1': ''">
            <p class="text--secondary">
              Мы 24/7 на связи!
            </p>
            <p class="text-number">
              8 800 555 7 550
            </p>
            <p>
              <v-icon color="primary">mdi-phone</v-icon>
              <a
                href="https://google.com/"
                target="_blank"
                rel="noopener noreferrer"
                title="chat"
              >
                Перезвоните!
              </a>
            </p>
          </v-col>
          <v-col cols="3" v-if="!isSmOrSmaller">
            <p class="text--secondary">
              4.7 из 5 - вау!
            </p>
            <p>
              <v-rating
                value="5"
                color="yellow darken-1"
                empty-icon="$ratingFull"
                half-increments
                readonly
                dense
                size="20"
              ></v-rating>
            </p>
            <p>
              <a
                href="https://google.com/"
                target="_blank"
                rel="noopener noreferrer"
                title="chat"
              >
                Отзывы о нас
              </a>
            </p>
          </v-col>
          <v-col cols="6" v-if="isMdOrSmaller"></v-col>
          <v-col cols="3">
            <p>
              <v-btn
                rounded
                color="success"
                dark
                :large="!isSmOrSmaller"
                :small="isSmOrSmaller"
                :fab="isSmOrSmaller"
              >
              <v-icon :left="!isSmOrSmaller">mdi-account-circle</v-icon>
                <span v-if="!isSmOrSmaller"> Войти </span>
              </v-btn>
            </p>
            <p v-if="!isSmOrSmaller" style="margin-top: 18px; margin-left: 25px">
              <a
                href="https://google.com/"
                target="_blank"
                rel="noopener noreferrer"
                title="chat"
              >
                Регистрация
              </a>
            </p>
          </v-col>
        </v-row>
    </v-app-bar>

    <v-main>
      <v-container>

        <v-tabs
          color="pink"
          grow
          background-color="transparent"
          v-if="!isSmOrSmaller"
        >
          <v-tab
            v-for="(item, i) in items"
            :key="i"
            :to="item.to"
          >{{item.title}}</v-tab>
        </v-tabs>
        <v-divider></v-divider>
        <Nuxt />
      </v-container>
    </v-main>

    <v-footer
      :absolute="!fixed"
      app
    >
      <span>&copy; {{ new Date().getFullYear() }}</span>
    </v-footer>
  </v-app>
</template>

<script>
export default {
  name: 'DefaultLayout',
  data () {
    return {
      drawer: false,
      fixed: false,
      items: [
        {
          title: 'Услуги',
          to: '/'
        },
        {
          title: 'Интеграция',
          to: '/integration'
        },
        {
          title: 'Цены',
          to: '/costs'
        },
        {
          title: 'Решения',
          to: '/solutions'
        },
        {
          title: 'Поддержка',
          to: '/support'
        },
        {
          title: 'Блог',
          to: '/blog'
        },
        {
          title: 'Компания',
          to: '/company'
        }
      ],
      miniVariant: false,
      title: 'Vuetify.js',
    }
  },
  computed: {
    isXs () { 
      return this.$breakpoints.xs 
    },
    isMd () { 
      return this.$breakpoints.md
    },
    isMdOrSmaller () { 
      return this.$breakpoints.md || this.$breakpoints.sm || this.$breakpoints.xs 
    },
    isSmOrSmaller () { 
      return this.$breakpoints.sm || this.$breakpoints.xs
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
.logo {
  height: 40px;
}
.logoAD {
  height: 30px;
  transform: translateX(40px) translateY(10px)
}
.subtitle-1 {
  font-size: 13px !important;
}
.mainbar {
  padding: 40px 100px; 
  height: auto !important;
}
.mainbarAD {
  padding: 20px auto; 
  height: auto !important;
}
.col {
  padding: 0px !important;
}
p {
  margin-bottom: 7px !important;
  line-height: 24px !important;
  font-size: 13px !important;
}
.text-number {
  font-style: normal;
  font-weight: 800;
  font-size: 18px !important;
}
.txtalignright p{
  text-align: right;
  padding-right: 40px;
}
.larg{
  transform: translateX(-50px);
}
.larg1{
  transform: translateX(-20px);
}
.larg2{
  transform: translateX(-20px);
}
.nav_links {
  white-space: nowrap !important;
}
.tb_text-number {
  font-style: normal;
  font-weight: 800 !important;
  font-size: 15px !important;
}
.tb_txt {
  margin: auto 20px;
  white-space: nowrap !important;
  font-weight: 400;
  font-size: 13px;
}
.nav_but {
  transform: translateY(8px); 
  background: black; 
  color: white !important;
}
</style>