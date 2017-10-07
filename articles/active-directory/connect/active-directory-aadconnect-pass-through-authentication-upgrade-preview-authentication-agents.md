---
title: "Azure AD Connect: Doğrudan kimlik doğrulama - yükseltme Önizleme kimlik doğrulama Aracısı | Microsoft Docs"
description: "Bu makalede nasıl tooupgrade, Azure Active Directory (Azure AD) doğrudan kimlik doğrulama yapılandırması."
services: active-directory
keywords: "Azure AD Connect doğrudan kimlik doğrulama, Active Directory yükleyin gerekli bileşenleri Azure AD, SSO, çoklu oturum açma"
documentationcenter: 
author: swkrish
manager: femila
ms.assetid: 9f994aca-6088-40f5-b2cc-c753a4f41da7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/04/2017
ms.author: billmath
ms.openlocfilehash: 1695326b182278944e9f1584da72b18862b6ef27
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-pass-through-authentication-upgrade-preview-authentication-agents"></a>Azure Active Directory doğrudan kimlik doğrulaması: Yükseltme Önizleme kimlik doğrulama Aracısı

## <a name="overview"></a>Genel Bakış

Bu makalede Önizleme aracılığıyla Azure AD geçişli kimlik doğrulaması kullanan müşteriler içindir. Biz son yükseltilmiş (ve rebranded) hello kimlik doğrulama Aracısı yazılım. Too_manually_ yükseltme Önizleme kimlik doğrulaması, şirket içi sunucularınızda yüklü aracıları gerekir. Bir kerelik eylem yalnızca bu el ile yükseltmedir. Tüm gelecekteki güncelleştirmeleri tooAuthentication aracıları otomatik olarak yapılır. Merhaba nedeniyle tooupgrade aşağıdaki gibidir:

- Kimlik Doğrulama Aracısı Hello Önizleme sürümleri, herhangi bir ek güvenlik veya hata düzeltmeleri almazsınız.
-   Kimlik Doğrulama Aracısı Hello Önizleme sürümleri, yüksek kullanılabilirlik için ek sunuculara yüklenemez.

## <a name="check-versions-of-your-authentication-agents"></a>Kimlik doğrulama aracılarınızı sürümlerini denetleyin

### <a name="step-1-check-where-your-authentication-agents-are-installed"></a>1. adım: kimlik doğrulaması aracılarınızı yüklendiği onay

Bu adımları toocheck kimlik doğrulaması aracılarınızı yüklendiği izleyin:

