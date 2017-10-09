---
title: Mobile Engagement REST API'leri ile aaaAuthenticate
description: "Açıklar nasıl Azure Mobile Engagement REST API'leri ile tooauthenticate"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: da82cb36-957a-4e19-a805-b44733cf6597
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 10/05/2016
ms.author: wesmc;ricksal
ms.openlocfilehash: 9b54aa5ec3da4bcf55ffe5b7e8d1759095d0c486
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="authenticate-with-mobile-engagement-rest-apis"></a>Mobil katılım REST API'leri ile kimlik doğrulaması
## <a name="overview"></a>Genel Bakış
Bu belgede nasıl tooget geçerli bir AAD Oauth belirteci hello Mobile Engagement REST API'leri ile tooauthenticate açıklanmaktadır. 

Geçerli bir Azure aboneliğinizin olması ve aşağıdakilerden birini kullanarak bir Mobile Engagement uygulaması oluşturdunuz varsayılır bizim [Geliştirici öğreticileri](mobile-engagement-windows-store-dotnet-get-started.md).

## <a name="authentication"></a>Kimlik Doğrulaması
Bir Microsoft Azure Active Directory token kimlik doğrulaması için kullanılan OAuth tabanlı. 

Sipariş tooauthentication bir API istekte bir authorization üstbilgisi form aşağıdaki Merhaba tooevery isteği eklenmesi gerekir:

    Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGmJlNmV2ZWJPamg2TTNXR1E...

> [!NOTE]
> Azure Active Directory belirteçleri 1 saat içinde süresi dolacak.
> 
> 

Bir belirteç birkaç yolu tooget vardır. API genellikle bir bulut hizmetinden adlı hello itibaren toouse bir API anahtarı istiyor. API anahtarını Azure terminolojisi içinde bir hizmet asıl parola adı verilir. Merhaba aşağıdaki yordamda açıklanmıştır tek yönlü toosetting onu el ile ayarlama.

### <a name="one-time-setup-using-script"></a>Tek seferlik kurulumu (kod kullanılarak)
Merhaba kümesi hello kurulum için en az zaman alır, ancak hello en izin verilen varsayılanlarını kullanır bir PowerShell komut dosyası kullanarak tooperform hello Kurulum aşağıdaki yönergeleri izlemelidir. İsteğe bağlı olarak, ayrıca hello hello yönergelerini izleyebilirsiniz [el ile kuruluma](mobile-engagement-api-authentication-manual.md) hello doğrudan Azure portal ve yüksekse yapılandırma bunu. 

1. Merhaba Azure PowerShell'in en son sürümünü almak [burada](http://aka.ms/webpi-azps). Bu bkz hello yükleme yönergeleri ile ilgili daha fazla bilgi için [bağlantı](/powershell/azure/overview).  
2. Azure PowerShell yüklendikten sonra hello sahip tooensure kullanım hello aşağıdaki komutları **Azure Modülü** yüklü:
   
    a. Hello Azure PowerShell modülü hello kullanılabilir modülleri listesinde kullanılabilir olduğundan emin olun. 
   
        Get-Module –ListAvailable 
   
    ![Mevcut Azure modülleri][1]
   
    b. Merhaba listesinin içinde hello Azure PowerShell modülü bulamazsanız toorun hello aşağıdaki gerekir:
   
        Import-Module Azure 
3. Çalıştırarak oturum açma toohello Azure Kaynak Yöneticisi'nden PowerShell komutunu aşağıdaki ve Azure hesabınız için kullanıcı adı ve parola sağlayarak hello: 
   
        Login-AzureRmAccount
4. Birden çok aboneliğiniz varsa, hello aşağıdaki değeri çalıştırmanız gerekir:
   
    a. Tüm abonelikleri ve kopyalama hello Subscriptionıd istediğiniz hello aboneliğin listesini toouse alın. Bu abonelik aynı olan hello adımıdır mobil katılım uygulamasını hello olduğundan emin olun kullanarak toointeract hello API'leri. 
   
        Get-AzureRmSubscription
   
    b. Çalışma hello aşağıdaki kullanılan sağlayan hello Subscriptionıd tooconfigure hello abonelik toobe komutu.
   
        Select-AzureRmSubscription –SubscriptionId <subscriptionId>
