---
title: "bir Azure Active Directory B2B işbirliği kullanıcının aaaProperties | Microsoft Docs"
description: "Azure Active Directory B2B işbirliği kullanıcı özellikleri yapılandırılabilir"
services: active-directory
documentationcenter: 
author: sasubram
manager: femila
editor: 
tags: 
ms.assetid: 
ms.service: active-directory
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: identity
ms.date: 05/25/2017
ms.author: sasubram
ms.openlocfilehash: 78709f64430ed4c14eadf4dc257f175c24698c5e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="properties-of-an-azure-active-directory-b2b-collaboration-user"></a>Bir Azure Active Directory B2B işbirliği kullanıcının özelliklerini

Bir Azure Active Directory (Azure AD) işletmeden işletmeye (B2B) işbirliği UserType sahip bir kullanıcı kullanıcıdır konuk =. Bu Konuk kullanıcı genellikle bir iş ortağı kuruluştan ve dizin, varsayılan olarak davet hello ayrıcalıkları sınırlıdır.

Kuruluşunuzun gereksinimlerini davet hello bağlı olarak, bir Azure AD B2B işbirliği kullanıcı hesabı durumları aşağıdaki hello biri olabilir:

- Durum 1: Azure AD dış örneğinde bağlantılı ve Konuk kullanıcı kuruluş davet hello olarak gösterilir. Bu durumda, hello B2B davet toohello Kiracı ait bir Azure AD hesabı kullanarak oturum açtığında. Azure AD Hello ortağı kuruluşu kullanmıyorsa, Azure AD'de hello Konuk kullanıcı hala oluşturulur. kullanıcıların davet almak ve Azure AD, e-posta adreslerini doğrular Hello gereksinimleri verilmiştir. Bu düzenlemenin, tam zamanında (JIT) Kiracı veya "viral" Kiracı olarak da bilinir.

- Durum 2: bir Microsoft hesabı bağlantılı ve Konuk kullanıcı hello konak kuruluş olarak gösterilir. Bu durumda, hello Konuk kullanıcı bir Microsoft hesabıyla oturum açar. Merhaba davet kullanıcının sosyal kimliğini (google.com veya benzer), bir Microsoft hesabı olmayan oluşturulur bir Microsoft hesabı olarak teklif kullanım sırasında.

- Durum 3: hello konak kuruluşun şirket içi Active Directory'de bağlantılı ve hello konak kuruluşunuzun Azure ile eşitlenen AD. Bu yayın sırasında hello bulutta PowerShell toomanually değişiklik hello böyle kullanıcıların UserType kullanmanız gerekir.

