---
title: "Koleksiyon aaaWhat tür Azure RemoteApp için gerekiyor? | Microsoft Belgeleri"
description: "Azure RemoteApp ile kullanılabilir koleksiyonların hello türleri hakkında bilgi edinin."
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: c13ec78d-07e9-4646-8194-cf3efafc1760
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: f00b5fe41af597cf75e26300bf7842c3a8ff94fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="what-kind-of-collection-do-you-need-for-azure-remoteapp"></a>Azure RemoteApp için nasıl bir koleksiyona ihtiyacınız var?
> [!IMPORTANT]
> Azure RemoteApp 31 Ağustos 2017’de kullanımdan kaldırılacaktır. Okuma hello [duyuru](https://go.microsoft.com/fwlink/?linkid=821148) Ayrıntılar için.
> 
> 

Azure RemoteApp uygulamalarına ve kaynaklarına herhangi bir cihazda kullanıcılarla paylaşmanıza olanak tanır. Koleksiyonları toohold hello uygulamalarına ve kaynaklarına oluşturarak bunu ve sonra bu koleksiyonları kullanıcılarıyla paylaşabilirsiniz. Farklı ağ ve sizin için uygun olan kimlik doğrulama seçenekleri - 2 farklı toplama seçeneklerini misiniz?

Şimdi hello farklı konuları ve Seçenekler toomake tooget hello Azure RemoteApp koleksiyonunuzun dışında en çok ihtiyaç yol. 

## <a name="quick-differences-between-hello-collection-types"></a>Hızlı farklarını hello koleksiyon türleri
|  | Bulut | Karma |
| --- | --- | --- |
| Varolan bir sanal ağ kullanın |Evet |Evet |
| AD bağlı hesapları (DirSync) gerektirir |Hayır |Evet |
| Etki alanına katılma gerektirir |Hayır |Evet |
| Etki alanı denetleyicisi erişilebilir tooVNET gerektirir |Hayır |Evet |

## <a name="cloud-collections"></a>Bulut koleksiyonları
* Hızlı toocreate - hello koleksiyonu hızla sağlanan toousers uygulamalarınızı daha hızlı alma anlamına gelir.
* Bizim paylaşma veya kendi uygulamalarınızı getirin. (Bir Azure sanal makineden yerleşik) özel bir görüntü veya aboneliğinizle dahil hello görüntülerden birini kullanabilirsiniz.
* Koleksiyonunuz ve şirket içi etki alanınızın arasında tooconfigure bağlantı gerekmez.
* Ancak, isteğe bağlı olarak, kendi Azure VNET tooprovide erişim şirket içi ortamınıza veri paylaşımı veya toouse Windows dışı kimlik doğrulaması için (veritabanı kimlik doğrulaması kullanarak) SQL Server gibi kaynaklarına içine kullanabilirsiniz.

Tamam, bir nasıl oluşturabilirim?

* Yalnızca bulutta? Create hello ile **hızlı Oluştur** hello portal seçeneği.
* Bulut + VNET? Oluşturma hello kullanarak **Create VNET ile** seçeneği ancak toojoin bir etki alanı seçmeyin.

## <a name="hybrid-collections"></a>Karma koleksiyonlar
* Tam erişim tooon içi ağı + Azure VNET sağlar.
* Etki alanı katılma erişimi uygulamaları ve verileri içerir. Uzak uygulamalar, şirket içi Active Directory kimlik doğrulaması için - sonra etki alanındaki kaynaklara erişebilir.
* Gelişmiş izleme ve var olan System Center çözümlerini ve Windows grup ilkeleri ile Yönetimi (aracılığıyla, Windows Server 2012 R2'de oluşturulan özel bir görüntü) etkinleştir
* Destek [ExpressRoute](https://azure.microsoft.com/services/expressroute/) tooconnect Azure VNET tooyour yerel VNET.

Oluşturma hello kullanarak **Create VNET ile** seçeneği ve toojoin bir etki alanı seçin.

## <a name="authentication-options"></a>Kimlik doğrulaması seçenekleri
Azure RemoteApp Microsoft hesapları ve Azure Active Directory hesaplarını destekler, ancak tüm koleksiyonlar tüm yöntemleri destekler. 

| Hesap türü |  | Bulut | Bulut + VNET | Karma |
| --- | --- | --- | --- | --- |
| Microsoft Hesabı | |Evet |Evet |Hayır |
| Azure Active Directory (Azure AD) | | | | |
| Yalnızca Azure AD |Evet |Evet |Hayır | |
| Parola Eşitleme ile AD Bağlan |Evet |Evet |Evet | |
| Parola Eşitleme olmadan AD Bağlan |Evet |Evet |Hayır | |
| AD Connect ile AD FS |Evet |Evet |Evet | |
| 3. taraf Azure tarafından desteklenen kimlik sağlayıcıları (örneğin, Ping) |Evet |Evet |Evet | |
| Multi-Factor Authentication | |Evet |Evet |Evet |

### <a name="cloud-and-cloud--vnet"></a>Bulut ve bulut + VNET
Bulut koleksiyonları ile Microsoft hesapları, Azure AD hesapları veya hello iki bir karışımını kullanabilirsiniz. Kullanıcılarınız için en iyi çalışır hello hesapları kullanın.

Microsoft hesapları kullanmak için belirli gereksinimler vardır. 

Toouse Azure AD hesapları istiyorsanız, Azure AD kiracınıza hello bir aboneliğinizle ilişkili eşleştiğinden emin toomake gerekir. Azure RemoteApp aboneliğiniz oluşturduğunuzda, kullanmakta olduğunuz hello Azure AD kiracısı aboneliğinizle otomatik olarak ilişkilendirildi. Herhangi bir Azure AD kullanıcı aynı kiracıyı tooneeds toobe izin verin. Gerekirse, [hello Azure AD kiracısını değiştirme](remoteapp-changetenant.md) aboneliğinizle ilişkili.

### <a name="hybrid-or-cloud--azure-ad--ad"></a>Karma (veya Bulut + Azure AD + AD)
Azure AD kullanarak + şirket içi Active Directory karma koleksiyon için bir önkoşuldur. Toouse AD Connect toointegrate hello iki dizini gerekir. Ancak toohow AD Connect yapılandırma geldiğinde bazı seçimi sahiptir. 

Parola Eşitleme veya AD Federasyon kullanarak bağlan Senaryo - 2 AD vardır. Merhaba denetleyin [AD Connect bilgi](../active-directory/active-directory-aadconnect.md) bunlardan çıkışı toofigure sizin için en iyi çalışır.

Bulut koleksiyonu ile Azure AD + AD de kullanabilirsiniz. Aynı adımları ayarlamak hello izlediğinizden emin olun.

Kullanıma [Azure AD + Azure RemoteApp için Active Directory gereksinimleri](remoteapp-ad.md) hello adımları gerekli tooconfigure Azure AD ve Active Directory için.

## <a name="go-create-your-collection"></a>Koleksiyonunuzu oluşturmak Git!
Tamam ' ı düşünün; böylece tek şey sol toodo biz bunu şimdi dahil edilir - ilk Azure RemoteApp koleksiyonu oluşturun.

[Bulut koleksiyonu oluşturma](remoteapp-create-cloud-deployment.md) veya [karma koleksiyon oluşturma](remoteapp-create-hybrid-deployment.md) -yalnızca oluşturma alın.

