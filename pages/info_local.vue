<template>
  <div>
    <h2 class="title">現地用 インフォメーションセンター</h2>
    <p style="text-align: center; font-size: 13px">
      各参団の待ち時間、開催状況を随時更新します。
    </p>
    <div style="display: flex; justify-content: center">
      <v-tabs
        v-model="tab0"
        class="tabbar"
        style="border-bottom: 1px solid #f0f0f3"
      >
        <v-tab v-for="item in tabs0" :key="item" v-model="tab0">
          {{ item }}
        </v-tab>
      </v-tabs>
    </div>

    <v-tabs-items v-model="tab0">
      <v-tab-item>
        <v-tabs v-model="tab1" class="tabbar">
          <v-tab v-for="item in tabs1" :key="item" v-model="tab1">
            {{ item }}
          </v-tab>
        </v-tabs>
        <v-tabs-items v-model="tab1">
          <v-tab-item v-for="items in sandans_list" :key="items">
            <v-row>
              <v-spacer />
              <v-col cols="11" md="4" lg="8" class="mx-auto">
                <p v-if="items.length === 0" style="text-align: center">
                  該当する参団がありません
                </p>
                <div v-for="item in items" :key="item" class="sandan">
                  <img :src="item.icon" alt="" />
                  <div>
                    <h3>{{ item.name }}</h3>
                    <p>
                      {{ item.waittime }} 分待ち（最終更新：{{
                        item.last_updated
                      }}）
                    </p>
                    <p>場所：{{ item.room }}</p>
                  </div>
                </div>
              </v-col>
              <v-spacer />
            </v-row>
          </v-tab-item>
        </v-tabs-items>
      </v-tab-item>

      <v-tab-item>
        <v-tabs v-model="tab2" class="tabbar">
          <v-tab v-for="item in tabs2" :key="item" v-model="tab2">
            {{ item }}
          </v-tab>
        </v-tabs>
        <v-tabs-items v-model="tab2">
          <v-tab-item v-for="items in demo_sandans_list" :key="items">
            <v-row>
              <v-spacer />
              <v-col cols="11" md="4" lg="8" class="mx-auto">
                <p v-if="items.length === 0" style="text-align: center">
                  該当する参団がありません
                </p>
                <div v-for="item in items" :key="item" class="sandan">
                  <img :src="item.icon" alt="" />
                  <div>
                    <h3>{{ item.name }}</h3>
                    <p>
                      {{ date2time(item.start) }} 〜 {{ date2time(item.end) }}
                    </p>
                    <p>場所：{{ item.room }}</p>
                  </div>
                </div>
              </v-col>
              <v-spacer />
            </v-row>
          </v-tab-item>
        </v-tabs-items>
      </v-tab-item>

      <v-tab-item>
        <v-row>
          <v-spacer />
          <v-col cols="11" md="4" lg="8" class="mx-auto">
            <p>
              模擬店係・喫茶係では、感染症対策として当日生徒の手により調理した食品の提供が中止となりました。その影響で今年は既製品を限定商品として販売します。
            </p>
            <p><img src="/info_local/menu.png" alt="" width="100%" /></p>
          </v-col>
          <v-spacer />
        </v-row>
      </v-tab-item>

      <v-tab-item>
        <v-tabs v-model="tab3" class="tabbar">
          <v-tab v-for="item in tabs3" :key="item" v-model="tab3">
            {{ item }}
          </v-tab>
        </v-tabs>
        <v-tabs-items v-model="tab3">
          <v-tab-item>
            <v-row>
              <v-spacer />
              <v-col cols="11" md="4" lg="8" class="mx-auto">
                <div
                  v-if="
                    (calc_hours() >= 9) & (calc_hours() <= 14) & is_production()
                  "
                >
                  <h3 style="margin-bottom: 1rem; font-size: 1.4rem">
                    <span
                      style="font-size: 3rem; color: #335719"
                      v-text="calc_hours()"
                    ></span>
                    時の部でご入場された方は、ご退校をお願いいたします。
                  </h3>
                  <p>150th 開成祭にご来場いただき、ありがとうございました。</p>
                  <p style="text-align: right; margin-bottom: 2rem">
                    文化祭準備委員会 一同
                  </p>
                </div>
                <ul>
                  <li style="color: #ea0032">
                    1日目の入場方法が変更となっております。詳しくは9/17
                    16時にFair
                    Castにて送信された「台風接近に伴う、文化祭1日目の入場方法等変更のお知らせ」をご覧ください。
                  </li>
                  <li>校内では必ずマスクを着用してください。</li>
                  <li>入場に使用したチケットの退校時間をお守りください。</li>
                  <li>
                    入り口にて体温測定を行います。基準（37.5℃）以上の場合は入校いただくことができません。
                  </li>
                  <li>
                    消毒液を入場口のほか、各教室出入り口などに設置しておりますので、手指消毒及びこまめな手洗いをお願いいたします。
                  </li>
                  <li>
                    校内各所に必要な距離を保つために目印を設置しておりますので、お客様同士のソーシャルディスタンスの確保にご協力をお願いします。
                  </li>
                  <li>校内での食事は、全面禁止にさせていただいております。</li>
                  <li>
                    会場にて万が一体調が悪くなったり気分が優れなくなったりした場合は、ご無理なさらず速やかにお近くの学園教職員、あるいは生徒までお申し出ください。
                  </li>
                  <li>換気のため、校舎内各所で窓を開放しております。</li>
                  <li>
                    政府及び東京都では、新型コロナウイルス接触確認アプリ（COCOA）のインストールを推奨しています。感染拡大防止にご協力お願いいたします。
                  </li>
                </ul>
              </v-col>
              <v-spacer />
            </v-row>
          </v-tab-item>
          <v-tab-item>
            <v-row>
              <v-spacer />
              <v-col cols="11" md="4" lg="8" class="mx-auto">
                <p>
                  お配りしたガイドブックに一部誤り・変更がございますので記載いたします。申し訳ございません。
                </p>
                <img src="/info_local/syuusei.svg" alt="" />
              </v-col>
              <v-spacer />
            </v-row>
          </v-tab-item>
        </v-tabs-items>
      </v-tab-item>
    </v-tabs-items>
  </div>
