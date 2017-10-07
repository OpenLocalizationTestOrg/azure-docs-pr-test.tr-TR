---
title: "aaaUse PowerShell tooget Azure Data Lake Store ile çalışmaya | Microsoft Docs"
description: "Temel işlemleri gerçekleştirmek ve Azure PowerShell toocreate bir Data Lake Store hesabı kullanın"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: bf85f369-f9aa-4ca1-9ae7-e03a78eb7290
ms.service: data-lake-store
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/29/2017
ms.author: nitinme
ms.openlocfilehash: 9c958bfd63e412ec0b0a4113a149f61aee026bc4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-data-lake-store-using-azure-powershell"></a>Azure PowerShell'i kullanarak Azure Data Lake Store ile çalışmaya başlama
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

Bir Azure Data Lake toouse Azure PowerShell toocreate nasıl depolamak öğrenin hesap ve gibi klasör oluşturma karşıya yükleme ve veri dosyalarını indirme temel işlemleri gerçekleştirmek, vb., hesabınızı silme. Data Lake Store hakkında daha fazla bilgi için bkz. [Data Lake Store'a Genel Bakış](data-lake-store-overview.md).

## <a name="prerequisites"></a>Ön koşullar
Bu öğreticiye başlamadan önce hello şunlara sahip olmanız gerekir:

* **Bir Azure aboneliği**. Bkz. [Azure ücretsiz deneme sürümü alma](https://azure.microsoft.com/pricing/free-trial/).
* **Azure PowerShell 1.0 veya üstü**. Bkz: [nasıl tooinstall Azure PowerShell'i ve yapılandırma](/powershell/azure/overview).

## <a name="authentication"></a>Kimlik Doğrulaması
Bu makalede Azure hesabı kimlik bilgileriniz istendiğinde tooenter nerede Data Lake Store ile basit bir kimlik doğrulama yaklaşım kullanır. Merhaba erişim düzeyi tooData Lake Store hesabı ve dosya sistemi, kullanıcı oturum hello hello erişim düzeyi sonra tabidir. Ancak, diğer yaklaşım vardır Data Lake Store ile iyi tooauthenticate olarak olan **son kullanıcı kimlik doğrulaması** veya **hizmeti için kimlik doğrulama**. Yönergeler ve hakkında daha fazla bilgi için tooauthenticate, bkz: [son kullanıcı kimlik doğrulaması](data-lake-store-end-user-authenticate-using-active-directory.md) veya [hizmeti için kimlik doğrulama](data-lake-store-authenticate-using-active-directory.md).

## <a name="create-an-azure-data-lake-store-account"></a>Azure Data Lake Store hesabı oluşturma
1. Masaüstünüzde yeni bir Windows PowerShell penceresi açın ve aşağıdaki kod parçacığında toolog tooyour Azure hesabı içinde hello girin, hello aboneliği ayarlamak ve hello Data Lake Store sağlayıcısını kaydetmek. ' De, istendiğinde toolog emin yaptığınızda, bir hello Abonelik Yöneticisi/sahibi oturum açın:

        # Log in tooyour Azure account
        Login-AzureRmAccount

        # List all hello subscriptions associated tooyour account
        Get-AzureRmSubscription

        # Select a subscription
        Set-AzureRmContext -SubscriptionId <subscription ID>

        # Register for Azure Data Lake Store
        Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.DataLakeStore"
2. Azure Data Lake Store hesabı, bir Azure Kaynak Grubu ile ilişkilidir. Azure Kaynak Grubu oluşturma işlemiyle başlayın.

        $resourceGroupName = "<your new resource group name>"
        New-AzureRmResourceGroup -Name $resourceGroupName -Location "East US 2"

    ![Bir Azure kaynak grubu oluşturma](./media/data-lake-store-get-started-powershell/ADL.PS.CreateResourceGroup.png "Create an Azure Resource Group")
3. Bir Azure Data Lake Store hesabı oluşturun. Belirttiğiniz hello adı yalnızca küçük harf ve sayı içermelidir.

        $dataLakeStoreName = "<your new Data Lake Store name>"
        New-AzureRmDataLakeStoreAccount -ResourceGroupName $resourceGroupName -Name $dataLakeStoreName -Location "East US 2"

    ![Azure Data Lake Store hesabı oluşturma](./media/data-lake-store-get-started-powershell/ADL.PS.CreateADLAcc.png "Create an Azure Data Lake Store account")
4. Merhaba hesabın başarıyla oluşturulduğunu doğrulayın.

        Test-AzureRmDataLakeStoreAccount -Name $dataLakeStoreName

    Bu olmalıdır çıktısı hello **doğru**.

## <a name="create-directory-structures-in-your-azure-data-lake-store"></a>Azure Data Lake Store'unuzda dizin yapıları oluşturma
Dizin, Azure Data Lake Store hesabı toomanage altında oluşturmak ve verileri depolamak.

1. Bir kök dizin belirtin.

        $myrootdir = "/"
2. Adlı yeni bir dizin oluşturun **mynewdirectory** hello belirtilen kök altında.

        New-AzureRmDataLakeStoreItem -Folder -AccountName $dataLakeStoreName -Path $myrootdir/mynewdirectory
3. Bu hello yeni bir dizin başarıyla oluşturuldu doğrulayın.

        Get-AzureRmDataLakeStoreChildItem -AccountName $dataLakeStoreName -Path $myrootdir

    Merhaba aşağıdaki gibi bir çıktı göstermesi gerekir:

    ![Dizin Doğrulama](./media/data-lake-store-get-started-powershell/ADL.PS.Verify.Dir.Creation.png "Verify Directory")

## <a name="upload-data-tooyour-azure-data-lake-store"></a>Veri tooyour Azure Data Lake Store karşıya yükle
Merhaba hesap içinde oluşturduğunuz doğrudan hello kök düzeyinde veya tooa dizininde tooData data Lake Store karşıya yükleyebilirsiniz. Merhaba parçacıkları göstermek nasıl tooupload bazı örnek veri toohello dizini (**mynewdirectory**) hello önceki bölümde oluşturduğunuz.

Bazı örnek veri tooupload için arıyorsanız, hello alabilirsiniz **Ambulance Data** hello klasöründen [Azure Data Lake Git deposu](https://github.com/MicrosoftBigData/usql/tree/master/Examples/Samples/Data/AmbulanceData). Merhaba dosyasını indirin ve C:\sampledata\ gibi bilgisayarınızdaki yerel bir klasörde saklayın.

    Import-AzureRmDataLakeStoreItem -AccountName $dataLakeStoreName -Path "C:\sampledata\vehicle1_09142014.csv" -Destination $myrootdir\mynewdirectory\vehicle1_09142014.csv


## <a name="rename-download-and-delete-data-from-your-data-lake-store"></a>Data Lake Store'unuzda verileri yeniden adlandırma, indirme ve silme
toorename bir dosya hello aşağıdaki komutu kullanın:

    Move-AzureRmDataLakeStoreItem -AccountName $dataLakeStoreName -Path $myrootdir\mynewdirectory\vehicle1_09142014.csv -Destination $myrootdir\mynewdirectory\vehicle1_09142014_Copy.csv

toodownload bir dosya hello aşağıdaki komutu kullanın:

    Export-AzureRmDataLakeStoreItem -AccountName $dataLakeStoreName -Path $myrootdir\mynewdirectory\vehicle1_09142014_Copy.csv -Destination "C:\sampledata\vehicle1_09142014_Copy.csv"

toodelete bir dosya hello aşağıdaki komutu kullanın:

    Remove-AzureRmDataLakeStoreItem -AccountName $dataLakeStoreName -Paths $myrootdir\mynewdirectory\vehicle1_09142014_Copy.csv

İstendiğinde, girin **Y** toodelete hello öğesi. Birden fazla dosya toodelete varsa, tüm hello yollarının virgülle ayırarak sağlayabilir.

    Remove-AzureRmDataLakeStoreItem -AccountName $dataLakeStoreName -Paths $myrootdir\mynewdirectory\vehicle1_09142014.csv, $myrootdir\mynewdirectoryvehicle1_09142014_Copy.csv

## <a name="delete-your-azure-data-lake-store-account"></a>Azure Data Lake Store hesabınızı silme
Komut toodelete aşağıdaki hello Data Lake Store hesabınızı kullanın.

    Remove-AzureRmDataLakeStoreAccount -Name $dataLakeStoreName

İstendiğinde, girin **Y** toodelete hello hesabı.

## <a name="performance-guidance-while-using-powershell"></a>PowerShell’i kullanırken performans rehberi

Aşağıda hello PowerShell toowork Data Lake Store ile kullanırken bizi tooget hello en iyi performans olabilir en önemli ayarlar şunlardır:

| Özellik            | Varsayılan | Açıklama |
|---------------------|---------|-------------|
| PerFileThreadCount  | 10      | Bu parametre toochoose hello yükleyerek veya her dosya indirme için paralel iş parçacığı sayısını sağlar. Bu sayı, dosya başına ayrılabilen hello en fazla iş parçacığı temsil eder, ancak senaryonuza bağlı olarak daha az iş parçacığı alabilirsiniz (örn. bir 1 KB dosya yüklüyorsanız, 20 iş parçacığı isteyin olsa bile bir iş parçacığı alırsınız).  |
| ConcurrentFileCount | 10      | Bu parametre özellikle klasörlerin karşıya yüklenmesi ve indirilmesi içindir. Bu parametre, karşıya veya karşıdan eşzamanlı dosya hello sayısını belirler. Bu sayı hello karşıya veya aynı anda indirilen eşzamanlı dosyaları en büyük sayısını temsil eder, ancak senaryonuza bağlı olarak daha az eşzamanlılık alabilirsiniz (örneğin iki dosya yüklüyorsanız sorduğunuz olsa bile iki eşzamanlı dosya yüklemeleri alırsınız 15). |

**Örnek**

Bu komut dosyası ve 100 eş zamanlı dosya başına 20 iş parçacığı kullanarak Azure Data Lake Store toohello kullanıcının yerel sürücüden dosyaları indirir.

    Export-AzureRmDataLakeStoreItem -AccountName <Data Lake Store account name> -PerFileThreadCount 20-ConcurrentFileCount 100 -Path /Powershell/100GB/ -Destination C:\Performance\ -Force -Recurse

### <a name="how-do-i-determine-hello-value-tooset-for-these-parameters"></a>Bu parametre için değer tooset hello nasıl belirlerim?

Aşağıda kullanabileceğiniz bazı yönergeler verilmiştir.

* **1. adım: hello toplam iş parçacığı sayısını belirleyin** -tarafından hesaplama hello toplam iş parçacığı sayısı toouse başlamanız gerekir. Genel bir kural olarak her fiziksel çekirdek için 6 iş parçacığı kullanmalısınız.

        Total thread count = total physical cores * 6

    **Örnek**

    Merhaba PowerShell kullanmakta olduğunuz varsayılarak D14 VM'den 16 çekirdeğe sahip komutları.

        Total thread count = 16 cores * 6 = 96 threads


* **2. adım: PerFileThreadCount hesaplamak** -biz hello hello dosya boyutuna göre bizim PerFileThreadCount hesaplanamıyor. 2.5 GB'den küçük dosyalar için var. gerek toochange Bu parametre hello varsayılan olarak 10 yeterli olduğundan 2.5 GB'den büyük olan dosyalar için Hello temeli ilk 2,5 GB hello ve dosya boyutu 1 iş parçacığı her ek 256 MB artırmak için ekleme gibi 10 iş parçacığı kullanmanız gerekir. Birçok farklı boyutta dosya içeren bir klasörü kopyalıyorsanız dosyaları benzer dosya boyutları halinde gruplandırmayı göz önünde bulundurun. Dosya boyutlarının benzer olmaması performansın düşmesine neden olabilir. Bu olası toogroup benzer dosya boyutları değilse, hello en büyük dosya boyutuna göre PerFileThreadCount ayarlamanız gerekir.

        PerFileThreadCount = 10 threads for hello first 2.5GB + 1 thread for each additional 256MB increase in file size

    **Örnek**

    1 GB too10GB arasında değişen 100 dosyalarınız varsayıldığında, hello olarak en büyük hello 10 GB dosya boyutu hello aşağıdaki gibi okuduğunuz eşitlik için kullanırız.

        PerFileThreadCount = 10 + ((10GB - 2.5GB) / 256MB) = 40 threads

* **3. adım: ConcurrentFilecount hesaplamak** -kullanım hello toplam iş parçacığı sayısı ve PerFileThreadCount toocalculate ConcurrentFileCount göre eşitlik aşağıdaki hello üzerinde.

        Total thread count = PerFileThreadCount * ConcurrentFileCount

    **Örnek**

    Biz kullanmakta olduğunuz hello örneği değerlerine göre

        96 = 40 * ConcurrentFileCount

    Bu nedenle, **ConcurrentFileCount** olan **2.4**, hangi biz çok yuvarlama**2**.

### <a name="further-tuning"></a>Daha fazla ayar

Dosya boyutları toowork ile bir dizi olduğundan ek ayarlama gerektirebilir. iyi tümünü veya bir hello dosyaların en büyük ve daha yakın toohello 10 GB aralık dışındaysa hello hesaplama üstünde çalışır. Bunun yerine çoğu dosya küçük olacak şekilde birçok farklı dosya boyutu varsa PerFileThreadCount değerini azaltabilirsiniz. Merhaba PerFileThreadCount azaltarak ConcurrentFileCount artırabilir. Bu nedenle, bizim hesaplama varsayıyoruz olursa bizim dosyaları hello 5 GB aralığında küçük çoğu, parolanızı yeniden yapın:

    PerFileThreadCount = 10 + ((5GB - 2.5GB) / 256MB) = 20

Bu nedenle, **ConcurrentFileCount** şimdi 4.8 olan 96/20, çok yuvarlanacak**4**.

Merhaba değiştirerek bu ayarları tootune sürdürebilirsiniz **PerFileThreadCount** dosya boyutlarınızı hello dağıtımını bağlı yukarı ve aşağı olarak.

### <a name="limitation"></a>Sınırlama

* **Dosya sayısı, ConcurrentFileCount değerinden**: hello karşıya dosya sayısı hello küçük olup olmadığını **ConcurrentFileCount** hesaplanmış ardından azaltmanız gerekir  **ConcurrentFileCount** toobe eşit toohello dosya sayısı. Kalan tüm iş parçacıklarının tooincrease kullanabileceğiniz **PerFileThreadCount**.

* **Çok fazla iş parçacığı**: iş parçacığı artırırsanız, küme boyutu artırmadan çok fazla sayısı, performans hello riskini çalıştırın. İçerik Geçişi hello CPU üzerinde Çekişme sorunları olabilir.

* **Yetersiz eşzamanlılık**: hello eşzamanlılık yeterli değildir sonra kümenizi çok küçük olabilir. Daha fazla eşzamanlılık erişmenizi sağlayan kümedeki düğüm sayısını hello artırabilir.

* **Azaltma hataları**: Eşzamanlılığınız çok yüksekse azaltma hataları görebilirsiniz. Hataları azaltma görüyorsanız hello eşzamanlılık azaltın veya bize ulaşın.

## <a name="next-steps"></a>Sonraki adımlar
* [Data Lake Store'da verilerin güvenliğini sağlama](data-lake-store-secure-data.md)
* [Azure Data Lake Analytics'i Data Lake Store ile kullanma](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [Azure HDInsight'ı Data Lake Store ile kullanma](data-lake-store-hdinsight-hadoop-use-portal.md)

