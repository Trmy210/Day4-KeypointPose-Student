# Mini guideline - nhóm: T020  |  người gán: Nghiem Tra My  |  ngày: 16/9/2026

> Điền file này **trong lúc** gán nhãn, không phải sau khi xong. Mỗi lần bạn dừng lại
> hơn 10 giây để phân vân, đó là một dòng phải ghi vào đây.

## 1. Luật bắt buộc (đã thống nhất cả lớp - không sửa)

- Bộ 17 điểm COCO, đúng tên, đúng thứ tự. Lấy từ file `.SVG` chung.
- Mọi người trong ảnh đều có **đủ 17 điểm**. Điểm không dùng được thì gắn cờ, không xoá.
- Trái/phải tính theo **cơ thể người**, không theo bức ảnh.
- Bị che, còn trong khung -> `v = 1`, **vẫn đặt chấm** ở vị trí ước lượng.
- Ra ngoài mép ảnh -> `v = 0`, **không** đặt chấm.
- Không dùng `Hidden` (`h`) - nó không được lưu vào file.

## 2. Luật của nhóm bạn (phải điền)

| Tình huống | Luật nhóm bạn chọn | Vì sao |
| --- | --- | --- |
| Hông của người mặc quần áo dài | v=1, vẫn đặt chấm. Vị trí = giao của đường nối vai cùng bên → đầu gối cùng bên với đường ngang đi qua nếp gấp quần/đáy áo. Không bao giờ dùng v=0 chỉ vì không nhìn thấy da/đường viền hông. | Quần áo che bề mặt, không đưa khớp ra khỏi khung hình. v=0 nghĩa là "ngoài ảnh", dùng sai ở đây sẽ xoá khớp khỏi bảng điểm OKS (lỗi số 3, slide 46). Hông là khớp không có bề mặt nhìn thấy được nên phải suy ra từ giải phẫu, đúng như slide 12 yêu cầu. |
| Tai bị tóc hoặc mũ bảo hiểm che một phần | v=1, đặt chấm tại vị trí ống tai ngoài ước lượng: trên đường viền hàm, cách đuôi mắt cùng bên khoảng 1 chiều rộng mắt về phía sau. Che 100% bởi mũ bảo hiểm vẫn là v=1. | Tai là khớp có %v=1 cao nhất trong bảng đếm của tôi (left_ear 66%, right_ear 55%) nên phải có luật cố định, nếu không mỗi ảnh sẽ quyết một kiểu. Vật che nằm trước khớp chứ không làm khớp ra khỏi khung → theo định nghĩa là occluded. |
| Người bị cắt ở mép ảnh (chỉ thấy từ hông trở lên) | Tâm khớp ước lượng nằm trong khung → v=1 và đặt chấm; nằm ngoài mép → v=0 và không đặt chấm. Quyết theo từng khớp, không quyết cả cụm chân một lần. | Ranh giới phải là "trong hay ngoài khung", không phải "nhìn thấy hay không". Đây là nguồn v=0 chính trong bộ của tôi (ankle: 9/29 người mỗi bên), và nếu áp dụng theo cụm thì sẽ vô tình đặt v=0 cho đầu gối vẫn còn trong ảnh. |
| Cổ tay nằm sau tay lái / sau thân mình | v=1, đặt chấm tại điểm suy ra từ hướng cẳng tay nối dài cắt với vị trí bàn tay/ghi đông nhìn thấy được. Nếu không thấy cả bàn tay lẫn cẳng tay thì vẫn v=1, đặt theo tư thế. | left_wrist có %v=1 = 38%, cao thứ ba - phần lớn do tay lái và thân mình che. Cổ tay hiếm khi ra khỏi khung khi thân người còn trong khung, nên v=0 ở cổ tay gần như luôn là lỗi (bảng của tôi chỉ có 1 trường hợp right_wrist v=0, cần kiểm lại). |
| Hai người chồng lên nhau | Gán đủ 17 điểm cho từng người riêng biệt. Khớp của người ở sau bị người ở trước che → v=1 tại vị trí ước lượng theo thân của chính người đó. Tuyệt đối không mượn khớp nhìn thấy được của người phía trước. | Đây là nguồn của lỗi nham_nguoi. Nếu mượn điểm, model học rằng hai skeleton có thể dùng chung một khớp, và trên ảnh đông người nó sẽ trộn các bộ xương vào nhau. |
| Người nhỏ đến mức nào thì không gán nữa | Ngưỡng số: bỏ qua khi chiều cao bounding box < 40 px hoặc không phân biệt được vai với hông bằng mắt ở mức zoom 100%. Dưới ngưỡng thì không tạo skeleton, không tạo skeleton "đoán mò". | Phải là ngưỡng đo được thì hai người gán mới ra cùng kết quả. Skeleton đoán mò ở người tí hon tạo nhãn nhiễu có trọng số OKS rất lớn (OKS chia cho diện tích người: người càng nhỏ, sai lệch càng bị phạt nặng). |

Với mỗi luật, chèn **một ảnh mẫu** (screenshot từ CVAT) thay vì chỉ viết một câu.
Slide 12 nói rõ: khớp không có bề mặt nhìn thấy được thì phải có ảnh mẫu, không phải
một câu văn chung chung.

## 3. Ba ca mơ hồ đã gặp (bắt buộc, ghi ít nhất 3)

### Ca 1 - ảnh train_04.jpg, người thứ 2 (người bên phải, mũ fullface), khớp left_ear / right_ear

