---
title: Azure RemoteApp aaaWhat mi? | Microsoft Belgeleri
description: "Bilgi nasıl tooshare uygulamalarına ve kaynaklarına tooany aygıtı Azure RemoteApp aracılığıyla."
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
editor: 
ms.assetid: d7a8a311-e70a-4463-ac85-c7f62c500921
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: e13909f3a5698f58c7e4348f3ce53f43560f9b1d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-azure-remoteapp"></a>Azure RemoteApp nedir?
> [!IMPORTANT]
> Azure RemoteApp 31 Ağustos 2017’de kullanımdan kaldırılacaktır. Okuma hello [duyuru](https://go.microsoft.com/fwlink/?linkid=821148) Ayrıntılar için.
> 
> 

Azure RemoteApp hello şirket içi Microsoft RemoteApp programı, tooAzure Uzak Masaüstü Hizmetleri tarafından desteklenen hello işlevselliğini getirir. Azure RemoteApp birçok farklı kullanıcı aygıtlardan tooapplications güvenli uzaktan erişim sağlamanıza yardımcı olur. Azure RemoteApp temelde hello bulutta kalıcı olmayan Terminal sunucusu oturumları barındırır ve toouse alma bunları ve kullanıcılarınızla paylaşabilirsiniz.

Azure RemoteApp ile neredeyse tüm cihazlardan kullanıcılarla uygulamaları ve kaynakları paylaşabilirsiniz. Merhaba bulut uygulamalarınızda hello donanımı ilgilenebilmek anlamına gelir ve toomeet kullanıcı taleplerini ölçeklendirme barındırır. Tüm toodo sahip olduğu tooshare istediğiniz ve ardından bu uygulamaları kullanıcıların toouse almak hello uygulamaları karşıya yükleme. [Kullanıcıların kendi cihazlarını tookeep almak](remoteapp-clients.md), her şeyi hello Azure portal aracılığıyla yönetirsiniz. Hatta, uygulamaları ve verileri hello güvenliğini sağlamaya izin vererek şirket kimlik bilgilerinizi kullanarak hello seçeneğiniz vardır.

Azure RemoteApp hakkında daha fazla bilgi için okumaya devam edin, veya zaten ikna olduysanız [şimdi deneyin](https://azure.microsoft.com/services/remoteapp/).

Azure RemoteApp hakkında sorularınız mı var? [SSS](remoteapp-faq.md)’lerimize göz atın.

Azure RemoteApp hello bir parçasıdır [Microsoft Sanal Masaüstü Altyapısı](http://www.microsoft.com/server-cloud/products/virtual-desktop-infrastructure/explore.aspx).

**Yeni!** Azure RemoteApp hakkında daha fazla toolearn istiyorsunuz? Veya toovalidate Azure RemoteApp ölçekte hazır? Haftalık katılma [hello uzmanlara sorun Web seminerimize](https://azureinfo.microsoft.com/AzureRemoteAppAskTheExperts-Registration-Page.html?ls=Website).

## <a name="azure-remoteapp-collections"></a>Azure RemoteApp koleksiyonları
İki tür [Azure RemoteApp koleksiyonu](remoteapp-collections.md) vardır:

* A **bulut koleksiyonu** barındırılır ve hello bulutta programlar için verileri depolar. Kullanıcılar, kendi Microsoft hesapları veya Azure Active Directory ile eşitlenen ya da federasyonla yönetilen kurumsal kimlik bilgilerini kullanarak uygulamalara erişebilir.
  
    Bulut koleksiyonu tooshare hello uygulamasıyla bir bağlantı tooany kaynağı gerekmediğinde, şirketinizin özel ağ (örneğin, bir VPN cihazı üzerinden) seçin. Merhaba uygulaması hello üzerinde Internet, OneDrive veya Azure'a kaynakları kullanıyorsa bulut koleksiyonu sizin için çalışır. Merhaba hızlı toocreate de olabilir.
* A **karma koleksiyon** barındırılır ve hello Azure bulut ancak de olanak tanır kullanıcıların access veri ve yerel ağınızda depolanan kaynakları verileri depolar. Kullanıcılar, Azure Active Directory ile eşitlenen ya da federasyonla yönetilen kurumsal kimlik bilgilerini kullanarak uygulamalara erişebilir.
  
    Şirketinizin özel ağındaki bağlantı tooresources gerekiyorsa karma koleksiyonu seçin. Örneğin, hello uygulama tooone hello aşağıdaki erişim:
  
  * İntranet üzerinde bulunan dosya sunucuları
  * Quicken
  * Bir güvenlik duvarının arkasındaki veritabanları
    
    Birçok kaynak olamaz kendi özel ağlardaki büyük şirketler toohello bulut taşınmış için genellikle daha kullanışlıdır.

Merhaba farklı koleksiyonlara ağlar da dahil farklı seçenekler vardır, bu nedenle [hangi koleksiyonu](remoteapp-collections.md) en iyi çalıştığını sizin için. 

### <a name="updating-your-collection"></a>Koleksiyonunuzu güncelleştirme
Merhaba karma ve bulut koleksiyonları arasındaki temel farklılıklar hello yazılım güncelleştirmelerinin işlenme biridir. Merhaba önceden yüklenmiş Office 365 ProPlus veya Office 2013 görüntüsünü kullanan bulut koleksiyonu ile tooworry herhangi bir güncelleştirme hakkında sahip değilsiniz. Merhaba hizmeti, kendi bakımını ve sürekli olarak, tooboth uygulamaları ve hello işletim sistemi güncelleştirmeleri yapar.

Karma koleksiyonlar, yanı sıra için bir özel şablon görüntüsü kullanan bulut koleksiyonlarında, hello görüntü ve uygulamaların güncelliğini sorumlu olan. Etki alanına katılmış görüntüler için Windows Update, Grup İlkesi veya System Center gibi araçları kullanarak güncelleştirmeleri denetleyebilirsiniz.

Özel şablon görüntünüzü güncelleştirdikten sonra hello yeni görüntü toohello Azure bulut karşıya yükleyin ve ardından hello koleksiyonu toouse hello yeni görüntüsü güncelleştirin. (Bunu Azure RemoteApp hello yapabilirsiniz **Hızlı Başlangıç** sayfası veya Pano hello.)

Daha fazla bilgi için bkz. [Koleksiyonunuzu güncelleştirme](remoteapp-update.md).

## <a name="supported-remoteapp-clients"></a>Desteklenen RemoteApp istemcileri
Azure RemoteApp, Mac, iOS ve Android için Windows ve Windows RT RemoteApp istemci uygulamaları hello yanı sıra üzerinde hello Microsoft Uzak Masaüstü uygulamalarında desteklenir. Kullanıcılarınız, bu uygulamaları kendi mobil Cihazınızda kullanın veya yeni Azure RemoteApp programları aygıtları tooaccess hello işlem.

Bkz: [Azure remoteapp'te uygulamalarınıza erişme](remoteapp-clients.md) hello istemcileri hakkında daha fazla bilgi için.

## <a name="next-steps"></a>Sonraki adımlar
Başlayın! Deneyin! Bu makaleler Azure RemoteApp kullanmaya başlamanıza yardımcı olur:

* [Azure RemoteApp için nasıl bir koleksiyona ihtiyacınız var?](remoteapp-collections.md)
* [Azure RemoteApp görüntüsü oluşturma](remoteapp-imageoptions.md)
* [Nasıl toocreate Azure RemoteApp bulut koleksiyonu](remoteapp-create-cloud-deployment.md)
* [Nasıl toocreate Azure RemoteApp karma koleksiyonu](remoteapp-create-hybrid-deployment.md)
* [Azure RemoteApp’te lisanslama nasıl çalışır?](remoteapp-licensing.md)
* [Azure RemoteApp’i kullanmak için en iyi uygulamalar](remoteapp-bestpractices.md)
* [Azure RemoteApp hakkında SSS](remoteapp-faq.md)

### <a name="help-us-help-you"></a>Yardımımıza katkıda bulunun
Toplama toorating bu makalede, aşağıda yorum yapmamanın, değişiklikleri toohello makalesi kendisini yapıp olduğunu biliyor muydunuz? Eksik bir şeyler mi var? Yanlış bir şeyler mi var? Kafa karıştırıcı bir şeyler mi yazdım? Yukarı doğru ilerleyin ve tıklatın **GitHub üzerinde Düzenle** veya **Düzenle** toomake değişiklikleri - olanlar gelen gözden geçirilmek üzere toous ve biz üzerlerinde edildikten sonra değişiklikleriniz ve iyileştirmeleriniz burada göreceğiniz.

