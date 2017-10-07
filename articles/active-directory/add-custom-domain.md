---
title: "özel etki alanı tooAzure AD aaaAdd | Microsoft Docs"
description: "Açıklar nasıl tooadd Azure Active Directory'de özel etki alanı."
services: active-directory
author: jeffgilb
manager: femila
ms.assetid: 0a90c3c5-4e0e-43bd-a606-6ee00f163038
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2017
ms.author: jeffgilb
ms.reviewer: jsnow
ms.custom: it-pro
ms.openlocfilehash: 878cecad364ec47f1c6755d742aaccbce627dc5e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="quickstart-add-a-custom-domain-name-tooazure-active-directory"></a>Hızlı Başlangıç: özel etki alanı adı tooAzure Active Directory Ekle

Her Azure AD dizini hello biçiminde bir ilk etki alanı adı ile birlikte gelen *domainname*. onmicrosoft.com. hello ilk etki alanı adı değiştirilemez veya silinemez, ancak, şirket etki alanı adı tooAzure AD de ekleyebilirsiniz. Örneğin, kuruluşunuzun büyük olasılıkla diğer etki alanı adları kullanılan toodo iş ve şirket etki alanı adınızı kullanarak oturum açan kullanıcıların sahiptir. Özel etki alanı adları tooAzure AD eklemeye izin verir, bilinen tooyour kullanıcılar gibi tooassign kullanıcı adları hello dizinindeki 'alice@contoso.com.' yerine ' @ alice*<domain name>*. onmicrosoft.com'. Merhaba basit bir işlemdir:

1. Merhaba özel etki alanı adı tooyour Dizin Ekle
2. Merhaba etki alanı adı kayıt şirketinize hello etki alanı adı için bir DNS Girişi Ekle
3. Azure AD'de Hello özel etki alanı adını doğrulayın

