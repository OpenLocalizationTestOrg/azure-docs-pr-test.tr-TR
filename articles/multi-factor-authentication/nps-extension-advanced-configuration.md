---
title: "aaaConfigure hello Azure MFA NPS uzantısı | Microsoft Docs"
description: "Merhaba NPS uzantısı yüklendikten sonra IP uygulamaları güvenilir listeye almayı ve UPN değiştirme gibi gelişmiş yapılandırma için aşağıdaki adımları kullanın."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/14/2017
ms.author: kgremban
ms.reviewer: yossib
ms.custom: it-pro
ms.openlocfilehash: c3aed077b23c95f874861eb00c8e6dca668329c1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="advanced-configuration-options-for-hello-nps-extension-for-multi-factor-authentication"></a>Gelişmiş çok faktörlü kimlik doğrulaması için hello NPS uzantısı için yapılandırma seçenekleri

Merhaba ağ ilkesi sunucusu (NPS) uzantısı, şirket içi altyapınızı, bulut tabanlı Azure çok faktörlü kimlik doğrulama özelliklerini genişletir. Bu makale, zaten yüklü hello uzantısına sahiptir ve şimdi nasıl toocustomize hello uzantısı sizin için gereken tooknow istediğiniz varsayar. 

## <a name="alternate-login-id"></a>Alternatif oturum açma kimliği

Şirket içi ve bulut Hello NPS uzantısı tooboth bağlayan bu yana dizinleri, burada, şirket içi kullanıcı asıl adları (UPN'ler) eşleşmiyor hello adları hello bulutta bir sorun karşılaşabileceğiniz. toosolve Bu sorun, kullanım alternatif oturum açma kimliklerini. 

NPS uzantısı Hello içinde UPN hello yerine Azure çok faktörlü kimlik doğrulaması için kullanılan bir Active Directory öznitelik toobe belirleyebilirsiniz. Bu, tooprotect şirket içi kaynaklarınızı iki aşamalı doğrulama ile şirket içi UPN değiştirmeden sağlar. 

tooconfigure alternatif oturum açma kimlikleri, Git çok`HKLM\SOFTWARE\Microsoft\AzureMfa` ve kayıt defteri değerleri aşağıdaki hello düzenleyin:

| Ad | Tür | Varsayılan değer | Açıklama |
| ---- | ---- | ------------- | ----------- |
| LDAP_ALTERNATE_LOGINID_ATTRIBUTE | Dize | boş | Merhaba toouse hello UPN yerine istediğiniz Active Directory öznitelik adını belirtin. Bu öznitelik hello AlternateLoginId özniteliği olarak kullanılır. Bu kayıt defteri değerini tooa ayarlarsanız [geçerli Active Directory özniteliğini](https://msdn.microsoft.com/library/ms675090.aspx) (örneğin, posta ya da displayName için), ardından hello özniteliğinin değeri yerine hello kullanıcının UPN kimlik doğrulaması için kullanılır. Bu kayıt defteri değerini veya boşsa, yapılandırıldıktan sonra AlternateLoginId devre dışıdır ve hello kullanıcının UPN kimlik doğrulaması için kullanılır. |
| LDAP_FORCE_GLOBAL_CATALOG | Boole değeri | False | Bu bayrak tooforce hello genel katalog LDAP aramaları için AlternateLoginId bakarken kullanın. Bir etki alanı denetleyicisini bir genel katalog olarak yapılandırma hello AlternateLoginId özniteliği toohello genel katalog ekleyin ve ardından bu bayrağı etkinleştirin. <br><br> LDAP_LOOKUP_FORESTS (boş değilse), yapılandırılmışsa, **bu bayrağı true zorlanır**hello kayıt defteri ayarı hello değerinin ne olursa olsun. Bu durumda, her orman için hello AlternateLoginId özniteliği ile yapılandırılmış hello genel katalog toobe hello NPS uzantısı gerektirir. |
| LDAP_LOOKUP_FORESTS | Dize | boş | Ormanlar toosearch noktalı virgülle ayrılmış listesini sağlayın. Örneğin, *contoso.com;foobar.com*. Bu kayıt defteri değeri yapılandırdıysanız, hello NPS uzantısı tüm hello ormanlar, bunlar listelenen ve hello ilk başarılı AlternateLoginId değeri döndürür hello sırayla tekrarlayarak arar. Bu kayıt defteri değeri yapılandırılmamışsa, hello AlternateLoginId arama yalıtılmış toohello geçerli etki alanıdır.|

Alternatif oturum açma kimlikleri, tootroubleshoot sorunları kullanma adımları için önerilen hello [alternatif oturum açma kimliği hataları](multi-factor-authentication-nps-errors.md#alternate-login-id-errors).

## <a name="ip-exceptions"></a>IP özel durumlar

Yük Dengeleyici iş yükleri, göndermeden önce hangi sunucuların çalıştıran doğrulayın, gibi toomonitor sunucu kullanılabilirliği gerekiyorsa doğrulama isteklerini tarafından engellenen bu denetimleri toobe istemezsiniz. Bunun yerine, hizmet hesapları tarafından kullanılan bildiğiniz IP adresleri listesi oluşturun ve bu liste çok faktörlü kimlik doğrulama gereksinimleri devre dışı. 

bir IP beyaz listesi tooconfigure Git çok`HKLM\SOFTWARE\Microsoft\AzureMfa` ve aşağıdaki kayıt defteri değeri hello yapılandırın: 

| Ad | Tür | Varsayılan değer | Açıklama |
| ---- | ---- | ------------- | ----------- |
| IP_WHITELIST | Dize | boş | IP adreslerinin noktalı virgülle ayrılmış listesini sağlayın. Merhaba, NAS/VPN sunucusu hello gibi hizmet istekleri burada kaynaklanan makinelerin IP adreslerini içerir. IP aralıkları, alt ağlar desteklenmez:. <br><br> Örneğin, *10.0.0.1;10.0.0.2;10.0.0.3*.

Bir istek hello beyaz mevcut bir IP adresinden geldiğinde, iki aşamalı doğrulama atlandı. Merhaba IP beyaz listesi hello sağlanan karşılaştırılan toohello IP adresidir *ratNASIPAddress* hello RADIUS isteğini özniteliğidir. Bir RADIUS isteğini hello ratNASIPAddress özniteliği olmadan geliyorsa, uyarı aşağıdaki hello kaydedilir: "P_WHITE_LIST_WARNING::IP beyaz liste yoksayılır kaynak IP RADIUS isteğini NasIpAddress öznitelik yok."

## <a name="next-steps"></a>Sonraki adımlar

[Azure çok faktörlü kimlik doğrulamasını hello NPS uzantısı hata iletilerini çözümleyin](multi-factor-authentication-nps-errors.md)
