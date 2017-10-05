---
title: "RemoteApp karma koleksiyonu oluşturma sorunlarını giderme | Microsoft Docs"
description: "RemoteApp karma koleksiyonu oluşturma hatalarını giderme öğrenin"
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
ms.openlocfilehash: a486dcb3f994cd78311ee86521a6792a4d57438e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshoot-creating-azure-remoteapp-hybrid-collections"></a>Azure RemoteApp karma koleksiyonları oluşturma sorunlarını giderme
> [!IMPORTANT]
> Azure RemoteApp 31 Ağustos 2017’de kullanımdan kaldırılacaktır. Ayrıntılı bilgi için [duyuruyu](https://go.microsoft.com/fwlink/?linkid=821148) okuyun.
> 
> 

Karma koleksiyon, içinde barındırılan ve Azure bulut ancak de olanak tanır kullanıcıların access veri ve yerel ağınızda depolanan kaynakları verileri depolar. Kullanıcılar, Azure Active Directory ile eşitlenen ya da federasyonla yönetilen kurumsal kimlik bilgilerini kullanarak uygulamalara erişebilir. Mevcut bir Azure sanal ağı kullanan bir karma koleksiyon dağıtabilir veya yeni bir sanal ağ oluşturabilirsiniz. Oluşturma veya bir sanal ağ alt beklenen gelişmeye Azure RemoteApp için bir CIDR aralığı büyüklükte kullanılmasını öneririz.

Koleksiyonunuz henüz oluşturmadınız? Bkz: [karma koleksiyon oluşturma](remoteapp-create-hybrid-deployment.md) adımlar için.

Koleksiyonunuzu oluşturma sorunu yaşıyor veya koleksiyon biçimini çalışmıyorsa gerektiği düşünün, aşağıdaki bilgileri denetleyin.

## <a name="your-image-is-invalid"></a>Görüntünüzü geçersiz
Koleksiyonunuz sağlamak Azure için beklenirken "GoldImageInvalid" gibi bir ileti görürseniz, şablon görüntünüzü karşılamıyor demektir [görüntü gereksinimleri tanımlanan](remoteapp-imagereqs.md). Bu nedenle, bu okuma Git [gereksinimleri](remoteapp-imagereqs.md)görüntünüzü düzeltin ve koleksiyonunuzu yeniden oluşturmayı deneyin.

## <a name="does-your-vnet-have-network-security-groups-defined"></a>Sanal ağınızı tanımlanan ağ güvenlik grupları var mı?
Koleksiyonunuz için kullandığınız alt ağdaki tanımlanan ağ güvenlik grupları varsa, bunlar emin olun [URL'lerin ve bağlantı noktalarının](remoteapp-ports.md) , alt ağ içinde erişilebilir.

Sizin tarafınızdan daha sıkı bir denetim için alt ağda dağıtılan VM'ler için ek ağ güvenlik gruplarını ekleyin.

## <a name="are-you-using-your-own-dns-servers-and-are-they-accessible-from-your-vnet-subnet"></a>Kendi DNS sunucularınızı kullanıyor musunuz? Ve sanal alt ağdan erişilebilir?
> [!NOTE]
> VNET içinde barındırılan sanal makineleri çözümlemek her zaman kullanabilirsiniz ve sanal ağınızın DNS sunucularının her zaman çalıştığından emin olmak zorunda. Google DNS bu için kullanmayın.
> 
> 

Karma koleksiyonlar için kendi DNS sunucularınızı kullanın. Sanal ağınızı oluştururken bunları ağ yapılandırma Şeması veya Yönetim Portalı aracılığıyla belirtin. DNS sunucuları (aksine, hepsini bir kez) bir yük devretme şekilde belirtildikleri sırada kullanılır.  
Lütfen [VM'ler ve rol örnekleri için ad çözümlemesi](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md) DNS sunucunuzun emin olmak için yapılandırılmış correcly sunucularıdır.

DNS sunucuları koleksiyonunuz için erişilebilir olduğundan ve bu koleksiyon için belirtilen sanal alt ağdan kullanılabilir emin olun.

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
Yalnızca şu anda bir Active Directory etki alanı Azure RemoteApp ile ilişkili olabilir. Karma koleksiyon DirSync aracıyla bir Windows Server Active Directory dağıtımdan eşitlenmiş Azure Active Directory hesaplarını destekler; Özellikle, parola eşitleme seçeneği ile eşitlenen ya da yapılandırılan Active Directory Federasyon Hizmetleri (AD FS) Federasyonuyla eşitlenir. Şirket içi etki alanınız için UPN etki alanı sonekiyle özel bir etki alanı oluşturabilir ve dizin tümleştirmesini ayarladıktan gerekir.

Bkz: [Azure RemoteApp için Active Directory yapılandırma](remoteapp-ad.md) daha fazla bilgi için.

Sağlanan etki alanı ayrıntıları geçerli olduğunu ve Azure RemoteApp için kullanılan alt ağda oluşturulan VM etki alanı denetleyicisi erişilebildiğinden emin olun. Ayrıca sağlanan hizmet hesabı kimlik bilgileri sağlanan etki alanına bilgisayar eklemek için izinlere sahip ve girilen AD adı sanal ağ içinde sağlanan DNS'den çözümlenebildiğinden emin olun.

## <a name="what-domain-name-did-you-specify-when-you-created-your-collection"></a>Koleksiyonunuz oluşturduğunuzda hangi etki alanı adı belirttiğiniz?
Oluşturulan ya da eklenen etki alanı adını bir iç etki alanı adı (, Azure AD etki alanı adı değil) olması ve çözümlenebilir DNS biçiminde (contoso.local) olması gerekir. Örneğin, bir Active Directory iç adı (contoso.local) ve Active Directory UPN (contoso.com) sahip - koleksiyonunuzu oluşturduğunuzda, iç adı kullanmak zorunda.

