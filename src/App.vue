<template>
<div class="flex flex-col h-screen justify-between">
  <header class="mb-10">
  <UAlert
    color="primary"
    variant="subtle"
    title="開源專案"
    description="https://github.com/chichungchen95/taidan-computed"
    icon="i-lucide-terminal"
  />
  </header>
  <main class="mb-auto">
    <h3>計算電費</h3>
    <p>輸入瓦數</p>
    <center><input type="text" v-model="watt" /></center>
    <p>輸入時數(一天就打24hr)</p>
    <center><input type="text" v-model="hour" /></center>
    <hr class="mb-10"/>
    <p>每日度數: {{ duo.toFixed(1) }} 每2個月度數: {{ duomon.toFixed(1) }} 以 {{ duoey.toFixed(2) }} 累積電價</p>
    <p>兩個月累積電費: {{ duocadd.toFixed(0) }}</p>
  </main>
  <footer class="h-10">
    <UButton
    :avatar="{
      src: 'https://github.com/github.png'
    }"
    to="https://github.com/chichungchen95/taidan-computed" target="_blank"
    size="md"
    color="neutral"
    variant="outline"
  >
    Github
  </UButton>
  </footer>
</div>
</template>

<script>
export default {
  name: 'App',
  data() {
    return {
      watt: 0,
      hour: 0,
      duoey: 0,
      duocadd: 0,
      taidal:
        [
          { name: 120, price: 1.68 },
          { name: 330, price: 2.45 },
          { name: 500, price: 3.7 },
          { name: 700, price: 5.04 },
          { name: 1000, price: 6.24 },
          { name: 2000, price: 8.46 },
        ],
    }
  },
  watch: {
    // 監聽瓦數
    watt() {
      this.duolist();
      this.duocap();
    },
    // 監聽時數
    hour() {
      this.duolist();
      this.duocap();
    },
  },
  computed: {
    // 計算每日度數
    duo() {
      return (this.watt * this.hour) / 1000;
    },
    money() {
      return (this.duomon * this.duoey);
    },
    // 計算每個月度數
    duomon() {
      return this.duo * 60 ;
    },

  },
  methods: {

    // 計算度數電費
    duolist() {
      if (this.duomon <240) {
        return this.duoey = 1.68;
      } else if (this.duomon < 660) {
        return this.duoey = 2.45;
      } else if (this.duomon < 1000) {
        return this.duoey = 3.7;
      } else if (this.duomon < 1400) {
        return this.duoey = 5.04;
      } else if (this.duomon < 2000) {
        return this.duoey = 6.24;
      } else if (this.duomon > 2000) {
        return this.duoey = 8.46;
      }
   },
    // 計算電費
    duocap() {
      if(this.duoey === 1.68){
        this.duocadd =  this.taidal[0].price * this.duomon;
      } else if(this.duoey ===2.45){
        this.duocadd =  this.taidal[1].price * (this.duomon - 240) +  this.taidal[0].price * 240;
      } else if(this.duoey === 3.7){
        this.duocadd =  this.taidal[2].price * (this.duomon - 660)  + this.taidal[1].price * 420 + this.taidal[0].price * 240;
      } else if(this.duoey === 5.04){
        this.duocadd =  this.taidal[3].price * (this.duomon - 1000) + this.taidal[2].price * 340 + this.taidal[1].price * 420 + this.taidal[0].price * 240;
      } else if(this.duoey === 6.24){
        this.duocadd = this.taidal[4].price * (this.duomon - 1400)  + this.taidal[3].price * 400 + this.taidal[2].price * 340 + this.taidal[1].price * 420 + this.taidal[0].price * 240;
      } else if(this.duoey === 8.46){
        this.duocadd = this.taidal[5].price * (this.duomon - 2000) + this.taidal[4].price * 600  + this.taidal[3].price * 400 + this.taidal[2].price * 340 + this.taidal[1].price * 420 + this.taidal[0].price * 240;
      }
    },
  },
}
</script>

<style>
h3 {
  text-align: center;
  color: #d8dde2;
  margin-bottom: 30px;
}
p {
  text-align: center;
  color: #d8dde2;
  margin-bottom: 30px;
}
input {
  text-align: center;
  color: #d8dde2;
  margin-bottom: 30px;
}
input[type="text"] {
  width: 200px;
  height: 30px;
  border-radius: 5px;
  border: 1px solid #ccc;
}
input[type="text"]:focus {
  outline: none;
  border: 1px solid #d8dde2;
}
input[type="text"]:hover {
  border: 1px solid #d8dde2;
}
input[type="text"]:active {
  border: 1px solid #d8dde2;
}
p:hover {
  color: #d8dde2;
}
p:active {
  color: #d8dde2;
}
p:focus {
  color: #d8dde2;
}
input[type="text"]:focus {
  color: #d8dde2;
}
input[type="text"]:hover {
  color: #d8dde2;
}
input[type="text"]:active {
  color: #d8dde2;
}
p:focus {
  color: #d8dde2;
}
p:hover {
  color: #d8dde2;
}
p:active {
  color: #d8dde2;
}
input[type="text"]:focus {
  color: #d8dde2;
} 
</style>
