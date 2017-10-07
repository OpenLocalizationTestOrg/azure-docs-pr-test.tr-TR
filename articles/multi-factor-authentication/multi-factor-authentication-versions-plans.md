---
title: "aaaAzure MSF sürümleri ve tüketim planlar | Microsoft Docs"
description: "Merhaba çok faktörlü kimlik doğrulama istemcisi ve hello farklı yöntemler ve kullanılabilir sürümlerini hakkında bilgiler. Her tüketim plan ayrıntıları"
keywords: 
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: 
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: kgremban
ms.openlocfilehash: 4914747e435531b9f950356d23aa386f3d9585d2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooget-azure-multi-factor-authentication"></a>Nasıl tooget Azure çok faktörlü kimlik doğrulaması

Hesaplarınızı tooprotecting geldiğinde, iki aşamalı doğrulama, kuruluş genelinde standart olmalıdır. Bu özellik erişim tooresources ayrıcalıklı olan yönetici hesapları için özellikle önemlidir. Bu nedenle, Microsoft temel iki aşamalı doğrulama özellikleri tooOffice 365 ve Azure Yöneticiler sunar. Yöneticiler için tooupgrade hello özellikler istiyorsanız veya iki aşamalı doğrulama toohello rest kullanıcılarınızın genişletmek, Azure multi-Factor Authentication satın alabilirsiniz. 

Bu makalede yer almaktadır hello fark tooadministrators ve hello tam Azure MFA sürümünü sunulan hello sürümleri arasında açıklar ve hangi özelliklerin her kullanılabilir olduğunu belirtir. Hazır olduğunuzda toodeploy hello Azure MFA sunumu tamamlamak, sonraki bölümlerde kapsar uygulama seçenekleri ve Microsoft tüketim nasıl hesaplar hello.

