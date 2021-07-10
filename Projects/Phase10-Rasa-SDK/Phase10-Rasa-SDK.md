<div dir="rtl" align='right'>

# توسعه اکشن سرور با رازا

توی فاز قبلی یک ربات با فریمورک رازا ساختی و باهاش صحبت کردی. ولی این ربات نمیتونه به درخواست هایی مانند هواشناسی جواب بده. توی این مرحله میخوایم بریم سراغ توسعه اکشن سرور با Rasa-SDK.
داکیومنت هاش رو میتونی توی سایت رازا پیدا کنی: 
[مستندات اکشن سرور رازا](https://rasa.com/docs/action-server)

چند تا مفهوم توی توسعه اکشن سرورها هست که اینجا به طور کلی توضیح میدیم ولی برای تسلط و اطلاعات بیشتر، به داکیومنت های خود رازا نگاه کن.

## توضیح Action
کلاس Action، کلاس پایه برای توسعه اکشن هست. دو تا متد مهم این کلاس name  و run هست که اولی اسم اکشن رو برمیگردونه و دومی اون عملیاتی که میخوایم رو انجام میده. هر وقت که اینتنت مربوط به این اکشن درخواست شد، این متد فراخوانی میشه.

## توضیح Tracker
توی معماری رازا، Tracker چیزی هست که تاریخچه کل گفتگوهای کاربر رو نگه میداره. اینکه چه پیام هایی رد و بدل شده، چه اسلات هایی مقدار گرفته و ... . به این Tracker هم از طریق کلاسش میشه دسترسی داشت و اطلاعات داخل اون رو دریافت کرد.

## توضیح Dispatcher
از این آبجکت استفاده می کنیم تا به کاربر جواب بدیم.

یک اکشن ساده اینطوریه:

<div dir="ltr" align='left'>

```Python
class GreetingHello(Action):

    def name(self) -> Text:

        return "greeting_hello"

    async def run(
        self, dispatcher, tracker: Tracker, domain: Dict[Text, Any],
    ) -> List[Dict[Text, Any]]:
        dispatcher.utter_message(text = "سلام! خوش اومدی")
        return []

```

<div dir="rtl" align='right'>

## پروژه
برای این فاز، این تسک ها رو انجام بده:
1. از اکشن سرور استفاده کن تا به درخواست های کاربر پاسخ بدی. برای همه ی اینتنت ها، یه اکشن بنویس.
2. پاسخ هایی که قراره به کاربر بدی رو توی دیتابیس مانگو بذار و موقع پاسخ به کاربر،از اونجا کوئری بزن و دریافت کن. اینکار باعث میشه که موقع اجرا، به راحتی پاسخ ها رو تغییر بدی و یا کم و زیادشون کنی.
3. درخواست هواشناسی رو هم اضافه کن. توی این درخواست، کاربر اسم شهر رو هم میتونه بگه، اگه نگفت، بصورت پیش فرض، شهر رو برابر تهران در نظر بگیر.

# معرفی Form

فرم ها یکی از قابلیت های مهم رازا هست که توسعه دهنده ها میتونن از اون در درخواست هایی که نیاز به اطلاعات هست، استفاده کنن. تفاوت اکشن و فرم در این هست که اکشن ها تک مرحله این هستند ولی فرم ها میتونن تک و چند مرحله ای باشند و بصورت تعاملی با کاربر صحبت کنن و اطلاعاتی مورد نیاز برای درخواست مورد نظر رو تکمیل کنن. توضیحات و مستندات توی سایت رازا هست: 
[مستندات فرم ها](https://rasa.com/docs/rasa/forms)