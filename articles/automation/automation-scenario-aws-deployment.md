---
title: "Amazon Web Hizmetleri'nde VM'nin dağıtımını aaaAutomating | Microsoft Docs"
description: "Bu makalede gösterilir nasıl toouse bir Amazon Web hizmeti VM'nin Azure Otomasyonu tooautomate oluşturma"
services: automation
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: 
ms.assetid: 1d85c01a-d795-4523-8194-84fc15b53838
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/14/2017
ms.author: tiandert; bwren
ms.openlocfilehash: dd1f3af47d8700ced85a3ee5a406dde1c1311990
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-automation-scenario---provision-an-aws-virtual-machine"></a>Azure Otomasyonu senaryo - bir AWS sanal makine sağlama
Azure Otomasyonu tooprovision Amazon Web hizmeti (AWS) aboneliğinizde bir sanal makine yararlanır ve bu VM – belirli bir ad verin nasıl bu makalede, biz gösterme "Merhaba VM etiketleme" tooas hangi AWS başvuruyor.

## <a name="prerequisites"></a>Ön koşullar
Bu makalede Hello amaçları doğrultusunda, toohave, bir Azure Otomasyonu hesabı ve bir AWS aboneliği gerekir. Bir Azure Otomasyonu hesabının ayarlanması ve AWS aboneliği kimlik bilgilerinizle yapılandırması hakkında daha fazla bilgi için gözden [Amazon Web Hizmetleri ile kimlik doğrulaması yapılandırma](automation-configure-aws-account.md).  Bu hesap oluşturulan veya hello adımları Bu hesapta başvurur devam etmeden önce AWS aboneliği kimlik bilgilerinizle güncellenir.

## <a name="deploy-amazon-web-services-powershell-module"></a>Amazon Web Hizmetleri PowerShell modülü dağıtma
Bizim VM runbook sağlama hello AWS PowerShell modülü toodo çalışmasını özelliğinden yararlanır. AWS aboneliği kimlik bilgilerinizle yapılandırılmış adımları tooadd hello modülü tooyour Otomasyon hesabı aşağıdaki hello gerçekleştirin.  

