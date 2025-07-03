<script>
  import Slider from './Slider.svelte';
  let menuOpen = false;
  let searchQuery = '';
  let searchResults = [];
  let showResults = false;
  
   // Demo: Tìm kiếm trên mảng dữ liệu mẫu (bạn thay bằng API hoặc dữ liệu thật)
  const data = [
    { title: 'Giới Thiệu', anchor: '#gioi-thieu' },
    { title: 'Hợp Tác', anchor: '#hop-tac' },
    { title: 'Sản Phẩm Đầu Tư', anchor: '#san-pham' },
    { title: 'Dự Án Sách', anchor: '#du-an-sach' },
    { title: 'Sự Kiện Quốc Tế', anchor: '#su-kien-quoc-te' },
    { title: 'Kết Nối Kinh Doanh', anchor: '#to-chuc-su-kien' },
    { title: 'Sản Phẩm Websites', anchor: '#san-pham-website' },
    { title: 'Hoạt Động Trong Nước', anchor: '#hoat-dong-trong-nuoc' },
    { title: 'Hành Động Quốc Tế', anchor: '#hanh-dong-quoc-te' },
    { title: 'Vị Trí Văn Phòng', anchor: '#lien-he-ban-do' },
    { title: 'Địa Chỉ Liên Hệ', anchor: '#dia-chi-lien-he' }
  ];

  // Danh sách các hình ảnh cho slider
  const sliderImages = [
    '/images/general/background-1.jpg',
    '/images/general/background-2.jpg',
    '/images/general/background-3.jpg',
    '/images/general/background-4.jpg',
    '/images/general/background-5.jpg',
    '/images/general/background-6.jpg',
    '/images/general/background-7.jpg',
    '/images/general/background-8.jpg',
    '/images/general/background-9.jpg',
    '/images/general/background-10.jpg'
  ];
  
  function toggleMenu() {
    menuOpen = !menuOpen;
  }
  
   function handleSearch(e) {
    searchQuery = e.target.value;
    if (searchQuery.trim().length > 0) {
      searchResults = data.filter(item =>
        item.title.toLowerCase().includes(searchQuery.toLowerCase())
      );
      showResults = true;
    } else {
      searchResults = [];
      showResults = false;
    }
  }

  function goToResult(anchor) {
    window.location.hash = anchor;
    showResults = false;
    searchQuery = '';
  }

  // Hàm xử lý khi nhấp vào liên kết menu
  function handleMenuClick(event) {
    // Lấy ID section từ href
    const targetId = event.target.getAttribute('href');
    
    // Đóng menu
    menuOpen = false;
    
    // Kiểm tra nếu là liên kết nội bộ (#) thì xử lý cuộn mượt
    if (targetId && targetId.startsWith('#')) {
      event.preventDefault();
      
      const targetElement = document.querySelector(targetId);
      
      if (targetElement) {
        // Tính toán vị trí cuộn, trừ đi một khoảng để tránh bị che bởi header cố định
        const headerOffset = 80; // Chiều cao của header hoặc khoảng trống mong muốn
        const elementPosition = targetElement.getBoundingClientRect().top;
        const offsetPosition = elementPosition + window.pageYOffset - headerOffset;
        
        // Cuộn đến vị trí đích
        window.scrollTo({
          top: offsetPosition,
          behavior: "smooth"
        });
      }
    }
  }
</script>

<header>
  <div class="header-container">
    <button class="menu-button" on:click={() => menuOpen = !menuOpen} aria-label="Menu">
      <span class="menu-icon"></span>
      <span class="menu-icon"></span>
      <span class="menu-icon"></span>
    </button>
    