1. İçinde toohello oturum [Azure Active Directory Yönetim Merkezi](https://aad.portal.azure.com) hello kiracınız için genel yönetici kimlik bilgileriyle.
2. Seçin **Azure Active Directory** hello sol gezinti çubuğunda.
3. Seçin **Azure AD Connect**. 
4. Seçin **doğrudan kimlik doğrulama**. Bu dikey kimlik doğrulaması aracılarınızı yüklendiği hello sunucuları listeler.

![Azure Active Directory Yönetim Merkezi - doğrudan kimlik doğrulama dikey penceresi](./media/active-directory-aadconnect-pass-through-authentication/pta8.png)

### <a name="step-2-check-hello-versions-of-your-authentication-agents"></a>2. adım: kimlik doğrulaması aracılarınızı hello sürümlerini denetleyin

adım, önceki hello tanımlanan her bir sunucuda kimlik doğrulama aracılarınızı toocheck hello sürümleri aşağıdaki yönergeleri izleyin:

1. Çok Git**Denetim Masası -> Programlar -> Programlar ve Özellikler** hello şirket içi sunucuda.
2. İçin bir giriş ise "**Microsoft Azure AD Connect kimlik doğrulama Aracısı**", bu sunucu üzerindeki herhangi bir işlem tootake gerekmez.
3. İçin bir giriş ise "**Microsoft Azure AD uygulama ara sunucusu Bağlayıcısı**", sürümleri 1.5.132.0 veya toomanually ihtiyacınız daha önce bu sunucuda yükseltme.

![Kimlik Doğrulama Aracısı'nın Önizleme sürümü](./media/active-directory-aadconnect-pass-through-authentication/pta6.png)

## <a name="best-practices-toofollow-before-starting-hello-upgrade"></a>Merhaba yükseltme işlemine başlamadan önce toofollow en iyi yöntemler

Yükseltmeden önce aşağıdaki yerinde öğelerindeki hello olduğundan emin olun:

1. **Yalnızca bulut genel yönetici hesabı oluşturma**: Burada doğrudan kimlik doğrulama aracılarınızı değil düzgün çalıştığını acil durumlarda bir yalnızca bulut genel yönetici hesabı toouse gerek kalmadan yükseltmeyin. Hakkında bilgi edinin [bir yalnızca bulut genel yönetici hesabı ekleme](../active-directory-users-create-azure-portal.md). Bu adımı uygulamadan önemlidir ve, kiracınızın dışında erişebilmenizin sağlar.
2.  **Yüksek kullanılabilirlik sağlamak**: daha önce tamamlanmamış, ikinci tek başına bir kimlik doğrulama Aracısı tooprovide yüksek kullanılabilirlik için bu kullanarak oturum açma istekleri yüklemek [yönergeleri](active-directory-aadconnect-pass-through-authentication-quick-start.md#step-5-ensure-high-availability).

## <a name="upgrading-hello-authentication-agent-on-your-azure-ad-connect-server"></a>Azure AD Connect sunucunuzda yükseltme hello kimlik doğrulama Aracısı

Azure AD Connect hello kimlik doğrulama Aracısı hello üzerinde yükseltmeden önce yükseltmeniz aynı sunucu. Hem birincil hem de Azure AD Connect sunucuları hazırlama üzerinde aşağıdaki adımları izleyin:

1. **Azure AD Connect yükseltme**: izleyin [makale](./active-directory-aadconnect-upgrade-previous-version.md) ve toohello en son Azure AD Connect sürümüne yükseltin.
2. **Merhaba kimlik doğrulama Aracısı Hello önizleme sürümünü kaldırın**: indirme [bu PowerShell Betiği](https://aka.ms/rmpreviewagent) çalıştırmak hello sunucuda yönetici olarak.
3. **Hello hello kimlik doğrulama Aracısı en son sürümünü indirin (sürümleri 1.5.193.0 veya sonrası)**: toohello içinde oturum [Azure Active Directory Yönetim Merkezi](https://aad.portal.azure.com) , kiracının genel yönetici kimlik bilgilerine sahip. Seçin **Azure Active Directory -> Azure AD Connect doğrudan kimlik doğrulama -> -> Yükleme Aracısı**. Hizmet Hello koşullarını kabul edin ve hello hello kimlik doğrulama Aracısı en son sürümünü yükleyin.
4. **Merhaba hello kimlik doğrulama Aracısı en son sürümünü yüklemek**: Çalıştır hello yürütülebilir indirilen adım 3'te. İstendiğinde, kiracının genel Yöneticisi kimlik bilgilerini sağlayın.
5. **Merhaba en son sürümünün yüklü doğrulayın**: önce gösterildiği gibi çok Git**Denetim Masası -> Programlar -> Programlar ve Özellikler** ve için bir giriş olduğundan emin olun "**Microsoft Azure AD Connect Kimlik Doğrulama Aracısı**".

>[!NOTE]
>Merhaba doğrudan kimlik doğrulama dikey penceresinde hello onay [Azure Active Directory Yönetim Merkezi](https://aad.portal.azure.com) hello önceki adımları tamamladıktan sonra sunucu - hello gösteren bir giriş başına iki kimlik doğrulama Aracısı giriş görürsünüz Kimlik doğrulama aracısı olarak **etkin** ve diğer gibi hello **devre dışı**. Bu _beklenen_. Merhaba **devre dışı** girişi birkaç gün sonra otomatik olarak bırakıldı.

## <a name="upgrading-hello-authentication-agent-on-other-servers"></a>Diğer sunucularda yükseltme hello kimlik doğrulama Aracısı

Bu adımları tooupgrade kimlik doğrulama Aracısı, (burada Azure AD Connect yüklenmemiş) üzerindeki diğer sunuculara izleyin:

1. **Merhaba kimlik doğrulama Aracısı Hello önizleme sürümünü kaldırın**: indirme [bu PowerShell Betiği](https://aka.ms/rmpreviewagent) çalıştırmak hello sunucuda yönetici olarak.
2. **Hello hello kimlik doğrulama Aracısı en son sürümünü indirin (sürümleri 1.5.193.0 veya sonrası)**: toohello içinde oturum [Azure Active Directory Yönetim Merkezi](https://aad.portal.azure.com) , kiracının genel yönetici kimlik bilgilerine sahip. Seçin **Azure Active Directory -> Azure AD Connect doğrudan kimlik doğrulama -> -> Yükleme Aracısı**. Hizmet Hello koşullarını kabul edin ve hello en son sürümünü yükleyin.
3. **Merhaba hello kimlik doğrulama Aracısı en son sürümünü yüklemek**: Çalıştır hello yürütülebilir 2. adımda indirdiğiniz. İstendiğinde, kiracının genel Yöneticisi kimlik bilgilerini sağlayın.
4. **Hello en son sürümünün yüklü doğrulayın**: önce gösterildiği gibi çok Git**Denetim Masası -> Programlar -> Programlar ve Özellikler** ve adlı bir giriş olduğundan emin olun **Microsoft Azure AD Connect Kimlik Doğrulama Aracısı**.

>[!NOTE]
>Merhaba doğrudan kimlik doğrulama dikey penceresinde hello onay [Azure Active Directory Yönetim Merkezi](https://aad.portal.azure.com) hello önceki adımları tamamladıktan sonra sunucu - hello gösteren bir giriş başına iki kimlik doğrulama Aracısı giriş görürsünüz Kimlik doğrulama aracısı olarak **etkin** ve diğer gibi hello **devre dışı**. Bu _beklenen_. Merhaba **devre dışı** girişi birkaç gün sonra otomatik olarak bırakıldı.

## <a name="next-steps"></a>Sonraki adımlar
- [**Sorun giderme** ](active-directory-aadconnect-troubleshoot-pass-through-authentication.md) -tooresolve ortak hello özelliğiyle nasıl sorunları öğrenin.
