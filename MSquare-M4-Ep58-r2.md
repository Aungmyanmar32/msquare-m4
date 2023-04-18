## MSquare Programing Fullstack Course
### Episode-*58* 
### Summary For `Room(2)`
##
### Passport app with *mui stepper*
- ခု သင်ခန်းစာမှာတော့ အရင် သင်ခန်းစာတွေမှာ သင်ထားခဲ့တဲ့ အကြောင်းအရာတွေကို အသုံးပြုပြီး passport booking app ကို  လုပ်ကြသွားပါမယ်။
##
- PassportStepper.tsx ဆိုပြီး component အသစ်တစ်ခုကို component folder ထဲမှာ လုပ်ပါမယ်။
- အဲ့ဒီအထဲကို mui stepper တစ်ခု ကူးထည့်လိုက်ပါမယ်။
```js
// PassportStepper.tsx
import React, { useState } from "react";
import Box from "@mui/material/Box";
import Stepper from "@mui/material/Stepper";
import Step from "@mui/material/Step";
import StepLabel from "@mui/material/StepLabel";
import Button from "@mui/material/Button";
import Typography from "@mui/material/Typography";


const steps = ["Date and time", "User info", "Review and confirm"];

const PassportStepper = () => {
  const [activeStep, setActiveStep] = useState(0);

  const handleNext = () => {
    setActiveStep(activeStep + 1);
  };

  const handleBack = () => {
    setActiveStep(activeStep - 1);
  };

  return (
    <Box sx={{ maxWidth: "50%", margin: "0 auto", mt: 5 }}>
      <Stepper activeStep={activeStep}>
        {steps.map((label, index) => {
          const stepProps: { completed?: boolean } = {};
          const labelProps: {
            optional?: React.ReactNode;
          } = {};
          return (
            <Step key={label} {...stepProps}>
              <StepLabel {...labelProps}>{label}</StepLabel>
            </Step>
          );
        })}
      </Stepper>
      <>
        <Typography sx={{ mt: 2, mb: 1 }}>
          Step {activeStep + 1}
        </Typography>
        <Box sx={{ display: "flex", flexDirection: "row", pt: 2 }}>
          <Button
            color="inherit"
            disabled={activeStep === 0}
            onClick={handleBack}
            sx={{ mr: 1 }}
          >
            Back
          </Button>
          <Box sx={{ flex: "1 1 auto" }} />
          <Button onClick={handleNext}>
            {activeStep === steps.length - 1 ? "Finish" : "Next"}
          </Button>
        </Box>
      </>
    </Box>
  );
};

export default PassportStepper;
```
- ` const [activeStep, setActiveStep] = useState(0);`
- activeStep ဆိုတဲ့ state တစ်ခုလုပ်ထားပြီး အဲ့ဒီ state ရဲ့ တန်ဖိုးပေါ် မူတည်ပြီး  step တွေကို update လုပ်မှာဖြစ်ပါတယ်။
```js
  const handleNext = () => {
    setActiveStep(activeStep + 1);
  };

  const handleBack = () => {
    setActiveStep(activeStep - 1);
  };
```

- next ခလုတ်ကို နှိပ်လိုက်ရင် activeStep တန်ဖိုးကို တစ် ပေါင်းပေးမှာဖြစ်ပြီး။ back ခလုတ်ကို နှိပ်လိုက်ရင်တော့ တစ် နှုတ်ပေးအောင် သတ်မှတ်ထားပါတယ်။
- 
```js
<>
        <Typography sx={{ mt: 2, mb: 1 }}>
          Step {activeStep + 1}
        </Typography>
        <Box sx={{ display: "flex", flexDirection: "row", pt: 2 }}>
          <Button
            color="inherit"
            disabled={activeStep === 0}
            onClick={handleBack}
            sx={{ mr: 1 }}
          >
            Back
          </Button>
          <Box sx={{ flex: "1 1 auto" }} />
          <Button onClick={handleNext}>
            {activeStep === steps.length - 1 ? "Finish" : "Next"}
          </Button>
```
- လက်ရှိရောက်နေတဲ့ step နဲ့ button တွေကို UI မှာ ပြပေးထားတာဖြစ်ပါတယ်။
- ပြီးရင် DateAndTime.tsx ဖိုင်တစ်ခု ထပ်လုပ်ပါမယ်။
- အဲ့ဒီအထဲကို PassportApp.tsx ထဲမှာ return လုပ်ထားတဲ့ code တွေ cut လုပ်ပြီး ထည့်ပေးလိုက်ပါမယ်။
```js
// DateAndTime.tsx
import { Box } from "@mui/material";
import { DatePicker } from "@mui/x-date-pickers";
import { DemoContainer } from "@mui/x-date-pickers/internals/demo";
import { Dayjs } from "dayjs";
import { useContext } from "react";
import { PassportAppContext } from "../contexts/PassportAppContext";

const DateAndTime = () => {
  const { updateData, ...data } = useContext(PassportAppContext);
  return (
    <>
      <Box sx={{ maxWidth: 200, margin: "0 auto", minHeight: 200 }}>
        <DemoContainer components={["DatePicker"]}>
          <DatePicker
            label="Basic date picker"
            disablePast
            format="DD-MM-YYYY"
            onChange={(value) => {
              const dayjsObj = value as Dayjs;
              const month = dayjsObj.month();
              updateData({
                ...data,
                bookingDate: dayjsObj.format("DD-MM-YYYY"),
              });
              //setSelectedMonth(month);
            }}
          />
        </DemoContainer>
      </Box>
    </>
  );
};

export default DateAndTime;
```
- ပြီးရင် PassportApp.tsx မှာ PassportStepper component ကို  render လုပ်ပါမယ်။
```js
// PassportApp.tsx

import { Box, Button } from "@mui/material";
import { DatePicker, LocalizationProvider } from "@mui/x-date-pickers";
import { AdapterDayjs } from "@mui/x-date-pickers/AdapterDayjs";
import { log } from "console";
import { Dayjs } from "dayjs";
import React, { useContext, useEffect, useState } from "react";
import { PassportAppContext } from "../contexts/PassportAppContext";
import PassportStepper from "../components/PassportStepper";

const PassportApp = () => {
  const [month, setMonth] = useState<number>();

  // useEffect(() => {
  //   if (month) {
  //     fetchAvailability();
  //   }
  // }, [month]);

  // fetch to server with query param
  // const fetchAvailability = async () => {
  //   const url = `http://localhost:5000/availability?month=${month}`;
  //   const response = await fetch(url);
  //   const data = await response.json();
  //   console.log(data);
  // };

  // use context from contexts
  const { updateData, ...data } = useContext(PassportAppContext);
  console.log(data);
  return <PassportStepper />;
};