<!-- Thanh search nằm giữa menu và logo -->
  <div class="header-search">
    <input
      type="text"
      placeholder="Tìm kiếm..."
      bind:value={searchQuery}
      on:input={handleSearch}
      on:focus={() => showResults = true}
      on:blur={() => setTimeout(() => showResults = false, 200)}
    />
    <i class="bi bi-search search-icon"></i>
    {#if showResults && searchResults.length > 0}
      <ul class="search-results">
        {#each searchResults as result}
          <li on:mousedown={() => goToResult(result.anchor)}>
            {result.title}
          </li>
        {/each}
      </ul>
    {/if}
  </div>

    <div class="logo">
      <img src="/images/logo_tmaisaigon.jpg" alt="TMAI Saigon Logo" />
    </div>
  </div>
  
  <!-- Thay thế hero-image bằng Slider component -->
  <Slider images={sliderImages} interval={5000} />
  
  <nav class="main-menu {menuOpen ? 'open' : ''}">
    <div class="menu-close" on:click={toggleMenu}>✕</div>
    <ul>
      <li><a href="#gioi-thieu" on:click={handleMenuClick}>Giới Thiệu</a></li>
      <li><a href="#hop-tac" on:click={handleMenuClick}>Hợp Tác</a></li>
      <li><a href="#san-pham" on:click={handleMenuClick}>Sản Phẩm Đầu Tư</a></li>
      <li><a href="#du-an-sach" on:click={handleMenuClick}>Sản Phẩm Hợp Tác - Dự Án Sách</a></li>
      <li><a href="#su-kien-quoc-te" on:click={handleMenuClick}>Sự Kiện Quốc Tế</a></li>
      <li><a href="#to-chuc-su-kien" on:click={handleMenuClick}>Kết Nối Kinh Doanh</a></li>
      <li><a href="#san-pham-website" on:click={handleMenuClick}>Sản Phẩm Websites</a></li>
      <li><a href="#hoat-dong-trong-nuoc" on:click={handleMenuClick}>Hoạt Động Trong Nước</a></li>
      <li><a href="#hanh-dong-quoc-te" on:click={handleMenuClick}>Hành Động Quốc Tế</a></li>
      <li><a href="#lien-he-ban-do" on:click={handleMenuClick}>Vị Trí Văn Phòng</a></li>
      <li><a href="#dia-chi-lien-he" on:click={handleMenuClick}>Địa Chỉ Liên Hệ</a></li>
    </ul>
  </nav>
  
  {#if menuOpen}
    <div class="overlay" on:click={toggleMenu}></div>
  {/if}
</header>

<style>
  header {
    position: relative;
    width: 100%;
    height: 100vh;
  }
  
  .header-container {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    display: flex;
    justify-content: flex-end; /* Đẩy logo sang phải */
    align-items: center;
    padding: 1rem;
    z-index: 10;
  }
  
  .menu-button {
    position: fixed;
    top: 24px;
    left: 24px;
    z-index: 1001;
    background: #00AEEF; /* Đổi từ #fff thành màu xanh (#00AEEF) */
    border: none;
    border-radius: 50%;
    width: 48px;
    height: 48px;
    box-shadow: 0 2px 8px rgba(0,0,0,0.12);
    display: flex;
    flex-direction: column; /* Đảm bảo 3 gạch xếp theo cột */
    align-items: center;
    justify-content: center;
    cursor: pointer;
    transition: all 0.3s ease; /* Thêm transition cho mượt */
  }
  
  .menu-button:hover {
    background-color: #fff; /* Khi hover thì đổi thành màu trắng */
  }
  
  .menu-icon {
    display: block;
    height: 3px;
    width: 24px; /* Độ rộng cố định cho gạch ngang */
    background-color: #fff; /* Màu gạch thành trắng */
    border-radius: 2px;
    transition: all 0.3s ease;
    margin: 2px 0;
  }
  
  .menu-button:hover .menu-icon {
    background-color: #00AEEF; /* Khi hover thì gạch đổi thành màu xanh */
  }
  
  .logo {
    height: 60px;
    margin-right: 20px;
  }
  
  .logo img {
    height: 100%;
    object-fit: contain;
  }
  
  .main-menu {
    position: fixed;
    top: 0;
    left: -300px;
    width: 300px;
    height: 100vh;
    background-color: rgba(0, 0, 0, 0.95);
    transition: all 0.3s ease;
    z-index: 100;
    overflow-y: auto;
    padding-top: 60px;
  }
  
  .main-menu.open {
    left: 0;
    box-shadow: 0 0 15px rgba(0, 0, 0, 0.5);
  }
  
  .menu-close {
    position: absolute;
    top: 20px;
    right: 20px;
    color: white;
    font-size: 24px;
    cursor: pointer;
  }
  
  .main-menu ul {
    list-style: none;
    padding: 0;
    margin: 0;
  }
  
  .main-menu li {
    border-bottom: 1px solid rgba(255, 255, 255, 0.1);
  }
  
  .main-menu a {
    color: white;
    text-decoration: none;
    font-size: 16px;
    display: block;
    padding: 15px 25px;
    transition: background-color 0.3s;
    position: relative;
    overflow: hidden;
  }
  
  .main-menu a:hover {
    background-color: rgba(0, 174, 239, 0.3);
  }
  
  .main-menu a:after {
    content: '';
    position: absolute;
    bottom: 0;
    left: 0;
    width: 0;
    height: 2px;
    background-color: #00AEEF;
    transition: width 0.3s ease;
  }
  
  .main-menu a:hover:after {
    width: 100%;
  }
  
  .overlay {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background-color: rgba(0, 0, 0, 0.5);
    z-index: 90;
  }

  .header-search {
  position: relative;
  margin: 0 24px;
  width: 280px;
  display: flex;
  align-items: center;
}

.header-search input {
  width: 100%;
  padding: 8px 36px 8px 14px;
  border-radius: 20px;
  border: 1px solid #00adef;
  outline: none;
  font-size: 16px;
  transition: border 0.2s;
  background: #fff;
}

.header-search input:focus {
  border-color: #0085c3;
}

.header-search .search-icon {
  position: absolute;
  right: 12px;
  top: 50%;
  transform: translateY(-50%);
  color: #00adef;
  font-size: 18px;
}

.search-results {
  position: absolute;
  top: 110%;
  left: 0;
  width: 100%;
  background: #fff;
  border-radius: 10px;
  box-shadow: 0 4px 16px rgba(0,0,0,0.08);
  z-index: 100;
  margin: 0;
  padding: 0;
  list-style: none;
  max-height: 220px;
  overflow-y: auto;
}

.search-results li {
  padding: 10px 16px;
  cursor: pointer;
  transition: background 0.2s;
}

.search-results li:hover {
  background: #e6f7ff;
}

  @media (max-width: 768px) {
    .logo {
      height: 50px;
    }
    
    .main-menu {
      width: 250px;
    }
  }
</style>



