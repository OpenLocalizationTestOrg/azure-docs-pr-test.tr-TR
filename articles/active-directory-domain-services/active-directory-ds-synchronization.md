---
title: "Azure Active Directory etki alanı Hizmetleri: Eşitleme yönetilen etki alanlarında | Microsoft Docs"
description: "Bir Azure Active Directory etki alanı Hizmetleri yönetilen etki alanında eşitleme anlama"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 57cbf436-fc1d-4bab-b991-7d25b6e987ef
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: maheshu
ms.openlocfilehash: 9be25b61823a6b031906f3576395782e73831fc4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="synchronization-in-an-azure-ad-domain-services-managed-domain"></a>Azure AD etki alanı Hizmetleri yönetilen etki alanında eşitleme
Merhaba Aşağıdaki diyagramda eşitleme Azure AD Etki Alanı Hizmetleri'nde yönetilen etki alanlarını nasıl çalıştığı gösterilmektedir.

![Azure AD Etki Alanı Hizmetleri'nde eşitleme topolojisi](./media/active-directory-domain-services-design-guide/sync-topology.png)

## <a name="synchronization-from-your-on-premises-directory-tooyour-azure-ad-tenant"></a>Şirket içi dizin tooyour Azure AD kiracınız eşitlemeden
Azure AD Connect eşitleme kullanılan toosynchronize kullanıcı hesapları, grup üyelikleri ve kimlik bilgisi karmaları tooyour Azure AD Kiracı ' dir. Kullanıcı özniteliklerini UPN hello gibi hesapları ve şirket içi SID (güvenlik tanımlayıcısı) eşitlenir. Azure AD etki alanı hizmetlerini kullanıyorsanız, NTLM ve Kerberos kimlik doğrulaması için gerekli eski kimlik bilgisi karmalarını ayrıca eşitlenmiş tooyour Azure AD kiracısı değildir.

Sonradan yazma yapılandırırsanız, Azure AD dizininizi gerçekleşen değişiklikler geri tooyour şirket içi Active Directory eşitlenir. Örneğin, Azure AD Self Servis parola değişikliği özellikleri kullanarak parolanızı değiştirirseniz, şirket içinde hello değiştirilen parola güncelleştirilir AD etki alanı.

> [!NOTE]
> Her zaman hello en son sürümünü kullanın Azure AD Connect tooensure tüm bilinen hatalar için düzeltmeler sahip.
>
>

## <a name="synchronization-from-your-azure-ad-tenant-tooyour-managed-domain"></a>Azure AD Kiracı tooyour eşitlemeden yönetilen etki alanı
Kullanıcı hesapları, grup üyelikleri ve kimlik bilgisi karmalarını, Azure AD Kiracı tooyour Azure AD etki alanı Hizmetleri yönetilen etki alanı eşitlenir. Bu eşitleme işlemi otomatik olarak yapılır. Tooconfigure, gerekmez izlemek veya bu eşitleme işlemi yönetin. Dizininizin Hello tek seferlik ilk eşitleme tamamlandıktan sonra yönetilen etki alanınızda genellikle 20 dakika içinde Azure AD toobe yapılan değişiklikleri alır yansıtılır. Bu eşitleme aralığı toopassword değişiklikleri uygular veya Azure AD içinde yapılan tooattributes değiştirir.

Merhaba eşitleme işlemi aynı zamanda bir-way/doğası gereği tek yönlüdür. Yönetilen etki alanınızı büyük ölçüde oluşturduğunuz özel OU'lar dışında salt okunurdur. Bu nedenle, değişiklikleri toouser öznitelikler, kullanıcı parolalarını veya grup üyeliklerini hello yönetilen etki alanı içinde yapamazsınız. Sonuç olarak, yönetilen etki alanı geri tooyour Azure AD kiracısı değişikliklerden birini ters eşitleme yoktur.

## <a name="synchronization-from-a-multi-forest-on-premises-environment"></a>Bir Çoklu orman şirket içi ortamından eşitleme
Çoğu kuruluş birden fazla hesap ormanına oluşan oldukça karmaşık şirket içi kimlik altyapınızı sahiptir. Azure AD Connect eşitleme kullanıcıları, grupları ve birden çok orman ortamlarına tooyour Azure AD Kiracı gelen kimlik bilgisi karmalarını destekler.

Buna karşılık, Azure AD kiracınıza kadar bir daha basit ve düz ad alanıdır. Azure AD tarafından güvenli hale getirilmiş tooenable kullanıcılar tooreliably uygulamalarına erişim farklı ormanlardaki kullanıcı hesapları arasında UPN çakışmaları çözümleyin. Azure AD etki alanı Hizmetleri yönetilen etki alanı bears benzerlik tooyour Azure AD kiracısı kapatın. Bu nedenle, yönetilen etki alanınızda düz bir OU yapısı bakın. Tüm kullanıcılar ve gruplar hello şirket içi etki alanı veya orman, bunlar içinde eşitlenmiş olan bağımsız olarak hello 'AADDC kullanıcılar' kapsayıcı içinde depolanır. Hiyerarşik bir OU yapılandırılmış yapı içi. Ancak, yönetilen etki alanınızı hala basit düz bir OU yapıya sahip.

## <a name="exclusions---what-isnt-synchronized-tooyour-managed-domain"></a>Dışlamalar ne eşitlenmiş tooyour yönetilen etki alanı değil-
Merhaba aşağıdaki nesneleri veya öznitelikleri eşitlenmiş tooyour Azure AD kiracısı veya tooyour yönetilen etki alanı olmayan:

* **Öznitelikler dışarıda:** tooexclude Azure AD Connect kullanarak şirket içi etki alanınızdan tooyour Azure AD Kiracı eşitleme belirli öznitelikler tercih edebilirsiniz. Dışlanan özniteliklerden, yönetilen etki alanında kullanılabilir değil.
* **Grup ilkeleri:** şirket içi etki alanınızda yapılandırılan Grup İlkesi eşitlenmiş tooyour yönetilen etki alanı değil.
* **SYSVOL paylaşımının:** benzer şekilde, SYSVOL paylaşımı şirket içi etki alanınızda hello Merhaba içeriğine eşitlenmiş tooyour yönetilen etki alanı olup olmadığı.
* **Bilgisayar nesnelerini:** Bilgisayarlar birleştirilmiş tooyour şirket içi etki alanı için bilgisayar nesnelerinin eşitlenmiş tooyour yönetilen etki alanı değil. Bu bilgisayarlar değil, yönetilen etki alanınız ile güven ilişkisine sahip ve tooyour şirket içi yalnızca etki alanı ait. Yönetilen etki alanınızda, yalnızca etki alanı toohello açıkça etki alanına katılmış bilgisayarları yönetilen bilgisayar nesnelerini bulur.
* **Kullanıcılar ve gruplar için SIDHistory öznitelikler:** hello birincil kullanıcı ve birincil grup SID şirket etki alanınızdan olan eşitlenmiş tooyour yönetilen etki alanı. Ancak, kullanıcılar ve gruplar için varolan SIDHistory öznitelikleri, şirket içi etki alanı tooyour yönetilen etki alanınızdan eşitlenmez.
* **Kuruluş birimi (OU) yapıları:** şirket içi etki alanınızda tanımlanan kuruluş birimleri tooyour yönetilen etki alanı eşitleme değil. Yönetilen etki alanınızda iki yerleşik OU'lar vardır. Varsayılan olarak, düz bir OU yapısı, yönetilen etki alanınız vardır. Ancak çok seçebilirsiniz[yönetilen etki alanınızda özel bir OU oluşturmanız](active-directory-ds-admin-guide-create-ou.md).

## <a name="how-specific-attributes-are-synchronized-tooyour-managed-domain"></a>Özel öznitelikler eşitlenmiş tooyour yönetilen etki alanı nasıl
Aşağıdaki tablonun hello bazı ortak öznitelikleri listeler ve eşitlenmiş tooyour yönetilen etki alanı nasıl oldukları açıklar.

| Yönetilen etki alanınızda özniteliği | Kaynak | Notlar |
|:--- |:--- |:--- |
| UPN |Azure AD kiracınızda kullanıcının UPN özniteliği |Yönetilen tooyour etki alanı olarak Azure AD kiracınıza hello UPN özniteliği eşitlenir. Bu nedenle, hello en güvenilir yolu toosign tooyour yönetilen etki alanında, UPN kullanıyor. |
| SAMAccountName |Kullanıcının mailNickname Azure AD kiracınızda özniteliği ya da otomatik olarak oluşturulan |Azure AD kiracınızda hello mailNickname özniteliğinden Hello SAMAccountName özniteliği kaynaklıdır. Birden çok kullanıcı hesapları aynı mailNickname özniteliği, hello SAMAccountName otomatik olarak oluşturulan hello varsa. Merhaba kullanıcının mailNickname veya UPN öneki 20 karakterden uzun hello SAMAccountName otomatik olarak oluşturulan toosatisfy hello 20 karakter sınırı SAMAccountName özniteliklerinde ise. |
| Parolaları |Azure AD kiracınıza kullanıcının parolasından |(Ek kimlik bilgileri olarak da bilinir) NTLM veya Kerberos kimlik doğrulaması için gerekli kimlik bilgisi karmalarını Azure AD kiracınıza eşitlenir. Azure AD kiracınıza eşitlenmiş Kiracı ise, bu kimlik bilgileri, şirket içi etki alanından elde edilir. |
| Birincil kullanıcı/Grup SID |Otomatik olarak oluşturulan |Merhaba birincil SID kullanıcı/grup hesapları için yönetilen etki alanında otomatik olarak üretilir. Bu öznitelik hello birincil kullanıcı/Grup SID şirket içi hello nesnesinin eşleşmiyor AD etki alanı. Merhaba yönetilen etki alanı, şirket içi etki alanı farklı bir SID ad alanı olduğundan bu eşleşmemesidir. |
| Kullanıcılar ve gruplar için SID Geçmişi |Şirket içi birincil kullanıcı ve Grup SID |Hello SIDHistory özniteliği, yönetilen etki alanındaki kullanıcılar ve gruplar için şirket içi etki alanınızda toomatch hello karşılık gelen birincil kullanıcı veya grup SID'si ayarlanır. Bu özellik yardımcı olun yükseltme-ve-shift, uygulamaları toohello yönetilen etki alanı daha kolay, toore ACL kaynakları gerekmediği şirket içi. |

> [!NOTE]
> **Merhaba UPN biçimini kullanarak toohello yönetilen etki alanına oturum:** hello SAMAccountName özniteliği, yönetilen etki alanınızdaki bazı kullanıcı hesapları için otomatik olarak oluşturulan olabilir. Birden çok kullanıcıya sahip hello aynı mailNickname özniteliği veya kullanıcıların aşırı uzun UPN önekleri sahip, hello SAMAccountName bu kullanıcılar için otomatik olarak oluşturulan. Bu nedenle, hello SAMAccountName biçimi (örneğin, ' CONTOSO100\joeuser') her zaman bir güvenilir şekilde toosign toohello etki alanında değil. Kullanıcıların otomatik olarak oluşturulan SAMAccountName kendi UPN önekten farklı olabilir. Kullanım hello UPN biçiminde (örneğin, 'joeuser@contoso100.com') toohello toosign yönetilen etki alanı güvenilir.
>
>

### <a name="attribute-mapping-for-user-accounts"></a>Kullanıcı hesapları için özellik eşlemesi
Azure AD kiracınızda kullanıcı nesneleri yönetilen etki alanınızdaki eşitlenmiş toocorresponding öznitelikleri için aşağıdaki tablonun hello nasıl belirli öznitelikleri gösterir.

| Azure AD kiracınızda kullanıcı özniteliği | Yönetilen etki alanınızdaki kullanıcı özniteliği |
|:--- |:--- |
| accountEnabled |userAccountControl (bit ACCOUNT_DISABLED hello temizler veya kümeleri) |
| city |m |
| Ülke |Ortak |
| Bölüm |Bölüm |
| Görünen adı |Görünen adı |
| facsimileTelephoneNumber |facsimileTelephoneNumber |
| givenName |givenName |
| İş Unvanı |Başlık |
| Posta |Posta |
| mailNickname |msDS-AzureADMailNickname |
| mailNickname |SAMAccountName (bazen otomatik olarak oluşturulan olabilir) |
| Mobil |Mobil |
| objectID |msDS-AzureADObjectId |
| onPremiseSecurityIdentifier |SID Geçmişi |
| passwordPolicies |userAccountControl (bit DONT_EXPIRE_PASSWORD hello temizler veya kümeleri) |
| physicalDeliveryOfficeName |physicalDeliveryOfficeName |
| posta kodu |posta kodu |
| preferredLanguage |preferredLanguage |
| durum |St |
| StreetAddress |StreetAddress |
| Soyadı |sn |
| telephoneNumber |telephoneNumber |
| userPrincipalName |userPrincipalName |

### <a name="attribute-mapping-for-groups"></a>Gruplar için özellik eşlemesi
Azure AD kiracınıza Grup nesneleri yönetilen etki alanınızdaki eşitlenmiş toocorresponding öznitelikleri için aşağıdaki tablonun hello nasıl belirli öznitelikleri gösterir.

| Azure AD kiracınıza Grup özniteliği | Yönetilen etki alanınızdaki Grup özniteliği |
|:--- |:--- |
| Görünen adı |Görünen adı |
| Görünen adı |SAMAccountName (bazen otomatik olarak oluşturulan olabilir) |
| Posta |Posta |
| mailNickname |msDS-AzureADMailNickname |
| objectID |msDS-AzureADObjectId |
| onPremiseSecurityIdentifier |SID Geçmişi |
| securityEnabled |groupType |

## <a name="objects-that-are-not-synchronized-tooyour-azure-ad-tenant-from-your-managed-domain"></a>Yönetilen etki alanınızdan tooyour Azure AD kiracısı olmayan nesneler eşitlendi
Bu makalenin önceki bölümde açıklandığı gibi yönetilen etki alanı geri tooyour Azure AD kiracısı gelen eşitleme yoktur. Çok seçebilirsiniz[özel kuruluş birimi (OU) oluşturun](active-directory-ds-admin-guide-create-ou.md) yönetilen etki alanınızdaki. Ayrıca, diğer OU'lar, kullanıcıların, grupların veya bu özel OU içinde hizmet hesapları oluşturabilirsiniz. İçinde özel OU'lar oluşturulan hello nesneler hiçbiri geri tooyour Azure AD kiracısı eşitlenir. Bu nesneler yalnızca yönetilen etki alanınızın içinde kullanılabilir. Bu nedenle, bu nesnelerin Azure AD PowerShell cmdlet'leri, Azure AD grafik API'si veya hello Azure AD Yönetimi kullanıcı arabirimini kullanarak görünür değildir.

## <a name="related-content"></a>İlgili İçerik
* [Özellikler - Azure AD etki alanı Hizmetleri](active-directory-ds-features.md)
* [Dağıtım senaryoları - Azure AD etki alanı Hizmetleri](active-directory-ds-scenarios.md)
* [Azure AD etki alanı Hizmetleri için ağ konuları](active-directory-ds-networking.md)
* [Azure AD etki alanı Hizmetleri ile çalışmaya başlama](active-directory-ds-getting-started.md)
