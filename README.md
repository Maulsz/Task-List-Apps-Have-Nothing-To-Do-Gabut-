# Task List App — JavaScript & DOM Learning Notes

## 1. Tentang Project

Project ini merupakan aplikasi Task List sederhana yang dibuat menggunakan:

- HTML untuk struktur halaman.
- CSS untuk tampilan dan styling.
- JavaScript untuk mengatur data, logika aplikasi, dan interaksi pengguna.
- DOM (Document Object Model) untuk mengakses serta memanipulasi elemen HTML.

Project ini dibuat sebagai latihan untuk menguji pemahaman dasar JavaScript sebelum mempelajari framework JavaScript.

### Fitur aplikasi

1. Menampilkan daftar tugas.
2. Menambahkan tugas baru.
3. Menandai tugas sebagai selesai atau belum selesai.
4. Menghapus tugas.
5. Memfilter tugas berdasarkan status.
6. Menghitung total tugas, tugas yang belum selesai, dan tugas yang sudah selesai.
7. Menampilkan pesan validasi ketika pengguna memasukkan judul kosong.

---

# 2. Memahami DOM (Document Object Model)

DOM merupakan salah satu bagian yang cukup penting dalam JavaScript ketika kita bekerja dengan halaman web.

Sebelum memahami kode project ini, kita perlu memahami terlebih dahulu apa itu DOM dan bagaimana JavaScript berinteraksi dengan HTML.

## 2.1 Apa itu DOM?

DOM adalah representasi struktur dokumen HTML dalam bentuk objek yang dapat diakses dan dimanipulasi menggunakan JavaScript.

Sederhananya:

- HTML bertugas membuat struktur halaman.
- CSS bertugas mengatur tampilan.
- JavaScript dapat menggunakan DOM untuk membaca, mengubah, menambahkan, atau menghapus elemen HTML.

Contohnya, kita mempunyai HTML:

```html
<h1 id="judul">Belajar JavaScript</h1>
```

Kemudian kita ingin mengubah tulisan tersebut menggunakan JavaScript.

```js
const judul = document.querySelector("#judul");

judul.textContent = "Belajar DOM";
```

Hasilnya, tulisan yang awalnya:

```text
Belajar JavaScript
```

Berubah menjadi:

```text
Belajar DOM
```

JavaScript bisa melakukan perubahan tersebut karena elemen HTML sudah direpresentasikan sebagai objek yang dapat diakses melalui DOM.

## 2.2 Apa itu `document`?

`document` merupakan objek yang merepresentasikan dokumen HTML yang sedang dibuka di browser.

Melalui `document`, JavaScript dapat mencari dan mengakses elemen HTML.

Contoh:

```js
document.querySelector("#judul");
```

Artinya, JavaScript meminta browser untuk mencari elemen HTML dengan selector `#judul`.

Beberapa contoh penggunaan `document`:

```js
document.querySelector("h1");
document.querySelector("#judul");
document.querySelector(".container");
```

Perbedaannya:

- `"h1"` mencari elemen berdasarkan nama tag.
- `"#judul"` mencari elemen berdasarkan ID.
- `".container"` mencari elemen berdasarkan class.

## 2.3 Apa itu `querySelector()`?

`querySelector()` merupakan method JavaScript yang digunakan untuk mengambil elemen HTML berdasarkan CSS selector.

Contoh:

```html
<input id="nama" type="text" />
```

JavaScript:

```js
const input = document.querySelector("#nama");
```

Variabel `input` sekarang menyimpan referensi ke elemen input tersebut.

Kita juga bisa mengakses elemen menggunakan class:

```html
<p class="deskripsi">Belajar DOM</p>
```

```js
const deskripsi = document.querySelector(".deskripsi");
```

**Kenapa menggunakan `const`?**

Karena variabel tersebut hanya perlu menyimpan referensi elemen HTML yang sudah ditemukan. Kita tidak perlu mengganti referensi variabelnya.

Perlu diingat, `const` tidak berarti isi objeknya tidak bisa berubah. Kita tetap bisa mengubah properti elemen HTML yang disimpan di dalamnya.

Contoh:

```js
const judul = document.querySelector("#judul");

judul.textContent = "Judul Baru";
```

Variabel `judul` tidak diganti, tetapi isi elemen HTML yang dirujuknya berubah.

## 2.4 Apa itu `textContent`?

`textContent` merupakan properti yang digunakan untuk membaca atau mengubah teks di dalam suatu elemen HTML.

Contoh HTML:

```html
<p id="pesan">Pesan lama</p>
```

Mengubah teks:

```js
const pesan = document.querySelector("#pesan");

pesan.textContent = "Pesan baru";
```

Hasilnya:

```html
<p id="pesan">Pesan baru</p>
```

Kita juga bisa membaca teks:

```js
console.log(pesan.textContent);
```

Hasil:

```text
Pesan baru
```

**Kenapa project Task List menggunakan `textContent`?**

Karena banyak bagian aplikasi yang isi teksnya berubah sesuai kondisi data.

Contohnya:

```js
totalCount.textContent = total;
```

Angka total tugas yang ditampilkan di halaman akan mengikuti nilai variabel `total`.

Contoh lainnya:

```js
toggleButton.textContent = item.completed ? "Batalkan Selesai" : "Selesaikan";
```

Teks tombol berubah sesuai status tugas.

## 2.5 Apa itu `createElement()`?

`createElement()` merupakan method untuk membuat elemen HTML baru melalui JavaScript.

Contoh:

```js
const paragraf = document.createElement("p");
```

Kode tersebut membuat elemen paragraf baru.

Namun, elemen tersebut belum otomatis muncul di halaman HTML.

Kita masih perlu memasukkannya ke dalam elemen lain.

Contoh:

```js
const paragraf = document.createElement("p");

paragraf.textContent = "Belajar DOM";

document.body.appendChild(paragraf);
```

Sekarang paragraf tersebut sudah muncul di halaman.

**Kenapa project Task List menggunakan `createElement()`?**

Karena jumlah tugas tidak selalu sama.

