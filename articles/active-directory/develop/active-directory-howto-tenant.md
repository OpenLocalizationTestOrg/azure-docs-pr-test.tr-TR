---
title: "Azure AD kiracısı edinme | Microsoft Belgeleri"
description: "Uygulamaları kaydetmek ve oluşturmak üzere Azure Active Directory kiracısı edinme."
services: active-directory
documentationcenter: 
author: bryanla
manager: mtillman
editor: 
ms.assetid: 1f4b24eb-ab4d-4baa-a717-2a0e5b8d27cd
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 07/19/2017
ms.author: bryanla
ms.custom: aaddev
ms.openlocfilehash: 5874e6ce7d19c5106bc88ce9ff7fddd1842e0c3b
ms.sourcegitcommit: 821b6306aab244d2feacbd722f60d99881e9d2a4
ms.translationtype: HT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/16/2017
---
# <a name="how-to-get-an-azure-active-directory-tenant"></a>Azure Active Directory kiracısı edinme
Azure Active Directory'de (Azure AD) [kiracı](https://msdn.microsoft.com/library/azure/jj573650.aspx#BKMK_WhatIsAnAzureADTenant), bir kuruluşun temsilcisidir.  Bir kuruluşun, Azure, Microsoft Intune veya Office 365 gibi bir Microsoft bulut hizmetine kaydolduğunda aldığı ve sahip olduğu adanmış bir Azure AD hizmeti örneğidir.  Her Azure AD kiracısı benzersizdir ve diğer Azure AD kiracılarından ayrıdır.  

Kiracı, bir şirket içindeki kullanıcıları ve bunlarla ilgili bilgileri (parolalarını, kullanıcı profili verilerini, izinlerini vb.) barındırır.  Ayrıca bir kuruluşa ve kuruluşun güvenliğine ilişkin grupları, uygulamaları ve diğer bilgileri de içerir.

Azure AD kullanıcılarının uygulamanızda oturum açmasına olanak tanımak için uygulamanızı kendi kiracınıza kaydetmeniz gerekir.  Bir Azure AD kiracısında uygulama yayımlamak **tamamen ücretsizdir**.  Hatta çoğu geliştirici, deneme, geliştirme, hazırlama ve test etme amacıyla çeşitli kiracılar ve uygulamalar oluşturur.  Uygulamanıza kaydolan ve uygulamanızı kullanan kuruluşlar, gelişmiş dizin özelliklerinden faydalanmak istemeleri halinde isteğe bağlı olarak lisans satın almayı tercih edebilir.

Peki, Azure AD kiracısını nasıl edinebilirsiniz?  Bu işlem, aşağıdaki koşullarda biraz farklı olabilir:

* [Mevcut bir Office 365 aboneliğiniz varsa](#use-an-existing-office-365-subscription)
* [Bir Microsoft Hesabı ile ilişkili olan mevcut bir Azure aboneliğiniz varsa](#use-an-msa-azure-subscription)
* [Bir kuruluş hesabı ile ilişkili olan mevcut bir Azure aboneliğiniz varsa](#use-an-organizational-azure-subscription)
* [Yukarıdakilerden hiçbirine sahip değilseniz ve sıfırdan başlamak istiyorsanız](#start-from-scratch)

## <a name="use-an-existing-office-365-subscription"></a>Mevcut bir Office 365 aboneliğini kullanma
Mevcut bir Office 365 aboneliğiniz varsa zaten bir Azure AD kiracınız vardır! O365 hesabınızla [Azure portal](https://portal.azure.com)’da oturum açabilir ve Azure AD’yi kullanmaya başlayabilirsiniz.

## <a name="use-an-msa-azure-subscription"></a>MSA Azure aboneliğini kullanma
Daha önce bireysel Microsoft Hesabınız ile bir Azure aboneliğine kaydolduysanız kiracınız zaten mevcuttur!  [Azure portalı](https://portal.azure.com)’nda oturum açtığınızda, otomatik olarak varsayılan kiracınızda oturumunuz açılır. Bu kiracıyı uygun gördüğünüz şekilde kullanabilirsiniz ancak bir Kuruluş yöneticisi hesabı oluşturmak isteyebilirsiniz.

Bunu yapmak için şu adımları uygulayın.  Alternatif olarak, benzer bir işlemi izleyerek yeni bir kiracı oluşturmak ve kiracı içinde bir yönetici oluşturmak isteyebilirsiniz.

1. Bireysel hesabınızla [Azure portalı](https://portal.azure.com)'nda oturum açın
2. Portalın "Azure Active Directory" bölümüne (sol gezinti çubuğunda, **Diğer Hizmetler**’in altında bulunur) gidin
3. Otomatik olarak "Varsayılan Dizin"de oturumunuzun açılması gerekir. Oturum açılmazsa sağ üst köşede hesap adınıza tıklayarak dizinleri değiştirebilirsiniz.
4. **Hızlı Görevler** bölümünde **Kullanıcı ekle**’yi seçin.
5. Kullanıcı Ekleme Formu'nda şu bilgileri sağlayın:

   * Ad: (uygun bir değer seçin)
   * Kullanıcı adı: (bu yönetici için bir kullanıcı adı seçin)
   * Profil: (Ad, Soyadı, İş unvanı ve Bölüm için uygun değerleri girin)
   * Rol: Genel Yönetici
6. Kullanıcı Ekleme Formu'nu doldurduktan ve yeni yönetici kullanıcı için geçici parolayı aldıktan sonra, parolayı değiştirmek üzere bu yeni kullanıcı ile oturum açmanız gerekeceğinden, bu parolayı kaydettiğinizden emin olun. Ayrıca alternatif bir e-posta adresi kullanarak parolayı doğrudan kullanıcıya da gönderebilirsiniz.
7. Yeni kullanıcıyı oluşturmak için **Oluştur**’a tıklayın.
8. Geçici parolayı değiştirmek için [https://login.microsoftonline.com](https://login.microsoftonline.com) adresinde bu yeni kullanıcı hesabı ile oturum açın ve istendiğinde parolayı değiştirin.

## <a name="use-an-organizational-azure-subscription"></a>Kuruluş Azure aboneliği kullanma
Daha önce kuruluş hesabınızla bir Azure aboneliğine kaydolduysanız kiracınız zaten mevcuttur!  [Azure portalı](https://portal.azure.com)’nda, "Diğer Hizmetler" ve "Azure Active Directory"e gittiğinizde bir kiracı bulmanız gerekir.  Bu kiracıyı uygun gördüğünüz şekilde kullanabilirsiniz.

## <a name="start-from-scratch"></a>Sıfırdan başlama
Yukarıdakilerin hiçbiri sizin için bir anlam ifade etmiyorsa endişelenmeyin. Yeni bir Azure AD dizini oluşturmak için [Azure portalı](https://portal.azure.com/#create/Microsoft.AzureActiveDirectory)’nı ziyaret edin. İşlemi tamamladıktan sonra, kayıt sırasında seçtiğiniz etki alanı adıyla kendi Azure AD kiracınıza sahip olursunuz.  [Azure portalı](https://portal.azure.com)'nda, sol gezinti çubuğunda bulunan **Azure Active Directory** konumuna giderek kiracınızı bulabilirsiniz.
