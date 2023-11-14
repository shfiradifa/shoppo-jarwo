# Tugas 7

## Perbedaan utama antara stateless dan statefull widget dalam konteks pengembangan aplikasi flutter
Dalam konteks pengembangan aplikasi flutter, `StatelessWidget` dan `StatefullWidget` memiliki beberapa perbedaan utama dalam mengatur kondisi atau state dari widget tersebut, yaitu:
- `Stateless Widget` bersifat statis, sedangkan `Stateful Widget` bersifat dinamis.
- `Stateless Widget` memiliki 1 objek yang mewakilinya, sedangkan `Statefull Widget` memiliki 2 objek yang mewakilinya, yaitu statefull widget itu sendiri dan objek state yang mengelola keadaannya.
- `Stateless Widget` tidak dapat dilakukan perubahan atau pembaruan tampilan, sedangkan `Statefull Widget` masih dapat dilakukan perubahan atau pembaruan tampilan setiap saat.

## Widget yang digunakan pada Tugas 7
- `MyApp`: Berfungsi me-manage aspek-aspek penting dari `MaterialApp` seperti, gesture, navigasi, tema, dan konfigurasi lainnya.
- `MyHomePage`: Berfungsi sebagai halaman utama aplikasi yang me-return `Scaffold` yang berisi struktur layout dasar seperti floating action button, body, app bar, dan lainnya.
- `SingleChildScrollView`: Berfungsi untuk dapat membuat konten yang melebihi ukuran layar dapat di-scroll secara vertikal atau horizontal. Widget ini yang membungkus `Padding` yang berisi `Column`. Dalam hal ini, digunakan dalam memberi jarak pada seluruh sisi konten dengan pinggiran layar.
- `Padding`: Berfungsi mengatur jarak pada bagian semua sisi, atas, kanan, bawah, ataupun kiri dari widget child.
- `Column`: Berfungsi mengatur letak/posisi widget secara vertikal. Dalam hal ini, digunakan dalam menampilkan judul dan grid layout.
- `Text`: Berfungsi menampilkan teks dengan pengaturan gaya, ukuran, warna, atau lainnya. Dalam hal ini, digunakan dalam judul `PBP Shop`.
- `GridView.count`: Berfungsi menampilkan widget child yang berbentuk grid dengan jumlah kolom statis. Dalam hal ini, digunakan untuk menampilkan tiga button dengan teks dan icon.
- `ShopCard`: Berfungsi menampilkan tiap item-nya dalam grid layout dengan ikon, teks, dan warna yang sesuai. Dalam hal ini, digunakan untuk menampilkan `InkWell` dan `Container` dari sebuah `Material`.
- `Material`: Berfungsi memberikan visual effect Material Design pada widget, seperti warna, bentuk, atau elevasi. Dalam hal ini, digunakan dalam memberi warna untuk setiap item yang disusun dalam grid layout
- `InkWell`: Berfungsi memberikan visual effect ketika user menyentuh widget child. Dalam hal ini, digunakan untuk memberikan respons saat user meng-click sebuah item dalam grid layout.
- `Container`: Berfungsi menampung dan mengatur dekorasi seperti padding, border, margin, warna, background, dan lainnya pada widget child.
- `Center`: Berfungsi mengatur posisi widget child untuk berada di tengah layar.
- `Icon`: Berfungsi menampilkan icon beserta dekorasinya enggunakan properti size, color, opacity, dan lainnya.

