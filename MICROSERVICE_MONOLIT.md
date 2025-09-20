1. Monolit arxitektura nima?

Monolit — bu butun ilova bitta kod bazada, bitta deploy qilinadigan arxitektura.

Barcha modullar (auth, user, order, payment) bitta kod ichida.

Deploy → butun dastur bir joyda ishga tushadi.

Oddiy misol:

Bir do‘kon ilovasida:

/users – foydalanuvchilar

/orders – buyurtmalar

/products – mahsulotlar

/payments – to‘lov
👉 Hammasi bitta dastur (app.js yoki app.jar) ichida.

Afzalliklari:

Oddiy start qilish.

Kodni tushunish oson (kichik jamoa uchun).

Debug va testing sodda.

Kamchiliklari:

Katta loyihada kod “spagetti” bo‘lib ketadi.

Bitta kichik o‘zgarish butun ilovani qayta deploy qilishga majbur qiladi.

Skalalash qiyin: hamma modulni birga ko‘paytirish kerak.

Texnologiya tanlash moslashuvchan emas (hamma modul bitta tex-stack’da).

2. Microservices arxitekturasi nima?

Microservices — bu ilovani bir nechta mustaqil xizmatlarga bo‘lib tashlash.

Har bir xizmat mustaqil kod, mustaqil deploy, mustaqil texnologiya.

Xizmatlar API (odatda REST yoki GraphQL) orqali bir-biri bilan gaplashadi.

Masalan:

Auth service

User service

Product service

Order service

Payment service

Afzalliklari:

Mustaqil rivojlantirish va deploy qilish mumkin.

Har bir xizmatni mustaqil skalalash mumkin (masalan, faqat order service’ni).

Turli texnologiyalardan foydalanish mumkin (masalan, auth Node.js’da, payment Java’da).

Katta jamoalar mustaqil ishlashi osonroq.

Nosozlik izolyatsiyasi (faqat bitta xizmat o‘chishi mumkin).

Kamchiliklari:

Murakkablik oshadi (tarmoq, monitoring, logging, tracing kerak).

Ma’lumotlarni konsistensiya qilish qiyinroq (eventual consistency).

Servislararo aloqa sekinroq (network overhead).

DevOps va infratuzilma (Docker, Kubernetes) zarur.

3. Monolit va Microservices taqqoslash
Aspekt	Monolit	Microservices
Deploy	Hammasi bitta joyda	Har xizmat alohida
Kod bazasi	Bitta katta kod	Kichik-kichik kodlar
Skalalash	Butun ilovani	Faqat kerakli xizmatni
Texnologiya	Bitta tex-stack	Har xil tex-stack
Jamoa	Kichik jamoa uchun yaxshi	Katta jamoalar uchun qulay
Tez start	Juda tez	Murakkab (infra kerak)
Xatolik	Bir modul ishdan chiqsa – butun ilova	Faqat bitta xizmat to‘xtashi mumkin
Ma’lumot	Bitta umumiy DB	Har servis o‘z DB’siga ega bo‘lishi mumkin
4. Analogiya (hayotiy misol)

Monolit → katta supermarket, hamma narsa ichida: oziq-ovqat, kiyim, elektronika, dorixona. Agar supermarket eshigi yopilsa, hammasi to‘xtaydi.

Microservices → bozor (market): har do‘kon alohida. Agar bir do‘kon yopilsa (masalan, poyabzal do‘koni), qolganlari ishlashda davom etadi.

5. Xulosa

Agar kichik loyiha yoki tez prototip kerak → Monolit oson va tez.

Agar katta loyiha, ko‘p jamoa, tez-tez yangilanish va skalalash kerak bo‘lsa → Microservices yaxshi.
