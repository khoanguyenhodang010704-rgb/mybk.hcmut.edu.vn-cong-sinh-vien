# mybk.hcmut.edu.vn-cong-sinh-vien
<!DOCTYPE html>
<html lang="vi">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Hệ thống Quản lý Sinh viên và Điểm Linh hoạt</title>
    <style>
        body { font-family: Arial, sans-serif; background-color: #f4f6f9; margin: 0; padding: 20px; color: #333; }
        .container { max-width: 1000px; margin: 0 auto; background: white; padding: 25px; border-radius: 8px; box-shadow: 0 4px 15px rgba(0,0,0,0.1); }
        h2, h3 { color: #0056b3; border-bottom: 2px solid #eee; padding-bottom: 8px; }
        .grid { display: grid; grid-template-columns: 1fr 1fr; gap: 20px; }
        @media (max-width: 768px) { .grid { grid-template-columns: 1fr; } }
        .card { background: #fafafa; border: 1px solid #e0e0e0; padding: 15px; border-radius: 6px; margin-bottom: 15px; }
        label { font-weight: bold; display: block; margin-top: 10px; margin-bottom: 4px; font-size: 14px; }
        input, button, select { width: 100%; padding: 10px; margin-bottom: 10px; border: 1px solid #ccc; border-radius: 4px; box-sizing: border-box; }
        button { background-color: #007bff; color: white; border: none; font-weight: bold; cursor: pointer; transition: 0.2s; }
        button:hover { background-color: #0056b3; }
        .btn-success { background-color: #28a745; }
        .btn-success:hover { background-color: #218838; }
        .btn-danger { background-color: #dc3545; }
        .btn-danger:hover { background-color: #bd2130; }
        .btn-secondary { background-color: #6c757d; }
        .btn-secondary:hover { background-color: #5a6268; }
        table { width: 100%; border-collapse: collapse; margin-top: 15px; background: white; }
        th, td { border: 1px solid #ddd; padding: 10px; text-align: left; }
        th { background-color: #f2f2f2; color: #333; }
        .flex-group { display: flex; gap: 10px; }
        .flex-group input { margin-bottom: 0; }
        .flex-group button { width: auto; white-space: nowrap; margin-bottom: 0; }
        .score-inputs { display: grid; grid-template-columns: 1fr 1fr; gap: 10px; background: #edf2f7; padding: 10px; border-radius: 4px; margin-top: 5px; }
        .score-item { display: flex; flex-direction: column; }
        .An { display: none; }
    </style>
</head>
<body>

<div class="container">
    <h2 style="text-align: center;">HỆ THỐNG TRA CỨU & QUẢN LÝ ĐIỂM LINH HOẠT</h2>

    <!-- GIAO DIỆN CHÍNH: CHIA ĐÔI ADMIN VÀ ĐĂNG NHẬP -->
    <div class="grid">
        
        <!-- CỘT 1: DÀNH CHO SINH VIÊN ĐĂNG NHẬP -->
        <div>
            <div id="khung-dang-nhap" class="card">
                <h3>Sinh Viên Đăng Nhập</h3>
                <label for="login-mssv">Mã số sinh viên (MSSV)</label>
                <input type="text" id="login-mssv" placeholder="Ví dụ: SV01">
                <label for="login-pass">Mật khẩu</label>
                <input type="password" id="login-pass" placeholder="Nhập mật khẩu">
                <button onclick="sinhVienDangNhap()">Đăng Nhập Xem Điểm</button>
            </div>

            <div id="khung-ket-qua" class="card An">
                <h3 id="view-ten-sv">Xin chào!</h3>
                <div id="bang-diem-sinh-vien">
                    <!-- Điểm số của sinh viên đăng nhập hiển thị tại đây -->
                </div>
                <button class="btn-secondary" onclick="dangXuat()">Đăng Xuất</button>
            </div>
        </div>

        <!-- CỘT 2: CẤU HÌNH MÔN HỌC (QUẢN TRỊ) -->
        <div>
            <div class="card">
                <h3>1. Quản Lý Môn Học</h3>
                <label>Thêm môn học mới hệ thống cần quản lý:</label>
                <div class="flex-group">
                    <input type="text" id="ten-mon-moi" placeholder="Ví dụ: Triết Học, Lập Trình Web...">
                    <button class="btn-success" onclick="themMonHoc()">Thêm Môn</button>
                </div>
                <div style="margin-top: 10px;">
                    <small><b>Các môn hiện có:</b> <span id="ds-mon-hien-tai" style="color: #555;">Chưa có môn nào</span></small>
                </div>
            </div>
        </div>

    </div>

    <!-- KHUNG QUẢN LÝ SINH VIÊN (DƯỚI CÙNG) -->
    <div class="card" style="margin-top: 20px;">
        <h3>2. Quản Lý & Nhập Điểm Sinh Viên</h3>
        <div style="display: grid; grid-template-columns: 1fr 1fr 1fr; gap: 10px;">
            <div>
                <label for="sv-mssv">Mã Số Sinh Viên (MSSV)</label>
                <input type="text" id="sv-mssv" placeholder="Ví dụ: SV01">
            </div>
            <div>
                <label for="sv-ten">Họ và Tên</label>
                <input type="text" id="sv-ten" placeholder="Nguyễn Văn A">
            </div>
            <div>
                <label for="sv-pass">Mật khẩu đăng nhập</label>
                <input type="password" id="sv-pass" placeholder="Nhập mật khẩu">
            </div>
        </div>

        <label style="margin-top: 10px; color: #0056b3;">Nhập/Sửa Điểm Số Cho Các Môn Học:</label>
        <div id="vung-nhap-diem" class="score-inputs">
            <!-- Các ô nhập điểm tự động sinh ra dựa trên danh sách môn học -->
        </div>

        <button class="btn-success" onclick="luuSinhVien()" style="margin-top: 15px; font-size: 16px;">Lưu / Cập Nhật Sinh Viên</button>
    </div>

    <!-- DANH SÁCH TẤT CẢ SINH VIÊN -->
    <div class="card">
        <h3>Danh Sách Sinh Viên Toàn Trường</h3>
        <div style="overflow-x: auto;">
            <table>
                <thead>
                    <tr id="th-bang-sv">
                        <th>MSSV</th>
                        <th>Họ Tên</th>
                        <th>Mật Khẩu</th>
                        <!-- Các môn học tự động render thêm cột ở đây -->
                        <th>Hành Động</th>
                    </tr>
                </thead>
                <tbody id="tbody-bang-sv">
                    <!-- Dữ liệu sinh viên -->
                </tbody>
            </table>
        </div>
    </div>

</div>

<script>
    // Khởi tạo hoặc tải dữ liệu từ Trình duyệt (LocalStorage)
    let danhSachMon = JSON.parse(localStorage.getItem('dsMonHoc')) || ["Toán Cao Cấp", "Ngữ Văn"];
    let danhSachSV = JSON.parse(localStorage.getItem('dsSinhVien')) || {
        "SV01": { ten: "Nguyễn Văn A", pass: "123", diem: { "Toan Cao Cap": 8.5, "Ngu Van": 7.0 } }
    };

    // Hàm chuẩn hóa tên môn để làm mã thuộc tính không dấu/khoảng trắng
    function chuanHoaIdMon(str) {
        return str.normalize("NFD").replace(/[\u0300-\u036f]/g, "").replace(/[^a-zA-Z0-9]/g, "");
    }

    // 1. Đồng bộ và hiển thị vùng nhập điểm, bảng admin
    function taiGiaoDienAdmin() {
        // Lưu dữ liệu vào LocalStorage
        localStorage.setItem('dsMonHoc', JSON.stringify(danhSachMon));
        localStorage.setItem('dsSinhVien', JSON.stringify(danhSachSV));

        // Hiện danh sách chữ các môn hiện tại
        document.getElementById("ds-mon-hien-tai").innerText = danhSachMon.length > 0 ? danhSachMon.join(", ") : "Chưa có môn nào";

        // Tạo các ô nhập điểm động ở form Quản lý
        const vungNhapDiem = document.getElementById("vung-nhap-diem");
        vungNhapDiem.innerHTML = "";
        if (danhSachMon.length === 0) {
            vungNhapDiem.innerHTML = "<p style='grid-column: 1/-1; color:gray; text-align:center;'>Vui lòng thêm môn học trước.</p>";
        }
        danhSachMon.forEach(mon => {
            let idMon = chuanHoaIdMon(mon);
            vungNhapDiem.innerHTML += `
                <div class="score-item">
                    <label style="color:#444">\${mon}</label>
                    <input type="number" id="score-\${idMon}" placeholder="Điểm 0-10" min="0" max="10" step="0.1">
                </div>
            `;
        });

        // Tạo tiêu đề cột cho bảng danh sách
        const thBang = document.getElementById("th-bang-sv");
        thBang.innerHTML = `<th>MSSV</th><th>Họ Tên</th><th>Mật Khẩu</th>`;
        danhSachMon.forEach(mon => {
            thBang.innerHTML += `<th>\${mon}</th>`;
        });
        thBang.innerHTML += `<th>Hành Động</th>`;

        // Đổ dữ liệu sinh viên vào bảng
        const tbody = document.getElementById("tbody-bang-sv");
        tbody.innerHTML = "";
        for (let mssv in danhSachSV) {
            let sv = danhSachSV[mssv];
            let chuoiDiemTD = "";
            
            danhSachMon.forEach(mon => {
                let idMon = chuanHoaIdMon(mon);
                let diemSo = (sv.diem && sv.diem[idMon] !== undefined) ? sv.diem[idMon] : "-";
                chuoiDiemTD += `<td>\${diemSo}</td>`;
            });

            tbody.innerHTML += `
                <tr>
                    <td><b>\${mssv}</b></td>
                    <td>\${sv.ten}</td>
                    <td><code>\${sv.pass}</code></td>
                    \${chuoiDiemTD}
                    <td>
                        <button onclick="chuanBiSua('\${mssv}')" style="padding:4px 8px; width:auto; font-size:12px; margin-right:5px;">Sửa</button>
                        <button onclick="xoaSinhVien('\${mssv}')" class="btn-danger" style="padding:4px 8px; width:auto; font-size:12px;">Xóa</button>
                    </td>
                </tr>
            `;
        }
    }

    // 2. Thêm môn học mới
    function themMonHoc() {
        let tenMon = document.getElementById("ten-mon-moi").value.trim();
        if (!tenMon) {
            alert("Vui lòng điền tên môn học!");
            return;
        }
        if (danhSachMon.includes(tenMon)) {
            alert("Môn học này đã tồn tại!");
            return;
        }
        danhSachMon.push(tenMon);
        document.getElementById("ten-mon-moi").value = "";
        taiGiaoDienAdmin();
    }

    // 3. Thêm hoặc cập nhật Sinh viên kèm điểm số
    function luuSinhVien() {
        let mssv = document.getElementById("sv-mssv").value.trim().toUpperCase();
        let ten = document.getElementById("sv-ten").value.trim();
