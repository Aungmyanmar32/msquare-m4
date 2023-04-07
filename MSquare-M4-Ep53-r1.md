## MSquare Programing Fullstack Course
### Episode-*50* 
### Summary For `Room(1)` intermediate Class
## Postgres
### delete database
- postgres မှာ database ကို ဖျက်ချင်ရင် drop ကို အသုံးပြုရပါမယ်။
```properties

postgres-# \l
                                                                      List of databases
         Name         |  Owner   | Encoding |          Collate           |           Ctype            | ICU Locale | Locale Provider |   Access privileges
----------------------+----------+----------+----------------------------+----------------------------+------------+-----------------+-----------------------
 passport_booking_app | postgres | UTF8     | English_United States.1252 | English_United States.1252 |            | libc            |
 postgres             | postgres | UTF8     | English_United States.1252 | English_United States.1252 |            | libc            |
 template0            | postgres | UTF8     | English_United States.1252 | English_United States.1252 |            | libc            | =c/postgres          +
                      |          |          |                            |                            |            |                 | postgres=CTc/postgres
 template1            | postgres | UTF8     | English_United States.1252 | English_United States.1252 |            | libc            | =c/postgres          +
                      |          |          |                            |                            |            |                 | postgres=CTc/postgres
(4 rows)

postgres=# DROP DATABASE passport_booking_app;
DROP DATABASE
postgres=# \l
                                                                List of databases
   Name    |  Owner   | Encoding |          Collate           |           Ctype            | ICU Locale | Locale Provider |   Access privileges
-----------+----------+----------+----------------------------+----------------------------+------------+-----------------+-----------------------
 postgres  | postgres | UTF8     | English_United States.1252 | English_United States.1252 |            | libc            |
 template0 | postgres | UTF8     | English_United States.1252 | English_United States.1252 |            | libc            | =c/postgres          +
           |          |          |                            |                            |            |                 | postgres=CTc/postgres
 template1 | postgres | UTF8     | English_United States.1252 | English_United States.1252 |            | libc            | =c/postgres          +
           |          |          |                            |                            |            |                 | postgres=CTc/postgres
(3 rows)
```

- psql ကိုဖွင့်ပြီး \l လို့ list လုပ်ကြည့်ချိန်မှာ database လေးခု ရှိတာကို တွေ့ရမှာပါ။
- အဲ့ဒီထဲကမှ passport_booking_app ဆိုတဲ့ database ကို DROP DATABASE နဲ့ ဖျက်ထုတ်လိုက်ပါတယ်
- ပြန်ပြီး list လုပ်ကြည့်ချိန်မှာ  passport_booking_app ဆိုတဲ့ database မရှိတော့တာကို မြင်ရမှာပါ။
##
### Connecting tables in postgres database
- SQL database တွေဟာ relational database အမျိုးအစားတွေ ဖြစ်ကြပါတယ်
-  SQL database ထဲရှိ table တွေဟာ တစ်ခုနဲ့ တစ်ခု ချိတ်ဆက်ပြီး အသုံးပြုလို့ ရပါတယ်
### why relation?
- SQL မှာ dataတွေကို table နဲ့ သိမ်းလေ့ရှိပါတယ်
- တကယ်လို့ data တွေကို table တစ်ခုထဲ စုပြီး သိမ်းထားမယ်ဆိုရင် 
  - data တွေ ထပ်လာမျိုး ရှိလာပါမယ် ( data duplicate)
  - အဲ့ဒီ table ထဲက data တစ်ခုခုရှာမယ်ဆို သိမ်းထားတာ တွေ များနေတာမလို့ အချိန်ကြာပါမယ်။
  - မလိုအပ်ပဲ resource တွေ အများကြီး သုံးရပါမယ်
- ဒါကြောင့်မလို့ SQL မှာ table တွေ အများကြီး လုပ်ပြီး တစ်ခုနဲ့ တစ်ခု ချိတ်ဆက်ပြီး သုံးလေ့ရှိပါတယ်။

