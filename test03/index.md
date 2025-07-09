# Test03


<!--more-->

## 1

### 11

11 test

> 近期很是猖狂哈，我是指垃圾灌水邮箱，但是引入邮箱验证机制又太麻烦而且拖慢博客的速度（~~绝对不是因为我不会~~）。所以我就想着从底层出发，拒绝垃圾邮箱通过评论。如果有注意或者有收到，那么大部分垃圾邮箱格式都是 `一串英文@qq.com` 那么我们就可以增加正则过滤，去除他们，虽然也有英文的qq邮箱，但是秉持宁可错杀，不可放过的原则!！

**!!! 操作有一定风险** :&(蛆音娘_害怕)  :$(2233娘_郁闷) 

> 未来声明：本文除文字描述外，code部分均由deepseek-v3实现

## 一种方法

首先我们找到验证邮箱地址合法性的位置，也很简单哈，只需要在typecho博客源码全局搜索 `邮箱地址不合法` 哈哈哈

最终位置在 `<typecho>/var/Widget/Feedback.php` 180行左右

```php
 		$validator = new Validate();
        $validator->addRule('author', 'required', _t('必须填写用户名'));
        $validator->addRule('author', 'xssCheck', _t('请不要在用户名中使用特殊字符'));
        $validator->addRule('author', [$this, 'requireUserLogin'], _t('您所使用的用户名已经被注册,请登录后再次提交'));
        $validator->addRule('author', 'maxLength', _t('用户名最多包含150个字符'), 150);

        if ($this->options->commentsRequireMail && !$this->user->hasLogin()) {
            $validator->addRule('mail', 'required', _t('必须填写电子邮箱地址'));
        }

        $validator->addRule('mail', 'strictEmail', _t('邮箱地址不合法喵~'));
        $validator->addRule('mail', 'maxLength', _t('电子邮箱最多包含150个字符'), 150);
```

其中 `Validate()` 里就隐藏我们的规则，来到 ``<typecho>/var/Typecho/Validate.php`，找到`mail`

可以看到大约在97行，使用了php标准的过滤规则

```php
public static function email(string $str): bool

    {

        $email = filter_var($str, FILTER_SANITIZE_EMAIL);

        return !!filter_var($str, FILTER_VALIDATE_EMAIL) && ($email === $str);

    }
```

只需要增加对英文qq邮箱前缀的过滤，与ai友好交流后

```php
public static function email(string $str): bool

    {

        // 1. 清理邮箱字符串
	    $email = filter_var($str, FILTER_SANITIZE_EMAIL);
	    
	    // 2. 验证邮箱格式并检查清理前后是否一致
	    $isValid = !!filter_var($str, FILTER_VALIDATE_EMAIL) && ($email === $str);
	    
	    // 3. 自定义规则：如果是QQ邮箱，前缀必须为纯数字
	    if ($isValid && preg_match('/@qq\.com$/i', $str)) {
	        $isValid = preg_match('/^\d+@qq\.com$/i', $str);
	    }
	    
	    return $isValid;

    }
```


保存后测试，即可过滤垃圾邮箱。但是这样写改变了原有的typecho代码的统一性，虽然熊猫大大也已经停更了。

## 稍好的一种方法

以下通过**注册自定义验证器**

-1. 首先在 `<typecho>/var/Typecho/Validate.php` 同级目录下新建 `MyValidate.php` 并写入如下内容

```php
<?php

namespace Typecho;

use Typecho\Validate;

class MyValidate extends Validate
{
    /**
     * RFC 5322 严格邮箱验证
     */
    public static function strictEmail($str)
    {
        // $email = filter_var($str, FILTER_SANITIZE_EMAIL);
        // return !!filter_var($str, FILTER_VALIDATE_EMAIL) && ($email === $str);
        // 1. 清理邮箱字符串
        $email = filter_var($str, FILTER_SANITIZE_EMAIL);
        
        // 2. 验证邮箱格式并检查清理前后是否一致
        $isValid = !!filter_var($str, FILTER_VALIDATE_EMAIL) && ($email === $str);
        
        // 3. 自定义规则：如果是QQ邮箱，前缀必须为纯数字
        if ($isValid && preg_match('/@qq\.com$/i', $str)) {
            $isValid = preg_match('/^\d+@qq\.com$/i', $str);
        }
        
        return $isValid;
        
    }
}
```

 -2. 回到 `<typecho>/var/Widget/Feedback.php` 处做如下修改

```php
// 新增
use Typecho\MyValidate;
// 约187行
// $validator = new Validate();
    $validator = new MyValidate();
    ...
    // $validator->addRule('mail', 'email', _t('邮箱地址不合法喵~'));
    $validator->addRule('mail', 'strictEmail', _t('邮箱地址不合法喵~'));
```

这样修改能够实现与第一种方法相同的效果，就这样吧，希望能消停一会！

自我验证了21次哈哈哈

![](https://static.moontung.top/2024/202503021807743.webp)
