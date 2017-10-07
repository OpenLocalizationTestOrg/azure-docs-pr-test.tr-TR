---
title: "iki aşamalı doğrulama Azure MFA hakkında aaaLearn | Microsoft Docs"
description: "Azure multi-Factor Authentication nedir, neden MFA, hello çok faktörlü kimlik doğrulama istemcisi ve hello farklı yöntemler ve kullanılabilir sürümleri hakkında daha fazla bilgi kullanın. "
keywords: "mfa nedir giriş tooMFA, mfa genel bakış"
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: c40d7a34-1274-4496-96b0-784850c06e9b
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/03/2017
ms.author: kgremban
ms.openlocfilehash: a91b8d6941d2b6ce72a789a97c57e10e594e7ada
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-azure-multi-factor-authentication"></a>Azure Multi-Factor Authentication nedir?
İki aşamalı doğrulama, birden fazla doğrulama yöntemi gerektiren ve güvenlik toouser oturum açmalarına ve işlemlerine önemli bir ikinci katmanı ekleyen kimlik doğrulama yöntemidir. Her iki veya daha fazla doğrulama yöntemlerini aşağıdaki hello isteyerek çalışır:

* (Genellikle parola) bildiğiniz bir şey
* (Kolayca, bir telefon gibi yineleniyor değil güvenilir bir cihaz) sahip olduğunuz şey
* (Biyometri) olan bir şey

<center>![Kullanıcı adı ve parola](./media/multi-factor-authentication/pword.png) &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ![sertifikaları](./media/multi-factor-authentication/phone.png) &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ![Akıllı Telefon](./media/multi-factor-authentication/hware.png) &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ![akıllı kart](./media/multi-factor-authentication/smart.png) &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ![sanal akıllı kart](./media/multi-factor-authentication/vsmart.png) &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ![kullanıcı adı ve parola](./media/multi-factor-authentication/cert.png)</center>

Azure Multi-Factor Authentication (MFA) Microsoft'un iki adımlı doğrulama çözümüdür. Azure MFA kullanıcı talebine basit bir oturum açma işlemi için buluştururken koruma erişim toodata ve uygulamaları yardımcı olur. Bir dizi doğrulama yöntemi (ör. telefon çağrısı, metin mesajı veya mobil uygulama doğrulaması) aracılığıyla güçlü kimlik doğrulaması sunar.

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/WA-MFA-Overview/player]
>
>

## <a name="why-use-azure-multi-factor-authentication"></a>Azure multi-Factor Authentication neden kullanılır?
Bugün, birden çok, kişilerin giderek bağlanır. Akıllı telefonlar, tabletler, dizüstü bilgisayarlar ve Bilgisayarları ile kişilerin nasıl tooconnect giderek ve herhangi bir zamanda bağlı kalın üzerinde birkaç farklı seçeneğiniz vardır. Kişiler kendi hesaplarının ve uygulamaların yerden, onların kullanıcılarınızın daha fazla işi halletmesine ve böylelikle müşterilerine hizmet anlamına gelir daha iyi erişebilir.

Azure çok faktörlü kimlik doğrulaması, ölçeklenebilir, kolay bir toouse ve kullanıcılarınızın her zaman korunması için güvenilir çözümü, ikinci bir kimlik doğrulama yöntemi sağlar.

| ![Kolay tooUse](./media/multi-factor-authentication/simple.png) | ![Ölçeklenebilir](./media/multi-factor-authentication/scalable.png) | ![Her zaman korunması](./media/multi-factor-authentication/protected.png) | ![Güvenilir](./media/multi-factor-authentication/reliable.png) |
|:---:|:---:|:---:|:---:|
| **Kolay toouse** |**Ölçeklenebilir** |**Her zaman korunması** |**Güvenilir** |

* **Kolay tooUse** -Azure çok faktörlü kimlik doğrulaması, basit tooset yukarı ve kullanın. Hello Azure multi-Factor Authentication ile birlikte gelen fazladan koruma kullanıcılar toomanage kendi cihazlarını sağlar. Birçok durumlarda tüm en iyi, yalnızca birkaç basit tıklama ile ayarlanabilir.
* **Ölçeklenebilir** -Azure multi-Factor Authentication hello bulut hello gücünü kullanır ve şirket içi ile tümleşir AD ve özel uygulamalar. Bu koruma bile tooyour yüksek hacimli, kritik senaryolar genişletilir.
* **Her zaman korumalı** -Azure multi-Factor Authentication hello yüksek endüstri standartları kullanarak güçlü kimlik doğrulaması sağlar.
* **Güvenilir** -Azure çok faktörlü kimlik doğrulaması % 99,9 kullanılabilirliğini garanti ediyoruz. erişemediği zaman hello hizmeti kullanılamaz olarak kabul edilir hello iki aşamalı doğrulamayı tooreceive veya işlem doğrulama istekleri.

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Windows-Azure-Multi-Factor-Authentication/player]


## <a name="next-steps"></a>Sonraki adımlar

- Hakkında bilgi edinin [Azure multi-Factor Authentication nasıl çalışır](multi-factor-authentication-how-it-works.md)

- Merhaba farklı hakkında okuyun [sürümleri ve Azure çok faktörlü kimlik doğrulaması için tüketim yöntemi](multi-factor-authentication-versions-plans.md)
