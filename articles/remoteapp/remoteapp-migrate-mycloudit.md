---
title: "Azure RemoteApp için fatura değiştirme | Microsoft Docs"
description: "Azure RemoteApp için fatura Durdur öğrenin."
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 8f94da9a-7848-4ddc-b7b7-d9c280ccf4d7
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: mbaldwin
ms.openlocfilehash: 32fc673eeef01e80c73375bf264206beea8cfbe5
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/29/2017
---
# <a name="migrate-from-azure-remoteapp-to-mycloudit"></a>Azure RemoteApp için MyCloudIT geçirme 

**Şu anda Microsoft Azure RemoteApp kullanıyor musunuz?** : MyCloudIT yerleşik Microsoft Azure üzerinde çalışmaya devam ederken MyCloudIT yönetim platformu için Azure RemoteApp (ARA) collection(s) geçirmek için otomatikleştirilmiş bir aracı.

**Azure Resource Manager portal yararlanmak**: MyCloudIT platform içine tamamlanan geçiş Azure'nın yeni Azure Resource Manager portal anında erişim sağlar. Yenilikler Microsoft Azure tarafından sunulan dahil olmak üzere, dağıtımınızı sağlamak için sanal makine boyutlarını kendi iş gereksinimlerinizi desteklemek için yerleşik olarak bulunur ve bu portalı tüm yeni özellikler içerir.

**Paralel gereksinimleriniz için doğru çözümdür emin olmak için test**: MyCloudIT geçiş aracı, test paralel süre geçerli ARA kullanıcılarınızın ARA kullanmaya devam eder ve geçiş işlemini başlatmak için oluşturulur.  Kullanıcılarınızın geçişinizi kadar ARA içinde kalır ve testi tamamlandı.  Geçiş Aracı tipik ARA koleksiyonu işlemek için yerleşik olarak bulunur.  Düşünüyorsanız lütfen bizimle iletişime geçin benzersiz, standart olmayan bir senaryo varsa [ sales@conexlink.com ](mailto:sales@conexlink.com) biz geçişinizi ile yardımcı olmak için özel bir plan sağlayabilir.

**Hizmet olarak masaüstü özellikleri**: Lütfen unutmayın MyCloudIT yalnızca için alışkın RemoteApp özellikler sunar, ancak ayrıca tam masaüstü-bir hizmet olarak sunuyoruz en az bir kullanıcı olmaksızın aylık aynı maliyet için özellikleri gereksinimleri.

## <a name="what-we-will-do-for-you"></a>Biz sizin için ne yapacağını

MyCloudIT aboneliğinizin Klasik Azure portalı, Azure RemoteApp şablonu Azure Resource Manager Portal'ın otomatik geçiş aracımız aboneliğinizle geçişini otomatikleştirir.  

> [!NOTE]
> Azure RemoteApp şablon özgün Azure RemoteApp dağıtımınız ile aynı Azure bölgede kalmalıdır.  Azure bölgeleri ya da Azure abonelik geçişi sırasında değiştirmeniz gerekiyorsa, lütfen bize ek yönergeler için başvurun [ sales@conexlink.com ](mailto:sales@conexlink.com).

MyCloudIT geçiş aracı otomatik geçiş işlemine ilişkin ayrıntılı bilgi için aşağıda okuyun:

1. Geçiş Aracı, tüm var olan ARA dağıtımlar için geçerli Abonelikleriniz tarar.  
2. Aynı anda geçirmek için bir ARA koleksiyon seçin.  Birden çok koleksiyon varsa, sunduğumuz aracı birden çok kez çalıştırın.
3. Eski veri almak veya el ile yeni dağıtım, UPD eşlemek üzere yeni dağıtımınız için kullanıcı profili diskleri (UPD) kopyalamak için seçeneğiniz vardır. UPD kopyalamak seçerseniz, biz UPD kaydetmek ve UPD ad her kullanıcı adıyla eşleşen bir metin dosyası içerir.  UPD RDSMGMT sunucusundaki bir paylaşımına kopyalanacak `F:\Shares\LegacyUPD` ve paylaşım yoluyla kullanıma `\\RDSmgmt\LegacyUPD`. 
4. Geçişinizi geçerli ARA dağıtımınız için kapalı kalma süresi gerektirir.  Ancak, herhangi bir değişiklik UPD (ARA) öğesinden sonra kopyalama yapılırsa, bu değişiklikler Azure Resource Manager portalında saklanan UPD içinde yansıtılmaz. 
5. Klasik Azure sanal ağınızda etki alanı denetleyicileri ve dosya sunucuları gibi ek Vm'leriniz varsa VNet arasında varolan Klasik Azure sanal ağınızda ve yeni Azure kaynak oluşturuyoruz, sizin için yeni sanal ağ eşlemesi oluşturmak Yönetici portalı.
6. Otomatik çözümümüzdür yalnızca sanal ağ, var olan ARA dağıtımınızı karma bir dağıtım ise varolan Klasik Azure sanal ağınızda ve yeni sanal ağ arasında eşleme kurar; yani, Windows Server Active Directory etki alanı denetleyicisi varolan Klasik sanal ağda doğrulama. Biz koleksiyonunuz için VNet eşlemesi kurma değil, ancak sanal ağ eşleme gerektirir, lütfen bize olarak başvurun [ sales@conexlink.com ](mailto:sales@conexlink.com) ve biz VNet eşlemesi hiçbir ek ücret yapılandırmak mutluluk olacaktır.
7. Otomatik çözümümüzdür Azure DNS yapılandırma ayarlarıyla yeni dağıtımınızı varolan etki alanı denetleyicinizi Klasik VNet içinde bağlanıp emin olmak için yeni sanal ağ güncelleştirilir güvence altına alır.
8. Otomatik çözümümüzdür Biz bu yeni bir sanal ağ oluşturur ve var olan Windows Server Active Directory Server sahip dağıtımlar için VNet eşlemesi kurma hiçbir IP adresi çakışmalarını olduğundan emin.
9. Kimlik doğrulaması için yalnızca Azure AD kullanıyorsanız MyCloudIT yeni bir Windows Server Active Directory etki alanı oluşturun ve Azure AD Connect kullanıcılar var olan Azure AD örneğini ve yeni Windows Server Active Directory tarafından oluşturulan etki alanı arasında eşitlemek için kullanın MyCloudIT.
10. ARA kullanıcıların kimliklerini doğrulamak için bir Windows Server Active Directory etki alanı kullanıyorsanız, otomatik çözümümüzdür var olan Windows Server Active Directory etki alanı VNet eşlemesi aracılığıyla denetleyicinize yeni MyCloudIT dağıtımınızı bağlanır.
11. Azure Active Directory etki alanı Hizmetleri kimlik doğrulaması kullanıyorsanız, size geçiş ancak biz bir özel geçiş planı sizin için oluşturabilmesi için lütfen bizimle iletişime geçin.  Lütfen e-posta Gönder [ sales@conexlink.com ](mailto:sales@conexlink.com). 
12. Geçirilecek koleksiyonu onaylandıktan sonra arkanıza yaslanın ve otomatik çözümümüzdür ARA toplama ve kullanıcı profili diskleri (isteğe bağlı) uzaktan uygulamaları çözüm güdümlü yeni MyCloudIT geçirir sırada hafifletin.
13. Dağıtım tamamlandıktan sonra biz yeniden ARA ve ek uygulamaları yayımlamak olur dağıtım sonrası yayımlanan aynı uygulamaları yayımlamak.

