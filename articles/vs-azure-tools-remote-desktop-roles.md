---
title: "aaaUsing Azure rolleriyle, Uzak Masaüstü'nü | Microsoft Docs"
description: "Azure rolleri ile Uzak Masaüstü'nü kullanma"
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: f5727ebe-9f57-4d7d-aff1-58761e8de8c1
ms.service: multiple
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/11/2016
ms.author: kraigb
ms.openlocfilehash: d35fd421cde8be9e3caa474db95974a54e528bae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="using-remote-desktop-with-azure-roles"></a>Azure rolleri ile Uzak Masaüstü'nü kullanma
Uzak Masaüstü Hizmetleri ve Hello Azure SDK kullanarak Azure rolleri ve Azure tarafından barındırılan sanal makinelerin erişebilir. Visual Studio'da bir Azure bulut hizmeti projesi Uzak Masaüstü Hizmetleri yapılandırabilirsiniz. tooenable Uzak Masaüstü Hizmetleri, bir veya daha fazla rolü içeren bir çalışma projesi oluşturun ve sonra tooAzure yayımlayın.

> [!IMPORTANT]
> Sorun giderme veya yalnızca geliştirme için Azure bir rolü erişim. Merhaba amacı, her bir sanal makinenin diğer istemci uygulamaları toorun Azure uygulamanız, değil toorun belirli bir rolde değil. Toouse Azure toohost herhangi bir amaçla kullanabileceğiniz bir sanal makine istiyorsanız, Azure sanal makineleri Sunucu Gezgini'nden erişme bakın.
> 
> 

## <a name="tooenable-and-use-remote-desktop-for-an-azure-role"></a>tooenable ve bir Azure rol için Uzak Masaüstü'nü kullanma
1. Çözüm Gezgini'nde, bulut hizmeti projenizi başlangıç kısayol menüsünü açın ve ardından **Yayımla**.
   
    Merhaba **Azure uygulamasını Yayımla** Sihirbazı görünür.
   
    ![Komutu için bir bulut hizmeti projesini Yayımla](./media/vs-azure-tools-remote-desktop-roles/IC799161.png)
2. Merhaba altındaki **Microsoft Azure yayımlama ayarları** hello sihirbazının select hello **Uzak Masaüstü'nü etkinleştirme** tüm rolleri onay kutusu. 
   
    Merhaba **uzak masaüstü yapılandırması** iletişim kutusu görüntülenir.
3. Merhaba hello sonundaki **uzak masaüstü yapılandırması** iletişim kutusunda, hello seçin **diğer seçenekler** düğmesi. 
   
    Bu oluşturmak veya Uzak Masaüstü aracılığıyla bağlanırken kimlik bilgilerini şifrelemek için bir sertifika seçin imkan tanıyan bir açılır liste kutusu görüntüler.
4. Merhaba aşağı açılan listesinde seçin  **&lt;Oluştur >**, veya mevcut bir hello listeden seçin. 
   
    Varolan bir sertifikayı seçerseniz, aşağıdaki adımları hello atlayın.
   
   > [!NOTE]
   > bir Uzak Masaüstü bağlantısı için gereksinim duyduğunuz hello sertifikalar, diğer Azure işlemleri için kullandığınız hello sertifikaları farklıdır. Merhaba uzaktan erişim sertifikasının özel anahtarı olması gerekir.
   > 
   > 
   
    Merhaba **oluşturduğunuz sertifika** iletişim kutusu görüntülenir.
   
   1. Merhaba yeni sertifika için kolay bir ad sağlayın ve ardından hello **Tamam** düğmesi. Merhaba yeni sertifika hello açılır liste kutusunda görüntülenir.
   2. Merhaba, **uzak masaüstü yapılandırması** iletişim kutusunda, bir kullanıcı adı ve parola sağlayın.
      
       Var olan bir hesap kullanamazsınız. Yönetici hello hello yeni hesap için kullanıcı adı olarak belirtmeyin.
      
      > [!NOTE]
      > Merhaba parola hello karmaşıklık gereksinimlerini karşılamıyorsa, kırmızı bir simge sonraki toohello parola metin kutusu görünür. Merhaba parola büyük harf, küçük harfler ve sayılar veya simgeler içermelidir.
      > 
      > 
   3. Hangi hello hesabın süresi dolacak ve hangi Uzak Masaüstü bağlantıları engellenir sonra bir tarihi seçin.
   4. Tüm gerekli bilgileri hello sağlanan seçtiğiniz sonra hello seçin **Tamam** düğmesi.
      
       Uzaktan erişim hizmetleri sağlayan birkaç ayarları toohello .cscfg ve .csdef dosyaları eklenir.
5. Merhaba, **Microsoft Azure yayımlama ayarları** Sihirbazı'nı hello seçin **Tamam** düğmesini gönderirken, bulut hizmetinizin toopublish hazır.
   
    Hazır toopublish değilseniz hello seçin **iptal** düğmesi. Merhaba yapılandırma ayarları kaydedilir ve daha sonra bulut hizmetinizi yayımlayın.

## <a name="connect-tooan-azure-role-by-using-remote-desktop"></a>Uzak Masaüstü'nü kullanarak tooan Azure rol Bağlan
Bulut hizmetinizde Azure yayımladıktan sonra Azure barındıran hello sanal makinelerine Sunucu Gezgini toolog kullanabilirsiniz. 

1. Sunucu Gezgini'nde hello genişletin **Azure** düğümü, bir bulut hizmeti ve kendi rolleri toodisplay örneklerinin bir listesini biri için hello düğümünü genişletin.
2. Bir örnek düğümü için hello kısayol menüsünü açın ve ardından **Uzak Masaüstü kullanarak bağlanmak**.
   
    ![Uzak Masaüstü aracılığıyla bağlanma](./media/vs-azure-tools-remote-desktop-roles/IC799162.png)
3. Merhaba kullanıcı adı ve daha önce oluşturduğunuz parolayı girin. Şimdi uzak oturumunuza günlüğe kaydedilir.

