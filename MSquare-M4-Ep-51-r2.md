## MSquare Programing Fullstack Course
### Episode-*50* 
### Summary For `Room(2)`
## Using  ***`mui`***  in react app
- mui ဆိုတာက  Material UI ကို အတိုကောက် ခေါ်တာဖြစ်ပြီး
- Material UI ဆိုတာ open-source React component library တစ်ခုဖြစ်ပြီး Google ရဲ့ Material Design ကို အသုံးပြုထားတာဖြစ်ပါတယ်။
- mui ကို သုံးနိုင်ရန် npm နဲ့ project ထဲ install လုပ်ပေးရပါမယ်။

```sh
npm install @mui/material @emotion/react @emotion/styled
```
-  ခု ကျနော်တို့ **mui** autocomplete component တစ်ခု စမ်းသုံးကြည့်ပါမယ်။
```js
// App.tsx

import "./App.css";
import TextField from "@mui/material/TextField";
import { Box, Autocomplete } from "@mui/material";

function App() {
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
          options={~~movies~~}
          sx={{ width: 300 }}
          renderInput={(params) => <TextField {...params} label="Movies" />}
        />
      </Box>
    </Box>
  );
}

export default App;
```
- Box ဆိုတာ mui မှာပါတဲ့ component တစ်ခု ဖြစ်ပြီး html က div တစ်ခုနဲ့ တူပါတယ်
- sx ဆိုတာ mui component တွေကို inline css ရေးလို့ရနိုင်တဲ့ props တစ်ခု ဖြစ်ပါတယ်။
- autocomplete ရဲ့ options မှာ ရွေးပြီး ရှာလို့ရမယ့် data ကို label အနေနဲ့ ပေးရမှာဖြစ်ပါတယ်
- လောလောဆက် movies ဆိုတဲ့ data မရှိသေးတာမလို့ error ပြနေပါမယ်။
> မှတ်ချက် ။   ။ `~~`...`~~` ကို error ဖြစ်နေကြောင်း ပြချင်လို့ ရေးထည့်ထားတာ ဖြစ်ပြီး code  ရေးသားရာတွင် ထည့်ရေးပေးရန်မလိုပါ။

- ခု movies data ကို သတ်မှတ်ပါမယ်
- src folder အောက်မှာ ultis ဆိုတဲ့ folder တစ်ခု ဆောက်ပါ။
- ultis ဆိုတဲ့ folder ထဲမှာ data.ts ဖိုင်တစ်ခုလုပ်ပြီး အောက်ကdata တွေကို ထည့်ပေးပါ။
```js
// data.ts



export const movies = [
  { label: "The Shawshank Redemption", year: 1994 },
  { label: "The Godfather", year: 1972 },
  { label: "The Godfather: Part II", year: 1974 },
  { label: "The Dark Knight", year: 2008 },
  { label: "12 Angry Men", year: 1957 },
  { label: "Schindler's List", year: 1993 },
  { label: "Pulp Fiction", year: 1994 },
 
];

```
- movies  တွေ အတွက် type ကို သတ်မှတ် ပေးပါမယ်။
- react မှာ type တွေအတွက် folder တစ်ခုသတ်မှတ်ပြီး importလုပ်ကာ ခေါ်သုံးလေ့ရှိပါတယ်
- src folder အောက်မှာ typings ဆိုတဲ့ folder တစ်ခု ဆောက်ပါ။
- typings  folder ထဲမှာ types.ts ဖိုင်တစ်ခုလုပ်ပြီး movies data အတွက် type လုပ်ပါမယ်
```js
// types.ts
export interface Movie {
  label: string;
  year: number;
}

```
- movies ထဲမှာ item တစ်ခုကို ကြည့်လိုက်ရင် { label: "The Shawshank Redemption", year: 1994 } ဆိုပြီး ရှိတဲ့ အတွက်   label ကို  string  type, yearကို number type လို့ သတ်မှတ်ပေးပြီး export လုပ်လိုက်ပါတယ်
- data.ts ဖိုင်မှာ import လုပ်ပြီး movies array ကို type လုပ်လိုက်ပါမယ်
```js
// data.ts

import { Movie } from  "../typings/types";

export const movies: Movie[] = [
  { label: "The Shawshank Redemption", year: 1994 },
  { label: "The Godfather", year: 1972 },
  { label: "The Godfather: Part II", year: 1974 },
  { label: "The Dark Knight", year: 2008 },
  { label: "12 Angry Men", year: 1957 },
  { label: "Schindler's List", year: 1993 },
  { label: "Pulp Fiction", year: 1994 },
 
];

```
- ခု App.tsx မှာ movies ကို import လုပ်ပေးလိုက်ရင် ပြနေတဲ့ error ပျောက်သွားမှာ ဖြစ်ပါတယ်။
```
// import at App.tsx

import { movies } from  "./utils/data";
```
- react app ကို start လုပ်ကြည့်ပြီး စမ်းသပ်ကြည့်ပါက autocomplete မှာ movie တွေ ကို ရှာလို့ ရွေးလို့ရမှာ ဖြစ်ပါတယ်။

![enter image description here](https://raw.githubusercontent.com/Aungmyanmar32/msquare-m4/main/ep522%20%281%29.png)
##
- ဆက်ပြီး mui button တစ်ခု သုံးကြည့်ပါမယ်

- < Bu လို့ ရိုက်ထည့်လိုက်တာနဲ့ mui button tag ကို auto suggestion ပြပေးမှာဖြစ်ပြီး ရွေးပေးလိုက်တာနဲ့ button component  ကို auto input  လုပ်ပေးသွားမှာ ဖြစ်ပါတယ်

![enter image description here](https://raw.githubusercontent.com/Aungmyanmar32/msquare-m4/main/ep522%20%282%29.png)
- button ကို click အဖြစ် သတ်မှတ်လိုက်ပြီး click လုပ်တဲ့ အချိန်မှာ hello ဆိုတဲ့ log တစ်ခု ထုတ်ကြည့်ပါမယ်

![enter image description here](https://raw.githubusercontent.com/Aungmyanmar32/msquare-m4/main/ep522%20%284%29.png)

##
- ဆက်ပြီး mui date picker တစ်ခု စမ်းသုံးကြည့်ရအောင်
https://mui.com/x/react-date-pickers/getting-started/#installation ကို သွားကြည့်လိုက်ရင် mui ရဲ့  date picker ကို အသုံးပြု နိုင်ဖို့ လိုအပ်တဲ့ module တွေ ထည့်ပေးရမှာ ဖြစ်ပါတယ်။

```sh
npm install @mui/x-date-pickers
```
```sh
npm install dayjs
```
- လိုအပ်တဲ့  module တွေ ထည့်ပေးပြီးရင် date picker တစ်ခု ထည့်စမ်းကြည့်ပါမယ်။
- App.tsxမှာ အထက်ပါ date picker componentကို ထည့်လိုက်တဲ့အခါ error ပြနေတာကို တွေ့ရမှာပါ။ ဘာလို့လဲ ဆိုတော့ date picker အတွက် လိုအပ်တဲ့ အရာတွေ import မလုပ်ရသေးလို့ ဖြစ်ပါတယ်။

![enter image description here](https://raw.githubusercontent.com/Aungmyanmar32/msquare-m4/main/ep522%20%285%29.png)
- error ပြနေတဲ့ code ကို  mouse ထောက်ကြည့်လိုက်ပါက အောက်နားမှာ Quick fix ဆိုပြီး ပါလာရင် နှိပ်ပေးလိုက်ပါ

![enter image description here](https://raw.githubusercontent.com/Aungmyanmar32/msquare-m4/main/ep522%20%286%29.png)
- ပြလာတဲ့ အထဲက add all missing import ကို ရွေးပေးလိုက်ပါက အဆင်ပြေသွားတာကို  မြင်ရမှာပါ

![enter image description here](https://raw.githubusercontent.com/Aungmyanmar32/msquare-m4/main/ep522%20%287%29.png)

- ခုဆိုရင်  react app မှာ ပေါ်လာတဲ့ Date picker ထဲက ပြက္ခဒိန်ပုံလေးနှိပ်ကြည့်ပါက အခုလို ရက်ရွေးလို့ရမယ့် date picker လေး ပြပေးမှာဖြစ်ပါတယ်။

![enter image description here](https://raw.githubusercontent.com/Aungmyanmar32/msquare-m4/main/ep522%20%288%29.png)
##
- ဆက်ပြီးတော့ Bus station တွေ ရှာရွေးလို့ရမယ့် autocomplete လေးတွေ စမ်းလုပ်ကြည့်ပါမယ်။
- အရင်ဆုံး station array တစ်ခုကို ဆောက်ပါမယ်
```js
// data.ts

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
```
- station array ရဲ့ type ကို station တွေပါတဲ့ array တစ်ခု အဖြစ် type ပေးထားတာမလို့ station type ကို types.tsx မှာ သတ်မှတ်ပြီး export လုပ်ပါမယ်
```js
// types.tsx
export interface Movie {
  label: string;
  year: number;
}

export interface Station {
  id: number;
  label: string;
}

```
- အဲ့ဒီ station interface ကို data.js မှာ import လုပ်ပေးလိုက်ပါမယ်

```js
// data.js

import { Movie, Station } from "../typings/types";


export const movies: Movie[] = [
  { label: "The Shawshank Redemption", year: 1994 },
  { label: "The Godfather", year: 1972 },
  { label: "The Godfather: Part II", year: 1974 },
  { label: "The Dark Knight", year: 2008 },
  { label: "12 Angry Men", year: 1957 },
  { label: "Schindler's List", year: 1993 },
  { label: "Pulp Fiction", year: 1994 },
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
```
- အခု station array ကို အသုံးပြုပြီး mui autocomplete မှာ station ရွေးလို့ရအောင် လုပ်ပါမယ်
ppp
- App.tsx မှာ autocomplete တစ်ခု ထပ်ထည့်လိုက်ပြီး options မှာ movies အစား stations data ကို ထည့်ပေးလိုက်ပါတယ်
- ပထမ autocomplete ကို start station အဖြစ်သတ်မှတ်ပြီး  ဒုတိယ autocomplete ကို End station အဖြစ်သတ်မှတ်လိုက်ပါတယ်
- ခု react app ကို စမ်းသပ်ကြည့်ပါက autocomplete နှစ်ခုမှာ stations တွေရွေးလို့ရမှာဖြစ်ပါတယ်

![enter image description here](https://raw.githubusercontent.com/Aungmyanmar32/msquare-m4/main/ep512%20%281%29.png)
##
- ဆက်ပြီး ရွေးလိုက်တဲ့ station နှစ်ခုကို UI မှာ ပြပေးနိုင်အောင် လုပ်ကြည့်ပါမယ်
- အရင်ဆုံး state တစ်ခု ကို App.tsx မှာ လုပ်ပါမယ်
```js
const [searchStations,setSearchStations]=useState<SearchStaitons> ({startStation:null,endStation:  null})
console.log(searchStations)
```
- searchStations ရဲ့ မူလတန်ဖိုးကို startStation နဲ့ endStation ပါတဲ့ object တစ်ခုအဖြစ်သတ်မှတ်လိုက်ပါတယ်
- အဲ့ဒီ stateရဲ့ type ကိုလည်း `useState<SearchStaitons> ` ဆိုပြီး type လုပ်လိုက်ပါတယ်
- searchStations ရဲ့ တန်ဖိုးကိုလည်း log ထုတ်ကြည့်ထားပါတယ်
- SearchStations type ကို types.tsx မှာ သတ်မှတ်ပေးပြီး App.tsx မှာ import လုပ်ပေးရပါမယ်
```js
// types.tsx

export interface Movie {
  label: string;
  year: number;
}

export interface Station {
  id: number;
  label: string;
}

export interface SearchStaitons {
  startStation: Station | null;
  endStation: Station | null;
}

-------
// App.tsx
import { SearchStaitons } from  "./typings/types";

```
- autocomplete မှာ  တစ်ခုခု ရွေးလိုက်တာနဲ့ state ကို update လုပ်ပြီး ရွေးလိုက်တဲ့ station ကို အရင်သိမ်းပါမယ်။
```js
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
```
- `start station` autocomplete မှာ  **onChange** event ကို ဖမ်းလိုက်ပြီး ရွေးလိုက်တဲ့ value ကို searchStations state ထဲက startStation ရဲ့ တန်ဖိုးအဖြစ် update လုပ်လိုက်တာဖြစ်ပါတယ်
- ဆက်ပြီး `start station` autocomplete မှာလည်း အလားတူ လုပ်ပြီး searchStations state ထဲက endStation ရဲ့ တန်ဖိုးကို ကို update လုပ်ပါမယ်
```js
  <Box sx={{ margin: "0 auto", textAlign: "center" }}>
        <Autocomplete
          disablePortal
          id="movies"
          options={stations}
          onChange={(event, value) =>
            value &&
            setSearchStations({ ...searchStations, endStation: value })
          }
          sx={{ width: 300 }}
          renderInput={(params) => (
            <TextField {...params} label="End Station" />
          )}
        />
      </Box>
```
- ခု ကျနော်တို့  
react app မှာ station တွေ ရွေးစမ်းကြည်ပါက ရွေးလိုက်တဲ့ station ပါတဲ့ object  တစ်ခုလုံးကို CONSOLE မှာ မြင်ရမှာ ဖြစ်ပါတယ်။

![enter image description here](https://raw.githubusercontent.com/Aungmyanmar32/msquare-m4/main/ep512%20%283%29.png)

##
- ဆက်ပြီးရွေးလိုက်တဲ့ stationတွေကို UI မှာ render လုပ်ပြီး ပြကြည့်ပါမယ်
```js
<Box sx={{ margin: "0 auto", mt: 2, textAlign: "center" }}>
        {searchStations.startStation && (
          <h1>{searchStations.startStation.label}</h1>
        )}
        {searchStations.endStation && (
          <h1>{searchStations.endStation.label}</h1>
        )}
      </Box>
```
>ရှင်းလင်းချက်
```
 {searchStations.startStation && (
          <h1>{searchStations.startStation.label}</h1>
        )}
```
- အကယ်လို့ searchStations.startStation က null မဟုတ်ခဲ့ရင် ( true) ဖြစ်ခဲ့ရင် ရွေးလိုက်တဲ့ start station ကို UI မှာ ပြခိုင်းလိုက်တာဖြစ်ပါတယ်
```
 {searchStations.endStation && (
          <h1>{searchStations.endStation.label}</h1>
        )}
```
- အကယ်လို့ searchStations.startStation က null မဟုတ်ခဲ့ရင် ( true) ဖြစ်ခဲ့ရင် ရွေးလိုက်တဲ့ end station ကို UI မှာ ပြခိုင်းလိုက်တာဖြစ်ပါတယ်
-  ခု ကျနော်တို့  
react app မှာ station တွေ ရွေးစမ်းကြည်ပါက ရွေးလိုက်တဲ့ station တွေကို  မြင်ရမှာ ဖြစ်ပါတယ်။
![enter image description here](https://raw.githubusercontent.com/Aungmyanmar32/msquare-m4/main/Screenshot%202023-04-02%20144229.png)