- Mơ hồ ở chỗ nào: người đội mũ fullface kín hoàn toàn, thêm kính goggle trên đỉnh mũ. Không thấy bất kỳ phần nào của vành tai, thậm chí không thấy đường viền đầu để suy ra vị trí tai. Không rõ đây là "bị che" hay "không tồn tại trong ảnh". So sánh trực tiếp: người trong train_11.jpg đội mũ lưỡi trai, vành tai vẫn ló ra - rõ ràng v=2; còn ca này thì không có mốc nào nhìn thấy được.
- Bạn quyết thế nào: v=1, đặt chấm tại ống tai ngoài ước lượng theo đường viền hàm và đuôi mắt cùng bên.
- Vì sao: tai vẫn nằm trong khung hình, chỉ bị vật thể khác nằm chắn phía trước. Đây đúng định nghĩa occluded. Chọn v=0 sẽ xoá khớp khỏi phép tính OKS thay vì chỉ hạ trọng số.
- Nếu người khác quyết ngược lại thì model học sai cái gì: model sẽ học rằng "đội mũ bảo hiểm = không có tai". Trong bộ 20 ảnh này có tới 7 ảnh người đội mũ bảo hiểm (train_02, 04, 06, 09, 12, 18, 20) - gần 1/3 dữ liệu. Sai lệch ở đây không phải nhiễu lẻ tẻ mà là sai lệch hệ thống: model sẽ bỏ trống toàn bộ vùng đầu ở ảnh giao thông, kéo theo sai luôn hướng mặt vì chỉ còn mắt và mũi để suy ra.

### Ca 2 - ảnh train_12.jpg, người thứ 1 (người chở thùng carton), khớp right_wrist

- Mơ hồ ở chỗ nào: tay phải vươn tới ghi đông xa, cổ tay khuất sau kính chắn gió và cụm gương chiếu hậu. Chỉ thấy bàn tay ló ra phía trước tay lái. Hai lựa chọn đều biện minh được: đặt chấm lên chỗ bàn tay (nhìn thấy được) hay đặt ở cổ tay thật (bị che).
- Bạn quyết thế nào: Bạn quyết thế nào: v=1, đặt chấm tại giao điểm của trục cẳng tay kéo dài với vị trí bàn tay/ghi đông nhìn thấy được.
- Vì sao: COCO định nghĩa wrist là khớp cổ tay, không phải "điểm nhìn thấy được gần cổ tay nhất". Đặt chấm lên bàn tay là lặng lẽ đổi định nghĩa của khớp chỉ vì nó dễ nhìn hơn. Cờ v=1 tồn tại đúng để xử lý tình huống này: vị trí ước lượng + đánh dấu bị che.
- Nếu người khác quyết ngược lại thì model học sai cái gì: nếu họ đặt chấm lên bàn tay, khoảng cách khuỷu→cổ tay trong dữ liệu bị kéo dài thêm khoảng một bàn tay ở mọi ảnh người cầm lái - mà bộ này có train_02, 06, 08, 09, 12, 18, 20 đều là tư thế cầm lái. Model học rằng cẳng tay dài hơn thực tế, và vì tư thế này chiếm phần lớn dữ liệu, sai lệch trở thành hệ thống chứ không phải nhiễu ngẫu nhiên. Nếu ngược lại họ đặt v=0, model mất tín hiệu độ dài cẳng tay khi tay chạm vật thể và sẽ dự đoán cổ tay trùng khuỷu tay - lỗi "trượt hẳn" theo phân loại slide 43.

### Ca 3 - ảnh train_20.jpg, người thứ 1 (cảnh sát trên mô tô), khớp left_ankle / right_ankle

- Mơ hồ ở chỗ nào: toàn bộ thân dưới khuất sau thùng hông, động cơ và tấm chắn của xe mô tô. Không thấy đầu gối lẫn cổ chân. Nhưng cổ chân vẫn nằm trong khung ảnh - chỉ bị thân xe che. Rất dễ phản xạ chọn v=0 vì "không thấy gì cả", trong khi đúng luật phải là v=1. Cùng tình huống lặp lại ở train_06, train_09, train_12.
- Bạn quyết thế nào: v=1. Dựng đường hông→gối theo tư thế ngồi lái (đùi gần ngang), rồi kéo dài một đoạn bằng chiều dài cẳng chân ước lượng để ra cổ chân. Đối chiếu với vị trí gác chân của xe. Chỉ dùng v=0 khi điểm dựng được rơi ra ngoài mép ảnh, không phải khi nó rơi vào sau thân xe.
- Vì sao: phải có phép dựng hình kiểm chứng được, nếu không mỗi lần gán sẽ ra kết quả khác. Quan trọng hơn: đây là chỗ hai khái niệm dễ bị nhập làm một. "Không nhìn thấy" ≠ "ngoài khung". Thân xe che là occluded; chỉ mép ảnh mới tạo ra outside.
- Nếu người khác quyết ngược lại thì model học sai cái gì: gắn v=0 ở đây sẽ xoá khớp khỏi OKS (lỗi số 3, slide 46) - model đoán cổ chân ở bất cứ đâu cũng không bị phạt. Vì bộ này có rất nhiều ảnh người ngồi xe, model sẽ học rằng "ngồi trên xe = không có chân" và mất hẳn khả năng ước lượng tư thế thân dưới bị che, đúng thứ ta cần nó làm được nhất. Ngược lại, dùng v=1 cho cổ chân đã thật sự ra ngoài ảnh (như train_10.jpg) thì model học cách "bịa" khớp bên ngoài biên và sẽ đẩy dự đoán ra sát mép ở mọi ảnh bị crop.

## 4. Sau khi so visibility report với bạn cùng nhóm

- Khớp lệch `%v=1` nhiều nhất: `______` (bạn `___%` / họ `___%`)
- Nguyên nhân là **guideline chưa rõ** hay **một trong hai bên gán sai**:
- Luật mới bổ sung vào mục 2 sau khi thống nhất:
