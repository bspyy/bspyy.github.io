文章id不连续是因为wordpress会自动保存编辑记录，也就是为这个重新生成一条数据，因此解决方法也很简单

第一步：取消自动保存和修订版本。在我们当前使用主题的 **functions.php** 文件加入如下代码即可：

```php
/* 取消自动保存和修订版本 */
remove_action('pre_post_update','wp_save_post_revision');
add_action('wp_print_scripts','disable_autosave');
function disable_autosave() {
    wp_deregister_script('autosave');
}

```

添加以上代码之后，在后台编辑已有文章时数据库并不会新增一条数据，但是在创建新文章时还是会创建一条post_status为auto-draft的数据，如果不保存，这条数据依然会存在数据库中，但是后台不会显示这条数据，实际上这个数据就是废弃的。

第二步：在创建新文章的时候先不创建数据，先查找数据库中是否有状态为auto-draft的数据，有的话就对这条数据进行编辑，否则使用默认方式

在打开**wp-admin/post-new.php**文件

在最下方找到下方代码
```php
$post = get_default_post_to_edit( $post_type, true ); 
$post_ID = $post->ID;
```

**get_default_post_to_edit( $post_type, true )** 方法会创建一条post_status为auto-draft的数据并返回，新增文章实际上是在对这条新建数据进行编辑

将上方代码修改为下方代码即可

```php
/* 查找当前用户是否存在post_status为auto-draft的数据，获取该数据，如果不存在，使用系统方式创建一条数据 */
$current_user_id = get_current_user_id();//当前登录用户ID
$query = "select * from {$wpdb->posts} where post_status = 'auto-draft' and post_author = {$current_user_id} order by id asc limit 1;";
$result = $wpdb->get_row($query);
if($result){
	$post = get_post($result);
}else{
	$post = get_default_post_to_edit( $post_type, true );
}
$post_ID = $post->ID;

```

参考链接

wordpress禁止自动草稿及历史版本保持文章ID连续的方法：www.cnblogs.com/wpjamer/articles/6575432.html

WordPress文章ID不连续的解决方法：down.chinaz.com/try/201203/1800_1.htm