Pengguna bisa menambahkan tugas sebanyak yang mereka inginkan. Oleh karena itu, JavaScript perlu membuat elemen HTML secara dinamis berdasarkan jumlah data tugas.

Jika ada tiga tugas, JavaScript membuat tiga elemen tugas.

Jika ada lima tugas, JavaScript membuat lima elemen tugas.

## 2.6 Apa itu `appendChild()`?

`appendChild()` merupakan method untuk memasukkan sebuah elemen ke dalam elemen HTML lainnya sebagai anak (child).

Contoh:

```js
const container = document.querySelector("#container");

const paragraf = document.createElement("p");

paragraf.textContent = "Halo Dunia";

container.appendChild(paragraf);
```

Struktur HTML yang dihasilkan:

```html
<div id="container">
  <p>Halo Dunia</p>
</div>
```

**Kenapa harus menggunakan `appendChild()`?**

Karena membuat elemen menggunakan `createElement()` saja belum cukup untuk menampilkannya di halaman.

Elemen tersebut harus dimasukkan ke dalam DOM.

Dalam project Task List, contohnya:

```js
taskElement.appendChild(titleElement);
taskElement.appendChild(toggleButton);
taskElement.appendChild(deleteButton);

list.appendChild(taskElement);
```

Alurnya:

1. Judul tugas dimasukkan ke dalam elemen tugas.
2. Tombol selesai dimasukkan ke dalam elemen tugas.
3. Tombol hapus dimasukkan ke dalam elemen tugas.
4. Elemen tugas yang sudah lengkap dimasukkan ke dalam daftar tugas.

Hasil struktur HTML-nya kurang lebih seperti ini:

```html
<div id="task-list">
  <div class="task">
    <span class="task-title">Belajar JavaScript</span>
    <button>Selesaikan</button>
    <button>Hapus</button>
  </div>
</div>
```

## 2.7 Apa itu `classList.add()`?

`classList` merupakan properti yang digunakan untuk mengelola class CSS pada suatu elemen HTML.

Salah satu method-nya adalah `add()`.

Contoh:

```js
const kotak = document.querySelector("#kotak");

kotak.classList.add("active");
```

JavaScript menambahkan class `active` ke elemen tersebut.

Sebelumnya:

```html
<div id="kotak"></div>
```

Sesudahnya:

```html
<div id="kotak" class="active"></div>
```

**Kenapa project Task List menggunakan `classList.add()`?**

Karena elemen tugas membutuhkan class tertentu agar bisa mendapatkan styling CSS.

Contohnya:

```js
taskElement.classList.add("task");
titleElement.classList.add("task-title");
```

Ketika tugas sudah selesai:

```js
if (item.completed) {
  taskElement.classList.add("done");
}
```

CSS:

```css
.task.done .task-title {
  text-decoration: line-through;
  color: #64748b;
}
```

Artinya, ketika sebuah elemen memiliki class `task`, kemudian di dalamnya terdapat elemen dengan class `task-title`, dan elemen pembungkusnya juga memiliki class `done`, maka judul tugas akan dicoret.

Selain `add()`, terdapat beberapa method lain:

```js
element.classList.remove("active");
```

Menghapus class `active`.

```js
element.classList.toggle("active");
```

Menambahkan class jika belum ada, atau menghapusnya jika sudah ada.

```js
element.classList.contains("active");
```

Memeriksa apakah elemen memiliki class `active`. Hasilnya berupa boolean (`true` atau `false`).

---

# 3. Memahami JavaScript yang Digunakan

Setelah memahami DOM, sekarang kita masuk ke bagian logika JavaScript.

## 3.1 Variabel `let` dan `const`

JavaScript menyediakan beberapa cara untuk membuat variabel. Dua yang digunakan dalam project ini adalah `let` dan `const`.

### `let`

Digunakan ketika nilai variabel perlu diubah atau ditetapkan ulang.

Contoh:

```js
let angka = 10;

angka = 20;

console.log(angka);
```

Hasil:

```text
20
```

Dalam project:

```js
let tasks = [
  { id: 1, title: "Pelajari array dan object", completed: false },
  { id: 2, title: "Latihan function", completed: true },
];

let nextId = 3;
```

`tasks` menggunakan `let` karena nantinya variabel tersebut bisa mendapatkan array baru ketika tugas dihapus.

`nextId` menggunakan `let` karena nilainya akan terus bertambah ketika tugas baru dibuat.

### `const`

Digunakan ketika variabel tidak perlu ditetapkan ulang.

Contoh:

```js
const nama = "Maul";
```

Dalam project:

```js
const form = document.querySelector("#task-form");
const input = document.querySelector("#task-input");
const list = document.querySelector("#task-list");
```

Variabel tersebut menyimpan referensi elemen HTML.

Kita tidak perlu mengganti referensi elemen tersebut selama aplikasi berjalan.

---

## 3.2 Array

Array adalah struktur data yang digunakan untuk menyimpan banyak nilai dalam satu variabel.

Contoh:

```js
const buah = ["Apel", "Jeruk", "Mangga"];
```

Setiap data dalam array memiliki index yang dimulai dari angka 0.

| Index | Nilai  |
| ----- | ------ |
| 0     | Apel   |
| 1     | Jeruk  |
| 2     | Mangga |

Mengakses data:

```js
console.log(buah[0]);
```

Hasil:

```text
Apel
```

Dalam project, array digunakan untuk menyimpan seluruh tugas:

```js
let tasks = [
  { id: 1, title: "Pelajari array dan object", completed: false },
  { id: 2, title: "Latihan function", completed: true },
];
```

Array `tasks` berisi beberapa object.

Artinya, setiap tugas direpresentasikan oleh sebuah object.

## 3.3 Object

Object adalah struktur data yang digunakan untuk menyimpan data dalam bentuk pasangan key dan value (properti dan nilainya).

Contoh:

```js
const siswa = {
  nama: "Maul",
  umur: 16,
  kelas: "11A",
};
```

Penjelasan:

- `nama`, `umur`, dan `kelas` merupakan key/properti.
- `"Maul"`, `16`, dan `"11A"` merupakan value.

