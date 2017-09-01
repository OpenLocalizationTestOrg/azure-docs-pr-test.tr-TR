**1. Müşteriler retiring SDK'sına nasıl bildirilir?**

Microsoft, desteklenen bir SDK sorunsuz bir geçiş kolaylaştırmak için 12 ay öncelikli bildirimi destek sonuna retiring SDK'sının sağlayacaktır. Ayrıca, müşterilerin çeşitli iletişim kanalları – Azure Yönetim Portalı, Geliştirici Merkezi, blog gönderisi bildirilir ve hizmet yöneticileri için doğrudan iletişim atanır.

**2. Müşteriler 12 aylık dönem boyunca "yüklenecek" devre dışı bırakılan bir DocumentDB SDK kullanan uygulamalar geliştirebilirler?** 

Evet, müşteri yazar, dağıtmak ve 12 ay yetkisiz kullanım süresi sırasında "yüklenecek" Çekildi DocumentDB SDK'sını kullanan uygulamaları değiştirmek için tam erişime sahip. 12 aylık yetkisiz kullanım süresi boyunca, müşterilerin yeni desteklenen bir sürümünü DocumentDB SDK'sı uygun şekilde geçirmek için önerilir.

**3. Müşteriler yazabilir ve 12 ay bildirim süre devre dışı bırakılan bir DocumentDB SDK'yı kullanarak uygulamaları değiştirmeyi?**

12 aylık bildirim süre SDK kullanımdan kaldırılacaktır. DocumentDB için herhangi bir erişimin Çekildi SDK kullanarak bir uygulama tarafından DocumentDB platformu tarafından izin verilmiyor. Ayrıca, Microsoft müşteri desteği devre dışı bırakılan SDK'sağlamaz.

**4. Desteklenmeyen DocumentDB SDK sürümü kullanan müşterinin çalışan uygulamalar için ne olur?**

DocumentDB hizmetini devre dışı bırakılan bir SDK sürümüyle bağlanmak için yapılan tüm denemeleri reddedilir. 

**5. Yeni özellikleri ve işlevleri tüm kullanımdan olmayan SDK'ları için uygulanır?**

Yeni özellikler ve işlevler yalnızca yeni sürümler eklenir. SDK eski, olmayan-kullanımdan, bir sürümünü kullanıyorsanız, istekleri documentdb'ye önceki gibi çalışmaya devam eder ancak tüm yeni özelliklere erişim yoktur.  

**6. Uygulamam sonlandırma tarihinden önce güncelleştirirseniz olamaz ne yapmalıyım?**

Son SDK'sını olabildiğince erken yükseltmenizi öneririz. Bir SDK devre dışı bırakma için etiketli sonra 12 ay uygulamanızı güncelleştirmeniz gerekir. Herhangi bir nedenle, olamaz bu zaman çerçevesi içinde uygulama güncelleştirmenizi tamamlamak sonra başvurun, [Cosmos DB takım](mailto:askcosmosdb@microsoft.com) ve kesme tarihinden önce kendi Yardım isteyin.

