---
title: Azure RemoteApp tooCitrix XenApp Essentials gelen aaaMigrate | Microsoft Docs
description: "Nasıl toomigrate Azure RemoteApp tooCitrix XenApp Essentials gelen"
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 695a8165-3454-4855-8e21-f2eb2c61201b
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: aa3ce28bc5a86d5b1dd3408196d51935395f55c1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-from-azure-remoteapp-toocitrix-xenapp-essentials"></a>Azure RemoteApp tooCitrix XenApp Essentials ' geçiş

Azure RemoteApp kullanın ve toomigrate tooCitrix XenApp Essentials istiyorsanız göz önünde birkaç Önkoşullar tookeep vardır. İlk olarak, Citrix'ın okuma [Citrix XenApp Essentials için adım adım Teknik Dağıtım Kılavuzu](https://docs.citrix.com/content/dam/docs/en-us/citrix-cloud/downloads/xenapp-essentials-deployment-guide.pdf) ve kendi [çevrimiçi Teknik Kitaplığı](http://docs.citrix.com/en-us/citrix-cloud/xenapp-and-xendesktop-service/xenapp-essentials.html). 

## <a name="prerequisite-steps-for-migration"></a>Geçiş için önkoşul adımları

1. Yeni bir sanal ağ oluşturun veya hangi Azure sanal ağı Azure kaynağı Citrix XenApp Essentials dağıtacağınıza Yöneticisi'nde belirleyin. Azure RemoteApp hello Klasik Azure portalı kullanır; Citrix XenApp Essentials yalnızca Azure Kaynak Yöneticisi'ni destekler.  
2. Citrix yalnızca karma dağıtımlarda desteklediğinden seçtiğiniz bu hello sanal ağ erişimi tooyour etki alanı denetleyicisi, ağ iletişimi olduğundan emin olun. Azure RemoteApp bulut dağıtımını kullanıyorsanız, sanal ağınızı erişim tooan Active Directory etki alanı denetleyicisi ağ olduğundan emin olun. Azure Active Directory etki alanı Hizmetleri (Azure AD DS) de kullanabilirsiniz. 
3. Bu hello bu etki alanına katılma, ilk denemede başarılı olması için DNS hello sanal ağ için doğru yapılandırılmış olduğundan emin olun. Seçtiğiniz hello sanal ağında bir sanal makine (VM) oluşturun ve o hello DNS el ile etki alanı katılma tooverify gerçekleştirmek ve etki alanına katılma beklendiği gibi çalışır. Bunun yapılması, Citrix XenApp Essentials dağıttığınız ilk kez başarılı hello olmasını sağlar. 
4. Gerekirse, Azure RemoteApp ile kullanmakta olduğunuz Azure Klasik portalı sanal ağı ve Azure Resource Manager sanal ağınız arasında eşleme sanal ağ oluşturun. Bu eşleme işlemi Hello iki ağlar aynı hello bulunuyorsa çalışır bölgesi. Yapmazsanız, siteden siteye VPN tooconnect hello Sanal Ağları için ağ kullanın. 
5. Gerekli olursa, okuma [nasıl toomigrate veri içine ve dışına Azure RemoteApp](remoteapp-migrate.md). 
6. Güncelleştirme, var olan Azure RemoteApp görüntüsü tooinclude hello Citrix VDA bileşeni (yönergeler için hello Citrix belgelere bakın). 
7. Toohello Azure Marketi gidin ve Citrix XenApp Essentials dağıtım başlayın.

## <a name="other-considerations"></a>Diğer konular

Ek hususlar geçirdiğinizde aşağıdaki Merhaba dikkat edin:
- Citrix XenApp Essentials yalnızca karma dağıtımları destekler. Diğer bir deyişle, sipariş tooperform etki alanına katılma alanındaki ağ erişim tooa etki alanı denetleyicisi gerektirir. Azure RemoteApp bulut dağıtımını kullanıyorsanız, Azure AD DS kullanabilir veya sanal ağınızı etki alanına katılma için erişim tooActive dizine sahip olduğundan emin olun. 
- toomove kullanıcı veri tooCitrix XenApp Essentials nasıl görürüm toolearn [nasıl toomigrate veri içine ve dışına Azure RemoteApp](remoteapp-migrate.md). 
- Citrix XenApp Essentials yalnızca Active Directory hesaplarını destekler. Microsoft hesapları (örneğin, outlook.com, msn.com veya hotmail.com) desteklemez. 

## <a name="citrix-xenapp-essentials-billing"></a>Citrix XenApp Essentials faturalama

Merhaba fiyatlandırma ile ilgili tam Ayrıntılar için bkz: [SSS](https://www.citrix.com/global-partners/microsoft/resources/xenapp-essentials-faq.html#tab-30699) ve [Citrix genel bakış makalesi](https://www.citrix.com/global-partners/microsoft/remote-app.html). TooCitrix XenApp Essentials üç fatura bileşenleri şunlardır:

- Merhaba Citrix hizmet 12 aylık kullanıcı başına olan ücretsiz olarak. Tüm Azure Market satın alımları gibi Azure aboneliğinizle ilişkili Faturalanan toohello ödeme yöntemi budur. Kurumsal Anlaşma (Kurumsal Sözleşme) müşteriler için Azure para kredisi kullanılamaz. 
- Uzak Veri Hizmetleri (RDS) istemci erişim lisansları (CAL). Şu anda hello getirilme uzaktan erişim ücret hello Citrix XenApp Essentials ödeme ile 6,25 için satın alabilirsiniz. Bir EA müşterisiyseniz, bu Azure para kredisi toopay kullanabilirsiniz. Varolan RDS CAL'leri toouse istiyorsanız adresinden bize başvurun [ arainfo@microsoft.com ](mailto:arainfo@microsoft.com), biz bu tooyour fatura uygulayabilirsiniz. 
- Azure işlem ve depolama. Bu hello Azure depolama maliyeti ve işlem tüketim hello VM'ler için tüketilen. VM boyutu ve kullanıcı yoğunluğu seçerken fiyatlandırma dikkat edin. Bir EA müşterisiyseniz, bu Azure para kredisi toopay kullanabilirsiniz.

Hala sorularınız varsa, şunları yapabilirsiniz:
- Adresinden bize e-posta [ arainfo@microsoft.com ](mailto:arainfo@microsoft.com).
- [Azure desteğine başvurun](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade). Tarafından Başlat [Azure destek talebi açarak](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) toohelp önkoşul ile adımları 1-5. Adım 6-7, Citrix hello Citrix Yönetim Portalı içinde bir destek bileti açılarak başvurun. 
