---
title: "Kapsam belirleme filtreleri ile uygulamalar sağlama | Microsoft Docs"
description: "Nesneleri nesneyi iş gereksinimlerinizi karşılamadığı, aslında sağlanacak otomatik kullanıcı sağlamayı destekleyen uygulamalarda önlemek için kapsam filtreleri kullanmayı öğrenin."
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
ms.openlocfilehash: 109635052e2ded33831b050eb12d50745944091b
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="attribute-based-application-provisioning-with-scoping-filters"></a>Kapsam belirleme filtreleri ile öznitelik tabanlı uygulama sağlama
Bu bölümün amacı, kapsam filtreleri hangi kullanıcıların uygulamayı sağlanan belirlemek öznitelik tabanlı kurallar tanımlamak için nasıl kullanılacağını açıklamaktadır sağlamaktır.

## <a name="clauses-and-scope-groups"></a>Yan tümceleri ve kapsam grupları
![Kapsamı filtresi][1] 

Bir veya daha fazla kapsam filtreleri tanımlanmış **Kapsam grupları**, her bir veya daha fazla tut **yan tümceleri**. Belirli kapsam grubu için yan tümceleri görmek için grup adının solundaki oka tıklayarak genişletin.

A **yan tümcesi** her kullanıcının öznitelikleri değerlendirerek kapsam filtresinden geçmesine izin verilen kullanıcıları belirler. Örneğin, yalnızca New York kullanıcıların uygulamaya sağlanan şekilde bir kullanıcının 'state' özniteliği, New York eşit gerektiren bir yan tümce olabilir.

![Ölçüm grubu adı][2] 

Her **kapsam grubu** bir zorunlu ile başlayan **yan tümcesi**, yukarıdaki ekran görüntüsünde gösterildiği gibi. Yalnızca durumları bu yan tümcesi, kapsam, filtreler tarafından değerlendirilir önce kullanıcının ilk uygulamaya atanması gerekir. Bu yan tümce silinmiş veya değiştirilmiş.

Uygun düğmesine basarak yeni yan tümcesi ya da Yeni Kapsam grupları ekleyebilirsiniz. Her bir kapsam grubu düzenleyerek bir ad verin, **kapsam grup adı** özelliği.

## <a name="how-scoping-filters-are-evaluated"></a>Kapsam belirleme filtreleri nasıl değerlendirilir
Sağlama işlemi sırasında Biz bu kullanıcının uygulamaya erişim hak varsa belirlemek için her atanan kullanıcı kapsam filtrelerinizi karşı test edin. Her yan tümcesi kullanıcının filtrelenmelidir önlemek sırayla geçirilmelidir bir test olarak düşünebilirsiniz. 

Tanımlanan birden çok kapsam gruplarınız varsa, her kullanıcının uygulamaya erişim için en az biri geçmesi gerekir. Her bir kapsam grubunda ancak, bu belirli kapsam grubu geçirmek için her yan tümcesi kullanıcı geçmesi gerekir. 

Diğer bir deyişle, kapsam grubu olarak düşünebilirsiniz veya birlikte and'lenir ve olarak yan tümceleri içinde bunları düşünebilirsiniz ve birlikte and'lenir. Örneğin, aşağıdaki ölçüm filtre göz önünde bulundurun:

![Ölçüm grubu adı][3]  

Bu kapsam filtresi göre kullanıcılar sağlanacak aşağıdaki ölçütleri karşılamalıdır:

1. Uygulamaya atanmaları gerekir.
2. Mühendislik departmanında çalışmanız gerekir
3. İş olmalıdır San Francisco veya Kanada.

## <a name="related-articles"></a>İlgili makaleler
* [Azure Active Directory'de Uygulama Yönetimi için Makale Dizini](active-directory-apps-index.md)
* [Sağlama ve SaaS uygulamaları etkinleştirmektir kullanıcı otomatikleştirme](active-directory-saas-app-provisioning.md)
* [Kullanıcı sağlama öznitelik eşlemelerini özelleştirme](active-directory-saas-customizing-attribute-mappings.md)
* [Özellik eşlemeleri için ifade yazma](active-directory-saas-writing-expressions-for-attribute-mappings.md)
* [Hesap sağlama bildirimleri](active-directory-saas-account-provisioning-notifications.md)
* [Kullanıcıların ve grupların Azure Active Directory'den uygulamalara otomatik olarak hazırlanmasını etkinleştirmek için SCIM'yi kullanma](active-directory-scim-provisioning.md)
* [SaaS uygulamalarını tümleştirme ile nasıl öğreticiler listesi](active-directory-saas-tutorial-list.md)

<!--Image references-->
[1]: ./media/active-directory-saas-scoping-filters/ic782811.png
[2]: ./media/active-directory-saas-scoping-filters/ic782812.png
[3]: ./media/active-directory-saas-scoping-filters/ic782813.png
