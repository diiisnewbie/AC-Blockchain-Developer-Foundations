# Bài 3.1 – Kiểu dữ liệu và biến Solidity (Báo cáo)

## 📄 Đề bài
Viết một smart contract tên `Profile`:
- Biến `name` (kiểu `string`) khai báo `public`
- Biến `age` (kiểu `uint`) khai báo `public`
- Hàm `setProfile(string _name, uint _age)` cập nhật name và age

## 📝 Mã nguồn contract

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

/// @title Profile
/// @notice Luu tru ten va tuoi cua mot nguoi dung tren blockchain.
/// @author Blockchain Developer Foundations
contract Profile {
    /// @notice Ten cua profile. Getter public tu dong sinh boi compiler.
    string public name;

    /// @notice Tuoi cua profile. Getter public tu dong sinh boi compiler.
    uint public age;

    /// @notice Cap nhat ten va tuoi cua profile (public, bat ky ai cung goi duoc).
    /// @dev Goi toan bo state -> storage. Doi so _name dung bo nho memory de tiet kiem gas.
    /// @param _name Ten moi, khong duoc rong
    /// @param _age Tuoi moi, phai lon hon 0
    function setProfile(string memory _name, uint _age) public {
        require(bytes(_name).length > 0, "Profile: name cannot be empty");
        require(_age > 0, "Profile: age must be greater than zero");
        name = _name;
        age = _age;
    }
}
```

## ✅ Checklist minh chứng

### 1. Viết contract `Profile`
- [x] Mở Remix IDE tại https://remix.ethereum.org
- [x] Tạo file `Profile.sol`
- [x] Dán mã nguồn contract `Profile` (biến `name`, `age` public và hàm `setProfile`)

### 2. Compile contract
- [x] Chọn compiler phiên bản `0.8.20` trở lên
- [x] Compile thành công không có lỗi

### 3. Deploy contract
- [x] Chọn environment (Remix VM hoặc Injected Provider)
- [x] Nhấn Deploy và đợi giao dịch thành công

> 📷 **Paste ảnh minh chứng Deploy trên Remix IDE vào đây:**

![Deploy contract trên Remix IDE](![alt text](image.png))

### 4. Gọi hàm `setProfile("Alice", 21)`
- [x] Tại phần Deployed Contracts, nhập `_name = "Alice"`, `_age = 21`
- [x] Nhấn `setProfile` và xác nhận transaction thành công

### 5. Kiểm tra kết quả
- [x] Gọi hàm `name()` → giá trị trả về là `Alice`
- [x] Gọi hàm `age()` → giá trị trả về là `21`

## 📝 Ghi chú kết quả
- Contract: `Profile`
- Compiler:
- Environment:
- Kết quả `setProfile("Alice", 21)`:
- Kết quả `name()`:
- Kết quả `age()`: