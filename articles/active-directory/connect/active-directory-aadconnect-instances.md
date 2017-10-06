---
title: "Azure AD Connect: Eşitleme hizmeti örnekleri | Microsoft Docs"
description: "Bu sayfa, Azure AD örnekleri için özel hususlar belgeler."
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: f340ea11-8ff5-4ae6-b09d-e939c76355a3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 2a0d8a599cf84cd6530bdbb24951156510d2cf3f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-special-considerations-for-instances"></a>Azure AD Connect: Özel konular örnekleri
Azure AD Connect Merhaba Dünya çapında Azure AD örneğinizle en yaygın olarak kullanılan ve Office 365. Ancak aynı zamanda diğer örneği vardır ve bu URL'leri ve diğer özel durumlar için farklı gereksinimlere sahip.

## <a name="microsoft-cloud-germany"></a>Microsoft Bulut Almanya
Merhaba [Microsoft Cloud Almanya](http://www.microsoft.de/cloud-deutschland) Almanca veri güvenliği tarafından işletilen bir sovereign bulut.

| Proxy sunucu olarak URL'leri tooopen |
| --- |
| \*. microsoftonline.de |
| \*.windows.net |
| + Sertifika iptal listeleri |

Tooyour Azure AD kiracısı'nda oturum açtığınızda hello onmicrosoft.de etki alanındaki bir hesabı kullanmanız gerekir.

Özellikleri hello Microsoft Cloud Almanya şu anda yok:

* **Azure AD Connect Health** kullanılabilir değil.
* **Otomatik Güncelleştirmeler** kullanılabilir değil.
* **Parola geri yazma** 1.1.570.0 Azure AD Connect sürümüyle ve sonra Önizleme için kullanılabilir.
* Diğer Azure AD Premium hizmetlerine kullanılabilir değil.

## <a name="microsoft-azure-government-cloud"></a>Microsoft Azure kamu bulut
Merhaba [Microsoft Azure kamu bulut](https://azure.microsoft.com/features/gov/) ABD devlet kurumları için bir bulut.

Bu bulut DirSync önceki sürümleri tarafından desteklenen. Yapıdan Azure AD Connect 1.1.180, yeni nesil hello bulut hello desteklenir. Bu oluşturma yalnızca ABD tabanlı uç noktalarını kullanarak ve proxy sunucunuzun URL'leri tooopen farklı bir listesi vardır.

| Proxy sunucu olarak URL'leri tooopen |
| --- |
| \*.microsoftonline.com |
| \*. microsoftonline.us |
| \*. gov.us.microsoftonline.com |
| + Sertifika iptal listeleri |

Azure AD Connect mümkün değil tooautomatically algılamak Azure AD kiracınıza hello Bulutu bulunur. Bunun yerine, Azure AD Connect yüklediğinizde eylemleri aşağıdaki tootake hello gerekir.

1. Hello Azure AD Connect yüklemesi başlatın.
2. Burada tooaccept hello EULA beklenen hello ilk sayfasını gördüğünüzde devam eder ancak hello Yükleme Sihirbazı'nı çalıştıran bırakın.
3. Regedit başlatın ve hello kayıt defteri anahtarını değiştirin `HKLM\SOFTWARE\Microsoft\Azure AD Connect\AzureInstance` toohello değeri `2`.
4. Toohello Azure AD Connect Yükleme Sihirbazı'nı geri dönün, hello EULA kabul edin ve devam edin. Yükleme sırasında emin toouse hello olun **özel yapılandırma** yükleme yolu (ve hızlı yükleme). Ardından hello yükleme her zamanki gibi devam edin.

Özellikleri hello Microsoft Azure kamu bulutta şu anda yok:

* **Azure AD Connect Health** kullanılabilir değil.
* **Otomatik Güncelleştirmeler** kullanılabilir değil.
* **Parola geri yazma** 1.1.570.0 Azure AD Connect sürümüyle ve sonra Önizleme için kullanılabilir.
* Diğer Azure AD Premium hizmetlerine kullanılabilir değil.

## <a name="next-steps"></a>Sonraki adımlar
[Şirket içi kimliklerinizi Azure Active Directory ile tümleştirme](active-directory-aadconnect.md) hakkında daha fazla bilgi edinin.