## Implementasi Checklist
1. Membuat direktori `shoppo-jarwo`
2. Meng-generate project baru flutter dengan nama `shoppo_jarwo` dengan perintah `flutter create shoppo_jarwo`
3. Membuat file `menu.dart` dalam sub-direktori `lib` dan meng-import package `material.dart` dari `flutter` di dalamnya.
4. Pada file `main.dart` dalam sub-direktori `lib` saya meng-import `menu.dart` dari `shoppo_jarwo` dan memindahkan class `MyHomePage` beserta `_MyHomePageState` ke dalam file `medu.dart` sebelumnya.
5. Mengganti widget pada `menu.dart` yang semula statefull menjadi stateless. Kemudian saya menambahkan beberapa widget, seperti card dan teks dengan kode sebagai berikut:
```
import 'package:flutter/material.dart';

class MyHomePage extends StatelessWidget {
    MyHomePage({Key? key}) : super(key: key);

    final List<ShopItem> items = [
        ShopItem("Lihat Produk", Icons.checklist, Colors.lightGreen),
        ShopItem("Tambah Produk", Icons.add_shopping_cart, Colors.pink),
        ShopItem("Logout", Icons.logout, Colors.deepPurple),
    ];

    @override
    Widget build(BuildContext context) {
        return Scaffold(
          appBar: AppBar(
            title: const Text(
              'Shoppo Jarwo',
            ),
          ),
          body: SingleChildScrollView(
            // Widget wrapper yang dapat discroll
            child: Padding(
              padding: const EdgeInsets.all(10.0), // Set padding dari halaman
              child: Column(
                // Widget untuk menampilkan children secara vertikal
                children: <Widget>[
                  const Padding(
                    padding: EdgeInsets.only(top: 10.0, bottom: 10.0),
                    // Widget Text untuk menampilkan tulisan dengan alignment center dan style yang sesuai
                    child: Text(
                      'PBP Shop', // Text yang menandakan toko
                      textAlign: TextAlign.center,
                      style: TextStyle(
                        fontSize: 30,
                        fontWeight: FontWeight.bold,
                      ),
                    ),
                  ),
                  // Grid layout
                  GridView.count(
                    // Container pada card kita.
                    primary: true,
                    padding: const EdgeInsets.all(20),
                    crossAxisSpacing: 10,
                    mainAxisSpacing: 10,
                    crossAxisCount: 3,
                    shrinkWrap: true,
                    children: items.map((ShopItem item) {
                      // Iterasi untuk setiap item
                      return ShopCard(item);
                    }).toList(),
                  ),
                ],
              ),
            ),
          ),
        );
    }
}

class ShopItem {
  final String name;
  final IconData icon;
  final Color color;

  ShopItem(this.name, this.icon, this.color);
}

class ShopCard extends StatelessWidget {
  final ShopItem item;

  const ShopCard(this.item, {super.key}); // Constructor

  @override
  Widget build(BuildContext context) {
    return Material(
      color: item.color,
      child: InkWell(
        // Area responsive terhadap sentuhan
        onTap: () {
          // Memunculkan SnackBar ketika diklik
          ScaffoldMessenger.of(context)
            ..hideCurrentSnackBar()
            ..showSnackBar(SnackBar(
                content: Text("Kamu telah menekan tombol ${item.name}!")));
        },
        child: Container(
          // Container untuk menyimpan Icon dan Text
          padding: const EdgeInsets.all(8),
          child: Center(
            child: Column(
              mainAxisAlignment: MainAxisAlignment.center,
              children: [
                Icon(
                  item.icon,
                  color: Colors.white,
                  size: 30.0,
                ),
                const Padding(padding: EdgeInsets.all(3)),
                Text(
                  item.name,
                  textAlign: TextAlign.center,
                  style: const TextStyle(color: Colors.white),
                ),
              ],
            ),
          ),
        ),
      ),
    );
  }
}
```
## Implementasi BONUS
[![image.png](https://ibb.co/xLMwp9C)](https://ibb.co/xLMwp9C)

# Tugas 8

## Jelaskan perbedaan antara `Navigator.push()` dan `Navigator.pushReplacement()`, disertai dengan contoh mengenai penggunaan kedua metode tersebut yang tepat!
Perbedaan antara keduanya terletak pada apa yang dilakukan kepada route yang berada pada atas stack. Method `Navigator.push()` akan memunculkan dan menampilkan route yang baru saja ditambahkan. Sedangakan method `Navigator.pushReplacement()` akan memindahkan halaman dari route yang sedang ditampilkan kepada pengguna ke suatu route yang diberikan.

Contoh penggunaan method `Navigator.push()` berada pada button **Tambah Produk** yang akan memunculkan halaman form setelah button tersebut ditekan. Contoh penggunaan method `Navigator.pushReplacement()` berada pada button list drawer **Halaman Utama** yang akan memindahkan halaman ketika sebelum di-klik ke halaman `MyHomePage()`.

## Jelaskan masing-masing layout widget pada Flutter dan konteks penggunaannya masing-masing!
1. **Container**: Sebagai wadah untuk menampung child widget dengan tampilan yang rapi dan teratur dengan efek visual tertentu (ukuran, warna, margin, padding, border, atau lainnya).
2. **Row dan Column**: Untuk menyusun child widget secara horizontal atau vertikal.
3. **Stack**: Untuk menyusun child secara bertumpukan dengan efek transparansi, shaddow, dan gradient.
4. **Padding**: Untuk memberikan jarak antara child widget dengan batas widget lainnya.
5. **Expanded**: Untuk membuat child widget mengisi space yang terdapat di dalam Row, Column, atau Flex agar dapat menciptakan ruang tampilan yang proporsional antara child widget.
6. **GridView**: Untuk menampilkan komponen atau child widget dalam bentuk grid sehingga tampilannya menjaid lebih terstruktur dan rapi. Cocok untuk data yang banyak dan beragam.
7. **ListView**: Merupakan salah satu widget scrolling yang paling umum digunakan. Dapat berisi banyak child widget dan mengatur alignment, scroll direction, dan separation child widget sehingga memungkinkan tampilan data yang panjang dan berurut.

## Sebutkan apa saja elemen input pada form yang kamu pakai pada tugas kali ini dan jelaskan mengapa kamu menggunakan elemen input tersebut!
1. **TextFormField**: Elemen input untuk memasukkan teks. Pada aplikasi Flutter ini digunakan untuk variable `_name` dan `_amount` yang bertipe data string dan integer. TextFormField ini memiliki validator yang berguna untuk memastikan bahwa field harus terisi sesuai dengan tipe datanya masing-masing.
2. **ElevatedButton**: Elemen input sebagai button untuk menyimpan form. Pada aplikasi Flutter ini digunakan ketika button `Save` ditekan, maka seluruh value dari field akan diperiksa validasinya melalui `_formKey.currentState!.validate()`. Jika sudah tervalidasi, maka akan ditampilkan informasi message bahwa produk berhasil tersimpan.

## Bagaimana penerapan clean architecture pada aplikasi Flutter?
1. **Lapisan domain**: Membangun lapisan domain yang menjadi pusat dari aplikasi yang mengandung model data dan logika bisnis.
2. **Lapisan aplikasi**: Menggunakan lapisan aplikasi yang merealisasikan kasus penggunaan aplikasi dan menghubungkan lapisan infrastruktur dengan presentasi.
3. **Lapisan infrastruktur**: Menyusun lapisan infrastruktur yang menangani interaksi dengan dunia luar seperti database, web server, user interface.
4. **Lapisan presentasi**: Mendesain lapisan presentasi yang berisi kode yang merender interface pengguna di mana request dibuat dan me-return respons.


## Implementasi checklist
### 1. Menambahkan Drawer Menu Untuk Navigasi
Untuk memudahkan navigasi ke halaman-halaman lainnya, saya menambahkan drawer pada bagian kiri halaman di aplikasi Flutter. Pertama-tama saya membuat berkas `left_drawer.dart` dalam folder baru `widgets`. Pada berkas ini akan diisi dengan fungsi untuk menampilkan fitur navigasi yang terdiri dari header dan set list menu (Halaman Utama & Tambah Produk). Kemudian, kedua menu di-routing ke halamannya masing-masing menggunakan Navigator Push Replacement. Menu **Halaman Utama** di-routing ke `MyHomePage()` dan **Tambah Produk** di-routing ke `ShopFormPage()`.

### 2. Menambahkan Form dan Elemen Input serta Memunculkan Data
Untuk memasukkan data barang pada aplikasi, saya membuat form sederhana dengan parameter `_name`, `_amount`, dan `_description`. Pertama-tama saya membuat berkas `shoplist_form.dart` dalam folder baru `screens`. Karena sebelumnya telah membuat drawer, maka kita perlu meng-import berkas `left_drawer.dart`. Saya menggunakan widget `Form` sebagai wadah bagi beberapa input field widget nantinya. Pada widget ini akan diisi `key` berupa variable baru bernama `_formKey` yang akan menjadi handler dari form state, validasi form, dan penyimpanan form. Selanjutnya, untuk membuat child widget di dalamnya menjadi scrollable, saya menggunakan widget `SingleChildScrollView`. Lalu, untuk `children` akan diisi 3 `TextFormField` untuk nama, harga, dan deskripsi produk. Kemudian, saya menambahkan button `Save` untuk menyimpan produk dengan validasi setiap value input tidak boleh kosong. Selain itu, saya juga menambahkan pop-up tampilan nama, harga, dan deskripsi produk sesaat ketika telah melakukan tap button `Save`.

### 3. Menambahkan Fitur Navigasi pada Tombol
Untuk menambahkan fitur navigasi pada tiga button widget ketika ditekan, pada berkas `menu.dart` dilakukan penambahan kode yang terletak pada atribut `onTap` dari `InkWell` dengan menggunakan Navigator Push.

### 4. Refactoring File
Terakhir saya melakukan refactoring file dengan memisahkan isi widget `ShopItem` pada berkas `menu.dart` ke dalam berkas baru yang bernama `shop_card.dart`. Kemudian, berkas tersebut akan dimasukkan ke folder `widgets` dengan meng-import `shoplist_form.dart`. Setelah itu, pindahkan berkas `menu.dart` ke dalam folder `screens`.