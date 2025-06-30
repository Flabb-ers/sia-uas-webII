# Alur Sistem Informasi Akademik Sekolah

## Deskripsi Sistem
Sistem Informasi Akademik Sekolah ini dirancang untuk mendukung proses akademik, seperti pengelolaan jadwal, presensi, dan penilaian siswa. Sistem terdiri dari tiga peran utama, yaitu admin, guru, dan siswa.

## Peran dan Fungsi

### 1. Admin
- Mengelola data master seperti siswa, guru, kelas, mata pelajaran, jadwal, dan tahun ajaran.
- Admin bertanggung jawab dalam pengelolaan data awal agar sistem dapat digunakan oleh guru dan siswa.

### 2. Guru
- Melihat jadwal mengajar berdasarkan kelas dan tahun ajaran.
- Menginput data presensi per siswa per pertemuan.
- Menginput nilai per siswa berdasarkan jenis nilai: UTS, UAS, Tugas, dan Sikap.
- Nilai tugas dapat diinput lebih dari satu kali. Sistem akan menghitung nilai rata-rata dari seluruh tugas.
- Nilai UTS, UAS, dan Sikap hanya dapat diisi satu kali untuk setiap siswa pada setiap mata pelajaran.
- Melihat hasil nilai akhir siswa.

> **Catatan:**  
> Nomor pertemuan pada presensi diisi secara otomatis oleh sistem berdasarkan jumlah pertemuan yang telah ada untuk jadwal tersebut. Guru tidak perlu menginput pertemuan secara manual di form.

### 3. Siswa
- Melihat jadwal kelas.
- Melihat nilai akhir yang telah dihitung secara otomatis berdasarkan komponen penilaian.

## Komponen Penilaian
Nilai akhir siswa dihitung secara otomatis dengan komposisi sebagai berikut:

- UTS: 25%
- UAS: 25%
- Tugas: 25% (rata-rata dari seluruh entri nilai tugas yang dimasukkan)
- Presensi: 15%
- Sikap: 10%

Presensi dihitung berdasarkan kehadiran siswa pada setiap pertemuan dan disimpan dalam tabel presensi.

## Alur Sistem

1. **Admin** mengisi data awal (guru, siswa, kelas, mapel, jadwal, tahun ajaran).
2. **Guru** melihat jadwal yang tersedia.
3. **Guru** melakukan input presensi per pertemuan untuk setiap siswa.
4. **Guru** menginput nilai per jenis:
   - Nilai `UTS`, `UAS`, dan `Sikap` hanya dapat dimasukkan satu kali per siswa per jadwal.
   - Nilai `Tugas` dapat diinput lebih dari satu kali. Sistem akan menghitung nilai rata-rata dari semua entri tersebut.
5. Sistem menghitung **nilai presensi otomatis** berdasarkan jumlah kehadiran siswa terhadap jumlah pertemuan.
6. Sistem menghitung **nilai akhir otomatis** dengan menggabungkan seluruh komponen berdasarkan persentase:
   - UTS: 25%
   - UAS: 25%
   - Tugas (rata-rata): 25%
   - Presensi: 15%
   - Sikap: 10%
7. **Siswa** dan **guru** dapat melihat hasil akhir nilai masing-masing.

> Catatan: Jika terdapat lebih dari satu entri nilai tugas pada jadwal yang sama untuk siswa yang sama, maka sistem otomatis menghitung nilai rata-rata tugas sebagai dasar penilaian akhir.

## Struktur Tabel
- `admin`
- `guru`
- `siswa`
- `kelas`
- `mapel`
- `tahun_ajaran`
- `jadwal`
- `presensi` (dengan kolom `pertemuan`, yang diisi otomatis)
- `nilai` (dengan kolom `jenis` sebagai ENUM: uts, uas, tugas, sikap)

---

## Catatan Pengembangan
Struktur database yang digunakan dalam sistem ini merupakan dasar utama agar seluruh fitur dapat berjalan sebagaimana mestinya.

Apabila di kemudian hari terdapat kebutuhan **untuk menjaga kelangsungan atau kelancaran sistem** (contoh: menambahkan kolom ID relasi tambahan, timestamp, dll), maka **penambahan kolom atau tabel diperbolehkan**.

Namun, **tidak diperkenankan menghapus, mengganti tipe data, atau mengubah struktur inti yang sudah ada**, karena dapat menyebabkan sistem tidak berjalan dengan baik atau terjadi error pada proses otomatisasi seperti perhitungan nilai dan presensi.

