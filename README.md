# Praktikum Menerapkan Plugin di Project Flutter

## Langkah 1: Buat Project Baru
Membuat sebuah project flutter baru dengan nama flutter_plugin_pubdev.
<img src = img\JS7-1.png>

Menjadikan repository di GitHub Anda dengan nama flutter_plugin_pubdev.
<img src = img\JS7-1-1.png>

## Langkah 2: Menambahkan Plugin
Tambahkan plugin auto_size_text menggunakan perintah berikut di terminal
<img src = img\JS7-2.png>

Jika berhasil, maka akan tampil nama plugin beserta versinya di file pubspec.yaml pada bagian dependencies.
<img src = img\JS7-2-1.png>

## Langkah 3: Buat file red_text_widget.dart
Membuat file baru bernama red_text_widget.dart di dalam folder lib.
<img src = img\JS7-3.png>

## Langkah 4: Tambah Widget AutoSizeText
Mengubah kode return Container()

```dart
import 'package:flutter/material.dart';

class RedTextWidget extends StatelessWidget {
  const RedTextWidget({Key? key}) : super(key: key);

  @override
  Widget build(BuildContext context) {
    return AutoSizeText(
      text,
      style: const TextStyle(color: Colors.red, fontSize: 14),
      maxLines: 2,
      overflow: TextOverflow.ellipsis,
    );
  }
}
``` 

- Terdapat error. Pertama, tidak mengimpor AutoSizeText di file Dart sehingga harus ditambahkan `import 'package:auto_size_text/auto_size_text.dart';`. Kemudian, error karena variabel text belum didefinisikan di dalam RedTextWidget.

## Langkah 5: Buat Variabel text dan parameter di constructor
Menambahkan variabel text dan parameter di constructor .

```dart
import 'package:auto_size_text/auto_size_text.dart';
import 'package:flutter/material.dart';

class RedTextWidget extends StatelessWidget {
final String text;

const RedTextWidget({Key? key, required this.text}) : super(key: key);

  @override
  Widget build(BuildContext context) {
    return AutoSizeText(
      text,
      style: const TextStyle(color: Colors.red, fontSize: 14),
      maxLines: 2,
      overflow: TextOverflow.ellipsis,
    );
  }
}
```

## Langkah 6: Tambahkan widget di main.dart
Menambahkan di dalam children: pada class _MyHomePageState pada file main.dart.

```dart
class _MyHomePageState extends State<MyHomePage> {
  int _counter = 0;

  void _incrementCounter() {
    setState(() {
      Container(
        color: Colors.yellowAccent,
        width: 50,
        child: const RedTextWidget(
          text: 'You have pushed the button this many times:',
        ),
      );
      Container(
        color: Colors.greenAccent,
        width: 100,
        child: const Text(
          'You have pushed the button this many times:',
        ),
      );
      _counter++;
    });
  }
```

<img src = img\JS7-6.png>

