## MSquare Programing Fullstack Course
### Episode-*49* 
### Summary For `Room(2)`
## Change Object property's value in react

- ရိုးရိုး JS မှာ Objectထဲ က property တစ်ခုခုရဲ့ value ကို ပြောင်းချင်ရင် property key ကို ‌ခေါ်ပြီး ပြောင်းပေးလိုက်လို့ ရပါတယ်
   - နမူနာ
   ```js
   const user = {name : "aung", age: 29}
   user.name = "John"
   console.log( user) // {name : "John", age: 29}
   ```

- react မှာ Objectထဲ က property တစ်ခုခုရဲ့ value ကို ပြောင်းချင်ရင် ရိုးရိုး JS မှာလို ပြောင်းလိုက်လို့ရှိရင် error ဖြစ်သွားနိုင်ပါတယ်
- အထူးသဖြင့် state နဲ့ update လုပ်တဲ့ အခါကျရင် မူလ object ထဲက properties တွေ မပါလာတော့ တာမျိုး / property တစ်ခုခုရဲ့ value ကို ပြောင်းလိုက်ပေမယ့်လဲ နဂိုအတိုင်းပဲ မပြောင်းပဲ update မဖြစ်သွားတာမျိုး ဖြစ်လာနိုင်ပါတယ်။
- react မှာ Objectထဲ က property တစ်ခုခုရဲ့ value ကို ပြောင်းချင်ရင် အရင် object ကို copy အရင် လုပ်ပြီးမှ ပြောင်းပေးရပါမယ်
   - နမူနာ
 ```js
const [user,setUser]= useState({name:"aung", age :  30})

setUser({...user, name :  "John"})

console.log(user)//{name : "John", age: 30}
```
- useState နဲ့ user ဆိုတဲ့ state ရဲ့ မူလတန်ဖိုးကို {name:"aung", age :  30} လို့ ပေးထားပါတယ်
- user ထဲက name ကို ပဲ ပြင်ပြီး update လုပ်ချင်တာမလို့ setUser function ကို ခေါ််ပါတယ်။
- parameter  ထဲမှာ အရင်ဆုံး မူလတန်ဖိုးဖြစ်တဲ့ object ကို copy လုပ်ပြီးမှ ပြင်ချင်တဲ့ property ရဲ့ key ကို ယူပြီး value အသစ်ထည့် ပြီး update လုပ်လိုက်တာဖြစ်ပါတယ်။
##
- အခု App.js မှာ state တစ်ခုသတ်မှတ်ပြီး UI မှာ ပြကြည့်ကြပါမယ်
```js
const App = () => {
  const [buss, setBuss] = useState({
    name: "Line 30",
    startStation: "Hle Dan",
    endStation: "Tamwe",
    stations: ["Hle Dan", "Myaynigone", "Mayangone", "Tamwe"],
  });
  return (
    <div
      className="App"
      style={{
        width: "100%",
        textAlign: "center",
        display: "flex",
        justifyContent: "center",
      }}
    >
      <header className="App-header">
        
        <ul>
          <li> Bus Name : {buss.name}</li>
          <li>Start Station : {buss.startStation}</li>
          <li>End Station : {buss.endStation}</li>
          <h2>All station</h2>
          {buss.stations.map((station) => {
            return <li key={station}>{station}</li>;
          })}
        </ul>
      </header>
    </div>
  );
};

export default App;

```

> ရှင်းလင်းချက်

```js
const [buss, setBuss] = useState({
    name: "Line 30",
    startStation: "Hle Dan",
    endStation: "Tamwe",
    stations: ["Hle Dan", "Myaynigone", "Mayangone", "Tamwe"],
  });
```
- buss ဆိုတဲ့ state တစ်ခု သတ်မှတ်ထားပါတယ်
- သူ့ရဲ့ မူလတန်ဖိုး အဖြစ် object တစ်ခု ထည့်ပေးထားပါတယ်
```js
       <ul>
          <li> Bus Name : {buss.name}</li>
          <li>Start Station : {buss.startStation}</li>
          <li>End Station : {buss.endStation}</li>
          <h2>All station</h2>
          {buss.stations.map((station) => {
            return <li key={station}>{station}</li>;
          })}
        </ul>
```
- return ထဲမှာ buss ထဲမှာ ရှိတဲ့ properties တွေအကုန် UI မှာ ပြပေးထားပါတယ်
- buss ထဲမှာ ပါတဲ့ stations ရဲ့ တန်ဖိုးဟာ array တစ်ခု ဖြစ်နေတာမလို့ loop လုပ်ပြီး station တစ်ခုချင်းစီးကို ပြပေးနိုင်အောင် ရေးထားပါတယ်
- react app ကို start လုပ်ကြည့်လိုက်တဲ့ အခါ အောက်ပါအတိုင်းမြင်ရမှာဖြစ်ပါတယ်။

![enter image description here](https://raw.githubusercontent.com/Aungmyanmar32/msquare-m4/main/Screenshot%202023-03-30%20114117.png)
##

### ဆက်ပြီးတော့ buss ထဲက name ကို line 40 လို့ ပြောင်းပြီး UI မှာ ပြပေးနိုင်အောင် လုပ်ကြရအောင်
- အဲ့လိုဆိုရင် သင်ခန်းစာ အစ မှာ ပြောပြခဲ့တဲ့ method ကို အသုံးပြုရမှာပါ။
- အရင်ဆုံး return မှာ button တစ်ခု ထည့်ပါမယ်
- button ကို နှိပ်လိုက်တဲ့အချိန်မှာ state ကို update လုပ်တဲ့ function ကို ခေါ်လိုက်ပါမယ်
```js
const App = () => {
  const [buss, setBuss] = useState({
    name: "Line 30",
    startStation: "Hle Dan",
    endStation: "Tamwe",
    stations: ["Hle Dan", "Myaynigone", "Mayangone", "Tamwe"],
  });
  return (
    <div
      className="App"
      style={{
        width: "100%",
        textAlign: "center",
        display: "flex",
        justifyContent: "center",
      }}
    >
      <header className="App-header">
        <button
          onClick={() => {
            setBuss({ ...buss, name: "Line 40"});
          }}
        >
          Change buss name
        </button>
    
        <ul>
          <li> Bus Name : {buss.name}</li>
          <li>Start Station : {buss.startStation}</li>
          <li>End Station : {buss.endStation}</li>
          <h2>All station</h2>
          {buss.stations.map((station) => {
            return <li key={station}>{station}</li>;
          })}
        </ul>
      </header>
    </div>
  );
};

export default App;
```

> ရှင်းလင်းချက်

```js
   <button onClick={() => setBuss({ ...buss, name: "Line 40"});}>
     Change buss name
   </button>
```
- button ကို နှိပ်လိုက်တဲ့အချိန်မှာ မူလတန်ဖိုးဖြစ်တဲ့ object ကို copy လုပ်ပြီးမှ ပြင်ချင်တဲ့ property ရဲ့ key ကို ယူပြီး value အသစ်ထည့် ပြီး update လုပ်လိုက်တာဖြစ်ပါတယ်။
- Change bus name ခလုတ်ကို နှိပ်ကြည့်ပါက line 40 သို့ ပြောင်းသွားတာ မြင်ရမှာပါ
![enter image description here](https://raw.githubusercontent.com/Aungmyanmar32/msquare-m4/main/Screenshot%202023-03-30%20141232.png)
