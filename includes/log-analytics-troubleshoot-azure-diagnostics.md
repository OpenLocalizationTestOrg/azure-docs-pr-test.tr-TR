### <a name="troubleshoot-azure-diagnostics"></a><span data-ttu-id="8647a-101">Azure Tanılama Sorunlarını Giderme</span><span class="sxs-lookup"><span data-stu-id="8647a-101">Troubleshoot Azure Diagnostics</span></span>

<span data-ttu-id="8647a-102">Merhaba aşağıdaki hata iletisini alırsanız, hello Microsoft.ınsights kaynak sağlayıcısı kayıtlı değil:</span><span class="sxs-lookup"><span data-stu-id="8647a-102">If you receive hello following error message, hello Microsoft.insights resource provider is not registered:</span></span>

`Failed tooupdate diagnostics for 'resource'. {"code":"Forbidden","message":"Please register hello subscription 'subscription id' with Microsoft.Insights."}`

<span data-ttu-id="8647a-103">tooregister hello kaynak sağlayıcısı hello Azure Portalı'ndaki adımları izleyerek hello gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="8647a-103">tooregister hello resource provider, perform hello following steps in hello Azure portal:</span></span>

1.  <span data-ttu-id="8647a-104">Merhaba Gezinti hello sol taraftaki bölmede *abonelikleri*</span><span class="sxs-lookup"><span data-stu-id="8647a-104">In hello navigation pane on hello left, click *Subscriptions*</span></span>
2.  <span data-ttu-id="8647a-105">Merhaba hata iletisinde belirtilen hello aboneliği seçin</span><span class="sxs-lookup"><span data-stu-id="8647a-105">Select hello subscription identified in hello error message</span></span>
3.  <span data-ttu-id="8647a-106">*Kaynak Sağlayıcıları*’ne tıklayın</span><span class="sxs-lookup"><span data-stu-id="8647a-106">Click *Resource Providers*</span></span>
4.  <span data-ttu-id="8647a-107">Hello bulur *Microsoft.ınsights* sağlayıcısı</span><span class="sxs-lookup"><span data-stu-id="8647a-107">Find hello *Microsoft.insights* provider</span></span>
5.  <span data-ttu-id="8647a-108">Merhaba tıklatın *kaydetmek* bağlantı</span><span class="sxs-lookup"><span data-stu-id="8647a-108">Click hello *Register* link</span></span>

![Microsoft.insights kaynak sağlayıcısını kaydetme](./media/log-analytics-troubleshoot-azure-diagnostics/log-analytics-register-microsoft-diagnostics-resource-provider.png)

<span data-ttu-id="8647a-110">Bir kez hello *Microsoft.ınsights* kaynak sağlayıcısı kayıtlı, tanılamaları yapılandırmayı yeniden deneyin.</span><span class="sxs-lookup"><span data-stu-id="8647a-110">Once hello *Microsoft.insights* resource provider is registered, retry configuring diagnostics.</span></span>


<span data-ttu-id="8647a-111">Merhaba aşağıdaki hata iletisini alırsanız, PowerShell'de tooupdate PowerShell sürümünüz ihtiyacınız:</span><span class="sxs-lookup"><span data-stu-id="8647a-111">In PowerShell, if you receive hello following error message, you need tooupdate your version of PowerShell:</span></span>

`Set-AzureRmDiagnosticSetting : A parameter cannot be found that matches parameter name 'WorkspaceId'.`

<span data-ttu-id="8647a-112">Kasım 2016 (v2.3.0) PowerShell toohello uygulamanızın sürümünü güncelleştirin veya hello hello yönergeleri kullanarak daha sonra serbest [Azure PowerShell cmdlet'leri kullanmaya başlama](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/) makalesi.</span><span class="sxs-lookup"><span data-stu-id="8647a-112">Update your version of PowerShell toohello November 2016 (v2.3.0), or later, release using hello instructions in hello [Get started with Azure PowerShell cmdlets](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/) article.</span></span>
