---
title: "Bulut Hizmetleri özel etki alanı adının aaaConfigure | Microsoft Docs"
description: "Bilgi nasıl tooexpose Azure uygulama ya da veri toohello Internet DNS ayarları yapılandırarak özel bir etki alanı üzerinde.  Bu örnekler hello Azure portalını kullanın."
services: cloud-services
documentationcenter: .net
author: Thraka
manager: timlt
editor: 
ms.assetid: 5783a246-a151-4fb1-b488-441bfb29ee44
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: adegeo
ms.openlocfilehash: a0f3186b6022fbc4570ef1ce4b921426842bde76
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-a-custom-domain-name-for-an-azure-cloud-service"></a>Bir Azure bulut hizmeti için bir özel etki alanı adı yapılandırma
> [!div class="op_single_selector"]
> * [Azure portal](cloud-services-custom-domain-name-portal.md)
> * [Klasik Azure Portalı](cloud-services-custom-domain-name.md)
> 
> 

Azure bulut hizmeti oluşturduğunuzda, tooa etki alanının alt atar **cloudapp.net**. Örneğin, bulut hizmetinizin "contoso" ise, kullanıcılarınızın olacak mümkün tooaccess uygulamanızda http://contoso.cloudapp.net gibi bir URL olabilir. Azure de bir sanal IP adresi atar.

Ancak, aynı zamanda uygulamanız kendi etki alanı adınızı gibi getirebilir **contoso.com**. Bu makalede açıklanır nasıl tooreserve veya Bulut hizmeti web rolleri için özel etki alanı adı yapılandırın.

