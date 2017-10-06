---
title: "aaaAzure AD Başlarken Android | Microsoft Docs"
description: "Nasıl toobuild oturum açma ve Azure AD aramalar için Azure AD ile tümleşen bir Android uygulaması API'leri OAuth kullanılarak korunan."
services: active-directory
documentationcenter: android
author: danieldobalian
manager: mbaldwin
editor: 
ms.assetid: da1ee39f-89d3-4d36-96f1-4eabbc662343
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: mobile-android
ms.devlang: java
ms.topic: article
ms.date: 01/07/2017
ms.author: dadobali
ms.custom: aaddev
ms.openlocfilehash: 1aedc8ff60874b405a182a4ccbfb2c8b4d9d3704
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-azure-ad-into-an-android-app"></a>Android uygulamaya Azure AD tümleştirme
[!INCLUDE [active-directory-devquickstarts-switcher](../../../includes/active-directory-devquickstarts-switcher.md)]

> [!TIP]
> Bizim yeni Hello önizlemesini denemek [Geliştirici Portalı](https://identity.microsoft.com/Docs/Android), hangi yardımcı olacak birkaç dakika içinde Azure AD ile başlamak ve çalıştırmak. Merhaba Geliştirici Portalı, bir uygulamayı kaydetme ve Azure AD kodunuza tümleştirme hello işleminde size rehberlik yapar. İşiniz bittiğinde, bu belirteçleri kabul edebilir ve doğrulama gerçekleştirmek kullanıcılar, Kiracı ve arka uç kimlik doğrulaması yapabilir basit bir uygulama gerekir.
>
>

Bir masaüstü uygulaması geliştiriyorsanız, Azure Active Directory (Azure AD), basit ve kolay, tooauthenticate için kullanıcılarınız, şirket içi Active Directory hesaplarını kullanarak sağlar. Ayrıca, uygulama toosecurely sağlar Office 365 API'leri hello veya Azure API hello gibi tüm web Azure AD tarafından korunan API'si kullanabilir.

Korumalı tooaccess kaynakları gereken Android istemciler için Azure AD hello Active Directory Authentication Library (ADAL) sağlar. ADAL tek amacı Hello toomake Bu, uygulama tooget erişim belirteçleri için kolay. toodemonstrate ne kadar kolay olduğu, biz Android Yapılacaklar listesi uygulaması, yapı:

* Alır erişim belirteçleri hello kullanarak bir Yapılacaklar listesi API çağırma [OAuth 2.0 kimlik doğrulama protokolü](https://msdn.microsoft.com/library/azure/dn645545.aspx).
* Bir kullanıcının yapılacaklar listesini alır.
* Oturumunu kullanıcılar kapatır.

başlatılan tooget, kullanıcı oluşturma ve bir uygulamayı kaydetme Azure AD kiracısı gerekir. Bir kiracı yoksa [öğrenin nasıl tooget bir](active-directory-howto-tenant.md).

## <a name="step-1-download-and-run-hello-nodejs-rest-api-todo-sample-server"></a>1. adım: İndirme ve hello Node.js REST API TODO örnek sunucusu çalıştırma
Merhaba Node.js REST API Yapılacaklar örnek özellikle toowork tek-Kiracı Yapılacaklar REST API'si için Azure AD oluşturmak için varolan örneğimizde karşı yazılır. Bu hello Hızlı Başlangıç için bir önkoşuldur.

Nasıl tooset Bu, bkz: Varolan örneklerimizi hakkında bilgi için [Microsoft Azure Active Directory örnek REST API'si hizmeti için Node.js](active-directory-devquickstarts-webapi-nodejs.md).


## <a name="step-2-register-your-web-api-with-your-azure-ad-tenant"></a>2. adım: Azure AD kiracınıza ile web API kaydetme
Active Directory, iki tür uygulamaları ekleme destekler:

- Web Hizmetleri toousers teklif API'leri
- Web API'leri olanlar erişim (Merhaba Web'de veya bir aygıtta çalışan) uygulamaları

Bu adımda, bu örnek test etmek için yerel olarak çalıştırıyorsanız hello web API kaydediliyor. Normalde, bu web API uygulama tooaccess istediğiniz teklifi işlevselliği bir REST hizmetidir. Azure AD, herhangi bir uç nokta korumaya yardımcı olabilir.

Merhaba Yapılacaklar REST API daha önce başvurulan kaydetme varsayılarak. Ancak bu Azure Active Directory toohelp korumak istediğiniz tüm web API çalışır.

1. İçinde toohello oturum [Azure portal](https://portal.azure.com).
2. Merhaba üst çubuğunda hesabınızı tıklatın. Merhaba, **Directory** listesinde, uygulamanızın hello Azure AD Kiracı tooregister istediğiniz yeri seçin.
3. Tıklatın **daha Hizmetleri** hello sol bölmesinde ve ardından **Azure Active Directory**.
4. Tıklatın **uygulama kayıtlar**ve ardından **Ekle**.
5. Merhaba uygulama için kolay bir ad girin (örneğin, **TodoListService**), select **Web uygulaması ve/veya Web API**, tıklatıp **sonraki**.
6. Merhaba oturum açma URL'sini hello örnek için hello temel URL'sini girin. Varsayılan olarak `https://localhost:8080`.
7. Tıklatın **Tamam** toocomplete hello kayıt.
8. Hello sırasında Azure portal, yine de tooyour uygulama sayfasına gidin, hello uygulama kimliği değerini bulmak ve kopyalayın. Bu daha sonra uygulamanızın yapılandırırken ihtiyacınız vardır.
9. Merhaba gelen **ayarları** -> **özellikleri** sayfasında, hello uygulama kimliği URI'SİNİN güncelleştirmesi - girin `https://<your_tenant_name>/TodoListService`. Değiştir `<your_tenant_name>` Azure AD kiracınıza hello adı.

## <a name="step-3-register-hello-sample-android-native-client-application"></a>3. adım: hello örnek Android yerel istemci uygulaması kaydetme
Bu örnekte, web uygulamanızı kaydetmeniz gerekir. Bu, uygulama toocommunicate hello henüz kayıtlı web API ile sağlar. Azure AD Reddet tooeven, kayıtlı olduğu sürece, uygulama tooask oturum açma için izin verin. Merhaba güvenlik hello modelinin parçası olan.

Daha önce başvurulan hello örnek uygulaması kaydettirilirken varsayılarak. Ancak bu yordam, geliştirmekte herhangi bir uygulama için geçerlidir.

> [!NOTE]
> Neden, hem uygulama hem de web API'si bir kiracı koyma merak ediyor. Tahmin gibi başka bir kiracı Azure AD'den kayıtlı bir API'nin erişen bir uygulama oluşturabilirsiniz. Bunu yaparsanız, müşterilerinizin olacaktır tooconsent toohello hello API hello uygulama kullanımını istenir. İOS için Active Directory Authentication Library sizin için bu onay ilgilenir. Biz daha gelişmiş özellikleri keşfetmenizde bu hello iş gerekli tooaccess hello paketinin Microsoft Azure ve Office yanı sıra, başka bir hizmet sağlayıcısı APIs önemli bir parçası olduğunu görürsünüz. Web API ve hello uygulamanızı kayıtlı için şu an için aynı Kiracı, sizden izin göremezsiniz. Yalnızca kendi şirket toouse için uygulama geliştirme yapıyorsanız bu genellikle hello durumdur.

1. İçinde toohello oturum [Azure portal](https://portal.azure.com).
2. Merhaba üst çubuğunda hesabınızı tıklatın. Merhaba, **Directory** listesinde, uygulamanızın hello Azure AD Kiracı tooregister istediğiniz yeri seçin.
3. Tıklatın **daha Hizmetleri** hello sol bölmesinde ve ardından **Azure Active Directory**.
4. Tıklatın **uygulama kayıtlar**ve ardından **Ekle**.
5. Merhaba uygulama için kolay bir ad girin (örneğin, **TodoListClient Android**), select **yerel istemci uygulaması**, tıklatıp **sonraki**.
6. Merhaba yeniden yönlendirme URI'si, girin `http://TodoListClient`. **Son**'a tıklayın.
7. Merhaba uygulama sayfasından hello uygulama kimliği değerini bulmak ve kopyalayın. Bu daha sonra uygulamanızın yapılandırırken ihtiyacınız vardır.
8. Merhaba gelen **ayarları** sayfasında, **gerekli izinler** seçip **Ekle**.  Bulun ve TodoListService seçin, hello eklemeniz **erişim TodoListService** altında izni **izinlere temsilci**, tıklatıp **Bitti**.

toobuild Maven ile Merhaba en üst düzeyde pom.xml kullanabilirsiniz:

1. Bu depodaki tercih ettiğiniz bir dizine kopyalayın:

  `$ git clone git@github.com:AzureADSamples/NativeClient-Android.git`  
2. Merhaba Hello adımları [Önkoşullar tooset Android için Maven ortamınızı](https://github.com/MSOpenTech/azure-activedirectory-library-for-android/wiki/Setting-up-maven-environment-for-Android).
3. Merhaba öykünücü SDK 19 ile ayarlayın.
4. Merhaba depodaki kopyaladığınız toohello kök klasörden gidin.
5. Bu komutu çalıştırın:`mvn clean install`
6. Merhaba dizin toohello hızlı başlangıç örnek değiştirin:`cd samples\hello`
7. Bu komutu çalıştırın:`mvn android:deploy android:run`

   Merhaba uygulama başlatma görmeniz gerekir.
8. Test kullanıcı kimlik bilgilerini tootry girin.

JAR paketleri hello AAR paketi gönderilir.

## <a name="step-4-download-hello-android-adal-and-add-it-tooyour-eclipse-workspace"></a>4. adım: hello Android ADAL indirin ve tooyour Eclipse çalışma Ekle
Bu, toohave daha kolay birden çok seçenekleri toouse ADAL Android projenize yaptık:

* Bu kitaplığı Eclipse ve bağlantı tooyour uygulamasına hello kaynak kodu tooimport kullanabilirsiniz.
* Android Studio kullanıyorsanız, hello AAR paket biçimi ve başvuru hello ikili dosyalarını kullanabilirsiniz.

### <a name="option-1-source-zip"></a>Seçenek 1: Kaynak Zip
toodownload hello kaynak kodu, bir kopyasını tıklatın **ZIP'i indir** hello hello sayfasının sağ tarafında. Veya [karşıdan Github'dan](https://github.com/AzureAD/azure-activedirectory-library-for-android/archive/v1.0.9.tar.gz).

### <a name="option-2-source-via-git"></a>Seçenek 2: Kaynak Git aracılığıyla
Merhaba tooget hello kaynak kodunun Git, üzerinden yazın:

    git clone git@github.com:AzureAD/azure-activedirectory-library-for-android.git
    cd ./azure-activedirectory-library-for-android/src

### <a name="option-3-binaries-via-gradle"></a>Seçenek 3: İkili dosyaları Gradle aracılığıyla
Merhaba Maven merkezi deposu hello ikili dosyaları alabilirsiniz. Android Studio projenizde Hello AAR paketi gibi eklenebilir:

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
Merhaba M2Eclipse eklenti kullanıyorsanız, pom.xml dosyanızda hello bağımlılık belirtebilirsiniz:

```xml
<dependency>
    <groupId>com.microsoft.aad</groupId>
    <artifactId>adal</artifactId>
    <version>1.1.1</version>
    <type>aar</type>
</dependency>
```


### <a name="option-5-jar-package-inside-hello-libs-folder"></a>5. seçenek: JAR hello libs klasörüne paketin
Merhaba Maven depodaki hello JAR dosyasını alın ve hello bırakma **kitaplıklar** projenizdeki klasöre. Merhaba JAR paketleri dahil olmayan için toocopy hello gerekli kaynakları tooyour proje de gerekir.

## <a name="step-5-add-references-tooandroid-adal-tooyour-project"></a>5. adım: başvuruları tooAndroid ADAL tooyour proje ekleme
1. Bir başvuru tooyour proje ekleyin ve bir Android kitaplığıdır belirtin. Belirsiz varsa nasıl toodo bunu hello hakkında daha fazla bilgi alabileceğiniz [Android Studio site](http://developer.android.com/tools/projects/projects-eclipse.html).
2. Proje ayarlarınızı hata ayıklama için hello proje bağımlılığı ekleyin.
3. Projenizin AndroidManifest.xml dosya tooinclude güncelleştirin:

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

4. Ana etkinliklerinizi Authenticationcontext'i örneği oluşturun. Bu çağrıyı Hello ayrıntılarını olan bu konuda hello kapsamı dışındadır, ancak hello bakarak iyi bir başlangıç alabilirsiniz [Android Native Client örnek](https://github.com/AzureADSamples/NativeClient-Android). Aşağıdaki örneğine hello SharedPreferences hello varsayılan önbellek ve yetkilisi hello biçiminde `https://login.microsoftonline.com/yourtenant.onmicrosoft.com`:

    `mContext = new AuthenticationContext(MainActivity.this, authority, true); // mContext is a field in your activity`

5. Hello kullanıcı kimlik bilgilerini girer ve bir kimlik doğrulama kodu aldıktan sonra bu kodu blok toohandle hello sonuna AuthenticationActivity Kopyala:

        @Override
         protected void onActivityResult(int requestCode, int resultCode, Intent data) {
             super.onActivityResult(requestCode, resultCode, data);
             if (mContext != null) {
                mContext.onActivityResult(requestCode, resultCode, data);
             }
         }

6. tooask bir belirteci için bir geri çağırma tanımlayın:

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

Merhaba parametreleri açıklaması aşağıda verilmiştir:

* *Kaynak* gereklidir ve tooaccess çalıştığınız hello kaynaktır.
* *ClientID* gereklidir ve Azure AD gelir.
* *RedirectUri* değil hello acquireToken çağrısı için sağlanan gerekli toobe. Bu, paket adı ayarlayabilirsiniz.
* *PromptBehavior* tooask kimlik bilgileri tooskip hello önbellek ve tanımlama bilgisi için yardımcı olur.
* *geri çağırma* hello yetkilendirme kodu için bir belirteç değiştirilir sonra çağrılır. Erişim belirteci sahip yazılımdan AuthenticationResult nesne varsa, tarih süresi ve belirteç bilgileri kimliği.
* *acquireTokenSilent* isteğe bağlıdır. Toohandle önbelleğe alma ve belirteç yenileme çağırabilirsiniz. Ayrıca, hello eşitleme sürümü sağlar. Kabul ettiği *UserID* bir parametre olarak.

        mContext.acquireTokenSilent(resource, clientid, userId, callback );

Bu kılavuzu kullanarak, hangi toosuccessfully Azure Active Directory ile tümleştirmeniz olması gerekir. Bu çalışma daha fazla örnek için hello AzureADSamples ziyaret / github'daki.

## <a name="important-information"></a>Önemli bilgiler
### <a name="customization"></a>Özelleştirme
Uygulama kaynakları kitaplığı proje kaynakları üzerine yazabilirsiniz. Bu, uygulamanızın yerleşik ortaya çıkar. Bu nedenle, istediğiniz kimlik doğrulama etkinliği düzeni hello biçimde özelleştirebilirsiniz. Merhaba denetimleri emin tookeep hello Kimliğini olması, ADAL (WebView) kullanır.

### <a name="broker"></a>Aracısı
Merhaba Microsoft Intune Şirket portalı uygulamasını hello Aracısı bileşeni sağlar. Merhaba hesap AccountManager içinde oluşturulur. Merhaba hesap türüdür "com.microsoft.workaccount." Yalnızca tek bir SSO hesaba AccountManager sağlar. Bir hello uygulama için hello aygıt sınaması tamamladıktan sonra hello kullanıcı için bir SSO tanımlama bilgisi oluşturur.

ADAL, bir kullanıcı hesabı, bu kimlik doğrulayıcı oluşturulur ve değil tooskip seçerseniz hello aracısı hesabı kullanır. Merhaba Aracısı kullanıcıyla atlayabilirsiniz:

   `AuthenticationSettings.Instance.setSkipBroker(true);`

Tooregister özel RedirectUri Aracısı kullanımı için gerekir. RedirectUri hello biçiminde olduğunu `msauth://packagename/Base64UrlencodedSignature`. Merhaba betik brokerRedirectPrint.ps1 veya hello API çağrısı mContext.getBrokerRedirectUri kullanarak uygulamanız için RedirectUri alabilirsiniz. Merhaba imza imzalama sertifikalarının ilgili tooyour değil.

Merhaba geçerli aracısı için bir kullanıcı modelidir. Authenticationcontext'i hello API yöntemi tooget hello Aracısı kullanıcı sağlar.

   `String brokerAccount =  mContext.getBrokerUser(); //Broker user is returned if account is valid.`

Uygulama bildiriminizi izinleri toouse AccountManager hesapları aşağıdaki hello olması gerekir. Merhaba Ayrıntılar için bkz [hello Android sitesinde AccountManager bilgileri](http://developer.android.com/reference/android/accounts/AccountManager.html).

* GET_ACCOUNTS
* USE_CREDENTIALS
* MANAGE_ACCOUNTS

### <a name="authority-url-and-ad-fs"></a>Yetkili URL'si ve AD FS
Hello Authenticationcontext'i Oluşturucusu false değerini iletir ve örnek bulma tooturn gerekir böylece active Directory Federasyon Hizmetleri (AD FS) STS, üretim tanınmıyor.

Merhaba yetkili URL'si STS örneği gerekir ve bir [Kiracı adı](https://login.microsoftonline.com/yourtenant.onmicrosoft.com).

### <a name="querying-cache-items"></a>Önbellek öğelerini sorgulama
ADAL SharedPreferences bazı basit önbelleği ile bir varsayılan önbellekte sorgu işlevleri sağlar. Kullanarak Authenticationcontext'i hello güncel önbelleğe alabilirsiniz:

    ITokenCacheStore cache = mContext.getCache();

Toocustomize istiyorsanız, önbellek uygulamanızı de sağlayabilirsiniz.

    mContext = new AuthenticationContext(MainActivity.this, authority, true, yourCache);

### <a name="prompt-behavior"></a>Komut istemi davranışı
ADAL, bir seçenek toospecify komut istemi davranışı sağlar. PromptBehavior.Auto hello UI hello yenileme belirteci geçersiz ve kullanıcı kimlik bilgileri gereklidir varsa gösterir. PromptBehavior.Always hello önbelleği kullanımını atlayın ve her zaman hello UI gösterir.

### <a name="silent-token-request-from-cache-and-refresh"></a>Sessiz belirteç isteği önbellek ve yenileme
Sessiz bir belirteç isteğini hello UI açılır kullanmaz ve bir etkinlik gerektirmez. Bu bir belirteci varsa hello önbellekten döndürür. Merhaba belirtecinin süresi varsa, bu yöntem toorefresh çalışır. Merhaba yenileme belirtecinin süresi dolmuş ya da başarısız olursa AuthenticationException döndürür.

    Future<AuthenticationResult> result = mContext.acquireTokenSilent(resource, clientid, userId, callback );

Ayrıca, bir eşitleme yapabilirsiniz bu yöntemi kullanarak çağırın. Null toocallback ayarlayın veya acquireTokenSilentSync kullanın.

### <a name="diagnostics"></a>Tanılama
Merhaba birincil bilgi kaynaklarıyla ilgili sorunları tanılamak için bunlar:

* Özel durumlar
* Günlükler
* Ağ izlerini

Bağıntı kimlikleri merkezi toohello tanılama hello kitaplığında olduğunu unutmayın. Bir ADAL isteği kodunuzda diğer işlemlerle toocorrelate istiyorsanız, bir istek başına temelinde bağıntı kimliklerinizi ayarlayabilirsiniz. Bağıntı kimliği ayarlamazsanız ADAL rastgele bir tane oluşturur. Tüm iletileri günlük ve ağ çağrıları sonra hello bağıntı kimliği ile damgalı Merhaba her istek kimliği değişiklikleri otomatik olarak oluşturulur.

#### <a name="exceptions"></a>Özel durumlar
Özel durumları olan hello ilk tanılama. Biz tooprovide yararlı hata iletileri deneyin. Yararlı olmayan bir fark ederseniz, Lütfen bir sorun dosya ve bize bildirin. Model ve SDK numarası gibi cihaz bilgileri içerir.

#### <a name="logs"></a>Günlükler
Merhaba kitaplığı toogenerate yapılandırabilirsiniz sorunları tanılamak günlük iletilerini toohelp kullanabilirsiniz. Merhaba aşağıdaki tooconfigure oluşturuldukça ADAL toohand her günlüğü iletisi kapalı kullanacağı bir geri çağırma çağrısı yaparak günlüğe kaydetmeyi yapılandırma.

    Logger.getInstance().setExternalLogger(new ILogger() {
        @Override
        public void Log(String tag, String message, String additionalMessage, LogLevel level, ADALError errorCode) {
        ...
        // You can write this toolog file depending on level or error code.
        writeToLogFile(getApplicationContext(), tag +":" + message + "-" + additionalMessage);
        }
    }

İletileri tooa özel günlük dosyası hello kod aşağıdaki gösterildiği gibi yazılabilir. Ne yazık ki, bir aygıttan günlüklerini alma standart bir yolu yoktur. Bu konuda yardımcı olabilecek bazı hizmetler vardır. Ayrıca kendi gibi gönderen hello dosya tooa sunucu stok.

    private syncronized void writeToLogFile(Context ctx, String msg) {
       File directory = ctx.getDir(ctx.getPackageName(), Context.MODE_PRIVATE);
       File logFile = new File(directory, "logfile");
       FileOutputStream outputStream = new FileOutputStream(logFile, true);
       OutputStreamWriter osw = new OutputStreamWriter(outputStream);
       osw.write(msg);
       osw.flush();
       osw.close();
    }

Bunlar hello günlük düzeyleri şunlardır:
* Hata (özel durumlar)
* Warn (uyarı)
* Info (bilgilendirme)
* Verbose (daha fazla ayrıntı)

Bu gibi hello günlük düzeyini ayarlayın:

    Logger.getInstance().setLogLevel(Logger.LogLevel.Verbose);

 Tüm günlük iletilerini toologcat, toplama tooany özel günlük geri gönderilir.
Bir günlük tooa dosyası logcat aşağıdaki gibi alabilirsiniz:

    adb logcat > "C:\logmsg\logfile.txt"

 Merhaba adb komutları hakkında daha fazla bilgi için bkz [hello Android sitesinde logcat bilgileri](https://developer.android.com/tools/debugging/debugging-log.html#startingLogcat).

#### <a name="network-traces"></a>Ağ izlerini
ADAL oluşturan çeşitli araçlar toocapture hello HTTP trafiği kullanabilirsiniz.  Bu, OAuth protokolünün hello ile aşinaysanız veya tooprovide tanılama bilgileri tooMicrosoft veya diğer destek kanallarını gerekirse en faydalı olur.

Fiddler hello kolay HTTP izleme aracıdır. Kullanım hello aşağıdaki bağlantılar tooset bunun toocorrectly kaydı ADAL ağ trafiği. Bir izleme aracı için fiddler'ı veya Charles toobe yararlı gibi şifrelenmemiş toorecord SSL trafiğini yapılandırmalısınız.  

> [!NOTE]
> Bu yolla oluşturulan izlemeleri erişim belirteçleri, kullanıcı adları ve parolalar gibi üst düzey ayrıcalıklı bilgileri içerebilir. Üretim hesapları kullanıyorsanız, bu izlemelerin üçüncü taraflarla paylaşmayın. Toosupply izleme toosomeone sipariş tooget desteğe ihtiyacınız varsa, hello sorunu paylaşma sorun yok geçici bir hesap kullanıcı adlarını ve parolaları kullanarak yeniden oluşturun.

* Merhaba Telerik Web sitesinden: [ayarı yukarı Fiddler için Android](http://docs.telerik.com/fiddler/configure-fiddler/tasks/ConfigureForAndroid)
* Github'dan: [için ADAL Fiddler kurallarını yapılandırma](https://github.com/AzureAD/azure-activedirectory-library-for-android/wiki/How-to-listen-to-httpUrlConnection-in-Android-app-from-Fiddler)

### <a name="dialog-mode"></a>İletişim modu
Merhaba acquireToken yöntemi etkinliği olmayan bir iletişim kutusu istemi destekler.

### <a name="encryption"></a>Şifreleme
ADAL hello belirteçleri ve SharedPreferences deposunda varsayılan olarak şifreler. Merhaba StorageHelper sınıfı toosee hello ayrıntıları bakabilirsiniz. Android 4.3 (API 18) için güvenilir depolama özel anahtarların Android anahtar deposu kullanıma sunuldu. ADAL, API 18 ve daha yüksek kullanır. Daha düşük SDK sürümleri için toouse ADAL istiyorsanız tooprovide AuthenticationSettings.INSTANCE.setSecretKey adresindeki gizli bir anahtar gerekir.

### <a name="oauth2-bearer-challenge"></a>OAuth2 taşıyıcı sınama
Merhaba AuthenticationParameters sınıfı hello OAuth2 taşıyıcı sınama gelen işlevselliği tooget authorization_uri sağlar.

### <a name="session-cookies-in-webview"></a>Web görünümü içinde oturum tanımlama bilgileri
Merhaba uygulama kapatıldıktan sonra android WebView oturum tanımlama bilgileri temizlemez. Bu örnek kodu kullanarak işleyebilir:

    CookieSyncManager.createInstance(getApplicationContext());
    CookieManager cookieManager = CookieManager.getInstance();
    cookieManager.removeSessionCookie();
    CookieSyncManager.getInstance().sync();

Tanımlama bilgileri hakkında daha fazla ayrıntı için bkz: Merhaba [hello Android sitesinde CookieSyncManager bilgileri](http://developer.android.com/reference/android/webkit/CookieSyncManager.html).

### <a name="resource-overrides"></a>Kaynak geçersiz kılmaları
Merhaba ADAL kitaplığı ProgressDialog iletileri için İngilizce dizeleri içerir. Yerelleştirilmiş dizeleri istiyorsanız, uygulamanızın bunları üzerine yazmalıdır.

     <string name="app_loading">Loading...</string>
     <string name="broker_processing">Broker is processing</string>
     <string name="http_auth_dialog_username">Username</string>
     <string name="http_auth_dialog_password">Password</string>
     <string name="http_auth_dialog_title">Sign In</string>
     <string name="http_auth_dialog_login">Login</string>
     <string name="http_auth_dialog_cancel">Cancel</string>

### <a name="ntlm-dialog-box"></a>NTLM iletişim kutusu
ADAL sürüm 1.1.0 hello onReceivedHttpAuthRequest WebViewClient olayından aracılığıyla işlenen bir NTLM iletişim kutusu destekler. Merhaba düzeni ve dizeleri hello iletişim kutusu için özelleştirebilirsiniz.

### <a name="cross-app-sso"></a>Uygulamalar arası SSO'nun
Bilgi [nasıl tooenable uygulamalar arası SSO'nun ADAL kullanarak Android üzerinde](active-directory-sso-android.md).  

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