- Durum 4: ana bilgisayar kuruluşunuzun Azure ana bilgisayara bağlı AD UserType ile = Konuk ve hello konak kuruluş yönetir kimlik bilgileri.

  ![görüntüleme hello davet eden'ın baş harfleri](media/active-directory-b2b-user-properties/redemption-diagram.png)


Şimdi bir Azure AD B2B işbirliği kullanıcı durumu 1'de nasıl Azure AD'de göründüğünü görelim.

### <a name="before-invitation-redemption"></a>Davet kullanım önce

![Teklif kullanım önce](media/active-directory-b2b-user-properties/before-redemption.png)

### <a name="after-invitation-redemption"></a>Sonra davet kullanım

![Teklif kullanım sonra](media/active-directory-b2b-user-properties/after-redemption.png)

## <a name="key-properties-of-hello-azure-ad-b2b-collaboration-user"></a>Hello Azure AD B2B işbirliği kullanıcı temel özellikleri
### <a name="usertype"></a>UserType
Bu özellik hello kullanıcı toohello konak kiralama hello ilişkisini gösterir. Bu özellik, iki değerlere sahip olabilir:
- Üye: Bu değer hello konak kuruluşun çalışan ve kullanıcı hello kuruluşunuzun Bordro olarak gösterir. Örneğin, bu kullanıcı toohave erişim yalnızca toointernal siteleri bekliyor. Bu kullanıcı dış bir ortak çalışanı kabul edilir değil.

- Konuk: Bu değer bir dış ortak çalışanı, iş ortağı, müşteri veya benzer kullanıcı gibi iç toohello şirket kabul olmayan bir kullanıcıyı gösterir. Böyle bir kullanıcı bir CEO'nun iç notları beklenen tooreceive olması veya şirket, örneğin avantajların yanı sıra olmayacaktır.

  > [!NOTE]
  > Merhaba UserType hiçbir ilişkisi toohow hello kullanıcı işaretleri, hello dizin rolünü hello kullanıcı, vb. vardır. Bu özellik yalnızca hello kullanıcının ilişki toohello konak kuruluş gösterir ve hello kuruluşunuzun bu özellikte bağımlı tooenforce ilkeleri olanak sağlar.

### <a name="source"></a>Kaynak
Bu özellik, nasıl hello kullanıcı oturum açtığında gösterir.

- Kullanıcı Davet: Bu kullanıcı davet edilen, ancak henüz bir davet kullanılan değil.

- Dış Active Directory: Bu kullanıcı bir dış kuruluşta bağlantılı ve diğer kuruluş toohello ait bir Azure AD hesabı kullanarak kimliğini doğrular. Bu tür bir oturum açma tooState 1 karşılık gelir.

- Microsoft hesabı: Bu kullanıcı bir Microsoft hesabı bağlantılı ve bir Microsoft hesabı kullanarak kimliğini doğrular. Bu tür bir oturum açma tooState 2 karşılık gelir.

- Windows Server Active Directory: Bu kullanıcı şirket içi Active Directory içinden toothis kuruluş ait oturum. Bu tür bir oturum açma tooState 3 karşılık gelir.

- Azure Active Directory: Toothis kuruluş ait bir Azure AD hesabı kullanarak bu kullanıcının kimliğini doğrular. Bu tür bir oturum açma tooState 4 karşılık gelir.
  > [!NOTE]
  > Kaynak ve UserType bağımsız özelliklerdir. Kaynak değerini belirli bir değeri için UserType göstermez.

## <a name="can-azure-ad-b2b-users-be-added-as-members-instead-of-guests"></a>Azure AD B2B kullanıcılar konuklar yerine üye olarak eklenebilir mi?
Genellikle, bir Azure AD B2B kullanıcı ve Konuk kullanıcı eşanlamlıdır. Bu nedenle, bir Azure AD B2B işbirliği kullanıcı UserType olan bir kullanıcı olarak eklenen varsayılan olarak konuk =. Ancak, bazı durumlarda, daha büyük bir kuruluş toowhich hello konak kuruluşunuz üyesi aynı zamanda ait hello ortağı kuruluşu olur. Bu durumda, hello konak kuruluş tootreat kullanıcıların hello ortağı kuruluştaki konuklar yerine üye olarak isteyebilirsiniz. Merhaba iş ortağı kuruluş toohello konak kuruluştan bir üye olarak kullanıcı davet veya Hello Azure AD B2B davet Manager API'leri tooadd kullanın.

## <a name="filter-for-guest-users-in-hello-directory"></a>Konuk kullanıcılar hello dizininde Filtrele

![Filtre Konuk kullanıcılar](media/active-directory-b2b-user-properties/filter-guest-users.png)

## <a name="convert-usertype"></a>UserType Dönüştür
Şu anda, PowerShell kullanarak kullanıcıların tooconvert UserType üye tooGuest ve tam tersini mümkündür. Ancak, hello UserType özelliği toorepresent hello kullanıcının ilişki toohello kuruluş varsayılır. Bu nedenle, yalnızca hello kullanıcı toohello kuruluşun hello ilişkisi değişirse hello bu özelliğin değerini değiştirmeniz gerekir. Merhaba kullanıcı Hello ilişkisi değişirse hello kullanıcı asıl adı (UPN) değiştirmeniz gerekir gibi sorunlar, ilgilenilmesi gerekir? Merhaba kullanıcı toohave erişim toohello devam etmesi gerektiğini aynı kaynakları? Bir posta kutusu atanması gerekir? Bu nedenle, atomik aktivite olarak PowerShell kullanarak hello UserType değiştirilmesi önerilmez. PowerShell kullanarak bu özellik sabit hale gelmesi durumu, ayrıca, bu değeri bir bağımlılık alma önermiyoruz.

## <a name="remove-guest-user-limitations"></a>Konuk kullanıcı kısıtlama Kaldır
Konuk kullanıcılar yüksek ayrıcalıkları toogive istediğiniz durumlar olabilir. Konuk kullanıcı tooany rolü ekleyip bile hello varsayılan Konuk kullanıcı kısıtlamaları hello dizin toogive aynı üye olarak ayrıcalıkları kullanıcı hello kaldırabilirsiniz.

Olası tooturn hello varsayılan Konuk kullanıcı kısıtlamaları devre dışı, böylelikle hello şirket dizinde Konuk kullanıcıya verilen hello aynı izinlere sahip bir üye kullanıcı.

![Konuk kullanıcı kısıtlama Kaldır](media/active-directory-b2b-user-properties/remove-guest-limitations.png)

## <a name="next-steps"></a>Sonraki adımlar

Azure AD B2B işbirliği ile ilgili diğer makalelerimize göz atın:

* [Azure AD B2B işbirliği nedir?](active-directory-b2b-what-is-azure-ad-b2b.md)
* [B2B işbirliği kullanıcı tooa rolü ekleme](active-directory-b2b-add-guest-to-role.md)
* [B2B işbirliği davetleri temsilci seçme](active-directory-b2b-delegate-invitations.md)
* [B2B işbirliği kullanıcı Denetim ve Raporlama](active-directory-b2b-auditing-and-reporting.md)
* [Dinamik gruplar ve B2B işbirliği](active-directory-b2b-dynamic-groups.md)
* [B2B işbirliği kodu ve PowerShell örnekleri](active-directory-b2b-code-samples.md)
* [SaaS uygulamaları B2B işbirliği için yapılandırma](active-directory-b2b-configure-saas-apps.md)
* [B2B işbirliği kullanıcı belirteçleri](active-directory-b2b-user-token.md)
* [B2B işbirliği kullanıcı taleplerini eşleme](active-directory-b2b-claims-mapping.md)
* [Office 365 dış paylaşım](active-directory-b2b-o365-external-user.md)
* [B2B işbirliği geçerli sınırlamalar](active-directory-b2b-current-limitations.md)
