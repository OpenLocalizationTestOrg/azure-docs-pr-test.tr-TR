---
title: "OMS BT Hizmet Yönetimi Bağlayıcısı aaaITSM bağlantıları | Microsoft Docs"
description: "ITSM ürünler/hizmetler ile BT Hizmet Yönetimi Bağlayıcısı OMS toocentrally İzleyicisi'nde bağlanmak ve hello ITSM iş öğelerini yönetin."
documentationcenter: 
author: JYOTHIRMAISURI
manager: riyazp
editor: 
ms.assetid: 8231b7ce-d67f-4237-afbf-465e2e397105
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/29/2017
ms.author: v-jysur
ms.openlocfilehash: 53ef51bf75fb8ed15ea3ce5072d9365c221f9f4f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-itsm-productsservices-with-it-service-management-connector-preview"></a>ITSM ürünler/hizmetler ile BT Hizmet Yönetimi Bağlayıcısı (Önizleme) bağlanma
Bu makalede hakkında bilgi sağlar tooconnect ITSM Ürün/hizmet tooIT Hizmet Yönetimi Bağlayıcısı OMS ve merkezi olarak, iş öğelerini yönetme. BT Hizmet Yönetimi Bağlayıcısı hakkında daha fazla bilgi [genel bakış](log-analytics-itsmc-overview.md).

Ürünler/Hizmetler aşağıdaki hello desteklenir:

- [System Center Service Manager](#connect-system-center-service-manager-to-it-service-management-connector-in-oms)
- [ServiceNow](#connect-servicenow-to-it-service-management-connector-in-oms)
- [Provance](#connect-provance-to-it-service-management-connector-in-oms)
- [Cherwell](#connect-cherwell-to-it-service-management-connector-in-oms)

## <a name="connect-system-center-service-manager-tooit-service-management-connector-in-oms"></a>System Center Service Manager tooIT OMS içinde Hizmet Yönetimi Bağlayıcısı Bağlan

Merhaba aşağıdaki bölümlerde verilmiştir hakkında ayrıntılı bilgi tooconnect System Center Service Manager ürün toohello BT Hizmet Yönetimi Bağlayıcısı OMS içinde.

### <a name="prerequisites"></a>Ön koşullar

Aşağıdaki önkoşulları yerine hello olduğundan emin olun:

- BT Hizmet Yönetimi Bağlayıcısı yüklü.
Daha fazla bilgi: [yapılandırma](log-analytics-itsmc-overview.md#configuration).
- Merhaba Service Manager Web uygulaması (Web uygulaması) dağıtılır ve yapılandırılır. Web uygulaması hakkında bilgi [burada](#create-and-deploy-service-manager-web-app-service).
- Karma bağlantı oluşturulur ve yapılandırılır. Daha fazla bilgi: [yapılandırma hello karma bağlantı](#configure-the-hybrid-connection).
- Service Manager sürümleri desteklenir: 2012 R2 veya 2016.
- Kullanıcı rolü: [gelişmiş işleç](https://technet.microsoft.com/library/ff461054.aspx).

### <a name="connection-procedure"></a>Bağlantı yordamı

Aşağıdaki yordam tooconnect hello System Center Service Manager örneğini toohello BT Hizmet Yönetimi Bağlayıcısı kullanın:

1. Çok Git**OMS** >**ayarları** > **bağlı kaynakları**.
2. Seçin **ITSM bağlayıcı** tıklatın **yeni bağlantı Ekle**.

    ![Hizmet Yöneticisi ](./media/log-analytics-itsmc/itsmc-service-manager-connection.png)
3. Aşağıdaki tablonun hello açıklandığı gibi Hello bilgileri sağlayın ve tıklatın **kaydetmek** toocreate hello bağlantı:

> [!NOTE]
> Bu parametre zorunludur.

| **Alan** | **Açıklama** |
| --- | --- |
| **Ad**   | Merhaba BT Hizmet Yönetimi Bağlayıcısı ile tooconnect istediğiniz hello System Center Service Manager örneği için bir ad yazın.  Bu örnekte iş öğelerini yapılandırma / ayrıntılı günlük analizi görünümü olduğunda, bu adı daha sonra kullanırsınız. |
| **Bağlantı türü seçin**   | Seçin **System Center Service Manager**. |
| **Sunucu URL'si**   | Merhaba hello Service Manager Web uygulamasının URL'sini yazın. Service Manager Web uygulaması hakkında daha fazla bilgiyi [burada](#create-and-deploy-service-manager-web-app-service).
| **İstemci kimliği**   | (Merhaba otomatik komut dosyası kullanarak) hello Web uygulaması kimlik doğrulaması için üretilen hello istemci kimliği yazın. Merhaba otomatik komut dosyası hakkında daha fazla bilgiyi [burada.](log-analytics-itsmc-service-manager-script.md)|
| **İstemci parolası**   | Türü hello istemci parolası, bu kimliği için oluşturulan   |
| **Veri Eşitleme kapsamı**   | Merhaba BT Hizmet Yönetimi bağlayıcısı aracılığıyla toosync istediğiniz hello Service Manager iş öğeleri seçin.  Bu iş öğeleri günlük analizi aktarılır. **Seçenekler:** olaylar, değişiklik istekleri.|
| **Eşitleme veri** | Merhaba hello verileri istediğiniz beri geçen gün sayısını yazın. **Üst sınır**: 120 gün. |
| **ITSM çözümde yeni yapılandırma öğesi oluşturma** | Merhaba ITSM ürün toocreate hello yapılandırma öğelerinin istiyorsanız bu seçeneği seçin. Yapılandırma öğelerini (CI var olmayan) durumunda hello ITSM sistem desteklenenler seçili olduğunda, OMS etkilenen hello CIS oluşturur. **Varsayılan**: devre dışı. |

Başarıyla bağlanıldı ve eşitlenen kullanıldığında:

- Seçili iş öğelerini Hizmet Yöneticisi'nden OMS aktarılır **günlük analizi.** Bunlar hello özetini görüntüleme hello BT Hizmet Yönetimi Bağlayıcısı kutucuğu iş öğeleri.

- OMS olaylar OMS uyarıları veya günlük arama, bu Service Manager örneğini oluşturabilirsiniz.

Daha fazla bilgi: [OMS uyarılar için iş öğeleri oluşturma ITSM](log-analytics-itsmc-overview.md#create-itsm-work-items-for-oms-alerts) ve [OMS günlükleri oluşturmak ITSM iş öğelerinden](log-analytics-itsmc-overview.md#create-itsm-work-items-from-oms-logs).

### <a name="create-and-deploy-service-manager-web-app-service"></a>Oluşturma ve Service Manager web uygulama hizmeti dağıtma

tooconnect hello BT Hizmet Yönetimi OMS bağlayıcısında ile şirket içi Service Manager Merhaba, Microsoft hello GitHub üzerinde bir Service Manager Web uygulaması oluşturmuştur.

Merhaba ITSM Web uygulaması için Service Manager yukarı tooset hello aşağıdaki:

- **Dağıtma hello Web uygulaması** – hello Web uygulaması dağıtma, hello özelliklerini ayarlama ve Azure AD ile kimlik doğrulaması. Hello kullanarak hello web uygulaması dağıtabilirsiniz [betik otomatik](log-analytics-itsmc-service-manager-script.md) Microsoft, sağlamıştır.
- **Merhaba karma bağlantı yapılandırma** - [bu bağlantıyı yapılandırmak](#configure-the-hybrid-connection), el ile.

#### <a name="deploy-hello-web-app"></a>Merhaba web uygulaması dağıtma
Kullanım hello otomatik [betik](log-analytics-itsmc-service-manager-script.md) toodeploy Web uygulaması Merhaba, hello özelliklerini ayarlama ve Azure AD ile kimlik doğrulaması.

Gerekli ayrıntıları aşağıdaki hello sağlayarak Hello komut dosyasını çalıştırın:

- Azure Abonelik Ayrıntıları
- Kaynak grubu adı
- Konum
- Service Manager sunucu ayrıntıları (sunucu adı, etki alanı, kullanıcı adı ve parola)
- Web uygulamanız için site adı öneki
- ServiceBus Namespace.

Merhaba betik belirttiğiniz hello adını kullanarak hello Web uygulamasını oluşturur (birkaç ek dizeleri toomake birlikte benzersiz onu). Merhaba oluşturur **Web uygulaması URL'si**, **istemci kimliği** ve **gizli**.

Bir bağlantı ile BT Hizmet Yönetimi Bağlayıcısı oluşturduğunuzda hello değerleri kaydetmek, bunları kullanın.

**Merhaba Web uygulama yükleme denetimi**

1. Çok Git**Azure portal** > **kaynakları**.
2. Merhaba Web uygulaması seçin, **ayarları** > **uygulama ayarları**.
3. Merhaba komut dosyası aracılığıyla hello uygulama dağıtma hello zaman sağlanan hello Service Manager örneğinin Hello bilgilerini doğrulayın.

### <a name="configure-hello-hybrid-connection"></a>Merhaba karma bağlantıyı yapılandırın

Merhaba BT Hizmet Yönetimi OMS Connector'daki ile Merhaba Service Manager örneğine bağlar yordamı tooconfigure hello karma bağlantı aşağıdaki hello kullanın.

1. Hello Service Manager Web uygulamasının altında bulur **Azure kaynakları**.
2. Tıklatın **ayarları** > **ağ**.
3. Altında **karma bağlantılar**, tıklatın **karma bağlantı uç noktalarınızı yapılandırın**.

    ![Karma bağlantının ağ](./media/log-analytics-itsmc/itsmc-hybrid-connection-networking-and-end-points.png)
4. Merhaba, **karma bağlantılar** dikey penceresinde tıklatın **karma Bağlantı Ekle**.

    ![Karma Bağlantısı Ekle](./media/log-analytics-itsmc/itsmc-new-hybrid-connection-add.png)

5. Merhaba, **eklemek karma bağlantılar** dikey penceresinde tıklatın **oluştur yeni karma bağlantı**.

    ![Yeni Karma bağlantı](./media/log-analytics-itsmc/itsmc-create-new-hybrid-connection.png)

6. Merhaba değerleri aşağıdaki komutu yazın:

    - **Uç nokta adı**: hello yeni karma bağlantı için bir ad belirtin.
    -  **Uç noktası ana bilgisayar**: hello Service Manager yönetim sunucusunun FQDN'si.
    - **Uç nokta bağlantı noktası**: 5724 yazın
    - **Servicebus ad alanı**: varolan bir servicebus ad kullanın veya yeni bir tane oluşturun.
    - **Konum**: hello konumu seçin.
    -  **Ad**:, oluşturuyorsanız adı toohello servicebus belirtin.

    ![Karma bağlantı değerleri](./media/log-analytics-itsmc/itsmc-new-hybrid-connection-values.png)
6. Tıklatın **Tamam** tooclose hello **karma bağlantı oluşturmak** dikey penceresinde ve başlangıç hello karma bağlantı oluşturma.

    Merhaba karma bağlantı oluşturulduktan sonra hello dikey altında görüntülenir.

7. Merhaba karma bağlantı oluşturulduktan sonra hello bağlantı tıklatıp **Ekle seçili karma bağlantı**.

    ![Yeni Karma bağlantı](./media/log-analytics-itsmc/itsmc-new-hybrid-connection-added.png)

#### <a name="configure-hello-listener-setup"></a>Merhaba dinleyicisi Kur yapılandırın

Yordam tooconfigure hello dinleyicisi Kur hello karma bağlantı için aşağıdaki hello kullanın.

1. Merhaba, **karma bağlantılar** dikey penceresinde tıklatın **indirme hello Bağlantı Yöneticisi** ve System Center Service Manager örneğinin çalıştığı hello makineye yükleyin.

    Merhaba yükleme tamamlandıktan sonra **karma Bağlantı Yöneticisi kullanıcı Arabirimi** seçeneği altında kullanılabilir **Başlat** menüsü.

2. Tıklatın **karma Bağlantı Yöneticisi kullanıcı Arabirimi** , Azure kimlik bilgileriniz istenir.

3. Azure kimlik bilgilerinizle oturum açma ve hello karma bağlantı oluşturulduğu aboneliğinizi seçin.

4. **Kaydet** düğmesine tıklayın.

Karma bağlantı başarıyla bağlandı.

![başarılı karma bağlantı](./media/log-analytics-itsmc/itsmc-hybrid-connection-listener-set-up-successful.png)
> [!NOTE]

> Merhaba karma bağlantı oluşturulduktan sonra doğrulayın ve Service Manager Web uygulaması hello ziyaret tarafından hello Bağlantıyı Sına dağıtılır. Tooconnect toohello BT Hizmet Yönetimi OMS Connector'daki denemeden önce hello bağlantı başarılı olduğundan emin olun.

Merhaba aşağıdaki görüntüde başarılı bir bağlantı hello ayrıntılarını gösterir:

![Karma bağlantı testi](./media/log-analytics-itsmc/itsmc-hybrid-connection-test.png)

## <a name="connect-servicenow-tooit-service-management-connector-in-oms"></a>ServiceNow tooIT OMS içinde Hizmet Yönetimi Bağlayıcısı Bağlan

Merhaba aşağıdaki bölümlerde verilmiştir hakkında ayrıntılı bilgi tooconnect ServiceNow ürün toohello BT Hizmet Yönetimi Bağlayıcısı OMS içinde.

### <a name="prerequisites"></a>Ön koşullar

Aşağıdaki önkoşulları yerine hello olduğundan emin olun:

- BT Hizmet Yönetimi Bağlayıcısı yüklü. Daha fazla bilgi: [yapılandırma.](log-analytics-itsmc-overview.md#configuration)
- ServiceNow sürümler – Fuji, Geneva, Helsinki desteklenir.

ServiceNow Admins gerçekleştirmelisiniz kendi ServiceNow örneği aşağıdaki hello:
- İstemci kimliği ve hello ServiceNow ürün için istemci parolası oluşturur. Nasıl toogenerate istemci kimliği ve parolası, bkz. bilgi [OAuth Kurulumu](http://wiki.servicenow.com/index.php?title=OAuth_Setup).
- Merhaba kullanıcı uygulama Microsoft OMS tümleştirme (ServiceNow uygulama) yükleyin. [Daha fazla bilgi edinin](https://store.servicenow.com/sn_appstore_store.do#!/store/application/ab0265b2dbd53200d36cdc50cf961980/1.0.0 ).
- Merhaba kullanıcı uygulamanın yüklendiği için tümleştirme kullanıcı rolü oluşturun. Toocreate hello tümleştirme kullanıcı rolü nasıl olduğu hakkında bilgi [burada](#create-integration-user-role-in-servicenow-app).


### <a name="connection-procedure"></a>**Bağlantı yordamı**

Aşağıdaki yordam toocreate ServiceNow bağlantı hello kullan:

1. Çok Git**OMS** > **ayarları** > **bağlı kaynakları**.
2. Seçin **ITSM bağlayıcı** tıklatın **yeni bağlantı Ekle**.

    ![ServiceNow bağlantı](./media/log-analytics-itsmc/itsmc-servicenow-connection.png)

3. Aşağıdaki tablonun hello açıklandığı gibi Hello bilgileri sağlayın ve tıklatın **kaydetmek** toocreate hello bağlantı:

> [!NOTE]
> Bu parametre zorunludur.

| **Alan** | **Açıklama** |
| --- | --- |
| **Ad**   | Merhaba BT Hizmet Yönetimi Bağlayıcısı ile tooconnect istediğiniz hello ServiceNow örneği için bir ad yazın.  İş öğeleri bu ITSM yapılandırma / ayrıntılı günlük analizi görünümü, OMS içinde daha sonra bu adı kullanın. |
| **Bağlantı türü seçin**   | Seçin **ServiceNow**. |
| **Kullanıcı Adı**   | Merhaba ServiceNow uygulama toosupport hello bağlantı toohello BT Hizmet Yönetimi Bağlayıcısı oluşturduğunuz hello tümleştirme kullanıcı adını yazın. Daha fazla bilgi: [oluşturma ServiceNow uygulama kullanıcı rolü](#create-integration-user-role-in-servicenow-app).|
| **Parola**   | Bu kullanıcı adıyla ilişkili hello parolayı yazın. **Not**: kullanıcı adı ve parola yalnızca kimlik doğrulama belirteçleri oluşturmak için kullanılır ve herhangi bir yere hello OMS hizmet içinde depolanmaz.  |
| **Sunucu URL'si**   | Merhaba tooconnect tooIT Hizmet Yönetimi Bağlayıcısı istediğiniz hello ServiceNow örneğinin URL'sini yazın. |
| **İstemci kimliği**   | Daha önce oluşturulan OAuth2 kimlik için toouse istediğiniz hello istemci kimliği yazın.  İstemci kimliği ve parolası oluşturma hakkında daha fazla bilgi: [OAuth Kurulumu](http://wiki.servicenow.com/index.php?title=OAuth_Setup). |
| **İstemci parolası**   | Türü hello istemci parolası, bu kimliği için oluşturulan   |
| **Veri Eşitleme kapsamı**   | Merhaba BT Hizmet Yönetimi bağlayıcısı aracılığıyla toosync tooOMS istediğiniz hello ServiceNow iş öğelerini seçin.  Seçili hello değerleri günlük analizi alınır.   **Seçenekler:** olaylar ve değişiklik istekleri.|
| **Eşitleme veri** | Merhaba hello verileri istediğiniz beri geçen gün sayısını yazın. **Üst sınır**: 120 gün. |
| **ITSM çözümde yeni yapılandırma öğesi oluşturma** | Merhaba ITSM ürün toocreate hello yapılandırma öğelerinin istiyorsanız bu seçeneği seçin. Yapılandırma öğelerini (CI var olmayan) durumunda hello ITSM sistem desteklenenler seçili olduğunda, OMS etkilenen hello CIS oluşturur. **Varsayılan**: devre dışı. |


Başarıyla bağlanıldı ve eşitlenen kullanıldığında:

- Seçili iş öğelerini ServiceNow bağlantısından OMS günlük analizi alınır.  Bunlar hello özetini görüntüleme hello BT Hizmet Yönetimi Bağlayıcısı kutucuğu iş öğeleri.
- Bu ServiceNow örneğinin OMS uyarıları veya günlük aramadan olaylar, uyarılar ve olaylar oluşturabilirsiniz.  


Daha fazla bilgi: [OMS uyarılar için iş öğeleri oluşturma ITSM](log-analytics-itsmc-overview.md#create-itsm-work-items-for-oms-alerts) ve [OMS günlükleri oluşturmak ITSM iş öğelerinden](log-analytics-itsmc-overview.md#create-itsm-work-items-from-oms-logs).

### <a name="create-integration-user-role-in-servicenow-app"></a>ServiceNow uygulamada tümleştirme kullanıcı rolü oluşturun

Aşağıdaki yordamı kullanıcı hello:

1.  Merhaba ziyaret [ServiceNow deposunu](https://store.servicenow.com/sn_appstore_store.do#!/store/application/ab0265b2dbd53200d36cdc50cf961980/1.0.0) hello yükleyip **ServiceNow ve Microsoft OMS tümleştirme için kullanıcı uygulaması** ServiceNow örneğinin içine.
2.  Yükleme tamamlandıktan sonra sol gezinti çubuğunda hello ServiceNow örneğinin, arama ve select Microsoft OMS Tümleştirici hello ziyaret edin.  
3.  Tıklatın **yükleme Yapılacaklar listesi**.

    Merhaba durumu olarak görüntülenir **tamamlanmadı** hello kullanıcı rolü henüz toobe oluşturuldu.

4.  Merhaba metin, sonraki çok kutular**tümleştirme kullanıcı oluşturma**, hello toohello BT Hizmet Yönetimi Bağlayıcısı OMS içinde bağlanıp hello kullanıcı için kullanıcı adı girin.
5.  Bu kullanıcı için Hello parola girin ve tıklayın **Tamam**.  

>[!NOTE]

> Bu kimlik bilgileri toomake hello ServiceNow bağlantı içinde OMS kullanın.

Yeni oluşturulan kullanıcı hello hello varsayılan rolleri atanmış görüntülenir.

Varsayılan roller:
- personalize_choices
- import_transformer
-   x_mioms_microsoft.user
-   ITIL
-   template_editor
-   view_changer

Merhaba kullanıcı başarıyla oluşturulduktan sonra durumu hello **denetleyin yükleme Yapılacaklar listesi** hello uygulaması için oluşturduğunuz hello kullanıcı rolü hello ayrıntılarını listeleme tooCompleted taşır.

> [!NOTE]

> tooallow kullanıcı toocreate **uyarıları** ve **olayları** OMS ServiceNow içinde:

> - Merhaba olay Yönetimi Modülü yüklü ServiceNow örneğinde olduğundan emin olun.

> - Rolleri toohello tümleştirme kullanıcısı aşağıdaki hello ekleyin:
>      - evt_mgmt_integration
>      - evt_mgmt_operator  


## <a name="connect-provance-tooit-service-management-connector-in-oms"></a>Provance tooIT OMS içinde Hizmet Yönetimi Bağlayıcısı Bağlan

Merhaba aşağıdaki bölümlerde verilmiştir hakkında ayrıntılı bilgi tooconnect Provance ürün toohello BT Hizmet Yönetimi Bağlayıcısı OMS içinde.

### <a name="prerequisites"></a>Ön koşullar

Aşağıdaki önkoşulları yerine hello olduğundan emin olun:

- BT Hizmet Yönetimi Bağlayıcısı yüklü. Daha fazla bilgi: [yapılandırma](log-analytics-itsmc-overview.md#configuration).
- Azure AD ile - provance uygulama kaydedileceğini ve istemci kimliği kullanımına sunulur. Ayrıntılı bilgi için bkz: [nasıl tooconfigure active directory kimlik doğrulaması](../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md).
- Kullanıcı rolü: yönetici.

### <a name="connection-procedure"></a>Bağlantı yordamı

Aşağıdaki yordam toocreate Provance bağlantı hello kullan:

1. Çok Git**OMS** > **ayarları** > **bağlı kaynakları**.
2. Seçin **ITSM bağlayıcı** tıklatın **yeni bağlantı Ekle**.  

    ![Provance bağlantı](./media/log-analytics-itsmc/itsmc-provance-connection.png)
3. Aşağıdaki tablonun hello açıklandığı gibi Hello bilgileri sağlayın ve tıklatın **kaydetmek** toocreate hello bağlantı.

> [!NOTE]
> Bu parametre zorunludur.

| **Alan** | **Açıklama** |
| --- | --- |
| **Ad**   | Merhaba BT Hizmet Yönetimi Bağlayıcısı ile tooconnect istediğiniz hello Provance örneği için bir ad yazın.  İş öğeleri bu ITSM yapılandırma / ayrıntılı günlük analizi görünümü, OMS içinde daha sonra bu adı kullanın. |
| **Bağlantı türü seçin**   | Seçin **Provance**. |
| **Kullanıcı Adı**   | Toohello BT Hizmet Yönetimi Bağlayıcısı bağlanabilir hello kullanıcı adını yazın.    |
| **Parola**   | Bu kullanıcı adıyla ilişkili hello parolayı yazın. **Not:** kullanıcı adı ve parola yalnızca kimlik doğrulama belirteçleri oluşturmak için kullanılır ve herhangi bir yere hello OMS hizmet içinde depolanmaz. _|
| **Sunucu URL'si**   | Tooconnect tooIT Hizmet Yönetimi Bağlayıcısı istediğiniz Provance örneğinizi Hello URL'sini yazın. |
| **İstemci kimliği**   | Provance örneğinde oluşturulan bu bağlantısının kimlik doğrulaması için Hello istemci kimliği yazın.  İstemci kimliği hakkında daha fazla bilgi [nasıl tooconfigure active directory kimlik doğrulaması](../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md). |
| **Veri Eşitleme kapsamı**   | Merhaba BT Hizmet Yönetimi bağlayıcısı aracılığıyla toosync tooOMS istediğiniz hello Provance iş öğelerini seçin.  Bu iş öğeleri günlük analizi aktarılır.   **Seçenekler:** olaylar, değişiklik istekleri.|
| **Eşitleme veri** | Merhaba hello verileri istediğiniz beri geçen gün sayısını yazın. **Üst sınır**: 120 gün. |
| **ITSM çözümde yeni yapılandırma öğesi oluşturma** | Merhaba ITSM ürün toocreate hello yapılandırma öğelerinin istiyorsanız bu seçeneği seçin. Yapılandırma öğelerini (CI var olmayan) durumunda hello ITSM sistem desteklenenler seçili olduğunda, OMS etkilenen hello CIS oluşturur. **Varsayılan**: devre dışı.|

Başarıyla bağlanıldı ve eşitlenen kullanıldığında:

- Seçili iş öğelerini Provance bağlantısından OMS aktarılır **günlük analizi.**  Bunlar hello özetini görüntüleme hello BT Hizmet Yönetimi Bağlayıcısı kutucuğu iş öğeleri.
- Olayları ve olayları OMS uyarıları veya günlük arama bu Provance örneğinde oluşturabilirsiniz.

Daha fazla bilgi: [OMS uyarılar için iş öğeleri oluşturma ITSM](log-analytics-itsmc-overview.md#create-itsm-work-items-for-oms-alerts) ve [OMS günlükleri oluşturmak ITSM iş öğelerinden](log-analytics-itsmc-overview.md#create-itsm-work-items-from-oms-logs).

## <a name="connect-cherwell-tooit-service-management-connector-in-oms"></a>Cherwell tooIT OMS içinde Hizmet Yönetimi Bağlayıcısı Bağlan

Merhaba aşağıdaki bölümlerde verilmiştir hakkında ayrıntılı bilgi tooconnect Cherwell ürün toohello BT Hizmet Yönetimi Bağlayıcısı OMS içinde.

### <a name="prerequisites"></a>Ön koşullar

Aşağıdaki önkoşulları yerine hello olduğundan emin olun:

- BT Hizmet Yönetimi Bağlayıcısı yüklü. Daha fazla bilgi: [yapılandırma](log-analytics-itsmc-overview.md#configuration).
- Oluşturulan istemci kimliği. Daha fazla bilgi: [Cherwell için istemci kodu oluştur](#generate-client-id-for-cherwell).
- Kullanıcı rolü: yönetici.

### <a name="connection-procedure"></a>Bağlantı yordamı

Aşağıdaki yordam toocreate Cherwell bağlantı hello kullan:

1. Çok Git**OMS** >  **ayarları** > **bağlı kaynakları**.
2. Seçin **ITSM bağlayıcı** tıklatın **yeni bağlantı Ekle**.  

    ![Cherwell kullanıcı kimliği](./media/log-analytics-itsmc/itsmc-cherwell-connection.png)

3. Aşağıdaki tablonun hello açıklandığı gibi Hello bilgileri sağlayın ve tıklatın **kaydetmek** toocreate hello bağlantı.

> [!NOTE]
> Bu parametre zorunludur.

| **Alan** | **Açıklama** |
| --- | --- |
| **Ad**   | Tooconnect toohello BT Hizmet Yönetimi Bağlayıcısı istediğiniz hello Cherwell örneği için bir ad yazın.  İş öğeleri bu ITSM yapılandırma / ayrıntılı günlük analizi görünümü, OMS içinde daha sonra bu adı kullanın. |
| **Bağlantı türü seçin**   | Seçin **Cherwell.** |
| **Kullanıcı Adı**   | Toohello BT Hizmet Yönetimi Bağlayıcısı bağlanabilir hello Cherwell kullanıcı adını yazın. |
| **Parola**   | Bu kullanıcı adıyla ilişkili hello parolayı yazın. **Not:** kullanıcı adı ve parola yalnızca kimlik doğrulama belirteçleri oluşturmak için kullanılır ve herhangi bir yere hello OMS hizmet içinde depolanmaz.|
| **Sunucu URL'si**   | Tooconnect tooIT Hizmet Yönetimi Bağlayıcısı istediğiniz Cherwell örneğinizi Hello URL'sini yazın. |
| **İstemci kimliği**   | Cherwell örneğinde oluşturulan bu bağlantısının kimlik doğrulaması için Hello istemci kimliği yazın.   |
| **Veri Eşitleme kapsamı**   | Merhaba BT Hizmet Yönetimi bağlayıcısı aracılığıyla toosync istediğiniz hello Cherwell iş öğelerini seçin.  Bu iş öğeleri günlük analizi aktarılır.   **Seçenekler:** olaylar, değişiklik istekleri. |
| **Eşitleme veri** | Merhaba hello verileri istediğiniz beri geçen gün sayısını yazın. **Üst sınır**: 120 gün. |
| **ITSM çözümde yeni yapılandırma öğesi oluşturma** | Merhaba ITSM ürün toocreate hello yapılandırma öğelerinin istiyorsanız bu seçeneği seçin. Yapılandırma öğelerini (CI var olmayan) durumunda hello ITSM sistem desteklenenler seçili olduğunda, OMS etkilenen hello CIS oluşturur. **Varsayılan**: devre dışı. |

Başarıyla bağlanıldı ve eşitlenen kullanıldığında:

- Seçili iş öğeleri bu Cherwell bağlantısından OMS günlük analizi alınır. Bunlar hello özetini görüntüleme hello BT Hizmet Yönetimi Bağlayıcısı kutucuğu iş öğeleri.
- Olayları ve olayları bu OMS Cherwell örneğinden oluşturabilirsiniz. Daha fazla bilgi: Oluştur ITSM iş öğeleri OMS uyarılar ve ITSM oluşturmak için iş öğelerini OMS günlüklerinden.

Daha fazla bilgi: [OMS uyarılar için iş öğeleri oluşturma ITSM](log-analytics-itsmc-overview.md#create-itsm-work-items-for-oms-alerts) ve [OMS günlükleri oluşturmak ITSM iş öğelerinden](log-analytics-itsmc-overview.md#create-itsm-work-items-from-oms-logs).

### <a name="generate-client-id-for-cherwell"></a>İstemci kimliği için Cherwell oluşturun.

toogenerate Cherwell için istemci kimliği/anahtar Merhaba, hello aşağıdaki yordamı kullanın:

1. İçinde tooyour Cherwell örneğinde yönetici olarak oturum
2. Tıklatın **güvenlik** > **Düzenle REST API İstemci Ayarları**.
3. Seçin **oluştur yeni istemci** > **gizli**.

    ![Cherwell kullanıcı kimliği](./media/log-analytics-itsmc/itsmc-cherwell-client-id.png)


## <a name="next-steps"></a>Sonraki adımlar
 - [OMS uyarılar için ITSM iş öğeleri oluşturma](log-analytics-itsmc-overview.md#create-itsm-work-items-for-oms-alerts)

 - [OMS günlüklerinden ITSM iş öğeleri oluşturma](log-analytics-itsmc-overview.md#create-itsm-work-items-from-oms-logs)

- [Bağlantınız için Görünüm günlük analizi](log-analytics-itsmc-overview.md#using-the-solution)
