# Cây Quyết Định (Decision Tree)

## 1. Định nghĩa

- Cây quyết định giúp chúng ta đưa ra quyết định bằng cách mô tả các lựa chọn khác nhau và kết quả có thể xảy ra.  
- Decision Tree đưa ra quyết định bằng cách thể hiện các lựa chọn và mối quan hệ giữa chúng.  
- Nó có cấu trúc giống như một cái cây, bắt đầu với một câu hỏi chính gọi là **nút gốc (root node)**, đại diện cho toàn bộ tập dữ liệu.  

### Các thành phần của cây:
- **Root node (nút gốc):** Điểm bắt đầu, biểu diễn toàn bộ dữ liệu.  
- **Branches (các nhánh):** Đường nối giữa các nút, thể hiện dòng chảy của quyết định.  
- **Internal nodes (nút trong):** Điểm nơi đưa ra quyết định dựa trên đặc trưng dữ liệu.  
- **Leaf nodes (nút lá):** Điểm cuối của cây, nơi đưa ra dự đoán hoặc quyết định cuối cùng.  

### Các loại cây quyết định:
- **Cây phân loại (Classification Tree):**  
  Dùng để dự đoán kết quả dạng phân loại, ví dụ: email *spam* hay *không spam*.  
  Cây này tách dữ liệu dựa trên đặc trưng để phân loại vào các nhóm đã xác định.  

- **Cây hồi quy (Regression Tree):**  
  Dùng để dự đoán giá trị liên tục, ví dụ: dự đoán giá nhà.  
  Thay vì gán nhãn, nó đưa ra giá trị số dựa trên đặc trưng đầu vào.  

## 2. Cách hoạt động của Decision Tree

1. **Bắt đầu từ nút gốc:** Cây bắt đầu với một câu hỏi chính tại nút gốc, được rút ra từ các đặc trưng trong tập dữ liệu.  
2. **Đặt câu hỏi Yes/No:** Từ nút gốc, cây đặt một loạt câu hỏi dạng có/không để chia dữ liệu thành các tập con dựa trên đặc trưng cụ thể.  
3. **Phân nhánh dựa trên câu trả lời:**  
   - Nếu *Yes* → đi theo một nhánh.  
   - Nếu *No* → đi theo nhánh khác.  
4. **Tiếp tục phân chia:** Quá trình phân nhánh tiếp tục với các câu hỏi tiếp theo, giúp thu hẹp dữ liệu từng bước.  
5. **Đến nút lá:** Quá trình kết thúc khi không còn câu hỏi hữu ích nào để tách, lúc đó ta đến nút lá – nơi quyết định hoặc dự đoán cuối cùng được đưa ra.  

## 3. Tiêu chí phân chia trong Decision Tree

Trong cây quyết định, quá trình chọn cách chia dữ liệu tại mỗi nút rất quan trọng.  
Tiêu chí phân chia tìm ra đặc trưng tốt nhất để tách dữ liệu.  

### Các tiêu chí phổ biến:

- **Gini Impurity (Độ nhiễm bẩn Gini):**  
  - Tính xác suất mà hai phần tử được chọn ngẫu nhiên từ cùng một nhóm có nhãn khác nhau.  
  - Gini = 0 → nhóm hoàn toàn thuần khiết (chỉ có một loại nhãn).  
  - Gini cao → nhóm pha trộn nhiều nhãn.  
  - ![Công thức Gini](img/formula_gini.png)
  - pi là tỷ lệ của lớp thứ i trong tập giữ liệu con và c là số lớp.

- **Entropy (Độ hỗn loạn):**  
  - Đo lường mức độ không chắc chắn hay hỗn loạn trong dữ liệu.  
  - Cây quyết định sẽ cố gắng giảm entropy bằng cách chọn đặc trưng giúp “giải thích” nhãn mục tiêu tốt nhất.  
    ![Công thức Entropy](img/formula_entropy.png)
- Cả 2 tiêu chí trên đều tuân theo nguyên tắc: tìm cách giảm thiểu sự không thuần khiết sau khi phân tách.

