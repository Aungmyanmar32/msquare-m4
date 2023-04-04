## MSquare Programing Fullstack Course
### Episode-*52* 
### Summary For `Room(2)`
##
### ပြီးခဲ့တဲ့ သင်ခန်းစာမှာ autocomplete ကနေ ရွေးလိုက်တဲ့ station တွေကို state တစ်ခုထဲသိမ်းပြီး UI မှာ ပြခဲ့ကြပါတယ်
### ဒီနေ့သင်ခန်းစာမှာတော့ ရွေးလိုက်တဲ့ station ဆီ သွားလို့ရမယ့် Bus ကားတွေ ပြပေးနိုင်အောင် လေ့လာကြပါမယ်
- အရင်ဆုံး busses array တစ်ခုလုပ်ပါမယ်
```js
// data.ts


export const movies: Movie[] = [
 .....
];

export const stations: Station[] = [
  { id: 1, label: "Hledan" },
  { id: 2, label: "Myaynigone" },
  { id: 3, label: "Yankin" },
  { id: 4, label: "Tamwe" },
  { id: 5, label: "Yuzana Plaza" },
  { id: 6, label: "Saint Paul" },
  { id: 7, label: "Suele" },
  { id: 8, label: "Thingangyun" },
  { id: 9, label: "South okkala" },
  { id: 10, label: "North okkala" },
  { id: 11, label: "Kabar Aye" },
  { id: 12, label: "Mm Plaza" },
  { id: 13, label: "Insein" },
  { id: 14, label: "South Dagon" },
  { id: 15, label: "North Dagon" },
  { id: 16, label: "Bayli" },
  { id: 17, label: "Sinmalike" },
  { id: 18, label: "Kyimyindaing" },
];

// ADD New array
export const buses = [
  {
    id: 1,
    name: "YBS40",
    stations: [
      { id: 1, label: "Hledan" },
      { id: 2, label: "Myaynigone" },
      { id: 3, label: "Yankin" },
      { id: 4, label: "Tamwe" },
      { id: 5, label: "Yuzana Plaza" },
    ],
  },
  {
    id: 2,
    name: "YBS45",
    stations: [
      { id: 3, label: "Yankin" },
      { id: 4, label: "Tamwe" },
      { id: 5, label: "Yuzana Plaza" },
      { id: 6, label: "Saint Paul" },
      { id: 7, label: "Suele" },
      { id: 8, label: "Thingangyun" },
      { id: 9, label: "South okkala" },
      { id: 10, label: "North okkala" },
    ],
  },
  {
    id: 2,
    name: "YBS50",
    stations: [
      { id: 8, label: "Thingangyun" },
      { id: 9, label: "South okkala" },
      { id: 10, label: "North okkala" },
      { id: 11, label: "Kabar Aye" },
      { id: 12, label: "Mm Plaza" },
      { id: 13, label: "Insein" },
      { id: 14, label: "South Dagon" },
      { id: 15, label: "North Dagon" },
      { id: 16, label: "Bayli" },
      { id: 17, label: "Sinmalike" },
      { id: 18, label: "Kyimyindaing" },
    ],
  },
];

```
- id ရယ် name ရယ် stations ရယ် ပါတဲ့ bus object တွေကို busses array ထဲ ထည့်ထားပါတယ်
- တစ်ခုသတိထားရမှာပါ အခု အသစ်လုပ်တဲ့ array ထဲမှာ ပါတဲ့ stations id တွေဟာ အပေါ်က stations array ထဲက id တွေနဲ့ တူအောင် ရေးပေးရပါမယ်။
- အပေါ်မှာ  Hledan အတွက် id က 1 ဆိုရင် busses array ထဲက stations မှာလဲ id 1 ပဲ ဖြစ်နေရမယ်လို့ 	ဆိုလိုတာပါ။
- ဆက်ပြီး busses array အတွက် type သတ်မှတ်ပါမယ်
```js
//types.ts
export interface Movie {
  label: string;
  year: number;
}

export interface SearchStaitons {
  startStation: Station | null;
  endStation: Station | null;
}

export interface Station {
  id: number;
  label: string;
}
//   {
//     id: 1,
//     name: "YBS40",
//     stations: [
//       { id: 1, label: "Hledan" },
//       { id: 2, label: "Myaynigone" },
//       { id: 3, label: "Yankin" },
//       { id: 4, label: "Tamwe" },
//       { id: 5, label: "Yuzana Plaza" },
//     ],
//   },

export interface Bus {
  id: number;
  name: string;
  stations: Station[];
}

```
- Bus interface တစ်ခုလုပ်လိုက်ပြီး  အပေါ်က နမူနာပုံစံ မှာ ရှိတဲ့ အတိုင်း  id က number ,name က string,  stations က  interface Station ကို ပြန်ခေါ်သုံးလိုက်ပြီး stations object တွေပါတဲ့ array တစ်ခု ဖြစ်ကြောင်း type လုပ်ပေးထားတာဖြစ်ပါတယ်
- data.ts ထဲက busses array ကို ခုသတ်မှတ်ထားတဲ့ Bus interface( object) တွေပါတဲ့array လို့  type ပေးလိုက်ပါမယ်
```js
// data.ts
import { Bus, Movie, Station } from  "../typings/types";

export const movies: Movie[] = [
 .....
];

export const stations: Station[] = [
  { id: 1, label: "Hledan" },
  { id: 2, label: "Myaynigone" },
  { id: 3, label: "Yankin" },
  { id: 4, label: "Tamwe" },
  { id: 5, label: "Yuzana Plaza" },
  { id: 6, label: "Saint Paul" },
  { id: 7, label: "Suele" },
  { id: 8, label: "Thingangyun" },
  { id: 9, label: "South okkala" },
  { id: 10, label: "North okkala" },
  { id: 11, label: "Kabar Aye" },
  { id: 12, label: "Mm Plaza" },
  { id: 13, label: "Insein" },
  { id: 14, label: "South Dagon" },
  { id: 15, label: "North Dagon" },
  { id: 16, label: "Bayli" },
  { id: 17, label: "Sinmalike" },
  { id: 18, label: "Kyimyindaing" },
];

// ADD New array
export const buses: Bus[] = [
  {
    id: 1,
    name: "YBS40",
    stations: [
      { id: 1, label: "Hledan" },
      { id: 2, label: "Myaynigone" },
      { id: 3, label: "Yankin" },
      { id: 4, label: "Tamwe" },
      { id: 5, label: "Yuzana Plaza" },
    ],
  },
  {
    id: 2,
    name: "YBS45",
    stations: [
      { id: 3, label: "Yankin" },
      { id: 4, label: "Tamwe" },
      { id: 5, label: "Yuzana Plaza" },
      { id: 6, label: "Saint Paul" },
      { id: 7, label: "Suele" },
      { id: 8, label: "Thingangyun" },
      { id: 9, label: "South okkala" },
      { id: 10, label: "North okkala" },
    ],
  },
  {
    id: 2,
    name: "YBS50",
    stations: [
      { id: 8, label: "Thingangyun" },
      { id: 9, label: "South okkala" },
      { id: 10, label: "North okkala" },
      { id: 11, label: "Kabar Aye" },
      { id: 12, label: "Mm Plaza" },
      { id: 13, label: "Insein" },
      { id: 14, label: "South Dagon" },
      { id: 15, label: "North Dagon" },
      { id: 16, label: "Bayli" },
      { id: 17, label: "Sinmalike" },
      { id: 18, label: "Kyimyindaing" },
    ],
  },
];

```
##
### ဆက်ပြီးတော့  autocomplete ကနေ ရွေးလိုက်တဲ့ station တွေကို တိုက်ရိုက်သွားလို့ရမယ့် Bus ကို ရှာပါမယ်

