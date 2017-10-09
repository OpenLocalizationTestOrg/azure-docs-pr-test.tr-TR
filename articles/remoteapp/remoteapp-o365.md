---
title: Azure RemoteApp ile Office aaaUsing | Microsoft Docs
description: "Office ve Azure RemoteApp birlikte nasıl çalıştığını öğrenin"
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: f1773baf-8aa1-423c-a2f9-e4679e0463d3
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: d065c1a0a2191c9e2e405264a835cecf791d6ab7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="using-office-with-azure-remoteapp"></a>Azure RemoteApp ile Office'i kullanma
> [!IMPORTANT]
> Azure RemoteApp 31 Ağustos 2017’de kullanımdan kaldırılacaktır. Okuma hello [duyuru](https://go.microsoft.com/fwlink/?linkid=821148) Ayrıntılar için.
> 
> 

Azure remoteapp'te Office uygulamalarını barındırmak için iki seçeneğiniz vardır: Office 365 ProPlus veya Office 2013 Professional Plus deneme.

**Hey, yeni, bu en kısa sürede değiştirecek makale daha iyi sahibiz biliyor muydunuz? Kullanıma [nasıl toouse Azure RemoteApp ile Office 365 aboneliğinize](remoteapp-officesubscription.md). Office 365 + Azure RemoteApp kullanarak gereksinim duyduğunuz tüm hello bilgilerini kapsar.**

## <a name="office-365-proplus"></a>Office 365 ProPlus
Merhaba Office 365 ProPlus şablon görüntüsü kullanarak bir RemoteApp koleksiyonunu oluşturabilirsiniz. Bu seçenek, tooextend sağlar, Office 365 hizmeti tooRemoteApp. Var olan bir abonelik planı olması ve kullanıcılarınızın hello Office 365 ProPlus hizmeti, tek başına veya hello Office 365 hizmet planları yoluyla lisansına sahip olması gerekir.

RemoteApp Office 365 paylaşılan bilgisayar etkinleştirmeyi destekler. Ne zaman, paylaşılan bilgisayar etkinleştirmesi ve hello kullan [Office dağıtım aracı](http://www.microsoft.com/download/details.aspx?id=36778) etkinleştirilmeden yükleme için Office 365 ProPlus yükler. Merhaba kullanıcı Office 365 ProPlus için sağlanmış bir kullanıcı işaretlerini girdiğinde Office 365 içeren bir koleksiyon, Office toosee denetler. Bu nedenle, Office geçici olarak Office 365 ProPlus - etkinleştirir, bu etkinleştirme, kullanıcılar işaretleri hello hizmet dışına kadar devam ettirir.

Office 365 paylaşılan bilgisayar etkinleştirme toouse, gereksinim duyduğunuz toocreate bir [özel şablon](remoteapp-create-custom-image.md) ve Office 365 ProPlus yükleme, aşağıdaki [şu yönergeleri](https://technet.microsoft.com/library/dn782858.aspx).

Merhaba, kullanıcılarınızın Office 365 lisans yönetebilirsiniz [Office 365 Yönetici portalı](https://portal.office365.com/). Hakkında daha fazla bilgi okuyun [Office 365 hizmet planları](http://technet.microsoft.com/library/office-365-plan-options.aspx).  

## <a name="office-2013-professional-plus-trial"></a>Office 2013 Professional Plus deneme
RemoteApp 30 günlük deneme sırasında hello Office 2013 Professional Plus (Deneme) şablonu görüntü toocreate RemoteApp koleksiyonu kullanabilirsiniz. Kullanıcıların toothis deneme koleksiyonu, Azure Active Directory iş hesaplarını veya Microsoft hesaplarını kullanarak atayabilirsiniz. Hiçbir ek abonelik gereklidir.

Bu harika seçeneği tookick hello özelliklerini ve RemoteApp Office için iyi bir duyguyu açığa alın. Ancak, bu seçenek yalnızca değerlendirme için tasarlanmıştır ve test edilir. RemoteApp koleksiyonları Hello Office 2013 Professional Plus (Deneme) şablon görüntüsü kullanılarak oluşturulan geçti tooproduction modu olamaz ve hello hello deneme süresinin sonunda devre dışı bırakılacak.

## <a name="switching-from-trial-tooproduction"></a>Deneme tooproduction geçiş yapma
30 günlük ücretsiz deneme sürümünüzü başlatın, hello hello portal RemoteApp bölümünü notta hesabına ödenen tootransition tooa ihtiyacınız önce ne kadar süreyle hello deneme bıraktığınız söyler. Bu notta hello bağlantıyı kullanarak, hesabı ve anahtarı tooproduction modunuzu etkinleştirebilirsiniz.

Hesabınızı etkinleştirdiğinizde, bu hesabınızın tüm hello RemoteApp koleksiyonları etkiler.

* Merhaba Windows Server 2012 R2 veya hello Office 365 ProPlus şablon görüntüleri çalıştıran koleksiyonları tooproduction sorunsuz olarak geçer. Tüm kullanıcı verilerini ve ayarları, devam eden oturumları dahil olmak üzere değişmeden kalır.
* Özel şablon görüntüleri karşıya yüklediyseniz, bu görüntüleri kullanarak koleksiyonları sorunsuz olarak geçer.
* Merhaba Office 2013 Professional Plus (Deneme) şablon görüntüsü yalnızca değerlendirme amacıyla tasarlanmıştır. Bu şablon görüntüsü ile çalışan koleksiyonları geçti tooproduction olamaz. Bunlar "disabled" durumuna sokar.

Deneme sürümünüzü hello sona erme tarafından tooproduction modu geçiş değil, RemoteApp koleksiyonlarınız devre dışı bırakılacak. Endişelenmeyin - hala hizmeti ve anahtar tooproduction modunuzu hiçbir veri kaybı olmadan etkinleştirebilirsiniz şekilde ayarlarınızı ve kullanıcıların veri için başka bir 90 gün kaydedilir.

