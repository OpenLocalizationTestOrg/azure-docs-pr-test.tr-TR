---
title: "Azure portal tooget aaaUse Data Lake Store ile çalışmaya | Microsoft Docs"
description: "Merhaba Data Lake Store temel işlemleri gerçekleştirmek ve Hello Azure portal toocreate bir Data Lake Store hesabı kullanın"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: fea324d0-ad1a-4150-81f0-8682ddb4591c
ms.service: data-lake-store
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/06/2017
ms.author: nitinme
ms.openlocfilehash: 6bb3413f00bfa4393f08aed18bc1d5f8a2f28fc5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-data-lake-store-using-hello-azure-portal"></a>Azure Data Lake hello Azure portal kullanarak Store ile çalışmaya başlama
> [!div class="op_single_selector"]
> * [Portal](data-lake-store-get-started-portal.md)
> * [PowerShell](data-lake-store-get-started-powershell.md)
> * [.NET SDK](data-lake-store-get-started-net-sdk.md)
> * [Java SDK](data-lake-store-get-started-java-sdk.md)
> * [REST API](data-lake-store-get-started-rest-api.md)
> * [Azure CLI 2.0](data-lake-store-get-started-cli-2.0.md)
> * [Node.js](data-lake-store-manage-use-nodejs.md)
> * [Python](data-lake-store-get-started-python.md)
>
> 

Nasıl toouse Azure portal toocreate bir Azure Data Lake Store hesabı hello ve gibi klasör oluşturma karşıya yükleyin ve veri dosyalarını indirme temel işlemleri gerçekleştirmek öğrenin, vb., hesabınızı silme. Daha fazla bilgi için bkz. [Azure Data Lake Store’a Genel Bakış](data-lake-store-overview.md).

iki videoları izleyerek hello içeren bu makalede anlatıldığı gibi aynı bilgileri hello:

* [Data Lake Store hesabı oluşturma](https://mix.office.com/watch/1k1cycy4l4gen)
* [Merhaba Veri Gezgini'ni kullanarak Data Lake Store verileri yönetmek](https://mix.office.com/watch/icletrxrh6pc)

## <a name="prerequisites"></a>Ön koşullar
Bu öğreticiye başlamadan önce aşağıdaki öğelerindeki hello sahip olmanız gerekir:

* **Bir Azure aboneliği**. Bkz. [Azure ücretsiz deneme sürümü alma](https://azure.microsoft.com/pricing/free-trial/).

## <a name="create-an-azure-data-lake-store-account"></a>Azure Data Lake Store hesabı oluşturma

1. Yeni toohello oturum [Azure portal](https://portal.azure.com).
2. **YENİ**'ye, **Veri + Depolama**'ya ve ardından **Azure Data Lake Store**'a tıklayın. Merhaba Hello bilgileri okuyun **Azure Data Lake Store** dikey ve ardından **oluşturma** hello sol alt köşesindeki hello dikey olarak.
3. Merhaba, **yeni Data Lake Store** dikey penceresinde hello ekran aşağıdaki gösterildiği gibi hello değerleri girin:
   
    ![Yeni bir Azure Data Lake Store hesabı oluşturma](./media/data-lake-store-get-started-portal/ADL.Create.New.Account.png "Create a new Azure Data Lake account")
   
   * **Ad**. Merhaba Data Lake Store hesabı için benzersiz bir ad girin.
   * **Abonelik**. Toocreate yeni bir Data Lake Store hesabı altında istediğiniz hello aboneliği seçin.
   * **Kaynak Grubu**. Varolan bir kaynak grubu seçin ya da seçin hello **Yeni Oluştur** seçeneği toocreate biri. Kaynak grubu, bir uygulama için ilgili kaynakları bir arada tutan bir kapsayıcıdır. Daha fazla bilgi için bkz. [Azure'da Kaynak Grupları](../azure-resource-manager/resource-group-overview.md#resource-groups).
   * **Konum**: toocreate hello Data Lake Store hesabı istediğiniz bir konum seçin.
   * **Şifreleme Ayarları**. Üç seçenek vardır:
     
     * **Şifrelemeyi etkinleştirme**.
     * **Azure Data Lake tarafından yönetilen anahtarları kullanma**.  Azure Data Lake Store toomanage şifreleme anahtarlarınızı istiyorsanız.
     * **Azure Key Vault'tan anahtarları seçin**. Mevcut bir Azure Key Vault’u seçin veya yeni bir Key Vault oluşturun. bir anahtar kasası toouse hello anahtarları, hello tooaccess Azure anahtar Kasası'hello Azure Data Lake Store hesabı izinlerini atamanız gerekir. Merhaba yönergeler için bkz: [izinleri tooAzure anahtar kasası atamak](#assign-permissions-to-azure-key-vault).
       
        ![Data Lake Store şifrelemesi](./media/data-lake-store-get-started-portal/adls-encryption-2.png "Data Lake Store encryption")
       
        Tıklatın **Tamam** hello içinde **şifreleme ayarları** dikey.

        Daha fazla bilgi için bkz. [Azure Data Lake Store'da verileri şifreleme](./data-lake-store-encryption.md).

4. **Oluştur**'a tıklayın. Toopin hello hesap toohello Panosu seçerseniz, toohello Pano geri alınır ve Data Lake Store hesabı sağlama hello ilerleme durumunu görebilirsiniz. Bir kez hello hesap dikey penceresi görünür hello Data Lake Store hesabı sağlanır.

İsterseniz Azure Resource Manager şablonlarını kullanarak bir Data Lake Store hesabı da oluşturabilirsiniz. Bu şablonlara [Azure Hızlı Başlangıç Şablonları](https://azure.microsoft.com/resources/templates/?term=data+lake+store)’ndan erişebilirsiniz:

- Veri şifreleme olmadan: [Azure Data Lake Store hesabını veri şifrelemesi olmadan dağıtma](https://azure.microsoft.com/en-us/resources/templates/101-data-lake-store-no-encryption/).
- Data Lake Store kullanarak veri şifrelemesi ile: [Şifreleme (Data Lake) ile Data Lake Store hesabı dağıtma](https://azure.microsoft.com/resources/templates/101-data-lake-store-encryption-adls/).
- Azure Key Vault kullanarak veri şifrelemesi ile: [Şifreleme (Key Vault) ile Data Lake Store hesabı dağıtma](https://azure.microsoft.com/resources/templates/101-data-lake-store-encryption-key-vault/).

### <a name="assign-permissions-to-azure-key-vault"></a>İzinleri tooAzure anahtar kasası atayın
Data Lake Store hesabı hello üzerinde bir Azure anahtar kasası tooconfigure şifreleme anahtarları kullandıysanız, hello Data Lake Store hesabı ve hello Azure anahtar kasası arasında erişim yapılandırmanız gerekir. Adımları toodo şekilde aşağıdaki hello gerçekleştirin.

1. Hello Azure anahtar kasası anahtarlarından kullandıysanız, hello Data Lake Store hesabı dikey penceresinde hello hello üstünde bir uyarı görüntüler. Merhaba uyarı tooopen hello tıklatın **anahtar kasası izinleri yapılandırma** dikey.
   
    ![Data Lake Store şifrelemesi](./media/data-lake-store-get-started-portal/adls-encryption-3.png "Data Lake Store encryption")
2. Merhaba dikey iki seçenekleri tooconfigure erişim gösterir.
   
   * Merhaba ilk seçeneğinde tıklatın **izni** tooconfigure erişim. hello ilk seçenek, yalnızca hello Data Lake Store hesabı oluşturulan hello kullanıcı hello Azure anahtar kasası için bir yönetici ayrıca olduğunda etkindir.
   * Merhaba diğer hello dikey penceresinde görüntülenen toorun hello PowerShell cmdlet'ini bir seçenektir. Azure anahtar kasası hello üzerinde hello özelliği toogrant izinlere sahip veya hello Azure anahtar kasası toobe hello sahibi gerekir. Merhaba cmdlet'ini çalıştırdıktan sonra toohello dikey penceresine geri dönün ve tıklayın **etkinleştirmek** tooconfigure erişim.

## <a name="createfolder"></a>Azure Data Lake Store hesabında klasör oluşturma
Data Lake Store hesabı toomanage altında klasörleri oluşturun ve veri depolayın.

1. Oluşturduğunuz hello Data Lake Store hesabını açın. Hello sol bölmeden tıklatın **Gözat**, tıklatın **Data Lake Store**ve hello hesap adı altında istediğiniz toocreate klasörleri hello Data Lake Store dikey penceresinden'ı tıklatın. Merhaba hesap toohello Sabitle sabitlenmiş varsa, bu hesap kutucuğuna tıklayın.
2. Data Lake Store hesabı dikey pencerenizde, **Veri Gezgini**'ne tıklayın.
   
    ![Data Lake Store hesabında klasör oluşturma](./media/data-lake-store-get-started-portal/ADL.Create.Folder.png "Create folders in Data Lake Store account")
3. Data Lake Store hesabı dikey penceresinde tıklayın **yeni klasör**hello yeni klasör için bir ad girin ve ardından **Tamam**.
   
    ![Data Lake Store hesabında klasör oluşturma](./media/data-lake-store-get-started-portal/ADL.Folder.Name.png "Create folders in Data Lake Store account")
   
    Yeni oluşturulan hello klasörü hello listelenen **Veri Gezgini** dikey. Herhangi bir düzeye kadar iç içe geçmiş klasörler oluşturabilirsiniz.
   
    ![Data Lake hesabında klasör oluşturma](./media/data-lake-store-get-started-portal/ADL.New.Directory.png "Create folders in Data Lake account")

## <a name="uploaddata"></a>Veri tooAzure Data Lake Store hesabı karşıya yükle
Veri tooan Azure Data Lake Store hesabı hello hesap içinde oluşturduğunuz doğrudan hello kök düzeyinde veya tooa klasöründe karşıya yükleyebilirsiniz. Hello hello hello adımları tooupload dosya tooa alt izleyin ekran, aşağıdaki **Veri Gezgini** dikey. Bu ekran görüntüsünde hello (kırmızı kutu içinde işaretlenmiştir) hello içerik haritalarında gösterilen karşıya yüklenen tooa alt dosyasıdır.

Bazı örnek veri tooupload için arıyorsanız, hello alabilirsiniz **Ambulance Data** hello klasöründen [Azure Data Lake Git deposu](https://github.com/MicrosoftBigData/usql/tree/master/Examples/Samples/Data/AmbulanceData).

![Veri yükleme](./media/data-lake-store-get-started-portal/ADL.New.Upload.File.png "Upload data")

## <a name="properties"></a>Özellikler ve Eylemler hello üzerinde kullanılabilir veriler
Merhaba yeni eklenen dosya tooopen hello tıklatın **özellikleri** dikey. Bu dikey penceresinde hello dosya ve hello dosya üzerinde gerçekleştirebileceğiniz hello Eylemler ile ilişkili hello özellikler kullanılabilir. Ekran aşağıdaki hello hello kırmızı kutusunda vurgulanan Azure Data Lake Store hesabınızda hello tam yolu toofile de kopyalayabilirsiniz:

![Merhaba veri özellikleri](./media/data-lake-store-get-started-portal/ADL.File.Properties.png "hello veri özellikleri")

* Tıklatın **Önizleme** toosee hello tarayıcısından doğrudan hello dosya önizlemesini. Merhaba Önizleme hello biçimi belirtebilirsiniz. Tıklatın **Önizleme**, tıklatın **biçimi** hello içinde **Dosya Önizleme** dikey penceresinde ve hello **dosya önizleme biçimi** dikey penceresinde hello gibi seçenekleri belirtin Satır toodisplay sayı olarak toouse, sınırlayıcı toouse vb. kodlama.
  
  ![Dosya önizleme biçimi](./media/data-lake-store-get-started-portal/ADL.File.Preview.png "File preview format")
* Tıklatın **karşıdan** toodownload hello dosya tooyour bilgisayar.
* Tıklatın **dosyayı yeniden adlandır** toorename hello dosya.
* Tıklatın **dosyasını** toodelete hello dosya.

## <a name="secure-your-data"></a>Verilerinizin güvenliğini sağlama
Azure Active Directory ve erişim denetimini (ACL'ler) kullanarak Azure Data Lake Store hesabınızda depolanan hello verilerin güvenliğini sağlayabilirsiniz. Yönergeler için bkz: toodo [Azure Data Lake Store'da verilerin güvenliğini sağlama](data-lake-store-secure-data.md).

## <a name="delete-azure-data-lake-store-account"></a>Azure Data Lake Store hesabını silme
bir Azure Data Lake Store hesabından, Data Lake Store dikey toodelete tıklatın **silmek**. tooconfirm hello eylem toodelete istediğiniz hello hesabı istendiğinde tooenter hello adı olması. Merhaba hello hesabının adını girin ve ardından **silmek**.

![Data Lake hesabını silme](./media/data-lake-store-get-started-portal/ADL.Delete.Account.png "Delete Data Lake account")

## <a name="next-steps"></a>Sonraki adımlar
* [Data Lake Store'da verilerin güvenliğini sağlama](data-lake-store-secure-data.md)
* [Azure Data Lake Analytics'i Data Lake Store ile kullanma](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [Azure HDInsight'ı Data Lake Store ile kullanma](data-lake-store-hdinsight-hadoop-use-portal.md)
* [Data Lake Store'a ilişkin tanılama günlüklerine erişme](data-lake-store-diagnostic-logs.md)