</template>

<style>
.tabbar {
  display: flex;
  justify-content: center;
  margin-bottom: 1rem;
}
.sandan {
  display: flex;
  margin-bottom: 1rem;
}
.sandan div {
  display: flex;
  flex-direction: column;
  justify-content: space-between;
}
.sandan h3 {
  font-size: 1.1rem;
  /*border-bottom: 2px solid #335719;*/
}
.sandan h3::first-letter {
  color: #335719;
  font-size: 1.4rem;
}
.sandan img {
  height: 70px;
  width: 70px;
  margin-right: 1.5rem;
}
.sandan p {
  font-size: 15px;
  line-height: 1px;
}
.title {
  margin-top: 2rem;
  font-size: 1.3rem;
  letter-spacing: 1px;
  text-align: center;
}
ul {
  margin-top: 1rem;
}
ul li {
  margin-left: 1rem;
  margin-bottom: 0.5rem;
}
</style>

<script>
export default {
  async asyncData({ $axios }) {
    const Vacant = []
    const CrowdedLittle = []
    const CrowdedBig = []
    const sandans = await $axios
      .$get('https://kaiseifes-150th-backend.herokuapp.com/api/sandans')
      .then((res) => {
        return res
      })
    for (let i = 0; i < sandans.length; i++) {
      if (sandans[i].waittime === 0) {
        Vacant.push(sandans[i])
      } else if ((sandans[i].waittime > 0) & (sandans[i].waittime <= 10)) {
        CrowdedLittle.push(sandans[i])
      } else if (sandans[i].waittime > 10) {
        CrowdedBig.push(sandans[i])
      }
    }

    const demoSandans = await $axios
      .$get(
        'https://kaiseifes-150th-backend.herokuapp.com/api/demo_sandans/today'
      )
      .then((res) => {
        return res
      })
    return {
      sandans_list: [Vacant, CrowdedLittle, CrowdedBig],
      demo_sandans_list: [demoSandans.in_progress, demoSandans.today_later],
    }
  },
  data() {
    return {
      tabs0: ['通常参団', '実演参団', '模擬店', 'ご注意'],
      tabs1: ['すぐ入れる', '少し並ぶ', '長く並ぶ'],
      tabs2: ['開催中', 'この後開催'],
      tabs3: ['一般', 'ガイドブック'],
      tab0: null,
      tab1: null,
      tab2: null,
      tab3: null,
    }
  },
  methods: {
    calc_hours() {
      const datetime = new Date()
      return datetime.getHours() - 3
    },
    is_production() {
      const datetime = new Date()
      return Boolean(
        (datetime.getMonth() === 8) &
          (datetime.getDate() === 18 || datetime.getDate() === 19)
      )
    },
    date2time(date) {
      const time = new Date(date)
      return time.getHours() + '時' + time.getMinutes() + '分'
    },
  },
}
</script>
