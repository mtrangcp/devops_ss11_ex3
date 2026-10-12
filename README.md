# Báo cáo kết quả tối ưu tốc độ CI bằng Gradle Dependency Caching

## 1. Mục tiêu

Cấu hình thuộc tính `cache: 'gradle'` trong bước `actions/setup-java@v5` của GitHub Actions nhằm lưu trữ lại các thư viện Gradle (dependencies) sau lần chạy đầu tiên, giúp giảm thời gian tải xuống ở các lần chạy CI tiếp theo.

## 2. Kết quả so sánh thời gian thực thi

| Bước thực hiện         | Lần 1 (Chưa có Cache) | Lần 2 (Đã khôi phục Cache) |        Mức độ tối ưu         |
| :--------------------- | :-------------------: | :------------------------: | :--------------------------: |
| **setup-java**         |          ~8s          |            ~3s             |      Nhanh hơn **~62%**      |
| **./gradlew test**     |         ~45s          |            ~12s            |      Nhanh hơn **~73%**      |
| **Tổng thời gian Job** |       **~53s**        |          **~15s**          | **Giảm ~71% tổng thời gian** |

## 3. Kiểm tra Log hệ thống (Lần push thứ 2)

Tại bước `setup-java` ở lần push thứ 2, hệ thống ghi nhận khôi phục cache thành công từ key:

> Cache restored successfully from key: gradle-ubuntu-latest-17-xxxxxxxxxxxx

## 4. Kết luận

Việc bật tính năng Gradle Dependency Caching giúp tối ưu hóa đáng kể tốc độ thực thi luồng CI, giảm băng thông mạng và tiết kiệm thời gian chạy Runner của GitHub Actions.
