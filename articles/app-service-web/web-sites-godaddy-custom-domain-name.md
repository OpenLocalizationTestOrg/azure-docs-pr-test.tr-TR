---
title: "Azure App Service (GoDaddy) bir özel etki alanı adı yapılandırma"
description: "GoDaddy etki alanı adından Azure Web uygulamaları ile kullanma hakkında bilgi edinin"
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
ms.openlocfilehash: 158c5dc06f83e16633d3c2fbb4eb27d3e8af030c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="configure-a-custom-domain-name-in-azure-app-service-purchased-directly-from-godaddy"></a>Azure App Service’te özel etki alanı adı yapılandırma (GoDaddy’den doğrudan satın alınan)
[!INCLUDE [web-selector](../../includes/websites-custom-domain-selector.md)]

[!INCLUDE [intro](../../includes/custom-dns-web-site-intro.md)]

Azure App Service Web Apps aracılığıyla etki alanı satın aldıktan sonra son adıma bakın [Web uygulamaları için etki alanı satın](custom-dns-web-site-buydomains-web-app.md).

Bu makalede doğrudan satın alınmış bir özel etki alanı adını kullanarak yönergeler sağlar. [GoDaddy](https://godaddy.com) ile [App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).

[!INCLUDE [introfooter](../../includes/custom-dns-web-site-intro-notes.md)]

<a name="understanding-records"></a>

## <a name="understanding-dns-records"></a>DNS kayıtlarını anlama
[!INCLUDE [understandingdns](../../includes/custom-dns-web-site-understanding-dns-raw.md)]

<a name="bkmk_configurecname"></a>

## <a name="add-a-dns-record-for-your-custom-domain"></a>Özel etki alanınız için DNS kaydı ekleyin
App Service'in web uygulamasında özel etki alanınızı ilişkilendirmek için yeni bir giriş DNS tabloda özel etki alanınız için GoDaddy tarafından sağlanan araçları kullanarak eklemeniz gerekir. DNS araçları için GoDaddy.com bulmak için aşağıdaki adımları kullanın

1. Hesabınıza GoDaddy.com ile oturum açın ve seçin **hesabım** ve ardından **my etki alanlarını yönetme**. Azure web uygulaması ile kullanın ve seçmek istediğiniz etki alanı adı açılan menüsünü **yönetmek DNS**.
   
    ![GoDaddy için özel etki alanı sayfası](./media/web-sites-godaddy-custom-domain-name/godaddy-customdomain.png)
2. Gelen **etki alanı ayrıntıları** sayfasında, kaydırarak **DNS bölge dosyasına** sekmesi. Bu, ekleme ve etki alanı adınız için DNS kayıtlarını değiştirme için kullanılan bölümüdür.
   
    ![DNS bölge dosyasına sekmesi](./media/web-sites-godaddy-custom-domain-name/godaddy-zonetab.png)
   
    Seçin **ekleme kaydı** varolan bir kayıt eklemek için.
   
    İçin **Düzenle** varolan bir kaydı kağıt kaydın yanındaki simge & Kalem seçin.
   
   > [!NOTE]
   > Yeni kayıtlar eklemeden önce GoDaddy popüler alt etki alanları için DNS kayıtlarını zaten oluşturmuş olduğunu unutmayın (adlı **konak** düzenleyicisinde) gibi **e-posta**, **dosyaları**, **posta**ve diğerleri. Zaten kullanmak istediğiniz adı zaten varsa, yeni bir tane oluşturmak yerine var olan kayıt değiştirin.
   > 
   > 
3. Bir kayıt eklerken, kayıt türünü seçmeniz gerekir.
   
    ![Kayıt türü seçin](./media/web-sites-godaddy-custom-domain-name/godaddy-selectrecordtype.png)
   
    Ardından, sağlamanız gereken **konak** (özel etki alanı veya alt etki alanı) ve neyin **işaret**.
   
    ![Bölge kaydı ekleme](./media/web-sites-godaddy-custom-domain-name/godaddy-addzonerecord.png)
   
   * Eklerken bir **(ana) kaydı** -ayarlamanız gerekir **konak** ya da alan  **@**  (Bu, kök etki alanı adı gibi temsil eden **contoso.com**,) * (birden çok alt etki alanlarını eşleştirmek için joker karakter) veya kullanmak istediğiniz alt etki alanı (örneğin, **www**.) Ayarlamalısınız **işaret** Azure web uygulamanızın IP adresi alanı.
   * Eklerken bir **CNAME kaydını (diğer ad)** -ayarlamalısınız **konak** kullanmak istediğiniz alt etki alanı. Örneğin, **www**. Ayarlamalısınız **işaret** alanı **. azurewebsites.net** Azure web uygulamanızın etki alanı adı. Örneğin, **contoso.azurewebsites.net**.
4. Tıklatın **başka bir tane eklemek**.
5. Seçin **TXT** kayıt türü olarak ardından belirtin bir **konak** değerini  **@**  ve **işaret** değerini  **&lt;yourwebappname&gt;. azurewebsites.net**.
   
   > [!NOTE]
   > Bu TXT kaydı, bir kayıt veya ilk TXT kaydı tarafından açıklanan etki alanına sahip olduğunuz doğrulamak için Azure tarafından kullanılır. Etki alanı Azure Portal'da web uygulamasına eşlenen sonra bu TXT kayıt girişi kaldırılabilir.
   > 
   > 
6. Ne zaman ekleme tamamlandı veya kayıtları değiştirme tıklatın **son** değişiklikler kaydedilemiyor.

<a name="enabledomain"></a>

## <a name="enable-the-domain-name-on-your-web-app"></a>Web uygulamanızdan etki alanı adını etkinleştir
[!INCLUDE [modes](../../includes/custom-dns-web-site-enable-on-web-site.md)]

> [!NOTE]
> Azure hesabı için kaydolmadan önce Azure App Service’i kullanmaya başlamak isterseniz, App Service’te hemen kısa süreli bir başlangıç web uygulaması oluşturabileceğiniz [App Service’i Deneyin](https://azure.microsoft.com/try/app-service/) sayfasına gidin. Kredi kartı ve taahhüt gerekmez.
> 
> 

## <a name="whats-changed"></a>Yapılan değişiklikler
* Web Sitelerinden App Service’e kadar değiştirme kılavuzu için bkz. [Azure App Service ve Mevcut Azure Hizmetlerine Etkileri](http://go.microsoft.com/fwlink/?LinkId=529714)

