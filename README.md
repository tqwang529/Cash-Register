# Cash-Register

var denominations=[
    {name: "ONE HUNDRED", value: 100.00},
    {name: "TWENTY", value: 20.00},
    {name: "TEN", value: 10.00},
    {name: "FIVE", value: 5.00},
    {name: "ONE", value: 1.00},
    {name: "QUARTER", value: 0.25},
    {name: "DIME", value: 0.10},
    {name: "NICKLE", value: 0.05},
    {name: "PENNY", value: 0.01},
  ];
  function checkCashRegister(price, cash, cid) {
    var change= cash-price;
    var totalCid=cid.reduce((acc,curr)=>{
      return acc+curr[1];
    },0.0);
  if (totalCid<change){
    return "INSUFFICIENT_FUNDS";
  } else if (totalCid===change){
    return "CLOSED";
  }
  cid=cid.reverse();

var result= denominations.reduce((acc,curr,index)=>{
  if (change>= curr.value){
    var currentValue = 0.0;
    while(change>=curr.value && cid[index][1]>=curr.value){
      currentValue+=curr.value;
      change-=curr.value;
      change= Math.round(change*100)/100;
      cid[index][1]-=curr.value;
    }
    acc.push([curr.name,currentValue]);
    return acc;
  } else{
    return acc;
  }
},[]);
return result.length>0 && change===0 ? result: "INSUFFICIENT_FUNDS";
}

// test project 
// first argument: Price; second argument: cash; third argument: cash in drawer.
console.log(checkCashRegister(19.5, 20, [["PENNY", 0.5], ["NICKEL", 0], ["DIME", 0], ["QUARTER", 0], ["ONE", 0], ["FIVE", 0], ["TEN", 0], ["TWENTY", 0], ["ONE HUNDRED", 0]]));
console.log(checkCashRegister(3.26, 100, [["PENNY", 1.01], ["NICKEL", 2.05], ["DIME", 3.1], ["QUARTER", 4.25], ["ONE", 90], ["FIVE", 55], ["TEN", 20], ["TWENTY", 60], ["ONE HUNDRED", 100]]));
console.log(checkCashRegister(19.5, 20, [["PENNY", 0.01], ["NICKEL", 0], ["DIME", 0], ["QUARTER", 0], ["ONE", 0], ["FIVE", 0], ["TEN", 0], ["TWENTY", 0], ["ONE HUNDRED", 0]]));