# Tugas Praktikum
#### 1. Selesaikan Praktikum tersebut, lalu dokumentasikan dan push ke repository Anda berupa screenshot hasil pekerjaan beserta penjelasannya di file README.md!
#### 2. Jelaskan maksud dari langkah 2 pada praktikum tersebut!
- Pada langkah 2, perintah flutter pub add auto_size_text digunakan untuk menambahkan plugin ke dalam project Flutter untuk menyesuaikan ukuran teks secara otomatis agar sesuai dengan batas lebar atau tinggi yang tersedia. Setelah menjalankan perintah tersebut, nama plugin dan versi yang sesuai akan ditambahkan di bawah bagian dependencies di file pubspec.yaml. Pada langkah ini memastikan bahwa plugin siap digunakan dalam project, dan nantinya bisa diimpor dan diimplementasikan pada file dart seperti red_text_widget.dart.
#### 3. Jelaskan maksud dari langkah 5 pada praktikum tersebut!
- Langkah 5 pada praktikum ini bertujuan untuk membuat widget `RedTextWidget` lebih dinamis dengan menambahkan variabel `text` yang digunakan untuk menyimpan teks yang akan ditampilkan. Constructor diperbarui dengan menambahkan parameter `required this.text`, sehingga teks harus diberikan setiap kali widget dipanggil. Hal ini memungkinkan widget `AutoSizeText` untuk menampilkan teks yang diterima secara dinamis dari luar, membuat widget dapat digunakan dengan teks yang berbeda-beda sesuai kebutuhan.
#### 4. Pada langkah 6 terdapat dua widget yang ditambahkan, jelaskan fungsi dan perbedaannya!
- Widget pertama:
    ```dart
    Container(
    color: Colors.yellowAccent,
    width: 50,
    child: const RedTextWidget(
        text: 'You have pushed the button this many times:',
    ),
    )
    ```
    Berfungsi untuk menampung widget RedTextWidget, yang merupakan widget kustom yang dibuat sebelumnya. Di dalamnya, AutoSizeText digunakan untuk menampilkan teks dengan warna merah dan ukuran yang dapat menyesuaikan secara otomatis sesuai dengan ruang yang tersedia. Lebar container ini dibatasi 50 unit, sehingga teks akan menyesuaikan ukuran dan mungkin terpotong jika tidak cukup ruang.
- Widget kedua
    ```dart
    Container(
    color: Colors.greenAccent,
    width: 100,
    child: const Text(
        'You have pushed the button this many times:',
    ),
    )
    ```
    Berfungsi untuk menampilkan teks secara statis dengan lebar container 100 unit. Tidak ada penyesuaian ukuran otomatis untuk teks, sehingga jika teks lebih panjang daripada ruang yang tersedia, teks akan tetap tampil penuh tetapi mungkin keluar dari batas container.<br><br>
- Perbedaan :
RedTextWidget menggunakan AutoSizeText untuk menyesuaikan ukuran teks agar muat dalam container yang sempit (50 unit). Widget kedua menggunakan Text biasa yang tidak menyesuaikan ukuran, sehingga teks mungkin keluar dari container jika tidak cukup ruang.
#### 5. Jelaskan maksud dari tiap parameter yang ada di dalam plugin auto_size_text berdasarkan tautan pada dokumentasi ini !

- **Usage (Penggunaan)**

1. maxLines  
   Parameter ini digunakan untuk menentukan jumlah maksimal baris yang dapat ditempati oleh teks. Jika tidak diatur, AutoSizeText hanya akan menyesuaikan teks berdasarkan lebar dan tinggi yang tersedia.

   Contoh:
   ```dart
   AutoSizeText(
     'Teks yang sangat panjang',
     style: TextStyle(fontSize: 30),
     maxLines: 2,
   )
   ```
   Pada contoh di atas, teks akan diatur ulang untuk menempati maksimal dua baris.

2. minFontSize & maxFontSize  
   - minFontSize menentukan ukuran font terkecil yang diperbolehkan saat menyesuaikan teks. Default-nya adalah 12.
   - maxFontSize menentukan ukuran font terbesar yang bisa digunakan.

   Contoh:
   ```dart
   AutoSizeText(
     'Teks yang sangat panjang',
     style: TextStyle(fontSize: 30),
     minFontSize: 18,
     maxLines: 4,
     overflow: TextOverflow.ellipsis,
   )
   ```
   Pada contoh ini, ukuran font akan disesuaikan antara 18 dan 30.

3. group  
   Parameter ini memungkinkan untuk menyinkronkan ukuran font dari beberapa AutoSizeText. Semua teks dalam grup ini akan disesuaikan berdasarkan ukuran teks terkecil dalam grup.

   Contoh:
   ```dart
   var myGroup = AutoSizeGroup();

   AutoSizeText(
     'Teks 1',
     group: myGroup,
   );

   AutoSizeText(
     'Teks 2',
     group: myGroup,
   );
   ```

