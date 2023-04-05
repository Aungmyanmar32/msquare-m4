## MSquare Programing Fullstack Course
### Episode-*50* 
### Summary For `Room(1)` intermediate Class
##
### Introducing Database
- database မှာ အဓိကအားဖြင့် SQL database နဲ့ No SQL database ဆိုပြီး နှစ်မျိုးရှိပါတယ် 


![enter image description here](https://raw.githubusercontent.com/Aungmyanmar32/msquare-m4/main/database1.png)

- ခု သင်ခန်းစာမှာတော့ ***Postgresql*** database အကြောင်း လေ့လာသွားပါမယ်
- Postgresql ကို Postgres ( ပို့စ်ဂရက်စ်) လို့လဲ ခေါ်ကြပါတယ်။
- SQL database အမျိုးအစားဖြစ်ပြီး data တွေကို table နဲ့ သိမ်းပေးရမှာ ဖြစ်ပါတယ်။
- Postgres ထဲက data တွေကို SQL language နဲ့ ချိတ်ဆက်အသုံးပြုရမှာဖြစ်ပါတယ်။
##
### Postgres ကို အသုံးပြုနိုင်ရန် မိမိ စက်ထဲမှာ install လုပ်ပေးရပါမယ်
https://www.postgresql.org/download/ မှာ postgres ကို download ရယူနိုင်ပါတယ်
- ရလာတဲ့ postgres ကို install လုပ်ပေးလိုက်ပါက အောက်ကပုံလို ရလာမှာဖြစ်ပါတယ်။

![enter image description here](https://raw.githubusercontent.com/Aungmyanmar32/msquare-m4/main/Screenshot%202023-04-05%20122416.png)
- postgres ကို setup လုပ်ဖို့ windows key ကို နှိပ်ပြီး psql လို့ ရှာလိုက်ပြီး ဖွင့်လိုက်ပါ။
Server [localhost]:
Database [postgres]:
Port [5432]:
Username [postgres]:
- တွေကို enter သာ ခေါက်ပေးလိုက်ပါ။
- password မေးလာတဲ့အခါ install လုပ်တုန်းက ထည့်ခဲ့တဲ့ password ကို ရေးထည့်ပြီး enter ခေါက်ပေးလိုက်ပါ
- password ကို ထည့်တဲ့အခါ terminal မှာ ဘာမှပြပေးမှာ မဟုတ်ပါဘူး။ မှန်အောင်သာရေးပြီး enter ခေါက်လိုက်ပါ။
- အောက်ကပုံလို ပေါ်လာရင် postgres database ထဲ  ရောက်ပါပြီး။

![enter image description here](https://raw.githubusercontent.com/Aungmyanmar32/msquare-m4/main/pgsq%20%284%29.png)
###
## Useful postgres psql command
|        command        |         Usage              | meaing                       |
|----------------|-------------------------------|-----------------------------|
|`\l`|`\l`|List all database            |
|`CREATE DATABASE`|`CREATE DATABASE your_db_name;`|Create new database           |
|`\q`|`\q`|Qiut from current          |
|`\c`|`\c`|show current database            |
|`\c`|`\c your_db_name`|switch and connect to your db           |
|`\dt`|`\dt`|show table details in current db            |
|`CREATE TABLE`|`CREATE TABLE IF NOT EXISTS table_name(table items);`|create table            |
|`DROP DATABASE`|`DROP DATABASE db_name;`|delete database            |
|`INSERT INTO `|`INSERT INTO table_name (items name) VALUE (values);`|Insert row into table           |
|`SELECT *`|`SELECT * FROM table-name;`|show table row           |
##
### postgres မှာ database တစ်ခု တည်ဆောက်ကြည့်ရအောင်
- psql ကို ဖွင့်ပြီး အထက်ပါအတိုင်း ၀င်ထားပါ။
- \c command ကို ရိုက်ထည့်ကြည့်ပါက လက်ရှိရောက်နေတဲ့ db ကို ပြပေးမှာဖြစ်ပါတယ်
```console
postgres=# \c
You are now connected to database "postgres" as user "postgres".
```
- database အသစ်တစ်ခုလုပ်ပါမယ်
```
postgres=# CREATE DATABASE passport_booking_app ;

```
- CREATE DATABASE လို့ပြရင် db အသစ်တစ်ခု လုပ်လို့အဆင်ပြေပါပြီး
- postgres ထဲမှာ database ဘယ်နှစ်ခုရှိလဲ ကြည့်ပါမယ်
```properties
postgres=# \l
                                                                List of databases
   Name    |  Owner   | Encoding |          Collate           |           Ctype            | ICU Locale | Locale Provider |   Access privileges
-----------+----------+----------+----------------------------+----------------------------+------------+-----------------+-----------------------
passport_booking_app  | postgres | UTF8     | English_United States.1252 | English_United States.1252 |            | libc            |
 postgres  | postgres | UTF8     | English_United States.1252 | English_United States.1252 |            | libc            |
 template0 | postgres | UTF8     | English_United States.1252 | English_United States.1252 |            | libc            | =c/postgres          +
           |          |          |                            |                            |            |                 | postgres=CTc/postgres
 template1 | postgres | UTF8     | English_United States.1252 | English_United States.1252 |            | libc            | =c/postgres          +
           |          |          |                            |                            |            |                 | postgres=CTc/postgres
(4 rows)

```
-  default ပါလာတဲ့ **postgres**, **template0** ,**template1** တွေအပြင် ခုနက အသစ်လုပ်ထားတဲ့ ** passport_booking_app ** db ပါ ရှိနေတာကို မြင်ရမှာပါ
-  passport_booking_app db ထဲကို ၀င်ပါမယ်
```properties
postgres=# \c  passport_booking_app 

```

- You are now connected to database " passport_booking_app" as user "postgres".
-  passport_booking_app db ထဲကို ရောက်နေပြီး ဖြစ်ကြောင်း ပြပေးတာကိုပါ မြင်ရမှာဖြစ်ပါတယ်
-   passport_booking_app db ထဲမှာ table တစ်ခု လုပ်ကြည့်ပါမယ်။
```properties
                     
passport_booking_app=# CREATE TABLE IF NOT EXISTS bookings(
passport_booking_app(# id  serial PRIMARY KEY,
passport_booking_app(# booking_date date,
passport_booking_app(# booking_time int);
```
- id ရယ် booking_date ရယ် booking_time ရယ် ပါတဲ့ bookings table တစ်ခု လုပ်လိုက်တာဖြစ်ပါတယ်
-  id ရဲ့ type ကို `serial PRIMARY KEY` , booking_date ရဲ့ type ကို `date` , booking_time ရဲ့ type ကို `int` (integer ) လို့ လုပ်ပေးထားတာဖြစ်ပါတယ်
- CREATE TABLE လို့ ပြလာပါက table လုပ်တာ အောင်မြင်ပါတယ်။
- \dt ကို သုံးပြီး table details ကို ကြည့်ပါမယ်
```properties
passport_booking_app=# \dt

          List of relations
 Schema |   Name   | Type  |  Owner
--------+----------+-------+----------
 public | bookings | table | postgres
(1 row)
```
- ခုဆိုရင် passport_booking_app database ထဲ bookings ဆိုတဲ့ table တစ်ခု create လုပ်လို့ ပြီးပါပြီး။
- အဲ့ဒီ table ထဲကို data row  တစ်ခု ထည့်စမ်းကြည့်ပါမယ်
```properties
passport_booking_app=# INSERT INTO bookings (booking_date,booking_time) VALUES ('2023-03-03',10);
```
- INSERT 0 1 လို့ ပြလာရင် row တစ်ခု ထည့်တာ အဆင်ပြေပါပြီး
- အဲ့ဒီ row ကို ရှိမရှိ ပြန်စစ်ကြည့်ရအောင်
```properties
passport_booking_app=# SELECT * FROM bookings;

 id | booking_date | booking_time
----+--------------+--------------
  1 | 2023-03-03   |           10
(1 row)
```
- ခနက စမ်းထည့်ထားတဲ့ data  row ကို မြင်ရမှာ ဖြစ်ပါတယ်။
- နောက်ထပ် row တစ်ခု ထပ်ထည့်ပါမယ်။
```properties

passport_booking_app=# INSERT INTO bookings (booking_date,booking_time) VALUES ('2023-03-04',12);

INSERT 0 1

passport_booking_app=# SELECT * FROM bookings;

 id | booking_date | booking_time
----+--------------+--------------
  1 | 2023-03-03   |           10
  2 | 2023-03-04   |           12
(2 rows)

```
- ရှိပြီးသားကော အသစ်ထပ်ထည့်လိုက်တဲ့ row ပါ table ထဲ ရှိနေတာကို မြင်ရမှာပါ

##
### Using PgAdmin ( database GUI client)
- windows key ကို နှိပ်ပြီး pgadmin ကိုရှာပြီးဖွင့်ပေးပါ။
-  password တစ်ခုခု ထည့်ပေးလိုက်ပါ။
- server ထဲ၀င်လိုက်ပါ
- password တောင်းလာရင် postgres install လုပ်တုန်းက ထားခဲ့တဲ့ password ကို ထည့်ပေးလိုက်ပါ။
- ဆက်ပြီးတော့ 
 ```
 Databases
   /passport_booking_app
     /Schemas
        /public
          /table
            ထိ ရောက်အောင်သွားပြီ
 table အောက်က bookings ကို R-click လုပ်ပြီး
    View/Edit data >
      All Rows 
      ကို click ပေးလိုက်ပါက
 အထက်မှာ ထည့်တားတဲ့ rows တွေကို မြင်ရမှာဖြစ်ပါတယ်
 
         

```

![enter image description here](https://raw.githubusercontent.com/Aungmyanmar32/msquare-m4/main/pgsq%20%285%29.png)