## 4. Quá trình phân tách:
- Quá trình lặp đi lặp lại tại mỗi nút của cây:
- **Tính toán Gini/Entropy cho nút hiện tại:** Đầu tiên, tính toán giá trị Gini Impurity hoặc Entropy cho nút cha trước khi phân tách.
- **Đánh giá từng đặc trưng:** Với mỗi đặc trưng có thể có, cây quyết định sẽ thử phân tách dữ liệu dựa trên các giá trị của đặc trưng đó. Sau đó, nó sẽ tính toán Gini hoặc Entropy trung bình có trọng số cho các nút con được tạo ra.
    + Gini Gain/Information Gain: Cây quyết diudnhj không chỉ nhìn vào giá trị Gini/Entropy của các nút con, mà còn tính toán mức độ gairm của Gini/Entropy sau khi phân tách. Mức giảm này được gọi là Gini Gain (hoặc Information Gain khi sử dụng Entropy).\
    ![Công thức Entropy](img/formula_informationgain.png)
- **Chọn đặc trưng tốt nhất:** Đặc trưng nào mang lại Information Gain lớn nhất (tức là làm giảm Entropy/Gini nhiều nhất) sẽ được chọn làm điểm phân tách tại nút đó.
- **Phân tách và lặp lại:** Dữ liệu sẽ được phân chia thành các tập con dựa trên đặc trưng đã chọn, và quá trình này được lặp lại cho mỗi nút con mới cho đến khi cây đạt đến một tiêu chí dừng nào đó (các nút hoàn toàn thuần khiết, hoặc số lượng nút tối đa).

---
## 5. Cắt tỉa trong cây quyết định:
- Cắt tỉa được dùng để ngừa overfitting trong DT. Overfitting xảy ra khi 1 cây trở nên quá sâu và bắt đầu học thuộc lòng dữ liệu huấn luyện thay vì học các quy luật chung.
- Kỹ thuật này giúp giảm độ phức tạp của cây bằng cách loại bỏ các nhánh có ít khả năng dự đoán. Nó cải thiện hiệu suất mô hình bằng cách giúp cây khái quát hóa tốt hơn với dữ liệu mới. Ngoài ra, nó giúp mô hình đơn giản hơn và triển khai nhanh hơn.
- Tỉa cây rất hữu ích khi một cây quyết định quá sâu và bắt đầu nắm bắt cả những nhiễu trong dữ liệu.

---
# Random Forest
## 1. Giới thiệu chung:
- Là thuật toán học máy sử dụng nhiều cây quyết định để đưa ra dự đoán tốt hơn. Mỗi cây xem xét các phần ngẫu nhiên khác nhau của dữ liệu và kết quả của chúng được kết hợp bằng cách bỏ phiếu cho phân loại (Classification) hoặc tính trung bình cho hồi quy (Regression) --> Tạo nên một kỹ thuật học tổng hợp.
## 2. Hoạt động của thuật toán Random Forest:
1. **Tạo nhiều cây quyết định:** Thuật toán tạo ra nhiều cây quyết định, mỗi cây sử dụng một phần dữ liệu ngẫu nhiên.
2. **Chọn tính năng ngẫu nhiên:** Khi xây dựng mỗi cây, nó không xem xét tất cả các tính năng (cột) cùng một lúc. Chọn ngẫu nhiên một vài tính năng để quyết định phân chia dữ liệu.
3. **Mỗi cây đưa ra một dự đoán:** Mỗi cây sẽ đưa ra 1 câu trả lời hoặc dự đoán riêng dựa trên những gì nó học được từ phần dữ liệu của mình.
4. **Kết hợp các dự đoán:**
  + **Classification:** Chọn một danh mục vì câu trả lời cuối cùng là câu trả lời mà hầu hết các cây đều đồng ý.
  + **Regression:** Dự đoán 1 số là trung bình của tất cả các dự đoán.

## 3. Giả định của Random Forest:
- Mỗi cây tự đưa ra quyết định của riêng mình: Mỗi cây trong rừng đều tự đưa ra dự đoán của riêng mình mà không cần dựa vào cây khác.
- Các phần dữ liệu ngẫu nhiên được sử dụng.
- Cần có đủ dữ liệu.
- Các dự đoán khác nhau cải thiện độ chính xác.

