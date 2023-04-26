## MSquare Programing Fullstack Course
### Episode-*58* 
### Summary For `Room(1)` intermediate Class
##
### Create db for POS app
- အရင်နေ့သင်ခန်းစာက modeling လုပ်ခဲ့တဲ့ table တွေကို database မှာ create လုပ်ပါမယ်။

- pgAdmin ကို ဖွင့်ပြီး database အသစ်တစ်ခု လုပ်ပါမယ်

![enter image description here](https://raw.githubusercontent.com/Aungmyanmar32/msquare-m4/main/hpos1%20%281%29.png)
- schemas ကို ၀င်ပြီး table ကို create လုပ်ပါမယ်

![enter image description here](https://raw.githubusercontent.com/Aungmyanmar32/msquare-m4/main/hpos1%20%282%29.png)
- table name ကို ထည့်ပေးလိုက်ပြီး columns တွေ ထပ်ပေါင်းထည့်ပါမယ်။

![enter image description here](https://raw.githubusercontent.com/Aungmyanmar32/msquare-m4/main/hpos1%20%283%29.png)
![enter image description here](https://raw.githubusercontent.com/Aungmyanmar32/msquare-m4/main/hpos1%20%284%29.png)
![enter image description here](https://raw.githubusercontent.com/Aungmyanmar32/msquare-m4/main/hpos1%20%285%29.png)
- ပြီးရင် save လိုက်ပြီး menus table ကို R-click နှိပ်ကာ view all row ကို ဖွင့်လိုက်ပါက အခုလို ပြပေးမှာဖြစ်ပါတယ်

![enter image description here](https://raw.githubusercontent.com/Aungmyanmar32/msquare-m4/main/hpos1%20%286%29.png)
- ခု GUI နဲ့ table တစ်ခု create လုပ်လိုက်တာဖြစ်ပြီး နောက်ထပ် table တစ်ခုကို sql နဲ့ create လုပ်ကြည့်မှာ ဖြစ်ပါတယ်။

![enter image description here](https://raw.githubusercontent.com/Aungmyanmar32/msquare-m4/main/hpos1%20%287%29.png)
- menus table နဲ့ menu_categories table မှာ row ( data ) တွေ ထည့်ပါမယ်။

![enter image description here](https://raw.githubusercontent.com/Aungmyanmar32/msquare-m4/main/hpos1%20%288%29.png)

![enter image description here](https://raw.githubusercontent.com/Aungmyanmar32/msquare-m4/main/hpos1%20%289%29.png)

![enter image description here](https://raw.githubusercontent.com/Aungmyanmar32/msquare-m4/main/hpos1%20%2810%29.png)

![enter image description here](https://raw.githubusercontent.com/Aungmyanmar32/msquare-m4/main/hpos1%20%2811%29.png)
- ခု ဆက်ပြီး menus table နဲ့ menu_categories table ကို join မယ့် table ကို ဆက်လုပ်ပါမယ်။

![enter image description here](https://raw.githubusercontent.com/Aungmyanmar32/msquare-m4/main/hpos1%20%2812%29.png)

- join table ထဲမှာ data တွေကို ဆက်ထည့်ပါမယ်။

![enter image description here](https://raw.githubusercontent.com/Aungmyanmar32/msquare-m4/main/hpos1%20%2813%29.png)

![enter image description here](https://raw.githubusercontent.com/Aungmyanmar32/msquare-m4/main/hpos1%20%2814%29.png)
- menus table ထဲက mont Hin  khar ရဲ့ id ကို menu_categories table ထဲက most popular id နဲ့ hot dish id ကို Join လိုက်တာဖြစ်ပါတယ်။

![enter image description here](https://raw.githubusercontent.com/Aungmyanmar32/msquare-m4/main/hpos1%20%2815%29.png)
- ခု inner join ကို သုံးပြီး menus name နဲ့ menu_categories name ကို ထုတ်ကြည့်ပါမယ်.
![enter image description here](https://raw.githubusercontent.com/Aungmyanmar32/msquare-m4/main/hpos1%20%2816%29.png)

##
- နောက်ထပ် addons နဲ့ addon_categories table တွေ ထပ်လုပ်ပါမယ်။
- addons table မှာ 
   - id
   - name
   - price
   - is_available
   
  ဆိုတဲ့ column တွေ ပါပါမယ်။
- addon_categories table မှာတော့
  - id
  - name
  - is_require
ဆိုတဲ့ column တွေ ပါပါမယ်။
### addons
![enter image description here](https://raw.githubusercontent.com/Aungmyanmar32/msquare-m4/main/hpos1%20%2817%29.png)
   
   ###  addon_categories![enter image description here](https://raw.githubusercontent.com/Aungmyanmar32/msquare-m4/main/hpos1%20%2818%29.png)
- ဆက်ပြီး addon တွေကို addon categories တွေနဲ့ ချိတ်ဆက်ဖို့ လုပ်ပါမယ်။
- addon က menu လို categories နှစ်ခု သုံးခု join စရာမလိုပဲ one to one ပဲ join ရမှာ မလို့  addons table မှာ relation column ( FK ) တစ်ခု ထပ်ထည့်လိုက်ပါမယ်။

![enter image description here](https://raw.githubusercontent.com/Aungmyanmar32/msquare-m4/main/hpos1%20%2819%29.png)
- ဒါဆိုရင်addons table မှာ column တစ်ခု ထပ်တိုးလာတာကို မြင်ရမှာပါ။

![enter image description here](https://raw.githubusercontent.com/Aungmyanmar32/msquare-m4/main/hpos1%20%2820%29.png)
##
- addon_categories table မှာ drink နဲ့ size ဆိုတဲ့ data တွေ ထည့်ကြည့်ပါမယ်။

![enter image description here](https://raw.githubusercontent.com/Aungmyanmar32/msquare-m4/main/hpos1%20%2821%29.png)

- addons မှာ လည်း pepsi , cola  ဆိုတဲ့ data ထည့်ပြီး drink category နဲ့ ချိတ်ပါမယ်။
- နောက်ထပ် large , normal ဆိုတဲ့ data ထပ်ထည့်ပြီး  size category နဲ့ ချိတ်ပါမယ်။

![enter image description here](https://raw.githubusercontent.com/Aungmyanmar32/msquare-m4/main/hpos1%20%2822%29.png)
- ခု addon နဲ့ categories ကို join ထားတာကို စမ်းကြည့်ပါမယ်။

![enter image description here](https://raw.githubusercontent.com/Aungmyanmar32/msquare-m4/main/hpos1%20%2823%29.png)
##
- ဆက်ပြီး အရင် လုပ်ထားတဲ့ menus table နဲ့ addon_categories table ကို menus_addon_categories table တစ်ခုလုပ်ပြီး one to many relation နဲ့ join ပါမယ်

![enter image description here](https://raw.githubusercontent.com/Aungmyanmar32/msquare-m4/main/hpos1%20%2824%29.png)
- ပြီးရင် menu ထဲက mont hin khar နဲ့  addon categories ထဲက drink / size တို့နဲ့ ချိတ်ဆက်ပါမယ်။

![enter image description here](https://raw.githubusercontent.com/Aungmyanmar32/msquare-m4/main/hpos1%20%2825%29.png)
- အဲ့လိုချိတ်ဆက်ပြီးရင် inner join နဲ့ ပြန်စမ်းကြည့်ပါမယ်။

![enter image description here](https://raw.githubusercontent.com/Aungmyanmar32/msquare-m4/main/hpos1%20%2826%29.png)
- ခုဆိုရင် table တွေကို join လုပ်တာကို သဘောပေါက်လာမယ်လို့ ထင်ပါတယ်။
- အိမ်စာအနေနဲ့ menu data တွေ ထည့်ကြည့်ပြီး addon တွေနဲ့ ချိတ်ဆက်ကာ UI မှာ ပြစမ်းကြည့်ကြပါ။

