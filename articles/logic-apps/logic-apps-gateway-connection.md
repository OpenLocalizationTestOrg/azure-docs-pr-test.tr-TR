---
title: "Şirket içi Azure Logic Apps için aaaAccess veri kaynakları | Microsoft Docs"
description: "Merhaba şirket içi veri ağ geçidi mantığı uygulamalardan şirket içi veri kaynaklarına erişebilmesi için ayarlama"
keywords: "Şirket içi veri aktarımı, şifreleme, veri kaynakları veri erişimi"
services: logic-apps
author: jeffhollan
manager: anneta
editor: 
documentationcenter: 
ms.assetid: 6cb4449d-e6b8-4c35-9862-15110ae73e6a
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 07/13/2017
ms.author: LADocs; dimazaid; estfan
ms.openlocfilehash: 1d3deaac5a095316ce78e224dab0c08559bc2ff2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="access-data-sources-on-premises-from-logic-apps-with-hello-on-premises-data-gateway"></a>Şirket içi hello şirket içi veri ağ geçidi ile mantığı uygulamalardan veri kaynaklarına erişim

Şirket içi mantığı uygulamalarınızdan tooaccess veri kaynakları ile desteklenen bağlayıcılar mantıksal uygulamaları kullanan şirket içi veri ağ geçidi ayarlayın. Merhaba ağ geçidi hızlı veri aktarımı ve logic apps ile şirket içi veri kaynakları arasındaki şifreleme sağlayan köprü gibi davranır. Merhaba ağ geçidi şifrelenmiş kanalda hello Azure Service Bus aracılığıyla şirket içi kaynaklardan veri aktarır. Güvenli giden trafiği hello ağ geçidi aracısından olarak tüm trafiğin kaynaklandığı. Daha fazla bilgi edinmek [hello veri ağ geçidi nasıl çalıştığını](logic-apps-gateway-install.md#gateway-cloud-service). 

Merhaba ağ geçidi bağlantıları toothese veri kaynakları şirket içinde destekler:

*   BizTalk Server 2016
*   DB2  
*   Dosya Sistemi
*   Informix
*   MQ
*   MySQL
*   Oracle Veritabanı
*   PostgreSQL
*   SAP uygulama sunucusu 
*   SAP ileti sunucusu
*   SharePoint
*   SQL Server
*   Teradata

Bu adımlar nasıl hello yukarı tooset veri ağ geçidi toowork logic apps ile şirket içi gösterir. Desteklenen bağlayıcılar hakkında daha fazla bilgi için bkz: [Azure Logic Apps bağlayıcılarının](../connectors/apis-list.md). 

Nasıl toouse hello diğer hizmetler ile ağ geçidi hakkında daha fazla bilgi için bu makalelere bakın:

*   [Microsoft Power BI şirket içi veri ağ geçidi](https://powerbi.microsoft.com/documentation/powerbi-gateway-onprem/)
*   [Azure Analysis Services veri ağ geçidi şirket içi](../analysis-services/analysis-services-gateway.md)
*   [Microsoft Flow şirket içi veri ağ geçidi](https://flow.microsoft.com/documentation/gateway-manage/)
*   [Microsoft PowerApps şirket içi veri ağ geçidi](https://powerapps.microsoft.com/tutorials/gateway-management/)

## <a name="requirements"></a>Gereksinimler

* Önceden olmalıdır [hello veri ağ geçidi yerel bir bilgisayarda yüklü](logic-apps-gateway-install.md).

* Toohello Azure portalında oturum açtığınızda hello aynı iş veya Okul çok kullanılan hesap toouse sahip[hello şirket içi veri ağ geçidi yükleme](logic-apps-gateway-install.md#requirements). Ağ geçidi yüklemenize hello Azure portalında bir ağ geçidi kaynak oluşturduğunuzda, oturum açma hesabı ayrıca bir Azure aboneliği toouse sahip olmalıdır.

* Ağ geçidi yüklemenizi zaten bir Azure ağ geçidi kaynağı tarafından istenemiyor. Ağ geçidi yükleme tooonly bir Azure ağ geçidi kaynağınız ilişkilendirebilirsiniz. Böylece Hello yükleme için diğer kaynaklar kullanılamıyor hello ağ geçidi kaynağı oluşturmak talep olur.

## <a name="set-up-hello-data-gateway-connection"></a>Merhaba veri ağ geçidi bağlantı kurma

### <a name="1-install-hello-on-premises-data-gateway"></a>1. Merhaba şirket içi veri ağ geçidi yükleyin

Henüz yapmadıysanız, hello izleyin [adımları tooinstall hello şirket içi veri ağ geçidi](logic-apps-gateway-install.md). Merhaba ile devam etmeden önce diğer adımlar, yerel bir bilgisayarda hello veri ağ geçidi yüklü olduğundan emin olun.

<a name="create-gateway-resource"></a>
### <a name="2-create-an-azure-resource-for-hello-on-premises-data-gateway"></a>2. Merhaba şirket içi veri ağ geçidi için bir Azure kaynağı oluşturma

Yerel bir bilgisayarda hello ağ geçidi yükledikten sonra bir kaynak olarak Azure data gateway oluşturmanız gerekir. Bu adım, ağ geçidi kaynağı ayrıca Azure aboneliğiniz ile ilişkilendirir.

1. İçinde toohello oturum [Azure portal](https://portal.azure.com "Azure portal"). Toouse hello aynı Azure iş veya Okul e-posta adresi tooinstall hello ağ geçidi kullanılan emin olun.

2. Merhaba sol menüsünde Azure, **yeni** > **Kurumsal tümleştirme** > **şirket içi veri ağ geçidi** aşağıda gösterildiği gibi:

   !["Şirket içi veri ağ geçidi" Bul](./media/logic-apps-gateway-connection/find-on-premises-data-gateway.png)

3. Merhaba üzerinde **oluşturma bağlantı ağ geçidi** dikey penceresinde, bu ayrıntıları toocreate veri ağ geçidi kaynağı sağlar:

    * **Ad**: ağ geçidi kaynağı için bir ad girin. 

    * **Abonelik**: seçin, ağ geçidi kaynağı ile Azure aboneliği tooassociate hello. 
    Bu abonelik olmalıdır hello mantıksal uygulamanızı aynı abonelik.
   
      Merhaba varsayılan abonelik hello toosign içinde kullanılan Azure hesabı temel alır.

    * **Kaynak grubu**: bir kaynak grubu oluşturun veya varolan bir kaynak grubu, ağ geçidi kaynağı dağıtmak için seçin. 
    Kaynak grupları ilgili Azure varlıklar koleksiyonu olarak yönetmenize yardımcı olur.

    * **Konum**: Azure kısıtlayan bu konumu toohello sırasında hello ağ geçidi bulut hizmeti için seçtiğiniz aynı bölgede [ağ geçidi yükleme](logic-apps-gateway-install.md). 

      > [!NOTE]
      > Merhaba ağ geçidi kaynak konumu hello ağ geçidi bulut hizmeti konumu eşleştiğinden emin olun. Aksi takdirde, ağ geçidi yüklemenizi hello yüklü ağ geçitleri listesinde, tooselect hello sonraki adımda görünmeyebilir.
      > 
      > Farklı bölgelerde mantıksal uygulamanızı ve ağ geçidi kaynağı için kullanabilirsiniz.

    * **Yükleme adı**: ağ geçidi yüklemenizi seçili değilse, daha önce yüklediğiniz hello ağ geçidi seçin. 

    tooadd hello ağ geçidi kaynak tooyour Azure Pano seçin **PIN toodashboard**. 
    İşiniz bittiğinde seçin **oluşturma**.

    Örneğin:

    ![Şirket içi data gateway ayrıntıları toocreate sağlayın](./media/logic-apps-gateway-connection/createblade.png)

    toofind veya görünümde herhangi bir zamanda data gateway hello ana Azure sol menüsünden Git çok **daha Hizmetleri** > **Kurumsal tümleştirme** > **şirket içi veri Ağ geçitleri**.

    ![Çok Git "Daha fazla Hizmetleri", "Kurumsal tümleştirme", "Şirket içi veri ağ geçidi"](./media/logic-apps-gateway-connection/find-on-premises-data-gateway-enterprise-integration.png)

<a name="connect-logic-app-gateway"></a>
### <a name="3-connect-your-logic-app-toohello-on-premises-data-gateway"></a>3. Mantıksal uygulama toohello şirket içi data gateway Bağlan

Veri ağ geçidi kaynağı oluşturulur ve Azure aboneliğiniz bu kaynakla ilişkili göre logic app ve hello data gateway arasında bir bağlantı oluşturun.

> [!NOTE]
> Ağ geçidi bağlantı konumunuz hello aynı bulunmalıdır bölgeye mantıksal uygulamanızı, ancak farklı bir bölgede mevcut bir veri ağ geçidi kullanabilirsiniz.

1. Hello Azure portal, oluşturun veya mantığı Uygulama Tasarımcısı'nda mantıksal uygulamanızı açın.

2. SQL Server gibi şirket içi bağlantıları destekleyen bir bağlayıcı ekleyin.

3. Gösterilen hello sırasının seçin **Connect şirket içi veri ağ geçidi üzerinden**benzersiz bağlantı adı belirtin ve hello gerekli bilgileri ve hello veri ağ geçidi kaynağı toouse istediğinizi seçin. İşiniz bittiğinde seçin **oluşturma**.

   > [!TIP]
   > Benzersiz bağlantı adı özellikle birden çok bağlantı oluşturduğunuzda bu bağlantıyı daha sonra kolayca belirlemenize yardımcı olur. Uygunsa, ayrıca Merhaba, kullanıcı adı için tam etki alanı içerir. 

   ![Mantıksal uygulama ve veri ağ geçidi arasında bağlantı oluşturma](./media/logic-apps-gateway-connection/blankconnection.png)

Tebrikler, ağ geçidi bağlantınızı, logic app toouse için hazırdır.

## <a name="edit-your-gateway-connection-settings"></a>Ağ geçidi bağlantı ayarlarını Düzenle

Mantıksal uygulamanız için bir ağ geçidi bağlantısı oluşturduktan sonra özel bağlantı toolater güncelleştirme hello ayarlarını isteyebilirsiniz.

1. toofind hello ağ geçidi bağlantısı:

   * Merhaba mantığını uygulaması dikey penceresinde, altında **geliştirme araçları**seçin **API bağlantıları**. 
   
     Merhaba **API bağlantıları** bölmesinde Ağ Geçidi bağlantıları dahil olmak üzere mantıksal uygulamanızı ile ilişkili tüm API bağlantıları gösterir.

     ![Tooyour mantıksal uygulama gidin, ""API bağlantıları seçin](./media/logic-apps-gateway-connection/logic-app-find-api-connections.png)

   * Veya hello ana Azure sol menüden, çok gidin **daha Hizmetleri** > **Web ve mobil Hizmetler** > **API bağlantıları** tüm API bağlantılarında Ağ Geçidi bağlantıları dahil olmak üzere, Azure aboneliğinizle ilişkilendirilmiş. 

   * Veya hello ana Azure sol menüde, çok gidin**tüm kaynakları** tüm API bağlantıları için Azure aboneliğinizle ilişkili ağ geçidi bağlantıları dahil olmak üzere.

2. Tooview veya düzenlemek istediğiniz ve seçin hello ağ geçidi bağlantısı seçin **Düzenle API bağlantı**.

   > [!TIP]
   > Yaptığınız güncelleştirmeler etkili değil olarak işaretlerse, [hello ağ geçidi Windows hizmetini durdurup yeniden başlatarak](./logic-apps-gateway-install.md#restart-gateway).

<a name="change-delete-gateway-resource"></a>
## <a name="switch-or-delete-your-on-premises-data-gateway-resource"></a>Geçiş veya şirket içi veri ağ geçidi kaynağı silme

toocreate farklı ağ geçidi kaynak ağ geçidiniz farklı bir kaynakla ilişkilendirme veya hello ağ geçidi kaynağı kaldırmak, hello ağ geçidi yükleme etkilemeden hello ağ geçidi kaynağı silebilirsiniz. 

1. Merhaba ana Azure sol menüden, çok Git**tüm kaynakları**. 
2. Bul ve veri ağ geçidi kaynağı seçin.
3. Seçin **şirket içi veri ağ geçidi**ve hello kaynak araç çubuğunda seçin **silmek**.

<a name="faq"></a>
## <a name="frequently-asked-questions"></a>Sık sorulan sorular

[!INCLUDE [existing-gateway-location-changed](../../includes/logic-apps-existing-gateway-location-changed.md)]

## <a name="next-steps"></a>Sonraki adımlar

* [Mantıksal uygulamanızı güvenli hale getirme](./logic-apps-securing-a-logic-app.md)
* [Yayın örnekleri ve senaryoları için logic apps](./logic-apps-examples-and-scenarios.md)
