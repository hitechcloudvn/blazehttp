> [English](README.md) | **Tiếng Việt**

<div align="center">
<img src="https://github.com/hitechcloudvn/blazehttp/assets/30664688/746026da-6b2f-4f9c-86f1-1e3cb129ca22" width="120"/>
</div>
<h1 align="center">BlazeHTTP</h1>

BlazeHTTP là công cụ **đánh giá hiệu quả bảo vệ** của WAF thân thiện với người dùng.

- 📦 **Mẫu thử phong phú**: Hiện có tổng cộng **33669** mẫu, liên tục được cập nhật...
- 🚀 **Không cần cấu hình**: Có cả **giao diện đồ hoạ** và phiên bản dòng lệnh; có thể tải trực tiếp bản dựng sẵn qua Releases hoặc clone mã nguồn về biên dịch cục bộ.
- 📖 **Báo cáo có thể xuất**: Tạo báo cáo chi tiết về kết quả chạy toàn bộ mẫu, bao gồm thuộc tính mẫu, thời gian chạy, mã trạng thái, trạng thái chặn, v.v.

## Các chỉ số kiểm thử

|  Chỉ số   | Mô tả  | Cách tính  |
|  ----  | ----  | ----  |
| Tỷ lệ phát hiện  | Phản ánh mức độ đầy đủ của khả năng phát hiện của WAF; nếu không phát hiện được mẫu nào thì gọi là "bỏ sót". | Số mẫu tấn công bị chặn  |
| Tỷ lệ dương tính giả  | Phản ánh sự can thiệp vào lưu lượng bình thường; kết quả không đáng tin bị coi là "dương tính giả". | Số mẫu bình thường bị chặn  |
| Độ chính xác  | Chỉ số độ chính xác kết hợp tỷ lệ phát hiện và tỷ lệ dương tính giả, tránh tập trung quá mức vào bỏ sót hoặc dương tính giả. |  |
| Thời gian phát hiện  | Phản ánh hiệu năng của WAF; thời gian tiêu tốn càng lớn nghĩa là hiệu năng càng kém. |  |

## Ví dụ mẫu

```bash
# Mẫu bình thường: testcases/00/02/5ebf56a710da27b73a9ad59219f0.white
GET /rc-virtual-list@3.5.2/lib/hooks/useHeights.js HTTP/1.1
Host: npm.staticblitz.com
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/114.0.0.0 Safari/537.36
Accept: */*
Origin: https://stackblitz.com
Sec-Fetch-Site: cross-site
Sec-Fetch-Mode: cors
Sec-Fetch-Dest: empty
Referer: https://stackblitz.com/
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9,en-US;q=0.8,en;q=0.7

# Mẫu độc hại: testcases/8a/36/0bbc7685860c526e33f3cbd83f9c.black
GET /vulnerabilities/sqli_blind/?id=1%27+or+%27%27%3D%27&Submit=Submit HTTP/1.1
Host: 10.10.3.128
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/114.0.0.0 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Referer: http://10.10.3.128/vulnerabilities/sqli_blind/?id=1%27+and+%27%27%3D%27&Submit=Submit
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9,en-US;q=0.8,en;q=0.7
Connection: close
```

## Hiệu quả kiểm thử

### [CloudFlare](https://www.cloudflare.com/) vs [ModSecurity](https://github.com/owasp-modsecurity/ModSecurity) vs [HiTechCloud vCWAF](https://hitechwaf.vn)

| Chỉ số | CloudFlare, bản miễn phí | ModSecurity, PARANOIA Level 1 | ModSecurity,  PARANOIA Level 4 | HiTechCloud vCWAF, bản miễn phí, chế độ Balance | HiTechCloud vCWAF, bản miễn phí, chế độ Strict |
| --- | --- | --- | --- | --- | --- |
| Tổng số mẫu | 33669 | 33669 | 33669 | 33669 | 33669 |
| Thành công | 33350 | 33669 | 33669 | 33669 | 33669 |
| Lỗi | 319 | 0 | 0 | 0 | 0 |
| **Tỷ lệ phát hiện (càng cao càng tốt)** | 10.70% (Tổng mẫu độc hại: 570, Chặn đúng: 61, Bỏ sót: 509) | 69.74% (Tổng mẫu độc hại: 575, Chặn đúng: 401, Bỏ sót: 174) | 🏆 **94.61%** (Tổng mẫu độc hại: 575, Chặn đúng: 544, Bỏ sót: 31) | 71.65% (Tổng mẫu độc hại: 575, Chặn đúng: 412, Bỏ sót: 163) | 76.17% (Tổng mẫu độc hại: 575, Chặn đúng: 438, Bỏ sót: 137) |
| **Tỷ lệ dương tính giả (càng thấp càng tốt)** | 0.07% (Tổng mẫu bình thường: 32780, Qua đúng: 32757, Dương tính giả: 23) | 17.58% (Tổng mẫu bình thường: 33094, Qua đúng: 27275, Dương tính giả: 5819) | 52.46% (Tổng mẫu bình thường: 33094, Qua đúng: 15732, Dương tính giả: 17362) | 🏆 **0.07%** (Tổng mẫu bình thường: 33094, Qua đúng: 33071, Dương tính giả: 23) | 0.22% (Tổng mẫu bình thường: 33094, Qua đúng: 33021, Dương tính giả: 73) |
| **Độ chính xác (càng cao càng tốt)** | 98.40% (Chặn đúng + Qua đúng) / Tổng số mẫu | 82.20% (Chặn đúng + Qua đúng) / Tổng số mẫu | 48.34% (Chặn đúng + Qua đúng) / Tổng số mẫu | 🏆 **99.45%** (Chặn đúng + Qua đúng) / Tổng số mẫu | 99.38% (Chặn đúng + Qua đúng) / Tổng số mẫu |
| Thời gian trung bình | 288.96 mili giây | 31.15 mili giây | 28.89 mili giây | 70.05 mili giây | 64.34 mili giây |

## Cài đặt và sử dụng

** Docker Container**

```bash
# kéo image mới nhất từ DockerHub
docker pull hitechcloudvn/blazehttp:latest
# chạy kiểm thử
docker run --rm --net=host hitechcloudvn/blazehttp:latest /app/blazehttp -t <URL>
```

Các bản dựng biên dịch sẵn từ GitHub CI đã được đăng lên Releases để tải trực tiếp phiên bản mới nhất [tại đây](https://github.com/hitechcloudvn/blazehttp/releases).

**Dòng lệnh**

![blazehttp_cmd](https://github.com/hitechcloudvn/blazehttp/assets/30664688/7be052e9-2dfb-4f96-a6f2-eb2a0251910e)

**GUI** (macOS & Windows)

> Nếu gặp lỗi như **untrusted** hoặc **moved to trash** trên macOS, chạy lệnh sau trước khi mở lại:
> ``` bash
> sudo xattr -d com.apple.quarantine blazehttp_1.0.0_darwin_arm64.app
> ```

![gui](https://github.com/hitechcloudvn/blazehttp/assets/30664688/dee16f13-8fef-413e-89c8-515b91c52c7a)

## Biên dịch cục bộ

Dự án chỉ phụ thuộc vào ngôn ngữ lập trình Go; vì vậy môi trường của bạn cần có Go, tải tại [đây](https://go.dev/dl/).

### Phiên bản dòng lệnh

```bash
# Clone mã nguồn
git clone https://github.com/hitechcloudvn/blazehttp.git && cd blazehttp
# Biên dịch cục bộ
bash build.sh # Sau khi chạy, tìm 'blazehttp' trong thư mục 'build'
# Chạy
./blazehttp -t https://example.org
```

### Phiên bản GUI

GUI được xây dựng bằng [fyne](https://github.com/fyne-io/fyne).

```bash
# Clone mã nguồn
git clone https://github.com/hitechcloudvn/blazehttp.git && cd blazehttp
# Chạy cục bộ
go run gui/main.go
```

![gui](https://github.com/hitechcloudvn/blazehttp/assets/30664688/3d7f90aa-eb6d-43b0-adea-251114c6ea43)

> Nếu cần đóng gói cục bộ, xem [tài liệu đóng gói](https://docs.fyne.io/started/packaging) của fyne
> Để đóng gói đa nền tảng, xem [fyne-cross](https://docs.fyne.io/started/cross-compiling)

## Đóng góp

Chúng tôi hoan nghênh mọi đóng góp, dù là thêm mẫu mới, tính năng, sửa lỗi, tối ưu hiệu năng hay bất kỳ điều gì khác. Trân trọng và cảm ơn mọi nỗ lực của bạn 👏

## Star

Nếu bạn thấy hữu ích, đừng ngần ngại tặng một Star ✨
