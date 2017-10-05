---
title: "Özel etki alanı adınızı Azure Active Directory'ye ekleme | Microsoft Belgeleri"
description: "Şirketinizin etki alanı adlarını Azure Active Directory'ye ekleme ve etki alanı adını doğrulama."
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
ms.openlocfilehash: ad72f768add7edc1d34a85c27dc2aa1b4e4b3a50
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="add-a-custom-domain-name-to-azure-active-directory"></a>Azure Active Directory'ye özel etki alanı adı ekleyin
> [!div class="op_single_selector"]
> * [Azure portal](active-directory-domains-add-azure-portal.md)
> * [Klasik Azure Portalı](active-directory-add-domain.md)
> 

Azure Active Directory (Azure AD) kullanarak, şirket etki alanı adınızı da Azure AD'ye ekleyebilirsiniz. İş ve şirket etki alanı adınızı kullanarak oturum açan kullanıcıların yapmak için kuruluşunuzun kullandığı etki alanı adları olabilir. Etki alanı adını Azure AD'ye ekleme gibi kullanıcılarınız için tanıdık dizindeki kullanıcı adları atama olanak tanır 'alice@contoso.com.' Bu basit bir işlemdir:

1. Dizine özel etki alanı adı ekleyin
2. Etki alanı adı kayıt şirketinize etki alanı adı için bir DNS girişi ekleyin
3. Azure AD'de özel etki alanı adını doğrulayın

## <a name="how-do-i-add-a-domain-name"></a>Bir etki alanı adı nasıl eklenir?
1. Oturum [Azure portal](https://portal.azure.com) dizini için genel yönetici olan bir hesapla.
2. Seçin **daha fazla hizmet**, girin **Azure Active Directory** metin kutusuna ve ardından **Enter**.
   
   ![Açılış kullanıcı yönetimi](./media/active-directory-domains-add-azure-portal/user-management.png)
3. Üzerinde ***dizin adı*** dikey penceresinde, select **etki alanı adları**.
4. Üzerinde  ***dizin adı* -etki alanı adları** dikey penceresinde, select **Ekle** komutu.
   
   ![Ekle komutu seçme](./media/active-directory-domains-add-azure-portal/add-command.png)
5. Üzerinde **etki alanı adı** dikey penceresinde kutusuna "contoso.com" gibi özel etki alanınızın adını girin ve ardından **etki alanı Ekle**. .com, .net veya diğer üst düzey uzantıları eklemeyi unutmayın.
6. Üzerinde ***domainname*** dikey (yeni etki alanı adınızı başlığında sahip açan diğer bir deyişle, dikey), Azure AD, kuruluşunuzun özel etki alanı adı sahip olduğunu doğrulamak için kullanacağınız DNS girdisi bilgi alın.
   
   ![DNS girişi bilgi alın](./media/active-directory-domains-add-azure-portal/get-dns-info.png)

Etki alanı adınızı ekledikten sonra, Azure AD etki alanının kuruluşunuza ait olduğunu doğrulamalıdır. Azure AD'nin bu doğrulamayı gerçekleştirebilmesi için etki alanı adına ilişkin DNS bölge dosyasına bir DNS girişi eklemeniz gerekir. Bu işlem, etki alanı adının ait olduğu etki alanı adı kayıt şirketinin web sitesinden gerçekleştirilir.

## <a name="add-the-dns-entry-at-the-domain-name-registrar-for-the-domain"></a>Etki alanının etki alanı adı kayıt şirketinde DNS girişi ekleme
Etki alanınızı Azure AD ile kullanmanın sonraki adımı, etki alanına ait DNS bölge dosyasının güncelleştirilmesidir. Bunun yapılması, kuruluşunuzun özel etki alanı adına sahip olduğunun Azure AD tarafından doğrulanmasını sağlar.

1. Etki alanına ilişkin etki alanı adı kayıt şirketinde oturum açın. DNS girişini güncelleştirmek için erişiminiz yoksa bu erişime sahip kişi ya da ekipten adım 2’yi tamamlamasını ve tamamlandığında size bildirmesini isteyin.
2. Azure AD tarafından size sağlanan DNS girişini ekleyerek etki alanına ilişkin DNS bölge dosyasını güncelleştirin. Azure AD, bu DNS girişi sayesinde etki alanının size ait olduğunu doğrulayabilir. DNS girişi, posta yönlendirme veya web barındırma gibi davranışları değiştirmez.

DNS girişi ekleme hakkında yardım için [Popüler DNS kayıt şirketlerinde DNS girişi ekleme yönergeleri](https://support.office.com/article/Create-DNS-records-for-Office-365-when-you-manage-your-DNS-records-b0f3fdca-8a80-4e8e-9ef3-61e8a2a9ab23/) bölümünü okuyun

## <a name="verify-the-domain-name-with-azure-ad"></a>Azure AD ile etki alanı adını doğrulama
DNS girişini ekledikten sonra etki alanı adını Azure AD ile doğrulamaya hazır olursunuz.

DNS kayıtlarını yalnızca dağıtıldıktan sonra bir etki alanı adı doğrulanabilir. Bu yayma genellikle yalnızca birkaç saniye sürer, ancak bazen bir saat veya daha fazla sürebilir. İlk denemede doğrulama çalışmazsa daha sonra yeniden deneyin.

1. Oturum [Azure portal](https://portal.azure.com) dizini için genel yönetici olan bir hesapla.
2. Seçin **Gözat**kullanıcı yönetimi metin kutusuna girin ve ardından **Enter**.
   
   ![Açılış kullanıcı yönetimi](./media/active-directory-domains-add-azure-portal/user-management.png)
3. Üzerinde **kullanıcı yönetimi - etki alanı adları** dikey penceresinde, doğrulamak istediğiniz doğrulanmamış etki alanı adı seçin.
4. Üzerinde ***domainname*** (yeni etki alanı adınızı başlığında sahip açan diğer bir deyişle, dikey), dikey penceresinde seçin **doğrula** doğrulamayı tamamlamak için.

Artık [özel etki alanı adınızı içeren kullanıcı adları atayabilirsiniz](active-directory-users-create-azure-portal.md).

## <a name="troubleshooting"></a>Sorun giderme
Bir özel etki alanı adını doğrulayamıyorsanız aşağıdakileri deneyin. En sık karşılaşılan ile başlayıp en az karşılaşılana kadar devam edeceğiz.

1. **Bir saat bekleyin**. Azure AD’nin etki alanını doğrulayabilmesi için DNS kayıtlarının yayılması gerekir. Bu işlem bir saat veya daha fazla sürebilir.
2. **DNS kaydının girildiğinden ve doğru olduğundan emin olun**. Bu adımı, etki alanının etki alanı adı kayıt şirketine ait web sitesinde tamamlayın. DNS girişi DNS bölge dosyasında mevcut değilse veya Azure AD’nin size sağladığı DNS girişi ile tam eşleşmiyorsa Azure AD etki alanı adını doğrulayamaz. Etki alanı adı kayıt şirketinde etki alanının DNS kayıtlarını güncelleştirmek için erişiminiz yoksa, DNS girişini bu erişime sahip olan kişi veya ekip ile paylaşın ve DNS girişini eklemesini isteyin.
3. **Etki alanı adını Azure AD'deki başka bir dizinden silin**. Bir etki alanı adı yalnızca tek bir dizinde doğrulanabilir. Bir etki alanı adı önce başka bir dizinde doğrulandıysa yeni dizininizde doğrulanabilmesi için oradan silinmelidir. Etki alanı adlarını silme hakkında bilgi edinmek için bkz. [Özel etki alanı adlarını yönetme](active-directory-domains-manage-azure-portal.md).    

## <a name="add-more-custom-domain-names"></a>Daha fazla özel etki alanı ekleme
Kuruluşunuz "contoso.com" ve "contosobank.com" gibi birden fazla özel etki alanı adı kullanıyorsa 900'e kadar etki alanı adı ekleyebilirsiniz. Her bir etki alanı adını eklemek için bu makaledeki adımları tekrarlayın.

## <a name="next-steps"></a>Sonraki adımlar
[Özel etki alanı adlarını yönetme](active-directory-domains-manage-azure-portal.md)

