### ⚙️ 方案一：Apifox IDEA 插件——最省心的自动化方式

这是官方主推，也是效率最高、体验最好的方式。

1. **安装插件**：在 IntelliJ IDEA 插件市场搜索 `Apifox Helper` 并安装。
2. **获取令牌**：在 Apifox Web 端或客户端，点击头像 ->【账号设置】->【API 访问令牌】->【新建令牌】，复制生成的令牌。
3. **配置插件**：在 IDEA 设置中找到 `Apifox Helper`，粘贴刚才的令牌并测试，成功后保存。
4. **一键同步**：在代码文件内右键选择 `Upload to Apifox`，或在整个项目根目录右键选择 `Upload to Apifox` 实现一键同步。
5. **查看文档**：打开 Apifox 项目，点击右上角刷新按钮，你所有写好的接口文档就已经自动同步在 Apifox 里了。之后再修改代码，也只需重复“一键同步”即可，文档自动更新，再也不用手动维护。



### 方案：先定义所有接口骨架，一次性同步，再逐个实现

1. **在 Controller 中把该模块的所有接口方法签名写好**（包括路径、方法、参数、返回值），方法体可以暂时空着或抛异常。

```java
@RestController
@RequestMapping("/auth")
public class AuthController {
    @PostMapping("/register")
    public Result<UserVO> register(@RequestBody RegisterRequest req) {
        throw new UnsupportedOperationException("Not implemented yet");
    }
    
    @PostMapping("/login")
    public Result<LoginResponse> login(@RequestBody LoginRequest req) {
        throw new UnsupportedOperationException("Not implemented yet");
    }
    
    // 其他接口...
}
```

1. **一次性同步到 Apifox**（在 Controller 类上右键 → Upload to Apifox）。此时 Apifox 中会出现该模块的所有接口定义。
2. **逐个实现 Service 和 Mapper**，并修改 Controller 方法体调用真正的 Service。期间不需要再同步，因为接口定义没有变化。
3. **如果某个接口需要修改定义**（比如增加一个参数），修改后单独同步该接口（Apifox 插件支持增量同步）。