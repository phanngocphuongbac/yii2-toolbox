# yii2-toolbox
Yii2-Toolbox is a collection of useful helpers, widgets etc. extending the basic functionality of Yii2


## Installation
The preferred way to install this extension is through [composer](http://getcomposer.org/download/).

	"asinfotrack/yii2-toolbox": "dev-master"


## Contents


### Components

###### PdfResponseFormatter
Additional response formatter for handling PDF-requests. You need to add the formatter to the config like this:
```php
'response' => [
	// ...
	'formatters'=>[
		'pdf'=>'asinfotrack\yii2\toolbox\components\PdfResponseFormatter',
		'pdf_download'=>[
			'class'=>'asinfotrack\yii2\toolbox\components\PdfResponseFormatter', 
			'forceDownload'=>true,
		],
	],
	// ...
],
```

After that you can use it to output PDFs via actions easily:

```php
public function actionPdf()
{
	//create pdf with some library (eg FPDF)
	$pdf = new FPDF();
	// ...

	$response = Yii::$app->response;
	$response->data = $pdf->Output();
	$response->format = 'pdf';
}
```


### Widgets

###### Panel
Renders a Bootstrap-Panel. You can either set its body via attribute or between `begin()` and `end()`.
The attributes `heading`, `body` and `footer` support setting via string or via Closure returning a string.
Exemplary usage:

```php
<?php Panel::begin([
	'heading'=>Html::tag('h3', 'Welcome!'),
	'footer'=>function() {
		return Yii::$app->formatter->asDatetime(time());
	},
]); ?>
 	
 	<p>Hello world! This is a simple panel with a heading.</p>
 	 	
<?php Penel::end(); ?>
```

###### Button
The button-widget extends the one provided by yii2. It adds functionality to specify an icon.
The Icons depend on font-awesome and hence require the yii2-extension `rmrevin/yii2-fontawesome`


### Helpers

###### Html
Extends the Html-helper of Yii2 with additional functionality

###### ServerConfig
Provides functionality to fetch the most important server vars and to check if certain
extensions are loaded

###### Timestamp
This helper is responsible for common tasks associated with UNIX-Timestamps
