## MSquare Programing Fullstack Course
### Episode-*50* 
### Summary For `Room(2)`
## React with typescript
### React app တစ်ခုကို typescriptနဲ့ ရေးနိုင်ဖို့ react app ကို create လုပ်တဲ့အခါ typescript template ကို တစ်ခါတည်း install လုပ်ပေးရပါမယ်
- react app project အသစ်တစ်ခု လုပ်ပါမယ်
```js
npx create-react-app react-ts --template typescript
```
- src folder အောက်မှာ component folder တစ်ခု ဆောက်ပြီး User component (**User.tsx**)တစ်ခု လုပ်ပါမယ်
- ပြီးရင် User component ကို App.tsx မှာ ခေါ်သုံးပြီး render လုပ်ပါမယ်
```js
// src/components/User.tsx

import React from "react";
import "../App.css";

const User = () => {
  return (
    <div>
      <h1>Hello world</h1>
    </div>
  );
};

export default User;

```
```js
//App.tsx

import "./App.css";
import User from "./components/User";

const App = () => {
  return (
    <div className="App-header">
      <User />
    </div>
  );
};

export default App;

```
- user object တစ်ခုကို App.tsx မှာ သတ်မှတ်ပြီး User component ဆီကို props အနေနဲ့ ထည့်ပေးလိုက်ပါမယ်
```js
// App.tsx

import { useState } from "react";
import "./App.css";
import User from "./components/User";

const App = () => {

const user ={name:"user1", email: "user1@gmail.com", age: 27}

  return (
    <div className="App-header">
      <User ~~user~~ = {user}/>
    </div>
  );
};

export default App;

```
> မှတ်ချက် ။  ။ `~~..~~` သည် error ဖြစ်နေကြောင်း ပြလို၍ ရေးထည့်ထားခြင်းဖြစ်ပြီး code များ ရေးသားသောအခါ ထည့်ပေးရန်မလိုအပ်ပါ။
- user props အောက်မှာ အနီရောင် လေးပေါ်လာတာက error ဖြစ်နေတယ်လို့ ts က သတိပေးနေတာဖြစ်ပါတယ်။
- သဘောက User component ဆီ props တစ်ခု ထည့်ပေးထားတာကို User.tsxမှာ လက်မခံရသေးလို့ဖြစ်ပါတယ်
- ခု User.tsx မှာ props အနေနဲ့ ၀င်လာမယ့် data ကို လက်ခံပါမယ်။
```js
//User.tsx

import React from "react";
import "../App.css";

const User = ({~~user~~}) => {
  return (
    <div>
      <h1>Hello world</h1>
    </div>
  );
};

export default User;
```
- ၀င်လာတဲ့ props ကို လက်ခံလိုက်ပြီးသော်လည်း error ထပ်ပြနေပါတယ်
- ဘာလို့လဲဆိုတော့ props အနေနဲ့ ၀င်လာတဲ့ data ကို type မလုပ်ရသေးလို့ ဖြစ်ပါတယ်
- ဒါကြောင်း props ကို type သတ်မှတ်ပါမယ်
```js
// User.jsx

import React from "react";
import "../App.css";

interface User {
  name: string;
  email: string;
  age: number;
}

interface Props {
  user: User;
}
const User = ({ user }: Props) => {
  return (
    <div>
      <h1>{user.name}</h1>
    </div>
  );
};

export default User;
```
> ရှင်းလင်းချက်
> 
```
interface User {
  name: string;
  email: string;
  age: number;
}
```
- props အနေနဲ့ ၀င်လာမယ့် user object အတွက် type သတ်မှတ်လိုက်ပါတယ်။
- user object ထဲမှာ name က string , email က string , age က number အနေနဲ့ ဖြစ်ပါတယ်လို့ interface တစ်ခု လုပ်လိုက်တာဖြစ်ပါတယ်။
```
interface Props {
  user: User;
}
```
- အဲ့ဒိလုပ်ထားတဲ့ User interface ကို Props ဆိုတဲ့ interface ထဲမှာ user ရဲ့ type အဖြစ် ပြန်ခေါ်သုံးလိုက်တာပါ
```
const User = ({ user }: Props) => {
  return (
    <div>
      <h1>{user.name}</h1>
    </div>
  );
};
```
- ၀င်လာတဲ့ propsကို user အဖြစ်လက်ခံထားပြီး သူ့ရဲ့ type က Props interface ဖြစ်ပါတယ်လို့ type လုပ်လိုက်ပါတယ်
- ပြီးတော့ ၀င်လာတဲ့ props ကို သုံးပြီး user object ထဲက name ကို render လုပ်( UI မှာပြ) ပေးထားတာဖြစ်ပါတယ်

