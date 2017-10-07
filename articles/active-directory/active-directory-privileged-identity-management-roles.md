---
title: Azure AD Privileged Identity Management aaaRoles | Microsoft Docs
description: "Hangi rollerin hello Azure Privileged Identity Management uzantısı ile ayrıcalıklı kimlikleri için kullanılan öğrenin."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: ac812ccc-cf4e-4ac2-b981-69598056c9ed
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/31/2017
ms.author: billmath
ms.custom: pim ; H1Hack27Feb2017;oldportal;it-pro;
ms.openlocfilehash: dc58d005489e3b51b3b3dbea4bf35bd795dbdfb6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="different-administrative-role-in-azure-active-directory-pim"></a>Azure Active Directory PIM farklı yönetim rolü
<!-- **PLACEHOLDER: Need description of how this works. Azure PIM uses roles from MSODS objects.**-->

Azure AD'de toodifferent yönetim rolleri, kuruluşunuzdaki kullanıcılar atayabilirsiniz. Kullanıcı ekleme veya kaldırma gibi görevleri, bu rol atamaları denetlemek veya hizmet ayarlarını değiştirmek, hello mümkün tooperform Azure üzerinde AD, Office 365 ve diğer Microsoft Online Services ve bağlı uygulamaların kullanıcılardır.  

> [!IMPORTANT]
> Microsoft önerir hello kullanarak Azure AD'yi yönetme [Azure AD Yönetim Merkezi](https://aad.portal.azure.com) hello yerine Azure portal hello bu makalede başvurulan Klasik Azure portalı.

