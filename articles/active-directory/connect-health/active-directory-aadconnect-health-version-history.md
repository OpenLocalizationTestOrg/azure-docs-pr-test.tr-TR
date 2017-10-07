---
title: "aaaAzure AD Connect Health sürüm geçmişi"
description: "Bu belgede, Azure AD Connect Health ve bu sürümlerde dahil hello sürümleri açıklanmaktadır."
services: active-directory
documentationcenter: 
author: karavar
manager: samueld
editor: curtand
ms.assetid: 8dd4e998-747b-4c52-b8d3-3900fe77d88f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: a583263e412f5da9af75947f3431de2494042388
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-health-version-release-history"></a>Azure AD Connect Health: Sürüm Yayınlama Geçmişi
Hello Azure Active Directory ekibi, yeni özellikler ve işlevsellik ile Azure AD Connect Health düzenli olarak güncelleştirir. Bu makalede hello sürümleri ve çıkarılan özellikleri listelenmektedir.

## <a name="october-2016"></a>Ekim 2016
**Aracı güncelleştirmesi:**

* AD FS için Azure AD Connect Health Aracısı \(sürüm 2.6.408.0\)
  1. İstemci IP adresleri kimlik doğrulama isteklerinin seviyelerinden geliştirmeleri
  2. Hata düzeltmeleri tooAlerts ilgili
* AD DS (sürüm 2.6.408.0) için Azure AD Connect Health Aracısı
  1. Hata düzeltmeleri tooAlerts ilgili.
* Azure AD Connect ile sürüm 1.1.281.0 yayımlanan eşitleme (sürüm 2.6.353.0) için Azure AD Connect Health Aracısı
  1. Eşitleme hata raporlarını hello için gerekli hello verileri sağlar
  2. Hata düzeltmeleri tooAlerts ilgili

**Yeni Önizleme özellikleri:**

* Azure ad eşitleme hata raporlarını Bağlan

**Yeni Özellikler:**

* Azure AD Connect Health AD FS için-IP adres alanını hatalı kullanıcı adı/parola ile ilk 50 kullanıcıya ilişkin hello rapordaki kullanılabilir.

## <a name="july-2016"></a>Temmuz 2016
**Yeni Önizleme özellikleri:**

* [Azure AD Connect Health için AD DS](active-directory-aadconnect-health-adds.md).

## <a name="january-2016"></a>2016 Ocak
**Aracı güncelleştirmesi:**

* AD FS (sürüm 2.6.91.1512) için Azure AD Connect Health Aracısı

**Yeni Özellikler:**

* [Test Bağlantısı aracı için Azure AD Connect Health aracıları](active-directory-aadconnect-health-agent-install.md#test-connectivity-to-azure-ad-connect-health-service)

## <a name="november-2015"></a>2015 Kasım
**Yeni Özellikler:**

* Desteği [rol tabanlı erişim denetimi](active-directory-aadconnect-health-operations.md#manage-access-with-role-based-access-control)

**Yeni Önizleme özellikleri:**

* [Azure AD Connect Health eşitleme](active-directory-aadconnect-health-sync.md).

**Giderilen sorunlar:**

* Aracı kaydı sırasında görülen hataları için hata düzeltmeleri.

## <a name="september-2015"></a>Eylül 2015
**Yeni Özellikler:**

* AD FS için kullanıcı adı parola rapor yanlış
* Destek tooconfigure kimliği doğrulanmamış HTTP Proxy
* Sunucu Çekirdeği yüklemesinde tooconfigure Aracısı desteği
* AD FS için geliştirmeler tooAlerts
* Bağlantı ve veriler için AD FS için Azure AD Connect Health Aracısı geliştirmeler karşıya yükleyin.

**Giderilen sorunlar:**

* AD FS hata türleri için kullanım incelemesi hata düzeltmeleri.

## <a name="june-2015"></a>Haziran 2015
**Azure AD Connect Health ilk sürüm için AD FS ve AD FS Proxy.**

**Yeni Özellikler:**

* AD FS ve AD FS Proxy sunucularının e-posta bildirimleri ile izleme için Uyarılar'ı tıklatın.
* Kolay erişim tooAD FS topolojisi ve AD FS performans sayaçları düzenleri.
* Uygulamalar, kimlik doğrulama yöntemleri, ağ konumu vb. isteği göre gruplandırılmış AD FS sunucularında başarılı belirteç isteklerini eğilimi.
* Hata türleri vb. uygulamalar tarafından gruplandırılmış AD FS sunucularındaki başarısız istek eğilimler.
* Azure AD genel yönetici kimlik bilgilerini kullanarak basit aracı dağıtımı.  

## <a name="next-steps"></a>Sonraki adımlar
Daha fazla bilgi edinmek [hello bulutta, şirket içi kimlik altyapınızı ve Eşitleme hizmetlerini izlemek](active-directory-aadconnect-health.md).

