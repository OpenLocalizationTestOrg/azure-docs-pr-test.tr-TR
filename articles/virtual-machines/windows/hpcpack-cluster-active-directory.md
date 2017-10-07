---
title: "aaaHPC paketi küme Azure Active Directory ile | Microsoft Docs"
description: "Azure Active Directory ile Azure toointegrate bir HPC Pack 2016 nasıl kümesi öğrenin"
services: virtual-machines-windows
documentationcenter: 
author: dlepow
manager: timlt
ms.assetid: 9edf9559-db02-438b-8268-a6cba7b5c8b7
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-multiple
ms.workload: big-compute
ms.date: 11/14/2016
ms.author: danlep
ms.openlocfilehash: 0806e544a468e27ca0567e18c55554811584fbc5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-an-hpc-pack-cluster-in-azure-using-azure-active-directory"></a>Azure Active Directory'yi kullanarak Azure HPC Pack kümede yönetme
[Microsoft HPC Pack 2016](https://technet.microsoft.com/library/cc514029) ile tümleştirmeyi destekleyen [Azure Active Directory](../../active-directory/index.md) (Azure AD) Azure HPC Pack kümede dağıtmak Yöneticiler için.



Yüksek düzey görevler aşağıdaki hello için bu makaledeki Hello adımları izleyin: 
* HPC Pack kümenizi Azure AD kiracınıza el ile tümleştirme
* Yönetmek ve azure'da HPC Pack kümenizdeki işlerini zamanla 

HPC Pack küme çözümünü Azure AD ile tümleştirme, diğer uygulamalar ve hizmetler standart adımları toointegrate izler. Bu makale, Azure AD'de temel kullanıcı yönetimi ile bildiğinizi varsayar. Daha fazla bilgi ve arka plan için hello bkz [Azure Active Directory belgelerindeki](../../active-directory/index.md) ve hello aşağıdaki bölümü.

## <a name="benefits-of-integration"></a>Tümleştirme yararları


Azure Active Directory (Azure AD), toocloud çözümleri çoklu oturum açma (SSO) erişimi sağlayan bir çok kiracılı bulut tabanlı dizin ve kimlik yönetimi hizmetidir.

HPC Pack küme Azure AD ile tümleştirilmesi hedeflerini izleyerek hello elde yardımcı olabilir:

* Merhaba geleneksel Active Directory etki alanı denetleyicisi hello HPC Pack kümeden kaldırın. Bu, bu, iş ve faturalamak hello dağıtım işlemi için gerekli değilse hello küme koruma hello maliyetlerini azaltmaya yardımcı olabilir.
* Azure AD tarafından yapılmadan avantajları aşağıdaki hello yararlanın:
    *   Çoklu oturum açma 
    *   Azure'da hello HPC paketi küme için bir yerel AD kimliği kullanma 

    ![Azure Active Directory ortamı](./media/hpcpack-cluster-active-directory/aad.png)


## <a name="prerequisites"></a>Ön koşullar
* **Azure sanal makinelerinde dağıtılan HPC Pack 2016 küme** - adımları için bkz: [Azure HPC Pack 2016 kümede dağıtmak](hpcpack-2016-cluster.md). Hello DNS ad hello baş düğümü ve bu makaledeki hello adımları tamamlamak için bir Küme Yöneticisi kimlik bilgilerini hello gerekir.

  > [!NOTE]
  > Azure Active Directory Tümleştirme HPC Pack HPC Pack 2016 önce sürümlerinde desteklenmez.



* **İstemci bilgisayar** -bir Windows veya Windows Server istemci bilgisayar çok çalıştırmak HPC Pack istemci yardımcı programları gerekir. Yalnızca toouse hello HPC paketi web portalı veya REST API toosubmit işleri istiyorsanız, tercih ettiğiniz herhangi bir istemci bilgisayarı kullanabilirsiniz.

* **HPC Pack istemci yardımcı programları** -hello HPC Pack istemci yardımcı programları hello istemci bilgisayarda, Microsoft Download Center hello kullanılabilir hello ücretsiz yükleme paketini kullanarak yükleyin.


## <a name="step-1-register-hello-hpc-cluster-server-with-your-azure-ad-tenant"></a>1. adım: Azure AD kiracınıza hello HPC küme sunucusu kaydetme
1. İçinde toohello oturum [Klasik Azure portalı](https://manage.windowsazure.com).
2. Tıklatın **Active Directory** hello soldaki menüden ve aboneliğinizi istenilen dizinde hello'ye tıklayın. İzni tooaccess kaynakları hello dizinde olması gerekir.
3. Tıklatın **kullanıcılar**ve kullanıcı hesapları zaten oluşturuldu veya yapılandırılmış olmadığından emin olun.
4. Tıklatın **uygulamaları** > **Ekle**ve ardından **kuruluşumun geliştirmekte olduğu bir uygulama Ekle**. Başlangıç Sihirbazı'nda bilgisinden hello girin:
    * **Ad** -HPCPackClusterServer
    * **Tür** - seçin **Web uygulaması ve/veya Web API'si**
    * **URL oturum açma**- hello varsayılan olarak hello örnek için ana URL`https://hpcserver`
    * **Uygulama Kimliği URI'si** - `https://<Directory_name>/<application_name>`. Değiştir `<Directory_name`> Merhaba, Azure AD kiracısıdır, örneğin, tam ad ile `hpclocal.onmicrosoft.com`ve değiştirme `<application_name>` daha önce seçtiğiniz hello ada sahip.

5. Merhaba uygulama eklendikten sonra tıklatın **yapılandırma**. Aşağıdaki özelliklere hello yapılandırın:
    * Seçin **Evet** için **uygulamasıdır çok kiracılı**
    * Seçin **Evet** için **kullanıcı atama gerekli tooaccess uygulama**.

6. **Kaydet** düğmesine tıklayın. Kaydetme tamamlandığında tıklayın **yönetmek bildirim**. Bu eylem, uygulamanızın bildirim JavaScript nesne gösterimi (JSON) dosyası indirir. Merhaba bulma tarafından düzenleme indirilen hello bildirimi `appRoles` ayarlama ve uygulama rolü aşağıdaki hello ekleme:
    ```json
    "appRoles": [
        {
        "allowedMemberTypes": [
            "User",
            "Application"
        ],
        "displayName": "HpcAdminMirror",
        "id": "61e10148-16a8-432a-b86d-ef620c3e48ef",
        "isEnabled": true,
        "description": "HpcAdminMirror",
        "value": "HpcAdminMirror"
        },
        {
        "allowedMemberTypes": [
            "User",
            "Application"
        ],
        "description": "HpcUsers",
        "displayName": "HpcUsers",
        "id": "91e10148-16a8-432a-b86d-ef620c3e48ef",
        "isEnabled": true,
        "value": "HpcUsers"
        }
    ],
    ```
7. Merhaba dosyasını kaydedin. Merhaba Portalı'nda, ardından **yönetmek bildirim** > **karşıya bildirim**. Ardından hello düzenlenen bildirimi karşıya yükleyebilirsiniz.
8. Tıklatın **kullanıcılar**, bir kullanıcı seçin ve ardından **atamak**. Merhaba kullanılabilir roller (HpcUsers veya HpcAdminMirror) toohello kullanıcı birine atayın. Merhaba dizinindeki ek kullanıcılar ile bu adımı yineleyin. Küme kullanıcılar hakkında bilgi için bkz: [küme kullanıcıları yönetme](https://technet.microsoft.com/library/ff919335(v=ws.11).aspx).

   > [!NOTE] 
   > hello Azure Active Directory Önizleme dikey penceresinde hello kullanmanızı öneririz toomanage kullanıcılar, [Azure portal](https://portal.azure.com).
   >


## <a name="step-2-register-hello-hpc-cluster-client-with-your-azure-ad-tenant"></a>2. adım: Azure AD kiracınıza hello HPC küme istemci Kaydet

1. İçinde toohello oturum [Klasik Azure portalı](https://manage.windowsazure.com).
2. Tıklatın **Active Directory** hello soldaki menüden ve aboneliğinizi istenilen dizinde hello'ye tıklayın. İzni tooaccess kaynakları hello dizinde olması gerekir.
3. Tıklatın **uygulamaları** > **Ekle**ve ardından **kuruluşumun geliştirmekte olduğu bir uygulama Ekle**. Başlangıç Sihirbazı'nda bilgisinden hello girin:

    * **Ad** -HPCPackClusterClient
    * **Tür** - seçin **yerel istemci uygulaması**
    * **Yeniden yönlendirme URI'si** - `http://hpcclient`

4. Merhaba uygulama eklendikten sonra tıklatın **yapılandırma**. Kopya hello **istemci kimliği** değer ve kaydedin. Bu daha sonra uygulamanızın yapılandırırken gerekir.

5. İçinde **izinleri tooother uygulamaları**, tıklatın **uygulama Ekle**. Arayın ve hello HpcPackClusterServer uygulama (1. adımda oluşturduğunuz) ekleyin.

6. Merhaba, **izinlere temsilci** açılan listesinde, select **erişim HpcClusterServer**. Daha sonra **Kaydet**'e tıklayın.


## <a name="step-3-configure-hello-hpc-cluster"></a>3. adım: hello HPC küme yapılandırma

1. Azure'da toohello HPC Pack 2016 baş düğüm bağlayın.

2. HPC PowerShell'i başlatın.

3. Merhaba aşağıdaki komutu çalıştırın:

    ```powershell

    Set-HpcClusterRegistry -SupportAAD true -AADInstance https://login.microsoftonline.com/ -AADAppName HpcClusterServer -AADTenant <your AAD tenant name> -AADClientAppId <client ID> -AADClientAppRedirectUri http://hpcclient
    ```
    Burada

    * `AADTenant`Hello Azure AD Kiracı adı gibi belirtir`hpclocal.onmicrosoft.com`
    * `AADClientAppId`2. adımda oluşturulan hello uygulaması Hello istemci Kimliğini belirtir.

4. Merhaba HpcSchedulerStateful hizmetini yeniden başlatın.

    Birden çok baş düğümü olan bir kümede hello baş düğüm tooswitch hello birincil çoğaltmadaki hello HpcSchedulerStateful hizmeti için PowerShell komutlarını aşağıdaki hello çalıştırabilirsiniz:

    ```powershell
    Connect-ServiceFabricCluster

    Move-ServiceFabricPrimaryReplica –ServiceName “fabric:/HpcApplication/SchedulerStatefulService”

    ```

## <a name="step-4-manage-and-submit-jobs-from-hello-client"></a>4. adım: Yönetmek ve işleri hello istemciden gönderin

tooinstall hello HPC Pack istemci yardımcı programları, bilgisayarınızda Microsoft Download Center hello HPC Pack 2016 Kurulum dosyaları (tam yükleme) indirin. Merhaba yükleme başladığınızda, hello Kurulum hello için seçeneği **HPC Pack istemci yardımcı programları**.

tooprepare hello istemci bilgisayar, yükleme sırasında kullanılan hello sertifikası [HPC Küme kurulumu](hpcpack-2016-cluster.md) hello istemci bilgisayarda. Kullanım standart Windows sertifika yönetimi yordamları tooinstall hello ortak sertifika toohello **Sertifikalar – Geçerli kullanıcı** > **güvenilen kök sertifika yetkilileri** depolar. 

Şimdi hello HPC Pack komutları çalıştırmak veya da hello HPC Pack İş Yöneticisi GUI'sini toosubmit kullanın ve küme işleri hello Azure AD hesabı'nı kullanarak yönetin. İş gönderme seçenekleri için bkz: [gönderme HPC işleri tooan HPC paketi küme Azure'da](hpcpack-cluster-submit-jobs.md#step-3-run-test-jobs-on-the-cluster).

> [!NOTE]
> Itanium tabanlı sistemler için tooconnect toohello HPC paketi küme azure'da hello için ilk kez çalıştığında, açılır pencereleri görüntülenir. Azure AD kimlik bilgilerini toolog girin. Merhaba belirteci sonra önbelleğe alınır. Kimlik doğrulaması değişiklikleri veya önbelleğe alınmış hello temizlenmediği sürece Azure kullanım hello sonraki bağlantıları toohello kümede belirteç önbelleğe alınmış.
>
  
Örneğin, hello önceki adımları tamamladıktan sonra bir şirket içi istemci işlerden şu şekilde sorgulayabilirsiniz:

```powershell 
Get-HpcJob –State All –Scheduler https://<Azure load balancer DNS name> -Owner <Azure AD account>
```

## <a name="useful-cmdlets-for-job-submission-with-azure-ad-integration"></a>Azure AD tümleştirmesiyle iş gönderme için kullanışlı cmdlet'leri 

### <a name="manage-hello-local-token-cache"></a>Merhaba yerel belirteç önbelleği yönetme

HPC Pack 2016 toomanage hello yerel belirteç önbelleği iki yeni HPC PowerShell cmdlet'leri sağlar. Bu cmdlet, işleri etkileşimsiz göndermek için faydalıdır. Aşağıdaki örnek hello bakın:

```powershell
Remove-HpcTokenCache

$SecurePassword = "<password>" | ConvertTo-SecureString -AsPlainText -Force

Set-HpcTokenCache -UserName <AADUsername> -Password $SecurePassword -scheduler https://<Azure load balancer DNS name> 
```

### <a name="set-hello-credentials-for-submitting-jobs-using-hello-azure-ad-account"></a>Hello Azure AD hesabı kullanarak işleri göndermek için hello kimlik bilgilerini ayarlayın 

Bazen, toorun hello iş hello HPC küme kullanıcı altında isteyebilirsiniz (bir etki alanı kullanıcısı olarak çalıştır etki alanına katılmış HPC Kümesi; hello baş düğümünde bir yerel kullanıcı olarak çalıştırılan bir etki alanına katılmış HPC Kümesi).

1. Aşağıdaki komutları tooset hello kimlik hello kullan:

    ```powershell
    $localUser = “<username>”

    $localUserPassword=”<password>”

    $secpasswd = ConvertTo-SecureString $localUserPassword -AsPlainText -Force

    $mycreds = New-Object System.Management.Automation.PSCredential ($localUser, $secpasswd)

    Set-HpcJobCredential -Credential $mycreds -Scheduler https://<Azure load balancer DNS name>
    ```

2. Ardından aşağıdaki gibi hello işi gönderin. Merhaba iş/görevi $localUser hello işlem düğümlerinde altında çalışır.

    ```powershell
    $emptycreds = New-Object System.Management.Automation.PSCredential ($localUser, (new-object System.Security.SecureString))
    ...
    $job = New-HpcJob –Scheduler https://<Azure load balancer DNS name>

    Add-HpcTask -Job $job -CommandLine "ping localhost" -Scheduler https://<Azure load balancer DNS name>

    Submit-HpcJob -Job $job -Scheduler https://<Azure load balancer DNS name> -Credential $emptycreds
    ```
    
   Varsa `–Credential` ile belirtilmemiş `Submit-HpcJob`, hello iş veya görev Azure AD hesabının hello gibi bir yerel eşlenen kullanıcı altında çalışır. (Merhaba HPC küme hello aynı Azure AD hesabı toorun hello görev hello ad ile yerel bir kullanıcı oluşturur.)
    
3. Hello Azure AD hesabı için genişletilmiş veri ayarlayın. Bu, bir MPI işi hello Azure AD hesabı kullanarak Linux düğümleri üzerinde çalışırken yararlıdır.

   * Hello Azure AD hesabının kendisi için genişletilmiş veri kümesi

      ```powershell
      Set-HpcJobCredential -Scheduler https://<Azure load balancer DNS name> -ExtendedData <data> -AadUser
      ```
      
   * Genişletilmiş veri kümesi ve HPC küme kullanıcı olarak çalıştırın
   
      ```powershell
      Set-HpcJobCredential -Credential $mycreds -Scheduler https://<Azure load balancer DNS name> -ExtendedData <data>
      ```

