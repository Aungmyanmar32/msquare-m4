## MSquare Programing Fullstack Course

### Episode-_46_

### Summary For  `Room(1)`  intermediate Class
##
## Data modeling
### web app တစ်ခု လုပ်တော့မယ် အရင်ဆုံး database မှာ data တွေ 
- ဘယ်လိုသိမ်းမယ်? 
- ဘယ်လိုထားမယ်?
- ဘယ်လိုချိတ်ဆက်မလဲ?
စတာတွေကို သေချာ လုပ်ရပါမယ်
- ခု သင်ခန်းစာမှာ လုပ်နေတဲ့ Bus app မှာလည်း Data modeling အတွက်သေချာ လုပ်ကြည့်ရအောင်
##
- အရင်ဆုံး components folder အောက်မှာ Busses folder တစ်ခု လုပ်ပြီး Busses.tsx component တစ်ခုလုပ်ပါမယ်။
- Busses component ထဲမှာ busses array တစ်ခုလုပ်ပါမယ်
```js
//Busses.tsx 

interface Station {
  from: string;
  to: string;
  duration: string;
}

export interface Bus {
  id: number;
  name: string;
  departureTimes: string[];
  price: number;
  hasAircon: boolean;
  totalStations: Station[];
}

export let busses: Bus[] = [
  {
    id: 1,
    name: "line 30",
    departureTimes: ["10:00 ", "10:30", "11:00", "11:30"],
    price: 30,
    hasAircon: true,
    totalStations: [
      {
        from: "Hledan",
        to: "Myaynigone",
        duration: "10min",
      },
      {
        from: "Myanigone",
        to: "Yankin",
        duration: "15min",
      },
      {
        from: "Yankin",
        to: "Tamwe",
        duration: "20min",
      },
    ],
  },
  {
    id: 1,
    name: "line 40",
    departureTimes: ["14:00 ", "16:30", "18:00", "19:30"],
    price: 30,
    hasAircon: false,
    totalStations: [
      {
        from: "Myaynigone",
        to: "Insein",
        duration: "10min",
      },
      {
        from: "Insein",
        to: "Suelay",
        duration: "5min",
      },
      {
        from: "Suelay",
        to: "Aung San",
        duration: "20min",
      },
    ],
  },
  {
    id: 3,
    name: "line 50",
    departureTimes: ["1:00 ", "5:30", "7:00", "8:30"],
    price: 30,
    hasAircon: true,
    totalStations: [
      {
        from: "Hledan",
        to: "Myaynigone",
        duration: "60min",
      },
      {
        from: "Myanigone",
        to: "Yankin",
        duration: "15min",
      },
      {
        from: "Yankin",
        to: "Tamwe",
        duration: "20min",
      },
    ],
  },
  {
    id: 4,
    name: "line 30",
    departureTimes: ["10:00 ", "10:30", "11:00", "11:30"],
    price: 30,
    hasAircon: true,
    totalStations: [
      {
        from: "Hledan",
        to: "Myaynigone",
        duration: "10min",
      },
      {
        from: "Myanigone",
        to: "Yankin",
        duration: "15min",
      },
      {
        from: "Yankin",
        to: "Tamwe",
        duration: "20min",
      },
    ],
  },
];

```
- busses array ထဲမှာ bus လိုင်း တစ်လိုင်းစီ အတွက်

     - id
    - name
   - departureTimes
   - price
   - hasAircon
   - totalStations
- စတာတွေ သတ်မှတ်ထားပါတယ်။
##
- busses array ထဲမှာရှိတဲ့ station တွေ ကို function တစ်ခုနဲ့ စစ်ထုတ်ပါမယ်။
```js
export const getAllStations = () => {
  const allStations: string[] = [];
  busses.forEach((bus) => {
    bus.totalStations.forEach((station) => {
      const fromStation = station.from;
      const toStation = station.to;
      const isExistFromStation = allStations.includes(fromStation);
      const isExistToStation = allStations.includes(toStation);
      if (!isExistFromStation) allStations.push(fromStation);
      if (!isExistToStation) allStations.push(toStation);
    });
  });
  return allStations;
};
```
- busses array ကို loop လုပ်လိုက်ပြီး အဲ့ဒီအထဲမှာ totalStations ကို loop ထပ်လုပ်ကာ ရှိသမျှ station တွေကို အရင်ထုတ်လိုက်ပါတယ်
-  ရှိသမျှ station တွေထဲကမှ from နဲ့ to station တွေကို ထပ်ယူလိုက်ပါတယ်။
- station တွေ မထပ်ရအောင် from နဲ့ to station တွေ ထဲကမှ မတူတဲ့ station တွေကို allStations array ထဲ push လုပ်ပြီး သိမ်းလိုက်ဖြစ်ပါတယ်
## Try this 
- အထက်က ပြူလုပ်ထားတဲ့ data တွေကို အသုံးပြုပြီး autocomplete input မှာ station တွေ ရွေးလို့ရအောင် လုပ်ကြည့်ကြပါ
- ထပ်ပြီး direct bus ရှိမရှိ ပါ ပြလို့ရအောင် စမ်းကြည့်ကြပါ။
-
![enter image description here](https://raw.githubusercontent.com/Aungmyanmar32/msquare-m4/main/Screenshot%202023-03-29%20091345.png)
