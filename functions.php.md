# CSSをfunctions.phpで読み込む

```
function custom_style_loader()
{
    wp_register_style( 'custom-style', get_template_directory_uri() . '/pc.css', array(), '20171229', 'all' );
    wp_register_style( 'custom-style', get_template_directory_uri() . '/smart.css', array(), '20171229', 'all' );
    wp_register_style( 'custom-style', get_template_directory_uri() . '/print.css', array(), '20171229', 'print' );
 
    // 登録したCSSをインクルード待ちリスト（キュー）に追加する
    wp_enqueue_style( 'custom-style' );
}
add_action( 'wp_enqueue_scripts', 'custom_style_loader' );
```

# 「テーマカスタマイズ」のカスタマイズ

```
// テーマカスタマイザーで、descriptionを設定する
function my_theme_customize_register( $wp_customize ) {

  // セクション:サイト基本情報に追加
  
   // originText
   // セッティング
  $wp_customize->add_setting( 'my_theme_options[originText]', array(
    'default'   => '',
    'type'      => 'option',
    'transport' => 'postMessage',
  ));
  
  // コントロール
  $wp_customize->add_control( 'my_theme_options_origin_text', array(
    'settings'  => 'my_theme_options[originText]',
    'label'     => 'ディスクリプション',
    'section'   => 'title_tagline',
    'type'      => 'text',
  ));
  
   // originKeyword
   // セッティング
  $wp_customize->add_setting( 'my_theme_options[originkeyword]', array(
    'default'   => '',
    'type'      => 'option',
    'transport' => 'postMessage',
  ));
  
  // コントロール
  $wp_customize->add_control( 'my_theme_options_origin_keyword', array(
    'settings'  => 'my_theme_options[originkeyword]',
    'label'     => 'キーワード',
    'section'   => 'title_tagline',
    'type'      => 'text',
  ));
  
   // originTitie
   // セッティング
  $wp_customize->add_setting( 'my_theme_options[originTitle]', array(
    'default'   => '',
    'type'      => 'option',
    'transport' => 'postMessage',
  ));
  
  // コントロール
  $wp_customize->add_control( 'my_theme_options_origin_title', array(
    'settings'  => 'my_theme_options[originTitle]',
    'label'     => 'タイトル',
    'section'   => 'title_tagline',
    'type'      => 'text',
  ));
}
add_action( 'customize_register', 'my_theme_customize_register' );
```

# サムネイルを有効にする

```
// サムネイルを有効にする
add_theme_support( 'post-thumbnails' ); 
```

# ウィジェットを有効にする

```
// ウィジェットを有効にする
$args = array(
'name'=>('サイドバー'),
'id'=>'sidebar-widget',
'description'=>'サイドバー用のウィジェットエリアです',
'before_widget'=>'',
'after_widget'=>''
);
register_sidebar($args);
```

# the_excerptのカスタマイズ

```
// the_excerpt()の後ろの...を無くします
function new_excerpt_more($more) {
	return '';
}
add_filter('excerpt_more', 'new_excerpt_more');
```

# カテゴリdescriptionにhtmlを利用できるようにする

```
// カテゴリdescriptionに、htmlを利用できるようにします
remove_filter( 'pre_term_description', 'wp_filter_kses' );
```

# カテゴリテンプレートを親のテンプレートからとってくれる

```
// 子カテゴリーのテンプレートを親カテゴリーのテンプレートからとってくれる
add_filter( 'category_template', 'my_category_template' );

function my_category_template( $template ) {
	$category = get_queried_object();
	if ( $category->parent != 0 &&
		( $template == "" || strpos( $template, "category.php" ) !== false ) ) {
		$templates = array();
		while ( $category->parent ) {
			$category = get_category( $category->parent );
			if ( !isset( $category->slug ) ) break;
			$templates[] = "category-{$category->slug}.php";
			$templates[] = "category-{$category->term_id}.php";
		}
		$templates[] = "category.php";
		$template = locate_template( $templates );
	}
	return $template;
}
```