---
# Rừng cô lập (Isolation Forest)
## 1. Giới thiệu chung:
- Là một thuật toán xác định các điểm ngoại lệ trong tập dữ liệu lớn bằng cách cô lập chúng thông qua phân cùng nhị phân, vốn đòi hỏi chi phí tính toán tối thiểu.
## 2. Các khái niệm chính:

1. **Cô lập:** Thuật toán cô lập các điểm bất thường bằng cách tập trung vào sự khác biệt của chúng so với các điểm dữ liệu thông thường thay vì điểm tương đồng.
2. **Phân vùng:** Dữ liệu được phân chia bằng cách chọn ngẫu nhiên các đặc điểm và sử dụng các giá trị ngẫu nhiên để phân vùng dữ liệu.
3. **Điểm bất thường:** Đo lường mức độ dễ dàng phân tác một điểm dữ liệu. Các điểm cần ít lần phân tán hơn để phân tách được coi là bất thường và được gán điểm cao hơn.

## 3. Hoạt động của thuật toán isolation forest:
- Hoạt động thông qua quy trình phân vùng đệ quy, tạo ra nhiều cây quyết định xác định các điểm bất thường.
1. **Phân vùng ngẫu nhiên:** Bắt đầu bằng cách chọn một tính năng ngẫu nhiên từ tập dữ liệu. Sau đó chia dữ liệu theo giá trị ngẫu nhiên trong phạm vi của tính năng đó, chia làm 2 phần. Lặp lại theo đệ quy, tạo ra cây nhị phân trong đó mỗi nhánh biểu diễn một phần chia tách trong dữ liệu.

2. **Đường dẫn cô lập:** Đề cập đến số lần phân tách cần thiết để cô lập một điểm dữ liệu. Các điểm bất thường có đường đi ngắn hơn vì chúng ở xa phần dữ liệu hơn, do đó cần ít lần phân tách hơn để tách chúng.

3. **Quần thể cây:** Thay vì dựa vào 1 cây duy nhất, nó xây dựng 1 tập hợp các cây. Mỗi cây được tạo độc lập với các phân tách ngẫu nhiên, giúp tạo ra đường cô lập đa dạng cho mỗi điểm dữ liệu trên nhiều cây.\
==> Đảm bảo tinh mạnh mẽ và độ tin cậy của kết quả.

4. **Điểm số bất thường:** Điểm bất thường cho mỗi điểm dữ liệu được tính bằng cách lấy trung bình độ dài đường dẫn trên tất cả các cây. Đường đi ngắn hơn (ít phân tách hơn) cho thấy điểm đó có nhiều khả năng là điểm bất thường.

5. **Phân loại:** Để phân loại các điểm dữ liệu là bình thường hay bất thường, thuật toán đặt ngưỡng cho điểm bất thường. Các điểm trên ngưỡng được phân loại là bất thường, trong khi các điểm dưới ngưỡng được coi là bình thường.

---
# CONTINUOS MONITORING OF DISTANCE-BASED OUTLIERS OVER DATA STREAMS
## Định nghĩa 1: Objects neighbors:
  Giả sử R >= 0 là một ngưỡng do người dùng xác định. Đối với 2 đối tượng dữ liệu pi và pj, nếu khoảng cách giữa chúng không lớn hơn R, pi và pj được gọi là hàng xóm. Hàm nn(pi, R) biểu thị số lượng hàng xóm mà đối tượng pi có, với tham số R.

## Định nghĩa 2: Distance-Based Outlier
  Với R và một tham số k>=O, một ngoại lệ dựa trên khoảng cách là một đối tượng pi, nơi nn(pi, R) < k.
  Tập distance-based outlier được ký hiệu là D(R, k) và tập Inlier là I(R, k).

## Vấn đề 1: Single-query Distance-Based Outlier Detection:
  Với các tham số R và k và 1 window size W cố định, đưa ra các điểm outlier dựa trên khoảng cách giữa tất cả các đối tượng chưa hết hạn tại mỗi luần trượt cửa sổ.

