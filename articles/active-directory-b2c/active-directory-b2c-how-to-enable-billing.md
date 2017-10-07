---
title: "bir Azure aboneliği tooAzure AD B2C aaaHow tooLink | Microsoft Docs"
description: "Bir Azure aboneliği içine adım adım kılavuzu tooenable faturalama Azure AD B2C kiracısı için."
services: active-directory-b2c
documentationcenter: dev-center-name
author: rojasja
manager: mbaldwin
ms.service: active-directory-b2c
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 12/05/2016
ms.author: joroja
ms.openlocfilehash: 07b2ed5f7f5f543c9cbb8e9a35107462448e9440
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="linking-an-azure-subscription-tooan-azure-b2c-tenant-toopay-for-usage-charges"></a>Bir Azure aboneliği tooan Azure B2C Kiracı toopay kullanım ücretleri için bağlama

Devam eden kullanım ücretleri için Azure Active Directory B2C (veya Azure AD B2C) Faturalanan tooan Azure aboneliği ' dir. Merhaba Kiracı yönetici tooexplicitly bağlantı hello Azure AD B2C Kiracı tooan hello B2C Kiracı kendisini oluşturduktan sonra Azure aboneliği gereklidir.  Bu bağlantı, Azure AD "B2C Kiracı" oluşturarak elde edilir hello hedef Azure aboneliği kaynak. Çok sayıda B2C Kiracı bağlantılı tooa tek bir Azure aboneliği yanı sıra diğer Azure kaynaklarının (örneğin, sanal makineleri, veri depolama, LogicApps) olabilir


