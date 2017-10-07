---
title: "aaaCloud Proxy Hizmetleri için uygulama bulma kayıt defteri ayarları | Microsoft Docs"
description: "Merhaba amacı, bu konuda, hello sizinle adımları tooprovide tooperform tooset hello gerekli bağlantı noktası hello Cloud App Discovery Aracısı çalıştıran hello bilgisayarlarda gerekir ' dir."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 8d78e925-e331-40ba-904a-e4ef14260cac
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: bb1fe20016459160b4f67cb0125b1781a0260c4b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="cloud-app-discovery-registry-settings-for-proxy-services"></a>Proxy Hizmetleri için cloud App Discovery kayıt defteri ayarları
Varsayılan olarak, hello Cloud App Discovery Aracısı yapılandırılmış toouse yalnızca başlangıç bağlantı noktası 80 veya 443 ' dir. Cloud App Discovery, özel bir bağlantı noktası (80 ne 443) kullanarak bir proxy sunucusu olan bir ortamda yüklemeyi planlıyorsanız, aracıları toouse tooconfigure gereken Bu bağlantı noktası. Merhaba yapılandırma, bir kayıt defteri anahtarı temel alır.

Merhaba amacı, bu konuda, hello sizinle adımları tooprovide tooperform tooset hello gerekli bağlantı noktası hello Cloud App Discovery Aracısı çalıştıran hello bilgisayarlarda gerekir ' dir.

**Merhaba Cloud App Discovery Aracısı çalıştıran hello bilgisayar tarafından kullanılan toomodify hello bağlantı hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba Kayıt Defteri Düzenleyicisi'ni başlatın. <br> ![Çalıştırın](./media/active-directory-cloudappdiscovery-registry-settings-for-proxy-services/proxy01.png)
2. Gezinme tooor hello aşağıdaki kayıt defteri anahtarı oluşturun: <br> **HKLM_LOCAL_MACHINE\Software\Microsoft\Cloud uygulama Discovery\Endpoint** 
3. Yeni bir **çok dizeli** adlı değeri **bağlantı noktalarını**. ![Yeni](./media/active-directory-cloudappdiscovery-registry-settings-for-proxy-services/proxy02.png)
4. tooopen hello **Çoklu Dize Düzenle** iletişim kutusunda, başlangıç bağlantı noktası değeri çift tıklatın.
5. Merhaba değer veri metin kutusuna, değerleri aşağıdaki hello yazın ve kuruluşunuz tarafından kullanılan tüm özel bağlantı noktalarını ekleyin: <br><br>
   **80** <br>
   **8080** <br>
   **8118** <br>
   **8888** <br>
   **81** <br>
   **12080** <br>
   **6999** <br>
   **30606** <br>
   **31595** <br>
   **4080** <br>
   **443** <br>
   **1110** <br><br>
   ![Çoklu Dize Düzenle](./media/active-directory-cloudappdiscovery-registry-settings-for-proxy-services/proxy03.png)
6. Tıklatın **Tamam** tooclose hello **Çoklu Dize Düzenle** iletişim.

**Ek Kaynaklar**

* [Nasıl ı Kuruluşum içinde kullanılan onaylanmamış bulut uygulamaları bulabilir](active-directory-cloudappdiscovery-whatis.md) 

