---
title: "Toplu işlemi için Azure CLI aaaGet Başlarken | Microsoft Docs"
description: "Bir giriş, Azure Batch hizmetinin kaynakları yönetmek için Azure CLI toohello toplu iş komutları Al"
services: batch
documentationcenter: 
author: tamram
manager: timlt
editor: 
ms.assetid: fcd76587-1827-4bc8-a84d-bba1cd980d85
ms.service: batch
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: multiple
ms.workload: big-compute
ms.date: 07/20/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 14f28311ecb16c8097d0d304a4ad89de282a2e9b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-batch-resources-with-azure-cli"></a>Batch kaynaklarını Azure CLI ile yönetme

Hello Azure CLI 2.0 Azure kaynaklarını yönetmek için Azure'nın yeni komut satırı deneyimidir. MacOS, Linux ve Windows’da kullanılabilir. Azure CLI 2.0 yönetmek ve hello komut satırından Azure kaynaklarını yönetmek için optimize edilmiştir. Azure toplu işlem hesaplarını ve havuzlar, işler ve görevler gibi toomanage kaynakları hello Azure CLI toomanage kullanabilirsiniz. Merhaba çoğunu komut Hello Azure CLI, yürütmek ile aynı görevleri hello Batch API'leri, Azure portal ve Batch PowerShell cmdlet'leri.

Bu makalede Batch ile [Azure CLI sürüm 2.0](https://docs.microsoft.com/cli/azure/overview) kullanımına genel bakışa yer verilmiştir. Bkz: [Azure CLI 2.0 ile çalışmaya başlama](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli) Azure ile Merhaba CLI kullanarak genel bir bakış için.

Microsoft hello Azure CLI, sürüm 2.0 hello en son sürümünü kullanmanızı önerir. Sürüm 2.0 hakkında daha fazla bilgi için bkz. [Azure Komut Satırı 2.0 genel kullanıma sunuldu](https://azure.microsoft.com/blog/announcing-general-availability-of-vm-storage-and-network-azure-cli-2-0/).

## <a name="set-up-hello-azure-cli"></a>Azure CLI Hello ayarlayın

tooinstall hello Azure CLI adımları özetlenen hello [yükleme hello Azure CLI](https://docs.microsoft.com/cli/azure/install-azure-cli.md).

> [!TIP]
> Azure CLI yüklemenizi güncelleştirmenizi öneririz sık tootake avantajlarından hizmet güncelleştirmeleri ve geliştirmeleri.
> 
> 

## <a name="command-help"></a>Komut yardımı

Her komut için Yardım metni hello Azure CLI ekleyerek görüntüleyebileceğiniz `-h` toohello komutu. Diğer seçenekleri atın. Örneğin:

* Merhaba tooget yardımını `az` komutu, girin:`az -h`
* tooget hello CLI, tüm toplu komutlarda listesini kullanın:`az batch -h`
* bir Batch hesabı oluşturma tooget Yardım girin:`az batch account create -h`

Şüpheli zaman hello kullan `-h` komut satırı seçeneği tooget Yardım herhangi bir Azure CLI komutu.

> [!NOTE]
> Merhaba kullanılan Azure CLI'ın önceki sürümlerini `azure` toopreface CLI komutu. Sürüm 2.0'da tüm komutlar `az` ile kullanılıyor. Sürüm 2.0, komut dosyaları toouse hello yeni sözdizimi emin tooupdate olabilir.
>
>  

Ayrıca, hakkında ayrıntılar için toohello Azure CLI başvuru belgelerine başvurun [toplu için Azure CLI komutları](https://docs.microsoft.com/cli/azure/batch). 

## <a name="log-in-and-authenticate"></a>Oturum açma ve kimlik doğrulaması

toouse hello Azure CLI toplu işlem ile içinde toolog gerekir ve kimlik doğrulaması. İki basit adımları toofollow vardır:

1. **Azure'da oturum açın.** Azure verir oturum dahil olmak üzere, tooAzure Resource Manager komutlara erişmek [toplu yönetim hizmeti](batch-management-dotnet.md) komutları.  
2. **Batch hesabınızda oturum açın.** Toplu işlem hesabı verir oturum tooBatch hizmeti komutları erişin.   

### <a name="log-in-tooazure"></a>İçinde tooAzure oturum

Azure, ayrıntılı olarak açıklanmıştır içine birkaç farklı şekilde toolog vardır [oturum Azure CLI 2.0 oturum](https://docs.microsoft.com/cli/azure/authenticate-azure-cli):

1. [Etkileşimli olarak oturum açma](https://docs.microsoft.com/cli/azure/authenticate-azure-cli#interactive-log-in). Azure CLI komutları kendiniz hello komut satırından çalıştırırken etkileşimli olarak oturum açın.
2. [Hizmet sorumlusu ile oturum açma](https://docs.microsoft.com/cli/azure/authenticate-azure-cli#logging-in-with-a-service-principal). Azure CLI komutlarını bir betikten veya uygulamadan çalıştırdığınızda hizmet sorumlusuyla oturum açın.

Bu makalede Hello amaçlarla gösteriyoruz nasıl toolog Azure içine etkileşimli olarak. Tür [az oturum açma](https://docs.microsoft.com/cli/azure/#login) hello komut satırında:

```azurecli
# Log in tooAzure and authenticate interactively.
az login
```

Merhaba `az login` tooauthenticate, aşağıda gösterildiği gibi kullanabileceğiniz belirteci komutu döndürür. Hello sağlanan yönergeleri tooopen bir web sayfası izleyin ve hello belirteci tooAzure gönderin:

![İçinde tooAzure oturum](./media/batch-cli-get-started/az-login.png)

Merhaba örnekler listelenen hello [örnek Kabuk komut dosyalarını](#sample-shell-scripts) de Göster nasıl bölümünde toostart Azure'da etkileşimli olarak oturum açarak, Azure CLI oturumunuz. Oturum açtıktan sonra toplu hesaplar, anahtarları, uygulama paketleri ve kotalar dahil olmak üzere Batch Yönetimi kaynaklarla komutları toowork çağırabilirsiniz.  

### <a name="log-in-tooyour-batch-account"></a>Toplu işlem hesabı tooyour içinde oturum

toouse hello Azure CLI toomanage toplu gibi kaynaklar havuzlar, işler ve görevler, Batch hesabınızda toolog gerekir ve kimlik doğrulaması. toohello Batch hizmeti toolog kullanmak hello [az toplu işlem hesabı oturum açma](https://docs.microsoft.com/cli/azure/batch/account#login) komutu. 

Batch hesabınızla kimlik doğrulamasından geçmek için kullanabileceğiniz iki seçenek vardır:

- **Azure Active Directory (Azure AD) kimlik doğrulamasını kullanmak.** 

    Azure AD ile kimlik doğrulaması toplu işlemle hello Azure CLI kullandığınızda hello varsayılan ayardır ve çoğu senaryolar için önerilir. 
    
    İçinde tooAzure hello önceki bölümde açıklandığı gibi etkileşimli olarak oturum açtığınızda hello Azure CLI tooyour toplu işlem hesabı bu kimlik bilgilerini kullanarak oturum için kimlik bilgilerinizi, önbelleğe alınır. Bir hizmet sorumlusunu kullanarak tooAzure içinde oturum açarsanız, bu kimlik bilgilerini tooyour toplu işlem hesabı içinde kullanılan toolog ayrıca değildir.

    Azure AD'nin avantajlarından biri rol tabanlı erişim denetimine (RBAC) sahip olmasıdır. Bunlar hello hesabı anahtarları sahip olup olmadığına yerine RBAC ile bir kullanıcının erişimi kendilerine atanmış rolün bağlıdır. Hesap anahtarlarını yönetmek yerine RBAC rollerini yönetebilir ve erişimle kimlik doğrulamasını Azure AD'ye bırakabilirsiniz.  

    Azure AD ile kimlik doğrulaması gereklidir oluşturduysanız Azure Batch hesabınızla kendi havuzu ayırma modu ayarlamak too'User abonelik '. 

    toolog tooyour toplu olarak Azure AD kullanarak hesap, çağrı hello [az toplu işlem hesabı oturum açma](https://docs.microsoft.com/cli/azure/batch/account#login) komutu: 

    ```azurecli
    az batch account login -g myresource group -n mybatchaccount
    ```

- **Paylaşılan Anahtar kimlik doğrulamasını kullanarak.**

    [Paylaşılan anahtar kimlik doğrulaması](https://docs.microsoft.com/rest/api/batchservice/authenticate-requests-to-the-azure-batch-service#authentication-via-shared-key) kullanır, hesabınız erişim tuşları tooauthenticate Azure CLI komutları hello için Batch hizmeti.

    Azure CLI betikleri tooautomate çağıran toplu iş komutları oluşturuyorsanız, paylaşılan anahtar kimlik doğrulaması veya bir Azure AD hizmet sorumlusu kullanabilirsiniz. Bazı senaryolarda Paylaşılan Anahtar ile kimlik doğrulaması, hizmet sorumlusu oluşturmaktan daha kolay olabilir.  

    Paylaşılan anahtar kimlik doğrulaması kullanarak toolog dahil hello `--shared-key-auth` hello komut satırı seçeneği:

    ```azurecli
    az batch account login -g myresourcegroup -n mybatchaccount --shared-key-auth
    ```

Merhaba örnekler listelenen hello [örnek Kabuk komut dosyalarını](#sample-shell-scripts) bölüm Göster nasıl toolog Batch hesabınızla içine hello Azure CLI her ikisini de kullanarak Azure AD ve paylaşılan anahtar.

## <a name="use-azure-batch-cli-templates-and-file-transfer-preview"></a>Azure Batch CLI Şablonlarını ve Dosya Aktarımı (Önizleme) özelliğini kullanma

Kod yazmadan hello Azure CLI toorun toplu işleri uçtan uca kullanabilirsiniz. Toplu işlem şablonu dosyaları oluşturma havuzlar, işler ve görevler hello Azure CLI ile destekler. Hello Azure CLI tooupload iş girdi dosyalarını da kullanabilirsiniz hello ile ilişkili toohello Azure depolama hesabı Batch hesabı ve proje çıktı dosyalarını indirin. Daha fazla bilgi için bkz. [Azure Batch CLI Şablonlarını ve Dosya Aktarımı (Önizleme) özelliğini kullanma](batch-cli-templates.md).

## <a name="sample-shell-scripts"></a>Örnek kabuk betikleri

Merhaba örnek komut dosyaları, toplu yönetim hizmeti tooaccomplish ortak görevleri hello Batch hizmeti ile nasıl toouse Azure CLI komutları Tablo Göster aşağıdaki hello listelenir. Bu örnek komut dosyalarını hello toplu işlemi için Azure CLI bulunan hello komutların çoğu kapsar. 

| Betik | Notlar |
|---|---|
| [Batch hesabı oluşturma](./scripts/batch-cli-sample-create-account.md) | Bir Batch hesabı oluşturur ve depolama hesabınızla ilişkilendirir. |
| [Uygulama ekleme](./scripts/batch-cli-sample-add-application.md) | Bir uygulama ekler ve paketlenmiş ikili dosyalarını karşıya yükler.|
| [Batch havuzlarını yönetme](./scripts/batch-cli-sample-manage-pool.md) | Havuzlar için oluşturma, yeniden boyutlandırma ve yönetme işlemlerini gösterir. |
| [Batch ile bir iş ve görevlerini çalıştırma](./scripts/batch-cli-sample-run-job.md) | Bir işi çalıştırmayı ve görev eklemeyi gösterir. |

## <a name="json-files-for-resource-creation"></a>Kaynak oluşturmak için JSON dosyaları

Havuzlar ve işler gibi Batch kaynaklarını oluşturduğunuzda, komut satırı seçeneklerini parametrelerini geçirme yerine hello yeni kaynağın yapılandırmasını içeren bir JSON dosyası belirtebilirsiniz. Örneğin:

```azurecli
az batch pool create my_batch_pool.json
```

Yalnızca komut satırı seçeneklerini kullanarak birçok Batch kaynaklarını oluşturabilirsiniz, ancak bazı özellikler hello kaynak ayrıntılarını içeren bir JSON biçimli dosya belirttiğiniz gerektirir. Örneğin, toospecify kaynak dosyaları için bir başlangıç görevi istiyorsanız bir JSON dosyası kullanmanız gerekir.

bir kaynak toosee hello JSON söz dizimi gerekli toocreate, toohello başvuran [Batch REST API'si başvurusu] [ rest_api] belgeleri. Her "Ekle *kaynak türü*" Merhaba REST API Başvurusu konudaki bu kaynağı oluşturmak için örnek JSON komut dosyaları içerir. JSON dosyaları toouse hello Azure CLI ile için bu örnek JSON komutlar şablon olarak kullanabilirsiniz. Toosee hello JSON söz dizimi havuzu oluşturma, örneğin, başvuran çok[bir havuz tooan hesabı eklemek][rest_add_pool].

Bir JSON dosyasını belirten örnek bir betik için bkz. [Batch ile bir iş ve görevlerini çalıştırma](./scripts/batch-cli-sample-run-job.md).

> [!NOTE]
> Bir kaynak oluşturduğunuzda bir JSON dosyası belirtirseniz, bu kaynak için hello komut satırında belirttiğiniz herhangi bir parametre yoksayılır.
> 
> 

## <a name="efficient-queries-for-batch-resources"></a>Batch kaynakları için etkili sorgular

Her Batch kaynak türü, Batch hesabınızı sorgulayan ve bu türdeki kaynakları listeleyen bir `list` komutunu destekler. Örneğin, bir iş hesabı ve hello görevleri de hello havuzları listeleyebilirsiniz:

```azurecli
az batch pool list
az batch task list --job-id job001
```

Merhaba Batch hizmetiyle sorguladığınızda bir `list` işlemi, döndürülen veriler, bir OData yan tümcesi toolimit hello miktarını belirtebilirsiniz. Filtre işleminin tümü sunucu tarafında oluştuğundan, yalnızca, istek hello verileri hello kablo kestiği. Bu yan tümceleri toosave bant genişliğini kullan (ve bu nedenle saat) listeleme işlemleri gerçekleştirdiğinizde.

Merhaba aşağıdaki tabloda hello OData yan tümceleri hello Batch hizmeti tarafından desteklenen açıklanmaktadır:

| Yan Tümce | Açıklama |
|---|---|
| `--select-clause [select-clause]` | Her varlık için bir özellik alt kümesi döndürür. |
| `--filter-clause [filter-clause]` | Merhaba eşleşen döndürür yalnızca varlıklar OData ifade belirtildi. |
| `--expand-clause [expand-clause]` | Tek bir temel REST çağrısı Hello varlık bilgileri alır. Merhaba genişletin destekler yalnızca hello yan tümcesi şu anda `stats` özelliği. |

Bir örnek komut dosyası için nasıl toouse bir OData yan tümcesi bkz gösteren [toplu işlemle bir işi ve görevleri çalıştırmak](./scripts/batch-cli-sample-run-job.md).

OData yan tümceleri içeren verimli listesi sorguları gerçekleştirme hakkında daha fazla bilgi için bkz: [hello Azure Batch hizmetinin verimli bir şekilde sorgu](batch-efficient-list-queries.md).

## <a name="troubleshooting-tips"></a>Sorun giderme ipuçları

Azure CLI sorunlarını giderirken hello aşağıdaki ipuçları yardımcı olabilir:

* Kullanım `-h` tooget **Yardım metni** için herhangi bir CLI komutu
* Kullanım `-v` ve `-vv` toodisplay **ayrıntılı** komut çıktı. Ne zaman hello `-vv` bayrağı dahil, hello Azure CLI hello gerçek REST isteklerinin ve yanıtlarının görüntüler. Bu anahtarlar tam hata çıktısını görüntülemek için kullanışlıdır.
* Görüntüleyebileceğiniz **komutu çıktıyı JSON olarak** hello ile `--json` seçeneği. Örneğin, `az batch pool show pool001 --json` seçeneği pool001'in özelliklerini JSON biçiminde gösterir. Daha sonra kopyalayın ve bu çıkış toouse değiştirme bir `--json-file` (bkz [JSON dosyaları](#json-files) bu makalenin önceki).
<!---Loc Comment: Please, check link [JSON files] since it's not redirecting tooany location.--->
* Merhaba [toplu işlem Forumu] [ batch_forum] Batch ekip üyeleri tarafından izlenir. Sorun yaşamanız veya belirli bir işlemle ilgili yardım almak istemeniz durumunda sorularınızı gönderebilirsiniz.

## <a name="next-steps"></a>Sonraki adımlar

* Merhaba hello Azure CLI hakkında daha fazla bilgi için bkz: [Azure CLI belgelerine](https://docs.microsoft.com/cli/azure/overview).
* Batch kaynakları hakkında daha fazla bilgi için bkz. [Geliştiriciler için Azure Batch'e genel bakış](batch-api-basics.md).
* Kod yazmadan toplu şablonları toocreate havuzlar, işler ve görevler kullanma hakkında daha fazla bilgi için bkz: [kullanım Azure Batch CLI şablonları ve dosya aktarımı (Önizleme)](batch-cli-templates.md).

[batch_forum]: https://social.msdn.microsoft.com/forums/azure/home?forum=azurebatch
[github_readme]: https://github.com/Azure/azure-xplat-cli/blob/dev/README.md
[rest_api]: https://msdn.microsoft.com/library/azure/dn820158.aspx
[rest_add_pool]: https://msdn.microsoft.com/library/azure/dn820174.aspx
