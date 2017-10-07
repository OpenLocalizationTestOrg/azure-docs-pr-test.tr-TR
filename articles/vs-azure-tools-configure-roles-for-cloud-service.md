---
title: "aaaConfigure hello rolleri bir Azure için bulut hizmeti Visual Studio ile | Microsoft Docs"
description: "Bilgi nasıl tooset ayarlama ve rolleri Visual Studio kullanarak Azure bulut Hizmetleri için yapılandırın."
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: d397ef87-64e5-401a-aad5-7f83f1022e16
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 03/21/2017
ms.author: kraigb
ms.openlocfilehash: d3c62eb57040ebe987787e73b17b468bb82122bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-azure-cloud-service-roles-with-visual-studio"></a>Azure bulut hizmeti rollerinizi ile Visual Studio'yu yapılandırma
Bir Azure bulut hizmeti bir veya daha fazla çalışan ya da web rolleri olabilir. Her rol için bu rol nasıl ayarlanacağını toodefine gerekir ve ayrıca bu rolü nasıl çalışacağını yapılandırabilirsiniz. Bulut Hizmetleri rolleri hakkında daha fazla toolearn bkz hello video [giriş tooAzure bulut Hizmetleri](https://channel9.msdn.com/Series/Windows-Azure-Cloud-Services-Tutorials/Introduction-to-Windows-Azure-Cloud-Services). 

Merhaba bilgileri bulut hizmetiniz için aşağıdaki dosyaları hello depolanır:

- **ServiceDefinition.csdef** -hello hizmet tanımı dosyası Bulut hizmeti hangi rollerin gerekli dahil olmak üzere, uç noktaları ve sanal makine boyutu hello çalışma zamanı ayarlarını tanımlar. Depolanan hello veri hiçbiri `ServiceDefinition.csdef` rolünüze çalıştırırken değiştirilebilir.
- **ServiceConfiguration.cscfg** - hello hizmet yapılandırma dosyası yapılandırır kaç bir rolün örnekleri çalıştırmak ve hello ayarlarının hello değerleri bir rol için tanımlanan. Merhaba depolanan verileri `ServiceConfiguration.cscfg` rolünüze çalışırken değiştirilebilir.

bir rolü nasıl çalışacağını denetleyen hello ayarlarını toostore farklı değerleri, birden çok hizmet yapılandırması tanımlayabilirsiniz. Her dağıtım ortamı için farklı hizmet yapılandırması kullanabilirsiniz. Örneğin, bir yerel hizmet yapılandırma, depolama hesabı bağlantı dizesi toouse hello yerel Azure storage öykünücüsü belirleyebilir ve başka bir hizmet yapılandırması toouse Azure depolama hello bulutta oluşturun.

Visual Studio'da bir Azure bulut hizmeti oluşturduğunuzda, iki hizmet yapılandırması otomatik olarak oluşturulur ve tooyour Azure projesi eklenir:

- `ServiceConfiguration.Cloud.cscfg`
- `ServiceConfiguration.Local.cscfg`

## <a name="configure-an-azure-cloud-service"></a>Bir Azure bulut hizmeti yapılandırın
Visual Studio'da Çözüm Gezgini'nden bir Azure bulut hizmeti aşağıdaki adımları hello gösterildiği gibi yapılandırabilirsiniz:

1. Oluşturun veya bir Azure bulut hizmeti projesini Visual Studio'da açın.

1. İçinde **Çözüm Gezgini**hello projesine sağ tıklayın ve, hello bağlam menüsünden seçin **özellikleri**.
   
    ![Çözüm Gezgini proje bağlam menüsü](./media/vs-azure-tools-configure-roles-for-cloud-service/solution-explorer-project-context-menu.png)

1. Merhaba Hello projenin Özellikler sayfasında, seçin **geliştirme** sekmesi. 

    ![Proje Özellikleri sayfası - geliştirme sekmesi](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-development-tab.png)

1. Merhaba, **hizmet yapılandırmasını** listesi, tooedit istediğiniz hello hizmet yapılandırmasının select hello adı. (Toomake tooall hello hizmet yapılandırması bu rol için değişiklikler istiyorsanız seçin **tüm yapılandırmaları**.)
   
    > [!IMPORTANT]
    > Belirli hizmet yapılandırmasını seçerseniz, tüm yapılandırmalar için yalnızca ayarlanamadığı için bazı özellikler devre dışı bırakılır. tooedit seçmeniz gerekir, bu özellikler **tüm yapılandırmaları**.
    > 
    > 
   
    ![Bir Azure bulut hizmeti için hizmet yapılandırmasını listesi](./media/vs-azure-tools-configure-roles-for-cloud-service/cloud-service-service-configuration-property.png)

## <a name="change-hello-number-of-role-instances"></a>Merhaba rol örneklerinin sayısını değiştirme
tooimprove hello performansını bulut hizmetinizin Merhaba, kullanıcılar ya da belirli bir rol için beklenen hello yük hello sayısına dayalı olarak çalıştırılan bir rol örneklerinin sayısını değiştirebilirsiniz. Merhaba bulut hizmeti Azure içinde çalıştığında ayrı bir sanal makine rol her örneği için oluşturulur. Bu bulut hizmeti dağıtımının hello hello faturalama etkiler. Faturalama hakkında daha fazla bilgi için bkz: [faturanızı anlamak için Microsoft Azure](billing/billing-understand-your-bill.md).

1. Oluşturun veya bir Azure bulut hizmeti projesini Visual Studio'da açın.

1. İçinde **Çözüm Gezgini**, başlangıç projesi düğümünü genişletin. Merhaba altında **rolleri** düğümü, tooupdate isterseniz ve, hello bağlam menüsünden seçin sağ hello rol **özellikleri**.

    ![Çözüm Gezgini Azure rol bağlam menüsü](./media/vs-azure-tools-configure-roles-for-cloud-service/solution-explorer-azure-role-context-menu.png)

1. Select hello **yapılandırma** sekmesi.

    ![Yapılandırma sekmesi](./media/vs-azure-tools-configure-roles-for-cloud-service/role-configuration-properties-page.png)

1. Merhaba, **hizmet yapılandırmasını** listesi, select hello hizmet yapılandırmasını tooupdate istiyor.
   
    ![Hizmet yapılandırma listesi](./media/vs-azure-tools-configure-roles-for-cloud-service/role-configuration-properties-page-select-configuration.png)

1. Merhaba, **örnek sayısını** metin kutusunda, bu rol için toostart istediğiniz örnekleri hello sayısını girin. Merhaba bulut hizmeti tooAzure yayımladığınızda, her bir örneği farklı bir sanal makinede çalışır.

    ![Güncelleştirme hello örnek sayısı](./media/vs-azure-tools-configure-roles-for-cloud-service/role-configuration-properties-page-instance-count.png)

1. Visual Studio hello gelen araç, select **kaydetmek**.

## <a name="manage-connection-strings-for-storage-accounts"></a>Depolama hesapları için bağlantı dizelerini Yönet
Ekleyin, kaldırın veya bağlantı dizeleri, hizmet yapılandırması için değiştirin. Örneğin, bir yerel bağlantı dizesi değerine sahip bir yerel hizmet yapılandırması için isteyebilirsiniz `UseDevelopmentStorage=true`. Tooconfigure Azure'da bir depolama hesabını kullanan bir bulut hizmeti yapılandırması da isteyebilirsiniz.

> [!WARNING]
> Bir depolama hesabı bağlantı dizesi için hello Azure depolama hesabı anahtar bilgileri girdiğinizde, bu bilgileri yerel olarak hello hizmet yapılandırma dosyasında depolanır. Ancak, bu bilgileri şu anda şifreli metin olarak depolanmaz.
> 
> 

Her hizmet yapılandırması için farklı bir değer kullanarak, değil toouse farklı bağlantı dizeleri, bulut hizmeti olan veya Bulut hizmeti tooAzure yayımladığınızda, kodunuzu değiştirin. Bulut hizmetinizi derlerken veya yayımladığınızda seçin hello hizmet yapılandırmasını temel alarak hello bağlantı dizesinde kodu ve hello değer için aynı adı farklı hello kullanabilirsiniz.

1. Oluşturun veya bir Azure bulut hizmeti projesini Visual Studio'da açın.

1. İçinde **Çözüm Gezgini**, başlangıç projesi düğümünü genişletin. Merhaba altında **rolleri** düğümü, tooupdate isterseniz ve, hello bağlam menüsünden seçin sağ hello rol **özellikleri**.

    ![Çözüm Gezgini Azure rol bağlam menüsü](./media/vs-azure-tools-configure-roles-for-cloud-service/solution-explorer-azure-role-context-menu.png)

1. Select hello **ayarları** sekmesi.

    ![Ayarlar sekmesi](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-settings-tab.png)

1. Merhaba, **hizmet yapılandırmasını** listesi, select hello hizmet yapılandırmasını tooupdate istiyor.

    ![Hizmet yapılandırması](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-settings-tab-select-configuration.png)

1. tooadd bir bağlantı dizesi seçin **ayar Ekle**.

    ![Bağlantı dizesi Ekle](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-settings-tab-add-setting.png)

1. Merhaba yeni ayar toohello listesi eklendikten sonra hello listesindeki hello satır hello gerekli bilgilerle güncelleştirin.

    ![Yeni bağlantı dizesi](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-settings-tab-add-setting-new-setting.png)

    - **Ad** -toouse hello bağlantı dizesi için istediğiniz hello adını girin.
    - **Tür** - seçin **bağlantı dizesi** hello aşağı açılan listeden.
    - **Değer** -hello bağlantı dizesi doğrudan hello girebilirsiniz **değeri** hücre veya select hello üç nokta (...) toowork hello içinde **depolama bağlantı dizesi oluştur** iletişim.  

1. Merhaba, **depolama bağlantı dizesi oluştur** iletişim kutusunda bir seçenek için **bağlanırken**. Ardından, hello seçeneği hello yönergeleri izleyin:

    - **Microsoft Azure storage öykünücüsü** -bu seçeneği seçerseniz, yalnızca tooAzure uygulamak gibi hello kalan ayarları hello iletişim kutusundaki devre dışı bırakılır. **Tamam**’ı seçin.
    - **Aboneliğinizi** - bu seçenek, kullanım hello açılır liste tooeither seçin ve oturum bir Microsoft hesabı seçin ya da bir Microsoft hesabı ekleyin. Bir Azure aboneliği ve depolama hesabı seçin. **Tamam**’ı seçin.
    - **Kimlik bilgileri'el ile girilen** - hello depolama hesabı adı girin ve ya da birincil veya ikinci anahtarı hello. Bir seçenek belirleyin **bağlantı** (HTTPS çoğu senaryolar için önerilir.) **Tamam**’ı seçin.

1. bir bağlantı dizesi toodelete hello bağlantı dizesi seçin ve ardından **Kaldır ayarını**.

1. Visual Studio hello gelen araç, select **kaydetmek**.

## <a name="programmatically-access-a-connection-string"></a>Bir bağlantı dizesi programlamayla erişme

Merhaba aşağıdaki adımlar nasıl tooprogrammatically erişim C# kullanarak bir bağlantı dizesi gösterir.

1. Merhaba aşağıdakileri ekleyin nerede bulacağınızı toouse hello ayarı yönergeleri tooa C# dosyasını kullanarak:

    ```csharp
    using Microsoft.WindowsAzure;
    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.ServiceRuntime;
    ```

1. Merhaba aşağıdaki kod örnek nasıl gösterilmiştir tooaccess bir bağlantı dizesi. Hello yerine &lt;ConnectionStringName > yer tutucu hello uygun değere sahip. 

    ```csharp
    // Setup hello connection tooAzure Storage
    var storageAccount = CloudStorageAccount.Parse(RoleEnvironment.GetConfigurationSettingValue("<ConnectionStringName>"));
    ```

## <a name="add-custom-settings-toouse-in-your-azure-cloud-service"></a>Azure bulut hizmetinize özel ayarları toouse Ekle
Hello hizmet yapılandırma dosyalarında özel ayarlar bir ad ve bir özel hizmet yapılandırması için bir dize değeri eklemenize olanak sağlar. Bir özellik başlangıç değeri okuyarak bulut hizmetinizde hello ayarlama ve bu değer toocontrol hello mantığı kodunuzda kullanarak bu ayarı tooconfigure toouse seçebilirsiniz. Hizmet paketi toorebuild kalmadan veya Bulut hizmetiniz çalıştırırken bu hizmeti yapılandırma değerlerini değiştirebilirsiniz. Kodunuzu bildirimleri için bir ayar değiştiğinde kontrol edebilirsiniz. Bkz: [RoleEnvironment.Changing olay](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.changing.aspx).

Ekleyin, kaldırın veya hizmet yapılandırmalarınızı için özel ayarları değiştirin. Bu dizeler için farklı hizmet yapılandırması için farklı değerler isteyebilirsiniz.

Her hizmet yapılandırması için farklı bir değer kullanarak, değil toouse farklı dizeleri, bulut hizmeti olan veya Bulut hizmeti tooAzure yayımladığınızda, kodunuzu değiştirin. Bulut hizmetinizi derlerken veya yayımladığınızda seçin hello hizmet yapılandırmasını temel alarak, kod ve hello değerindeki hello dizesi için aynı adı farklı hello kullanabilirsiniz.

1. Oluşturun veya bir Azure bulut hizmeti projesini Visual Studio'da açın.

1. İçinde **Çözüm Gezgini**, başlangıç projesi düğümünü genişletin. Merhaba altında **rolleri** düğümü, tooupdate isterseniz ve, hello bağlam menüsünden seçin sağ hello rol **özellikleri**.

    ![Çözüm Gezgini Azure rol bağlam menüsü](./media/vs-azure-tools-configure-roles-for-cloud-service/solution-explorer-azure-role-context-menu.png)

1. Select hello **ayarları** sekmesi.

    ![Ayarlar sekmesi](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-settings-tab.png)

1. Merhaba, **hizmet yapılandırmasını** listesi, select hello hizmet yapılandırmasını tooupdate istiyor.

    ![Hizmet yapılandırma listesi](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-settings-tab-select-configuration.png)

1. tooadd özel bir ayar seçin **ayar Ekle**.

    ![Özel ayar Ekle](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-settings-tab-add-setting.png)

1. Merhaba yeni ayar toohello listesi eklendikten sonra hello listesindeki hello satır hello gerekli bilgilerle güncelleştirin.

    ![Yeni özel ayar](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-settings-tab-add-setting-new-setting.png)

    - **Ad** -hello ayarı hello adını girin.
    - **Tür** - seçin **dize** hello aşağı açılan listeden.
    - **Değer** -hello ayarı hello değeri girin. Merhaba değeri doğrudan hello girebilirsiniz **değeri** hücre veya select hello üç nokta (...) tooenter hello hello değerinde **dize Düzenle** iletişim.  

1. toodelete özel bir ayar hello ayarı seçin ve ardından **Kaldır ayarını**.

1. Visual Studio hello gelen araç, select **kaydetmek**.

## <a name="programmatically-access-a-custom-settings-value"></a>Özel bir ayarın değerini programlamayla erişme
 
Merhaba aşağıdaki adımlar nasıl tooprogrammatically erişim C# kullanarak özel bir ayar gösterir.

1. Merhaba aşağıdakileri ekleyin nerede bulacağınızı toouse hello ayarı yönergeleri tooa C# dosyasını kullanarak:

    ```csharp
    using Microsoft.WindowsAzure;
    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.ServiceRuntime;
    ```

1. Merhaba aşağıdaki kod örnek nasıl gösterilmiştir tooaccess özel bir ayar. Hello yerine &lt;SettingName > yer tutucu hello uygun değere sahip. 
    
    ```csharp
    var settingValue = RoleEnvironment.GetConfigurationSettingValue("<SettingName>");
    ```

## <a name="manage-local-storage-for-each-role-instance"></a>Her rol örneği için yerel depolama yönetin
Her bir rol örneği için yerel dosya sistemi depolama ekleyebilirsiniz. Depolama erişilebilir değil, diğer örnekler için hangi hello veriler hello rolünün tarafından veya diğer rolleri tarafından depolanan hello verileri.  

1. Oluşturun veya bir Azure bulut hizmeti projesini Visual Studio'da açın.

1. İçinde **Çözüm Gezgini**, başlangıç projesi düğümünü genişletin. Merhaba altında **rolleri** düğümü, tooupdate isterseniz ve, hello bağlam menüsünden seçin sağ hello rol **özellikleri**.

    ![Çözüm Gezgini Azure rol bağlam menüsü](./media/vs-azure-tools-configure-roles-for-cloud-service/solution-explorer-azure-role-context-menu.png)

1. Select hello **yerel depolama** sekmesi.

    ![Yerel depolama sekmesi](./media/vs-azure-tools-configure-roles-for-cloud-service/role-local-storage-tab.png)

1. Merhaba, **hizmet yapılandırmasını** listesinde **tüm yapılandırmaları** hello yerel depolama ayarlarını tooall hizmet yapılandırması geçerli olarak seçilen. Başka bir değer devre dışı bırakılıyor hello sayfasında tüm hello giriş alanları sonuçlanır. 

    ![Hizmet yapılandırma listesi](./media/vs-azure-tools-configure-roles-for-cloud-service/role-local-storage-tab-service-configuration.png)

1. tooadd bir yerel depolama girdisi seçin **yerel depolama alanı Ekle**.

    ![Yerel depolama ekleyin](./media/vs-azure-tools-configure-roles-for-cloud-service/role-local-storage-tab-add-local-storage.png)

1. Merhaba yeni yerel depolama girdisi toohello listesi eklendikten sonra hello listesindeki hello satır hello gerekli bilgilerle güncelleştirin.

    ![Yeni yerel depolama girdisi](./media/vs-azure-tools-configure-roles-for-cloud-service/role-local-storage-tab-new-local-storage.png)

    - **Ad** -toouse hello yeni yerel depolama için istediğiniz hello adını girin.
    - **Boyut (MB)** -hello yeni yerel depolama için gereksinim duyduğunuz MB hello boyutu girin.
    - **Rol geri dönüşüm üzerinde temiz** -hello sanal makine hello rol için geri dönüştürüldüğünde hello yeni yerel depolama bu seçeneği tooremove hello verileri seçin.

1. toodelete bir yerel depolama girdisi hello girişi seçin ve ardından **kaldırmak yerel depolama**.

1. Visual Studio hello gelen araç, select **kaydetmek**.

## <a name="programmatically-accessing-local-storage"></a>Program aracılığıyla yerel depolamaya erişme

Bu bölümde nasıl tooprogrammatically erişim kullanarak C# test metin dosyası yazarak yerel depolama anlatılacaktır `MyLocalStorageTest.txt`.  

### <a name="write-a-text-file-toolocal-storage"></a>Bir metin dosyası toolocal depolama yazma

koddan hello nasıl toowrite bir metin dosyası toolocal depolama örneği gösterir. Hello yerine &lt;LocalStorageName > yer tutucu hello uygun değere sahip. 

    ```csharp
    // Retrieve an object that points toohello local storage resource
    LocalResource localResource = RoleEnvironment.GetLocalResource("<LocalStorageName>");
    
    //Define hello file name and path
    string[] paths = { localResource.RootPath, "MyLocalStorageTest.txt" };
    String filePath = Path.Combine(paths);
    
    using (FileStream writeStream = File.Create(filePath))
    {
        Byte[] textToWrite = new UTF8Encoding(true).GetBytes("Testing Web role storage");
        writeStream.Write(textToWrite, 0, textToWrite.Length);
    }

    ```

### <a name="find-a-file-written-toolocal-storage"></a>Toolocal depolama yazılmış bir dosya bulunamadı

Merhaba önceki bölümdeki hello kodu tarafından oluşturulan tooview hello dosyasını aşağıdaki adımları izleyin:
    
1.  Buna Windows bildirim alanındaki hello hello Azure simgesini sağ tıklatın ve, hello bağlam menüsünden seçin **Göster işlem öykünücüsü kullanıcı Arabiriminde**. 

    ![Azure işlem öykünücüsünü Göster](./media/vs-azure-tools-configure-roles-for-cloud-service/show-compute-emulator.png)

1. Merhaba web rolü seçin.

    ![Azure işlem öykünücüsü](./media/vs-azure-tools-configure-roles-for-cloud-service/compute-emulator.png)

1. Merhaba üzerinde **Microsoft Azure işlem öykünücüsü** menüsünde, select **Araçları** > **açık yerel deposu**.

    ![Açık yerel deposu menü öğesi](./media/vs-azure-tools-configure-roles-for-cloud-service/compute-emulator-open-local-store-menu.png)

1. Merhaba Windows Gezgini penceresi açıldığında, girin ' MyLocalStorageTest.txt'' hello içine **arama** metin kutusu ve select **Enter** toostart hello arama. 

## <a name="next-steps"></a>Sonraki adımlar
Visual Studio'da Azure projeler hakkında daha fazla bilgi okuyarak [bir Azure projesi yapılandırma](vs-azure-tools-configuring-an-azure-project.md). Okuyarak hello bulut hizmeti şeması hakkında daha fazla bilgi [şema başvurusu](https://msdn.microsoft.com/library/azure/dd179398).

