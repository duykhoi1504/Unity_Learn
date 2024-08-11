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


# ROTATION
## Xoay đều đặng theo 1 hướng nào đó
```CSharp
 this.transform.Rotate(0,0,5*Time.deltaTime);
```
## set thẳng 1 góc quây về 1 hướng
```CSharp
this.transform.eulerAngles =new Vector3(90,0,0);
```
## liên tục quây về hướng của 1 vật thể khác    
```CSharp
this.transform.LookAt(_target);
```
## Muốn vật thể từ từ xoay đến vị trí chính xác
```CSharp
   Quaternion _targetAngle=new Quaternion();
        _targetAngle.eulerAngles=new Vector3(0,90,0);
        this.transform.rotation=Quaternion.RotateTowards(this.transform.rotation, _targetAngle, 5);
```
## Xoay enemy từ từ theo player khóa trục y
```Csharp
void FaceToTarget(){
        // transform.LookAt(new Vector3(target.transform.position.x,0, target.transform.position.z));
        Vector3 direction = (target.position-transform.position).normalized;
        Debug.DrawRay(transform.position,direction,Color.green);
        Quaternion lookRotation=Quaternion.LookRotation(new Vector3(direction.x,0,direction.z));
        transform.rotation=Quaternion.Slerp(transform.rotation,lookRotation,Time.deltaTime*turnSpeed);
    }
```

## LookRotation(hit.normal)
```Csharp
Instantiate(hitEffect, hit.point, Quaternion.LookRotation(hit.normal));
```
Vector hit.normal đại diện cho pháp tuyến bề mặt tại điểm va chạm. Hàm LookRotation() sử dụng véc-tơ pháp tuyến này để xác định góc quay của đối tượng hitEffect, sao cho nó sẽ được định hướng vuông góc với bề mặt nơi xảy ra va chạm.


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

# Scroll chuot
 if(Input.GetAxis("Mouse ScrollWheel")<0){}

# Input GET MOUSE
Input.GetMouseButtonDown("0"): chuột trái
Input.GetMouseButtonDown("1"):  chuột phải
Input.GetButtonDown("Fire1"): chuột trái
Input.GetButtonDown("Fire2"): chuột phải

# Cursor
``` csharp
Cursor.lockState=CursorLockMode.None;    
     Cursor.visible=true;
```
Cursor.visible=true: làm cho con trỏ chuột hiển thị trên màn hình.
CursorLockMode.None:cho phép con trỏ chuột di chuyển tự do trên màn hình mà không có bất kỳ hạn chế nào.
CursorLockMode.Confined:con trỏ chuột được giới hạn trong cửa sổ trò chơi hoặc ứng dụng, nhưng vẫn có thể di chuyển tự 
 bên trong cửa sổ đó.
CursorLockMode.Locked:Chế độ này hoàn toàn khóa con trỏ chuột, ẩn nó khỏi tầm nhìn và hạn chế sự di chuyển của nó trong cửa sổ ứng dụng hoặc trò chơi. Con trỏ chuột không thể rời khỏi ranh giới của cửa sổ.


# OnDrawGizmos()
để vẽ vòng trong xung quanh enemy
```Csharp
 private void OnDrawGizmos() {
           Gizmos.color = Color.red;
        Gizmos.DrawWireSphere(transform.position, chaseRange);
 }
 ```


# Dictionary 
là một cấu trúc dữ liệu. để tìm kiếm và truy cập dữ liệu dựa trên khóa.
```CSharp
public class Example : MonoBehaviour
{
    private Dictionary<string, int> scoreDictionary;
 
    private void Start()
    {
        scoreDictionary = new Dictionary<string, int>();
        // Thêm các cặp khóa-giá trị vào Dictionary
        scoreDictionary.Add("Player1", 100);
        scoreDictionary.Add("Player2", 200);
        scoreDictionary.Add("Player3", 150);
        int score = scoreDictionary["Player2"];
        Debug.Log("Player2's score: " + score);
        if (scoreDictionary.ContainsKey("Player3"))
        {
            Debug.Log("Player3's score exists!");
        }
 
        // Lặp qua tất cả các cặp khóa-giá trị trong Dictionary
        foreach (KeyValuePair<string, int> kvp in scoreDictionary)
        {
            Debug.Log("Key: " + kvp.Key + ", Value: " + kvp.Value);
        }
 
        // Xóa một cặp khóa-giá trị khỏi Dictionary
        scoreDictionary.Remove("Player1");
    }
}
```

# Particle System :"Simulation Space"

>1.'<Local>': Khi Simulation Space được đặt thành Local, các hạt sẽ được mô phỏng trong không gian cục bộ của đối tượng chứa Particle System. Điều này có nghĩa là nếu bạn di chuyển đối tượng chứa Particle System, các hạt sẽ di chuyển theo cùng với nó.
 
>2.'<World>': Khi Simulation Space được đặt thành World, các hạt sẽ được mô phỏng trong không gian toàn cầu của scene. Việc di chuyển đối tượng chứa Particle System không ảnh hưởng đến vị trí của các hạt.

# Unity Editor
Khi render thì những mã code có dùng Unity Editor sẽ ko được tích hợp vào trong game

>một cách thông thường để xử lý việc tách Unity Editor liên quan khỏi ứng dụng cuối cùng là tạo một thư mục riêng gọi là "Editor" trong dự án Unity của bạn. Bạn có thể đặt các script chứa mã nguồn liên quan đến Unity Editor vào thư mục này.

