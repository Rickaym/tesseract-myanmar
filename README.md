# Tesseract Myanmar

Myanmar Script အတွက် tesseract OCR ရဲ့ out of the box ပေးထားတဲ့ traineddata ဖိုင်ဟာ error rate အရမ်းများပါတယ်၊ အကြောင်းက
- ( ၌၊ ၍၊ ၏၊ ၎) နှင့် (ပုဒ်ထီး၊ ပုဒ်မ) အက္ခရာတို့ မပါ
- ဖွန့်အမျိုးအစားများစွာအတွက် training လုပ်ထားခြင်းမရှိ
- training text ထဲမှာ zawgyi encoded စာတွေ ရောနှောနေတာတို့ကြောင့်ဖြစ်ပါသည်။

မြန်မာစာအတွက် OCR အမှန်ဆုံးလို့ ဆို့ရမယ့် Google Vision ရဲ့ OCR ကလည်း မြန်မာဝေါဟာရအတွက်ဘဲ အဆင်ပြေတယ်။ ပါဠိဝေါဟာရများအတွက် error rate အရမ်းများနေသေးတယ်။ ပါဠိ၊ အဋ္ဌကထာ၊ ဋီကာ နိဿယများကို scan version မှ text version သို့ စွမ်းနိုင်သလောက် ပြောင်းထားဘို့ စိတ်ကူးပေါ်တုန်း tesseract OCR ရဲ့ myanmar script အတွက် trainneddata ဖိုင်ကို layer replacing နည်းဖြင့် fine tune လုပ်ပြီး စမ်းကြည့်တာ အတော်လေး ရလာဒ်ကောင်းမွန်တာမို့ ပြန်လည်ဝေမျှလိုက်ပါသည်။ error rate ကို ဇယားမှာ ကြည့်ပါ။

မှတ်ချက်။ ။ accuracy အတော်ကောင်းပါသော်လည်း tesseract OCR ၏ text-line finding သည် ဗျည်းထက်၌ ရှိသော လုံးကြီးတင်၊ လုံးကြီးတင်ဆံခတ်၊ အသတ်စသည်တို့သည် ဗျည်းနှင့် မထိစပ်ဘဲ လွတ်နေသော စာလုံးဒီဇိုင်းမျိုးဖြစ်ပါက ထိုလုံးကြီးတင်စသည်တို့ကို လိုင်းတလိုင်းအနေဖြင့် ခွဲထုတ်သောကြောင့် အချို့သော မြန်မာဖွန့်ဒီဇိုင်းများအတွက် မမှန်ပါ။ (  အာရေဗျ၊ ဂျပန်၊ ဂျာမနီ စသည်တို့အတွက်လည်း မမှန်သေး၏ ဟု ဆိုကြ) ။

tesseract ရဲ့ text line segmentation fail ဖြစ်တဲ့အခါမှာ သုံးလို့ရအောင် opencv + python သုံးပြီး text line segment script လေး စမ်းကြည့်ထားတယ်။ လိုအပ်တွေ အများကြီးပါ။ စာကြောင်းတွေ ထပ်နေရင် ( line spacing နည်းလွန်းရင်)၊ စာကြောင်းတွေ ကွေးနေရင် ( warp ဖြစ်နေရင် ) အဆင်မပြေပါဘူး။

## အသုံးပြု့နည်း 

<!-- https://saiashish90.medium.com/training-tesseract-ocr-with-custom-data-d3f4881575c0#:~:text=5,data%20and%20start%20from%20scratch -->

၁. `tessdata` ဆိုသော directory ကိုရှာပါ၊ ဒီ directory တွင် Tesseract အသုံးပြုသည့် ဘာသာစကားဒေတာဖိုင်များ ကိုထားရှိသည်။.

