---
title: "aaa \"Azure Batch havuzu oluşturma olayı | Microsoft Docs\""
description: "Batch havuzundaki başvurusunu olayı oluşturun."
services: batch
author: tamram
manager: timlt
ms.assetid: 
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 04/20/2017
ms.author: tamram
ms.openlocfilehash: ad31251969af553baa21e8c533d8ea95d3eeaf91
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="pool-create-event"></a>Havuz oluşturma olayı

 Bu olay, bir havuz oluşturulduktan sonra yayınlanır. Merhaba günlük Merhaba içeriğine hello havuzu hakkındaki genel bilgileri açığa çıkarır. Bir havuzu yeniden boyutlandırma başlangıç olay hello havuzunun Hello hedef boyutu 0 işlem düğümleri büyükse, bu olay hemen sonra oluşacak unutmayın.

 Merhaba aşağıdaki örnek hello gövdesi bir havuz oluşturma olayı hello CloudServiceConfiguration özelliği kullanılarak oluşturulan bir havuz için gösterir.

```
{
    "id": "myPool1",
    "displayName": "Production Pool",
    "vmSize": "Small",
    "cloudServiceConfiguration": {
        "osFamily": "3",
        "targetOsVersion": "*"
    },
    "networkConfiguration": {
        "subnetId": " "
    },
    "resizeTimeout": "300000",
    "targetDedicated": 2,
    "maxTasksPerNode": 1,
    "vmFillType": "Spread",
    "enableAutoScale": false,
    "enableInterNodeCommunication": false,
    "isAutoPool": false
}
```

|Öğesi|Tür|Notlar|
|-------------|----------|-----------|
|id|Dize|Merhaba havuzun Hello kimliği.|
|Görünen adı|Dize|Merhaba hello havuzunun adını görüntüler.|
|vmSize|Dize|Merhaba havuzunda hello sanal makinelerin Hello boyutu. Bir havuzdaki tüm sanal makinelerin hello olduğunu aynı boyutta. <br/><br/> Hakkında bilgi için kullanılabilir boyutları sanal makineleri bulut Hizmetleri için havuzları (cloudServiceConfiguration ile oluşturulan havuzlarının), bkz: [Cloud Services boyutları](http://azure.microsoft.com/documentation/articles/cloud-services-sizes-specs/). Toplu işlem dışında tüm Cloud Services VM boyutlarını destekler `ExtraSmall`.<br/><br/> Kullanılabilir VM hakkında bilgi için hello Virtual Machines Market (virtualMachineConfiguration ile oluşturulan havuzlarının) görüntülerden kullanarak havuzları için Boyutlar bkz [sanal makineler için Boyutlar](https://azure.microsoft.com/documentation/articles/virtual-machines-linux-sizes/) (Linux) veya [için boyutları Sanal makineler](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-sizes/) (Windows). Batch `STANDARD_A0` ve premium depolama alanına sahip olanlar (`STANDARD_GS`, `STANDARD_DS` ve `STANDARD_DSV2` serisi) dışında tüm Azure sanal makinelerini destekler.|
|[cloudServiceConfiguration](#bk_csconf)|Karmaşık türü|Merhaba havuzu için Hello bulut hizmeti yapılandırması.|
|[virtualMachineConfiguration](#bk_vmconf)|Karmaşık türü|Merhaba havuzu için Hello sanal makine yapılandırma.|
|[networkConfiguration](#bk_netconf)|Karmaşık türü|Merhaba havuzu Hello ağ yapılandırması.|
|resizeTimeout|Zaman|Merhaba havuzunda hello son yeniden boyutlandırma işlemi için belirtilen işlem düğümleri toohello havuzu ayırma için Hello zaman aşımı.  (Merhaba hello havuzu yeniden boyutlandırma sayıları oluşturulduğunda boyutlandırma ilk.)|
|targetDedicated|Int32|Merhaba hello havuzu için istenen işlem düğümleri sayısı.|
|enableAutoScale|bool|Merhaba havuz boyutu otomatik olarak zaman içinde ayarlar olup olmadığını belirtir.|
|enableInterNodeCommunication|bool|Merhaba havuzu düğümler arasında doğrudan iletişim için ayarlanmış olup olmadığını belirtir.|
|isAutoPool|bool|Speficies hello havuzu bir işin AutoPool mekanizması olup oluşturuldu.|
|maxTasksPerNode|Int32|Merhaba en fazla sayıda hello havuzu tek işlem düğümünde eşzamanlı olarak çalışabilecek görev.|
|vmFillType|Dize|Merhaba toplu işlem hizmetinin görevleri hello havuzdaki işlem düğümleri arasında nasıl dağıtacağını tanımlar. Geçerli değerler paketindeki veya yayılır.|

###  <a name="bk_csconf"></a>cloudServiceConfiguration

|Öğe adı|Tür|Notlar|
|------------------|----------|-----------|
|osFamily|Dize|Merhaba havuzunda hello sanal makinelerde yüklü hello Azure konuk işletim sistemi ailesi toobe.<br /><br /> Olası değerler şunlardır:<br /><br /> **2** – işletim sistemi ailesi 2, eşdeğer tooWindows Server 2008 R2 SP1.<br /><br /> **3** – işletim sistemi ailesi 3, eşdeğer tooWindows Server 2012.<br /><br /> **4** – işletim sistemi ailesi 4, eşdeğer tooWindows Server 2012 R2.<br /><br /> Daha fazla bilgi için bkz: [Azure konuk işletim sistemi sürümleri](https://azure.microsoft.com/documentation/articles/cloud-services-guestos-update-matrix/#releases).|
|targetOSVersion|Dize|hello Azure konuk işletim sistemi sürümü toobe hello havuzunda hello sanal makinelerde yüklü.<br /><br /> Merhaba varsayılan değer  **\***  belirtilen ailesi hello için hello en son işletim sistemi sürümünü belirtir.<br /><br /> İzin verilen diğer değerleri için bkz: [Azure konuk işletim sistemi sürümleri](https://azure.microsoft.com/documentation/articles/cloud-services-guestos-update-matrix/#releases).|

###  <a name="bk_vmconf"></a>virtualMachineConfiguration

|Öğe adı|Tür|Notlar|
|------------------|----------|-----------|
|[Imagereference](#bk_imgref)|Karmaşık türü|Merhaba platform veya Market görüntü toouse hakkındaki bilgileri belirtir.|
|nodeAgentSKUId|Dize|Merhaba hello işlem düğümü üzerinde sağlanan hello toplu işlem düğüm Aracısı SKU.|
|[windowsConfiguration](#bk_winconf)|Karmaşık türü|Merhaba sanal makineye Windows işletim sistemi ayarlarını belirtir. Bu özellik olmamalıdır hello Imagereference Linux işletim sistemi görüntüsü başvuran varsa belirtildi.|

###  <a name="bk_imgref"></a>Imagereference

|Öğe adı|Tür|Notlar|
|------------------|----------|-----------|
|Yayımcı|Dize|Merhaba görüntüsünün Hello yayımcı.|
|Teklif|Dize|Merhaba görüntüsünün Hello teklif.|
|SKU|Dize|Merhaba hello görüntüsünün SKU.|
|Sürüm|Dize|Merhaba hello görüntü sürümü.|

###  <a name="bk_winconf"></a>windowsConfiguration

|Öğe adı|Tür|Notlar|
|------------------|----------|-----------|
|enableAutomaticUpdates|Boole değeri|Merhaba sanal makine otomatik güncelleştirmeler için etkinleştirilip etkinleştirilmediğini gösterir. Bu özellik belirtilmezse, hello varsayılan değer true şeklindedir.|

###  <a name="bk_netconf"></a>networkConfiguration

|Öğe adı|Tür|Notlar|
|------------------|--------------|----------|
|subnetId|Dize|Hangi hello havuzun işlem düğümleri oluşturulan hello alt Hello kaynak tanımlayıcısını belirtir.|
