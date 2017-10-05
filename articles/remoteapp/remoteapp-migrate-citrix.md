---
title: "Azure RemoteApp için Citrix XenApp Essentials geçirme | Microsoft Docs"
description: "Azure RemoteApp için Citrix XenApp Essentials geçirme"
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
ms.openlocfilehash: fcd96a466d1c0dad17d7012308281ef868463b19
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="migrate-from-azure-remoteapp-to-citrix-xenapp-essentials"></a>Azure RemoteApp için Citrix XenApp Essentials geçirme

Azure RemoteApp kullanıyorsanız ve Citrix XenApp Essentials geçirmek istediğiniz, dikkate alınması gereken birkaç önkoşul vardır. İlk olarak, Citrix'ın okuma [Citrix XenApp Essentials için adım adım Teknik Dağıtım Kılavuzu](https://docs.citrix.com/content/dam/docs/en-us/citrix-cloud/downloads/xenapp-essentials-deployment-guide.pdf) ve kendi [çevrimiçi Teknik Kitaplığı](http://docs.citrix.com/en-us/citrix-cloud/xenapp-and-xendesktop-service/xenapp-essentials.html). 

## <a name="prerequisite-steps-for-migration"></a>Geçiş için önkoşul adımları

1. Yeni bir sanal ağ oluşturun veya hangi Azure sanal ağı Azure kaynağı Citrix XenApp Essentials dağıtacağınıza Yöneticisi'nde belirleyin. Azure RemoteApp Klasik Azure portalını kullanır; Citrix XenApp Essentials yalnızca Azure Kaynak Yöneticisi'ni destekler.  
2. Citrix yalnızca karma dağıtımlarda desteklediğinden, seçilen sanal ağ, etki alanı denetleyicisine ağ erişimi olduğundan emin olun. Azure RemoteApp bulut dağıtımını kullanıyorsanız, uygulamalarınızın sanal ağınızdaki bir Active Directory etki alanı denetleyicisi ağ erişimi olduğundan emin olun. Azure Active Directory etki alanı Hizmetleri (Azure AD DS) de kullanabilirsiniz. 
3. Bu etki alanına katılma, ilk denemede başarılı olması için DNS düzgün sanal ağ için yapılandırılmış olduğundan emin olun. Seçtiğiniz sanal ağdaki sanal makine (VM) oluşturun ve etki alanı ve DNS works beklendiği gibi katılın doğrulamak için el ile etki alanına katılma gerçekleştirin. Bu, Citrix XenApp Essentials dağıttığınız ilk kez başarılı olarak sağlar. 
4. Gerekirse, Azure RemoteApp ile kullanmakta olduğunuz Azure Klasik portalı sanal ağı ve Azure Resource Manager sanal ağınız arasında eşleme sanal ağ oluşturun. İki ağ aynı bölgede bulunuyorsa bu eşleme işlemi çalışır. Yapmazsanız, siteden siteye VPN ağ için sanal ağlara bağlanmak için kullanın. 
5. Gerekli olursa, okuma [içine ve dışına Azure RemoteApp verileri geçirmek nasıl](remoteapp-migrate.md). 
6. Var olan Azure RemoteApp görüntünüzü Citrix VDA bileşen içerecek şekilde güncelleştirmek (yönergeler için Citrix belgelere bakın). 
7. Azure Marketi'nde gidin ve Citrix XenApp Essentials dağıtım başlayın.

## <a name="other-considerations"></a>Diğer konular

Geçiş yaparken aşağıdaki ek hususlara dikkat edin:
- Citrix XenApp Essentials yalnızca karma dağıtımları destekler. Diğer bir deyişle, etki alanına katılma gerçekleştirmek için bir etki alanı denetleyicisi ağ erişim gerektirir. Azure RemoteApp bulut dağıtımını kullanıyorsanız, Azure AD DS kullanabilir veya sanal ağınızı etki alanına katılma için Active Directory'ye erişimi olduğundan emin olun. 
- Citrix XenApp Essentials kullanıcı verilerini taşıma hakkında bilgi edinmek için [içine ve dışına Azure RemoteApp verileri geçirmek nasıl](remoteapp-migrate.md). 
- Citrix XenApp Essentials yalnızca Active Directory hesaplarını destekler. Microsoft hesapları (örneğin, outlook.com, msn.com veya hotmail.com) desteklemez. 

## <a name="citrix-xenapp-essentials-billing"></a>Citrix XenApp Essentials faturalama

Fiyatlandırma hakkında ayrıntılar için bkz: [SSS](https://www.citrix.com/global-partners/microsoft/resources/xenapp-essentials-faq.html#tab-30699) ve [Citrix genel bakış makalesi](https://www.citrix.com/global-partners/microsoft/remote-app.html). Citrix XenApp Essentials üç fatura bileşenleri şunlardır:

- Citrix hizmet 12 aylık kullanıcı başına olan ücretsiz olarak. Tüm Azure Market satın alımları gibi bu Azure aboneliğinizle ilişkili ödeme yöntemi için faturalandırılır. Kurumsal Anlaşma (Kurumsal Sözleşme) müşteriler için Azure para kredisi kullanılamaz. 
- Uzak Veri Hizmetleri (RDS) istemci erişim lisansları (CAL). Şu anda 6,25 için Citrix XenApp Essentials ödeme ile birlikte paketlenebilir uzaktan erişim ücret satın alabilirsiniz. Bir EA müşterisiyseniz, bu için ödeme yapmak için Azure para kredisi kullanabilirsiniz. Varolan RDS CAL'leri kullanmak istiyorsanız, adresinden bize başvurun [ arainfo@microsoft.com ](mailto:arainfo@microsoft.com), biz Bu, faturanıza uygulayabilirsiniz. 
- Azure işlem ve depolama. Bu Azure depolama maliyeti ve işlem tüketim VM'ler için tüketilen. VM boyutu ve kullanıcı yoğunluğu seçerken fiyatlandırma dikkat edin. Bir EA müşterisiyseniz, bu için ödeme yapmak için Azure para kredisi kullanabilirsiniz.

Hala sorularınız varsa, şunları yapabilirsiniz:
- Adresinden bize e-posta [ arainfo@microsoft.com ](mailto:arainfo@microsoft.com).
- [Azure desteğine başvurun](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade). Tarafından Başlat [Azure destek talebi açarak](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) yardımcı olmak için 1-5 önkoşul adımları. Adım 6-7, Citrix Yönetim Portalı içinde bir destek bileti açılarak Citrix başvurun. 
