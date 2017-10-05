---
title: "Azure mantıksal uygulamaları için şirket içi veri kaynaklarına erişim | Microsoft Docs"
description: "Mantığı uygulamalardan şirket içi veri kaynaklarına erişebilmesi için şirket içi veri ağ geçidi kurun ayarlayın"
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
ms.openlocfilehash: 24793b83ca284fe9510fe21bc2d13b0589209d36
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="access-data-sources-on-premises-from-logic-apps-with-the-on-premises-data-gateway"></a>Şirket içi şirket içi veri ağ geçidi ile mantığı uygulamalardan veri kaynaklarına erişim

Mantıksal uygulamalarınızı şirket içi veri kaynaklarına erişmek için ile desteklenen bağlayıcılar mantıksal uygulamaları kullanan şirket içi veri ağ geçidi ayarlayın. Ağ geçidi hızlı veri aktarımı ve logic apps ile şirket içi veri kaynakları arasındaki şifreleme sağlayan köprü gibi davranır. Ağ geçidi şifrelenmiş kanalda Azure Service Bus aracılığıyla şirket içi kaynaklardan veri aktarır. Ağ geçidi aracısından güvenli giden trafik olarak tüm trafiğin kaynaklandığı. Daha fazla bilgi edinmek [veri ağ geçidinin nasıl çalıştığını](logic-apps-gateway-install.md#gateway-cloud-service). 

Ağ geçidi, şirket içinde bu veri kaynaklarının bağlantılarını destekler:

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

Bu adımları, şirket içi veri ağ geçidi kurun logic apps ile çalışacak biçimde ayarlamak gösterilmektedir. Desteklenen bağlayıcılar hakkında daha fazla bilgi için bkz: [Azure Logic Apps bağlayıcılarının](../connectors/apis-list.md). 

Ağ geçidi diğer hizmetlerle birlikte kullanma hakkında daha fazla bilgi için bu makalelere bakın:

*   [Microsoft Power BI şirket içi veri ağ geçidi](https://powerbi.microsoft.com/documentation/powerbi-gateway-onprem/)
*   [Azure Analysis Services veri ağ geçidi şirket içi](../analysis-services/analysis-services-gateway.md)
*   [Microsoft Flow şirket içi veri ağ geçidi](https://flow.microsoft.com/documentation/gateway-manage/)
*   [Microsoft PowerApps şirket içi veri ağ geçidi](https://powerapps.microsoft.com/tutorials/gateway-management/)

## <a name="requirements"></a>Gereksinimler

* Önceden olmalıdır [veri ağ geçidi yerel bir bilgisayarda yüklü](logic-apps-gateway-install.md).

* Azure portalında oturum açtığınızda, aynı iş veya Okul hesabı için kullanılan kullanmak zorunda [şirket içi veri ağ geçidi yükleme](logic-apps-gateway-install.md#requirements). Oturum açma hesabınızın Ayrıca ağ geçidi yükleme için Azure portalında bir ağ geçidi kaynak oluştururken kullanmak için bir Azure aboneliğine sahip olmalıdır.

* Ağ geçidi yüklemenizi zaten bir Azure ağ geçidi kaynağı tarafından istenemiyor. Ağ geçidi yüklemenizi yalnızca bir Azure ağ geçidi kaynağına ilişkilendirebilirsiniz. Yükleme için diğer kaynaklar kullanılamıyor, ağ geçidi kaynağı oluşturun, böylece talep olur.

## <a name="set-up-the-data-gateway-connection"></a>Veri ağ geçidi bağlantısı kurma

### <a name="1-install-the-on-premises-data-gateway"></a>1. Şirket içi veri ağ geçidi yükleme

Henüz yapmadıysanız, izleyin [şirket içi veri ağ geçidi yüklemek için adımları](logic-apps-gateway-install.md). Diğer adımlarla devam etmeden önce veri ağ geçidi yerel bir bilgisayarda yüklü emin olun.

<a name="create-gateway-resource"></a>
### <a name="2-create-an-azure-resource-for-the-on-premises-data-gateway"></a>2. Şirket içi veri ağ geçidi için bir Azure kaynağı oluşturma

Yerel bir bilgisayarda ağ geçidi'ni yükledikten sonra bir kaynak olarak Azure data gateway oluşturmanız gerekir. Bu adım, ağ geçidi kaynağı ayrıca Azure aboneliğiniz ile ilişkilendirir.

1. [Azure portalı](https://portal.azure.com "Azure portalı") oturumunu açın. Ağ geçidi yüklemek için kullanılan e-posta adresi okul veya aynı Azure iş emin olun.

2. Azure sol menüsünde, **yeni** > **Kurumsal tümleştirme** > **şirket içi veri ağ geçidi** aşağıda gösterildiği gibi:

   !["Şirket içi veri ağ geçidi" Bul](./media/logic-apps-gateway-connection/find-on-premises-data-gateway.png)

3. Üzerinde **oluşturma bağlantı ağ geçidi** dikey penceresinde, veri ağ geçidi kaynağı oluşturmak için bu ayrıntıları sağlayın:

    * **Ad**: ağ geçidi kaynağı için bir ad girin. 

    * **Abonelik**: ağ geçidi kaynağınız ile ilişkilendirmek için Azure aboneliğini seçin. 
    Bu abonelik mantıksal uygulamanızı aynı abonelik olmalıdır.
   
      Varsayılan abonelik oturum açmak için kullandığınız Azure hesabı temel alır.

    * **Kaynak grubu**: bir kaynak grubu oluşturun veya varolan bir kaynak grubu, ağ geçidi kaynağı dağıtmak için seçin. 
    Kaynak grupları ilgili Azure varlıklar koleksiyonu olarak yönetmenize yardımcı olur.

    * **Konum**: Azure kısıtlayan sırasında ağ geçidi bulut hizmeti için seçtiğiniz aynı bölgede bu konuma [ağ geçidi yükleme](logic-apps-gateway-install.md). 

      > [!NOTE]
      > Ağ geçidi kaynak konumu ağ geçidi bulut hizmeti konumu eşleştiğinden emin olun. Aksi halde, sonraki adımda seçebilmeniz için yüklü ağ geçitleri listesinde ağ geçidi yüklemenizi görünmeyebilir.
      > 
      > Farklı bölgelerde mantıksal uygulamanızı ve ağ geçidi kaynağı için kullanabilirsiniz.

    * **Yükleme adı**: ağ geçidi yüklemenizi seçili değilse, daha önce yüklediğiniz ağ geçidi seçin. 

    Ağ geçidi kaynağı Azure panonuza eklemek için **panoya Sabitle**. 
    İşiniz bittiğinde seçin **oluşturma**.

    Örneğin:

    ![Şirket içi veri ağ geçidi oluşturmak için ayrıntıları belirtin](./media/logic-apps-gateway-connection/createblade.png)

    Bulma veya ana menüden Azure sol, herhangi bir zamanda data gateway görüntülemek için Git **daha Hizmetleri** > **Kurumsal tümleştirme** > **şirket içi veri ağ geçidi**.

    !["Daha fazla Hizmetleri", "Kurumsal tümleştirme", "şirket içi veri ağ geçidi" sayfasına gidin](./media/logic-apps-gateway-connection/find-on-premises-data-gateway-enterprise-integration.png)

<a name="connect-logic-app-gateway"></a>
### <a name="3-connect-your-logic-app-to-the-on-premises-data-gateway"></a>3. Şirket içi veri ağ geçidi mantıksal uygulamanızı Bağlan

Veri ağ geçidi kaynağı oluşturulur ve Azure aboneliğiniz bu kaynakla ilişkili olduğundan, mantıksal uygulamanızı ve veri ağ geçidi arasında bir bağlantı oluşturun.

> [!NOTE]
> Ağ geçidi bağlantı konumunuz mantıksal uygulamanızı ile aynı bölgede olması gerekir, ancak farklı bir bölgede bulunan bir veri ağ geçidi kullanabilirsiniz.

1. Azure portalında oluşturun veya mantığı Uygulama Tasarımcısı'nda mantıksal uygulamanızı açın.

2. SQL Server gibi şirket içi bağlantıları destekleyen bir bağlayıcı ekleyin.

3. Gösterilen sırada aşağıdaki seçin **Connect şirket içi veri ağ geçidi üzerinden**benzersiz bağlantı adı ve gerekli bilgileri sağlayın ve kullanmak istediğiniz veri ağ geçidi kaynağı seçin. İşiniz bittiğinde seçin **oluşturma**.

   > [!TIP]
   > Benzersiz bağlantı adı özellikle birden çok bağlantı oluşturduğunuzda bu bağlantıyı daha sonra kolayca belirlemenize yardımcı olur. Uygunsa, ayrıca, kullanıcı adı için tam etki alanı içerir. 

   ![Mantıksal uygulama ve veri ağ geçidi arasında bağlantı oluşturma](./media/logic-apps-gateway-connection/blankconnection.png)

Tebrikler, ağ geçidi bağlantınızı kullanmak mantığı uygulamanız için hazırdır.

## <a name="edit-your-gateway-connection-settings"></a>Ağ geçidi bağlantı ayarlarını Düzenle

Mantıksal uygulamanız için bir ağ geçidi bağlantısı oluşturduktan sonra daha sonra özel bağlantı ayarlarını güncelleştirmek isteyebilirsiniz.

1. Ağ geçidi bağlantısı bulmak için:

   * Mantıksal uygulama dikey altında **geliştirme araçları**seçin **API bağlantıları**. 
   
     **API bağlantıları** bölmesinde Ağ Geçidi bağlantıları dahil olmak üzere mantıksal uygulamanızı ile ilişkili tüm API bağlantıları gösterir.

     ![Mantıksal uygulamanızı gidin, ""API bağlantıları seçin](./media/logic-apps-gateway-connection/logic-app-find-api-connections.png)

   * Veya, ana Azure sol menüden, Git **daha Hizmetleri** > **Web ve mobil Hizmetler** > **API bağlantıları** tüm API bağlantıları için Azure aboneliğinizle ilişkili ağ geçidi bağlantıları dahil olmak üzere. 

   * Veya, ana Azure sol menüde, Git **tüm kaynakları** tüm API bağlantıları için Azure aboneliğinizle ilişkili ağ geçidi bağlantıları dahil olmak üzere.

2. Görüntüleyin veya düzenleyin ve seçmek istediğiniz ağ geçidi bağlantısı seçin **Düzenle API bağlantı**.

   > [!TIP]
   > Yaptığınız güncelleştirmeler etkili değil olarak işaretlerse, [ağ geçidi Windows hizmeti durdurup](./logic-apps-gateway-install.md#restart-gateway).

<a name="change-delete-gateway-resource"></a>
## <a name="switch-or-delete-your-on-premises-data-gateway-resource"></a>Geçiş veya şirket içi veri ağ geçidi kaynağı silme

Farklı ağ geçidi kaynağı oluşturmak, ağ geçidiniz farklı bir kaynakla ilişkilendirme veya ağ geçidi kaynağı kaldırmak için ağ geçidi kaynağına ağ geçidi yükleme etkilemeden silebilirsiniz. 

1. Ana Azure sol menüden, Git **tüm kaynakları**. 
2. Bul ve veri ağ geçidi kaynağı seçin.
3. Seçin **şirket içi veri ağ geçidi**ve kaynak araç çubuğunda seçin **silmek**.

<a name="faq"></a>
## <a name="frequently-asked-questions"></a>Sık sorulan sorular

[!INCLUDE [existing-gateway-location-changed](../../includes/logic-apps-existing-gateway-location-changed.md)]

## <a name="next-steps"></a>Sonraki adımlar

* [Mantıksal uygulamanızı güvenli hale getirme](./logic-apps-securing-a-logic-app.md)
* [Yayın örnekleri ve senaryoları için logic apps](./logic-apps-examples-and-scenarios.md)
