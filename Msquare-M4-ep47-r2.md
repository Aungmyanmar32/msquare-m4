## MSquare Programing Fullstack Course
### Episode-*47* 
### Summary For `Room(2)` 
## render in react
### react မှာ component တစ်ခုဟာ အဓိက အားဖြင့်
1. Props change ချိန်းလိုက်ရင် 
2. သူ့ကို ထိန်းထားတဲ့ parent component က ren-render ပြန်လုပ်ရင်
3. State ချိန်းလိုက်ရင်
### re-render ( တစ်ခါပြန်run) လုပ်ပေးပါတယ်
- အခု ဒါကို နမူနာကြည့်ရအောင်
- App.jsx နဲ့ User.jsx မှာ log တစ်ခုဆီ ထုတ်ထားပါမယ်
```js
// App.jsx
import User from "./components/User";

const App = () => {
  console.log("App component rendered...");
  return (
    <div className="App">
      <User userName="user1" email="user1@gmial.com" />
    </div>
  );
};

export default App;

```
```js
// User.jsx
const User = (props) => {
  console.log("User component rendered...");
  return (
    <div>
      <h1>User name is {props.userName}</h1>
      <h1>email is {props.email}</h1>
    </div>
  );
};

export default User;

```
- ခု ကျနော်တို့ react app ကို refresh လုပ်ကြည့်လိုက်တဲ့အခါ console မှာ App component နဲ့ User component ကို render လုပ်ပေးတာကို မြင်ရမှာဖြစ်ပါတယ်။


