<script>
  import Header from './components/Header.svelte';
  import Footer from './components/Footer.svelte';
  import { onMount } from 'svelte';
  let partners = [];
  let products = [];
  let bookProjects = [];
  let events = [];
  let businessEvents = [];
  let websiteProducts = [];
  let current = 0;
  export let name;

  // Tăng số lượng ảnh
  const totalImages = 20;

  let currentInternational = 0;
  const totalInternationalImages = 20;

   // Thay YOUR_API_KEY bằng API key thực của bạn
  const GOOGLE_MAPS_API_KEY = 'YOUR_API_KEY';
  
  // Đúng cho từng section:
onMount(async () => {
  const res = await fetch('http://localhost:8000/api/partners');
  partners = await res.json();
});

onMount(async () => {
  const res = await fetch('http://localhost:8000/api/products');
  products = await res.json();
});

onMount(async () => {
  const res = await fetch('http://localhost:8000/api/book-projects');
  bookProjects = await res.json();
});

onMount(async () => {
  const res = await fetch('http://localhost:8000/api/events');
  events = await res.json();
});

onMount(async () => {
  const res = await fetch('http://localhost:8000/api/business-events');
  businessEvents = await res.json();
});

onMount(async () => {
  const res = await fetch('http://localhost:8000/api/website-products');
  websiteProducts = await res.json();
});

  onMount(() => {
    // Load Google Maps API
    const script = document.createElement('script');
    script.src = `https://maps.googleapis.com/maps/api/js?key=${GOOGLE_MAPS_API_KEY}&callback=initMap`;
    script.async = true;
    script.defer = true;
    
    // Callback function to initialize map
    window.initMap = function() {
      // Tọa độ HM Town
      const hmTownLocation = { lat: 10.7866654, lng: 106.6934333 };
      
      // Tạo map
      const map = new google.maps.Map(document.getElementById('map'), {
        zoom: 16,
        center: hmTownLocation,
        mapTypeId: 'roadmap'
      });
      
      // Tạo marker (điểm đỏ)
      const marker = new google.maps.Marker({
        position: hmTownLocation,
        map: map,
        title: 'Tòa nhà HM Town',
        animation: google.maps.Animation.DROP
      });
      
      // Tạo info window
      const infoWindow = new google.maps.InfoWindow({
        content: `
          <div style="padding: 10px;">
            <h4>Tòa nhà HM Town</h4>
            <p>Floor 14, HM Tower<br>
            412 Lý Chính Thắng, Quận 3<br>
            Hồ Chí Minh 700000</p>
          </div>
        `
      });
      
      // Click marker để hiện info
      marker.addListener('click', () => {
        infoWindow.open(map, marker);
      });
    };
    
    document.head.appendChild(script);
  });

</script>

