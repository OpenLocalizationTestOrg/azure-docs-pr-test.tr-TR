---
title: "Azure Active Directory'de yönetici rolleri aaaAssigning | Microsoft Docs"
description: "Yönetici rolü oluşturmak veya kullanıcıları Düzenle, yönetici rollerini tooothers ata, kullanıcı parolalarını sıfırlama, kullanıcı lisanslarını yönetme veya etki alanlarını yönetme. Yönetici rolü atanan bir kullanıcının hello sahip aynı izinlere kuruluşunuzun abone tüm bulut Hizmetleri toowhich arasında."
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 7fc27e8e-b55f-4194-9b8f-2e95705fb731
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: curtand
ms.reviewer: Vince.Smith
ms.custom: it-pro;
ms.openlocfilehash: 41cddbf311767d9995c99ee386e6d276745dad18
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="assigning-administrator-roles-in-azure-active-directory"></a>Azure Active Directory’de yönetici rolü atama
> [!div class="op_single_selector"]
> * [Azure portal](active-directory-assign-admin-roles-azure-portal.md)
> * [Klasik Azure Portalı](active-directory-assign-admin-roles.md)
>
>

Azure Active Directory (Azure AD) kullanarak, ayrı Yöneticiler tooserve farklı işlevler belirleyebilirsiniz. Bu yöneticileri hello Azure portalında veya Klasik Azure portalına erişim toovarious özelliklerine sahip olacak ve, kendi role bağlı olarak mümkün toocreate olması veya kullanıcıları Düzenle, yönetici rollerini tooothers ata, kullanıcı parolalarını sıfırlama, kullanıcı lisanslarını yönetme ve etki alanları, başka şeylerin yönetin. Yönetici rolü atanan bir kullanıcının tüm kuruluşunuz için bağımsız olarak atamak olup abone hello bulut hizmetleri arasında aynı izinleri hello Office 365 portalı rolünde hello veya hello Klasik Azure portalı veya kullanarak hello hello gerekir Windows PowerShell için Azure AD modülü.

yönetici rolleri aşağıdaki hello kullanılabilir:

* **Faturalama Yöneticisi**: satın alma işlemleri yapar, abonelikleri yönetir, destek biletlerini yönetir ve hizmetin sistem durumunu izler.

* **Uyumluluk Yöneticisi**: Bu rolün kullanıcılarla hello Office 365 güvenlik ve Uyumluluk Merkezi ve Exchange yönetici merkezini içinde yönetim izinlerine sahip. Daha fazla bilgi "[Office 365 Yönetici rolleri hakkında](https://support.office.com/en-us/article/About-Office-365-admin-roles-da585eea-f576-4f55-a1e0-87090b6aaa9d)."

* **CRM Hizmet Yöneticisi**: Bu rolüne sahip kullanıcılar, Microsoft CRM Online içinde genel izinlere sahip, hello hizmet bulunduğunda hello özelliği toomanage yanı sıra biletleri destekler ve hizmetin sistem durumunu izleme. Daha fazla bilgi [hakkında Office 365 Yönetici rollerine](https://support.office.com/article/About-Office-365-admin-roles-da585eea-f576-4f55-a1e0-87090b6aaa9d).

* **Cihaz yöneticileri**: kullanıcılar bu rol ile birleştirilen tooAzure Active Directory olan tüm Windows 10 cihazlarda yerel makine yöneticilerinin haline gelir. Bunlar hello özelliği toomanage aygıtları nesneler Azure Active Directory'de yok.

* **Dizin okuyucular**: hello desteklemeyen atanan toobe tooapplications eski bir rolü budur [onayı Framework](active-directory-integrating-applications.md). Tooany kullanıcılar atanmamalıdır.

* **Dizin eşitleme hesapları**: kullanmayın. Bu rol toohello Azure AD Connect hizmetinin otomatik olarak atanır ve değil kullanılmaya veya diğer kullanım için desteklenir.

* **Directory yazıcılarının**: hello desteklemeyen atanan toobe tooapplications eski bir rolü budur [onayı Framework](active-directory-integrating-applications.md). Tooany kullanıcılar atanmamalıdır.

* **Exchange Hizmet Yöneticisi**: Bu rol ile kullanıcınız Microsoft Exchange Online içinde genel izinleri hello hizmet bulunduğunda. Daha fazla bilgi [hakkında Office 365 Yönetici rollerine](https://support.office.com/article/About-Office-365-admin-roles-da585eea-f576-4f55-a1e0-87090b6aaa9d).

* **Genel yönetici / şirket Yöneticisi**: Bu rolüne sahip kullanıcılar Azure Active Directory'ye erişim tooall yönetim özelliklerine sahip yanı sıra bu federate tooAzure Exchange Online, SharePoint Online gibi Active Directory Hizmetleri ve Skype Kurumsal çevrimiçi sürüm. hello Azure Active Directory Kiracı için kaydolan hello kişi genel yönetici olur. Yalnızca küresel Yöneticiler diğer yönetici rollerini atayabilir. Şirketinizde birden fazla genel yönetici olabilir. Genel Yöneticiler hello parolanızı herhangi bir kullanıcı ve diğer tüm yöneticileri için sıfırlayabilir.

  > [!NOTE]
  > Microsoft Graph API, Azure AD Graph API ve Azure AD PowerShell Bu rolün "Şirket Yönetici" olarak tanımlanır. "Genel yönetici" hello olduğu [Azure portal](https://portal.azure.com).
  >
  >

* **Konuk davet eden**: Bu roldeki kullanıcılar, Azure Active Directory B2B Konuk kullanıcı davetleri yönetebilir, hello "Üyeleri davet edebilirsiniz" Kullanıcı ayarı tooNo olarak ayarlandığında geçerlidir. B2B işbirliğinin hakkında daha fazla bilgi [hello Azure AD B2B işbirliği önizleme hakkında](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-b2b-what-is-azure-ad-b2b). Diğer izinler içermez.

* **Intune hizmet yöneticisinin**: Bu rolüne sahip kullanıcılar hello hizmet mevcut olduğunda Microsoft Intune çevrimiçi içinde genel izinlere sahiptir. Ayrıca, bu rolü hello özelliği toomanage kullanıcıları ve aygıtları sipariş tooassociate İlkesi ' nde içeren yanı sıra oluşturun ve grupları yönetin.

* **Posta kutusu yönetici**: Bu rol yalnızca RIM Blackberry cihazlar için Exchange Online e-posta desteği bir parçası olarak kullanılır. Kuruluşunuz RIM Blackberry cihazlarda Exchange Online e-posta kullanmıyorsa, bu rolü kullanmayın.

* **İş ortağı Katman 1 destek**: kullanmayın. Bu rolü kullanım dışı bırakıldı ve gelecekteki hello Azure AD'de kaldırılır. Bu rol, az sayıda Microsoft satışı iş ortakları tarafından kullanılmaya yöneliktir ve genel kullanıma yönelik değildir.

* **İş ortağı Katman 2 Destek**: kullanmayın. Bu rolü kullanım dışı bırakıldı ve gelecekteki hello Azure AD'de kaldırılır. Bu rol, az sayıda Microsoft satışı iş ortakları tarafından kullanılmaya yöneliktir ve genel kullanıma yönelik değildir.

* **Parola Yöneticisi / Yardım Masası Yöneticisi**: Bu rolüne sahip kullanıcılar parolalarını sıfırlama, hizmet istekleri yönetebilir ve hizmetin sistem durumunu izleme. Parola yöneticileri yalnızca kullanıcılar ve diğer parola yöneticileri için sıfırlayabilir.

  > [!NOTE]
  > Microsoft Graph API, Azure AD Graph API ve Azure AD PowerShell, bu rolün "Yardım Masası Yönetici" olarak tanımlanır. Bunu "parola" hello yöneticisidir [Azure portal](https://portal.azure.com/).
  >
  >
  
* **Power BI Hizmet Yöneticisi**: Bu rolüne sahip kullanıcılar, Microsoft Power BI içinde genel izinlere sahip, hello hizmet bulunduğunda hello özelliği toomanage yanı sıra biletleri destekler ve hizmetin sistem durumunu izleme. Daha fazla bilgi [hakkında Office 365 Yönetici rollerine](https://support.office.com/en-us/article/About-Office-365-admin-roles-da585eea-f576-4f55-a1e0-87090b6aaa9d?ui=en-US&rs=en-001&ad=US).

* **Ayrıcalıklı Rol Yöneticisi**: Bu rolüne sahip kullanıcılar, Azure Active Directory'de yanı sıra Azure AD Privileged Identity Management içinde rol atamalarını yönetebilir. Ayrıca, bu rolün tüm yönlerini Privileged Identity Management yönetilmesine izin verir.

* **Güvenlik Yöneticisi**: Bu rolün kullanıcılarla hello salt okunur izinleri hello güvenlik okuyucu rolüne yanı sıra güvenlikle ilgili hizmetleri için hello özelliği toomanage yapılandırmaya sahip: Azure Active Directory kimlik koruması, Privileged Identity Management ve Office 365 güvenlik ve Uyumluluk Merkezi. Office 365 izinleri hakkında daha fazla bilgi için bkz. [hello Office 365 güvenlik ve Uyumluluk Merkezi izinleri](https://support.office.com/en-us/article/Permissions-in-the-Office-365-Security-Compliance-Center-d10608af-7934-490a-818e-e68f17d0e9c1).

* **Güvenlik okuyucu**: Bu rolüne sahip kullanıcılar tüm bilgileri de dahil olmak üzere Azure Active Directory, kimlik koruması, Privileged Identity Management, genel salt okunur erişime sahip yanı sıra özelliği tooread Azure Active Directory oturum açma hello raporlar ve Denetim günlükleri. Merhaba rol, ayrıca Office 365 güvenlik ve Uyumluluk Merkezi salt okunur izni verir. Office 365 izinleri hakkında daha fazla bilgi için bkz. [hello Office 365 güvenlik ve Uyumluluk Merkezi izinleri](https://support.office.com/en-us/article/Permissions-in-the-Office-365-Security-Compliance-Center-d10608af-7934-490a-818e-e68f17d0e9c1).

* **Hizmet desteği Yöneticisi**: Bu rolü olan kullanıcılar açabilir destek istekleri ile Microsoft Azure ve Office 365 Hizmetleri ve görünümler hello hizmet Pano ve ileti Merkezi'nde hello Azure portal ve Office 365 Yönetici portalı. Daha fazla bilgi [hakkında Office 365 Yönetici rollerine](https://support.office.com/article/About-Office-365-admin-roles-da585eea-f576-4f55-a1e0-87090b6aaa9d).

* **SharePoint Hizmet Yöneticisi**: Bu rolüne sahip kullanıcılar, Microsoft SharePoint Online içinde genel izinlere sahip, hello hizmet bulunduğunda hello özelliği toomanage yanı sıra biletleri destekler ve hizmetin sistem durumunu izleme. Daha fazla bilgi [hakkında Office 365 Yönetici rollerine](https://support.office.com/article/About-Office-365-admin-roles-da585eea-f576-4f55-a1e0-87090b6aaa9d).

* **Skype Kurumsal / Lync Hizmet Yöneticisi**: Bu rolüne sahip kullanıcılar hello hizmet bulunduğunda Microsoft Skype Kurumsal, genel izinlere sahip yanı sıra Azure Active Directory'de Skype özgü kullanıcı özniteliklerini yönetme. Ayrıca, bu rolü verir hello özelliği toomanage destek biletlerini ve İzleyici sistem durumu hizmeti. Daha fazla bilgi [hakkında Office 365 Yönetici rollerine](https://support.office.com/article/About-Office-365-admin-roles-da585eea-f576-4f55-a1e0-87090b6aaa9d).

  > [!NOTE]
  > Microsoft Graph API, Azure AD Graph API ve Azure AD PowerShell, bu rolün "Lync Hizmet Yöneticisi olarak" tanımlanır. Hello "Skype için iş Hizmet Yöneticisi" olan [Azure portal](https://portal.azure.com/).
  >
  >

* **Kullanıcı hesabı yönetici**: Bu rolüne sahip kullanıcılar oluşturabilir ve kullanıcıların ve grupların tüm yönlerini yönetebilirsiniz. Ayrıca, bu rolü hello özelliği toomanage destek biletlerini içerir ve izleyicileri Sağlık Hizmeti. Bazı kısıtlamalar uygulanır. Örneğin, bu rol bir genel yönetici silinmesine izin vermiyor ve yönetici olmayanlar için parola değiştirme izin verirken, genel yöneticileri için parolaları veya diğer ayrıcalıklı yöneticileri değiştirilmesine izin vermez.

## <a name="administrator-permissions"></a>Yönetici izinleri

### <a name="billing-administrator"></a>Faturalama Yöneticisi

| Yapabilirsiniz | Yapamaz |
| --- | --- |
|<p>Şirket ve kullanıcı bilgilerini görüntüleme</p><p>Office destek biletlerini yönetme</p><p>Office ürünlerinin faturalama ve satın alma işlemleri gerçekleştirme</p> |<p>Kullanıcı parolalarını sıfırlama</p><p>Oluşturma ve kullanıcı görünümleri yönetme</p><p>Oluşturmak, düzenlemek ve kullanıcıları ve grupları silme ve kullanıcı lisanslarını yönetme</p><p>Etki alanlarını yönetme</p><p>Şirket bilgilerini yönetme</p><p>Yönetici rolleri tooothers temsilci seçme</p><p>Dizin eşitleme kullanma</p><p>Denetim günlüklerini görüntüleme</p>|

### <a name="global-administrator"></a>Genel yönetici
| Yapabilirsiniz | Yapamaz |
| --- | --- |
| <p>Şirket ve kullanıcı bilgilerini görüntüleme</p><p>Office destek biletlerini yönetme</p><p>Office ürünlerinin faturalama ve satın alma işlemleri gerçekleştirme</p><p>Kullanıcı parolalarını sıfırlama</p>
<p>Diğer yönetici parolalarını sıfırlama</p> <p>Oluşturma ve kullanıcı görünümleri yönetme</p><p>Oluşturmak, düzenlemek ve kullanıcıları ve grupları silme ve kullanıcı lisanslarını yönetme</p><p>Etki alanlarını yönetme</p><p>Şirket bilgilerini yönetme</p><p>Yönetici rolleri tooothers temsilci seçme</p><p>Dizin eşitleme kullanma</p><p>Etkinleştirmek veya çok faktörlü kimlik doğrulamasını devre dışı bırakma</p><p>Denetim günlüklerini görüntüleme</p> |Yok |

### <a name="password-administrator"></a>Parola Yöneticisi
| Yapabilirsiniz | Yapamaz |
| --- | --- |
| <p>Şirket ve kullanıcı bilgilerini görüntüleme</p><p>Office destek biletlerini yönetme</p><p>Kullanıcı parolalarını sıfırlama</p> <p>Diğer yönetici parolalarını sıfırlama</p>|<p>Office ürünlerinin faturalama ve satın alma işlemleri gerçekleştirme</p><p>Oluşturma ve kullanıcı görünümleri yönetme</p><p>Oluşturmak, düzenlemek ve kullanıcıları ve grupları silme ve kullanıcı lisanslarını yönetme</p><p>Etki alanlarını yönetme</p><p>Şirket bilgilerini yönetme</p><p>Yönetici rolleri tooothers temsilci seçme</p><p>Dizin eşitleme kullanma</p><p>Raporları görüntüleme</p>|

### <a name="service-administrator"></a>Hizmet Yöneticisi
| Yapabilirsiniz | Yapamaz |
| --- | --- |
| <p>Şirket ve kullanıcı bilgilerini görüntüleme</p><p>Office destek biletlerini yönetme</p> |<p>Kullanıcı parolalarını sıfırlama</p><p>Office ürünlerinin faturalama ve satın alma işlemleri gerçekleştirme</p><p>Oluşturma ve kullanıcı görünümleri yönetme</p><p>Oluşturmak, düzenlemek ve kullanıcıları ve grupları silme ve kullanıcı lisanslarını yönetme</p><p>Etki alanlarını yönetme</p><p>Şirket bilgilerini yönetme</p><p>Yönetici rolleri tooothers temsilci seçme</p><p>Dizin eşitleme kullanma</p><p>Denetim günlüklerini görüntüleme</p> |

### <a name="user-administrator"></a>Kullanıcı Yöneticisi
| Yapabilirsiniz | Yapamaz |
| --- | --- |
| <p>Şirket ve kullanıcı bilgilerini görüntüleme</p><p>Office destek biletlerini yönetme</p><p>Kısıtlamalarla kullanıcı parolalarını sıfırlayın.</p><p>Diğer yönetici parolalarını sıfırlama</p><p>Diğer kullanıcıların parolalarını sıfırlayın</p><p>Oluşturma ve kullanıcı görünümleri yönetme</p><p>Oluşturmak, düzenlemek ve kullanıcıları ve grupları silme ve kısıtlamalarla kullanıcı lisanslarını yönetme. İsterse bir genel yöneticiyi silemez veya başka Yöneticiler oluşturamaz.</p> |<p>Office ürünlerinin faturalama ve satın alma işlemleri gerçekleştirme</p><p>Etki alanlarını yönetme</p><p>Şirket bilgilerini yönetme</p><p>Yönetici rolleri tooothers temsilci seçme</p><p>Dizin eşitleme kullanma</p><p>Etkinleştirmek veya çok faktörlü kimlik doğrulamasını devre dışı bırakma</p><p>Denetim günlüklerini görüntüleme</p> |

### <a name="security-reader"></a>Güvenlik okuyucusu
| İçinde | Yapabilirsiniz |
| --- | --- |
| Kimlik koruması Merkezi |Tüm güvenlik raporları ve güvenlik özellikleri için ayarlar bilgilerini okuyun<ul><li>İstenmeyen postadan koruma<li>Şifreleme<li>Veri kaybını önleme<li>Kötü amaçlı yazılım<li>Gelişmiş tehdit koruması<li>Avından<li>Mailflow kuralları |
| Privileged Identity Management |<p>Azure AD PIM ortaya salt okunur erişim tooall bilgi: güvenlik ilkelerine ve Azure AD rol atamaları için raporları, gözden geçirir ve toopolicy verilere erişmek ve Azure AD rol ataması yanı sıra senaryoları için raporlar gelecekteki hello okuyun.<p>**Olamaz** Azure AD PIM için kaydolun veya tüm değişiklikleri tooit olun. Merhaba kullanıcı bunları aday ise PIM'ın portal veya PowerShell aracılığıyla, birisi Bu roldeki ek roller (örneğin, genel yönetici veya ayrıcalıklı Rol Yöneticisi) etkinleştirebilirsiniz. |
| <p>İzleyici Office 365 hizmeti durumu</p><p>Office 365 güvenlik ve Uyumluluk Merkezi</p> |<ul><li>Okuma ve Uyarıları yönetme<li>Güvenlik ilkelerini oku<li>Tehdit bilgileri, Cloud App Discovery ve arama ve Araştır Karantinadaki okuyun<li>Tüm raporları okuma |

### <a name="security-administrator"></a>Güvenlik Yöneticisi
| İçinde | Yapabilirsiniz |
| --- | --- |
| Kimlik koruması Merkezi |<ul><li>Merhaba güvenlik okuyucu rolünün tüm izinleri.<li>Ayrıca, parolaları sıfırlama hariç tüm IPC işlemleri özelliği tooperform hello. |
| Privileged Identity Management |<ul><li>Merhaba güvenlik okuyucu rolünün tüm izinleri.<li>**Olamaz** Azure AD rol üyeliklerini veya ayarlarını yönetin. |
| <p>İzleyici Office 365 hizmeti durumu</p><p>Office 365 güvenlik ve Uyumluluk Merkezi |<ul><li>Merhaba güvenlik okuyucu rolünün tüm izinleri.<li>Tüm ayarlar hello Advanced Threat Protection özelliği (kötü amaçlı yazılım ve virüs koruması, kötü amaçlı URL yapılandırma, URL izleme, vb.) yapılandırabilirsiniz. |

## <a name="details-about-hello-global-administrator-role"></a>Merhaba genel Yönetici rolüne hakkındaki ayrıntıları
Merhaba genel yönetici erişimi tooall yönetim özelliklerine sahiptir. Varsayılan olarak, Azure aboneliği için kaydolan hello kişi hello dizin hello genel Yönetici rolüne atanır. Yalnızca küresel Yöneticiler diğer yönetici rollerini atayabilir.

### <a name="tooadd-a-colleague-as-a-global-administrator"></a>tooadd genel yönetici olarak bir iş arkadaşı

1. İçinde toohello oturum [Azure Active Directory Yönetim Merkezi'ni](https://aad.portal.azure.com) hello Kiracı dizin için genel yönetici olan bir hesapla.

   ![Azure AD Yönetim Merkezi açma](./media/active-directory-assign-admin-roles-azure-portal/active-directory-admin-center.png)

2. Seçin **kullanıcılar ve gruplar &gt; tüm kullanıcılar**

3. Genel yönetici olarak toodesignate istediğiniz ve o kullanıcı hello dikey penceresini açmak hello kullanıcıyı bulun.

4. Merhaba kullanıcı dikey penceresinde, seçin **dizin rolünü**.
 
5. Merhaba dizin rolü dikey penceresinde hello seçin **genel yönetici** rolü ve kaydedin.

## <a name="assign-or-remove-administrator-roles"></a>Atama veya yönetici rolleri kaldırma
Azure Active Directory'de tooassign yönetici rollerini tooa kullanıcıya nasıl görürüm toolearn [tooadministrator rolleri Azure Active Directory Önizleme'de bir kullanıcı atamak](active-directory-users-assign-role-azure-portal.md).

## <a name="deprecated-roles"></a>Kullanım dışı rolleri

rolleri aşağıdaki hello kullanılmamalıdır. Bunlar edilmiş kullanım dışıdır ve gelecekteki hello Azure AD'de kaldırılır.

* AdHoc Lisans Yöneticisi
* E-posta doğrulanan kullanıcı Oluşturucusu
* Cihaz birleştirme
* Cihaz yöneticileri
* Aygıt kullanıcıları
* Çalışma alanına cihaz katılma

## <a name="next-steps"></a>Sonraki adımlar

* toolearn nasıl toochange Yöneticiler bir Azure aboneliğine yönelik bakın hakkında daha fazla bilgi [nasıl tooadd ya da değişiklik Azure yönetici rolleri](../billing-add-change-azure-subscription-administrator.md)
* Microsoft Azure'da kaynak erişiminin nasıl denetlendiğini hakkında daha fazla toolearn bkz [azure'da kaynak erişimini anlama](active-directory-understanding-resource-access.md)
* Azure Active Directory tooyour Azure aboneliği ilişkilendirilme şekli ile ilgili daha fazla bilgi için bkz: [Azure aboneliklerinin Azure Active Directory ile ilişkili](active-directory-how-subscriptions-associated-directory.md)
* [Kullanıcıları yönetme](active-directory-create-users.md)
* [Parolaları yönetme](active-directory-manage-passwords.md)
* [Grupları yönetme](active-directory-manage-groups.md)