Mengakses properti:

```js
console.log(siswa.nama);
console.log(siswa.umur);
```

Dalam project, setiap tugas menggunakan object:

```js
{
  id: 1,
  title: "Pelajari array dan object",
  completed: false
}
```

Penjelasan setiap properti:

| Properti    | Kegunaan                    |
| ----------- | --------------------------- |
| `id`        | Identitas unik setiap tugas |
| `title`     | Judul tugas                 |
| `completed` | Status penyelesaian tugas   |

Kenapa menggunakan object?

Karena satu tugas memiliki beberapa informasi yang saling berhubungan.

Daripada menyimpan judul dan status dalam array terpisah, kita bisa mengelompokkannya dalam satu object.

## 3.4 Boolean

Boolean adalah tipe data yang hanya memiliki dua nilai:

```js
true;
false;
```

Dalam project:

```js
completed: false;
```

Artinya tugas tersebut belum selesai.

Sedangkan:

```js
completed: true;
```

Artinya tugas sudah selesai.

Boolean sangat berguna untuk membuat kondisi.

Contoh:

```js
const sudahSelesai = true;

if (sudahSelesai) {
  console.log("Tugas sudah selesai");
}
```

---

# 4. Memahami Method Array

Project ini menggunakan beberapa method array yang sangat penting.

## 4.1 `push()`

`push()` digunakan untuk menambahkan data baru ke bagian akhir array.

Contoh:

```js
const angka = [1, 2, 3];

angka.push(4);

console.log(angka);
```

Hasil:

```js
[1, 2, 3, 4];
```

Dalam project:

```js
tasks.push({
  id: nextId,
  title: judul,
  completed: false,
});
```

Artinya, object tugas baru dimasukkan ke bagian akhir array `tasks`.

Kenapa menggunakan `push()`?

Karena setiap kali pengguna menambahkan tugas, data baru harus disimpan ke dalam array.

## 4.2 `find()`

`find()` digunakan untuk mencari satu elemen dalam array berdasarkan kondisi tertentu.

Contoh:

```js
const angka = [10, 20, 30, 40];

const hasil = angka.find((nilai) => nilai === 30);

console.log(hasil);
```

Hasil:

```text
30
```

`find()` akan mengembalikan elemen pertama yang memenuhi kondisi.

Jika tidak ditemukan, hasilnya adalah `undefined`.

Dalam project:

```js
const tugas = tasks.find((task) => task.id === id);
```

Artinya, JavaScript mencari object tugas yang memiliki `id` sama dengan parameter `id`.

Contoh:

```js
tasks.find((task) => task.id === 2);
```

JavaScript akan mencari tugas yang memiliki ID 2.

Kenapa menggunakan `find()`?

Karena ketika pengguna menekan tombol selesai, JavaScript harus mengetahui tugas mana yang perlu diubah statusnya.

## 4.3 `filter()`

`filter()` digunakan untuk membuat array baru yang hanya berisi elemen-elemen yang memenuhi kondisi tertentu.

Contoh:

```js
const angka = [10, 15, 20, 25, 30];

const hasil = angka.filter((nilai) => nilai >= 20);

console.log(hasil);
```

Hasil:

```js
[20, 25, 30];
```

Dalam project, `filter()` digunakan untuk menghapus tugas:

```js
const hasilFilter = tasks.filter((task) => task.id !== id);

tasks = hasilFilter;
```

Penjelasan:

Misalnya array `tasks` memiliki ID:

```js
[1, 2, 3];
```

Kemudian pengguna menghapus tugas dengan ID 2.

Kondisi:

```js
task.id !== 2;
```

Artinya, hanya tugas yang ID-nya tidak sama dengan 2 yang dipertahankan.

Hasil array baru:

```js
[1, 3];
```

Kemudian:

```js
tasks = hasilFilter;
```

Array `tasks` diganti menggunakan hasil filter tersebut.

**Kenapa tidak langsung menggunakan `delete`?**

Karena `filter()` lebih sesuai untuk membuat array baru tanpa elemen yang ingin dihapus.

## 4.4 `forEach()`

`forEach()` digunakan untuk menjalankan suatu fungsi pada setiap elemen array.

Contoh:

```js
const buah = ["Apel", "Jeruk", "Mangga"];

buah.forEach((item) => {
  console.log(item);
});
```

Hasil:

```text
Apel
Jeruk
Mangga
```

Dalam project:

```js
filteredTasks.forEach((item) => {
  // Membuat elemen tugas
});
```

Artinya, JavaScript akan menjalankan isi callback untuk setiap tugas yang ada di `filteredTasks`.

Misalnya terdapat tiga tugas, maka callback dijalankan tiga kali.

Kenapa menggunakan `forEach()`?

Karena setiap tugas harus dibuatkan elemen HTML-nya masing-masing.

**Perbedaan sederhana `forEach()` dan `map()`:**

- `forEach()` digunakan untuk menjalankan proses pada setiap elemen, misalnya menampilkan data.
- `map()` digunakan untuk menghasilkan array baru berdasarkan hasil pengolahan setiap elemen.

Contoh `map()`:

```js
const harga = [10000, 20000, 30000];

const hargaBaru = harga.map((nilai) => nilai + 5000);

console.log(hargaBaru);
```

Hasil:

```js
[15000, 25000, 35000];
```

---

# 5. Memahami Function

Function merupakan blok kode yang dibuat untuk menjalankan tugas tertentu.

Contoh:

```js
function sapa() {
  console.log("Halo!");
}
```

Function tersebut belum berjalan hanya karena dibuat.

Untuk menjalankannya, kita perlu memanggil:

```js
sapa();
```

## 5.1 Parameter dan Argument

Parameter adalah variabel yang ditulis di dalam tanda kurung saat membuat function.

Argument adalah nilai yang diberikan ketika function dipanggil.

Contoh:

```js
function sapa(nama) {
  console.log("Halo " + nama);
}

sapa("Maul");
```

Penjelasan:

- `nama` adalah parameter.
- `"Maul"` adalah argument.

Hasil:

```text
Halo Maul
```

Dalam project:

```js
function tambahTugas(judul) {
  // ...
}
```

`judul` merupakan parameter yang akan menerima judul tugas dari pengguna.

Pemanggilannya:

```js
tambahTugas(input.value);
```

Nilai input pengguna dikirim sebagai argument.

## 5.2 `return`

`return` digunakan untuk mengembalikan nilai dari sebuah function sekaligus menghentikan proses function tersebut.

Contoh:

```js
function tambah(a, b) {
  return a + b;
}

const hasil = tambah(10, 20);

console.log(hasil);
```

Hasil:

```text
30
```

Kenapa hasilnya bisa disimpan ke variabel `hasil`?

Karena function mengembalikan nilai melalui `return`.

### `return` tanpa nilai

Contoh:

```js
function cekNama(nama) {
  if (nama === "") {
    return;
  }

  console.log(nama);
}
```

Ketika nama kosong, function langsung berhenti dan tidak menjalankan `console.log()`.

Dalam project:

```js
if (judul.trim() === "") {
  message.textContent = "Judul tugas tidak boleh kosong";
  return;
}
```

Jika judul kosong, pesan error ditampilkan dan function dihentikan.

Dengan begitu, kode setelah kondisi tersebut tidak dijalankan.

### Perbedaan `return` dan assignment

Assignment adalah proses memberikan nilai kepada variabel.

Contoh:

```js
let angka = 10;

angka = 50;

console.log(angka);
```

Hasil:

```text
50
```

Sedangkan `return` mengembalikan nilai dari function.

Keduanya memiliki fungsi berbeda.

Contoh assignment dalam kondisi:

```js
let angka;

if (true) {
  angka = 100;
}

console.log(angka);
```

Hasil:

```text
100
```

Kita tidak membutuhkan `return` karena tujuannya hanya mengubah nilai variabel.

---

# 6. Memahami Operator dan Kondisi

## 6.1 Operator perbandingan

Operator perbandingan digunakan untuk membandingkan dua nilai. Hasilnya berupa boolean (`true` atau `false`).

| Operator | Arti                            |
| -------- | ------------------------------- |
| `===`    | Sama nilai dan tipe data        |
| `!==`    | Tidak sama nilai atau tipe data |
| `>`      | Lebih besar dari                |
| `<`      | Lebih kecil dari                |
| `>=`     | Lebih besar atau sama dengan    |
| `<=`     | Lebih kecil atau sama dengan    |

Contoh:

```js
console.log(10 === 10);
// true

console.log(10 !== 5);
// true
```

Dalam project:

```js
task.id === id;
```

Artinya, apakah ID tugas sama dengan ID yang sedang dicari?

Sedangkan:

```js
task.id !== id;
```

Artinya, apakah ID tugas tidak sama dengan ID yang ingin dihapus?

## 6.2 Operator logika

Dua operator logika yang sering digunakan:

### AND (`&&`)

Kedua kondisi harus bernilai benar agar hasilnya `true`.

```js
console.log(true && true);
// true

console.log(true && false);
// false
```

### OR (`||`)

Cukup salah satu kondisi bernilai benar agar hasilnya `true`.

```js
console.log(true || false);
// true

console.log(false || false);
// false
```

## 6.3 `if`, `else if`, dan `else`

Digunakan untuk menjalankan kode berdasarkan kondisi.

Contoh:

```js
const nilai = 80;

if (nilai >= 90) {
  console.log("A");
} else if (nilai >= 75) {
  console.log("B");
} else {
  console.log("C");
}
```

JavaScript memeriksa kondisi dari atas ke bawah.

Dalam project, kondisi digunakan untuk menentukan filter:

```js
if (filter.value === "all") {
  filteredTasks = tasks;
} else if (filter.value === "pending") {
  filteredTasks = tasks.filter((task) => task.completed === false);
} else if (filter.value === "done") {
  filteredTasks = tasks.filter((task) => task.completed === true);
}
```

Penjelasan:

- Jika pilihan filter adalah `all`, tampilkan semua tugas.
- Jika pilihan filter adalah `pending`, tampilkan tugas yang belum selesai.
- Jika pilihan filter adalah `done`, tampilkan tugas yang sudah selesai.

**Kenapa menggunakan assignment ke `filteredTasks`?**

Karena kita ingin menentukan array mana yang akan ditampilkan berdasarkan pilihan filter.

Kita tidak perlu menggunakan `return` karena kode ini tidak sedang mengembalikan nilai dari function.

## 6.4 Ternary Operator

Ternary operator merupakan bentuk singkat dari kondisi `if...else`.

Bentuk umum:

```js
kondisi ? nilaiJikaBenar : nilaiJikaSalah;
```

Contoh:

```js
const umur = 18;

const status = umur >= 18 ? "Dewasa" : "Anak-anak";
```

Hasil:

```text
Dewasa
```

Dalam project:

```js
toggleButton.textContent = item.completed ? "Batalkan Selesai" : "Selesaikan";
```

Artinya:

- Jika `item.completed` bernilai `true`, teks tombol menjadi `"Batalkan Selesai"`.
- Jika `false`, teks tombol menjadi `"Selesaikan"`.

Kenapa menggunakan ternary?

Karena kondisi yang dibutuhkan hanya memiliki dua kemungkinan sehingga bisa ditulis lebih ringkas.

---

# 7. Memahami DOM Event

Event adalah kejadian atau interaksi yang dilakukan pengguna terhadap halaman web.

Contohnya:

- Klik tombol.
- Mengetik di input.
- Mengirim form.
- Mengubah pilihan select.

JavaScript dapat mendeteksi kejadian tersebut menggunakan `addEventListener()`.

## 7.1 Apa itu `addEventListener()`?

`addEventListener()` merupakan method untuk memasang pendengar event pada suatu elemen.

Contoh:

```html
<button id="tombol">Klik Saya</button>
```

JavaScript:

```js
const tombol = document.querySelector("#tombol");

tombol.addEventListener("click", () => {
  console.log("Tombol diklik!");
});
```

Ketika tombol diklik, callback function akan dijalankan.

Struktur umumnya:

```js
element.addEventListener("namaEvent", callbackFunction);
```

Penjelasan:

- `element` adalah elemen HTML yang ingin didengarkan.
- `namaEvent` adalah jenis event.
- `callbackFunction` adalah function yang dijalankan ketika event terjadi.

## 7.2 Apa itu Callback Function?

Callback function adalah function yang diberikan sebagai argument kepada function lain untuk dijalankan pada waktu tertentu.

Contoh:

```js
tombol.addEventListener("click", () => {
  console.log("Halo!");
});
```

Function:

```js
() => {
  console.log("Halo!");
};
```

merupakan callback.

Function tersebut tidak langsung dijalankan ketika `addEventListener()` dipasang.

Function baru dijalankan ketika event `click` terjadi.

## 7.3 Apa itu `event`?

Pada event listener, callback dapat menerima objek event sebagai parameter.

Contoh:

```js
form.addEventListener("submit", (event) => {
  console.log(event);
});
```

Parameter `event` berisi informasi tentang kejadian yang terjadi.

Nama `event` sebenarnya bebas. Kita bisa menggunakan nama lain:

```js
form.addEventListener("submit", (e) => {
  console.log(e);
});
```

Keduanya sama saja.

## 7.4 Apa itu `preventDefault()`?

`preventDefault()` merupakan method untuk mencegah perilaku bawaan browser pada suatu event.

Contohnya, ketika form dikirim, browser secara default dapat melakukan proses submit yang menyebabkan halaman dimuat ulang.

Dalam project:

```js
form.addEventListener("submit", (event) => {
  event.preventDefault();

  tambahTugas(input.value);
  input.value = "";
});
```

Kenapa menggunakan `preventDefault()`?

Karena kita ingin mengolah data form menggunakan JavaScript tanpa membuat halaman dimuat ulang.

Jika halaman dimuat ulang, data yang hanya disimpan di array JavaScript bisa kembali ke kondisi awal.

**Penting:** `preventDefault()` tidak menghentikan seluruh kode di dalam callback. Method ini hanya mencegah perilaku bawaan browser.

## 7.5 Perbedaan Event `submit` dan `change`

### `submit`

Event `submit` terjadi ketika form dikirim.

Contoh:

```js
form.addEventListener("submit", (event) => {
  event.preventDefault();

  console.log("Form dikirim");
});
```

Biasanya digunakan untuk memproses data form.

### `change`

Event `change` terjadi ketika nilai suatu elemen berubah dan perubahan tersebut dikonfirmasi.

Contoh:

```js
filter.addEventListener("change", () => {
  console.log("Filter berubah");
});
```

Dalam project, event `change` digunakan untuk mendeteksi perubahan pilihan filter.

---

# 8. Memahami DOM secara Dinamis dalam Project

Bagian ini merupakan salah satu bagian paling penting dalam project Task List.

Kita tidak hanya mengakses elemen HTML yang sudah tersedia, tetapi juga membuat elemen HTML baru melalui JavaScript.

Contohnya:

```js
const taskElement = document.createElement("div");
const titleElement = document.createElement("span");
const toggleButton = document.createElement("button");
const deleteButton = document.createElement("button");
```

Apa yang terjadi?

JavaScript membuat empat elemen baru:

1. `div` sebagai pembungkus tugas.
2. `span` sebagai judul tugas.
3. `button` untuk mengubah status tugas.
4. `button` untuk menghapus tugas.

Selanjutnya, kita memberikan class:

```js
taskElement.classList.add("task");
titleElement.classList.add("task-title");
```

Kemudian memasukkan judul tugas:

```js
titleElement.textContent = item.title;
```

Mengatur teks tombol:

```js
toggleButton.textContent = item.completed ? "Batalkan Selesai" : "Selesaikan";

deleteButton.textContent = "Hapus";
```

Setelah itu, semua elemen disusun menggunakan `appendChild()`:

```js
taskElement.appendChild(titleElement);
taskElement.appendChild(toggleButton);
taskElement.appendChild(deleteButton);

list.appendChild(taskElement);
```

Hasil akhirnya kurang lebih:

```html
<div id="task-list">
  <div class="task">
    <span class="task-title">Belajar JavaScript</span>
    <button>Selesaikan</button>
    <button>Hapus</button>
  </div>
</div>
```

**Kesimpulan bagian ini:**

JavaScript dapat membuat struktur HTML berdasarkan data yang tersimpan dalam array.

Inilah salah satu konsep penting ketika membuat aplikasi interaktif.

---

# 9. Memahami Seluruh Function dalam Project

Sekarang kita bahas fungsi utama yang digunakan dalam aplikasi.

## 9.1 `tambahTugas(judul)`

Function ini bertugas menambahkan tugas baru ke dalam array `tasks`.

```js
function tambahTugas(judul) {
  if (judul.trim() === "") {
    message.textContent = "Judul tugas tidak boleh kosong";
    return;
  }

  message.textContent = "";

  tasks.push({ id: nextId, title: judul, completed: false });
  nextId += 1;

  render();
}
```

Penjelasan setiap bagian:

**1. Memeriksa judul**

```js
if (judul.trim() === "") {
```

`trim()` merupakan method string yang menghapus spasi di awal dan akhir teks.

Contoh:

```js
const nama = "   Maul   ";

console.log(nama.trim());
```

Hasil:

```text
Maul
```

Kenapa menggunakan `trim()`?

Karena pengguna mungkin memasukkan teks yang hanya berisi spasi.

Contohnya:

```text
"       "
```

Jika hanya memeriksa apakah input kosong, teks yang berisi spasi masih dianggap memiliki karakter.

Dengan `trim()`, teks tersebut menjadi string kosong.

**2. Menampilkan pesan error**

```js
message.textContent = "Judul tugas tidak boleh kosong";
```

Pesan ditampilkan melalui elemen HTML yang sudah diakses menggunakan DOM.

**3. Menghentikan function**

```js
return;
```

Jika judul tidak valid, proses penambahan tugas dihentikan.

**4. Menghapus pesan error**

```js
message.textContent = "";
```

Jika judul valid, pesan error sebelumnya dibersihkan.

**5. Menambahkan tugas**

```js
tasks.push({
  id: nextId,
  title: judul,
  completed: false,
});
```

Object baru dimasukkan ke dalam array.

**6. Menambahkan ID**

```js
nextId += 1;
```

Nilai `nextId` bertambah satu agar tugas berikutnya memiliki ID berbeda.

Contoh:

- Tugas pertama mendapatkan ID 1.
- Tugas kedua mendapatkan ID 2.
- Tugas ketiga mendapatkan ID 3.

**7. Memperbarui tampilan**

```js
render();
```

Setelah data berubah, tampilan halaman diperbarui agar tugas baru muncul.

## 9.2 `toggleTugas(id)`

Function ini digunakan untuk mengubah status tugas.

```js
function toggleTugas(id) {
  const tugas = tasks.find((task) => task.id === id);

  if (tugas) {
    tugas.completed = !tugas.completed;
    render();
  }
}
```

**1. Mencari tugas berdasarkan ID**

```js
const tugas = tasks.find((task) => task.id === id);
```

JavaScript mencari object tugas yang memiliki ID sesuai argument.

**2. Memeriksa apakah tugas ditemukan**

```js
if (tugas) {
```

Jika tugas ditemukan, kondisi bernilai `true`.

Jika tidak ditemukan, nilainya `undefined` sehingga kondisi tidak dijalankan.

**3. Membalik status tugas**

```js
tugas.completed = !tugas.completed;
```

Operator `!` digunakan untuk membalik nilai boolean.

Contoh:

```js
let status = false;

status = !status;

console.log(status);
```

Hasil:

```text
true
```

Jika awalnya `true`, maka berubah menjadi `false`.

Jadi, ketika tombol diklik:

- Tugas yang belum selesai menjadi selesai.
- Tugas yang sudah selesai menjadi belum selesai.

**4. Memperbarui tampilan**

```js
render();
```

Setelah status berubah, tampilan diperbarui.

## 9.3 `hapusTugas(id)`

Function ini digunakan untuk menghapus tugas berdasarkan ID.

```js
function hapusTugas(id) {
  const hasilFilter = tasks.filter((task) => task.id !== id);

  tasks = hasilFilter;

  render();
}
```

**1. Membuat array baru**

```js
const hasilFilter = tasks.filter((task) => task.id !== id);
```

`filter()` membuat array baru yang hanya berisi tugas dengan ID berbeda dari ID yang ingin dihapus.

**2. Memperbarui array utama**

```js
tasks = hasilFilter;
```

Array `tasks` diganti dengan hasil filter.

**3. Memperbarui tampilan**

```js
render();
```

Setelah data diperbarui, tugas yang dihapus tidak akan ditampilkan lagi.

## 9.4 `render()`

Ini merupakan salah satu function paling penting dalam project.

```js
function render() {
  // Menghitung data
  // Mengatur tampilan angka
  // Memfilter tugas
  // Membuat elemen HTML
  // Memasang event listener
}
```

Apa tugas utama `render()`?

`render()` bertugas menampilkan kondisi terbaru dari data aplikasi ke halaman HTML.

Misalnya:

- Ada tugas baru → tampilkan tugas baru.
- Tugas dihapus → hilangkan tugas tersebut.
- Status berubah → perbarui tampilan tugas.
- Filter berubah → tampilkan tugas sesuai filter.

### A. Menghitung jumlah tugas

```js
const total = tasks.length;
```

`length` merupakan properti untuk mengetahui jumlah elemen dalam array.

Contoh:

```js
const angka = [10, 20, 30];

console.log(angka.length);
```

Hasil:

```text
3
```

Dalam project, `tasks.length` menghitung seluruh tugas.

### B. Menghitung tugas yang belum selesai

```js
const pending = tasks.filter((task) => task.completed === false).length;
```

Penjelasan:

1. `filter()` mengambil tugas yang `completed` bernilai `false`.
2. Hasil filter berupa array baru.
3. `length` menghitung jumlah tugas dalam array tersebut.

### C. Menghitung tugas yang sudah selesai

```js
const done = tasks.filter((task) => task.completed === true).length;
```

Logikanya sama, tetapi kondisi yang dicari adalah `true`.

### D. Menampilkan angka ke HTML

```js
totalCount.textContent = total;
pendingCount.textContent = pending;
doneCount.textContent = done;
```

Nilai hasil perhitungan dimasukkan ke elemen HTML.

### E. Mengosongkan daftar tugas

```js
list.innerHTML = "";
```

`innerHTML` merupakan properti untuk membaca atau mengubah isi HTML suatu elemen.

Ketika diberikan string kosong, seluruh isi di dalam elemen tersebut dihapus.

Kenapa dilakukan sebelum membuat daftar tugas lagi?

Karena `render()` bisa dipanggil berkali-kali.

Misalnya, pengguna menekan tombol selesai. `render()` dipanggil lagi.

Jika daftar lama tidak dikosongkan, elemen tugas yang lama bisa tetap ada dan kemudian dibuat lagi. Akibatnya, tugas bisa tampil berulang.

Dengan mengosongkan daftar terlebih dahulu, kita memastikan bahwa elemen yang ditampilkan merupakan hasil render terbaru.

**Catatan keamanan:** `innerHTML` dapat digunakan untuk memasukkan HTML, tetapi perlu hati-hati jika memasukkan teks yang berasal dari pengguna. Dalam project ini, judul tugas lebih aman ditampilkan menggunakan `textContent`.

### F. Menyiapkan array hasil filter

```js
let filteredTasks = [];
```

Variabel ini akan menyimpan daftar tugas yang nantinya ditampilkan.

Kenapa menggunakan `let`?

Karena nilainya akan diisi ulang berdasarkan pilihan filter.

### G. Memeriksa pilihan filter

```js
if (filter.value === "all") {
  filteredTasks = tasks;
} else if (filter.value === "pending") {
  filteredTasks = tasks.filter((task) => task.completed === false);
} else if (filter.value === "done") {
  filteredTasks = tasks.filter((task) => task.completed === true);
}
```