## Vấn đề 2: Multi-query Distance-Based Outlier Detection:
  Với 1 tập query Q, đưa ra các outlier giữa các điểm hết hạn cho mỗi query tại mỗi lần trượt.

## SIMPLE ALGORITHM
### 1. Phân loại neighbor:
  Để phát hiện các outliers dựa trên khoảng cách D(R, k) cho một R và k cụ thể, chỉ cần duy trì tối đa k neighbors đi trước và số lượng neighbors đi sau cho mỗi đối tượng.\
  ==> Đối với neighbor đi sau của p, ta chỉ cần lưu trữ số lượng np(+).
- Note:
  + Nếu số lượng p có >= k neighbors đi sau, thì p sẽ không bao giờ trở thành outliers và nó được gọi là safe inliers.
  + Một safe inliers không được lưu trong event queue.
  + Nếu p là inlier nhưng không phải là safe inlier (nghĩa là np(+) < k) thì ta lưu k - np(+) đối tượng gần nhất trong tập Pp. Vì chỉ những đối tượng này có thể ảnh hưởng đến trạng thái của p (tổng cộng có k neighbors).\
==> Tất cả các đối tượng được lưu trong một cấu trúc hỗ trợ truy vấn phạm vi hiệu quả (ví dụ M-tree). Tiếp theo, chúng tôi mô tả cách lược đồ dựa trên sự kiện được áp dụng.

Giả sử p là 1 đối tượng, và đặt: p.minexp = min{pi.exp | pi ∈ Pp} là thời gian hết hạn nhỏ nhất trong tập Pp.

Giả sử p là một inlier (không phải safe inlier) tại thời điểm hiện tại (now). Khi đó, sự kiện tương ứng với p sẽ có timestamp p.ev = p.minexp, và p sẽ được kiểm tra lại như một outlier candidate tại thời điểm p.ev.

### 2. Cách xử lý event queue và update D(R, k).
Có 2 trường hợp dẫn đến xử lý hàng đợi sự kiện và cập nhật D(R, k). Dựa trên cách xử lý khi có đối tượng mới đến, ta có 2 biến thể của phương pháp đề xuất, xử lý hàng đợi sự kiện theo những cách khác nhau:
- **Lazy Update of Events (LUE)**
  + Khi một đối tượng mới p' đến:
    + Thực hiện truy vấn phạm vi.
    + Với mọi đối tượng pi ∈ D(R, k) được trả về, tăng npi(+) thêm 1.
    + Nếu một đối tượng pi đạt đủ k neighbors, nó được đưa vào event queue và giá trị p.ev được thiết lập tương ứng.
    + Tập Pp' được xây dựng với kích thước tối đa k.
    + Với mỗi pi ∈ I được trả về từ truy vấn, giá trị npi(+) cũng được tăng thêm 1.
    + Cuối cùng:
      + Nếu np'(-) < k thì p' là outlier và được thêm vào D(R, k).
      + Ngược lại, p' được thêm vào event queue.

  + Khi một đối tượng rời đi, một sự kiện có thể được kích hoạt bằng cách gọi extractmin, trả về đối tượng x sao cho x.ev = now.
    + If nx(-) + nx(+) < k thì x trở thành outlier và được thêm vào D(R, k). Nếu không, x.ev và Px được cập nhật, rồi chèn lại vào event queue.

- **Direct Update of Event (DUE)**
  + Khi đối tượng p' đến: Thời gian sự kiện của các đối tượng trong hàng đợi sự kiện được tính toán lại.
  + Cụ thể, tất cả các phép tính giống LUE, ngoại trừ:
    + Mọi đối tượng pi ∈ I trả về từ truy cấn phạm vi đều được cập nhật lại thời gian sự kiện.
    + Tập Ppi của mỗi đối tượng đó được cập nhật và kiểm tra xem nó có trở thành safe inlier không.
  + Điều này có nghĩa là với mỗi đối tượng như vậy, một thao tác increasetime được thực hiện (ít tốn kém hơn extractmin). Khi một sự kiện được xử lý liên quan đến đối tượng x do một đối tượng khác rời đi, thì sự kiện này chắc chắn sẽ khiến x trở thành outlier.
  + Như vậy, số lần gọi extractmin được giảm cách thay thế bằng các lần gọi increasetime.
    + Các dòng 4 và 6-10 bị xóa trong hàm Procerss Event Queue (vì mỗi sự kiện đều ứng với một outlier).
    + Ngay sau dòng 11 trong thuật toán Arrival, thêm một số dòng để tính lại thời gian sự kiện mới ev trong q vbaf gọi thủ tục increasetime(q.ev - now).

