 # Network Architecture

 Günümüzde ağların, insanları ve çok daha fazla cihazı birbirine bağlamak, bilgi alışverişi sağlamak gibi görevler için kullanıldığını biliyoruz. Ağlar bu görevleri sağlarken bir yandan da doğru şekilde işleyebilmeleri için ağların güvenliği, verimliliği, ölçeklenebilirliği gibi bir çok önemli etken göz önünde bulundurulmalıdır. Bu etkenler bir ağın "Reliable" olması için gerekli faktörlerdir.

 Kullanıcı beklentilerini karşılamak ve ağın "Reliable" olmasını sağlamak için ağın temel mimarisini oluştaracak 4 ana kavrama dikkat edilir;

 ## Fault Tolerance

 Fault tolerant network, ağdaki bir ya da birden fazla bileşende meydana gelen herhangi bir aksaklığın iletişimi engellememesi için iletimi sadece tek bir yola bağımlı bırakmaktansa, alternatif yolları da tercih edebileceği anlamına gelir. Bu yapı, bir aksamadan dolayı etkilenecek cihazların sayısını minimuma indirmeye olanak tanır. Kaynaktan hedefe giden süreçte birden fazla yol yani alternatif olmasına "Redundancy" denir.

 Bir ağda "Packet Switching" özelliğini kullanmak, o ağın redundancy sağlaması için bir yoldur. Packet switching, verilerin küçük paketlere bölünerek bir ağ üzerinden iletilmesini sağlayan bir veri aktarım yöntemidir. Bu bölünen paketler ağda farklı yolları izleyerek hedefe ulaşır ve varış noktasında doğru sırayla tekrar birleştirilir.

 ## Scalability

 Scability yani ölçeklenebilirlik en kısa tabiriyle, bir sistemin veya yapının mevcut koşullara uygun bir biçimde büyültülebilir ya da küçültülebilir olmasıdır. Bu özellik ağlara kolayca cihaz eklenip çıkarılabileceğinin yanı sıra bunu yaparken ağ performansının da olumsuz etkilenmeyeceğinin garantisini verir. Bu, mevcut ağdaki cihazlar ile yeni eklenecek cihazların kabul görmüş standartlar ve protokoller kullanmasıyla sağlanır. Bu sayede yazılım ve donanım satıcılarının, ağları yönetebilmek için yeni bir dizi kural tasarlamasının da önüne geçilir.