##
### *primary key*(PK) and *foreign key*(FK) in postgresql
- table တစ်ခု ကို နောက် table တစ်ခုနဲ့ ချိတ်ဆက်သုံးတဲ့ အခါ *foreign key* အနေနဲ့ ချိတ်ဆက်ပေးလေ့ရှိပါတယ်။
### နမူနာ
![enter image description here](https://res.cloudinary.com/practicaldev/image/fetch/s--UlPvjfOb--/c_limit,f_auto,fl_progressive,q_auto,w_880/https://i.postimg.cc/cHDd4FyP/one-to-many-erd-generic.png)
- parent table ကို child table နဲ့ ချိတ်ဆက်လိုတဲ့အခါ parent ရဲ့  id ( PK ) ကို child table ထဲမှာ ( FK ) အနေနဲ့ column တစ်ခု ထည့်ပြီး ချိတ်ဆက်ပေးရပါမယ်။
- အဲ့ဒီ သီအိုရီကို စမ်းသုံးကြည့်ပြီး table တွေကို relation လုပ်ကြည့်ကြပါမယ်။
##

- သင်ခန်းစာ အစောပိုင်းမှာ passport_booking_app DB ကို ဖျက်ကြည့်ထားတာမလို့ database အသစ်တစ်ခုပြန်လုပ်ပြီး အဲ့ဒီ db အသစ်ထဲ ၀င်ထားပါမယ်
```properties
postgres=# \c
You are now connected to database "postgres" as user "postgres".

postgres=# CREATE DATABASE passport_booking_app;
CREATE DATABASE

postgres=# \c passport_booking_app
You are now connected to database "passport_booking_app" as user "postgres".

```
- passport_booking_app db ထဲ table တစ်ခု create လုပ်ပါမယ်
```properties
You are now connected to database "passport_booking_app" as user "postgres".
passport_booking_app=# CREATE TABLE IF NOT EXISTS users (
passport_booking_app(# id serial primary key,
passport_booking_app(# email text not null,
passport_booking_app(# nrc_number text not null,
passport_booking_app(# date_of_birth text not null,
passport_booking_app(# city text);

```
- CREATE TABLE လို့ ပြပေးရင် users table တစ်ခု လုပ်ပြီးပါပြီး
- \dt နဲ့ ပြန်စစ်ကြည့်ပါမယ်
```properties
passport_booking_app=# \dt

         List of relations
 Schema | Name  | Type  |  Owner
--------+-------+-------+----------
 public | users | table | postgres
(1 row)
```
- ဆက်ပြီး bookings table တစ်ခု ထပ်လုပ်ပါမယ်
- အဲ့ဒီ bookings tableကို ( PK , FK ) ကိုသုံးပြီး users table နဲ့ relation လုပ်ပါမယ်။
```properties
passport_booking_app=# CREATE TABLE bookings (
passport_booking_app(# id serial primary key,
passport_booking_app(# booking_date date not null,
passport_booking_app(# time integer not null,
passport_booking_app(# user_id integer references users);
```
- `user_id integer references users` ဆိုတာ FK အနေနဲ့ users table ထဲက id ကို references လုပ်ပြီး  FK အနေနဲ့ ထည့်ပေးထားတာဖြစ်ပါတယ်
- \d နဲ့ စစ်ကြည့်ပါက tableလေးခုရှိလာတာကို မြင်ရမှာ ပါ။
```properties

passport_booking_app=# \d

               List of relations
 Schema |      Name       |   Type   |  Owner
--------+-----------------+----------+----------
 public | bookings        | table    | postgres
 public | bookings_id_seq | sequence | postgres
 public | users           | table    | postgres
 public | users_id_seq    | sequence | postgres
(4 rows)
```
-  users_id_seq  ,bookings_id_seq က postgres က auto လုပ်ပေးလိုက်တာဖြစ်ပါတယ်
- \d+ ကို သုံးပြီး table တွေထဲ က cloumn ကို ကြည့်လို့ရပါတယ်
```properties

passport_booking_app=# \d+ bookings
                                                          Table "public.bookings"
    Column    |  Type   | Collation | Nullable |               Default                | Storage | Compression | Stats target | Description
--------------+---------+-----------+----------+--------------------------------------+---------+-------------+--------------+-------------
 id           | integer |           | not null | nextval('bookings_id_seq'::regclass) | plain   |             |              |
 booking_date | date    |           | not null |                                      | plain   |             |              |
 time         | integer |           | not null |                                      | plain   |             |              |
 user_id      | integer |           |          |                                      | plain   |             |              |
Indexes:
    "bookings_pkey" PRIMARY KEY, btree (id)
Foreign-key constraints:
    "bookings_user_id_fkey" FOREIGN KEY (user_id) REFERENCES users(id)
Access method: heap

```
- ဆက်ပြီး table တွေထဲကို rows ( data) တွေ ထည့်ပေးပါမယ်။
```properties
                         
passport_booking_app=# insert into users (email,nrc_number,date_of_birth,city) values ('msquare@gmail.com', 'mkn009','01-01-2000','yangon');

```
- ခု table ထဲ ဘာတွေရှိလဲ စစ်ကြည့်ပါက
```properties
passport_booking_app=# select * from users;
 id |       email       | nrc_number | date_of_birth |  city
----+-------------------+------------+---------------+--------
  1 | msquare@gmail.com | mkn009     | 01-01-2000    | yangon
(1 row)
```
- ခုနက ထည့်လိုက်တဲ့ row ကို မြင်ရမှာဖြစ်ပါတယ်
- ဆက်ပြီး data row တစ်ခု ထပ်ထည့်ပါမယ်
```properties
      
passport_booking_app=# insert into users (email,nrc_number,date_of_birth,city) values
passport_booking_app-# ('aung@gmail.com',
passport_booking_app(# 'mon001',
passport_booking_app(# '02-02-2000',
passport_booking_app(# 'mawlamyine');
```
- select နဲ့ ထပ်စစ်ကြည့်ပါက အောက်ပါအတိုင်း မြင်ရမှာပါ။
```properties
passport_booking_app=# select * from users;

 id |       email       | nrc_number | date_of_birth |    city
----+-------------------+------------+---------------+------------
  1 | msquare@gmail.com | mkn009     | 01-01-2000    | yangon
  2 | aung@gmail.com    | mon001     | 02-02-2000    | mawlamyine
(2 rows)
```
 ##
 - ဆက်ပြီး bookings table ထဲမှာ data တွေ ထည့်ပါမယ်။
 ```properties
 passport_booking_app=# insert into bookings (booking_date,time,user_id) values (CURRENT_DATE,10,1);
```
- user_id နေရာမှာ ထည့်လိုက်တဲ့  1 ဆိုတာ  FK ဖြစ်ပြီး users table ထဲက id 1ဖြစ်တဲ့   | msquare@gmail.com | mkn009     | 01-01-2000    | yangon နဲ့ ချိတ်ဆက်လိုက်တာဖြစ်ပါတယ်
-  ခု bookings table ထဲ ထည့်လိုက်တဲ့ booking data ( row) ဟာ user table ထဲက id 1 ဖြစ်တဲ့ user  ရဲ့  booking info ဖြစ်ပါတယ်လို့ ဆိုလိုတာပါ။
- user table ထဲမှာ user နှစ်ဦး ရှိတာမလို့ နောက် user ( id 2) အတွက် booking info ကို ထည့်ပါမယ်
```properties
passport_booking_app=# insert into bookings (booking_date,time,user_id) values (CURRENT_DATE,13,2);
```
- bookings table ထဲ ဘာတွေ ရှိနေပြီးလဲ စစ်ကြည့်တဲ့အခါ အောက်ပါအတိုင်းမြင်ရမှာဖြစ်ပါတယ်။
```properties
INSERT 0 1
passport_booking_app=# select * from bookings;

 id | booking_date | time | user_id
----+--------------+------+---------
  1 | 2023-04-07   |   10 |       1
  2 | 2023-04-07   |   13 |       2
(2 rows)
```