![enter image description here](https://raw.githubusercontent.com/Aungmyanmar32/msquare-m4/main/ep50r2%20%282%29.png)
##
### useState တွေ အသုံးပြုပြီး typescript  နဲ့ ရေးကြည့်ရအောင်
- အရင်ဆုံး allUsers array တစ်ခု လုပ်ပါမယ်
- ပြီးရင် users  state တစ်ခု လုပ်ပြီး ထို state ကို type လုပ်ပါမယ် ။
```js
// App. tsx
import { useState } from "react";
import "./App.css";


interface User {
  name: string;
  email?: string;
  age?: number;
}

const allUsers: User[] = [
  { name: "aung myanmar", email: "user1@gmail.com", age: 30 },
  { name: "msquare", email: "user1@gmail.com", age: 20 },
  { name: "okar", email: "user1@gmail.com", age: 10 },
  { name: "panneiphy", email: "user1@gmail.com", age: 20 },
];

const App = () => {
  const [users, setUsers] = useState<User[]>(allUsers);
  return (
    <div className="App-header">
      <div style={{ marginTop: "20px" }}>
          {users.map((user) => {
            return <div>{user.name}</div>;
          })}
        </div>
    </div>
  );
};

export default App;
```
> ရှင်းလင်းချက်
```
interface User {
  name: string;
  email?: string;
  age?: number;
}

const allUsers: User[] = [
  { name: "aung myanmar", email: "user1@gmail.com", age: 30 },
  { name: "msquare", email: "user1@gmail.com", age: 20 },
  { name: "okar", email: "user1@gmail.com", age: 10 },
  { name: "panneiphy", email: "user1@gmail.com", age: 20 },
];
```
- User interface တစ်ခုလုပ်ထားပြီး allUsers array ရဲ့ type ဟာ User array ဖြစ်ပါတယ်လို့ သတ်မှတ်ထားပါတယ်

```
const [users, setUsers] = useState<User[]>(allUsers);
```
- users state တစ်ခု သတ်မှတ်လိုက်ပြီး users ရဲ့ မူလတန်ဖိုးကို allUsers အဖြစ် သတ်မှတ်ထားပါတယ်
- state ရဲ့ တန်ဖိုးဟာ လည်း User array ပဲ ဖြစ်ကြောင်းကိုလဲ `useState<User[]>` ဆိုပြီး သတ်မှတ်ထားပါတယ်
- state ရဲ့ type ကို သတ်မှတ်တဲ့အခါ `<`  `>` ထဲ ထည့်ပေးပြီး သတ်မှတ်ရပါမယ်
```
 return (
    <div className="App-header">
      <div style={{ marginTop: "20px" }}>
          {users.map((user) => {
            return <div>{user.name}</div>;
          })}
        </div>
    </div>
  );
```
- users state ကို loop လုပ်ပြီး UI မှာ user အားလုံးရဲ့ name တွေ ပြပေးထားပါတယ်

![enter image description here](https://raw.githubusercontent.com/Aungmyanmar32/msquare-m4/main/Screenshot%202023-04-01%20005838.png)
##
### ဆက်ပြီး input တစ်ခု နဲ့ button တစ်ခု လုပ်ကာ user အသစ်တွေ ထည့်ပေါင်းနိုင်အောင် လုပ်ကြပါမယ်
```js
// in App.tsx

const App = () => {
  const [users, setUsers] = useState<User[]>(allUsers);
  
  //get new user name
  const [inputName , setInputName] = useState<string>()

  return (
    <div className="App-header">

      {/* Add input and button tag */}
      <input
          type="text"
          value={inputName}
          onChange={(evt) => setInputName(evt.target.value)}
        />
        <button style={{ marginTop: "10px" }} onClick={handleOnclick}>
          Add user
        </button>


      <div style={{ marginTop: "20px" }}>
          {users.map((user) => {
            return <div>{user.name}</div>;
          })}
        </div>
    </div>
  );
};
```
> ရှင်းလင်းချက်

```
 
  const [inputName , setInputName] = useState<string>()

```
- inputName ဆိုတဲ့ state တစ်ခု လုပ်လိုက်ပြီး string type အနေနဲ့ ပေးထားပါတယ်

```
        <input
          type="text"
          value={inputName}
          onChange={(evt) => setInputName(evt.target.value)}
        />
        
        <button style={{ marginTop: "10px" }} onClick={handleOnclick}>
          Add user
        </button>

```
- Input tag တစ်ခုလုပ်ထားပြီး သူ့အထဲ ရိုက်ထည့်လိုက်တဲ့ text ကို onchage event နဲ့ ဖမ်းပြီး **inputName** ရဲ့ state အဖြစ် update လုပ်ထားပါတယ်
- Input tag ရဲ့ value ကို inputName အဖြစ် သတ်မှတ်ပေးထားပါတယ်
- ခလုတ်တစ်ခုလည်း လုပ်ထားပြီး ထိုခလုတ်ကို နှိပ်လိုက်ချိန်မှာ handleOnclick function ကို ခေါ်ထားပါတယ်
- ခု handleOnclick function ကို သတ်မှတ်ပါမယ်
```js
......
  //get new user name
  const [inputName , setInputName] = useState<string>()

  //handle on click function
  const handleOnclick = () => {
    if (inputName) {

      //create new users array
      const newUsers = [...users, { name: inputName }];

      //update users state
      setUsers(newUsers);

      // update inputName state as empty
      setInputName("");
    }
  };

  return (
    <div className="App-header">
    ........
```
 ` if (inputName) {...code...}`
 - inputName ရဲ့ state က တစ်ခုခုရှိခဲ့ရင် သူ့အထဲက code တွေ run ခိုင်းထားပါတယ်
 ```js
 const newUsers = [...users, { name: inputName }];

setUsers(newUsers);
```
- users ရဲ့ လက်ရှိ state ကို copy လုပ်ပြီး နောက်ထပ် name property တစ်ခုပါတဲ့ object ကို ထပ်ပေါင်းထည့်လိုက်ပြီး array အသစ်အဖြစ် သတ်မှတ်လိုက်ပါတယ်
- ရလာတဲ့ newUsers array အသစ်ကို users ရဲ့ state အဖြစ် update လုပ်လိုက်ပါတယ်
```
setInputName("");
```
- ဒါကတော့ inputName ရဲ့ state ကို empty အဖြစ် update လုပ်လိုက်တာပါ။
- react app မှာ input tag ထဲ name တစ်ခုခုထည့်ပြီး ADD user ခလုတ်ကို  နှိပ်ပေးလိုက်ပါက user name အသစ်တစ်ခုကို render လုပ်ပေးမှာဖြစ်ပါတယ်

![enter image description here](https://raw.githubusercontent.com/Aungmyanmar32/msquare-m4/main/ep50r2%20%283%29.png)

![enter image description here](https://raw.githubusercontent.com/Aungmyanmar32/msquare-m4/main/ep50r2%20%281%29.png)