4. stepGranularity  
   Parameter ini menentukan besarnya langkah pengurangan ukuran font saat menyesuaikan teks. Semakin kecil angkanya, semakin halus penyesuaiannya.

   Contoh:
   ```dart
   AutoSizeText(
     'Teks yang sangat panjang',
     style: TextStyle(fontSize: 40),
     minFontSize: 10,
     stepGranularity: 5,
     maxLines: 4,
     overflow: TextOverflow.ellipsis,
   )
   ```

5. presetFontSizes  
   Jika Anda hanya ingin ukuran font tertentu yang digunakan, Anda bisa mendefinisikan array ukuran font menggunakan presetFontSizes. Parameter ini akan mengabaikan minFontSize, maxFontSize, dan stepGranularity.

   Contoh:
   ```dart
   AutoSizeText(
     'Teks yang sangat panjang',
     presetFontSizes: [40, 20, 14],
     maxLines: 4,
   )
   ```

6. overflowReplacement  
   Jika teks terlalu panjang untuk muat dalam batasannya, widget ini akan ditampilkan sebagai gantinya. Ini membantu mencegah teks yang terlalu kecil dan sulit dibaca.

   Contoh:
   ```dart
   AutoSizeText(
     'Teks terlalu panjang',
     maxLines: 1,
     overflowReplacement: Text('Maaf, teks terlalu panjang'),
   )
   ```

- **Rich Text** <br>
AutoSizeText mendukung penggunaan Rich Text, yang memungkinkan Anda menerapkan beberapa gaya dalam satu teks. Untuk menggunakannya, Anda perlu menggunakan AutoSizeText.rich().

    Contoh:
    ```dart
    AutoSizeText.rich(
    TextSpan(
        text: 'Teks yang sangat panjang',
        style: TextStyle(fontSize: 20),
    ),
    minFontSize: 5,
    )
    ```

- **Parameters** <br>
Berbagai parameter yang telah dijelaskan sebelumnya seperti key, textKey, style, minFontSize, maxFontSize, stepGranularity, dan lain-lain membantu menyesuaikan ukuran teks agar sesuai dengan area yang tersedia.

- **Performance (Performa)** <br>
Meskipun AutoSizeText sangat cepat dan bisa menggantikan widget Text biasa, untuk performa yang optimal:
Hindari menggunakan ukuran font yang sangat besar yang tidak diperlukan.
Jika rentang ukuran font sangat besar, pertimbangkan untuk meningkatkan stepGranularity agar penyesuaian lebih cepat.

- **Troubleshooting (Pemecahan Masalah)**

1. Missing bounds (Batas yang hilang)  
   Jika AutoSizeText tidak menyesuaikan ukurannya atau meluap, kemungkinan besar lebar dan tinggi dari teks tidak dibatasi. Dalam widget seperti Row, Column, atau ListView, Anda perlu membungkus AutoSizeText dengan Expanded atau widget lain yang memberikan batasan.

   Salah:
   ```dart
   Row(
     children: <Widget>[
       AutoSizeText('Teks sangat panjang'),
     ],
   )
   ```

   Benar:
   ```dart
   Row(
     children: <Widget>[
       Expanded(
         child: AutoSizeText('Teks sangat panjang'),
       ),
     ],
   )
   ```

2. MinFontSize too large (MinFontSize terlalu besar)  
   Jika teks tidak disesuaikan dengan baik, periksa apakah nilai minFontSize terlalu besar. Misalnya, jika Anda menggunakan AutoSizeText.rich() tanpa mengatur minFontSize, ukuran font default mungkin terlalu besar untuk memungkinkan penyesuaian teks.

   Salah:
   ```dart
   AutoSizeText.rich(
     TextSpan(
       text: 'Teks tidak disesuaikan dengan baik',
       style: TextStyle(fontSize: 200),
     ),
   )
   ```

   Benar:
   ```dart
   AutoSizeText.rich(
     TextSpan(
       text: 'Teks disesuaikan dengan benar',
       style: TextStyle(fontSize: 200),
     ),
     minFontSize: 0,
     stepGranularity: 0.1,
   )
   ```