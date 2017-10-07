---
title: "aaaAdd özel etki alanı adı ve Federasyon oturum açma tooAzure Active Directory'yi ayarlama | Microsoft Docs"
description: "Nasıl tooadd tooAzure Active Directory tooset federe oturum açma Azure Active Directory ile şirket içi Federasyon çözümünüzü arasında yukarı şirketinizin etki alanı adları"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 27126c7e-e6d6-4ef3-a4fb-f5f0706e749d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: curtand
ms.openlocfilehash: 77f8cc87c27871ac96581360762aaa8d24c0eb8d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="add-your-custom-domain-name-tooazure-active-directory"></a>Özel etki alanı adı tooAzure Active Directory ekleme
‘contoso.com’ gibi özel bir etki alanı adını, contoso.com içindeki kullanıcılar şirket ağınızdan çoklu federasyon oturumu açma deneyimi yaşayabilsin diye yapılandırabilirsiniz. Active Directory Federasyon Hizmetleri (AD FS) zaten varsa veya Kurumsal ağınızda çalışan farklı Federasyon sunucusu, Azure AD toouse özel etki alanı adınızı hello Azure AD Connect aracını kullanarak yapılandırabilirsiniz. Azure AD Connect toodeploy yeni bir AD FS ortamını kullanın ve Federasyon tek oturum açma tooAzure için AD yapılandırın.

Sahip değil ve toodeploy AD FS veya başka bir federasyon sunucusu planlıyor musunuz, aşağıdaki yönergeleri izleyin: [özel etki alanı adı tooAzure Active Directory eklemek](active-directory-add-domain.md).

