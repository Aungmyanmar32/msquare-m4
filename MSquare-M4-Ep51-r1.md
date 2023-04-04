## MSquare Programing Fullstack Course
### Episode-*50* 
### Summary For `Room(1)` intermediate Class
##
### Using context in project
- တကယ့် project တွေလုပ်တဲ့အခါ function တွေ component တွေကို သက်ဆိုင်ရာ folder ထဲမှာ တစ်ခုဆီ ခွဲသိမ်းလေ့ရှိပါတယ်။
- ဥပမာ - type တွေအတွက် သီးသန့်ဖိုင်တစ်ခုခွဲပြီး သိမ်းထာဟတာမျိုး / ROUTE တွေ အတွက် သီးသန့် folder လုပ်ပြီး ခွဲ သိမ်း ထားတာမျိုးကို ဆိုလိုတာပါ
- အခု project ထဲမှာလဲ အဲ့ဒီလို လုပ်ထားလိုက်ပါမယ်
- context အတွက် src အောက်မှာ contexts folder တစ်ခုလုပ်ပါ။
- typing အတွက် src အောက်မှာပဲ typings folder တစ်ခုလုပ်ပါ။
- contexts folder အထဲမှာ PassportAppContext ဖိုင် တစ်ခုလုပ်ပြီး passport app အတွက်  context တစ်ခု လုပ်ပါမယ်။
```js
// src/contexts/PassportAppContext.tsx

import React, { createContext } from "react";

const defaultPassportContext = {
  date: null,
  time: null,
  user: null,
  handleUpdate: (data:any)=>{}
};

export const PassportAppContext = createContext(defaultPassportContext);

```
- context ရဲ့ default value အနေနဲ့ date,time နဲ့ user info တွေပါတဲ့ object တစ်ခု သတ်မှတ်ပေးထားပါတယ်
- ခု context ကို type လုပ်ပါမယ်
- src folder အောက်က typings folder ထဲမှာ PassportAppContextType.ts ဖိုင်တစ်ခုလုပ်ပါမယ်။
```js
// src/typings/PassportAppContextTypes.ts

interface User {
  name: string;
  dateOfBirth: Date;
  nrcNumber: string;
  email: string;
  phoneNumber: string;
}

export interface PassportAppContextType {
  date: Date | null;
  time: number | null;
  user: User | null;
  handleUpdate: (data:any)=> void
}

```
- အဲ့ဒီ သတ်မှတ်ထားတဲ့ type ကို context type အဖြစ်ပေးပါမယ်

```js
// src/contexts/PassportAppContext.tsx
import { PassportAppContextType } from  "../typings/PassportAppContextType";
import React, { createContext } from "react";

const defaultPassportContext: PassportAppContextType = {
  date: null,
  time: null,
  user: null,
  handleUpdate: (data:any)=>{}
};

export const PassportAppContext = createContext<PassportAppContextType>(defaultPassportContext);

```
##
- ဆက်ပြီးတော့ Passport.tsx component မှာ context ကို အသုံးပြုကြည့်ပါမယ်
```js
// src/apps/Passport.tsx

import { Button } from "@mui/material";
import { useContext } from "react";
import { PassportAppContext } from "../../contexts/PassportAppContext";

const Passport = () => {

  //Using context
  const { handleUpdate, ...data } = useContext(PassportAppContext);

  return (
    <div className="container">
      <div className="app">
      
     
          {/* add Button for test context */}
        <Button
          variant="contained"
          sx={{ mb: 2 }}
          onClick={() => {
            handleUpdate({ ...data, time: 20 });
            console.log("outSide", data);
          }}
        >
          Update context
        </Button>

        <Button variant="contained" sx={{ mb: 2 }}>
          <a
            href={`/passport/create-booking`}
            style={{ textDecoration: "none", color: "white" }}
          >
            Create Booking
          </a>
        </Button>
        <Button variant="contained" sx={{ mb: 2 }}>
          <a
            href={`/passport/check-booking`}
            style={{ textDecoration: "none", color: "white" }}
          >
            Check Booking
          </a>
        </Button>
      </div>
    </div>
  );
};

export default Passport;
```
- Passport comportnent ထဲမှာ PassportAppContext ကို ခေါ်သုံးထားပါပြီး handleUpdate function ကို PassportAppContext ရဲ့ value ထဲကနေ ပြန်ထုတ်ထားပါတယ်
- return ထဲမှာ button တစ်ခု လုပ်ထားပြီး click လုပ်လိုက်ရင် context ထဲက  handleUpdate function ကို ခေါ်ပေးထားပါတယ်။ အဲ့ဒီfunction အထဲက parameter မှာ time ရဲ့ တန်ဖိုးကို null အစား 40 အဖြစ် update လုပ်ထားပါတယ်
- ခု react app  ကို start လုပ်ပြီး passport app ထဲ ၀င်ကာ update context ကို clickကြည့်ပါက provider ထဲက log က မပေါ်လာပဲ outside log ဖြစ်တဲ့ Passport component ထဲက logပဲ ပြပေးတာမြင်ရမှာပါ။

![enter image description here](https://raw.githubusercontent.com/Aungmyanmar32/msquare-m4/main/Screenshot%202023-04-04%20152056.png)

### React မှာ context provider ကို သုံးချင်ရင် , သုံးချင်တဲ့ component ကို context.provider ထဲ ထည့်ခေါ်ပေးရမှာ ဖြစ်ပါတယ်။
- ခု project မှာ context ကို သုံးထားတဲ့ Passport component ကို  ခေါ်သုံးထားတဲ့ နေရာကို သွားပြီး context provider နဲ့ wrap လုပ်ပေးပါမယ်။
```js
//src index.tsx 

import ReactDOM from "react-dom/client";
import "./index.css";
import App from "./App";
import { createBrowserRouter, RouterProvider } from "react-router-dom";
import CreateBooking from "./Routes/CreateBooking";
import CheckBooking from "./Routes/CheckBooking";
import { PassportAppProvider } from "./contexts/PassportAppContext";
import BusRoute from "./Routes/BusRoute";
import Passport from "./components/Apps/Passport";

const router = createBrowserRouter([
  {
    path: "/",
    element: <App />,
  },
  {
    path: "/bus",
    element: <BusRoute />,
  },
  {
    path: "/passport",
    element: (
      <PassportAppProvider>
        <Passport />
      </PassportAppProvider>
    ),
  },
  {
    path: "/passport/create-booking",
    element: <CreateBooking />,
  },
  {
    path: "/passport/check-booking",
    element: <CheckBooking />,
  },
]);

const root = ReactDOM.createRoot(
  document.getElementById("root") as HTMLElement
);
root.render(<RouterProvider router={router} />);

```
- ခုဆိုရင် Update Context ကို နှိပ်ကြည့်လိုက်ပါက log နှစ်ခုလုံး ပြပေးမှာဖြစ်ပြီး time ရဲ့ value လည်း 40 အဖြစ် update ဖြစ်သွားတာကိုမြင်ရမှာပါ။

![enter image description here](https://raw.githubusercontent.com/Aungmyanmar32/msquare-m4/main/Screenshot%202023-04-04%20154505.png)
