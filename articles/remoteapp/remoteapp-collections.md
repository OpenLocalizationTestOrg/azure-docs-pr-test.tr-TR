---
title: "Azure RemoteApp için nasıl bir koleksiyona ihtiyacınız var? | Microsoft Belgeleri"
description: "Azure RemoteApp ile kullanılabilir koleksiyonların türleri hakkında bilgi edinin."
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
ms.openlocfilehash: 10f6c0533027767b6635ebff1e6a9872bde06a68
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="what-kind-of-collection-do-you-need-for-azure-remoteapp"></a>Azure RemoteApp için nasıl bir koleksiyona ihtiyacınız var?
> [!IMPORTANT]
> Azure RemoteApp 31 Ağustos 2017’de kullanımdan kaldırılacaktır. Ayrıntılı bilgi için [duyuruyu](https://go.microsoft.com/fwlink/?linkid=821148) okuyun.
> 
> 

Azure RemoteApp uygulamalarına ve kaynaklarına herhangi bir cihazda kullanıcılarla paylaşmanıza olanak tanır. Uygulamaları ve kaynakları tutmak için koleksiyonları oluşturarak bunu ve sonra bu koleksiyonları kullanıcılarıyla paylaşabilirsiniz. Farklı ağ ve sizin için uygun olan kimlik doğrulama seçenekleri - 2 farklı toplama seçeneklerini misiniz?

Şimdi farklı önemli noktalar ve en iyi Azure RemoteApp koleksiyonunuzun almak yapmanız gereken seçimler yol. 

## <a name="quick-differences-between-the-collection-types"></a>Hızlı farklarını koleksiyon türleri
|  | Bulut | Karma |
| --- | --- | --- |
| Varolan bir sanal ağ kullanın |Evet |Evet |
| AD bağlı hesapları (DirSync) gerektirir |Hayır |Evet |
| Etki alanına katılma gerektirir |Hayır |Evet |
| Etki alanı denetleyicisi VNET'e erişilebilir gerektirir |Hayır |Evet |

## <a name="cloud-collections"></a>Bulut koleksiyonları
* Hızlı oluşturmak - uygulamalarınızı kullanıcılara daha hızlı alma anlamına gelir, koleksiyon hızlı bir şekilde sağlanır.
* Bizim paylaşma veya kendi uygulamalarınızı getirin. (Bir Azure sanal makineden yerleşik) özel bir görüntü veya aboneliğinizde yer alan görüntülerden birini kullanabilirsiniz.
* Koleksiyonunuz ve şirket içi etki alanınızın arasında bir bağlantı yapılandırmak gerekmez.
* Ancak isteğe bağlı olarak şirket içi ortamınıza veri paylaşımı için erişim sağlamak veya (veritabanı kimlik doğrulaması kullanarak) SQL Server gibi kaynaklarına içine Windows dışı kimlik doğrulaması kullanacak şekilde kendi Azure VNET kullanabilirsiniz.

Tamam, bir nasıl oluşturabilirim?

* Yalnızca bulutta? İle oluşturma **hızlı Oluştur** portalında seçeneği.
* Bulut + VNET? Kullanarak oluşturduğunuz **Create VNET ile** seçeneği ancak bir etki alanına katılmak seçmeyin.

## <a name="hybrid-collections"></a>Karma koleksiyonlar
* Şirket içi ağ + Azure VNET tam erişim sağlar.
* Etki alanı katılma erişimi uygulamaları ve verileri içerir. Uzak uygulamalar, şirket içi Active Directory kimlik doğrulaması için - sonra etki alanındaki kaynaklara erişebilir.
* Gelişmiş izleme ve var olan System Center çözümlerini ve Windows grup ilkeleri ile Yönetimi (aracılığıyla, Windows Server 2012 R2'de oluşturulan özel bir görüntü) etkinleştir
* Destek [ExpressRoute](https://azure.microsoft.com/services/expressroute/) yerel ağınızı Azure sanal bağlanmak için.

Kullanarak oluşturduğunuz **Create VNET ile** seçeneği ve bir etki alanına katılmak seçin.

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
Bulut koleksiyonları ile Microsoft hesapları, Azure AD hesapları veya ikisinin bir karışımı kullanabilirsiniz. Kullanıcılarınız için en iyi iş hesaplarını kullanın.

Microsoft hesapları kullanmak için belirli gereksinimler vardır. 

Azure AD hesapları kullanmak istiyorsanız, Azure AD kiracınıza bir aboneliğinizle ilişkili eşleştiğinden emin olmak gerekir. Azure RemoteApp aboneliğiniz oluşturduğunuzda, kullanmakta olduğunuz Azure AD kiracısı aboneliğinizle otomatik olarak ilişkilendirildi. İzin verdiğiniz herhangi bir Azure AD kullanıcı aynı kiracıyı olması gerekir. Gerekirse, [Azure AD kiracısını değiştirme](remoteapp-changetenant.md) aboneliğinizle ilişkili.

### <a name="hybrid-or-cloud--azure-ad--ad"></a>Karma (veya Bulut + Azure AD + AD)
Azure AD kullanarak + şirket içi Active Directory karma koleksiyon için bir önkoşuldur. İki dizin tümleştirmek için AD Connect kullanmanız gerekir. Ancak AD Connect yapılandırma nasıl geldiğinde bazı seçimi sahiptir. 

Parola Eşitleme veya AD Federasyon kullanarak bağlan Senaryo - 2 AD vardır. Kullanıma [AD Connect bilgi](../active-directory/active-directory-aadconnect.md) hangi bu works'ün en iyi sizin için bulmak için.

Bulut koleksiyonu ile Azure AD + AD de kullanabilirsiniz. Aynı adımları ayarlamak izlediğinizden emin olun.

Kullanıma [Azure AD + Azure RemoteApp için Active Directory gereksinimleri](remoteapp-ad.md) Azure AD yapılandırmak için gerekli adımlar için ve Active Directory.

## <a name="go-create-your-collection"></a>Koleksiyonunuzu oluşturmak Git!
Tamam, bu yüzden sol yapın - ilk Azure RemoteApp koleksiyonu oluşturmak için tek şey biz bunu şimdi dahil edilir düşünüyorum.

[Bulut koleksiyonu oluşturma](remoteapp-create-cloud-deployment.md) veya [karma koleksiyon oluşturma](remoteapp-create-hybrid-deployment.md) -yalnızca oluşturma alın.

