---
title: "Azure AD öznitelik eşlemelerini aaaCustomizing | Microsoft Docs"
description: "Hangi öznitelik eşlemelerini Azure Active Directory'de SaaS uygulamaları için nasıl bunları tooaddress işletmenizin değiştirebilirsiniz olduğunu öğrenin gerekiyor."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 549e0b8c-87ce-4c9b-b487-b7bf0155dc77
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/17/2017
ms.author: markvi
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 14db5303f06fc8df3b07a0a8b75713312e71bbfd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="customizing-user-provisioning-attribute-mappings-for-saas-applications-in-azure-active-directory"></a>Kullanıcı Azure Active Directory'de SaaS uygulamaları için öznitelik eşlemelerini hazırlama özelleştirme
Microsoft Azure AD Kullanıcı hazırlama Salesforce, Google Apps ve diğerleri gibi toothird taraf SaaS uygulamaları için destek sağlar. Etkin bir üçüncü taraf SaaS uygulaması için sağlama kullanıcınız varsa, öznitelik değerleri "özellik eşlemesi." adlı bir yapılandırma biçiminde hello Azure Yönetim Portalı denetler

Önceden yapılandırılmış öznitelik eşlemelerini Azure AD kullanıcı ve her SaaS uygulamanın kullanıcı nesneleri arasında birtakım yoktur. Bazı uygulamalar, diğer grupların veya kişilerin gibi nesne türlerini yönetin. <br> 
 Merhaba varsayılan öznitelik eşlemelerini tooyour iş gereksinimlerinize göre özelleştirebilirsiniz. Bu anlamına gelir, değiştirin veya varolan öznitelik eşlemelerini silebilir veya yeni öznitelik eşlemelerini oluşturun.

Hello Azure AD Portalı'nda tıklatarak bu özellik erişebilirsiniz bir **eşlemeleri** yapılandırmada **sağlama** hello içinde **Yönet** bölümünü bir  **Kuruluş uygulaması**.


![Salesforce][5] 

Tıklatarak bir **eşlemeleri** yapılandırma, ilgili hello açılır **eşleme özniteliği** dikey.  
Bir SaaS uygulaması toofunction tarafından doğru şekilde gerekli öznitelik eşlemelerini vardır. Gerekli öznitelikler için hello **silmek** özelliği kullanılamıyor.


![Salesforce][6]  

Merhaba yukarıdaki örnekte, bu hello görebilirsiniz **kullanıcıadı** Salesforce içinde yönetilen bir nesnenin öznitelik hello ile doldurulur **userPrincipalName** hello değerini bağlı Azure Active Directory nesnesi.

Varolan özelleştirebilirsiniz **öznitelik eşlemelerini** eşleme tıklatarak. Merhaba açılır **öznitelik Düzenle** dikey.

![Salesforce][7]  


  

## <a name="understanding-attribute-mapping-types"></a>Öznitelik eşleme türlerini anlama
Öznitelik eşlemelerini ile öznitelikleri bir üçüncü taraf SaaS uygulamasına nasıl doldurulur denetler. Desteklenen dört farklı eşleme türleri şunlardır:

