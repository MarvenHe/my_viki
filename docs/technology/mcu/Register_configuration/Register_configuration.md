# 寄存器配置 Register configuration

平常对于MCU或者一些器件的寄存器进行配置时，如果直接使用寄存器的数值进行配置比较麻烦...<br>
每次都需要看手册，并且查看寄存器每个位的功能。<br>


这里面说明一些使用结构体 + 枚举变量进行寄存器配置的方法<br>

通常 结构体声明 和枚举定义在.h头文件中，<br>
配置操作在.c文件中进行。<br>


### 📌 常规操作
使用结构体 映射寄存器，<br>
使用枚举变量预先定义好与寄存器对应的参数。<br>
定义时，只需要按结构体与枚举的内容进行参数配置即可完成。<br>
最后把配置好的结构体变量写入寄存器。<br>
#### 使用方法（代码示例）
```c
// 1.定义 OSCCON 寄存器的地址 
// 通常MCU已经定义好了寄存器名称，不需要用户另外定义

// 通常器件未定义寄存器名称，只给出寄存器地址 需要用户定义
#define OSCCON (0x14)

// 2. 
// 查看手册，根据OSCCON寄存器 定义枚举
// 这样做的好处是代码自解释，不需要去查手册就能知道每个值代表什么
typedef enum {
    IRCF_32KHZ        = 0b000, // 32kHz 低频内部振荡器
    IRCF_FOSC_DIV_64  = 0b001, // Fosc / 64
    IRCF_FOSC_DIV_32  = 0b010, // Fosc / 32
    IRCF_FOSC_DIV_16  = 0b011, // Fosc / 16
    IRCF_FOSC_DIV_8   = 0b100, // Fosc / 8
    IRCF_FOSC_DIV_4   = 0b101, // Fosc / 4 (默认)
    IRCF_FOSC_DIV_2   = 0b110, // Fosc / 2
    IRCF_FOSC_DIV_0   = 0b111  // Fosc (全速)
} OSCCON_IRCF_t;


// 3. 
// 定义 OSCCON 寄存器的位结构体
// 用户配置时需使用
typedef struct {
    uint8_t reserved0  : 1; // Bit 0: 未用
    uint8_t SWDTEN     : 1; // Bit 1: 软件看门狗使能
    uint8_t reserved2  : 2; // Bit 2-3: 未用
    uint8_t IRCF       : 3; // Bit 4-6: 频率选择 (3位)
    uint8_t reserved7  : 1; // Bit 7: 未用
} OSCCON_Bits_t;

// 4. 联合体定义
typedef union {
    uint8_t all;
    OSCCON_Bits_t bits;
} OSCCON_Union_t;


// 5. 函数实现
uint8_t OSCCON_INIT(void) {
    OSCCON_Union_t temp_union = {.all = 0;} // 使用联合体作为临时变量
    
    // 配置位域
    temp_union.bits.SWDTEN = 0;
    temp_union.bits.IRCF = IRCF_FOSC_DIV_4;
    
    OSCCON = temp_union.all; // 一次性写入物理寄存器

    temp_union.all = OSCCON; // 重新读取物理寄存器的值到联合体

    // 检查读取的值是否符合预期
    if(temp_union.bits.IRCF == IRCF_FOSC_DIV_4){
        return 0; // 成功
    }
    else {
        return 1; // 失败
    }
}
```


  
### 📌 简化操作，把结构体装进联合体中
C语言允许直接在 union 内部定义 struct，这就是匿名结构体<br>
这样写不仅代码更紧凑，而且因为结构体没有名字，可以直接用 .bits 来访问成员，逻辑上非常清晰。<br>

#### 这样写的好处
代码更整洁。<br>
不需要先定义一个 OSCCON_Bits_t，再定义一个 OSCCON_Union_t，现在只有一个类型。<br>
虽然结构体没有名字，但你在联合体里给了它一个成员名 bits，所以用法完全一样。<br>

#### 使用方法（代码示例）
H文件 对联合体&结构体进行声明。<br>
```c
// 查看手册，根据OSCCON寄存器 定义枚举
// 这样做的好处是代码自解释，不需要去查手册就能知道每个值代表什么
typedef enum {
    IRCF_32KHZ        = 0b000, // 32kHz 低频内部振荡器
    IRCF_FOSC_DIV_64  = 0b001, // Fosc / 64
    IRCF_FOSC_DIV_32  = 0b010, // Fosc / 32
    IRCF_FOSC_DIV_16  = 0b011, // Fosc / 16
    IRCF_FOSC_DIV_8   = 0b100, // Fosc / 8
    IRCF_FOSC_DIV_4   = 0b101, // Fosc / 4 (默认)
    IRCF_FOSC_DIV_2   = 0b110, // Fosc / 2
    IRCF_FOSC_DIV_0   = 0b111  // Fosc (全速)
} OSCCON_IRCF_t;

typedef union {
    uint8_t all;  // 用于整体读写（例如：union_var.all = 0xFF）
    
    // 直接在联合体内部定义结构体
    struct {
        uint8_t reserved0  : 1; // Bit 0
        uint8_t SWDTEN     : 1; // Bit 1
        uint8_t reserved2  : 2; // Bit 2-3
        uint8_t IRCF       : 3; // Bit 4-6
        uint8_t reserved7  : 1; // Bit 7
    }; // 注意这里没有名字，也没有分号后的名字
} OSCCON_Union_t; // 联合体直接叫 OSCCON_Union_t 即可
```

C文件 在函数中使用。<br>
```c
uint8_t OSCCON_INIT(void) {
    OSCCON_Union_t temp_union = {.all = 0;} // 使用联合体作为临时变量
    
    // ✅ 配置位域
    temp_union.SWDTEN = 0;
    temp_union.IRCF = IRCF_FOSC_DIV_4;
    
    OSCCON = temp_union.all; // 一次性写入物理寄存器

    temp_union.all = OSCCON; // 重新读取物理寄存器的值到联合体

    // 检查读取的值是否符合预期
    if(temp_union.IRCF == IRCF_FOSC_DIV_4){
        return 0; // 成功
    }
    else {
        return 1; // 失败
    }
}
```
<br>
实际操作中会遇到同一个功能，会有多个寄存器需要配置的情况。<br>
例如：ADC芯片配置，会涉及采样时钟、ADC参考电压、PGA倍数等参数。<br>
test!!<br>
test2!!<br>
test3!!<br>

