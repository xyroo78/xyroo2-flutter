# XYROO Flutter

Project Flutter untuk antarmuka XYROO dan simulasi lokal.

## Perbaikan Android
Folder `android/` sudah ditambahkan menggunakan Android embedding v2:
- `MainActivity` menggunakan `io.flutter.embedding.android.FlutterActivity`.
- `AndroidManifest.xml` mencantumkan `flutterEmbedding=2`.
- Gradle menggunakan konfigurasi Kotlin DSL modern.

## Build APK
Di lingkungan yang memiliki Flutter SDK dan Android SDK:
1. Ekstrak ZIP.
2. Masuk ke folder `xyroo_flutter`.
3. Jalankan `flutter pub get`.
4. Jika folder `android/gradle/wrapper/gradle-wrapper.jar` dan skrip `android/gradlew` tidak disediakan oleh layanan build, jalankan `flutter create --platforms=android .` untuk menghasilkan wrapper/template Android standar. Tinjau perubahan agar `MainActivity.kt` tetap memakai embedding v2.
5. Jalankan `flutter build apk --debug`.

APK biasanya dibuat di `build/app/outputs/flutter-apk/app-debug.apk`.

## Login demo
- Username: `xyroo`
- Password: `100911`
- Access key simulasi: `XYROO-NEW`

Fungsi panel WhatsApp di aplikasi ini hanya simulasi lokal; tidak mengirim pesan dan tidak menyerang akun.
