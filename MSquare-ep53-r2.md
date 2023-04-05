## MSquare Programing Fullstack Course
### Episode-*53* 
### Summary For `Room(2)`
## useEffect hook
- useEffect ဆိုတာက state တွေကို management လုပ်တဲ့ react hook တစ်မျိုး ဖြစ်ပါတယ်
- -   component တစ်ခု ပထမအကြိမ် render ပြီးသွားတဲ့အချိန် မှာ useEffect( ) ကို တစ်ခါ run ပေးလေ့ရှိပါတယ်
### syntex
```js
useEffect( callback-function , Dependency List [])
```
- useEffect မှာ **parameter နှစ်ခု** လက်ခံပါတယ်
- ဒုတိယ parameter ဖြစ်တဲ့ **Dependency List array ထဲ ရှိ state ရဲ့ တန်ဖိုး update ဖြစ်တဲ့အခါတိုင်း**  ပထမ parameter ဖြစ်တဲ့ **callbcak function  ကို ခေါ်ပေး**မှာဖြစ်ပါတယ်
##



- PassportApp.tsx မှာ useEffect ကို စမ်းသုံးကြည့်ပါမယ်
```js
//PassportApp.tsx

import { Box, Button } from "@mui/material";
import { log } from "console";
import React, { useEffect, useState } from "react";

const PassportApp = () => {
  const [number, setNumber] = useState(0);

  console.log("passport app rendered...")

  useEffect(() => {
    console.log("inside use effect");
  }, []);

  console.log("outside use effect ");

  return (
    <Box sx={{ mw: "300px", display: "flex", justifyContent: "center", p: 2 }}>
      
      <h1>Passport App</h1>

      <Button variant="contained" onClick={() => setNumber(number + 1)}>
        Click {number}
      </Button>
      
    </Box>
  );
};

export default PassportApp;

```
> ရှင်းလင်းချက်

```
const [number, setNumber] = useState(0);
```
- number state တစ်ခု လုပ်ထားပြီး number ရဲ့ မူလတန်ဖိုး က 0 ပေးထားပါတယ်။
```
console.log("passport app rendered...")
```
- component က render ဖြစ်သွားကြောင်း log ထုတ်ထားတာပါ
```
 useEffect(() => {
    console.log("inside use effect");
  }, []);
```
-  useEffect ကို သုံးထားပါတယ်။
   - callback function အထဲမှာ inside use effect ဆိုပြီး log ထုတ်ထားပါတယ်
   -  Dependency List ကို empty array ပဲ သတ်မှတ်ထားပါတယ်
```
console.log("outside use effect ");
```
- useEffect ရဲ့ အပြင်မှာ log တစ်ခု ထပ်ထုတ်ထားပါတယ်
```
 return (
    <Box sx={{ mw: "300px", display: "flex", justifyContent: "center", p: 2 }}>
      
      <h1>Passport App</h1>

      <Button variant="contained" onClick={() => setNumber(number + 1)}>
        Click {number}
      </Button>
      
    </Box>
  );
```
- button တစ်ခု return လုပ်ထားပြီး နှိပ်လိုက်တဲ့ အချိန်တိုင်း number ကို တစ်ပေါင်းပေးပြီး state update လုပ်ထားပါတယ်။
- ခု react app  ကို start လုပ်ပါ
- passport app ထဲ ၀င်ပါ
-  console မှာ အခုလို မြင်ရမှာဖြစ်ပါတယ်