> [!IMPORTANT]
> Faturalama ve fiyatlandırma sayfası aşağıdaki hello B2C için kullanım en son bilgiler Hello: [Azure AD B2C fiyatlandırma](
https://azure.microsoft.com/pricing/details/active-directory-b2c/)

## <a name="step-1---create-an-azure-ad-b2c-tenant"></a>1. adım - Azure AD B2C Kiracısı oluşturma
B2C Kiracı oluşturma önce tamamlanması gerekir. B2C Kiracı hedef zaten oluşturduysanız bu adımı atlayın. [Azure AD B2C ile çalışmaya başlama](active-directory-b2c-get-started.md)

## <a name="step-2---open-azure-portal-in-hello-azure-ad-tenant-that-shows-your-azure-subscription"></a>2. adım - hello Azure aboneliğinize gösteren Azure AD Kiracı açık Azure portalında
Toohello gidin [Azure portal](https://portal.azure.com). Toohello hello toouse istediğiniz Azure aboneliği gösteren Azure AD Kiracısı geçin. Bu Azure AD kiracısı hello B2C kiracısından farklı. Azure portal Hello içinde hello sağ üst köşesinde, hello Pano tooselect hello Azure AD Kiracı hello hesap adına tıklayın. Bir Azure aboneliği gerekli tooproceed ' dir. [Bir Azure aboneliği edinme](https://account.windowsazure.com/signup?showCatalog=True)

![Tooyour Azure AD Kiracısını değiştirme](./media/active-directory-b2c-how-to-enable-billing/SelectAzureADTenant.png)

## <a name="step-3---create-a-b2c-tenant-resource-in-azure-marketplace"></a>3. adım - Azure Marketi'nde bir B2C Kiracı kaynak oluşturma
Merhaba Market simgesine tıklayarak, veya yeşil "+" Merhaba seçerek hello sol üst köşedeki hello panonun Market açın.  Arayın ve Azure Active Directory B2C seçin. Bu seçeneği belirleyin.

![Market seçin](./media/active-directory-b2c-how-to-enable-billing/marketplace.png)

![AD B2C arama](./media/active-directory-b2c-how-to-enable-billing/searchb2c.png)

Hello Azure AD B2C kaynak şu parametreler iletişim kapsar hello oluşturun:

1. Azure AD B2C Kiracısı – Azure AD B2C Kiracısı hello aşağı açılır listeden seçin.  Yalnızca uygun Azure AD B2C kiracılar gösterir.  Uygun B2C kiracılar bu koşullara uyan: hello hello B2C kiracısının genel Yöneticisi olduğunuz ve hello B2C Kiracı şu anda ilişkili tooan Azure aboneliği değil

2. Azure AD B2C kaynak adı - olduğu seçilmiş toomatch hello hello B2C Kiracı etki alanı adı

3. Abonelik - bir yönetici veya bir ortak yönetici olan bir etkin Azure aboneliği.  Birden çok Azure AD B2C Kiracı tooone Azure aboneliği eklenebilir

4. Kaynak grubu ve kaynak grubu konumu - bu yapı birden çok Azure kaynağı düzenlemenize yardımcı olur.  Bu seçenek B2C Kiracı konumu, performans veya faturalama durumu üzerinde bir etkisi yoktur

5. PIN bilgilerini ve hello B2C Kiracı ayarlarını faturalama kolay erişim tooyour B2C kiracısı toodashboard ![B2C kaynak oluşturma](./media/active-directory-b2c-how-to-enable-billing/createresourceb2c.png)

## <a name="step-4---manage-your-b2c-tenant-resources-optional"></a>4. adım - (isteğe bağlı), B2C Kiracı kaynaklarını yönetme
Dağıtım tamamlandıktan sonra yeni bir "B2C Kiracı" kaynak hello hedef kaynak grubunda oluşturduğunuz ve Azure abonelik ilgili.  Yeni bir kaynak türü "B2C Kiracı" eklenen yanı sıra diğer Azure kaynaklarınızı görmeniz gerekir.

![B2C kaynağı oluşturma](./media/active-directory-b2c-how-to-enable-billing/b2cresourcedashboard.png)

Merhaba B2C Kiracı kaynak tıklayarak, olan
- Abonelik adı tooreview fatura bilgilerini'ı tıklatın. Faturalama ve kullanım bakın.
- Azure AD B2C ayarlarını tooopen yeni tarayıcı sekmesinde doğrudan tooyour B2C Kiracı ayarlar dikey tıklatın
- Destek talebi gönderme
- B2C Kiracı kaynak tooanother taşıma Azure abonelik veya kaynak grubu tooanother.  Bu seçim değişiklikleri kullanım ücretleri hangi Azure aboneliği alır.

![B2C kaynak ayarları](./media/active-directory-b2c-how-to-enable-billing/b2cresourcesettings.png)

## <a name="known-issues"></a>Bilinen sorunlar
- B2C Kiracı silme. B2C Kiracı oluşturduysanız, silinir ve yeniden oluşturulması hello aynı etki alanı adı, lütfen ayrıca silin ve hello "Bağlantı" Merhaba kaynakla yeniden oluşturmanız aynı etki alanı adı.  Bu, "" Tüm kaynaklar"altında kaynak hello abonelik Kiracı hello Azure portal aracılığıyla bağlama" bulacaksınız.
- Bölgesel kaynak konumu Self potansiyel kısıtlamalar.  Nadir durumlarda, bir kullanıcı Azure kaynak oluşturma için bölgesel bir kısıtlama oluşturulmuş.  Bu kısıtlama, bir Azure aboneliği ve B2C Kiracısı arasında bağlantı hello hello oluşturulmasını engelleyebilir. toomitigate, lütfen bu kısıtlama hafifletin.

## <a name="next-steps"></a>Sonraki adımlar
Bu adımları her B2C kiracılarınız için tamamlandıktan sonra Azure aboneliğinizin Azure doğrudan ya da Kurumsal Anlaşma ayrıntılarınızı göre faturalandırılır.
- Kullanım ve fatura seçili Azure aboneliğiniz içinde gözden geçirin
- Hello kullanarak ayrıntılı gün gün kullanım raporları gözden [kullanım raporlama API'si](active-directory-b2c-reference-usage-reporting-api.md)
