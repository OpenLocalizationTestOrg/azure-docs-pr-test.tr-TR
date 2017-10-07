---
title: "kiracılar - Azure kısıtlayarak aaaManage erişim toocloud uygulamalar | Microsoft Docs"
description: "Nasıl toouse Kiracı kısıtlamaları toomanage uygulamaları erişebilen kullanıcıları kendi Azure AD kiracısı temel."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: kgremban
ms.openlocfilehash: 6470fa217738b29104353ae17a2f53216f825c19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-tenant-restrictions-toomanage-access-toosaas-cloud-applications"></a>Kiracı kısıtlamaları toomanage erişim tooSaaS bulut uygulamaları kullanın

Office 365 gibi toomove toocloud hizmetlerine güvenlik vurgulamak büyük kuruluşlar istiyor ancak, kullanıcılar yalnızca erişebilir gerek tooknow kaynakları onaylandı. Geleneksel olarak, toomanage erişim istediğinizde şirket etki alanı adlarını veya IP adreslerini kısıtlayın. Bu yaklaşım, paylaşılan etki alanı adları outlook.office.com ve login.microsoftonline.com gibi çalışan bir genel bulutta SaaS uygulamaları barındırıldığı dünyada başarısız olur. Bu adresler engelleme kullanıcılar Outlook hello Web'de tamamen yalnızca bunları tooapproved kimlikleri ve kaynakları kısıtlama yerine erişmesini önlemek.

Azure Active Directory'nin çözüm toothis sınama Kiracı kısıtlamaları adlı bir özelliktir. Kiracı kısıtlamaları etkinleştirir kuruluşlar toocontrol erişim tooSaaS hello Azure AD Kiracı hello uygulamaları kullanmak için çoklu oturum açma dayalı uygulamalar, bulut. Örneğin, bu aynı uygulama erişim tooother kurumların örneklerinin önlerken tooallow erişim tooyour kuruluşunuzun Office 365 uygulamaları isteyebilirsiniz.  

Kiracı kısıtlamaları kuruluşlar hello özelliği toospecify hello kullanıcılarının tooaccess izin verilen Kiracı listesini sağlar. Ardından Azure AD erişim izin toothese kiracılar yalnızca verir.

