---
title: "Azure AD Android Başlarken | Microsoft Docs"
description: "Oturum açma ve Azure AD aramalar için Azure AD ile tümleşen bir Android uygulamasının nasıl oluşturulacağını OAuth2.0 kullanarak API'leri korumalı."
services: active-directory
documentationcenter: android
author: danieldobalian
manager: mtillman
editor: 
ms.assetid: da1ee39f-89d3-4d36-96f1-4eabbc662343
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: mobile-android
ms.devlang: java
ms.topic: article
ms.date: 11/30/2017
ms.author: dadobali
ms.custom: aaddev
ms.openlocfilehash: 619334b3ca65654fd845a62c2fc068156d94d6fc
ms.sourcegitcommit: 234c397676d8d7ba3b5ab9fe4cb6724b60cb7d25
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/20/2017
---
# <a name="azure-ad-android-getting-started"></a>Azure AD Android Başlarken
[!INCLUDE [active-directory-devquickstarts-switcher](../../../includes/active-directory-devquickstarts-switcher.md)]

Bir masaüstü uygulaması geliştiriyorsanız, Azure Active Directory (Azure AD), basit ve kolay, kullanıcılarınız, şirket içi Active Directory hesaplarını kullanarak kimlik doğrulaması kılar. Ayrıca, tüm web API Office 365 API'leri veya Azure API'sini gibi Azure AD tarafından korunan güvenli bir şekilde kullanmak uygulamanızı sağlar.

Korunan kaynaklara erişim için gereken Android istemciler için Active Directory Authentication Library (ADAL) Azure AD sağlar. ADAL tek amacı, erişim belirteçleri almak, uygulamanız için kolay hale getirmektir. Ne kadar kolay olduğunu göstermek için size bir Android Yapılacaklar listesi uygulaması, yapı:

