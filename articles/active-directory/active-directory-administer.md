---
title: "aaaHow toouse bir Azure Active Direcory Kiracı directory genel bakış | Microsoft Docs"
description: "Ne açıklanır Azure AD kiracısı olan ve nasıl toomanage Azure Active Directory'yi kullanarak Azure"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
ms.assetid: d4ca2365-6729-48f7-bb7f-c0f5ffe740a3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/23/2017
ms.author: curtand
ms.reviewer: jeffsta
ms.custom: it-pro;oldportal
ms.openlocfilehash: ddb16d89bf06a3753ed5106bd95162130ad51b08
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-your-azure-ad-directory"></a>Azure AD dizininizi yönetme

## <a name="what-is-an-azure-ad-tenant"></a>Azure AD kiracısı nedir?
Azure Active Directory’de (Azure AD) kiracı, kuruluşunuzun Azure veya Office 365 gibi bir Microsoft bulut hizmetinde oturum açtığında aldığı ve sahip olduğu bir Azure AD dizininin adanmış örneğidir. Her Azure AD dizini, diğer Azure AD dizinlerinden farklı ve ayrıdır. Kurumsal ofis binasının yalnızca gibi güvenli varlık belirli tooonly kuruluşunuz, Azure AD dizini de güvenli bir varlık yalnızca kuruluşunuz tarafından kullanılmak üzere tasarlanmış toobe oluştu. böylece kullanıcılar ve yöneticiler bir Azure AD Directory yanlışlıkla veya kötü amaçlı olarak başka bir dizindeki verilere erişemezsiniz hello Azure AD mimarisi müşteri verileri ve kimlik bilgileri yalıtır.

