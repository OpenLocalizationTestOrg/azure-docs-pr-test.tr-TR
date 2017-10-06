---
title: aaaTroubleshoot Azure RBAC | Microsoft Docs
description: "Sorunları veya soruları rol tabanlı erişim denetimi kaynaklar hakkında yardım alın."
services: azure-portal
documentationcenter: na
author: andredm7
manager: femila
ms.assetid: df42cca2-02d6-4f3c-9d56-260e1eb7dc44
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: andredm
ms.reviewer: rqureshi
ms.openlocfilehash: 15feced32d8459d90c4c246d335932f90e1fc91f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="role-based-access-control-troubleshooting"></a>Rol tabanlı erişim denetimi sorunlarını giderme

Hello Azure portal rollerinde hello ve erişim sorunlarını giderebilirsiniz kullanarak hangi tooexpect bilmesi belge makalede rolleri ile verilen hello özel erişim hakları hakkında sık sorulan soruları yanıtlar. Bu üç rol tüm kaynak türleri kapsar:

* Sahip  
* Katılımcı  
* Okuyucu  

Tam erişim toohello yönetim deneyimi sahipleri ve katkıda bulunanları sahip ancak katılımcı erişim tooother kullanıcıları veya grupları veremez. Burada süre çok harcama yaptığımız böylece şeyler hello okuyucu rol ile biraz daha ilginç alın. Merhaba bkz [rol tabanlı erişim denetimi get-started makale](role-based-access-control-configure.md) nasıl toogrant erişim ile ilgili ayrıntılar için.

## <a name="app-service-workloads"></a>Uygulama hizmeti iş yükleri
### <a name="write-access-capabilities"></a>Yazma erişimi özellikleri
Bir kullanıcı salt okunur erişim tooa tek bir web uygulaması vermek, beklediğiniz değil, bazı özellikler devre dışı bırakılır. aşağıdaki yönetim özelliklerini hello gerektiren **yazma** erişim tooa web uygulaması (Katkıda bulunan veya sahibi) ve herhangi bir salt okunur senaryoda kullanılamaz.

* Komutları (örneğin, Başlat, Durdur, vs.)
* Genel yapılandırma, Ölçek ayarları, Yedekleme ayarlarını ve izleme ayarları gibi ayarlarını değiştirme
* Yayımlama kimlik bilgileri ve uygulama ayarlarının ve bağlantı dizeleri gibi diğer parolaları erişme
* Akış günlükleri
* Tanılama günlüklerini yapılandırma
* Konsol (komut istemi)
* Etkin ve en son dağıtımları (için yerel git sürekli dağıtımı)
* Tahmini harcamanız
* Web testleri
* Sanal ağ (sanal ağ yazma erişimine sahip bir kullanıcı tarafından önceden yapılandırılmışsa, yalnızca görünür tooa okuyucu).

Bu kutucukların erişemiyorsanız tooask katkıda bulunan erişim toohello web uygulaması için yöneticinize gerekir.

### <a name="dealing-with-related-resources"></a>İlgili kaynaklar postalarla
Web uygulamaları tarafından Interplay birkaç farklı kaynakların hello varlığı karmaşık. Birkaç Web sitelerini tipik kaynak grubuyla şöyledir:

![Web uygulaması kaynak grubu](./media/role-based-access-control-troubleshooting/website-resource-model.png)

Erişim toojust hello web uygulaması vermeniz, sonuç olarak, hello Web sitesi dikey penceresinde hello Azure portalı üzerinde hello işlevlerinin çoğunu devre dışı bırakılır.

Bu öğeler gerektiren **yazma** toohello erişim **uygulama hizmeti planı** tooyour Web sitesi karşılık gelen:  

* Görüntüleme hello web uygulaması fiyatlandırma Katmanı (ücretsiz veya standart)  
* Ölçek yapılandırma (örnekleri, sanal makine boyutu, otomatik ölçeklendirme ayarlarını sayısı)  
* Kotalar (depolama, bant genişliği, CPU)  

Bu öğeler gerektiren **yazma** erişim toohello tüm **kaynak grubu** Web sitenizi içerir:  

* SSL sertifikaları ve bağlamaları (SSL sertifikalarını hello siteler arasında paylaşılabilir aynı kaynak grubunu ve coğrafi konum)  
* Uyarı kuralları  
* otomatik ölçeklendirme ayarları  
* Uygulama Öngörüler bileşenleri  
* Web testleri  

## <a name="virtual-machine-workloads"></a>Sanal makine iş yükleri
Çok gibi web apps ile bazı özellikler hello sanal makine dikey yazma erişimi toohello sanal makine ya da tooother kaynakları hello kaynak grubunda gerektirir.

Sanal makine ilgili tooDomain adları, sanal ağlar, depolama hesapları ve uyarı kuralları yok.

Bu öğeler gerektiren **yazma** toohello erişim **sanal makine**:

* Uç Noktalar  
* IP adresleri  
* Diskler  
* Uzantılar  

Bunlar **yazma** erişim tooboth hello **sanal makine**ve hello **kaynak grubu** (Merhaba etki alanı adı ile birlikte), BT zamanı:  

* Kullanılabilirlik kümesi  
* Yük dengeli kümesi  
* Uyarı kuralları  

Bu kutucukların erişemiyorsanız yöneticinize katkıda bulunan erişim toohello kaynak grubu için isteyin.

## <a name="see-more"></a>Diğerlerini görüntüle
* [Rol tabanlı erişim denetimi](role-based-access-control-configure.md): hello Azure portalında RBAC ile çalışmaya başlama.
* [Yerleşik roller](role-based-access-built-in-roles.md): Get RBAC standart gelen hello rolleri hakkında ayrıntılar.
* [Azure rbac'de özel roller](role-based-access-control-custom-roles.md): toocreate özel roller toofit erişiminizi nasıl gerektiğini öğrenin.
* [Erişim değişiklik geçmişi raporu oluşturma](role-based-access-control-access-change-history-report.md): RBAC içinde rol atamalarını değiştirme izler.

