<footer class="footer">
  <div class="footer-container">
    <div class="footer-info">
      <p>Công ty TNHH TMAI Sài Gòn - Website: tmaisaigon.vn</p>
      <p>Văn phòng: HM Town, 412 Nguyễn Thị Minh Khai, P. 5, Quận 3, TPHCM</p>
      <p>Điện thoại: 08.65.327.003</p>
      <p>Email: ngaymoisaigon@gmail.com; tmaisaigon@ngaymoisaigon.com</p>
      <p>Website: ngaymoisaigon.com - ngaymoisaigon.vn</p>
      <div class="footer-logo">
        <img src="images/logo_tmaisaigon.jpg" alt="TMAI Logo" />
      </div>
      <p class="copyright">Bản quyền thuộc về công ty TNHH TMAI Sài Gòn©2016</p>
    </div>
    <div class="footer-logos">
      <a href="http://ngaymoisaigon.com/" target="_blank" class="logo-link">
        <img src="images/logotmai_X_56.png" alt="Ngày Mới Sài Gòn Logo" class="ngaymoi-logo" />
      </a>
      <div class="lonicera-logo">
        <img src="images/lonicerasaigon.png" alt="Lonicera Logo" />
      </div>
    </div>
  </div>
</footer>

<style>
  .footer {
    background-color: #005586;
    color: white;
    padding: 40px 0;
    width: 100%;
  }

  .footer-container {
    display: flex;
    justify-content: space-between;
    max-width: 1200px;
    margin: 0 auto;
    padding: 0 20px;
  }

  .footer-info {
    flex: 2;
  }

  .footer-info p {
    margin: 10px 0;
    font-size: 16px;
    line-height: 1.5;
  }

  .footer-logos {
    display: flex;
    flex-direction: column;
    justify-content: space-around;
    flex: 1;
  }

  .logo-link {
    display: block;
    margin-bottom: 20px;
  }

  .ngaymoi-logo {
    max-width: 250px;
    height: auto;
  }

  .lonicera-logo img {
    max-width: 300px;
    height: auto;
  }

  .footer-logo {
    margin-top: 20px;
  }

  .footer-logo img {
    max-width: 180px;
    height: auto;
  }

  .copyright {
    margin-top: 20px;
    font-size: 14px;
  }

  @media (max-width: 768px) {
    .footer-container {
      flex-direction: column;
    }

    .footer-info {
      margin-bottom: 30px;
    }

    .footer-logos {
      align-items: flex-start;
    }
  }
</style>