# BroadcastMessage
là một phương thức của GameObject để gửi một thông điệp đến tất cả các thành phần (Components) được gắn trên chính GameObject đó, hoặc các GameObject con của nó.

## Ưu điểm:
Linh hoạt: BroadcastMessage() cho phép gửi thông điệp đến tất cả các thành phần (Components) được gắn trên GameObject hoặc các GameObject con, mà không cần phải tham chiếu trực tiếp đến từng thành phần. Điều này giúp mã code trở nên linh hoạt và dễ bảo trì hơn.
Tách biệt: Sử dụng BroadcastMessage() giúp tách biệt logic xử lý tổn thương (damage handling) khỏi các thành phần khác, như AI. Điều này làm cho mã code trở nên rõ ràng và dễ hiểu hơn.

## Nhược điểm:
Không kiểm soát: BroadcastMessage() gửi thông điệp đến tất cả các thành phần, ngay cả khi chúng không cần hoặc không mong muốn nhận thông điệp đó. Điều này có thể dẫn đến hiệu suất giảm sút và lỗi không mong muốn.
Khó debug: Khi sử dụng BroadcastMessage(), việc debug và xác định xem thông điệp đang được gửi đến đâu có thể trở nên khó khăn hơn.

# Sử dụng GetComponent<EnemyAI>().OnDamageTaken():

 ## Ưu điểm:
Kiểm soát: Bằng cách gọi trực tiếp phương thức OnDamageTaken() trên thành phần EnemyAI, bạn có thể kiểm soát chặt chẽ hơn việc xử lý tổn thương.
Dễ debug: Khi sử dụng phương pháp này, việc debug trở nên dễ dàng hơn vì bạn biết chính xác thông điệp đang được gửi đến đâu.

## Nhược điểm:
Gắn chặt: Phương pháp này gắn chặt logic xử lý tổn thương với thành phần EnemyAI, làm giảm tính linh hoạt và khả năng tái sử dụng của mã code.
Không linh hoạt: Nếu bạn muốn thêm các thành phần khác xử lý tổn thương, bạn sẽ phải sửa đổi mã code ở nhiều nơi.
# TextMeshPro
 ##  TextMeshProGUI
cho phép bạn sử dụng các tính năng nâng cao của TextMeshPro
 ##  TextMeshPro
không tích hợp trực tiếp với hệ thống UI, vì vậy nó thường được sử dụng cho các văn bản trong thế giới 3D.


# [System.Serializable] 
được sử dụng để đánh dấu một class có thể được serialized, nghĩa là có thể lưu trữ và tải lại dữ liệu của object này.
    cho phép các trường của class được hiển thị trong Unity Inspector,


## code mẫu  
```csharp
 [SerializeField] AmmoSlot[] ammoSlot;
    [System.Serializable]
    private class AmmoSlot
    {
        public AmmoType ammoType;
        public int ammoAmount;
    }
```
