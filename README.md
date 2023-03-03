# Gold-Price-Prediction
Thành viên trong nhóm 11:
1. Mai Chí Trung - 20280109
2. Mai Chí Thanh - 20280084
3. Nguyễn Quốc HUy - 20280045
4. Đặng Ngọc Hưng - 20280039
-----------------------------

  ### Bước 1: Nhập các thư viện cần thiết
Sử dụng Pandas để nhập dữ liệu, Matplotlib và Seaborn để trực quan hóa dữ liệu, sklearn cho các thuật toán, tran_test_split để chia tập dữ liệu trong tập kiểm tra và traing set, accuracy_score để đánh giá mô hình.
![image](https://user-images.githubusercontent.com/125122891/222760649-2bce7413-70ad-40a9-806b-957efbddcaa4.png)

  ### Bước 2: Tải bộ dữ liệu 
Lấy dữ liệu từ trang: https://www.nasdaq.com/marketactivity/commodities/gc%3Acmx
![image](https://user-images.githubusercontent.com/125122891/222761474-248f5352-ee4c-42cf-8e0a-de857b73fc90.png)

Bộ dữ liệu này bao gồm giá vàng theo thời gian thực tính bằng USD từ năm 2012 đến năm 2022.
                   Date - Ngày ghi giá
                   Close - Ngày đóng giá vàng tính bằng USD
                   Volume - Tổng lượng mua và bán của hàng hoá vàng
                   Open - Giá mở của vàng vào ngày cụ thể đó
                   High - Giá vàng cao nhất của ngày cụ thể đó
                   Low - Giá vàng thấp nhất vào ngày cụ thể đó.
![image](https://user-images.githubusercontent.com/125122891/222761714-9321825e-c60d-4692-833c-cc09245a6d67.png)
![image](https://user-images.githubusercontent.com/125122891/222761749-4ea65489-5a0f-464d-a94f-bb2cf9aaae35.png)

Đọc dữ liệu vàng hàng ngày trong 10 năm qua và lưu trữ nó trong df. Xóa các cột không liên quan 
![image](https://user-images.githubusercontent.com/125122891/222761784-1eeb7a3c-160f-4b47-9e44-62219126ba2c.png)
 
 ### Bước 3: Đánh giá thống kê thông tin
![image](https://user-images.githubusercontent.com/125122891/222761834-4ef9aa80-8cb9-4ed9-8e36-121eb9c2b512.png)
Các thuộc tính có kiểu dữ liệu phù hợp để phân tích, cột Date đã có kiểu Datetime
![image](https://user-images.githubusercontent.com/125122891/222761874-562d75b5-e618-4a5c-8ed8-dcb0af91cb1b.png)
  Kích thước của dữ liệu:
![image](https://user-images.githubusercontent.com/125122891/222761913-80d25cca-4c43-4649-83cc-ee4df0238c84.png)
  
  Dữ liệu có missing value nên phải xử lý lại dữ liệu
![image](https://user-images.githubusercontent.com/125122891/222761963-9c072ca6-e0b3-41a4-a3d7-32492e65b0e8.png)
Sau khi xử lý missing value chúng ta loại bỏ đi 39 hàng trong bộ dữ liệu. 
           Do 39 dòng nhỏ so với số lượng hơn 2000 dòng trong bộ dữ liệu nên sau khi loại bỏ 39 dòng, bộ dữ liệu vẫn còn đủ tốt để phân tích và train model.
  
  ### Bước 4:   Trực quan hóa dữ liệu
            Sử dụng hàm pairplot, heatmap để tìm kiếm các biến có tương quan mạnh với giá vàng
            ![image](https://user-images.githubusercontent.com/125122891/222762136-c6f50d81-8e4c-45b1-970b-e9b405aa13c6.png)
            ![image](https://user-images.githubusercontent.com/125122891/222762166-72dccbb0-c603-413e-b24d-5fbd79f24943.png)

              Nhìn vào biểu đồ trên ta thấy các biến Close/Last, Open, High, Low có tương quan với nhau
               Ngoài ra có thể sử dụng heatmap để tìm tương quan giữa các biến 
![image](https://user-images.githubusercontent.com/125122891/222762217-4820a3e8-23fa-48e8-9496-5636f126050a.png)
Qua biểu đồ trên cho thấy các biến Close/Last, Open, High, Low có tương quan mạnh với nhau
  ### Bước 5: Features engineering and selection
Sử dụng tính năng tương quan để train model
![image](https://user-images.githubusercontent.com/125122891/222762306-d2d2fb89-9e69-446d-9cc2-55774fa4578b.png)
Sử dụng MinMaxScaler của sklearn để chuẩn hóa lại dữ liệu trong khoảng từ 0 đến 1
![image](https://user-images.githubusercontent.com/125122891/222762371-68c4f6c3-ec69-4522-8add-d0cb2be236ce.png)
            
Phía dưới là dữ liệu sau khi biến đổi:
![image](https://user-images.githubusercontent.com/125122891/222762409-bb50b7d1-153b-4871-b8c3-40f468c525d2.png)
 So sánh dữ liệu trước và sau khi biến đổi
![image](https://user-images.githubusercontent.com/125122891/222762464-d38c6660-2de6-49be-8532-ca1c04b78c8e.png)
![image](https://user-images.githubusercontent.com/125122891/222762487-e63a65e5-ed63-4823-ac1d-cd92f86d2264.png)
![image](https://user-images.githubusercontent.com/125122891/222762506-bdad4c05-1a6f-4bdc-b5e4-e5c1eb50190f.png)
  
  ### Bước 6: Model creation and training
Tiếp theo tách dữ liệu để train model theo kích thước 8:2
![image](https://user-images.githubusercontent.com/125122891/222762568-c2ea6f5b-54c4-4bc3-837d-00179808a20e.png)
![image](https://user-images.githubusercontent.com/125122891/222762596-acf8112d-52ae-4819-94c1-db9933f7c18d.png)
![image](https://user-images.githubusercontent.com/125122891/222762662-24192336-20ee-4f82-b496-4007e805b841.png)
![image](https://user-images.githubusercontent.com/125122891/222762667-e092a2df-260c-4469-a28b-51d80110afab.png)
## ĐÁNH GIÁ MÔ HÌNH
![image](https://user-images.githubusercontent.com/125122891/222762811-5acf2d95-c748-4d98-ad36-15ac1d038c8a.png)

## MÔ HÌNH ANN:

- 3 hidden layers
- 40 Neuron node on each layer
- Relu activation function

![image](https://user-images.githubusercontent.com/125122891/222762855-24e99dc3-6bc8-4431-b0ab-e93c95f02c73.png)

Mô hình sẽ biên dịch với:
- Chức năng tối ưu hóa Adam
- Với hàm mất lỗi bình phương trung bình
- Tiến trình training với: 
- 100 Epochs
- 50 rows of batch size

![image](https://user-images.githubusercontent.com/125122891/222763009-eee61e2f-eb18-4e41-9427-f64b791ebce0.png)
![image](https://user-images.githubusercontent.com/125122891/222763070-5a248643-397c-4087-9e1c-e336897cd429.png)

## DecisionTreeRegressor:
Sử dụng mô hình DecisionTree Regressor để dự đoán với tham số mặc định
![image](https://user-images.githubusercontent.com/125122891/222763265-d6c2b60a-7551-4a38-843b-b78524a36d52.png)
![image](https://user-images.githubusercontent.com/125122891/222763344-7f1516cd-8207-4176-b2e4-9169d61ec5c5.png)

## RandomForest:
Random Forest là một thuật toán học có giám sát. Nó tạo ra một khu rừng và biến nó thành ngẫu nhiên theo cách nào đó. Các rừng mà nó xây dựng, là một tập hợp các Cây quyết định, phần lớn thời gian được huấn luyện bằng phương pháp “đóng gói”. Các ý tưởng chung của phương pháp đóng gói là sự kết hợp của các mô hình học tập sẽ làm tăng kết quả tổng thể.Các khu rừng quyết định ngẫu nhiên sửa lỗi cho các cây quyết định có thói quen khớp quá mức với tập huấn luyện của chúng.Tôi đã sử dụng hai tham số n_estimators=50 (giá trị mặc định =10), số lượng cây trong rừng. và random_state=0, random_state là hạt giống được sử dụng bởi trình tạo số ngẫu nhiên.
             Trong phần này sẽ chỉnh 3 thông số của RamdomForest là n_estimators, max_features, max_depth
![image](https://user-images.githubusercontent.com/125122891/222763477-4efd5ec0-6d30-4257-9bfc-77510634d018.png)
![image](https://user-images.githubusercontent.com/125122891/222763505-715ab5b5-77fc-4193-807b-aae6c24c0eea.png)
Sau khi áp dụng random forest với n_estimators = 100, đạt được kết quả như sau:
![image](https://user-images.githubusercontent.com/125122891/222763556-f5aca2df-da8b-4ef5-8229-2f8209a4d06c.png)

## SVR:
Mô hình được tạo ra bởi Support Vector Regression chỉ phụ thuộc vào một tập con của dữ liệu huấn luyện, bởi vì hàm chi phí để xây dựng mô hình bỏ qua mọi dữ liệu huấn luyện gần với dự đoán của mô hình.
Sử dụng SVR với (kernel=’linear’)
![image](https://user-images.githubusercontent.com/125122891/222763631-c5d758d0-d505-40f4-9c1f-399669c889f3.png)
![image](https://user-images.githubusercontent.com/125122891/222763651-3012aee6-71a4-42dc-a160-8186556193f3.png)
![image](https://user-images.githubusercontent.com/125122891/222763677-956801d3-bab9-470b-9089-a1df3dd415b6.png)