![Azure Active Directory'yi yönetme](./media/active-directory-administer/aad_portals.png)

## <a name="how-can-i-get-an-azure-ad-directory"></a>Azure AD dizinine nasıl sahip olabilirim?
Azure AD hello çekirdek dizin ve kimlik yönetimi özellikleri dahil olmak üzere Microsoft bulut hizmetlerinin çoğu arkasında sağlar:

* Azure
* Microsoft Office 365
* Microsoft Dynamics CRM Online
* Microsoft Intune

Bu Microsoft bulut hizmetlerinden herhangi birine kaydolduğunuzda, bir Azure AD dizinine sahip olursunuz. Gerektikçe ek dizinler oluşturabilirsiniz. Örneğin, ilk dizininizi üretim dizini olarak tutup test veya hazırlama işlemleri için başka bir dizin oluşturabilirsiniz.

### <a name="using-hello-azure-ad-directory-that-comes-with-a-new-azure-subscription"></a>Yeni bir Azure aboneliğiyle birlikte gelen hello Azure AD dizini kullanma

Diğer Microsoft Hizmetleri için kaydolduğunuzda ilk hizmetiniz için kullanılan hello yönetici hesabı kullanmanızı öneririz. Merhaba, sağladığınız bilgileri hello ilk kez, kaydolmak için bir Microsoft hizmeti kullanılan toocreate yeni bir Azure AD dizini örneğinin, kuruluşunuz için. Bu dizin tooauthenticate kullanırsanız tooother Microsoft hizmetlerine abone olduğunuzda, oturum açma denemesi, varolan kullanıcı hesapları, ilkeler, ayarlar ya da şirket içi dizin tümleştirmesi, varsayılan dizininizde yapılandırmanız hello kullanabilirsiniz.

Örneğin, oturum için bir Microsoft Intune abonelik ve şirket içi Active Directory'nizi Azure AD diziniyle daha fazla eşitleme yaparsanız, Office 365 gibi başka bir Microsoft hizmeti için kaydolun ve kolayca hello elde aynı dizinde Microsoft Intune sahip tümleştirme avantajlarından.

Şirket içi dizininizi Azure AD ile tümleştirme hakkında daha fazla bilgi için bkz. [Azure AD Connect ile dizin tümleştirme](active-directory-aadconnect.md).

### <a name="associate-an-existing-azure-ad-directory-with-a-new-azure-subscription"></a>Mevcut bir Azure AD dizinini yeni bir Azure aboneliğiyle ilişkilendirme
Yeni bir Azure aboneliği ile Merhaba ilişkilendirebilirsiniz oturum açma mevcut bir Office 365 veya Microsoft Intune aboneliğiniz için kimlik doğrulaması aynı dizin. Bu senaryo hakkında daha fazla bilgi için bkz: [bir Azure aboneliği tooanother hesap sahipliğini aktarma](../billing/billing-subscription-transfer.md)

### <a name="create-an-azure-ad-directory-by-signing-up-for-a-microsoft-cloud-service-as-an-organization"></a>Microsoft bulut hizmetine bir kuruluş olarak kaydolarak Azure AD dizini oluşturma
Abonelik tooa Microsoft bulut hizmeti henüz yoksa, bağlantılar toosign takip hello birini kullanabilirsiniz. İlk hizmetiniz için kaydolduğunuzda otomatik olarak bir Azure AD dizini oluşturulur.

* [Microsoft Azure](https://account.azure.com/organization)
* [Office 365](http://products.office.com/business/compare-office-365-for-business-plans/)
* [Microsoft Intune](https://portal.office.com/Signup/Signup.aspx?OfferId=40BE278A-DFD1-470a-9EF7-9F2596EA7FF9&dl=INTUNE_A&ali=1#0%20)

### <a name="how-toochange-hello-default-directory-for-a-subscription"></a>Nasıl toochange hello bir abonelik için varsayılan dizini

1. İçinde toohello oturum [Azure hesap Merkezi](https://account.windowsazure.com/Home/Index) hello hello abonelik tootransfer abonelik olma hesap yöneticisi olan bir hesapla.
2. Hedeflenen hello dizinde toobe hello abonelik sahibi olan isteyen bu hello kullanıcı emin olun.
3. **Aboneliği devret**'e tıklayın.
4. Merhaba alıcı belirtin. Merhaba alıcı otomatik olarak kabul bağlantı içeren bir e-posta alır.
5. Merhaba alıcı hello bağlantıya tıklar ve ödeme bilgilerini girme dahil hello yönergeleri izler. Merhaba alıcı başarılı olduğunda hello abonelik aktarılır. 
6. Merhaba varsayılan dizini hello aboneliğin dönüştürülür içinde olduğu hello abonelik sahipliği aktarımı başarılı olup olmadığını kullanıcı hello toohello dizin.

### <a name="manage-hello-default-directory-in-azure"></a>Azure'da Hello varsayılan dizini yönetme
Azure için kaydolduğunuzda, aboneliğiniz ile bir varsayılan Azure AD dizini ilişkilendirilir. Azure AD kullanmanın maliyeti yoktur ve dizinleriniz ücretsiz kaynaklardır. Ayrı olarak lisanslanan ve şirkete özel oturum açma, self servis parola sıfırlama gibi ek işlevler sunan ücretli Azure AD hizmetleri vardır. Merhaba varsayılan yerine sahip olduğunuz bir DNS adını kullanarak özel bir etki alanı da oluşturabilirsiniz *. onmicrosoft.com etki alanı.

## <a name="how-can-i-manage-directory-data"></a>Dizin verilerini nasıl yönetebilirim?
tooadminister bir veya daha fazla Microsoft bulut hizmeti aboneliklerinizde, hello kullanabilirsiniz [Azure AD Yönetim Merkezi](https://aad.portal.azure.com)hello Microsoft Intune hesap portalı veya hello [Office 365 Yönetim Merkezi](https://portal.office.com/) toomanage, Kuruluşunuzun dizin verileri. Aynı zamanda [Azure Active Directory PowerShell cmdlet'lerini](https://docs.microsoft.com/powershell/azure/active-directory) toohelp Azure AD'de depolanan verileri yönetin.

Bu portallardan (veya cmdlet'lerden) birini kullanarak şunları yapabilirsiniz:

* Kullanıcı ve grup hesapları oluşturma ve yönetme
* Kuruluşunuzun abonelikleri için bulut hizmetlerini yönetme
* Azure AD kimlik ve kimlik doğrulama hizmetleri ile şirket içi tümleştirmeyi ayarlama

Hello Azure AD Yönetim Merkezi, Office 365 Yönetim Merkezi, Microsoft Intune hesap portalı ve Azure AD cmdlet'lerinin hello tüm okuma ve yazma tooa tek paylaşılan kuruluşunuzun dizinle ilişkili Azure AD örneğini. Bu araçların her biri, dizin verilerinizdeki değişiklikleri alan bir ön uç arabirimi olarak görev yapar.

Hello portalları veya hello bağlamında Bu hizmetlerden biri oturum açtıktan sonra cmdlet'leri herhangi birini kullanarak, kuruluşunuzun verileri değiştirdiğinizde, hello değişiklikler de hello diğer portalları, oturum açtığınızda hello gösterilir. Bu veriler üzerinde hello Microsoft bulut Hizmetleri toowhich abone paylaşılır.

Merhaba Office 365 Yönetim Merkezi tooblock bir kullanıcının oturum açarken, eylem blokları içinde tooany imzalama kullanıcının hello kullanırsanız, örneğin, diğer hizmet toowhich Kuruluşunuz şu anda abone olduğu. Merhaba görüntülerseniz aynı kullanıcı hesabı hello Microsoft Intune hesap portalındaki de gördüğünüz hello kullanıcı engellendi.

## <a name="how-can-i-add-and-manage-multiple-directories"></a>Birden fazla dizini nasıl ekleyip yönetebilirim?
Yapabilecekleriniz [hello Azure portalında bir Azure AD dizini eklemek](https://portal.azure.com/#create/Microsoft.AzureActiveDirectory). Merhaba bilgileri doldurun ve seçin **oluşturma**.

Her dizini tamamen bağımsız bir kaynak olarak yönetebilirsiniz: Her dizin eşdüzeyde, tam özellikli ve yönettiğiniz diğer dizinlerden mantıksal olarak bağımsızdır ve dizinler arasında üst-alt ilişkisi yoktur. Dizinler arasındaki bu bağımsızlığa kaynak bağımsızlığı, yönetim bağımsızlığı ve eşitleme bağımsızlığı dahildir.

* **Kaynak bağımsızlığı**. Oluşturursanız veya bir dizinde kaynak silin, dış kullanıcıların hello kısmi durumla başka bir dizinde herhangi bir kaynak üzerinde hiçbir etkisi yoktur. Bir dizinde "contoso.com" özel etki alanını kullanırsanız başka bir dizinde kullanamazsınız.
* **Yönetim bağımsızlığı**.  "Contoso" dizininin yönetici olmayan bir kullanıcısı "Test" adlı bir test dizini oluşturursa:
  
  * bir yönetici 'Test' özellikle vermediği sürece hiçbir doğrudan yönetim ayrıcalıkları toodirectory 'Test' hello Yöneticiler 'Contoso' dizininin sahiptir. Yöneticileri 'Contoso', 'Test' oluşturulan hello kullanıcı hesabını denetleyebildiği erişim toodirectory 'Test' kontrol edebilirsiniz
    
  * Atadığınız veya herhangi bir yönetici rolü Kaldır bir dizindeki hello değişikliği bir kullanıcı için bir yönetici rolü etkilemez kullanıcı başka bir dizinde sahip.
* **Eşitleme bağımsızlığı**. Her Azure yapılandırabilirsiniz AD Kiracı bağımsız olarak bir tek örnek hello Azure AD Connect dizin eşitleme aracından tooget verileri.

Diğer Azure kaynaklarının aksine dizinlerinizin bir Azure aboneliğinin alt kaynakları olmadığını unutmayın. İptal etmek veya Azure aboneliği tooexpire izin vermek istiyorsanız, bu nedenle hello Office 365 Yönetici merkezi gibi Azure AD PowerShell, hello Azure grafik API'sini veya diğer arabirimleri kullanarak dizin verilerinize erişmeye devam edebilirsiniz. Ayrıca, başka bir abonelik hello dizinle ilişkilendirebilirsiniz.

## <a name="how-tooprepare-toodelete-an-azure-ad-directory"></a>Nasıl tooprepare toodelete Azure AD dizini
Genel yöneticinin Azure AD dizini hello portalından silebilirsiniz. Bir dizin silindiğinde, hello dizinde bulunan tüm kaynaklar da silinir. Silmeden önce dizin hello mu olduğunu doğrulayın.

> [!NOTE]
> Merhaba kullanıcı bir iş veya Okul hesabıyla oturum açtıysanız, hello kullanıcı toodelete kendi giriş dizininde bağlanmıyor gerekir. Örneğin, Merhaba, kullanıcı olarak oturum joe@contoso.onmicrosoft.com, bu kullanıcı, varsayılan etki alanı contoso.onmicrosoft.com olan hello dizini silemezsiniz.

Azure AD belirli koşullar sağlanmadığı toodelete bir dizin olmasını gerektirir. Bu, bir dizin olumsuz silme kullanıcı veya kullanıcılar toosign tooOffice 365 içinde veya azure'daki kaynaklara erişememeleri hello yeteneği gibi uygulamaları etkiler riskini azaltır. Örneğin, bir abonelik için bir dizin yanlışlıkla silinirse, ardından kullanıcılar erişemez Bu abonelik için Azure kaynaklarını hello.

Aşağıdaki koşullar hello denetlenir:

* Merhaba yalnızca kullanıcı hello dizinindeki toodelete hello dizin hello genel bir yönetici olmalıdır. Merhaba dizin silinmeden önce diğer tüm kullanıcılar silinmelidir. Kullanıcıların şirket içi, eşitlendikten sonra eşitleme devre dışı ve kullanarak hello bulut dizininde hello kullanıcılar silinmelidir Azure portalında veya Azure PowerShell cmdlet'leri hello. Gereksinim toodelete grupları veya hello Office 365 Yönetim Merkezi'nden eklenen kişiler gibi kişiler yoktur.
* Merhaba Directory'de hiçbir uygulamalar olabilir. Merhaba dizin silinmeden önce tüm uygulamaların silinmesi gerekir.
* Çok faktörlü kimlik doğrulama sağlayıcısı yok bağlantılı toohello dizin olabilir.
* Microsoft Azure, Office 365 gibi Microsoft çevrimiçi hizmetlerine ilişkin hiçbir aboneliğin olabilir veya Azure AD Premium hello dizin ile ilişkilendirilmiştir. Örneğin, sizin için Azure'da varsayılan bir dizin oluşturulduysa ve Azure aboneliğinizin kimlik doğrulaması için hâlâ bu dizini kullanıyor olması halinde bu dizini silemezsiniz. Benzer şekilde, başka bir kullanıcı dizinle bir aboneliği ilişkilendirdiyse o dizini silemezsiniz. 


## <a name="next-steps"></a>Sonraki adımlar
* [Azure AD Forumu](https://social.msdn.microsoft.com/Forums/home?forum=WindowsAzureAD)
* [Azure Multi-Factor Authentication Forumu](https://social.msdn.microsoft.com/Forums/home?forum=windowsazureactiveauthentication)
* [Azure soruları için Stack Overflow](http://stackoverflow.com/questions/tagged/azure)
* [Azure Active Directory PowerShell](https://docs.microsoft.com/powershell/azure/active-directory)
* [Azure AD’de yönetici rolü atama](active-directory-assign-admin-roles.md)