- အရင်သင်ခန်းစာတုန်းက mui button တစ်ခုကို စမ်းထည့်ခဲ့ကြပါတယ်
- အဲ့ဒီ button ကို click လုပ်လိုက်တဲ့အခါ helloဆိုပြီး log တစ်ခုထုတ်ခဲ့ကြပါတယ်
- ခု log မထုတ်တော့ပဲ handleClick ဆိုတဲ့ function တစ်ခုကို clickလုပ်လိုက်တဲ့အခါ run ခိုင်းဖို့ ပြင်ဆင်ပါမယ်
```js
//App.tsx
.........
 <Autocomplete
          disablePortal
          id="movies"
          options={stations}
          onChange={(event, value) =>
            value && setSearchStations({ ...searchStations, endStation: value })
          }
          sx={{ width: 300 }}
          renderInput={(params) => (
            <TextField {...params} label="End Station" />
          )}
        />
      </Box>

      {/* // find bus on click */}
      <Button
        variant="contained"
        sx={{ margin: "0 auto", mt: 2 }}
        onClick={handleClick}
      >
        Find Bus
      </Button>

      <Box sx={{ margin: "0 auto", mt: 2, textAlign: "center" }}>
        {searchStations.startStation && (
          <h1>{searchStations.startStation.label}</h1>
        )}
        {searchStations.endStation && (
          <h1>{searchStations.endStation.label}</h1>
        )}
      </Box>
      ............................
```
- hadleClick function ကို return မလုပ်ခင်လေးမှာ define လုပ်ပါမယ်
- အဲ့ဒီ function ထဲမှာ ရွေးလိုက်တဲ့ station နဲ့ busses array ထဲက station တွေ တူမတူ တိုက်စစ်ပြီး ရွေးလိုက်တဲ့ station နှစ်ခုလုံး ပါတဲ့ bus ရှိခဲ့ရင် array အသစ်ထဲ သိမ်းလိုက်မှာဖြစ်ပါတယ်။
```js
//App.tsx
import...........
import { Bus, SearchStaitons } from  "../typings/types";
import { buses, movies, stations } from  "../utils/data";

const App =()=>{.................
.............................
//set new direct bus state
  const [directBus, setDirectBus] = useState<Bus[] | null>(null);
  

  const handleClick = () => {

    //find bus with station A
    const busWithStartStation = buses.filter((bus) =>
      bus.stations.find(
        (station) => station.id === searchStations.startStation?.id
      )
    );

    // check direct bus 
    const directBus = busWithStartStation.filter((bus) =>
      bus.stations.find((staion) => staion.id === searchStations.endStation?.id)
    );

    console.log("direct-Bus", directBus);

// update state with direct bus array
    setDirectBus(directBus);
  };

return(........
...........
```
> ရှင်းလင်းချက်

