# Srping MVC之参数类型转换方式
spring mvc中类型转换的方式有：PropertyEditor、ConversionService
==注：如果有自定义PropertyEditor，会优先使用PropertyEditor，否则就用默认的ConversionService==
### PropertyEditor
spring 3.0之前使用方式，通过扩展j2se的PropertyEditor属性编辑器。
==注：PropertyEditor方式，每次解析一个参数都会注册自定义的属性编辑器，是个缺点==
#### PropertyEditor和PropertyEditorSupport
java自带的属性编辑器，主要用来将String类型转为java对象类型，PropertyEditorSupport继承PropertyEditor

#### PropertyEditorRegistry
spring中注册属性编辑器的接口

#### 向Spring注册自定义属性编辑器
1、@InitBinder
Controller级别的自定义属性编辑器，示例：

```
@InitBinder
 public void initBinder(PropertyEditorRegistry registry) { 
    registry.registerCustomEditor(Date.class, new DemoDateEditor(new SimpleDateFormat("yyyy-HH-dd"), true)); 
}
```
2、xml配置WebBindingInitializer
全局的自定义属性编辑器，示例：


```
<bean class="org.springframework.web.servlet.mvc.method.annotation.RequestMappingHandlerAdapter">

        <property name="webBindingInitializer">
            <bean
                    class="org.springframework.web.bind.support.ConfigurableWebBindingInitializer">
                <property name="propertyEditorRegistrars">
                    <array>
                        <bean
                                class="com.duotin.controller.handler.CustomPropertyEditorRegistrar"/>
                    </array>
                </property>
            </bean>
        </property>
		
    </bean>

```

==注：同类型局部会覆盖全局==

### ConversionService

spring 3.0之后，可以使用ConversionService方式
1、xml配置ConversionService，示例：


```
<bean id="conversionService"
            class="org.springframework.format.support.FormattingConversionServiceFactoryBean">
        <property name="converters">
            <set>
                <bean class="org.example.MyConverter"/>
            </set>
        </property>
        <property name="formatters">
            <set>
                <bean class="org.example.MyFormatter"/>
                <bean class="org.example.MyAnnotationFormatterFactory"/>
            </set>
        </property>
        <property name="formatterRegistrars">
            <set>
                <bean class="org.example.MyFormatterRegistrar"/>
            </set>
        </property>
    </bean>

```