5. Merhaba Hello metni kopyalayın [yeni AzureRmServicePrincipalOwner.ps1](https://raw.githubusercontent.com/matt-gibbs/azbits/master/src/New-AzureRmServicePrincipalOwner.ps1) tooyour yerel makine komut dosyası ve bir PowerShell cmdlet'ini olarak kaydedin (örneğin `APIAuth.ps1`) ve bu yürütme `.\APIAuth.ps1`. 
6. Merhaba komut dosyası, giriş için bir tooprovide ister **principalName**. Active Directory uygulamanız (örneğin APIAuth) toouse toocreate istediğiniz uygun bir ad sağlayın. 
7. Merhaba betik tamamlandıktan sonra ihtiyacınız olacak dört değerleri aşağıdaki hello görüntülenir tooauthenticate program aracılığıyla AD ile nedenle emin toocopy olun bunları. 
   
    **Tenantıd**, **Subscriptionıd**, **ApplicationId**, ve **gizli**.
   
    Tenantıd olarak kullanacağınız `{TENANT_ID}`, ApplicationId olarak `{CLIENT_ID}` ve gizli olarak `{CLIENT_SECRET}`.
   
   > [!NOTE]
   > Varsayılan güvenlik ilkenizin bir PowerShell komut dosyalarının çalışmasını engelleyebilir. Gerekiyorsa, komutu aşağıdaki hello kullanarak, yürütme İlkesi tooallow komut dosyası yürütme geçici olarak yapılandırın:
   > 
   > Set-ExecutionPolicy RemoteSigned
   > 
   > 
8. İşte nasıl hello PS cmdlet'leri kümesini aşağıdaki gibidir. 
   
    ![][3]
9. Hello Azure Yönetim Portalı'nda toohello komut dosyasının sağlanan yeni bir AD uygulamasını hello adıyla, oluşturulduğunu denetleyin **principalName** altında **Şirketimin sahip olduğu uygulamalar Göster**.
   
    ![][4]

#### <a name="steps-tooget-a-valid-token"></a>Adımları tooget geçerli bir belirteci
1. Şu parametreler hello ile Merhaba API çağrısı ve emin tooreplace hello KİRACI olun\_kimliği, istemci\_kimliği ve istemci\_gizli anahtarı:
   
   * **İstek URL'si** olarak *https://login.microsoftonline.com/ {KİRACI\_kimliği} / oauth2/belirteci*
   * **HTTP Content-Type üstbilgisi** olarak *uygulama/x-www-form-urlencoded*
   * **HTTP isteği gövdesinin** olarak *vermek\_türü = istemci\_kimlik bilgileri & client_id = {istemci\_kimliği} & client_secret = {istemci\_gizli} & resource=https%3A%2F%2Fmanagement.core.windows.net%2F*
     
     Merhaba, bir örnek isteği aşağıdadır:
     
       POST / {TENANT_ID} / oauth2/token HTTP/1.1 ana: login.microsoftonline.com Content-Type: uygulama/x-www-form-urlencoded grant_type client_credentials & client_id = {CLIENT_ID} = & client_secret {CLIENT_SECRET} = & çözüm kaynağına https % 3A % = 2f%2Fmanagement.Core.Windows.NET%2f
     
     Bir örnek yanıt şöyledir:
     
       HTTP/1.1 200 Tamam Content-Type: uygulama/json; Charset = utf-8 İçerik-Uzunluk: 1234
     
       {"token_type": "Bearer", "expires_in": "3599", "expires_on": "1445395811", "not_before": "144 5391911","kaynak": "https://management.core.windows.net/", "access_token": {ACCESS_TOKEN}}
     
     Bu örnek hello POST parametrelerinin URL kodlaması dahil `resource` değerdir gerçekten `https://management.core.windows.net/`. Tooalso URL kodlama dikkatli olun `{CLIENT_SECRET}` gibi özel karakterleri içerebilir.
     
     > [!NOTE]
     > Test etmek için bir HTTP istemci aracı gibi kullanabilirsiniz [Fiddler](http://www.telerik.com/fiddler) veya [Chrome Postman uzantısı](https://chrome.google.com/webstore/detail/postman/fhbjgbiflinjbdggehcddcbncdddomop) 
     > 
     > 
2. Artık her API çağrısı hello yetkilendirme istek üstbilgisi içerir:
   
        Authorization: Bearer {ACCESS_TOKEN}
   
    Döndürülen, 401 durum kodu onay hello yanıt gövdesi alırsanız, hello belirtecinin süresi size. Bu durumda, yeni belirteç alın.

## <a name="using-hello-apis"></a>Merhaba API kullanma
Geçerli bir belirteci sahip olduğunuza göre hazır toomake hello API çağrıları aynıdır.

1. Her API isteği toopass hello önceki bölümde edindiğiniz bir geçerli, süresi dolmamış belirteci gerekir.
2. Bazı parametreler tooplug hello isteği uygulamanızı tanımlayan URI gerekir. Merhaba isteğin URI hello aşağıdaki gibi görünür
   
        https://management.azure.com/subscriptions/{subscription-id}/resourcegroups/{resource-group-name}/
        providers/Microsoft.MobileEngagement/appcollections/{app-collection}/apps/{app-resource-name}/
   
    tooget hello parametreleri, uygulama adınız ve Pano'e tıklayın ve tüm hello aşağıdakilerle 3 parametre hello gibi bir sayfa görürsünüz.
   
   * **1** `{subscription-id}`
   * **2** `{app-collection}`
   * **3** `{app-resource-name}`
   * **4** bilgisayarınızı kaynak grubu adı toobe giderek **MobileEngagement** yeni bir tane oluşturduğunuz sürece. 
     
     ![Mobile Engagement API URI parametreleri][2]

> [!NOTE]
> <br/>
> 
> 1. Merhaba, bu gibi hello API kök adresi yoksay önceki API'leri.<br/>
> 2. Daha sonra Klasik Azure portalını kullanarak hello uygulama oluşturduysanız hello uygulama adından kendisini farklı toouse hello Uygulama kaynağı adı gerekir. Hello Azure Portal hello uygulama oluşturduysanız hello uygulama adının kendisi (Uygulama kaynağı adı ve hello yeni portalında oluşturulan uygulamalar için uygulama adı arasında hiçbir ayrım yoktur) kullanmanız gerekir.  
> 
> 

<!-- Images -->
[1]: ./media/mobile-engagement-api-authentication/azure-module.png
[2]: ./media/mobile-engagement-api-authentication/mobile-engagement-api-uri-params.png
[3]: ./media/mobile-engagement-api-authentication/ps-cmdlets.png
[4]: ./media/mobile-engagement-api-authentication/ad-app-creation.png



