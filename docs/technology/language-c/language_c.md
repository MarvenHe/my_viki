# C 语言知识

> 这里是记录C语言相关知识的地方。


### 结构体变量
结构体是 C 语言中最常用的构造类型之一，它允许我们将不同类型的数据组合在一起，形成一个有意义的整体。

#### 定义与声明
结构体的定义描述了一个数据的“模板”，而结构体变量则是根据这个模板创建的具体实例。

#### 应用举例
```c
// 定义一个结构体类型
struct Student {
    char name[50];
    int age;
    float score;
};
struct Student stu1 = {"Alice", 20, 95.5};
// 定义时，需要写struct关健字

typedef struct sysdat_t {
    uint8_t flag :1 ; // 定义为位域，对于仅需BOOL型的变量可以节约空间
    uint8_t pwr_flag :1 ;
    uint8_t score;
};
sysdat_t sysdat; // 声明结构体变量
// 定义时，无需写struct关健字，可直接定义
```


### 枚举变量
枚举类型用于定义一组具名的整数常量，它可以使代码更具可读性和可维护性。

#### 枚举的优点
- 代码可读性：使用 RED 比使用数字 0 更容易理解。
- 类型安全：虽然 C 语言的枚举本质上还是整数，但在逻辑上它限制了变量的取值范围。
- 方便调试：调试器通常能显示枚举常量的名称，而不是晦涩的数字。

#### 基本语法 & 应用举例
使用 enum 关键字来定义枚举类型。

```c
// 1) 使用 enum 关键字定义枚举类型
// 不指定值，数值按顺序增加。
enum Color {
    RED,    // 默认值为 0
    GREEN,  // 默认值为 1
    BLUE    // 默认值为 2
};
// 定义一个枚举变量
enum Color myColor = RED;

// 2) 使用typedef定义方式，typedef将enum Color整体重命名为Color，使其成为独立类型名。
// 也可以手动为枚举成员指定值。
typedef enum Status {
    DEVICE_RUNNING = 404,
    DEVICE_ERROR   = 500
};

// 直接以类型方式定义枚举变量
Status Server_Status = NOT_FOUND;

// 可读性高
if (Server_Status == DEVICE_RUNNING) { ... }

```
