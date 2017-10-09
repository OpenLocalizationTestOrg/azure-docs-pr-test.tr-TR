---
title: "Azure veri Kataloğu Data Lake Store'da aaaRegister verilerden | Microsoft Docs"
description: "Azure veri Kataloğu'nda Data Lake Store verileri kaydetme"
services: data-lake-store,data-catalog
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 3294d91e-a723-41b5-9eca-ace0ee408a4b
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: 3e895b42cab4ba39d288950763312a243883cbdf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="register-data-from-data-lake-store-in-azure-data-catalog"></a>Azure veri Kataloğu'nda Data Lake Store verileri kaydetme
Bu makalede nasıl toointegrate Azure Data Lake depolamak Azure veri Kataloğu toomake ile bir kuruluş içinde bulunabilir, verilerinizi veri Kataloğu ile tümleştirerek öğreneceksiniz. Veri katalog daha fazla bilgi için bkz: [Azure veri Kataloğu](../data-catalog/data-catalog-what-is-data-catalog.md). Veri Kataloğu, kullanabileceğiniz toounderstand senaryolar görmek [Azure veri Kataloğu genel senaryoları](../data-catalog/data-catalog-common-scenarios.md).

## <a name="prerequisites"></a>Ön koşullar
Bu öğreticiye başlamadan önce hello şunlara sahip olmanız gerekir:

* **Bir Azure aboneliği**. Bkz. [Azure ücretsiz deneme sürümü alma](https://azure.microsoft.com/pricing/free-trial/).
* **Azure aboneliğinizi etkinleştirme** Data Lake Store genel önizlemesi için. Bkz. [yönergeler](data-lake-store-get-started-portal.md).
* **Azure Data Lake Store hesabı**. Merhaba yönergeleri izleyin [Azure Data Lake hello Azure Portal kullanarak Store ile çalışmaya başlama](data-lake-store-get-started-portal.md). Bu öğretici için bize adlı bir Data Lake Store hesabı oluşturmak **datacatalogstore**.

    Merhaba hesabı oluşturduktan sonra bir örnek veri kümesi tooit karşıya yükleyin. Bu öğretici için bize hello altındaki tüm hello .csv dosyaları karşıya **AmbulanceData** hello klasöründe [Azure Data Lake Git deposu](https://github.com/Azure/usql/tree/master/Examples/Samples/Data/AmbulanceData/). Çeşitli istemciler gibi kullanabilir [Azure Storage Gezgini](http://storageexplorer.com/), tooupload veri tooa blob kapsayıcısı.
* **Azure veri Kataloğu**. Kuruluşunuz zaten bir Azure veri Kataloğu, kuruluşunuz için oluşturulmuş olması gerekir. Yalnızca bir katalog her kuruluş için izin verilir.

## <a name="register-data-lake-store-as-a-source-for-data-catalog"></a>Veri kataloğu için bir kaynak olarak kayıt Data Lake Store

> [!VIDEO https://channel9.msdn.com/Series/AzureDataLake/ADCwithADL/player]

1. Çok Git`https://azure.microsoft.com/services/data-catalog`, tıklatıp **başlama**.
2. Hello Azure veri Kataloğu portalında oturum öğesini tıklatıp **veri yayımlama**.

    ![Veri kaynağını kaydetme](./media/data-lake-store-with-data-catalog/register-data-source.png "veri kaynağını kaydetme")
3. Merhaba sonraki sayfasında, tıklatın **uygulama Başlat**. Bu hello uygulama bildirim dosyasının, bilgisayarınıza yükleyecek. Merhaba bildirim dosyası toostart hello uygulamasını çift tıklatın.
4. Merhaba Hoş Geldiniz sayfasında, tıklatın **oturum**ve kimlik bilgilerinizi girin.

    ![Hoş Geldiniz ekranı](./media/data-lake-store-with-data-catalog/welcome.screen.png "Hoş Geldiniz ekranı")
5. Hello seçin bir veri kaynağı sayfasında, seçin **Azure Data Lake**ve ardından **sonraki**.

    ![Veri kaynağı seçme](./media/data-lake-store-with-data-catalog/select-source.png "veri kaynağını seçin")
6. Merhaba sonraki sayfada hello tooregister veri Kataloğu'nda istediğiniz Data Lake Store hesabı adını sağlayın. Bırakın hello diğer seçenekleri varsayılan olarak ve ardından **Bağlan**.

    ![Connect toodata kaynak](./media/data-lake-store-with-data-catalog/connect-to-source.png "Bağlan toodata kaynağı")
7. Merhaba sonraki sayfaya kesimleri aşağıdaki hello ayrılabilir.

    a. Merhaba **sunucusu hiyerarşisi** kutusunu hello Data Lake Store hesabı klasör yapısını temsil eder. **$Root** temsil hello Data Lake Store hesabı kök ve **AmbulanceData** hello hello hello Data Lake Store hesabı kökünde oluşturulan klasör temsil eder.

    b. Merhaba **kullanılabilir nesneler** kutusu listeler hello altındaki hello dosya ve klasörler **AmbulanceData** klasör.

    c. **Nesneleri toobe kayıtlı kutusunu** listeleri hello dosya ve klasörleri Azure veri Kataloğu'nda tooregister istiyor.

    ![Veri yapısı görüntülemek](./media/data-lake-store-with-data-catalog/view-data-structure.png "görüntülemek veri yapısı")
8. Bu öğretici için tüm hello dosyaları hello dizininde kaydetmelisiniz. Bunun için hello'i tıklatın (![nesneleri taşıma](./media/data-lake-store-with-data-catalog/move-objects.png "nesneleri taşıma")) tüm hello düğmesi toomove dosyaları çok**kayıtlı nesneleri toobe** kutusu.

    Merhaba veri bir kuruluş genelinde veri Kataloğu'nda kayıtlı olması nedeniyle bir maskelenmesi önerilen yaklaşımını tooadd daha sonra kullanabileceğiniz bazı meta veri olan tooquickly hello veri bulun. Örneğin, hello veri sahip (örneğin, kimse hello veri yüklemek) için bir e-posta adresi ekleyin veya bir etiket tooidentify hello veri ekleyin. Aşağıdaki ekran görüntüsünde Hello toohello veri eklediğimiz bir etiket gösterir.

    ![Veri yapısı görüntülemek](./media/data-lake-store-with-data-catalog/view-selected-data-structure.png "görüntülemek veri yapısı")

    Tıklatın **kaydetmek**.
9. Merhaba aşağıdaki ekran yakalama hello veri hello veri Kataloğu başarıyla kaydedildiğini gösterir.

    ![Kayıt tamamlandı](./media/data-lake-store-with-data-catalog/registration-complete.png "görüntülemek veri yapısı")
10. Tıklatın **portalı görüntüle** toogo geri toohello veri Kataloğu portalını ve hello Portalı'ndan veri erişim hello kayıtlı artık açabilir doğrulayın. toosearch hello verileri hello veri kaydedilirken kullanılan hello etiketi kullanabilirsiniz.

     ![Veri Kataloğu'nda arama](./media/data-lake-store-with-data-catalog/search-data-in-catalog.png "veri Kataloğu'nda arama")
11. Şimdi, ek açıklamalar ve belgeleri toohello veri ekleme gibi işlemleri gerçekleştirebilir. Daha fazla bilgi için bağlantılar aşağıdaki hello bakın.

    * [Veri Kataloğu veri kaynaklarına açıklama ekleme](../data-catalog/data-catalog-how-to-annotate.md)
    * [Belge veri kaynakları veri Kataloğu](../data-catalog/data-catalog-how-to-documentation.md)

## <a name="see-also"></a>Ayrıca bkz.
* [Veri Kataloğu veri kaynaklarına açıklama ekleme](../data-catalog/data-catalog-how-to-annotate.md)
* [Belge veri kaynakları veri Kataloğu](../data-catalog/data-catalog-how-to-documentation.md)
* [Data Lake Store diğer Azure hizmetleriyle tümleştirme](data-lake-store-integrate-with-other-services.md)
