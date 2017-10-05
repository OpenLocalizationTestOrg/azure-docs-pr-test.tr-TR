---
title: "Azure MFA sürümleri ve tüketim planları | Microsoft Docs"
description: "Çok faktörlü kimlik doğrulaması istemci farklı yöntemler ve kullanılabilir sürümlerini hakkında bilgiler. Her tüketim plan ayrıntıları"
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
ms.openlocfilehash: 5adffb0d461503b57ff9152671c44716dd044b1e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-get-azure-multi-factor-authentication"></a>Azure multi-Factor Authentication alma

Hesaplarınızı korumaya geldiğinde, iki aşamalı doğrulama, kuruluş genelinde standart olmalıdır. Bu özellik, ayrıcalıklı kaynaklara erişimi olan yönetici hesapları için özellikle önemlidir. Bu nedenle, Microsoft Office 365 ve Azure yöneticilere temel iki aşamalı doğrulama özellikleri sunar. Yöneticilerinizin özelliklerini Yükselt ya da kullanıcılarınızın geri kalanı için iki aşamalı doğrulamayı genişletmek istiyorsanız, Azure multi-Factor Authentication satın alabilirsiniz. 

Bu makalede yer almaktadır yöneticileri ve Azure MFA'ın tam sürümünü sunulan sürümleri arasındaki farkı açıklar ve hangi özelliklerin her kullanılabilir olduğunu belirtir. Teklifi tam Azure MFA dağıtmak hazırsanız, sonraki bölümlerde uygulama seçenekleri ve Microsoft tüketim nasıl hesaplar kapsar.

