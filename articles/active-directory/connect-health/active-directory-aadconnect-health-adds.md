---
title: Azure AD Connect Health AD DS ile aaaUsing | Microsoft Docs
description: "Ele alınacaktır hello Azure AD Connect Health sayfasında budur nasıl toomonitor AD DS."
services: active-directory
documentationcenter: 
author: arluca
manager: femila
editor: curtand
ms.assetid: 19e3cf15-f150-46a3-a10c-2990702cd700
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: e2fb6be65407d02c214dcab385b85d6cb54f48de
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="using-azure-ad-connect-health-with-ad-ds"></a>Azure AD Connect Health'i AD DS ile Kullanma
Belge aşağıdaki hello belirli toomonitoring Active Directory etki alanı Hizmetleri ile Azure AD Connect Health ' dir. AD DS hello desteklenen sürümler: Windows Server 2008 R2, Windows Server 2012, Windows Server 2012 R2 ve Windows Server 2016.

Azure Connect Health ile AD FS'yi izleme hakkında daha fazla bilgi almak için bkz. [Azure AD Connect Health'i AD FS ile kullanma](active-directory-aadconnect-health-adfs.md). Ek olarak, Azure AD Connect’i (Eşitleme) Azure AD Connect Health ile izleme hakkında bilgi için bkz. [Eşitleme için Azure AD Connect Health Kullanma](active-directory-aadconnect-health-sync.md).

![AD DS için Azure AD Connect Health](./media/active-directory-aadconnect-health/aadconnect-health-adds-entry.png)

## <a name="alerts-for-azure-ad-connect-health-for-ad-ds"></a>AD DS için Azure AD Connect Health uyarıları
AD DS için Azure AD Connect Health uyarıları bölümde Merhaba, etkin veya çözümlenmiş uyarıları, ilgili tooyour etki alanı denetleyicilerinin listesini sağlar. Etkin veya çözümlenmiş bir uyarıyı seçtiğinizde, çözüm adımları yanı sıra ek bilgiler içeren yeni bir dikey pencere açar ve toosupporting belgelerine bağlar. Her uyarı türünü belirli bu uyarıdan etkilenen hello etki alanı denetleyicilerinin tooeach karşılık gelen bir veya birden çok örneği olabilir. Merhaba uyarı dikey penceresinde Hello altına, etkilenen etki alanı denetleyicisi tooopen ek bir dikey penceresinde, uyarı örneği hakkında daha fazla ayrıntı çift tıklatabilirsiniz.

Bu Dikey içinde uyarılar için e-posta bildirimlerini etkinleştirmek ve hello zaman aralığı görünümünde değiştirin. Merhaba zaman aralığı genişletme toosee önceki çözümlenen uyarılar sağlar.

![Azure AD Connect eşitleme hatası](./media/active-directory-aadconnect-health/aadconnect-health-adds-alerts.png)

## <a name="domain-controllers-dashboard"></a>Etki Alanı Denetleyicileri Panosu
Bu pano teme çalışma ölçümleri ve izlenen etki alanlarınızın her birinin sistem durumu ile birlikte ortamınızın topolojik bir görünümünü sağlar. Merhaba sunulan ölçümleri tanımlamak tooquickly Yardım, araştırma gerektirebilecek herhangi bir etki alanı denetleyicisine daha fazla. Varsayılan olarak, yalnızca bir sütun alt kümesi hello görüntülenir. Ancak, hello sütunlar komutunu tıklatarak hello kümesinin tamamını kullanılabilir sütunlar bulabilirsiniz. En, bu panoyu tek ve kolay yerleştirin, AD DS ortamında tooview hello durumunu kapatır ilgilendiğiniz hello sütunları seçme.

![Etki Alanı Denetleyicileri](./media/active-directory-aadconnect-health/aadconnect-health-adds-domainsandsites-dashboard.png)

Etki alanı denetleyicileri, kendi etki alanı veya hello ortamı topolojisi anlamak için faydalıdır siteye göre gruplanabilir. Merhaba dikey penceresi başlığı çift tıklarsanız, son olarak, hello Pano tooutilize hello kullanılabilir ekran-Gayrimenkul en üst düzeye çıkarır. Daha geniş olan bu görünüm birden fazla sütun gösterilirken yararlıdır.

## <a name="replication-status-dashboard"></a>Çoğaltma Durumu Panosu
Bu panoyu izlenen etki alanı denetleyicileriniz hello çoğaltma durumu ve çoğaltma topolojisi bir görünümünü sağlar. Merhaba en son çoğaltma denemesi Hello durumunu, bulunan herhangi bir hata için yararlı belgelerle birlikte listelenir. Tooopen bilgi içeren yeni bir dikey pencere bir hata ile bir etki alanı denetleyicisi gibi çift tıklayarak: çözüm adımları, önerilen hello hata hakkındaki ayrıntılar ve tootroubleshooting belgelerine bağlar.

![Çoğaltma Durumu](./media/active-directory-aadconnect-health/aadconnect-health-adds-replication.png)

## <a name="monitoring"></a>İzleme
Bu özellik, grafik eğilimleri her hello izlenen etki alanı denetleyicileri sürekli olarak toplanan farklı performans sayaçları sağlar. Bir etki alanı denetleyicisinin performansı, ormanınızdaki diğer tüm izlenen etki alanı denetleyicileri arasında kolayca karşılaştırılabilir. Ayrıca, ortamınızdaki sorunları gidermede yardımcı olmak üzere çeşitli performans sayaçlarını yan yana görebilirsiniz.

![İzleme](./media/active-directory-aadconnect-health/aadconnect-health-adds-monitoring.png)

Varsayılan olarak, şu dört performans sayaçları seçilmiş; Ancak, diğerleri hello filtre komutunu tıklatarak ve seçerek veya herhangi bir istediğiniz performans sayacı seçimini içerebilir. Ayrıca, bir performans sayacı grafik tooopen her hello izlenen etki alanı denetleyicileri için veri noktaları içeren yeni bir dikey pencere, çift tıklayabilirsiniz.

## <a name="related-links"></a>İlgili bağlantılar
* [Azure AD Connect Health](active-directory-aadconnect-health.md)
* [Azure AD Connect Health Aracısı Yüklemesi](active-directory-aadconnect-health-agent-install.md)
* [Azure AD Connect Health İşlemleri](active-directory-aadconnect-health-operations.md)
* [Azure AD Connect Health'i AD FS ile Kullanma](active-directory-aadconnect-health-adfs.md)
* [Eşitleme için Azure AD Connect Health'i kullanma](active-directory-aadconnect-health-sync.md)
* [Azure AD Connect Health ile ilgili SSS](active-directory-aadconnect-health-faq.md)
* [Azure AD Connect Health Sürüm Geçmişi](active-directory-aadconnect-health-version-history.md)

