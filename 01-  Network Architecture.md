 # Network Architecture

 Günümüzde ağların, insanları ve çok daha fazla cihazı birbirine bağlamak, bilgi alışverişi sağlamak gibi görevler için kullanıldığını biliyoruz. Ağlar bu görevleri sağlarken bir yandan da doğru şekilde işleyebilmeleri için ağların güvenliği, verimliliği, ölçeklenebilirliği gibi bir çok önemli etken göz önünde bulundurulmalıdır. Bu etkenler bir ağın "Reliable" olması için gerekli faktörlerdir.

 Kullanıcı beklentilerini karşılamak ve ağın "Reliable" olmasını sağlamak için ağın temel mimarisini oluştaracak 4 ana kavrama dikkat edilir;

 ## Fault Tolerance

 Fault tolerant network, ağdaki bir ya da birden fazla bileşende meydana gelen herhangi bir aksaklığın iletişimi engellememesi için iletimi sadece tek bir yola bağımlı bırakmaktansa, alternatif yolları da tercih edebileceği anlamına gelir. Bu yapı, bir aksamadan dolayı etkilenecek cihazların sayısını minimuma indirmeye olanak tanır. Kaynaktan hedefe giden süreçte birden fazla yol yani alternatif olmasına "Redundancy" denir.

 Bir ağda "Packet Switching" özelliğini kullanmak, o ağın redundancy sağlaması için bir yoldur. Packet switching, verilerin küçük paketlere bölünerek bir ağ üzerinden iletilmesini sağlayan bir veri aktarım yöntemidir. Bu bölünen paketler ağda farklı yolları izleyerek hedefe ulaşır ve varış noktasında doğru sırayla tekrar birleştirilir.

 ## Scalability

 Scalaility yani ölçeklenebilirlik en kısa tabiriyle, bir sistemin veya yapının mevcut koşullara uygun bir biçimde büyültülebilir ya da küçültülebilir olmasıdır. Bu özellik ağlara kolayca cihaz eklenip çıkarılabileceğinin yanı sıra bunu yaparken ağ performansının da olumsuz etkilenmeyeceğinin garantisini verir. Bu, mevcut ağdaki cihazlar ile yeni eklenecek cihazların kabul görmüş standartlar ve protokoller kullanmasıyla sağlanır. Bu sayede yazılım ve donanım satıcılarının, ağları yönetebilmek için yeni bir dizi kural tasarlamasının da önüne geçilir.

## Quality of Service (QoS)

Günümüzde ağlarda birden fazla servisin aynı anda kullanılmasıyla beraber hizmetlerin önceliklendirmesi büyük bir önem taşımaktadır. Mevcut bant genişliğinin aşılması ağda "Congestion" adını verdiğimiz tıkanıklığı meydana getirecektir. Bu durum ağda aynı anda birden fazla hizmet talep edildiğinde oluşur. Örneğin aynı anda hem video izlenip hem de indirme yapıldığında, bant genişliği dolabilir ve donmalar, gecikmeler meydana gelebilir. QoS uygulaması ise bilhassa zamana duyarlı iletişimlere öncelik vererek, ağdaki o hizmetin aksamadan düzgün işlemesine olanak tanır. Örneğin bir ağda, ağ üzerinden VoIP iletişimi gerçekleşirken aynı anda bir web sayfasında istekte bulunuyor olsun. QoS uygulamaları, zamana duyarlı iletişim olan VoIP iletişimine öncelik tanıyarak bir aksama olmamasını sağlayabilir. Burada önemli olan trafiğin içeriği değil ne tür bir trafik olduğudur.

## Network Security

Bir ağın güvenliğini sağlamak iki farklı kategoride incelenebilir;

### Securing the Network Infrastructure

Bu, genel olarak ağ cihazlarına fiziksel erişimi ve üzerinde bulunan yönetim yazılımlarına erişimi engellemek anlamına gelir.

### Securing the Information

Bu ise, ağ üzerinde iletilen ya da ağdaki cihazlarda depolanan bilgiyi korumayı içerir.

Ağ güvenliğini sağlamak için üç temel gereklilik vardır;

### Confidentiality

Veri gizliliği, verilerin sadece amaçlanan veya yetkilendirilmiş kişilerce erişilebilmesi ya da okunabilmesi anlamına gelir.

### Integrity

Veri bütünlülüğü, bir verinin kaynaktan nasıl çıktıysa, hedefe de o şekilde ulaşabilmesini sağlar. Yani verinin transfer sırasında değiştirilmediğinden emin olunmasına olanak tanır.

### Availability

Veri erişilebilirliği, yetkili kullanıcıların veri hizmetlerine zamanında ve güvenilir bir şekilde erişmesini sağlar.
