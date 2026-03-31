# C 语言知识

> 这里是记录C语言相关知识的地方。


### 📚结构体变量
结构体是 C 语言中最常用的构造类型之一，它允许我们将不同类型的数据组合在一起，形成一个有意义的整体。

#### 定义与声明
结构体的定义描述了一个数据的“模板”，而结构体变量则是根据这个模板创建的具体实例。
通常，结构体在.h文件中声明，然后在.c文件中定义，
如果需要在其它的.c文件中使用本结构体变量，则需要在.h文件中定义为外部变量。

#### 应用举例 1
```c
struct sysdat_t {
    uint8_t flag :1 ; // 定义为位域，对于仅需BOOL型的变量可以节约空间
    uint8_t pwr_flag :1 ;
    uint8_t score;
    uint8_t name[10];
};
extern struct sysdat_t sysdat; //声明为外部变量以供其它.c文件使用

struct sysdat_t sysdat = {
    .flag = 0;
    .score = 0;
};
// 定义时，需要写struct关健字
```

#### 应用举例 2
```c
// .h定义一个结构体类型
typedef struct sysdat_t {
    uint8_t flag :1 ; // 定义为位域，对于仅需BOOL型的变量可以节约空间
    uint8_t pwr_flag :1 ;
    uint8_t score;
    uint8_t name[10];
};
extern sysdat_t sysdat; //声明为外部变量以供其它.c文件使用

// .c文件中声明结构体变量
sysdat_t sysdat; // 声明结构体变量 无需写struct关健字，可直接定义

sysdat.score = 10; // 直接使用 赋值操作
```

#### 结构体指针变量定义
```c
// 定义一个结构体指针变量，它可以指向已经声明过的结构体变量 sysdat_t 的地址
// 刚定义的时候它是没有地址的，不能使用，使用前需要给它赋值已经声明的结构体变量的地址。
sysdat_t* sysdat_user;
sysdat_user = sysdat; // 给指针赋值 指向变量sysdat

sysdat_t* sysdat_user = sysdat; // 定义时直接给指针赋值 指向变量sysdat

sysdat_user->score = 15;  // 使用指针对结构体成员进行赋值操作

```

#### 在 函数传参数时 定义结构体指针变量
```c
// 这其中的 sysdat_t* 表示为结构体指针变量，指向传入的结构体地址
// u_sysdat为函数内部的指针
void function ( sysdat_t* u_sysdat ){
    u_sysdat->score = 15;  // 对结构体成员进行赋值操作
    if(u_sysdat->score == 15){...} // 读取结构体成员数值 
}

// 由于函数接收的是指针变量
// 所以在调用函数时，需要把结构体变量的地址传递给函数
function(&sysdat);

// 由于函数接收的是指针变量
// 也可以直接把指针变量 直接传递给函数
function(sysdat_user); 
```

### 📚枚举变量
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
// 定义一个枚举变量 并初始化
enum Color myColor = RED;
extern Color myColor; //.h文件中声明为外部变量以供其它.c文件使用

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


✅ :white_check_mark: 完成 / 正确
❌ :x: 错误 / 失败
⚠️ :warning: 警告
💡 :bulb: 提示 / 想法
✨ :sparkles: 新功能 / 亮点
🚀 :rocket: 发布 / 快速
🔥 :fire: 热门 / 重要
❗ :exclamation: 重要提醒
❓ :question: 问题 / 疑问

开发与操作
📝 :memo: 笔记 / 文档
🔗 :link: 链接
📌 :pushpin: 固定 / 置顶
📊 :bar_chart: 数据 / 统计
🐛 :bug: 缺陷 / 问题
🔧 :wrench: 工具 / 设置
⚙️ :gear: 配置
📦 :package: 打包 / 依赖
⬇️ :arrow_down: 下载
⬆️ :arrow_up: 上传

内容与分类
📚 :books: 书籍 / 文档集
💻 :computer: 电脑 / 技术
📱 :iphone: 移动端
🧩 :jigsaw: 插件 / 模块
🗑️ :wastebasket: 删除
🔒 :lock: 安全 / 锁定
🔓 :unlock: 开放 / 解锁

