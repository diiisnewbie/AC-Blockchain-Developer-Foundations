# Bài 3.2 – Hàm, Control Flow và Visibility (Báo cáo)

## 📄 Đề bài
Viết một smart contract tên `VotingEligibility`:
- Biến `minAge` kiểu uint, giá trị khởi tạo = 18.
- Hàm `checkEligibility(uint age)` trả về true/false:
  - Nếu `age >= minAge` → trả về true.
  - Ngược lại → trả về false.
- Hàm `updateMinAge(uint newMinAge)`:
  - Chỉ cho phép người deploy gọi được (sử dụng require với `msg.sender`).
  - Cập nhật lại `minAge`.

## 📝 Mã nguồn contract

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

/// @title VotingEligibility
/// @notice Kiem tra tuoi du dieu kien di bo phieu dua tren minAge.
/// @dev Chi nguoi deploy (deployer) moi duoc cap nhat minAge.
/// @author Blockchain Developer Foundations
contract VotingEligibility {
    /// @notice Tuoi toi thieu de du dieu kien bo phieu, mac dinh 18.
    uint public minAge = 18;

    /// @notice Dia chi nguoi deploy, immutable => khong lo doi doi duoc quyen.
    address public immutable deployer;

    /// @dev Gan deployer = msg.sender ngay khi deploy.
    constructor() {
        deployer = msg.sender;
    }

    /// @notice Kiem tra mot nguoi dc cho la du tuoi de bo phieu hay khong.
    /// @dev Func view (chi doc minAge), khong ton phi cap nhat state.
    /// @param age Tuoi can kiem tra
    /// @return true neu age >= minAge, nguoc lai false
    function checkEligibility(uint age) public view returns (bool) {
        if (age >= minAge) {
            return true;
        }
        return false;
    }

    /// @notice Cap nhat lai minAge, chi deployer goi duoc.
    /// @dev require kiem tra chu so huu + chan gia tri vo nghia.
    /// @param newMinAge Gia tri tuoi toi thieu moi (1..150)
    function updateMinAge(uint newMinAge) public {
        require(msg.sender == deployer, "VotingEligibility: only deployer");
        require(newMinAge > 0 && newMinAge <= 150, "VotingEligibility: invalid minAge");
        minAge = newMinAge;
    }
}
```

## ✅ Checklist minh chứng

### 1. Viết contract `VotingEligibility`
- [ ] Mở Remix IDE tại https://remix.ethereum.org
- [ ] Tạo file `VotingEligibility.sol`
- [ ] Dán mã nguồn contract (biến `minAge = 18`, `deployer` immutable, hàm `checkEligibility` và `updateMinAge`)

### 2. Compile contract
- [ ] Chọn compiler phiên bản `0.8.20` trở lên
- [ ] Compile thành công không có lỗi

### 3. Deploy contract
- [ ] Chọn environment (Remix VM hoặc Injected Provider)
- [ ] Nhấn Deploy và đợi giao dịch thành công
- [ ] Kiểm tra `minAge()` trả về `18`

> 📷 **Paste ảnh minh chứng Deploy trên Remix IDE vào đây:**

![Deploy contract trên Remix IDE](![alt text](image.png))

### 4. Kiểm tra hàm `checkEligibility(uint age)`
- [ ] Gọi `checkEligibility(21)` → trả về `true`
- [ ] Gọi `checkEligibility(18)` → trả về `true` (biên `age == minAge`)
- [ ] Gọi `checkEligibility(17)` → trả về `false`

### 5. Kiểm tra hàm `updateMinAge(uint newMinAge)`
- [ ] Từ tài khoản khác (không phải deployer) gọi `updateMinAge(16)` → revert "only deployer"
- [ ] Từ tài khoản deployer gọi `updateMinAge(16)` → thành công
- [ ] Kiểm tra lại `checkEligibility(17)` → trả về `true` (minAge đã = 16)
- [ ] Kiểm tra `minAge()` trả về `16`

## 📝 Ghi chú kết quả
- Contract: `VotingEligibility`
- Compiler:
- Environment:
- Deployer:
- Kết quả `minAge()` ban đầu:
- Kết quả `checkEligibility(21)` / `checkEligibility(18)` / `checkEligibility(17)`:
- Kết quả `updateMinAge(16)`:
- Kết quả `minAge()` sau khi cập nhật: