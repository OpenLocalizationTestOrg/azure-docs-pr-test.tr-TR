---
title: "Dile özgü şirket, oturum açma sayfasına Azure Active Directory'de markası ekleme | Microsoft Docs"
description: "Belirli bir dil şirketten eklemeyi öğrenin marka resimler ve Azure bir oturum açma sayfası metni"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: a0310d6a-aaa7-4ea0-991d-6d3135b4382a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: curtand
ms.openlocfilehash: e1fe8d855386ceec39edbc985538cdf32d78a13b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="add-language-specific-company-branding-to-your-sign-in-page-in-the-azure-active-directory"></a>Dile özgü şirket, oturum açma sayfasına Azure Active Directory'de markası ekleme
Birçok şirket, karışıklığı önlemek için yönettikleri hizmetlerde ve web sitelerinde tutarlı bir genel görünüm uygulamak ister. Azure Active Directory şirket Logonuzla ve özel renk düzenleri ile oturum açma sayfasının görünümünü özelleştirmenize olanak tanıyarak bu yeteneği sağlar. Oturum açma sayfası, Office 365 veya Azure AD kimlik sağlayıcınız olarak kullanan diğer web tabanlı uygulamalar için oturum açtığınızda görüntülenen sayfadır. Kimlik bilgilerinizi girmek için bu sayfayı ile etkileşim.

## <a name="customizing-the-sign-in-page-for-another-language"></a>Başka bir dil için oturum açma sayfasını özelleştirme
Yalnızca, özel bir oturum açma sayfasında açıklandığı gibi oluşturduysanız, özel oturum açma sayfasına dile özgü öğeleri ekleyebilirsiniz [şirket markası, oturum açma sayfasına ekleme](active-directory-branding-custom-signon-azure-portal.md). Dizin başına bir oturum açma sayfası özelleştirilebilir öğeler varsayılan kümesiyle yapılandırabilirsiniz. Sayfa öğeleri varsayılan kümesini yapılandırdıktan sonra farklı yerel ayarlar için daha fazla sürüm yapılandırabilirsiniz. Ayrıca, çeşitli öğeleri karıştırabilir ve eşleştirebilirsiniz. Örneğin, olabilir:

* Varsayılan oluşturma **oturum açma sayfası görüntü** tüm kültürler için ardından oluşturduğunuz belirli sürümler İngilizce ve Fransızca için. Tarayıcılarınızı bu iki dilden birine ayarladığınızda, varsayılan çizim için tüm diğer dillere görüntülenirken dile özgü görüntüsü görünür.
* Kuruluşunuz için farklı logolar (örneğin, Japonca veya İbranice sürümler) yapılandırabilirsiniz.

Dil Varyasyon sayısını düşük bakım ve performans nedenleriyle tutmanızı öneririz.

**Şirket markası dizininize eklemek için:**

1. Oturum [Azure portal](https://portal.azure.com) dizini için genel yönetici olan bir hesapla.
2. Seçin **daha fazla hizmet**, girin **kullanıcılar ve gruplar** metin kutusuna ve ardından **Enter**.

   ![Açılış kullanıcı yönetimi](./media/active-directory-branding-localize-azure-portal/user-management.png)
3. Üzerinde **kullanıcılar ve gruplar** dikey penceresinde, select **şirket markası**.
4. Üzerinde **kullanıcılar ve gruplar - şirket markası** dikey penceresinde, select **dil eklemek** komutu.

    ![Dile özgü marka öğeleri ekleme](./media/active-directory-branding-localize-azure-portal/add-language.png)
5. Özelleştirmek istediğiniz öğeleri değiştirin. Tüm öğeler isteğe bağlıdır.
6. **Kaydet** düğmesine tıklayın.

Bunu görünmesi marka oturum açma sayfasına yapılan değişiklikler bir saate kadar sürebilir.

## <a name="next-steps"></a>Sonraki adımlar
[Şirket, oturum açma sayfasına markası ekleme](active-directory-branding-custom-signon-azure-portal.md)
