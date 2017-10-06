---
title: "aaaAdd özel etki alanınızı adlandırın tooAzure Active Directory | Microsoft Docs"
description: "Nasıl tooadd tooAzure Active Directory, şirketinizin etki alanı adları ve nasıl tooverify hello etki alanı adı."
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: d97e57c6-578a-4929-8fb8-42e858a711c7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: curtand
ms.openlocfilehash: 88d5f443cd10b098a9a9ffb3137f5e1ca33b6aad
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

Azure Active Directory (Azure AD) kullanarak, şirket etki alanı adı tooAzure AD de ekleyebilirsiniz. Bu, kuruluşunuzun kullandığı toodo iş ve şirket etki alanı adınızı kullanarak oturum açan kullanıcıların bir etki alanı adlarına sahip olabilir. Merhaba etki alanı adı tooAzure AD eklemeye izin verir, bilinen tooyour kullanıcılar gibi tooassign kullanıcı adları hello dizinindeki 'alice@contoso.com.' Merhaba basit bir işlemdir:

1. Merhaba özel etki alanı adı tooyour Dizin Ekle
2. Merhaba etki alanı adı kayıt şirketinize hello etki alanı adı için bir DNS Girişi Ekle
3. Azure AD'de Hello özel etki alanı adını doğrulayın