>[!IMPORTANT]
>Bu makalede, Azure multi-Factor Authentication satın almak için kullanılabilecek çeşitli yöntemler anlamanıza yardımcı olacak bir kılavuz olması amaçlanmıştır. Fiyatlandırma ve faturalama hakkında belirli Ayrıntılar için her zaman için başvurmalıdır [çok faktörlü kimlik doğrulaması fiyatlandırma sayfası](https://azure.microsoft.com/pricing/details/multi-factor-authentication/).

## <a name="available-versions-of-azure-multi-factor-authentication"></a>Azure multi-Factor Authentication kullanılabilir sürümleri

Aşağıdaki tabloda, çok faktörlü kimlik doğrulaması üç sürümleri arasındaki farklar açıklanmaktadır:

| Sürüm | Açıklama |
| --- | --- |
| Office 365 için Multi-Factor Authentication |Bu sürümü yalnızca Office 365 uygulamaları ile çalışır ve Office 365 Portalı'ndan yönetilen. Yöneticiler [iki aşamalı doğrulama ile Office 365 kaynakları güvenli hale getirme](https://support.office.com/article/Set-up-multi-factor-authentication-for-Office-365-users-8f0454b2-f51a-4d9c-bcde-2c48e41621c6). Bu sürüm bir Office 365 aboneliğinizin bir parçasıdır. |
| Azure yöneticileri için çok faktörlü kimlik doğrulaması | Azure kiracıların genel Yöneticiler, genel yönetici hesaplarını hiçbir ek ücret ödemeden için iki aşamalı doğrulamayı etkinleştirebilirsiniz.|
| Azure Multi-Factor Authentication | Genellikle için "tam" sürüm olarak adlandırılır, Azure multi-Factor Authentication richest kümesi sunar. Aracılığıyla ek yapılandırma seçeneklerini sağlar [Klasik Azure portalı](https://manage.windowsazure.com), Gelişmiş raporlama ve şirket içi aralığı için destek ve bulut uygulamaları. Azure çok faktörlü kimlik doğrulaması Azure Active Directory Premium (P1 ve P2 planları) ve Enterprise Mobility + güvenlik (E3 ve E5 planları) içinde bulunur ve olabilir ya da dağıtılmış [bulutta veya şirket içi](multi-factor-authentication-get-started.md). |

## <a name="feature-comparison-of-versions"></a>Sürümlerinin özellik karşılaştırması
Aşağıdaki tabloda, çeşitli Azure multi-Factor Authentication'ın sürümlerinde kullanılabilen özellikleri listesini sağlar.

> [!NOTE]
> Bu karşılaştırma tablosu, çok faktörlü kimlik doğrulaması her sürümü parçası olan özellikler açıklanmaktadır. Tam Azure çok faktörlü kimlik doğrulama hizmeti varsa, bazı özellikler bağlı olarak kullanıp kullanılamayabilir [bulutta MFA veya MFA şirket içi](multi-factor-authentication-get-started.md).


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

## <a name="how-to-get-azure-multi-factor-authentication"></a>Azure multi-Factor Authentication alma
Azure multi-Factor Authentication tarafından sunulan tam işlevselliği istiyorsanız, birkaç seçeneğiniz vardır:

### <a name="option-1---mfa-licenses"></a>Seçenek 1 - MFA lisansları

Azure çok faktörlü kimlik doğrulama lisansı satın alın ve kullanıcılarınızın Azure Active Directory'de atayın. 

Bu seçeneği kullanırsanız, yalnızca aynı zamanda lisansları olmayan bazı kullanıcılar için iki aşamalı doğrulamayı sağlamanız gerekir, bir Azure çok faktörlü kimlik doğrulama sağlayıcısı oluşturmanız gerekir. Aksi takdirde, iki kez fatura.

### <a name="option-2---bundled-licenses-that-include-mfa"></a>MFA dahil paketlenmiş seçeneği 2 - lisansları

Kullanıcılarınızın Azure Active Directory'de atayın ve Azure Active Directory Premium (P1 veya P2) veya Enterprise Mobility + Security'nin (E3 veya E5) gibi Azure multi-Factor Authentication içeren lisansları satın alın. 

Bu seçeneği kullanırsanız, yalnızca aynı zamanda lisansları olmayan bazı kullanıcılar için iki aşamalı doğrulamayı sağlamanız gerekir, bir Azure çok faktörlü kimlik doğrulama sağlayıcısı oluşturmanız gerekir. Aksi takdirde, iki kez fatura. 

### <a name="option-3---mfa-consumption-based-model"></a>Seçenek 3 - MFA tüketim tabanlı modeli

Bir Azure aboneliği içindeki Azure çok faktörlü kimlik doğrulama sağlayıcısı oluşturun. Azure MFA sağlayıcıları Kurumsal Anlaşma, Azure parasal taahhüt veya kredi kartı gibi diğer tüm Azure kaynaklarına karşı faturalandırılır Azure kaynaklardır. Bu sağlayıcılar, yalnızca tam Azure abonelik bir harcama sınırı 0 sınırlı Azure aboneliklerini oluşturulabilir. Lisans gibi seçenekleri 1 ve 2 etkinleştirdiğinizde sınırlı abonelikleri oluşturulur. 

Azure çok faktörlü kimlik doğrulama sağlayıcısı kullanırken, Azure aboneliğinizin faturalandırılır kullanılabilir iki kullanım modeli vardır:  

1. **Kullanıcı başına** - sabit sayıda düzenli aralıklarla kimlik doğrulama isteyen çalışanlar için iki aşamalı doğrulamayı etkinleştirmek istediğiniz kurumlar için. Kullanıcı başına faturalama MFA için Azure AD kiracınıza ve/veya Azure MFA sunucusu etkin kullanıcı sayısını temel alır. Kullanıcılar için MFA hem de Azure AD'de etkin olup olmadığını ve Azure MFA sunucusu ve etki alanı eşitleme (Azure AD Connect) etkinleştirilmişse, ardından biz kullanıcıları büyük kümesini sayısı. Etki alanı eşitleme etkin değil sonra biz tüm kullanıcılar Azure AD'de MFA için etkin toplam sayısı ve Azure MFA sunucusu. Faturalama eşit olarak ve ticaret sisteme günlük bildirdi. 

  > [!NOTE]
  > Faturalama örnek 1: MFA için bugün etkin 5.000 kullanıcıların sahip. MFA sistem bu sayıyı o gün için 31 ve raporları 161.29 kullanıcılar tarafından böler. Yarın MFA sistem 161.77 kullanıcılar o gün için raporlar için 15 daha fazla kullanıcı etkinleştirin. Faturalama döngüsü sonu Azure aboneliğinize göre faturalandırılır kullanıcıların toplam sayısı kadar 5.000 ekler. 
  >
  > Faturalama örnek 2: farkını yapmak için bir kullanıcı başına Azure MFA sağlayıcısı alacak şekilde lisansların ve olmadan, kullanıcılar karışımına sahip. 4.500 vardır, Enterprise Mobility + Kiracı güvenlik lisansları ancak MFA için etkin 5.000 kullanıcıların. Azure aboneliğinizin 500 kullanıcılar için faturalandırılır, eşit olarak ve günlük 16.13 kullanıcılar olarak bildirdi. 

2. **Kimlik doğrulaması başına** - çok sayıda seyrek kimlik doğrulaması gereken kullanıcılar için iki aşamalı doğrulamayı etkinleştirmek istediğiniz kurumlar için. Faturalama bu Doğrulamalar başarılı veya reddedilir bağımsız olarak Azure MFA bulut hizmeti tarafından alınan iki aşamalı doğrulama isteklerinin sayısını temel alır. Bu fatura Azure kullanım deyiminizde 10 kimlik doğrulama paketlerine görünür ve ticaret sisteme günlük bildirilir. 

  > [!NOTE]
  > Faturalama örnek 3: Bugün, Azure MFA hizmeti 3,105 iki aşamalı doğrulama isteği aldı. Azure aboneliğiniz için 310.5 kimlik doğrulama paketlerini faturalandırılır. 

Azure MFA lisansları olabilir, ancak hala tüketim tabanlı yapılandırma için fatura dikkate almak önemlidir. Bir kimlik doğrulaması başına Azure MFA Sağlayıcısı'nı ayarlarsanız, her iki aşamalı doğrulama isteği için olanlar lisanslara sahip kullanıcılar tarafından gerçekleştirilen faturalandırılır. Azure AD kiracınıza bağlı olmayan bir etki alanındaki bir kullanıcı Azure MFA Sağlayıcısı'nı ayarlarsanız, kullanıcılarınızın üzerinde Azure AD lisanslara sahip olsa bile etkin kullanıcı başına faturalandırılır. 

## <a name="next-steps"></a>Sonraki adımlar

- Daha fazla fiyatlandırma ayrıntıları için bkz: [Azure MFA fiyatlandırma](https://azure.microsoft.com/pricing/details/multi-factor-authentication/).

- Azure MFA dağıtmak isteyip istemediğinizi seçin [bulutta veya şirket içi](multi-factor-authentication-get-started.md)