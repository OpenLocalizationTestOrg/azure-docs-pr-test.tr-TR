---
title: "Uygulama Proxy Aracısı Bağlayıcısı hello aaaProblem yükleme | Microsoft Docs"
description: "Nasıl tootroubleshoot, yüklerken yüz uygulama Proxy Aracısı Bağlayıcısı hello sorunlar"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 07ac366a429083af0c9b87aa9df9cf3876132b90
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="problem-installing-hello-application-proxy-agent-connector"></a>Merhaba uygulama Proxy Aracısı Bağlayıcısı yükleme sorunu

Microsoft AAD Application Proxy Connector hello bulut kullanılabilir uç nokta toohello iç etki alanından giden bağlantılar tooestablish hello bağlantı kullanan bir iç etki alanının bileşendir.

## <a name="general-problem-areas-with-connector-installation"></a>Genel sorun alanlarından bağlayıcısını yükleme

Bir bağlayıcının Hello yüklemesi başarısız olduğunda hello kök nedeni genellikle alanları aşağıdaki hello biridir:

1.  **Bağlantı** – toocomplete başarılı bir yükleme yeni bağlayıcı gereksinimlerini tooregister hello ve gelecekteki güven özellikleri oluşturmaktır. Bu, toohello AAD uygulama proxy'si bulut hizmetine bağlanarak yapılır.

2.  **Güven oluşturma** – hello yeni bir bağlayıcı otomatik olarak imzalanan bir sertifika oluşturur ve toohello bulut hizmetine kaydeder.

3.  **Hello Yöneticisi kimlik doğrulaması** – yükleme sırasında hello kullanıcı yönetici kimlik bilgilerini toocomplete hello Bağlayıcısı yükleme sağlamanız gerekir.

## <a name="verify-connectivity-toohello-cloud-application-proxy-service-and-microsoft-login-page"></a>Bağlantı toohello bulut uygulama proxy'si hizmeti ve Microsoft Login sayfasına doğrulayın

**Hedef:** bu hello bağlayıcı makine toohello AAD uygulama proxy'si kayıt uç noktasını ve bunun yanı sıra Microsoft oturum açma sayfasına bağlanabilir doğrulayın.

1.  Web sayfası aşağıdaki tarayıcı ve Git toohello açın: <https://aadap-portcheck.connectorporttest.msappproxy.net> , o hello bağlantı tooCentral ABD doğrulayın ve bağlantı noktaları 9090 ve 9091 Doğu ABD veri merkezlerinde çalıştığından.

2.  Bu bağlantı noktalarının hiçbirinde yoksa başarılı (yeşil bir onay yok), o hello güvenlik duvarı doğrulamak veya arka uç proxy sahip \*. msappproxy.net 9090 ve doğru şekilde tanımlanan 9091 bağlantı noktasına sahip.

3.  Bir tarayıcı (ayrı sekmesi) açın ve web sayfasını aşağıdaki toohello: <https://login.microsoftonline.com>, toothat sayfasında oturum açabileceğiniz emin olun.

## <a name="verify-machine-and-backend-components-support-for-application-proxy-trust-cert"></a>Makine ve arka uç bileşenleri için uygulama proxy'si güven sertifikası desteklediğini doğrulayın

**Hedef:** hello bağlayıcı makine, arka uç proxy ve güvenlik duvarı gelecekteki güven hello Bağlayıcısı tarafından oluşturulan hello sertifika destekleyebilir doğrulayın.

>[!NOTE]
>Merhaba bağlayıcı toocreate TLS1.2 tarafından desteklenen bir SHA512 cert çalışır. Merhaba makine veya hello arka uç güvenlik duvarı ve proxy desteklemiyor TLS1.2 hello yükleme başarısız.
>
>

**tooresolve hello sorunu:**

1.  Merhaba makine TLS1.2 destekleyen – 2012 R2 sonra tüm Windows sürümlerinde TLS 1.2 desteklemelidir doğrulayın. Bağlayıcı makinenizi 2012 R2 sürümü ya da önceki ise, aşağıdaki KB hello makinede yüklü o hello emin olun: <https://support.microsoft.com/help/2973337/sha512-is-disabled-in-windows-when-you-use-tls-1.2>

2.  Ağ yöneticinize başvurun ve hello arka uç proxy ve güvenlik duvarı SHA512 giden trafiği için engellemez tooverify isteyin.

## <a name="verify-admin-is-used-tooinstall-hello-connector"></a>Kullanılan tooinstall hello Bağlayıcısı yönetici olduğunu doğrulayın

**Hedef:** tooinstall hello bağlayıcı çalıştığında bu hello kullanıcı doğru kimlik bilgilerine sahip bir yönetici olduğunu doğrulayın. Şu anda hello kullanıcının hello yükleme toosucceed için genel yönetici olması gerekir.

**tooverify hello kimlik bilgilerinin doğru olduğundan:**

Çok bağlanmak<https://login.microsoftonline.com> ve aynı kimlik bilgilerini hello kullanın. Merhaba oturum açma başarılı olduğundan emin olun. Çok giderek hello kullanıcı rolü denetleyebilirsiniz**Azure Active Directory**  - &gt; **kullanıcılar ve gruplar**  - &gt; **tüm kullanıcılar**. 

Kullanıcı hesabınız, ardından "dizin rolü" Merhaba ortaya çıkan menüde seçin. Bu hello seçili rol "Genel yönetici" olduğunu doğrulayın. Merhaba hiçbirini sayfaları adımları oluşturulamıyor tooaccess varsa, genel bir yönetici değilsiniz.

## <a name="next-steps"></a>Sonraki adımlar
[Azure AD uygulama proxy'si bağlayıcılar anlama](application-proxy-understand-connectors.md)
