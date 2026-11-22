# YTRear

[English](README.md) · **Tiếng Việt**

[![Bản phát hành mới nhất](https://img.shields.io/github/v/release/Tnina2612/YTRear-on-Xiaomi-17-Pro-Series?style=flat-square&label=release)](https://github.com/Tnina2612/YTRear-on-Xiaomi-17-Pro-Series/releases)
[![CI](https://github.com/Tnina2612/YTRear-on-Xiaomi-17-Pro-Series/actions/workflows/ci.yml/badge.svg?branch=main)](https://github.com/Tnina2612/YTRear-on-Xiaomi-17-Pro-Series/actions/workflows/ci.yml)
[![Quy trình phát hành](https://github.com/Tnina2612/YTRear-on-Xiaomi-17-Pro-Series/actions/workflows/release.yml/badge.svg?branch=main)](https://github.com/Tnina2612/YTRear-on-Xiaomi-17-Pro-Series/actions/workflows/release.yml)
[![Giấy phép](https://img.shields.io/github/license/Tnina2612/YTRear-on-Xiaomi-17-Pro-Series?style=flat-square)](LICENSE)
[![Lượt tải](https://img.shields.io/github/downloads/Tnina2612/YTRear-on-Xiaomi-17-Pro-Series/total?style=flat-square)](https://github.com/Tnina2612/YTRear-on-Xiaomi-17-Pro-Series/releases)
[![Nền tảng](https://img.shields.io/badge/platform-Android%2016%20%2F%20HyperOS-3ddc84?style=flat-square&logo=android&logoColor=white)](#cài-đặt)

> **Bản fork được duy trì.** Kho lưu trữ này là bản fork của
> [megadonkatsu/YTRear](https://github.com/megadonkatsu/YTRear), có thêm bản sửa lỗi và tính năng
> mới. Repo gốc đã ngừng hoạt động: chủ repo không còn phản hồi issue hay pull request. Vui lòng báo
> lỗi và gửi pull request tại [bản fork này](https://github.com/Tnina2612/YTRear-on-Xiaomi-17-Pro-Series)
> thay vì repo gốc.

Bản fork giữ nguyên cách tiếp cận chuyển tiếp màn hình sau của bản gốc và bổ sung một số cải tiến
thực tế:

- **Tự động theo dõi trình phát** kèm danh sách loại trừ theo ứng dụng, để thẻ màn sau chuyển giữa
  các trình phát mà không cần mở lại YTRear.
- **Quy trình thiết lập đầy đủ hơn**: hướng dẫn tối ưu pin, ô bật/tắt nhanh trong Quick Settings và
  một checklist chung cho quyền thông báo, pin và tự khởi động HyperOS.
- **Kiểm chứng firmware** cho cả HyperOS `OS3.0.318.0.WBLCNXM` và `OS4.0.6.0.XBLCNXM`, kèm cảnh
  báo thay vì tự giả định một firmware chưa kiểm chứng có hành vi giống hệt.
- **Bản địa hóa tiếng Việt** với bộ chọn ngôn ngữ trong ứng dụng; tiếng Anh vẫn là ngôn ngữ gốc.
- **Quyền truy cập gọn hơn**: loại trừ toàn bộ các trình phát đã được HyperOS hỗ trợ sẵn, đồng thời
  bỏ quyền overlay và các probe không còn cần thiết.

Điều khiển trình phát nhạc Android đã chọn từ màn hình sau "Magic Back Screen" của Xiaomi 17 Pro
trong khi màn hình chính đã tắt. Chạy trên máy đã khóa bootloader và không root — không cần Shizuku,
không cần cài đặt đặc biệt.

Bản phát hành công khai mới nhất: **1.5.1** (`versionCode 19`) — tự phát hiện trình phát đang hoạt
động gần nhất hoặc chọn một ứng dụng cụ thể, kèm checklist thiết lập, kiểm chứng firmware và bản địa
hóa tiếng Việt. Xem [changelog](CHANGELOG.md) để biết thay đổi và
[releases](https://github.com/Tnina2612/YTRear-on-Xiaomi-17-Pro-Series/releases) để tải APK đã ký.
Bản 1.2 vẫn là mốc ổn định đã gắn tag.

## Có gì mới trong 1.5.1

- **Một thẻ Thiết lập duy nhất** thay cho các nút quyền thông báo và pin riêng lẻ. Thẻ hiển thị
  quyền thông báo, miễn trừ tối ưu pin và tự khởi động HyperOS cùng lúc, rồi tự ẩn khi cả ba đã xong.
- **Xác nhận tự khởi động.** HyperOS không cung cấp trạng thái tự khởi động cho ứng dụng, nên YTRear
  mở màn hình hệ thống và ghi nhận xác nhận của bạn bằng checkbox. Thẻ cũng nhắc giữ YTRear trong
  Recents, vì vuốt bỏ ứng dụng sẽ bị coi là buộc dừng.
- **Kiểm chứng firmware.** Các bản HyperOS đã kiểm chứng gồm cả `OS3.0.318.0.WBLCNXM` và
  `OS4.0.6.0.XBLCNXM`. Firmware chưa kiểm chứng sẽ hiện cảnh báo nhỏ trong **Nâng cao** và báo trạng
  thái trong phần chẩn đoán.
- **Giao diện tiếng Việt và bộ chọn ngôn ngữ.** Nút quả địa cầu ở góc trên bên phải chuyển giữa
  **Theo hệ thống**, **English** và **Tiếng Việt**. Lựa chọn được lưu theo từng ứng dụng, giữ nguyên
  sau khi khởi động lại và cũng bản địa hóa thông báo dịch vụ nền cùng thông báo media.

## Có gì mới trong 1.5.0

- **Thiết lập pin nằm trong quy trình bắt đầu.** Màn hình chính giữ nút **Đặt pin thành Không hạn
  chế** cho đến khi YTRear được miễn trừ tối ưu pin, để Greezer của HyperOS không đóng băng tiến
  trình vài giây sau khi bạn rời ứng dụng hoặc tắt màn hình. Bảng chẩn đoán báo trạng thái hiện tại.
  Thẻ Thiết lập của 1.5.1 thay thế nút độc lập này.
- **Ô Quick Settings.** Thêm YTRear vào bảng Quick Settings để bật/tắt chuyển tiếp màn sau chỉ với
  một chạm, không cần mở ứng dụng. Tắt sẽ xóa proxy và trả lại thông báo media gốc của trình phát;
  bật lại sẽ khôi phục cả hai. Ô chỉ hoạt động khi đã cấp quyền thông báo và đã chọn trình phát; nếu
  chưa thiết lập xong, chạm vào sẽ mở YTRear.
- **Icon trong bộ chọn trình phát.** Bộ chọn hiển thị icon launcher của từng ứng dụng, ghim dòng tự
  phát hiện lên đầu và tải icon ngoài luồng chính để cuộn mượt.

## Có gì mới trong 1.4.1

- **Loại trừ toàn bộ danh sách trình phát gốc của HyperOS.** Mọi ứng dụng nhạc mà HyperOS đã hỗ trợ
  sẵn trên màn hình sau (`Spotify`, `Xiaomi Music`, `QQ Music`, `NetEase Cloud Music`, `Kugou` và
  `Kuwo`) đều bị bỏ qua trong cả bộ chọn thủ công lẫn tự phát hiện, để widget gốc của firmware xử lý
  trực tiếp.
- **Không cần quyền overlay.** Đã bỏ `SYSTEM_ALERT_WINDOW` và các probe overlay/custom-widget cũ.
  YTRear giờ chỉ yêu cầu quyền thông báo và foreground service.
- **CI tự động.** Thêm GitHub Actions CI để chạy `:app:assembleDebug` và `:app:lintDebug` trên mỗi
  lần push và pull request.

## Có gì mới trong 1.4.0

- **Tự phát hiện trình phát đang hoạt động.** Chọn **Tự phát hiện trình phát đang hoạt động** ở đầu
  bộ chọn để YTRear đi theo ứng dụng nhạc phù hợp vừa bắt đầu phát, không cần mở lại YTRear để đổi
  mục tiêu. Vẫn có thể chọn thủ công một trình phát bất kỳ lúc nào.
- **Chuyển thẻ màn sau ổn định.** Khi một trình phát mới nhận audio focus, YTRear mồi cửa sổ giữ
  widget màn sau `< 200 ms` của HyperOS, chuyển phiên proxy tại chỗ, tạm ẩn thông báo `MediaStyle`
  của trình phát mới và trả thông báo của trình phát cũ về khay.
- **Loại trừ theo ứng dụng.** Ở chế độ tự động, **Ứng dụng loại trừ** trên màn hình chính mở một
  danh sách tìm kiếm các ứng dụng có launcher mà tự phát hiện nên bỏ qua, để ứng dụng video hoặc
  trình duyệt giữ thẻ media riêng.
- **Đã kiểm chứng trên thiết bị với nhiều lần chuyển trình phát trực tiếp** (`YT Music Morphe` ↔
  `SoundCloud`), không có lần nào widget màn sau bị gỡ, thông báo được khôi phục ngay và mọi nút
  điều khiển đều được chuyển tiếp đầy đủ.

## Có gì mới trong 1.3.2

- **Chuyển trình phát giờ tự dọn dẹp.** Khi chọn trình phát khác, YTRear trả lại thông báo media
  đang bị tạm ẩn của trình phát cũ thay vì để nó bị ẩn hết 30 ngày. Notification listener thông
  thường không có cách bỏ tạm ẩn trực tiếp, nên YTRear rút ngắn thời gian tạm ẩn hiện có xuống 250 ms
  và để Android đăng lại thông báo bình thường — sau khi mục tiêu mới đã tiếp quản.
- **Dọn dẹp vẫn hoạt động sau khi khởi động lại.** Các lần khôi phục đang chờ được lưu lại, nên việc
  chuyển trình phát vẫn xử lý đúng kể cả khi notification listener bị ngắt hoặc tiến trình bị khởi
  động lại.
- **Đã kiểm chứng trên thiết bị theo cả hai chiều.** Chuyển khỏi YouTube Music đang phát đã xóa nó
  khỏi cả hai danh sách tạm ẩn của Android và khôi phục thông báo gốc ngay; chuyển lại chỉ tạm ẩn
  YouTube Music. Nếu trình phát cũ không chạy, thông báo của nó sẽ trở lại ở lần đăng tiếp theo.

## Có gì mới trong 1.3.1

- **Chọn bất kỳ trình phát nào.** Bộ chọn có tìm kiếm mở cùng màn hình chính và liệt kê mọi ứng dụng
  đã cài có launcher. Chọn ứng dụng YTRear sẽ chuyển tiếp; lựa chọn được giữ qua khởi động lại và
  khởi động lại máy, và nút **Trình phát** trên màn hình chính cho phép đổi bất cứ lúc nào.
- **Bản sửa Dynamic Island đi theo lựa chọn của bạn.** Cách xử lý thông báo đã kiểm chứng cho YouTube
  Music ở 1.2 áp dụng cho bất kỳ trình phát nào bạn chọn: YTRear tạm ẩn thông báo `MediaStyle` của
  ứng dụng đó và đăng proxy thay thế, để thẻ gốc không giành lại thứ hạng media cao nhất của HyperOS
  và làm thu gọn Dynamic Island khi chuyển bài.
- **Áp dụng ngay khi cần** — khi đổi trình phát, khi notification listener kết nối và mỗi khi trình
  phát đã chọn đăng thông báo media mới.
- **Đã kiểm chứng trên thiết bị với Poweramp** cùng toàn bộ bài kiểm tra hồi quy YouTube Music.
  Spotify không có trong bộ chọn vì firmware này đã điều khiển nó trực tiếp.

## Cách hoạt động

HyperOS giới hạn widget nhạc màn sau gốc bằng một danh sách package chính xác. Ở cổng đó, hệ thống
không kiểm tra chứng chỉ, trình cài đặt, nguồn gốc UID hay trạng thái đặc quyền. YTRear được build
dưới một package nằm trong danh sách cho phép, chuyển tiếp `MediaSession` của ứng dụng đã chọn qua
`MediaController` được cấp quyền bởi notification listener, rồi đăng lại lên widget màn sau gốc. Các
callback điều khiển từ màn hình sau được chuyển ngược về ứng dụng đó.

```text
MediaSession của trình phát đã chọn
        |  MediaController (notification listener)
        v
    MediaHub.kt
        |  metadata, ảnh bìa, trạng thái phát, vị trí
        v
 NativeMediaProxy.kt
        |
        v
 Widget màn sau HyperOS unified.music:music_media
        |  callback MediaSession gốc
        +---> nút điều khiển của trình phát đã chọn
```

## Cài đặt

Tải APK từ [bản phát hành mới nhất](https://github.com/Tnina2612/YTRear-on-Xiaomi-17-Pro-Series/releases)
và sideload — copy sang điện thoại rồi chạm để cài, hoặc
`adb install -r YTRear-1.5.1-debug.apk`. HyperOS sẽ hỏi bạn có cho phép cài đặt từ ứng dụng đã mở
file hay không. Mỗi bản phát hành có kèm file `.sha256`; hãy đối chiếu trước khi cài.

Sau đó thiết lập các mục sau, tất cả trên YTRear:

| Cài đặt | Vị trí | Lý do |
|---|---|---|
| **Quyền truy cập thông báo** | Cài đặt → Ứng dụng → Quyền truy cập ứng dụng đặc biệt → Quyền truy cập thông báo | Bắt buộc. Đây là cách YTRear đọc phiên media của trình phát đã chọn. Không có quyền này thì mọi thứ đều không hoạt động. |
| **Thông báo** | Lời nhắc lần đầu mở ứng dụng | Thẻ màn sau của YTRear *là* một thông báo. Từ chối quyền này sẽ làm hỏng widget. |
| **Tự khởi động** | Thẻ Thiết lập → **Mở**, sau đó tick **Đã bật tự khởi động** | Giúp listener kết nối lại sau khi khởi động lại máy hoặc khởi động lại trình phát đã chọn. |
| **Tiết kiệm pin: Không hạn chế** | Thẻ Thiết lập → **Đặt** (hoặc thông tin ứng dụng HyperOS → Tiết kiệm pin) | Ngăn HyperOS đóng băng proxy khi màn hình tắt. Dòng này chuyển xanh khi đã được miễn trừ. |

Mở YTRear và chọn cách chọn trình phát. Chọn **Tự phát hiện trình phát đang hoạt động** ở đầu danh
sách để đi theo bất kỳ ứng dụng nhạc nào bắt đầu phát, hoặc chọn một ứng dụng cụ thể để chuyển tiếp.
Cấp quyền được yêu cầu, sau đó mở trình phát và bắt đầu phát. Thẻ **Thiết lập** tự ẩn khi quyền thông
báo, miễn trừ pin và tự khởi động đều đã được xác nhận.

YTRear theo ngôn ngữ hệ thống mặc định. Dùng nút quả địa cầu ở góc trên bên phải màn hình chính để
chuyển giữa **Theo hệ thống**, **English** và **Tiếng Việt** bất cứ lúc nào.

### Sử dụng hằng ngày

Ở chế độ **Tự phát hiện**, YTRear ghi nhớ chế độ và trình phát hoạt động gần nhất qua khởi động lại
ứng dụng và khởi động lại máy; bắt đầu phát ở một trình phát phù hợp khác sẽ tự chuyển thẻ màn sau, và
**Ứng dụng loại trừ** cho phép bỏ qua những ứng dụng cụ thể. Ở chế độ **Thủ công**, YTRear hỏi mục
tiêu mỗi khi mở màn hình chính và ghi nhớ lựa chọn hiện tại. Dùng **Trình phát** trên màn hình chính
để đổi chế độ hoặc mục tiêu bất cứ lúc nào. Để bật/tắt nhanh hơn, thêm **YTRear** vào bảng Quick
Settings: một chạm tắt proxy và trả lại thông báo media gốc của trình phát, chạm lần nữa để bật lại.

Đừng vuốt YTRear khỏi Recents. HyperOS coi đó là buộc dừng và sẽ từ chối kết nối lại notification
listener cho đến khi bạn mở lại ứng dụng.

## Tương thích trình phát

Ứng dụng được chọn phải công bố `MediaSession` chuẩn của Android. Play/pause, next, previous,
metadata và ảnh bìa phụ thuộc vào những gì phiên media đó cung cấp. Ứng dụng không có media session
vẫn có thể được chọn, nhưng YTRear sẽ đứng ở trạng thái **Đang chờ nhạc**.

Các ứng dụng trong danh sách nhạc màn sau được biên dịch sẵn của HyperOS (như Spotify, Xiaomi Music,
QQ Music, NetEase Cloud Music, Kugou và Kuwo) được cố ý bỏ khỏi cả bộ chọn lẫn tự phát hiện vì
firmware Xiaomi này đã hỗ trợ chúng trên màn hình sau mà không cần proxy.

Thông báo MediaStyle của trình phát đã chọn bị tạm ẩn trong khi YTRear cung cấp trình phát thay thế.
Điều này ngăn ứng dụng gốc giành lại thứ hạng media cao nhất của HyperOS và làm thu gọn Dynamic Island
khi chuyển bài. YouTube Music là mục tiêu được kiểm chứng đầy đủ; phiên, nút điều khiển và việc thay
thế thông báo của Poweramp đã được kiểm chứng trên thiết bị. Các ứng dụng khác công bố MediaSession
chuẩn nên hoạt động, nhưng vẫn cần kiểm tra hồi quy thực tế.

### Lưu ý về thông báo của trình phát đã chọn

Không cần đổi quyền hay cài đặt nào trên chính trình phát đã chọn. Chỉ cần lưu ý một điều:

**Giữ thông báo của trình phát đã chọn được bật.** Đừng tắt toàn bộ thông báo của ứng dụng đó. YTRear
làm việc *cùng* thông báo media — nó tạm ẩn thông báo đó và đăng thông báo của mình thay thế.

Thông báo media của trình phát đã chọn sẽ biến mất khỏi khay trong khi YTRear đang chạy. Đây là chủ
ý, không phải lỗi: nếu cả hai cùng xuất hiện trong SystemUI, HyperOS sẽ bỏ mục Dynamic Island của
YTRear khi chuyển bài. Việc phát nhạc không bị ảnh hưởng, và thẻ của YTRear trở thành trình phát hiển
thị. Để lấy lại thông báo gốc, tắt ô Quick Settings của YTRear (hoặc tắt quyền truy cập thông báo của
YTRear), sau đó buộc dừng và mở lại trình phát.

Khi chọn trình phát khác, YTRear tự trả lại thông báo đang bị tạm ẩn của trình phát trước. Nếu trình
phát đó vẫn chạy, thông báo có thể trở lại ngay; nếu không, nó sẽ xuất hiện bình thường ở lần tiếp
theo trình phát khởi động hoặc đăng thông báo media.

Gỡ YTRear không làm thay đổi cài đặt hay dữ liệu của trình phát đã chọn. Android có thể vẫn giữ thông
báo đang bị tạm ẩn sau khi gỡ; nếu thông báo không trở lại ngay, hãy buộc dừng trình phát, mở lại và
bắt đầu phát.

## Build

Yêu cầu JDK 17 và Android SDK (compileSdk 36, build tools 36.0.0).

```bash
./gradlew :app:assembleDebug
```

APK nằm tại `app/build/outputs/apk/debug/app-debug.apk`.

APK phát hành 1.5.1 cũng được lưu cục bộ tại `releases/YTRear-1.5.1-debug.apk` với SHA-256
`1F7AE9113AE52F118469ED1DD7DEBD07804B64BEC97312E956BB086A100A395B`. APK báo
`com.luna.music` phiên bản 1.5.1 (`versionCode 19`) và nâng cấp đè lên 1.5.0 trong khi giữ dữ liệu
ứng dụng và quyền đã cấp.

### Phát hành tự động

Workflow **Release** chạy khi có push lên `main`. Workflow đọc `versionName` và `versionCode` từ
`app/build.gradle.kts`, build APK debug, tạo tag `v<version>` nếu chưa có, rồi đăng GitHub Release
kèm APK và file `.sha256`. Nếu release của phiên bản đó đã tồn tại, workflow bỏ qua. Nếu tag đã tồn
tại ở commit khác, workflow dừng với lỗi thay vì di chuyển tag. Có thể chạy lại thủ công từ tab
**Actions** bằng **Release** → **Run workflow**. Nếu còn tag cũ từ lần thử trước, hãy xóa trước bằng
`git tag -d vX.Y.Z` và `git push origin :refs/tags/vX.Y.Z`.

## Định danh package

Bản build đặt `applicationId` thành một package nằm trong danh sách nhạc màn sau của firmware, trong
khi namespace Kotlin vẫn là `dev.ytrear.app`. Android không thể cài chủ sở hữu thật của package đó
song song với bản build này. Chỉ dùng trên thiết bị bạn sở hữu, cho mục đích kiểm thử tương thích.

## Issue và đóng góp

Repo gốc đã ngừng hoạt động. Hãy báo lỗi, đề xuất tính năng và gửi pull request tại
[issue tracker của bản fork này](https://github.com/Tnina2612/YTRear-on-Xiaomi-17-Pro-Series/issues).
Nếu tab Issues chưa khả dụng, hãy để lại bình luận ở bản phát hành mới nhất.

Nếu thấy YTRear hữu ích, một star cho repo là nguồn động viên rất lớn.

## Giấy phép

Các thay đổi gốc của bản fork được phát hành theo [Giấy phép MIT](LICENSE). Dự án gốc không kèm file
giấy phép, nên mã nguồn gốc vẫn thuộc quyền của tác giả gốc; xem [NOTICE](NOTICE) để biết chi tiết.

## Tài liệu

- [Changelog](CHANGELOG.md) — thay đổi theo phiên bản và ghi chú về các tính năng đã bỏ
- [Nghiên cứu](docs/RESEARCH.md) — kết quả reverse-engineering và các hướng đã loại bỏ
- [Kiểm thử](docs/TESTING.md) — trạng thái kiểm chứng và lệnh chẩn đoán
- [Phiên bản và rollback](docs/ROLLBACK.md) — mốc 1.2 đã ghim và lệnh hạ cấp đã kiểm chứng

Đã kiểm chứng trên Android 16 / SDK 36 với Xiaomi 17 Pro chạy HyperOS `OS3.0.318.0.WBLCNXM` và
`OS4.0.6.0.XBLCNXM`. Đường dẫn widget màn sau phụ thuộc firmware; các bản build ngoài danh sách đã
kiểm chứng sẽ hiện cảnh báo trong **Nâng cao** thay vì giả định hành vi giống hệt.