` const [directBus, setDirectBus] = useState<Bus[] | null>(null);`
- directBus ဆိုတဲ့ state တစ်ခုသတ်မှတ်လိုက်ပြီး type ကို Bus object တွေပါတဲ့ array (သို့မဟုတ်) null ဖြစ်ပါတယ်လို့ ပေးလိုက်ပါတယ်။ လောလောဆယ်တော့ သူ့ရဲ့ မူလတန်ဖိုးကို null အဖြစ်ပဲ ပေးထားလိုက်ပါမယ်
```
 const busWithStartStation = buses.filter((bus) =>
      bus.stations.find(
        (station) => station.id === searchStations.startStation?.id
      )
    );
```
- busses array ကို filter နဲ့  loop လုပ်ပြီး bus object တစ်ခုချင်းမှာရှိတဲ့ station array တွေမှာ searchStations ထဲက startStation ရဲ့ id နဲ့ တူတဲ့ station  တွေ ပါမပါ ရှာလိုက်ပြီး ရှာတွေ့တဲ့အခါ အဲဒီ station ပါတဲ့ bus object တွေကို busWithStartStation ဆိုတဲ့ array အသစ်မှာ သိမ်းထားလိုက်တာဖြစ်ပါတယ်
- ဥပမာ ။   ။ Station A input ( autocomplete ) မှာ Hledan ကို ရွေးလိုက်တယ်ဆိုပါစို့။
   - Hledan ရဲ့ id က 1 ဖြစ်ပါမယ်
   - အဲ့ဒီ station id 1 ဟာ busses array ထဲက bus တွေထဲမှာ ရှိနေတဲ့ stations id တွေနဲ့ တူမတူ ရှာကြည့်လိုက်တဲ့ အခါ YBS40 bus name ဖြစ်တဲ့ bus object တစ်ခု ရလာမှာဖြစ်ပါတယ်
   - အကယ်လို့  Station A input ( autocomplete ) မှာ Tamwe ကို ရွေးလိုက်တယ်ဆိုရင်
   - YBS40 ရော YBS45ပါ ရှာတွေ့မှာ မို့လို့ busWithStartStation ဆိုတဲ့ array အသစ်မှာ items နှစ်ခု ရှိလာမှာ ဖြစ်ပါတယ်။
   
```
 const directBus = busWithStartStation.filter((bus) =>
      bus.stations.find((staion) => staion.id === searchStations.endStation?.id)
    );
```
- ဆက်ပြီးတော့ ခုနကရှာတွေ့တဲ့ bus တွေထဲမှာ station B autocomplete မှာ ရွေးလိုက်တဲ့ station ပါမပါ ထပ်ရှာလိုက်တာပါ။
- station A မှာ Hledan , station B  မှာ Tamwe လို့ ရှာလိုက်တယ်ဆိုရင် YBS 40 ထဲမှာ အဲ့ဒီ station နှစ်ခုလုံးပါတာမလို့ YBS40 ပါတဲ့ bus object တစ်ခု ကို directBus ဆိုတဲ့ array အသစ်ထဲ သိမ်းပေးလိုက်မှာဖြစ်ပါတယ်
```
  console.log("direct-Bus", directBus);


    setDirectBus(directBus);
```
- ဒါကတော့ နောက်ဆုံး ရလဒ်ဖြစ်တဲ့ directBus array ကို log ထုတ်ကြည့်ထားပြီး directBus(state) ရဲ့ တန်ဖိုးအဖြစ် update လုပ်လိုက်တာဖြစ်ပါတယ်
##
### ဆက်ပြီးတော့ direct bus ကို တွေ့ခဲ့လို့ရှိရင် UI မှာ bus နာမည်ကို ပြပေးပါမယ်
```js
//App.tsx
...........
............
..........
<Box sx={{ margin: "0 auto", mt: 2, textAlign: "center" }}>
        {searchStations.startStation && (
          <h1>{searchStations.startStation.label}</h1>
        )}
        {searchStations.endStation && (
          <h1>{searchStations.endStation.label}</h1>
        )}
      </Box>
      
{/* Show direct Bus Name */}
      <Box sx={{ margin: "0 auto", mt: 2, textAlign: "center" }}>
        {directBus &&
          directBus?.map((bus) => {
            return <h1>{bus.name}</h1>;
          })}
      </Box>
{/* end of Show direct Bus Name */}

      <Box sx={{ margin: "0 auto", mt: 2, textAlign: "center" }}>
        <LocalizationProvider dateAdapter={AdapterDayjs}>
          <DatePicker />
        </LocalizationProvider>
      </Box>
    </Box>
............
...........
...........
```
>ရှင်းလင်းချက်
```js
<Box sx={{ margin: "0 auto", mt: 2, textAlign: "center" }}>
        {directBus &&
          directBus?.map((bus) => {
            return <h1>{bus.name}</h1>;
          })}
      </Box>
```
- direct bus state ရဲ့ တန်ဖိုးဟာ တစ်ခုခုရှိခဲ့ရင် (null မဟုတ်ခဲ့ရင်) ရှာတွေ့ထားတဲ့ bus object ထဲက name ကို ပြခိုင်းလိုက်တာဖြစ်ပါတယ်
- ခု   react app ကို start လုပ်ပြီး စမ်းကြည့်ပါမယ်
- ပုံပါအတိုင်း station နှစ်ခုကို ရွေးကြည့်လိုက်ပြီး Find Bus ကို နှိပ်ကြည့်လိုက်ပါက station နှစ်ခုလုံး ရောက်တဲ့ YBS40 ကို ပြပေးမှာဖြစ်ပါတယ်

