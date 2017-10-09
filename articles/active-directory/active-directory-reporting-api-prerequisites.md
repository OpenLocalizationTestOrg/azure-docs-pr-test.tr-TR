---
title: aaaPrerequisites tooaccess hello Azure AD raporlama API'si. | Microsoft Belgeleri
description: "Merhaba Önkoşullar tooaccess hello Azure AD raporlama API'si hakkında bilgi edinin"
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
ms.openlocfilehash: e9d7ceaedb07d18fbd75b70d68b5cfbebc756c36
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="prerequisites-tooaccess-hello-azure-ad-reporting-api"></a>Önkoşullar tooaccess hello Azure AD raporlama API'si
Merhaba [API'leri raporlama Azure AD](https://msdn.microsoft.com/library/azure/ad/graph/howto/azure-ad-reports-and-events-preview) bir dizi REST tabanlı API'ler aracılığıyla programlı erişim toohello verilerle sağlayın. Çeşitli programlama dilleri ve araçlarından bu API'leri çağırabilirsiniz.

API kullandığı raporlama hello [OAuth](https://msdn.microsoft.com/library/azure/dn645545.aspx) tooauthorize erişim toohello web API'leri. 

tooprepare raporlama API'si, erişim toohello yapmanız gerekir:

1. Azure AD kiracınızda uygulama oluşturma 
2. Azure AD Veri GRANT hello uygulama uygun izinleri tooaccess hello
3. Yapılandırma ayarları dizininizden toplayın

Sorularınız, sorunları veya Geri bildiriminiz için lütfen başvurun [raporlama AAD Yardım](mailto:aadreportinghelp@microsoft.com).

## <a name="create-an-azure-ad-application"></a>Azure AD uygulaması oluştur
tooconfigure, dizin tooaccess hello Azure AD raporlama API'si, toohello Klasik Azure portalı, aynı zamanda Azure AD kiracınızda hello genel yönetici dizin rolünün bir üyesi olan bir Azure aboneliği yönetici hesabıyla oturum açmanız gerekir.

> [!IMPORTANT]
> Bu gibi "Yönetici" ayrıcalıkları olan kimlik bilgileri altında çalışan uygulamalar çok güçlü olabilir, bu nedenle lütfen emin tookeep hello uygulamanın kimliği/parola kimlik bilgileri güvenli.
> 
> 

1. Merhaba, [Klasik Azure portalı](https://manage.windowsazure.com), üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Active Directory**.
   
    ![Uygulamayı Kaydet](./media/active-directory-reporting-api-prerequisites/01.png) 
2. Merhaba gelen **active directory** listesinde, dizininizi seçin.
3. Hello içinde hello üst menüsünde **uygulamaları**.
   
    ![Uygulamayı Kaydet](./media/active-directory-reporting-api-prerequisites/02.png) 
4. Merhaba alt çubuğunda **Ekle**.
   
    ![Uygulamayı Kaydet](./media/active-directory-reporting-api-prerequisites/03.png) 
5. Merhaba üzerinde **neler toodo istediğiniz?** iletişim kutusunda, tıklatın **kuruluşumun geliştirmekte olduğu bir uygulama Ekle**. 
   
    ![Uygulamayı Kaydet](./media/active-directory-reporting-api-prerequisites/04.png) 
6. Merhaba üzerinde **bize uygulamanızı anlatın** iletişim kutusunda, hello aşağıdaki adımları gerçekleştirin: 
   
    ![Uygulamayı Kaydet](./media/active-directory-reporting-api-prerequisites/05.png) 
   
    a. Merhaba, **adı** metin kutusuna, bir ad yazın (örneğin: Reporting API uygulaması).
   
    b. Seçin **Web uygulaması ve/veya web API'si**.
   
    c. **İleri**’ye tıklayın.
7. Merhaba üzerinde **uygulama özellikleri** iletişim kutusunda, hello aşağıdaki adımları gerçekleştirin: 
   
    ![Uygulamayı Kaydet](./media/active-directory-reporting-api-prerequisites/06.png) 
   
    a. Merhaba, **oturum açma URL'si** metin kutusuna, türü `https://localhost`.
   
    b. Merhaba, **uygulama kimliği URI'si** metin kutusuna, türü ```https://localhost/ReportingApiApp```.
   
    c. **Tamamla**’ya tıklayın.

## <a name="grant-your-application-permission-toouse-hello-api"></a>Uygulama izni toouse hello API verin
1. Merhaba, [Klasik Azure portalı](https://manage.windowsazure.com/), üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Active Directory**.
   
    ![Uygulamayı Kaydet](./media/active-directory-reporting-api-prerequisites/01.png) 
2. Merhaba gelen **active directory** listesinde, dizininizi seçin.
3. Hello içinde hello üst menüsünde **uygulamaları**.
   
    ![Uygulamayı Kaydet](./media/active-directory-reporting-api-prerequisites/02.png)
4. Merhaba uygulamalar listesinde yeni oluşturulan uygulamanızı seçin.
   
    ![Uygulamayı Kaydet](./media/active-directory-reporting-api-prerequisites/07.png)
5. Hello içinde hello üst menüsünde **yapılandırma**.
   
    ![Uygulamayı Kaydet](./media/active-directory-reporting-api-prerequisites/08.png)
6. Merhaba, **izinleri tooother uygulamaları** hello için bölüm **Azure Active Directory** kaynak hello tıklatın **uygulama izinleri** aşağı açılan listesinde ve ardından seçin **dizin verilerini okuma**.
   
    ![Uygulamayı Kaydet](./media/active-directory-reporting-api-prerequisites/09.png)
7. Merhaba alt çubuğunda **kaydetmek**.
   
    ![Uygulamayı Kaydet](./media/active-directory-reporting-api-prerequisites/10.png)

## <a name="gather-configuration-settings-from-your-directory"></a>Yapılandırma ayarları dizininizden toplayın
Bu bölümde, nasıl gösterilir dizininizden ayarları aşağıdaki tooget hello:

* Etki alanı adı
* İstemci kimliği
* Gizli anahtar

Bu değerleri çağrıları toohello raporlama API yapılandırırken gerekir. 

### <a name="get-your-domain-name"></a>Etki alanı adınızı alma
1. Merhaba, [Klasik Azure portalı](https://manage.windowsazure.com), üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Active Directory**.
   
    ![Uygulamayı Kaydet](./media/active-directory-reporting-api-prerequisites/01.png) 
2. Merhaba gelen **active directory** listesinde, dizininizi seçin.
3. Hello içinde hello üst menüsünde **etki alanları**.
   
    ![Uygulamayı Kaydet](./media/active-directory-reporting-api-prerequisites/11.png) 
4. Merhaba, **etki alanı adı** sütun, etki alanı adınızı kopyalayın.
   
    ![Uygulamayı Kaydet](./media/active-directory-reporting-api-prerequisites/12.png) 

### <a name="get-hello-applications-client-id"></a>Merhaba uygulamanın istemci kimliği alın
1. Merhaba, [Klasik Azure portalı](https://manage.windowsazure.com), üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Active Directory**.
   
    ![Uygulamayı Kaydet](./media/active-directory-reporting-api-prerequisites/01.png) 
2. Merhaba gelen **active directory** listesinde, dizininizi seçin.
3. Hello içinde hello üst menüsünde **uygulamaları**.
   
    ![Uygulamayı Kaydet](./media/active-directory-reporting-api-prerequisites/02.png) 
4. Merhaba uygulamalar listesinde yeni oluşturulan uygulamanızı seçin.
   
    ![Uygulamayı Kaydet](./media/active-directory-reporting-api-prerequisites/07.png)
5. Hello içinde hello üst menüsünde **yapılandırma**.
   
    ![Uygulamayı Kaydet](./media/active-directory-reporting-api-prerequisites/08.png)
6. Kopyalama, **istemci kimliği**.
   
    ![Uygulamayı Kaydet](./media/active-directory-reporting-api-prerequisites/13.png)

### <a name="get-hello-applications-client-secret"></a>Merhaba uygulamanın istemci parolası mı almak
tooget uygulamanızın istemci gizli, toocreate yeni bir anahtar gerekir ve bu değer daha sonra artık olası tooretrieve olmadığından hello yeni anahtarı kaydetme sırasında değerini kaydedin.

1. Merhaba, [Klasik Azure portalı](https://manage.windowsazure.com), üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Active Directory**.
   
    ![Uygulamayı Kaydet](./media/active-directory-reporting-api-prerequisites/01.png) 
2. Merhaba gelen **active directory** listesinde, dizininizi seçin.
3. Hello içinde hello üst menüsünde **uygulamaları**.
   
    ![Uygulamayı Kaydet](./media/active-directory-reporting-api-prerequisites/02.png) 
4. Merhaba uygulamalar listesinde yeni oluşturulan uygulamanızı seçin.
   
    ![Uygulamayı Kaydet](./media/active-directory-reporting-api-prerequisites/07.png)
5. Hello içinde hello üst menüsünde **yapılandırma**.
   
    ![Uygulamayı Kaydet](./media/active-directory-reporting-api-prerequisites/08.png)
6. Merhaba, **anahtarları** bölümünde, hello aşağıdaki adımları gerçekleştirin: 
   
    ![Uygulamayı Kaydet](./media/active-directory-reporting-api-prerequisites/14.png)
   
    a. Merhaba süre listesinden bir süre seçin
   
    b. Merhaba alt çubuğunda **kaydetmek**.
   
    ![Uygulamayı Kaydet](./media/active-directory-reporting-api-prerequisites/10.png)
   
    c. Merhaba anahtar değerini kopyalayın.

## <a name="next-steps"></a>Sonraki Adımlar
* , Tooaccess hello Azure AD verilerden hello gibi raporlama API programlı bir şekilde? Kullanıma [hello Azure Active Directory raporlama API'si ile çalışmaya başlama](active-directory-reporting-api-getting-started.md).
* Merhaba toofind Azure Active Directory raporlama hakkında daha fazla bilgi isterseniz bkz [Azure Active Directory raporlama Kılavuzu](active-directory-reporting-guide.md).  