![enter image description here](https://raw.githubusercontent.com/Aungmyanmar32/msquare-m4/main/Screenshot%202023-03-25%20230139.png)
> မှတ်ချက် ။   ။ log နှစ်ခုစီ ထုတ်ပေးနေပါက index.js မှာ အောက်ပါအတိုင်း ပြင်ပေးလိုက်ပါ။
```js
// index.js
import React from "react";
import ReactDOM from "react-dom/client";
import "./index.css";
import App from "./App";

const root = ReactDOM.createRoot(document.getElementById("root"));
root.render(
  <>
    <App />
  </>
);

```
- ခု App.jsx မှာ တစ်ခုခု ပြင်ကြည့်လိုက်ပါက App component သာမကသူ့အထဲမှာ render လုပ်ထားတဲ့ child component ဖြစ်တဲ့ User component ပါ re-render ဖြစ်သွားတာကို မြင်ရမှာပါ။
```js
// console output

App component rendered...
User component rendered...
App component rendered...
User component rendered...
```
- အဲ့ဒီလို parent component မှာ ပြောင်းလဲမှု ဖြစ်တိုင်း re-render လုပ်တဲ့အခါ child component ကို render တစ် ထပ်မလုပ်စေချင်ဘူးဆိုရင် component ကို export လုပ်တဲ့ အခါmemo( ) ကို အသုံးပြုနိုင်ပါတယ်။


```js
// App.jsx (parent )
import User from "./components/User";

const App = () => {
  const num1 = 10;
  console.log("App component rendered...");
  return (
    <div className="App">
      <User userName="user1" email="user1@gmial.com" />
    </div>
  );
};

export default App;

```
```js
// User.jsx (child)
import { memo } from  "react";
const User = (props) => {
  console.log("User component rendered...");
  return (
    <div>
      <h1>User name is {props.userName}</h1>
      <h1>email is {props.email}</h1>
    </div>
  );
};

export default memo(User);

```
- App component မှာ num1 ဆိုပြီး variable တစ်ခု ကြေငြာထားပါတယ်။
- User component မှာ memo ကို import လုပ်ထားပြီး export လုပ်တဲ့အခါ User component ကို memo function ထဲမှာ ထည့်ပေးထားတာဖြစ်ပါတယ်။
- num1 ရဲ့ တန်ဖိုး ကို တစ်ခုခု ပြောင်းကြည့်ပြီး  save လိုက်တဲ့ အခါ ခုနကလို App component ကော User component ပါ re-render မဖြစ်တော့ပဲ ပြောင်းလဲမှု ရှိတဲ့ parent component ကို သာ re-render လုပ်ပေးတာကို တွေ့ရမှာဖြစ်ပါတယ်
-  **memo( ) ကို အသုံးပြုခြင်းဖြင့် parent component က re-render လုပ်ချိန်မှာ child component  မှာ ပြောင်းလဲမှု မရှိဘူးဆိုရင် child component ကို re-render မဖြစ်အောင် ထိန်းချုပ်နိုင်ပါတယ်**


![enter image description here](https://raw.githubusercontent.com/Aungmyanmar32/msquare-m4/main/Screenshot%202023-03-25%20232200.png)

- ဒါပေမယ့် num1 ကို မချိန်းပဲ Props တန်ဖိုးတစ်ခုခု ( **userName = "user3"** )ကို ပြောင်းကြည့်လိုက်ပါက User component ကို memo ထဲ ထည့်းပေးထားသော်လည်း re-render လုပ်ပေးသွားတာကို မြင်တွေ့ရမှာပါ

![enter image description here](https://raw.githubusercontent.com/Aungmyanmar32/msquare-m4/main/Screenshot%202023-03-25%20232709.png)
- ဘာကြောင့်လဲ ဆိုရင် **react component တွေဟာ props ပြောင်းလဲမှု ရှိရင် re-render ပြန်လုပ်ပေး**တာမို့လို့ ဖြစ်ပါတယ်။
##
### React Hook
- react မှာ hook ဆိုတာ function တစ်မျိုးပဲ ဖြစ်ပြီး state တွေကို ထိန်းချုပ်နိုင်ဖို့အတွက် အသုံးပြုကြပါတယ်။
### State in react
- state ဆိုတာ react component တစ်ခုရဲ့ လက်ရှိအခြေအနေ ကို ဆိုလိုတာဖြစ်ပါတယ်။
- react ကို functional component နဲ့ ရေးတဲ့အခါ state တွေ သုံးလို့ရအောင် hook တွေနဲ့ ချိတ်ပေးရပါတယ်။
- react hook  ဆိုတာကလည်း function တစ်မျိုးလို့ သတ်မှတ်နိုင်ပါတယ်။
##
### useState hook
syntax
`const [ state , set-function] = useState(initialState) `
- **state** ဆိုတဲ့ နေရာမှာ useState ရဲ့ နောက် **(initialState )  ထဲက တန်ဖိုး** ၀င်လာမှာ ဖြစ်ပြီး၊
- **set-function** ကတော့  useState ရဲ့ နောက် **( initialState)  ထဲက တန်ဖိုးကို updateလုပ်တဲ့ function** လို့ အကြမ်းဖျင်းမှတ်သားထားပါ။


### Example code

    const [number ,setNumber] = useState(1)

##
### Using useState() hook in react
```js
// App.jsx 

import { useState } from "react";
import User from "./components/User";

const App = () => {
  const num1 = 30;
  const [name, setName] = useState("Aung");
  console.log("App component rendered...");
  return (
    <div className="App">
      <h1>My name is {name}</h1>
      <button onClick={() => setName("Myanmar")}>Click Me</button>
    </div>
  );
};

export default App;

```
> ရှင်းလင်းချက်

`import { useState } from "react";`
- useState hook ကို အသုံးပြုမှာမလို့ import လုပ်ထားပါတယ်

`const [name, setName] = useState("Aung");`
- useState hook ကို ကြေငြာထားပါတယ်
- ခု အချိန်မှာတော့ name ရဲ့ တန်ဖိုးက Aung ဖြစ်ပါတယ်။

```
return (
    <div className="App">
      <h1>My name is {name}</h1>
      <button onClick={() => setName("Myanmar")}>Click Me</button>
    </div>
  );
```
- return လုပ်ထားတဲ့နေရာမှာ name ရဲ့ တန်ဖိုးကို h1 tag အထဲ ယူသုံးထားပါတယ်
- Click Me button တစ်ခုလဲလုပ်ထားပြီး အဲ့ဒီခလုတ်ကို နှိပ်လိုက်တဲ့ အခါ useState hook ထဲက setName ဆိုတဲ့ function ကို ခေါ်လိုက်ပြီး မူလstate ရဲ့ တန်ဖိုး  ( Aung) ကို (Myanmar) အဖြစ်သို့ update လုပ်ခိုင်းထားပါတယ်
- react app ကို  start လိုက်တဲ့အခါ  အောက်ပါအတိုင်းအရင်ပြပေးမှာဖြစ်ပါတယ်။
-
![enter image description here](https://raw.githubusercontent.com/Aungmyanmar32/msquare-m4/main/Screenshot%202023-03-26%20000012.png)
- Click Me ခလုတ်ကို နှိပ်လိုက်ပါက state update ဖြစ်ပြီး အောက်ပါအတိုင်း ပြပေးမှာဖြစ်ပါတယ်

![enter image description here](https://raw.githubusercontent.com/Aungmyanmar32/msquare-m4/main/Screenshot%202023-03-26%20000244.png)

- console ထဲမှာ လဲ re-render တစ်ခါ ထပ်လုပ်ပေးသွားတာကို မြင်ရမှာပါ။
- react မှာ state ပြောင်းလဲမှု ရှိရင် ထို component ကို re-render လုပ်ပေးတာမို့လို့ ဖြစ်ပါတယ်။
