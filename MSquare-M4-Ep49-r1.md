## MSquare Programing Fullstack Course

### Episode-_4_

### Summary For  `Room(1)`  intermediate Class
##
### Episode-48 မှာ ရေးခဲ့တဲ့ code တွေကို clean နဲ့ powerful ဖြစ်အောင် ပြန်ရေးကြပါမယ်
- အရင်ဆုံး data တွေ ပြန်သတ်မှတ်ပါမယ်
- ပြီးရင် autocomplete ကနေ ရှာလိုက်တဲ့ အခါ station name သက်သက်ကိုပဲ မယူတော့ပဲ သူ့ရဲ့ object တစ်ခုလုံး ကို ယူလိုက်ပါမယ်
```js
// Bus.tsx
import { Autocomplete, Box, Button, Input, TextField } from "@mui/material";
import React, { useEffect, useState } from "react";

interface Station {
  id: number;
  label: string;
}

interface Busses {
  id: number;
  name: string;
  stations: Station[];
}
const busses: Busses[] = [
  {
    id: 1,
    name: " line 30",
    stations: [
      { id: 1, label: "hledan" },
      { id: 2, label: "myaynigone" },
      { id: 3, label: "mayangone" },
      { id: 4, label: "tamwe" },
      { id:  6, label:  "suelay" },
    ],
  },
  {
    id: 2,
    name: " line 40",
    stations: [
      { id: 5, label: "hlaing" },
      { id: 2, label: "myaynigone" },
      { id: 3, label: "mayangone" },
      { id: 6, label: "suelay" },
    ],
  },
  {
    id: 3,
    name: " line 50",
    stations: [
      { id: 7, label: "mandalay" },
      { id: 8, label: "yangon" },
      { id: 6, label: "suelay" },
    ],
  },
];

const stations: Station[] = [
  { id: 1, label: "hledan" },
  { id: 2, label: "myaynigone" },
  { id: 3, label: "mayangone" },
  { id: 4, label: "tamwe" },
  { id: 5, label: "hlaing" },
  { id: 6, label: "suelay" },
  { id: 7, label: "mandalay" },
  { id: 8, label: "yangon" },
];
interface StartAndEndStations {
  startStation: Station | null;
  endStation: Station | null;
}

interface Route {
  startBus: Busses;
  endBus: Busses;
  startStation: Station | null;
  endStation: Station | null;
  switchStations: Station[];
}
const Bus = () => {
  const [searchStations, setSearchStations] = useState<StartAndEndStations>({
    startStation: null,
    endStation: null,
  });

  useEffect(() => {
     console.log(searchStations);
  }, [searchStations]);

  const searchBus = () => {};

  return (
    <Box
      sx={{
        display: "flex",
        justifyContent: "center",
        width: "100%",
      }}
    >
      <Box sx={{ m: "10px" }}>
        <Autocomplete
          options={stations}
          onChange={(event, value) =>
            value &&
            setSearchStations({ ...searchStations, startStation: value })
          }
          sx={{ width: 200 }}
          renderInput={(params) => <TextField {...params} label="From" />}
        />
      </Box>

      <Box sx={{ m: "10px" }}>
        <Autocomplete
          options={stations}
          onChange={(event, value) =>
            value && setSearchStations({ ...searchStations, endStation: value })
          }
          sx={{ width: 200 }}
          renderInput={(params) => <TextField {...params} label="To" />}
        />
      </Box>
      <Button
        variant="contained"
        sx={{ height: "30px", m: "20px" }}
        onClick={searchBus}
      >
        find Bus
      </Button>
    </Box>
  );
};

export default Bus;

```
- busses array နဲ့ station array ကို အသစ်ပြန်သတ်မှတ်လိုက်ပါတယ်
- start and end station နဲ့ route ဆိုတဲ့ data တွေအတွက် type တွေ သတ်မှတ်ထားပါတယ်
- autocomplete ကနေ ရှာလိုက်တဲ့ အခါ station name သက်သက်ကိုပဲ မယူတော့ပဲ သူ့ရဲ့ object တစ်ခုလုံး ကို ယူလိုက်ပါတယ်
- အခု app ကို စမ်းကြည့်လိုက်ရင် ရွေးလိုက်တဲ့ station တွေနဲ့ သက်ဆိုင်တဲ့ object တစ်ခုလုံး log ထုတ်ပေးမှာဖြစ်ပါတယ်
##
- ဆက်ပြီး autocomplete ကနေ ရှာလိုက်တဲ့ station နှစ်လုံးရှိမှ find bus button ကို အလုပ်လုပ်အောင် စစ်ပါမယ်
```js
  const searchBus = () => {
    const hasFoundBothStations =
      searchStations.startStation && searchStations.endStation;

    if (!hasFoundBothStations) return;

  };
```
- လိုအပ်တဲ့ station နှစ်ခု ရှိမရှိ စစ်လိုက်ပြီး မရှိခဲ့ပါက return လုပ်ပြီး code တွေ ဆက် မ run တော့အောင် လုပ်လိုက်ပါတယ်
- ဒါကို early return လို့ ခေါ်ပါတယ်။ app တစ်ခု လုပ်တဲ့ အချိန်မှာ အရေးကြီးတဲ့ အဆင့်ဖြစ်ပါတယ်။
- ဆက်ပြီး လိုအပ်တဲ့ data တွေရပြီး ဆိုပါက ရွေးလိုက်တဲ့ station ပါတဲ့ bus ကို ဆက်ရှာပါမယ်။
```js
 const searchBus = () => {
    const hasFoundBothStations =
      searchStations.startStation && searchStations.endStation;

    if (!hasFoundBothStations) return;

    let routes: Route[] = [];
    busses.forEach((buss) => {
      const currentBusStations = buss.stations;
      const hasStartStation = currentBusStations.find(
        (station) => station.id === searchStations.startStation?.id
      );
      const hasEndStation = currentBusStations.find(
        (station) => station.id === searchStations.endStation?.id
      );

      if (hasStartStation && hasEndStation) {
        routes.push({
          startBus: buss,
          endBus: buss,
          startStation: searchStations.startStation,
          endStation: searchStations.endStation,
          switchStations: [],
        });
        console.log("routes", routes);
      }
    });
  };
```
- busses array ထဲက bus တွေ loop လုပ်ပြီး autocomplete ထဲ ရွေးပေးလိုက်တဲ့ station နှစ်ခု ပါမပါ ရှာပါတယ်
- ပါခဲ့လို့ရှိရင် routes array ထဲ push လုပ်လိုက်တာဖြစ်ပါတယ်။
- ဒါက direct သွားလို့ရမယ့် bus ကို ရှာလိုက်တာဖြစ်ပါတယ်
- အခု app မှာ bus တစ်စီးထဲ ရောက်မယ့် station နှစ်ခု ရွေးကြည့်လိုက်ရင် console က routes ထဲ တိုက်ရိုက်ရောက်တယ့် bus ကို  ပြပေးနေမှာဖြစ်ပါတယ်။

