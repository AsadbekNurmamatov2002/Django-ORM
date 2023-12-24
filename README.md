# Django ORM so'rovlari

***
### Umumiy koʻrinish
Django veb-ramka SQLite, PostgreSQL va MySQL kabi turli relyatsion ma'lumotlar bazalari ma'lumotlari bilan o'zaro ishlash uchun ishlatilishi mumkin bo'lgan standart ob'ektga aloqador xaritalash qatlamini (ORM) o'z ichiga oladi. Django bizga ORM deb nomlangan API yordamida ob'ektlarni qo'shish, o'chirish, o'zgartirish va so'rov qilish imkonini beradi. ORM qisqartmasi Ob'ekt bilan bog'liq xaritalash degan ma'noni anglatadi. Ob'ektga aloqador mapper SQL so'rovlarini yozmasdan, relyatsion ma'lumotlar bazalari va ob'ektga yo'naltirilgan dasturlash tillari o'rtasida ob'ektga yo'naltirilgan qatlamni ta'minlaydi.

### Django ORM so'rovlariga kirish
Django bizga ORM deb nomlangan API yordamida o'zining ma'lumotlar bazasi modellari bilan o'zaro ishlash imkonini beradi . ORM ning asosiy maqsadi ma'lumotlar bazasi va dastur modellari o'rtasida ma'lumotlarni yuborishdir. U ma'lumotlar bazasi va model o'rtasidagi munosabatni ifodalaydi. Django ORM so'rovlaridan foydalanishning asosiy afzalligi shundaki, u tezlashtiradi va ishlab chiqish jarayonida xatolarni yo'q qiladi.

### QuerySet nima?
So'rovlar to'plami ma'lumotlar bazasidan olingan ma'lumotlar to'plamidir. So'rovlar to'plami bizga filtrlash, yaratish, buyurtma qilish va hokazolarni amalga oshirish orqali ma'lumotlarni osongina olish imkonini beradi. Keling, talabalar nomli ma'lumotlar bazasi jadvalini misol qilib olaylik.

