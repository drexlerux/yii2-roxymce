# RoxyMce - Beautiful File manager for Tinymce
This allow to integrate [TinyMce](https://github.com/tinymce/tinymce) 4 with [Roxy Fileman](http://roxyfileman.com)

User story
---
I'm try to find a good file manager for tinymce for a long time.  
elFinder is good, but too much function and it's not my style. MoxieManager maybe best with tinymce, but it's too much for me.  
One day, I saw roxyman, immediately, I know it is all I need.  
Install
---
Preferred way to install this extension through [composer](http://getcomposer.org)  
Either run
~~~
composer require drexlerux/yii2-roxymce "*"
~~~
Or add to `require` section of `composer.json` then run `composer update`
~~~
"drexlerux/yii2-roxymce" : "*" 
~~~
Configure
---
Just add to `config/web.php`
### Simple config
~~~
[php]
	'modules'    => [
		'roxymce'  => [
			'class' => '\drexlerux\roxymce\Module',
		]
	]
~~~
### Advanced config
~~~
[php]
	'modules'    => [
		'roxymce'  => [
			'class' => '\drexlerux\roxymce\Module',
			'config'=> [
			//all below is not required
				'FILES_ROOT'           => 'uploads/image', //The root directory of roxymce's resource, where can be uploaded to. if not existed, Roxy will auto create
				'DEFAULTVIEW'          => 'list', //default view when you call roxymce (thumb/list)
				'THUMBS_VIEW_WIDTH'    => '100', //default width of thumbs when thumb view activated
				'THUMBS_VIEW_HEIGHT'   => '100', //default height of thumbs when thumb view activated
				'MAX_IMAGE_WIDTH'      => '1000', //default maximum width of image allowed to upload
				'MAX_IMAGE_HEIGHT'     => '1000', //default maximum height of image allowed to upload
				'FORBIDDEN_UPLOADS'    => 'zip js jsp jsb mhtml mht xhtml xht php phtml php3 php4 php5 phps shtml jhtml pl sh py cgi exe application gadget hta cpl msc jar vb jse ws wsf wsc wsh ps1 ps2 psc1 psc2 msh msh1 msh2 inf reg scf msp scr dll msi vbs bat com pif cmd vxd cpl htpasswd htaccess', //default forbidden upload files extension
				'ALLOWED_UPLOADS'      => 'jpeg jpg png gif mov mp3 mp4 avi wmv flv mpeg', //default allowed upload files extension
				'FILEPERMISSIONS'      => '0644', //default file permissions
				'DIRPERMISSIONS'       => '0755', //default folder permissions
				'LANG'                 => 'en', //fix language interface. if NOT SET, language interface will auto follow Yii::$app->language
				'DATEFORMAT'           => 'dd/MM/yyyy HH:mm', //default datetime format
				'OPEN_LAST_DIR'        => 'yes', //default roxymce will open last dir where you leave
			]
		],
	],
~~~
Usage
---
In your view file, call roxymce widget
### Include ActiveRecord Model
~~~
[php]
//example in action create
$model = new Post(); 
//example in action update
$model = Post::findOne(['id' => 1]); 
echo \drexlerux\roxymce\widgets\RoxyMceWidget::widget([
	'model'       => $model, //your Model, REQUIRED
	'attribute'   => 'content', //attribute name of your model, REQUIRED if using 'model' section
	'name'        => 'Post[content]', //default name of textarea which will be auto generated, NOT REQUIRED if using 'model' section
	'value'       => isset($_POST['Post']['content']) ? $_POST['Post']['content'] : $model->content, //default value of current textarea, NOT REQUIRED
	'action'      => Url::to(['roxymce/default']), //default roxymce action route, NOT REQUIRED
	'options'     => [//TinyMce options, NOT REQUIRED, see https://www.tinymce.com/docs/
		'title' => 'RoxyMCE',//title of roxymce dialog, NOT REQUIRED
	],
	'htmlOptions' => [],//html options of this widget, NOT REQUIRED
]);
~~~
### Sample HTML without ActiveRecord Model
~~~
[php]
echo \drexlerux\roxymce\widgets\RoxyMceWidget::widget([
	'name'        => 'content', //default name of textarea which will be auto generated, REQUIRED if not using 'model' section
	'value'       => isset($_POST['content']) ? $_POST['content'] : '', //default value of current textarea, NOT REQUIRED
	'action'      => Url::to(['roxymce/default']), //default roxymce action route, NOT REQUIRED
	'options'     => [//TinyMce options, NOT REQUIRED, see https://www.tinymce.com/docs/
		'title' => 'RoxyMCE',//title of roxymce dialog, NOT REQUIRED
	],
	'htmlOptions' => [],//html options of this widget, NOT REQUIRED
]);
~~~
### Sample HTML Input Demo
~~~
[php]

use yii\bootstrap\Modal;
Modal::begin([
    'header' => '<h2>Hello world</h2>',
    'size' => Modal::SIZE_LARGE,
    'id' => "modal"
    //'toggleButton' => ['label' => 'click me'],
]);
echo "<div id='modalContent'><iframe width='100%' height='470px' src='".Url::to(['roxymce/default', 'type' => 'image', 'input' => 'filepath','modal'=>'modal','tabindex'=>-1,])."'></iframe></div>";

Modal::end();
[html]
<input type="text" id="filepath"/>
<a href="#" onclick="return demoPopup();">Choose Picture</a>
[javascript]
<script type="text/javascript">
    function demoPopup() {
        $('#modal').modal('show');
        return false;
    }
</script>
~~~
Screenshot & Demo
---
### Demo
Please referrence to [RoxyFileMan demo](http://www.roxyfileman.com/demo) and scroll down to TinyMce section
### Thumb view
![thumbview](http://i.imgur.com/mEascq0.png)
### List view
![listview](http://i.imgur.com/IkA92kK.png)
### Upload view
![upload](http://i.imgur.com/9zvpFTM.png)

Resource
---

 * [TinyMce](http://tinymce.com)
 * [RoxyFileMan](http://roxyfileman.com)
 * [Project root](https://github.com/drexlerux/yii2-roxymce)

Bugs & Issues
---
Found some bugs? Just [create an issue](https://github.com/drexlerux/yii2-roxymce/issues/new) or [fork it](https://github.com/drexlerux/yii2-roxymce) and send pull request