## <a name="how-do-i-add-a-domain-name"></a>Bir etki alanı adı nasıl eklenir?
1. İçinde toohello oturum [Azure portal](https://portal.azure.com) hello dizin için genel yönetici olan bir hesapla.
2. Seçin **daha fazla hizmet**, girin **Azure Active Directory** hello metin kutusuna ve ardından **Enter**.
   
   ![Açılış kullanıcı yönetimi](./media/active-directory-domains-add-azure-portal/user-management.png)
3. Merhaba üzerinde ***dizin adı*** dikey penceresinde, select **etki alanı adları**.
4. Merhaba üzerinde  ***dizin adı* -etki alanı adları** dikey penceresinde, select hello **Ekle** komutu.
   
   ![Merhaba Ekle komutu seçme](./media/active-directory-domains-add-azure-portal/add-command.png)
5. Merhaba üzerinde **etki alanı adı** dikey penceresinde hello kutusunda, "contoso.com" gibi özel etki alanınızı hello adını girin ve ardından **etki alanı Ekle**. Emin tooinclude hello .com, .net veya diğer üst düzey uzantıları.
6. Merhaba üzerinde ***domainname*** dikey (Merhaba başlığında yeni etki alanı adınızı içeren açan diğer bir deyişle, hello dikey), Azure AD kuruluşunuz hello özel etki alanı adına sahip tooverify kullanacağını hello DNS girişi bilgi alın.
   
   ![DNS girişi bilgi alın](./media/active-directory-domains-add-azure-portal/get-dns-info.png)

Merhaba etki alanı adınızı ekledikten, Azure AD kuruluşunuz hello etki alanı adına sahip olduğunu doğrulamanız gerekir. Azure AD bu doğrulamayı gerçekleştirebilmesi hello DNS bölge dosyasına hello etki alanı adı için bir DNS girişi eklemeniz gerekir. Bu görev, etki alanı adı kayıt hello etki alanı adı için hello Web sitesindeki gerçekleştirilir.

## <a name="add-hello-dns-entry-at-hello-domain-name-registrar-for-hello-domain"></a>Merhaba etki alanı adı kayıt hello etki alanı için Hello DNS girişi ekleyin
özel etki alanınızı adlandırın Azure AD ile Merhaba sonraki adım toouse tooupdate hello DNS bölge hello etki alanı için bir dosyadır. Bu, kuruluşunuz hello özel etki alanı adına sahip Azure AD tooverify sağlar.

1. Oturum açma toohello etki alanı adı kayıt hello etki alanı için. Erişim tooupdate hello DNS girişi yoksa, hello kişi ya da bu erişim toocomplete adım 2 sahip ekibi ve tamamlandığında bildiğiniz toolet isteyin.
2. Güncelleştirme hello DNS bölge dosyasına hello DNS girişini ekleyerek hello etki alanı için tooyou Azure AD tarafından sağlanır. Bu DNS girişi hello etki alanının, sahipliği Azure AD tooverify sağlar. Merhaba DNS girişi, posta yönlendirme veya web barındırma gibi davranışları değiştirmez.

Bu eklemeyi hello DNS girişi ile ilgili Yardım için okuma [popüler DNS kayıt şirketlerinde DNS girişi ekleme yönergeleri](https://support.office.com/article/Create-DNS-records-for-Office-365-when-you-manage-your-DNS-records-b0f3fdca-8a80-4e8e-9ef3-61e8a2a9ab23/)

## <a name="verify-hello-domain-name-with-azure-ad"></a>Azure AD ile Merhaba etki alanı adını doğrulayın
Merhaba DNS girişini ekledikten sonra hazır tooverify hello etki alanı adını Azure AD ile demektir.

Merhaba DNS kayıtları yalnızca dağıtıldıktan sonra bir etki alanı adı doğrulanabilir. Bu yayma genellikle yalnızca birkaç saniye sürer, ancak bazen bir saat veya daha fazla sürebilir. Doğrulama hello ilk kez işe yaramazsa, daha sonra yeniden deneyin.

1. İçinde toohello oturum [Azure portal](https://portal.azure.com) hello dizin için genel yönetici olan bir hesapla.
2. Seçin **Gözat**kullanıcı yönetimi hello metin kutusuna girin ve ardından **Enter**.
   
   ![Açılış kullanıcı yönetimi](./media/active-directory-domains-add-azure-portal/user-management.png)
3. Merhaba üzerinde **kullanıcı yönetimi - etki alanı adları** dikey penceresinde, tooverify istediğinizi seçin hello doğrulanmamış etki alanı adı.
4. Merhaba üzerinde ***domainname*** dikey penceresinde (Merhaba başlığında yeni etki alanı adınızı içeren açan diğer bir deyişle, hello dikey penceresinde) seçin **doğrula** toocomplete hello doğrulama.

Artık [özel etki alanı adınızı içeren kullanıcı adları atayabilirsiniz](active-directory-users-create-azure-portal.md).

## <a name="troubleshooting"></a>Sorun giderme
Bir özel etki alanı adını doğrulayamıyorsanız hello aşağıdakileri deneyin. Merhaba en yaygın ve iş toohello az ortak aşağı ile başlayacağız.

1. **Bir saat bekleyin**. Azure AD etki alanı hello doğrulayabilirsiniz önce DNS kayıtlarını toopropagate gerekir. Bu işlem bir saat veya daha fazla sürebilir.
2. **DNS kaydı girildi hello ve doğru olduğundan emin olun**. Merhaba etki alanı adı kayıt hello etki alanı için hello Web sitesindeki bu adımı tamamlayın. Hello DNS girişini DNS bölge dosyasına hello sunmak veya tam bir eşleşme hello DNS girişi ile değilse Azure AD, sağladığınız değilse azure AD hello etki alanı adını doğrulayın. Merhaba etki alanı adı kayıt hello etki alanı için erişim tooupdate DNS kayıtlarını yoksa hello kişi veya ekiple erişim izni kuruluşunuz hello DNS girişi paylaşmasına ve tooadd hello DNS girdisi isteyin.
3. **Merhaba etki alanı adını Azure AD içinde başka bir dizinden silin**. Bir etki alanı adı yalnızca tek bir dizinde doğrulanabilir. Bir etki alanı adı önce başka bir dizinde doğrulandıysa yeni dizininizde doğrulanabilmesi için oradan silinmelidir. etki alanı adları, silinmesi hakkında toolearn okuma [özel etki alanı adlarını yönetme](active-directory-domains-manage-azure-portal.md).    

## <a name="add-more-custom-domain-names"></a>Daha fazla özel etki alanı ekleme
Kuruluşunuz birden fazla özel etki alanı adları, 'contoso.com' ve 'contosobank.com' gibi kullanıyorsa tooa en fazla 900 etki alanı adlarını ekleyebilirsiniz. Bu makale tooadd etki alanı içinde her aynı adımları hello kullanın.

## <a name="next-steps"></a>Sonraki adımlar
[Özel etki alanı adlarını yönetme](active-directory-domains-manage-azure-portal.md)

