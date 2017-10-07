---
title: "Kullanıcı tooan Azure AD galeri uygulama sağlama yapılandırma aaaProblem | Microsoft Docs"
description: "Kullanıcı zaten hello Azure AD uygulama galerisinde listelenen tooan uygulama sağlama yapılandırırken tootroubleshoot sık karşılaşılan sorunları nasıl karşılaştığı"
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
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 19b12be019b05faecef74c6f92a9de03b52a5ef9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="problem-configuring-user-provisioning-tooan-azure-ad-gallery-application"></a>Kullanıcı tooan Azure AD galeri uygulama sağlama yapılandırma sorunu

Yapılandırma [otomatik kullanıcı sağlamayı](https://docs.microsoft.com/azure/active-directory/active-directory-saas-app-provisioning) bir uygulama için (desteklendiği yerlerde), özel yönergeler otomatik sağlama izlenen tooprepare Merhaba uygulaması olmasını gerektirir. Ardından, hizmet toosynchronize kullanıcı hesapları toohello uygulaması sağlama hello Azure portal tooconfigure hello kullanabilirsiniz.

Her zaman, uygulamanız için sağlama yukarı hello Kurulum öğretici belirli toosetting bularak başlamanız gerekir. Ardından bu adımları tooconfigure hem hello uygulama izleyin ve Azure AD toocreate hello sağlama bağlantı. Uygulama öğreticilerin bir listesi bulunabilir [nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları](https://docs.microsoft.com/azure/active-directory/active-directory-saas-tutorial-list).

## <a name="how-toosee-if-provisioning-is-working"></a>Sağlama durumunda toosee nasıl çalıştığını 

Merhaba hizmet yapılandırıldıktan sonra iki yerde hello işlemi hello hizmetinin çoğu Öngörüler çizilebilir:

-   **Denetim günlükleri** – hello hizmet sağlama hello tarafından gerçekleştirilen tüm hello işlemler denetim günlüklerini kaydını sağlama, Azure AD için sorgulama dahil olmak üzere atanan sağlama kapsamında olan kullanıcılar. Sorgu hello hedef uygulama hello kullanıcı nesneleri hello sistem arasında karşılaştırma kullanıcılarla hello varlığı. Sonra ekleme, güncelleştirme veya hello karşılaştırma üzerine dayalı hello hedef sistemdeki hello kullanıcı hesabı devre dışı bırakın. Denetim günlüklerini sağlama hello hello Azure portalında, hello erişilebilir **Azure Active Directory &gt; Kurumsal uygulamaları &gt; \[uygulama adı\] &gt; denetim günlükleri**sekmesi. Filtre hello hello üzerinde oturum **hesap sağlama** kategori tooonly olayları bu uygulama için sağlama hello bakın.

-   **Sağlama durumu –** hello son sağlama Özet çalıştırmak için belirli bir uygulamanın hello görülebilir **Azure Active Directory &gt; Kurumsal uygulamaları &gt; \[uygulama adı\] &gt; Sağlama** kısmına hello ekranın alt kısmındaki hello hello hizmet ayarları altında. Bu bölümde, kaç tane kullanıcıların (ve/veya grupları) şu anda hello arasında iki sistem eşitlenmekte olan ve herhangi bir hata olup olmadığını özetler. Hata ayrıntılarını hello denetim günlükleri'olmalıdır. Sağlama durumu hello Not değil doldurulmuş Azure AD arasında bir tam ilk eşitleme işlemi tamamlanana kadar ve hello uygulama.

## <a name="general-problem-areas-with-provisioning-tooconsider"></a>Tooconsider sağlama ile genel sorunlu alanları

Merhaba listesini nereden hakkında bir fikir varsa, ayrıntılarına geçebilir genel sorunlu alanları aşağıdadır toostart.

* [Hizmet sağlama toostart görünmüyor](#provisioning-service-does-not-appear-to-start)
* [Yapılandırma çalışmıyor tooapp kimlik bilgileri nedeniyle kaydedilemiyor.](#can’t-save-configuration-due-to-app-credentials-not-working)
* [Atanmış olan olsa bile kullanıcılar "atlanacak" ve sağlanan değil, denetim günlüklerini söyleyin](#audit-logs-say-users-are-skipped-and-not-provisioned-even-though-they-are-assigned)

## <a name="provisioning-service-does-not-appear-toostart"></a>Hizmet sağlama toostart görünmüyor

Merhaba ayarlarsanız **sağlama durumu** toobe **üzerinde** hello içinde **Azure Active Directory &gt; Kurumsal uygulamaları &gt; \[Uygulamaadı\] &gt;Sağlama** hello Azure portalı bölümü. Ancak sonraki yeniden yükler sonra diğer bir durum ayrıntıları bu sayfada gösterilir. Merhaba hizmeti çalışıyor ancak bir ilk eşitleme henüz tamamlanmadı olasıdır. Merhaba denetleyin **denetim günlüklerini** toodetermine açıklanan hangi işlemleri hello hizmetin çalıştığını ve herhangi bir hata olup olmadığını.

>[!NOTE]
>Bir başlangıç eşitlemesi herhangi bir yere hello boyutunu hello Azure AD dizini ve hello sayısı, kullanıcı sağlama kapsamında bağlı olarak 20 dakika tooseveral saat sürebilir. Sonraki eşitlemeler hello ilk eşitleme sonra daha hızlı olması hizmet sağlama hello sonraki eşitlemeler performansını iyileştirme hello ilk eşitleme sonrasında her iki sistemle hello durumunu temsil filigranlar depolar.
>
>

## <a name="cant-save-configuration-due-tooapp-credentials-not-working"></a>Yapılandırma çalışmıyor tooapp kimlik bilgileri nedeniyle kaydedilemiyor.

Sağlama toowork için sırayla Azure AD tooconnect tooa kullanıcı yönetimi, uygulama tarafından sağlanan API izin geçerli kimlik bilgileri gerektirir. Bu kimlik bilgileri çalışmıyor ya da bunlar wat bilmiyorsanız, daha önce açıklanan bu uygulamasını kurup hello Öğreticisi gözden geçirin.

## <a name="audit-logs-say-users-are-skipped-and-not-provisioned-even-though-they-are-assigned"></a>Denetim günlüklerini kullanıcılar atlanacak ve atanmış olan olsa bile sağlanan değil söyleyin

"Hello denetim günlükleri atlandı gibi" kullanıcı görüntülenir çok önemli tooread hello hello günlük iletisi toodetermine hello neden ayrıntılarında genişletilmiş olur. Ortak nedenleri ve çözümleri aşağıda verilmiştir:

-   **Bir kapsam filtresi yapılandırılmış** **filtrelemesi hello kullanıcı bir öznitelik değerini temel**. Kapsam belirleme filtreleri ile ilgili daha fazla bilgi için bkz: <https://docs.microsoft.com/azure/active-directory/active-directory-saas-scoping-filters>.

-   **Merhaba kullanıcı "etkili bir şekilde alınarak" dir.** Bu belirli bir hata iletisi görürseniz, Azure AD'de depolanan başlangıç kullanıcı atama kaydı ile ilgili bir sorun olduğundan değildir. toofix Bu sorun, atamayı hello uygulamadan kullanıcı (veya grubu) hello ve tekrar yeniden atayın. Atama hakkında daha fazla bilgi için bkz: <https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal>.

-   **Gerekli bir öznitelik eksik veya bir kullanıcı için doldurulan değil.** Sağlama yukarı ayarı tooreview kullanırken önemli şey tooconsider hello öznitelik eşlemelerini ve hangi kullanıcı (veya grubu) özellikleri akışı Azure AD toohello uygulamasından tanımlamak iş akışları ve yapılandırın. Bu hello "eşleşen özellik" ayarı içerir kullanılan toouniquely olması tanımlamak ve eşleşen kullanıcıları/grupları hello iki sistemleri arasında. Bu önemli işlemi hakkında daha fazla bilgi için bkz: <https://docs.microsoft.com/azure/active-directory/active-directory-saas-customizing-attribute-mappings>.

   * **Öznitelik grupları için eşlemeleri:** hello sağlama grup adı ve Grup ayrıntıları toplama toohello üyeleri, bazı uygulamalar için destekleniyorsa. Etkinleştirmek veya bu işlevi etkinleştirmek veya hello devre dışı bırakarak devre dışı **eşleme** hello gösterilen grubu nesnelerinin **sağlama** sekmesi. Grupları sağlama etkinleştirilirse tooreview hello öznitelik eşlemelerini tooensure uygun bir alan "Eşleşen kimliği" Merhaba kullanılan emin olun. Bu olabilir hello görünen ad veya e-posta diğer adı), hello grubu ve üyelerini hello varsa sağlanması olmayan özellik eşleşen Azure AD içinde boş veya bir grup için doldurulan aynıdır.

#<a name="next-steps"></a>Sonraki adımlar
[Kullanıcı hazırlama ve sağlamayı kaldırma işlemlerini tooSaaS Azure Active Directory ile uygulamaları otomatikleştirme](active-directory-saas-app-provisioning.md)
