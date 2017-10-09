---
title: Mobile Engagement REST API'leri - el ile kuruluma ile aaaAuthenticate
description: "Nasıl toomanually Kurulum kimlik doğrulaması için Mobile Engagement REST API'leri"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 2e79f9c9-41e4-45ac-b427-3b8338675163
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 3884f94afcd6b9a62bfcf498fb6ee84bb6e837b7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="authenticate-with-mobile-engagement-rest-apis---manual-setup"></a>Mobile Engagement REST API'leri ile - el ile kuruluma kimlik doğrulaması
Bu bir ek çok belgesidir[Mobile Engagement REST API'leri ile kimlik doğrulama](mobile-engagement-api-authentication.md). İlk tooget hello bağlam okuma emin olun. Merhaba Mobile Engagement REST API'lerini kullanarak hello için Azure Portal Bu, kimlik doğrulama kurma bir alternatif bir yol toodo hello kerelik Kurulum açıklar. 

> [!NOTE]
> Merhaba yönergelerde bu dayalı [Active Directory Kılavuzu](../azure-resource-manager/resource-group-create-service-principal-portal.md) ve Mobile Engagement API'leri için kimlik doğrulaması için gerekli olan için özelleştirilebilir. Ayrıntılı toounderstand hello adımları istiyorsanız, bu nedenle tooit bakın. 
> 
> 

1. Merhaba aracılığıyla Azure hesabı oturum açma tooyour [Klasik portal](https://manage.windowsazure.com/).
2. Seçin **Active Directory** hello sol bölmesinden.
   
     ![Active Directory'yi seçin][1]
3. Merhaba seçin **varsayılan Active Directory** , Azure portalında. 
   
     ![dizin seçin][2]
   
   > [!IMPORTANT]
   > Bu yaklaşım, yalnızca hello varsayılan Active Directory hesabınızın çalışıyorsanız ve hesabınızı oluşturduğunuz bir Active Directory bu yapıyorlarsa, işe yaramaz olduğunda çalışır. 
   > 
   > 
4. dizininizde, tooview hello uygulamaları tıklayın **uygulamaları**.
   
     ![uygulamaları görüntüle][3]
5. Tıklayın **eklemek**. 
   
     ![Uygulama ekleme][4]
6. Tıklayın **kuruluşumun geliştirmekte olduğu bir uygulama Ekle**
   
     ![Yeni uygulama][5]
7. Merhaba uygulama ve uygulamanın olarak select hello türü adını doldurun **WEB uygulaması ve/veya WEB API** ve hello İleri düğmesine tıklayın.
   
     ![Uygulama adı][6]
8. Herhangi bir kukla URL için sağladığınız **oturum açma URL** ve **uygulama kimliği URI'si**. Senaryomuz için kullanılmaz ve hello URL'leri kendilerini doğrulanmamış.  
   
     ![Uygulama özellikleri][7]
9. Bu Hello sonunda hello aşağıdaki gibi daha önce sağlanan hello adı bir AAD uygulaması gerekir. Bu, **AD\_uygulama\_adı** ve onu not edin.  
   
     ![Uygulama adı][8]
10. Merhaba uygulama adına tıklayın ve tıklayın **yapılandırma**.
    
      ![uygulamayı yapılandırma][9]
11. Hello olarak kullanılacak bir istemci kimliği Not **istemci\_kimliği** API'nize çağırır. 
    
     ![uygulamayı yapılandırma][10]
12. Toohello aşağı **anahtarları** bölüm ve tercihen 2 yıl (Bitiş) süresi ile bir anahtar ekleyin ve tıklatın **kaydetmek**. 
    
     ![uygulamayı yapılandırma][11]
13. Hemen herhangi bir zamanda yeniden görüntülenmeyecek depolanır, böylece değildir ve yalnızca şimdi gösterilen gibi hello anahtarı gösterilen hello değeri kopyalayın. Ardından, kaybetmeniz durumunda toogenerate yeni bir anahtar gerekir. Bu hello olacaktır **CLIENT_SECRET** API'nize çağırır. 
    
     ![uygulamayı yapılandırma][12]
    
    > [!IMPORTANT]
    > Bu anahtar, başlangıç zamanı Aksi takdirde, API kimlik geldiğinde artık çalışmaz, bunu yap emin toorenew belirtilen hello hello süre sonunda süresi dolar. Ayrıca silin ve tehlikeye düşünüyorsanız, bu anahtarı oluşturun.
    > 
    > 
14. Tıklayın **uç noktalarını GÖRÜNTÜLE** düğmesini şimdi hello açılacağı **uygulama uç noktaları** iletişim kutusu. 
    
    ![][13]
15. Merhaba Hello uygulama uç noktaları iletişim kutusundan kopyalama **OAUTH 2.0 BELİRTEÇ uç noktası**. 
    
    ![][14]
16. Bu uç noktaya hello hello URL'de GUID olduğu form aşağıdaki hello olacaktır, **TENANT_ID** bu nedenle, not edin: 
    
        https://login.microsoftonline.com/<GUID>/oauth2/token
17. Şimdi biz tooconfigure hello bu uygulama izinlerini devam edin. Bu tooopen hello yukarı olacaktır [Azure portal](https://portal.azure.com). 
18. Tıklayın **kaynak grupları** ve hello bulur **Mobile Engagement** kaynak grubu.  
    
    ![][15]
19. Hello tıklatın **Mobile Engagement** kaynak grubu ve toohello gidin **ayarları** dikey burada. 
    
    ![][16]
20. Tıklayın **kullanıcılar** ayarlar dikey penceresinde hello ve tıklayın **Ekle** tooadd bir kullanıcı. 
    
    ![][17]
21. Tıklayın **bir rol seçin**
    
    ![][18]
22. Tıklayın **sahibi**
    
    ![][19]
23. Uygulamanızın hello adını arayın **AD\_uygulama\_adı** hello arama kutusuna. Bunu burada varsayılan olarak görmez. Bulduğunuzda, onu seçin ve tıklayın **seçin** hello dikey penceresinde hello sonundaki. 
    
    ![][20]
24. Merhaba üzerinde **eklemek erişim** dikey penceresinde gösterilir olarak **1 kullanıcının, 0 gruplarını**. Tıklatın **Tamam** bu dikey tooconfirm hello değişir. 
    
    ![][21]

Gerekli hello AAD yapılandırmasını tamamladınız ve tüm kümesi toocall hello API'leri demektir. 

<!-- Images -->
[1]: ./media/mobile-engagement-api-authentication-manual/active-directory.png
[2]: ./media/mobile-engagement-api-authentication-manual/active-directory-details.png
[3]: ./media/mobile-engagement-api-authentication-manual/view-applications.png
[4]: ./media/mobile-engagement-api-authentication-manual/add-icon.png
[5]: ./media/mobile-engagement-api-authentication-manual/what-do-you-want-to-do.png
[6]: ./media/mobile-engagement-api-authentication-manual/tell-us-about-your-application.png
[7]: ./media/mobile-engagement-api-authentication-manual/app-properties.png
[8]: ./media/mobile-engagement-api-authentication-manual/aad-app.png
[9]: ./media/mobile-engagement-api-authentication-manual/configure-menu.png
[10]: ./media/mobile-engagement-api-authentication-manual/client-id.png
[11]: ./media/mobile-engagement-api-authentication-manual/client_secret.png
[12]: ./media/mobile-engagement-api-authentication-manual/keys.png
[13]: ./media/mobile-engagement-api-authentication-manual/view-endpoints.png
[14]: ./media/mobile-engagement-api-authentication-manual/app-endpoints.png
[15]: ./media/mobile-engagement-api-authentication-manual/resource-groups.png
[16]: ./media/mobile-engagement-api-authentication-manual/resource-groups-settings.png
[17]: ./media/mobile-engagement-api-authentication-manual/add-users.png
[18]: ./media/mobile-engagement-api-authentication-manual/add-role.png
[19]: ./media/mobile-engagement-api-authentication-manual/select-role.png
[20]: ./media/mobile-engagement-api-authentication-manual/add-user-select.png
[21]: ./media/mobile-engagement-api-authentication-manual/add-access-final.png



