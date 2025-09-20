1. Event Loop nima?

Node.js bitta threadda (bir ipda) ishlaydi. Ya’ni, bir vaqtning o‘zida faqat bitta kod satrini bajaradi.
Lekin shunday bo‘lsa ham, Node.js minglab parallel so‘rovlarni boshqara oladi. Sir — event loopda.

👉 Event loop – bu “navbatchi” mexanizm. U navbatdagi vazifalarni tartib bilan bajaradi: kim navbatda – o‘sha ishlaydi.

2. Oddiy analogiya

Tasavvur qiling:

Restoranda bitta ofitsiant bor (Node.js thread).

50 ta stol mijoz (so‘rovlar).

Har stol ichimlik, ovqat, desert buyuradi.

👉 Ofitsiantning strategiyasi:

Har stolga ketma-ket qaraydi.

Ovqatni pishirish (I/O operatsiya) oshxonaga (OS/libuv) topshiradi.

Pishishini kutib o‘tirmaydi, keyingi stolga qarab ketadi.

Oshxonadan signal kelganda (callback), tayyor ovqatni olib boradi.

Shu bilan, bitta ofitsiant yuzlab mijozga xizmat qila oladi.

3. Event Loopning bosqichlari

Event loop fazalarga bo‘lingan:

Timers → setTimeout, setInterval callbacklari ishlaydi.

Pending callbacks → tizim callbacklari (I/O’lar uchun).

Idle/Prepare → ichki ishlov berish.

Poll → asosiy bosqich. I/O eventlari shu yerda kutib turadi.

Check → setImmediate callbacklari shu yerda ishlaydi.

Close callbacks → masalan, socket.on('close').

⚡️ Har bir faza tugagach, microtask queue (Promises .then(), process.nextTick) ishlanadi.

4. Misol bilan tushuntirish
console.log("1");

setTimeout(() => {
  console.log("2 - setTimeout");
}, 0);

Promise.resolve().then(() => {
  console.log("3 - promise");
});

process.nextTick(() => {
  console.log("4 - nextTick");
});

console.log("5");


👉 Natija tartibi:

1
5
4 - nextTick   // microtask
3 - promise    // microtask
2 - setTimeout // timers


📝 Sabab:

Synchronous kod → darhol (1,5).

process.nextTick → microtasklardan ham ustun.

Promise → microtask.

setTimeout → keyingi “timers” fazasida.

5. Backend samaradorligi

🔑 Asosiy g‘oya: Node.js I/O (disk, tarmoq, DB) ishlarini bloklamaydi.

Agar bitta so‘rov katta fayl o‘qiyapti → bu ishni libuv OS’ga topshiradi.

Shu paytda boshqa foydalanuvchilarning so‘rovlarini qabul qilishda davom etadi.

Fayl o‘qilishi tugaganda → callback navbatga qo‘yiladi → event loop uni bajaradi.

👉 Natija:

Bir thread bilan minglab ulanishni boshqarish mumkin.

Kam resurs sarflanadi.

Shuning uchun Node.js real-time chat, API gateway, streamingda juda samarali.

6. Oddiy rasmiy chizma
   [JS kod] → Call stack
       |
       v
[Event Loop] ↔ [Callback Queue]
       |
       v
   [libuv / OS APIs]

7. Xulosa

Event loop – Node.js yuragi.

U navbat prinsipida ishlaydi va I/O’ni OS’ga topshirib yuboradi.

Shu sababli Node.js:

ko‘p ulanishni bir vaqtning o‘zida boshqara oladi,

resurslarni tejamli ishlatadi,

backendda samaradorlikni oshiradi.