<div class="app">
  <Header />
  
  <main>
    <section id="gioi-thieu">
      <h1>Giới Thiệu</h1>
      
      <div class="info-grid">
        <div class="info-card">
          <div class="icon">
            <i class="fas fa-home"></i>
          </div>
          <h2>Thành Lập</h2>
          <div class="date">25/02/2014</div>
        </div>

        <div class="info-card">
          <div class="icon">
            <i class="fas fa-layer-group"></i>
          </div>
          <h2>Hoạt Động</h2>
          <p>Lĩnh vực truyền thông quảng cáo, software, xúc tiến thương mại, tổ chức sự kiện, sản xuất chương trình truyền hình, dịch vụ ẩm thực, sản xuất quà tặng,...</p>
        </div>
      </div>
    </section>
    
    <section id="hop-tac">
      <h1>Hợp Tác</h1>
      <div class="partners-grid">
         {#each partners as partner}
      <div class="partner-logo">
        <img src={partner.logo} alt="Logo đối tác" />
      </div>
    {/each}
      </div>
    </section>
    
    <section id="san-pham">
      <h1>Sản Phẩm Đầu Tư</h1>
      <div class="products-grid">
       {#each products as product}
    <a href={product.website} target="_blank" class="product-card">
      <img src={product.image} alt={product.name} />
      <div class="overlay">
        <h3>{product.name}</h3>
        <p>{product.description}</p>
      </div>
    </a>
  {/each}
      </div>
    </section>
    <section id="du-an-sach">
      <h1>Sản Phẩm Hợp Tác - Dự Án Sách</h1>
      <div class="books-grid">
        {#each bookProjects as book}
    <a href={book.website} target="_blank" class="book-card">
      <img src={book.image} alt={book.name} />
      <div class="book-overlay">
        <h3>{book.name}</h3>
        <p>{book.description}</p>
      </div>
    </a>
  {/each}
      </div>
    </section>
    <section id="su-kien-quoc-te">
      <h1>Sự Kiện Quốc Tế</h1>
      <div class="events-grid">
        {#each events as event}
    <a href={event.website} target="_blank" class="event-card">
      <img src={event.image} alt="Sự kiện" />
      <div class="event-info">
        <h3>{event.description}</h3>
        <p class="event-date">{event.date}</p>
      </div>
    </a>
  {/each}
      </div>
    </section>
    
    <section id="to-chuc-su-kien">
      <h1>Tổ Chức Sự Kiện Kết Nối Kinh Doanh</h1>
      <div class="business-events-grid">
        {#each businessEvents as event}
    <a href={event.website} target="_blank" class="business-event-card">
      <img src={event.image} alt="Sự kiện kết nối kinh doanh" />
      <div class="event-info">
        <h3>{event.description}</h3>
        <p class="event-date">{event.date}</p>
      </div>
    </a>
  {/each}
      </div>
    </section>
    <section id="san-pham-website">
      <h1>Sản Phẩm Websites</h1>
      <div class="websites-grid">
        {#each websiteProducts as website}
    <div class="website-card">
      <a href={website.website} target="_blank">
        <img src={website.image} alt={website.name} />
        <div class="overlay">
          <h3>{website.name}</h3>
          <p>{website.description}</p>
        </div>
      </a>
    </div>
  {/each}
      </div>
    </section>
  <section id="hoat-dong-trong-nuoc" style="margin-bottom:40px;">
  <h1 style="text-align:center; color:#005F86;">Hoạt Động Trong Nước</h1>
  <div class="gallery-container">
    <button class="gallery-nav left" on:click={() => current = (current + totalImages - 1) % totalImages}>&lt;</button>
    <img class="gallery-main" src={`/images/internal/${current + 1}.jpg`} alt="Hoạt động ${current + 1}" />
    <button class="gallery-nav right" on:click={() => current = (current + 1) % totalImages}>&gt;</button>
  </div>
  <div class="gallery-thumbnails">
    {#each Array(totalImages) as _, i}
      <img
        src={`/images/internal/${i + 1}.jpg`}
        alt="Thumbnail ${i + 1}"
        class:selected={i === current}
        on:click={() => current = i}
      />
    {/each}
  </div>
</section>
<section id="hanh-dong-quoc-te" style="margin-bottom:40px;">
  <h1 style="text-align:center; color:#005F86;">Hành Động Quốc Tế</h1>
  <div class="gallery-container">
    <button
      class="gallery-nav left"
      on:click={() => currentInternational = (currentInternational + totalInternationalImages - 1) % totalInternationalImages}
    >&lt;</button>
    <img
      class="gallery-main"
      src={`/images/international/${currentInternational + 1}.jpg`}
      alt="Hành động quốc tế ${currentInternational + 1}"
    />
    <button
      class="gallery-nav right"
      on:click={() => currentInternational = (currentInternational + 1) % totalInternationalImages}
    >&gt;</button>
  </div>
  <div class="gallery-thumbnails">
    {#each Array(totalInternationalImages) as _, i}
      <img
        src={`/images/international/${i + 1}.jpg`}
        alt="Thumbnail quốc tế ${i + 1}"
        class:selected={i === currentInternational}
        on:click={() => currentInternational = i}
      />
    {/each}
  </div>
</section>
<section id="lien-he-ban-do" style="margin-bottom:40px;">
  <h1 style="text-align:center; color:#005F86; margin-bottom: 30px;">Vị Trí Văn Phòng</h1>
  <div class="map-container-full">
    <iframe 
      src="https://www.google.com/maps/embed?pb=!1m18!1m12!1m3!1d3919.3356195225133!2d106.6819615752157!3d10.785586359024363!2m3!1f0!2f0!3f0!3m2!1i1024!2i768!4f13.1!3m3!1m2!1s0x31752f07b3a24645%3A0x8190331668205de4!2zVMOyYSBuaMOgIEhNIFRvd24!5e0!3m2!1svi!2s!4v1748275035173!5m2!1svi!2s"
      width="100%" 
      height="500" 
      style="border:0;" 
      allowfullscreen="" 
      loading="lazy" 
      referrerpolicy="no-referrer-when-downgrade"
      title="Vị trí HM Town">
    </iframe>
  </div>
  <div class="address-info" id="dia-chi-lien-he">
    <h3>Địa chỉ liên hệ:</h3>
    <p><strong>Tòa nhà HM Town</strong></p>
    <p>Floor 14, HM Tower, 412 Lý Chính Thắng, Quận 3, Hồ Chí Minh 700000</p>
    <p>📞 Điện thoại: 0865327003</p>
    <p>📧 Email: tmaisaigon@ngaymoisaigon.com</p>
  </div>
</section>
  </main>
  <Footer />
</div>

<style>
  :global(body) {
    margin: 0;
    padding: 0;
    font-family: Arial, sans-serif;
    box-sizing: border-box;
    overflow-x: hidden;
  }
  
  :global(*) {
    box-sizing: inherit;
  }
  
  :global(html) {
    scroll-behavior: smooth;
  }
  
  .app {
    width: 100%;
  }
  
  main {
    padding: 0;
    max-width: 1200px;
    margin: 0 auto;
  }
  
  section {
    margin-bottom: 40px;
    padding: 60px 20px;
  }
  
  #gioi-thieu {
    padding-top: 10px;
    text-align: center;
    background-color: #ffffff;
  }

  .info-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
    gap: 2rem;
    padding: 2rem;
    max-width: 1200px;
    margin: 0 auto;
  }

  .info-card {
    background: white;
    padding: 2rem;
    border-radius: 10px;
    box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
    transition: transform 0.3s ease;
  }

  .info-card:hover {
    transform: translateY(-5px);
  }

  .icon {
    font-size: 2.5rem;
    color: #00AEEF;
    margin-bottom: 1rem;
  }

  .date {
    font-size: 2rem;
    color: #ff4444;
    font-weight: bold;
    margin: 1rem 0;
  }

  h2 {
    color: #333;
    margin-bottom: 1rem;
  }

  p {
    color: #666;
    line-height: 1.6;
  }

  #hop-tac {
    padding: 60px 20px;
    text-align: center;
    background-color: white;
  }

  .partners-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
    gap: 2rem;
    padding: 2rem;
    max-width: 1200px;
    margin: 0 auto;
  }

  .partner-logo {
    padding: 1rem;
    display: flex;
    align-items: center;
    justify-content: center;
    transition: transform 0.3s ease;
  }

  .partner-logo:hover {
    transform: scale(1.05);
  }

  .partner-logo img {
    max-width: 100%;
    height: auto;
    object-fit: contain;
    filter: grayscale(100%);
    transition: filter 0.3s ease;
  }

  .partner-logo:hover img {
    filter: grayscale(0%);
  }

  #san-pham {
    padding: 60px 20px;
    text-align: center;
    background-color: #ffffff;
  }

  .products-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
    gap: 2rem;
    padding: 2rem;
    max-width: 1200px;
    margin: 0 auto;
  }

  .product-card {
    position: relative;
    border-radius: 10px;
    overflow: hidden;
    box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
    transition: transform 0.3s ease;
    aspect-ratio: 3/4;
  }

  .product-card:hover {
    transform: translateY(-5px);
  }

  .product-card img {
    width: 100%;
    height: 100%;
    object-fit: cover;
    filter: grayscale(100%) contrast(120%);
    transition: filter 0.3s ease;
  }

  .product-card:hover img {
    filter: none;
  }

  .overlay {
    position: absolute;
    bottom: 0;
    left: 0;
    right: 0;
    padding: 1.5rem;
    background: linear-gradient(to top, rgba(0,0,0,0.8), transparent);
    color: white;
    opacity: 0;
    transition: opacity 0.3s ease;
  }

  .product-card:hover .overlay {
    opacity: 1;
  }

  .overlay h3 {
    font-size: 1.2rem;
    margin-bottom: 0.5rem;
    color: white;
  }

  .overlay p {
    font-size: 0.9rem;
    color: rgba(255,255,255,0.9);
    margin: 0;
  }

  h1 {
    color: #005F86;
    font-size: 2.5rem;
    margin-bottom: 2rem;
  }

  #du-an-sach {
    padding: 60px 20px;
    text-align: center;
    background-color: #ffffff;
  }

  .books-grid {
    display: flex;
    flex-direction: row;
    flex-wrap: nowrap;
    gap: 1.5rem;
    padding: 2rem;
    max-width: 1200px;
    margin: 0 auto;
    overflow-x: auto; /* Add horizontal scrolling for smaller screens */
  } 

  .book-card {
    position: relative;
    border-radius: 8px;
    overflow: hidden;
    box-shadow: 0 4px 15px rgba(0, 0, 0, 0.1);
    transition: transform 0.3s ease, box-shadow 0.3s ease;
    height: 400px;
    flex: 1 0 280px; /* Give each card equal width but don't shrink below 280px */
    max-width: calc(25% - 1.125rem); /* Each card takes exactly 25% of space minus some gap space */
  }

  .book-card:hover {
    transform: translateY(-10px);
    box-shadow: 0 10px 25px rgba(0, 0, 0, 0.2);
  }

  .book-card img {
    width: 100%;
    height: 100%;
    object-fit: cover;
    transition: transform 0.5s ease;
  }

  .book-card:hover img {
    transform: scale(1.1);
  }

  .book-overlay {
    position: absolute;
    bottom: 0;
    left: 0;
    right: 0;
    top: 0;
    background: linear-gradient(to top, rgba(0, 95, 134, 0.9), rgba(0, 95, 134, 0.7));
    color: white;
    padding: 1.5rem;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    opacity: 0;
    transition: opacity 0.3s ease;
    transform: translateY(20px);
  }

  .book-card:hover .book-overlay {
    opacity: 1;
    transform: translateY(0);
  }

  .book-overlay h3 {
    font-size: 1.4rem;
    margin-bottom: 1rem;
    color: white;
    position: relative;
    padding-bottom: 0.5rem;
  }

  .book-overlay h3:after {
    content: '';
    position: absolute;
    bottom: 0;
    left: 50%;
    transform: translateX(-50%);
    width: 50px;
    height: 2px;
    background-color: #ffffff;
  }

  .book-overlay p {
    font-size: 1rem;
    color: rgba(255, 255, 255, 0.9);
    text-align: center;
    line-height: 1.6;
  }

  /* Responsive adjustments */
  @media (max-width: 992px) {
    .books-grid {
      flex-wrap: wrap;
    }
    
    .book-card {
      max-width: calc(50% - 0.75rem); /* Two cards per row on tablets */
    }
  }

  @media (max-width: 768px) {
    .books-grid {
      grid-template-columns: repeat(auto-fit, minmax(220px, 1fr));
    }
    
    .book-card {
      height: 350px;
    }
    
    .book-overlay h3 {
      font-size: 1.2rem;
    }
    
    .book-overlay p {
      font-size: 0.9rem;
    }
  }

  @media (max-width: 576px) {
    .book-card {
      max-width: 100%; /* One card per row on mobile */
    }
  }

#su-kien-quoc-te {
    padding: 60px 20px;
    text-align: center;
  }

  .events-grid {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
    gap: 2rem;
    padding: 2rem;
    max-width: 1200px;
    margin: 0 auto;
  }

  .event-card {
    position: relative;
    border-radius: 8px;
    overflow: hidden;
    box-shadow: 0 4px 15px rgba(0, 0, 0, 0.1);
    transition: transform 0.3s ease, box-shadow 0.3s ease;
    text-decoration: none;
    color: inherit;
    display: block;
    height: 100%;
  }

  .event-card:hover {
    transform: translateY(-10px);
    box-shadow: 0 10px 25px rgba(0, 0, 0, 0.2);
  }

  .event-card img {
    width: 100%;
    height: 220px;
    object-fit: cover;
    transition: transform 0.5s ease;
  }

  .event-card:hover img {
    transform: scale(1.05);
  }

  .event-info {
    padding: 1.5rem;
    background-color: white;
  }

  .event-info h3 {
    font-size: 1.1rem;
    color: #333;
    margin-bottom: 0.5rem;
    line-height: 1.4;
    transition: color 0.3s ease;
  }

  .event-card:hover .event-info h3 {
    color: #005F86;
  }

  .event-date {
    font-size: 0.9rem;
    color: white;
    display: inline-block;
    padding: 0.3rem 0.6rem;
    background-color: #292626;
    border-radius: 4px;
    margin-top: 0.5rem;
  }

  /* Responsive adjustments */
  @media (max-width: 768px) {
    .events-grid {
      grid-template-columns: repeat(auto-fill, minmax(250px, 1fr));
    }
    
    .event-info h3 {
      font-size: 1rem;
    }
  }

  @media (max-width: 576px) {
    .events-grid {
      grid-template-columns: 1fr;
    }
  }

  #to-chuc-su-kien {
      padding: 60px 20px;
      text-align: center;
      background-color: #ffffff;
    }

    .business-events-grid {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
      gap: 2rem;
      padding: 2rem;
      max-width: 1200px;
      margin: 0 auto;
    }

    .business-event-card {
      position: relative;
      border-radius: 10px;
      overflow: hidden;
      box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
      transition: transform 0.3s ease;
      aspect-ratio: 4/3;
    }

    .business-event-card:hover {
      transform: translateY(-5px);
    }

    .business-event-card img {
      width: 100%;
      height: 100%;
      object-fit: cover;
      transition: transform 0.3s ease;
    }

    .business-event-card:hover img {
      transform: scale(1.05);
    }

    .business-event-card .event-info {
      position: absolute;
      bottom: 0;
      left: 0;
      right: 0;
      padding: 1.5rem;
      background: linear-gradient(to top, rgba(0,0,0,0.8), transparent);
      color: white;
    }

    .business-event-card .event-info h3 {
      font-size: 1.2rem;
      margin-bottom: 0.5rem;
      color: white;
    }

    .business-event-card .event-info .event-date {
      font-size: 0.9rem;
      color: rgba(255,255,255,0.9);
      margin: 0;
    }

    @media (max-width: 768px) {
      .business-events-grid {
        grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
      }
    }

    #san-pham-website {
    padding: 60px 20px;
    text-align: center;
    background-color: #ffffff;
  }

  .websites-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
    gap: 2rem;
    padding: 2rem;
    max-width: 1200px;
    margin: 0 auto;
  }

  .website-card {
    position: relative;
    border-radius: 10px;
    overflow: hidden;
    box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
    transition: transform 0.3s ease;
  }

  .website-card:hover {
    transform: translateY(-5px);
  }

  .website-card img {
    width: 100%;
    height: 100%;
    object-fit: cover;
  }

  .website-card a {
    text-decoration: none;
    color: inherit;
    display: block;
    height: 100%;
  }

  .website-card .overlay {
    position: absolute;
    bottom: 0;
    left: 0;
    right: 0;
    background: linear-gradient(to top, rgba(0,0,0,0.8), transparent);
    color: white;
    padding: 1.5rem;
    opacity: 0;
    transition: opacity 0.3s ease;
  }

  .website-card:hover .overlay {
    opacity: 1;
  }

  .website-card .overlay h3 {
    font-size: 1.4rem;
    margin-bottom: 0.5rem;
    color: white;
  }

  .website-card .overlay p {
    font-size: 1rem;
    color: rgba(255,255,255,0.9);
    margin: 0;
  }

