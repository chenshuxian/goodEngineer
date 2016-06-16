# ESLint 使用说明
ESLint 配置方法:
----
>1. Configuration Comment: 直接嵌入每一支 JS 中。  
2. Configuration Files: 经由一份文件的配置，文件格式可为 JavaScript,JSON,YAML。如果用过 .eslintrc or package.json 进行配置，系统就会自动检测这两个文件，文件的优先顺序如下:  

>>1. eslintrc.js  
2. eslintrc.yaml
3. eslintrc.yml
4. eslintrc.json
5. eslintrc  

ESLint 配置的主要内容
----
>1. Environments: 定义脚本运行环境，配置此項主因是因为每个不同的运行环境都会有预先定义的不同的 glolbal variables。  
>2. Globals: 配置脚本运行过程中附件的全局变量。  
>3. Rules: 项目中，需要配置的代码规则，并可以指定每条规则的警告级别。

ESLint 正式设定
----
1.Specifying language Options  

>> .eslintrc 预设支持 ECMAScript5，如想改为支持ECMAScript2016 可以在 ecmaFeatures 属性进行设置，当我们在环境配置时设定 es6: true，我们就已拥有 ECMAScript2015 的新特性了，所以只要在加个模块就可了。  
```
>> {    
   "ecmaFeatures":{
       modules:true
   }
}
```   

2.解析器的配置 (Specifying Parser)  
预设为 Espress 解析器，可以修改，但需要满足一些条件，在此我们就不说了。  
3.环境设定  

>> ESLint 提供了许多，我们可以依我们项目进行配置。  
举个例子:  
```
>> {    
  "env":{
       browser: true,
       node: true,
       es6: true    
  }
}
```  

4.指定额外全局变量 (Specifying Globals)  

>> no-undef 規則在我們使用沒有在同一文件中定義的變量的时候会报错，当我们使用全局变量的时候，我们必须对额外的全局变量进行配置，避免 no-undef 误会。我们可已经由以下例子进行设定:  

```
{
  globals:{
    var:  true        
    var2: false          
  }
}  
```  

5.引入插件 (Specifying Plugins)  

>> 插入第三方插件前，需先通过 npm 安装所需插件。通过 plugins 键来指定插件，插件前缀可省略，如例子:  

```
{
  plugins:{
    plugin1,
    eslint-plugin-plugin2
  }
}
```  

6.配置 Rules (Configuring Rules)  

>> **重要的东西往往放在最后，也就是 Rules 配置文件的核心部分，在配置时除了级别 0 (off)、1 (warning)、2 (error)外，还可以指定其他选项，如例子:  

```
{
  rules:{
    eqeqeq: 0,
    curly: 2,
    quotes: {2,"double"}      
  }
}
```  

如果一条 rule 是经由 plugins 引入的，那配置 id 前面要加 plugin 名和 "/"，如例子:  

```
{
  plugins:{
    plugin1
  },
  rules:{
    plugin1/test1: 2
  }
}
**注意在进行制定 plugin 中的 rules 时，我们需要把 plugin 前缀去除。
**所有的 rules ， default value: 2。
```  

7.配置文件扩展 (Extending Configuration Files)  

>> 如果想扩展其他配置文件，如例子:  

```
{
  extends: [
    "./xxx/xxx/.eslintrc",
    // Override eslintrc
    "./xxx/xxx/.eslintrc2",
    // Override eslintrc2
    "./xxx/xxx/.eslintrc3",
    rules: {
      // 此处会覆写父类中相同的 rule
      eqeqeq: 1
    }
}
** extends 可引用 github 共享配置包，首先要通过 npm 安装配置包文件，引用时前缀也可去除。
```  

8.制定 ESLint 忽略检测文件或路径  

>> 可通过生成一个 .eslintignore 文件来设定，设定中每一行代码代表一忽略的路径。  
ESLint 运行前会先查找当前文件中的 .eslintignore ，注意一个文件中只能有一个 .eslintignore 文件。
