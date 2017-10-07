---
title: aaaInstall hello Azure CLI 1.0 | Microsoft Docs
description: "Azure hizmetlerini kullanarak Mac, Linux ve Windows toostart için Azure CLI 1.0 Hello yükleyin"
editor: 
manager: timlt
documentationcenter: 
author: squillace
services: virtual-machines-linux,virtual-network,storage,azure-resource-manager
tags: azure-resource-manager,azure-service-management
ms.assetid: bdb776c8-7a76-4f3a-887c-236b4fffee10
ms.service: multiple
ms.workload: multiple
ms.tgt_pltfrm: command-line-interface
ms.devlang: na
ms.topic: article
ms.date: 03/20/2017
ms.author: rasquill
ms.openlocfilehash: a8cd4e38fde6e4b17a768a7caecd280cd91a70f2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="install-hello-azure-cli-10"></a>Hello Azure CLI 1.0 yükleyin
> [!div class="op_single_selector"]
> * [PowerShell](/powershell/azure/overview)
> * [Azure CLI 1.0](cli-install-nodejs.md)
> * [Azure CLI 2.0](/cli/azure/install-azure-cli)

> [!IMPORTANT]
> Bu konuda, çok sayıda Resource Manager dağıtım etkinliklerini yanı sıra nasıl tooinstall hello nodeJs inşa edilmiş ve tüm Klasik dağıtım API destekleyen Azure CLI 1.0 çağırır açıklanmaktadır. Merhaba kullanması gereken [Azure CLI 2.0](/cli/azure/overview) yeni veya forward-looking CLI dağıtım ve yönetimi için.

Hızlı bir şekilde hello Azure komut satırı arabirimi (Azure CLI 1.0) toouse oluşturmak ve Microsoft Azure kaynakları yönetmek için açık kaynaklı, komut kabuğu tabanlı kümesini yükleyin. Bu platformlar arası araçları çeşitli seçenekler tooinstall bilgisayarınızda var:

* **npm paket** - çalışma npm (JavaScript için Paket Yöneticisi hello) tooinstall hello en son Azure CLI 1.0 paket Linux dağıtımı veya işletim sistemi. Node.js ve bilgisayarınızda npm gerektirir.
* **Yükleyici** -Mac veya Windows kolay yükleme için bir yükleyici indirin.
* **Docker kapsayıcısı** - başlangıç hello kullanarak en son CLI hazır Çalıştır Docker kapsayıcısı içinde. Docker ana bilgisayarınızda gerektirir.