![enter image description here](https://raw.githubusercontent.com/Aungmyanmar32/msquare-m4/main/ep52r2%20%281%29.png)
- အောက်ကပုံလို ရွေးကြည့်လိုက်ပါက Bus နာမည် မပေါ်လာတာ ကြုံရမှာပါ

![enter image description here](https://raw.githubusercontent.com/Aungmyanmar32/msquare-m4/main/ep52r2%20%282%29.png)
   - ဘာလို့လဲ	ဆိုတော့ Hledan ကနေ  North okkala ကို တိုက်ရိုက်ရောက်တဲ့ Bus မရှိလို့ဖြစ်ပါတယ်။
   - အဲ့ဒါဆိုရင် Bus နှစ်ဆင့် စီးရပါတော့မယ် ( in-direct bus )
   -  in-direct bus ကို ဘယ်လို ရှာရမလဲ ဆိုတာတော့   နောက် သင်ခန်းစာတွေမှ ဆက်လေ့လာကြပါမယ်။
   ##
   ## React Router Dom
   ### react မှာ route တွေ ခွဲပြီး သက်ဆိုင်ရာ routeတွေမှာrender လုပ်ချင်တဲ့ component ကိုပဲ ပြစေလိုတဲ့အခါ  ***`React Router Dom`*** ကို အသုံးပြုရပါမယ်

- react router dom ကို အသုံးပြုနိုင်ရန် project ထဲကို install လုပ်ပေးရပါမယ်
`npm i react-router-dom`

- နောက်တစ်ဆင့်အနေနဲ့ ကျနော်ဆိုရဲ့ project folder ထဲမှာ apps  ဆိုတဲ့ folder တစ်ခုလုပ်ပါမယ် ( src/apps )
- အဲ့ဒီ apps folder ထဲမှာ BussApp.tsx နဲ့ PassportApp.tsx ဆိုတဲ့ ဖိုင်နှစ်ခုလုပ်ပါမယ်။
   - src/apps/BussApp.tsx
   - src/apps/PassportApp.tsx
- BussApp.tsx ထဲကို လက်ရှိ project ထဲက App.tsx ထဲရှိ code တွေအကုန် ကူးထည့်ပေးလိုက်ပါ။
- App.tsx ထဲမှာတော့code တွေ အကုန်ဖျက်ပြီး mui button နှစ်ခုပဲ render လုပ်ပေးပါမယ်

```js
// BusApp.tsx

import "../App.css";
import TextField from "@mui/material/TextField";
import { Box, Autocomplete, Button } from "@mui/material";

import { LocalizationProvider, DatePicker } from "@mui/x-date-pickers";
import { AdapterDayjs } from "@mui/x-date-pickers/AdapterDayjs";
import { useState } from "react";
import { Bus, SearchStaitons } from "../typings/types";
import { buses, movies, stations } from "../utils/data";

function BusApp() {
  const [searchStations, setSearchStations] = useState<SearchStaitons>({
    startStation: null,
    endStation: null,
  });
//set new direct bus state
  const [directBus, setDirectBus] = useState<Bus[] | null>(null);
  

  const handleClick = () => {

    //find bus with station A
    const busWithStartStation = buses.filter((bus) =>
      bus.stations.find(
        (station) => station.id === searchStations.startStation?.id
      )
    );

    // check direct bus or not
    const directBus = busWithStartStation.filter((bus) =>
      bus.stations.find((staion) => staion.id === searchStations.endStation?.id)
    );

    console.log("direct-Bus", directBus);

// update state with direct bus array
    setDirectBus(directBus);
  };

  return (
    <Box
      sx={{
        display: "flex",
        flexDirection: "column",
        justifyContent: "center",
        mt: 5,
      }}
    >
      <Box sx={{ margin: "0 auto", textAlign: "center" }}>
        <Autocomplete
          disablePortal
          id="movies"
          options={stations}
          onChange={(event, value) =>
            value &&
            setSearchStations({ ...searchStations, startStation: value })
          }
          sx={{ width: 300 }}
          renderInput={(params) => (
            <TextField {...params} label="Start Station" />
          )}
        />
      </Box>
      <Box sx={{ margin: "0 auto", textAlign: "center", mt: 2 }}>
        <Autocomplete
          disablePortal
          id="movies"
          options={stations}
          onChange={(event, value) =>
            value && setSearchStations({ ...searchStations, endStation: value })
          }
          sx={{ width: 300 }}
          renderInput={(params) => (
            <TextField {...params} label="End Station" />
          )}
        />
      </Box>

      {/* // find bus on click */}
      <Button
        variant="contained"
        sx={{ margin: "0 auto", mt: 2 }}
        onClick={handleClick}
      >
        Find Bus
      </Button>

      <Box sx={{ margin: "0 auto", mt: 2, textAlign: "center" }}>
        {searchStations.startStation && (
          <h1>{searchStations.startStation.label}</h1>
        )}
        {searchStations.endStation && (
          <h1>{searchStations.endStation.label}</h1>
        )}
      </Box>

{/* Show direct Bus Name */}
      <Box sx={{ margin: "0 auto", mt: 2, textAlign: "center" }}>
        {directBus &&
          directBus?.map((bus) => {
            return <h1>{bus.name}</h1>;
          })}
      </Box>

      <Box sx={{ margin: "0 auto", mt: 2, textAlign: "center" }}>
        <LocalizationProvider dateAdapter={AdapterDayjs}>
          <DatePicker />
        </LocalizationProvider>
      </Box>
    </Box>
  );
}

export default BusApp;

```

```js
//App.tsx

import { Box, Button } from "@mui/material";
import React from "react";

const App = () => {
  return (
    <Box
      sx={{
        display: "flex",
        flexDirection: "column",
        justifyContent: "center",
        mt: 5,
      }}
    >
      <Button variant="contained" sx={{ margin: "0 auto", mt: 2 }}>
        Bus App
      </Button>
      <Button variant="contained" sx={{ margin: "0 auto", mt: 2 }}>
        Passport App
      </Button>
    </Box>
  );
};

export default App;

```
- PassportApp.tsx မှာတော့ အောက်ကအတိုင်း ပဲ ရေးထားလိုက်ပါမယ်

![enter image description here](https://raw.githubusercontent.com/Aungmyanmar32/msquare-m4/main/ep52r2%20%283%29.png)
##
- ဆက်ပြီး route တွေသတ်မှတ်ပါမယ်။
- route တွေ သတ်မှတ်ဖို့ html မှာ render လုပ်ပေးတဲ့ index.ts မှာ သတ်မှတ်ပါမယ်
- react မှာ route တွေ လုပ်နိုင်ဖို့ react router dom ထဲ က createBrowserRouter နဲ့ RouterProvider နှစ်ခုကို import လုပ်ပေးရပါမယ်
```js
// index.tsx
.....
....
import { createBrowserRouter, RouterProvider } from  "react-router-dom";
....
....

```
- import လုပ်ထားတဲ့ createBrowserRouter ကို သုံးပြီး router တွေသတ်မှတ်ပါမယ်
```js
// index.tsx
import { createBrowserRouter, RouterProvider } from "react-router-dom";
import BusApp from "./apps/BusApp";
import PassportApp from "./apps/PassportApp";

const router = createBrowserRouter([
  {
    path: "/",
    element: <App />,
  },
  {
    path: "/bus",
    element: <BusApp />,
  },
  {
    path: "/passport",
    element: <PassportApp />,
  },
]);
```
- path ဆိုတာက route တစ်ခုဖြစ်ပြီး element ဆိုတာက path ထဲ route ကို ရောက်တဲ့အခါ ပြပေးရမယ့် ( render လုပ်ပေးရမယ့် ) component ဖြစ်ပါတယ်
- ဥပမာ ။  ။
```
{
    path: "/bus",
    element: <BusApp />,
  },
```
-  http://localhost:3000/bus ကို ရောက်လာရင် BusApp component ကို render လုပ်ပေးလိုက်ပါလို့ ဆိုလိုတာပါ
- ဆက်ပြီးတော့ အသစ်သတ်မှတ်ထားတဲ့ router array ကို  import လုပ်ထားတဲ့ RouterProvider မှာ props အဖြစ် သုံးပြီး render လုပ်ပေးရပါမယ်
```js
//index.tsx

import React from "react";
import "./index.css";
import App from "./App";
import reportWebVitals from "./reportWebVitals";
import ReactDOM from "react-dom/client";
import { createBrowserRouter, RouterProvider } from "react-router-dom";
import BusApp from "./apps/BusApp";
import PassportApp from "./apps/PassportApp";

const router = createBrowserRouter([
  {
    path: "/",
    element: <App />,
  },
  {
    path: "/bus",
    element: <BusApp />,
  },
  {
    path: "/passport",
    element: <PassportApp />,
  },
]);

const root = ReactDOM.createRoot(
  document.getElementById("root") as HTMLElement
);
root.render(<RouterProvider router={router} />);
```
- ခု react app ကို start ထားပြီး  http://localhost:3000/bus  ကို browser မှာ ၀င်ကြည့်ပါက သင်ခန်းစာအစောပိုင်းမှာ လုပ်တဲ့တဲ့ bus ရှာတဲ့ page ကို မြင်ရမှာဖြစ်ပြီး 

![enter image description here](https://raw.githubusercontent.com/Aungmyanmar32/msquare-m4/main/ep52r2%20%284%29.png)
- http://localhost:3000/passport ကို ၀င်ကြည့်ပါက PassportApp လို့ ပြပေးတာကို မြင်ရမှာဖြစ်ပါတယ်

![enter image description here](https://raw.githubusercontent.com/Aungmyanmar32/msquare-m4/main/ep52r2%20%285%29.png)
- http://localhost:3000 ကိုပဲ ပြန်၀င်ကြည့်ပါက root route မှာ render လုပ်ထားတဲ့ App component ကို မြင်ရမှာဖြစ်ပါတယ်

![enter image description here](https://raw.githubusercontent.com/Aungmyanmar32/msquare-m4/main/ep52r2%20%286%29.png)
##
### ဆက်ပြီးတော့ route တွေကို ကိုယ်တိုင်ရိုက်ထည့်စရာမလိုပဲ App.tsx ထဲက ခလုတ်တွေ နှိပ်ပေးလိုက်တာနဲ့  သွားနိုင်အောင် လုပ်ပါမယ်
```js
//App.tsx

import { Box, Button } from "@mui/material";
import React from "react";

const App = () => {
  return (
    <Box
      sx={{
        display: "flex",
        flexDirection: "column",
        justifyContent: "center",
        mt: 5,
      }}
    >
      <Button variant="contained" sx={{ margin: "0 auto", mt: 2 }}>
        <a href="/bus">Bus App</a>
      </Button>
      <Button variant="contained" sx={{ margin: "0 auto", mt: 2 }}>
        <a href="/passport">Passport App</a>
      </Button>
    </Box>
  );
};

export default App;

```
- a tag ကို အသုံးပြုပြီး Bus App ခလုတ်ကို click လိုက်ရင် /bus ဆိုတဲ့ route  ဆီ redirect လုပ်ပေးလိုက်တာဖြစ်ပါတယ်
- အလားတူပဲ  Passport App ခလုတ်ကို click လိုက်ရင် /passport ဆိုတဲ့ route  ဆီ redirect လုပ်ပေးလိုက်တာဖြစ်ပါတယ်
- ခု react app ကို စမ်းသပ်ကြည့်ပါက သက်ဆိုင်ရာ route တွေဆီ ရောက်သွားပြီး အဲဒီ route တွေထဲ render လုပ်ထားတဲ့ component တွေကို မြင်ရမှာဖြစ်ပါတယ်
