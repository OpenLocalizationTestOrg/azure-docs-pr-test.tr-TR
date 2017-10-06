---
title: "Azure Active Directory'de aaaLicense kullanıcılar | Microsoft Docs"
description: "Bilgi nasıl toolicense kendinizin ve kullanıcılarınızın Azure Active Directory'de."
services: active-directory
documentationcenter: 
author: jeffgilb
manager: femila
editor: 
ms.assetid: f8b932bc-8b4f-42b5-a2d3-f2c076234a78
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/22/2017
ms.author: jeffgilb
custom: it-pro
ms.openlocfilehash: ae0bc030fa02b79d1dd01ca961b4e96e6b9c470d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="quickstart-license-users-in-azure-active-directory"></a>Hızlı Başlangıç: Azure Active Directory'deki kullanıcı lisansı
Lisans tabanlı Azure AD, Azure kiracınızdaki bir Azure Active Directory (Azure AD) aboneliği etkinleştirerek iş Hizmetleri. Hello abonelik etkinleştirildikten sonra hizmet özellikleri Azure AD yöneticileri tarafından yönetilir ve lisanslı kullanıcılar tarafından kullanılır. Enterprise Mobility + güvenlik, Azure AD Premium veya Azure AD temel, Kiracı satın ne zaman geçerlilik süresinin dahil olmak üzere hello abonelikle güncelleştirilir ve lisansları ön ödemeli. Merhaba atanan veya kullanılabilir lisans sayısı gibi abonelik bilgilerinizi hello Azure kullanılabilir altında portal **Azure Active Directory** açma hello tarafından **lisansları** döşeme. Merhaba **lisansları** dikey olduğunu da hello en iyi yeri toomanage lisans atamalarınızı.

Bir aboneliği elde tüm yetenekleri Ücretli tooconfigure ihtiyacınız olsa da, hala özellikleri Ücretli Ücretli Azure AD için kullanıcı lisansları atamanız gerekir. Kimin erişiminiz veya bir Azure üzerinden, yönetilen kimin herhangi bir kullanıcı bir lisans özelliği Ücretli AD atanmış. Lisans atama, kullanıcı ve Azure AD Premium, Basic veya Enterprise Mobility + Security gibi bir satın alınan hizmet arasındaki bir eşlemedir.

Kullanabileceğiniz [grup tabanlı lisans atamasını](active-directory-licensing-whatis-azure-portal.md) tooset hello aşağıdaki gibi kurallar:
* Dizininizdeki tüm kullanıcılara otomatik olarak bir lisans alın
* Merhaba uygun iş unvanı herkesle bir lisans alır
* Merhaba karar tooother yöneticileri hello kuruluşunuzdaki devredebilirsiniz (kullanarak [Self Servis grup](active-directory-accessmanagement-self-service-group-management.md))

