---
title: "Azure Site kurtarma aaaAdd Azure Otomasyonu runbook'ları toorecovery planları | Microsoft Docs"
description: "Azure Site Recovery kurtarma planları Azure otomasyonu kullanarak genişletme nasıl yardımcı olabileceğini öğrenin. Kurtarma tooAzure sırasında nasıl toocomplete karmaşık görevleri öğrenin."
services: site-recovery
documentationcenter: 
author: ruturaj
manager: gauravd
editor: 
ms.assetid: ecece14d-5f92-4596-bbaf-5204addb95c2
ms.service: site-recovery
ms.devlang: powershell
ms.tgt_pltfrm: na
ms.topic: article
ms.workload: storage-backup-recovery
ms.date: 06/23/2017
ms.author: ruturajd@microsoft.com
ms.openlocfilehash: 90d517200cec5527e98a0d00da466bace587b70b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="add-azure-automation-runbooks-toorecovery-plans"></a>Azure Otomasyonu runbook'ları toorecovery planları ekleme
Bu makalede, sizi Azure Site Recovery Azure Otomasyonu toohelp ile nasıl tümleşik çalıştığını açıklamak kurtarma planlarınızı genişletir. Kurtarma planları korunan sanal makineleri kurtarma Site Recovery ile düzenleyebilirsiniz. Kurtarma planları çoğaltma tooa ikincil bulut hem çoğaltma tooAzure çalışır. Kurtarma planları de yardımcı hello kurtarma yapmak **tutarlı bir şekilde doğru**, **yinelenebilir**, ve **otomatik**. Azure Otomasyonu ile tümleştirme, VM'ler tooAzure başarısız olursa kurtarma planlarınızı genişletir. Güçlü bir otomatikleştirme görevleri teklif tooexecute runbook'lar kullanabilirsiniz.

