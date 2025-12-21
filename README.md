# 🟡 Unstoppable Force Bot Trade XAU MT4

**Unstoppable Force Bot Trade XAU MT4** là một Expert Advisor (EA) dành cho **MetaTrader 4**, được thiết kế **chuyên biệt cho giao dịch vàng (XAUUSD)** trên **khung thời gian M1 và M5**.

Bot kết hợp **SuperTrend (custom indicator)** để xác định đảo chiều xu hướng và chiến lược **DCA (Dollar Cost Averaging)** với **lot tăng dần**, nhằm tối ưu lợi nhuận trong các pha pullback hoặc sideway ngắn hạn.

---

## 🚀 Tính năng chính

- ✅ Giao dịch **XAUUSD**
- ✅ Tối ưu cho **M1 & M5**
- ✅ Tự động vào lệnh theo **SuperTrend đảo chiều**
- ✅ Chiến lược **DCA theo khoảng giá cố định**
- ✅ Lot tăng dần theo cấp số nhân
- ✅ Chốt toàn bộ lệnh khi đạt **Account Profit target**
- ❌ Không sử dụng Stop Loss (High Risk Strategy)

---

## 🧠 Chiến lược giao dịch

### 1. Xác định xu hướng
Bot sử dụng indicator custom:

```
Supertrend-MA_1a
```

Khi SuperTrend đổi trạng thái:
- DOWN → UP → vào **BUY**
- UP → DOWN → vào **SELL**

---

### 2. Vào lệnh DCA
- Lệnh đầu tiên được mở ngay khi có tín hiệu
- Các lệnh tiếp theo:
  - BUY: mở khi giá giảm thêm `dcaStep`
  - SELL: mở khi giá tăng thêm `dcaStep`

Công thức tăng lot:

```
lot[n] = lotSize * (lotRate ^ n)
```

---

### 3. Thoát lệnh
- Khi **AccountProfit ≥ Profit**
- Bot đóng **toàn bộ lệnh của symbol hiện tại**

---

## ⚙️ Tham số cấu hình

### 🔹 SuperTrend
| Tham số | Mô tả |
|------|------|
| `period` | Chu kỳ SuperTrend |
| `SuperTrend_Factor` | Hệ số nhân |
| `Training_Data_Len` | Độ dài dữ liệu huấn luyện |
| `Inphigh` | Ngưỡng xác suất cao |
| `Inpmedium` | Ngưỡng xác suất trung bình |
| `Inplow` | Ngưỡng xác suất thấp |

---

### 🔹 DCA & Quản lý vốn
| Tham số | Mô tả |
|------|------|
| `lotSize` | Lot khởi đầu |
| `lotRate` | Hệ số tăng lot |
| `maxOrdersPerDirect` | Số lệnh tối đa mỗi chiều |
| `dcaStep` | Khoảng cách DCA (point) |
| `initialDirection` | Hướng khởi tạo (0 = BUY, 1 = SELL) |

---

### 🔹 Thoát lệnh
| Tham số | Mô tả |
|------|------|
| `Profit` | Target lợi nhuận theo AccountProfit |
| `slippage` | Trượt giá cho phép |

---

## 📝 Cấu trúc Order Comment

Mỗi lệnh được gắn comment theo format:

```
SYMBOL|TYPE|INDEX|PRICE
```

Ví dụ:
```
XAUUSD|0|2|2365.40
```

Giúp bot:
- Đếm số lệnh theo chiều
- Tính giá vào trung bình
- Quản lý DCA chính xác

---

## 📐 Logic hoạt động (High-level)

```
OnTick
 ├─ Kiểm tra nến mới
 ├─ Nếu AccountProfit ≥ Profit → đóng toàn bộ lệnh
 ├─ Kiểm tra SuperTrend đảo chiều
 └─ Thực hiện DCA theo xu hướng mới
```

---

## ⚠️ Cảnh báo rủi ro

> ⚠️ **CHIẾN LƯỢC RỦI RO CAO**

- Không có Stop Loss
- Sử dụng DCA + tăng lot
- Có thể cháy tài khoản nếu thị trường đi một chiều mạnh

👉 **Bắt buộc backtest và forward test trước khi dùng tiền thật**

---

## 🧪 Khuyến nghị sử dụng

- Tài khoản **thử nghiệm hoặc vốn nhỏ**
- Spread thấp
- VPS ổn định
- Không chạy cùng nhiều EA khác trên XAU

---

## 📄 Giấy phép

Tác giả chịu **không trách nhiệm** cho mọi rủi ro tài chính phát sinh.

---

## ⭐ Disclaimer

> Giao dịch tài chính có rủi ro cao.  
> EA này **không đảm bảo lợi nhuận** và **không phù hợp cho người mới**.
