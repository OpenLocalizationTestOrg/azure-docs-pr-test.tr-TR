---
title: "Azure Batch aaaRun (Önizleme) kod yazmadan uçtan uca iş | Microsoft Docs"
description: "Şablon dosyalarını hello Azure CLI toocreate toplu havuzlar, işler ve görevler için oluşturun."
services: batch
author: mscurrell
manager: timlt
ms.assetid: 
ms.service: batch
ms.devlang: na
ms.topic: article
ms.workload: big-compute
ms.date: 07/20/2017
ms.author: markscu
ms.openlocfilehash: c0434d09766451f6ba516efbad949834711ee819
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-batch-cli-templates-and-file-transfer-preview"></a>Azure Batch CLI Şablonlarını ve Dosya Aktarımı (Önizleme) özelliğini kullanma

Hello Azure CLI kullanarak kod yazma olmadan olası toorun toplu işleri değildir.

Şablon dosyaları oluşturulur ve hello Batch havuzları, işleri ve görevleri toobe oluşturulan izin Azure CLI ile kullanılır. İş giriş dosyaları karşıdan hello toplu işlem hesabı ve iş çıktısı dosyalarıyla ilişkili hello depolama hesabı kolayca yüklenebilir.

## <a name="overview"></a>Genel Bakış

Bir uzantı toohello Azure CLI toplu kullanılan toobe uçtan uca geliştiriciler olmayan kullanıcılar tarafından sağlar. Bir havuz oluşturulabilir, işler ve oluşturulan, ilişkili görevler girdi verileri karşıya ve karşıdan – hello elde edilen çıktı verilerini kod gerekmez, CLI hello doğrudan kullanılan veya komut dosyalarına tümleştirilmekte.

Toplu şablonları yapı hello üzerinde [hello Azure CLI mevcut toplu desteği](https://docs.microsoft.com/azure/batch/batch-cli-get-started#json-files-for-resource-creation) JSON dosyaları hello oluşturulmasını havuzlar, işler, görevler ve diğer öğeleri için toospecify özellik değerlerine izin verir. Toplu işlem şablonları ile Merhaba aşağıdaki özellikleri hello JSON dosyaları ile olası nedir üzerinden eklendi:

-   Parametreleri tanımlanabilir. Merhaba şablon kullanıldığında, yalnızca hello parametre hello şablon gövdesinde belirtilen diğer öğesi özellik değerleri ile belirtilen toocreate hello öğesi değerlerdir. Batch ve uygulamaları toobe Batch tarafından çalıştırma özelliğini algılayan bir kullanıcı, havuz, iş ve görev özellik değerlerini belirterek şablonları oluşturabilirsiniz. Toplu işlem ve/veya uygulamalar bilmiyorsanız daha az bir kullanıcı toospecify hello değerleri hello tanımlanan parametreler için yeterlidir.

-   İş görevi oluşturucuları oluşturun veya pek çok görev tanımları toobe oluşturulan ve önemli ölçüde basitleştirme iş gönderme hello önleme bir iş ile ilgili daha fazla görev gerekir.


Çıktı veri dosyaları çoğunlukla üretilir ve girdi veri dosyalarını işleri sağlanan toobe gerekir. Varsayılan olarak bir depolama hesabını ilişkili, her Batch ile kolayca aktarılan tooand hiçbir kodlama ile CLI kullanarak bu depolama hesabından hesabı ve dosyaları olabilir ve hiçbir depolama kimlik bilgileri gerekir.

Örneğin, [ffmpeg](http://ffmpeg.org/) , ses ve video dosyaları işler yaygın bir uygulamadır. Hello Azure Batch CLI kullanılan tooinvoke ffmpeg tootranscode kaynak video dosyaları toodifferent çözümleri olabilir.

-   Bir havuzu şablonu oluşturulur. Hello şablon oluşturma hello kullanıcı toocall nasıl hello ffmpeg uygulama ve gereklilikleri bilir; Merhaba belirtin uygun işletim sistemi, VM boyutu nasıl ffmpeg yüklü (bir uygulama paketi veya örneğin bir paket Yöneticisi'ni kullanarak) ve diğer havuz özellik değerleri. Bu nedenle Hello şablon kullanıldığında, yalnızca hello havuzu kimliği ve VM'lerin sayısını belirtilen toobe gerekir parametreleri oluşturulur.

-   Bir proje şablonu oluşturulur. Merhaba kullanıcı oluşturma hello şablonu nasıl ffmpeg gereksinimlerini toobe tootranscode kaynak video tooa farklı çözümleme çağrılır ve hello görev komut satırını belirtir bilir; Bunlar, ayrıca her giriş dosyası için gerekli bir görev ile Merhaba kaynak video dosyaları içeren bir klasör olduğunu bilirsiniz.

-   Video dosyaları tootranscode kümesi son kullanıcı ilk hello havuzu şablonunu kullanarak, yalnızca hello havuzu kimliği ve gerekli VM'lerin sayısını belirten bir havuz oluşturur. Ardından hello kaynak dosyaları tootranscode karşıya yükleyebilirsiniz. Bir işi yalnızca hello Havuz kimliği ve karşıya hello kaynak dosyalarının konumunu belirtme hello proje şablonunu kullanarak ardından gönderilebilir. oluşturulan giriş dosya başına tek bir görev Hello toplu iş oluşturulur. Son olarak, hello kod çevrimi çıktı dosyaları karşıdan yüklenebilir.

## <a name="installation"></a>Yükleme

Merhaba şablon ve dosya aktarımı özellikleri yüklü bir uzantı toobe gerektirir.

Yönergeler için nasıl tooinstall hello Azure CLI bkz [Azure CLI 2.0 yükleme](https://docs.microsoft.com/cli/azure/install-azure-cli).

Azure CLI yüklenmiş bir kez hello hello toplu uzantısı aşağıdaki CLI komutu kullanılarak yüklenebilir:

```azurecli
az component update --add batch-extensions --allow-third-party
```

Merhaba toplu uzantısı hakkında daha fazla bilgi için bkz: [için Microsoft Azure toplu işlem CLI uzantıları Windows, Mac ve Linux](https://github.com/Azure/azure-batch-cli-extensions#microsoft-azure-batch-cli-extensions-for-windows-mac-and-linux).

## <a name="templates"></a>Şablonlar

Hello Azure Batch CLI havuzlar, işler ve görevler toobe özellik adlarını ve değerlerini içeren bir JSON dosyası belirterek oluşturulan gibi öğeleri sağlar. Örneğin:

```azurecli
az batch pool create –-json-file AppPool.json
```

Azure Batch işlevsellik ve sözdizimi benzer tooAzure Resource Manager şablonları şablonlarıdır. Öğe özellik adları ve değerleri içerir, ancak ana kavramlar aşağıdaki hello eklemek JSON dosyaları bunlar:

-   **Parametreler**

    -   Yalnızca hello şablon kullanıldığında, sağlanan toobe gerek parametre değerleri ile bir gövde bölümünde belirtilen özellik değerleri toobe izin verir. Örneğin, bir havuz için tam tanımı hello hello gövde ve havuzu kimliği için tanımlanan yalnızca bir parametre yerleştirilemedi; yalnızca bir havuz kimliği dizesi, bu nedenle bir havuzu sağlanan toobe toocreate gerekir.
        
    -   Merhaba şablon gövde toplu bilgisine sahip biri tarafından yazılan ve hello uygulamaları toobe Batch tarafından çalıştırın; Merhaba şablon kullanıldığında, yalnızca hello yazar tarafından tanımlanan parametreler için değer sağlanmalıdır. Merhaba ayrıntılı toplu olmayan bir kullanıcı ve/veya uygulama bilgisi, bu nedenle şablonları kullanabilirsiniz.

-   **Değişkenler**

    -   Tek bir yerde belirtilen ve hello şablon gövdesi bir veya daha fazla yerde kullanılan basit veya karmaşık parametre değerleri toobe izin verir. Değişkenleri basitleştirmek ve hello şablon hello boyutunu yanı daha rahat bir değeri değişebilir konumu toochange özellikleri sağlayarak kolaylaştırır.

-   **Daha yüksek düzeyli yapıları**

    -   Bazı daha yüksek düzeyli yapıları hello Batch API'lerini henüz kullanılamıyor hello şablon kullanılabilir. Örneğin, bir görev fabrikası ortak görev tanımı kullanarak hello işi için birden çok görev oluşturur bir proje şablonu içinde tanımlanabilir. Bu yapıları dinamik olarak görev başına bir dosyayı gibi birden çok JSON dosyası oluşturun yanı sıra betiği örneğin bir paket Yöneticisi üzerinden dosyaları tooinstall uygulamaları oluşturmak için hello gerek toocode kaçının.

    -   Bazı noktası, geçerli, bu yapıları olabilir toothe Batch hizmetini ve kullanılabilir eklendiği hello Batch API'leri, Uı'lar vb..

### <a name="pool-templates"></a>Havuzu şablonları

Ayrıca toohello standart şablon özelliklerini parametreler ve değişkenler, daha yüksek düzeyli yapıları aşağıdaki hello hello havuzu şablonu tarafından desteklenir:

-   **Paket referanslarını**

    -   İsteğe bağlı olarak yazılım kopyalanan toobe toopool düğümlere paketini kullanarak yöneticileri izin verir. Merhaba Paket Yöneticisi ve paket kimliği belirtilmedi. Mümkün toodeclare olan bir veya daha fazla paket önler hello gerek toocreate hello gerekli paketleri alır bir komut dosyası, hello komut dosyası yükleyin ve her bir havuz düğümde hello komut dosyasını çalıştırın.

bir havuz kimliği dizesi ve hello sayısı VM'ler sağlanan toobe toouse yüklü ve yalnızca Linux VM'ler havuzu ile ffmpeg oluşturan bir şablon örneği gerektirir Hello aşağıda verilmiştir:

```json
{
    "parameters": {
        "nodeCount": {
            "type": "int",
            "metadata": {
                "description": "hello number of pool nodes"
            }
        },
        "poolId": {
            "type": "string",
            "metadata": {
                "description": "hello pool id "
            }
        }
    },
    "pool": {
        "type": "Microsoft.Batch/batchAccounts/pools",
        "apiVersion": "2016-12-01",
        "properties": {
            "id": "[parameters('poolId')]",
            "virtualMachineConfiguration": {
                "imageReference": {
                    "publisher": "Canonical",
                    "offer": "UbuntuServer",
                    "sku": "16.04.0-LTS",
                    "version": "latest"
                },
                "nodeAgentSKUId": "batch.node.ubuntu 16.04"
            },
            "vmSize": "STANDARD_D3_V2",
            "targetDedicatedNodes": "[parameters('nodeCount')]",
            "enableAutoScale": false,
            "maxTasksPerNode": 1,
            "packageReferences": [
                {
                    "type": "aptPackage",
                    "id": "ffmpeg"
                }
            ]
        }
    }
}
```

Merhaba şablon dosyası adlandırırsanız _havuzu ffmpeg.json_, hello şablon gibi çağrıldığı sonra:

```azurecli
az batch pool create --template pool-ffmpeg.json
```

### <a name="job-templates"></a>Proje şablonları

Ayrıca toohello standart şablon özelliklerini parametreler ve değişkenler, daha yüksek düzeyli yapıları aşağıdaki hello hello proje şablonu tarafından desteklenir:

-   **Görev Fabrika**

    -   Bir iş için birden çok görevleri bir görev tanımından oluşturur. Üç tür görev Fabrika desteklenir – parametrik, dosya başına görev sweep ve görev koleksiyonu.

Merhaba, her kaynak video dosyası oluşturulan bir görev ile ffmpeg kodlamasını MP4 video dosyaları tooone iki alt çözünürlüğü için kullandığı bir işi oluşturan bir şablon örneği aşağıdadır:

```json
{
    "parameters": {
        "poolId": {
            "type": "string",
            "metadata": {
                "description": "hello name of Azure Batch pool which runs hello job"
            }
        },
        "jobId": {
            "type": "string",
            "metadata": {
                "description": "hello name of Azure Batch job"
            }
        },
        "resolution": {
            "type": "string",
            "defaultValue": "428x240",
            "allowedValues": [
                "428x240",
                "854x480"
            ],
            "metadata": {
                "description": "Target video resolution"
            }
        }
    },
    "job": {
        "type": "Microsoft.Batch/batchAccounts/jobs",
        "apiVersion": "2016-12-01",
        "properties": {
            "id": "[parameters('jobId')]",
            "constraints": {
                "maxWallClockTime": "PT5H",
                "maxTaskRetryCount": 1
            },
            "poolInfo": {
                "poolId": "[parameters('poolId')]"
            },
            "taskFactory": {
                "type": "taskPerFile",
                "source": { 
                    "fileGroup": "ffmpeg-input"
                },
                "repeatTask": {
                    "commandLine": "ffmpeg -i {fileName} -y -s [parameters('resolution')] -strict -2 {fileNameWithoutExtension}_[parameters('resolution')].mp4",
                    "resourceFiles": [
                        {
                            "blobSource": "{url}",
                            "filePath": "{fileName}"
                        }
                    ],
                    "outputFiles": [
                        {
                            "filePattern": "{fileNameWithoutExtension}_[parameters('resolution')].mp4",
                            "destination": {
                                "autoStorage": {
                                    "path": "{fileNameWithoutExtension}_[parameters('resolution')].mp4",
                                    "fileGroup": "ffmpeg-output"
                                }
                            },
                            "uploadOptions": {
                                "uploadCondition": "TaskSuccess"
                            }
                        }
                    ]
                }
            },
            "onAllTasksComplete": "terminatejob"
        }
    }
}
```

Merhaba şablon dosyası adlandırırsanız _iş ffmpeg.json_, hello şablon gibi çağrıldığı sonra:

```azurecli
az batch job create --template job-ffmpeg.json
```

## <a name="file-groups-and-file-transfer"></a>Dosya grupları ve dosya aktarımı

Çoğu işler ve görevler girdi dosyası gerektirir ve çıktı dosyaları üretir. Her ikisi de girişi dosyaları ve çıktı dosyaları genellikle hello istemci toohello düğümünden veya hello düğüm toohello istemcisi aktarılan toobe gerekir. Hello Azure Batch CLI uzantısı koyma dosya aktarımı soyutlar ve her toplu işlem hesabı için varsayılan olarak oluşturulan hello depolama hesabı kullanır.

Bir dosya grubu hello Azure depolama hesabı oluşturulur tooa kapsayıcı karşılık gelir. Merhaba dosya grubu alt klasörleri olabilir.

Merhaba toplu CLI uzantısını komutları istemci tooa belirtilen dosya grubu karşıya yükleme dosyalarından ve hello belirtilen dosya grubu tooa istemci yükleme dosyalarını sağlar.

```azurecli
az batch file upload --local-path c:\source_videos\*.mp4 
    --file-group ffmpeg-input

az batch file download --file-group ffmpeg-output --local-path
    c:\output_lowres_videos
```

Havuz ve proje şablonları havuzu düğümleri üzerine kopyalama için belirtilen dosya grupları toobe depolanan dosyaları izin verin veya havuzu düğümleri tooa dosya grubu yedekleme. Örneğin, hello kaynak video dosyalarının üzerine hello düğümü kodlama dönüştürme için aşağı kopyalanan hello konumu olarak daha önce belirtilen iş şablonunda hello dosya grubu "ffmpeg-Giriş" Merhaba görev Fabrika için belirtilir; Merhaba dosya grubu "ffmpeg-output" Hello hello kod çevrimi çıkış dosyalarının nerede konumu kopyalanan her görev çalıştıran toofrom hello düğüm olarak kullanılır.

## <a name="summary"></a>Özet

Şablon ve dosya aktarımı desteği şu anda eklenmiş yalnızca Azure CLI toohello. Merhaba, Araştırmacıları, BT kullanıcıları vb. gibi hello Batch API'lerini kullanarak toodevelop kod gerekmez toplu toousers kullanabilirsiniz tooexpand hello İzleyici hedeftir. Kodlama olmadan Azure, toplu ve toplu iş çalıştırmak hello uygulamaları toobe bilgisine sahip kullanıcılar havuzu ve iş oluşturma için şablonlar oluşturabilirsiniz. Şablon parametreleri ile kullanıcılar toplu işlem ve hello uygulamaların ayrıntılı bilgisi olmadan hello şablonları kullanabilirsiniz.

Merhaba hello Azure CLI için toplu uzantısı denemek ve bu makalenin veya hello aracılığıyla ya da hello yorumlarını bize herhangi bir geri bildirim veya öneriler, sağlayın [Azure Batch forumunu](https://social.msdn.microsoft.com/forums/azure/home?forum=azurebatch).

## <a name="next-steps"></a>Sonraki adımlar

- Merhaba toplu şablonları blog gönderisi bkz: [çalışan Azure Batch işleri kullanarak hello Azure CLI – gerekli kod](https://azure.microsoft.com/en-us/blog/running-azure-batch-jobs-using-the-azure-cli-no-code-required/).
- Ayrıntılı Kurulum ve kullanım belgeler, örnekler ve kaynak kodu hello kullanılabilir [Azure GitHub deposunu](https://github.com/Azure/azure-batch-cli-extensions).
