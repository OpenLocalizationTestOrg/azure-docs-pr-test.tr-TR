---
title: "RemoteApp karma koleksiyonu oluşturma aaaTroubleshoot | Microsoft Docs"
description: "Bilgi nasıl tootroubleshoot RemoteApp karma koleksiyonu oluşturma hataları"
services: remoteapp
documentationcenter: 
author: vkbucha
manager: mbaldwin
ms.assetid: b32033ee-8d52-4e74-bb78-86ca873c34e2
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: mbaldwin
ms.openlocfilehash: cc426f24bd0c349a8862d54acbafa9cf84446f4a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-creating-azure-remoteapp-hybrid-collections"></a>Azure RemoteApp karma koleksiyonları oluşturma sorunlarını giderme
> [!IMPORTANT]
> Azure RemoteApp 31 Ağustos 2017’de kullanımdan kaldırılacaktır. Okuma hello [duyuru](https://go.microsoft.com/fwlink/?linkid=821148) Ayrıntılar için.
> 
> 

Karma koleksiyon, içinde barındırılan ve hello Azure bulut ancak de olanak tanır kullanıcıların access veri ve yerel ağınızda depolanan kaynakları verileri depolar. Kullanıcılar, Azure Active Directory ile eşitlenen ya da federasyonla yönetilen kurumsal kimlik bilgilerini kullanarak uygulamalara erişebilir. Mevcut bir Azure sanal ağı kullanan bir karma koleksiyon dağıtabilir veya yeni bir sanal ağ oluşturabilirsiniz. Oluşturma veya bir sanal ağ alt beklenen gelişmeye Azure RemoteApp için bir CIDR aralığı büyüklükte kullanılmasını öneririz.

Koleksiyonunuz henüz oluşturmadınız? Bkz: [karma koleksiyon oluşturma](remoteapp-create-hybrid-deployment.md) hello adımlar için.

Koleksiyonunuzu oluşturma sorunu yaşıyor veya hello koleksiyonu çalışmıyorsa düşündüğünüz hello şekilde gerektiğini bilgisinden hello kontrol edin.

## <a name="your-image-is-invalid"></a>Görüntünüzü geçersiz
Koleksiyonunuz için Azure tooprovision beklenirken "GoldImageInvalid" gibi bir ileti görürseniz, şablon görüntünüzü hello karşılamıyor demektir [görüntü gereksinimleri tanımlanan](remoteapp-imagereqs.md). Bu nedenle, bu okuma Git [gereksinimleri](remoteapp-imagereqs.md)görüntünüzü düzeltin ve toocreate koleksiyonunuzu yeniden deneyin.

## <a name="does-your-vnet-have-network-security-groups-defined"></a>Sanal ağınızı tanımlanan ağ güvenlik grupları var mı?
Koleksiyonunuz için kullandığınız hello alt ağdaki tanımlanan ağ güvenlik grupları varsa, bunlar emin olun [URL'lerin ve bağlantı noktalarının](remoteapp-ports.md) , alt ağ içinde erişilebilir.

Ek ağ güvenlik grupları toohello Vm'lerinde dağıtılan sizin tarafınızdan daha sıkı bir denetim için hello alt ekleyebilirsiniz.

## <a name="are-you-using-your-own-dns-servers-and-are-they-accessible-from-your-vnet-subnet"></a>Kendi DNS sunucularınızı kullanıyor musunuz? Ve sanal alt ağdan erişilebilir?
> [!NOTE]
> Sanal ağınızın DNS sunucularının her zaman çalışır durumda toomake emin hello ve hello VNET barındırılan her zaman mümkün tooresolve hello sanal makineler var. Google DNS bu için kullanmayın.
> 
> 

Karma koleksiyonlar için kendi DNS sunucularınızı kullanın. Sanal ağınızı oluştururken bunları ağ yapılandırma Şeması veya hello Yönetim Portalı aracılığıyla belirtin. DNS sunucuları, bir yük devretme şekilde (karşılıklı tooround deneme) belirtildikleri hello sırada kullanılır.  
Lütfen çok başvurun[VM'ler ve rol örnekleri için ad çözümlemesi](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md) toomake, DNS sunucularınızın yapılandırılmış correcly emin.

Koleksiyonunuz için Hello DNS sunucuları bu koleksiyon için belirtilen hello sanal ağ alt ağı üzerinden erişilebilir ve kullanılabilir olduğundan emin olun.

Örneğin:

    <VirtualNetworkConfiguration>
    <Dns>
      <DnsServers>
        <DnsServer name="" IPAddress=""/>
      </DnsServers>
    </Dns>
    </VirtualNetworkConfiguration>

![DNS sunucunuzun tanımlayın](./media/remoteapp-hybridtrouble/dnsvpn.png)

## <a name="are-you-using-an-active-directory-domain-controller-in-your-collection"></a>Bir Active Directory etki alanı denetleyicisi koleksiyonunuzda kullanıyor musunuz?
Yalnızca şu anda bir Active Directory etki alanı Azure RemoteApp ile ilişkili olabilir. Merhaba karma koleksiyon DirSync aracıyla bir Windows Server Active Directory dağıtımdan eşitlenmiş Azure Active Directory hesaplarını destekler; Özellikle, hello parola eşitleme seçeneği ile eşitlenen ya da yapılandırılan Active Directory Federasyon Hizmetleri (AD FS) Federasyonuyla eşitlenir. Dizin tümleştirmesini ayarladıktan ve toocreate hello UPN etki alanı sonekiyle'şirket içi etki alanınız için özel bir etki alanı gerekir.

Bkz: [Azure RemoteApp için Active Directory yapılandırma](remoteapp-ad.md) daha fazla bilgi için.

Sağlanan hello etki alanı ayrıntıları geçerli olduğundan ve VM Azure uzak uygulaması için kullanılan hello alt ağda oluşturulan hello hello etki alanı denetleyicisi erişilebildiğinden emin olun. Ayrıca hello hizmet hesabı etki alanı ve, sağlanan AD adı hello sağlanan kimlik bilgileri sağlandı izinleri tooadd bilgisayarlar toohello sahip hello hello VNET sağlanan DNS gelen çözümlenebildiğinden emin olun.

## <a name="what-domain-name-did-you-specify-when-you-created-your-collection"></a>Koleksiyonunuz oluşturduğunuzda hangi etki alanı adı belirttiğiniz?
oluşturulan ya da eklenen hello etki alanı adı bir iç etki alanı adı (, Azure AD etki alanı adı değil) olması ve çözümlenebilir DNS biçiminde (contoso.local) olması gerekir. Örneğin, bir Active Directory iç adı (contoso.local) varsa ve Active Directory UPN (contoso.com) - koleksiyonunuzu oluşturduğunuzda toouse hello iç adına sahip.

