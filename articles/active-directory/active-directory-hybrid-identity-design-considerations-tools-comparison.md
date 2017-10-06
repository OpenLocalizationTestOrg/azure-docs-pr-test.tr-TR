---
title: "Karma Kimlik: Dizin tümleştirme araçları karşılaştırması | Microsoft Belgeleri"
description: "Bu sayfa hello karşılaştıran kapsamlı bir tablo dizin tümleştirmesi için kullanılabilen çeşitli dizin tümleştirme araçları sağlar."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: curtand
ms.assetid: 1e62a4bd-4d55-4609-895e-70131dedbf52
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: 18ac0a0f58726eceb85510df516e8db71429b313
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="hybrid-identity-directory-integration-tools-comparison"></a>Karma Kimlik dizin tümleştirme araçları karşılaştırması
Merhaba yıllar içinde hello dizin tümleştirme araçları büyütmüş ve gelişim.  Bu belge toohelp değil, bu araçlara yönelik birleştirilmiş bir görünüm ve her hello özellikleri karşılaştırması sağlar.

<!-- hello hardcoded link is a workaround for campaign ids not working in acom links-->

> [!NOTE]
> Azure AD Connect hello bileşenleri ve önceden Dirsync ve AAD eşitleme olarak yayımlanan işlevselliği içerir. Bu araçlar artık tek tek yayınlanmamaktadır ve ilerideki tüm geliştirmeler güncelleştirmeleri tooAzure AD eklenecektir bağlanma, böylece her zaman, nerede tooget hello en güncel işlevlere bilirsiniz.
> 
> DirSync ve Azure AD Eşitleme kullanım dışı bırakılmıştır. [Buradan](active-directory-aadconnect-dirsync-deprecated.md) daha fazla bilgi edinebilirsiniz.
> 
> 

Anahtarı her hello tablolar için aşağıdaki hello kullanın.

●  = Şimdi Kullanılabilir  
GS = Gelecekteki Sürüm  
GÖ = Genel Önizleme  

## <a name="on-premises-toocloud-synchronization"></a>Şirket içi tooCloud eşitleme
| Özellik | Azure Active Directory Connect | Azure Active Directory Eşitleme Hizmetleri (AAD Eşitleme) | Azure Active Directory Eşitleme Aracı (DirSync) | Forefront Identity Manager 2010 R2 (FIM) | Microsoft Identity Manager 2016 (MIM) |
|:--- |:---:|:---:|:---:|:---:|:---:|
| Toosingle bağlanmak şirket içi AD ormanı |● |● |● |● |● |
| Connect toomultiple şirket içi AD ormanına |● |● | |● |● |
| Connect toomultiple şirket içi Exchange kuruluşu |● | | | | |
| Toosingle şirket içi LDAP dizinine bağlanma |GS | | |● |● |
| Toomultiple şirket içi LDAP dizinine bağlanma |GS | | |● |● |
| Tooon içi bağlanmak AD ve şirket içi LDAP dizinleri |GS | | |● |● |
| Toocustom sistemleri (örneğin SQL, Oracle, MySQL, vb.) bağlanma |GS | | |● |● |
| Müşteri tanımlı öznitelikleri (dizin uzantıları) eşitleme |● | | | | |
| Tooon içi ik (SAP, Oracle eBusiness, PeopleSoft) bağlanma |GS | | |● |● |
| FIM eşitleme kurallarını ve bağlayıcıları tooon içi sistemlerinin sağlanmasını destekler. | | | |● |● |

## <a name="cloud-tooon-premises-synchronization"></a>Bulut tooOn içi eşitlemesi
| Özellik | Azure Active Directory Connect | Azure Active Directory Eşitleme Hizmetleri | Azure Active Directory Eşitleme Aracı (DirSync) | Forefront Identity Manager 2010 R2 (FIM) | Microsoft Identity Manager 2016 (MIM) |
|:--- |:---:|:---:|:---:|:---:|:---:|
| Cihazlar için geri yazma |● | |● | | |
| Öznitelik geri yazma (Exchange karma dağıtımı için) |● |● |● |● |● |
| Gruplar nesneleri için geri yazma |● | | | | |
| Parola geri yazma (self servis parola sıfırlama (SSPR) ve parola değiştirme işleminden) |● |● | | | |

## <a name="authentication-feature-support"></a>Kimlik Doğrulama Özelliği Desteği
| Özellik | Azure Active Directory Connect | Azure Active Directory Eşitleme Hizmetleri | Azure Active Directory Eşitleme Aracı (DirSync) | Forefront Identity Manager 2010 R2 (FIM) | Microsoft Identity Manager 2016 (MIM) |
|:--- |:---:|:---:|:---:|:---:|:---:|
| Tek şirket içi AD ormanı için Parola Eşitleme |● |● |● | | |
| Birden çok şirket içi AD ormanı için Parola Eşitleme |● |● | | | |
| Federasyon ile Çoklu Oturum Açma |● |● |● |● |● |
| Parola geri yazma (SSPR ve parola değiştirme işleminden) |● |● | | | |

## <a name="set-up-and-installation"></a>Kurulum ve Yükleme
| Özellik | Azure Active Directory Connect | Azure Active Directory Eşitleme Hizmetleri | Azure Active Directory Eşitleme Aracı (DirSync) | Microsoft Identity Manager 2016 (MIM) |
|:--- |:---:|:---:|:---:|:---:|
| Etki Alanı Denetleyicisi üzerinde yüklemeyi destekler |● |● |● | |
| SQL Express kullanarak yüklemeyi destekler |● |● |● | |
| DirSync'ten kolay yükseltme |● | | | |
| Yönetici kullanıcı Deneyiminin tooWindows Server dillerine yerelleştirmesi |● |● |● | |
| Son kullanıcı UX tooWindows Server dillerine yerelleştirmesi | | | |● |
| Windows Server 2008 ve Windows Server 2008 R2 desteği |● Eşitleme içindir, Federasyon için hayır |● |● |● |
| Windows Server 2012 ve Windows Server 2012 R2 desteği |● |● |● |● |

## <a name="filtering-and-configuration"></a>Filtreleme ve Yapılandırma
| Özellik | Azure Active Directory Connect | Azure Active Directory Eşitleme Hizmetleri | Azure Active Directory Eşitleme Aracı (DirSync) | Forefront Identity Manager 2010 R2 (FIM) | Microsoft Identity Manager 2016 (MIM) |
|:--- |:---:|:---:|:---:|:---:|:---:|
| Etki Alanları ve Kuruluş Birimleri üzerinde filtreleme |● |● |● |● |● |
| Nesnelerin öznitelik değerleri üzerinde filtreleme |● |● |● |● |● |
| Eşitlenen öznitelikler toobe (MinSync) en az sayıda izin ver |● |● | | | |
| Öznitelik akışları için uygulanan farklı hizmet şablonları toobe izin ver |● |● | | | |
| AD tooAzure AD akan özniteliklerin kaldırılması izin ver |● |● | | | |
| Öznitelik akışları için gelişmiş özelleştirmeye izin ver |● |● | |● |● |

## <a name="next-steps"></a>Sonraki adımlar
[Şirket içi kimliklerinizi Azure Active Directory ile tümleştirme](active-directory-aadconnect.md) hakkında daha fazla bilgi edinin.

