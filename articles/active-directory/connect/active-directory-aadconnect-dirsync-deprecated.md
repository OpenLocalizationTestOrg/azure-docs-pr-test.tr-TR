---
title: "DirSync ve Azure AD eşitleme aaaUpgrade | Microsoft Docs"
description: "Açıklar nasıl tooupgrade DirSync ve Azure AD eşitleme tooAzure AD alanından Bağlan."
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: bd68fb88-110b-4d76-978a-233e15590803
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: d465b137fb54f0c6e28ccf73429c4bd3aafd8698
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="upgrade-windows-azure-active-directory-sync-and-azure-active-directory-sync"></a>Windows Azure Active Directory eşitleme ve Azure Active Directory Eşitleme'yi Yükselt
Azure AD Connect şirket içi dizininizi Azure AD ile en iyi şekilde tooconnect hello ve Office 365. Çok fazla zaman tooupgrade tooAzure AD Connect Windows Azure Active Directory eşitleme (DirSync) veya Azure AD eşitleme olarak bu araçlar artık kullanım dışı ve destek 13 Nisan 2017 tarihinde sona ermesi ulaşabileceği bir budur.

kullanım dışı bırakılmıştır hello iki kimlik eşitleme Araçları tek orman müşteriler (DirSync) ve Çoklu orman ve diğer gelişmiş müşteriler (Azure AD eşitleme) sunulan. Bu eski araçları tüm senaryoları için kullanılabilir olan tek bir çözüm değiştirilmiştir: Azure AD Connect. Yeni işlev, özellik geliştirmeleri ve yeni senaryolar için destek sunar. toobe mümkün toocontinue toosynchronize, şirket içi kimlik veri tooAzure AD ve Office 365, tooAzure AD yükseltmenizi öneririz Bağlan.

DirSync son sürümü Hello Temmuz 2014'te yayımlanmıştır ve Azure AD eşitleme son sürümü hello Mayıs 2015'te yayımlanmıştır.

## <a name="what-is-azure-ad-connect"></a>Azure AD Connect nedir?
Azure AD Connect hello ardıl tooDirSync ve Azure AD eşitleme ' dir. Bu, desteklenen bu iki tüm senaryoları birleştirir. Daha fazla bilgiyi içinde hakkında [şirket içi kimliklerinizi Azure Active Directory ile tümleştirme](active-directory-aadconnect.md).

## <a name="deprecation-schedule"></a>Kullanımdan kaldırma zamanlaması
| Tarih | Açıklama |
| --- | --- |
| 13 Nisan 2016 |Windows Azure Active Directory eşitleme ("DirSync") ve Microsoft Azure Active Directory eşitleme ("Azure AD eşitleme") kullanım dışı bırakıldı olarak bildirilir. |
| 13 Nisan 2017 |Desteği sona eriyor. Müşteriler artık mümkün tooopen tooAzure AD yükseltme olmadan bir destek servis talebi olması önce bağlanın. |
|31 Aralık 2017|Azure AD artık Windows Azure Active Directory eşitleme ("DirSync") ve Microsoft Azure Active Directory eşitleme ("Azure AD eşitleme") gelen iletişimleri kabul eder.

## <a name="how-tootransition-tooazure-ad-connect"></a>Nasıl tootransition tooAzure AD Connect
DirSync çalıştırıyorsanız, Yükseltme yapabileceğiniz iki yolu vardır: yerinde yükseltme ve paralel dağıtım. Yerinde yükseltme çoğu müşteri için önerilen ve en son varsa işletim sistemi ve 50. 000'den az nesneniz. Diğer durumlarda, Azure AD Connect çalıştıran tooa yeni sunucu toodo DirSync yapılandırmanızı olduğu paralel dağıtım taşınmış önerilir.

Azure AD eşitleme kullanırsanız, bir yerinde yükseltme önerilir. İsterseniz, yeni bir Azure AD Connect sunucusu paralel olası tooinstall olduğunu ve Azure AD eşitleme sunucusu tooAzure AD esnek geçişini yapmak Bağlan.

| Çözüm | Senaryo |
| --- | --- |
| [DirSync’ten yükseltme](active-directory-aadconnect-dirsync-upgrade-get-started.md) |<li>Zaten çalışmakta olan bir DirSync sunucunuz varsa.</li> |
| [Azure AD eşitleme'den yükseltme](active-directory-aadconnect-upgrade-previous-version.md) |<li>Azure AD eşitleme'den taşıyorsanız.</li> |

Toosee nasıl istiyorsanız toodo bir yerinde yükseltme DirSync tooAzure AD Connect, sonra bu Channel 9 video bkz:

> [!VIDEO https://channel9.msdn.com/Series/Azure-Active-Directory-Videos-Demos/Azure-Active-Directory-Connect-in-place-upgrade-from-legacy-tools/player]
>
>

## <a name="faq"></a>SSS
**S: bir e-posta bildirimi hello Azure ekibi ve/veya ileti hello Office 365 ileti Merkezi'nden aldım ancak bağlanırken kullanılacak.**  
Merhaba bildirim ayrıca yapı numarası 1.0 ile Azure AD Connect'i kullanarak toocustomers gönderildi. \*.0 (öncesi 1.1 sürüm kullanarak). Microsoft Azure AD Connect ile geçerli toostay serbest müşteriler önerir. Merhaba [otomatik yükseltme](active-directory-aadconnect-feature-automatic-upgrade.md) de 1.1 sunulan özelliğinin kolay tooalways kılar Azure AD Connect'i yeni bir sürümü yüklü.

**S: olacak DirSync/Azure AD eşitleme çalışmamaya 13 Nisan 2017?**  
DirSync/Azure AD eşitleme toowork 13 Nisan 2017 üzerinde devam eder.  Ancak, Azure AD DirSync/Azure AD eşitleme iletişimlerinden 31 Aralık 2017 üzerinde kabul artık.

**S: gelen hangi DirSync sürümleri yükseltebilir miyim?**  
Şu anda kullanılan DirSync sürümünden desteklenen tooupgrade olur.

**S: ne hakkında FIM/MIM için Azure AD Bağlayıcısı hello?**  
Merhaba FIM/MIM için Azure AD Bağlayıcısı sahip **değil** edilmiş kullanım dışı duyurdu. Bu **özelliği dondurma**; hiçbir yeni işlevsellik eklenir ve hiçbir hata düzeltmeleri alır. Microsoft önerir tooplan toomove dışarı kullanan müşteriler tooAzure AD Connect. Kesinlikle olduğu toonot başlangıç kullanmaya yeni dağıtımların önerilir. Bu bağlayıcı hello gelecekteki kullanım dışı duyurulacaktır.

## <a name="additional-resources"></a>Ek Kaynaklar
* [Şirket içi kimliklerinizi Azure Active Directory ile tümleştirme](active-directory-aadconnect.md)
