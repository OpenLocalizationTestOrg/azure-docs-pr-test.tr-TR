---
title: "Azure kaynak grubu projeleri kullanarak VS Team Services aaaContinuous tümleştirme | Microsoft Docs"
description: "Visual Studio'da Azure kaynak grubu dağıtım kullanarak sürekli tümleştirme Visual Studio Team Services tooset nasıl projeleri açıklar."
services: visual-studio-online
documentationcenter: na
author: mlearned
manager: erickson-doug
editor: 
ms.assetid: b81c172a-be87-4adc-861e-d20b94be9e38
ms.service: azure-resource-manager
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/01/2016
ms.author: mlearned
ms.openlocfilehash: 0fe4a4b8989ee323e8ef2206fa4ebed503025670
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="continuous-integration-in-visual-studio-team-services-using-azure-resource-group-deployment-projects"></a>Azure kaynak grubu dağıtım projeleri kullanarak Visual Studio Team Services sürekli tümleştirme
çeşitli aşamalarda görevleri gerçekleştirmeniz toodeploy bir Azure şablonu,:, Test, yapı kopyalama tooAzure ("Hazırlama" olarak da adlandırılır) ve şablon dağıtma. İki farklı şekilde toodeploy şablonları tooVisual Studio Team Services (VS Team Services) vardır. Yöntemlerin her ikisi de aynı sonuçları hello sağlar, böylece hello iş akışınızı en uygun bir seçin.

1. Hello Azure kaynak grubu dağıtım projesi (dağıtma-AzureResourceGroup.ps1) dahil hello PowerShell Betiği çalıştıran tek adımda tooyour derleme tanımını ekleyin. Hello betik yapıları kopyalar ve ardından hello şablon dağıtır.
2. Birden çok VS Team Services adımlar, her bir aşama görevi gerçekleştirme derleme ekleyin.

Bu makalede her iki seçenek gösterilmektedir. Merhaba ilk seçenek, aynı komut kullanılan hello geliştiriciler tarafından Visual Studio kullanarak ve hello yaşam döngüsü boyunca tutarlılık sağlamak hello avantajına sahiptir. uygun alternatif toohello ile yerleşik bir komut dosyası Hello ikinci seçeneği sunar. Her iki yordamı, VS Team Services içinde kullanıma Visual Studio dağıtım projesi zaten olduğunu varsayın.

## <a name="copy-artifacts-tooazure"></a>Yapıları tooAzure kopyalama
Şablon dağıtımı için gerekli olan herhangi bir yapı varsa hello senaryo bağımsız olarak, Azure Resource Manager erişim toothem vermeniz gerekir. Bu yapıtların dosyaları gibi içerebilir:

* İç içe geçmiş şablonları
* Yapılandırma ve DSC komut dosyaları
* Uygulama ikili dosyaları

### <a name="nested-templates-and-configuration-scripts"></a>İç içe geçmiş şablonları ve yapılandırma betikleri
Visual Studio tarafından sağlanan hello şablonları kullandığınızda (veya Visual Studio parçacıkları ile oluşturulmuş), yalnızca aşamaları hello yapıları hello PowerShell komut dosyası, ayrıca farklı dağıtımları için hello kaynaklar için URI hello parameterizes. Merhaba betik sonra Azure'da hello yapıları tooa güvenli kapsayıcı kopyalar, bu kapsayıcı için bir SaS belirteci oluşturur ve bu bilgiye toohello şablon dağıtımı geçirir. Bkz: [şablon dağıtımı oluşturmak](https://msdn.microsoft.com/library/azure/dn790564.aspx) toolearn hakkında daha fazla bilgi, şablonları iç içe geçmiş.  Görevler VS Team Services içinde kullanırken, şablon dağıtımınız için uygun görevleri hello seçin ve gerekirse, adım toohello şablon dağıtımı hazırlama hello parametre değerlerini geçirin.

