---
title: "aaaAzure AD Microsoft Cloud Almanya Bağlan"
description: "Azure AD Connect, şirket içi dizinlerinizi Azure Active Directory ile tümleştirir. Bu, Office 365, Azure ve SaaS uygulamaları için ortak bir kimlik Azure AD ile tümleşik tooprovide sağlar."
keywords: "Giriş tooAzure AD Connect, Azure AD Connect'e genel bakış, Azure AD Connect nedir active directory, Almanya, siyah orman yükleme"
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: 2bcb0caf-5d97-46cb-8c32-bda66cc22dad
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: f32194fa6c365614f68e5d1ddcf0dac44d223292
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-in-microsoft-cloud-germany---public-preview"></a>Microsoft Bulut Almanya’da Azure AD Connect - Genel Önizleme
## <a name="introduction"></a>Giriş
Azure AD Connect, şirket içi Active Directory’niz ile Azure Active Directory arasında eşitleme sağlar.
Şu anda, birçok hello senaryolarda [Microsoft Cloud Almanya](https://www.microsoft.com/de-de/cloud/deutschland/default.aspx) hello operatör tarafından yapılması gerekir. Microsoft Cloud Almanya kullanırken hello aşağıdakilerin bilincinde olmanız gerekir:

* Merhaba aşağıdaki URL'ler eşitleme toooccur için bir proxy sunucusu başarıyla açılması gerekir:
  
  * *. microsoftonline.de
  * *.windows.net
  * * Sertifika İptal Listeleri
* Tooyour Azure AD dizininde oturum açtığınızda hello onmicrosoft.de etki alanındaki bir hesabı kullanmanız gerekir.
* özellikler aşağıdaki hello kullanılabilir değil:
  * Azure AD Connect Health
  * Otomatik güncelleştirmeler
 
## <a name="download"></a>İndir
Azure AD Connect hello portalındaki hello Azure AD Connect dikey penceresinden yükleyebilirsiniz.  Merhaba toolocate hello Azure AD Connect dikey aşağıdaki yönergeleri kullanın.

### <a name="hello-azure-ad-connect-blade"></a>Hello Azure AD Connect dikey penceresi
Toohello Azure portalında oturum açtıktan sonra aşağıdaki hello:

1. TooBrowse gidin
2. Azure Active Directory'yi seçin
3. Azure AD Connect'i seçin

Merhaba şunları görmeniz gerekir:

![Azure AD Connect Dikey Penceresi](media/active-directory-aadconnect-germany/germany1.png)

Merhaba aşağıdaki tabloda hello dikey penceresinde gösterilen hello özellikleri açıklar.

| Başlık | Açıklama |
| --- | --- |
| EŞİTLEME DURUMU |Eşitlemenin etkin mi yoksa devre dışı mı olduğunu gösterir. |
| SON EŞİTLEME |Son başarılı eşitleme tamamlandı hello. |
| FEDERASYON ETKİ ALANLARI |Şu anda yapılandırılmış Federasyon etki alanı Hello sayısını gösterir. |

## <a name="installation"></a>Yükleme
tooinstall Azure AD Connect, kullanabileceğiniz hello belgelerine [burada](active-directory-aadconnect.md#install-azure-ad-connect).

## <a name="advanced-features-and-additional-information"></a>Gelişmiş özellikler ve Ek Bilgiler
Özel ayarlar veya gelişmiş yapılandırmalar hakkında ek bilgiler ya da kılavuzluk edinmek için [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md) (Şirket içi kimliklerinizi Azure Active Directory ile tümleştirme) makalesinden başlayın.  Bu sayfayı tooadditional Kılavuzu bilgi ve bağlantılar sağlar.