>[!IMPORTANT]
>Bu makalede toobe tasarlanmıştır anladığınızdan Kılavuzu toohelp hello farklı şekillerde toobuy Azure çok faktörlü kimlik doğrulaması. Fiyatlandırma ve faturalama hakkında belirli Ayrıntılar için her zaman toohello başvurmalıdır [çok faktörlü kimlik doğrulaması fiyatlandırma sayfası](https://azure.microsoft.com/pricing/details/multi-factor-authentication/).

## <a name="available-versions-of-azure-multi-factor-authentication"></a>Azure multi-Factor Authentication kullanılabilir sürümleri

Merhaba aşağıdaki tabloda çok faktörlü kimlik doğrulaması üç sürümleri arasında hello farklar açıklanmaktadır:

| Sürüm | Açıklama |
| --- | --- |
| Office 365 için Multi-Factor Authentication |Bu sürüm yalnızca Office 365 uygulamaları ile çalışır ve hello Office 365 portalından yönetilir. Yöneticiler [iki aşamalı doğrulama ile Office 365 kaynakları güvenli hale getirme](https://support.office.com/article/Set-up-multi-factor-authentication-for-Office-365-users-8f0454b2-f51a-4d9c-bcde-2c48e41621c6). Bu sürüm bir Office 365 aboneliğinizin bir parçasıdır. |
| Azure yöneticileri için çok faktörlü kimlik doğrulaması | Azure kiracıların genel Yöneticiler, genel yönetici hesaplarını hiçbir ek ücret ödemeden için iki aşamalı doğrulamayı etkinleştirebilirsiniz.|
| Azure Multi-Factor Authentication | Sık sık başvurulan tooas hello "tam" sürümü, Azure multi-Factor Authentication hello richest özellik kümesi sunar. Merhaba aracılığıyla ek yapılandırma seçeneklerini sağlar [Klasik Azure portalı](https://manage.windowsazure.com), Gelişmiş raporlama ve şirket içi aralığı için destek ve bulut uygulamaları. Azure çok faktörlü kimlik doğrulaması Azure Active Directory Premium (P1 ve P2 planları) ve Enterprise Mobility + güvenlik (E3 ve E5 planları) içinde bulunur ve olabilir ya da dağıtılmış [hello bulutta veya şirket içi](multi-factor-authentication-get-started.md). |

## <a name="feature-comparison-of-versions"></a>Sürümlerinin özellik karşılaştırması
Merhaba aşağıdaki tabloda hello kullanılabilir hello özelliklerin bir listesi çeşitli sürümlerini Azure çok faktörlü kimlik doğrulaması sağlar.

> [!NOTE]
> Bu karşılaştırma tablosu çok faktörlü kimlik doğrulaması her sürümü parçası olan hello özellikleri açıklanmaktadır. Merhaba tam Azure çok faktörlü kimlik doğrulama hizmeti varsa, bazı özellikler bağlı olarak kullanıp kullanılamayabilir [hello bulutta MFA veya MFA şirket içi](multi-factor-authentication-get-started.md).


| Özellik | Office 365 için Multi-Factor Authentication | Azure yöneticileri için çok faktörlü kimlik doğrulaması | Azure Multi-Factor Authentication |
| --- |:---:|:---:|:---:|
| Yönetici hesapları MFA ile koruma |● |● (yalnızca genel yönetici hesapları için) |● |
| İkinci öğe olarak mobil uygulama |● |● |● |
| İkinci öğe olarak telefon araması |● |● |● |
| İkinci öğe olarak SMS |● |● |● |
| MFA desteklemeyen istemciler için uygulama parolaları |● |● |● |
| Doğrulama yöntemleri üzerinde yönetici denetimi |● |● |● |
| PIN modu | | |● |
| Sahtekarlık uyarısı | | |● |
| MFA Raporları | | |● |
| Bir Kerelik Atlama | | |● |
| Telefon aramaları için özel karşılama | | |● |
| Telefon aramaları için özel arayan kimliği | | |● |
| Güvenilen IP'ler | | |● |
| Güvenilen cihazlar için MFA hatırlama |● |● |● |
| MFA SDK | | |● (gerektirir multi-Factor Auth sağlayıcısı ve tam Azure abonelik) |
| MFA için şirket içi uygulamalar | | |● |

## <a name="how-tooget-azure-multi-factor-authentication"></a>Nasıl tooget Azure çok faktörlü kimlik doğrulaması
Azure multi-Factor Authentication tarafından sunulan hello tam işlevselliği istiyorsanız, birkaç seçeneğiniz vardır:

### <a name="option-1---mfa-licenses"></a>Seçenek 1 - MFA lisansları

Azure çok faktörlü kimlik doğrulama lisansı satın alın ve Azure Active Directory'de tooyour kullanıcılar atayın. 

Bu seçeneği kullanırsanız, yalnızca size ayrıca tooprovide iki aşamalı doğrulamayı lisansları olmayan bazı kullanıcılar için gerekiyorsa, bir Azure çok faktörlü kimlik doğrulama sağlayıcısı oluşturmanız gerekir. Aksi takdirde, iki kez fatura.

### <a name="option-2---bundled-licenses-that-include-mfa"></a>MFA dahil paketlenmiş seçeneği 2 - lisansları

Azure Active Directory'de tooyour kullanıcılar atayın ve Azure Active Directory Premium (P1 veya P2) veya Enterprise Mobility + Security'nin (E3 veya E5) gibi Azure multi-Factor Authentication içeren lisansları satın alın. 

Bu seçeneği kullanırsanız, yalnızca size ayrıca tooprovide iki aşamalı doğrulamayı lisansları olmayan bazı kullanıcılar için gerekiyorsa, bir Azure çok faktörlü kimlik doğrulama sağlayıcısı oluşturmanız gerekir. Aksi takdirde, iki kez fatura. 

### <a name="option-3---mfa-consumption-based-model"></a>Seçenek 3 - MFA tüketim tabanlı modeli

Bir Azure aboneliği içindeki Azure çok faktörlü kimlik doğrulama sağlayıcısı oluşturun. Azure MFA sağlayıcıları Kurumsal Anlaşma, Azure parasal taahhüt veya kredi kartı gibi diğer tüm Azure kaynaklarına karşı faturalandırılır Azure kaynaklardır. Bu sağlayıcılar, yalnızca tam Azure abonelik bir harcama sınırı 0 sınırlı Azure aboneliklerini oluşturulabilir. Lisans gibi seçenekleri 1 ve 2 etkinleştirdiğinizde sınırlı abonelikleri oluşturulur. 

Azure çok faktörlü kimlik doğrulama sağlayıcısı kullanırken, Azure aboneliğinizin faturalandırılır kullanılabilir iki kullanım modeli vardır:  

1. **Kullanıcı başına** - tooenable iki aşamalı doğrulama için düzenli aralıklarla kimlik doğrulama gereken çalışanlar sabit sayıda istediğiniz kurumlar için. Kullanıcı başına faturalama hello MFA için Azure AD kiracınıza ve/veya Azure MFA sunucusu etkin kullanıcı sayısını temel alır. Kullanıcılar için MFA hem de Azure AD'de etkin olup olmadığını ve Azure MFA sunucusu ve etki alanı eşitleme (Azure AD Connect) etkinleştirilmişse, ardından biz hello kapsamlı kullanıcıların sayısı. Etki alanı eşitleme etkin değil sonra size Azure AD MFA için etkinleştirilmiş tüm kullanıcılar hello toplamını sayısı ve Azure MFA sunucusu. Faturalama eşit olarak bölünmüş ve bildirilen toohello ticaret günlük sistemidir. 

  > [!NOTE]
  > Faturalama örnek 1: MFA için bugün etkin 5.000 kullanıcıların sahip. Merhaba MFA sistem bu sayıyı o gün için 31 ve raporları 161.29 kullanıcılar tarafından böler. Yarın Hello MFA sistem 161.77 kullanıcılar o gün için raporlar için 15 daha fazla kullanıcı etkinleştirin. Faturalama döngüsü hello Hello sonuna 5.000 tooaround hello toplam sayısı, Azure aboneliğinize göre faturalandırılır kullanıcı ekler. 
  >
  > Faturalama örnek 2: kullanıcı başına Azure MFA sağlayıcısı toomake hello fark yukarı alacak şekilde lisansların ve olmadan, kullanıcılar karışımına sahip. 4.500 vardır, Enterprise Mobility + Kiracı güvenlik lisansları ancak MFA için etkin 5.000 kullanıcıların. Azure aboneliğinizin 500 kullanıcılar için faturalandırılır, eşit olarak ve günlük 16.13 kullanıcılar olarak bildirdi. 

2. **Kimlik doğrulaması başına** - tooenable iki aşamalı doğrulamayı çok sayıda seyrek kimlik doğrulaması gereken kullanıcılar için istediğiniz kurumlar için. Faturalama hello hello bu Doğrulamalar başarılı veya reddedilir bağımsız olarak Azure MFA bulut hizmeti tarafından alınan iki aşamalı doğrulama isteklerinin sayısını temel alır. Bu fatura Azure kullanım deyiminizde 10 kimlik doğrulama paketlerine görünür ve bildirilen toohello ticaret günlük sistemidir. 

  > [!NOTE]
  > Faturalama örnek 3: Bugün, hello Azure MFA hizmeti 3,105 iki aşamalı doğrulama isteği aldı. Azure aboneliğiniz için 310.5 kimlik doğrulama paketlerini faturalandırılır. 

Azure MFA lisansları olabilir, ancak hala tüketim tabanlı yapılandırma için fatura önemli toonote olur. Bir kimlik doğrulaması başına Azure MFA Sağlayıcısı'nı ayarlarsanız, her iki aşamalı doğrulama isteği için olanlar lisanslara sahip kullanıcılar tarafından gerçekleştirilen faturalandırılır. Bağlantılı tooyour Azure AD kiracısı olmayan bir etki alanında bir kullanıcı Azure MFA Sağlayıcısı'nı ayarlama, kullanıcılarınızın üzerinde Azure AD lisanslara sahip olsa bile etkin kullanıcı başına faturalandırılır. 

## <a name="next-steps"></a>Sonraki adımlar

- Daha fazla fiyatlandırma ayrıntıları için bkz: [Azure MFA fiyatlandırma](https://azure.microsoft.com/pricing/details/multi-factor-authentication/).

- Seçin olup olmadığını toodeploy Azure MFA [hello Bulut veya şirket içi](multi-factor-authentication-get-started.md)
