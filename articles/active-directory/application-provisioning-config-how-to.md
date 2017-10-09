---
title: "Azure AD tooan galeri uygulama sağlama aaaHow tooconfigure kullanıcı | Microsoft Docs"
description: "Nasıl hızlı sağlama ve zaten hello Azure AD uygulama galerisinde listelenen tooapplications etkinleştirmektir zengin bir kullanıcı hesabı yapılandırabilirsiniz"
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
ms.openlocfilehash: 2c28e59a3ac8f221ed93b2f6b0b1221f7604af23
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-user-provisioning-tooan-azure-ad-gallery-application"></a>Nasıl tooconfigure kullanıcı tooan Azure AD galeri uygulama sağlama

*Kullanıcı hesabı sağlama* oluşturma, güncelleştirme ve/veya bir uygulamanın yerel kullanıcı profili deposundaki kullanıcı hesabı kayıtlarını devre dışı bırakma, hello işlemidir. Çoğu Bulut ve SaaS uygulamaları hello kullanıcıların rol ve izinler kendi yerel kullanıcı profili deposunda saklar ve bu tür bir kullanıcı kaydı yerel depolarındaki varlığını olduğundan *gerekli* tek oturum açma ve erişim toowork için.

Hello Azure portal, hello **sağlama** hangi sağlama modları bu uygulama için desteklenen bir kuruluş uygulama görüntüler için hello sol gezinti bölmesinde sekmesinde. Bu iki değerden biri olabilir:

## <a name="configuring-an-application-for-manual-provisioning"></a>El ile sağlama için uygulamayı yapılandırma

*El ile* sağlama anlamına gelir kullanıcı hesaplarını bu uygulama tarafından sağlanan hello yöntemleri kullanarak el ile oluşturulması gerekir. Bu uygulama için bir yönetim portalı oturum açma ve bir web tabanlı kullanıcı arabirimini kullanarak kullanıcı ekleme anlamına gelebilir. Veya uygulama tarafından sağlanan bir mekanizma kullanarak, kullanıcı hesabı ayrıntı elektronik karşıya. Merhaba uygulaması veya kişi hello uygulama geliştiricisi toodetermine wat mekanizmaları kullanılabilir olması koşuluyla hello belgelerine başvurun.

El ile hello yalnızca modu gösterilir belirli bir uygulama için bağlayıcı sağlama hiçbir otomatik Azure AD için başlangıç uygulaması henüz oluşturulduğunu anlamına gelir. Veya hello uygulama değil destek hello önkoşul kullanıcı yönetimi API hangi toobuild bağlı bir otomatik sağlama Bağlayıcısı mu anlamına gelir.

Toorequest desteği için belirli bir uygulamanın otomatik sağlamayı istiyorsanız, bir isteğiyle doldurabilir <http://aka.ms/aadapprequest>.

## <a name="configuring-an-application-for-automatic-provisioning"></a>Otomatik sağlama için uygulamayı yapılandırma

*Otomatik* bağlayıcı sağlama Azure AD bu uygulama için geliştirilmiştir anlamına gelir. Azure AD hizmeti ve nasıl çalıştığı, sağlama hello hakkında daha fazla bilgi için bkz: [otomatikleştirmek kullanıcı hazırlama ve sağlamayı kaldırma işlemlerini tooSaaS Azure Active Directory ile uygulamaları](https://docs.microsoft.com/azure/active-directory/active-directory-saas-app-provisioning).

Tooprovision belirli kullanıcılar ve gruplar tooan uygulama nasıl görürüm hakkında daha fazla bilgi için [kullanıcı hesabı Kurumsal uygulamaları için sağlama yönetme](https://docs.microsoft.com/azure/active-directory/active-directory-enterprise-apps-manage-provisioning).

Gerçek adımları gerekli tooenable hello ve yapılandırma otomatik sağlamayı hello uygulamaya bağlı olarak değişir.

>[!NOTE]
>Uygulamanız için sağlama yukarı Kurulum öğretici belirli toosetting hello ve bu adımları tooconfigure hello uygulama ve Azure AD toocreate sağlama bağlantı hello bularak başlamanız gerekir. 
>
>

Uygulama öğreticileri bulunabilir [nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları](https://docs.microsoft.com/azure/active-directory/active-directory-saas-tutorial-list).

Sağlama yukarı ayarı tooreview kullanırken önemli şey tooconsider hello öznitelik eşlemelerini ve hangi kullanıcı (veya grubu) özellikleri akışı Azure AD toohello uygulamasından tanımlamak iş akışları ve yapılandırın. Bu hello "eşleşen özellik" ayarı içerir kullanılan toouniquely olması tanımlamak ve eşleşen kullanıcıları/grupları hello iki sistemleri arasında. Bu önemli işlemi hakkında daha fazla bilgi için.

## <a name="next-steps"></a>Sonraki adımlar
[Kullanıcı Azure Active Directory'de SaaS uygulamaları için öznitelik eşlemelerini hazırlama özelleştirme](https://docs.microsoft.com/azure/active-directory/active-directory-saas-customizing-attribute-mappings)