CNAME ve A kayıtlarını nelerdir zaten biliyor musunuz? [Atlama hello açıklama geçmiş](#add-a-cname-record-for-your-custom-domain).

> [!NOTE]
> Bu görevde Hello yordamlar tooAzure bulut Hizmetleri geçerlidir. Uygulama hizmetleri için bkz: [bu](../app-service-web/web-sites-custom-domain-name.md). Depolama hesapları için bkz: [bu](../storage/blobs/storage-custom-domain-name.md).
> 
> 

<p/>

> [!TIP]
> Daha hızlı--yapmalarını hello yeni Azure kullanmak [izlenecek destekli](http://support.microsoft.com/kb/2990804)!  Özel etki alanı adı ve güvenliğini sağlama iletişim (SSL) ilişkilendirme Azure Cloud Services veya Azure Web siteleri bir ek kolaylaştırır.
> 
> 

## <a name="understand-cname-and-a-records"></a>CNAME ve A kayıtları anlama
CNAME (veya diğer ad kayıtları) ve bir kayıt hem tooassociate belirli bir sunucunun bir etki alanı adıyla izin ver (veya bu durumda, hizmet) ancak bunlar farklı şekilde çalışır. Aynı zamanda bir kayıt hangi toouse karar vermeden önce dikkate almanız gereken Azure bulut Hizmetleri ile kullanırken ayrıca bazı belirli noktalar vardır.

### <a name="cname-or-alias-record"></a>CNAME veya diğer ad kaydı
Bir CNAME kaydı eşleyen bir *belirli* etki alanı gibi **contoso.com** veya **www.contoso.com**, tooa kurallı etki alanı adı. Bu durumda, hello hello kurallı etki alanı adı olduğundan **[Uygulamam] .cloudapp .net** Azure etki alanı adını barındırılan uygulama. Bir kez oluşturduktan sonra hello CNAME hello için diğer ad oluşturur **[Uygulamam] .cloudapp .net**. Merhaba CNAME girişi toohello IP adresini çözümlenir, **[Uygulamam] .cloudapp .net** hello bulut hizmetinin başlangıç IP adresi değişirse, tootake herhangi bir eylem olmayan şekilde otomatik olarak, hizmet.

> [!NOTE]
> Bazı etki alanı kayıt yalnızca toomap alt etki alanları www.contoso.com ve contoso.com gibi kök adları değil gibi bir CNAME kaydı kullanırken sağlar. CNAME kayıtları hakkında daha fazla bilgi için şirketiniz tarafından sağlanan hello belgelerine bakın [CNAME kaydı Wikipedia girişinde hello](http://en.wikipedia.org/wiki/CNAME_record), veya hello [IETF etki alanı adları - uygulama ve belirtim](http://tools.ietf.org/html/rfc1035) Belge.
> 
> 

### <a name="a-record"></a>Bir kayıt
Bir *A* kaydı bir etki alanı gibi eşler **contoso.com** veya **www.contoso.com**, *veya bir joker karakter etki alanı* gibi  **\*. contoso.com**, tooan IP adresi. Azure bulut hizmeti Hello durumda hello hizmetinin sanal IP hello. Bir A kaydı bir CNAME kaydı üzerinden ana avantajı Hello gibi bir joker karakter kullanan bir giriş olduğunu nedenle \* **. contoso.com**, hangi işlemek birden çok alt etki alanı için istekleri gibi  **Mail.contoso.com**, **login.contoso.com**, veya **www.contso.com**.

> [!NOTE]
> Bir A kaydı eşlenen beri tooa statik IP adresi otomatik olarak bulut hizmetinizin değişiklikleri toohello IP adresi çözümlenemiyor. Başlangıç IP adresi, bulut hizmeti tarafından kullanılan tooan boş yuva (üretim veya hazırlama.) dağıtmak ilk kez hello ayrılır Merhaba dağıtım hello yuva için silerseniz, başlangıç IP adresi Azure tarafından yayınlanan ve tüm gelecekteki dağıtımlar toohello yuvası verilen yeni bir IP adresi.
> 
> Başlangıç IP adresi (üretim veya hazırlama) belirli dağıtım yuvasının rahat, hazırlama ve üretim dağıtımları veya varolan bir dağıtım yerinde yükseltme gerçekleştirme arasında takası zaman kalıcı. Bu eylemler gerçekleştirme hakkında daha fazla bilgi için bkz: [nasıl toomanage bulut hizmetlerini](cloud-services-how-to-manage.md).
> 
> 

## <a name="add-a-cname-record-for-your-custom-domain"></a>Özel etki alanınız için bir CNAME kaydı ekleyin
toocreate bir CNAME kaydı, kayıt şirketiniz tarafından sağlanan hello araçları kullanarak özel etki alanınız için hello DNS tablosunda yeni bir giriş eklemelisiniz. Her kayıt için bir CNAME kaydı belirtmenin benzer ancak biraz farklı bir yöntem olsa da, kavramlar hello hello aynı.

1. Bu yöntemleri toofind hello birini kullanın **. cloudapp.net** tooyour bulut hizmetine atanan etki alanı adı.
   
   * Oturum açma toohello [Azure portal], bulut hizmetinizi seçin, hello Ara **Essentials** bölümünde ve hello bulur **Site URL'si** girişi.
     
       ![Hızlı Bakış bölümüne Hello site URL'si gösterme][csurl]
     
       **VEYA**
   * Yükleme ve yapılandırma [Azure Powershell](/powershell/azure/overview), ve ardından kullanımı hello aşağıdaki komutu:
     
       ```powershell
       Get-AzureDeployment -ServiceName yourservicename | Select Url
       ```
     
     Merhaba etki alanı adı ya da yöntemi tarafından döndürülen hello URL'de bir CNAME kaydı oluştururken gerekir olarak kullanılan kaydedin.
2. Tooyour DNS kayıt şirketinizin sitesinde oturum ve DNS yönetme toohello sayfasına gidin. Bağlantıları arayın veya hello sitesinin alanları etiketli olarak **etki alanı adı**, **DNS**, veya **adı sunucu yönetimi**.
3. Şimdi burada seçin veya CNAME'ın girin bulun. Bir açılan yazın veya Gelişmiş Ayarları sayfası tooan Git tooselect hello kaydına sahip olabilir. Merhaba sözcükleri göz önünde bulundurmanız gerekenler **CNAME**, **diğer**, veya **alt etki alanları**.
4. Ayrıca hello etki alanı ya da alt etki alanı diğer adı Merhaba CNAME, gibi sağlamanız gereken **www** için diğer ad toocreate istiyorsanız **www.customdomain.com**. Hello kök etki alanı için bir diğer ad toocreate istiyorsanız, bunu hello listelenmeyebilir '**@**' kayıt şirketinizin DNS araçlarında simgesi.
5. Ardından, uygulamanızın bir kurallı ana bilgisayar adı sağlamalısınız **cloudapp.net** bu durumda etki alanı.

Örneğin, gelen tüm trafiği CNAME kaydını aşağıdaki hello iletir **www.contoso.com** çok**contoso.cloudapp.net**, dağıtılan uygulamanızın hello özel etki alanı adı:

| Diğer ad/ana bilgisayar adı/alt etki alanı | Kurallı etki alanı |
| --- | --- |
| www |contoso.cloudapp.NET |

> [!NOTE]
> Bir ziyaretçi, **www.contoso.com** iletme işlemi hello görünmez toothe son kullanıcı olacak şekilde hello gerçek ana bilgisayar (contoso.cloudapp.net) hiçbir zaman görürsünüz.
> 
> Merhaba yukarıdaki örnekte yalnızca hello adresindeki tootraffic geçerlidir **www** alt etki alanı. Sahip CNAME kayıtlarına joker karakterler kullanılamaz olduğundan, her etki alanı/alt etki alanı için bir CNAME oluşturmanız gerekir. Alt etki alanları, toodirect trafiğinden gibi istiyorsanız *. contoso.com, tooyour cloudapp.net adres, yapılandırabileceğiniz bir **yeniden yönlendirme URL'si** veya **İleri URL** DNS ayarlarınız giriş veya bir A kaydını oluşturun.
> 
> 

## <a name="add-an-a-record-for-your-custom-domain"></a>Özel etki alanınız için bir A kaydı ekleme
toocreate bir A kaydı hello sanal IP adresi bulut hizmetinizin ilk bulmanız gerekir. Ardından yeni bir giriş hello özel etki alanınız için DNS tablosunda kayıt şirketiniz tarafından sağlanan hello araçları kullanarak ekleyin. Her kayıt için bir A kaydı belirtmenin benzer ancak biraz farklı bir yöntem olsa da, kavramlar hello hello aynı.

1. Yöntemleri tooget hello IP adresini bulut hizmetinizin izleyen hello birini kullanın.
   
   * Oturum açma toohello [Azure portal], bulut hizmetinizi seçin, hello Ara **Essentials** bölümünde ve hello bulur **ortak IP adresleri** girişi.
     
       ![Hızlı Bakış bölümüne Hello VIP gösterme][vip]
     
       **VEYA**
   * Yükleme ve yapılandırma [Azure Powershell](/powershell/azure/overview), ve ardından kullanımı hello aşağıdaki komutu:
     
       ```powershell
       get-azurevm -servicename yourservicename | get-azureendpoint -VM {$_.VM} | select Vip
       ```
     
     Başlangıç IP adresi, bir A kaydı oluştururken gerekir olarak kaydedin.
2. Tooyour DNS kayıt şirketinizin sitesinde oturum ve DNS yönetme toohello sayfasına gidin. Bağlantıları arayın veya hello sitesinin alanları etiketli olarak **etki alanı adı**, **DNS**, veya **adı sunucu yönetimi**.
3. Şimdi burada seçin veya bir kaydın girin bulun. Bir açılan yazın veya Gelişmiş Ayarları sayfası tooan Git tooselect hello kaydına sahip olabilir.
4. Merhaba etki alanı ya da bu A kaydı kullanacağı alt etki alanı girin veya seçin. Örneğin, seçin **www** için diğer ad toocreate istiyorsanız **www.customdomain.com**. Tüm alt etki alanlarını toocreate bir joker karakter girişi istiyorsanız, ' ***'. Bu gibi tüm alt etki alanlarını kapsar **mail.customdomain.com**, **login.customdomain.com**, ve **www.customdomain.com**.
   
    Merhaba kök etki alanı toocreate bir A kaydını istiyorsanız, bunu hello listelenmeyebilir '**@**' kayıt şirketinizin DNS araçlarında simgesi.
5. Bulut Hizmetinizin başlangıç IP adresi alanı sağlanan hello girin. Bu, bulut hizmeti dağıtımınızın hello IP adresiyle hello A kaydında kullanılan hello etki alanı girdisi ilişkilendirir.

Örneğin, bir kaydı takip hello gelen tüm trafiği iletir **contoso.com** çok**137.135.70.239**, hello dağıtılan uygulamanızın IP adresi:

| Ana bilgisayar adı/alt etki alanı | IP adresi |
| --- | --- |
| @ |137.135.70.239 |

Bu örnek, bir A kaydı hello kök etki alanı oluşturmayı gösterir. Joker karakter girişi toocover toocreate isterseniz, tüm alt etki alanları, girersiniz ' ***' hello alt etki alanı olarak.

> [!WARNING]
> Azure'daki IP adresleri, varsayılan olarak dinamik. Büyük olasılıkla toouse isteyeceksiniz bir [ayrılmış IP adresi](../virtual-network/virtual-networks-reserved-public-ip.md) IP adresiniz değişmeyen tooensure.
> 
> 

## <a name="next-steps"></a>Sonraki adımlar
* [TooManage Cloud Services nasıl](cloud-services-how-to-manage.md)
* [Nasıl tooMap CDN içerik tooa özel etki alanı](../cdn/cdn-map-content-to-custom-domain.md)
* [Genel yapılandırma bulut hizmetinizin](cloud-services-how-to-configure-portal.md).
* Nasıl çok öğrenin[bir bulut hizmetinin dağıtılacağı](cloud-services-how-to-create-deploy-portal.md).
* Yapılandırma [ssl sertifikalarını](cloud-services-configure-ssl-certificate-portal.md).

[Expose Your Application on a Custom Domain]: #access-app
[Add a CNAME Record for Your Custom Domain]: #add-cname
[Expose Your Data on a Custom Domain]: #access-data
[VIP swaps]: cloud-services-how-to-manage-portal.md#how-to-swap-deployments-to-promote-a-staged-deployment-to-production
[Create a CNAME record that associates hello subdomain with hello storage account]: #create-cname
[Azure portal]: https://portal.azure.com
[vip]: ./media/cloud-services-custom-domain-name-portal/csvip.png
[csurl]: ./media/cloud-services-custom-domain-name-portal/csurl.png
