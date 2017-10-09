---
title: Azure remoteapp'te Outlook aaaUsing | Microsoft Docs
description: "Bilgi nasıl tooconfigure ve Azure Remoteapp'te Outlook kullanma | Microsoft Azure"
services: remoteapp
documentationcenter: 
author: pavithir
manager: mbaldwin
ms.assetid: cb2a498f-9539-4522-a874-542114926a61
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 119d2629ac47bd8d20d617985a9b488068aa959f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="using-microsoft-outlook-in-azure-remoteapp"></a>Azure RemoteApp’te Microsoft Outlook kullanma
> [!IMPORTANT]
> Azure RemoteApp 31 Ağustos 2017’de kullanımdan kaldırılacaktır. Okuma hello [duyuru](https://go.microsoft.com/fwlink/?linkid=821148) Ayrıntılar için.
> 
> 

Azure RemoteApp Microsoft Outlook O365’i destekler. [Azure RemoteApp’te Office’in çalışması](remoteapp-officesubscription.md) hakkında daha fazla bilgi edinin. Azure RemoteApp’te kullanılırken Outlook için bazı önerilen ayarlar vardır.

## <a name="cached-mode"></a>Önbelleğe alınmış mod
Önbelleğe alınmış mod, Azure RemoteApp’te Outlook kullanırken önerilen bir yapılanmadır. Bir Outlook 2013 hesabı toouse yapılandırdığınızda, Önbelleğe Alınmış Exchange Modu, Outlook 2013 hello çevrimdışı adres defteri birlikte hello kullanıcının bilgisayarında bir çevrimdışı veri dosyasında (OST dosyası) depolanan hello kullanıcının Microsoft Exchange posta kutusu yerel bir kopyasından çalışır (OAB). Hello önbelleğe alınmış posta kutusu ve OAB hello O365 hizmeti düzenli aralıklarla güncelleştirilir. Daha fazla bilgi edinin [hello önbelleğe alınmış ve çevrimiçi mod arasındaki farklar](https://technet.microsoft.com/library/jj683103.aspx).

Merhaba kullanıcı seçebilirsiniz **Önbelleğe Alınmış Exchange Modu** veya **çevrimiçi moda** hesap kurulumu sırasında veya hello hesap ayarlarını değiştirerek. Bir mod ya da diğer hello hello Office Özelleştirme Aracı'nı (OCT) ya da Grup İlkesi kullanarak da dağıtabilirsiniz.  

[Adım adım önbelleğe alınmış modu etkinleştirme yönergeleri](https://technet.microsoft.com/library/c6f4cad9-c918-420e-bab3-8b49e1885034#proc)ni okuyun.

## <a name="search"></a>Arama
Azure RemoteApp’te Outlook arama özelliğini kullanmanın sınırlamaları vardır. Azure RemoteApp havuza alınmış sanal makineleri tooaccommodate kullanıcı oturumlarını kullanır. Arama dizini oluşturma farklı VM'ler için farklı hello makine Kimliğine bağlıdır. Bir kullanıcı Azure Remoteapp'te oturum açtığı her sefer olmalarını yönlendirilmiş tooa mümkündür yeni VM. Bu, yerel aramayı etkinleştirdiğimizde, (Merhaba kullanıcı farklı sanal olduğunda) hello makine kimliği her değiştiğinde hello dizin oluşturucunun çalışacağı anlamına gelir. Merhaba Hello boyutuna bağlı olarak. OST dosyası hello dizin oluşturucu uzun süre toocomplete alın ve diğer uygulamalar için gereken kaynakları kullanmak. Arama yavaş olacağı gibi sonuç da vermeyebilir. Bir çevrimiçi moda hesap profili kullanılarak çalışması bu sorunu, ancak genel performansı yerel önbelleği toohello eksikliği yaşar (Merhaba önbelleğe alınmış ve çevrimiçi mod arasındaki fark hakkında daha fazla bilgi için yukarıda bağlantı hello bakın). Ne yazık ki, Outlook 2013’te dizinli/yerel arama devre dışı bırakılamaz ve çevrimiçi arama varsayılan olarak etkinleştirilmez.

