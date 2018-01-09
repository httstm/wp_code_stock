# リンクがついている親カテゴリ込みリストが必要な場合
テンプレートタグ/get the category list
https://wpdocs.osdn.jp/%E3%83%86%E3%83%B3%E3%83%97%E3%83%AC%E3%83%BC%E3%83%88%E3%82%BF%E3%82%B0/get_the_category_list
<?php get_the_category_list( $separator, $parents, $post_id ); ?>

※ もっと強力なリスト取得用関数として wp_list_categories() があります。

# 今の投稿or Archiveと無関係に、カテゴリ情報全部を出したい場合
get_categories();

https://wpdocs.osdn.jp/%E9%96%A2%E6%95%B0%E3%83%AA%E3%83%95%E3%82%A1%E3%83%AC%E3%83%B3%E3%82%B9/get_categories#.E3.83.89.E3.83.AD.E3.83.83.E3.83.97.E3.83.80.E3.82.A6.E3.83.B3.E3.83.9C.E3.83.83.E3.82.AF.E3.82.B9

# 今のカテゴリ名を表示する
single_cat_title()

# カテゴリが複数ある場合は、一つだけ表示する
$categories = get_the_category();
$separator = ' ';
$output = '';
if ( $categories ) {
	foreach( $categories as $category ) {
		$output .= '<a href="' . get_category_link( $category->term_id ) . '" title="' 
			. esc_attr( sprintf( __( "View all posts in %s" ), $category->name ) ) 
			. '">' . $category->cat_name . '</a>' . $separator;
	}
echo trim( $output, $separator );
}

https://wpdocs.osdn.jp/%E3%83%86%E3%83%B3%E3%83%97%E3%83%AC%E3%83%BC%E3%83%88%E3%82%BF%E3%82%B0/get_the_category

# 最上位カテゴリのterm_idを取得する。
## header版
$ch_cat = get_category($cat_id);
$ch_cat_parent = $ch_cat->parent;
$tmp_cat_parent = $ch_cat_parent;
while($tmp_cat_parent !== 0){
    $arr_category = get_category($ch_cat_parent);
    $tmp_cat_parent = $arr_category->parent;
    if($tmp_cat_parent !== 0) $ch_cat_parent = $tmp_cat_parent;
}
echo '<br>'.$ch_cat_parent;
## archive.php版
// 最上位のカテゴリのディスクリプションを取得する 
$ch_cat = get_the_category();
var_dump($ch_cat);
$ch_cat_parent = $ch_cat[0]->category_parent;

$tmp_cat_parent = $ch_cat_parent;
while($tmp_cat_parent !== 0){
	$arr_category = get_category($ch_cat_parent);
	$tmp_cat_parent = $arr_category->parent;
	if($tmp_cat_parent !== 0) $ch_cat_parent = $tmp_cat_parent;
}
$cat_description = category_description($ch_cat_parent);


