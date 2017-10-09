---
title: "aaaNo kullanıcılar sağlanan tooan Azure AD galeri uygulama olan | Microsoft Docs"
description: "Tootroubleshoot sık karşılaşılan sorunları nasıl karşılaştığı görüntülenmesini kullanıcılar görmüyorsanız, Azure AD bir kullanıcı Azure AD ile sağlamak için yapılandırdığınız uygulama Galerisi"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: asteen
ms.openlocfilehash: 4d9693a202ed657e1de5571b50e5d499bef1bb3f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="no-users-are-being-provisioned-tooan-azure-ad-gallery-application"></a>Hiçbir kullanıcı sağlanan tooan Azure AD galeri uygulama yükleniyor

Bir kez otomatik sağlama (Merhaba uygulama sağlanan kimlik bilgileri tooAzure AD tooconnect toohello uygulama geçerli doğrulama dahil) bir uygulama için yapılandırıldı. Kullanıcılar ve/veya grupları sağlanan toohello uygulamasına ve şeyler aşağıdaki hello tarafından belirlenir:

-   Hangi kullanıcıların ve grupların olmuştur **atanan** toohello uygulama. Atama hakkında daha fazla bilgi için bkz: [Azure Active Directory'de bir kullanıcı veya grup tooan kuruluş uygulama atama](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal).

-   Desteklemediğini **öznitelik eşlemelerini** Azure AD toohello uygulamadan etkinleştirilmiş ve yapılandırılmış toosync geçerli öznitelikleridir. Öznitelik eşlemelerini hakkında daha fazla bilgi için bkz: [özelleştirme kullanıcı sağlama öznitelik eşlemelerini Azure Active Directory'de SaaS uygulamaları için](https://docs.microsoft.com/azure/active-directory/active-directory-saas-customizing-attribute-mappings).

-   Olsun veya olmasın bir **kapsam filtresi** kullanıcıları filtreleme mevcut dayalı belirli öznitelik değerleri. Kapsam belirleme filtreleri ile ilgili daha fazla bilgi için bkz: [kapsam belirleme filtreleri ile öznitelik tabanlı uygulama sağlama](https://docs.microsoft.com/azure/active-directory/active-directory-saas-scoping-filters).

Kullanıcıların sağlanan değil Gözlemleme, belirli bir kullanıcı için günlük girdilerini arayın ve Azure AD'de hello denetim günlüklerine bakın.

Denetim günlüklerini sağlama hello hello Azure portalında, hello erişilebilir **Azure Active Directory &gt; Kurumsal uygulamaları &gt; \[uygulama adı\] &gt; denetim günlükleri**sekmesi. Filtre hello hello üzerinde oturum **hesap sağlama** kategori tooonly olayları bu uygulama için sağlama hello bakın. "Hello öznitelik eşlemelerini kendileri için yapılandırılan hello eşleşen ID" temel alarak kullanıcılara arayabilirsiniz. Örneğin hello "kullanıcı asıl adı" veya "Merhaba Azure AD tarafında özniteliği eşleşen hello olarak e-posta adresi" yapılandırılmış ve değil sağlama hello kullanıcı değerine sahip "audrey@contoso.com". Merhaba denetim günlüklerini arama "audrey@contoso.com" ve gözden geçirin, ardından girdi döndü.

Tüm Azure AD sağlama, bu kullanıcıların hello varlığı hello hedef uygulama sorgulama, hello karşılaştırma kapsamında atanan kullanıcılar için sorgulama dahil olmak üzere hello sağlama hizmeti tarafından gerçekleştirilen işlemler hello kayıt denetim sağlama hello günlükleri kullanıcı nesneleri arasında hello sistem. Sonra ekleme, güncelleştirme veya hello karşılaştırma üzerine dayalı hello hedef sistemdeki hello kullanıcı hesabı devre dışı bırakın.

## <a name="general-problem-areas-with-provisioning-tooconsider"></a>Tooconsider sağlama ile genel sorunlu alanları

Merhaba listesini nereden hakkında bir fikir varsa, ayrıntılarına geçebilir genel sorunlu alanları aşağıdadır toostart.

* [Hizmet sağlama toostart görünmüyor](#provisioning-service-does-not-appear-to-start)
* [Atanmış olan olsa bile kullanıcılar atlanacak ve sağlanan değil, denetim günlüklerini söyleyin](#audit-logs-say-users-are-skipped-and-not-provisioned-even-though-they-are-assigned)

## <a name="provisioning-service-does-not-appear-toostart"></a>Hizmet sağlama toostart görünmüyor

Merhaba ayarlarsanız **sağlama durumu** toobe **üzerinde** hello içinde **Azure Active Directory &gt; Kurumsal uygulamaları &gt; \[Uygulamaadı\] &gt;Sağlama** hello Azure portalı bölümü. Ancak başka durumunu Ayrıntılar gösterilir bu sayfada sonraki yeniden yükler sonra hello hizmeti çalışıyor ancak bir ilk eşitleme henüz tamamlanmadı olasıdır. Merhaba denetleyin **denetim günlüklerini** toodetermine açıklanan hangi işlemleri hello hizmetin çalıştığını ve herhangi bir hata olup olmadığını.

>[!NOTE]
>Bir başlangıç eşitlemesi herhangi bir yere hello boyutunu hello Azure AD dizini ve hello sayısı, kullanıcı sağlama kapsamında bağlı olarak 20 dakika tooseveral saat sürebilir. Sonraki eşitlemeler hello ilk eşitleme sonra daha hızlı, hello hizmet sağlama hello ilk eşitleme sonrasında her iki sistemle hello durumunu temsil filigranlar depolar. Bu, sonraki eşitlemeler performansını artırır.
>
>

## <a name="audit-logs-say-users-are-skipped-and-not-provisioned-even-though-they-are-assigned"></a>Denetim günlüklerini kullanıcılar atlanacak ve atanmış olan olsa bile sağlanan değil söyleyin

"Hello denetim günlükleri atlandı gibi" kullanıcı görüntülenir çok önemli tooread hello hello günlük iletisi toodetermine hello neden ayrıntılarında genişletilmiş olur. Ortak nedenleri ve çözümleri aşağıda verilmiştir:

-   **Bir kapsam filtresi yapılandırılmış** **filtrelemesi hello kullanıcı bir öznitelik değerini temel**. Kapsam belirleme filtreleri ile ilgili daha fazla bilgi için bkz: <https://docs.microsoft.com/azure/active-directory/active-directory-saas-scoping-filters>.

-   **Merhaba kullanıcı "etkili bir şekilde alınarak" dir.** Bu belirli bir hata iletisi görürseniz, Azure AD'de depolanan başlangıç kullanıcı atama kaydı ile ilgili bir sorun olduğundan değildir. toofix Bu sorun, atamayı hello uygulamadan kullanıcı (veya grubu) hello ve tekrar yeniden atayın. Atama hakkında daha fazla bilgi için bkz: <https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal>.

-   **Gerekli bir öznitelik eksik veya bir kullanıcı için doldurulan değil.** Sağlama yukarı ayarı tooreview kullanırken önemli şey tooconsider hello öznitelik eşlemelerini ve hangi kullanıcı (veya grubu) özellikleri akışı Azure AD toohello uygulamasından tanımlamak iş akışları ve yapılandırın. Bu hello "eşleşen özellik" ayarı içerir kullanılan toouniquely olması tanımlamak ve eşleşen kullanıcıları/grupları hello iki sistemleri arasında. Bu önemli işlemi hakkında daha fazla bilgi için bkz: [özelleştirme kullanıcı sağlama öznitelik eşlemelerini Azure Active Directory'de SaaS uygulamaları için](https://docs.microsoft.com/azure/active-directory/active-directory-saas-customizing-attribute-mappings).

  * **Öznitelik grupları için eşlemeleri:** hello sağlama grup adı ve Grup ayrıntıları toplama toohello üyeleri, bazı uygulamalar için destekleniyorsa. Etkinleştirmek veya bu işlevi etkinleştirmek veya hello devre dışı bırakarak devre dışı **eşleme** hello gösterilen grubu nesnelerinin **sağlama** sekmesi. Grupları sağlama etkinleştirilirse tooreview hello öznitelik eşlemelerini tooensure uygun bir alan "Eşleşen kimliği" Merhaba kullanılan emin olun. Bu olabilir hello görünen ad veya e-posta diğer adı), hello grubu ve üyelerini hello varsa sağlanması olmayan özellik eşleşen Azure AD içinde boş veya bir grup için doldurulan aynıdır.

## <a name="next-steps"></a>Sonraki adımlar
[Azure AD Connect eşitleme: bildirim temelli hazırlama anlama](active-directory-aadconnectsync-understanding-declarative-provisioning.md)