export default PassportApp;

```
- ဆက်ပြီးတော့  PassportStepper.tsx မှာ active step ရဲ့ state ကို စစ်ပြီး ပထမအဆင့်မှာ DateAndTime component ကို render လုပ်ပါမယ်။
- 
![enter image description here](https://raw.githubusercontent.com/Aungmyanmar32/msquare-m4/main/ep58r2%20%281%29.png)

- activeStep ရဲ့ တန်ဖိုး 0 ဖြစ်နေတဲ့အချိန်မှာ DateAndTime component ကို render လုပ်ပေးမှာ ဖြစ်ပါတယ်။
- npm start လုပ်ပြီး app  ကို စမ်းသပ်ကြည့်တဲ့ အခါ ခုလို ပြပေးမှာ ဖြစ်ပါတယ်။

![enter image description here](https://raw.githubusercontent.com/Aungmyanmar32/msquare-m4/main/ep58r2%20%282%29.png)
##
### ဆက်ပြီး UserInfo.tsx ဖိုင်တစ်ခု ထပ်လုပ်ပါမယ်
- အဲဒီအထဲမှာ User info တွေ ထည့်ပေးလို့ရမယ့် text field ( input) တွေ လုပ်ပါမယ်။
```js
// UserInfo.tsx
import { Box, TextField } from "@mui/material";
import { useContext } from "react";
import { PassportAppContext } from "../contexts/PassportAppContext";

const UserInfo = () => {
  const { updateData, ...data } = useContext(PassportAppContext);
  return (
    <Box
      sx={{
        display: "flex",
        flexDirection: "column",
      }}
    >
      <TextField
        required
        id="name"
        sx={{ maxWidth: "300px", margin: "0 auto", mb: 2 }}
        placeholder="Name"
        onChange={(evt) => console.log(evt.target.value)}
      />
      <TextField
        required
        id="nrc_number"
        sx={{ maxWidth: "300px", margin: "0 auto", mb: 2 }}
        placeholder="NRC number"
      />
      <TextField
        required
        id="email"
        sx={{ maxWidth: "300px", margin: "0 auto", mb: 2 }}
        placeholder="Email"
      />
    </Box>
  );
};

export default UserInfo;
```
- mui text field သုံးခု လုပ်ထားပြီး name ဆိုတဲ့ text field မှာ onchange event ဖမ်းကာ log ထုတ်ကြည့်ထားပါတယ်။
- ခု UserInfo component  ကို PassportStepper component မှာ step 2 ဖြစ်တဲ့အချိန် render လုပ်ပါမယ်

![enter image description here](https://raw.githubusercontent.com/Aungmyanmar32/msquare-m4/main/ep58r2%20%283%29.png)
- ကျနော်တို့ရဲ့ app မှာ next ကို step 2 ပြောင်းကြည့်ပါက ခုလို မြင်ရမှာ ဖြစ်ပါတယ်။

![enter image description here](https://raw.githubusercontent.com/Aungmyanmar32/msquare-m4/main/ep58r2%20%284%29.png)
##
### step 3
- step 3 မှာ render လုပ်ဖို့ ConfirmAndReivew component တစ်ခု ထပ်လုပ်ပါမယ်။
```js

    // ConfirmAndReview.tsx
    import { Box } from "@mui/material";
    
    const ConfirmAndReivew = () => {
      return (
        <Box sx={{ display: "flex", justifyContent: "center" }}>
          <h1>Confirm and review</h1>
        </Box>
      );
    };
    
    export default ConfirmAndReivew;
   
