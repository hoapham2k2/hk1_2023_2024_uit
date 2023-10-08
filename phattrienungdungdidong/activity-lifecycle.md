# Activity và Activity Lifecycle

## 1. Activity là gì

Lớp Activity là thành phần cơ bản của một ứng dụng Android. Nó cung cấp giao diện người dùng cho ứng dụng.
Thông thường các ứng dụng android đều sử dụng nhiều màn hình khác nhau, mỗi màn hình sẽ là một Activity. Ví dụ như ứng dụng Facebook, khi ta đăng nhập vào ứng dụng, màn hình hiển thị là màn hình chính, khi ta click vào một bài viết, màn hình sẽ chuyển sang màn hình chi tiết bài viết, khi ta click vào một ảnh, màn hình sẽ chuyển sang màn hình xem ảnh, khi ta click vào một link, màn hình sẽ chuyển sang màn hình trình duyệt web, ... Tất cả các màn hình này đều là các Activity khác nhau.

**main activity** là activity đầu tiên được khởi chạy khi ta mở ứng dụng. Nó có thể là màn hình chính của ứng dụng, hoặc là màn hình đăng nhập, hoặc là màn hình giới thiệu ứng dụng, ...

Để sử dụng một Activity, ta cần phải đăng ký nó trong file `AndroidManifest.xml` của ứng dụng.

### Cấu hình Activity trong file AndroidManifest.xml

Để đăng ký một Activity trong file `AndroidManifest.xml`, ta sử dụng thẻ `<activity>`. Ví dụ:

```xml
<manifest ... >
  <application ... >
      <activity android:name=".ExampleActivity" />
      ...
  </application ... >
  ...
</manifest >
```

Trong đó, thuộc tính `android:name` chỉ định tên của Activity. Tên của Activity có thể là tên đầy đủ (ví dụ: `com.example.ExampleActivity`) hoặc là tên ngắn gọn (ví dụ: `.ExampleActivity`). Nếu tên ngắn gọn, nó sẽ được tự động thêm vào package name của ứng dụng

Ngoài ra, ta có thể sử dụng các thuộc tính khác để cấu hình Activity. Ví dụ:

```xml
<activity android:name=".ExampleActivity"
          android:label="@string/example_label"
          android:theme="@style/Theme.AppCompat.Light" />
```

Trong đó:

- `android:label` chỉ định tên của Activity sẽ hiển thị trên thanh tiêu đề của Activity
- `android:theme` chỉ định theme sẽ được sử dụng cho Activity

## 2. Activity Lifecycle

Hình minh họa dưới đây mô tả các trạng thái của Activity và các lifecycle callback methods được gọi trong mỗi trạng thái:
![image](public/activity_lifecycle.png)

Khi user điều hướng ứng dụng (ví dụ: bằng cách click vào một button, hoặc click vào một item trong menu, ...) thì ứng dụng sẽ chuyển đổi giữa các Activity. Khi một Activity được khởi chạy, nó sẽ đi qua một chuỗi các trạng thái khác nhau. Chuỗi các trạng thái này được gọi là Activity Lifecycle.

Với **lifecyle callback methods**, ta có thể thực hiện các thao tác cần thiết khi Activity chuyển đổi giữa các trạng thái khác nhau. Ví dụ: khi Activity được khởi chạy, ta có thể khởi tạo các biến, tải dữ liệu, ...; khi Activity bị tạm dừng, ta có thể lưu trạng thái của Activity, ...; khi Activity bị hủy, ta có thể giải phóng bộ nhớ, ... Trong ReactJs thì các lifecycle callback methods được gọi là các lifecycle hooks (ví dụ: `componentDidMount`, `componentWillUnmount`, ...)

### Các trạng thái của Activity

Activity class cung cấp 6 **lifecycle callback methods** để ta có thể thực hiện các thao tác cần thiết khi Activity chuyển đổi giữa các trạng thái khác nhau. Các lifecycle callback methods này được gọi theo thứ tự như sau:

- `onCreate()`: được gọi khi Activity được khởi tạo.

- `onStart()`: được gọi khi Activity được hiển thị trên màn hình. 
- `onResume()`: được gọi khi Activity được hiển thị trên màn hình và người dùng có thể tương tác với Activity.
- `onPause()`: được gọi khi Activity bị tạm dừng.
- `onStop()`: được gọi khi Activity bị dừng.
- `onDestroy()`: được gọi khi Activity bị hủy.

### Các lifecycle callback methods

#### onCreate()

`onCreate()` được gọi khi Activity được khởi tạo. Trong lifecycle callback method này, ta thường thực hiện các thao tác khởi tạo Activity, ví dụ: khởi tạo các biến, tải dữ liệu, ...

```java
@Override
protected void onCreate(Bundle savedInstanceState) {
    super.onCreate(savedInstanceState);
    setContentView(R.layout.activity_main);
    // ...
}
```

#### onStart()

`onStart()` được gọi khi Activity được hiển thị trên màn hình. Trong lifecycle callback method này, ta thường thực hiện các thao tác cần thiết để Activity có thể hiển thị trên màn hình, ví dụ: khởi tạo các biến, tải dữ liệu, ...

```java

@Override
protected void onStart() {
    super.onStart();
    // ...
}
```

#### onResume()

`onResume()` được gọi khi Activity được hiển thị trên màn hình và người dùng có thể tương tác với Activity. Trong lifecycle callback method này, ta thường thực hiện các thao tác cần thiết để Activity có thể hiển thị trên màn hình và người dùng có thể tương tác với Activity, ví dụ: khởi tạo các biến, tải dữ liệu, ...

```java

@Override
protected void onResume() {
    super.onResume();
    // ...
}
```

#### onPause()


`onPause()` được gọi khi Activity bị tạm dừng. Trong lifecycle callback method này, ta thường thực hiện các thao tác cần thiết để Activity bị tạm dừng, ví dụ: lưu trạng thái của Activity, ...

```java

@Override
protected void onPause() {
    super.onPause();
    // ...
}
```

#### onStop()


`onStop()` được gọi khi Activity bị dừng. Trong lifecycle callback method này, ta thường thực hiện các thao tác cần thiết để Activity bị dừng, ví dụ: lưu trạng thái của Activity, ...

```java

@Override
protected void onStop() {
    super.onStop();
    // ...
}
```

#### onDestroy()


`onDestroy()` được gọi khi Activity bị hủy. Trong lifecycle callback method này, ta thường thực hiện các thao tác cần thiết để Activity bị hủy, ví dụ: giải phóng bộ nhớ, ...

```java

@Override
protected void onDestroy() {
    super.onDestroy();
    // ...
}
```