* **Doğrudan** – hello target özniteliği, Azure AD'de hello bağlantılı nesne özniteliği hello değeri ile doldurulur.
* **Sabit** – hello target özniteliği, belirttiğiniz için belirli bir dizeyi doldurulur.
* **İfade** -hello target özniteliği hello sonucuna göre bir betik benzeri ifadesi doldurulur. 
  Daha fazla bilgi için bkz: [Azure Active Directory'de özellik eşlemeleri için ifade yazma](active-directory-saas-writing-expressions-for-attribute-mappings.md).
* **Hiçbiri** -hello target özniteliği değişmeden değiştirilmemiş. Ancak, Hello Hedef öznitelik sürekli boşsa, belirttiğiniz hello varsayılan değeri ile doldurulur.

Toplama toothese dört temel özniteliği eşleme türlerinde, özel öznitelik eşlemelerini isteğe bağlı bir hello kavramı Destek **varsayılan** değer atama. Merhaba varsayılan değer atama hello hedef nesne ya da Azure AD'de hiçbiri bir değer varsa bir target özniteliği değeri ile doldurulur sağlar. Merhaba en yaygın tooleave bu boş bir yapılandırmadır.


## <a name="understanding-attribute-mapping-properties"></a>Öznitelik Eşleme Özellikleri Anlama

Merhaba önceki bölümde sunulan toohello öznitelik eşleme türü özelliği zaten silinmiş.
Toplama toothis özelliğinde öznitelik eşlemelerini de öznitelikleri aşağıdaki hello destekler:

- **Kaynak özniteliği** -hello kullanıcı özniteliği hello kaynak sistemden (örn: Azure Active Directory).
- **Hedef öznitelik** – hello kullanıcı özniteliği hello hedef sisteminde (örn: ServiceNow).
- **Eşleşen nesneleri bu öznitelik kullanarak** – Bu eşleme kullanılmalıdır olup olmadığına bakılmaksızın toouniquely kullanıcılar hello kaynak ve hedef sistemler arasında tanımlayın. Bu, genellikle hello userPrincipalName üzerinde ayarlanır veya posta özniteliğinin genellikle Azure AD'de bir hedef uygulama tooa kullanıcı adı alanı eşlenir.
- **Öncelik eşleşen** – birden çok öznitelikleri eşleşen ayarlanabilir. Olduğunda birden çok, bu alana göre tanımlanan hello sırayla değerlendirilir. Bir eşleşme olarak başka eşleştirme öznitelikleri değerlendirilir.
- **Bu eşleme Uygula**
    - **Her zaman** – hem kullanıcı oluşturulması bu eşleme uygulamak ve güncelleştirme eylemleri
    - **Yalnızca oluşturma sırasında** -bu eşlemenin yalnızca kullanıcı oluşturma eylemlerini uygulamak


## <a name="what-you-should-know"></a>Bilmeniz gerekenler

Microsoft Azure AD eşitleme işlemini verimli bir uygulamasını sağlar. Başlatılmış bir ortamda, bir eşitleme döngüsü sırasında yalnızca güncelleştirmeleri gerektiren nesneler işlenir. Öznitelik eşlemelerini güncelleştirme bir eşitleme döngüsü hello performans üzerinde bir etkisi vardır. Bir güncelleştirme toohello özniteliği eşleme yapılandırmasını yeniden değerlendirimiş tüm yönetilen nesneleri toobe gerektirir. Bu bir önerilen en iyi yöntem tookeep hello ardışık değişiklikleri tooyour öznitelik eşlemelerini en az sayısıdır.

## <a name="next-steps"></a>Sonraki adımlar

* [Azure Active Directory'de Uygulama Yönetimi için Makale Dizini](active-directory-apps-index.md)
* [Kullanıcı hazırlama/sağlama kaldırmayı tooSaaS uygulamaları otomatikleştirme](active-directory-saas-app-provisioning.md)
* [Özellik eşlemeleri için ifade yazma](active-directory-saas-writing-expressions-for-attribute-mappings.md)
* [Kapsam belirleme filtreleri kullanıcı sağlama](active-directory-saas-scoping-filters.md)
* [SCIM'yi tooenable otomatik kullanıcıların ve grupların Azure Active Directory tooapplications sağlama kullanma](active-directory-scim-provisioning.md)
* [Hesap sağlama bildirimleri](active-directory-saas-account-provisioning-notifications.md)
* [İlgili nasıl öğreticiler listesi tooIntegrate SaaS uygulamaları](active-directory-saas-tutorial-list.md)

<!--Image references-->
[1]: ./media/active-directory-saas-customizing-attribute-mappings/ic765497.png
[2]: ./media/active-directory-saas-customizing-attribute-mappings/ic775419.png
[3]: ./media/active-directory-saas-customizing-attribute-mappings/ic775420.png
[4]: ./media/active-directory-saas-customizing-attribute-mappings/ic775421.png
[5]: ./media/active-directory-saas-customizing-attribute-mappings/21.png
[6]: ./media/active-directory-saas-customizing-attribute-mappings/22.png
[7]: ./media/active-directory-saas-customizing-attribute-mappings/23.png

