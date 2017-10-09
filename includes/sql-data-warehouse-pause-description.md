
<!--
includes/sql-data-warehouse-include-pause-description.md

Latest Freshness check:  2016-04-22 , barbkess.

As of circa 2016-04-22, hello following topics might include this include:
articles/sql-data-warehouse/sql-data-warehouse-manage-scale-out-tasks.md
articles/sql-data-warehouse/sql-data-warehouse-manage-scale-out-tasks-powershell.md
articles/sql-data-warehouse/sql-data-warehouse-manage-scale-out-tasks-rest-api.md

-->
<span data-ttu-id="2a1f1-101">toosave maliyetleri'nın, duraklatma ve sürdürme işlem kaynakları isteğe bağlı.</span><span class="sxs-lookup"><span data-stu-id="2a1f1-101">toosave costs, you can pause and resume compute resources on-demand.</span></span> <span data-ttu-id="2a1f1-102">Örneğin, hello veritabanı hello gece sırasında ve hafta sonları kullandığınız olmaz, bu saatlerde duraklatma ve hello günde sürdürün.</span><span class="sxs-lookup"><span data-stu-id="2a1f1-102">For example, if you won't be using hello database during hello night and on weekends, you can pause it during those times, and resume it during hello day.</span></span> <span data-ttu-id="2a1f1-103">Merhaba veritabanı duraklatıldığında Dwu için sizden ücret olmaz.</span><span class="sxs-lookup"><span data-stu-id="2a1f1-103">You won't be charged for DWUs while hello database is paused.</span></span>

<span data-ttu-id="2a1f1-104">Ne zaman bir veritabanı duraklatılamadı:</span><span class="sxs-lookup"><span data-stu-id="2a1f1-104">When you pause a database:</span></span>

* <span data-ttu-id="2a1f1-105">İşlem ve bellek kaynakları kullanılabilir kaynaklar toohello havuzu hello veri merkezinde döndürülür</span><span class="sxs-lookup"><span data-stu-id="2a1f1-105">Compute and memory resources are returned toohello pool of available resources in hello data center</span></span>
* <span data-ttu-id="2a1f1-106">DWU maliyetleri hello Duraklat hello süre sıfırdır.</span><span class="sxs-lookup"><span data-stu-id="2a1f1-106">DWU costs are zero for hello duration of hello pause.</span></span>
* <span data-ttu-id="2a1f1-107">Veri depolama etkilenmez ve verileriniz olduğu gibi kalır.</span><span class="sxs-lookup"><span data-stu-id="2a1f1-107">Data storage is not affected and your data stays intact.</span></span> 
* <span data-ttu-id="2a1f1-108">SQL veri ambarı çalışan ya da sıraya alınan tüm işlemleri iptal eder.</span><span class="sxs-lookup"><span data-stu-id="2a1f1-108">SQL Data Warehouse cancels all running or queued operations.</span></span>

