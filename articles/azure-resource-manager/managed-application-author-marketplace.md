---
title: "aaaAzure yönetilen hello Market uygulamalarda | Microsoft Docs"
description: "Azure açıklar yönetilen Market hello kullanılabilir olan uygulamalar."
services: azure-resource-manager
author: ravbhatnagar
manager: rjmax
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 07/09/2017
ms.author: gauravbh; tomfitz
ms.openlocfilehash: b3cdf3f1fccdd47db699e4892ae8bce35118bfd8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-managed-applications-in-hello-marketplace"></a>Azure Market hello uygulamalarda yönetilen

 MSP'ler, ISV ve sistem tümleştiricileri (SIS) kullanabilir Azure yönetilen uygulamaları toooffer çözümleri tooall Azure Marketi müşterilerine. Bu tür çözümler hello Bakım ve müşteriler için ek yükü bakım azaltın. Yayımcılar, altyapı ve yazılım hello Market aracılığıyla satın. Bunlar, hizmetler ve işletimsel destek toomanaged uygulamalar ekleyebilirsiniz. Daha fazla bilgi için bkz: [yönetilen uygulama genel bakış](managed-application-overview.md).

Bu makalede, nasıl bir MSP, ISV veya SI uygulama toohello Market yayımlayabilir ve geniş çapta kullanılabilir toocustomers olun açıklanmaktadır.

## <a name="prerequisites-for-publishing-a-managed-application"></a>Yönetilen bir uygulamayı yayımlamak için Önkoşullar

Önkoşullar toolisting hello Market içinde:

* Teknik

    *  Merhaba temel yapısını ve Azure Resource Manager şablonları sözdizimi hakkında daha fazla bilgi için bkz: [Azure Resource Manager şablonları](resource-group-authoring-templates.md).
    *  tooview tam şablon çözümleri, bakın [Azure hızlı başlangıç şablonlarını](https://azure.microsoft.com/en-us/documentation/templates/) veya hello [Hızlı Başlangıç şablonu deposu](https://github.com/azure/azure-quickstart-templates).
    *  Nasıl toocreate hello arabirimi hello Market üzerinden uygulamanızı dağıtmak müşteriler hakkında daha fazla bilgi için bkz: [bir kullanıcı arabirimi tanımı dosyası oluşturma](managed-application-createuidefinition-overview.md).

* Yedeğin (iş gereksinimlerini)

    *   Şirketiniz veya onun yan burada satış Market hello tarafından desteklenen bir ülkede bulunmalıdır.
    *   Ürünü Market hello tarafından desteklenen faturalama modelleri ile uyumlu şekilde lisansına sahip olması gerekir.
    *   Teknik Destek kullanılabilir toocustomers ticari koşulların elverdiği oranda makul bir biçimde yapmaktan sorumlu. Merhaba destek Ücretli, boş veya topluluk desteklemez.
    *   Yazılım ve üçüncü taraf yazılım bağımlılıkları lisansı sağlamaktan sorumlu.
    *   Azure portal teklifi toobe ölçütlerini karşılayan içerik hello Market ve hello listelenen sağlamanız gerekir.
    *   Toohello hello Azure Market katılım ilkeleri ve yayımcı Sözleşmesi koşullarını kabul etmeniz gerekir.
    *   Merhaba kullanım koşulları, Microsoft gizlilik bildirimi ve Microsoft Azure sertifikalı Program Sözleşmesi ile toocomply kabul etmeniz gerekir.

## <a name="create-a-new-azure-application-offer"></a>Yeni bir Azure uygulama teklifi oluşturma

Merhaba önkoşulları karşılaması sonra hazır toocreate olduğunuz yönetilen uygulamayı teklifiniz. Bir teklif ve bir SKU hızlı bir genel bakış atalım.

### <a name="offer"></a>Sunduğu

yönetilen bir uygulama için Hello teklifi tooa sınıf bir yayımcıdan sunumu ürünün karşılık gelir. Yeni bir çözüm/uygulama toomake hello Market kullanılabilir istediğiniz türü varsa, bunu yeni bir teklif ayarlayabilirsiniz. Bir teklif, SKU'ları koleksiyonudur. Her teklif hello Market kendi varlık gibi görünür.

### <a name="sku"></a>SKU

Bir SKU hello en küçük purchasable bir teklif birimidir. Merhaba içinde bir SKU kullanabilirsiniz arasında aynı ürün sınıfı (teklif) toodifferentiate:

* Desteklenen farklı özellikleri.
* Merhaba teklif yönetilen yönetilmeyen mı.
* Desteklenen faturalama modelleri.

Bir SKU hello Market hello üst teklif altında görüntülenir. Hello Azure portal purchasable kendi varlık gibi görünür.

### <a name="set-up-an-offer"></a>Bir teklif ayarlayın

1. İçinde toohello oturum [bulut iş ortağı portalına](https://cloudpartner.azure.com/).

2. Merhaba soldaki Hello Gezinti Bölmesi'nde seçin **+ yeni teklif** > **Azure uygulamaları**.

    ![Yeni teklif](./media/managed-application-author-marketplace/newOffer.png)

3. Hello sol hello görünür hello form doldurmak **Düzenleyicisi** görünümü. Gerekli alanları ile kırmızı yıldız işareti (*) işaretlenir.

    ![Teklif ayarları](./media/managed-application-author-marketplace/newOffer_OfferSettings.png)

    Dört ana forms kullanılan toocreate bir yönetilen uygulamayı şunlardır:

    a. Teklif ayarları

    b. SKU'ları

    c. Market

    d. Destek

Bu form bölümleri aşağıdaki hello içinde daha ayrıntılı açıklanmıştır.

## <a name="offer-settings-form"></a>Teklif ayarları formu
Bu temel form toospecify hello teklif ayarları kullanın.

1. Hello dolgu **teklif ayarları** formu. Merhaba farklı alanları şunlardır:

    a. **Teklif kodu**: Yayımcı profilindeki hello teklif bu benzersiz tanımlayıcı tanımlar. Bu kimliği ürün URL'ler, Resource Manager şablonları görünür ve faturalama raporlar. Yalnızca küçük harf alfasayısal karakterler veya tire (-) birleştirilebilir. Merhaba kimliği, bir tire bitemez. Sınırlı tooa en çok 50 karakter var. Bu alan, bir teklif Canlı göründükten sonra kilitlendi.

    b. **Yayımcı kimliği**: Bu teklif altında toopublish istediğiniz bu açılan liste toochoose hello yayımcı profili kullanın. Bu alan, bir teklif Canlı göründükten sonra kilitlendi.

    c. **Ad**: hello Market ve hello portal teklifiniz için bu görünen ad görüntülenir. En çok 50 karakter olabilir. Ürününüzün tanınabilir bir marka adını ekleyin. Nasıl pazarlama olmadığı sürece, şirketinizin adını buraya dahil etmeyin. Kendi Web sitesinde bu teklif pazarlama varsa, bu hello adı tam olarak, Web sitenizde görünme olduğundan emin olun.

2. Seçin **kaydetmek** toosave ilerleme durumunuzu. 

## <a name="skus-form"></a>SKU'ları formu
Merhaba sonraki teklifiniz için tooadd SKU'ları adımdır.

1. Seçin **SKU'ları** > **yeni SKU**. 

    ![Yeni SKU seçin](./media/managed-application-author-marketplace/newOffer_skus.png)

2. Girin bir **SKU kimliği**. SKU kimliği hello SKU bir teklif içinde benzersiz tanımlayıcısıdır. Bu kimliği ürün URL'ler, Resource Manager şablonları görünür ve faturalama raporlar. Yalnızca küçük harf alfasayısal karakterler veya tire (-) birleştirilebilir. Hello kimliği bir tire bitemez ve sınırlı tooa en çok 50 karakter değil. Bu alan, bir teklif Canlı göründükten sonra kilitlendi. Bir teklif içinde birden çok SKU olabilir. Bir SKU gereksinim duyduğunuz her görüntü için toopublish planlayın.

3. Merhaba dolgu **SKU ayrıntıları** form aşağıdaki hello bölümünde:

    ![Yeni SKU sağlayın](./media/managed-application-author-marketplace/newOffer_newsku.png)

    Alanları aşağıdaki hello doldurun:
    
    a. **Başlık**: Bu SKU için bir başlık girin. Bu öğe için hello galerisinde bu başlığı görüntülenir.

    b. **Özet**: kısa bir özeti için bu SKU girin. Bu metin hello başlığı altında görüntülenir.

    c. **Açıklama**: hello SKU hakkında ayrıntılı bir açıklama girin.

    d. **SKU tür**: hello izin verilen değerler: **yönetilen uygulamayı** ve **çözüm şablonları**. Bu durumda, seçin **yönetilen uygulamayı**.

4. Merhaba dolgu **Paket ayrıntılarını** form aşağıdaki hello bölümünde:

    ![Paket](./media/managed-application-author-marketplace/newOffer_newsku_package.png)

    Alanları aşağıdaki hello doldurun:

    a. **Geçerli sürüm**: bir sürümü için karşıya yüklediğiniz hello paketi girin. Merhaba biçiminde olmalıdır `{number}.{number}.{number}{number}`.

    b. **Bir paket dosyası seçmek**: Bu paket, sıkıştırılmış dosyalar bir .zip dosyasına aşağıdaki hello içerir:
    * **applianceMainTemplate.json**: toodeploy hello çözüm/uygulama kullandı hello dağıtım şablon dosyası. Hakkında bilgi için bkz toocreate dağıtım şablonu dosyalarını [, ilk Azure Resource Manager şablonu oluşturma](resource-manager-create-first-template.md).
    * **appliancecreateUIDefinition.json**: Bu dosya bu çözümü/uygulama tooprovision kullandığı hello Azure portal toogenerate hello kullanıcı arabirimi tarafından kullanılır. Daha fazla bilgi için bkz: [CreateUiDefinition ile çalışmaya başlama](managed-application-createuidefinition-overview.md).
    * **mainTemplate.json**: Bu şablon dosyası, yalnızca hello Microsoft.Solution/appliances kaynak içeriyor. Merhaba mainTemplate dosyası, aşağıdaki özelliklere hello içerir:

        *  **tür**: kullanım **Market** hello Market yönetilen uygulamalar için.
        *  **ManagedResourceGroupId**: applianceMainTemplate.json içinde tanımlanan tüm hello kaynaklara dağıtıldığı hello müşterinin aboneliğini bu kaynak grubunda bulunuyor.
        *  **PublisherPackageId**: Bu dize hello paketi benzersiz olarak tanımlar. Merhaba biçiminde Hello değer sağlamanız `{publisherId}.{OfferId}.{SKUID}.{PackageVersion}`.

Merhaba elde **Teklif kimliği** ve **yayımcı kimliği** hello görüntü aşağıdaki gösterildiği gibi portal, yayımlama hello gelen:

![Teklif kimliği](./media/managed-application-author-marketplace/UniqueString_pubid_offerid.png)
        
Merhaba elde **SKU kimliği**hello görüntü aşağıdaki gösterildiği gibi:

![SKU KİMLİĞİ](./media/managed-application-author-marketplace/UniqueString_skuid.png)
        
Merhaba paketi almasını **sürüm**hello görüntü aşağıdaki gösterildiği gibi:

![Paket sürümü](./media/managed-application-author-marketplace/UniqueString_packageversion.png)
    
  Örnekler önceki hello üzerinde bağlı olarak, hello değerini **PublisherPackageId** olan `azureappliance-test.ravmanagedapptest.ravpreviewmanagedsku.1.0.0`.

  Örnek mainTemplate.json:

  ```json
  {
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
      "storageAccountNamePrefix": {
        "type": "string",
        "metadata": {
          "description": "Specify hello name of hello storage account"
        }
      },
      "storageAccountType": {
        "type": "string"
      }
    },
    "variables": {
      "managedResourceGroup": "[concat(resourceGroup().id,uniquestring(resourceGroup().id))]"
    },
    "resources": [{
      "type": "Microsoft.Solutions/appliances",
      "apiVersion": "2016-09-01-preview",
      "name": "[concat(parameters('storageAccountNamePrefix'), '-', 'managed')]",
      "location": "[resourceGroup().location]",
      "kind": "marketplace",
      "properties": {
        "managedResourceGroupId": "[variables('managedResourceGroup')]",
        "PublisherPackageId":"azureappliancetest.ravmanagedapptest.ravpreviewmanagedsku.1.0.0",
        "parameters": {
          "storageAccountName": {
            "value": "[parameters('storageAccountNamePrefix')]"
          },
          "storageAccountType": {
            "value": "[parameters('storageAccountType')]"
          }
        }
      }
    }],
    "outputs": {

    }
  }
  ```

Bu paketin diğer iç içe geçmiş şablonları içermesi veya bu uygulamayı gerekli toosuccessfully olan komutlar sağlamak. Merhaba mainTemplate.json, applianceMainTemplate.json ve applianceCreateUIDefinition.json dosyaları hello Kök klasörde mevcut olması gerekir.

* **Yetkilerini**: Bu özellik müşterilerin abonelikleri toohello kaynaklarında kimin erişim ve hello erişim düzeyini alır tanımlar. Merhaba yayımcı toomanage hello uygulama hello müşteri adına kullanabilirsiniz.
* **Principalıd**: Bu özellik hello Azure Active Directory (Azure AD) kullanıcı, kullanıcı grubu veya hello müşterinin aboneliğini hello kaynaklarında belirli izinleri verildi uygulama tanımlayıcısıdır. Merhaba rol tanımı hello izinleri açıklar. 
* **Rol tanımı**: Bu özellik Azure AD tarafından sağlanan tüm hello yerleşik rol tabanlı erişim denetimi (RBAC) rolleri listesini içerir. En uygun toouse toomanage hello kaynakları hello müşteri adına hello rolü seçebilirsiniz.

Birden çok yetkilerini ekleyebilirsiniz. Bir AD kullanıcı grubu oluşturun ve kendi Kimliğini belirtin öneririz **Principalıd**. Bu şekilde hello gerek tooupdate hello SKU olmadan daha fazla kullanıcı toohello kullanıcı grubu ekleyebilirsiniz.

RBAC hakkında daha fazla bilgi için bkz: [hello Azure portalında RBAC ile çalışmaya başlama](../active-directory/role-based-access-control-what-is.md).

## <a name="marketplace-form"></a>Market formu

Merhaba Market form ister hello üzerinde görünmesini alanlar için [Azure Marketi](https://azuremarketplace.microsoft.com) ve hello [Azure portal](https://portal.azure.com/).

### <a name="preview-subscription-ids"></a>Önizleme abonelik kimlikleri

Azure aboneliği yayımlandıktan sonra hello teklif erişebilirsiniz kimlikleri listesini girin. Bunu yapmadan önce bu abonelikleri beyaz listelenen tootest önizlemesi hello teklif kullanabilirsiniz Canlı. Merhaba iş ortağı portalında too100 abonelikleri yukarı beyaz listesi derleyebilirsiniz.

### <a name="suggested-categories"></a>Önerilen kategorileri

Toofive kategorileri teklifiniz en iyi ilişkilendirilebilir hello listeden seçin. Bu kategoriler kullanılan toomap hello kullanılabilir, teklif toohello ürün kategorileri şunlardır [Azure Marketi](https://azuremarketplace.microsoft.com) ve hello [Azure portal](https://portal.azure.com/).

#### <a name="azure-marketplace"></a>Azure Market

Merhaba, yönetilen uygulamanızın özetini alanları izleyen hello görüntüler:

![Market özeti](./media/managed-application-author-marketplace/publishvm10.png)

Merhaba **genel bakış** sekmesi, yönetilen uygulamanızın alanları izleyen hello görüntüler:

![Market’e genel bakış](./media/managed-application-author-marketplace/publishvm11.png)

Merhaba **planları + fiyatlandırma** sekmesi, yönetilen uygulamanızın alanları izleyen hello görüntüler:

![Market planları](./media/managed-application-author-marketplace/publishvm15.png)

#### <a name="azure-portal"></a>Azure portalına

Merhaba, yönetilen uygulamanızın özetini alanları izleyen hello görüntüler:

![Portal özeti](./media/managed-application-author-marketplace/publishvm12.png)

Merhaba genel bakış için yönetilen uygulamanızın alanları izleyen hello görüntüler:

![Portal genel bakış](./media/managed-application-author-marketplace/publishvm13.png)

#### <a name="logo-guidelines"></a>Logo yönergeleri

Merhaba bulut iş ortağı Portalı'nda karşıya logo aşağıdaki yönergeleri izleyin:

*   Hello Azure tasarım basit renk paleti vardır. Merhaba sayısı birincil ve ikincil renkleri logonuzun sınırlandırın.
*   Merhaba Tema renkleri hello portalı beyaz ve siyah. Bu renkleri hello arka plan rengi olarak logonuzun için kullanmayın. Logonuzun hello portalında belirgin hale getirir bir renk kullanın. Basit birincil renkleri öneririz. *Saydam arka plan kullanırsanız, hello logo ve metin beyaz, olduğundan emin olun siyah veya mavi.*
*   Gradyan arka planı hello logosu kullanmayın.
*   Metin hello logosu, bile, şirket veya marka adı yerleştirmeyin. logonuzun Hello Görünüm ve yapısını, düz ve gradyan kaçının.
*   Hello logosu uzatılmış olmadığından emin olun.

#### <a name="hero-logo"></a>Kahramanı logosu

Merhaba kahramanı logosu isteğe bağlıdır. Merhaba yayımcı değil tooupload kahramanı logosu seçebilirsiniz. Merhaba kahramanı simgesi yüklendikten sonra silinemez. O anda hello ortağı kahramanı simgeler için hello Market yönergelere uyması gerekir.

Merhaba kahramanı logo simgesini için aşağıdaki yönergeleri izleyin:

*   Merhaba yayımcı görünen adı, hello planı başlık ve hello teklif uzun Özet beyaz görüntülenir. Bu nedenle, açık bir renk hello kahramanı simgesi hello arka planı için kullanmayın. Siyah, beyaz veya saydam arka plan kahramanı simgelerini izin verilmiyor.
*   Merhaba teklif listelenen sonra hello publisher görüntüler adı, hello planı başlık, hello teklif uzun Özet ve hello **oluşturma** düğmesi program aracılığıyla hello kahramanı logosunun içinde katıştırılmış. Sonuç olarak, hello kahramanı logosu tasarlarken herhangi bir metin girmeyin. Merhaba metni program aracılığıyla bu alana dahil olduğundan boş alanı hello üzerinde sağ bırakın. Merhaba boş alan hello metin hello sağ üzerinde 415 x 100 piksel olmalıdır. Merhaba soldan 370 piksel uzakta bulunur.

    ![Kahramanı logosu örneği](./media/managed-application-author-marketplace/publishvm14.png)

## <a name="support-form"></a>Form desteği

Merhaba doldurun **Destek** kişiler şirketinizden desteğiyle formu. Bu bilgileri, kişiler ve müşteri destek ilgili kişisi mühendislik.

## <a name="publish-an-offer"></a>Bir teklifi yayımlama

Tüm hello bölümleri doldurduktan sonra seçin **Yayımla** , teklif kullanılabilir toocustomers yapar toostart hello işlemi.

## <a name="next-steps"></a>Sonraki adımlar

* Bir giriş toomanaged uygulamalar için bkz [yönetilen uygulama genel bakış](managed-application-overview.md).
* Merhaba Market yönetilen bir uygulamadan kullanma hakkında daha fazla bilgi için bkz: [tüketen Azure hello Market uygulamalarda yönetilen](managed-application-consume-marketplace.md).
* Hizmet Kataloğu yönetilen uygulama yayımlama hakkında daha fazla bilgi için bkz: [oluşturma ve bir hizmet Kataloğu yönetilen uygulamayı yayımlayın](managed-application-publishing.md).
* Hizmet Kataloğu yönetilen uygulama kullanma hakkında daha fazla bilgi için bkz: [bir hizmet Kataloğu yönetilen uygulama tüketen](managed-application-consumption.md).
