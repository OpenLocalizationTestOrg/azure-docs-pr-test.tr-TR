---
title: "Azure AD kimlik doğrulama tooaccess .NET ile Azure Media Services API aaaUse | Microsoft Docs"
description: "Bu konu, nasıl toouse Azure Active Directory (Azure AD) kimlik doğrulama tooaccess Azure Media Services gösterir (AMS) API .NET ile."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/17/2017
ms.author: juliako
ms.openlocfilehash: 2f750e460d9e476ad92e96adeac6500cb692cd77
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-ad-authentication-tooaccess-azure-media-services-api-with-net"></a>.NET ile Azure AD kimlik doğrulama tooaccess Azure Media Services API kullanın

4.0.0.4 windowsazure.mediaservices ile başlayarak, Azure Media Services, Azure Active Directory (Azure AD) tabanlı kimlik doğrulamasını destekler. Bu konu, nasıl gösterir toouse Azure AD kimlik doğrulama tooaccess Microsoft .NET ile Azure Media Services API.

## <a name="prerequisites"></a>Ön koşullar

- Bir Azure hesabı. Ayrıntılı bilgi için bkz. [Azure Ücretsiz Deneme Sürümü](https://azure.microsoft.com/pricing/free-trial/). 
- Bir Media Services hesabı. Daha fazla bilgi için bkz: [hello Azure portal kullanarak bir Azure Media Services hesabı oluşturma](media-services-portal-create-account.md).
- Merhaba son [NuGet](https://www.nuget.org/packages/windowsazure.mediaservices) paket.
- Merhaba konu aşina [AAD kimlik doğrulamasına genel bakış ile Azure Media Services API erişme](media-services-use-aad-auth-to-access-ams-api.md). 

Azure Media Services ile Azure AD kimlik doğrulaması kullanırken, aşağıdaki iki yöntemden biriyle doğrulayabilir:

- **Kullanıcı kimlik doğrulaması** Azure Media Services kaynaklarla hello uygulama toointeract kullanan bir kişinin kimliğini doğrular. Merhaba etkileşimli uygulaması ilk hello kullanıcıdan kimlik bilgilerini ister. İşlerini kodlama yetkili kullanıcıların toomonitor tarafından kullanılan veya canlı akış Yönetimi konsol uygulaması örneğidir. 
- **Hizmet asıl kimlik doğrulaması** bir hizmetin kimliğini doğrular. Genellikle bu kimlik doğrulama yöntemini kullanan uygulamalar, arka plan programı services, orta katman Hizmetleri veya web uygulamaları, işlev uygulamalarının, logic apps, API veya mikro gibi zamanlanmış işleri çalıştırma uygulamalardır.

>[!IMPORTANT]
>Azure medya hizmeti şu anda Azure erişim denetimi hizmeti kimlik doğrulama modelini destekler. Ancak, erişim denetimi yetkilendirme 1 Haziran 2018 kullanım toobe geçiyor. Mümkün olan en kısa sürede tooan Azure Active Directory kimlik doğrulama modeli geçirmek öneririz.

## <a name="get-an-azure-ad-access-token"></a>Bir Azure AD erişim belirteci alma

Azure AD kimlik doğrulaması ile tooconnect toohello Azure Media Services API, hello istemci uygulamanın toorequest bir Azure AD erişim belirteci gerekir. Merhaba Media Services .NET İstemci SDK, birçok tooacquire bir Azure AD erişim belirteci nasıl Sarmalanan ve sizin için hello Basitleştirilmiş hakkında hello ayrıntılarının kullandığınızda [AzureAdTokenProvider](https://github.com/Azure/azure-sdk-for-media-services/blob/dev/src/net/Client/Common/Common.Authentication/AzureAdTokenProvider.cs) ve [AzureAdTokenCredentials ](https://github.com/Azure/azure-sdk-for-media-services/blob/dev/src/net/Client/Common/Common.Authentication/AzureAdTokenCredentials.cs) sınıfları. 

Örneğin, tooprovide hello Azure AD yetkilisi, Media Services kaynak URI'si ya da yerel gerekmeyen Azure AD uygulama ayrıntıları. Bunlar hello Azure AD erişim belirteci sağlayıcısı sınıfı tarafından zaten yapılandırılmış iyi bilinen değerlerdir. 

Azure medya hizmeti .NET SDK'sı kullanmıyorsanız hello kullanmanızı öneririz [Azure AD kimlik doğrulama Kitaplığı](../active-directory/develop/active-directory-authentication-libraries.md). Azure AD kimlik doğrulama kitaplığı ile toouse gerektiğini hello parametreleri tooget değerlerini görmek [hello Azure portal tooaccess Azure AD kimlik doğrulama ayarlarını kullanmak](media-services-portal-get-started-with-aad.md).

Merhaba hello varsayılan uygulaması değiştirme hello seçeneğiniz de **AzureAdTokenProvider** kendi uygulaması.

## <a name="install-and-configure-azure-media-services-net-sdk"></a>Yükleme ve Azure Media Services .NET SDK'sını yapılandırma

>[!NOTE] 
>Merhaba Media Services .NET SDK'sı ile toouse Azure AD kimlik doğrulaması, gereksinim duyduğunuz toohave hello son [NuGet](https://www.nuget.org/packages/windowsazure.mediaservices) paket. Ayrıca, bir başvuru toohello ekleme **Microsoft.IdentityModel.Clients.activedirectory tarafından** derleme. Mevcut bir uygulamayı kullanıyorsanız, hello dahil **Microsoft.WindowsAzure.MediaServices.Client.Common.Authentication.dll** derleme. 

1. Visual Studio'da yeni bir C# konsol uygulaması oluşturun.
2. Kullanım hello [windowsazure.mediaservices](https://www.nuget.org/packages/windowsazure.mediaservices) NuGet paketi tooinstall **Azure Media Services .NET SDK'sı**. 

    NuGet, kullanarak tooadd başvuruları hello aşağıdaki adımları gerçekleştirin: içinde **Çözüm Gezgini**hello proje adına sağ tıklayın ve ardından **Manage NuGet paketleri**. Ardından, arama **windowsazure.mediaservices** seçip **yükleme**.
    
    -veya-

    Çalışma hello komutunda aşağıdaki **Paket Yöneticisi Konsolu** Visual Studio.

        Install-Package windowsazure.mediaservices -Version 4.0.0.4

3. Ekleme **kullanarak** tooyour kaynak kodu.

        using Microsoft.WindowsAzure.MediaServices.Client; 

## <a name="use-user-authentication"></a>Kullanıcı kimlik doğrulamasını kullan

Merhaba kullanıcı kimlik doğrulaması seçeneği ile tooconnect toohello Azure medya hizmeti API'si, hello istemci uygulamasını kullanarak bir Azure AD belirteci hello şu parametreler toorequest gerekir:  

- Azure AD Kiracı uç noktası. Azure portal hello Hello Kiracı bilgi alınabilir. Merhaba oturum açmış kullanıcı hello sağ üst köşedeki üzerine gelerek.
- Media Services kaynak URI'si.
- Media Services (yerel) uygulama istemci kimliği 
- Media Services (yerel) uygulama yeniden yönlendirme URI'si. 

Bu parametrelerin Hello değerleri bulunabilir **AzureEnvironments.AzureCloudEnvironment**. Merhaba **AzureEnvironments.AzureCloudEnvironment** hello .NET SDK'sı tooget bir yardımcı hello sağ ortam değişkeni ayarlarının ortak bir Azure veri merkezi için sabittir. 

Önceden tanımlanmış ortam ayarları yalnızca hello ortak veri merkezlerinde Media Services erişmek için içerir. Sovereign veya kamu bulut bölgeleri için kullandığınız **AzureChinaCloudEnvironment**, **AzureUsGovernmentEnvrionment**, veya **AzureGermanCloudEnvironment** sırasıyla.

Aşağıdaki kod örneğine hello bir belirteç oluşturur:
    
    var tokenCredentials = new AzureAdTokenCredentials("microsoft.onmicrosoft.com", AzureEnvironments.AzureCloudEnvironment);
    var tokenProvider = new AzureAdTokenProvider(tokenCredentials);
  
toostart Media Services karşı programlama, toocreate gereken bir **CloudMediaContext** hello sunucu bağlamı temsil eden örneği. Merhaba **CloudMediaContext** işleri, varlıklar, dosyaları, erişim ilkeleri ve bulucular dahil olmak üzere başvuruları tooimportant koleksiyonları içerir. 

Toopass hello etmeniz **kaynak medya REST Hizmetleri için URI** toohello **CloudMediaContext** Oluşturucusu. Medya REST Hizmetleri, oturum açma toohello Azure portal, Azure Media Services hesabınızı seçin tooget hello kaynak URI'si seçin **API erişimini**ve ardından **tooAzure Media Services kullanıcıyla Bağlan kimlik doğrulama**. 

Merhaba aşağıdaki kod örneği oluşturur bir **CloudMediaContext** örneği:

    CloudMediaContext context = new CloudMediaContext(new Uri("YOUR REST API ENDPOINT HERE"), tokenProvider);

Aşağıdaki örneğine hello nasıl toocreate hello Azure AD belirteci ve hello bağlamını gösterir:

    namespace AADAuthSample
    {
        class Program
        {
            static void Main(string[] args)
            {
                // Specify your Azure AD tenant domain, for example "microsoft.onmicrosoft.com".
                var tokenCredentials = new AzureAdTokenCredentials("{YOUR AAD TENANT DOMAIN HERE}", AzureEnvironments.AzureCloudEnvironment);
    
                var tokenProvider = new AzureAdTokenProvider(tokenCredentials);
    
                // Specify your REST API endpoint, for example "https://accountname.restv2.westcentralus.media.azure.net/API".
                CloudMediaContext context = new CloudMediaContext(new Uri("YOUR REST API ENDPOINT HERE"), tokenProvider);
    
                var assets = context.Assets;
                foreach (var a in assets)
                {
                    Console.WriteLine(a.Name);
                }
            }
    
        }
    }

>[!NOTE]
>Bildiren bir özel durum alırsanız "Merhaba uzak sunucu bir hata döndürdü: (401) yetkisiz" Merhaba bkz [erişim denetimi](media-services-use-aad-auth-to-access-ams-api.md#access-control) erişme Azure Media Services API bölümle Azure AD kimlik doğrulamasına genel bakış.

## <a name="use-service-principal-authentication"></a>Hizmet asıl kimlik doğrulaması kullanma
    
Merhaba hizmet asıl seçeneğiyle tooconnect toohello Azure Media Services API, orta katman uygulamanızın (web API ya da web uygulaması) ile şu parametreler hello toorequests bir Azure AD belirteci gerekir:  

- Azure AD Kiracı uç noktası. Azure portal hello Hello Kiracı bilgi alınabilir. Merhaba oturum açmış kullanıcı hello sağ üst köşedeki üzerine gelerek.
- Media Services kaynak URI'si.
- Azure AD uygulama değerleri: Merhaba **istemci kimliği** ve **gizli**.

Merhaba hello değerlerini **istemci kimliği** ve **gizli** parametreleri hello Azure portalında bulunabilir. Daha fazla bilgi için bkz: [hello Azure portalında Azure AD kimlik doğrulaması kullanarak ile çalışmaya başlama](media-services-portal-get-started-with-aad.md).

Merhaba aşağıdaki kod örneğinde bir belirteç hello kullanarak oluşturur **AzureAdTokenCredentials** alan oluşturucu **AzureAdClientSymmetricKey** bir parametre olarak: 
    
    var tokenCredentials = new AzureAdTokenCredentials("{YOUR Azure AD TENANT DOMAIN HERE}", 
                                new AzureAdClientSymmetricKey("{YOUR CLIENT ID HERE}", "{YOUR CLIENT SECRET}"), 
                                AzureEnvironments.AzureCloudEnvironment);

    var tokenProvider = new AzureAdTokenProvider(tokenCredentials);

Ayrıca hello belirtebilirsiniz **AzureAdTokenCredentials** alan oluşturucu **AzureAdClientCertificate** bir parametre olarak. 

Hakkında yönergeler için toocreate ve Azure AD tarafından kullanılabilmesi için bkz: bir formda bir sertifika yapılandırmak [tooAzure AD sertifikalarla - elle yapılandırma adımları arka plan programı uygulamalarında kimlik doğrulama](https://github.com/Azure-Samples/active-directory-dotnet-daemon-certificate-credential/blob/master/Manual-Configuration-Steps.md).

    var tokenCredentials = new AzureAdTokenCredentials("{YOUR Azure AD TENANT DOMAIN HERE}", 
                                new AzureAdClientCertificate("{YOUR CLIENT ID HERE}", "{YOUR CLIENT CERTIFICATE THUMBPRINT}"), 
                                AzureEnvironments.AzureCloudEnvironment);

toostart Media Services karşı programlama, toocreate gereken bir **CloudMediaContext** hello sunucu bağlamı temsil eden örneği. Toopass hello etmeniz **kaynak medya REST Hizmetleri için URI** toohello **CloudMediaContext** Oluşturucusu. Merhaba alabilirsiniz **kaynak medya REST Hizmetleri için URI** hello Azure portalı değerinden.

Merhaba aşağıdaki kod örneği oluşturur bir **CloudMediaContext** örneği:

    CloudMediaContext context = new CloudMediaContext(new Uri("YOUR REST API ENDPOINT HERE"), tokenProvider);
    
Aşağıdaki örneğine hello nasıl toocreate hello Azure AD belirteci ve hello bağlamını gösterir:

    namespace AADAuthSample
    {
    
        class Program
        {
            static void Main(string[] args)
            {
                var tokenCredentials = new AzureAdTokenCredentials("{YOUR Azure AD TENANT DOMAIN HERE}", 
                                            new AzureAdClientSymmetricKey("{YOUR CLIENT ID HERE}", "{YOUR CLIENT SECRET}"), 
                                            AzureEnvironments.AzureCloudEnvironment);
            
                var tokenProvider = new AzureAdTokenProvider(tokenCredentials);
    
                // Specify your REST API endpoint, for example "https://accountname.restv2.westcentralus.media.azure.net/API".      
                CloudMediaContext context = new CloudMediaContext(new Uri("YOUR REST API ENDPOINT HERE"), tokenProvider);
    
                var assets = context.Assets;
                foreach (var a in assets)
                {
                    Console.WriteLine(a.Name);
                }
    
                Console.ReadLine();
            }
    
        }
    }

## <a name="next-steps"></a>Sonraki adımlar

Kullanmaya başlama [tooyour hesabı dosyaları karşıya yükleme](media-services-dotnet-upload-files.md).
