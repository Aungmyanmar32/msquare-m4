## MSquare Programing Fullstack Course

### Episode-_48_

### Summary For  `Room(1)`  intermediate Class
##
## find common station 
### ပြီးခဲ့တဲ့ သင်ခန်းစာတွေမှာ လေ့လာခဲ့တဲ့ bus tracking app မှာ သွားချင်တဲ့ station တွေ ရောက်ဖို့ bus နှစ်ဆင့်ပြောင်းစီးရမယ်ဆိုလို့ရှိရင် Bus ပြောင်းစီးရမယ့် station ကို ရှာကြည့်ရအောင်။
- အရင်ဆုံး Bus.tsx ထဲမှာ အရင်လုပ်ထားတဲ့ state တွေ ဖျက်ပြီး state အသစ်တစ်ခု ပြန်လုပ်ပါမယ်
- autocomplete input နှစ်ခု စလုံးက ရွေးလိုက်တဲ့ station တွေကို အသစ်လုပ်ထားတဲ့ state ထဲမှာ သိမ်းလိုက်မှာ ဖြစ်ပါတယ်။
```js
// Bus.tsx

import { Autocomplete, Box, Input, TextField } from "@mui/material";
import React, { useEffect, useState } from "react";

const stations = [
  {
    id: 1,
    label: "hledan",
    destination: [
      {
        id: 2,
        label: "myaynigone",
      },
      {
        id: 3,
        label: "mayangone",
      },
    ],
  },
  {
    id: 2,
    label: "myaynigone",
    destination: [
      {
        id: 1,
        label: "hledan",
      },
      {
        id: 3,
        label: "mayangone",
      },
    ],
  },
  {
    id: 3,
    label: "mayangone",
    destination: [
      {
        id: 4,
        label: "suelay",
      },
    ],
  },
  {
    id: 4,
    label: "suelay",
    destination: [],
  },
];

interface Station {
  id: number;
  label: string;
  destination: Destination[];
}

interface Destination {
  id: number;
  label: string;
}
const Bus = () => {
//create search station state as object
  const [searchStations, setSearchStations] = useState({
    startStation: "",
    stopStation: "",
  });
  useEffect(() => {
    console.log(searchStations);
  }, [searchStations]);

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
            setSearchStations({ ...searchStations, startStation: value.label })
          }
          sx={{ width: 300 }}
          renderInput={(params) => <TextField {...params} label="From" />}
        />
      </Box>

      <Box sx={{ m: "10px" }}>
        <Autocomplete
          options={stations}
          onChange={(event, value) =>
            value &&
            setSearchStations({ ...searchStations, stopStation: value.label })
          }
          sx={{ width: 300 }}
          renderInput={(params) => <TextField {...params} label="To" />}
        />
      </Box>
    </Box>
  );
};

export default Bus;

```
- searchStations state တစ်ခု လုပ်လိုက်ပြီး မူလ state တန်ဖိုးကို
` { startStation: "", stopStation: "" }`
အဖြစ် ထားလိုက်ပါတယ်။
- Autocomplete ( from ) မှာ တစ်ခုခု ရွေးလိုက်တဲ့အခါ 
`setSearchStations({ ...searchStations, startStation: value.label }) `
လို့ မူလ တန်ဖိုး ကို အရင် clone လုပ်ပြီး searchStations ထဲက startStation ရဲ့ တန်ဖိုးအဖြစ် ရွေးလိုက်တဲ့ station ကို ပြောင်းထည့်လိုက်တာဖြစ်ပါတယ်။
- အလားတူပဲ Autocomplete ( to) မှာ တစ်ခုခု ရွေးလိုက်တဲ့အခါ 
`setSearchStations({ ...searchStations, stopStation: value.label }) `
လို့ မူလ တန်ဖိုး ကို အရင် clone လုပ်ပြီး searchStations ထဲက stopStation ရဲ့ တန်ဖိုးအဖြစ် ရွေးလိုက်တဲ့ station ကို ပြောင်းထည့်လိုက်တာဖြစ်ပါတယ်။
- useEffect မှာ searchStations state ကို update လုပ်တိုင်း render လုပ်ခိုင်းထားပြီး searchStations ကို log ထုတ်ကြည့်ထားပါတယ်။
- ခု react app ကို start လုပ်ပြီး Bus App ထဲ၀င်ကာ စမ်းသပ်ကြည့်ပါက ရွေးထားတဲ့ station တွေ ပါတဲ့ object တစ်ခုကို log ပြပေးမှာဖြစ်ပါတယ်။

