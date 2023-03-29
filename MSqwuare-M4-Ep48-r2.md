## MSquare Programing Fullstack Course
### Episode-*48* 
### Summary For `Room(2)` 
##
### State in React
- state ဆိုတာ react component တစ်ခုရဲ့ လက်ရှိအခြေအနေ ကို ဆိုလိုတာဖြစ်ပါတယ်။
- react ကို functional component နဲ့ ရေးတဲ့အခါ state တွေ သုံးလို့ရအောင် hook တွေနဲ့ ချိတ်ပေးရပါတယ်။
- react hook  ဆိုတာကလည်း function တစ်မျိုးလို့ သတ်မှတ်နိုင်ပါတယ်။
##
### useState hook
syntax
`const [ state , set-state-function] = useState(initialState) `
- **state** ဆိုတဲ့ နေရာမှာ useState ရဲ့ နောက် **(initialState )  ထဲက တန်ဖိုး** ၀င်လာမှာ ဖြစ်ပြီး၊
- **set-function** ကတော့  useState ရဲ့ နောက် **( initialState)  ထဲက တန်ဖိုးကို updateလုပ်တဲ့ function** လို့ အကြမ်းဖျင်းမှတ်သားထားပါ။
##
### Autocomplete with useState hook
- အရင်ဆုံး allUser array တစ်ခု သတ်မှတ်ပါမယ်
```js
//App.jsx
const allUser= [
  {id:1 , name: "aung myanmar", email: "aung@gmial.com"},
  {id:2 , name: "hsu thel mwe", email: "hsu@gmial.com"},
  {id:3 , name: "chan myae", email: "chan@gmial.com"},
  {id:4 , name: "okar phyo", email: "okar@gmial.com"},
]
```
-ပြီးရင် users ဆိုတဲ့ state တစ်ခုကို useState သုံးပြီးသတ်မှတ်ပါမယ်။
- users ရဲ့ မူလ state ကို allUser array အဖြစ် ထားလိုက်ပါမယ်
```js
const [users, setUsers] = useState(allUser);
```
- users ကို အသုံးပြုပြီး UI မှာ user အားလုံးရဲ့ name တွေ ပြပါမယ်

```js
const [users, setUsers] = useState(allUser);

  return (
    <div>
      {users.map((user) => {
        return (
          <ul>
            <li>{user.name}</li>
          </ul>
        );
      })}
    </div>

```
- users က array တစ်ခု ဖြစ်တာမလို့ map လုပ်ပြီး name တွေကို ပြလိုက်တာဖြစ်ပါတယ်။
- ဆက်ပြီး input tag တစ်ခု ထပ်လုပ်ပါမယ်။
- input ထဲမှတစ်ဆင့် ထည့်လိုက်တဲ့ textကို အသုံးပြုပြီး allUsers name တွေနဲ့ တူမတူ စစ်ကြည့်ပါမယ်။
- တူတဲ့ name ရှိခဲ့ရင် UI မှာ ရှိသမျှ name တွေ မပြတော့ပဲ စစ်ထုတ်လိုက်တဲ့ user name ပဲ ပြပေးမှာဖြစ်ပါတယ်

```js
return (
    <div>
      <input
        type="text"
        onChange={(e) => {
          const inputText = e.target.value;
          const filteredUsers = users.filter((user) =>
            user.name.includes(inputText)
          );
          setUsers(filteredUsers);
        }}
      />
      {users.map((user) => {
        return (
          <ul>
            <li>{user.name}</li>
          </ul>
        );
      })}
    </div>
  );
```
> ရှင်းလင်းချက်

    
    <input
           type="text"
           onChange={(e) => {
             const inputText = e.target.value;
             const filteredUsers = users.filter((user) =>
               user.name.includes(inputText)
              );
             setUsers(filteredUsers);
            }}
          />
          

  

- input tag တစ်ခု လုပ်လိုက်ပြီး 
   - onchange event မှာ ရိုက်ထည့်လိုက်တဲ့ text နဲ့
    - users ထဲက name စာလုံးနဲ့ တူမတူ ( ပါ မပါ) စစ် လိုက်ပြီး
    - တူတဲ့ဟာ ရှိခဲ့ရင် users ရဲ့ state ကို update လုပ်လိုက်တာဖြစ်ပါတယ်။

- အခုဆိုရင် input ထဲမှာ aung လို့ ရိုက်ထည့်ကြည့်ပါက အောက်ပါအတိုင်း aung myanmar ကိုပဲ ပြပေးမှာ ဖြစ်ပါတယ်။

![enter image description here](https://raw.githubusercontent.com/Aungmyanmar32/msquare-m4/main/Screenshot%202023-03-29%20104546.png)
- ဒါပေမယ့် aung ကို ပြန်ဖျက်ပြီး hsu လို့ထပ်ရှာကြည့်တဲ့ အခါ ရှာလို့ မတွေ့တော့ကို မြင်ရမှာပါ
   - users ရဲ့ state က input မှာ aung လို့ ထည့်လိုက်တဲ့ အချိန်မှာ update ဖြစ်သွားပြီး 
   - မူလ state ဖြစ်တဲ့ users အားလုံးပါတဲ့ allUser array ကနေ filter စစ်ထုတ်လိုက်တဲ့ aung ဆိုတဲ့ name ပါတဲ့ object တစ်ခုပဲ ပါတဲ့ array အဖြစ်သို့ update ဖြစ်သွားပါတယ်။
  
```js
//initial users  state
[
  {id:1 , name: "aung myanmar", email: "aung@gmial.com"},
  {id:2 , name: "hsu thel mwe", email: "hsu@gmial.com"},
  {id:3 , name: "chan myae", email: "chan@gmial.com"},
  {id:4 , name: "okar phyo", email: "okar@gmial.com"},
]

//Update users state
[
{id:1 , name: "aung myanmar", email: "aung@gmial.com"}
]
```
- input မှာ နောက်တစ်ခါ ထပ်ရှာတဲ့ အခါ ရိုက်ထည့်လိုက်တဲ့ text ကို users မှာပဲ ထပ် filter လုပ်တဲ့ အခါ user တစ်ယောက်ပဲ ရှိတာမလို့ ရှာမတွေ့တော့ တာဖြစ်ပါတယ်။
- အဲ့ဒီ errorကို ဖြေရှင်းဖို့ filter လုပ်တဲ့ အခါ users ကို မသုံးတော့ပဲ allUser array ကို တိုက်ရိုက်သုံးပေးလိုက်ပါ။
```js
//App.js
import { useState } from "react";
import User from "./components/User";

const allUser = [
  { id: 1, name: "aung myanmar", email: "aung@gmial.com" },
  { id: 2, name: "hsu thel mwe", email: "hsu@gmial.com" },
  { id: 3, name: "chan myae", email: "chan@gmial.com" },
  { id: 4, name: "okar phyo", email: "okar@gmial.com" },
];

const App = () => {
  const [users, setUsers] = useState(allUser);

  return (
    <div>
      <input
        type="text"
        onChange={(e) => {
          const inputText = e.target.value;
          const filteredUsers = allUser.filter((user) =>
            user.name.includes(inputText)
          );
          setUsers(filteredUsers);
        }}
      />
      {users.map((user) => {
        return (
          <ul>
            <li>{user.name}</li>
          </ul>
        );
      })}
    </div>
  );
};

export default App;
```
- ခု react app ကို ထပ်စမ်းသပ်ကြည့်ပါက စောစောကလို error မဖြစ်တော့ပဲ အဆင်ပြေပြေရှာလို့ ရသွားမှာဖြစ်ပါတယ်။