## <a name="add-a-custom-domain-name-tooyour-directory"></a>Özel etki alanı adı tooyour Dizin Ekle
1. İçinde toohello oturum [Klasik Azure portalı](https://manage.windowsazure.com/) Azure AD dizininizin genel yöneticisi olan bir kullanıcı hesabı ile.
2. İçinde **Active Directory**dizininizi açın ve seçin hello **etki alanları** sekmesi.
3. Merhaba komut çubuğunda seçin **Ekle**ve ardından hello "contoso.com" gibi özel bir etki alanı adını girin. Emin tooinclude hello .com, .net veya diğer üst düzey uzantıları.
4. Select hello **t tooconfigure bu etki alanı için çoklu oturum açma bilgilerimi yerel Active Directory ile planlama** onay kutusu.
5. **Add (Ekle)** seçeneğini belirleyin.

Hello Azure AD Connect aracı tooget hello DNS girişi çalıştırmak, Azure AD tooverify hello etki alanı kullanır. Merhaba hello DNS giriş görürsünüz **Azure AD etki alanı** hello Sihirbazı'nda adım. Hangi adımın gibi görünüyor hello Sihirbazı'nda görebilirsiniz [bu yönergelerindeki](connect/active-directory-aadconnect-get-started-custom.md#verify-the-azure-ad-domain-selected-for-federation). Hello Azure AD Connect aracını yoksa, şunları yapabilirsiniz [buradan indirin](http://go.microsoft.com/fwlink/?LinkId=615771).

## <a name="add-hello-dns-entry-at-hello-domain-name-registrar-for-hello-domain"></a>Merhaba etki alanı adı kayıt hello etki alanı için Hello DNS girişi ekleyin
özel etki alanınızı adlandırın Azure AD ile Merhaba sonraki adım toouse tooupdate hello DNS bölge hello etki alanı için bir dosyadır. Bu, kuruluşunuz hello özel etki alanı adına sahip Azure AD tooverify sağlar.

1. Etki alanı adınız için etki alanı adı kayıt toohello Web sitesinde oturum açın. Bu erişim toodo sahip değilseniz, hello kişi veya 2. Bu erişim toocomplete adım olan Kuruluş ve tamamlandığında bildiğiniz toolet ekibi isteyin.
2. Güncelleştirme hello DNS bölge dosyasına hello DNS girişini ekleyerek hello etki alanı için tooyou Azure AD tarafından sağlanır. Bu DNS girişi hello etki alanının, sahipliği Azure AD tooverify sağlar. Merhaba DNS girişi, posta yönlendirme veya web barındırma gibi davranışları değiştirmez.

Bu adımla ilgili yardım için [Popüler DNS kayıt şirketlerinde DNS girişi ekleme yönergeleri](https://support.office.com/article/Create-DNS-records-for-Office-365-when-you-manage-your-DNS-records-b0f3fdca-8a80-4e8e-9ef3-61e8a2a9ab23/) bölümünü okuyun

## <a name="verify-hello-domain-name-with-azure-ad"></a>Azure AD ile Merhaba etki alanı adını doğrulayın
Merhaba DNS girişini ekledikten sonra hazır tooverify hello etki alanı adını Azure AD ile demektir.

tooverify hello etki alanı, select **sonraki** hello üzerinde **Azure AD etki alanı** hello Azure AD Connect Sihirbazı. Azure AD hello DNS bölge dosyasına hello etki alanı için DNS girişi hello arar. Azure AD hello DNS kayıtlarını dağıtıldıktan sonra hello etki alanı adı yalnızca doğrulayın. Yayma genellikle yalnızca birkaç saniye sürer, ancak bazen bir saat veya daha fazla sürebilir. Doğrulama hello ilk kez işe yaramazsa, daha sonra yeniden deneyin.

Sonra hello Azure AD Connect Sihirbazı'ndaki adımları kalan hello ile devam edin. Bu, Windows Server AD tooAzure AD kullanıcılardan eşitler. Federasyon için yapılandırılmış hello etki alanındaki eşitlenmiş kullanıcıların bir Federasyon tek oturum açma deneyimi şirket ağı tooAzure AD mümkün tooget olacaktır.

## <a name="troubleshooting"></a>Sorun giderme
Bir özel etki alanı adını doğrulayamıyorsanız hello aşağıdakileri deneyin. Merhaba en yaygın ve iş toohello az ortak aşağı ile başlayacağız.

1. **Bir saat bekleyin**. Azure AD etki alanı hello doğrulayabilirsiniz önce DNS kayıtlarını toopropagate gerekir. Bu işlem bir saat veya daha fazla sürebilir.
2. **DNS kaydı girildi hello ve doğru olduğundan emin olun**. Merhaba etki alanı adı kayıt hello etki alanı için hello Web sitesindeki bu adımı tamamlayın. Hello DNS girişini DNS bölge dosyasına hello sunmak veya tam bir eşleşme hello DNS girişi ile değilse Azure AD, sağladığınız değilse azure AD hello etki alanı adını doğrulayın. Merhaba etki alanı adı kayıt hello etki alanı için erişim tooupdate DNS kayıtlarını yoksa hello kişi veya ekiple erişim izni kuruluşunuz hello DNS girişi paylaşmasına ve tooadd hello DNS girdisi isteyin.
3. **Merhaba etki alanı adını Azure AD içinde başka bir dizinden silin**. Bir etki alanı adı yalnızca tek bir dizinde doğrulanabilir. Bir etki alanı adı önce başka bir dizinde doğrulandıysa yeni dizininizde doğrulanabilmesi için oradan silinmelidir. etki alanı adları, silinmesi hakkında toolearn okuma [özel etki alanı adlarını yönetme](active-directory-add-manage-domain-names.md).

## <a name="add-more-custom-domain-names"></a>Daha fazla özel etki alanı ekleme
Kuruluşunuz birden fazla özel etki alanı adları, 'contoso.com' ve 'contosobank.com' gibi kullanıyorsa tooa en fazla 900 etki alanı adlarını ekleyebilirsiniz. Bu makale tooadd etki alanı içinde her aynı adımları hello kullanın.

## <a name="next-steps"></a>Sonraki adımlar
* [Özel etki alanı adlarını yönetme](active-directory-add-manage-domain-names.md)
* [Azure AD'deki etki alanı yönetimi kavramları hakkında bilgi edinme](active-directory-add-domain-concepts.md)
* [Kullanıcılarınız oturum açtığında şirketinizin markasını gösterme](active-directory-add-company-branding.md)
* [Azure AD PowerShell toomanage etki alanı adlarını kullanın](https://msdn.microsoft.com/library/azure/e1ef403f-3347-4409-8f46-d72dafa116e0#BKMK_ManageDomains)