![image](https://github.com/AsadbekNurmamatov2002/Django-ORM/assets/144318530/31fa8728-23fb-4dcc-8a04-62ea377c066e)

__views.py__ da bizda test deb nomlangan ko'rinish mavjud bo'lib, unda biz turli so'rovlarni sinab ko'ramiz. Quyidagi manba kodida biz talabalar modelining barcha yozuvlari va maydonlarini olish uchun __all()__ dan foydalanamiz. Ob'ekt mydata deb nomlanuvchi o'zgaruvchiga joylashtirilgan , u mystudents sifatida kontekst ob'ekti orqali shablonga yuboriladi:
![image](https://github.com/AsadbekNurmamatov2002/Django-ORM/assets/144318530/1052c281-cdfa-4234-94b8-5501c2d582c7)
Model talabalari 5 ta yozuvni o'z ichiga oladi, ular so'rovlar to'plamida 5 ta ob'ekt sifatida ro'yxatga olinadi.
![image](https://github.com/AsadbekNurmamatov2002/Django-ORM/assets/144318530/bf6772aa-9b4a-4372-89a7-ab564b56f018)
### Django Shell
Shunday qilib, Django qobig'iga kirish uchun virtual muhitda buyruq satriga quyidagi buyruq kiritilishi kerak:
>       >>> python manage.py shell
Bu bizni interaktiv konsolga olib boradi.
>       (InteractiveConsole)
>       >>>

### Barcha ob'ektlar
Modeldan ma'lumotlarni so'rovlar to'plamiga olishning ba'zi usullari mavjud: 1. all() U har bir ob'ektni Python lug'ati sifatida nomlari va qiymatlari mos ravishda kalit va qiymat juftlari sifatida qaytaradi. Xuddi shu narsa uchun manba kodi quyida keltirilgan:
>       Students.objects.all().values()
__Chiqish_
![image](https://github.com/AsadbekNurmamatov2002/Django-ORM/assets/144318530/81633382-1084-46c8-8ac3-2803dc248c86)
__values_list()__

values_list () faqat belgilangan ustunni qaytaradi. Xuddi shu narsa uchun manba kodi quyida keltirilgan:
>     >>> Students.objects.values_list('Subjects')

__Chiqish:_
![image](https://github.com/AsadbekNurmamatov2002/Django-ORM/assets/144318530/42482edc-4d3c-432c-8520-9de912d5c8c2)
- Ob'ektlar yaratish
Ob'ektni yaratish uchun dastlab talabalarni import qilishimiz kerak
>      >>>from django.contrib.auth.models import Students
>      >>>Students.objects.create(id=06,name=’Victor’, subject='Ecology')
- Ob'ektlarni filtrlash
__filter ()__ filtrlangan qidiruvni qaytaradi. Xuddi shu narsa uchun manba kodi quyida keltirilgan:

>      >>>Students.objects.filter(name=’Robert’)
The queryset object:
<QuerySet [{'id': 04, 'name': 'Robert', 'subjects': 'Computer Science'}]>

| ID  | Name   | Subjects         |
| --- | ------ | ---------------- |
| 04  | Robert | Computer Science |


Django shuningdek, __AND__ va __OR__ operatsiyalari kabi bir nechta shartlar asosida filtrlangan ma'lumotlarni olish va ularni bajarish imkonini beradi.

### 1. VA

Biz yuqorida ko'rsatilgan ikkala so'rovni qondiradigan filtrlangan ma'lumotlarni olishimiz mumkin. Namoyish uchun misolga qarang.
>       >>>Students.objects.filter(name='Jerry', id=2).values()
U qaytaradigan natija :
The queryset object:
<QuerySet [{'id': 02, 'name': 'Jerry', 'subjects': ‘Mathematics'}]>
| ID  | Name  | Subjects    |
| --- | ----- | ----------- |
| 02  | Jerry | Mathematics |

__2. OR__

Shuningdek, biz yuqorida ko'rsatilgan so'rovlardan biriga mos keladigan filtrlangan ma'lumotlarni olishimiz mumkin. Quyida misol keltiriladi.
>        >>> Students.objects.filter(name='Jacob').values()| Students.objects.filter(name='Robert').values()
U qaytaradigan natija :
>
The queryset object:
<QuerySet [{'id': 03, 'name': 'Jacob', 'subjects': 'Biology'}, {'id': 04, 'name': 'Robert', 'subjects': 'Computer Science'}]>

| ID  | Name   | Subjects         |
| --- | ------ | ---------------- |
| 03  | Jacob  | Biology          |
| 04  | Robert | Computer Science |
>
__3. Maydonlarni qidirish__

Maydonlarni qidirish - bu aniq SQL kalit so'zlarini ifodalovchi kalit so'zlar.

>     >>>Students.objects.filter(name__startswith='J').values()
The queryset object:
<QuerySet [{'id': 02, 'name': 'Jerry', 'Subjects': 'Mathematics'}, {'id': 03, 'name': 'Jacob', 'subjects': 'Biology'}, {'id': 05, 'name': 'Julia', 'subjects': 'Chemistry'}]>

| ID  | Name  | Subjects    |
| --- | ----- | ----------- |
| 02  | Jerry | Mathematics |
| 03  | Jacob | Biology     |
| 05  | Julia | Chemistry   |

__Ob'ektlarga buyurtma berish__
Django __order_by()__ yordamida so'rovlar to'plamini saralash xususiyatini taqdim etadi .

1. Natijani nomi bo'yicha alifbo tartibida tartiblash

>        >>>Students.objects.all().order_by('name').values()
U quyidagilarni qaytaradi:
***
The queryset object:
<QuerySet [{'id': 03, 'name': 'Jacob', 'subjects': 'Biology'}, {'id': 02, 'name': 'Jerry', 'Subjects': 'Mathematics'}, {'id': 05, 'name': 'Julia', 'subjects': 'Chemistry'}, {'id': 04, 'name': 'Robert', 'subjects': 'Computer Science'} {'id': 01, 'name': 'Thomas', 'subjects': 'Physics'}]>

| ID  | Name   | Subjects         |
| --- | ------ | ---------------- |
| 03  | Jacob  | Biology          |
| 02  | Jerry  | Mathematics      |
| 05  | Julia  | Chemistry        |
| 04  | Robert | Computer Science |
| 01  | Thomas | Physics          |

__2. Kamayish tartibida saralash "-"__

Natijalar sukut bo'yicha o'sish tartibida tartiblangan. Kamayish tartibida saralash uchun maydon nomi oldiga __“-”__ minus belgisini qo‘yamiz . Shunday qilib, teskari alifbo tartibida tartiblash uchun "nom" oldiga  __"-"__  qo'shamiz .
>       >>>Students.objects.all().order_by('-name').values()
__Yuqoridagi kod qaytaradi_
***
The queryset object:
<QuerySet [{'id': 01, 'name': 'Thomas', 'subjects': 'Physics'}, {'id': 04, 'name': 'Robert', 'Subjects': 'Computer Science'}, {'id': 05, 'name': 'Julia', 'subjects': 'Chemistry'}, {'id': 02, 'name': 'Jerry', 'subjects': 'Mathematics'} {'id': 03, 'name': 'Jacob', 'subjects': 'Biology'}]>

| ID  | Name   | Subjects         |
| --- | ------ | ---------------- |
| 01  | Thomas | Physics          |
| 04  | Robert | Computer Science |
| 05  | Julia  | Chemistry        |
| 02  | Jerry  | Mathematics      |
| 03  | Jacob  | Biology          |

__3. Bir nechta buyurtma bo'yicha__

Bir nechta maydonga buyurtma berish uchun quyidagi kodni ko'rib chiqing.

>       >>>Students.objects.all().order_by('name', ’-id’).values()
natija
***
The queryset object:
<QuerySet [{'id': 03, 'name': 'Jacob', 'subjects': 'Biology'}, {'id': 02, 'name': 'Jerry', 'Subjects': 'Mathematics'}, {'id': 05, 'name': 'Julia', 'subjects': 'Chemistry'}, {'id': 04, 'name': 'Robert', 'subjects': 'Computer Science'}, {'id': 01, 'name': 'Thomas', 'subjects': 'Physics'}]>

| ID  | Name   | Subjects         |
| --- | ------ | ---------------- |
| 03  | Jacob  | Biology          |
| 02  | Jerry  | Mathematics      |
| 05  | Julia  | Chemistry        |
| 04  | Robert | Computer Science |
| 01  | Thomas | Physics          |

__Usul zanjiri orqali murakkab so'rovlar__
So'rovlar to'plamini zanjirband qilish orqali boshqa so'rovlar to'plami bilan birlashtirish mumkin,

>      >>>Students.objects.filter(id=1).filter(subject=’Chemistry’)

***
Yuqoridagi kod qaytib keladi
Usul zanjiri orqali murakkab so'rovlar
So'rovlar to'plamini zanjirband qilish orqali boshqa so'rovlar to'plami bilan birlashtirish mumkin,

>      >>>Students.objects.filter(id=1).filter(subject=’Chemistry’)
***
Yuqoridagi kod qaytib keladi
The queryset object:
<QuerySet [{'id': 05, 'name': 'Julia', 'subjects': 'Chemistry'}, {'id': 01, 'name': 'Thomas', 'subjects': 'Physics'}]>

| ID  | Name   | Subjects  |
| --- | ------ | --------- |
| 05  | Julia  | Chemistry |
| 01  | Thomas | Physics   |
## Har bir ORM so'rovi va bog'langan SQL so'rovlarini tushuntirish

__Har bir ORM so'rovi va bog'langan SQL so'rovlarini tushuntirish_

>    class Album(models.Model):
>        title = models.CharField(max_length=50)
>        artist = models.CharField(max_length=50)
>        genre = models.CharField(max_length=50)
>        def __str__(self):
>           return self.title
>  
>    class Song(models.Model):
>        name = models.CharField(max_length=50)
>        album = models.ForeignKey(Album, on_delete=models.CASCADE)
>        def __str__(self):
>           return self.name

Yuqoridagi kodda biz ikkita Albom va Qo'shiq modelini yaratdik. Har doim Django-da modelning namunasi yaratilganda, u ob'ektni administrator interfeysida Model nomi ob'ekti (1) sifatida ko'rsatadi. Demak, ko'rsatilgan nomni o'zgartirish uchun biz def __str__(self) funksiyasidan foydalanamiz . Django modelidagi Str funksiyasi ushbu model uchun misollarning ko'rsatiladigan nomi sifatida ko'rsatilgan qatorni qaytaradi . Bizning holatda, u Model albomi sarlavhasi va Model qo'shig'i uchun qo'shiq nomini ko'rsatadi. Model qo'shig'ida biz ikkinchi maydonni, albomni Model albomi bilan bog'laymiz.

Modellarni yaratgandan so'ng, biz quyidagi buyruqni ishlatishimiz kerak:
>    Python manage.py makemigrations
>    Python manage.py migrate
Yuqoridagi buyruqlarda makemigrations o'zgarishlarni individual migratsiya fayllariga to'plash uchun javobgar, migrate esa ularni ma'lumotlar bazasiga qo'llash uchun javobgardir.

Endi biz Django ORM ga kirishimiz kerak, unga loyiha katalogimizdagi quyidagi buyruq yordamida kirish mumkin:

>       python manage.py shell
Bu bizni interaktiv Python konsoliga olib boradi. Keyinchalik, quyidagi buyruq yordamida modellarimizni import qilishimiz kerak:
>        >>> from playlist.models import Song, Album
>        >>>a = Album.objects.create(title="Add", artist="Sheeran", genre="pop")
>        >>>a.save()
>        >>>a = Album.objects.create(title="Abstract Road", artist="The Beatles", genre="rock")
>        >>>a.save()
>        >>>a = Album.objects.create(title="Run Evolver", artist="The Beatles", genre="slow")
>        >>>a.save()

Modelning barcha ob'ektlarini olish uchun __all()__ dan foydalaniladi:
>        >>> Album.objects.all()
>        <QuerySet [<Album: Add>, <Album: Abstract Road>, <Album: Run evolver>]>
__SQL da__
>        SELECT * FROM ALBUM;
Jadvalga ma'lumot __kiritish__ (Model)
Jadval (Model) albomiga yozuvni qo'shish va saqlash uchun quyidagi kodni yozamiz:
>        >>>a = Album.objects.create(title="Add", artist="Sheeran", genre="Pop")
>        >>> a.save()
__SQL da__
>        INSERT INTO Album VALUES ('Add', 'Sheeran', 'Pop');










