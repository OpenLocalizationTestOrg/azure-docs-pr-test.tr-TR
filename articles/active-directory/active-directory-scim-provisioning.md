---
title: "aaaUsing sistemi etki alanları arası kimlik yönetimi için otomatik olarak sağlamak kullanıcıların ve grupların Azure Active Directory tooapplications | Microsoft Docs"
description: "Azure Active Directory Kullanıcıları ve bir web hizmeti tarafından hello SCIM'yi protokolü belirtimi tanımlanan hello arabirimiyle fronted grupları tooany uygulama ya da kimlik deposunu otomatik olarak sağlayabilirsiniz"
services: active-directory
documentationcenter: 
author: asmalser-msft
manager: femila
editor: 
ms.assetid: 4d86f3dc-e2d3-4bde-81a3-4a0e092551c0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/28/2017
ms.author: asmalser
ms.reviewer: asmalser
ms.custom: aaddev;it-pro;oldportal
ms.openlocfilehash: 43045c97e68d0d22db598dcb5ec23481c4e97718
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="using-system-for-cross-domain-identity-management-tooautomatically-provision-users-and-groups-from-azure-active-directory-tooapplications"></a>Etki alanları arası Kimlik Yönetimi tooautomatically sağlama kullanıcılar ve grupların Azure Active Directory tooapplications için sistem kullanma

## <a name="overview"></a>Genel Bakış
Azure Active Directory (Azure AD) kullanıcı ve bir web hizmeti tarafından hello tanımlanan hello arabirimiyle fronted grupları tooany uygulama ya da kimlik deposunu otomatik olarak sağlayabilirler [sistem etki alanları arası Kimlik Yönetimi (SCIM'yi) 2.0 protokol belirtimi](https://tools.ietf.org/html/draft-ietf-scim-api-19). Azure Active Directory istekleri toocreate göndermek, değiştirmek veya atanan kullanıcılar ve gruplar toohello web hizmetini silin. Merhaba web hizmeti işlemlere hello hedef kimlik deposu bu istekleri sonra çevirebilir. 

> [!IMPORTANT]
> Microsoft önerir hello kullanarak Azure AD'yi yönetme [Azure AD Yönetim Merkezi](https://aad.portal.azure.com) hello yerine Azure portal hello bu makalede başvurulan Klasik Azure portalı. 



![][0]
*Şekil 1: bir web hizmeti aracılığıyla Azure Active Directory tooan kimlik deposu sağlama*

Bu özellik "kendi uygulamanızı getir" Merhaba yeteneğine Azure AD tooenable çoklu oturum açma ve otomatik kullanıcı sağlayan veya SCIM'yi web hizmeti tarafından fronted uygulamalar için hazırlama birlikte kullanılabilir.

Azure Active Directory'de SCIM'yi kullanma iki kullanım örnekleri şunlardır:

* **SCIM'yi destek kullanıcılar ve gruplar tooapplications sağlama** SCIM'yi 2.0 desteği ve yapılandırma olmadan Azure AD ile kimlik doğrulaması çalışır OAuth taşıyıcı belirteçlerini kullanmak uygulamalar.
* **Diğer API tabanlı sağlama destekleyen uygulamalar için kendi sağlama çözümü derleme** SCIM'yi olmayan uygulamalar için SCIM'yi uç nokta tootranslate hello Azure AD SCIM'yi endpoint herhangi API hello uygulamanızın desteklediği arasındaki oluşturabilirsiniz. Kullanıcı sağlama için. toohelp SCIM'yi endpoint geliştirme, ortak dil altyapısı (CLI) kitaplıkları ile birlikte nasıl toodo SCIM'yi uç nokta sağlar ve SCIM'yi iletileri Çevir Göster kod örnekleri sunuyoruz.  

## <a name="provisioning-users-and-groups-tooapplications-that-support-scim"></a>Kullanıcılar ve SCIM'yi destek grupları tooapplications sağlama
Azure AD uygulayan yapılandırılmış tooautomatically sağlama atanan kullanıcılar ve gruplar tooapplications olabilir bir [sistemi için etki alanları arası Kimlik Yönetimi 2 (SCIM'yi)](https://tools.ietf.org/html/draft-ietf-scim-api-19) web hizmeti ve kimlik doğrulaması için OAuth taşıyıcı belirteçlerini kabul edin . Merhaba SCIM'yi 2.0 belirtimi içinde uygulamalar bu gereksinimleri karşılamalıdır:

* Kullanıcılara ve/veya hello SCIM'yi Protokolü 3.3 bölümünü göredir grupları oluşturmayı destekler.  
* Kullanıcılara ve/veya patch isteklerinde hello SCIM'yi Protokolü 3.5.2'de bölümünü göredir gruplarla değiştirerek destekler.  
* Bilinen kaynak hello SCIM'yi Protokolü 3.4.1 bölümünü göredir alma destekler.  
* Kullanıcılara ve/veya grupları hello SCIM'yi Protokolü 3.4.2 bölümünü göredir sorgulama destekler.  Varsayılan olarak, kullanıcılar tarafından externalID seçmeleri istenir ve grupları displayName tarafından sorgulanır.  
* Kullanıcı kimliği ve hello SCIM'yi Protokolü 3.4.2 bölümünü göredir Yöneticisi tarafından sorgulama destekler.  
* Gruplar ve üye hello SCIM'yi Protokolü 3.4.2 bölümünü göredir kimliği tarafından sorgulama destekler.  
* Merhaba SCIM'yi Protokolü bölüm 2.1 göredir yetkilendirme için OAuth taşıyıcı belirteçleri kabul eder.

Uygulama sağlayıcınıza veya bu gereksinimleri ile uyumluluk bilgilerinin uygulama sağlayıcınızın belgelerine başvurun.

### <a name="getting-started"></a>Başlarken
Bu makalede açıklanan hello SCIM'yi profili destekleyen uygulamalar bağlı tooAzure Active Directory olabilir hello Azure AD uygulama galerisinde galeri olmayan hello "uygulama" özelliğini kullanma. Bağlı, Azure AD çalıştıran sonra eşitleme işlemi burada hello uygulamanın SCIM'yi uç noktası için sorgular 20 dakikada kullanıcılar ve gruplar, atanan ve oluşturur veya bunları toohello atama ayrıntıları göre değiştirir.

**tooconnect SCIM'yi destekleyen bir uygulama:**

1. Çok oturum[Azure portal hello](https://portal.azure.com). 
2. Çok Gözat ** Azure Active Directory > Kurumsal uygulamaları ve select **yeni uygulama > tüm > olmayan galeri uygulama**.
3. Uygulamanız için bir ad girin ve tıklayın **Ekle** simgesi toocreate bir uygulama nesnesi.
    
  ![][1]
  *Şekil 2: Azure AD uygulama galerisinde*
    
4. Merhaba Hello elde edilen ekranında şunları seçin **sağlama** hello sol sütunda sekmesi.
5. Merhaba, **sağlama modu** menüsünde, select **otomatik**.
    
  ![][2]
  *Şekil 3: hello Azure portal sağlama yapılandırma*
    
6. Merhaba, **Kiracı URL** alanında, hello hello uygulamanın SCIM'yi uç nokta URL'sini girin. Örnek: https://api.contoso.com/scim/v2/
7. Merhaba SCIM'yi uç nokta gerektiriyor Azure AD dışında bir veren bir OAuth taşıyıcı belirtecinden sonra kopyalama hello gerekli OAuth taşıyıcı belirteci hello isteğe bağlı **gizli belirteci** alan. Bu alan boş bırakılırsa, Azure AD her istek ile Azure AD tarafından verilen bir OAuth taşıyıcı belirteci dahil. Azure AD kimlik sağlayıcısı bu Azure AD doğrulayabilirsiniz olarak kullanan uygulamaları-belirteç.
8. Merhaba tıklatın **Bağlantıyı Sına** düğmesi toohave Azure Active Directory girişimi tooconnect toohello SCIM'yi uç noktası. Merhaba deneme başarısız olursa hata bilgileri görüntülenir.  
9. Merhaba denemeleri tooconnect toohello uygulaması başarılı olursa, ardından **kaydetmek** toosave hello yönetici kimlik bilgileri.
10. Merhaba, **eşlemeleri** bölümünde, iki seçilebilir öznitelik eşlemelerini kümesi vardır: biri kullanıcı nesneleri ve Grup nesneleri için bir tane. Eşitlenen her bir tooreview hello öznitelikleri, Azure Active Directory tooyour uygulamasını seçin. Merhaba olarak seçilen öznitelikler **eşleşen** kullanılan toomatch hello kullanıcılar ve gruplar güncelleştirme işlemleri için uygulamanızda özellikleridir. Merhaba Kaydet düğmesine toocommit herhangi bir değişiklik seçin.

    >[!NOTE]
    >İsteğe bağlı olarak, "Merhaba grupları eşleme" devre dışı bırakarak group nesnelerini eşitlemeyi devre dışı bırakın. 

11. Altında **ayarları**, hello **kapsam** alanı tanımlar hangi kullanıcı ve grup veya eşitlenir. "Eşitleme yalnızca kullanıcılar ve gruplar (önerilen) atanan" seçerek yalnızca eşitlendiğini kullanıcılar ve gruplar hello atanan **kullanıcılar ve gruplar** sekmesi.
12. Merhaba, yapılandırma tamamlandıktan sonra değiştirmek **sağlama durumu** çok**üzerinde**.
13. Tıklatın **kaydetmek** toostart hello Azure AD sağlama hizmeti. 
14. Kullanıcılar ve gruplar (önerilen) yalnızca eşitleniyor atanan emin tooselect hello olması **kullanıcılar ve gruplar** sekmesinde ve hello kullanıcılara ve/veya toosync istediğiniz grupları atayabilirsiniz.

Merhaba ilk eşitleme başladıktan sonra hello kullanabilirsiniz **denetim günlüklerini** sekmesinde uygulamanızdan hizmet sağlama hello tarafından gerçekleştirilen tüm eylemler gösterir toomonitor devam ediyor. Hello Azure AD tooread sağlama nasıl oturum ile ilgili daha fazla bilgi için bkz: [otomatik olarak bir kullanıcı hesabı sağlama raporlama](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).

>[!NOTE]
>Merhaba ilk eşitleme yaklaşık 20 dakikada hello çalıştığı sürece oluşan sonraki eşitlemeler daha uzun tooperform alır. 


## <a name="building-your-own-provisioning-solution-for-any-application"></a>Herhangi bir uygulama için kendi sağlama çözümü oluşturma
Azure Active Directory ile arabirimleri SCIM'yi web hizmeti oluşturarak, bir REST veya SOAP kullanıcı API hazırlama sağlar neredeyse her uygulama için tek oturum açma ve otomatik kullanıcı sağlamayı etkinleştirebilirsiniz.

İşte nasıl çalışır:

1. Azure AD sağlar adlı ortak dil altyapısı kitaplık [Microsoft.SystemForCrossDomainIdentityManagement](https://www.nuget.org/packages/Microsoft.SystemForCrossDomainIdentityManagement/). Sistem tümleştiricileri ve geliştiriciler, bu kitaplık toocreate kullanabilir ve bir SCIM'yi tabanlı web hizmeti uç noktası Azure AD tooany uygulamanın kimlik deposu bağlanıp bağlanamayacağını dağıtabilirsiniz.
2. Eşlemeleri hello web hizmeti toomap hello standartlaştırılmış kullanıcı şema toohello kullanıcı şeması ve hello uygulama tarafından istenen Protokolü uygulanır.
3. Merhaba uç nokta URL'si hello uygulama galerisinde özel bir uygulama bir parçası olarak Azure AD'de kayıtlı değil.
4. Kullanıcıların ve grupların Azure AD toothis uygulamada atanır. Atama oldukları bir sıra eşitlenen toobe toohello hedef uygulamasına yerleştirilir. Hello sıra işleme hello eşitleme işlemi 20 dakikada bir çalışır.

### <a name="code-samples"></a>Kod Örnekleri
toomake bu işlem daha kolay bir dizi [kod örnekleri](https://github.com/Azure/AzureAD-BYOA-Provisioning-Samples/tree/master) SCIM'yi web hizmeti uç noktası oluşturun ve otomatik sağlamayı göstermek sağlanır. Kullanıcılar ve gruplar temsil eden virgülle ayrılmış değerler satırlarla bir dosyayı korur bir sağlayıcının bir örnek verilmiştir.  Merhaba diğer hello Amazon Web Hizmetleri kimlik ve erişim yönetimi hizmetini çalışır bir sağlayıcı değil.  

**Önkoşullar**

* Visual Studio 2013 veya üzeri
* [.NET için Azure SDK](https://azure.microsoft.com/downloads/)
* Merhaba ASP.NET framework 4.5 toobe destekleyen Windows makine SCIM'yi endpoint hello kullanılır. Bu makinenin hello buluttan erişilebilir olması gerekir
* [Bir Azure aboneliği ile Azure AD Premium deneme veya lisanslı bir sürümü](https://azure.microsoft.com/services/active-directory/)
* Merhaba Amazon AWS örneği gerektirir hello kitaplıklarından [Visual Studio için AWS Araç Seti](http://docs.aws.amazon.com/AWSToolkitVS/latest/UserGuide/tkv_setup.html). Daha fazla bilgi için bkz: hello Benioku hello örnekle dahil dosya.

### <a name="getting-started"></a>Başlarken
Azure AD'den sağlama kabul edebileceği bir SCIM'yi uç noktası istekleri hello en kolay yolu tooimplement toobuild olan ve hello sağlanan kullanıcılar tooa virgülle ayrılmış değer (CSV) dosyası çıkarır hello kod örneği dağıtın.

**toocreate bir örnek SCIM'yi uç noktası:**

1. Merhaba kod örnek paketin karşıdan [https://github.com/Azure/AzureAD-BYOA-Provisioning-Samples/tree/master](https://github.com/Azure/AzureAD-BYOA-Provisioning-Samples/tree/master)
2. Merhaba paketin sıkıştırmasını açın ve Windows makinenizdeki C:\AzureAD-BYOA-Provisioning-Samples\ gibi bir konuma yerleştirin.
3. Bu klasörde, Visual Studio'da hello FileProvisioningAgent çözüm başlatın.
4. Seçin **Araçlar > Kitaplık Paket Yöneticisi > Paket Yöneticisi Konsolu**ve komutları hello FileProvisioningAgent proje tooresolve hello çözüm başvuruları için aşağıdaki hello yürütün:
  ```` 
   Install-Package Microsoft.SystemForCrossDomainIdentityManagement
   Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory
   Install-Package Microsoft.Owin.Diagnostics
   Install-Package Microsoft.Owin.Host.SystemWeb
  ````
5. Merhaba FileProvisioningAgent projesi oluşturun.
6. (Yönetici) olarak Windows Hello komut istemi uygulamasını başlatma ve hello kullan **cd** komutu toochange hello dizin tooyour **\AzureAD-BYOA-Provisioning-Samples\ProvisioningAgent\bin\Debug** klasör.
7. Aşağıdaki komut, < IP adresi > merhaba IP adresine veya etki alanı adıyla hello Windows makinenin değiştirerek hello çalıştırın:
  ````   
   FileAgnt.exe http://<ip-address>:9000 TargetFile.csv
  ````
8. Windows altında **Windows Ayarları > Ağ ve Internet ayarlarını**seçin hello **Windows Güvenlik Duvarı > Gelişmiş ayarları**ve oluşturma bir **gelen kuralı** , gelen erişim tooport 9000 sağlar.
9. Merhaba Windows makine yönlendiricisi arkasında ise, sunulan toohello olan yönlendirici gereksinimlerini yapılandırılmış toobe tooperform ağ erişim çevirisi, bağlantı noktası 9000 arasında hello Internet ve bağlantı noktası 9000 hello Windows makinede. Bu Azure AD toobe mümkün tooaccess gereklidir hello bulutta Bu uç nokta.

**tooregister hello örnek SCIM'yi uç noktası Azure AD'de:**

1. Çok oturum[Azure portal hello](https://portal.azure.com). 
2. Çok Gözat ** Azure Active Directory > Kurumsal uygulamaları ve select **yeni uygulama > tüm > olmayan galeri uygulama**.
3. Uygulamanız için bir ad girin ve tıklayın **Ekle** simgesi toocreate bir uygulama nesnesi. oluşturulan hello uygulama hedeflenen toorepresent hello hedef uygulama tek oturum açma için ve yalnızca hello SCIM'yi endpoint uygulama tooand sağlama nesnesidir.
4. Merhaba Hello elde edilen ekranında şunları seçin **sağlama** hello sol sütunda sekmesi.
5. Merhaba, **sağlama modu** menüsünde, select **otomatik**.
    
  ![][2]
  *Şekil 4: hello Azure portal sağlama yapılandırma*
    
6. Merhaba, **Kiracı URL** alanında, hello Internet kullanıma sunulan URL ve SCIM'yi bitiş bağlantı noktası girin. Http://testmachine.contoso.com:9000 veya http://<ip-address>:9000/, burada < IP adresi > olan hello internet IP kullanıma sunulan gibi bu bir şey olacaktır adresi.  
7. Merhaba SCIM'yi uç nokta gerektiriyor Azure AD dışında bir veren bir OAuth taşıyıcı belirtecinden sonra kopyalama hello gerekli OAuth taşıyıcı belirteci hello isteğe bağlı **gizli belirteci** alan. Bu alan boş bırakılırsa, Azure AD her istek ile Azure AD tarafından verilen bir OAuth taşıyıcı belirteci dahil edilir. Azure AD kimlik sağlayıcısı bu Azure AD doğrulayabilirsiniz olarak kullanan uygulamaları-belirteç.
8. Merhaba tıklatın **Bağlantıyı Sına** düğmesi toohave Azure Active Directory girişimi tooconnect toohello SCIM'yi uç noktası. Merhaba deneme başarısız olursa hata bilgileri görüntülenir.  
9. Merhaba denemeleri tooconnect toohello uygulaması başarılı olursa, ardından **kaydetmek** toosave hello yönetici kimlik bilgileri.
10. Merhaba, **eşlemeleri** bölümünde, iki seçilebilir öznitelik eşlemelerini kümesi vardır: biri kullanıcı nesneleri ve Grup nesneleri için bir tane. Eşitlenen her bir tooreview hello öznitelikleri, Azure Active Directory tooyour uygulamasını seçin. Merhaba olarak seçilen öznitelikler **eşleşen** kullanılan toomatch hello kullanıcılar ve gruplar güncelleştirme işlemleri için uygulamanızda özellikleridir. Merhaba Kaydet düğmesine toocommit herhangi bir değişiklik seçin.
11. Altında **ayarları**, hello **kapsam** alanı tanımlar hangi kullanıcı ve grup veya eşitlenir. "Eşitleme yalnızca kullanıcılar ve gruplar (önerilen) atanan" seçerek yalnızca eşitlendiğini kullanıcılar ve gruplar hello atanan **kullanıcılar ve gruplar** sekmesi.
12. Merhaba, yapılandırma tamamlandıktan sonra değiştirmek **sağlama durumu** çok**üzerinde**.
13. Tıklatın **kaydetmek** toostart hello Azure AD sağlama hizmeti. 
14. Kullanıcılar ve gruplar (önerilen) yalnızca eşitleniyor atanan emin tooselect hello olması **kullanıcılar ve gruplar** sekmesinde ve hello kullanıcılara ve/veya toosync istediğiniz grupları atayabilirsiniz.

Merhaba ilk eşitleme başladıktan sonra hello kullanabilirsiniz **denetim günlüklerini** sekmesinde uygulamanızdan hizmet sağlama hello tarafından gerçekleştirilen tüm eylemler gösterir toomonitor devam ediyor. Hello Azure AD tooread sağlama nasıl oturum ile ilgili daha fazla bilgi için bkz: [otomatik olarak bir kullanıcı hesabı sağlama raporlama](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).

Merhaba örnek doğrulama hello son adımı tooopen hello Windows makinenizde hello \AzureAD-BYOA-Provisioning-Samples\ProvisioningAgent\bin\Debug klasöründeki TargetFile.csv dosyasını oluşturur. Sağlama işlemi hello çalıştırdıktan sonra bu dosyayı tüm hello ayrıntılarını atanan ve kullanıcılar ve gruplar sağlanan gösterir.

### <a name="development-libraries"></a>Geliştirme kitaplıkları
toodevelop toohello SCIM'yi belirtimine uygun kendi web hizmeti ilk tanıyın kendinizi Microsoft tarafından toohelp hızlandırmak sağlanan hello geliştirme sürecinin kitaplıkları aşağıdaki hello ile: 

1. Ortak dil altyapısı (CLI) kitaplıklar gibi C#, altyapı göre dilleri ile kullanıma sunulur. Bu kitaplıklar birini [Microsoft.SystemForCrossDomainIdentityManagement.Service](https://www.nuget.org/packages/Microsoft.SystemForCrossDomainIdentityManagement/), hello aşağıdaki çizimde gösterilen bir arabirim Microsoft.SystemForCrossDomainIdentityManagement.IProvider, bildirir: A Merhaba kitaplıkları kullanarak geliştirici için genel sağlayıcısı olarak adlandırılabilir bir sınıf ile bu arabirimini uygulaması. Merhaba kitaplıkları hello Geliştirici toodeploy toohello SCIM'yi belirtimi uyumlu bir web hizmeti etkinleştirin. Merhaba web hizmeti ya da Internet Information Services veya yürütülebilir bir ortak dil altyapısı derlemesi içinde barındırılabilir. İstek hello Geliştirici toooperate bazı kimlik deposu olarak programlanmış çağrıları toohello sağlayıcının yöntemlerde çevrilir.
  
  ![][3]
  
2. [Rota işleyicileri express](http://expressjs.com/guide/routing.html) tooa node.js web hizmetine yapılan çağrılar (tarafından tanımlanan hello SCIM'yi belirtimi), temsil eden bir node.js isteği nesneleri ayrıştırmak için kullanılabilir.   

### <a name="building-a-custom-scim-endpoint"></a>Bir özel SCIM'yi uç noktası oluşturma
Merhaba CLI kitaplıkları kullanarak, bu kitaplığı kullanan geliştiriciler kendi Hizmetleri veya Internet Information Services yürütülebilir ortak dil altyapısı derlemeler içinde barındırabilir. Merhaba adresinde http://localhost:9000 yürütülebilir bütünleştirilmiş kod içinde bir hizmet barındırma için örnek kod aşağıda verilmiştir: 

    private static void Main(string[] arguments)
    {
    // Microsoft.SystemForCrossDomainIdentityManagement.IMonitor, 
    // Microsoft.SystemForCrossDomainIdentityManagement.IProvider and 
    // Microsoft.SystemForCrossDomainIdentityManagement.Service are all defined in 
    // Microsoft.SystemForCrossDomainIdentityManagement.Service.dll.  

    Microsoft.SystemForCrossDomainIdentityManagement.IMonitor monitor = 
      new DevelopersMonitor();
    Microsoft.SystemForCrossDomainIdentityManagement.IProvider provider = 
      new DevelopersProvider(arguments[1]);
    Microsoft.SystemForCrossDomainIdentityManagement.Service webService = null;
    try
    {
        webService = new WebService(monitor, provider);
        webService.Start("http://localhost:9000");

        Console.ReadKey(true);
    }
    finally
    {
        if (webService != null)
        {
            webService.Dispose();
            webService = null;
        }
    }
    }

    public class WebService : Microsoft.SystemForCrossDomainIdentityManagement.Service
    {
    private Microsoft.SystemForCrossDomainIdentityManagement.IMonitor monitor;
    private Microsoft.SystemForCrossDomainIdentityManagement.IProvider provider;

    public WebService(
      Microsoft.SystemForCrossDomainIdentityManagement.IMonitor monitoringBehavior, 
      Microsoft.SystemForCrossDomainIdentityManagement.IProvider providerBehavior)
    {
        this.monitor = monitoringBehavior;
        this.provider = providerBehavior;
    }

    public override IMonitor MonitoringBehavior
    {
        get
        {
            return this.monitor;
        }

        set
        {
            this.monitor = value;
        }
    }

    public override IProvider ProviderBehavior
    {
        get
        {
            return this.provider;
        }

        set
        {
            this.provider = value;
        }
    }
    }

Bu hizmet hangi hello kök sertifika yetkilisi hello aşağıdakilerden biri olan bir HTTP adresi ve bir sunucu kimlik doğrulama sertifikası olması gerekir: 

* CNNIC
* Comodo
* CyberTrust
* DigiCert
* GeoTrust
* GlobalSign
* Daddy gidin
* VeriSign
* WoSign

Bir sunucu kimlik doğrulama sertifikası hello ağ Kabuğu yardımcı programını kullanarak bir Windows ana bilgisayardaki ilişkili tooa bağlantı noktası olabilir: 

    netsh http add sslcert ipport=0.0.0.0:443 certhash=0000000000003ed9cd0c315bbb6dc1c08da5e6 appid={00112233-4455-6677-8899-AABBCCDDEEFF}  

Merhaba AppID bağımsız değişkeni için sağlanan hello değeri rastgele bir genel benzersiz tanımlayıcı olsa da burada hello certhash bağımsız değişkeni için sağlanan hello hello sertifikanın parmak izini Merhaba, değerdir.  

toohost hello hizmet Internet Information Services içinde bir geliştirici, başlangıç hello derlemenin hello varsayılan ad alanında adlı bir sınıf ile CLA kod kitaplığı derleme oluşturma.  Böyle bir sınıfın bir örneği aşağıda verilmiştir: 

    public class Startup
    {
    // Microsoft.SystemForCrossDomainIdentityManagement.IWebApplicationStarter, 
    // Microsoft.SystemForCrossDomainIdentityManagement.IMonitor and  
    // Microsoft.SystemForCrossDomainIdentityManagement.Service are all defined in 
    // Microsoft.SystemForCrossDomainIdentityManagement.Service.dll.  

    Microsoft.SystemForCrossDomainIdentityManagement.IWebApplicationStarter starter;

    public Startup()
    {
        Microsoft.SystemForCrossDomainIdentityManagement.IMonitor monitor = 
          new DevelopersMonitor();
        Microsoft.SystemForCrossDomainIdentityManagement.IProvider provider = 
          new DevelopersProvider();
        this.starter = 
          new Microsoft.SystemForCrossDomainIdentityManagement.WebApplicationStarter(
            provider, 
            monitor);
    }

    public void Configuration(
      Owin.IAppBuilder builder) // Defined in in Owin.dll.  
    {
        this.starter.ConfigureApplication(builder);
    }
    }

### <a name="handling-endpoint-authentication"></a>İşleme uç noktası kimlik doğrulaması
Azure Active Directory gelen istekleri bir OAuth 2.0 taşıyıcı belirteci içerir.   Herhangi bir hizmet alıcı hello isteği hello veren erişim toohello Azure Active Directory Graph web hizmeti için beklenen hello Azure Active Directory Kiracı adına Azure Active Directory olarak kimlik doğrulaması.  Merhaba belirteçte hello veren "ISS" gibi bir ISS talep tanımlanır: "https://sts.windows.net/cbb1a5ac-f33b-45fa-9bf5-f37db0fed422/".  Bu örnekte, hello talep değeri, taban adresini hello https://sts.windows.net, veren hello gibi Azure Active Directory tanımlar, hello göreli adresi segment, cbb1a5ac-f33b-45fa-9bf5-f37db0fed422, benzersiz tanıtıcısının olsa da Azure Active hello Dizin Kiracı adına hangi hello belirteci verilmiş.  Merhaba belirteci hello Azure Active Directory Graph web hizmeti, bu hizmeti sonra hello tanıtıcısı erişmek için verilmişse 00000002-0000-0000-c000-000000000000, olması hello belirtecin aud hello değerinin talep.  

Geliştiriciler SCIM'yi hizmet oluşturmak için Microsoft tarafından sağlanan hello CLA kitaplıkları kullanarak aşağıdaki adımları izleyerek hello Microsoft.Owin.Security.ActiveDirectory paketi kullanılarak Azure Active Directory'ye gelen istekleri doğrulayabilir: 

1. Sağlayıcı, bu hello hizmeti başlatıldığında adlı bir yöntem toobe dönüş sağlayarak hello Microsoft.SystemForCrossDomainIdentityManagement.IProvider.StartupBehavior özelliği uygulayın: 

  ````
    public override Action\<Owin.IAppBuilder, System.Web.Http.HttpConfiguration.HttpConfiguration\> StartupBehavior
    {
      get
      {
        return this.OnServiceStartup;
      }
    }

    private void OnServiceStartup(
      Owin.IAppBuilder applicationBuilder,  // Defined in Owin.dll.  
      System.Web.Http.HttpConfiguration configuration)  // Defined in System.Web.Http.dll.  
    {
    }
  ````

2. Aşağıdaki kod toothat yöntemi toohave hello hello hizmetin uç noktaları erişim toohello Azure AD grafik web hizmeti için belirtilen bir kiracı adına Azure Active Directory tarafından verilmiş bir belirteç pul olarak kimliği doğrulanmış tüm istek tooany ekleyin: 

  ````
    private void OnServiceStartup(
      Owin.IAppBuilder applicationBuilder IAppBuilder applicationBuilder, 
      System.Web.Http.HttpConfiguration HttpConfiguration configuration)
    {
      // IFilter is defined in System.Web.Http.dll.  
      System.Web.Http.Filters.IFilter authorizationFilter = 
        new System.Web.Http.AuthorizeAttribute(); // Defined in System.Web.Http.dll.configuration.Filters.Add(authorizationFilter);

      // SystemIdentityModel.Tokens.TokenValidationParameters is defined in    
      // System.IdentityModel.Token.Jwt.dll.
      SystemIdentityModel.Tokens.TokenValidationParameters tokenValidationParameters =     
        new TokenValidationParameters()
        {
          ValidAudience = "00000002-0000-0000-c000-000000000000"
        };

      // WindowsAzureActiveDirectoryBearerAuthenticationOptions is defined in 
      // Microsoft.Owin.Security.ActiveDirectory.dll
      Microsoft.Owin.Security.ActiveDirectory.
      WindowsAzureActiveDirectoryBearerAuthenticationOptions authenticationOptions =
        new WindowsAzureActiveDirectoryBearerAuthenticationOptions()    {
        TokenValidationParameters = tokenValidationParameters,
        Tenant = "03F9FCBC-EA7B-46C2-8466-F81917F3C15E" // Substitute hello appropriate tenant’s 
                                                      // identifier for this one.  
      };

      applicationBuilder.UseWindowsAzureActiveDirectoryBearerAuthentication(authenticationOptions);
    }
  ````


## <a name="user-and-group-schema"></a>Kullanıcı ve Grup şeması
Azure Active Directory kaynakları tooSCIM web hizmetleri iki tür sağlayabilirsiniz.  Bu kaynakların kullanıcılar ve gruplar türleridir.  

Kullanıcı kaynakları hello şema tanımlayıcısı, bu protokolü belirtimi içinde bulunan urn: ietf:params:scim:schemas:extension:enterprise:2.0:User tanımlanır: http://tools.ietf.org/html/draft-ietf-scim-core-schema.  Kullanıcıların Azure Active Directory toohello özniteliklerinde urn: ietf:params:scim:schemas:extension:enterprise:2.0:User kaynakların hello özniteliklerin Hello Varsayılan eşleme Tablo 1, aşağıda verilmiştir.  

Grup kaynaklarının hello şema tanımlayıcılarına göre tanımlanır http://schemas.microsoft.com/2006/11/ResourceManagement/ADSCIM/Group.  Aşağıda, gösterir hello Varsayılan eşleme gruplarının Azure Active Directory toohello öznitelikleri http://schemas.microsoft.com/2006/11/ResourceManagement/ADSCIM/Group kaynakların hello özniteliklerin Tablo 2.  

### <a name="table-1-default-user-attribute-mapping"></a>Tablo 1: Varsayılan kullanıcı özniteliği eşlemesi
| Azure Active Directory kullanıcısı | urn: ietf:params:scim:schemas:extension:enterprise:2.0:User |
| --- | --- |
| IsSoftDeleted |Etkin |
| Görünen adı |Görünen adı |
| Faks TelephoneNumber |PhoneNumber [türü eq "faks"] .value |
| givenName |name.givenName |
| İş Unvanı |Başlık |
| Posta |e-postaları [türü eq "İş"] .value |
| mailNickname |externalID |
| Yöneticisi |Yöneticisi |
| Mobil |PhoneNumber [türü eq "mobile"] .value |
| objectID |id |
| posta kodu |adresler [türü eq "İş"] .postalCode |
| Proxy adresleri |e-postaları [eq "diğer" yazın]. Değer |
| fiziksel teslim OfficeName |adresler [eq "diğer" yazın]. Biçimlendirilmiş |
| StreetAddress |adresler [türü eq "İş"] .streetAddress |
| Soyadı |name.familyName |
| telefon numarası |PhoneNumber [türü eq "İş"] .value |
| Kullanıcı PrincipalName |Kullanıcı adı |

### <a name="table-2-default-group-attribute-mapping"></a>Tablo 2: Varsayılan grup özellik eşlemesi
| Azure Active Directory grubu | http://schemas.microsoft.com/2006/11/ResourceManagement/ADSCIM/Group |
| --- | --- |
| Görünen adı |externalID |
| Posta |e-postaları [türü eq "İş"] .value |
| mailNickname |Görünen adı |
| Üyeleri |Üyeleri |
| objectID |id |
| proxyAddresses |e-postaları [eq "diğer" yazın]. Değer |

## <a name="user-provisioning-and-de-provisioning"></a>Kullanıcı hazırlama ve sağlamayı kaldırma özelliklerini
Merhaba, aşağıdaki çizimde gösterilmektedir Merhaba iletileri Azure Active Directory tooa SCIM'yi hizmet toomanage hello kullanım ömrü boyunca bir kullanıcı başka bir kimlik deposu gönderir. Merhaba diyagramı de nasıl hello CLI kitaplıkları kullanılarak uygulanan SCIM'yi sağlanan bir hizmeti Microsoft tarafından yapı için bu tür hizmetlerin bu istekleri bir sağlayıcısının çağrıları toohello yöntemlerin içine Çevir gösterir.  

![][4]
*Şekil 5: Kullanıcı sağlama ve sağlamayı kaldırma özelliklerini sırası*

1. Azure Active Directory sorgularını hello mailNickname öznitelik değeri, bir kullanıcının Azure AD içinde eşleşen bir externalID öznitelik değeri olan bir kullanıcı için hizmet hello. Merhaba sorgu; burada görüntülerle jyoung mailNickname bir kullanıcının Azure Active Directory'de örneğidir Bu örnekte gibi bir Köprü Metni Aktarım Protokolü (HTTP) istek olarak ifade edilir: 
  ````
    GET https://.../scim/Users?filter=externalId eq jyoung HTTP/1.1
    Authorization: Bearer ...
  ````
  Merhaba hizmet SCIM'yi Hizmetleri uygulamak için Microsoft tarafından sağlanan Merhaba ortak dil altyapısı kitaplıkları kullanılarak oluşturuldu, hello isteği çağrısı toohello hello hizmetin sağlayıcısının sorgu yöntemini çevrilir.  Bu yöntem hello imzası şöyledir: 
  ````
    // System.Threading.Tasks.Tasks is defined in mscorlib.dll.  
    // Microsoft.SystemForCrossDomainIdentityManagement.Resource is defined in 
    // Microsoft.SystemForCrossDomainIdentityManagement.Schemas.  
    // Microsoft.SystemForCrossDomainIdentityManagement.IQueryParameters is defined in 
    // Microsoft.SystemForCrossDomainIdentityManagement.Protocol.  

    System.Threading.Tasks.Task<Microsoft.SystemForCrossDomainIdentityManagement.Resource[]> Query(
      Microsoft.SystemForCrossDomainIdentityManagement.IQueryParameters parameters, 
      string correlationIdentifier);
  ````
  Merhaba Microsoft.SystemForCrossDomainIdentityManagement.IQueryParameters arabirimi hello tanımı aşağıda verilmiştir: 
  ````
    public interface IQueryParameters: 
      Microsoft.SystemForCrossDomainIdentityManagement.IRetrievalParameters
    {
        System.Collections.Generic.IReadOnlyCollection <Microsoft.SystemForCrossDomainIdentityManagement.IFilter> AlternateFilters 
        { get; }
    }

    public interface Microsoft.SystemForCrossDomainIdentityManagement.IRetrievalParameters
    {
      system.Collections.Generic.IReadOnlyCollection<string> ExcludedAttributePaths 
      { get; }
      System.Collections.Generic.IReadOnlyCollection<string> RequestedAttributePaths 
      { get; }
      string SchemaIdentifier 
      { get; }
    }

    public interface Microsoft.SystemForCrossDomainIdentityManagement.IFilter
    {
        Microsoft.SystemForCrossDomainIdentityManagement.IFilter AdditionalFilter 
          { get; set; }
        string AttributePath 
          { get; } 
        Microsoft.SystemForCrossDomainIdentityManagement.ComparisonOperator FilterOperator 
          { get; }
        string ComparisonValue 
          { get; }
    }

    public enum Microsoft.SystemForCrossDomainIdentityManagement.ComparisonOperator
    {
        Equals
    }
  ````
  Bir kullanıcı için bir sorgu hello externalID özniteliği için belirtilen bir değerle örneği aşağıdaki hello toohello sorgu yöntemi hello değişkenlerin değerleri şunlardır: 
  * parametreleri. AlternateFilters.Count: 1
  * parametreleri. AlternateFilters.ElementAt(0). AttributePath: "externalID"
  * parametreleri. AlternateFilters.ElementAt(0). Karşılaştırmaİşleci: ComparisonOperator.Equals
  * parametreleri. AlternateFilter.ElementAt(0). ComparisonValue: "jyoung"
  * correlationIdentifier: System.Net.Http.HttpRequestMessage.GetOwinEnvironment["owin. RequestId"] 

2. Merhaba yanıt tooa sorgu toohello web hizmeti, bir kullanıcının hello mailNickname öznitelik değeri ile eşleşen bir externalID öznitelik değeri olan bir kullanıcı için tüm kullanıcıların döndürmezse, Azure Active Directory bu hello hizmet sağlama kullanıcı istekleri karşılık gelen toohello bir Azure Active Directory'de.  Böyle bir istek bir örneği burada verilmiştir: 
  ````
    POST https://.../scim/Users HTTP/1.1
    Authorization: Bearer ...
    Content-type: application/json
    {
      "schemas":
      [
        "urn:ietf:params:scim:schemas:core:2.0:User",
        "urn:ietf:params:scim:schemas:extension:enterprise:2.0User"],
      "externalId":"jyoung",
      "userName":"jyoung",
      "active":true,
      "addresses":null,
      "displayName":"Joy Young",
      "emails": [
        {
          "type":"work",
          "value":"jyoung@Contoso.com",
          "primary":true}],
      "meta": {
        "resourceType":"User"},
       "name":{
        "familyName":"Young",
        "givenName":"Joy"},
      "phoneNumbers":null,
      "preferredLanguage":null,
      "title":null,
      "department":null,
      "manager":null}
  ````
  Merhaba ortak dil altyapısı kitaplıkları SCIM'yi Hizmetleri uygulamak için Microsoft tarafından sağlanan bu isteği bir çağrı toohello hello hizmetin sağlayıcısının oluşturma yöntemini çevirir.  Merhaba Create yönteminin bu imzaya sahip: 
  ````
    // System.Threading.Tasks.Tasks is defined in mscorlib.dll.  
    // Microsoft.SystemForCrossDomainIdentityManagement.Resource is defined in 
    // Microsoft.SystemForCrossDomainIdentityManagement.Schemas.  

    System.Threading.Tasks.Task<Microsoft.SystemForCrossDomainIdentityManagement.Resource> Create(
      Microsoft.SystemForCrossDomainIdentityManagement.Resource resource, 
      string correlationIdentifier);
  ````
  Bir istek tooprovision bir kullanıcı hello hello kaynak bağımsız değişkeni hello Microsoft.SystemForCrossDomainIdentityManagement örneği değeridir. Merhaba Microsoft.SystemForCrossDomainIdentityManagement.Schemas Kitaplığı'nda tanımlanan Core2EnterpriseUser sınıfı.  Merhaba isteği tooprovision hello kullanıcı başarılı olursa, ardından hello hello yöntemi beklenen tooreturn hello Microsoft.SystemForCrossDomainIdentityManagement örneği uygulamasıdır. Merhaba tanımlayıcısı özelliği hello değeriyle Core2EnterpriseUser sınıfı hello yeni sağlanan kullanıcının benzersiz tanıtıcısı toohello ayarlayın.  

3. tooupdate tooexist bir kimlik deposu olarak bilinen bir kullanıcı tarafından bir SCIM'yi, kullanıcının geçerli durumunu hello gibi bir istekle hello Hizmeti'nden istiyor tarafından Azure Active Directory kazançlar fronted: 
  ````
    GET ~/scim/Users/54D382A4-2050-4C03-94D1-E769F1D15682 HTTP/1.1
    Authorization: Bearer ...
  ````
  Merhaba ortak dil altyapısı kitaplıkları SCIM'yi Hizmetleri uygulamak için Microsoft tarafından sağlanan kullanılarak oluşturulmuş bir hizmetinde hello isteği çağrısı toohello hello hizmetin sağlayıcısının alma yöntemini çevrilir.  Merhaba alma yöntemini hello imzası şöyledir: 
  ````
    // System.Threading.Tasks.Tasks is defined in mscorlib.dll.  
    // Microsoft.SystemForCrossDomainIdentityManagement.Resource and 
    // Microsoft.SystemForCrossDomainIdentityManagement.IResourceRetrievalParameters 
    // are defined in Microsoft.SystemForCrossDomainIdentityManagement.Schemas.  
    System.Threading.Tasks.Task<Microsoft.SystemForCrossDomainIdentityManagement.Resource> 
       Retrieve(
         Microsoft.SystemForCrossDomainIdentityManagement.IResourceRetrievalParameters 
           parameters, 
           string correlationIdentifier);

    public interface 
      Microsoft.SystemForCrossDomainIdentityManagement.IResourceRetrievalParameters:   
        IRetrievalParameters
        {
          Microsoft.SystemForCrossDomainIdentityManagement.IResourceIdentifier 
            ResourceIdentifier 
              { get; }
    }
    public interface Microsoft.SystemForCrossDomainIdentityManagement.IResourceIdentifier
    {
        string Identifier 
          { get; set; }
        string Microsoft.SystemForCrossDomainIdentityManagement.SchemaIdentifier 
          { get; set; }
    }
  ````
  Bir kullanıcı bir istek tooretrieve hello geçerli durumu Hello örnekte hello'hello parametreleri bağımsız değişkenin değeri sağlanan hello nesne hello özelliklerinin hello değerleri aşağıdaki gibidir: 
  
  * Tanımlayıcı: "54D382A4-2050-4C03-94D1-E769F1D15682"
  * SchemaIdentifier: "urn: ietf:params:scim:schemas:extension:enterprise:2.0:User"

4. Hello hello başvuru özniteliği hello kimlik deposundaki geçerli değeri tarafından fronted olup olmadığına bakılmaksızın bir başvuru özniteliği güncelleştirilmiş, toobe sonra Azure Active Directory sorgularını hello hizmet toodetermine ise hello hizmeti zaten bu özniteliğin değerini hello eşleşir Azure Active Directory'de. Kullanıcılar için hangi hello geçerli değeri bu şekilde sorgulanır hello yalnızca öznitelik hello Yöneticisi özniteliğidir. Burada, belirli bir kullanıcı nesnesinin hello Yöneticisi özniteliği şu anda belirli bir değere sahip olup olmadığını isteği toodetermine örneği verilmiştir: 
  ````
    GET ~/scim/Users?filter=id eq 54D382A4-2050-4C03-94D1-E769F1D15682 and manager eq 2819c223-7f76-453a-919d-413861904646&attributes=id HTTP/1.1
    Authorization: Bearer ...
  ````
  Merhaba değeri hello öznitelikleri sorgu parametresinin kimliği güveninin bir kullanıcı nesnesi varsa hello hello filtre sorgu parametresi değeri olarak sağlanan hello ifadeyi karşılayan sonra hello hizmetidir beklenen toorespond urn: ietf:params:scim:schemas ile: yalnızca bu kaynağın ID özniteliği hello değeri de dahil olmak üzere çekirdek: 2.0:User veya urn: ietf:params:scim:schemas:extension:enterprise:2.0:User kaynak.  Merhaba hello değerini **kimliği** toohello istek sahibi bilinen öznitelik. Merhaba filtre sorgu parametresi hello değerinde bulunur; Merhaba amacı söylemelisiniz gerçekten toorequest hello filtre ifadesinin olup olmadığına böyle nesne bir gösterge olarak çağıran mevcut bir kaynak en az bir gösterimi ' dir.   

  Merhaba hizmet SCIM'yi Hizmetleri uygulamak için Microsoft tarafından sağlanan Merhaba ortak dil altyapısı kitaplıkları kullanılarak oluşturuldu, hello isteği çağrısı toohello hello hizmetin sağlayıcısının sorgu yöntemini çevrilir. hello'hello parametreleri bağımsız değişkenin değeri sağlanan hello nesnesinin hello özelliklerini Hello değeri aşağıdaki gibidir: 
  
  * parametreleri. AlternateFilters.Count: 2
  * parametreleri. AlternateFilters.ElementAt(x). AttributePath: "id"
  * parametreleri. AlternateFilters.ElementAt(x). Karşılaştırmaİşleci: ComparisonOperator.Equals
  * parametreleri. AlternateFilter.ElementAt(x). ComparisonValue: "54D382A4-2050-4C03-94D1-E769F1D15682"
  * parametreleri. AlternateFilters.ElementAt(y). AttributePath: "Yönetici"
  * parametreleri. AlternateFilters.ElementAt(y). Karşılaştırmaİşleci: ComparisonOperator.Equals
  * parametreleri. AlternateFilter.ElementAt(y). ComparisonValue: "2819c223-7f76-453a-919d-413861904646"
  * parametreleri. RequestedAttributePaths.ElementAt(0): "id"
  * parametreleri. SchemaIdentifier: "urn: ietf:params:scim:schemas:extension:enterprise:2.0:User"

  Burada, hello dizinin x hello değeri 0 olabilir ve hello hello dizin y değerini 1, olabilir ya da x hello değeri 1 olabilir ve hello y değerini hello filtre sorgu parametresi hello ifadelerin hello sırasını bağlı olarak 0 olabilir.   

5. Azure Active Directory tooan SCIM'yi hizmet tooupdate bir kullanıcı bir isteğin bir örnek aşağıda verilmiştir: 
  ````
    PATCH ~/scim/Users/54D382A4-2050-4C03-94D1-E769F1D15682 HTTP/1.1
    Authorization: Bearer ...
    Content-type: application/json
    {
      "schemas": 
      [
        "urn:ietf:params:scim:api:messages:2.0:PatchOp"],
      "Operations":
      [
        {
          "op":"Add",
          "path":"manager",
          "value":
            [
              {
                "$ref":"http://.../scim/Users/2819c223-7f76-453a-919d-413861904646",
                "value":"2819c223-7f76-453a-919d-413861904646"}]}]}
  ````
  hello Microsoft ortak dil altyapısı kitaplıkları SCIM'yi Hizmetleri uygulamak için bir çağrı toohello hello hizmetin sağlayıcısının güncelleştirme yöntemini hello isteği çevirir. Merhaba güncelleştirme yöntemi hello imzası şöyledir: 
  ````
    // System.Threading.Tasks.Tasks and 
    // System.Collections.Generic.IReadOnlyCollection<T>
    // are defined in mscorlib.dll.  
    // Microsoft.SystemForCrossDomainIdentityManagement.IPatch, 
    // Microsoft.SystemForCrossDomainIdentityManagement.PatchRequestBase, 
    // Microsoft.SystemForCrossDomainIdentityManagement.IResourceIdentifier, 
    // Microsoft.SystemForCrossDomainIdentityManagement.PatchOperation, 
    // Microsoft.SystemForCrossDomainIdentityManagement.OperationName, 
    // Microsoft.SystemForCrossDomainIdentityManagement.IPath and 
    // Microsoft.SystemForCrossDomainIdentityManagement.OperationValue 
    // are all defined in Microsoft.SystemForCrossDomainIdentityManagement.Protocol. 

    System.Threading.Tasks.Task Update(
      Microsoft.SystemForCrossDomainIdentityManagement.IPatch patch, 
      string correlationIdentifier);

    public interface Microsoft.SystemForCrossDomainIdentityManagement.IPatch
    {
    Microsoft.SystemForCrossDomainIdentityManagement.PatchRequestBase 
      PatchRequest 
        { get; set; }
    Microsoft.SystemForCrossDomainIdentityManagement.IResourceIdentifier 
      ResourceIdentifier 
        { get; set; }        
    }

    public class PatchRequest2: 
      Microsoft.SystemForCrossDomainIdentityManagement.PatchRequestBase
    {
    public System.Collections.Generic.IReadOnlyCollection
      <Microsoft.SystemForCrossDomainIdentityManagement.PatchOperation> 
        Operations
        { get;}

    public void AddOperation(
      Microsoft.SystemForCrossDomainIdentityManagement.PatchOperation operation);
    }

    public class PatchOperation
    {
    public Microsoft.SystemForCrossDomainIdentityManagement.OperationName 
      Name
      { get; set; }

    public Microsoft.SystemForCrossDomainIdentityManagement.IPath 
      Path
      { get; set; }

    public System.Collections.Generic.IReadOnlyCollection
      <Microsoft.SystemForCrossDomainIdentityManagement.OperationValue> Value
      { get; }

    public void AddValue(
      Microsoft.SystemForCrossDomainIdentityManagement.OperationValue value);
    }

    public enum OperationName
    {
      Add,
      Remove,
      Replace
    }

    public interface IPath
    {
      string AttributePath { get; }
      System.Collections.Generic.IReadOnlyCollection<IFilter> SubAttributes { get; }
      Microsoft.SystemForCrossDomainIdentityManagement.IPath ValuePath { get; }
    }

    public class OperationValue
    {
      public string Reference
      { get; set; }

      public string Value
      { get; set; }
    }
  ````
    İstek tooupdate kullanıcı Hello örnekte hello'hello düzeltme eki bağımsız değişkenin değeri sağlanan hello nesnesi bu özellik değerlerini içerir: 
  
  * ResourceIdentifier.Identifier: "54D382A4-2050-4C03-94D1-E769F1D15682"
  * ResourceIdentifier.SchemaIdentifier: "urn: ietf:params:scim:schemas:extension:enterprise:2.0:User"
  * (PatchRequest PatchRequest2 olarak). Operations.Count: 1
  * (PatchRequest PatchRequest2 olarak). Operations.ElementAt(0). OperationName: OperationName.Add
  * (PatchRequest PatchRequest2 olarak). Operations.ElementAt(0). Path.AttributePath: "Yönetici"
  * (PatchRequest PatchRequest2 olarak). Operations.ElementAt(0). Value.Count: 1
  * (PatchRequest PatchRequest2 olarak). Operations.ElementAt(0). Value.ElementAt(0). Başvuru: http://.../scim/Users/2819c223-7f76-453a-919d-413861904646
  * (PatchRequest PatchRequest2 olarak). Operations.ElementAt(0). Value.ElementAt(0). Değer: 2819c223-7f76-453a-919d-413861904646

6. toode sağlama SCIM'yi hizmeti tarafından bir kimlik deposu kullanıcıdan fronted, Azure AD gibi bir isteği gönderir: 
  ````
    DELETE ~/scim/Users/54D382A4-2050-4C03-94D1-E769F1D15682 HTTP/1.1
    Authorization: Bearer ...
  ````
  Merhaba hizmet SCIM'yi Hizmetleri uygulamak için Microsoft tarafından sağlanan Merhaba ortak dil altyapısı kitaplıkları kullanılarak oluşturuldu, hello isteği çağrısı toohello hello hizmetin sağlayıcısının Delete yöntemini çevrilir.   Bu yöntem, bu imza sahiptir: 
  ````
    // System.Threading.Tasks.Tasks is defined in mscorlib.dll.  
    // Microsoft.SystemForCrossDomainIdentityManagement.IResourceIdentifier, 
    // is defined in Microsoft.SystemForCrossDomainIdentityManagement.Protocol. 
    System.Threading.Tasks.Task Delete(
      Microsoft.SystemForCrossDomainIdentityManagement.IResourceIdentifier  
        resourceIdentifier, 
      string correlationIdentifier);
  ````
  Hello'hello resourceIdentifier bağımsız değişkenin değeri sağlanan hello nesnesi istek toode-provizyon kullanıcı hello örnekte bu özellik değerlerini içerir: 
  
  * ResourceIdentifier.Identifier: "54D382A4-2050-4C03-94D1-E769F1D15682"
  * ResourceIdentifier.SchemaIdentifier: "urn: ietf:params:scim:schemas:extension:enterprise:2.0:User"

## <a name="group-provisioning-and-de-provisioning"></a>Grup sağlama ve sağlamayı kaldırma özelliklerini
Merhaba, aşağıdaki çizimde gösterilmektedir Merhaba iletileri Azure AcD tooa SCIM'yi hizmet toomanage hello kullanım ömrü boyunca bir grubu başka bir kimlik deposu gönderir.  Bu iletiler toousers üç yolla ilgili Merhaba iletileri farklıdır: 

* bir grup kaynak Hello şeması http://schemas.microsoft.com/2006/11/ResourceManagement/ADSCIM/Group tanımlanır.  
* Bu hello üyeleri öznitelik tooretrieve grupları iznine isteği yanıt toohello isteğinde sağlanan herhangi bir kaynağa dışında toobe sayısıdır.  
* İstekleri toodetermine olan istekleri hello üyeleri özniteliği hakkında bir başvuru özniteliği belirli bir değere sahip olup olmadığını belirler.  

![][5]
*Şekil 6: Grup sağlama ve sağlamayı kaldırma özelliklerini sırası*

## <a name="related-articles"></a>İlgili makaleler
* [Azure Active Directory'de Uygulama Yönetimi için Makale Dizini](active-directory-apps-index.md)
* [Kullanıcı hazırlama/sağlama kaldırmayı tooSaaS uygulamaları otomatikleştirme](active-directory-saas-app-provisioning.md)
* [Kullanıcı sağlama öznitelik eşlemelerini özelleştirme](active-directory-saas-customizing-attribute-mappings.md)
* [Özellik eşlemeleri için ifade yazma](active-directory-saas-writing-expressions-for-attribute-mappings.md)
* [Kapsam belirleme filtreleri kullanıcı sağlama](active-directory-saas-scoping-filters.md)
* [Hesap sağlama bildirimleri](active-directory-saas-account-provisioning-notifications.md)
* [İlgili nasıl öğreticiler listesi tooIntegrate SaaS uygulamaları](active-directory-saas-tutorial-list.md)

<!--Image references-->
[0]: ./media/active-directory-scim-provisioning/scim-figure-1.PNG
[1]: ./media/active-directory-scim-provisioning/scim-figure-2a.PNG
[2]: ./media/active-directory-scim-provisioning/scim-figure-2b.PNG
[3]: ./media/active-directory-scim-provisioning/scim-figure-3.PNG
[4]: ./media/active-directory-scim-provisioning/scim-figure-4.PNG
[5]: ./media/active-directory-scim-provisioning/scim-figure-5.PNG
