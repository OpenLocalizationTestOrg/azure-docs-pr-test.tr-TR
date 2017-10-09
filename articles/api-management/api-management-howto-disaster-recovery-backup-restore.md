---
title: "aaaImplement olağanüstü durum kurtarma'yı kullanarak yedekleme ve geri yükleme Azure API Management'te | Microsoft Docs"
description: "Bilgi nasıl toouse yedekleme ve geri yükleme Azure API Management'te tooperform olağanüstü durum kurtarma."
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 6f10be3c-f796-4a6c-bacd-7931b6aa82af
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: 058bfb579e3a3f51fb1dac8ea37eb4fdbc83a4ad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooimplement-disaster-recovery-using-service-backup-and-restore-in-azure-api-management"></a>Nasıl tooimplement olağanüstü durum kurtarma'yı kullanarak ve yedekleme hizmeti Azure API Management'te geri yükleme
Göre toopublish seçme ve Apı'lerinizi uygulamak ve yönetmek toodesign, aksi takdirde olması gereken çok sayıda hataya dayanıklılık ve altyapı özelliklerinden yapmakta Azure API Yönetimi yoluyla yönetin. Hello Azure platformu hello maliyet bir kısmı olası hatalar büyük kesir azaltır.

API Management hizmetiniz olduğu hello bölge etkileyen kullanılabilirlik sorunlardaki toorecover barındırılan hazır tooreconstitute herhangi bir zamanda hizmetiniz farklı bir bölgede olmalıdır. Kullanılabilirlik hedefleriniz ve kurtarma süresi hedefi bağlı olarak tooreserve yedekleme hizmeti bir veya daha fazla bölgelerde istediğiniz ve kendi yapılandırma ve içerik hello etkin hizmeti ile eşitlenmiş toomaintain deneyin. Merhaba hizmeti yedekleme ve geri yükleme özelliği, olağanüstü durum kurtarma stratejiniz uygulamak üzere hello gerekli yapı taşı sağlar.

Bu kılavuz, Azure Resource Manager tooauthenticate istekleri nasıl ve nasıl gösterir toobackup ve API Management hizmeti örnekleri geri yükleyin.

> [!NOTE]
> Yedekleme ve olağanüstü durum kurtarma için bir API Management hizmet örneği geri yükleme için hello işlemi de API Management hizmeti örnekleri hazırlama gibi senaryolar için çoğaltmak için kullanılabilir.
>
> Her yedekleme 30 gün sonra süresi dolar unutmayın. Merhaba 30 günlük süre sona erdiğinde toorestore bir yedekleme çalışırsanız hello geri yükleme başarısız bir `Cannot restore: backup expired` ileti.
>
>

## <a name="authenticating-azure-resource-manager-requests"></a>Kimlik doğrulama Azure Resource Manager istekleri
> [!IMPORTANT]
> Merhaba yedekleme ve geri yükleme için REST API Azure Resource Manager kullanır ve API Management varlıklarınızı yönetmek için REST API'leri hello daha farklı kimlik doğrulama mekanizması vardır. Bu bölümdeki Hello adımları nasıl tooauthenticate Azure Resource Manager istekleri açıklanmaktadır. Daha fazla bilgi için bkz: [Azure Resource Manager kimlik doğrulama istekleri](http://msdn.microsoft.com/library/azure/dn790557.aspx).
>
>

Tüm kaynakları hello Azure Resource Manager kullanarak bunu hello görevleri Azure hello aşağıdaki adımları kullanarak Active Directory'e ile kimliğinin doğrulanması gerekir.

* Bir uygulama toohello Azure Active Directory Kiracı ekleyin.
* Eklediğiniz hello uygulama izinlerini ayarlayın.
* Merhaba belirteç isteklerini tooAzure Resource Manager kimlik doğrulaması için alın.

Merhaba ilk adımı toocreate bir Azure Active Directory uygulaması oluşturur. Merhaba günlüğüne [Klasik Azure portalı](http://manage.windowsazure.com/) API Management hizmetiniz içeren hello aboneliğinden örneği ve toohello gidin **uygulamaları** varsayılan Azure Active Directory sekmesi.

> [!NOTE]
> Hello Azure Active Directory varsayılan dizin görünür tooyour hesabı değilse, hello Azure aboneliği toogrant hello kişi hello Yöneticisi izinleri tooyour hesabı gerekiyor.

![Azure Active Directory uygulaması oluşturma][api-management-add-aad-application]

Tıklatın **Ekle**, **kuruluşumun geliştirmekte olduğu bir uygulama Ekle**ve seçin **yerel istemci uygulaması**. Açıklayıcı bir ad girin ve hello İleri okuna tıklayın. Yer tutucu URL girin `http://resources` hello için **yeniden yönlendirme URI'si**, gerekli bir alandır ancak hello değer daha sonra kullanılmaz. Merhaba onay kutusunu toosave hello uygulama'yı tıklatın.

Merhaba uygulama kaydedildikten sonra tıklatın **yapılandırma**, toohello aşağı kaydırın **izinleri tooother uygulamaları** bölüm ve'ı tıklatın **uygulama eklemek**.

![İzinleri ekleme][api-management-aad-permissions-add]

Seçin **Windows** **Azure Hizmet Yönetimi API'si** ve hello onay kutusunu tooadd hello uygulama'yı tıklatın.

![İzinleri ekleme][api-management-aad-permissions]

Tıklatın **izinlere temsilci** yeni eklenen hello yanında **Windows** **Azure Hizmet Yönetimi API'si** uygulama, hello kutuyu **erişim Azure Hizmet Yönetimi (Önizleme)**, tıklatıp **kaydetmek**.

![İzinleri ekleme][api-management-aad-delegated-permissions]

Önceki tooinvoking hello oluşturmak API'leri yedekleme hello ve geri yüklemek, gerekli tooget bir belirteç değildir. Merhaba aşağıdaki örnek kullanır hello [Microsoft.IdentityModel.Clients.activedirectory tarafından](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory) nuget paketi tooretrieve hello belirteci.

```c#
using Microsoft.IdentityModel.Clients.ActiveDirectory;
using System;

namespace GetTokenResourceManagerRequests
{
    class Program
    {
        static void Main(string[] args)
        {
            var authenticationContext = new AuthenticationContext("https://login.microsoftonline.com/{tenant id}");
            var result = authenticationContext.AcquireToken("https://management.azure.com/", {application id}, new Uri({redirect uri});

            if (result == null) {
                throw new InvalidOperationException("Failed tooobtain hello JWT token");
            }

            Console.WriteLine(result.AccessToken);

            Console.ReadLine();
        }
    }
}
```

Değiştir `{tentand id}`, `{application id}`, ve `{redirect uri}` yönergeleri izleyerek hello kullanarak.

Değiştir `{tenant id}` hello oluşturduğunuz Azure Active Directory Uygulama hello Kiracı kimliği. Tıklatarak hello kimliği erişebilirsiniz **uç noktaları görüntülemek**.

![Uç Noktalar][api-management-aad-default-directory]

![Uç Noktalar][api-management-endpoint]

Değiştir `{application id}` ve `{redirect uri}` hello kullanarak **istemci kimliği** ve hello URL hello **yeniden yönlendirme URI'ler** Azure Active Directory uygulamanızın bölümünden **Yapılandır**  sekmesi.

![Kaynaklar][api-management-aad-resources]

Hello değerleri belirlendikten sonra Merhaba kodu örneği aşağıdaki örneğine belirteci benzer bir toohello döndürmelidir.

![Belirteç][api-management-arm-token]

Arama hello yedekleme ve geri yükleme işlemleri hello aşağıdaki bölümlerde açıklanan önce hello yetkilendirme istek üstbilgisi REST çağrısı için ayarlayın.

```c#
request.Headers.Add(HttpRequestHeader.Authorization, "Bearer " + token);
```

## <a name="step1"></a>Bir API Management hizmeti yedekleyin
HTTP isteği izleyen bir API Management hizmet sorunu hello yukarı tooback:

`POST https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/backup?api-version={api-version}`

Burada:

* `subscriptionId`-toobackup çalıştığınız hello API Management hizmeti içeren hello abonelik kimliği
* `resourceGroupName`-'Api - varsayılan-{hizmeti-bölge}' hello biçiminde bir dize nerede `service-region` hello Azure bölgesi hello toobackup çalıştığınız API Management hizmeti barındırıldığı, örneğin tanımlar`North-Central-US`
* `serviceName`-Merhaba, bir yedeğini Merhaba, oluşturma sırasında belirtilen API Management hizmeti hello adı
* `api-version`-değiştirin`2014-02-14`

Merhaba isteği Hello gövdesinde hello hedef Azure depolama hesabı adı, erişim tuşu, blob kapsayıcı adı ve yedek adı belirtin:

```
'{  
    storageAccount : {storage account name for hello backup},  
    accessKey : {access key for hello account},  
    containerName : {backup container name},  
    backupName : {backup blob name}  
}'
```

Merhaba hello değerini ayarlamak `Content-Type` isteği üstbilgisi çok`application/json`.

Yedekleme birden çok dakika toocomplete sürebilir uzun süren bir işlemdir.  Merhaba istek başarılı oldu ve hello yedekleme işlemi başlatıldı, alırsınız bir `202 Accepted` yanıt durum koduyla bir `Location` üstbilgi.  Oluştur 'GET' hello toohello URL'de istekleri `Location` üstbilgi toofind hello hello işlemin durumunu çıkışı. Merhaba yedekleme işlemi devam ederken tooreceive '202 kabul' durum kodunu devam eder. Bir yanıt kodu, `200 OK` hello yedekleme işlemi başarılı şekilde tamamlandığını gösterir.

Lütfen yedekleme isteği yapılırken kısıtlamaları aşağıdaki hello unutmayın.

* **Kapsayıcı** hello istek gövdesinde belirtilen **bulunmalıdır**.
* Yedekleme, sürerken **herhangi bir hizmet yönetim işlemini çalışmamalısınız** SKU yükseltme veya indirgeme, etki alanı adı değişikliği gibi vb..
* Geri yükleme bir **yedekleme yalnızca 30 gün boyunca garanti** hello anda oluşturulduktan sonra.
* **Kullanım verileri** analytics raporları oluşturmak için kullanılan **eklenmedi** hello yedekleme. Kullanım [Azure API Management REST API] [ Azure API Management REST API] tooperiodically almak analytics raporları güvenli olarak saklamak için.
* Hizmet yedeklemeler gerçekleştirmek hello sıklığı, kurtarma noktası hedefi etkiler. Bu sizi düzenli yedeklemeler uygulama yanı sıra önemli yaptıktan sonra isteğe bağlı yedeklemeleri gerçekleştirmek bildirmek toominimize tooyour API Management hizmeti değiştirir.
* **Değişiklikleri** yapılmış toohello hizmet (örneğin API'leri, ilkeleri, Geliştirici Portalı Görünüm) yedekleme işlemi sırasında yapılandırmadır işleminde **hello yedeklemeye dahil değildir ve bu nedenle kaybolacak**.

## <a name="step2"></a>Bir API Management hizmeti geri yükleme
toorestore önceden oluşturulmuş bir yedekten bir API Management hizmeti, HTTP isteği aşağıdaki hello olun:

`POST https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/restore?api-version={api-version}`

Burada:

* `subscriptionId`-içine bir yedeği geri yüklediğiniz hello API Management hizmeti içeren hello abonelik kimliği
* `resourceGroupName`-'Api - varsayılan-{hizmeti-bölge}' hello biçiminde bir dize nerede `service-region` hello Azure bölgesi hello içine bir yedeği geri yüklediğiniz API Management hizmeti barındırıldığı, örneğin tanımlar`North-Central-US`
* `serviceName`-hello API uygulamasına geri yükleniyor hizmet Merhaba, oluşturma sırasında belirtilen yönetim hello adı
* `api-version`-değiştirin`2014-02-14`

Merhaba isteği Hello gövdesinde hello yedekleme dosyası konumu, yani Azure depolama hesabı adı, erişim tuşu, blob kapsayıcı adı ve yedek adı belirtin:

```
'{  
    storageAccount : {storage account name for hello backup},  
    accessKey : {access key for hello account},  
    containerName : {backup container name},  
    backupName : {backup blob name}  
}'
```

Merhaba hello değerini ayarlamak `Content-Type` isteği üstbilgisi çok`application/json`.

Geri yükleme too30 veya daha fazla dakika toocomplete sürebilir uzun süren bir işlemdir.  Merhaba istek başarılı oldu ve hello geri yükleme işlemi başlatıldı, alırsınız bir `202 Accepted` yanıt durum koduyla bir `Location` üstbilgi.  Oluştur 'GET' hello toohello URL'de istekleri `Location` üstbilgi toofind hello hello işlemin durumunu çıkışı. Merhaba geri yükleme işlemi devam ederken tooreceive '202 kabul edilen' durum kodunu devam eder. Bir yanıt kodu, `200 OK` hello geri yükleme işlemi başarılı şekilde tamamlandığını gösterir.

> [!IMPORTANT]
> **Merhaba SKU** hello hizmet uygulamasına geri yükleniyor **eşleşmelidir** hello hello SKU'su yedeklenen hizmetini geri yükleniyor.
>
> **Değişiklikleri** yapılmış toohello hizmet yapılandırmasını (örneğin API'leri, ilkeleri, Geliştirici Portalı Görünüm) geri yükleme işlemi sırasında ediyor **üzerine yazılabilir**.
>
>

## <a name="next-steps"></a>Sonraki adımlar
Microsoft bloglar hello yedekleme/geri yükleme işleminin iki farklı izlenecek yollar için aşağıdaki hello göz atın.

* [Azure API Management hesapları Çoğalt](https://www.returngis.net/en/2015/06/replicate-azure-api-management-accounts/)
  * TooGisela kendi katkı toothis makalesi için teşekkür ederiz.
* [Azure API Management: Yedekleme ve yapılandırmasını geri yükleme](http://blogs.msdn.com/b/stuartleeks/archive/2015/04/29/azure-api-management-backing-up-and-restoring-configuration.aspx)
  * ancak çok ilginç Stuart tarafından ayrıntılı hello yaklaşım hello resmi Kılavuzu eşleşmiyor.

[Backup an API Management service]: #step1
[Restore an API Management service]: #step2


[Azure API Management REST API]: http://msdn.microsoft.com/library/azure/dn781421.aspx

[api-management-add-aad-application]: ./media/api-management-howto-disaster-recovery-backup-restore/api-management-add-aad-application.png

[api-management-aad-permissions]: ./media/api-management-howto-disaster-recovery-backup-restore/api-management-aad-permissions.png
[api-management-aad-permissions-add]: ./media/api-management-howto-disaster-recovery-backup-restore/api-management-aad-permissions-add.png
[api-management-aad-delegated-permissions]: ./media/api-management-howto-disaster-recovery-backup-restore/api-management-aad-delegated-permissions.png
[api-management-aad-default-directory]: ./media/api-management-howto-disaster-recovery-backup-restore/api-management-aad-default-directory.png
[api-management-aad-resources]: ./media/api-management-howto-disaster-recovery-backup-restore/api-management-aad-resources.png
[api-management-arm-token]: ./media/api-management-howto-disaster-recovery-backup-restore/api-management-arm-token.png
[api-management-endpoint]: ./media/api-management-howto-disaster-recovery-backup-restore/api-management-endpoint.png
