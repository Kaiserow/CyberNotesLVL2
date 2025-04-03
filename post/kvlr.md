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

# Hierarchical Network Design

## Physical and Logical Addresses

Bir insanın ismi genelde değişmez ama yaşadığı yerin adresi değişebilir. MAC adresleri de aynı insanların isimlerine benzer bir şekilde fiziksel adres olarak NIC'e atanır ve değişmez. Bunun yanında IP adresleri ise insanların yaşadığı yerlerin adreslerine benzetilebilir. IP adresleri, bir hostun hangi ağda nerede konumlandığı belirlemeye yarayan logical (mantıksal) adreslerdir. Ağdaki iletişim için hem MAC adresleri hem de IP adresleri vazgeçilmezdir ve birlikte kullanılmalıdır. Neden sadece MAC adresi kullanılmadığını merak ediyor olabilirsiniz. Örneğin, insanların sadece isimleri kullanarak birbirine mektup göndermeye çalıştığını düşünün. O isimden dünyada sadece bir tane olsa dahi, adresi olmadan o kişiyi bulmanın ne kadar zor olabileceğini tahmin edebilirsiniz. Bu yüzden ağlar da, spesifik olarak bir yere mesaj gönderilmesi için IP adreslerine ihtiyaç duyarlar. 

Aslında IP adresleri ağları bloklara bölerek, tüm cihazların tek bir ağda olmasını engeller. Bu sayede milyonlarca cihaz arasından birini bulmak yerine çok daha küçük sayılar arasından cihazı bulabiliriz. Bununla beraber, cihazların aynı ağda olması aynı zamanda aynı broadcast domain içerisinde olması demek olduğundan, o ağda broadcast yapılması halinde fazlasıyla gereksiz trafik meydana gelecek ve ağ performansı olumsuz yönde etkilenecektir. Bu iki etkeni göz önünde bulundurduğumuzda, büyük ağları daha küçük ağlara bölmek elzemdir.

Bunu yapmanın bir yolu da "Hierarchical Design Model"ını dikkate almaktır.

## Access, Distribution, and Core Layer

Hiyerarşik bir ağ dizaynı dikkate alındığında yukarıdaki 3 katman göz önünde bulundurulmalıdır.

### Access Layer

Access Layer, end-user cihazlarını ağa dahil etmeye ve hostların diğer hostlara bağlanmasına yarar. Bunları yapan ana cihazlar ise genelde layer 2 switch ve access point'tir (AP). Aynı access layer içerisinde bulunan cihazlar aynı network portiona sahip olacaktır. Mesajın yerelde kalmayıp farklı bir ağa gitmesi gerekirse, bu konumda distribution layer devreye girmelidir.

### Distribution Layer

Bu katman, ağları birbirine bağlayan bir nokta görevi görür ve ağlar arasında trafik akışını kontrol eder. Hostların "routing" yani yönlendirme işlemleri burada yapılır. Distribution layer, access layer ile core layer arasında aracılık yaparak, aradaki trafiğin türünü ve miktarını kontrol eder. Layer 3 switchlerin ve routerlerin burada çalıştığını söyleyebiliriz.

### Core Layer

High-speed bağlantılar ve "redundant" (yedek) bağlantılar sağlayan bir backbone katmanıdır. Büyük miktarda veriyi end networklere taşımakla görevlidir. Çok güçlü ve yüksek hıza sahip switchler ve routerler bu katmana dahil olabilir. Bu katmanın ana hedefi veriyi en hızlı şekilde transfer etmektir.