> [!TIP]
> Lisans atama toogroups hakkında ayrıntılı bilgi için Gelişmiş senaryoları ve Office 365 senaryoları, lisanslama dahil olmak üzere bkz [Ata lisansları Azure Active Directory'de Grup üyeliğiyle toousers](active-directory-licensing-group-assignment-azure-portal.md).

## <a name="assign-licenses-toousers-and-groups"></a>Lisansları toousers ve grupları atama
Etkin bir aboneliğiniz kullanarak ilk lisans tooyourself atayın ve aboneliğinizle gördüğünüz tüm beklenen hello özellikler dahil, tarayıcı tooensure yenileyin. Merhaba sonraki toopaid Azure AD özelliklerine erişmek isteyen tooassign lisansları toohello kullanıcılar adımdır. Bir kolay bir yolu tooassign lisansı tooassign lisansları toogroups tooindividuals yerine kullanıcıların olabilir. Lisansları tooa grubu atadığınızda, tüm Grup üyeleri lisansı atanır. Kullanıcıların eklediyseniz veya hello grubundan kaldırılmış hello uygun lisans otomatik olarak atanmış veya kaldırılana. 

> [!NOTE]
> Bazı Microsoft Hizmetleri tüm konumlarda kullanılabilir değil. Bir lisans tooa kullanıcı atanabilmesi için önce hello yönetici hello belirtmelidir **kullanım konumu** hello kullanıcı özelliği. Bu özelliği altında ayarlayabilirsiniz **kullanıcı** &gt; **profil** &gt; **ayarları** hello Azure Portalı'nda. Grup lisans atamasını kullanırken, kullanım konumu belirtilmezse herhangi bir kullanıcı hello dizininin hello konumu devralır.

tooassign lisansı altında **Azure Active Directory** &gt; **lisansları** &gt; **tüm ürünleri**, bir veya daha fazla ürünleri seçin ve ardından seçin **Atamak** hello komut çubuğunda.

![Bir lisans tooassign seçin](media/license-users-groups/select-license-to-assign.png)

Merhaba kullanabilirsiniz **kullanıcılar ve gruplar** birden çok kullanıcı veya grupları ve toodisable hizmet planları hello üründe dikey toochoose. Merhaba arama kutusunu üzerinde üst toosearch için kullanıcı ve grup adları kullanın.

![Bir kullanıcı veya grup için lisans atamasını seçin](media/license-users-groups/select-user-for-license-assignment.png)

Lisansları tooa grubu atadığınızda, hello lisans hello grubunun hello boyutunu bağlı olarak tüm kullanıcılar devralırlar önce biraz zaman alabilir. Merhaba hello işleme durumunu denetleyebilirsiniz **grup** hello altında dikey **lisansları** döşeme.

![Lisans atama durumu](media/license-users-groups/license-assignment-status.png)

Atama hataları sırasında Azure AD lisans atamasını gerçekleşebileceğini, ancak Azure AD yönetirken görece olarak daha ender ve Enterprise Mobility + güvenlik ürünleri. Olası atama hataları sınırlıdır:
- Atama çakışma: ne zaman bir kullanıcı daha önce atanma hello geçerli lisans ile uyumsuz bir lisans. Bu durumda, hello yeni lisans atama hello geçerli kaldırılması gerekir.
- Kullanılabilir lisans aşıldı: atanan gruplarındaki kullanıcılar hello sayısı hello kullanılabilir lisans aşarsa, bir kullanıcının atama durumu hatası tooassign toomissing lisansları son yansıtır.

### <a name="azure-ad-b2b-collaboration-licensing"></a>Azure AD B2B işbirliği lisanslama

B2B işbirliği, Azure AD Kiracı tooprovide erişim tooAzure AD hizmetlerine tooinvite Konuk kullanıcılar sağlar ve Azure kaynaklarını kullanılabilir yapın.  

B2B kullanıcıları davet ve bunları Azure AD'de tooan uygulama atama için ücretsizdir. Konuk başına too10 uygulamaları yukarı kullanıcı ve 3 temel raporları da B2B işbirliği kullanıcılar için boş. Konuk kullanıcı hello ortağın Azure AD kiracısında atanmış uygun lisans varsa, bunlar sizin içinde de lisansına sahip olması.

Gerekli değildir, ancak tooprovide erişim toopaid Azure AD özellikler istiyorsanız, bu B2B Konuk kullanıcılar lisansına sahip olması gerekir ile Azure AD lisansları uygun. Lisans Ücretli bir Azure AD ile bir davet Kiracı davet tooan ek beş Konuk kullanıcılar B2B işbirliği kullanıcı hakları atamak toohello Kiracı. Senaryolar ve bilgi için bkz: [Kılavuzu lisans B2B işbirliği](active-directory-b2b-licensing.md).

## <a name="view-assigned-licenses"></a>Görünüm atanan lisansları

Atanan ve kullanılabilir lisans Özet görünümünü altında görüntülenen **Azure Active Directory** &gt; **lisansları** &gt; **tüm ürünleri**.

![Özet görünümü lisans](media/license-users-groups/view-license-summary.png)

Atanan kullanıcıların ve grupların ayrıntılı bir liste, belirli bir ürün seçildiğinde kullanılabilir. Merhaba **lisanslı kullanıcı** listesi şu anda bir lisans ve olup hello lisans doğrudan toohello kullanıcı veya gruptan devralınan varsa atandı kullanan tüm kullanıcıları gösterir.

![Lisans ayrıntıları görüntüle](media/license-users-groups/view-license-detail.png)

Benzer şekilde, hello **lisans grupları** liste toowhich lisansları atanmış tüm grupları gösterir. Bir kullanıcı veya grup tooopen hello seçin **lisansları** tüm lisanslar gösteren dikey atanan toothat nesnesi.

## <a name="remove-a-license"></a>Bir lisans Kaldır

tooremove bir lisans toohello kullanıcı veya grup gidin ve açmak hello **lisansları** döşeme. Merhaba lisans seçin ve tıklayın **kaldırmak**.

![Bir lisans Kaldır](media/license-users-groups/remove-license.png)

Bir gruptan hello kullanıcı tarafından devralınmış lisansları doğrudan kaldırılamaz. Bunun yerine, hello kullanıcı, bunlar hello lisans devralan hello grubundan kaldırın.


## <a name="next-steps"></a>Sonraki adımlar
Bu hızlı başlangıç nasıl tooassign toousers ve Azure AD dizini gruplarında lisansları öğrendiniz. 

Bağlantı tooconfigure abonelik lisans anlaşmalarını hello Azure portal ' Azure AD içinde aşağıdaki hello kullanabilirsiniz.

> [!div class="nextstepaction"]
> [Azure AD lisansları atama](https://aad.portal.azure.com/#blade/Microsoft_AAD_IAM/LicensesMenuBlade/Overview) 