#hoat-dong-trong-nuoc {
    padding: 60px 20px 20px 20px;
    background: #fff;
  }
  .gallery-container {
    display: flex;
    align-items: center;
    justify-content: center;
    background: #333;
    position: relative;
    max-width: 90vw;
    margin: 0 auto;
    min-height: 480px;
  }
  .gallery-main {
    max-width: 900px;
    max-height: 480px;
    width: 100%;
    object-fit: contain;
    background: #222;
    border-radius: 8px;
    margin: 0 40px;
    box-shadow: 0 4px 16px rgba(0,0,0,0.15);
  }
  .gallery-nav {
    background: #222;
    color: #fff;
    border: none;
    font-size: 2rem;
    width: 48px;
    height: 48px;
    border-radius: 6px;
    cursor: pointer;
    z-index: 2;
    transition: background 0.2s;
  }
  .gallery-nav:hover {
    background: #005F86;
  }
  .gallery-nav.left {
    position: absolute;
    left: 0;
  }
  .gallery-nav.right {
    position: absolute;
    right: 0;
  }
  .gallery-thumbnails {
    display: flex;
    gap: 10px;
    justify-content: center;
    align-items: center;
    margin-top: 16px;
    overflow-x: auto;
    padding-bottom: 8px;
  }
  .gallery-thumbnails img {
    width: 80px;
    height: 60px;
    object-fit: cover;
    border-radius: 4px;
    opacity: 0.6;
    cursor: pointer;
    border: 2px solid transparent;
    transition: opacity 0.2s, border 0.2s;
  }
  .gallery-thumbnails img.selected,
  .gallery-thumbnails img:hover {
    opacity: 1;
    border: 2px solid #00AEEF;
  }

    #lien-he-ban-do {
    padding: 60px 0 60px 0; /* Remove horizontal padding */
    background: #ffffff;
  }
  
  #lien-he-ban-do h1 {
    padding: 0 20px; /* Add padding only to title */
  }
  
  .map-container-full {
    width: 100vw; /* Full viewport width */
    position: relative;
    left: 50%;
    right: 50%;
    margin-left: -50vw;
    margin-right: -50vw;
    margin-bottom: 40px;
  }
  
  .address-info {
     max-width: 1000px;
    margin: 0 auto;
    text-align: center;
    background: white;
    padding: 30px;
    border-radius: 12px;
    box-shadow: 0 2px 10px rgba(0,0,0,0.05);
    margin-left: auto;
    margin-right: auto;
  }
  
  .address-info h3 {
    color: #005F86;
    margin-bottom: 15px;
    text-align: center;
  }
  
  .address-info p {
   margin: 8px 0;
    color: #666;
    line-height: 1.6;
    text-align: center;
  }
  
  @media (max-width: 768px) {
    .map-container-full iframe {
      height: 350px;
    }
    
    .address-info {
      padding: 20px;
      margin: 0 auto;
      max-width: calc(100% - 20px);
    }
  }
  
  @media (max-width: 900px) {
    .gallery-main {
      max-width: 100vw;
      max-height: 40vw;
      margin: 0 10px;
    }
    .gallery-container {
      min-height: 220px;
    }
    .gallery-thumbnails img {
      width: 50px;
      height: 38px;
    }
  }
</style>