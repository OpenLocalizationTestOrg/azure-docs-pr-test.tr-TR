---
title: "belirli bir kullanıcı mümkün tooaccess uygulamanın ne zaman olacağını çıkışı aaaFind | Microsoft Docs"
description: "Nasıl oldukça önemli bir kullanıcı mümkün tooaccess uygulamanın ne zaman olması çıkışı toofind kullanıcı Azure AD ile sağlamak için yapılandırdığınız"
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
ms.openlocfilehash: bb9520499dcc8bbbe6fae05c5238c8852815ea0a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="find-out-when-a-specific-user-will-be-able-tooaccess-an-application"></a>Belirli bir kullanıcı mümkün tooaccess bir uygulamayı kullanırken öğrenin
Bir uygulama ile otomatik kullanıcı sağlamayı kullanırken, Azure AD uygulama sağlama ve güncelleştirme kullanıcı hesapları gibi şeyleri temel alınarak otomatik olarak [kullanıcı ve grup atama](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal) genellikle her 10 dakikada bir düzenli olarak zamanlanan saat aralığında.

## <a name="how-long-does-it-take"></a>Ne kadar sürer?

Merhaba süresini sağlanan verilen kullanıcı toobe için çoğunlukla desteklemediğini ilk bir "tam" eşitleme zaten oluştu üzerinde bağlıdır.

Merhaba ilk eşitleme Azure AD arasında ve bir uygulamayı herhangi bir yere hello boyutunu hello Azure AD dizini ve hello sayısı, kullanıcı sağlama kapsamında bağlı olarak 20 dakika tooseveral saat sürebilir. 

Hizmet sağlama hello sonraki eşitlemeler performansını iyileştirme hello ilk eşitleme sonrasında her iki sistemle hello durumunu temsil filigranlar depolar hello ilk eşitleme sonrasında sonraki eşitlemeler (örn. 10 dakika içinde), daha hızlı olması.

## <a name="how-toocheck-hello-status-of-a-user"></a>Nasıl toocheck hello kullanıcı durumu

Seçili bir kullanıcı için toosee hello sağlama durumu hello Azure AD'de denetim günlüklerini inceleyin.

Denetim günlüklerini sağlama hello hello Azure portalında, hello erişilebilir **Azure Active Directory &gt; Kurumsal uygulamaları &gt; \[uygulama adı\] &gt; denetim günlükleri**sekmesi. Filtre hello hello üzerinde oturum **hesap sağlama** kategori tooonly olayları bu uygulama için sağlama hello bakın. "Hello öznitelik eşlemelerini kendileri için yapılandırılan hello eşleşen ID" temel alarak kullanıcılara arayabilirsiniz. 

Örneğin hello "kullanıcı asıl adı" veya "Merhaba Azure AD tarafında özniteliği eşleşen hello olarak e-posta adresi" yapılandırılmış ve değil sağlama hello kullanıcı değerine sahip "audrey@contoso.com", için arama hello denetim günlüklerini"audrey@contoso.com" ve gözden geçirin girişleri döndürdü.

Denetim sağlama hello tüm hello hizmeti sağlama hello tarafından gerçekleştirilen işlemler kayıt günlüklerini de dahil olmak üzere:

* Azure AD sağlama kapsamında atanan kullanıcılar için sorgulama
* Merhaba hedef uygulama kullanıcılarla hello varlığı sorgulama
* Merhaba sistem arasında Hello kullanıcı nesneleri karşılaştırma
* Ekleme, güncelleştirme veya hello karşılaştırma üzerine dayalı hello hedef sistemdeki hello kullanıcı hesabı devre dışı bırakma

## <a name="next-steps"></a>Sonraki adımlar
[Kullanıcı hazırlama ve sağlamayı kaldırma işlemlerini tooSaaS Azure Active Directory ile uygulamaları otomatikleştirmek](https://docs.microsoft.com/azure/active-directory/active-directory-saas-app-provisioning)''