Daha fazla seçenekleri ve arka plan için hello proje deposu bakın [GitHub](https://github.com/azure/azure-xplat-cli).

Hello Azure CLI 1.0 yüklendikten sonra [Azure aboneliğinizle bağlanmak](xplat-cli-connect.md) ve çalışma hello **azure** komutları, komut satırı arabiriminden (Bash, Terminal, komut istemi vb.) ile toowork Azure kaynaklarınızı.

## <a name="option-1-install-an-npm-package"></a>Seçenek 1: bir npm paket yükleme
bir npm paketinden tooinstall hello CLI indirilir ve hello yüklü olduğundan emin olun [en son Node.js ve npm](https://nodejs.org/en/download/package-manager/). Daha sonra çalıştırın **npm yükleme** tooinstall hello azure CLI paketi:

```bash
npm install -g azure-cli
```

Linux dağıtımları hakkında toouse gerekebilecek **sudo** çalıştırmak toosuccessfully hello **npm** komutu, şu şekilde:

```bash
sudo npm install -g azure-cli
```

> [!NOTE]
> Node.js ve npm Linux dağıtımı veya işletim sistemi güncelleştirme veya tooinstall ihtiyacınız varsa, hello en son Node.js LTS sürüm (4.x) yüklemenizi öneririz. Eski bir sürümünü kullanıyorsanız, yükleme hataları alabilirsiniz.

İsterseniz, indirme son Linux hello [tar dosya] [ linux-installer] hello npm paket yerel olarak. Ardından, hello indirilen npm paket aşağıdaki gibi yükleyin (Linux dağıtımları toouse gerekebilecek **sudo**):

```bash
npm install -g <path toodownloaded tar file>
```

## <a name="option-2-use-an-installer"></a>Seçenek 2: bir yükleyici kullanın
Mac veya Windows bilgisayarı kullanıyorsanız, CLI yükleyicileri aşağıdaki hello indirme için kullanılabilir:

* [Mac OS X yükleyici][mac-installer]
* [Windows MSI][windows-installer]

> [!TIP]
> Windows hello de indirebilirsiniz [Web Platformu yükleyicisi](https://go.microsoft.com/?linkid=9828653) tooinstall hello CLI. Seçenek tooinstall hello yükleyici kazandırır yükledikten sonra komut satırı araçları ve ek Azure SDK'sını hello CLI.

## <a name="option-3-use-a-docker-container"></a>Seçenek 3: bir Docker kapsayıcısı kullanın
Bilgisayarınızda olarak ayarladıysanız, bir [Docker](https://docs.docker.com/engine/understanding-docker/) ana çalıştırabileceğiniz bir Docker kapsayıcısı en son Azure CLI 1.0 hello. Çalışma hello komutu aşağıdaki (Linux dağıtımları toouse gerekebilecek **sudo**):

```bash
docker run -it microsoft/azure-cli
```

## <a name="run-azure-cli-10-commands"></a>Azure CLI 1.0 komutlarını çalıştırın
Hello Azure CLI 1.0 yüklendikten sonra hello çalıştıracak **azure** komutu, komut satırı kullanıcı arabiriminden (Bash, Terminal, komut istemi vb.). Örneğin, toorun hello Yardım komutu hello aşağıdaki komutu yazın:

```azurecli
azure help
```

> [!NOTE]
> Bazı Linux dağıtımları üzerinde benzer bir hata çok alabileceğiniz`/usr/bin/env: ‘node’: No such file or directory`. Bu hata /usr/bin/nodejs sırasında yüklenen Node.js son yüklemeleri gelir. toofix, şu komutu çalıştırarak sembolik bağlantıyı çok/usr/bin/düğüm oluşturun:

```bash
sudo ln -s /usr/bin/nodejs /usr/bin/node
```

hello Azure CLI yüklediğiniz, 1.0 aşağıdaki türü hello toosee hello sürümü:

```azurecli
azure --version
```

Artık hazırsınız! Tüm tooaccess hello CLI komutları toowork kendi kaynaklarla [tooyour Azure aboneliği hello Azure CLI ' bağlanma](xplat-cli-connect.md).

> [!NOTE]
> Azure CLI ilk kullandığınızda tooallow Microsoft toocollect kullanım bilgileri isteyip istemediğinizi soran bir ileti görürsünüz. Katılım gönüllüdür. Tooparticipate seçerseniz, çalıştırarak herhangi bir zamanda durdurabilirsiniz `azure telemetry --disable`. herhangi bir zamanda tooenable katılım çalıştırmak `azure telemetry --enable`.

## <a name="update-hello-cli"></a>Merhaba CLI güncelleştir
Microsoft, sık hello Azure CLI güncelleştirilmiş sürümlerini serbest bırakır. Yeniden işletim sisteminizi hello Yükleyicisi'ni kullanarak CLI hello veya hello son Docker kapsayıcısı'nı çalıştırın. Veya sahip Merhaba, en son Node.js ve yüklü npm hello aşağıdakileri yazarak güncelleştirmeniz (Linux dağıtımları toouse gerekebilecek **sudo**).

```bash
npm update -g azure-cli
```

## <a name="enable-tab-completion"></a>Sekme tamamlama etkinleştir
Sekme tamamlama CLI komutlarının Mac ve Linux için desteklenir.

tooenable zsh, içinde çalıştırın:

```bash
echo '. <(azure --completion)' >> .zshrc
```

tooenable bash, içinde çalıştırın:

```bash
azure --completion >> ~/azure.completion.sh
echo 'source ~/azure.completion.sh' >> ~/.bash_profile
```


## <a name="next-steps"></a>Sonraki adımlar
* [Hello CLI tooyour Azure aboneliği ' bağlanma](xplat-cli-connect.md) toocreate ve Azure kaynaklarınızı yönetmek.
* toolearn hello Azure CLI hakkında daha fazla kaynak kodunu indirebilir, rapor sorunları veya toohello proje katkıda, hello ziyaret [hello Azure CLI için GitHub depo](https://github.com/azure/azure-xplat-cli).
* Hello Azure CLI veya Azure kullanma hakkında sorularınız varsa, hello ziyaret [Azure forumları](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurescripting).


[mac-installer]: http://aka.ms/mac-azure-cli
[windows-installer]: http://aka.ms/webpi-azure-cli
[linux-installer]: http://aka.ms/linux-azure-cli
[cliasm]: /cli/azure/get-started-with-az-cli2
[cliarm]: ./virtual-machines/azure-cli-arm-commands.md