## <a name="set-up-continuous-deployment-in-vs-team-services"></a>VS Team Services sürekli dağıtım ayarlayın
toocall hello PowerShell Betiği VS Team Services tooupdate ihtiyacınız derleme tanımı. Kısaca, hello adımlar şunlardır: 

1. Merhaba derleme tanımı düzenleyin.
2. VS Team Services Azure yetkilendirme ayarlayın.
3. Hello Azure kaynak grubu dağıtım projesi hello PowerShell betik başvuruda bulunan bir Azure PowerShell derleme adımı ekleyin.
4. Merhaba hello değerini ayarlamak *- ArtifactsStagingDirectory* parametresi toowork VS Team Services içinde yerleşik bir proje ile.

### <a name="detailed-walkthrough-for-option-1"></a>Seçenek 1 için ayrıntılı kılavuz
Hello aşağıdaki yordamları, VS Team Services projenizde hello PowerShell Betiği çalıştıran tek bir görevi kullanılarak hello adımları gerekli tooconfigure sürekli dağıtım yol. 

1. VS Team Services yapı tanımınızı düzenleyin ve bir Azure PowerShell derleme adımı ekleyin. Merhaba derleme tanımı hello altında seçin **yapı tanımları** kategori ve ardından hello **Düzenle** bağlantı.
   
   ![Yapı tanımı düzenleme][0]
2. Yeni bir ekleme **Azure PowerShell** adım toohello yapı tanımı oluşturun ve ardından hello **derleme adımı Ekle...** tıklayın.
   
   ![Derleme adımı ekleme][1]
3. Merhaba seçin **dağıtma görev** kategori, select hello **Azure PowerShell** görev ve ardından kendi **Ekle** düğmesi.
   
   ![Görev ekleme][2]
4. Merhaba seçin **Azure PowerShell** adım oluşturma ve değerlerini doldurun.
   
   1. Zaten varsa bir Azure hizmet uç noktası tooVS Team Services eklenen, hello abonelik hello seçin **Azure aboneliği** aşağı açılan liste kutusunu ve ardından Atla toohello sonraki bölüm. 
      
      VS Team Services içinde bir Azure hizmet uç noktası yoksa, tooadd biri gerekir. Bu alt bölümde hello işlemi boyunca sürer. Azure hesabınızda bir Microsoft hesabı (örneğin, Hotmail) kullanıyorsa, bir hizmet asıl kimlik doğrulama adımları tooget aşağıdaki hello almanız gerekir.
   2. Merhaba seçin **Yönet** sonraki toohello bağlantı **Azure aboneliği** aşağı açılan liste kutusu.
      
      ![Azure Aboneliklerini yönetmek][3]
   3. Seçin **Azure** hello içinde **yeni hizmet uç noktası** aşağı açılan liste kutusu.
      
      ![Yeni hizmet uç noktası][4]
   4. Merhaba, **Azure aboneliği Ekle** iletişim kutusu, select hello **hizmet sorumlusu** seçeneği.
      
      ![Hizmet asıl seçeneği][5]
   5. Azure abonelik bilgilerini toohello ekleme **Azure aboneliği Ekle** iletişim kutusu. Aşağıdaki öğelerindeki tooprovide hello gerekir:
      
      * Abonelik kimliği
      * Abonelik adı
      * Hizmet sorumlusu kimliği
      * Hizmet sorumlusu anahtarı
      * Kiracı kimliği
   6. Seçim toohello adını eklemek **abonelik** adı kutusu. Bu değer daha sonra hello görünür **Azure aboneliği** VS Team Services aşağı açılan listesinde. 
   7. Azure abonelik Kimliğinizi bilmiyorsanız, aşağıdaki komutları tooretrieve hello birini kullanabilirsiniz.
      
      PowerShell komut dosyaları için kullanın:
      
      `Get-AzureRmSubscription`
      
      Azure CLI için şunu kullanın:
      
      `azure account show`
   8. tooget bir hizmet asıl kimliği hizmet asıl anahtar ve Kiracı kimliği izleyin hello yordamda [oluşturma Active Directory uygulaması ve hizmet sorumlusu portal kullanarak](resource-group-create-service-principal-portal.md) veya [hizmet sorumlusuyla kimlik doğrulaması Azure Resource Manager](resource-group-authenticate-service-principal.md).
   9. Ekle hello hizmet asıl kimliği, hizmet asıl anahtar ve Kiracı kimliği değerleri toohello **Azure aboneliği Ekle** iletişim kutusuna ve ardından hello **Tamam** düğmesi.
      
      Artık geçerli hizmet sorumlusu toouse toorun hello Azure PowerShell komut dosyası vardır.