`filter.value` mengambil nilai yang sedang dipilih oleh pengguna pada elemen select.

Contohnya, HTML:

```html
<select id="filter">
  <option value="all">Semua</option>
  <option value="pending">Belum Selesai</option>
  <option value="done">Selesai</option>
</select>
```

Jika pengguna memilih "Belum Selesai", maka:

```js
filter.value;
```

menghasilkan:

```text
pending
```

JavaScript kemudian mengambil tugas yang belum selesai.

### H. Mengulang setiap tugas

```js
filteredTasks.forEach((item) => {
  // Membuat elemen HTML
});
```

Setiap object tugas akan diproses satu per satu.

Parameter `item` mewakili object tugas yang sedang diproses.

Contoh jika data:

```js
[
  { id: 1, title: "Belajar HTML", completed: false },
  { id: 2, title: "Belajar CSS", completed: true },
];
```

Maka `forEach()` dijalankan dua kali:

- Pertama, `item` berisi tugas Belajar HTML.
- Kedua, `item` berisi tugas Belajar CSS.

### I. Membuat elemen HTML

```js
const taskElement = document.createElement("div");
const titleElement = document.createElement("span");
const toggleButton = document.createElement("button");
const deleteButton = document.createElement("button");
```

Setiap tugas mendapatkan elemen HTML sendiri.

### J. Memberikan class CSS

```js
taskElement.classList.add("task");
titleElement.classList.add("task-title");

if (item.completed) {
  taskElement.classList.add("done");
}
```

Class diberikan sesuai kebutuhan styling.

Jika tugas sudah selesai, class `done` ditambahkan.

### K. Memasukkan judul tugas

```js
titleElement.textContent = item.title;
```

Judul dari object tugas dimasukkan ke elemen span.

### L. Mengatur teks tombol

```js
toggleButton.textContent = item.completed ? "Batalkan Selesai" : "Selesaikan";

deleteButton.textContent = "Hapus";
```

Teks tombol disesuaikan dengan kondisi tugas.

### M. Menyusun elemen HTML

```js
taskElement.appendChild(titleElement);
taskElement.appendChild(toggleButton);
taskElement.appendChild(deleteButton);

list.appendChild(taskElement);
```

Elemen-elemen yang sudah dibuat disusun menjadi satu struktur HTML.

### N. Memasang event listener

```js
toggleButton.addEventListener("click", () => {
  toggleTugas(item.id);
});

deleteButton.addEventListener("click", () => {
  hapusTugas(item.id);
});
```

Setiap tugas mempunyai tombol sendiri.

Ketika tombol selesai diklik, JavaScript memanggil `toggleTugas()` dengan ID tugas yang sesuai.

Ketika tombol hapus diklik, JavaScript memanggil `hapusTugas()` dengan ID tugas yang sesuai.

**Kenapa menggunakan `item.id`?**

Karena setiap tugas memiliki ID yang berbeda. Dengan begitu, JavaScript mengetahui tugas mana yang harus diubah atau dihapus.

---

# 10. Memahami Alur Keseluruhan Aplikasi

Sekarang kita gabungkan semua konsep tadi.

## 10.1 Ketika halaman pertama kali dibuka

JavaScript menjalankan:

```js
render();
```

Prosesnya:

1. Menghitung jumlah tugas.
2. Menghitung tugas yang selesai.
3. Menghitung tugas yang belum selesai.
4. Menampilkan angka ke HTML.
5. Mengosongkan daftar tugas sebelumnya.
6. Memeriksa pilihan filter.
7. Mengulang data tugas.
8. Membuat elemen HTML untuk setiap tugas.
9. Memasukkan elemen ke dalam halaman.
10. Memasang event listener pada tombol.

## 10.2 Ketika pengguna menambahkan tugas

Alurnya:

```text
Pengguna mengetik judul
        |
        v
Pengguna mengirim form
        |
        v
Event submit dijalankan
        |
        v
preventDefault()
        |
        v
tambahTugas(input.value)
        |
        v
Memeriksa apakah judul kosong
        |
        v
Jika valid, data masuk ke array tasks
        |
        v
nextId bertambah
        |
        v
render() dijalankan
        |
        v
Tugas baru muncul di halaman
```

## 10.3 Ketika pengguna menyelesaikan tugas

```text
Pengguna klik tombol Selesaikan
        |
        v
Event click dijalankan
        |
        v
toggleTugas(item.id)
        |
        v
find() mencari tugas berdasarkan ID
        |
        v
completed dibalik menggunakan !
        |
        v
render() dijalankan
        |
        v
Tampilan tugas diperbarui
```

## 10.4 Ketika pengguna menghapus tugas

```text
Pengguna klik tombol Hapus
        |
        v
Event click dijalankan
        |
        v
hapusTugas(item.id)
        |
        v
filter() membuat array tanpa tugas tersebut
        |
        v
tasks diperbarui
        |
        v
render() dijalankan
        |
        v
Tugas yang dihapus menghilang
```

## 10.5 Ketika pengguna mengganti filter

```text
Pengguna memilih filter
        |
        v
Event change dijalankan
        |
        v
render() dijalankan
        |
        v
JavaScript membaca filter.value
        |
        v
Memilih data sesuai filter
        |
        v
Membuat ulang tampilan daftar tugas
```

---

# 11. Kenapa `render()` Dipanggil Berkali-kali?

Pertanyaan ini penting karena `render()` menjadi pusat pembaruan tampilan aplikasi.

Dalam project ini, data disimpan dalam array JavaScript:

```js
let tasks = [];
```

Sementara itu, pengguna melihat hasilnya melalui HTML.

Artinya, ada dua hal yang perlu dijaga agar tetap sesuai:

1. Data aplikasi.
2. Tampilan halaman.

Contoh:

```js
tasks.push({
  id: 3,
  title: "Belajar DOM",
  completed: false,
});
```

Data sudah bertambah, tetapi HTML tidak otomatis membuat elemen baru hanya karena array berubah.

Karena itu, kita memanggil:

```js
render();
```

Supaya tampilan HTML dibuat ulang berdasarkan data terbaru.

