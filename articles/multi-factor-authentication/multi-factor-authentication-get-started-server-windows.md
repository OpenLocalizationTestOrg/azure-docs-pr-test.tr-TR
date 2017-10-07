---
title: "aaaWindows kimlik doğrulaması ve Azure MFA sunucusu | Microsoft Docs"
description: "Bu, Windows kimlik doğrulaması ve Azure multi-Factor Authentication Sunucusu'nu dağıtmada yardımcı olacak hello Azure multi-Factor authentication sayfasıdır."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 19a4043f-c4ce-43c0-80e7-2548ee92cb74
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/06/2017
ms.author: kgremban
ms.reviewer: yossib
ms.custom: it-pro
ms.openlocfilehash: 0fc38fd751966bf883d4eae7c48055988922af80
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="windows-authentication-and-azure-multi-factor-authentication-server"></a>Windows Kimlik Doğrulaması ve Azure Multi-Factor Authentication Sunucusu
Merhaba Windows kimlik doğrulaması hello Azure çok faktörlü kimlik doğrulama sunucusu tooenable bölümünü kullanın ve uygulamaları için Windows kimlik doğrulamasını yapılandırın. Windows kimlik doğrulamasını ayarlamadan önce göz önünde listesinde aşağıdaki hello tutun:

* Kurulum sonrasında, Terminal Hizmetleri tootake etkisi için Azure multi-Factor Authentication hello yeniden başlatın.
* ' Azure multi-Factor Authentication kullanıcılarının eşleşmesini gerektir' seçeneği işaretliyse ve hello kullanıcı listesinde olmayan, yeniden başlatmanın ardından hello makine içine mümkün toolog olmaz.
* IP'leri hello uygulama hello istemci IP hello kimlik doğrulamasına sahip olup olmadığını sağlayabilir bağlı olduğu güvenilen. Şu anda yalnızca Terminal Hizmetleri desteklenmektedir.  

> [!NOTE]
> Bu özellik Windows Server 2012 R2'de desteklenen toosecure Terminal Hizmetleri'ni değil.

## <a name="toosecure-an-application-with-windows-authentication-use-hello-following-procedure"></a>Windows kimlik doğrulaması, aşağıdaki yordamı kullanın hello uygulamayla toosecure.
1. Hello Azure çok faktörlü kimlik doğrulama sunucusu hello Windows kimlik doğrulaması simgesine tıklayın.
   ![Windows Kimlik Doğrulaması](./media/multi-factor-authentication-get-started-server-windows/windowsauth.png)
2. Merhaba denetleyin **Windows kimlik doğrulamasını etkinleştir** onay kutusu. Varsayılan olarak, bu kutu işaretlenmemiştir.
3. Merhaba uygulamalar sekmesini hello yönetici tooconfigure bir veya daha fazla uygulamayı Windows kimlik doğrulaması sağlar.
4. Bir sunucu veya uygulama seçin – hello sunucusunun/uygulamanın etkinleştirilip etkinleştirilmeyeceğini belirtin. **Tamam** düğmesine tıklayın.
5. **Ekle...** düğmesine tıklayın.
6. Merhaba güvenilen IP'ler sekmesi belirli ıp'lerden gelen tooskip Azure çok faktörlü kimlik doğrulaması Windows oturumları için sağlar. Örneğin, çalışanlar hello ofisten ve evden hello uygulama kullanıyorsa, hello ofisteki Azure multi-Factor Authentication için telefonlarının çalmasını istemediğiniz karar verebilirsiniz. Bunun için güvenilen IP'ler girişi olarak hello ofis alt belirtirsiniz.
7. **Ekle...** düğmesine tıklayın.
8. Seçin **tek bir IP** tooskip tek bir IP adresi istiyorsanız.
9. Seçin **IP aralığı** tooskip tüm IP aralığını istiyorsanız. Örnek: 10.63.193.1-10.63.193.100.
10. Seçin **alt** bir alt ağ gösterimini kullanarak IP aralığı toospecify istiyorsanız. Merhaba alt ağın başlangıç IP'sini girin ve hello hello aşağı açılan listeden uygun ağ maskesini seçin.
11. **Tamam** düğmesine tıklayın.

## <a name="next-steps"></a>Sonraki adımlar

- [Azure MFA Sunucusu için üçüncü taraf VPN cihazları yapılandırma](multi-factor-authentication-advanced-vpn-configurations.md)

- [Varolan kimlik altyapınızı hello NPS uzantısı ile Azure MFA için büyütmek](multi-factor-authentication-nps-extension.md)
