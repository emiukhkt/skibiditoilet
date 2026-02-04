# skibiditoilet
nhaccudantoc
<!DOCTYPE html>
<html lang="vi">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Tinh Hoa Nhạc Cụ Việt</title>
    <script type="module" src="https://ajax.googleapis.com/ajax/libs/model-viewer/3.4.0/model-viewer.min.js"></script>
    
    <style>
        :root {
            --gold: #d4af37;
            --dark-red: #800000;
            --paper: #f9f4e8;
        }
        body { font-family: 'Segoe UI', sans-serif; margin: 0; background: var(--paper); }
        
        /* Menu điều hướng */
        nav { background: var(--dark-red); display: flex; justify-content: center; position: sticky; top: 0; z-index: 100; }
        nav button {
            background: none; border: none; color: white; padding: 15px 25px;
            cursor: pointer; font-size: 16px; font-weight: bold; transition: 0.3s;
        }
        nav button:hover, nav button.active-nav { background: var(--gold); color: black; }

        .tab-content { display: none; padding: 40px 20px; max-width: 1000px; margin: auto; animation: fadeIn 0.5s; }
        .active-tab { display: block; }

        @keyframes fadeIn { from { opacity: 0; } to { opacity: 1; } }

        /* Trang chủ: Các nút chọn đàn */
        .instrument-nav { display: flex; gap: 10px; justify-content: center; flex-wrap: wrap; margin-bottom: 30px; }
        .btn-dan {
            padding: 10px 20px; border: 2px solid var(--dark-red); background: white;
            border-radius: 25px; cursor: pointer; font-weight: bold;
        }
        .btn-dan:hover { background: var(--dark-red); color: white; }

        /* Khu vực hiển thị nội dung đàn */
        #display-box { 
            background: white; border-radius: 15px; padding: 30px; 
            box-shadow: 0 10px 30px rgba(0,0,0,0.1); display: none;
        }
        .grid-container { display: grid; grid-template-columns: 1fr 1fr; gap: 20px; }
        @media (max-width: 768px) { .grid-container { grid-template-columns: 1fr; } }

        img.dan-img { width: 100%; border-radius: 10px; border: 3px solid #eee; }
        model-viewer { width: 100%; height: 350px; background: #f0f0f0; border-radius: 10px; }

        h2 { color: var(--dark-red); border-bottom: 2px solid var(--gold); padding-bottom: 10px; }
    </style>
</head>
<body>

<nav>
    <button onclick="openTab('home', this)" class="active-nav">TRANG CHỦ</button>
    <button onclick="openTab('intro', this)">GIỚI THIỆU</button>
    <button onclick="openTab('game', this)">TRÒ CHƠI</button>
    <button onclick="openTab('collection', this)">SƯU TẦM</button>
</nav>

<div id="home" class="tab-content active-tab">
    <h1 style="text-align:center;">Khám Phá Nhạc Cụ 3D</h1>
    <div class="instrument-nav">
        <button class="btn-dan" onclick="viewDan('tranh')">Đàn Tranh</button>
        <button class="btn-dan" onclick="viewDan('nhi')">Đàn Nhị</button>
        <button class="btn-dan" onclick="viewDan('day')">Đàn Đáy</button>
        <button class="btn-dan" onclick="viewDan('tamthapluc')">Đàn Tam Thập Lục</button>
        <button class="btn-dan" onclick="viewDan('bau')">Đàn Bầu</button>
    </div>

    <div id="display-box">
        <h2 id="dan-title"></h2>
        <div class="grid-container">
            <div>
                <h3>Hình ảnh thực tế</h3>
                <img id="dan-img" class="dan-img" src="" alt="Hình ảnh đàn">
                <p id="dan-desc" style="text-align:justify; margin-top:15px;"></p>
            </div>
            <div>
                <h3>Mô hình 3D tương tác</h3>
                <model-viewer id="dan-3d" src="" auto-rotate camera-controls shadow-intensity="1" ar></model-viewer>
                <p style="font-size: 12px; color: #666;">* Dùng chuột để xoay, lăn chuột để phóng to mô hình 3D.</p>
            </div>
        </div>
    </div>
</div>

<div id="intro" class="tab-content">
    <h2>Hệ thống Nhạc cụ Dân tộc Việt Nam</h2>
    <p>Việt Nam có một kho tàng nhạc cụ phong phú với hàng trăm loại khác nhau, chia làm các bộ: Dây, Gõ, Hơi và Màng.</p>
</div>

<div id="game" class="tab-content">
    <h2>Thử tài đoán nhạc cụ</h2>
    <div style="border: 2px dashed #ccc; padding: 50px; text-align: center;">
        Tính năng Mini-game đang được phát triển...
    </div>
</div>

<div id="collection" class="tab-content">
    <h2>Bộ sưu tập của tôi</h2>
    <p>Những nhạc cụ bạn đã đánh dấu yêu thích sẽ xuất hiện ở đây.</p>
</div>

<script>
    // Dữ liệu nội dung
    const danData = {
        tranh: {
            title: "Đàn Tranh",
            img: "https://upload.wikimedia.org/wikipedia/commons/e/e0/Dan_tranh.jpg",
            model: "link-to-your-model/dan_tranh.glb", // Thay link file 3D tại đây
            desc: "Đàn Tranh thuộc họ dây, chi gảy. Âm sắc trong trẻo, sáng sủa, thường dùng độc tấu hoặc hòa tấu trong nhạc tài tử, chèo, v.v."
        },
        nhi: {
            title: "Đàn Nhị",
            img: "https://upload.wikimedia.org/wikipedia/commons/d/d3/Dan_nhi.jpg",
            model: "link-to-your-model/dan_nhi.glb",
            desc: "Đàn Nhị là nhạc cụ cung kéo, có âm thanh biểu cảm giống tiếng người, rất quan trọng trong hát chèo, chầu văn."
        },
        day: {
            title: "Đàn Đáy",
            img: "https://upload.wikimedia.org/wikipedia/commons/0/07/Dan_day.jpg",
            model: "link-to-your-model/dan_day.glb",
            desc: "Nhạc cụ đặc hữu của Việt Nam với thùng đàn hình thang, cần rất dài, là linh hồn của nghệ thuật Ca trù."
        },
        tamthapluc: {
            title: "Đàn Tam Thập Lục",
            img: "https://upload.wikimedia.org/wikipedia/commons/4/4e/Dan_Tam_Thap_Luc.jpg",
            model: "link-to-your-model/dan_tam_thap_luc.glb",
            desc: "Nhạc cụ gõ dây có 36 dây, âm thanh rộn ràng, sắc nét, giữ vai trò dẫn dắt trong dàn nhạc dân tộc."
        },
        bau: {
            title: "Đàn Bầu",
            img: "https://upload.wikimedia.org/wikipedia/commons/e/e5/Dan_bau_01.jpg",
            model: "link-to-your-model/dan_bau.glb",
            desc: "Nhạc cụ độc nhất vô nhị chỉ có một dây nhưng tạo ra âm thanh bồi âm huyền ảo, 'ngọt' như tiếng mẹ ru."
        }
    };

    // Hàm chuyển đổi Thẻ (Tab)
    function openTab(tabId, btn) {
        document.querySelectorAll('.tab-content').forEach(tab => tab.classList.remove('active-tab'));
        document.querySelectorAll('nav button').forEach(b => b.classList.remove('active-nav'));
        
        document.getElementById(tabId).classList.add('active-tab');
        btn.classList.add('active-nav');
    }

    // Hàm hiển thị thông tin Đàn
    function viewDan(id) {
        const item = danData[id];
        document.getElementById('display-box').style.display = 'block';
        document.getElementById('dan-title').innerText = item.title;
        document.getElementById('dan-img').src = item.img;
        document.getElementById('dan-desc').innerText = item.desc;
        document.getElementById('dan-3d').src = item.model;
    }
</script>

</body>
</html>