* Alır erişim belirteçleri kullanarak bir Yapılacaklar listesi API çağırma [OAuth 2.0 kimlik doğrulama protokolü](https://msdn.microsoft.com/library/azure/dn645545.aspx).
* Bir kullanıcının yapılacaklar listesini alır.
* Oturumunu kullanıcılar kapatır.

Başlamak için kullanıcı oluşturma ve bir uygulamayı kaydetme Azure AD kiracısı gerekir. Bir kiracı yoksa [edinebileceğinizi öğrenin](active-directory-howto-tenant.md).

## <a name="step-1-download-and-run-the-nodejs-rest-api-todo-sample-server"></a>1. adım: İndirme ve Node.js REST API TODO örnek sunucusu çalıştırma
Node.js REST API Yapılacaklar örnek bir tek-Kiracı Yapılacaklar REST API için Azure AD oluşturmak için varolan örneğimizde karşı özel olarak çalışmak için yazılmıştır. Bu Hızlı Başlangıç için bir önkoşuldur.

Varolan örneklerimizi bu ayarlama hakkında daha fazla bilgi için bkz: [Microsoft Azure Active Directory örnek REST API'si hizmeti için Node.js](active-directory-devquickstarts-webapi-nodejs.md).


## <a name="step-2-register-your-web-api-with-your-azure-ad-tenant"></a>2. adım: Azure AD kiracınıza ile web API kaydetme
Active Directory, iki tür uygulamaları ekleme destekler:

- Web Hizmetleri kullanıcılara sunmak API'leri
- Web API'leri olanlar erişim (Web'de veya bir aygıtta çalışan) uygulamaları

Bu adımda, bu örnek test etmek için yerel olarak çalıştırıyorsanız API web kaydediliyor. Normalde, bu web API uygulama erişmek için istediğiniz işlevselliği sunan bir REST hizmetidir. Azure AD, herhangi bir uç nokta korumaya yardımcı olabilir.

Daha önce başvurulan Yapılacaklar REST API kaydetme varsayılarak. Ancak bu, tüm web korunmasına yardımcı olmak için Azure Active Directory istediğiniz API çalışır.

1. [Azure Portal](https://portal.azure.com) oturum açın.
2. Üst çubuğunda hesabınızı tıklatın. İçinde **Directory** listesinde, Azure AD Kiracı uygulamanızı kaydetmek istediğiniz yeri seçin.
3. Tıklatın **daha Hizmetleri** sol bölmesinde ve seçip **Azure Active Directory**.
4. Tıklatın **uygulama kayıtlar**ve ardından **Ekle**.
5. Uygulama için kolay bir ad girin (örneğin, **TodoListService**), select **Web uygulaması ve/veya Web API**, tıklatıp **sonraki**.
6. Oturum açma URL'sini örnek için temel URL'sini girin. Varsayılan olarak `https://localhost:8080`.
7. Tıklatın **Tamam** kayıt işlemini tamamlamak için.
8. Hala Azure portalında sırasında uygulama sayfasına gidin, uygulama kimliği değerini bulmak ve kopyalayın. Bu daha sonra uygulamanızın yapılandırırken ihtiyacınız vardır.
9. Gelen **ayarları** -> **özellikleri** sayfasında, uygulama kimliği URI'SİNİN güncelleştirmesi - girin `https://<your_tenant_name>/TodoListService`. Değiştir `<your_tenant_name>` Azure AD kiracınıza adı.

## <a name="step-3-register-the-sample-android-native-client-application"></a>3. adım: örnek Android yerel istemci uygulaması kaydetme
Bu örnekte, web uygulamanızı kaydetmeniz gerekir. Bu, yalnızca kayıtlı web API ile iletişim kurmak uygulamanızı sağlar. Azure AD bile, kayıtlı olduğu sürece, oturum açma için sormak, uygulamanızın izin vermek reddeder. Güvenlik modelinin parçası olan.

Daha önce başvurulan örnek uygulaması kaydettirilirken varsayılarak. Ancak bu yordam, geliştirmekte herhangi bir uygulama için geçerlidir.

> [!NOTE]
> Neden, hem uygulama hem de web API'si bir kiracı koyma merak ediyor. Tahmin gibi başka bir kiracı Azure AD'den kayıtlı bir API'nin erişen bir uygulama oluşturabilirsiniz. Bunu yaparsanız, müşterilerinizin API uygulamasında kullanımına izin istenir. İOS için Active Directory Authentication Library sizin için bu onay ilgilenir. Biz daha gelişmiş özellikleri keşfetmenizde bu Microsoft APIs suite Azure ve Office, yanı sıra herhangi bir hizmet sağlayıcısına erişmek için gerekli iş önemli bir parçası olduğunu görürsünüz. Web API ve aynı Kiracı uygulamanızı kayıtlı olduğundan, şu an için sizden izin görmezsiniz. Bu genellikle kullanmak yalnızca kendi şirket için bir uygulama geliştiriyorsanız karşılaşılan bir durumdur.

1. [Azure Portal](https://portal.azure.com) oturum açın.
2. Üst çubuğunda hesabınızı tıklatın. İçinde **Directory** listesinde, Azure AD Kiracı uygulamanızı kaydetmek istediğiniz yeri seçin.
3. Tıklatın **daha Hizmetleri** sol bölmesinde ve seçip **Azure Active Directory**.
4. Tıklatın **uygulama kayıtlar**ve ardından **Ekle**.
5. Uygulama için kolay bir ad girin (örneğin, **TodoListClient Android**), select **yerel istemci uygulaması**, tıklatıp **sonraki**.
6. Yeniden yönlendirme URI'si, girin `http://TodoListClient`. **Son**'a tıklayın.
7. Uygulama sayfasından uygulama kimliği değerini bulmak ve kopyalayın. Bu daha sonra uygulamanızın yapılandırırken ihtiyacınız vardır.
8. Gelen **ayarları** sayfasında, **gerekli izinler** seçip **Ekle**.  Bulun ve TodoListService seçin, eklemeniz **erişim TodoListService** altında izni **izinlere temsilci**, tıklatıp **Bitti**.

Maven ile oluşturmak için en üst düzeyinde pom.xml kullanabilirsiniz:

1. Bu depodaki tercih ettiğiniz bir dizine kopyalayın:

  `$ git clone git@github.com:AzureADSamples/NativeClient-Android.git`  
2. Adımları [Android için Maven ortamınızı ayarlamak için Önkoşullar](https://github.com/MSOpenTech/azure-activedirectory-library-for-android/wiki/Setting-up-maven-environment-for-Android).
3. Öykünücü SDK 19 ile ayarlayın.
4. Depodaki kopyaladığınız kök klasörüne gidin.
5. Bu komutu çalıştırın:`mvn clean install`
6. Dizini için hızlı başlangıç örnek değiştirin:`cd samples\hello`
7. Bu komutu çalıştırın:`mvn android:deploy android:run`

   Uygulama başlangıç görmeniz gerekir.
8. Denemek için test kullanıcı kimlik bilgilerini girin.

JAR paketleri AAR paketi gönderilir.

## <a name="step-4-download-the-android-adal-and-add-it-to-your-eclipse-workspace"></a>4. adım: Android ADAL karşıdan yükleme ve Eclipse alanınıza ekleyin
Bu, Android projenize ADAL kullanmak için birden çok seçeneğiniz kolay yaptık:

* Bu kitaplık Eclipse ve bağlantı halinde uygulamanıza almak için kaynak kodunu kullanabilirsiniz.
* Android Studio kullanıyorsanız, AAR paket biçimini kullanın ve ikili dosyaları başvuru.

### <a name="option-1-source-zip"></a>Seçenek 1: Kaynak Zip
Kaynak kodu bir kopyasını indirmek için tıklayın **ZIP'i indir** sayfasının sağ tarafında. Veya [karşıdan Github'dan](https://github.com/AzureAD/azure-activedirectory-library-for-android/archive/v1.0.9.tar.gz).

### <a name="option-2-source-via-git"></a>Seçenek 2: Kaynak Git aracılığıyla
Git aracılığıyla SDK kaynak kodunu almak için şunu yazın:

    git clone git@github.com:AzureAD/azure-activedirectory-library-for-android.git
    cd ./azure-activedirectory-library-for-android/src

### <a name="option-3-binaries-via-gradle"></a>Seçenek 3: İkili dosyaları Gradle aracılığıyla
Maven merkezi deposu ikili dosyaları alabilirsiniz. Android Studio projenizde AAR paketi gibi eklenebilir:

```gradle
repositories {
    mavenCentral()
    flatDir {
        dirs 'libs'
    }
    maven {
        url "YourLocalMavenRepoPath\\.m2\\repository"
    }
}
dependencies {
    compile fileTree(dir: 'libs', include: ['*.jar'])
    compile('com.microsoft.aad:adal:1.1.1') {
        exclude group: 'com.android.support'
    } // Recent version is 1.1.1
}
```

### <a name="option-4-aar-via-maven"></a>Seçenek 4: AAR Maven üzerinden
Eklenti M2Eclipse kullanıyorsanız, bağımlılık pom.xml dosyanızda belirtebilirsiniz:

```xml
<dependency>
    <groupId>com.microsoft.aad</groupId>
    <artifactId>adal</artifactId>
    <version>1.1.1</version>
    <type>aar</type>
</dependency>
```


### <a name="option-5-jar-package-inside-the-libs-folder"></a>5. seçenek: JAR libs klasörüne paketin
Maven depodaki JAR dosyasını alın ve içine bırakma **kitaplıklar** projenizdeki klasöre. JAR paketleri dahil olmayan için gerekli kaynakları projenize de kopyalamanız gerekir.

## <a name="step-5-add-references-to-android-adal-to-your-project"></a>5. adım: Android ADAL başvurular projenize ekleyin.
1. Projeniz için bir başvuru ekleyin ve bir Android kitaplığıdır belirtin. Bunu yapmak nasıl kucaklayacaklarından emin değilseniz, daha fazla bilgi alabilirsiniz [Android Studio site](http://developer.android.com/tools/projects/projects-eclipse.html).
2. Proje ayarlarınızı hata ayıklama için proje bağımlılığı ekleyin.
3. Projenizin AndroidManifest.xml dosyasını içerecek şekilde güncelleştirin:

        <uses-permission android:name="android.permission.INTERNET" />
        <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
        <application
            android:allowBackup="true"
            android:debuggable="true"
            android:icon="@drawable/ic_launcher"
            android:label="@string/app_name"
            android:theme="@style/AppTheme" >

            <activity
                android:name="com.microsoft.aad.adal.AuthenticationActivity"
                android:label="@string/title_login_hello_app" >
            </activity>
            ....
        <application/>

4. Ana etkinliklerinizi Authenticationcontext'i örneği oluşturun. Bu çağrı ayrıntılarını bu konunun kapsamı dışındadır olsa da iyi bir başlangıç bakarak alabileceğiniz [Android Native Client örnek](https://github.com/AzureADSamples/NativeClient-Android). Aşağıdaki örnekte, SharedPreferences varsayılan önbellek ve yetkilisi biçiminde `https://login.microsoftonline.com/yourtenant.onmicrosoft.com`:

    `mContext = new AuthenticationContext(MainActivity.this, authority, true); // mContext is a field in your activity`

5. Kullanıcı kimlik bilgilerini girer ve bir kimlik doğrulama kodu aldıktan sonra AuthenticationActivity sonuna işlemek için bu kod bloğunu kopyalayın:

        @Override
         protected void onActivityResult(int requestCode, int resultCode, Intent data) {
             super.onActivityResult(requestCode, resultCode, data);
             if (mContext != null) {
                mContext.onActivityResult(requestCode, resultCode, data);
             }
         }

6. İçin bir belirteç sormak için bir geri çağırma tanımlayın:

        private AuthenticationCallback<AuthenticationResult> callback = new AuthenticationCallback<AuthenticationResult>() {

            @Override
            public void onError(Exception exc) {
                if (exc instanceof AuthenticationException) {
                    textViewStatus.setText("Cancelled");
                    Log.d(TAG, "Cancelled");
                } else {
                    textViewStatus.setText("Authentication error:" + exc.getMessage());
                    Log.d(TAG, "Authentication error:" + exc.getMessage());
                }
            }

            @Override
            public void onSuccess(AuthenticationResult result) {
                mResult = result;

                if (result == null || result.getAccessToken() == null
                        || result.getAccessToken().isEmpty()) {
                    textViewStatus.setText("Token is empty");
                    Log.d(TAG, "Token is empty");
                } else {
                    // request is successful
                    Log.d(TAG, "Status:" + result.getStatus() + " Expired:"
                            + result.getExpiresOn().toString());
                    textViewStatus.setText(PASSED);
                }
            }
        };

7. Son olarak, bu geri çağırma kullanarak için bir belirteç isteyin:

    `mContext.acquireToken(MainActivity.this, resource, clientId, redirect, user_loginhint, PromptBehavior.Auto, "",
                   callback);`

Bir açıklama parametreleri şöyledir:

* *Kaynak* gereklidir ve erişmeye çalıştığınız kaynak değil.
* *ClientID* gereklidir ve Azure AD gelir.
* *RedirectUri* acquireToken çağrısı sağlanması için gerekli değildir. Bu, paket adı ayarlayabilirsiniz.
* *PromptBehavior* önbellek ve tanımlama bilgisi atlamak için kimlik bilgileri istemek için yardımcı olur.
* *geri çağırma* yetkilendirme kodu için bir belirteç değiştirilir sonra çağrılır. Erişim belirteci sahip yazılımdan AuthenticationResult nesne varsa, tarih süresi ve belirteç bilgileri kimliği.
* *acquireTokenSilent* isteğe bağlıdır. Tanıtıcı önbelleğe alma ve belirteç Yenile çağırabilirsiniz. Ayrıca, eşitleme sürümü sağlar. Kabul ettiği *UserID* bir parametre olarak.

        mContext.acquireTokenSilent(resource, clientid, userId, callback );

Bu kılavuzu kullanarak, başarılı bir şekilde Azure Active Directory ile tümleştirmek ihtiyacınız olması gerekir. Bu çalışma daha fazla örnek için AzureADSamples ziyaret / github'daki.

## <a name="important-information"></a>Önemli bilgiler
### <a name="customization"></a>Özelleştirme
Uygulama kaynakları kitaplığı proje kaynakları üzerine yazabilirsiniz. Bu, uygulamanızın yerleşik ortaya çıkar. Bu nedenle, kimlik doğrulama etkinliği düzeni istediğiniz şekilde özelleştirebilirsiniz. ADAL (WebView) kullanan denetimleri Kimliğini tuttuğunuzdan emin olun.

### <a name="broker"></a>Aracısı
Microsoft Intune Şirket portalı uygulamasını Aracısı bileşeni sağlar. Hesap AccountManager içinde oluşturulur. Hesap türüdür "com.microsoft.workaccount." Yalnızca tek bir SSO hesaba AccountManager sağlar. Bir uygulama için cihaz sınaması tamamladıktan sonra kullanıcı için bir SSO tanımlama bilgisi oluşturur.

Bu Doğrulayıcı ve, bir kullanıcı hesabı oluşturduysanız, aracısı hesabı seçin atlamak değil için ADAL kullanır. Aracısı kullanıcıyla atlayabilirsiniz:

   `AuthenticationSettings.Instance.setSkipBroker(true);`

Aracısı kullanım için özel bir RedirectUri kaydetmeniz gerekir. RedirectUri biçiminde olduğunu `msauth://packagename/Base64UrlencodedSignature`. Komut dosyası brokerRedirectPrint.ps1 veya API çağrısı mContext.getBrokerRedirectUri kullanarak uygulamanız için RedirectUri alabilirsiniz. İmza imzalama sertifikalarınızı ilişkilidir.

Geçerli aracısı için bir kullanıcı modelidir. Authenticationcontext'i Aracısı kullanıcı almak için API yöntemi sağlar.

   `String brokerAccount =  mContext.getBrokerUser(); //Broker user is returned if account is valid.`

Uygulama bildiriminizi AccountManager hesaplarını kullanmak için aşağıdaki izinlere sahip olmalıdır. Ayrıntılar için bkz [Android sitesinde AccountManager bilgileri](http://developer.android.com/reference/android/accounts/AccountManager.html).

* GET_ACCOUNTS
* USE_CREDENTIALS
* MANAGE_ACCOUNTS

### <a name="authority-url-and-ad-fs"></a>Yetkili URL'si ve AD FS
Active Directory Federasyon Hizmetleri (AD FS), bu nedenle, örnek bulunabilirliği ve Authenticationcontext'i Oluşturucusu false değerini iletir gerekir STS, üretim tanınmıyor.

Yetkili URL'si STS örneği gerekir ve bir [Kiracı adı](https://login.microsoftonline.com/yourtenant.onmicrosoft.com).

### <a name="querying-cache-items"></a>Önbellek öğelerini sorgulama
ADAL SharedPreferences bazı basit önbelleği ile bir varsayılan önbellekte sorgu işlevleri sağlar. Kullanarak Authenticationcontext'i güncel önbelleğe alabilirsiniz:

    ITokenCacheStore cache = mContext.getCache();

Özelleştirmek istiyorsanız, önbellek uygulamanız da sağlayabilir.

    mContext = new AuthenticationContext(MainActivity.this, authority, true, yourCache);

### <a name="prompt-behavior"></a>Komut istemi davranışı
ADAL komut istemi davranışı belirtmek için bir seçenek sağlar. PromptBehavior.Auto UI yenileme belirteci geçersiz ve kullanıcı kimlik bilgileri gereklidir gösterir. PromptBehavior.Always önbelleği kullanımını atlayın ve her zaman kullanıcı arabirimini göster.

### <a name="silent-token-request-from-cache-and-refresh"></a>Sessiz belirteç isteği önbellek ve yenileme
Sessiz bir belirteç isteğini açılır UI kullanmaz ve bir etkinlik gerektirmez. Bu belirteç önbellekten varsa döndürür. Belirtecin süresi varsa, bu yöntem yenilemeniz çalışır. Yenileme belirtecinin süresi dolmuş ya da başarısız olursa AuthenticationException döndürür.

    Future<AuthenticationResult> result = mContext.acquireTokenSilent(resource, clientid, userId, callback );

Ayrıca, bir eşitleme yapabilirsiniz bu yöntemi kullanarak çağırın. İçin geri çağırma null ayarlayın veya acquireTokenSilentSync kullanın.

### <a name="diagnostics"></a>Tanılama
Birincil bilgi kaynaklarıyla ilgili sorunları tanılamak için bunlar:

* Özel durumlar
* Günlükler
* Ağ izlerini

Bağıntı kimlikleri Kitaplığı'nda tanılama merkezi olduğunu unutmayın. Bağıntı ayarlayabileceğiniz bir ADAL ilişkilendirmek istiyorsanız, istek başına temelinde kimlikleri isteği kodunuzda diğer işlemlerle. Bağıntı kimliği ayarlamazsanız ADAL rastgele bir tane oluşturur. Tüm iletileri günlük ve ağ çağrıları sonra bağıntı kimliği ile damgalı Kendinden oluşturulmuş kimliği değişiklikleri her istek.

#### <a name="exceptions"></a>Özel durumlar
İlk tanılama durumlardır. Yararlı hata iletileri sağlamak deneyin. Yararlı olmayan bir fark ederseniz, Lütfen bir sorun dosya ve bize bildirin. Model ve SDK numarası gibi cihaz bilgileri içerir.

#### <a name="logs"></a>Günlükler
Sorunları tanılamak için kullanabileceğiniz günlük iletilerini oluşturmak için kitaplık yapılandırabilirsiniz. Günlüğe kaydetme oluşturuldukça ADAL her günlük iletiyi kapatmak el kullanan bir geri çağırma yapılandırmak için aşağıdaki çağrıyı yaparak yapılandırın.

    Logger.getInstance().setExternalLogger(new ILogger() {
        @Override
        public void Log(String tag, String message, String additionalMessage, LogLevel level, ADALError errorCode) {
        ...
        // You can write this to log file depending on level or error code.
        writeToLogFile(getApplicationContext(), tag +":" + message + "-" + additionalMessage);
        }
    }

Aşağıdaki kodda gösterildiği gibi özel bir günlük dosyasına iletileri yazılabilir. Ne yazık ki, bir aygıttan günlüklerini alma standart bir yolu yoktur. Bu konuda yardımcı olabilecek bazı hizmetler vardır. Ayrıca kendi bir sunucuya dosya gönderme gibi stok.

    private syncronized void writeToLogFile(Context ctx, String msg) {
       File directory = ctx.getDir(ctx.getPackageName(), Context.MODE_PRIVATE);
       File logFile = new File(directory, "logfile");
       FileOutputStream outputStream = new FileOutputStream(logFile, true);
       OutputStreamWriter osw = new OutputStreamWriter(outputStream);
       osw.write(msg);
       osw.flush();
       osw.close();
    }

Bu günlük düzeyleri şunlardır:
* Hata (özel durumlar)
* Warn (uyarı)
* Info (bilgilendirme)
* Verbose (daha fazla ayrıntı)

Bu gibi günlük düzeyini ayarlayın:

    Logger.getInstance().setLogLevel(Logger.LogLevel.Verbose);

 Tüm günlük iletilerini herhangi özel günlük geri aramalar yanı sıra logcat gönderilir.
Bir günlük bir dosyaya logcat aşağıdaki gibi alabilirsiniz:

    adb logcat > "C:\logmsg\logfile.txt"

 Adb komutları hakkında daha fazla ayrıntı için bkz: [Android sitesinde logcat bilgileri](https://developer.android.com/tools/debugging/debugging-log.html#startingLogcat).

#### <a name="network-traces"></a>Ağ izlerini
ADAL oluşturur HTTP trafiği yakalamak için çeşitli araçları kullanabilirsiniz.  Bu, OAuth protokolüyle aşinaysanız ya da Microsoft veya diğer destek kanallarını tanılama bilgileri sağlamak ihtiyacınız varsa en faydalı olur.

Fiddler kolay HTTP izleme aracıdır. Doğru kayıt ADAL ağ trafiğini kadar ayarlamak için aşağıdaki bağlantıları kullanın. Fiddler veya Charles kullanışlı olması için benzer bir izleme aracı için şifrelenmemiş SSL trafiğini kaydetmek için yapılandırmanız gerekir.  

> [!NOTE]
> Bu yolla oluşturulan izlemeleri erişim belirteçleri, kullanıcı adları ve parolalar gibi üst düzey ayrıcalıklı bilgileri içerebilir. Üretim hesapları kullanıyorsanız, bu izlemelerin üçüncü taraflarla paylaşmayın. Destek almak için bir izleme birine sağlamanız gerekiyorsa, kullanıcı adları ve paylaşımı sizin için sorun parolalarla geçici bir hesap kullanarak sorunu yeniden oluşturun.

* Telerik Web sitesinden: [ayarı yukarı Fiddler için Android](http://docs.telerik.com/fiddler/configure-fiddler/tasks/ConfigureForAndroid)
* Github'dan: [için ADAL Fiddler kurallarını yapılandırma](https://github.com/AzureAD/azure-activedirectory-library-for-android/wiki/How-to-listen-to-httpUrlConnection-in-Android-app-from-Fiddler)

### <a name="dialog-mode"></a>İletişim modu
AcquireToken yöntemi etkinliği olmayan bir iletişim kutusu istemi destekler.

### <a name="encryption"></a>Şifreleme
ADAL belirteçleri ve SharedPreferences deposunda varsayılan olarak şifreler. Ayrıntıları görmek için StorageHelper sınıfta bakabilirsiniz. Android 4.3 (API 18) için güvenilir depolama özel anahtarların Android anahtar deposu kullanıma sunuldu. ADAL, API 18 ve daha yüksek kullanır. ADAL alt SDK sürümleri için kullanmak istiyorsanız, bir gizli anahtar AuthenticationSettings.INSTANCE.setSecretKey, sağlamanız gerekir.

### <a name="oauth2-bearer-challenge"></a>OAuth2 taşıyıcı sınama
AuthenticationParameters sınıfı authorization_uri OAuth2 taşıyıcı sınama almak için işlevsellik sağlar.

### <a name="session-cookies-in-webview"></a>Web görünümü içinde oturum tanımlama bilgileri
Uygulama kapatıldıktan sonra android WebView oturum tanımlama bilgileri temizlemez. Bu örnek kodu kullanarak işleyebilir:

    CookieSyncManager.createInstance(getApplicationContext());
    CookieManager cookieManager = CookieManager.getInstance();
    cookieManager.removeSessionCookie();
    CookieSyncManager.getInstance().sync();

Tanımlama bilgileri hakkında daha fazla ayrıntı için bkz: [Android sitesinde CookieSyncManager bilgileri](http://developer.android.com/reference/android/webkit/CookieSyncManager.html).

### <a name="resource-overrides"></a>Kaynak geçersiz kılmaları
ADAL kitaplığını ProgressDialog iletileri için İngilizce dizeleri içerir. Yerelleştirilmiş dizeleri istiyorsanız, uygulamanızın bunları üzerine yazmalıdır.

     <string name="app_loading">Loading...</string>
     <string name="broker_processing">Broker is processing</string>
     <string name="http_auth_dialog_username">Username</string>
     <string name="http_auth_dialog_password">Password</string>
     <string name="http_auth_dialog_title">Sign In</string>
     <string name="http_auth_dialog_login">Login</string>
     <string name="http_auth_dialog_cancel">Cancel</string>

### <a name="ntlm-dialog-box"></a>NTLM iletişim kutusu
ADAL sürüm 1.1.0 WebViewClient onReceivedHttpAuthRequest olayından aracılığıyla işlenen bir NTLM iletişim kutusu destekler. Düzen ve iletişim kutusu dizeleri özelleştirebilirsiniz.

### <a name="cross-app-sso"></a>Uygulamalar arası SSO'nun
Bilgi [ADAL kullanarak uygulamalar arası SSO'nun android'de etkinleştirmek nasıl](active-directory-sso-android.md).  

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