```
- အဲ့ဒီ component ကို step 3 အဖြစ် PassportStepper မှာ render လုပ်ပါမယ်

![enter image description here](https://raw.githubusercontent.com/Aungmyanmar32/msquare-m4/main/ep58r2%20%286%29.png)
- အောက်နားက next button ကို ပြတဲ့နေရာမှာလည်း activeStep ရဲ့ တန်ဖိုးကို စစ်ပြီး button ထဲက text နဲ့ onclick ကို ပြင်ထားပါတယ်။
##
- ဆက်ပြီး useContext နဲ့ useState ကို အသုံးပြုပြီး context ရဲ့ default value ကို update လုပ်ပါမယ်
```js
// UserInfo.tsx
import { Box, TextField } from "@mui/material";
import { useContext } from "react";
import { PassportAppContext } from "../contexts/PassportAppContext";

const UserInfo = () => {
  const { updateData, ...data } = useContext(PassportAppContext);
 
  return (
    <Box
      sx={{
        display: "flex",
        flexDirection: "column",
      }}
    >
      <TextField
        required
        id="name"
        sx={{ maxWidth: "300px", margin: "0 auto", mb: 2 }}
        placeholder="Name"
        onChange={(evt) =>
          updateData({
            ...data,
            user: { ...data.user, name: evt.target.value },
          })
        }
      />
      <TextField
        required
        id="nrc_number"
        sx={{ maxWidth: "300px", margin: "0 auto", mb: 2 }}
        placeholder="NRC number"
        onChange={(evt) =>
          updateData({
            ...data,
            user: { ...data.user, nrcNumber: evt.target.value },
          })
        }
      />
      <TextField
        required
        id="email"
        sx={{ maxWidth: "300px", margin: "0 auto", mb: 2 }}
        placeholder="Email"
        onChange={(evt) =>
          updateData({
            ...data,
            user: { ...data.user, email: evt.target.value },
          })
        }
      />
    </Box>
  );
};

export default UserInfo;

```
- `  const { updateData, ...data } = useContext(PassportAppContext);`
- useContext နဲ့ PassportAppContext ကို ခေါ်သုံးထားပြီး PassportAppContext ရဲ့ တန်ဖိုးအနေနဲ့ ပါလာတဲ့ value တွေထဲက updateData function ကို ခွဲထုတ်လိုက်ပြီး ကျန်တဲ့ data တွေကို data ဆိုတဲ့ object ထဲမှာ ပြန်သိမ်းထားတာဖြစ်ပါတယ်။
- 
```js
<TextField
        required
        id="name"
        sx={{ maxWidth: "300px", margin: "0 auto", mb: 2 }}
        placeholder="Name"
        onChange={(evt) =>
          updateData({
            ...data,
            user: { ...data.user, name: evt.target.value },
          })
        }
      />
```
- text field တွေမှာ onchange event ကို  ဖမ်းထာလိုက်ပြီး ရိုက်ထည့်လိုက်တဲ့ text တွေကို updateData function နဲ့ context ရဲ့ value ကို update လုပ်ပါတယ်။
```js
updateData({
            ...data,
            user: { ...data.user, name: evt.target.value },
          })
```
- updateData function ကို ခေါ်သုံးတဲ့အခါ အရင်ဆုံး `...data` ဆိုပြီး data ထဲရှိသမျှ ကူးလိုက်ပါတယ်။
- ပြီးမှ data ထဲမှာ ပါလာတဲ့ user ဆိုတဲ့ object အထဲက name ကို ရိုက်ထည့်ပေးလိုက်တဲ့ text အနေနဲ့ update လုပ်မှာမလို့ `...data.user` ဆိုပြီး နဂို ရှိပြီးသား user object ကို copy အရင် လုပ်ပါတယ်။
- user object အထဲက မှ name ရဲ့ တန်ဖိုးကို text field ကနေ ရိုက်ထည့်လိုက်တဲ့ စာအနေနဲ့ update လုပ်လိုက်တာဖြစ်ပါတယ်။
- ကျန် တဲ့ email နဲ့ NRC တွေကိုလည်း ထိုနည်းအတိုင်းပဲ update လုပ်လိုက်မှာဖြစ်ပါတယ်။
- ခု ကျနော်တို့ရဲ့ app ကို စမ်းသပ်ကြည့်တဲ့အခါ ခုလို မြင်ရမှာဖြစ်ပါတယ်။


![enter image description here](https://raw.githubusercontent.com/Aungmyanmar32/msquare-m4/main/ep58r2%20%287%29.png)

