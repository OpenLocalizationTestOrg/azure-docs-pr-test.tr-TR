### <a name="troubleshoot-azure-diagnostics"></a><span data-ttu-id="27c39-101">Azure Tanılama Sorunlarını Giderme</span><span class="sxs-lookup"><span data-stu-id="27c39-101">Troubleshoot Azure Diagnostics</span></span>

<span data-ttu-id="27c39-102">Aşağıdaki hata iletisini alırsanız, Microsoft.insights kaynak sağlayıcısı kayıtlı değildir:</span><span class="sxs-lookup"><span data-stu-id="27c39-102">If you receive the following error message, the Microsoft.insights resource provider is not registered:</span></span>

`Failed to update diagnostics for 'resource'. {"code":"Forbidden","message":"Please register the subscription 'subscription id' with Microsoft.Insights."}`

<span data-ttu-id="27c39-103">Kaynak sağlayıcısını kaydetmek için Azure portalında aşağıdaki adımları uygulayın:</span><span class="sxs-lookup"><span data-stu-id="27c39-103">To register the resource provider, perform the following steps in the Azure portal:</span></span>

1.  <span data-ttu-id="27c39-104">Sol gezinti bölmesinde *Abonelikler*’e tıklayın</span><span class="sxs-lookup"><span data-stu-id="27c39-104">In the navigation pane on the left, click *Subscriptions*</span></span>
2.  <span data-ttu-id="27c39-105">Hata iletisinde belirtilen aboneliği seçin</span><span class="sxs-lookup"><span data-stu-id="27c39-105">Select the subscription identified in the error message</span></span>
3.  <span data-ttu-id="27c39-106">*Kaynak Sağlayıcıları*’ne tıklayın</span><span class="sxs-lookup"><span data-stu-id="27c39-106">Click *Resource Providers*</span></span>
4.  <span data-ttu-id="27c39-107">*Microsoft.insights* sağlayıcısını bulun</span><span class="sxs-lookup"><span data-stu-id="27c39-107">Find the *Microsoft.insights* provider</span></span>
5.  <span data-ttu-id="27c39-108">*Kaydet* bağlantısına tıklayın</span><span class="sxs-lookup"><span data-stu-id="27c39-108">Click the *Register* link</span></span>

![Microsoft.insights kaynak sağlayıcısını kaydetme](./media/log-analytics-troubleshoot-azure-diagnostics/log-analytics-register-microsoft-diagnostics-resource-provider.png)

<span data-ttu-id="27c39-110">*Microsoft.insights* kaynak sağlayıcısı kaydedildikten sonra tanılama yapılandırmasını yeniden deneyin.</span><span class="sxs-lookup"><span data-stu-id="27c39-110">Once the *Microsoft.insights* resource provider is registered, retry configuring diagnostics.</span></span>


<span data-ttu-id="27c39-111">PowerShell'de aşağıdaki hata iletisini alırsanız, PowerShell sürümünüz güncelleştirmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="27c39-111">In PowerShell, if you receive the following error message, you need to update your version of PowerShell:</span></span>

`Set-AzureRmDiagnosticSetting : A parameter cannot be found that matches parameter name 'WorkspaceId'.`

<span data-ttu-id="27c39-112">PowerShell sürümünüz güncelleştirme Kasım 2016 (v2.3.0) ya da daha sonra ' ndaki yönergeleri kullanarak serbest [Azure PowerShell cmdlet'leri kullanmaya başlama](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/) makalesi.</span><span class="sxs-lookup"><span data-stu-id="27c39-112">Update your version of PowerShell to the November 2016 (v2.3.0), or later, release using the instructions in the [Get started with Azure PowerShell cmdlets](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/) article.</span></span>
