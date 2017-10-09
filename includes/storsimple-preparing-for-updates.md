<!--author=jgerend last changed: 03/16/16-->

## <a name="preparing-for-updates"></a><span data-ttu-id="1aef6-101">Güncelleştirmeler için hazırlama</span><span class="sxs-lookup"><span data-stu-id="1aef6-101">Preparing for updates</span></span>
<span data-ttu-id="1aef6-102">Tarama ve hello güncelleştirmeyi uygulamak için önce aşağıdaki adımları tooperform hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="1aef6-102">You will need tooperform hello following steps before you scan and apply hello update:</span></span>

1. <span data-ttu-id="1aef6-103">Bir bulut anlık görüntüsünü hello cihaz verileri alın.</span><span class="sxs-lookup"><span data-stu-id="1aef6-103">Take a cloud snapshot of hello device data.</span></span>
2. <span data-ttu-id="1aef6-104">IP'leri sabit denetleyicinizi yönlendirilebilir ve toohello Internet bağlanabildiğinizden emin olun.</span><span class="sxs-lookup"><span data-stu-id="1aef6-104">Ensure that your controller fixed IPs are routable and can connect toohello Internet.</span></span> <span data-ttu-id="1aef6-105">Bu IP'ler sabit kullanılan tooservice güncelleştirmeleri tooyour aygıt olacaktır.</span><span class="sxs-lookup"><span data-stu-id="1aef6-105">These fixed IPs will be used tooservice updates tooyour device.</span></span> <span data-ttu-id="1aef6-106">Bu test cmdlet'i her denetleyicisinde hello Windows PowerShell arabiriminden hello cihaz aşağıdaki hello edebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="1aef6-106">You can test this by running hello following cmdlet on each controller from hello Windows PowerShell interface of hello device:</span></span>
   
     `Test-Connection -Source <Fixed IP of your device controller> -Destination <Any IP or computer name outside of datacenter network> `
   
    <span data-ttu-id="1aef6-107">**Örnek çıktı için sabit IP'leri toohello Internet bağlanabildiğinizde Bağlantıyı Sına**</span><span class="sxs-lookup"><span data-stu-id="1aef6-107">**Sample output for Test-Connection when fixed IPs can connect toohello Internet**</span></span>

        Controller0>Test-Connection -Source 10.126.173.91 -Destination bing.com

        Source      Destination     IPV4Address      IPV6Address
        ----------------- -----------  -----------
        HCSNODE0  bing.com        204.79.197.200
        HCSNODE0  bing.com        204.79.197.200
        HCSNODE0  bing.com        204.79.197.200
        HCSNODE0  bing.com        204.79.197.200

        Controller0>Test-Connection -Source 10.126.173.91 -Destination  204.79.197.200

        Source      Destination       IPV4Address    IPV6Address
        ----------------- -----------  -----------
        HCSNODE0  204.79.197.200  204.79.197.200
        HCSNODE0  204.79.197.200  204.79.197.200
        HCSNODE0  204.79.197.200  204.79.197.200
        HCSNODE0  204.79.197.200  204.79.197.200

<span data-ttu-id="1aef6-108">Bu el ile ön denetimleri başarıyla tamamladıktan sonra tooscan devam ve hello güncelleştirmeleri yükleyin.</span><span class="sxs-lookup"><span data-stu-id="1aef6-108">After you have successfully completed these manual pre-checks, you can proceed tooscan and install hello updates.</span></span>

