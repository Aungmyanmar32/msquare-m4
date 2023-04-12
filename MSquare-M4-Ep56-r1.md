## MSquare Programing Fullstack Course
### Episode-*56* 
### Summary For `Room(1)` intermediate Class
## connect to Postgres database with express server
- express server ကနေ postgres database  ဆီကို ချိတ်ဆက်နိုင်ဖို့ [node postgres PG ](https://www.npmjs.com/package/pg) ဆိုတဲ့ module ကို အသုံးပြုရပါမယ်
- express server ရှိတဲ့ backend folder မှာ pg install လုပ်ပေးပါ။
```properties
npm install pg
```
- install လုပ်ပြီးရင် backend folder အောက်မှာ db ဆိုတဲ့ folder တစ်ခုလုပ်ပါ။
- db folder ထဲမှာ db.ts ဖိုင်တစ်ခု ထပ်လုပ်ပါမယ်။
- ပြီးရင် pg အတွက် type ကို install လုပ်ပေးပါ
```properties
npm i --save-dev @types/pg
```
- db.ts မှာ Pool တစ်ခု လုပ်ပါမယ်။
```js
import { Pool } from "pg";

export const pool = new Pool({
  host: "localhost",
  user: "postgres",
  password: "your-password",
  database: "passport_booking_app",
  max: 20,
  idleTimeoutMillis: 30000,
  connectionTimeoutMillis: 2000,
});
```
- အခု server.ts မှာ အဲ့ဒီ Pool ကို သုံးပြီး database ဆီ connect လုပ်ပါမယ်။
```js
// server.ts
import express from "express";
import cors from "cors";
import { availableSlot, Availability, Slot } from "./data";
import { pool } from "./db/db";

const app = express();
const port = 5000;
app.use(cors());
app.use(express.json());


// connect to db
app.get("/test",async(req,res)=>{
const {rows }= await pool.query('SELECT * FROM bookings')
res.send(rows)
})



app.listen(port, () => {
  console.log(`Server listening on port ${port}!`);
});
```
- အခု server ကို start လုပ်ပြီး postman ကနေ စမ်းကြည့်ပါမယ်။

- Response မှာ database ရှိ booking table ထဲက row တွေ ပြပေးမှာဖြစ်ပါတယ်

![enter image description here](https://raw.githubusercontent.com/Aungmyanmar32/msquare-m4/main/Screenshot%202023-04-12%20115023.png)
##
### Insert to table(db)
```js
// server.ts
import express from "express";
import cors from "cors";
import { availableSlot, Availability, Slot } from "./data";
import { pool } from "./db/db";

const app = express();
const port = 5000;
app.use(cors());
app.use(express.json());


// connect to db
app.get("/test", async (req, res) => {
  // const { rows } = await pool.query("SELECT * from bookings");
  // res.send(rows);

  const text = `INSERT INTO bookings(booking_date,time,user_id) VALUES($1,$2,$3) RETURNING *`;
  const values = ["2023-06-08", 11, 2];
  const { rows } = await pool.query(text, values);
  res.send(rows);
});



app.listen(port, () => {
  console.log(`Server listening on port ${port}!`);
});
```
```
const text =  `INSERT INTO bookings(booking_date,time,user_id) VALUES($1,$2,$3) RETURNING *`;  
const values =  ["2023-06-08",  11,  2];  
const  { rows }  =  await pool.query(text, values);
```
- အစောပိုင်း SELECT ကလို pool,query ကနေ sql command တွေကို တိုက်ရိုက်မရေးပဲ text ထဲမှာ sql ရေး ၊ values ထဲမှာ insert လုပ်ချင်တဲ့ values တွေ ရေးပြီးမှ
-  pool.query(text, values) ဆိုပြီး ခေါ်သုံးလိုက်တာဖြစ်ပါတယ်
- အဲ့ဒါကို **Parameterized SQL queries** လို့ ခေါ်ပါတယ်။
- မသမာသူတွေရဲ့  SQL injection ( hacking) လုပ်ခြင်းကနေ ကာကွယ်ပြီးသား ဖြစ်အောင်လို့ အသုံးပြုလေ့ရှိပါတယ်
- အခု postman ကနေ စမ်းကြည့်ပါက values ထဲက array ကို rowအသစ်အဖြစ် db မှာ သွားထည့်ပေးတာကို တွေ့ရမှာဖြစ်ပါတယ်။

![enter image description here](https://raw.githubusercontent.com/Aungmyanmar32/msquare-m4/main/Screenshot%202023-04-12%20123810.png)

![enter image description here](https://raw.githubusercontent.com/Aungmyanmar32/msquare-m4/main/Screenshot%202023-04-12%20124102.png)
##
### Create postgres database on cloud ( render.com)
- render.com ကို သွားပါ
- github နဲ့ sign in ၀င်ပါ
- NEW + ကို ရွေးပါ

![enter image description here](https://raw.githubusercontent.com/Aungmyanmar32/msquare-m4/main/render_db%20%281%29.png)

- postgres SQL ကို ရွေးပါ


![enter image description here](https://raw.githubusercontent.com/Aungmyanmar32/msquare-m4/main/render_db%20%282%29.png)
- ပုံပါအတိုင်းဖြည့်ပြီး အောက်ကို scroll လုပ်လိုက်ပါ

![enter image description here](https://raw.githubusercontent.com/Aungmyanmar32/msquare-m4/main/render_db%20%283%29.png)
- create database ကို နှိပ်ပေးပါ

![enter image description here](https://raw.githubusercontent.com/Aungmyanmar32/msquare-m4/main/render_db%20%284%29.png)

- status မှာ Creating.. ပြနေတာကို ခနေစာင့်ပါ
- available ပြလာရင် အောက်ကို scroll လုပ်ပေးပါ

![enter image description here](https://raw.githubusercontent.com/Aungmyanmar32/msquare-m4/main/Screenshot%202023-04-12%20131657.png)

- Connection အောက်မှာ database အတွက် အချက်အလက်တွေရလာမှာဖြစ်ပါတယ်
- ခု PgAdmin ကို ဖွင့်ပါ။
- server >> add new server ကို ရွေးပါ
![enter image description here](https://raw.githubusercontent.com/Aungmyanmar32/msquare-m4/main/pgrender%20%281%29.png)
![enter image description here](https://raw.githubusercontent.com/Aungmyanmar32/msquare-m4/main/pgrender%20%282%29.png)
- General tab က name မှာ render db လို့ ထည့်ပါ

![enter image description here](https://raw.githubusercontent.com/Aungmyanmar32/msquare-m4/main/pgrender%20%283%29.png)

- Connection tab အောက်မှာ render ထဲက အချက်အလက်တွေထည့်ပေးရပါမယ်
- Connection tab အောက် က  Hostname နေရာမှာ render က Hostname + **.singapore-postgres.render.com** ဆိုပြီး ထပ်ထည့်ပေးရမှာကို သတိပြုပါ။
- အားလုံးထည့်ပေးပြီးရင် save လုပ်လိုက်ပါက ***render db*** ဆိုတဲ့ database server တစ်ခု ရလာမှာဖြစ်ပါတယ်။

![enter image description here](https://raw.githubusercontent.com/Aungmyanmar32/msquare-m4/main/pgrender%20%284%29.png)