5. Merhaba derleme tanımı düzenleyin ve hello seçin **Azure PowerShell** adım oluşturma. Hello Hello aboneliği seçin **Azure aboneliği** aşağı açılan liste kutusu. (Merhaba abonelik görünmüyorsa, hello seçin **yenileme** düğmesine bir sonraki hello **Yönet** bağlantıyı.) 
   
   ![Azure PowerShell derleme görevi yapılandırın][8]
6. Yol toohello dağıtma AzureResourceGroup.ps1 PowerShell komut dosyası sağlar. toodo bunu hello üç nokta (...) düğmesini sonraki toohello seçin **betik yolu** kutusunda, hello toohello dağıtma AzureResourceGroup.ps1 PowerShell betik gidin **betikleri** projenizin klasörü seçin, ve ardından hello **Tamam** düğmesi.    
   
   ![Yol tooscript seçin][9]
7. Merhaba betik seçtikten sonra Build.StagingDirectory hello çalışabilmesi hello yolu toohello komut dosyasını güncelleştir (Merhaba aynı dizinde, *ArtifactsLocation* ayarlanır). Bunu "$(Build.StagingDirectory)/" toohello başlangıcı hello betik yolu. ekleyerek yapabilirsiniz
   
    ![Yol tooscript Düzenle][10]
