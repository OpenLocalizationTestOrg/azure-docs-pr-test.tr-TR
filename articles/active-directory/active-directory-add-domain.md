---
title: "aaaAdd özel etki alanınızı adlandırın tooAzure Active Directory | Microsoft Docs"
description: "Nasıl tooadd tooAzure Active Directory, şirketinizin etki alanı adları ve nasıl tooverify hello etki alanı adı."
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 35a6e20a-9907-432b-9d36-16b916a5c249
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/24/2017
ms.author: curtand
ms.custom: oldportal;it-pro;
robots: NOINDEX
ms.openlocfilehash: eb208138f2633aaecc54f68dc947caf80d856d23
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="add-a-custom-domain-name-tooazure-active-directory"></a>Özel etki alanı adı tooAzure Active Directory ekleme
> [!div class="op_single_selector"]
> * [Azure portal](active-directory-domains-add-azure-portal.md)
> * [Klasik Azure Portalı](active-directory-add-domain.md)
> 
> 

Kuruluşunuz toodo iş kullanır ve kullanıcılarınız şirket etki alanı adınızı kullanarak tooyour şirket ağında oturum bir veya daha fazla etki alanı adları açıyor. Azure Active Directory (Azure AD) kullanıyorsanız, sizin şirket etki alanı adı tooAzure AD de ekleyebilirsiniz. Tanıdık tooyour kullanıcılar gibi tooassign kullanıcı adları hello dizininde bu sayede 'alice@contoso.com.' Merhaba basit bir işlemdir:

1. Merhaba özel etki alanı adı tooyour Dizin Ekle
2. Merhaba etki alanı adı kayıt şirketinize hello etki alanı adı için bir DNS Girişi Ekle
3. Azure AD'de Hello özel etki alanı adını doğrulayın