ဥပမာ
1. /usr/local/share/tessdata/` or
2. /usr/share/tesseract-ocr/4.00/tessdata/ on Linux, and
3. C:\Program Files\Tesseract-OCR\tessdata\ on Windows 

၂. `mya.traineddata` ဖိုင်ကို `tessdata` directory ထဲသို့ ရွှေ့ပြောင်းပါ

၃. Tesseract ကိုအသုံးပြု့သောအခါ၊ "-l" သို့မဟုတ် "--lang" option ဖြင့် language "mya" ဆိုပြီးပေးပါ။

ဥပမာ
```
tesseract input.png output -l mya
```

## Error Rates

ဒါကတော့ noise မပါတဲ့ eval data set ပေါ်မှာ evaluate လုပ်ထားတာပါ။ noise စသည်ပါလာရင်တော့ ဒီထက်ပိုပြီး error rate များပါလိမ့်မယ်။

|    |     font   | char error rate | word error rate |
|----|-------------------------|------------|-----------|
| 1  | Myanmar_PaOh            | 0.42941127 | 4.3377578 |
| 2  | Myanmar_Ethnic_Sans     | 0.46718541 | 4.4345238 |
| 3  | Myanmar_Yein            | 0.6053413  | 5.8825121 |
| 4  | Myanmar_Sans_Pro        | 0.63756975 | 5.4966313 |
| 5  | Myanmar_UI              | 0.63978621 | 5.8351371 |
| 6  | Pyidaungsu              | 0.68607731 | 5.9856023 |
| 7  | MUA_Office              | 0.70245574 | 6.7455202 |
| 8  | Myanmar_Tagu            | 0.70260465 | 7.8238946 |
| 9  | Myanmar_Sabae           | 0.72382359 | 4.8816138 |
| 10 | Noto_Sans_Myanmar       | 0.73380574 | 5.7155067 |
| 11 | Myanmar_MUA             | 0.74944535 | 6.5346529 |
| 12 | Pyidaungsu_Bold         | 0.76580684 | 7.2995682 |
| 13 | Myanmar_Pangram         | 0.81070258 | 6.2678314 |
| 14 | Myanmar_Grand           | 0.81442107 | 6.0077483 |
| 15 | Myanmar_Squarehand      | 0.82573218 | 7.8014958 |
| 16 | Myanmar_Sagar           | 0.83168089 | 6.2852262 |
| 17 | Padauk_Bold             | 0.87910899 | 8.6717926 |
| 18 | Padauk                  | 0.88295635 | 7.7363192 |
| 19 | Noto_Sans_Myanmar_UI    | 0.90406301 | 6.977467  |
| 20 | Myanmar_Sanpya          | 0.90629666 | 6.7556471 |
| 21 | KhunPaOh                | 0.93467255 | 10.175707 |
| 22 | Hopong                  | 0.9837311  | 7.7665043 |
| 23 | ThanLwin                | 0.98857813 | 7.5042972 |
| 24 | Myanmar_Text            | 0.99648591 | 5.7332251 |
| 25 | Ours-Unicode            | 1.053145   | 7.3451244 |
| 26 | Myanmar_Pauklay         | 1.0548857  | 7.8954101 |
| 27 | Myanmar_Ekaya           | 1.0671492  | 7.4526902 |
| 28 | Cherry_Unicode          | 1.0777003  | 7.1956848 |
| 29 | Hsi_Hseng               | 1.1190725  | 10.013299 |
| 30 | Myanmar_Square          | 1.1897668  | 9.5039683 |
| 31 | Myanmar_Gantgaw         | 1.2558542  | 7.7054364 |
| 32 | Myanmar_Chatu           | 1.3166145  | 10.894742 |
| 33 | Myanmar_Phiksel_Smooth  | 1.3338799  | 12.17939  |
| 34 | Myanmar_Taungthu        | 1.3414034  | 10.334584 |
| 35 | Myanmar_Katkuu          | 1.4077546  | 10.765435 |
| 36 | Myanmar_BoKaow          | 1.4745422  | 10.716612 |
| 37 | Myanmar_Waitzar         | 1.4890937  | 12.193301 |
| 38 | Myanmar_Phetsot         | 1.5279923  | 12.255201 |
| 39 | Myanmar_four            | 1.7663877  | 12.963214 |
| 40 | Myanmar_Nayone          | 1.9427612  | 13.551888 |
| 41 | Noto_Sans_Myanmar_Bold  | 1.9637489  | 13.091575 |
| 42 | tawzin-018              | 2.0036169  | 5.4761    |
| 43 | alankar                 | 2.1429148  | 20.204365 |
| 44 | Yunghkio                | 2.157214   | 9.1917768 |
| 45 | Myanmar_Chatu_Light     | 2.1715123  | 13.758966 |
| 46 | Noto_Serif_Myanmar      | 2.2559152  | 13.520698 |
| 47 | monotype_eval_1         | 2.4217351  | 16.954887 |
| 48 | Myanmar_Sketch          | 2.5663688  | 12.084607 |
| 49 | monotype_eval_2         | 2.57996    | 19.210526 |
| 50 | Myanmar_Square_Light    | 2.76287    | 16.257971 |
| 51 | Myanmar_Njaun           | 2.7668908  | 13.564779 |
| 52 | Myanmar_Tagaung         | 2.9754883  | 19.844419 |
| 53 | Yangon                  | 3.4642327  | 45.052338 |
| 54 | buddhavan               | 3.8319597  | 27.555556 |
| 55 | YoeYar-One              | 3.8710353  | 27.79239  |
| 56 | Myanmar_Text_Bold       | 4.0489174  | 10.442834 |
| 57 | Myanmar_Taunggyi        | 4.1705694  | 28.81169  |
| 58 | Myanmar_Khway           | 4.6355567  | 24.030112 |
| 69 | salin_eval              | 4.9816442  | 26.211735 |
| 60 | maeu_eval               | 5.920616   | 26.839827 |
| 61 | Myanmar_Handwriting     | 18.287787  | 46.761013 |
