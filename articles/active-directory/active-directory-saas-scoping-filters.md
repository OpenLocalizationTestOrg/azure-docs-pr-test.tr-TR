---
title: Kapsam belirleme filtreleri ile aaaProvisioning uygulamalar | Microsoft Docs
description: "Toouse kapsamı tooprevent nesneleri nesneyi iş gereksinimlerinizi karşılamadığı, aslında sağlanacak otomatik kullanıcı sağlamayı destekleyen uygulamaları nasıl filtreler hakkında bilgi edinin."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: bcfbda74-e4d4-4859-83bc-06b104df3918
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: markvi
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f0299390dc3fdb70aa9d271e835069a08827d635
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="attribute-based-application-provisioning-with-scoping-filters"></a>Kapsam belirleme filtreleri ile öznitelik tabanlı uygulama sağlama
Merhaba amacı, bu bölümde, hangi kullanıcıların belirlemek toodefine öznitelik tabanlı kurallar toouse kapsamı nasıl filtreler tooexplain toohello uygulama sağlanan ' dir.

## <a name="clauses-and-scope-groups"></a>Yan tümceleri ve kapsam grupları
![Kapsamı filtresi][1] 

Bir veya daha fazla kapsam filtreleri tanımlanmış **Kapsam grupları**, her bir veya daha fazla tut **yan tümceleri**. Belirli kapsam grubu için toosee hello yan tümceleri genişletin, hello ok toohello sol hello grup adının tıklayarak.

A **yan tümcesi** toopass her kullanıcının öznitelikleri değerlendirerek kapsamı filtresi hello aracılığıyla izin verilen kullanıcıları belirler. Örneğin, yalnızca New York kullanıcıların hello uygulamasına sağlanan şekilde bir kullanıcının 'state' özniteliği eşit New York, gerektiren bir yan tümce olabilir.

![Ölçüm grubu adı][2] 

Her **kapsam grubu** bir zorunlu ile başlayan **yan tümcesi**, yukarıdaki hello ekran görüntüsünde gösterildiği gibi. Yalnızca durumları bu yan tümcesi, kapsam, filtreler tarafından değerlendirilir önce hello kullanıcının ilk toohello uygulama atanması gerekir. Bu yan tümce silinmiş veya değiştirilmiş.

Merhaba uygun düğmesine basarak yeni yan tümcesi ya da Yeni Kapsam grupları ekleyebilirsiniz. Her bir kapsam grubu düzenleyerek bir ad verin, **kapsam grup adı** özelliği.

## <a name="how-scoping-filters-are-evaluated"></a>Kapsam belirleme filtreleri nasıl değerlendirilir
Bu kullanıcının erişim toohello uygulama hak varsa sağlama işlemi sırasında biz kapsam, filtreler toodetermine karşı atanan her kullanıcı sınayın. Her yan tümcesinin filtrelenmelidir hello kullanıcı tooavoid geçirilmesi gereken bir test olarak düşünebilirsiniz. 

Tanımlanan birden çok kapsam gruplarınız varsa, her kullanıcı en az biri tooaccess Merhaba uygulaması geçmesi gerekir. Her bir kapsam grubunda ancak hello kullanıcı her yan tümcesi toopass bu belirli kapsam grubu geçmesi gerekir. 

Diğer bir deyişle, kapsam grubu olarak düşünebilirsiniz veya birlikte and'lenir ve bunların içindeki hello tümceleri olarak düşünebilirsiniz ve birlikte and'lenir. Örneğin, aşağıdaki filtre kapsamı hello göz önünde bulundurun:

![Ölçüm grubu adı][3]  

Filtre kapsamı toothis göre kullanıcıların hello aşağıdaki getirmelidir ölçütleri, sağlanan toobe:

1. Toohello uygulama atanmaları gerekir.
2. Merhaba mühendislik departmanı çalışmanız gerekir
3. İş olmalıdır San Francisco veya Kanada.

## <a name="related-articles"></a>İlgili makaleler
* [Azure Active Directory'de Uygulama Yönetimi için Makale Dizini](active-directory-apps-index.md)
* [Kullanıcı hazırlama ve sağlamayı kaldırma işlemlerini tooSaaS uygulamaları otomatikleştirme](active-directory-saas-app-provisioning.md)
* [Kullanıcı sağlama öznitelik eşlemelerini özelleştirme](active-directory-saas-customizing-attribute-mappings.md)
* [Özellik eşlemeleri için ifade yazma](active-directory-saas-writing-expressions-for-attribute-mappings.md)
* [Hesap sağlama bildirimleri](active-directory-saas-account-provisioning-notifications.md)
* [SCIM'yi tooenable otomatik kullanıcıların ve grupların Azure Active Directory tooapplications sağlama kullanma](active-directory-scim-provisioning.md)
* [İlgili nasıl öğreticiler listesi tooIntegrate SaaS uygulamaları](active-directory-saas-tutorial-list.md)

<!--Image references-->
[1]: ./media/active-directory-saas-scoping-filters/ic782811.png
[2]: ./media/active-directory-saas-scoping-filters/ic782812.png
[3]: ./media/active-directory-saas-scoping-filters/ic782813.png
