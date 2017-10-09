Devam eden geliştirme nedeniyle hello Android SDK sürüm Android Studio'da yüklü hello kod hello sürümünde eşleşmeyebilir. Merhaba Bu öğreticide başvurulan Android SDK sürüm 23 hello son hello yazıldığı sırada ' dir. Merhaba sürüm numarası SDK görünür hello yeni sürümleri artırabilir ve hello kullanılabilir en son sürümünü kullanmanızı öneririz.

Sürüm uyuşmazlığı iki belirtileri şunlardır:

- Derleme ya da Merhaba projeyi yeniden gibi Gradle hata iletileri alabilirsiniz "**toofind hedef Google Inc.:Google APIs:n başarısız**".
- Standart Android nesneleri çözümlenmelidir kod temelinde `import` ifadeleri hata iletileri oluşturur.

Bunlardan görünürse, hello hello Android Studio'da yüklü Android SDK sürümünü karşıdan hello projesinin hello SDK hedefini eşleşmeyebilir. tooverify hello sürüm, aşağıdaki değişiklikler hello olun:

1. Android Studio'da sırasıyla **Araçları** > **Android** > **SDK Manager**. Merhaba SDK Platform en son sürümünü hello yüklü değilse, tooinstall'ı tıklatın. Merhaba sürüm numarasını not edin.
2. Merhaba üzerinde **Proje Gezgini** sekmesinde, altında **Gradle betikleri**açın hello dosya **build.gradle (modeule: uygulama)**. Bu hello olun **compileSdkVersion** ve **buildToolsVersion** toohello yüklü en son SDK sürümünü ayarlayın. Başlangıç etiketleri şuna benzeyebilir:

             compileSdkVersion 'Google Inc.:Google APIs:23'
            buildToolsVersion "23.0.2"
3. Merhaba Android Studio Proje Gezgini, hello proje düğümüne sağ tıklayın, seçin **özellikleri**ve hello sol sütunda seçin **Android**. Bu hello olun **proje derleme hedefi** toohello ayarlamak hello olarak aynı SDK sürümü **targetSdkVersion**.

Android Studio'da hello bildirim dosyası artık kullanılan toospecify hello hedef SDK ve Eclipse hello durumuyla aksine en düşük SDK sürümü değil.
