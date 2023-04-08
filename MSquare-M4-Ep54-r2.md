## MSquare Programing Fullstack Course
### Episode-*54* 
### Summary For `Room(2)`
##
### param and query string 
![enter image description here](https://raw.githubusercontent.com/Aungmyanmar32/msquare-m4/main/paramquery.png)
### Request to Server with param
- param ကို အသုံးပြုပြီး server ဆီ REQUEST လုပ်ကြည့်ရအောင်
```js
// backend/server.ts

app.get("/users/:id", (req, res) => {
  const param = req.params;
 
  console.log("param", param);
  
 res.send(param)
  
});

```
- param အနေနဲ့ ၀င်လာတဲ့ data ကို id ဆိုတဲ့ key နဲ့ ဖမ်းထားလိုက်ပါတယ်
- { id : param} ဆိုပြီး object တစ်ခုအနေနဲ့ ရလာမှာဖြစ်ပါတယ်
- အဲ့တာကို Postman ကနေ request လုပ်ကြည့်ပါမယ်

![enter image description here](https://raw.githubusercontent.com/Aungmyanmar32/msquare-m4/main/queryparam%20%281%29.png)

##
### request to server with query
- query ကို အသုံးပြုပြီး server ဆီ REQUEST လုပ်ကြည့်ရအောင်
- backend ထဲက server.ts မှာ အရင် ပြင်ဆင်ပါမယ်။
```js\
// backend/server.ts

app.get("/users", (req, res) => {
  const query = req.query;

  console.log("query", query);

  res.send(query);
});
```
- query ကို လက်ခံတဲ့အခါ params
- postman ကနေ request လုပ်တဲ့အခါမှာ url ထဲ query ထည့်ပြီး request လုပ်ပါမယ်။
![enter image description here](https://raw.githubusercontent.com/Aungmyanmar32/msquare-m4/main/queryparam%20%283%29.png)
![enter image description here](https://raw.githubusercontent.com/Aungmyanmar32/msquare-m4/main/queryparam%20%282%29.png)
- { name: "aung"} ဆိုပြီး server မှာ log ထုတ်ပေးတာမြင်ရမှာပါ
##
### request to server with both param and query
- ခုတစ်ခါ ကျတော့ param ရော query ပါ ထည့်ပြီး request လုပ်ကြည့်ပါမယ်.
```js
// backend/server.ts
app.get("/users/:id", (req, res) => {
  
  const query = req.query;
  const param = req.params;

  console.log("query", query);
  console.log("param", param);

  res.send({ query, param });
});
```
![enter image description here](https://raw.githubusercontent.com/Aungmyanmar32/msquare-m4/main/queryparam%20%284%29.png)
##
### request to sever with month query in react project
- ခု ကျနော်တို့ project မှာ ဆက်ပြီး လေ့လာသွားကြပါမယ်
- အရင်ဆုံး backed folder ထဲမှာ data.ts ဖိုင်တစ်ခု လုပ်ပြီး availability array တစ်ခု လုပ်ပါမယ်။
```js
// backend/data.ts
export interface Slot {
  time: number;
  totoalSlot: number;
  bookedSlot: number;
  availableSlot: number;
}

export interface Availability {
  date: string;
  month: number;
  slots: Slot[];
}

export const availability: Availability[] = [
  {
    date: "07-04-2023",
    month: 3,
    slots: [
      { time: 9, totoalSlot: 100, bookedSlot: 50, availableSlot: 50 },
      { time: 10, totoalSlot: 100, bookedSlot: 70, availableSlot: 30 },
      { time: 11, totoalSlot: 100, bookedSlot: 20, availableSlot: 80 },
      { time: 12, totoalSlot: 100, bookedSlot: 100, availableSlot: 0 },
      { time: 13, totoalSlot: 100, bookedSlot: 60, availableSlot: 40 },
    ],
  },
  {
    date: "08-04-2023",
    month: 3,
    slots: [
      { time: 9, totoalSlot: 100, bookedSlot: 50, availableSlot: 50 },
      { time: 10, totoalSlot: 100, bookedSlot: 70, availableSlot: 30 },
      { time: 11, totoalSlot: 100, bookedSlot: 20, availableSlot: 80 },
      { time: 12, totoalSlot: 100, bookedSlot: 100, availableSlot: 0 },
      { time: 13, totoalSlot: 100, bookedSlot: 60, availableSlot: 40 },
    ],
  },
  {
    date: "09-04-2023",
    month: 3,
    slots: [
      { time: 9, totoalSlot: 100, bookedSlot: 50, availableSlot: 50 },
      { time: 10, totoalSlot: 100, bookedSlot: 70, availableSlot: 30 },
      { time: 11, totoalSlot: 100, bookedSlot: 20, availableSlot: 80 },
      { time: 12, totoalSlot: 100, bookedSlot: 100, availableSlot: 0 },
      { time: 13, totoalSlot: 100, bookedSlot: 60, availableSlot: 40 },
    ],
  },
  {
    date: "01-05-2023",
    month: 4,
    slots: [
      { time: 9, totoalSlot: 100, bookedSlot: 50, availableSlot: 50 },
      { time: 10, totoalSlot: 100, bookedSlot: 70, availableSlot: 30 },
      { time: 11, totoalSlot: 100, bookedSlot: 20, availableSlot: 80 },
      { time: 12, totoalSlot: 100, bookedSlot: 100, availableSlot: 0 },
      { time: 13, totoalSlot: 100, bookedSlot: 60, availableSlot: 40 },
    ],
  },
];


```
- ပြီးရင် request နဲ့အတူ ပါလာမယ့် month ( query) ကို availability array ထဲရှိ month နဲ့ တူမတူ စစ်ထုတ်ပြီး response ပြန်လုပ်ပေးမှာဖြစ်ပါတယ်။
```js
// backend /server.ts

import express from "express";
import cors from "cors";
import { availability } from "./data";
const app = express();
const port = 5000;
app.use(cors());

// app.get("/users/:id", (req, res) => {
//   const query = req.query;
//   const param = req.params;

//   console.log("query", query);
//   console.log("param", param);

//   res.send({ query, param });
// });

app.get("/availability", (req, res) => {
  //@ts-ignore
  const choosenMonth = parseInt(req.query.month, 10);
  console.log(choosenMonth);

  const foundedAvailability = availability.filter(
    (ele) => ele.month === choosenMonth
  );
  console.log(foundedAvailability);

  res.send(foundedAvailability);
});

app.listen(port, () => {
  console.log(`Example app listening on port ${port}!`);
});

```
>ရှင်းလင်းချက်

```
app.get("/availability", (req, res) => {
  //@ts-ignore
  const choosenMonth = parseInt(req.query.month, 10);
  console.log(choosenMonth);

  const foundedAvailability = availability.filter(
    (ele) => ele.month === choosenMonth
  );
  console.log(foundedAvailability);

  res.send(foundedAvailability);
});
```
- query အနေနဲ့ ပါလာမယ့် month ကို number type အရင်ပြောင်းလိုက်ပါတယ်
- availability array ထဲ က month နဲ့ choosenMonth  ရဲ့ တန်ဖိုး တူမတူ တိုက်စစ်လိုက်ပြီး တူတဲ့ elementတွေကို filter လုပ်ပြီး foundedAvailability  arrayအနေနဲ့ သိမ်းလိုက်တာဖြစ်ပါတယ်။
- နောက်ဆုံးအနေနဲ့ foundedAvailability  array ကို response လုပ်ပေးလိုက်ပါတယ်။
- ၀င်လာမယ့် request အတွက် ဆာဗာမှာ ပြင်ဆင်လို့ပြီးပါပြီး။
##
- ခု backend ကော frontend နှစ်ခုလုံး start လုပ်ထားပြီး Date picker မှာ april လ ထဲက ရက်တစ်ရက်ကိုရွေးကြည့်လိုက်ပါက 
  - backend server ထဲရှိ data က month : 3 ဖြစ်တဲ့ dataတွေ log ထုတ်ပေးတာကို မြင်ရမှာဖြစ်ပါတယ်။
  
  ![enter image description here](https://raw.githubusercontent.com/Aungmyanmar32/msquare-m4/main/Screenshot%202023-04-08%20152623.png)

