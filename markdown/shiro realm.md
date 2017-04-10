## shiro realm##

自定义realm常用到三个方法：

`doGetAuthenticationInfo`

这个方法在登陆的时候，判断用户名是否正确时候执行，通过用户名查出基本信息

`assertCredentialsMatch`

再通过这个方法判断密码是否一致

`doGetAuthorizationInfo`

这个方法，在判断权限`isPermitted`或者判断角色`hasRoles`的时候才会调用



​																--顾晨波

