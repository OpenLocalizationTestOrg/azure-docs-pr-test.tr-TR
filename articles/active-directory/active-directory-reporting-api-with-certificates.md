---
title: aaaGet verileri kullanarak Azure AD raporlama API'si sertifikalarla hello | Microsoft Docs
description: "Nasıl toouse hello Azure AD raporlama API'si ile sertifika kimlik bilgileri tooget verileri kullanıcı müdahalesi olmadan dizinlerinden açıklanmaktadır."
services: active-directory
documentationcenter: 
author: ramical
writer: v-lorisc
manager: kannar
ms.assetid: 
ms.service: active-directory
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/24/2017
ms.author: ramical
ms.openlocfilehash: 00ddfaefe32ea6ae48f276c974a17ddcf84f7894
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-data-using-hello-azure-ad-reporting-api-with-certificates"></a>Hello Azure AD raporlama API'si ile sertifika kullanımı Veri Al
Bu makalede nasıl toouse hello Azure AD raporlama API'si ile sertifika kimlik bilgileri tooget verileri kullanıcı müdahalesi olmadan dizinlerinden anlatılmaktadır. 

## <a name="use-hello-azure-ad-reporting-api"></a>Kullanım hello Azure AD raporlama API'si 
Azure AD raporlama API'si hello aşağıdaki adımları tamamlamanız gerekir:
 *  Ön koşulları yükleme
 *  Uygulamanızda hello sertifikayı ayarlayın
 *  Bir erişim belirteci alma
 *  Merhaba erişim belirteci toocall hello grafik API'sini kullanın

Kaynak kodu hakkında bilgi için bkz. [Rapor API Modülünden Yararlanma](https://github.com/AzureAD/azure-activedirectory-powershell/tree/gh-pages/Modules/AzureADUtils). 

### <a name="install-prerequisites"></a>Ön koşulları yükleme
Azure AD PowerShell V2 toohave ve AzureADUtils modül yüklü gerekir.

1. Azure AD Powershell V2 hello yönergeleri izleyerek, karşıdan yüklenip [Azure Active Directory PowerShell](https://github.com/Azure/azure-docs-powershell-azuread/blob/master/Azure AD Cmdlets/AzureAD/index.md).
2. Hello Azure AD yardımcı programları modülünden karşıdan [Azuread'i/azure-Active Directory-powershell](https://github.com/AzureAD/azure-activedirectory-powershell/blob/gh-pages/Modules/AzureADUtils/AzureADUtils.psm1). 
  Bu modül aşağıdaki çeşitli yardımcı program cmdlet'lerini sağlar:
   * Nuget kullanarak ADAL Hello en son sürümü
   * ADAL kullanarak kullanıcı, uygulama anahtarları ve sertifikalardan erişim belirteçleri
   * Disk belleğine alınmış Grafik API'si işleme sonuçları

**tooinstall hello Azure AD yardımcı programları Modülü:**

1. Bir dizin toosave hello yardımcı programları modül (örneğin, c:\azureAD) oluşturun ve hello modül Github'dan yükleyin.
2. Bir PowerShell oturumu açın ve yeni oluşturduğunuz toohello dizinine gidin. 
3. Merhaba modülünü içeri aktarın ve hello yükleme AzureADUtilsModule cmdlet'ini kullanarak hello PowerShell modülü yolunda yükleyin. 

Merhaba oturum toothis ekran benzer görünmelidir:

  ![Windows PowerShell](./media/active-directory-report-api-with-certificates/windows-powershell.png)

### <a name="set-hello-certificate-in-your-app"></a>Uygulamanızda hello sertifikayı ayarlayın
1. Bir uygulama zaten varsa, nesne kimliği hello Azure Portal ' alın. 

  ![Azure portalına](./media/active-directory-report-api-with-certificates/azure-portal.png)

2. Bir PowerShell oturumu açın ve tooAzure AD connect hello Connect-Azuread'i cmdlet'ini kullanarak.

  ![Azure portalına](./media/active-directory-report-api-with-certificates/connect-azuaread-cmdlet.png)

3. Sertifika kimlik bilgisi tooit AzureADUtils tooadd'ndan Hello yeni AzureADApplicationCertificateCredential cmdlet'ini kullanın. 

>[!Note]
>Tooprovide hello uygulama, daha önce yakalanan bir nesne kimliği gerekir yanı sıra hello sertifika nesnesi (kullanarak bu almak sertifika hello: sürücü).
>


  ![Azure portalına](./media/active-directory-report-api-with-certificates/add-certificate-credential.png)
  
### <a name="get-an-access-token"></a>Bir erişim belirteci alma

tooget bir erişim belirteci AzureADUtils'ndan hello Get-AzureADGraphAPIAccessTokenFromCert cmdlet'ini kullanın. 

>[!NOTE]
>Merhaba hello son bölümünde kullanılan nesne kimliği yerine toouse hello uygulama kimliği gerekir.
>

 ![Azure portalına](./media/active-directory-report-api-with-certificates/application-id.png)

### <a name="use-hello-access-token-toocall-hello-graph-api"></a>Merhaba erişim belirteci toocall hello grafik API'sini kullanın

Şimdi hello komut dosyası oluşturabilirsiniz. Aşağıda hello AzureADUtils'ndan hello Invoke-AzureADGraphAPIQuery cmdlet'ini kullanarak bir örnektir. Bu cmdlet birden çok disk belleğine alınmış sonuçlar işler ve daha sonra bu sonuçlar toohello PowerShell komut zincirini gönderir. 

 ![Azure portalına](./media/active-directory-report-api-with-certificates/script-completed.png)

Hazır tooexport tooa CSV sunulmuştur ve tooa SIEM sisteminde kaydedin. Ayrıca kodunuzu bir zamanlanmış görev tooget Azure AD veri kiracınız düzenli aralıklarla hello kaynak kodunda toostore uygulama anahtarları gerekmeden kayabilir. 

## <a name="next-steps"></a>Sonraki adımlar
[Azure Kimlik Yönetimi Hello temelleri](https://docs.microsoft.com/en-us/azure/active-directory/fundamentals-identity)<br>