![enter image description here](https://raw.githubusercontent.com/Aungmyanmar32/msquare-m4/main/Screenshot%202023-03-30%20014134.png)
##
- ဆက်ပြီးတော့ bus တွေ အတွက် array တစ်ခု သတ်မှတ်ပါမယ်
```js
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
      { id: 5, label: "tamwe" },
    ],
  },
  {
    id: 2,
    name: " line 40",
    stations: [
      { id: 6, label: "hlaing" },
      { id: 2, label: "myaynigone" },
      { id: 3, label: "mayangone" },
      { id: 4, label: "suelay" },
    ],
  },
];
```
- ပြီးရင် autocomplete တွေ အောက်မှာ button တစ်ခု ထပ်ထည့်ပြီး click လုပ်လိုက်တဲ့ အချိန်မှာ searchBus function ကို ခေါ်ထားလိုက်ပါမယ်
```js
   <Button 
    variant="contained" 
    sx={{ height: "30px", m: "20px" }} 
    onClick ={searchBus}>
        find Bus
   </Button>
```
- searchBus function ကို သတ်မှတ်ပြီး ရွေးလိုက်တဲ့ station တွေ ကို သွားလို့ရမယ့် bus ကို ရှာပါမယ်။
```js

 const searchBus = () => {
    const hasBothStations =
      searchStations.startStation.length > 0 &&
      searchStations.stopStation.length > 0;
    if (!hasBothStations) return;

    const busWithStartStations = busses.filter((bus) =>
      bus.stations.find(
        (station) => station.label === searchStations.startStation
      )
    );

    const busWithEndStations = busses.filter((bus) =>
      bus.stations.find(
        (station) => station.label === searchStations.stopStation
      )
    );
    console.log(busWithStartStations, busWithEndStations);
  };
```
- ပထမဆုံး ရွေးလိုက်တဲ့ station တွေ ရှိမရှိ အရင်စစ်လိုက်ပါတယ်
- station တွေ ရှိခဲ့ရင် startStations နဲ့ stopStation တွေပါတဲ့ bus တွေကို စစ်ထုတ်လိုက်ပြီး log ထုတ်ကြည့်ထားပါတယ်
- အခု app ကို စမ်းသပ်ကြည့်တဲ့အခါ startStations နဲ့ stopStation တွေပါတဲ့ bus တွေကို log ထုတ်ပေးတာ တွေ့ရမှာပါ။

![enter image description here](https://raw.githubusercontent.com/Aungmyanmar32/msquare-m4/main/Screenshot%202023-03-30%20022914.png)

-ဆက်ပြီးတော့ သွားချင်တဲ့ station ကို တစ်ဆင့်ထဲနဲ့  မရရင်  နှစ်ဆင့် စီးရမယ့် Bus တွေ ရှိမရှိကို ရှာကြည့်ပါမယ်
```js
const searchBus = () => {
    const hasBothStations =
      searchStations.startStation.length > 0 &&
      searchStations.stopStation.length > 0;
    if (!hasBothStations) return;

    const busWithStartStations = busses.filter((bus) =>
      bus.stations.find(
        (station) => station.label === searchStations.startStation
      )
    );

    const busWithEndStations = busses.filter((bus) =>
      bus.stations.find(
        (station) => station.label === searchStations.stopStation
      )
    );
    console.log(busWithStartStations, busWithEndStations);

//New code under
    //find indrect bus and common station
    const firstBus = busWithStartStations.length > 0 && busWithStartStations[0];
    const secondBus = busWithEndStations.length > 0 && busWithEndStations[0];
    const hasFoundIndirectBus = firstBus && secondBus;

    if (!hasFoundIndirectBus) return [];

    const firstBusStation = firstBus.stations;
    const secondBusStation = secondBus.stations;

    const indirectBusses: Busses[] = [];

    firstBusStation.find((station) => {
      const hasFound = secondBusStation.find(
        (innerStaton) => innerStaton.label === station.label
      );
      if (hasFound) {
        indirectBusses.push(firstBus, secondBus);
      }
    });

    console.log(indirectBusses);
    return indirectBusses;
  };
```


     const firstBus = busWithStartStations.length > 0 && busWithStartStations[0];
     const secondBus = busWithEndStations.length > 0 && busWithEndStations[0];
     const hasFoundIndirectBus = firstBus && secondBus

- directBus ရှိမရှိ အရင်စစ်ပါတယ်
```
 const firstBusStation = firstBus.stations;
 const secondBusStation = secondBus.stations;
 ```
- directBus ရှိခဲ့ရင်  ပထမ နဲ့ ဒုတိယ bus တွေက station တွေကို လှမ်းယူလိုက်ပါတယ်

 `const indirectBusses: Busses[] = [];`
 - indirectBusses array တစ်ခု လုပ်ပါတယ်
 
 ```js
 firstBusStation.find((station) => {
      const hasFound = secondBusStation.find(
        (innerStaton) => innerStaton.label === station.label
      );
      if (hasFound) {
        indirectBusses.push(firstBus, secondBus);
      }
    });

    console.log("indirectBusses",indirectBusses);
    return indirectBusses;
```
- 
-  ဆက်ပြီး second station ထဲမှာ first station ထဲက station တစ်ချို့ ပါမပါ ရှာလိုက်ပြီး ပါခဲ့လို့ရှိရင် အဲ့ဒီ station ကို ရောက်တဲ့ bus တွေကို indirectBusses array ထဲ push လုပ်လိုက်ပြီး 
log ထုတ်ကြည့်ထားပါတယ်

- ခု bus app မှာ bus တစ်စီးထဲနဲ့ မရနိုင်တဲ့ station နှစ်ခု ကို ရွေးကြည့်လိုက်ပါက Bus နှစ်စီး ကို ပြပေးမှာဖြစ်ပါတယ်။

![enter image description here](https://raw.githubusercontent.com/Aungmyanmar32/msquare-m4/main/Screenshot%202023-03-30%20105304.png)

