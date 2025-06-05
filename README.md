### 🚀 Proyek Kelompok 1 🚀

| **Nama** | **NPM** | 
|:-----------------------|:-------------------:|
| Koreza Almukadima        | G1A023011 |
| Hana Syarifah    | G1A023017 |
| Ricardo Gellael        | G1A023061 | 
| Merischa Theresia Hutauruk       | G1A023071 |


# 🛡️ Aplikasi Kriptografi Caesar Cipher 🛡️

Caesar Cipher adalah metode enkripsi substitusi monoalfabetik klasik yang identik dengan Julius Caesar untuk menjaga kerahasiaan komunikasi militer. Cara kerjanya adalah dengan mengganti setiap karakter dalam *plaintext* (teks asli) dengan karakter lain yang bergeser sejauh *n* posisi dalam urutan alfabet. Parameter *n* ini dikenal sebagai **kunci (key)** atau **nilai pergeseran (shift value)**.

-----

## ✨ Tampilan Aplikasi Kami ✨
![image](https://github.com/user-attachments/assets/0615d166-b586-4546-80ba-e130113f92cd)

Aplikasi ini dilengkapi dengan **Antarmuka Aksi Fungsional** yang intuitif, terdiri dari empat tombol utama untuk menjalankan operasi spesifik:

  * 🔐 **Enkripsi (Encrypt):** Mengubah *plaintext* menjadi *ciphertext* untuk menjaga **kerahasiaan informasi**.

  * 🔓 **Dekripsi (Decrypt):** Mengembalikan *ciphertext* ke *plaintext* untuk **mengakses informasi asli**.

  * 🔍 **Analisis (Analyze):** Melakukan prosedur kriptanalitik untuk mengidentifikasi pola atau potensi kunci, **memfasilitasi pemecahan kode**.

  * 🧪 **Pengujian (Test):** Menjalankan *routine* diagnostik untuk memverifikasi fungsionalitas dan integritas operasional.

-----

## 📈 Kriptanalisis Berbasis Frekuensi untuk Caesar Cipher Analyzer 📊

Untuk meningkatkan kemampuan "Caesar Cipher Analyzer" yang ada, kami telah mengintegrasikan fitur **analisis frekuensi huruf**. Metode kriptanalitik ini **fundamental dan sangat efektif**, memanfaatkan properti statistik intrinsik bahasa — yaitu distribusi kemunculan huruf yang konsisten — untuk mendekripsi *cipher* substitusi unialfabetik seperti Caesar Cipher.

### 🔬 Prinsip Dasar Kriptanalisis Frekuensi

Setiap bahasa alami memiliki profil distribusi frekuensi karakter yang **unik dan dapat diprediksi secara statistik**. Contohnya, dalam Bahasa Inggris, huruf 'E' adalah yang paling sering muncul, diikuti oleh 'T', 'A', 'O', 'I', 'N', dan seterusnya. Serupa dengan itu, dalam Bahasa Indonesia, karakter seperti 'A', 'I', 'U', 'E', 'O', 'N', dan 'R' secara konsisten memiliki frekuensi kemunculan yang tinggi.

Pada Caesar Cipher, enkripsi hanya melibatkan **pergeseran siklik** posisi karakter dalam alfabet. Akibatnya, **struktur frekuensi asli** dari *plaintext* tetap dipertahankan dalam *ciphertext*, hanya saja posisinya bergeser. Jika 'E' adalah karakter paling sering di *plaintext*, maka karakter yang bergeser dari 'E' akan menjadi karakter paling sering di *ciphertext*.

### 🔍 Metodologi Analisis Frekuensi (untuk Dekripsi Caesar Cipher)

Prosedur kriptanalitik ini melibatkan langkah-langkah berurutan berikut:

1.  **Menghitung Frekuensi Huruf *Ciphertext***: Mengumpulkan data numerik mengenai frekuensi kemunculan setiap karakter alfabet (A-Z) dalam teks terenkripsi. 🔢
2.  **Menentukan Karakter Mayoritas *Ciphertext***: Mengidentifikasi satu atau beberapa karakter yang paling sering muncul dalam *ciphertext*. 🥇
3.  **Mengorelasikan Statistik dengan Frekuensi Bahasa Referensi**: Mengasumsikan bahwa karakter paling dominan dalam *ciphertext* (misalnya, 'X') secara statistik berkorelasi dengan karakter yang paling dominan dalam bahasa *plaintext* (misalnya, 'A' atau 'I' untuk Bahasa Indonesia). 🔄
4.  **Mendapatkan Kandidat Kunci**: Menghitung selisih posisi alfabet antara karakter dominan *ciphertext* dan karakter dominan bahasa referensi untuk mengidentifikasi kandidat kunci.
      * **Contoh:** Jika 'X' (indeks 23) adalah karakter paling sering di *ciphertext* dan diduga mewakili 'A' (indeks 0) dari *plaintext*, maka potensi pergeseran (kunci) adalah $(23 - 0) \\pmod{26} = 23$. Jika diasumsikan mewakili 'I' (indeks 8), maka $(23 - 8) \\pmod{26} = 15$. 🔑
5.  **Validasi Dekripsi Empiris**: Menerapkan setiap kandidat kunci untuk mendekripsi *ciphertext*. Kunci yang berhasil menghasilkan *plaintext* yang **koheren dan memiliki makna** divalidasi sebagai solusi yang akurat. ✅

-----

## ⚙️ Implementasi Fungsionalitas Analisis Frekuensi (Modifikasi Kode JavaScript)

Kami telah mengintegrasikan fungsionalitas baru ini dan memperbarui fungsi `analyze()` yang ada untuk mendukung kapabilitas ini secara menyeluruh.

### 1\. Basis Data Frekuensi Huruf Referensi (untuk Bahasa Indonesia): 📚

Dataset ini menyediakan profil frekuensi huruf rata-rata Bahasa Indonesia (menggunakan indeks 0-25 untuk A-Z), berfungsi sebagai referensi komparatif:

```javascript
// Data frekuensi huruf rata-rata dalam bahasa Indonesia (estimasi, dapat disesuaikan dengan korpus linguistik spesifik)
// Urutan: A, B, C, D, E, F, G, H, I, J, K, L, M, N, O, P, Q, R, S, T, U, V, W, X, Y, Z
const indoFreq = [
    19.3, 3.4, 3.0, 3.7, 7.5, 0.4, 1.2, 1.0, 8.7, 0.4, 0.2, 4.0, 2.5, 9.1, 4.3, 2.8, 0.05, 5.7, 5.0, 4.8, 2.8, 0.2, 0.05, 0.01, 0.05, 0.05
];
// Karakter dengan frekuensi tertinggi yang umum di Bahasa Indonesia: A (indeks 0), I (indeks 8), N (indeks 13), E (indeks 4)
```

### 2\. Algoritma Penghitungan Frekuensi Karakter *Ciphertext*: 🔢

Fungsi ini dirancang khusus untuk menghitung distribusi frekuensi karakter dalam teks yang diberikan:

```javascript
// Fungsi untuk melakukan kalkulasi frekuensi karakter dalam teks input
function calculateFrequency(text) {
    const frequencies = new Array(26).fill(0); // Inisialisasi array 26 elemen dengan nilai nol untuk representasi A-Z
    let totalLetters = 0; // Inisialisasi penghitung untuk total karakter alfabetis yang valid

    // Iterasi melalui setiap karakter dalam teks input
    for (let i = 0; i < text.length; i++) {
        const charCode = text.charCodeAt(i); // Akuisisi kode ASCII dari karakter
        if (charCode >= 65 && charCode <= 90) { // Kondisi untuk karakter alfabetis kapital (A-Z)
            frequencies[charCode - 65]++; // Inkremen hitungan pada indeks yang sesuai
            totalLetters++; // Inkremen total huruf yang diproses
        } else if (charCode >= 97 && charCode <= 122) { // Kondisi untuk karakter alfabetis kecil (a-z)
            frequencies[charCode - 97]++; // Inkremen hitungan pada indeks yang sesuai
            totalLetters++; // Inkremen total huruf yang diproses
        }
    }

    // Konversi hitungan absolut menjadi representasi persentase untuk analisis komparatif
    const percentageFrequencies = frequencies.map(count =>
        totalLetters > 0 ? (count / totalLetters) * 100 : 0 // Proteksi terhadap pembagian dengan nol
    );

    return percentageFrequencies;
}
```

### 3\. Pembaruan Fungsi `analyze()`: Integrasi Kriptanalisis Frekuensi Komprehensif: 🧠

Fungsi `analyze()` kini diperkaya untuk menyajikan dua pendekatan dekripsi yang saling melengkapi: metode *brute-force* dan pendekatan kriptanalisis berbasis frekuensi.

```javascript
function analyze() {
    const text = document.getElementById("inputText").value;
    let results = "🔍 **Hasil Dekripsi Potensial (Metode Brute Force):**\n\n";

    // Bagian Brute Force (dipertahankan untuk menyediakan cakupan referensi yang komprehensif)
    for (let i = 1; i < 26; i++) {
        results += `🔑 Shift ${i.toString().padStart(2, '0')}: ${caesarCipher(text, i, true)}\n\n`;
    }

    results += "\n--- **Analisis Frekuensi Probabilistik (Referensi Bahasa Indonesia)** ---\n\n";

    const inputFreq = calculateFrequency(text); // Eksekusi kalkulasi frekuensi untuk teks input

    // Identifikasi karakter dengan frekuensi kemunculan tertinggi dalam ciphertext
    let maxFreqCharIndex = -1;
    let maxFreq = -1;
    for (let i = 0; i < 26; i++) {
        if (inputFreq[i] > maxFreq) {
            maxFreq = inputFreq[i];
            maxFreqCharIndex = i;
        }
    }

    if (maxFreqCharIndex === -1 || maxFreq === 0) { // Validasi kondisi untuk data huruf yang tidak memadai
        results += "Dataset karakter alfabetis tidak mencukupi untuk analisis frekuensi. 📉\n";
    } else {
        const inputMostFrequentChar = String.fromCharCode(65 + maxFreqCharIndex); // Konversi indeks numerik menjadi representasi karakter

        results += `Karakter dominan dalam korpus teks terenkripsi: '**${inputMostFrequentChar}**' (${maxFreq.toFixed(2)}%)\n\n`;
        results += `Pengujian Hipotesis Kunci Berbasis Asumsi Karakter Paling Sering: \n`;

        // Pengujian beberapa hipotesis kunci paling probabel berdasarkan karakter frekuensi tinggi Bahasa Indonesia
        // Pendekatan ini secara substansial meningkatkan probabilitas identifikasi kunci yang valid
        const topIndoChars = [
            { char: 'A', index: 0 }, // 'A' sebagai karakter paling sering (indeks 0)
            { char: 'I', index: 8 }, // 'I' sebagai karakter dengan frekuensi tinggi berikutnya (indeks 8)
            { char: 'N', index: 13 },// 'N' sebagai karakter dengan frekuensi tinggi berikutnya (indeks 13)
            { char: 'E', index: 4 }  // 'E' sebagai karakter dengan frekuensi tinggi berikutnya (indeks 4)
        ];

        topIndoChars.forEach(targetChar => {
            // Kalkulasi potensi kunci: (Posisi Karakter Cipher - Posisi Karakter Plaintext + 26) mod 26
            const potentialShift = (maxFreqCharIndex - targetChar.index + 26) % 26;
            const decryptedText = caesarCipher(text, potentialShift, true); // Eksekusi dekripsi menggunakan kunci hipotesis
            results += `  Asumsi '${inputMostFrequentChar}' $\\approx$ '${targetChar.char}': 🔑 Shift ${potentialShift.toString().padStart(2, '0')} $\\rightarrow$ "**${decryptedText.substring(0, 50)}**..."\n`; // Presentasi cuplikan hasil dekripsi
        });

        results += "\n(Disarankan untuk secara **kritis mengevaluasi** koherensi linguistik dari hasil dekripsi di atas untuk menemukan *plaintext* yang valid) 🧐\n";
    }

    document.getElementById("output").innerText = results;
    animateOutput(); // Aplikasi animasi visual pada elemen output
}
```

#### 🚀 Manfaat Fungsionalitas Analisis Frekuensi:

Dengan integrasi kapabilitas analisis frekuensi ini, alat Caesar Cipher Anda bertransformasi melampaui fungsi konverter dasar. Ketika pengguna menginisiasi operasi "Analyze", mereka akan memperoleh:

1.  **Dekripsi *Brute Force***: Sebuah **tinjauan komprehensif** 📋 dari seluruh 25 permutasi dekripsi potensial, memfasilitasi deteksi visual *plaintext* yang valid.
2.  **Wawasan Kriptanalitik Berbasis Frekuensi**: Ini menyediakan **wawasan heuristik yang cerdas** 💡 dan rekomendasi kunci yang terinformasi secara statistik.
      * Alat ini secara otomatis menyoroti karakter dengan frekuensi tertinggi dalam *ciphertext* yang diberikan. 🎯
      * Selanjutnya, alat ini menyajikan beberapa **kandidat dekripsi paling mungkin** berdasarkan korelasi statistik dengan distribusi frekuensi karakter Bahasa Indonesia. 📊
      * Fitur ini secara substansial **mengurangi ruang pencarian** untuk kunci yang valid, mengubah proses dari *random guessing* menjadi **investigasi yang terarah dan berbasis ilmiah**. 🔭