Konsep sederhananya:

```text
Data berubah
    |
    v
render()
    |
    v
DOM diperbarui
```

Ini merupakan pola dasar yang juga akan sering ditemui ketika mempelajari framework JavaScript.

Framework seperti React memiliki pendekatan tersendiri untuk mengelola perubahan data dan tampilan. Namun, memahami proses manual menggunakan DOM seperti project ini akan membantu kita memahami konsep dasarnya terlebih dahulu.

---

# 12. Kumpulan Method dan Properti yang Digunakan

Berikut rangkuman method dan properti yang digunakan dalam project.

| Method / Properti    | Kegunaan                                       |
| -------------------- | ---------------------------------------------- |
| `querySelector()`    | Mengambil elemen HTML                          |
| `textContent`        | Membaca atau mengubah teks                     |
| `createElement()`    | Membuat elemen HTML                            |
| `appendChild()`      | Memasukkan elemen ke elemen lain               |
| `classList.add()`    | Menambahkan class CSS                          |
| `classList.remove()` | Menghapus class CSS                            |
| `classList.toggle()` | Menambah atau menghapus class                  |
| `addEventListener()` | Memasang event listener                        |
| `preventDefault()`   | Mencegah perilaku bawaan browser               |
| `push()`             | Menambahkan data ke array                      |
| `find()`             | Mencari satu elemen array                      |
| `filter()`           | Membuat array baru berdasarkan kondisi         |
| `forEach()`          | Mengulang setiap elemen array                  |
| `map()`              | Menghasilkan array baru dari hasil pemrosesan  |
| `trim()`             | Menghapus spasi di awal dan akhir string       |
| `length`             | Menghitung jumlah elemen atau panjang string   |
| `innerHTML`          | Membaca atau mengubah isi HTML                 |
| `value`              | Mengambil nilai input atau select              |
| `completed`          | Properti status tugas                          |
| `return`             | Mengembalikan nilai atau menghentikan function |

---

# 13. Hal yang Perlu Diingat

Beberapa konsep penting yang harus dipahami dari project ini:

1. Membuat elemen menggunakan `createElement()` tidak otomatis membuat elemen tersebut muncul di halaman.
2. `appendChild()` digunakan untuk memasukkan elemen ke dalam elemen lain.
3. `textContent` digunakan untuk mengatur teks, bukan membuat struktur HTML.
4. `querySelector()` digunakan untuk mengambil elemen berdasarkan CSS selector.
5. `addEventListener()` digunakan untuk mendeteksi interaksi pengguna.
6. `preventDefault()` mencegah perilaku bawaan browser, bukan menghentikan seluruh kode.
7. `filter()` menghasilkan array baru dan tidak menghapus data dari array awal secara langsung.
8. `find()` mencari satu elemen, sedangkan `filter()` bisa menghasilkan banyak elemen.
9. `forEach()` menjalankan callback untuk setiap elemen array.
10. `return` dapat menghentikan function sehingga kode setelahnya tidak dijalankan.
11. Perubahan pada array tidak otomatis mengubah tampilan HTML.
12. `render()` digunakan untuk memperbarui tampilan berdasarkan data terbaru.

---

# 14. Latihan Pemahaman

Bagian ini bisa digunakan untuk menguji apakah konsep-konsep di atas sudah benar-benar dipahami.

Usahakan menjawab tanpa langsung melihat bagian penjelasan sebelumnya.

### A. Dasar DOM

1. Apa itu DOM?
2. Apa perbedaan `document.querySelector()` dengan `textContent`?
3. Kenapa `createElement()` saja belum cukup untuk menampilkan elemen HTML?
4. Apa fungsi `appendChild()`?
5. Apa perbedaan `classList.add()` dengan `classList.toggle()`?

### B. JavaScript Dasar

6. Apa perbedaan `let` dan `const`?
7. Apa perbedaan array dan object?
8. Kenapa setiap tugas menggunakan properti `id`, `title`, dan `completed`?
9. Apa perbedaan parameter dan argument?
10. Apa fungsi `return`?

### C. Array

11. Apa perbedaan `find()` dan `filter()`?
12. Kenapa `filter()` digunakan untuk menghapus tugas?
13. Apa fungsi `forEach()` dalam function `render()`?
14. Apa perbedaan `forEach()` dan `map()`?
15. Apa yang terjadi jika `tasks.push()` dijalankan?

### D. Event dan Interaksi

16. Apa fungsi `addEventListener()`?
17. Apa itu callback function?
18. Kenapa form menggunakan event `submit`?
19. Kenapa kita menggunakan `event.preventDefault()`?
20. Apa perbedaan event `submit` dan `change`?

### E. Memahami Alur Project

21. Kenapa `render()` dipanggil setelah tugas ditambahkan?
22. Kenapa `list.innerHTML = ""` dijalankan sebelum membuat elemen tugas?
23. Bagaimana cara kerja `toggleTugas()`?
24. Kenapa `item.id` dikirim ke `hapusTugas()`?
25. Apa yang akan terjadi jika `render()` tidak dipanggil setelah data berubah?

---

# 15. Penutup

Project Task List ini bukan hanya latihan membuat aplikasi sederhana, tetapi juga latihan memahami bagaimana JavaScript bekerja bersama HTML melalui DOM.

Hal paling penting yang perlu dipahami bukan sekadar menghafal nama method, melainkan mengetahui:

- Data apa yang sedang diolah?
- Elemen HTML mana yang sedang diakses?
- Kenapa elemen baru perlu dibuat?
- Bagaimana event pengguna menjalankan function?
- Bagaimana perubahan data memengaruhi tampilan?

Jika sudah memahami alur tersebut, kita akan lebih mudah mempelajari konsep yang lebih kompleks, termasuk manipulasi DOM yang lebih lanjut dan framework JavaScript.

**Catatan:** README ini merupakan dokumentasi belajar dari project Task List (GabutZ Azzah). Tidak semua konsep JavaScript dan DOM dibahas di sini. Fokus utamanya adalah konsep yang digunakan dalam project ini dan alasan penggunaannya.
