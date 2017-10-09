---
title: "aaaSubmit işleri tooan HPC paketi küme Azure'da | Microsoft Docs"
description: "Bir şirket içi bilgisayar toosubmit yukarı tooset tooan HPC Pack Azure kümesinde nasıl işler öğrenin"
services: virtual-machines-windows
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management,hpc-pack
ms.assetid: 78f6833c-4aa6-4b3e-be71-97201abb4721
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-multiple
ms.workload: big-compute
ms.date: 10/14/2016
ms.author: danlep
ms.openlocfilehash: 2918cf633917d8730487152e6a5ddb863eb8bb5e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="submit-hpc-jobs-from-an-on-premises-computer-tooan-hpc-pack-cluster-deployed-in-azure"></a>Azure'da dağıtılan bir kümeden şirket içi bilgisayar tooan HPC Pack HPC iş gönderme
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

Bir şirket içi istemci bilgisayar toosubmit işleri tooa yapılandırma [Microsoft HPC Pack](https://technet.microsoft.com/library/cc514029) Azure kümesinde. Bu makalede, nasıl Azure toohello kümede HTTPS üzerinden toosubmit iş tooset yerel bir bilgisayar istemcisi ile araçları gösterir. Bu şekilde, işleri tooa bulut tabanlı HPC paketi küme, birden çok küme kullanıcı gönderebilirsiniz ancak toohello üstbilgi düğüm VM'ine doğrudan bağlanma veya bir Azure aboneliği erişme.

![Azure iş tooa kümede gönderme][jobsubmit]

## <a name="prerequisites"></a>Ön koşullar
* **Bir Azure VM dağıtılan HPC paketi üstbilgi düğümü** -otomatik araçları gibi kullanmanızı öneririz bir [Azure Hızlı Başlangıç şablonu](https://azure.microsoft.com/documentation/templates/) veya bir [Azure PowerShell Betiği](classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) toodeploy hello baş düğüm ve Küme. Hello DNS ad hello baş düğümü ve bu makaledeki hello adımları tamamlamak için bir Küme Yöneticisi kimlik bilgilerini hello gerekir.
* **İstemci bilgisayar** -HPC Pack istemci yardımcı programları çalıştırmak bir Windows veya Windows Server istemci bilgisayar gerekir (bkz [sistem gereksinimleri](https://technet.microsoft.com/library/dn535781.aspx)). Yalnızca toouse hello HPC paketi web portalı veya REST API toosubmit işleri istiyorsanız, tercih ettiğiniz herhangi bir istemci bilgisayarı kullanabilirsiniz.
* **HPC Pack yükleme medyasını** -tooinstall hello HPC Pack istemci yardımcı programları ' hello ücretsiz yükleme paketinin en son sürümünü HPC Pack (HPC Pack 2012 R2) kullanılabilir için [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkId=328024). Merhaba yüklediğinizden emin olun hello baş düğümünde VM yüklü HPC Pack aynı sürümü.

## <a name="step-1-install-and-configure-hello-web-components-on-hello-head-node"></a>1. adım: Yükleme ve hello baş düğümünde hello web bileşenleri yapılandırma
tooenable, HTTPS üzerinden REST arabirimi toosubmit işleri toohello küme hello HPC paketi web bileşenleri hello HPC paketi üstbilgi düğümü üzerinde yapılandırıldığından emin olun. Bunlar zaten yüklü değilse, ilk hello HpcWebComponents.msi yükleme dosyasını çalıştırarak hello web bileşenlerini yükleyin. Ardından, hello HPC PowerShell betiğini çalıştırarak hello bileşenlerini yapılandırma **kümesi HPCWebComponents.ps1**.

Ayrıntılı yordamlar için bkz: [yükleme hello Microsoft HPC Pack Web Bileşenleri](http://technet.microsoft.com/library/hh314627.aspx).

> [!TIP]
> HPC Pack için belirli Azure hızlı başlangıç şablonlarını yükleyin ve hello web bileşenleri otomatik olarak yapılandırın. Merhaba kullanırsanız [HPC Pack Iaas dağıtım betiği](classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) toocreate hello küme, isteğe bağlı olarak yükleyebilir ve hello web bileşenleri hello dağıtımının bir parçası yapılandırabilirsiniz.
> 
> 

**tooinstall hello web bileşenleri**

1. Toohello üstbilgi düğüm VM'ine hello bir Küme Yöneticisi kimlik bilgilerini kullanarak bağlanın.
2. Merhaba HPC Pack kurulum klasöründen HpcWebComponents.msi hello baş düğümünde çalıştırın.
3. Merhaba Sihirbazı tooinstall hello web bileşenleri Hello adımları izleyin

**tooconfigure hello web bileşenleri**

1. Merhaba baş düğümünde HPC PowerShell'i yönetici olarak başlatın.
2. toochange dizin toohello konumu hello yapılandırma komut dosyası, komut aşağıdaki türü hello:
   
    ```powershell
    cd $env:CCP_HOME\bin
    ```
3. tooconfigure REST arabirimi hello ve hello HPC Web hizmeti, komutu aşağıdaki türü hello başlatın:
   
    ```powershell
    .\Set-HPCWebComponents.ps1 –Service REST –enable
    ```
4. İstendiğinde tooselect bir sertifika hello sertifika seçtiğinizde, toohello Genel DNS adı hello baş düğümü karşılık gelir. Örneğin, hello baş düğüm hello Klasik dağıtım modeli, hello sertifika adını kullanarak VM CN gibi görünüyor dağıtırsanız =&lt;*HeadNodeDnsName*&gt;. cloudapp.net. Merhaba Resource Manager dağıtım modeli kullanırsanız hello sertifika adı CN gibi görünüyor =&lt;*HeadNodeDnsName*&gt;.&lt; *bölge*&gt;. cloudapp.azure.com.
   
   > [!NOTE]
   > Bir şirket içi bilgisayardan toohello baş düğüm işleri gönderdiğinizde, bu sertifika daha sonra seçin. Verme seçin veya hello baş düğümü hello Active Directory etki alanındaki toohello bilgisayar adına karşılık gelen bir sertifika yapılandırın (örneğin, CN =*MyHPCHeadNode.HpcAzure.local*).
   > 
   > 
5. İş gönderme, komutu aşağıdaki türü hello için tooconfigure hello web portalı:
   
    ```powershell
    .\Set-HPCWebComponents.ps1 –Service Portal -enable
    ```
6. Merhaba betik tamamlandıktan sonra durdurmak ve komutları aşağıdaki hello yazarak hello HPC İş Zamanlayıcısı hizmeti yeniden başlatın:
   
    ```powershell
    net stop hpcscheduler
    net start hpcscheduler
    ```

## <a name="step-2-install-hello-hpc-pack-client-utilities-on-an-on-premises-computer"></a>2. adım: bir şirket içi bilgisayar hello HPC Pack istemci yardımcı programları yükle
Tooinstall hello HPC Pack istemci yardımcı programları istiyorsanız, HPC paketi Kurulum dosyaları (tam yükleme) hello karşıdan [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkId=328024). Merhaba yükleme başladığınızda, hello Kurulum hello için seçeneği **HPC Pack istemci yardımcı programları**.

toosubmit işleri toohello üstbilgi düğüm VM'ine toouse hello HPC Pack istemcisi araçları, ayrıca tooexport hello baş düğümünden bir sertifika gerekir ve hello istemci bilgisayara yükleyin. Merhaba sertifika olması gerekir. CER biçimi.

**Merhaba baş düğümünden tooexport hello sertifika**

1. Merhaba baş düğümünde hello Sertifikalar ek bileşenini tooa Microsoft Yönetim Konsolu için hello yerel bilgisayar hesabı ekleyin. Tooadd hello ek bileşenini adımlar için bkz: [Sertifikalar ek bileşenini tooan hello MMC eklemek](https://technet.microsoft.com/library/cc754431.aspx).
2. Merhaba konsol ağacında **sertifikalar – yerel bilgisayar** > **kişisel**ve ardından **Sertifikalar**.
3. Merhaba HPC paketi web bileşenleri için yapılandırılmış hello sertifikayı bulun [1. adım: yükleme ve hello baş düğümünde hello web bileşenleri yapılandırma](#step-1:-install-and-configure-the-web-components-on-the-head-node) (örneğin, CN =&lt;*HeadNodeDnsName* &gt;. cloudapp.net).
4. Merhaba sertifikayı sağ tıklatın ve **tüm görevler** > **verme**.
5. Hello Sertifika Verme Sihirbazı'nı tıklatın **sonraki**ve emin **Hayır, hello özel anahtarı verme** seçilir.
6. Merhaba Sihirbazı tooexport hello DER sertifikada adımlardan kalan izleyin hello ile kodlanmış ikili X.509 (. CER) biçimi.

**Merhaba istemci bilgisayarda tooimport hello sertifika**

1. Merhaba istemci bilgisayarda hello baş düğüm tooa klasöründen dışarı hello sertifika kopyalayın.
2. Merhaba istemci bilgisayarda certmgr.msc çalıştırın.
3. Sertifika Yöneticisi'nde **Sertifikalar – Geçerli kullanıcı** > **güvenilen kök sertifika yetkilileri**, sağ **sertifikaları**ve ardından tıklatın **tüm görevler** > **alma**.
4. Hello Sertifika Alma Sihirbazı'nı tıklatın **sonraki** ve dışarı aktardığınız güvenilen kök sertifika yetkilileri deposuna hello baş düğüm toohello izleyin hello adımları tooimport hello sertifikası.

> [!TIP]
> Merhaba baş düğümüne sertifika yetkilisinde Hello hello istemci bilgisayar tarafından tanınmadığından bir güvenlik uyarısı görebilirsiniz. Test amacıyla, bu uyarı ve tam hello sertifika alma yoksayabilirsiniz.
> 
> 

## <a name="step-3-run-test-jobs-on-hello-cluster"></a>3. adım: Çalıştır test işleri hello kümede
Merhaba üzerinde çalışan işleri deneyin yapılandırmanızı küme Azure'da hello tooverify bilgisayar şirket içi. Örneğin, HPC Pack GUI araçları veya komut satırı komutlarını toosubmit işleri toohello küme kullanabilirsiniz. Bir web tabanlı portal toosubmit işleri de kullanabilirsiniz.

**Merhaba istemci bilgisayarda toorun iş gönderme komutları**

1. Merhaba HPC Pack istemci yardımcı programları yüklü olduğu bir istemci bilgisayarda bir komut istemi başlatın.
2. Bir örnek komutu yazın. Örneğin, toolist hello küme üzerindeki tüm işleri yazın komutu benzer tooone, hello tam DNS adı hello baş düğümü bağlı olarak aşağıdaki hello olarak:
   
    ```command
    job list /scheduler:https://<HeadNodeDnsName>.cloudapp.net /all
    ```
   
    or
   
    ```command
    job list /scheduler:https://<HeadNodeDnsName>.<region>.cloudapp.azure.com /all
    ```
   
   > [!TIP]
   > Merhaba Zamanlayıcı URL'de Hello hello baş düğüm, başlangıç IP adresi değil, tam DNS adı kullanın. Başlangıç IP adresi belirtirseniz, bir hata çok benzer görünür "Merhaba sunucu sertifikası tooeither gereken güven veya hello güvenilir kök deposuna yerleştirilen toobe geçerli zincirine sahip."
   > 
   > 
3. İstendiğinde, hello kullanıcı adını yazın (hello formunda &lt;DomainName&gt;\\&lt;kullanıcı adı&gt;) ve hello HPC Küme Yöneticisi ya da yapılandırdığınız başka bir küme kullanıcının parolası. Merhaba kimlik bilgileri yerel olarak daha fazla iş işlemlerini toostore seçebilirsiniz.
   
    İşlerini listesi görüntülenir.

**Merhaba istemci bilgisayarda toouse HPC İş Yöneticisi**

1. Daha önce bir küme kullanıcının etki alanı kimlik bilgilerini bir işi gönderirken depoladığınız alamadık, kimlik bilgileri Yöneticisi'nde hello kimlik bilgileri ekleyebilirsiniz.
   
    a. Merhaba istemci bilgisayardaki Denetim Masası'ndaki kimlik bilgisi Yöneticisi'ni başlatın.
   
    b. Tıklatın **Windows kimlik bilgileri** > **genel bir kimlik bilgisi Ekle**.
   
    c. Merhaba Internet adresi belirtin (örneğin, https://&lt;HeadNodeDnsName&gt;.cloudapp.net/HpcScheduler veya https://&lt;HeadNodeDnsName&gt;.&lt; Bölge&gt;.cloudapp.azure.com/HpcScheduler) ve hello kullanıcı adı (&lt;DomainName&gt;\\&lt;kullanıcıadı&gt;) ve hello Küme Yöneticisi veya başka bir parola yapılandırdığınız küme kullanıcı.
2. Merhaba istemci bilgisayarda, HPC İş Yöneticisi'ni başlatın.
3. Merhaba, **baş düğüm Seç** iletişim kutusu, türü hello URL toohello baş düğümünde Azure (örneğin, https://&lt;HeadNodeDnsName&gt;. cloudapp.net veya https://&lt;HeadNodeDnsName&gt;. &lt;bölge&gt;. cloudapp.azure.com).
   
    HPC İş Yöneticisi'ni açar ve hello baş düğümünde işlerin bir listesini gösterir.

**Merhaba baş düğüm üzerinde çalışan toouse hello web portalı**

1. Merhaba istemci bilgisayarda bir web tarayıcı başlatmak ve adresleri hello tam DNS adı hello baş düğümü bağlı olarak aşağıdaki hello birini girin:
   
    ```
    https://<HeadNodeDnsName>.cloudapp.net/HpcPortal
    ```
   
    or
   
    ```
    https://<HeadNodeDnsName>.<region>.cloudapp.azure.com/HpcPortal
    ```
2. Görüntülenen hello güvenlik iletişim kutusunda, hello HPC Küme Yöneticisi hello etki alanı kimlik bilgilerini yazın. (Diğer küme kullanıcılar da farklı rolleri ekleyebilirsiniz. Bkz: [küme kullanıcıları yönetme](https://technet.microsoft.com/library/ff919335.aspx).)
   
    Merhaba web portalı toohello iş liste görünümü açılır.
3. "Hello World" Merhaba kümeden hello dizesi döndüren bir örnek iş toosubmit tıklatın **yeni iş** hello sol gezinti içinde.
4. Merhaba üzerinde **yeni iş** sayfasında **gönderme sayfalarından**, tıklatın **HelloWorld**. Merhaba iş gönderme sayfası görüntülenir.
5. Tıklatın **gönderme**. İstenirse, hello HPC Küme Yöneticisi hello etki alanı kimlik bilgilerini sağlayın. Merhaba iş gönderildi ve hello iş kimliği üzerinde hello görünür **İşlerim** sayfası.
6. gönderdiğiniz, hello iş tooview hello sonuçlarını hello iş kimliği'ni tıklatın ve ardından **görünümü görevleri** tooview hello komut çıktısı (altında **çıkış**).

## <a name="next-steps"></a>Sonraki adımlar
* İşlerini toohello hello Azure kümeyle gönderebilmek için [HPC Pack REST API](http://social.technet.microsoft.com/wiki/contents/articles/7737.creating-and-submitting-jobs-by-using-the-rest-api-in-microsoft-hpc-pack-windows-hpc-server.aspx).
* Bir Linux istemciden toosubmit küme işleri istiyorsanız hello Python bakın hello örnek [HPC Pack 2012 R2 SDK'sı ve örnek kod](https://www.microsoft.com/download/details.aspx?id=41633).

<!--Image references-->
[jobsubmit]: ./media/virtual-machines-windows-hpcpack-cluster-submit-jobs/jobsubmit.png
