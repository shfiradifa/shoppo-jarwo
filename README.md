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