## MULTIPLE OUTLIER DETECTOR
## 1. Tổng quan:
- Phần này nghiên cứu việc đánh gái liên tục nhiều truy vấn, có 2 trường hợp riêng như sau:
  + k thay đổi và R cố định
  + R thay đổi và k cố định\
==> Cuối cùng, ta kết hợp 2 phương pháp trên để xử lý trường hợp cả R và k cùng thay đổi.

## 2. R cố định và k thay đổi.
- Tất cả các truy vấn trong Q có cùng R nhưng giá trị k khác nhau. Các láng giềng của một đối tượng là giống nhau cho tất cả các truy vấn, vì R là cố định. Do đó, số láng giềng kết tiếp (np(+)) của một đối tượng p là như nhau cho tất cả các truy vấn.

- Với một điểm truy vấn q, giá trị của số lượng neighbors trước (np(-)) của p tối đa là q.k - np(+).

## MICRO-CLUSTER BASED CONTINUOUS OUTLIER DETECTION
### 1. Tổng quan:
- **Mục tiêu:** Trong luồng dữ liệu với cửa sổ trượt (time-based hoặc count-based), phát hiện distance-based outliers: Một điểm p là outlier nếu số neighbors trong bán kính R là nhỏ hơn k.
- **Vấn đề thực tế:** Các phương pháp trước yêu cầu chạy range query trên toàn bộ tập active objects cho mỗi arrival --> Rất tốn tài nguyên tính toán.
- **Ý tưởng MCOD:** Duy trì các micro-clusters (vùng nhỏ chỉ chứa inliers). Nếu điểm nằm trong micro-cluster thì nó chắc chắn không phải outlier ==> Không phải xét trong event queue và không làm range query toàn bộ. Khi arrival chỉ phải xét:
  + Tập các điểm không thuộc cluster (PD) - gọi là candidate set, thường nhỏ nếu có nhiều cluster
  + Các micro-cluster có khả năng chứa neighbors (Các cluster cách điểm <= 3R/2).
- **Kết quả:** giảm mạnh số phép tính khoảng cách.

### 2. Các tham số và giả thiết:
- Tham số chính: Radius (R), số neighbors (k).
- Fixed assumptions:
  + micro-cluster radius = R/2
  + minimum clusster size = k + 1 (Nếu cluster có >= k + 1 điểm thì mọi điểm trong clusterr có >= k neighbors trong bán kính R).
  + Centers cố định sau khi tạo (đơn giản hóa online).
- Hỗ trợ: cả time-based và count-based sliding windows (mối điểm có arrival và expire).