1. Web tarayıcınızı açın ve toohello gidin [PowerShell Galerisi](http://www.powershellgallery.com/packages/AWSPowerShell/) üzerinde hello tıklatıp **dağıtma tooAzure Otomasyon düğmesi**.<br><br> ![AWS PS modülü içe aktarma](./media/automation-scenario-aws-deployment/powershell-gallery-download-awsmodule.png)
2. Toohello Azure oturum açma sayfasına yönlendirilir ve kimlik doğrulaması sonra yönlendirilmiş toohello Azure Portal olacaktır ve dikey penceresinde aşağıdaki hello ile sunulan.<br><br> ![İçeri aktarma modülü dikey penceresi](./media/automation-scenario-aws-deployment/deploy-aws-powershell-module-parameters.png)
3. Select hello kaynak grubu hello gelen **kaynak grubu** aşağı açılan listesinde ve hello parametreler dikey penceresinde, aşağıdaki bilgilerle hello sağlayın:
   
   * Merhaba gelen **yeni veya var olan Otomasyon hesabı (dize)** aşağı açılan listesinde seçin **varolan**.  
   * Merhaba, **Otomasyon hesabı adı (dize)** kutusuna hello AWS aboneliğinizi hello kimlik bilgilerini içeren bir Otomasyon hesabı hello tam adı yazın.  Adlı bir adanmış hesabı oluşturduysanız, örneğin, **AWSAutomation**, hello kutuya yazın olur.
   * Select hello hello uygun bölgesinden **Otomasyon hesabı konumu** aşağı açılan liste.
4. Gerekli hello bilgi girmeyi tamamladığınızda, tıklatın **oluşturma**.
   
   > [!NOTE]
   > PowerShell modülü Azure Automation'a içeri bu da hello cmdlet'leri ayıklanıyor ve bu etkinlikler kadar görünmez hello modülü içeri aktarma ve hello cmdlet'leri ayıklama tamamen bitirdi. Bu işlem birkaç dakika sürebilir.  
   > <br>
   > 
   > 
5. Hello Azure Portal, 3. adımda başvurulan Automation hesabınızı açın.
6. Tıklatın hello üzerinde **varlıklar** döşeme ve hello **varlıklar** dikey penceresinde, select hello **modülleri** döşeme.
7. Merhaba üzerinde **modülleri** dikey penceresinde hello görürsünüz **AWSPowerShell** modülü hello listesinde.

## <a name="create-aws-deploy-vm-runbook"></a>Oluşturma AWS VM runbook dağıtma
Bir kez AWS PowerShell modülü dağıtılan hello, biz şimdi bir sanal makinede bir PowerShell Betiği kullanılarak AWS sağlama runbook tooautomate yazabilirsiniz. Merhaba adımları nasıl tooleverage yerel PowerShell komut dosyası Azure Otomasyonu'nda gösterilmektedir.  

> [!NOTE]
> Daha fazla seçenekleri ve bu komut dosyası ile ilgili bilgi için lütfen hello adresini ziyaret edin [PowerShell Galerisi](https://www.powershellgallery.com/packages/New-AwsVM/DisplayScript).
> 

1. Merhaba PowerShell Betiği yeni AwsVM bir PowerShell oturumu'ni açıp hello aşağıdakileri yazarak hello PowerShell Galerisi ' indirin:<br>
   ```
   Save-Script -Name New-AwsVM -Path <path>
   ```
   <br>
2. Hello Azure Portal'da, Automation hesabınızı açın ve Başlangıç'ı tıklatın **Runbook'lar** döşeme.  
3. Merhaba gelen **Runbook'lar** dikey penceresinde, select **runbook Ekle**.
4. Merhaba üzerinde **runbook Ekle** dikey penceresinde, select **hızlı Oluştur** (yeni bir runbook oluşturma).
5. Merhaba üzerinde **Runbook** özellikleri dikey penceresinde, bir ad hello adı kutusuna, runbook için ve hello yazın **Runbook türü** aşağı açılan listesinde seçin **PowerShell**ve 'ıtıklatın **Oluşturma**.<br><br> ![İçeri aktarma modülü dikey penceresi](./media/automation-scenario-aws-deployment/runbook-quickcreate-properties.png)
6. Hello PowerShell Runbook'unu Düzenle dikey penceresi görüntülendiğinde, kopyalayıp tuvale yazma hello runbook'a hello PowerShell Betiği yapıştırın.<br><br> ![Runbook PowerShell Betiği](./media/automation-scenario-aws-deployment/runbook-powershell-script.png)<br>
   
    > [!NOTE]
    > Lütfen hello örnek PowerShell komut dosyası ile çalışırken hello aşağıdakileri unutmayın:
    > 
    > * Merhaba runbook varsayılan parametre değerlerini içerir. Lütfen tüm varsayılan değerlerini değerlendirmek ve gerekirse güncelleştirin.
    > * Daha farklı bir kimlik bilgisi varlığı adlı gibi AWS kimlik bilgilerinizi depolanan durumunda **AWScred**, buna göre tooupdate hello komut satırı 57 toomatch gerekir.  
    > * AWS CLI komutlarıyla PowerShell, özellikle bu örnek runbook Hello ile çalışırken, hello AWS bölge belirtmeniz gerekir. Aksi takdirde hello cmdlet'leri başarısız olur.  Görünüm AWS konu [AWS bölge belirtin](http://docs.aws.amazon.com/powershell/latest/userguide/pstools-installing-specifying-region.html) hello AWS araçları PowerShell belge daha fazla bilgi için.  
    >

7. tooretrieve AWS aboneliğiniz görüntü adlarının bir listesini PowerShell ISE başlatın ve hello AWS PowerShell modülünü içeri aktarın.  Değiştirerek karşı AWS kimlik doğrulaması **Get-AutomationPSCredential** ISE ortamınızda **AWScred Get-Credential =**.  Bu kimlik bilgilerinizi ister ve bunu sağlayabilir, **erişim anahtarı kimliği** hello kullanıcı adı için ve **gizli erişim anahtar** hello parolası.  Merhaba örneğe bakın:  

        #Sample tooget hello AWS VM available images
        #Please provide hello path where you have downloaded hello AWS PowerShell module
        Import-Module AWSPowerShell
        $AwsRegion = "us-west-2"
        $AwsCred = Get-Credential
        $AwsAccessKeyId = $AwsCred.UserName
        $AwsSecretKey = $AwsCred.GetNetworkCredential().Password
   
        # Set up hello environment tooaccess AWS
        Set-AwsCredentials -AccessKey $AwsAccessKeyId -SecretKey $AwsSecretKey -StoreAs AWSProfile
        Set-DefaultAWSRegion -Region $AwsRegion
   
        Get-EC2ImageByName -ProfileName AWSProfile

    Merhaba aşağıdaki çıktı döndürülür:<br><br>
   ![AWS görüntüleri alma](./media/automation-scenario-aws-deployment/powershell-ise-output.png)<br>  
8. Kopyalayıp hello hello görüntü adlarından biri hello runbook'taki başvurulan bir Otomasyon değişkeninde **$InstanceType**. Hello kullanarak Biz bu örnekte boş AWS aboneliği katmanlı beri kullanacağız **t2.micro** runbook örneğimizde için.  
9. Merhaba runbook'u kaydedin ve ardından **Yayımla** toopublish hello runbook ardından **Evet** istendiğinde.

### <a name="testing-hello-aws-vm-runbook"></a>Merhaba AWS VM runbook test etme
Sınama hello runbook'la ilerlemeden önce birkaç tooverify gerekiyor. Bu avantajlar şunlardır:  

* AWS karşı kimlik doğrulaması için bir varlık çağrılan oluşturuldu **AWScred** veya hello betik güncelleştirilmiş tooreference hello kimlik bilgisi varlığının adını açıldı.    
* Azure Otomasyonu'nda Hello AWS PowerShell modülünü içeri aktarıldı  
* Yeni bir runbook oluşturulur ve parametre değerlerini doğrulandı ve gerektiğinde güncelleştirildi  
* **Ayrıntılı kayıtları günlüğe** ve isteğe bağlı olarak **oturum ilerleme durumu kayıtlarını** hello runbook ayarı altında **günlüğe kaydetme ve izleme** çok ayarlamak**üzerinde**.<br><br> ![Runbook günlüğü ve izleme](./media/automation-scenario-aws-deployment/runbook-settings-logging-and-tracing.png)  

1. Toostart hello runbook istediğiniz, bu nedenle tıklatın **Başlat** ve ardından **Tamam** zaman hello Runbook'u Başlat dikey pencere açılır.
2. Merhaba Runbook'u Başlat dikey penceresinde sağlayan bir **VMname**.  Merhaba Hello varsayılan değerleri hello komut dosyasında daha önce yapılandırılmış diğer parametreleri kabul eder.  Tıklatın **Tamam** toostart hello runbook işi.<br><br> ![Yeni AwsVM runbook başlatın](./media/automation-scenario-aws-deployment/runbook-start-job-parameters.png)
3. Yeni oluşturduğumuz hello runbook işi için bir iş bölmesi açıldı. Bu bölmesini kapatın.
4. Biz hello iş ve görünüm çıkış ilerlemesini görüntülemek **akışları** hello seçerek **tüm günlükleri** döşeme hello runbook işi dikey penceresinden.<br><br> ![Akış çıkışı](./media/automation-scenario-aws-deployment/runbook-job-streams-output.png)
5. VM sağlanmakta, tooconfirm hello günlüğüne hello AWS Yönetim Konsolu, şu anda oturum açmış değil.<br><br> ![AWS Konsolu VM dağıtılan](./media/automation-scenario-aws-deployment/aws-instances-status.png)

## <a name="next-steps"></a>Sonraki adımlar
* Grafik runbook'ları ile çalışmaya tooget bakın [ilk grafik runbook Uygulamam](automation-first-runbook-graphical.md)
* PowerShell iş akışı runbook'ları ile başlatılan tooget bakın [ilk PowerShell iş akışı runbook Uygulamam](automation-first-runbook-textual.md)
* runbook türleri, avantajları ve sınırlamaları, hakkında daha fazla tooknow bakın [Azure Automation runbook türleri](automation-runbook-types.md)
* PowerShell betik desteği özelliği hakkında daha fazla bilgi için bkz. [Azure Automation’da Yerel PowerShell betik desteği](https://azure.microsoft.com/blog/announcing-powershell-script-support-azure-automation-2/)

