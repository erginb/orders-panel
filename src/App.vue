<template>
<Card :orders="orders"/>
</template>

<script>
import Card from './components/Card'
const awsUrl = process.env.awsURL
const dumpCSV1 = awsUrl+'HistoryDumpCSV_44187485.csv'

export default {  
  name: "App",
  components: {Card},
  data() {
    return {
      json: []
    }
  },
  mounted() {
    this.fetchData()
    setInterval(this.fetchData, 30000)
   /* if(localStorage.getItem('json') === null) this.fetchData()
    else {
      this.json = JSON.parse(localStorage.getItem('json'))
    }*/
    
  },
  computed: {
    orders: function() {
      //console.log(this.json[0])
      const data = this.filterData(this.json)
      //console.log(data)
      return data
    }
  },
  methods: {
    fetchData: function() {
      console.log('fetchedData')
      fetch(dumpCSV1)
      .then(res => res.text())
      .then(res => JSON.parse(this.csvJSON(res)))
      .then(json => {
        this.json = json
        localStorage.setItem('json',JSON.stringify(json))
      })
      
    },
    filterData: ( json) => {
    const todayDate = new Date(new Date().setHours(0,0,0,0))
      /*const {
        symbol,
        magicNumber
      } = props;*/
      let data = json.map(d => {
        return {
          type: d.Type,
          symbol: d.Symbol,
          ticket: parseInt(d.Ticket,0),
          profit: parseFloat(d.Profit,2),
          netProfit: parseFloat(d.NetProfit,2),
          openTime: d.ServerOpenTime,
          openTime_MT: d.ServerOpenTime_MT,
          closeTime: d.ServerCloseTime,
          closeTime_MT: d.ServerCloseTime_MT,
          magicNumber: parseInt(d.MagicNumber,0),
          lots: parseFloat(d.Lots,2),
          points: parseInt(d.Points,0),
          pips: parseInt(d.Pips,0),
          openPrice: parseFloat(d.OpenPrice,5),
          closePrice: parseFloat(d.ClosePrice,5),
          takeProfitPrice: parseFloat(d.TakeProfit,5),
          stopLossPrice: parseFloat(d.StopLoss,5)
        };
      });
     // console.log(data[0])
      data = data
        //.filter(a => a.symbol === symbol)
        .filter(c => c.type === "OP_SELL" || c.type === "OP_BUY")
        //.filter(d => new Date(d.openTime_MT) > todayDate)
        //.filter(m => m.magicNumber === magicNumber)
        .filter(g => {
          var openTimeAll = g.openTime_MT.split(" ");
          var openDate = openTimeAll[0].split(".");
          return (
            parseInt(openDate[0], 0) === todayDate.getFullYear() && // beginYear &&
            parseInt(openDate[1], 0) === todayDate.getMonth()+1 && //beginMonth &&
            parseInt(openDate[2], 0) === todayDate.getDate()         
          )
        })

      data = data.sort((a, b) => (a.ticket > b.ticket) ? 1 : -1)
      //console.log(data)
      return data;
    
    },
    csvJSON: function(csv) {
      var lines=csv.split("\n");
      var result = [];
      var headers=lines[0].split(",");

      for(var i=1;i<lines.length;i++) {
        var obj = {};
        var currentline=lines[i].split(",");
      
        for(var j=0;j<headers.length;j++){
          obj[headers[j]] = currentline[j];
        }
        //if(i===1) console.log(obj)
        result.push(obj);
      }
  
      //return result; //JavaScript object
    return JSON.stringify(result); //JSON
    },
  }
  
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
