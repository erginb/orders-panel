<template>
    <div class="card card--one">
      <p class="card__number">
        <span>Lost: {{lostsInRole}}</span> -
        <span>Win: {{winsInRole}}</span>
      </p>
      <ul class="list" >

        <li v-for="(order,i) in ordersTF" :key="i" 
        :class="checkType(order)">{{countOrders(ordersTF,i)}}</li>
       
        
      </ul>
      <!--  <p class="card__owner">Gale P</p>
      <div class="card__info">
        <p class="card__integral">Integral: 0</p>
        <p class="card__amount">Amount: 500,087</p>
      </div>-->  
    </div>
</template>

<script>
export default {
  name:'CardItems',
  props: ['ordersTF'],
  mounted() {
    //console.log(this.ordersTF)
  },
  computed: {
lostsInRole: function() {
      let maxLost = 0;
      let curLost = 0;
      let lastDay = "";
      this.ordersTF.map(a => {
        const openTime = a.openTime.split(' ')[0];
        if(lastDay ==="") lastDay = openTime
        else {
          if(openTime !== lastDay) {
            curLost = 0;
            lastDay = openTime;
          }
        }
        if (a.netProfit < 0) curLost++;
        else curLost = 0;

        if (curLost > maxLost) maxLost = curLost;
      });
      return maxLost;
    },
    winsInRole: function() {
      let maxWin = 0;
      let curWin = 0;
      let lastDay = ""
      this.ordersTF.map(a => {
        const openTime = a.openTime.split(' ')[0];
        if(lastDay ==="") lastDay = openTime
        else {
          if(openTime !== lastDay)  {
            curWin = 0;
            lastDay = openTime;
            }
        }
        if (a.netProfit > 0) curWin++;
        else curWin = 0;

        if (curWin > maxWin) maxWin = curWin;
      });
      return maxWin;
    },
  },
  methods: {
    countOrders: function(orders,i) {
      if(i>0) {
        let type = -1;
        var count = 1;
        if(orders[i].netProfit>0) type =1
        for(let a = i; a+1>0; a-- ) {
          if(type===1 && orders[a].netProfit<0) break;
          else if(type===-1 && orders[a].netProfit>0) break;
          else count++;
          
        }
      }
      else return 1
      return count-1
    },
    
    checkType: function (order) {
      if(order.netProfit>0) return 'list-item list-item-win'
      return  'list-item list-item-lost'
    }
  }
}
</script>

