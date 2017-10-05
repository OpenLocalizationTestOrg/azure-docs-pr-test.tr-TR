---
title: "Azure AD raporlama API'si erişmek için Önkoşullar. | Microsoft Belgeleri"
description: "Azure AD raporlama API'si erişmek için önkoşullar hakkında bilgi edinin"
services: active-directory
documentationcenter: 
author: dhanyahk
manager: femila
editor: 
ms.assetid: ada19f69-665c-452a-8452-701029bf4252
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/16/2017
ms.author: dhanyahk;markvi
ms.openlocfilehash: 6e409fc56b77f37dac7f37382e664c577666ad4d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="prerequisites-to-access-the-azure-ad-reporting-api"></a>Azure AD raporlama API'si erişmek için Önkoşullar
[API'leri raporlama Azure AD](https://msdn.microsoft.com/library/azure/ad/graph/howto/azure-ad-reports-and-events-preview) verilere bir dizi REST tabanlı API'ler aracılığıyla programlı erişim sağlar. Çeşitli programlama dilleri ve araçlarından bu API'leri çağırabilirsiniz.

Raporlama API kullandığı [OAuth](https://msdn.microsoft.com/library/azure/dn645545.aspx) web API'leri erişim yetkisi vermek için. 

Raporlama API erişiminizi hazırlamak için şunları yapmanız gerekir:

1. Azure AD kiracınızda uygulama oluşturma 
2. Azure AD verilere erişmek için uygulama uygun izinleri verin
3. Yapılandırma ayarları dizininizden toplayın

Sorularınız, sorunları veya Geri bildiriminiz için lütfen başvurun [raporlama AAD Yardım](mailto:aadreportinghelp@microsoft.com).

## <a name="create-an-azure-ad-application"></a>Azure AD uygulaması oluştur
Azure AD raporlama API'si erişmek için dizininize yapılandırmak için Azure Klasik portalı, aynı zamanda Azure AD kiracınızda genel yönetici dizin rolünün bir üyesi olan bir Azure aboneliği yönetici hesabıyla oturum gerekir.

> [!IMPORTANT]
> Bu gibi "Yönetici" ayrıcalıkları olan kimlik bilgileri altında çalışan uygulamalar çok güçlü olabilir, bu nedenle Lütfen uygulamanın kimliği/parola kimlik bilgileri güvenli tutmak emin olun.
> 
> 

1. İçinde [Klasik Azure portalı](https://manage.windowsazure.com), sol gezinti bölmesinde tıklatın **Active Directory**.
   
    ![Uygulamayı Kaydet](./media/active-directory-reporting-api-prerequisites/01.png) 
2. Gelen **active directory** listesinde, dizininizi seçin.
3. Üstteki menüde tıklatın **uygulamaları**.
   
    ![Uygulamayı Kaydet](./media/active-directory-reporting-api-prerequisites/02.png) 
4. Alt çubuğunda **Ekle**.
   
    ![Uygulamayı Kaydet](./media/active-directory-reporting-api-prerequisites/03.png) 
5. Üzerinde **ne yapmak istiyorsunuz?** iletişim kutusunda, tıklatın **kuruluşumun geliştirmekte olduğu bir uygulama Ekle**. 
   
    ![Uygulamayı Kaydet](./media/active-directory-reporting-api-prerequisites/04.png) 
6. Üzerinde **bize uygulamanızı anlatın** iletişim kutusunda, aşağıdaki adımları gerçekleştirin: 
   
    ![Uygulamayı Kaydet](./media/active-directory-reporting-api-prerequisites/05.png) 
   
    a. İçinde **adı** metin kutusuna, bir ad yazın (örneğin: Reporting API uygulaması).
   
    b. Seçin **Web uygulaması ve/veya web API'si**.
   
    c. **İleri**’ye tıklayın.
7. Üzerinde **uygulama özellikleri** iletişim kutusunda, aşağıdaki adımları gerçekleştirin: 
   
    ![Uygulamayı Kaydet](./media/active-directory-reporting-api-prerequisites/06.png) 
   
    a. İçinde **oturum açma URL'si** metin kutusuna, türü `https://localhost`.
   
    b. İçinde **uygulama kimliği URI'si** metin kutusuna, türü ```https://localhost/ReportingApiApp```.
   
    c. **Tamamla**’ya tıklayın.

## <a name="grant-your-application-permission-to-use-the-api"></a>Uygulama API kullanma izni verin
1. İçinde [Klasik Azure portalı](https://manage.windowsazure.com/), sol gezinti bölmesinde tıklatın **Active Directory**.
   
    ![Uygulamayı Kaydet](./media/active-directory-reporting-api-prerequisites/01.png) 
2. Gelen **active directory** listesinde, dizininizi seçin.
3. Üstteki menüde tıklatın **uygulamaları**.
   
    ![Uygulamayı Kaydet](./media/active-directory-reporting-api-prerequisites/02.png)
4. Uygulamalar listesinde yeni oluşturulan uygulamanızı seçin.
   
    ![Uygulamayı Kaydet](./media/active-directory-reporting-api-prerequisites/07.png)
5. Üstteki menüde tıklatın **yapılandırma**.
   
    ![Uygulamayı Kaydet](./media/active-directory-reporting-api-prerequisites/08.png)
6. İçinde **diğer uygulamalara izinler** bölümünde için **Azure Active Directory** kaynak tıklatın **uygulama izinleri** aşağı açılan listeyi ve ardından **dizin verilerini okuma**.
   
    ![Uygulamayı Kaydet](./media/active-directory-reporting-api-prerequisites/09.png)
7. Alt çubuğunda **kaydetmek**.
   
    ![Uygulamayı Kaydet](./media/active-directory-reporting-api-prerequisites/10.png)

## <a name="gather-configuration-settings-from-your-directory"></a>Yapılandırma ayarları dizininizden toplayın
Bu bölüm, aşağıdaki ayarları dizininizden alma gösterir:

* Etki alanı adı
* İstemci kimliği
* Gizli anahtar

Raporlama API çağrıları yapılandırırken bu değerleri gerekir. 

### <a name="get-your-domain-name"></a>Etki alanı adınızı alma
1. İçinde [Klasik Azure portalı](https://manage.windowsazure.com), sol gezinti bölmesinde tıklatın **Active Directory**.
   
    ![Uygulamayı Kaydet](./media/active-directory-reporting-api-prerequisites/01.png) 
2. Gelen **active directory** listesinde, dizininizi seçin.
3. Üstteki menüde tıklatın **etki alanları**.
   
    ![Uygulamayı Kaydet](./media/active-directory-reporting-api-prerequisites/11.png) 
4. İçinde **etki alanı adı** sütun, etki alanı adınızı kopyalayın.
   
    ![Uygulamayı Kaydet](./media/active-directory-reporting-api-prerequisites/12.png) 

### <a name="get-the-applications-client-id"></a>Uygulamanın istemci kimliği alın
1. İçinde [Klasik Azure portalı](https://manage.windowsazure.com), sol gezinti bölmesinde tıklatın **Active Directory**.
   
    ![Uygulamayı Kaydet](./media/active-directory-reporting-api-prerequisites/01.png) 
2. Gelen **active directory** listesinde, dizininizi seçin.
3. Üstteki menüde tıklatın **uygulamaları**.
   
    ![Uygulamayı Kaydet](./media/active-directory-reporting-api-prerequisites/02.png) 
4. Uygulamalar listesinde yeni oluşturulan uygulamanızı seçin.
   
    ![Uygulamayı Kaydet](./media/active-directory-reporting-api-prerequisites/07.png)
5. Üstteki menüde tıklatın **yapılandırma**.
   
    ![Uygulamayı Kaydet](./media/active-directory-reporting-api-prerequisites/08.png)
6. Kopyalama, **istemci kimliği**.
   
    ![Uygulamayı Kaydet](./media/active-directory-reporting-api-prerequisites/13.png)

### <a name="get-the-applications-client-secret"></a>Uygulamanın istemci parolası mı almak
Uygulamanızın istemci parolası mı almak için yeni bir anahtar oluşturun ve bu değer daha sonra artık almak mümkün olmadığı için yeni anahtarı kaydetme sırasında değerini kaydedin gerekir.

1. İçinde [Klasik Azure portalı](https://manage.windowsazure.com), sol gezinti bölmesinde tıklatın **Active Directory**.
   
    ![Uygulamayı Kaydet](./media/active-directory-reporting-api-prerequisites/01.png) 
2. Gelen **active directory** listesinde, dizininizi seçin.
3. Üstteki menüde tıklatın **uygulamaları**.
   
    ![Uygulamayı Kaydet](./media/active-directory-reporting-api-prerequisites/02.png) 
4. Uygulamalar listesinde yeni oluşturulan uygulamanızı seçin.
   
    ![Uygulamayı Kaydet](./media/active-directory-reporting-api-prerequisites/07.png)
5. Üstteki menüde tıklatın **yapılandırma**.
   
    ![Uygulamayı Kaydet](./media/active-directory-reporting-api-prerequisites/08.png)
6. İçinde **anahtarları** bölümünde, aşağıdaki adımları gerçekleştirin: 
   
    ![Uygulamayı Kaydet](./media/active-directory-reporting-api-prerequisites/14.png)
   
    a. Bir süre süre listesinden seçin
   
    b. Alt çubuğunda **kaydetmek**.
   
    ![Uygulamayı Kaydet](./media/active-directory-reporting-api-prerequisites/10.png)
   
    c. Anahtar değerini kopyalayın.

## <a name="next-steps"></a>Sonraki Adımlar
* Verileri Azure AD raporlama API'si programlı bir şekilde erişmek ister misiniz? Kullanıma [Azure Active Directory raporlama API'si ile çalışmaya başlama](active-directory-reporting-api-getting-started.md).
* Azure Active Directory raporlama hakkında daha fazla bilgi edinmek istiyorsanız, bkz: [Azure Active Directory raporlama Kılavuzu](active-directory-reporting-guide.md).  