![enter image description here](https://raw.githubusercontent.com/Aungmyanmar32/msquare-m4/main/01useEffect%20%281%29.png)
- ပထမ အကြိမ် render ဖြစ်တဲ့ အချိန်မှာ 
  - line 8 က console log ထွက်လာပါတယ်
  - line 11 က useEffect ကို ရောက်တဲ့အခါ useEffect က component တစ်ခု ပထမအကြိမ် render ဖြစ်တဲ့ အခါ ထို component ထဲရှိ သမျှ code တွေ render လုပ်ပြီး မှ run ပေးမှာ မို့လို့ useEffect ကို ကျော်ပြီး  ကျန်တဲ့ code တွေ ဆက်ပြီး render လုပ်သွားမှာ ဖြစ်ပါတယ်
  - ဒါကြောင့် console မှာ line 14 က **outside use effect**  က အရင် ပြပေးတာဖြစ်ပါတယ်
  - **component တစ်ခုလုံး ပထမ အကြိမ် render ပြီးတဲ့အခါကျမှ** useEffect ထဲက callback function ကို ပြန်ခေါ်ပေးတာမလို့ **inside use effect** က နောက်ဆုံးမှ ပေါ်လာတာဖြစ်ပါတယ်
  - ဆက်ပြီး button ကို click ပြီး number ရဲ့ state ကို update လုပ်ပါမယ်
  - state update ဖြစ်တာမလို့ passport component က render တစ်ခါ ထပ်ဖြစ်ပါမယ်
  
  ![enter image description here](https://raw.githubusercontent.com/Aungmyanmar32/msquare-m4/main/01useEffect%20%282%29.png)
  - render တစ်ခါ ထပ်ဖြစ်ပေမယ့် useEffect ထဲက log ထွက်မလာတာကို မြင်ရမှာပါ။
- useEffect ရဲ့ ဒုတိယ parameter ဖြစ်တဲ့ Dependency List ကို empty array ပဲ သတ်မှတ်ထားတာမလို့ useEffect  ထဲက callback function ဟာ component တစ်ခုလုံး ပထမ အကြိမ် render ပြီးတဲ့အခါ တစ်ကြီမ်သာ run ပေးမှာ ဖြစ်ပြီး 
- ထို component နောက်တစ်ကြိမ် render ထပ်ဖြစ်တဲ့အခါ useEffect က ထပ်မံ အလုပ်လုပ်မှာ မဟုတ်တော့ပါဘူး
- အထက်မှာ ရှင်းပြခဲ့သလိုပဲ ဒုတိယ parameter ဖြစ်တဲ့ Dependency List array ထဲ ရှိ state ရဲ့ တန်ဖိုး update ဖြစ်တဲ့အခါ useEffect ရဲ့ callback function က  တစ်ခါ ထပ်run ပေးမှာဖြစ်တာမလို့ 
- ဒိတစ်ခါ ဒုတိယ parameter ဖြစ်တဲ့ Dependency List ကို empty array မထားတော့ပဲ useState ထဲက number ကို list ထဲထည့်ပေးလိုက်ပါမယ်

```js
//PassportApp.tsx

import { Box, Button } from "@mui/material";
import { log } from "console";
import React, { useEffect, useState } from "react";

const PassportApp = () => {
  const [number, setNumber] = useState(0);

  console.log("passport app rendered...")

  useEffect(() => {
    console.log("inside use effect");
  }, [number]);

  console.log("outside use effect ");

  return (
    <Box sx={{ mw: "300px", display: "flex", justifyContent: "center", p: 2 }}>
      
      <h1>Passport App</h1>

      <Button variant="contained" onClick={() => setNumber(number + 1)}>
        Click {number}
      </Button>
      
    </Box>
  );
};

export default PassportApp;

```
- ဒီတစ်ခါ button ကို click လိုက်ပါက number state က update ဖြစ်သွားတာမလို့
- useEffect ရဲ့ အထဲက log ပါ ပြပေးလာတာကို မြင်ရမှာ ဖြစ်ပါတယ်

![enter image description here](https://raw.githubusercontent.com/Aungmyanmar32/msquare-m4/main/Screenshot%202023-04-06%20024528.png)
##
### Query params
![enter image description here](https://nullbeans.com/wp-content/uploads/2020/05/urldescription-1.png)

- url တစ်ခုရဲ့ route နောက်မှာ  ? ပါလာခဲ့ရင် 
- ? နောက်ကအရာတွေကို query params လို့ သတ်မှတ်ပါတယ်
```
http://localhost:5000/route-name?(query param)
```
- query param မှာ key နဲ့ value ဆိုပြီး ရှိပါတယ်
```
http://localhost:5000/route-name?key=value
```
```
http://localhost:5000/upload?user=aung
```
- query param ကို အသုံးပြုပြီး backend server  ဆီ request လုပ်တဲ့အခါ ပို့ချင်တဲ့ data ကို request url နဲ့ အတူ တစ်ပါတည်း ပို့ပေးလို့ ရပါတယ်
- အခု query param ကို စမ်းသုံးကြည့်ပါမယ်
- အရင်ဆုံး backend folder အသစ်တစ်ခု လုပ်ပါ
- အဲ့ဒိမှာ npm init လုပ်ပေးပါ
- package.json ရလာရင် အောက်ကကုဒ်တွေနဲ့ အစားထိုးပေးလိုက်ပြီး npm install ပြန်လုပ်ပေးပါ။
```
{
  "name": "backend",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "start": "nodemon server.ts"
  },
  "keywords": [],
  "author": "",
  "license": "ISC",
  "dependencies": {
    "cors": "^2.8.5",
    "express": "^4.18.2",
    "ts-node": "^10.9.1",
    "typescript": "^4.9.5"
  },
  "devDependencies": {
    "@types/express": "^4.17.17",
    "@types/cors": "^2.8.13",
    "nodemon": "^2.0.22"
  }
}
```
- npm install လုပ်ပြီးပါက server.ts ဖိုင်တစ်ခုလုပ်ပြီး express server တစ်ခု လုပ်ပေးပါ
```js
//server.ts

import express from "express";
import cors from "cors";
const app = express();
const port = 5000;
app.use(cors());

app.get("/availability", (req, res) => {
  res.send("Hello World!");
});

app.listen(port, () => {
  console.log(`Example app listening on port ${port}!`);
});
```
##
- ခု react app ထဲက PassportApp.tsx မှာ express server  ဆီ query paramနဲ့ request လုပ်ပါမယ်
```js
// PassportApp.tsx

import { Box, Button } from "@mui/material";
import { log } from "console";
import React, { useEffect, useState } from "react";

const PassportApp = () => {
  const [number, setNumber] = useState(0);

  useEffect(() => {
    fetchAvailability();
  }, []);

  // fetch to server with query param
  const fetchAvailability = async () => {
    const url = "http://localhost:5000/availability?user=aung";
    const response = await fetch(url);
    const data = await response.json();
    console.log(data);
  };

  return (
    <Box sx={{ mw: "300px", display: "flex", justifyContent: "center", p: 2 }}>
      <h1>Passport App</h1>

      <Button variant="contained" onClick={() => setNumber(number + 1)}>
        Click {number}
      </Button>
    </Box>
  );
};

export default PassportApp;

```
> ရှင်းလင်းချက်
```
useEffect(() => {
    fetchAvailability();
  }, []);

  // fetch to server with query param
  const fetchAvailability = async () => {
    const url = "http://localhost:5000/availability?user=aung";
    const response = await fetch(url);
    const data = await response.json();
    console.log(data);
  };
```
- fetchAvailability  ဆိုတဲ့ function တစ်ခု လုပ်ထားပြီး  express server ဆီ request လုပ်ထားပါတယ်
- fetchAvailability  function ကို useEffect ထဲမှာ  ခေါ်ထားပါတယ်
- PassportApp component render လုပ်ပြီးတဲ့အခါမှာ express serverဆီ fetch လုပ်မှာ ဖြစ်ပါတယ်
- ခု express server မှာ request ကို လက်ခံပြီး response လုပ်ဖို့ ပြင်ဆင်ပါမယ်
```js
// backend/server.ts

import express from "express";
import cors from "cors";
const app = express();
const port = 5000;
app.use(cors());

app.get("/availability", (req, res) => {
  const user = req.query;
  console.log(user);
  res.send(user);
});

app.listen(port, () => {
  console.log(`Example app listening on port ${port}!`);
});
```
>ရှင်းလင်းချက်
```
app.get("/availability", (req, res) => {
  const user = req.query;
  console.log(user);
  res.send(user);
});
```
- get middleware ကို သုံးပြီး  ၀င်လာတဲ့ requestကို လက်ခံပါတယ်
- user ဆိုတဲ့ variable ထဲမှာ request urlနဲ့အတူပါလာတဲ့ query param ကို သိမ်းလိုက်ပါတယ်
-query param ကို သိမ်းထားတဲ့ user ဆိုတဲ့ variable ကိုပဲ server မှာ log လဲထုတ်ကြည့်ထားပြီး responseလဲ ပြန်ထားလိုက်ပါတယ်
- ခု express server ကို run ပေးထားပါ
```properties
aungm@MSquare MINGW64 ~/Desktop/backend
$ npm start
```
- react app ကိုလည်း start လုပ်ပေးပါ။
```properties
aungm@MSquare MINGW64 ~/Documents/apps (main)
$ npm start
```
> မှတ်ချက် ။   ။ express server ရော react app ပါ start လုပ်ပေးထားနိုင်ရန် 
> vs code မှာ terminal နှစ်ခု ဖွင့်၍သော်လည်းကောင်း ၊ 
> apps folder နှင့် backend folder တို့ကို vs code window တစ်ခုစီ ခွဲ ဖွင့်ထား၍သော်လည်းကောင်း အသုံးပြုနိုင်ပါသည်

-  ခု react app မှာ passport app ထဲ၀င်ပြီး terminal ကို ကြည့်လိုက်ပါက express server ကနေ response ပြန်လာတဲ့ user object ကို မြင်ရမှာ  ဖြစ်ပြီး 
```js
// browser console
Object
user: "aung"
[[Prototype]]: Object
```
- express server မှာလည်း query param အဖြစ် ၀င်လာတဲ့ data ကို log ထုတ်ကြည့်ထားတာမို့ terminal မှာ လည်း object တစ်ခု ပြပေးတာမြင်ရမှာပါ

```js
// epress ternimal

{ user: 'aung' }
```
##
### PassportApp မှာ mui date-picker တစ်ခု ထည့်ပြီး date တစ်ခုခုရွေးလိုက်တဲ့အခါ ရလာမယ့် month ကို query param အနေနဲ့ သုံးပြီး server ဆီ request လုပ်ကြည့်ရအောင်

```js
// PassportApp.tsx

import { Box, Button } from "@mui/material";
import { LocalizationProvider, DatePicker } from "@mui/x-date-pickers";
import { AdapterDayjs } from "@mui/x-date-pickers/AdapterDayjs";
import { log } from "console";
import { Dayjs } from "dayjs";
import React, { useEffect, useState } from "react";

const PassportApp = () => {
  const [month, setMonth] = useState<number>();

  useEffect(() => {
    fetchAvailability();
  }, [month]);

  // fetch to server with query param
  const fetchAvailability = async () => {
    const url = `http://localhost:5000/availability?month=${month}`;
    const response = await fetch(url);
    const data = await response.json();
    console.log(data);
  };

  return (
    <Box sx={{ mw: "300px", display: "flex", justifyContent: "center", p: 2 }}>
      <h1>Passport App</h1>

      <Box sx={{ margin: "0 auto", mt: 2, textAlign: "center" }}>
        <LocalizationProvider dateAdapter={AdapterDayjs}>
          <DatePicker
            disablePast
            onChange={(value) => {
              const dayJsObj = value as Dayjs;
              setMonth(dayJsObj.month());
            }}
          />
        </LocalizationProvider>
      </Box>
    </Box>
  );
};

export default PassportApp;

```
> ရှင်းလင်းချက်

```
const [month, setMonth] = useState<number>();
```
- useState နဲ့ state တစ်ခု လုပ်ထားပါတယ်
```
useEffect(() => {
    fetchAvailability();
  }, [month]);
```
- month ရဲ့ state  ချိန်းတိုင်း useEffect ထဲက  fetchAvailability() ကို ခေါ်ခိုင်းထားပါတယ်
```
 const fetchAvailability = async () => {
    const url = `http://localhost:5000/availability?month=${month}`;
    const response = await fetch(url);
    const data = await response.json();
    console.log(data);
  };
```
- request လုပ်တဲ့ url ထဲမှာ query param အဖြစ် month state ရဲ့ value ကို  ထည့်ပေးလိုက်ပါတယ်
```
<Box sx={{ margin: "0 auto", mt: 2, textAlign: "center" }}>
        <LocalizationProvider dateAdapter={AdapterDayjs}>
          <DatePicker
            disablePast
            onChange={(value) => {
              const dayJsObj = value as Dayjs;
              setMonth(dayJsObj.month());
            }}
          />
        </LocalizationProvider>
      </Box>
```
- mui date picker တစ်ခု ယူသုံးထားပါတယ်
```
onChange={(value) => {
              const dayJsObj = value as Dayjs;
              setMonth(dayJsObj.month());
            }}
```
- date picker မှာ ရက်တစ်ခုခု  ရွေးလိုက်တဲ့အခါ ရလာမယ့် VALUE ထဲက month() ကို month state ရဲ့ တန်ဖိုးအဖြစ် သတ်မှတ်လိုက်တာဖြစ်ပါတယ်။
- ခု react app မှာ date တစ်ခုခု ရွေးကြည့်လိုက်ပါ server ကresponse ပြန်လာတဲ့ object ကို မြင်ရမှာဖြစ်ပါတယ်

![enter image description here](https://raw.githubusercontent.com/Aungmyanmar32/msquare-m4/main/Screenshot%202023-04-06%20040845.png)