Yeni tooAzure Otomasyon varsa, şunları yapabilirsiniz [kaydolun](https://azure.microsoft.com/services/automation/) ve [örnek komut dosyası yükleme](https://azure.microsoft.com/documentation/scripts/). Daha fazla bilgi ve toolearn nasıl kullanarak tooorchestrate kurtarma tooAzure [kurtarma planlarına](https://azure.microsoft.com/blog/?p=166264), bkz: [Azure Site Recovery](https://azure.microsoft.com/services/site-recovery/).

Bu makalede, nasıl Azure Otomasyon çalışma kitabı kurtarma planlarınızı tümleştirebilir açıklanmaktadır. Daha önce el ile müdahale gerekli örnekler tooautomate temel görevleri kullanırız. Biz de nasıl tooconvert çok adımlı kurtarma tooa tek tıklamayla kurtarma eylemi açıklar.

## <a name="customize-hello-recovery-plan"></a>Merhaba kurtarma planını özelleştirin
1. Toohello Git **Site Recovery** kurtarma planı kaynak dikey. Bu örnekte, kurtarma için iki VM'ler eklenen tooit hello kurtarma planına sahip. bir runbook ekleme toobegin tıklatın hello **Özelleştir** sekmesi.

    ![Merhaba Özelleştir düğmesini tıklatın](media/site-recovery-runbook-automation-new/essentials-rp.png)


2. Sağ **Grup 1: Başlangıç**ve ardından **post eylem eklemek**.

    ![Sağ Grup 1: Başlatın ve sonrası eylemi ekleyin](media/site-recovery-runbook-automation-new/customize-rp.png)

3. Tıklatın **bir komut dosyası seçin**.

4. Merhaba üzerinde **güncelleştirme eylem** dikey penceresinde, adı hello betik **Hello World**.

    ![Merhaba güncelleştirme eylem dikey penceresi](media/site-recovery-runbook-automation-new/update-rp.png)

5. Bir Otomasyon hesabı adı girin.
    >[!NOTE]
    > Merhaba Automation hesabı Azure herhangi bir bölgede olabilir. Merhaba Otomasyon hesabı hello olmalıdır hello Azure Site kurtarma kasasıyla aynı abonelik.

6. Otomasyon hesabınızda bir runbook seçin. Bu runbook hello ilk grubunun hello kurtarma işleminden sonra hello kurtarma planının hello yürütme sırasında çalışır hello komut dosyasıdır.

7. toosave hello betik tıklatın **Tamam**. Merhaba betik çok eklenen**Grup 1: sonrası adımları**.

    ![Eylem sonrası Grup 1:Start](media/site-recovery-runbook-automation-new/addedscript-rp.PNG)


## <a name="considerations-for-adding-a-script"></a>Bir komut dosyası eklemek için dikkat edilecek noktalar

* Seçenekler için çok**bir adım silme** veya **güncelleştirme hello betik**, hello komut dosyasını sağ tıklatın.
* Bir komut dosyası Azure üzerinde bir şirket içi makineyi tooAzure yük devretme sırasında çalıştırabilirsiniz. Ayrıca Azure üzerinde bir birincil site komut dosyası kapatma önce olarak Azure tooan şirket içi makineden yeniden çalışma sırasında çalıştırabilirsiniz.
* Bir komut dosyası çalıştığında, bir kurtarma planı içeriği yerleştirir. Aşağıdaki örnek hello bir bağlam değişkeni gösterir:

    ```
            {"RecoveryPlanName":"hrweb-recovery",

            "FailoverType":"Test",

            "FailoverDirection":"PrimaryToSecondary",

            "GroupId":"1",

            "VmMap":{"7a1069c6-c1d6-49c5-8c5d-33bfce8dd183":

                    { "SubscriptionId":"7a1111111-c1d6-49c5-8c5d-111ce8dd183",

                    "ResourceGroupName":"ContosoRG",

                    "CloudServiceName":"pod02hrweb-Chicago-test",

                    "RoleName":"Fabrikam-Hrweb-frontend-test",

                    "RecoveryPointId":"TimeStamp"}

                    }

            }
    ```

    Aşağıdaki tablonun hello hello adını ve her bir değişken hello bağlamda açıklamasını listeler.

    | **Değişken adı** | **Açıklama** |
    | --- | --- |
    | RecoveryPlanName |çalıştırılan hello planının Hello adı. Bu değişken, hello kurtarma planı adına göre farklı eylemleri yardımcı olur. Ayrıca hello betiği yeniden kullanabilirsiniz. |
    | FailoverType |Merhaba yük devretme testi olup olmadığını belirtir, planlı veya plansız. |
    | FailoverDirection |Kurtarma tooa birincil veya ikincil site olup olmadığını belirtir. |
    | GroupID |Merhaba planı çalıştırırken hello Grup numarası hello kurtarma planında tanımlar. |
    | VmMap |Merhaba grubundaki tüm sanal makineleri bir dizi. |
    | VMMap anahtarı |Her VM için benzersiz anahtar (GUID). Aynı Azure Virtual Machine Manager (VMM) Kimliğini Merhaba, hello uygunsa VM hello. |
    | SubscriptionId |hello Azure abonelik kimliği, VM hello oluşturuldu. |
    | Rol adı |Merhaba kurtarılmakta olan Azure VM Hello adı. |
    | CloudServiceName |hello Azure bulut hizmeti adı altında VM hello oluşturuldu. |
    | resourceGroupName|hello Azure kaynak grubu adı altında VM hello oluşturuldu. |
    | Recoverypointıd|Merhaba VM zaman kurtarılan için hello zaman damgası. |

* Bu Otomasyon hesabı hello modülleri aşağıdaki hello sahip emin olun:
    * AzureRM.profile
    * AzureRM.Resources
    * AzureRM.Automation
    * AzureRM.Network
    * AzureRM.Compute

Tüm modüllerin uyumlu sürümlerini olmalıdır. Tüm modüllerin uyumlu bir kolay bir yolu tooensure toouse hello en son sürümlerini hello olan tüm modülleri ' dir.

### <a name="access-all-vms-of-hello-vmmap-in-a-loop"></a>Merhaba VMMap döngü tüm Vm'leri erişim
Kod tooloop hello Microsoft VMMap tüm VM'ler üzerindeki aşağıdaki hello kullan:

```
$VMinfo = $RecoveryPlanContext.VmMap | Get-Member | Where-Object MemberType -EQ NoteProperty | select -ExpandProperty Name
$vmMap = $RecoveryPlanContext.VmMap
 foreach($VMID in $VMinfo)
 {
     $VM = $vmMap.$VMID                
             if( !(($VM -eq $Null) -Or ($VM.ResourceGroupName -eq $Null) -Or ($VM.RoleName -eq $Null))) {
         #this check is tooensure that we skip when some data is not available else it will fail
 Write-output "Resource group name ", $VM.ResourceGroupName
 Write-output "Rolename " = $VM.RoleName
     }
 }

```

> [!NOTE]
> Merhaba betik bir ön eylem tooa önyükleme Grup olduğunda hello kaynak grubu adı ve rol adı değeri boş. Merhaba, o grubun VM yük devretme kümesinde yalnızca başarılı olursa hello değerleri doldurulur. Merhaba betik hello önyükleme grubunun sonrası bir işlemdir.

## <a name="use-hello-same-automation-runbook-in-multiple-recovery-plans"></a>Kullanım hello aynı Otomasyon runbook'ta birden çok kurtarma planları

Dış değişkenler kullanarak birden çok kurtarma planları tek bir komut dosyası kullanabilirsiniz. Kullanabileceğiniz [Azure Otomasyon değişkenleri](../automation/automation-variables.md) için bir kurtarma geçirebilirsiniz toostore parametreleri yürütme planlayın. Merhaba kurtarma planı adı öneki toohello değişken olarak ekleyerek, her kurtarma planı için bağımsız değişkenleri oluşturabilirsiniz. Ardından, hello değişkenleri olarak parametreler kullanın. Merhaba betik değiştirmeden bir parametre değiştirebilirsiniz, ancak hala değişiklik hello şekilde hello betik çalışır.

### <a name="use-a-simple-string-variable-in-a-runbook-script"></a>Basit bir dize değişkeni bir runbook komut dosyası kullanın

Bu örnekte, bir komut dosyası hello girdi bir ağ güvenlik grubu (NSG) alır ve bir kurtarma planı toohello Vm'leri uygular.

Hangi kurtarma planı çalıştıran hello betik toodetect için hello kurtarma planı bağlam kullanın:

```
workflow AddPublicIPAndNSG {
    param (
          [parameter(Mandatory=$false)]
          [Object]$RecoveryPlanContext
    )

    $RPName = $RecoveryPlanContext.RecoveryPlanName
```

Varolan bir NSG tooapply, hello NSG adını ve hello NSG kaynak grubu adını bilmeniz gerekir. Bu değişkenler kurtarma planı komut için giriş olarak kullanın. toodo Bu, iki değişken hello Otomasyon hesabı varlıklar oluşturun. Bir önek toohello değişken adı olacak şekilde hello parametrelerini oluşturmakta olduğunuz hello kurtarma planı Hello adını ekleyin.

1. Bir değişken toostore hello NSG adı oluşturun. Merhaba kurtarma planı hello adını kullanarak bir önek toohello değişken adı ekleyin.

    ![Bir NSG adı değişkeni oluşturun](media/site-recovery-runbook-automation-new/var1.png)

2. Değişken toostore hello NSG'ın bir kaynak grubu adı oluşturun. Merhaba kurtarma planı hello adını kullanarak bir önek toohello değişken adı ekleyin.

    ![Bir NSG kaynak grubu adı oluşturma](media/site-recovery-runbook-automation-new/var2.png)


3.  Merhaba komut dosyasında başvuru kodu tooget hello değişken değerleri aşağıdaki hello kullanın:

    ```
    $NSGValue = $RecoveryPlanContext.RecoveryPlanName + "-NSG"
    $NSGRGValue = $RecoveryPlanContext.RecoveryPlanName + "-NSGRG"

    $NSGnameVar = Get-AutomationVariable -Name $NSGValue
    $RGnameVar = Get-AutomationVariable -Name $NSGRGValue
    ```

4.  Merhaba runbook tooapply hello NSG toohello ağ arabiriminin hello kullan hello değişkenleri başarısız oldu-VM üzerinde:

    ```
    InlineScript {
    if (($Using:NSGname -ne $Null) -And ($Using:NSGRGname -ne $Null)) {
            $NSG = Get-AzureRmNetworkSecurityGroup -Name $Using:NSGname -ResourceGroupName $Using:NSGRGname
            Write-output $NSG.Id
            #Apply hello NSG tooa network interface
            #$vnet = Get-AzureRmVirtualNetwork -ResourceGroupName TestRG -Name TestVNet
            #Set-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name FrontEnd `
            #  -AddressPrefix 192.168.1.0/24 -NetworkSecurityGroup $NSG
        }
    }
    ```

Her kurtarma planı için bağımsız değişkenleri oluşturun, böylece hello betiği yeniden kullanabilirsiniz. Merhaba kurtarma planı adı kullanarak bir önek ekleyin. Bir tam, uçtan uca komut dosyası için bu senaryo için bkz: [bir Site Recovery kurtarma planı test yük devretmesi sırasında genel bir IP ve NSG tooVMs eklemek](https://gallery.technet.microsoft.com/Add-Public-IP-and-NSG-to-a6bb8fee).


### <a name="use-a-complex-variable-toostore-more-information"></a>Daha fazla bilgi karmaşık değişkeni toostore kullanın

Genel IP belirli vm'lerde üzerinde tek bir komut dosyası tooturn istediğiniz bir senaryo düşünün. Başka bir senaryoda tooapply isteyebilirsiniz farklı Nsg'leri farklı vm'lerde (değil, tüm VM'ler). Herhangi bir kurtarma planı için yeniden kullanılabilir bir komut dosyası yapabilirsiniz. Her kurtarma planı VM'ler değişken sayıda olabilir. Örneğin, bir SharePoint kurtarma iki ön ucu vardır. Bir temel çizgi iş kolu (LOB) uygulaması yalnızca bir ön uç vardır. Her kurtarma planı için ayrı değişkenler oluşturamaz. 

Merhaba, aşağıdaki örnek, yeni bir teknik kullanır ve oluşturma bir [karmaşık değişkeni](https://msdn.microsoft.com/library/dn913767.aspx?f=255&MSPPError=-2147217396) hello Azure Otomasyon hesabı varlıkları içinde. Bunun için birden çok değer belirterek. Azure PowerShell toocomplete hello aşağıdaki adımları kullanmanız gerekir:

1. PowerShell'de tooyour Azure aboneliği imzalayın:

    ```
    login-azurermaccount
    $sub = Get-AzureRmSubscription -Name <SubscriptionName>
    $sub | Select-AzureRmSubscription
    ```

2. toostore hello parametreleri hello kurtarma planı hello adını kullanarak hello karmaşık değişkeni oluşturun:

    ```
    $VMDetails = @{"VMGUID"=@{"ResourceGroupName"="RGNameOfNSG";"NSGName"="NameOfNSG"};"VMGUID2"=@{"ResourceGroupName"="RGNameOfNSG";"NSGName"="NameOfNSG"}}
        New-AzureRmAutomationVariable -ResourceGroupName <RG of Automation Account> -AutomationAccountName <AA Name> -Name <RecoveryPlanName> -Value $VMDetails -Encrypted $false
    ```

3. Bu karmaşık değişkeninde **VMDetails** VM hello korumalı hello VM kimliği aranır. hello Azure portal tooget hello VM kimliği hello VM özelliklerini görüntüleyin. Merhaba aşağıdaki ekran görüntüsünde iki VM hello ayrıntılarını depolayan bir değişken gösterir:

    ![Merhaba VM kimliği GUID hello olarak kullanın](media/site-recovery-runbook-automation-new/vmguid.png)

4. Runbook'unuzda bu değişkeni kullanın. Merhaba VM GUID hello kurtarma planı bağlamda bulunan belirtilmişse hello NSG hello VM üzerinde geçerlidir:

    ```
    $VMDetailsObj = Get-AutomationVariable -Name $RecoveryPlanContext.RecoveryPlanName
    ```

4. Runbook'unuzda, hello kurtarma planı bağlam hello VM'ler döngü. Merhaba VM var olup olmadığını denetleyin **$VMDetailsObj**. Varsa, erişim hello değişken tooapply hello NSG hello özellikleri:

    ```
        $VMinfo = $RecoveryPlanContext.VmMap | Get-Member | Where-Object MemberType -EQ NoteProperty | select -ExpandProperty Name
        $vmMap = $RecoveryPlanContext.VmMap

        foreach($VMID in $VMinfo) {
            Write-output $VMDetailsObj.value.$VMID

            if ($VMDetailsObj.value.$VMID -ne $Null) { #If hello VM exists in hello context, this will not b Null
                $VM = $vmMap.$VMID
                # Access hello properties of hello variable
                $NSGname = $VMDetailsObj.value.$VMID.'NSGName'
                $NSGRGname = $VMDetailsObj.value.$VMID.'NSGResourceGroupName'

                # Add code tooapply hello NSG properties toohello VM
            }
        }
    ```

Farklı bir kurtarma planları için aynı komut dosyası hello kullanabilirsiniz. Tooa kurtarma planı farklı değişkenlerine karşılık gelen hello değer depolayarak farklı parametreler girin.

## <a name="sample-scripts"></a>Örnek komut dosyaları

toodeploy örnek komut dosyaları tooyour Automation hesabını tıklatın hello **tooAzure dağıtmak** düğmesi.

[![TooAzure dağıtma](https://azurecomcdn.azureedge.net/mediahandler/acomblog/media/Default/blog/c4803408-340e-49e3-9a1f-0ed3f689813d.png)](https://aka.ms/asr-automationrunbooks-deploy)

Video aşağıdaki hello başka bir örnek için bkz. Bunu gösteren nasıl toorecover iki katmanlı WordPress uygulama tooAzure:


> [!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/One-click-failover-of-a-2-tier-WordPress-application-using-Azure-Site-Recovery/player]



## <a name="additional-resources"></a>Ek kaynaklar
* [Azure Otomasyon hizmeti farklı çalıştır hesabı](../automation/automation-sec-configure-azure-runas-account.md)
* [Azure Otomasyonu genel bakış](http://msdn.microsoft.com/library/azure/dn643629.aspx "Azure Otomasyonu genel bakış")
* [Azure Automation örnek betikler](http://gallery.technet.microsoft.com/scriptcenter/site/search?f\[0\].Type=User&f\[0\].Value=SC%20Automation%20Product%20Team&f\[0\].Text=SC%20Automation%20Product%20Team "Azure Automation örnek betikler")