![enter image description here](https://raw.githubusercontent.com/Aungmyanmar32/msquare-m4/main/Screenshot%202023-03-31%20131601.png)
##
### Find indirect Busses with common stations
- ဆက်ပြီး indirect Busses ကို ရှာကြည့်ပါမယ်
- အရင်ဆုံး from station ကနေ ထွက်မယ့် bus နဲ့ to station ဆီ  ရောက်မယ့် bus တွေကို အရင်ရှာပါမယ်
```js
//In searchBus function (Bus.tsx)

  //indirect busses
    const bussesWithStartStation = busses.filter((bus) =>
      bus.stations.find(
        (station) => station.id === searchStations.startStation?.id
      )
    );
    const bussesWithEndStation = busses.filter((bus) =>
      bus.stations.find(
        (station) => station.id === searchStations.endStation?.id
      )
    );
    console.log(bussesWithStartStation, bussesWithEndStation);
```
- from hledan to suelay လို့ ရွေးကြည့်ပါကbussesWithStartStatio အဖြစ် hledan ကနေ စထွက်တဲ့ line 30 bus နဲ့ bussesWithEndStation အဖြစ် suelay ရောက်တဲ့ line 40 ,line 50 bus တွေကို console မှာ ပြပေးမှာဖြစ်ပါတယ်။
- ဆက်ပြီးတော့ bus တွေမှာ တူညီတဲ့ ဘုံ station ပါမပါ စစ်ပါမယ်။
```js
//In searchBus function (Bus.tsx)

....
console.log(bussesWithStartStation, bussesWithEndStation);

//find common station
  //find common station
    bussesWithStartStation.forEach((startBusses) => {
      bussesWithEndStation.forEach((endBusses) => {
        //If direct or not
        const isDirectbus = routes.find(
          (route) =>
            route.startBus.id === startBusses.id &&
            route.endBus.id === endBusses.id
        );
        
//loop and compare both start and end buss station
        startBusses.stations.forEach((startBussesStaion) => {
          endBusses.stations.forEach((endBussesStation, index) => {

            // check startbus and end bus has common station
            if (
              startBussesStaion.id === endBussesStation.id &&
              index !== endBusses.stations.length - 1
            ) {

              //check routes is already exist or not
              const route = routes.find(
                (route) =>
                  route.startBus.id === startBusses.id &&
                  route.endBus.id === endBusses.id
              );

              //when routes exist
              if (route) {
                routes.map((route) => {
                  if (
                    route.startBus.id === startBusses.id &&
                    route.endBus.id === endBusses.id
                  ) {
                    return {
                      ...route,
                      switchStations: isDirectbus
                        ? []
                        : [...route.switchStations, endBussesStation],
                    };
                  }
                  return route;
                });
              } else {
                //when routes not exist
                routes.push({
                  startBus: startBusses,
                  endBus: endBusses,
                  startStation: searchStations.startStation,
                  endStation: searchStations.endStation,
                  switchStations: isDirectbus ? [] : [endBussesStation],
                });
              }
            }
          });
        });
      });
      console.log(routes);
    });
```
> ရှင်းလင်ချက်


```js
//find common station
    bussesWithStartStation.forEach((startBusses) => {
      bussesWithEndStation.forEach((endBusses) => {
        //If direct or not
        const isDirectbus = routes.find(
          (route) =>
            route.startBus.id === startBusses.id &&
            route.endBus.id === endBusses.id
        );
        
//loop and compare both start and end buss station
        startBusses.stations.forEach((startBussesStaion) => {
          endBusses.stations.forEach((endBussesStation, index) => {

            // check startbus and end bus has common station
            if (
              startBussesStaion.id === endBussesStation.id &&
              index !== endBusses.stations.length - 1
            ) {

              //check routes is already exist or not
              const route = routes.find(
                (route) =>
                  route.startBus.id === startBusses.id &&
                  route.endBus.id === endBusses.id
              );
```
- start station ကနေ ထွက်သမျှ bus တွေ ရောက်တဲ့ station အားလုံးကို loop လုပ်ပါတယ်
- အဲ့ဒီ loop အထဲမှာ end station ရောက်တဲ့ bus တွေ  ရပ်တဲ့ station အားလုံးကို ထပ် loop 
လုပ်ပြီး routes ရှိနေပြီးသားလား အသစ်ထပ်ထည့်ရမလားဆိုတာကို စစ်လိုက်ပါတယ်။

```js
            if (route) {
                routes.map((route) => {
                  if (
                    route.startBus.id === startBusses.id &&
                    route.endBus.id === endBusses.id
                  ) {
                    return {
                      ...route,
                      switchStations: isDirectbus
                        ? []
                        : [...route.switchStations, endBussesStation],
                    };
                  }
                  return route;
                });
```
- route ရှိခဲ့ရင် အဲ့ဒီ route ကိုပဲ copy လုပ်ပြီး switch stations မှာလည်း direct bus ဆိုရင် empty array ပဲ ပြန်ထည့်ပေးလိုက်ပြီး indirect bus ဆိုရင် bus ပြောင်းလို့ရမယ့် station ကို ထည့်ပေးလိုက်ပါတယ်။
```js
        else {
                //when routes not exist
                routes.push({
                  startBus: startBusses,
                  endBus: endBusses,
                  startStation: searchStations.startStation,
                  endStation: searchStations.endStation,
                  switchStations: isDirectbus ? [] : [endBussesStation],
                });
              }
```
- routes က မရှိခဲ့ရင် routes array ထဲ ကို လိုအပ်တဲ့ data ကို push လုပ်လိုက်တာဖြစ်ပါတယ်။
- အခု bus app ကို စမ်းသပ်ကြည့်တဲ့အခါ direct bus ရှိရင် ထို bus ကို log ထုတ်ပေးမှာ ဖြစ်ပြီး
- indirect bus ပဲ ရှိခဲ့ရင် bus နှစ်စီးနဲ့  ပြောင်းစီးလို့ရမယ့် station ကို ပါ switch station မှာ ပြပေးမှာဖြစ်ပါတယ်
- ရွေးလိုက်တဲ့ stations နှစ်ခုက direct bus ကော indirect bus ပါရှိခဲ့ အထက်က နှစ်ခုလုံးကို ပြပေးမှာဖြစ်ပါတယ်