> [!IMPORTANT]
> Microsoft önerir hello kullanarak Azure AD'yi yönetme [Azure AD Yönetim Merkezi](https://aad.portal.azure.com) hello yerine Azure portal hello bu makalede başvurulan Klasik Azure portalı. Nasıl tooadd şirket etki alanı adınızı hello Azure AD Yönetim Merkezi'nden görmek için [Azure Active Directory'de yönetici rolleri atama](active-directory-domains-add-azure-portal.md).

Active Directory Federasyon Hizmetleri (AD FS) veya şirket ağınızdaki farklı güvenlik belirteci hizmeti (STS) ile kullanılan, özel etki alanı adı toobe tooconfigure düşünüyorsanız hello yönergeleri izleyin [Ekle ve bir etki alanı için yapılandırma Azure Active Directory ile Federasyon](active-directory-add-domain-federated.md). Kurumsal dizin tooAzure AD, toosynchronize kullanıcılar planlıyorsanız yararlıdır ve [parola karması eşitlemesi](active-directory-aadconnectsync-implement-password-synchronization.md) , gereksinimleri karşılamıyor.

## <a name="add-a-custom-domain-name-tooyour-directory"></a>Özel etki alanı adı tooyour Dizin Ekle
1. İçinde toohello oturum [Klasik Azure portalı](https://manage.windowsazure.com/) Azure AD dizininizin genel yöneticisi olan bir kullanıcı hesabı ile.
2. İçinde **Active Directory**dizininizi açın ve seçin hello **etki alanları** sekmesi.
3. Merhaba komut çubuğunda seçin **Ekle**. Merhaba "contoso.com" gibi özel bir etki alanı adını girin. Tooinclude hello .com, .net veya diğer üst düzey uzantıları ve için "çoklu oturum açma" Merhaba kutusunu seçili olarak bırakın emin olun (Federasyon) temizlendi.
4. **Add (Ekle)** seçeneğini belirleyin.
5. Merhaba ikinci sayfasında hello etki alanı Ekle Sihirbazı'nın hello Azure AD kuruluşunuz hello özel etki alanı adına sahip tooverify kullanacağı DNS girişi alın.

Merhaba etki alanı adınızı ekledikten, Azure AD kuruluşunuz hello etki alanı adına sahip olduğunu doğrulamanız gerekir. Azure AD bu doğrulamayı gerçekleştirebilmesi hello DNS bölge dosyasına hello etki alanı adı için bir DNS girişi eklemeniz gerekir. Bu görev, etki alanı adı kayıt hello etki alanı adı için hello Web sitesindeki gerçekleştirilir.

## <a name="add-hello-dns-entry-at-hello-domain-name-registrar-for-hello-domain"></a>Merhaba etki alanı adı kayıt hello etki alanı için Hello DNS girişi ekleyin
özel etki alanınızı adlandırın Azure AD ile Merhaba sonraki adım toouse tooupdate hello DNS bölge hello etki alanı için bir dosyadır. Bu, kuruluşunuz hello özel etki alanı adına sahip Azure AD tooverify sağlar.

1. Oturum açma toohello etki alanı adı kayıt hello etki alanı için. Erişim tooupdate hello DNS girişi yoksa, hello kişi ya da bu erişim toocomplete adım 2 sahip ekibi ve tamamlandığında bildiğiniz toolet isteyin.
2. Güncelleştirme hello DNS bölge dosyasına hello DNS girişini ekleyerek hello etki alanı için tooyou Azure AD tarafından sağlanır. Bu DNS girişi hello etki alanının, sahipliği Azure AD tooverify sağlar. Merhaba DNS girişi, posta yönlendirme veya web barındırma gibi davranışları değiştirmez.

Bu eklemeyi hello DNS girişi ile ilgili Yardım için okuma [popüler DNS kayıt şirketlerinde DNS girişi ekleme yönergeleri](https://support.office.com/article/Create-DNS-records-for-Office-365-when-you-manage-your-DNS-records-b0f3fdca-8a80-4e8e-9ef3-61e8a2a9ab23/)

## <a name="verify-hello-domain-name-with-azure-ad"></a>Azure AD ile Merhaba etki alanı adını doğrulayın
Merhaba DNS girişini ekledikten sonra hazır tooverify hello etki alanı adını Azure AD ile demektir.

Merhaba yaşamaya devam ediyorsanız **etki alanı Ekle** Sihirbazı'nı açın, select **doğrula** hello sihirbazının üçüncü sayfasında hello. Seçtiğinizde, **doğrula**, Azure AD hello DNS bölge dosyasına hello etki alanı için DNS girişi hello için görünür. Merhaba DNS kayıtları yalnızca dağıtıldıktan sonra azure AD hello etki alanı adı doğrulayabilirsiniz. Bu yayma genellikle yalnızca birkaç saniye sürer, ancak bazen bir saat veya daha fazla sürebilir. Doğrulama hello ilk kez işe yaramazsa, daha sonra yeniden deneyin.

Merhaba, **etki alanı Ekle** Sihirbazı hala açık değilse, hello etki alanında hello doğrulayabilirsiniz [Klasik Azure portalı](https://manage.windowsazure.com/):

1. Azure AD dizininizin genel yöneticisi olan bir kullanıcı hesabıyla oturum açın.
2. Dizin ve select hello açmak **etki alanları** sekmesi.
3. Tooverify istediğiniz ve seçin select hello etki alanı adı **doğrula** hello komut çubuğunda.
4. Seçin **doğrula** hello iletişim kutusu toocomplete hello doğrulamasında.

Artık [özel etki alanı adınızı içeren kullanıcı adları atayabilirsiniz](active-directory-add-domain-add-users.md).

## <a name="troubleshooting"></a>Sorun giderme
Bir özel etki alanı adını doğrulayamıyorsanız hello aşağıdakileri deneyin. Merhaba en yaygın ve iş toohello az ortak aşağı ile başlayacağız.

1. **Bir saat bekleyin**. Azure AD etki alanı hello doğrulayabilirsiniz önce DNS kayıtlarını toopropagate gerekir. Bu işlem bir saat veya daha fazla sürebilir.
2. **DNS kaydı girildi hello ve doğru olduğundan emin olun**. Merhaba etki alanı adı kayıt hello etki alanı için hello Web sitesindeki bu adımı tamamlayın. Hello DNS girişini DNS bölge dosyasına hello sunmak veya tam bir eşleşme hello DNS girişi ile değilse Azure AD, sağladığınız değilse azure AD hello etki alanı adını doğrulayın. Merhaba etki alanı adı kayıt hello etki alanı için erişim tooupdate DNS kayıtlarını yoksa hello kişi veya ekiple erişim izni kuruluşunuz hello DNS girişi paylaşmasına ve tooadd hello DNS girdisi isteyin.
3. **Merhaba etki alanı adını Azure AD içinde başka bir dizinden silin**. Bir etki alanı adı yalnızca tek bir dizinde doğrulanabilir. Bir etki alanı adı önce başka bir dizinde doğrulandıysa yeni dizininizde doğrulanabilmesi için oradan silinmelidir. etki alanı adları, silinmesi hakkında toolearn okuma [özel etki alanı adlarını yönetme](active-directory-add-manage-domain-names.md).

## <a name="add-more-custom-domain-names"></a>Daha fazla özel etki alanı ekleme
Kuruluşunuz birden fazla özel etki alanı adları, 'contoso.com' ve 'contosobank.com' gibi kullanıyorsa tooa en fazla 900 etki alanı adlarını ekleyebilirsiniz. Bu makale tooadd etki alanı içinde her aynı adımları hello kullanın.

## <a name="next-steps"></a>Sonraki adımlar
* [Özel etki alanı adınızı içeren kullanıcı adları atama](active-directory-add-domain-add-users.md)
* [Özel etki alanı adlarını yönetme](active-directory-add-manage-domain-names.md)
* [Azure AD'deki etki alanı yönetimi kavramları hakkında bilgi edinme](active-directory-add-domain-concepts.md)
* [Kullanıcılarınız oturum açtığında şirketinizin markasını gösterme](active-directory-add-company-branding.md)
* [Azure AD PowerShell toomanage etki alanı adlarını kullanın](https://msdn.microsoft.com/library/azure/e1ef403f-3347-4409-8f46-d72dafa116e0#BKMK_ManageDomains)