# ToolTip
[Tooltip] trong Unity. Thuộc tính này được sử dụng để hiển thị thông báo gợi ý (tooltip) khi di chuột qua một trường dữ liệu hoặc một thuộc tính trên trình biên dịch Unity.

```CS
    [Tooltip("Adds amount to EnemyHP when thay dies.")]
    [SerializeField] int difficultyRamp = 1;

```

# [RequireComponent(typeof(Enemy))]
bạn đang đảm bảo rằng khi nào script này được thêm vào một đối tượng game, thành phần Enemy sẽ tự động được thêm vào nếu nó chưa tồn tại
```CS
[RequireComponent(typeof(Enemy))]
public class SomeScript : MonoBehaviour
{
    // ...
}
```
# activeSelf & activeInHierarchy
## activeSelf
 chỉ kiểm tra trạng thái kích hoạt của đối tượng cụ thể
 ## activeInHierarchy
  kiểm tra trạng thái kích hoạt của đối tượng cũng như trạng thái của các đối tượng cha hoặc con của nó.

# OnMouseOver

tương tác cới collider khi di chuột vào

```CSharp
 void OnMouseOver() {
        Debug.Log(this.transform.name);
    }
void OnMouseOver() {
       
       if (Input.GetMouseButtonDown(0)) {
         Debug.Log(this.transform.name);
       }
    }
```

# Mathf.RoundToInt
 là một phương thức trong thư viện Mathf của Unity được sử dụng để làm tròn một số thực về số nguyên gần nhất. Nó làm tròn số thực đến số nguyên gần nhất và trả về kết quả dưới dạng một số nguyên.

Ví dụ, nếu bạn có một số thực là 3.6, sau khi áp dụng Mathf.RoundToInt(3.6), bạn sẽ nhận được kết quả là 4.



# ExecuteAlways
 trên một script, script đó sẽ được thực thi cả trong Editor Mode và Play Mode. Điều này khác với [ExecuteInEditMode] chỉ thực thi trong Editor Mode.
```CSharp
[ExecuteAlways]
public class ExampleClass : MonoBehaviour
{
    void Start()
    {
        if (Application.IsPlaying(gameObject))
        {
            // Play logic
        }
        else
        {
            // Editor logic
        }
    }
}
``` 
# Post Processing
để tạo những hậu kỳ màn lọc cho game

tạo Game Object gắn post volumn -> tạo layer cao nhất

gắn component post layer cho camera -> gắn layer cho post layer(COMPONENT)

# SingleTon for soundfx
để nhạc không chạy lại khi reset màn chơi thì dùng singleton
```CS
void Awake()
    {
        int numMusicPlayer = FindObjectsOfType<MusicPlayer>().Length;
        if (numMusicPlayer > 1)
        {
            Destroy(this.gameObject);
        }
        else
        {
            DontDestroyOnLoad(gameObject);
        }
    }
```

# SceneManager
```cs
int currentSceneIndex =SceneManager.GetActiveScene().buildIndex;
        //GetActiveScene(): Hàm này trả về Scene hiện tại mà người chơi đang chơi trong game
        //buildIndex:  trả về chỉ số (index) của Scene 
        SceneManager.LoadScene(currentSceneIndex);
    
```

# Action<int,Vector2>
* Action<int,Vector2> là một delegate (một kiểu dữ liệu đặc biệt) trong C#.
* Nó định nghĩa một hàm mà có thể nhận hai tham số: một int và một Vector2.
* Ví dụ, bạn có thể sử dụng Action<int,Vector2> để định nghĩa một sự kiện "OnDamageTaken" trong một script, và các script khác có thể đăng ký với sự kiện này để xử lý khi một đối tượng chịu thiệt hại.
```CSharp
public class Enemy : MonoBehaviour
{
    public Action<int, Vector2> OnDamageTaken;

    public void TakeDamage(int damage, Vector2 hitPosition)
    {
        // Xử lý logic khi đối tượng chịu thiệt hại
        OnDamageTaken?.Invoke(damage, hitPosition);
    }
}
```
# Dictionary<TKey, TValue>
* Dictionary<TKey, TValue> là một collection trong C# cho phép lưu trữ các cặp key-value.
* Nó rất hữu ích khi bạn cần lưu trữ và truy xuất dữ liệu nhanh chóng dựa trên một khóa (key).
* Ví dụ, bạn có thể sử dụng Dictionary<string, GameObject> để lưu trữ các GameObject trong game dựa trên tên của chúng.
```CSharp
public class GameManager : MonoBehaviour
{
    private Dictionary<string, GameObject> gameObjects = new Dictionary<string, GameObject>();

    public void RegisterGameObject(string name, GameObject obj)
    {
        gameObjects[name] = obj;
    }

    public GameObject GetGameObject(string name)
    {
        if (gameObjects.TryGetValue(name, out var obj))
            return obj;
        else
            return null;
    }
}
```
# List<T>
* List<T> là một collection trong C# cho phép lưu trữ các phần tử của cùng một kiểu dữ liệu.
* Nó rất hữu ích khi bạn cần lưu trữ và thao tác với một danh sách các đối tượng.
* Ví dụ, bạn có thể sử dụng List<Enemy> để lưu trữ tất cả các đối tượng Enemy trong game.
```CSharp
public class GameManager : MonoBehaviour
{
    private List<Enemy> enemies = new List<Enemy>();

    public void AddEnemy(Enemy enemy)
    {
        enemies.Add(enemy);
    }

    public void RemoveEnemy(Enemy enemy)
    {
        enemies.Remove(enemy);
    }

    public void UpdateEnemies()
    {
        foreach (var enemy in enemies)
        {
            enemy.Update();
        }
    }
}
```