Bu makalede, Office 365 için Kiracı kısıtlamalar odaklanır, ancak hello özelliği çoklu oturum açma için Azure AD ile modern kimlik doğrulama protokollerini kullanan herhangi bir SaaS bulut uygulama ile çalışması gerekir. Office 365 tarafından kullanılan hello kiracısındaki farklı bir Azure AD ile uygulamaları Kiracı SaaS kullanırsanız, gerekli tüm kiracılar izin verilen emin olun. SaaS bulut uygulamaları hakkında daha fazla bilgi için bkz: Merhaba [Active Directory Marketi](https://azure.microsoft.com/en-us/marketplace/active-directory/).

## <a name="how-it-works"></a>Nasıl çalışır?

Merhaba genel çözüm bileşenlerini aşağıdaki hello şunları kapsar: 

1. **Azure AD** – hello varsa `Restrict-Access-To-Tenants: <permitted tenant list>` kiracılar hello için sorunları güvenlik belirteçleri izin yalnızca mevcut, Azure AD değil. 

2. **Şirket içi proxy sunucu altyapısını** – SSL incelenmesi hello listesini içeren yapılandırılmış tooinsert hello üstbilgi yeteneğine sahip bir proxy aygıtını kiracılar için Azure AD giden trafiğe izin. 

3. **İstemci yazılımı** – toosupport Kiracı, istemci yazılımı gerekir istek kısıtlamaları belirteçleri doğrudan Azure AD'den böylece trafiği hello proxy altyapısı tarafından müdahale edilebilir. Kiracı kısıtlamaları şu anda desteklenen tarayıcı tabanlı Office 365 uygulamaları ve Office istemcileri tarafından modern kimlik doğrulaması (gibi OAuth 2.0) kullanıldığında. 

4. **Modern kimlik doğrulaması** – bulut Hizmetleri, modern kimlik doğrulaması toouse Kiracı kısıtlamaları kullanmalıdır ve tooall izin olmayan kiracılar erişimi engelleme. Office 365 bulut Hizmetleri, varsayılan olarak yapılandırılmış toouse modern kimlik doğrulama protokolleri olması gerekir. Merhaba son hakkında bilgi için Office 365 modern kimlik doğrulama desteği okuma [güncelleştirilmiş Office 365 modern kimlik doğrulaması](https://blogs.office.com/2015/11/19/updated-office-365-modern-authentication-public-preview/).

Aşağıdaki diyagramda hello hello üst düzey trafik akışı gösterilmektedir. SSL denetlemesi yalnızca trafik tooAzure AD, değil toohello Office 365 bulut Hizmetleri gereklidir. Bu ayrım Hello trafik hacmi kimlik doğrulama tooAzure AD için genellikle çok daha az trafik birim tooSaaS uygulamaları Exchange Online ve SharePoint Online gibi daha olduğundan önemlidir.

![Kısıtlamaları trafiği akışı Kiracı - diyagram](./media/active-directory-tenant-restrictions/traffic-flow.png)

## <a name="set-up-tenant-restrictions"></a>Kiracı sınırlamaları

Kiracı kısıtlamalarıyla başlatılan iki adımları tooget vardır. Merhaba ilk toomake istemcileriniz toohello doğru adresleri bağlanabildiğinden emin adımdır. Merhaba ikinci tooconfigure, proxy altyapısıdır.

### <a name="urls-and-ip-addresses"></a>URL'leri ve IP adresleri

toouse Kiracı kısıtlamaları, istemcilerinizin Azure AD URL'leri tooauthenticate aşağıdaki mümkün tooconnect toohello olmalıdır: login.microsoftonline.com, login.microsoft.com ve login.windows.net. Ayrıca, tooaccess Office 365, istemcilerinizi de mümkün tooconnect toohello FQDN'ler/URL'leri olmalıdır ve IP adreslerini tanımlanan [Office 365 URL'leri ve IP adresi aralıkları](https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2). 

### <a name="proxy-configuration-and-requirements"></a>Proxy yapılandırmasını ve gereksinimleri

yapılandırma aşağıdaki hello proxy altyapınızı aracılığıyla gerekli tooenable Kiracı kısıtlamaları ' dir. Bu kılavuz için belirli uygulama adımlarını tooyour proxy satıcısının belgelerine başvurmalısınız geneldir.

#### <a name="prerequisites"></a>Ön koşullar

- Hello proxy mümkün tooperform SSL kişiler tarafından ele, HTTP üstbilgisi ekleme ve FQDN'ler/URL'leri kullanarak filtre hedefleri olması gerekir. 

- İstemciler için SSL iletişimlerini hello proxy tarafından sunulan hello sertifika zinciri güvenmesi gerekir. Örneğin, bir iç PKI sertifikaları kullandıysanız, hello iç veren kök sertifika yetkilisi sertifikası güvenilir olması gerekir.

- Bu özellik, Office 365 abonelikleri dahil ancak Azure AD Premium 1 lisansları toouse Kiracı kısıtlamaları toocontrol erişim tooother SaaS uygulamaları istiyorsanız sonra gereklidir.

#### <a name="configuration"></a>Yapılandırma

Her gelen istek toologin.microsoftonline.com, login.microsoft.com ve login.windows.net için iki HTTP üstbilgileri ekleme: *kiracılar için sınırla erişim* ve *sınırla erişim bağlamı*.

Merhaba üstbilgi öğeleri aşağıdaki hello içermelidir: 
- İçin *kiracılar için sınırla erişim*, değerini \<Kiracı listesi izin\>, virgülle ayrılmış bir liste olduğu kiracılar tooallow kullanıcılar tooaccess istiyor. Bir kiracı ile kayıtlı herhangi bir etki alanı bu listede kullanılan tooidentify hello Kiracı olabilir. Örneğin, toopermit tooboth Contoso ve Fabrikam kiracıları erişmek için ad/değer çifti görülüyor hello:`Restrict-Access-To-Tenants: contoso.onmicrosoft.com,fabrikam.onmicrosoft.com` 
- İçin *sınırla erişim bağlam*, hangi Kiracı hello Kiracı kısıtlamalarını ayarlama bildiren bir tek bir dizin kimliği değeri. Örneğin, Contoso hello Kiracı kısıtlamaları İlkesi ayarlama hello Kiracı olarak toodeclare, başlangıç ad/değer çifti şuna benzer:`Restrict-Access-Context: 456ff232-35l2-5h23-b3b3-3236w0826f3d`  

> [!TIP]
> Dizin Kimliğinizi hello bulabilirsiniz [Azure portal](https://portal.azure.com). Bir yönetici olarak oturum açın, select **Azure Active Directory**seçeneğini belirleyip **özellikleri**.

zaten hello gelen istekte mevcut değilse tooprevent kullanıcıların onaylanmamış kiracılarla kendi HTTP üstbilgisi eklemek için tooreplace hello kiracılar için sınırla erişim üstbilgi hello proxy gerekir. 

İstemciler için tüm istekleri toologin.microsoftonline.com, login.microsoft.com ve login.windows.net zorlanmış toouse hello proxy olmalıdır. Örneğin, PAC dosyalar kullanılan toodirect istemcileri toouse hello proxy olduğunda, son kullanıcıların mümkün tooedit olması veya gerekir hello PAC dosyaları devre dışı bırakın.

## <a name="hello-user-experience"></a>Merhaba kullanıcı deneyimi

Bu bölümde, son kullanıcılar ve Yöneticiler için hello deneyimi gösterir.

### <a name="end-user-experience"></a>Son kullanıcı deneyimi

Bir örnek kullanıcı hello Contoso ağ üzerindeyse, ancak tooaccess hello Fabrikam paylaşılan SaaS uygulamasına Outlook gibi çevrimiçi örneği çalışıyor. Contoso Bu örnek için izin verilen olmayan bir kiracı yoksa, hello kullanıcı sayfası aşağıdaki hello görür:

![Sayfa kiracılar izin olmayan kullanıcılar için erişim reddedildi](./media/active-directory-tenant-restrictions/end-user-denied.png)

### <a name="admin-experience"></a>Yönetici deneyimi

Kiracı kısıtlamaları yapılandırmasını hello Kurumsal proxy altyapısında yapılır, ancak admins hello Kiracı kısıtlamaları hello Azure portalı raporlarında doğrudan erişebilirsiniz. tooview hello raporları, toohello Azure Active Directory genel bakış sayfasına gidin ve ardından 'Altında diğer Özellikler' arayın.

Hello Yöneticisi hello Kiracı için hello kısıtlı erişim bağlam Kiracı olarak belirtilen tüm oturum açma işlemleri nedeniyle hello kullanılan hello kimliği de dahil olmak üzere, Kiracı kısıtlamaları İlkesi engellendi. Bu rapor toosee kullanabilirsiniz ve hello hedef dizin kimliği

![Merhaba kısıtlanmış Azure portal tooview oturum açma girişimlerinin kullanın](./media/active-directory-tenant-restrictions/portal-report.png)

Diğer raporlarında gibi hello Azure portal, filtreleri toospecify hello raporunuzu kapsamını kullanabilirsiniz. Belirli bir kullanıcı, uygulama, istemci veya zaman aralığı üzerinde filtre uygulayabilirsiniz.

## <a name="office-365-support"></a>Office 365 desteği

Office 365 uygulamaları iki ölçütü toofully destek Kiracı kısıtlamaları karşılaması gerekir:

1. modern kimlik doğrulaması kullanılan hello istemci destekler
2. Modern kimlik doğrulaması hello hello bulut hizmeti için varsayılan kimlik doğrulama protokolü olarak etkinleştirilir.

Çok başvuran[güncelleştirilmiş Office 365 modern kimlik doğrulaması](https://blogs.office.com/2015/11/19/updated-office-365-modern-authentication-public-preview/) hello en son bilgileri hangi Office istemcileri şu anda modern kimlik doğrulamasını desteklemek için. Bu sayfa ayrıca modern kimlik doğrulamasını belirli Exchange Online ve Skype Kurumsal çevrimiçi kiracılar için etkinleştirme bağlantılar tooinstructions içerir. Modern kimlik doğrulaması zaten SharePoint Online'daki varsayılan olarak etkindir.

Kiracı kısıtlamaları şu an Office 365 tarayıcı tabanlı uygulamalar tarafından desteklenen (Merhaba Office portalı, Yammer, SharePoint siteleri, Outlook Web Merhaba, vb..). Kalın istemciler için (Outlook, Skype iş, Word, Excel, PowerPoint, vb.) Modern kimlik doğrulama kullanıldığında, Kiracı kısıtlamaları yalnızca zorunlu tutulabilir.  

Outlook ve Skype modern kimlik doğrulamasını destekleyen iş koruyabilmeyi toouse eski protokolleri kiracılar karşı burada modern kimlik doğrulaması etkinleştirilmediğinden istemcileridir için etkili bir şekilde Kiracı kısıtlamaları atlama. Windows için Outlook, müşteriler son kullanıcıların onaylanmamış posta hesaplarını tootheir profilleri ekleme önleme tooimplement kısıtlamaları seçebilirsiniz. Örneğin, hello bkz [varsayılan olmayan Exchange hesapları ekleme engelle](http://gpsearch.azurewebsites.net/default.aspx?ref=1) Grup İlkesi ayarı. Windows olmayan platformlarında Outlook ve Skype Kurumsal tüm platformlarda Kiracı kısıtlamaları için tam destek şu anda kullanılamıyor.

## <a name="testing"></a>Test Etme

Tüm kuruluşunuz için uygulamadan önce Kiracı kısıtlamaları çıkışı tootry isterseniz, iki seçenek vardır: Fiddler veya aşamalı bir sunum proxy ayarları gibi bir araç kullanarak ana bilgisayar tabanlı bir yaklaşım.

### <a name="fiddler-for-a-host-based-approach"></a>Ana bilgisayar tabanlı bir yaklaşım için fiddler

Fiddler kullanılan toocapture ve HTTP üstbilgileri ekleme de dahil olmak üzere HTTP/HTTPS trafiğini değiştirme proxy hata ayıklama ücretsiz bir web uygulamasıdır. tooconfigure Fiddler tootest Kiracı kısıtlamaları hello aşağıdaki adımları gerçekleştirin:

1.  [Fiddler'ı yükleyip](http://www.telerik.com/fiddler).
2.  Fiddler toodecrypt HTTPS trafiği başına yapılandırma [Fiddler'ın Yardım belgelerine](http://docs.telerik.com/fiddler/Configure-Fiddler/Tasks/DecryptHTTPS).
3.  Fiddler tooinsert hello yapılandırma *kiracılar için sınırla erişim* ve *sınırla erişim bağlam* özel kuralları kullanarak üstbilgileri:
  1. Hello Hello Fiddler Web hata ayıklayıcısı Aracı'nda seçin **kuralları** menü ve select **özelleştirme kuralları...** tooopen hello CustomRules dosyası.
  2. Merhaba hello başında satırlardan hello eklemek *OnBeforeRequest* işlevi. Değiştir \<Kiracı etki alanı\> bir etki alanında kayıtlı ile Kiracı, örneğin, contoso.onmicrosoft.com. Değiştir \<dizin kimliği\> , kiracınıza ait Azure AD GUID tanımlayıcısı.

  ```
  if (oSession.HostnameIs("login.microsoftonline.com") || oSession.HostnameIs("login.microsoft.com") || oSession.HostnameIs("login.windows.net")){      oSession.oRequest["Restrict-Access-To-Tenants"] = "<tenant domain>";      oSession.oRequest["Restrict-Access-Context"] = "<directory ID>";}
  ```

  Birden çok kiracıya tooallow gerekiyorsa, bir virgülle tooseparate hello Kiracı adları kullanın. Örneğin:

  ```
  oSession.oRequest["Restrict-Access-To-Tenants"] = "contoso.onmicrosoft.com,fabrikam.onmicrosoft.com";
  ```

4. Merhaba CustomRules dosyasını kaydedip kapatın.

Fiddler'ı yapılandırdıktan sonra tarafından toohello giden trafiği yakalayabilir **dosya** menü ve seçerek **trafiği Yakala**.

### <a name="staged-rollout-of-proxy-settings"></a>Proxy ayarları aşamalı dağıtımı

Proxy altyapınızı yeteneklerini Hello bağlı olarak, mümkün toostage hello sunum ayarları tooyour kullanıcıların olabilir. Değerlendirme için birkaç üst düzey seçenekleri şunlardır:

1.  PAC dosyaları toopoint test kullanıcıları tooa test proxy altyapısını, normal kullanıcılara toouse hello üretim proxy altyapısını devam ederken kullanın.
2.  Bazı proxy sunucular farklı yapılandırmaları gruplarını kullanarak destekleyebilir.

Belirli Ayrıntılar için tooyour proxy sunucunuzun belgelerine bakın.

## <a name="next-steps"></a>Sonraki adımlar

- Hakkında bilgi edinin [güncelleştirilmiş Office 365 modern kimlik doğrulaması](https://blogs.office.com/2015/11/19/updated-office-365-modern-authentication-public-preview/)

- Gözden geçirme hello [Office 365 URL'leri ve IP adresi aralıkları](https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2)
