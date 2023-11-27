---
title: WebRTC: Định nghĩa, Lợi ích và Quy trình hoạt động
type: docs
weight: 2
---

# WebRTC: Cái gì, Tại sao, và Làm thế nào

## WebRTC là gì?

WebRTC, là cách nói ngắn gọn của Web Real-Time Communication, bao gồm APIs và giao thức. Giao thức WebRTC là một bộ quy tắc để 2 đối tượng sử dụng WebRTC thỏa thuận truyền thông tin thời gian thực. WebRTC API cho phép lập trình viên sử dùng giao thức WebRTC. WebRTC API chỉ được sử dụng cho JavaScript.

Một cách tương tự như quan hệ giữa HTTP và Fetch API. Giao thức WebRTC có thể xem như là HTTP, còn WebRTC API được xem như là Fetch API.

Giao thức WebRTC có sẵn trong các API và ngôn ngữ khác ngoài JavaScript. Bạn có thể tìm thấy các máy chủ và các công cụ cụ thể cho miền cho WebRTC. Tất cả các triển khai này sử dụng giao thức WebRTC để có thể tương tác với nhau. 

Giao thức WebRTC được phát triển bởi IETF có thể được tìm thấy tại [rtcweb](https://datatracker.ietf.org/wg/rtcweb/documents/). WebRTC API là tài liệu được W3C cung cấp tại [webrtc](https://www.w3.org/TR/webrtc/)

## Tại sao bạn nên học WebRTC?

Một vài lời ích mà WebRTC mang lại:

* Tiêu chuẩn mở
* Nhiều triển khai
* Sẵn có trên trình duyệt
* Bắt buộc mã hóa
* NAT Traversal
* Tái sử dụng công nghệ hiện tại
* Kiểm soát quá tải
* Độ trễ dưới một giây

Danh sách này không phải là đầy đủ, chỉ là một ví dụ về một số điều bạn có thể đánh giá trong hành trình của mình. Đừng lo lắng nếu bạn chưa biết tất cả những thuật ngữ này, cuốn sách này sẽ giúp bạn hiểu chúng dần dần qua quá trình học.

## Giao thức WebRTC là sự thu nạp từ nhiều công nghệ

Giao thức WebRTC là một chủ đề lớn nó cần một quyển sách dày để giải thích. Tuy nhiên chúng ta có thể bắt đầu bằng việc chia ra làm 4 bước:

1. Tín hiệu (Signaling)
2. Kết nối (Connecting)
3. Bảo mật (Securing)
4. Giao tiếp (Communicating)

Các bước sẽ được thực hiện theo thứ tự, nghĩa là các bước phải thành công 100% để bắt đầu bước tiếp theo.

Có một sự thật khá hay về WebRTC đó là mỗi bước được thực hiện bởi nhiều giao thức khác nhau! Để tạo lên WebRTC, chúng ta kết hợp nhiều công nghệ lại với nhau. Chính vì thế bạn có thể xem như WebRTC là tổ hợp công nghệ từ những năm 2000 thay vì là một công nghệ mới.

Mỗi bước trong này đầu có một chương riêng, nhưng sẽ giúp ích cho việc hiểu chúng ở mức tổng quan trước. Vì chúng phụ thuộc lẫn nhau, điều này sẽ giúp khi giải thích mục đích của từng bước trong quá trình tiếp theo.

### Signaling: Làm thế nào để mỗi người dùng tìm thấy nhau trong WebRTC

Khi một người dùng WebRTC bắt đầu, họ không biết phải kết nối thế nào hoặc kết nối với ai. Chính vì thế  *Signaling* là bước giải quyết vấn đền này. Signaling là bước đầu để kết nối cho phép người sử dụng WebRTC có thể bắt đầu giao tiếp.

Signaling sử dụng một giao thưc văn bản được gọi là SDP (Session Description Protocal). Mỗi văn bản SDP được tạo bởi các cặp key/value chứa thông tin media trong phiên làm việc đó. SDP được trao đổi giữa hai đối tượng sử dụng WebRTC bao gồm một vài thuộc tính:

* The IPs and Ports cái mà WebRTC có thể kết nối (candidates).
* Số lượng audio và video mà người dùng WebRTC mong muốn gửi đi.
* Codecs mà WebRTC có thể hỗ trợ.
* Giá trị dùng để kết nối (`uFrag`/`uPwd`).
* Giá trị dùng để tạo bảo mật (certificate fingerprint).

Quan trọng cần lưu ý rằng signaling xảy ra "bên ngoài", nghĩa là ứng dụng thường không sử dụng WebRTC để trao đổi những thông tin về signaling của chính nó. Chúng ta có thể sử dụng nhiều kiến trúc phù hợp để truyền SDPs giữa các người dùng (ví dụ: REST endpoints, WebSocket connections hoặc authentication proxies).

### Kết nối và NAT Traversal với STUN/TURN

Khi mà hai đối tượng sử dụng WebRTC có trao đổi SDPs, họ phải có đủ thông tin để thử kết nối với nhau. Để tạo được sự kết nối này, WebRTC sử dụng công nghệ khác để khởi tạo được gọi là ICE (Interactive Connectivity Establishment).

ICE là một giao thức giúp thiết lập kết nối trực tiếp giữa hai đối tượng sử dụng mà không cần đến server trung gian, cho phép họ kết nối trực tiếp qua cùng một mạng hoặc qua các mạng khác nhau.

Mặc dùICE cho phép kết nối trực tiếp, nhưng phần thú vị thực sự của quá trình kết nối liên quan đến một khái niệm gọi là 'NAT Traversal' và sử dụng các máy chủ STUN/TURN. Hai khái niệm này, mà chúng ta sẽ khám phá sâu hơn sau này, là tất cả những gì bạn cần để giao tiếp với một đối tượng ICE ở trong một subnet khác.

Khi hai đối tượng tạo thành công kết nối ICE, WebRTC sẽ chuyển sang bước tiếp theo đó là thiết lập bảo mật để chia sẻ audio, video và data giữa chúng.

### Bảo mật lớp truyền tin với DTLS và SRTP

Khi tạo kết nối ICE thành công chúng ta có thể giao tiếp hai chiều thông qua ICE, chính vì thế chúng ta cần bảo mật việc giao tiếp này. Điều này được thực hiện với 2 giao thức đã có trước WebRTC; DTLS (Datagram Transport Layer Security) và SRTP (Secure Real-Time Transport Protocol). Giao thức đầu tiên, DTLS, đơn giản là TLS qua UDP (TLS là giao thức mật mã được sử dụng để bảo vệ giao tiếp qua HTTPS). Giao thức thứ hai, SRTP, được sử dụng để đảm bảo mã hóa của RTP (Real-time Transport Protocol) các gói dữ liệu.

Đầu tiên, WebRTC kết nối bằng cách thực hiện quá trình bắt tay DTLS thông qua kết nối được thiết lập bởi ICE. Khác với HTTPS, WebRTC không sử dụng một cơ chế tập trung để xác nhận. Thay vào đó, nó đơn giản xác nhận rằng chứng chỉ được trao đổi qua DTLS phải khớp với fingerprint được chia sẻ qua tín hiệu. Kết nối DTLS sau đó được sử dụng cho các thông điệp DataChannel. 

Tiếp theo, WebRTC sử dụng giao thức RTP, được bảo mật bởi SRTP, cho việc trao đổi audio/video. Chúng ta khởi tạo một phiên làm việc SRTP bằng cách trích xuất các khóa từ thỏa thuận của phiên làm việc DTLS.

Chúng ta sẽ thảo luận về lý do tại sao phương tiện và dữ liệu được trao đổi thông qua các phương tiện riêng biệt trong các chương sau, nơi chúng ta có thể thấy rằng các thông tin này được xử lý độc lập.

Phần cơ bản của quá trình đã được hoàn tất! Chúng ta đã thành công trong việc thiết lập giao tiếp hai chiều và đảm bảo tính an toàn. Nếu bạn có một kết nối ổn định giữa các đối tượng WebRTC của mình, đây là những yếu tố quan trọng. Trong phần tiếp theo, chúng ta sẽ thảo luận về cách WebRTC giải quyết các vấn đề về mất dữ liệu và băng thông.

### Giao tiếp giữa các đối tượng thông qua RTP và SCTP

Giả sử chúng ta có hai đối tượng WebRTC đã kết nối và bảo mật, kết nối hai chiều được thiết lập và đã bắt đầu trao đổi thông tin. Như ở trên, WebRTC sẽ sử dụng hai giao thức đã có sẵn: RTP (Real-time Transport Protocol), and SCTP (Stream Control Transmission Protocol). Chúng ta sử dụng RTP để trao đổi media đã được mã hóa với SRTP, và chúng ta sử dụng SCTP để gửi và nhận thông điệp DataChannel đã được mã hóa với DTLS.

RTP là một giao thức đơn giản, nhưng nó đủ mạnh mẽ để triển khai luồng truyền thời gian thực. Điểm quan trọng với RTP là khả năng của nó để người phát triển kiểm soát độ trễ, mức độ mất mát, và vấn đề tắc nghẽn của các gói tin. Chúng ta sẽ thảo luận chi tiết về media trong chương tiếp theo.

Giao thức cuối cùng mà chúng ta xem xét trong chương này là SCTP. Điều quan trọng với SCTP là khả năng tắt mở tính năng bảo mật và xác định thứ tự tin nhắn (cùng với nhiều tính năng khác). Nó cung cấp cho người phát triển khả năng đảm bảo độ trễ trong một hệ thống thời gian thực.

## WebRTC, tổng hợp của các giao thức

WebRTC giải quyết rất nhiều vấn đề. Nó không được tạo ra với mục địch làm tất cả mọi thứ tốt hơn mà thay vào đó nó sử dụng những công nghệ đã có sẵn một cách linh hoạt và có thể ứng dụng rộng rãi.

Nó cho phép chúng ta kiểm tra lại kiến thức mà học những kiến thức mới của từng công nghệ. Cách để có cái nhìn tổng quan về "WebRTC agent" đó là nó sử dụng nhiều giao thức khác nhau.

![WebRTC Agent](../images/01-webrtc-agent.png "WebRTC Agent Diagram")

## WebRTC API được sử dụng thế nào?

Phần này trình bày cách API JavaScript của WebRTC tương ứng với giao thức WebRTC được mô tả ở trên. Nó không được thiết kế như một bài thực hành mở rộng về API WebRTC, mà  là tạo ra một mô hình tư duy về cách chúng liên kết với nhau. Nếu bạn chưa quen với cả giao thức và API, đừng lo lắng. Đây có thể là một phần thú vị để quay lại khi bạn tìm hiểu thêm!

### `new RTCPeerConnection`

`RTCPeerConnection` là phần cao nhất của "WebRTC Session", nó bao gồm các giao thức được nhắc đến ở trên. The subsystems are all allocated but nothing happens yet.

### `addTrack`

`addTrack` cho phép chúng ta tạo luồng RTP. Một nguồn đồng bộ hóa ngẫu nhiên (SSRC) sẽ được tạo ra cho luồng này. Sau đó, luồng này sẽ nằm trong mô tả phiên làm việc  được tạo ra bởi `createOffer` bên trong một phiên media. Mỗi lần gọi `addTrack` sẽ tạo ra một SSRC và một phiên media mới.

Ngay sau khi phiên làm việc SRTP được thiết lập thì các gói tin media sẽ bắt đầu được mã hóa bằng SRTP và gửi đi thông qua ICE.

### `createDataChannel`

`createDataChannel` tạo một luồng SCTP mới nếu không có luồng SCTP nào tồn tại. SCTP không được khởi tạo mặc đinh. Nó chỉ được bắt đầu khi một bên yêu cầu một kênh dữ liệu.

Ngay sau khi một phiên làm việc DTLS được thiết lập, SCTP liên quan sẽ bắt đầu gửi nhưng gói tin đã được mã hóa bằng DTLS thông qua ICE. 

### `createOffer`

`createOffer` tạo ra một mô tả phiên làm việc của các trạng thái làm việc của chính nó để thông tin đó được chia sẻ đến cho đối tượng còn lại.

Việc gọi `createOffer` sẽ không làm thay đổi bất cứ thông tin gì của đối tượng gọi nó.

### `setLocalDescription`

`setLocalDescription` xác nhận bất kỳ thay đổi nào được yêu cầu. Các cuộc gọi như `addTrack`, `createDataChannel`, và các cuộc gọi tương tự chỉ là tạm thời cho đến khi cuộc gọi này được thực hiện. `setLocalDescription` được gọi với giá trị được tạo ra bởi `createOffer`.

Sau khi gọi `setLocalDescription` chúng ta sẽ gửi lại các thay đổi mới cho các đối tượng còn lại và nó sẽ sử dụng để gọi `setRemoteDescription`.

### `addIceCandidate`

`addIceCandidate` cho phép đối tượng sử dụng WebRTC them nhiều giá trị ICE tại nhiều thời điểm. API này sẽ gửi giá trị ICE có thể sử dụng đển "ICE subsystem" và nó sẽ không tác động gì với kêt nối WebRTC tốt hơn.

### `ontrack`

`ontrack` là một callback được trả về giá trị khi gói tin RTP được các đối tượng khác gửi về. Các gói tin đến sẽ đã được khai báo trong Session Description được truyền vào setRemoteDescription.

WebRTC sử dụng SSRC và tìm kiếm MediaStream và MediaStreamTrack liên quan, sau đó kích hoạt callback này với các thông tin đầy đủ.

### `oniceconnectionstatechange`

`oniceconnectionstatechange` là một callback được kích hoạt mô tả sự thay đổi trạng thái của một đối tượng ICE. Khi mà chúng ta thay đổi kết nối mạng nó sẽ được kích hoạt

### `onconnectionstatechange`

`onconnectionstatechange` bao gồm trạng thái của ICE và DTLS. Chúng ta có thể thấy nó được kích hoạt khi cả ICE và DTLS hoàn thành nhiệm vụ thành công.