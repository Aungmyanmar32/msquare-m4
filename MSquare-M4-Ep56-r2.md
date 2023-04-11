## MSquare Programing Fullstack Course
### Episode-*56* 
### Summary For `Room(2)`
## context provider
- ပြီးခဲ့တဲ့ သင်ခန်းစာမှာ context တစ်ခု create လုပ်ပြီး default value ကို ထည့်ပေးထားကာ အခြားcomponent ကနေ useContext နဲ့ အသုံးပြုခဲ့ကြပါတယ်။
-  အဲ့ဒီလို အသုံးပြုတဲ့အခါ context ရဲ့ default value ကို ပြောင်းလဲလို့မရပဲ  ရှိတဲ့အတိုင်းအသုံးပြုရပါတယ်။
- context ရဲ့ default value ကို state update ဖြစ်တိုင်း ပြောင်းလဲပြီး အသုံးပြုလို့ရအောင် provider နဲ့ အသုံးပြုပေးရပါတယ်
- cnotext ကို အသုံးပြုတဲ့ component ကို context provider နဲ့ wrap လုပ်ပေးရပါမယ်။
- context provider နဲ့ wrap လုပ်ထားတဲ့ မည်သည့်component မဆို context ကို အသုံးပြုတဲ့အခါ ပုံသေပေးထားတဲ့ value ကို dynamic ဖြစ်ဖြစ် အသုံးပြုလို့ ရပါတယ်
##
### Using context provider
- အရင်ဆုံး PassportAppContext **.ts** ကို PassportAppContext **.tsx** အဖြစ် tsxဖိုင်သို့ပြောင်းလိုက်ပါမယ်
- ပြီးတော့ အထဲက default value ကို null အဖြစ် ပြောင်းပြီး type ပြန်လုပ်လိုက်ပါမယ်။
```js
// PassportAppContext.tsx

import { createContext } from "react";

interface User {
  name: string;
  nrcNumber: string;
  dateOfBirth: string;
  phoneNumber: string;
  email: string;
}

interface BookingInfo {
  bookingDate: string | null;
  time: number | null;
  user: User | null;
  updateData: (value: any) => void;
}

const defaultContext = {
  bookingDate: null,
  time: null,
  user: null,
  updateData: () => {},
};

export const PassportAppContext = createContext<BookingInfo>(defaultContext);


```
- defaultContext မှာ updateData ဆိုတဲ့ function တစ်ခု ထပ်ထည့်လိုက်ပြီး
- PassportAppContext ကို name export လုပ်ထားလိုက်ပါတယ်။
- ဆက်ပြီး provider တစ်ခု သတ်မှတ်ပါမယ်။
```js
import { createContext, useState } from "react";

interface User {
  name: string;
  nrcNumber: string;
  dateOfBirth: string;
  phoneNumber: string;
  email: string;
}

interface BookingInfo {
  bookingDate: string | null;
  time: number | null;
  user: User | null;
  updateData: (value: any) => void;
}

const defaultContext = {
  bookingDate: null,
  time: null,
  user: null,
  updateData: () => {},
};

export const PassportAppContext = createContext<BookingInfo>(defaultContext);

const PassportProvider = ({children} : any) => {
  const [bookingData, setBookingData] = useState(defaultContext);

  return (
    <PassportAppContext.Provider value={{ ...bookingData, updateData: setBookingData }}>
      {children}
    </PassportAppContext.Provider>
  );
};

export default PassportProvider; 
```
> ရှင်းလင်းချက်
```js
const PassportProvider = ({children} : any) => {...}
```
- PassportProvider ဆိုတဲ့ component တစ်ခု လုပ်လိုက်ပါတယ်
- parameter အနေနဲ့  PassportProvider နဲ့ wrap လုပ်မယ့် ( context ကို အသုံးပြုမယ့်) children component ကို ခေါ်ထားလိုက်ပါတယ်။
```js
const [bookingData, setBookingData] = useState(defaultContext);

```
- bookingData ဆိုတဲ့ state  တစ်ခု ကို useState နဲ့ လုပ်ထားပြီး မူလတန်ဖိုးကို defaultContext အဖြစ်ထည်ပေးထားပါတယ်။
```js
return (
    <PassportAppContext.Provider value={{ ...bookingData, updateData: setBookingData }}>
      {children}
    </PassportAppContext.Provider>
  );
```
- parameter( props) အနေနဲ့ လက်ခံထားတဲ့ children component ကို PassportAppContext.Provider နဲ့ wrap လုပ်ပြီး return လုပ်ထားပါတယ်
- PassportAppContext.Provider မှာ value( props) အနေနဲ့ bookingData ဆိုတဲ့ state ရဲ့ တန်ဖိုးကို  အရင် copy လုပ်ပြီး ၊ သူ့အထဲက updateData ရဲ့ တန်ဖိုးကို setBookingData အဖြစ် ပြောင်းလဲသတ်မှတ်ပေးလိုက်ပါတယ်။
```js
export default PassportProvider; 
```
- ဒါကတော့  PassportProvider ကို  default export လုပ်ပေးလိုက်တာပါ။
- 
- ခု PassportAppContext ကို အသုံးပြုမယ့် PassportApp.tsx ကို PassportProvider component နဲ့ wrap လုပ်ပေးပါမယ်။
-  PassportApp.tsx ကို ခေါ်သုံးပြီး route လုပ်ထားတဲ့ index.tsx မှာ wrap လုပ်ပေးရမှာဖြစ်ပါတယ်။

ppp

- PassportApp.tsx ထဲမှာ context ကို သုံးပြီး datepicker မှာ ရွေးလိုက်တဲ့ ရက်ကို render လုပ်ပါမယ်။

```js
// PassportApp.tsx

import { Box, Button } from "@mui/material";
import { DatePicker, LocalizationProvider } from "@mui/x-date-pickers";
import { AdapterDayjs } from "@mui/x-date-pickers/AdapterDayjs";
import { log } from "console";
import { Dayjs } from "dayjs";
import React, { useContext, useEffect, useState } from "react";
import {PassportAppContext} from"../contexts/PassportAppContext";

const PassportApp = () => {
  const [month, setMonth] = useState<number>();

  useEffect(() => {
    if (month) {
      fetchAvailability();
    }
  }, [month]);

  // fetch to server with query param
  const fetchAvailability = async () => {
    const url = `http://localhost:5000/availability?month=${month}`;
    const response = await fetch(url);
    const data = await response.json();
    console.log(data);
  };

  // use context from contexts
  const { updateData, ...data } = useContext(PassportAppContext);

  return (
    <Box
      sx={{
        mw: "300px",
        display: "flex",
        flexDirection: "column",
        justifyContent: "center",
        p: 2,
        alignItems: "center",
      }}
    >
      <h1>Passport App</h1>
      <Box sx={{ margin: "0 auto", mt: 2, textAlign: "center" }}>
        <LocalizationProvider dateAdapter={AdapterDayjs}>
          <DatePicker
            disablePast
            format="DD/MM/YYYY"
            onChange={(value) => {
              const dayJsObj = value as Dayjs;
              setMonth(dayJsObj.month());
              updateData({
                ...data,
                bookingDate: dayJsObj.format("DD-MM-YYYY"),
              });
            }}
          />
        </LocalizationProvider>
      </Box>

      {/* show selected date */}
      <h1>{data.bookingDate}</h1>

    </Box>
  );
};

export default PassportApp;


```
> ရှင်းလင်းချက်
```js
import React, { useContext, useEffect, useState } from "react";
import {PassportAppContext} from"../contexts/PassportAppContext";
```
- PassportAppContext ကို  import လုပ်လိုက်တာဖြစ်ပါတယ်
```js
 const { updateData, ...data } = useContext(PassportAppContext);
```
- PassportAppContext ကို useContext နဲ့ သုံးလိုက်ပြီး ရလာတဲ့ object ကို destructure လုပ်ကာ updateData function နဲ့  ကျန် data တွေကို ခွဲ ထုတ်လိုက်ပါတယ်
```js
        <DatePicker
            disablePast
            format="DD/MM/YYYY"
            onChange={(value) => {
              const dayJsObj = value as Dayjs;
              setMonth(dayJsObj.month());
              updateData({
                ...data,
                bookingDate: dayJsObj.format("DD-MM-YYYY"),
              });
            }}
          />
```
- Date picker ထဲက onchange မှာ updateData function ကို ခေါ်လိုက်ပြီး bookingData ရဲ့   state ကို update လုပ်လိုက်တာဖြစ်ပါတယ်။

```js
<h1>{data.bookingDate}</h1>
```
- နောက်ဆုံးမှာတော့ data ထဲက bookingDate ကို h1 tag အနေနဲ့ ပြပေးလိုက်တာဖြစ်ပါတယ်။
##
### အနှစ်ချုပ်
 - react မှာ context ကို အသုံးပြုနိုင်ဖို့ 
   - context ကို default value နဲ့ အရင် create လုပ်ပေးရပါမယ်။
   ```js
   const defaultContext = 1
   const context1 = createContext(defaultContext)
   ```
   - ပြီးရင် context provider component တစ်ခု create လုပ်ပေးရပါမယ်

   - context provider component ထဲမှာ ပထမ create လုပ်ထားတဲ့ context ရဲ့ default value ကို update လုပ်နိုင်မယ့် useState တစ်ခု လုပ်ပေးပြီး
   - return လုပ်တဲ့အခါ ထို state ရဲ့ တန်ဖိုးကို props အနေနဲ့ ထည့်ပေးရပါမယ်။
   - wrap လုပ်ထားတဲ့ component ကို props အနေနဲ့ လက်ခံပြီး ထို propထဲက children ကို contextProvider နဲ့ wrap ပြီး return လုပ်ပေးရပါမယ်
```js

const contextProvider = ({ children }: any) => {
  const [contextValue, setContextValue] = useState(defaultContext);

  return (
    <context1.Provider value={contextValue} >
      {children}
    </context1.Provider>
  );
};
```

   - context ကို ခေါ်သုံးမယ့် component တွေကို context provider component ထဲမှာ wrap လုပ်ပြီးမှ ခေါ်သုံးပေးရမှာ ဖြစ်ပါတယ်
 ```js
<contextProvider>
   <Children/>
</contextProvider>
```
    
