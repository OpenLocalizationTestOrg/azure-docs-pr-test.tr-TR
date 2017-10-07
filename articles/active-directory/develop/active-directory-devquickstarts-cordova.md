---
title: "aaaAzure AD Başlarken Cordova | Microsoft Docs"
description: "Nasıl toobuild bir Cordova uygulaması, oturum açma için Azure AD ile tümleşir ve OAuth kullanarak Azure AD korumalı API'lerini çağırır."
services: active-directory
documentationcenter: 
author: vibronet
manager: mbaldwin
editor: 
ms.assetid: b1a8d7bd-7ad6-44d5-8ccb-5255bb623345
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: javascript
ms.topic: article
ms.date: 01/07/2017
ms.author: vittorib
ms.custom: aaddev
ms.openlocfilehash: 573ed638c2180c5231648bcb8c49ceb6f53296f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-azure-ad-with-an-apache-cordova-app"></a>Azure AD tümleştirme bir Apache Cordova uygulaması
[!INCLUDE [active-directory-devquickstarts-switcher](../../../includes/active-directory-devquickstarts-switcher.md)]

[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

Mobil aygıtlarda tam özellikli yerel uygulamalar olarak çalıştırabilirsiniz Apache Cordova toodevelop HTML5/JavaScript uygulamaları kullanabilir. Azure Active Directory ile (Azure AD), kurumsal düzeyde kimlik doğrulama özellikleri tooyour Cordova uygulamaları ekleyebilirsiniz.

Cordova eklentisi Azure sarmalar AD yerel SDK'ları iOS, Android, Windows mağazası ve Windows Phone. Eklenti, uygulamanızın geliştirebilirsiniz olduğunu kullanarak toosupport kullanıcılarınızın Windows Server Active Directory hesapları, kazanç erişim tooOffice 365 ve Azure API'leri ile oturum açma ve hatta korunmasına yardımcı olur çağrıları tooyour kendi özel web API.

Bu öğreticide, hello Apache Cordova eklentisi Active Directory Authentication Library (ADAL) tooimprove basit bir uygulama için özellikler aşağıdaki hello ekleyerek kullanacağız:

* Yalnızca birkaç satır kod ile bir kullanıcının kimliğini doğrulamak ve bir belirteç elde edin.
* Merhaba sonuçlarını görüntülemek ve bu dizine, belirteç tooinvoke hello grafik API'si tooquery kullanın.  
* Merhaba ADAL belirteç önbelleği toominimize kimlik doğrulamasını kullan hello kullanıcıya sorar.

toomake Bu geliştirmeler, gerekir:

1. Bir uygulamayı Azure AD'ye kaydedin.
2. Kod tooyour uygulama toorequest belirteçleri ekleyin.
3. Merhaba grafik API'si sorgulanırken kod toouse hello belirteci ekleyin ve sonuçları görüntüler.
4. Merhaba Cordova dağıtım projesi oluşturmak tüm hello platformlarında, tootarget istediğiniz, hello Cordova ADAL eklenti ekleme ve test hello çözüm içinde Öykünücüler.

## <a name="prerequisites"></a>Ön koşullar
toocomplete Bu öğretici, gerekir:

* Uygulama geliştirme hakları olan bir hesabın sahip olduğu bir Azure AD kiracısı.
* Apache Cordova toouse yapılandırmış bir geliştirme ortamı.  

Her ikisi de varsa, ayarlamak, doğrudan toostep 1 devam edin.

Azure AD kiracısı yoksa, hello kullan [yönergeler tooget bir](active-directory-howto-tenant.md).

Apache Cordova makinenizde ayarlanan yoksa, hello aşağıdakileri yükleyin:

* [Git](http://git-scm.com/book/en/v2/Getting-Started-Installing-Git)
* [Node.js](https://nodejs.org/download/)
* [Cordova CLI](https://cordova.apache.org/) (NPM Paket Yöneticisi kolayca yüklenebilir: `npm install -g cordova`)

yüklemeleri önceki hello hello PC ve Mac hello çalışması gerekir

Her hedef platformu farklı Önkoşullar vardır:

* toobuild ve Windows Tablet/PC veya Windows Phone için uygulama çalıştırın:
  * Yükleme [Windows Update 2 veya sonraki sürümü için Visual Studio 2013](http://www.visualstudio.com/downloads/download-visual-studio-vs#d-express-windows-8) (Express veya başka bir sürümü) veya [Visual Studio 2015](https://www.visualstudio.com/downloads/download-visual-studio-vs#d-community).

* toobuild ve iOS için uygulama çalıştırın:

  * Xcode yükleme 6.x veya sonraki bir sürümü. Hello karşıdan [Apple Developer site](http://developer.apple.com/downloads) veya hello [Mac App Store](http://itunes.apple.com/us/app/xcode/id497799835?mt=12).
  * Yükleme [ios-SIM](https://www.npmjs.org/package/ios-sim). İOS simülatörü hello komut satırından içinde toostart iOS uygulamalarını bunu kullanabilirsiniz. (Kolayca hello terminal yükleyebilirsiniz: `npm install -g ios-sim`.)
* toobuild ve Android için uygulama çalıştırın:

  * Yükleme [Java Geliştirme Seti (JDK) 7](http://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html) veya sonraki bir sürümü. Emin olun `JAVA_HOME` (ortam değişkeni), toohello JDK yükleme yolu (örneğin, C:\Program Files\Java\jdk1.7.0_75) göre doğru şekilde ayarlanır.
  * Yükleme [Android SDK](http://developer.android.com/sdk/installing/index.html?pkg=tools) ve hello ekleyin `<android-sdk-location>\tools` konum (örneğin, C:\tools\Android\android-sdk\tools) tooyour `PATH` ortam değişkeni.
  * Android SDK Yöneticisi'ni açın (örneğin, terminal hello aracılığıyla: `android`) ve yükleyin:
    * *Android 5.0.1 (API 21)* platform SDK'si
    * *Android SDK derleme araçlarını* sürüm 19.1.0 veya daha yenisi
    * *Android desteği depo* (ek özellikler)

  Merhaba Android SDK varsayılan öykünücü örnek sağlamaz. Çalıştırarak oluşturmak `android avd` hello terminal ve ardından seçerek **oluşturma**toorun hello Android uygulamasını bir öykünücü istiyorsanız. 19 veya daha yüksek bir API düzeyi öneririz. Merhaba Android öykünücü ve oluşturma seçenekleri hakkında daha fazla bilgi için bkz: [AVD Yöneticisi](http://developer.android.com/tools/help/avd-manager.html) hello Android sitesinde.

## <a name="step-1-register-an-application-with-azure-ad"></a>1. adım: bir uygulamayı Azure AD ile kaydedin.
Bu adım isteğe bağlıdır. Bu öğretici, kendi Kiracı sağlama yapmadan eylem örnek toosee kullanabileceğiniz önceden sağlanan değerlerin hello sağlar. Ancak, bu adımı gerçekleştirmek ve kendi uygulamaları oluştururken gerekli olacağı için hello işlemiyle aşina öneririz.

Azure AD uygulamaları bilinen belirteçleri tooonly verir. Azure AD, uygulamanızdan kullanmadan önce toocreate bir girdi için kiracınızda gerekir. Yeni bir uygulama kiracınızda tooregister:

1. İçinde toohello oturum [Azure portal](https://portal.azure.com).
2. Merhaba üst çubuğunda hesabınızı tıklatın. Merhaba, **Directory** listesinde, uygulamanızın hello Azure AD Kiracı tooregister istediğiniz yeri seçin.
3. Tıklatın **daha Hizmetleri** hello sol bölmesinde ve ardından **Azure Active Directory**.
4. Tıklatın **uygulama kayıtlar**ve ardından **Ekle**.
5. Merhaba komut istemlerini izleyin ve oluşturma bir **yerel istemci uygulaması**. (Cordova uygulamaları HTML bağlı olsa da, bir yerel istemci uygulaması oluşturuyoruz. Merhaba **yerel istemci uygulaması** seçeneği seçili olmalıdır veya Merhaba uygulaması çalışmayacak.)
  * **Ad** uygulama toousers açıklar.
  * **Yeniden yönlendirme URI'si** hello tooreturn belirteçleri tooyour uygulama kullanılan URI değil. Girin **http://MyDirectorySearcherApp**.

Kayıt işlemini tamamladıktan sonra Azure AD benzersiz uygulama kimliği tooyour uygulama atar. Bu değer hello sonraki bölümlerde gerekir. Merhaba uygulama sekmesinde yeni uygulama oluşturulan hello bulabilirsiniz.

toorun `DirSearchClient Sample`, yeni oluşturulan hello uygulama izni tooquery hello Azure AD Graph API verin:

1. Merhaba gelen **ayarları** sayfasında, **gerekli izinler**ve ardından **Ekle**.  
2. Hello Azure Active Directory uygulamasını seçmek **Microsoft Graph** olarak API hello ve hello ekleyin **erişim hello dizini hello oturum açmış kullanıcı olarak** altında izni **atanan İzinleri**.  Bu, kullanıcılar için uygulama tooquery hello grafik API'si sağlar.

## <a name="step-2-clone-hello-sample-app-repository"></a>2. adım: hello örnek uygulama depoyu kopyalayın
Kabuk veya komut satırı hello aşağıdaki komutu yazın:

    git clone -b skeleton https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-Cordova.git

## <a name="step-3-create-hello-cordova-app"></a>3. adım: Merhaba Cordova uygulaması oluşturma
Birden çok yol toocreate Cordova uygulamaları vardır. Bu öğreticide, hello Cordova komut satırı arabirimi (CLI) kullanacağız.

1. Kabuk veya komut satırı hello aşağıdaki komutu yazın:

        cordova create DirSearchClient

   Bu komut, hello klasör yapısını ve hello Cordova projesi için askılamayı oluşturur.

2. Toohello yeni DirSearchClient klasör taşınamadı:

        cd .\DirSearchClient

3. Hello başlangıç projesi Merhaba içeriğine, Dosya Yöneticisi veya, kabuk komutu aşağıdaki hello kullanarak hello www alt klasörüne kopyalayın:

  * Windows:`xcopy ..\NativeClient-MultiTarget-Cordova\DirSearchClient www /E /Y`
  * Mac:`cp -r  ../NativeClient-MultiTarget-Cordova/DirSearchClient/* www`

4. Merhaba beyaz liste eklentisini ekleyin. Bu, hello grafik API'si çağırma için gereklidir.

        cordova plugin add cordova-plugin-whitelist

5. Toosupport istediğiniz tüm hello platformlar ekleyin. bir çalışma örneği toohave, tooexecute en az bir komutları aşağıdaki Merhaba, gerekir. Olmaz mümkün tooemulate iOS Windows olması veya bir Mac bilgisayar Windows'ta öykünmek unutmayın

        cordova platform add android
        cordova platform add ios
        cordova platform add windows

6. Cordova eklentisi tooyour projesi için ADAL Hello ekleyin:

        cordova plugin add cordova-plugin-ms-adal

## <a name="step-4-add-code-tooauthenticate-users-and-obtain-tokens-from-azure-ad"></a>4. adım: kodu tooauthenticate kullanıcı ekleyin ve Azure AD'den belirteçleri elde
Bu öğreticide geliştirirken Merhaba uygulaması bir Basit Dizin arama özelliğini sağlar. Merhaba kullanıcı daha sonra hello dizini hello diğer herhangi bir kullanıcı adını yazın ve bazı temel öznitelikler görselleştirin. Merhaba başlangıç projesi hello tanımı hello temel kullanıcı arabiriminin hello uygulamada (www/index.html) içerir ve temel uygulama olay bağlayan hello yapı iskelesi, kullanıcı arabirimi bağlamaları döngüleri görüntü mantığında (www/js/index.js) sonuçlanır. Merhaba, sol yalnızca kimlik görevleri uygulayan tooadd hello mantığı bir görevdir.

Merhaba kodunuzda toodo gereken ilk şey uygulamanızı tanımlamak için Azure AD kullanır hello Protokolü değerleri tanıtmak olduğunu ve kaynakları, hedefleyen hello. Bu değerleri kullanılan tooconstruct hello belirteç isteklerini daha sonra olacaktır. Aşağıdaki kod parçacığında hello dosyanın üst kısmındaki hello index.js hello ekleyin:

```javascript
var authority = "https://login.microsoftonline.com/common",
    redirectUri = "http://MyDirectorySearcherApp",
    resourceUri = "https://graph.windows.net",
    clientId = "a5d92493-ae5a-4a9f-bcbf-9f1d354067d3",
    graphApiVersion = "2013-11-08";
```

Merhaba `redirectUri` ve `clientId` değerleri, uygulamanızı Azure AD'de açıklayan hello değerler eşleşmelidir. Merhaba olanlardan bulabilirsiniz **yapılandırma** 1. adımda Bu öğreticide daha önce açıklandığı gibi hello Azure portal sekmesinde.

> [!NOTE]
> Yeni bir uygulama, kendi Kiracı kayıt değil için ettiyseniz, olduğu gibi hello önceden yapılandırılmış değerleri yalnızca yapıştırabilirsiniz. Üretim için yöneliktir uygulamalarınız için her zaman kendi giriş oluşturmalısınız olsa hello örnek çalıştıran, daha sonra görebilirsiniz.

Ardından, hello belirteç isteği kodu ekleyin. Merhaba arasında parçacığını aşağıdaki hello Ekle `search` ve `renderData` tanımları:

```javascript
    // Shows hello user authentication dialog box if required
    authenticate: function (authCompletedCallback) {

        app.context = new Microsoft.ADAL.AuthenticationContext(authority);
        app.context.tokenCache.readItems().then(function (items) {
            if (items.length > 0) {
                authority = items[0].authority;
                app.context = new Microsoft.ADAL.AuthenticationContext(authority);
            }
            // Attempt tooauthorize hello user silently
            app.context.acquireTokenSilentAsync(resourceUri, clientId)
            .then(authCompletedCallback, function () {
                // We require user credentials, so this triggers hello authentication dialog box
                app.context.acquireTokenAsync(resourceUri, clientId, redirectUri)
                .then(authCompletedCallback, function (err) {
                    app.error("Failed tooauthenticate: " + err);
                });
            });
        });

    },
```
Bu işlev, iki ana bölüme çiğnemekten tarafından inceleyelim.
Bu örnek karşılıklı toobeing tooa belirli bir bağlı tasarlanmış toowork tüm Kiracı ile aynıdır. Merhaba kullanan hello kullanıcı tooenter herhangi bir hesabı kimlik doğrulaması anında sağlar ve ait olduğu hello isteği toohello Kiracı yönlendirir "/ ortak" uç nokta.

Bir belirteç zaten depolanıyorsa hello ADAL önbellek toosee hello yöntemi ilk bu parçası olup olmadığını denetler. Bu durumda, hello yöntemi nereden hello belirteci ADAL yeniden geldiğini hello kiracılar kullanır. Bu gerekli tooavoid hello kullan "/ ortak", her zaman yeni bir hesap hello kullanıcı tooenter soran içinde sonuçları fazladan istemleri olmasıdır.

```javascript
        app.context = new Microsoft.ADAL.AuthenticationContext(authority);
        app.context.tokenCache.readItems().then(function (items) {
            if (items.length > 0) {
                authority = items[0].authority;
                app.context = new Microsoft.ADAL.AuthenticationContext(authority);
            }
```
Merhaba yöntemi Hello ikinci bölümü hello uygun belirteç isteği gerçekleştirir. Merhaba `acquireTokenSilentAsync` yöntemi belirtilen hello için bir belirteç ADAL tooreturn ister herhangi UX gösteren olmadan kaynak Merhaba önbellek depolanan, uygun erişim belirteci zaten varsa oluşabilir veya bir yenileme belirteci olup olmadığını kullanılan tooget yeni bir erişim belirteci herhangi bir istem göstermeden. O deneme başarısız olursa, biz geri dönmesi `acquireTokenAsync`--hangi görünür şekilde ister hello kullanıcı tooauthenticate.

```javascript
            // Attempt tooauthorize hello user silently
            app.context.acquireTokenSilentAsync(resourceUri, clientId)
            .then(authCompletedCallback, function () {
                // We require user credentials, so this triggers hello authentication dialog box
                app.context.acquireTokenAsync(resourceUri, clientId, redirectUri)
                .then(authCompletedCallback, function (err) {
                    app.error("Failed tooauthenticate: " + err);
                });
            });
```
Biz hello belirteci sahip olduğunuza göre biz son hello grafik API'si çağırma ve istiyoruz hello arama sorgusu gerçekleştirin. Merhaba aşağıdaki kod parçacığını aşağıdaki hello Ekle `authenticate` tanımı:

```javascript
// Makes an API call tooreceive hello user list
    requestData: function (authResult, searchText) {
        var req = new XMLHttpRequest();
        var url = resourceUri + "/" + authResult.tenantId + "/users?api-version=" + graphApiVersion;
        url = searchText ? url + "&$filter=mailNickname eq '" + searchText + "'" : url + "&$top=10";

        req.open("GET", url, true);
        req.setRequestHeader('Authorization', 'Bearer ' + authResult.accessToken);

        req.onload = function(e) {
            if (e.target.status >= 200 && e.target.status < 300) {
                app.renderData(JSON.parse(e.target.response));
                return;
            }
            app.error('Data request failed: ' + e.target.response);
        };
        req.onerror = function(e) {
            app.error('Data request failed: ' + e.error);
        }

        req.send();
    },

```
bir kullanıcının diğer adı metin kutusuna girmek için basit bir UX sağladığı Hello başlangıç noktası dosyalar. Bu yöntem tooconstruct bir sorgu değeri, hello erişim belirteciyle birleştirmek, tooMicrosoft grafik göndermek ve hello sonuçlarını ayrıştırmak kullanır. Merhaba `renderData` yöntemi, hello başlangıç noktası dosyasında zaten mevcut hello sonuçlarını görselleştirme mvc'deki.

## <a name="step-5-run-hello-app"></a>Adım 5: hello uygulama çalıştırma
Uygulamanız son hazır toorun ' dir. Bu işletim basittir: hello uygulama başlatıldığında hello diğer yukarı toolook istediğiniz hello kullanıcı adını girin ve sonra hello düğmesine tıklayın. Kimlik doğrulaması için istenir. Başarılı kimlik doğrulama ve başarılı arama sırasında aranır hello kullanıcı hello özniteliklerini görüntülenir.

Sonraki çalıştırır, herhangi bir istem göstermeden hello arama gerçekleştirilir, thanks hello toohello varlığını önceden önbelleğinde belirteç alındı.

Merhaba uygulama çalıştırmaya hello somut adımları platforma göre değişir.

### <a name="windows-10"></a>Windows 10
   Tablet/bilgisayar:`cordova run windows --archs=x64 -- --appx=uap`

   Mobil (Windows 10 Mobile cihaz bağlı tooa PC gerektirir):`cordova run windows --archs=arm -- --appx=uap --phone`

   > [!NOTE]
   > İlk çalıştırma hello sırasında içinde toosign Geliştirici lisansı istenebilir. Daha fazla bilgi için bkz: [Geliştirici lisansı](https://msdn.microsoft.com/library/windows/apps/hh974578.aspx).

### <a name="windows-81-tabletpc"></a>Windows 8.1 Tablet/PC
   `cordova run windows`

   > [!NOTE]
   > İlk çalıştırma hello sırasında içinde toosign Geliştirici lisansı istenebilir. Daha fazla bilgi için bkz: [Geliştirici lisansı](https://msdn.microsoft.com/library/windows/apps/hh974578.aspx).

### <a name="windows-phone-81"></a>Windows Phone 8.1
   bağlı bir cihazda toorun:`cordova run windows --device -- --phone`

   toorun hello varsayılan öykünücü üzerinde:`cordova emulate windows -- --phone`

   Kullanım `cordova run windows --list -- --phone` toosee tüm kullanılabilir hedefler ve `cordova run windows --target=<target_name> -- --phone` toorun Merhaba uygulaması belirli cihaz veya öykünücü (örneğin, `cordova run windows --target="Emulator 8.1 720P 4.7 inch" -- --phone`).

### <a name="android"></a>Android
   bağlı bir cihazda toorun:`cordova run android --device`

   toorun hello varsayılan öykünücü üzerinde:`cordova emulate android`

   Bir öykünücü örneğinde AVD Yöneticisi'ni kullanarak daha önce hello "Önkoşullar" bölümünde açıklandığı gibi oluşturduğunuz emin olun.

   Kullanım `cordova run android --list` toosee tüm kullanılabilir hedefler ve `cordova run android --target=<target_name>` toorun Merhaba uygulaması belirli cihaz veya öykünücü (örneğin, `cordova run android --target="Nexus4_emulator"`).

### <a name="ios"></a>iOS
   bağlı bir cihazda toorun:`cordova run ios --device`

   toorun hello varsayılan öykünücü üzerinde:`cordova emulate ios`

   > [!NOTE]
   > Merhaba olduğundan emin olun `ios-sim` hello öykünücüsü üzerinde yüklü paket toorun. Daha fazla bilgi için bkz: hello "Önkoşullar" bölümü.

    Use `cordova run ios --list` toosee all available targets and `cordova run ios --target=<target_name>` toorun hello application on specific device or emulator (for example, `cordova run android --target="iPhone-6"`).

    Use `cordova run --help` toosee additional build and run options.

## <a name="next-steps"></a>Sonraki adımlar
Başvuru için (yapılandırma değerleriniz olmadan) tamamlandı hello örnek kullanılabilir [GitHub](https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-Cordova/tree/complete/DirSearchClient).

Şimdi Gelişmiş toomore (ve daha ilginç) taşıma senaryoları kullanabilirsiniz. Tootry isteyebilirsiniz: [Azure AD ile bir Node.js Web API'SİNİN güvenliğini](active-directory-devquickstarts-webapi-nodejs.md).

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
