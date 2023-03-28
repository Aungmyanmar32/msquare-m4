## MSquare Programing Fullstack Course

### Episode-_46_

### Summary For  `Room(1)`  intermediate Class
##
### ပြီခဲ့တဲ့ သင်ခန်းစာမှာ အစပျိုးခဲ့တဲ့ Bus tracking App ကို  ဆက်လုပ်ကြပါမယ်။
- Apps folder ထဲ က Bus component မှာ input tag တစ်ခု လုပ်ပါမယ်။
```js
//Bus.tsx

import { Box, Input } from "@mui/material";
import React from "react";

const Bus = () => {
  return (
    <Box
      sx={{
        display: "flex",
        justifyContent: "center",
        alignItems: "center",
        width: "100%",
      }}
    >
      <Box sx={{ mt: "10px" }}>
        <input
          type="text"
          style={{
            width: "200px",
            height: "30px",
            marginBottom: "5px",
            padding: "5px",
          }}
        />
        <Box
          sx={{
            height: "200px",
            border: "2px solid balck",
            backgroundColor: "grey",
          }}
        >
          station
        </Box>
      </Box>
      {/* <Box sx={{ mt: "10px" }}>
        <input type="text" />
        <div>station2</div>
      </Box> */}
    </Box>
  );
};

export default Bus;


```
![enter image description here](https://raw.githubusercontent.com/Aungmyanmar32/msquare-m4/main/Screenshot%202023-03-27%20150818.png)

- ဆက်ပြီးတော့ input ထဲမှာ တစ်ခုခု မရှိရင်  အောက်က staion box ကို ဖျောက်ထားပြီး input တစ်ခုခုထည့်ပေးမှ ပြန်ပေါ်လာအောင်လုပ်ပါမယ်။
- အရင်ဆုံး  inputထဲမှာ ရိုက်ထည့်လိုက်တဲ့ စာတွေကို state တစ်ခုထဲသိမ်းပါမယ်။
- ပြီးတော့ input ရဲ့  onChange eventကို သုံးပြီး state ကို update လုပ်ပါမယ်။
- update လုပ်လိုက်တဲ့ state ပေါ်မူတည်ပြီး input အောက်က station box ကို display လုပ်မှာဖြစ်ပါတယ်
```js
// Bus.tsx --> input tag

 <Box sx={{ mt: "10px" }}>
        <input
          type="text"
          style={{
            width: "200px",
            height: "30px",
            marginBottom: "5px",
            padding: "5px",
          }}
          onChange={(e) => setOrgStation(e.target.value)}
        />
        <Box
          sx={{
            height: "200px",
            border: "2px solid black",
            backgroundColor: "grey",
            display: orgStation ? "block" : "none",
          }}
        >
          <h2>station</h2>
        </Box>
      </Box>
```
- အခု react app မှာ bus tracking app ထဲ၀င်ပြီး စမ်းကြည့်ပါက text input တစ်ခု ပြနေမှာဖြစ်ပြီး text တစ်ခုခုရိုက်ထည့်ကြည့်ပါက အောက်မှာ station ဆိုတဲ့ box လေး ပေါ်လာမှာဖြစ်ပါတယ်။

![enter image description here](https://raw.githubusercontent.com/Aungmyanmar32/msquare-m4/main/Screenshot%202023-03-27%20152719.png)

![enter image description here](https://raw.githubusercontent.com/Aungmyanmar32/msquare-m4/main/Screenshot%202023-03-27%20152731.png)
- ပေါ်လာတဲ့ box မှာ station ဆိုတာက ပြချင်တာမဟုတ်ပဲ input ထည့်လိုက်တဲ့ text နဲ့ နမူနာ သတ်မှတ်ထားတဲ့ station နာမည် တူမတူ တိုက်စစ်ပြီး autocomplete လုပ်မှာမလို့ နမူနာ data တစ်ခုကို သတ်မှတ်ပါမယ်။
```js
//Bus.tsx (add new data)

const stations =[
  {
    id: 1,
    station: "Hledan"
  },
  {
    id: 2,
    station: "Tarmwe"
  },
  {
    id: 3,
    station: "Alone"
  },
  {
    id: 4,
    station: "Suelay"
  },
]
```
- နမူနာ station တွေနဲ့ input text ကို တိုက်စစ်ပြီး ရလာတဲ့ data ကို station box မှာ ပြပေးပါမယ်။
```js
// Bus.tsx

import { Block } from "@mui/icons-material";
import { Box, Input } from "@mui/material";
import React, { useEffect, useState } from "react";
const stations = [
  {
    id: 1,
    station: "Hledan",
  },
  {
    id: 2,
    station: "Tarmwe",
  },
  {
    id: 3,
    station: "Alone",
  },
  {
    id: 4,
    station: "Suelay",
  },
];

interface Station {
  id: number;
  station: string;
}
const Bus = () => {
  const [orgStation, setOrgStation] = useState<string>();
  const [searchResult, setSearchResult] = useState<Station[]>([]);

  useEffect(() => {
    if (orgStation) {
      const filteredStation = stations.filter((item) =>
        item.station.toLocaleLowerCase().includes(orgStation.toLowerCase())
      );
      if (filteredStation.length > 0) {
        setSearchResult(filteredStation);
      } else {
        setSearchResult([{ id: 0, station: "No station found!" }]);
      }
    }
  }, [orgStation]);

  return (
    <Box
      sx={{
        display: "flex",
        justifyContent: "center",
        alignItems: "center",
        width: "100%",
      }}
    >
      <Box sx={{ mt: "10px" }}>
        <input
          type="text"
          style={{
            width: "200px",
            height: "30px",
            marginBottom: "5px",
            padding: "5px",
          }}
          onChange={(e) => setOrgStation(e.target.value)}
        />
        <Box
          sx={{
            height: "200px",
            border: "2px solid black",
            backgroundColor: "grey",
            display: orgStation ? "block" : "none",
            textAlign:  "center"
          }}
        >
          {searchResult.map((item) => {
            return  <h3>{item.station}</h3>;
          })}
        </Box>
      </Box>
      {/* <Box sx={{ mt: "10px" }}>
        <input type="text" />
        <div>station2</div>
      </Box> */}
    </Box>
  );
};

export default Bus;


```
- အခု Bus app မှာ text inputလုပ်ပြီး စမ်းကြည့်ပါက နမူနာ data ထဲမှာ ရှိတဲ့ station နဲ့ ကိုက်ညီရင် station box မှာ ပြပေးမှာ ဖြစ်ပြီး မရှိတဲ့station ဖြစ်ရင်တော့ NO station found ပြပေးမှာဖြစ်ပါတယ်။

![enter image description here](https://github.com/Aungmyanmar32/msquare-m4/blob/main/Screenshot%202023-03-27%20155857.png?raw=true)

![enter image description here](https://raw.githubusercontent.com/Aungmyanmar32/msquare-m4/main/Screenshot%202023-03-27%20155908.png)
##
- အခု autocomplete input ကို MUI autocomplete အသုံးပြုပြီး ပြင်ရေးပါမယ်
- stations array ကို data ပုံစံ အနည်းငယ်ပြောင်းရေးပါမယ်။
```js
//Update stations array in Bus.tsx
const stations = [
  {
    id: 1,
    label: "Hledan",
    destination: [
      {
        id: 2,
        label: "Tarmwe",
      },
      {
        id: 3,
        label: "Alone",
      },
    ],
  },
  {
    id: 2,
    label: "Tarmwe",
    destination: [
      {
        id: 1,
        label: "Hledan",
      },
      {
        id: 3,
        label: "Alone",
      },
    ],
  },
  {
    id: 3,
    label: "Alone",
    destination: [
      {
        id: 4,
        label: "Suelay",
      },
    ],
  },
  {
    id: 4,
    label: "Suelay",
    destination: [],
  },
];
```
- station နာမည်တွေကို label အနေနဲ့ ပြောင်းရေးလိုက်ပြီး destination array item  တစ်ခုထပ်ဖြည့်လိုက်ပါတယ်။
- ဆက်ပြီး mui autocomplete ကို အသုံးပြုပါမယ်
```js
//  Bus.tsx


import { Autocomplete, Box, Input, TextField } from "@mui/material";
import React, { useEffect, useState } from "react";
const stations = [
  {
    id: 1,
    label: "Hledan",
    destination: [
      {
        id: 2,
        label: "Tarmwe",
      },
      {
        id: 3,
        label: "Alone",
      },
    ],
  },
  {
    id: 2,
    label: "Tarmwe",
    destination: [
      {
        id: 1,
        label: "Hledan",
      },
      {
        id: 3,
        label: "Alone",
      },
    ],
  },
  {
    id: 3,
    label: "Alone",
    destination: [
      {
        id: 4,
        label: "Suelay",
      },
    ],
  },
  {
    id: 4,
    label: "Suelay",
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
  const [orgStation, setOrgStation] = useState<string>();
  const [searchResult, setSearchResult] = useState<Station[]>([]);

  useEffect(() => {
    if (orgStation) {
      const filteredStation = stations.filter((item: Station) =>
        item.label.toLocaleLowerCase().includes(orgStation.toLowerCase())
      );
      setSearchResult(filteredStation);
    }
  }, [orgStation]);

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
          sx={{ width: 300 }}
          renderInput={(params) => <TextField {...params} label="From" />}
        />
      </Box>
    </Box>
  );
};

export default Bus;


```
- အခုဆိုရင် react app မှာ mui autocomplete နဲ့ station ရွေးလို့ရပြီး ဖြစ်ပါတယ်

![enter image description here](https://raw.githubusercontent.com/Aungmyanmar32/msquare-m4/main/ep461%20%282%29.png)

-ဆက်ပြီးတော့ station တစ်ခုခု ရွေးလိုက်တာနဲ့ ရွေးလိုက်တဲ့ station ကို state တစ်ခုမှာ သိမ်းဖို့ လုပ်ပါမယ်။
```js
//define new state for selected station
 const [selectedStation, setSelectedStation] = useState<Station>();

//set clicked station as selectedStation state 
 <Autocomplete
          options={stations}
          onChange={(event, value) => value && setSelectedStation(value)}
          sx={{ width: 300 }}
          renderInput={(params) => <TextField {...params} label="From" />}
        />
```
- state အသစ်လုပ်ပြီးတော့ mui autocomplete မှာ ရွေးလိုက်တဲ့ station ကို onchange event ကိုသုံးပြီး အသစ်လုပ်ထားတဲ့ state ကို update လုပ်လိုက်တာဖြစ်ပါတယ်။
- ##
- update လုပ်ထားတဲ့ selectedStation ကို အသုံးပြုပြီး ရွေးထားတဲ့ station ကနေ သွားလို့ရမယ့် station တွေကို နောက်ထပ် autocomplete တစ်ခုနဲ့ ပြအောင် လုပ်ကြည့်ကြပါမယ်။

- selectedStation  ထဲက destination ကို state တစ်ခုနဲ့ ထပ်သိမ်းပါမယ်
```js
  const [destinationStation, setDestinationStation] = useState<Destination[]>();
  
  useEffect(() => {
    if (orgStation) {
      const filteredStation = stations.filter((item: Station) =>
        item.label.toLocaleLowerCase().includes(orgStation.toLowerCase())
      );
      setSearchResult(filteredStation);
    }
    setDestinationStation(selectedStation?.destination);
  }, [orgStation, selectedStation]);

```
-  return section မှာ mui autocomplete တစ်ခု ထပ်ထည့်ပါမယ်။
- အဲ့ဒီအထဲမှာ destination station တွေကို ပြပေးပါမယ်။

![enter image description here](https://raw.githubusercontent.com/Aungmyanmar32/msquare-m4/main/ep461%20%283%29.png)
- option မှာ destinationStation ကို ထည့်ပေးလိုက်တဲ့ အခါ error ပြနေတာကို တွေ့ရမှာ ဖြစ်ပါတယ်
- လောလောဆယ် အဆိုပါ options={destinationStation} ဆိုတဲ့ code ကို typecsript ကို မကြည့်ခိုင်းပဲ ကျော်သွားစေချင်တာ မလို့ //@ts-ignore ကို အသုံးပြုလိုက်ပါမယ်။

![enter image description here](https://raw.githubusercontent.com/Aungmyanmar32/msquare-m4/main/ep461%20%281%29.png)
- အခုဆိုရင် from မှာ station တစ်ခု ရွေးလိုက်တာနဲ့ သွားလို့ရနိုင်မယ့် station တွေကို To မှာ ပြပေးနိုင်ပြီး ဖြစ်ပါတယ်။

![enter image description here](https://raw.githubusercontent.com/Aungmyanmar32/msquare-m4/main/Screenshot%202023-03-28%20135016.png)
