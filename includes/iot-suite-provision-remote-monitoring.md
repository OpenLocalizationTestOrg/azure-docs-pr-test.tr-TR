## <a name="provision-the-solution"></a><span data-ttu-id="7993d-101">Çözüm sağlama</span><span class="sxs-lookup"><span data-stu-id="7993d-101">Provision the solution</span></span>

<span data-ttu-id="7993d-102">Önceden yapılandırılmış uzaktan izleme çözümünüzü hesabınızda henüz hazırlamadıysanız:</span><span class="sxs-lookup"><span data-stu-id="7993d-102">If you haven't already provisioned the remote monitoring preconfigured solution in your account:</span></span>

1. <span data-ttu-id="7993d-103">Azure hesabı kimlik bilgilerinizi kullanarak [azureiotsuite.com][lnk-azureiotsuite] adresinde oturum açın ve çözüm oluşturmak için **+** seçeneğine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="7993d-103">Log on to [azureiotsuite.com][lnk-azureiotsuite] using your Azure account credentials, and click **+** to create a solution.</span></span>
2. <span data-ttu-id="7993d-104">**Uzaktan izleme** kutucuğunda **Seç**'e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="7993d-104">Click **Select** on the **Remote monitoring** tile.</span></span>
3. <span data-ttu-id="7993d-105">Önceden yapılandırılmış uzaktan izleme çözümünüz için bir **Çözüm adı** girin.</span><span class="sxs-lookup"><span data-stu-id="7993d-105">Enter a **Solution name** for your remote monitoring preconfigured solution.</span></span>
4. <span data-ttu-id="7993d-106">Çözümü sağlamak için kullanmak istediğiniz **Bölge** ve **Abonelik** seçimini yapın.</span><span class="sxs-lookup"><span data-stu-id="7993d-106">Select the **Region** and **Subscription** you want to use to provision the solution.</span></span>
5. <span data-ttu-id="7993d-107">Hazırlama işlemini başlatmak için **Çözümü Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="7993d-107">Click **Create Solution** to begin the provisioning process.</span></span> <span data-ttu-id="7993d-108">Bu işlemin çalışması genellikle birkaç dakika sürer.</span><span class="sxs-lookup"><span data-stu-id="7993d-108">This process typically takes several minutes to run.</span></span>

### <a name="wait-for-the-provisioning-process-to-complete"></a><span data-ttu-id="7993d-109">Hazırlama işleminin tamamlanmasını bekleme</span><span class="sxs-lookup"><span data-stu-id="7993d-109">Wait for the provisioning process to complete</span></span>
1. <span data-ttu-id="7993d-110">Çözümünüzün **Hazırlama** durumuna sahip olan kutucuğuna tıklayın.</span><span class="sxs-lookup"><span data-stu-id="7993d-110">Click the tile for your solution with **Provisioning** status.</span></span>
2. <span data-ttu-id="7993d-111">Azure hizmetleri Azure aboneliğinize dağıtılırken **Hazırlama durumlarına** dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="7993d-111">Notice the **Provisioning states** as Azure services are deployed in your Azure subscription.</span></span>
3. <span data-ttu-id="7993d-112">Hazırlama tamamlandığında durum **Hazır** olarak değişir.</span><span class="sxs-lookup"><span data-stu-id="7993d-112">Once provisioning completes, the status changes to **Ready**.</span></span>
4. <span data-ttu-id="7993d-113">Kutucuğa tıkladığınızda sağ bölmede çözümünüzün ayrıntılarını görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="7993d-113">Click the tile to see the details of your solution in the right-hand pane.</span></span>

> [!NOTE]
> <span data-ttu-id="7993d-114">Önceden yapılandırılmış çözümün dağıtımında sorunlarla karşılaşıyorsanız bkz. [Azureiotsuite.com sitesindeki izinler][lnk-permissions] ve [SSS][lnk-faq].</span><span class="sxs-lookup"><span data-stu-id="7993d-114">If you are encountering issues deploying the pre-configured solution, review [Permissions on the azureiotsuite.com site][lnk-permissions] and the [FAQ][lnk-faq].</span></span> <span data-ttu-id="7993d-115">Sorunlar devam ederse [portalda][lnk-portal] bir hizmet bileti oluşturun.</span><span class="sxs-lookup"><span data-stu-id="7993d-115">If the issues persist, create a service ticket on the [portal][lnk-portal].</span></span>
> 
> 

<span data-ttu-id="7993d-116">Görmeyi beklediğiniz ancak çözümünüz için listelenmemiş ayrıntılar mı var?</span><span class="sxs-lookup"><span data-stu-id="7993d-116">Are there details you'd expect to see that aren't listed for your solution?</span></span> <span data-ttu-id="7993d-117">[User Voice](https://feedback.azure.com/forums/321918-azure-iot)'da bize özellik önerileri verin.</span><span class="sxs-lookup"><span data-stu-id="7993d-117">Give us feature suggestions on [User Voice](https://feedback.azure.com/forums/321918-azure-iot).</span></span>

[lnk-azureiotsuite]: https://www.azureiotsuite.com
[lnk-permissions]: ../articles/iot-suite/iot-suite-permissions.md
[lnk-portal]: http://portal.azure.com/
[lnk-faq]: ../articles/iot-suite/iot-suite-faq.md