### 3. Ký hiệu:
- MCi: micro-cluster thứ i:
  + mcc_i: center (vector DIM).
  + mcn_i: size (#members).
  + members[]: danh sách con trỏ/index đến điểm
- Imc: Tập points thuộc micro-cluster (inliers chắc chắn).
- PD: Tập points không thuộc cluster (candidate outliers).
- Mỗi point p lưu:
  + p.features.
  + p.arrival, p.expire.
  + p.mc (cluster id hoặc -1).
  + p.succ (succeeding neighbors count).
  + p.pred_list (k most recent preceding neighbors's expire times or ids).
  + p.Rmc (list của cluster ids có center cách p <= 3R/2).
  + p.is_outlier flag.
- Event Queue: (Min-heap) giữ events (p, p.ev) cho p ∈ PD. p.ev = min{expire(q) | q ∈ pred_list(p)}.

### 4. Bổ đề:
- Lemma 3: Nếu p thuộc một micro-cluster (Radius <= R/2 và size >= k + 1) --> p không phải outlier.
- Lemma 4: Khi xét neighbors của p, ta chỉ cần xem:
  + points ∈ PD
  + points trong micro-cluster có center cách p <= 3R/2. Nếu center cách p > 3R/2 thì mọi member cluster cách p > R (vì cluster radius = R/2) --> Không là neighbors.

- Kết luận: an toàn khi bỏ qua tất cả cluster centers > 3R/2, và không đưa members của Imc vào event-queue. 

### 5. Các bước thực hiện:
- **Bước 1:** Các đối tượng hết hạn được loại bỏ sau khi cập nhật bộ đếm `mcn` của các micro-cluster tương ứng (Nếu có). Sau đó, bước 2 và 3 được thực hiện cho mỗi đối tượng dữ liệu mới p, các đối tượng mới được xử lý theo thứ tự đến.
- **Bước 2:** Với mỗi đối tượng p, ta xác định (i) micro-cluster có tâm gần đối tượng đó nhất và (ii) tất cả các micro-cluster có tâm nằm trong phạm vi 3/2R. Nếu có xung đột (tức là hai tâm có khoảng cách bằng nhau), thì giải quyết tùy ý. Lưu ý rằng ta có thể sử dụng một cấu trúc đặc thù để lưu trữ các tâm micro-cluster, chẳng hạn như M-tree, để thực hiện bước này hiệu quả hơn.
- **Bước 3:**
  + Nếu khoảng cách từ p đến tâm gần nhất không lớn hơn R/2, thì:
    + (3a-i) đối tượng mới được gán vào micro-cluster tương ứng và giá trị của p.mc được cập nhật.
    + (3a-ii) Kích thước của micro-cluster tương ứng được tăng thêm 1.
    + (3a-iii) Giả sử MCi là micro-cluster mà đối tượng mới được thêm vào. Ta đánh giá khoảng cách giữa đối tượng mới và tất cả các đối tượng trong PD có chứa MCi trong danh sách Rmc của chúng, để kiểm tra:
      + (i) Liệu số lượng láng giềng kết tiếp của những đối tượng đó có cần tăng lên hay không?
      + (ii) Liệu có đối tượng nào trước đây được báo cáo là ngoại lai nhưng trở thành inlier không?
  + Ngược lại, nếu khoảng cách từ tâm gần nhất lớn hơn R/2, thì không có việc gán nào xảy ra và quá trình sau được áp dụng:
    + (3b-i) Với đối tượng mới p, không được gán vào bất kì micro-cluster nào, ta thực hiện một truy vấn phạm vi chỉ xem xét:
      + (i) các đối tượng trong PD
      + (ii) Các đổi tượng trong các micro-cluster mà tâm của chúng cách p không lớn hơn 3/2R (các micro-cluster liên quan này đã xác định ở trong Bước 2).
    + (3b-ii) Nếu số lượng láng giềng từ tập PD trong phạm vi R/2 vượt quá Ok(O >= 1.2) thì một micro-cluster mới được tạo ra, với một đối tượng mới làm tâm. Tất cả các đối tượng tương ứng được chuyển từ PD sang Imc. Tất cả đối tượng vẫn còn trong PD nhưng cách xa dưới 3/2R sẽ cập nhật danh sách Rmc của chúng với mã định danh của micro-cluster mới.
    + (3b-iii) Ngược lại, thuật toán dựa trên sự kiện được mô tả trong các phần trước được áp dụng (tức là tạo danh sách thời điểm hết hạn của các láng giềng của đối tượng mới và cập nhật số lượng láng giềng kế tiếp.). Các đối tượng trong p.Rmc chính là các micro-cluster có tâm cách xa không quá 3/2R.

- **Bước 4:** Nếu kích thước của một micro-cluster giảm xuống dưới k+1 thì micro-cluster sẽ bị giải tán, và các đối tượng trong đây nó được xử lý tương tự như trong 3b.
  + Kết thúc bước này, các ngoại lai bổ sung sẽ được báo cáo với sự hỗ trợ cảu hàng đợi sự kiện, vốn trong MCOD không bao gồm bất kì đối tượng nào p ∈ Imc. Ưu điểm chính so với các thuật toán trong các phần trước là số lượng phép tính khoảng cách giảm đáng kể.