Genel yönetici olan kullanıcılar güncelleştirebilirsiniz **kalıcı olarak** tooroles PowerShell cmdlet'lerini kullanarak Azure AD'de atanan `Add-MsolRoleMember` ve `Remove-MsolRoleMember`, ya da açıklandığı gibi hello Klasik portal üzerinden [ Azure Active Directory'de yönetici rolleri atama](active-directory-assign-admin-roles.md).

Azure AD Privileged Identity Management (PIM) Azure AD'de kullanıcıları için ayrıcalıklı erişim ilkelerini yönetir. PIM, Azure AD'de kullanıcıları tooone veya daha fazla rol atar ve birisi atayabilirsiniz toobe kalıcı olarak hello rol ya da hello rolü için uygun olarak. Ne zaman bir kullanıcı tooa rol kalıcı olarak atanan veya Azure Active Directory, Office 365 ve diğer uygulamalar tootheir rolleri atanmış hello izinlerle yönetebilecekleri sonra uygun rol atama etkinleştirir.

Kalıcı bir uygun rol ataması karşı toosomeone verilen hello erişim fark yoktur. Merhaba tek fark bazı kişiler bu erişim hello zaman gerekmemesidir. Merhaba rolü için uygun yapılır ve bunu etkinleştirebilirsiniz ve devre dışı olduğunda gerekir.

## <a name="roles-managed-in-pim"></a>PIM içinde yönetilen roller
Privileged Identity Management, kullanıcıların toocommon yönetici rolleri de dahil olmak üzere, atamanıza olanak sağlar:

* **Genel yönetici** (şirket yönetici olarak da bilinir) erişim tooall yönetim özelliklerine sahiptir. Kuruluşunuzda birden çok genel yönetici olabilir. otomatik olarak Office 365 toopurchase açan hello kişi bir genel yönetici olur
* **Ayrıcalıklı Rol Yöneticisi** Azure AD PIM yönetir ve diğer kullanıcılar için rol atamalarını güncelleştirir.  
* **Faturalama Yöneticisi** satın alma işlemleri yapar, abonelikleri yönetir, destek biletlerini yönetir ve hizmetin sistem durumunu izler.
* **Parola Yöneticisi** parolaları sıfırlar, hizmet isteklerini yönetir ve hizmetin sistem durumunu izler. Parola yönetici kullanıcılar için sınırlı tooresetting parolalar yaşıyor.
* **Hizmet Yöneticisi** hizmet isteklerini yönetir ve hizmetin sistem durumunu izler.
  
  > [!NOTE]
  > Office 365 kullanıyorsanız, ardından hello hizmet Yönetici rolü tooa kullanıcı atamadan önce ilk hello kullanıcı yönetim izinleri tooa hizmeti, Exchange Online gibi atayın.
  > 
  > 
* **Kullanıcı Yönetimi Yöneticisi** parolaları sıfırlar, hizmetin sistem durumunu izler ve kullanıcı hesapları, kullanıcı grupları ve hizmet isteklerini yönetir. Hello kullanıcı yönetimi Yöneticisi genel yönetici silinemez, diğer yönetici rolleri oluşturabilir veya fatura, genel ve hizmet yöneticileri için parolaları sıfırlayın.
* **Exchange Yöneticisi** hello Exchange yönetici merkezini (Seçmeye) yönetim erişimi tooExchange çevrimiçi olan ve neredeyse her görevi'te Exchange Online gerçekleştirebilirsiniz.
* **SharePoint Yöneticisi** hello SharePoint Online Yönetim Merkezi yönetim erişimi tooSharePoint çevrimiçi olan ve neredeyse her görev SharePoint Online'da gerçekleştirebilirsiniz.
* **İş Yöneticisi Skype** Merhaba Skype iş Yönetim Merkezi aracılığıyla iş için yönetim erişimi tooSkype sahiptir ve neredeyse her görev Skype Kurumsal çevrimiçi gerçekleştirebilirsiniz.

Daha fazla ayrıntı için bu makaleler okuyun [Azure AD'de yönetici rolleri atama](active-directory-assign-admin-roles.md) ve [Office 365'te yönetici rolleri atama](https://support.office.com/article/Assigning-admin-roles-in-Office-365-eac4d046-1afd-4f1a-85fc-8219c79e1504).

<!--**PLACEHOLDER: hello above article may not be hello one we want since PIM gets roles from places other that Office 365**-->


PIM yapabilecekleriniz [bu rolleri tooa kullanıcı atama](active-directory-privileged-identity-management-how-to-add-role-to-user.md) hello kullanıcı böylece [gerektiğinde Merhaba rolünü etkinleştirmek](active-directory-privileged-identity-management-how-to-activate-role.md).

PIM kendisini hello kullanıcı toohave daha ayrıntılı açıklanır PIM gerektiren hello rolleri başka bir kullanıcı erişimi toomanage toogive istiyorsanız [nasıl toogive erişim tooPIM](active-directory-privileged-identity-management-how-to-give-access-to-pim.md).

<!-- ## hello PIM Security Administrator Role **PLACEHOLDER: Need description of hello Security Administrator role.**-->

## <a name="roles-not-managed-in-pim"></a>PIM içinde yönetilmeyen rolleri
Exchange Online veya SharePoint Online içinde rolleri olanlar, yukarıda belirtilen dışında Azure AD'de temsil edilmez ve bu nedenle PIM görünür değildir. Bu Office 365 Hizmetleri hassas rol atamalarını değiştirme hakkında daha fazla bilgi için bkz: [Office 365'te izinleri](https://support.office.com/article/Permissions-in-Office-365-da585eea-f576-4f55-a1e0-87090b6aaa9d).

Ayrıca Azure Abonelikleriniz ve kaynak gruplarınız Azure AD'de temsil edilmez. toomanage Azure abonelikleri görmek [nasıl tooadd ya da değişiklik Azure yönetici rolleri](../billing/billing-add-change-azure-subscription-administrator.md) ve Azure RBAC bakın hakkında daha fazla bilgi için [Azure rol tabanlı erişim denetimi](role-based-access-control-configure.md).

<!--**hello above links might be replaced by ones that are from within this documentation repository **-->


## <a name="user-roles-and-signing-in"></a>Kullanıcı rolleri ve oturum açma
Bazı Microsoft Hizmetleri ve uygulamaları için bir kullanıcı tooa rol atama olmayabilir yeterli tooenable o kullanıcı toobe bir yönetici olmalıdır.

Klasik Azure portalına erişim toohello gerektirir hello kullanıcı bir Hizmet Yöneticisi veya bir Azure aboneliğinin ortak yönetici, hello kullanıcı olmasa bile toomanage Azure abonelikleri hello.  Örneğin, Azure AD Klasik portalında Merhaba, bir kullanıcı için toomanage yapılandırma ayarları, Azure AD genel yönetici ve bir Azure aboneliği abonelik ortak yönetici olması gerekir.  nasıl tooadd kullanıcılar tooAzure abonelikleri görmek toolearn [nasıl tooadd ya da değişiklik Azure yönetici rolleri](../billing/billing-add-change-azure-subscription-administrator.md).

Online Services gerektirebilir erişim tooMicrosoft hello kullanıcı da atanabilir bir lisans hello hizmetin portalını açın veya yönetim görevlerini gerçekleştirmek için önce.

## <a name="assign-a-license-tooa-user-in-azure-ad"></a>Azure AD içinde lisans tooa kullanıcı atama
1. İçinde toohello oturum [Klasik Azure portalı](http://manage.windowsazure.com) bir genel yönetici hesabını veya bir ortak yönetici hesabı.
2. Seçin **tüm öğeleri** hello ana menüden.
3. İle toowork ve lisansları kendisiyle ilişkilendirilmiş istediğiniz hello dizini seçin.
4. Seçin **lisansları**. kullanılabilir lisans Hello listesi görüntülenir.
5. Toodistribute istediğiniz hello lisans içeren hello lisans planını seçin.
6. Seçin **kullanıcı atama**.
7. Tooassign bir lisans istiyor select hello kullanıcı için.
8. Merhaba tıklatın **atamak** düğmesi.  Merhaba kullanıcı artık tooAzure oturum açabilir.

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a>Sonraki adımlar
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