## <a name="post-migration-benefits"></a>POST geçiş avantajları

1. Uzak uygulamalar dağıtımınızın tam yaşam döngüsünü yönetmenize olanak sağlayan Yönetim Konsolu sunuyoruz.
2. Bizim portalından sanal makinelerinizi yönetme kabiliyeti olacaktır.  Başlatma / durdurma ve gerekirse tek tek sanal makineleri yeniden boyutlandırın.
3. Yönetim Konsolu oluşturmak ve kullanıcıları yönetme olanağı sağlar / bizim Yönetim Portalı'ndan gruplandırır.
4. Yönetim Konsolu kullanıcıları aynı bir oturum açma deneyimi oluşturmak için Office 365 ile eşitleme olanağı sağlar.
5. Yönetim Konsolu ek RemoteApp ve Masaüstü koleksiyonları yinelenen kullanıcı maliyetler veya en düşük kullanıcı gereksinimleri oluşturma olanağı sağlar. 
6. Yönetim Konsolu yeni uzak uygulamalar uygulamaları yayımlama olanağı sağlar.
7. Yönetim Konsolu çözümünüzü yalnızca belirli saatlerde gerekiyorsa başlatma ve kapatma, uzak uygulamalar dağıtımınızın zamanlama olanağı sağlar.
8. Yönetim Konsolu yükleme ve yapılandırma, müşteri verileri için bir belge bekletme geçmişini sağlayan Azure yedekleme Aracısı'nın otomatik hale getirme olanağı sağlar.
9. Yönetim Konsolu performans ölçümleri, dağıtımınızın erişim sağlar.  Bu, ek performans yönetim araçlarını yükleme olmadan tüm olası performans sorunlarını tanımlamak için olanak sağlar.
10. Birden çok oturumu ana bilgisayar varsa, yalnızca çalıştırıyor olmanız gerekir ana çalışan oturum ölçeklendirme otomatik etkinleştir kuramaz.
11. MyCloudIT MyCloudIT etki alanı adı üzerinden RDWeb Ağ Geçidi sunucusuna erişim sağlar.  Özel bir URL URL'sine markalama son kullanıcıdan yeniden eşleme özelliğini de sunuyoruz.

## <a name="prerequisites-for-migration"></a>Geçiş için Önkoşullar

1. Geçerli Azure RemoteApp çözümünüzü barındıran Azure aboneliğine erişiminiz olmalıdır.
2. Şablonunuzu geçirmek ve oluştur / yeni MyCloudIT dağıtımınızı değiştirmek için aboneliğinizi içinde bizim portal izinleri vermeniz gerekir.
3. Lütfen Azure RemoteApp içinde bir sınırlama nedeniyle unutmayın, her bir koleksiyon yalnızca üç kez geçirilebilir.  Üç defadan fazla bir koleksiyonuna geçirmek gerekiyorsa, bir bilet verme sayınız artırmak için Azure yükseltmek veya bizimle iletişime geçin ve dışarı aktarma sayısını artırmak için ARA istekte yardımcı olacaktır.

## <a name="mycloudit-billing"></a>MyCloudIT faturalama

Lütfen bakın [MyCloudIT fiyatlandırma RemoteApp çözümleri için](https://mcitdocuments.blob.core.windows.net/terms/MyCloudIT_Pricing_Overview.pdf) (PDF) tahmin etmek ve genel Azure maliyetleriniz yönetme hakkında bilgi için.

Hala sorularınız varsa lütfen bizimle iletişime geçin [ sales@conexlink.com ](mailto:sales@conexlink.com) veya tam tanıtım videosunu izleyin [Azure RemoteApp geçiş aracı - MyCloudIT](https://www.youtube.com/watch?v=YQ_1F-JeeLM&t=482s). 

