<template>
  <h3>計算電費</h3>
  <p>輸入瓦數</p>
  <center><input type="text" v-model="watt" /></center>
  <p>輸入時數(一天就打24hr)</p>
  <center><input type="text" v-model="hour" /></center>
  <hr/>
  <p>每日度數: {{ duo }} 每2個月度數: {{ duomon }} 以 {{ duoey }} 累積電價</p>
  <p>兩個月累積電費: {{ duocadd }}</p>
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
          { name: 500, price: 3.70 },
          { name: 700, price: 5.04 },
          { name: 1000, price: 6.24 },
          { name: 1001, price: 8.46 },
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
      if (this.duomon <120) {
        return this.duoey = 1.68;
      } else if (this.duomon < 330) {
        return this.duoey = 2.45;
      } else if (this.duomon < 500) {
        return this.duoey = 3.7;
      } else if (this.duomon < 700) {
        return this.duoey = 5.04;
      } else if (this.duomon < 1000) {
        return this.duoey = 6.24;
      } else if (this.duomon < 1001) {
        return this.duoey = 8.46;
      }
   },
    // 計算電費
    duocap() {
      if(this.duoey === 1.68){
        this.duocadd = this.taidal[0].price * this.duomon - this.taidal[0].price * this.taidal[0].name;
      } else if(this.duoey ===2.45){
        this.duocadd = this.taidal[1].price * this.duomon - this.taidal[0].price * (this.taidal[1].name - this.taidal[0].name);
      } else if(this.duoey === 3.7){
        this.duocadd = this.taidal[2].price * (this.duomon-this.taidal[1].name) + this.taidal[1].price * (this.taidal[1].name - this.taidal[0].name) + this.taidal[0].price * this.taidal[0].name;
      } else if(this.duoey === 5.04){
        this.duocadd = this.taidal[3].price * this.duomon - this.taidal[2].name + this.taidal[2].price * (this.taidal[1].name - this.taidal[0].name) + this.taidal[0].price * this.taidal[0].name;
      } else if(this.duoey === 6.24){
        this.duocadd = this.taidal[4].price * this.duomon - this.taidal[3].name + this.taidal[3].price * (this.taidal[1].name - this.taidal[0].name) + this.taidal[0].price * this.taidal[0].name;
      } else if(this.duoey === 8.46){
        this.duocadd = this.taidal[5].price * this.duomon - this.taidal[4].name + this.taidal[4].price * (this.taidal[1].name - this.taidal[0].name) + this.taidal[0].price * this.taidal[0].name;
      }
    },
  },
}
</script>

<style>
h3 {
  text-align: center;
  color: #2c3e50;
  margin-bottom: 30px;
}
p {
  text-align: center;
  color: #2c3e50;
  margin-bottom: 30px;
}
input {
  text-align: center;
  color: #2c3e50;
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
  border: 1px solid #2c3e50;
}
input[type="text"]:hover {
  border: 1px solid #2c3e50;
}
input[type="text"]:active {
  border: 1px solid #2c3e50;
}
p:hover {
  color: #2c3e50;
}
p:active {
  color: #2c3e50;
}
p:focus {
  color: #2c3e50;
}
input[type="text"]:focus {
  color: #2c3e50;
}
input[type="text"]:hover {
  color: #2c3e50;
}
input[type="text"]:active {
  color: #2c3e50;
}
p:focus {
  color: #2c3e50;
}
p:hover {
  color: #2c3e50;
}
p:active {
  color: #2c3e50;
}
input[type="text"]:focus {
  color: #2c3e50;
} 
</style>