8. Merhaba, **komut dosyası değişkenleri** kutusunda, şu parametreler (tek satırdaki) hello girin. Visual Studio'da hello komut çalıştırdığınızda nasıl VS kullanır hello parametrelerinde hello görebilirsiniz **çıkış** penceresi. Bu yapı adımınız hello parametre değerlerini ayarlamak için bir başlangıç noktası olarak kullanabilirsiniz.
   
   | Parametre | Açıklama |
   | --- | --- |
   | -ResourceGroupLocation |Merhaba hello kaynak grubu bulunduğu, gibi coğrafi konum değeri **eastus** veya **'Doğu ABD'**. (Tek tırnak hello adı bir boşluk ise ekleyin.) Bkz: [Azure bölgeleri](https://azure.microsoft.com/en-us/regions/) daha fazla bilgi için. |
   | -ResourceGroupName |Bu dağıtım için kullanılan hello kaynak grubunun adını Hello. |
   | -UploadArtifacts |Toobe gereken yapıları karşıya varsa, bu parametre belirtir hello yerel sistemden tooAzure. Şablon dağıtımı (örneğin, yapılandırma komut dosyaları veya iç içe geçmiş şablonlarını) hello PowerShell Betiği kullanılarak toostage istediğiniz ek yapıları gerektiriyorsa, bu anahtar yalnızca tooset gerekir. |
   | -StorageAccountName |Bu dağıtım için kullanılan toostage yapıları hello depolama hesabı Hello adı. Yapıtlar dağıtım için hazırlama varsa bu parametre yalnızca kullanılır. Bu parametre belirtilirse hello betik önceki dağıtım sırasında bir oluşturmadı değilse yeni bir depolama hesabı oluşturulur. Merhaba parametresi belirtilirse, hello depolama hesabı önceden var olmalıdır. |
   | -StorageAccountResourceGroupName |Merhaba hello depolama hesabıyla ilişkili hello kaynak grubunun adı. Merhaba StorageAccountName parametresi için bir değer belirtirseniz, bu parametre gereklidir. |
   | -TemplateFile |Merhaba yolu toohello şablon dosyasında hello Azure kaynak grubu dağıtım projesi. tooenhance esneklik, hello mutlak bir yol yerine PowerShell Betiği göreli toohello konumudur Bu parametre için bir yol kullanın. |
   | -TemplateParametersFile |Merhaba yolu toohello Parametreler dosyasında hello Azure kaynak grubu dağıtım projesi. tooenhance esneklik, hello mutlak bir yol yerine PowerShell Betiği göreli toohello konumudur Bu parametre için bir yol kullanın. |
   | -ArtifactStagingDirectory |Bu parametre hello projenin ikili dosyaları nerede kopyalanacağı hello klasörü bilmeniz hello PowerShell komut dosyası sağlar. Bu değer hello PowerShell betiği tarafından kullanılan hello varsayılan değerini geçersiz kılar. VS Team Services kullanmak için başlangıç değeri ayarlayın: - ArtifactStagingDirectory $(Build.StagingDirectory) |
   
   Bir komut bağımsız değişkenleri örneğin (okunabilirlik için ayrılmış çizgi) aşağıdadır:
   
   ```    
   -ResourceGroupName 'MyGroup' -ResourceGroupLocation 'eastus' -TemplateFile '..\templates\azuredeploy.json' 
   -TemplateParametersFile '..\templates\azuredeploy.parameters.json' -UploadArtifacts -StorageAccountName 'mystorageacct' 
   –StorageAccountResourceGroupName 'Default-Storage-EastUS' -ArtifactStagingDirectory '$(Build.StagingDirectory)'    
   ```
   
   İşlemi tamamladığınızda, hello **komut dosyası değişkenleri** kutusu listesi aşağıdaki hello benzer:
   
   ![Betik bağımsız değişkenleri][11]
9. Tüm hello Azure PowerShell derleme adımı gereken öğeleri toohello ekledikten sonra hello seçin **sıra** düğmesini toobuild Merhaba projeyi oluşturun. Merhaba **yapı** ekran hello hello PowerShell Betiği çıktısını gösterir.

### <a name="detailed-walkthrough-for-option-2"></a>Seçenek 2 için ayrıntılı kılavuz
Merhaba aşağıdaki yordamlar, size hello adımları gerekli tooconfigure VS Team Services hello yerleşik görevlerini kullanarak sürekli dağıtım yol.

1. VS Team Services derleme tanımı tooadd iki yeni derleme adımlarınız düzenleyin. Merhaba derleme tanımı hello altında seçin **yapı tanımları** kategori ve ardından hello **Düzenle** bağlantı.
   
   ![Yapı tanımı düzenleme][12]
2. Yeni Ekle hello yapı adımları hello kullanarak toohello derleme tanımı **derleme adımı Ekle...** tıklayın.
   
   ![Derleme adımı ekleme][13]
3. Merhaba seçin **dağıtma** görev kategorisi, select hello **Azure dosya kopyalama** görev ve ardından kendi **Ekle** düğmesi.
   
   ![Azure dosya kopyalama görevi][14]
4. Merhaba seçin **Azure kaynak grubu dağıtımı** görev'ı seçin, **Ekle** düğmesine ve ardından **Kapat** hello **görev katalog**.
   
   ![Azure kaynak grubu dağıtımı görev ekleme][15]
5. Merhaba seçin **Azure dosya kopyalama** görev ve değerlerini doldurun.
   
   Zaten varsa bir Azure hizmet uç noktası tooVS Team Services eklenen, hello abonelik hello seçin **Azure aboneliği** aşağı açılan liste kutusu. Bir abonelik yoksa bkz [seçeneği 1](#detailed-walkthrough-for-option-1) bir VS Team Services içinde ayarlama hakkında yönergeler için.
   
   * Kaynak - girin **$(Build.StagingDirectory)**
   * Azure bağlantı türü - seçin **Azure Resource Manager**
   * Azure RM abonelik - hello toouse istediğiniz hello depolama hesabı için select hello abonelik **Azure aboneliği** aşağı açılan liste kutusu. Merhaba abonelik görünmüyorsa, hello seçin **yenileme** düğmesine bir sonraki hello **Yönet** bağlantı.
   * Hedef türü - seçin **Azure Blob**
   * Merhaba depolama hesabına RM depolama hesabı - seçin yapıları hazırlama için toouse istiyorsunuz
   * Kapsayıcı adı - hello adı girin hello kapsayıcının hazırlama; toouse istiyorsunuz herhangi bir geçerli kapsayıcı adı olabilir ancak bir adanmış toothis derleme tanımı kullanın
   
   Merhaba çıkış değerleri için:
   
   * Depolama kapsayıcısı URI - girin **artifactsLocation**
   * Depolama kapsayıcısı SAS belirteci - girin **artifactsLocationSasToken**
   
   ![Azure dosya kopyalama görevi yapılandırmak][16]
6. Merhaba seçin **Azure kaynak grubu dağıtımı** adım oluşturma ve değerlerini doldurun.
   
   * Azure bağlantı türü - seçin **Azure Resource Manager**
   * Azure RM abonelik - hello dağıtım için select hello abonelik **Azure aboneliği** aşağı açılan liste kutusu. Bu genellikle hello önceki adımda aynı abonelik kullanılan hello olacaktır
   * Eylem - select **oluşturma veya güncelleştirme kaynak grubu**
   * Kaynak grubu - bir kaynak grubu seçin veya hello hello dağıtım için yeni bir kaynak grubu adını girin
   * Konumu - hello kaynak grubu için select hello konumu
   * Şablon - hello yolu ve hello şablon dağıtılan toobe eklenmesini adı girin **$(Build.StagingDirectory)**, örneğin: **$(Build.StagingDirectory/DSC-CI/azuredeploy.json)**
   * Şablon parametreleri - girin hello yolu ve adı kullanıldığında, hello parametreleri toobe eklenmesini **$(Build.StagingDirectory)**, örneğin: **$(Build.StagingDirectory/DSC-CI/azuredeploy.parameters.json)**
   * Şablon parametreleri geçersiz kılma - girin veya kopyalayın ve hello aşağıdaki kodu yapıştırın:
     
     ```    
     -_artifactsLocation $(artifactsLocation) -_artifactsLocationSasToken (ConvertTo-SecureString -String "$(artifactsLocationSasToken)" -AsPlainText -Force)
     ```
     ![Azure kaynak grubu dağıtım görev yapılandırın][17]
7. Tüm gerekli hello öğeleri ekledikten sonra hello derleme tanımını kaydedin ve seçin **sıraya yeni derleme** hello üstünde.

## <a name="next-steps"></a>Sonraki adımlar
Okuma [Azure Resource Manager'a genel bakış](azure-resource-manager/resource-group-overview.md) toolearn Azure Resource Manager ve Azure kaynak grupları hakkında daha fazla bilgi.

[0]: ./media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough1.png
[1]: ./media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough2.png
[2]: ./media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough3.png
[3]: ./media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough4.png
[4]: ./media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough5.png
[5]: ./media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough6.png
[8]: ./media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough9.png
[9]: ./media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough10.png
[10]: ./media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough11b.png
[11]: ./media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough12.png
[12]: ./media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough13.png
[13]: ./media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough14.png
[14]: ./media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough15.png
[15]: ./media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough16.png
[16]: ./media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough17.png
[17]: ./media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough18.png