## <a name="add-your-custom-domain"></a>Özel etki alanınızı ekleme
1. İçinde toohello oturum [Azure portal](https://portal.azure.com) hello dizin için genel yönetici olan bir hesapla.
2. Seçin **daha fazla hizmet**, girin **Azure Active Directory** hello metin kutusuna ve ardından **Enter**.
   
   ![Açılış kullanıcı yönetimi](./media/active-directory-domains-add-azure-portal/user-management.png)
3. Merhaba üzerinde ***dizin adı*** dikey penceresinde, select **etki alanı adları**.
4. Merhaba üzerinde  ***dizin adı* -etki alanı adları** dikey penceresinde, select hello **Ekle** komutu.
   
   ![Merhaba Ekle komutu seçme](./media/active-directory-domains-add-azure-portal/add-command.png)
5. Merhaba üzerinde **etki alanı adı** dikey penceresinde hello kutusunda, "contoso.com" gibi özel etki alanınızı hello adını girin ve ardından **etki alanı Ekle**. Emin tooinclude hello .com, .net veya diğer üst düzey uzantıları.
6. Merhaba üzerinde ***etki alanı adı*** (ile özel etki alanı adınızı hello başlığında), dikey penceresinde hello kuruluşunuz hello özel etki alanı adına sahip DNS girdisi bilgi toouse tooverify alın.
   
   ![DNS girişi bilgi alın](./media/active-directory-domains-add-azure-portal/get-dns-info.png)

> [!TIP]
> Şirket içi Windows Server'ınızın Azure AD ile toofederate planlama sonra tooselect hello gereksinim **t tooconfigure bu etki alanı için çoklu oturum açma bilgilerimi yerel Active Directory ile planlama** hello Azure AD Connect aracı çalıştırdığınızda, onay kutusu toosynchronize dizinlerinizi. Tooregister etmeniz hello Seçtiğiniz federasyona eklemek için şirket içi dizininizde hello ile aynı etki alanı adı **Azure AD etki alanı** hello Sihirbazı'nda adım. Hangi adımın gibi görünüyor hello Sihirbazı'nda görebilirsiniz [bu yönergelerindeki](./connect/active-directory-aadconnect-get-started-custom.md#verify-the-azure-ad-domain-selected-for-federation). Hello Azure AD Connect aracını yoksa, şunları yapabilirsiniz [buradan indirin](http://go.microsoft.com/fwlink/?LinkId=615771).

Merhaba etki alanı adınızı ekledikten, Azure AD kuruluşunuz hello etki alanı adına sahip olduğunu doğrulamanız gerekir. Azure AD bu doğrulamayı gerçekleştirebilmesi hello DNS bölge dosyasına hello etki alanı adı için bir DNS girişi eklemeniz gerekir. Bu görev, etki alanı adı kayıt hello etki alanı adı için hello Web sitesindeki gerçekleştirilir.

## <a name="add-hello-dns-entry-at-hello-domain-name-registrar-for-hello-domain"></a>Merhaba etki alanı adı kayıt hello etki alanı için Hello DNS girişi ekleyin
özel etki alanınızı adlandırın Azure AD ile Merhaba sonraki adım toouse tooupdate hello DNS bölge hello etki alanı için bir dosyadır. Azure AD kuruluşunuz hello özel etki alanı adına sahip doğrulayabilirsiniz.

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
4. Merhaba üzerinde ***etki alanı adı*** dikey penceresinde (Merhaba başlığında yeni etki alanı adınızı içeren açan diğer bir deyişle, hello dikey penceresinde) seçin **doğrula** toocomplete hello doğrulama.

> [!TIP]
> Too900 özel etki alanı adlarını ekleyebilirsiniz, ancak yalnızca bir olabilir [hello Azure AD dizininiz için birincil etki alanı adı olarak ayarlanmış](active-directory-domains-manage-azure-portal.md#set-the-primary-domain-name-for-your-azure-ad-directory) yeni hesapları oluşturduğunuzda varsayılan olarak kullanılır.

Özel etki alanı adınızı kullanarak, şirket içi kullanıcı hesabı bilgilerini güncelleştirme daha önce Eşitlenenleri veya bulut tabanlı kullanıcı hesaplarına şimdi oluşturabilirsiniz. Ayrıca önceden eşitlenen kullanıcı hesabı etki alanı soneki bilgileri kullanarak değiştirebileceğiniz [Microsoft PowerShell](https://msdn.microsoft.com/library/azure/e1ef403f-3347-4409-8f46-d72dafa116e0#BKMK_ManageDomains) veya hello [grafik API'si](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/domains-operations).

## <a name="troubleshooting"></a>Sorun giderme
Özel etki alanı adını doğrulayamıyorsanız, aşağıdaki sorun giderme adımları hello deneyin:

1. **Bir saat bekleyin**. Azure AD etki alanı hello doğrulayabilirsiniz önce DNS kayıtlarını toopropagate gerekir. Bu işlem bir saat veya daha fazla sürebilir.
2. **DNS kaydı girildi hello ve doğru olduğundan emin olun**. Merhaba etki alanı adı kayıt hello etki alanı için hello Web sitesindeki bu adımı tamamlayın. Hello DNS girişini DNS bölge dosyasına hello sunmak veya tam bir eşleşme hello DNS girişi ile değilse Azure AD, sağladığınız değilse azure AD hello etki alanı adını doğrulayın. Merhaba etki alanı adı kayıt hello etki alanı için erişim tooupdate DNS kayıtlarını yoksa hello kişi veya ekiple erişim izni kuruluşunuz hello DNS girişi paylaşmasına ve tooadd hello DNS girdisi isteyin.
3. **Merhaba etki alanı adını Azure AD içinde başka bir dizinden silin**. Bir etki alanı adı yalnızca tek bir dizinde doğrulanabilir. Bir etki alanı adı önce başka bir dizinde doğrulandıysa yeni dizininizde doğrulanabilmesi için oradan silinmelidir. etki alanı adları, silinmesi hakkında toolearn okuma [özel etki alanı adlarını yönetme](active-directory-domains-manage-azure-portal.md).    

## <a name="add-more-custom-domain-names"></a>Daha fazla özel etki alanı ekleme
Kuruluşunuz 'contoso.com' ve 'contosobank.com' gibi birden fazla özel etki alanı adı kullanıyorsa, her biri için bu makaledeki hello adımları yineleyerek too900 daha ekleyebilirsiniz.

### <a name="learn-more"></a>Daha fazla bilgi edinin
[Azure AD'de özel etki alanı adlarına kavramsal genel bakış](active-directory-add-domain-concepts.md)

[Özel etki alanı adlarını yönetme](active-directory-domains-manage-azure-portal.md)


## <a name="next-steps"></a>Sonraki adımlar
Bu Hızlı Başlangıç, öğrendiğinize nasıl tooadd özel etki alanı tooAzure AD. 

Bağlantı tooadd yeni bir özel etki alanı Azure AD'de hello Azure portal ' aşağıdaki hello kullanabilirsiniz.

> [!div class="nextstepaction"]
> [Özel bir etki alanı Ekle](https://aad.portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/QuickStart) 