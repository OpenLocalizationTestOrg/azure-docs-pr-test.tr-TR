---
title: "aaaConfigure (GoDaddy) Azure App Service'te özel etki alanı adı"
description: "Nasıl toouse bir etki alanı adını Azure Web uygulamalarıyla GoDaddy gelen öğrenin"
services: app-service
documentationcenter: 
author: erikre
manager: erikre
editor: jimbe
ms.assetid: 33233e30-5846-488f-83f3-b32e5c114564
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/12/2016
ms.author: cephalin
ms.openlocfilehash: 48158ee752f9833249bbf85adf80f572d1c68486
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-custom-domain-name-in-azure-app-service-purchased-directly-from-godaddy"></a>Azure App Service’te özel etki alanı adı yapılandırma (GoDaddy’den doğrudan satın alınan)
[!INCLUDE [web-selector](../../includes/websites-custom-domain-selector.md)]

[!INCLUDE [intro](../../includes/custom-dns-web-site-intro.md)]

Azure App Service Web Apps aracılığıyla etki alanı satın aldıktan sonra toohello son adımı başvuran [Web uygulamaları için etki alanı satın](custom-dns-web-site-buydomains-web-app.md).

Bu makalede doğrudan satın alınmış bir özel etki alanı adını kullanarak yönergeler sağlar. [GoDaddy](https://godaddy.com) ile [App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).

[!INCLUDE [introfooter](../../includes/custom-dns-web-site-intro-notes.md)]

<a name="understanding-records"></a>

## <a name="understanding-dns-records"></a>DNS kayıtlarını anlama
[!INCLUDE [understandingdns](../../includes/custom-dns-web-site-understanding-dns-raw.md)]

<a name="bkmk_configurecname"></a>

## <a name="add-a-dns-record-for-your-custom-domain"></a>Özel etki alanınız için DNS kaydı ekleyin
tooassociate App Service'te bir web uygulaması ile özel etki alanınızı, yeni bir giriş hello DNS tabloda özel etki alanınız için GoDaddy tarafından sağlanan araçları kullanarak eklemeniz gerekir. GoDaddy.com için adımları toolocate hello DNS araçları aşağıdaki hello kullanın

1. GoDaddy.com tooyour hesabıyla oturum ve seçin **hesabım** ve ardından **my etki alanlarını yönetme**. Azure web uygulaması ile toouse istiyor ve seçin hello etki alanı adı için Select hello açılır menü **yönetmek DNS**.
   
    ![GoDaddy için özel etki alanı sayfası](./media/web-sites-godaddy-custom-domain-name/godaddy-customdomain.png)
2. Merhaba gelen **etki alanı ayrıntıları** sayfasında, toohello kaydırma **DNS bölge dosyasına** sekmesi. Bu ekleme ve etki alanı adınız için DNS kayıtlarını değiştirme için kullanılan hello bölümüdür.
   
    ![DNS bölge dosyasına sekmesi](./media/web-sites-godaddy-custom-domain-name/godaddy-zonetab.png)
   
    Seçin **ekleme kaydı** tooadd varolan bir kaydı.
   
    çok**Düzenle** varolan kaydı, hello kaydın yanındaki select hello Kalem & kağıt simgesi.
   
   > [!NOTE]
   > Yeni kayıtlar eklemeden önce GoDaddy popüler alt etki alanları için DNS kayıtlarını zaten oluşturmuş olduğunu unutmayın (adlı **konak** düzenleyicisinde) gibi **e-posta**, **dosyaları**, **posta**ve diğerleri. Toouse zaten istediğiniz hello adı zaten varsa, yeni bir tane oluşturmak yerine varolan kaydına hello değiştirin.
   > 
   > 
3. Bir kayıt eklerken hello kayıt türü seçmeniz gerekir.
   
    ![Kayıt türü seçin](./media/web-sites-godaddy-custom-domain-name/godaddy-selectrecordtype.png)
   
    Ardından, hello sağlamalısınız **konak** (özel veya alt etki alanı hello) ve BT'nin **işaret**.
   
    ![Bölge kaydı ekleme](./media/web-sites-godaddy-custom-domain-name/godaddy-addzonerecord.png)
   
   * Eklerken bir **(ana) kaydı** -hello ayarlamalısınız **konak** alan tooeither  **@**  (Bu, kök etki alanı adı gibi temsil eder  **contoso.com**,) * (birden çok alt etki alanlarını eşleştirmek için joker karakter) veya toouse istediğiniz hello alt etki alanı (örneğin, **www**.) Merhaba ayarlamalısınız **işaret** alan toohello IP adresi, Azure web uygulamanızın.
   * Eklerken bir **CNAME kaydını (diğer ad)** -hello ayarlamalısınız **konak** toouse istediğiniz alan toohello alt etki alanı. Örneğin, **www**. Merhaba ayarlamalısınız **işaret** alan toohello **. azurewebsites.net** Azure web uygulamanızın etki alanı adı. Örneğin, **contoso.azurewebsites.net**.
4. Tıklatın **başka bir tane eklemek**.
5. Seçin **TXT** hello kayıt türü olarak ardından belirtin bir **konak** değerini  **@**  ve **işaret** değerini  **&lt;yourwebappname&gt;. azurewebsites.net**.
   
   > [!NOTE]
   > Bu TXT kaydı hello etki alanı kaydı veya hello ilk TXT kaydı hello tarafından açıklanan kendi Azure toovalidate tarafından kullanılır. Merhaba etki alanı hello Azure Portal web uygulamasında eşlenen toohello silindikten sonra bu TXT kayıt girişi kaldırılabilir.
   > 
   > 
6. Ne zaman ekleme tamamlandı veya kayıtları değiştirme tıklatın **son** toosave değişiklikler.

<a name="enabledomain"></a>

## <a name="enable-hello-domain-name-on-your-web-app"></a>Web uygulamanızdan Hello etki alanı adını etkinleştir
[!INCLUDE [modes](../../includes/custom-dns-web-site-enable-on-web-site.md)]

> [!NOTE]
> Azure hesabı için kaydolmadan önce Azure App Service ile başlatılan tooget istiyorsanız, çok Git[App Service'i deneyin](https://azure.microsoft.com/try/app-service/), burada hemen bir kısa süreli başlangıç web uygulaması App Service'te oluşturabilirsiniz. Kredi kartı ve taahhüt gerekmez.
> 
> 

## <a name="whats-changed"></a>Yapılan değişiklikler
* Web siteleri tooApp hizmet değişikliği Kılavuzu toohello için bkz: [Azure App Service ve mevcut Azure hizmetlerine etkileri](http://go.microsoft.com/fwlink/?LinkId=529714)

